# WebLogic con Docker

- [WebLogic con Docker](#weblogic-con-docker)
	- [Descripción](#descripción)
	- [Instalación y uso](#instalación-y-uso)

## Descripción

Montaje de imagen de docker que contiene un servidor weblogic

## Instalación y uso

*Prerequisitos:*

- Docker
- Usuario registrado en Oracle

*Herramientas:*

- IDE de su preferencia, recomendado: **vscode**
- Para usuarios windows: Docker Desktop, WSL

*Inicialización:*

- Clonar repositorio

```bash
#Utilizando github cli
gh repo clone Joredjs/docker-weblogic

#Con git a través de https
git clone https://github.com/Joredjs/docker-weblogic.git
```

- Loguearse en docker al container registry con la cuenta de Oracle

```bash
docker login container-registry.oracle.com
```

- Ir a [container-registry](https://container-registry.oracle.com/) iniciar sesión, seleccionar el contenedor ***middleware***, seleccionar weblogic, clic en continuar, aceptar los términos y condiciones.
- *(Opcional)* Modificar el archivo *app/domain.properties* con las credenciales deseadas.
- Descargar la imagen weblogic de la versión deseada. (Se usará como ejemplo el tag 12.2.1.3-221121)

```bash
#12.2.1.3-221121 es el tag a utlizar
#Cambiarlo por la version (tag) deseada
docker pull container-registry.oracle.com/middleware/weblogic:12.2.1.3-221121
```

- Ejecutar el contenedor

```bash
#Debe estar ubicado en la carpeta raíz del repositorio
#si la ruta es distinta, modificar *"$(pwd)"* por la ruta absoluta en la máquina local
#La configuración de puertos remotos y ruta de montaje en el contenedor debe quedar como está en el script
docker container run -d -p 7000:7001 -p 9001:9002 -it --name wlnode01 -v /"$(pwd)"/app/://u01/oracle/properties container-registry.oracle.com/middleware/weblogic:12.2.1.3-221121
```
