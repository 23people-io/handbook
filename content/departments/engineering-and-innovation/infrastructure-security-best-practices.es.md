---
title: "Buenas prácticas de Infraestructura y Seguridad"
date: 2022-03-21T00:00:00-03:00
lastmod: 2022-03-21T00:00:00-03:00
weight: 3
draft: false
keywords: ["buenas", "practicas", "infraestructura", "seguridad"]
mantained_by:
    - matias.pizarro
    - anibal.cordero
---

En este artículo vamos a ver cómo configurar un servidor desde cero, utilizando buenas prácticas de infraestructura y seguridad.

En la presente documentación se mostrarán los pasos seguidos para realizar la configuración del snapshot [`mean-snapshot-template-23p-v1.1.22-03-2022`](https://cloud.digitalocean.com/droplets/291642648/snapshots?i=61ca4c) basado en la distribución **Rocky Linux 8.5**. En éste se configuró lo siguiente:

-   Se creó el usuario `jedi` con privilegios administrativos
-   Se deshabilitó el acceso por SSH al usuario `root`
-   Se configuró un firewall con los puertos HTTP abiertos
-   Se configuraron las actualizaciones automáticas
-   Se instaló lo siguiente:
    -   Vim
    -   Nginx
    -   Node.js (versión LTS)
    -   MongoDB (versión 5.0)

> Nota: debido a que el snapshot se configuró utilizando la distribución **Rocky Linux 8.5**, será necesario adaptar los comandos en caso de querer configurar una distribución distinta (aunque normalmente sólo cambia el gestor de paquetes).

# Actualización inicial

Antes de realizar una acción con el gestor de paquetes del sistema operativo, siempre es recomendado descargar las últimas actualizaciones disponibles. De esta manera, prevenimos las actualizaciones parciales, las cuales pueden generar conflictos de versiones y otros problemas _raros_.

Para hacer esto, se debe ejecutar el siguiente comando:

```bash
dnf update -y
```

# Crear un usuario administrador

A pesar de que podríamos utilizar el usuario `root` para hacer tareas de administración, por temas de seguridad es recomendado crear un usuario que tenga la menor cantidad de privilegios para cumplir su objetivo.

```bash
useradd -m -s /bin/bash -G wheel jedi
passwd jedi
```

Con los comandos anteriores, se creó el usuario `jedi`, el cual fue agregado al grupo `wheel` con el fin de que pueda utilizar `sudo` para ejecutar comandos con privilegios elevados.

> Nota: una vez creado, se recomienda utilizar el nuevo usuario en vez de `root` para ejecutar los comandos posteriores.

# Deshabilitar login por SSH al usuario root

```bash
sudo sed -i 's/^PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
```

# Configurar el firewall

```bash
sudo dnf install -y firewalld
sudo systemctl enable --now firewalld
sudo firewall-cmd --permanent --add-service=http
sudo firewall-cmd --reload
```

# Instalar Vim

¿Por qué no? Ejecutar el siguiente comando:

```bash
sudo dnf install -y vim
```

# Habilitar actualizaciones automáticas

```bash
sudo dnf install -y dnf-automatic
sudo sed -i 's/^upgrade_type = default/upgrade_type = security/' /etc/dnf/automatic.conf
sudo sed -i 's/^apply_updates = no/apply_updates = yes/' /etc/dnf/automatic.conf
sudo sed -i 's/^emit_via = .+/apply_updates = yes/' /etc/dnf/automatic.conf
sudo systemctl enable --now dnf-automatic.timer
```

# Instalar y configurar Nginx

```bash
sudo dnf install -y nginx
mkdir -p ~/your-project/{dev,demo,test,prod}/{frontend,backend}
```

Una vez instalado Nginx y creadas las carpetas para nuestro proyecto, debemos editar el archivo `/etc/nginx/nginx.conf` y agregar dentro del bloque `http`, bloques similares al siguiente:

=======

````text
=======

>>>>>>> config
```nginx
# Esto debe ir debajo de la regla `types_hash_max_size`
server_tokens       off;
server_names_hash_bucket_size 64;

# Esto debe ir al final del block `http`
=======
```text
>>>>>>> Cambios
server {
  listen       80;
  listen       [::]:80;
  server_name  your-project-front-prod.23people.dev;
  root         /usr/share/nginx/html;

  # Load configuration files for the default server block.
  include /etc/nginx/default.d/*.conf;

  add_header X-Frame-Options SAMEORIGIN;
  add_header X-Content-Type-Options nosniff;

  location / {
      proxy_pass http://127.0.0.1:3000;
      proxy_set_header Host your-project-front-prod.23people.dev;
      proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header X-Forwarded-Proto $scheme;
      proxy_set_header X-Forwarded-Port $server_port;
  }
}
````

Con el bloque anterior, se creará un proxy que redirigirá las peticiones que van a `your-project-front-prod.23people.dev` a `127.0.0.1:3000`.

> Tip: Normalmente, lo único que cambia en esta configuración es el dominio y el puerto al que redirige el proxy.

# Configurar SELinux para permitir conexiones remotas HTTP

```bash
sudo setsebool httpd_can_network_connect on -P
```

> Nota: esto es para evitar tener el siguiente error con el proxy de Nginx:
>
> ```text
> connect() to 127.0.0.1:5000 failed (13: Permission denied) while connecting to upstream
> ```

# Instalar Node.js

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
nvm install —-lts
nvm use —-lts
nvm alias default node
```

Una vez instalado, necesitamos configurar NPM para que nos permita acceder a las librerías privadas de 23people. Para esto, debemos agregar una variable de entorno que se utilizará por los proyectos al conectarse a NPM. Esto se puede realizar con el siguiente comando:

```bash
echo "export NPM_TOKEN=8dca72c7-cebc-43c6-8100-40f89515ed3b" >> ~/.bashrc
```

Este token posteriormente será utilizado por los proyectos a través del archivo `.npmrc`, el cual normalmente tendrá lo siguiente:

```shell
//registry.npmjs.org/:_authToken=${NPM_TOKEN}
```

# Instalar y configurar MongoDB

```bash
printf "[mongodb-org-5.0]\nname=MongoDB Repository\nbaseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/5.0/x86_64/\ngpgcheck=1\nenabled=1\ngpgkey=https://www.mongodb.org/static/pgp/server-5.0.asc" | sudo tee -a /etc/yum.repos.d/mongodb-org-5.0.repo
sudo dnf update -y
sudo dnf install -y mongodb-org
sudo systemctl start mongod # Para que inicie automáticamente al encender la máquina, utilizar enabled
```

> Nota: en este caso utilizamos la versión 5.0 de Mongo. Recomendamos en el futuro ver si existe una versión más reciente que sea ideal para su uso en producción.
