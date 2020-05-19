# Tarefa 1

                                                       SENTENCIAS DDL
                                        
# DEFINICIÓN
Usando sentencias **``DDL``** para crear y manejar tablas

Un esquema es la colección de múltiples objetos de una BBDD, que son conocidos como objetos de un esquema.

Estos objetos tienen un acceso directo al esquema del propietario. Debajo una lista con la enumeración de objetos de un esquema 👇



  * Tabla     --> Para el almacenamiento de datos
  * Vista     --> Para proyectar datos en un formato deseado desde una o más tablas
  * Secuencia --> Para generar valores númericos
  * Índice    --> Para mejorar el rendimiento de las consultas en tablas.
  * Sinónimo  --> Nombre similar/alternativo de un objeto
  
Uno de los primero(s) pasos a la hora de crear una BBDD, es crear las tablas que almacenarán los datos de una organización. Independientemente del tamaño y complejidad de una base de datos, cada una de estas se compone de **tablas**.

***
# INDICE <a name="ddl_index"></a>
1. ⚡ [DDL - CREATE](#ddl_create)
2. ⚡ [DDL - ALTER](#ddl_alter)
3. ⚡ [DDL - DROP](#ddl_drop)
***
# CREATE <a name="ddl_create"></a>

La consula ``CREATE`` es usada para crear una base de datos u objetos, tales como tablas, vistas, almacenamientos procesados, etc.

### CREANDO UNA BBDD - [``CREATE DATABASE`` | ``CREATE SCHEMA``]

El ejemplo siguiente demuestra como la consulta ``CREATE`` puede ser usada para crear una base de datos.

```sql
CREATE DATABASE LibreriaDB [IF NOT EXISTS] <nombreBBDD>
                           [CHARACTER SET <nombreCharset>] 
                           [COLLATE <nombreCollate>];
```

Otro ejemplo

```sql
CREATE SCHEMA LibreriaDB [IF NOT EXISTS] <nombreBBDD>
                         [CHARACTER SET <nombreCharset>] 
                         [COLLATE <nombreCollate>];
```

NOTA: La diferencia es inexistente en MySQL, pero no en PostgreSQL, donde ``SCHEMA`` añade atributos de permiso. En la práctica se aconseja usar ``SCHEMA``

- `[IF NOT EXISTS]`: Este campo es opcional. Revisa si la BBDD que vayamos a crear exista (o no) en nuestro sistema gestor de base de datos...
- `CHARACTER SET`: Este campo es opcional. Establece un parámetro de conjunto de caracteres que se vaya a utilizar... Ejemplo: UTF-8
- `COLLATE`: Este campo es opcional. Junto a CHARACTER_SET, establece la variante específica global Ejemplo: utf8_unicode_ci

👁 [ÍNDICE](#ddl_index)

### CREANDO UNA TABLA - [``CREATE TABLE``]

La consulta ``CREATE`` también es usada para añadir tablas en una BBDD existentes, tal y como muestra este script 👇

```sql 
CREATE TABLE Libros (
    Nombre VARCHAR (50) NOT NULL,
    Precio CHAR(10)
);
```

👁 [ÍNDICE](#ddl_index)


### AÑADIENDO ATRIBUTOS

- Más adelante, veremos que a la hora de declarar atributos, podemos aplicar ciertas RESTRICCIONES (**CONSTRAINT**)

Ejemplo
```sql 
CREATE TABLE Libros (
    Id INT PRIMARY KEY IDENTITY(1,1),
    Nombre VARCHAR (50) NOT NULL,
    Precio CHAR(10)
    
    CONSTRAINT PK_Libros
            PRIMARY KEY (Precio)
);
```

👁 [ÍNDICE](#ddl_index)

### Tipos de datos - Dominios
<!-- Tabla de datos -->
| TIPO DE DATO  | CATEGORÍA |                             DEFINICIÓN                                                   |             
|---------------|-----------|------------------------------------------------------------------------------------------|
| INTEGER       | Numérico  | Es un número entero y a su vez el más empleado                                           |
| DECIMAL       | Numérico  | Es un núm. preciso. 131070 dígitos (antes de la coma) y 16385 dígitos (desp. de la coma) |               
| REAL          | Numérico  | Es nu número no preciso.                                                                 |
| CHAR          | Texto     | Longitud total y fija limitada                                                           |
| VARCHAR       | Texto     | Longitud variable                                                                        |
| TEXT          | Texto     | Longitud ilimitada variable                                                              |
| DATE          | Fecha     | La fecha del día. Usa 4 BYTES                                                            |
| TIME          | Fecha     | La hora del día. Usa 8 BYTES                                                             |
| TIMESTAMP     | Fecha     | La fecha y hora del día. Es una combinación de ``DATE`` + ``TIME``                       |
| BOOLEAN       | Booleano  | Indica si un valor es ``TRUE`` **OR** ``FALSE``. También puede ser ``NOT NULL``          |
| MONEY         | Dinero    | Número de precisión limitada. Hasta '4' cifras decimales. Se usa con **SUM**             |
| UUID          | OS        | Identificador universal único                                                            |
| JSON          | Fichero   | JavaScript Object Notation                                                               |
| XML           | Fichero   | Extensible Markup Language                                                               |    
| CIDR          | Network   | Direcciones IPV4 e IPV6. No permite bits distintos a '0' a la derecha de la máscara      |
| INET          | Network   | Direcciones IPV4 e IPV6.                                                                 |
<!-- Tabla de datos -->

👁 [ÍNDICE](#ddl_index)

### CREANDO UN DOMINIO - [CREATE DOMAIN]
A partir del campo de datos anterior, ya podemos crear nuestros propios dominios 👇

```sql
CREATE DOMAIN <nombreTipoDato> CHAR(10);
```
Una vez realizado lo anterior, podremos usar este dominio para la creación de tablas y asignaciones de dominios a los atributos...

👁 [ÍNDICE](#ddl_index)

### AÑADIENDO RESTRICCIONES A ATRIBUTOS - [``CONSTRAINTS``]

Una restricción es un método para especificar/establecer las:

- PRIMARY KEY
- FOREIGN KEY
- UNIQUE
- NOT NULL
- CHECK

Se utilizan con el ``CREATE TABLE`` y con el ``ALTER TABLE``.

👁 [ÍNDICE](#ddl_index)

### PRIMARY KEY

Establece cual es la clave principal de una tabla. Que según las reglas de E/R, las claves no pueden ser nulas y estos valores no pueden repetirse...

**Método simplificado**
```sql
CREATE TABLE Libreria (
  cantidadLibros INT PRIMARY KEY
);
```

**Método extenso**
```sql
CREATE TABLE Libreria (
  cantidadLibros INT,
  tomos CHAR(5),
  ...
  PRIMARY KEY (cantidadLibros)[, tomos, ..., ...])
);
```

👁 [ÍNDICE](#ddl_index)

### FOREIGN KEY

Es usada cuando un atributo/atributos de una tabla, es a su vez la clave principal de otra... En las claves foráneas, es preciso que deban tener el mismo tipo de dominio o atributo que la tabla principal. Hay varias maneras de hacerlo 👇


**Método simple**

```sql
CREATE TABLE Libreria1 (
  cantidadLibrosPequenhos dominio_ejemplo1 PRIMARY KEY,
  cantidadLibrosGrandes   dominio_ejemplo2,  
);
CREATE TABLE Libreria2 (
  cantidadTomosPequenhos  dominio_ejemplo1 PRIMARY KEY,
  cantidadTomosGrandes    dominio_ejemplo2 REFERENCES Libreria1 (cantidadLibrosPequenhos)
);
```

**Método extenso**

```sql
CREATE TABLE Libreria1 (
  cantidadLibrosPequenhos dominio_ejemplo1,
  cantidadLibrosGrandes   dominio_ejemplo2,  
  [CONSTRAINT PK_Libreria1]
    PRIMARY KEY (cantidadLibrosPequenhos[, cantidadLibrosGrandes])
);
CREATE TABLE Libreria2 (
  cantidadTomosPequenhos  dominio_ejemplo1 PRIMARY KEY,
  cantidadTomosGrandes    dominio_ejemplo2 REFERENCES Libreria1 (cantidadLibrosPequenhos)
  [CONSTRAINT PK_Libreria2]
    FOREIGN KEY (cantidadTomosPequenhos[, cantidadTomosGrandes])
    REFERENCES Libreria1 (cantidadLibrosPequenhos[, cantidadLibrosGrandes])
    ON DELETE [CASCADE | NO ACTION | SET NULL | SET DEFAULT <valorporDefecto>]
    ON UPDATE [CASCADE | NO ACTION | SET NULL | SET DEFAULT <valorporDefecto>]
);
```
🛡 NOTA: El único valor que **NO** puse a mano, fue el "valorporDefecto", tanto en el 'ON DELETE' como en el 'ON UPDATE'.

- VALORES de ``ON DELETE`` y ``ON UPDATE``.
  - CASCADE     -> Mediante esta opción, si el atributo al que hace referencia se modifica o elimina, este también modifica o elimina las claves ajenas.
  - NO ACTION   -> Mediante esta opción, si el atributo al que hace referencia se modifica o elimina, este no realiza nada. 🤐
  - SET NULL    -> Mediante esta opción, si el atributo al que hace referencia se modifica o elimina, los valores de las claves ajenas se ponen todas a **NULL**.
  - SET DEFAULT -> Mediante esta opción, si el atributo al que hace referencia se modifica o elimina, los valores de las claves ajenas se reestablecen por completo.

👁 [ÍNDICE](#ddl_index)

### UNIQUE
Estos valores deben de ser solamente **ÚNICOS**. Bajo ninguna excepción deben de repetirse en toda la tabla
```sql
CREATE TABLE Libreria(
Autores CHAR PRIMARY KEY,
Titulos CHAR UNIQUE,
...
);
```

👁 [ÍNDICE](#ddl_index)

### NOT NULL
Si utilizamos ``UNIQUE`` junto a ``NOT NULL`` podemos llegar a declarar **claves alternativas**..
```sql
CREATE TABLE Libreria(
Autores CHAR PRIMARY KEY,
Titulos CHAR UNIQUE NOT NULL,
...
);
```

👁 [ÍNDICE](#ddl_index)

# Modificación - [``ALTER``] <a name="ddl_alter"></a>
Instrucción utilizada para modificar columnas, tablas y restricciones. 
  > ``ALTER`` también nos permite renombrar ciertos elementos y vincular tablas de una base de datos a otra...
  
```sql 
ALTER TABLE [IF EXISTS] grecia
            [RENAME TO  esparta],
            [RENAME [COLUMN | CONSTRAINT] focida TO cefalonia]
            [SET SCHEMA persia],
            [ADD | DROP [COLUMN | CONSTRAINT] atenas]
            
```

👁 [ÍNDICE](#ddl_index)

# Eliminación  - [``DROP``] <a name="ddl_drop"></a>
Instrucción utilizada para borrar una BBDD y/o una tabla. Ejemplos 👇
```sql
DROP SCHEMA [IF EXISTS] langostasDB;
```
```sql
DROP TABLE [IF EXISTS] [CASCADE|RESTRICT] langostaCubana;
```
  > Mediante *IF EXISTS*, si la BBDD no existe, este solamente nos devolvería **``FALSE``** 
  > Mediante ``CASCADE``, esta eliminaría **TODA** la tabla y sus sub-adyacentes.
  > Mediante ``RESTRICT`` en si no se "carga" la tabla, mientras que esta dependa de otro atributo referenciada en otra tabla
  
🛡 IMPORTANTE: En MySQL, cuando se hace un ``DROP`` a una tabla, los *privilegios* otorgados para la tabla **NO** se eliminan automáticamente. Debería (y es aconsajable) hacer un ``DROP`` a cada una manualmente...

👁 [ÍNDICE](#ddl_index)



                                                         SENTENCIAS DML
                                        
# DEFINICIÓN
Usando sentencias **``DML``** formaremos instrucciones con la capacidad de modificar datos en las tablas creadas previamente.

Una agrupación de instrucciones DML, que se ejecutan consecutivamente, se denominan transacciones.

  > Esta opera sobre los objetos en una base de datos, es decir sobre su estructura

Veremos más adelante, ejemplos de su uso... ✌
  > Para guardar los datos, usaremos la sentencia ``COMMIT``
  > Para cancelar lo que hayamos insertado, usaremos la sentencia ``ROLLBACK``
***
***
# INDICE <a name="dml_index"></a>
1. ⚡ [DML - INSERT](#dml_insert)
2. ⚡ [DML - UPDATE](#dml_update)
3. ⚡ [DML - DELETE](#dml_delete)
***
## INSERT <a name="dml_insert"></a>

La consula ``INSERT`` es usada para añadir filas a una tabla


```sql
  INSERT INTO <nombre-tabla> [ (<ejemploAtributo1>, <ejemploAtributo2>] 
  VALUES (<valor1>, <valor2>)

```

El orden en que se les asignen los valores en ``VALUES`` tiene que coincidir el orden con el que se han definido las columnas en la creación de una tabla ``INSERT``. Los valores son asignados mediante un posicionamiento relativo 
 

Ejemplos 👇
```sql
INSERT INTO EDADES
VALUES (1,'WILSON');
```

```sql
INSERT INTO PAQUETES (CODPEDIDO,ESTADO)
VALUES (130,1);
```

👁 [ÍNDICE](#dml_index)

### INSERCCIÓN DE SENTENCIAS CON MÚLTIPLES FILAS [``INSERT`` + ``SELECT``]
En este caso, para introducir un sub-conjunto de fila(s) de una tabla dentro de otra, se escribe solamente una sentencia ``INSERT`` y una sentencia ``SUBSELECT`` interna (es decir, dentro de ella...) Ejemplo:

```sql
INSERT INTO tabla1 (columna1, columna2, columna3...)
SELECT ([sentencia SELECT]);
```

```sql
INSERT INTO PAQUETES (CODPEDIDO,ESTADO,NOMAPELLIDO)
SELECT CODPEDIDO+75,ESTADO,NOMAPELLIDO FROM PAQUETES WHERE CODPEDIDO IN (0,1,2);
```
  > Referencia a las columnas los valores que han sido recuperados mediante la sentencia ``SELECT``.
  > Añade en la tabla en su totalidad, las filas que se recuperen mediante la sentencia ``SELECT``.

👁 [ÍNDICE](#dml_index)

## UPDATE <a name="dml_update"></a>

La consula ``UPDATE`` es usada para actualizar valores, en una o varias columnas (para un subconjunto de tuplas de una tabla).

Ejemplos (Sintáxis y Prueba): 

```sql
UPDATE <tablaEjemplo>
SET <atributo1> = <ejemploValor1>, <columna2> = <ejemploValor2>, <columna3> = <ejemploValor3>...
[WHERE <predicado>];
```

```sql
UPDATE grecia
SET ( 
    pais = 'Grecia',
    anho = 480, 
    lider = 'Leonidas')
WHERE faccion = 'Esparta';
```

👁 [ÍNDICE](#dml_index)

## DELETE <a name="dml_delete"></a>

La consula ``DELETE`` es usada para eliminar fila(s) de una o varias tablas. En ella se debe especificar, al menos la tabla, y después mediante la sentencia ``WHERE``, las filas que queramos eliminar.

Ejemplos (Sintáxis y Prueba): 👇 

```sql
DELETE FROM <ejemploTABLA> 
[WHERE <filaOPCIONAL>];
```

```sql
DELETE FROM grecia 
WHERE pais = 'Grecia';
```

🛡 IMPORTANTE: Si no usamos la sentencia ``WHERE``, haremos que los cambios se efectuen en **TODAS** las *TUPLAS*. En este caso, si se omitiese, se ~~borrarían~~ todas las tuplas...

👁 [ÍNDICE](#dml_index)

