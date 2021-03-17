# <u>**Instalar Consul**</u>

1) Descargar la ultima version de Consul de su web oficial.
https://www.consul.io/downloads

2) Extraer y guardar su contenido en una carpeta de facil acceso.

3) Ejecutar CMD y ubicarse sobre la carpeta donde tiene el archivo **consul**

4) En el CMD ubicado dentro de la carpeta, ejecute el siguiente comando.

```
consul agent -server -bootstrap-expect=1 -data-dir=consul-data -ui
```

5) Si todo ha salido bien debe mostrarse al final **Consul agent running!**

![image-20210317111036816](C:\Users\PC-5CDO35C7T9\AppData\Roaming\Typora\typora-user-images\image-20210317111036816.png)

# **<u>Integracion con Spring Boot</u>**

**Requisitos:**

- Tener en las dependencias de sus microservicios (pon.xml) las siguientes dependencias:

  ```
          <dependency>
              <groupId>org.springframework.cloud</groupId>
              <artifactId>spring-cloud-starter-consul-discovery</artifactId>
          </dependency>
          
         <dependency>
              <groupId>org.springframework.boot</groupId>
              <artifactId>spring-boot-actuator</artifactId>
              <version>2.3.2.RELEASE</version>
          </dependency>
  ```

- En la App principal agregar

  ```
  @EnableDiscoveryClient
  ```

1) Configuracion **application.yml**

```
server:
  port: 9100 #A eleccion del desarrollado

spring:
  cloud:
    consul:
      host: 127.0.0.1 #Se ejecuta por defecto en consul pero puede ser modificada al momento de ejecutar el comando para iniciarlo.
      port: 8500 #Se ejecuta por defecto en consul pero puede ser modificada al momento de ejecutar el comando para iniciarlo.
      discovery:
        health-check-path: /actuator/health #Lo utiliza para conocer el estado de salud del microservicio.
        prefer-ip-address: true
        instanceId: ${spring.application.name}
  application:
    name: prueba-consultest #Nombre del microservicio
```

2) Con el consul en ejecucion, ejecutar el microservicio y dirigirse a:

```
http://localhost:8500/
```

Si todo ha se ejecutado correctamente  deberia mostrarse los microservicios que se encuentra ejecuntadose y conectado a consul

![image-20210317112434102](C:\Users\PC-5CDO35C7T9\AppData\Roaming\Typora\typora-user-images\image-20210317112434102.png)
