## CREAR CONTENEDOR
1. docker run -it --name mi_ubuntu -p 8080:80 ubuntu:22.04 /bin/bash
	- `-it` → modo interactivo
	- `--name` → nombre del contenedor
	- `-p 8080:80` → expone Apache (host → contenedor)
	- `ubuntu:22.04` → imagen base
	
2. apt update    / Para no instalar versiones antiguas (Pull en github)
3. apt-get install apache2 -y      / Instala el servidor web apache
4. exit

## Mostrar todos los contenedores
	docker ps -a
## Levantar contenedor
	docker start (nombre del contenedor)
## Comprobar estado del contenedor
	docker ps -a 
## Entrar al contenedor
	docker exec -it (nombre del contenedor) /bin/bash
	

```
docker exec -it (nombre del contenedor) /bin /bash
```





## INSTALAR OFUSCADO
```
npm init -y  
npm install javascript-obfuscator
```

## OFUSCAR
```
npx javascript-obfuscator app.js --output app.obf.js
```






## Crear DOCKERFILE

	FROM ubuntu:22.04
	ENV DEBIAN_FRONTEND=noninteractive
	
	# Instalar Apache
	
	RUN apt update && \
    apt install -y apache2 && \
    apt clean
    
     # Copiar tu sitio web
     COPY html/ /var/www/html/
     
     # Configurar ServerName (evita warning)
     RUN echo "ServerName localhost" >> /etc/apache2/apache2.conf
     
     # Exponer puerto 80
     EXPOSE 80
     
     # Ejecutar Apache en primer plano
     CMD ["apachectl", "-D", "FOREGROUND"]

## Construir contenedor
	docker build -t apache-ejercicio .



## Comando para ejecutar contenedor con DOCKERFILE
	docker run -d -p 8080:80 --name apache-test ejercicio2
	
	EXPLICACIÓN:
		-d -> Ejecutar en segundo plano
		-p 8080:80 -> mapping de puertos
		-name apache-test -> Nombre del Contenedor
		-ejercicio2 -> Nombre de la imagen que se construyo






como correr a un sevidor web o nginx, el que ya tengo en agenda

PREGUNTA EXAMEN - como poner el script javascript en el header sin que haya error
