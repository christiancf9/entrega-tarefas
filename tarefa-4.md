# Tarefa 4

                                                      COMANDOS ÚTILES MySQL 
                                        
# EXPLICACIÓN
Trataremos de enseñar los comandos más utilizados, para MySQL

  
***
***
# ÍNDICE <a name="comandos_index"></a>
1. ⚡ [COMPROBAR ESTADO](#comandos_estado)
2. ⚡ [VER LAS BASES DE DATOS](#comandos_ver-bbdd)
3. ⚡ [SELECCIONAR UNA BBDD](#comandos_seleccion)
4. ⚡ [VER LAS TABLAS](#comandos_ver-tablas)
5. ⚡ [MOSTRAR INFORMACIÓN - TABLAS](#comandos_desc-tablas)
6. ⚡ [MOSTRAR VERSIÓN DE MYSQL](#comandos_version)
7. ⚡ [LIMPIAR PANTALLA - CLEAR](#comandos_clean)
***

## COMPROBAR ESTADO <a name="comandos_estado"></a>

Para comprobar el estado del proceso de MySQL en Ubuntu, escribiremos lo siguiente:

```console
christian@christian-VirtualBox:~$ systemctl status mysql.service
```
![SYSTEMCTL_REPASO](./imagenes/repaso_systemctl.png)
  > Podemos observar que el servicio `MySQL` se está ejecutando correctamente..
  > Systemctl no funciona con el usuario `root`. Eso si, nos pedirá obviamente la password..
  >
  > Si nos sigue sin funcionar, podemos usar el comando ``systemctl restart mysql.service``
  >
  > 🛡NOTA: No es lo mismo `RELOAD` que `RESTART`, el 1º recarga los archivos del sistema,
  > el otro "apaga" y vuelve a "encender" el SGBD.

## VER LAS BASES DE DATOS <a name="comandos_ver-bbdd"></a>

Con este sencillo comando, visualizaremos las bases de datos `BBDD` creadas en este SGBD.

```sql
SHOW DATABASES;
```
![SHOW_DATABASES](./imagenes/show_and_use-databases.png)
  > También podemos usar el siguiente comando: ``SHOW SCHEMAS;``.
  
## SELECCIONAR UNA BASE DE DATOS <a name="comandos_seleccion"></a>

Con este sencillo comando, seleccionaremos una BBDD para más adelante, mostrar sus respectivas tablas 👇

```sql
USE <BBDD_Ejemplo>;
```
![SHOW_DATABASES](./imagenes/use_naves-espaciales.png)
  > También podemos usar el siguiente comando: ``CONNECT Naves_Espaciales;``.
 
👁 [ÍNDICE](#comandos_index)

## VER LAS TABLAS <a name="comandos_ver-tablas"></a>

Sobre como visualizar las tablas..

```sql
SHOW TABLES;
```
![MOSTRAR_TABLAS](./imagenes/show_tables_2.png)
  > También podemos usar el comando ``SHOW TABLE STATUS;``, pero en este caso
  > nos mostrara un "output" propio, del motor de MySQL

## MOSTRAR INFORMACIÓN - TABLAS <a name="comandos_desc-tablas"></a>

```sql
DESC <Ejemplo-de-tabla>;
```
![MOSTRAR INFO - TABLA](./imagenes/desc_departamento.png)
  > La opción `DESC` también se conoce como la opción `DESCRIBE` (la cual detalla cualquier tabla que seleccionemos...).
  >
  > También podemos usar el comando ``SHOW COLUMNS FROM Departamento;``

👁 [ÍNDICE](#comandos_index)

## MOSTRAR VERSIÓN DE MYSQL <a name="comandos_version"></a>

```console
christian@christian-VirtualBox:~$ mysql --version
```
![MYSQL_VERSION](./imagenes/comandos_mysql-version.png)
  > Si usamos el comando ``apt-get update``, y volvemos a [instalar](https://gist.github.com/christiancf9/2d4452556ae7fbd1514f65af6360619b) el programa, tendremos actualizado `MySQL`
  
  > Opcionalmente podremos consultar la versión de MySQL**d** (Servidor ejecutable), para ello, escribiremos ``mysqld --version``
  
También dentro de **MySQL**, podremos realizar dicha consulta 👇

```sql
SELECT version();
```
![MYSQL_2 - VERSION](./imagenes/comandos_select-version.png)
  > O también podemos usar este comando -> ``select @@version;``
  >
  > 🛡NOTA: Solo para **MySQL**, en MariaDB sería ``SHOW VARIABLES LIKE ‘%version%’;``
  >
  > Y en `MySQL` *OR* `MariaDB` -> ``SELECT VERSION();``

## LIMPIAR PANTALLA - CLEAR <a name="comandos_clean"></a>

Y para terminar... Un comando súuuuper útil 😎, sería el siguiente..

Cuando nos situemos **dentro** de MySQL, realizaremos la siguiente combinación de teclas..

``CTRL`` + ``L``.
  > Supongo, "no estoy seguro", pero debería funcionar también en MariaDB..
  >
  > Es equivalente al ``CLEAR`` de Ubuntu o al ``CLS`` de Windows

Con esto, tendremos la pantalla de comandos limpita

👁 [ÍNDICE](#comandos_index)
