# Guía del Proyecto  

## Introducción  

Este proyecto implementa un entorno de despliegue con Vagrant para simular un escenario con un proxy inverso a través de dos máquinas virtuales:  

- **proxy:** Es un servidor Nginx encargado de redirigir las solicitudes hacia la máquina _web1_.  
- **web1:** Contiene un servidor Nginx que ofrece una página HTML estática.  

## Estructura del Proyecto  

- **.vagrant/**  
  Carpeta donde Vagrant almacena el estado y la configuración de las máquinas virtuales.  

- **Vagrantfile**  
  Archivo de configuración que define la creación de dos máquinas virtuales:  
  - **proxy:** Tiene el hostname `www.example.test`, está configurada con una red pública y una privada (IP: `192.168.57.10`).  
  - **web1:** Usa el hostname `web1.example.test`, cuenta con una red privada (IP: `192.168.57.11`) y se le instala Nginx automáticamente.  

- **files/proxy/default**  
  Configuración de Nginx en la máquina _proxy_, estableciendo el proxy inverso hacia _web1_.  
  **Nota:** La directiva `proxy_pass` debe incluir el esquema (`http://`).  

- **files/web1/web1**  
  Archivo de configuración de Nginx en _web1_, definiendo el servidor que atiende en el puerto `8080`.  

- **files/web1/index.html**  
  Página HTML estática servida desde la máquina _web1_, ubicada en `/var/www/web1/html`.  

## Configuración y Despliegue  

### Vagrantfile  

Para iniciar el entorno, ejecuta el siguiente comando en la raíz del proyecto:  

```bash
vagrant up
```