# Para iniciar SQL DESDE XAMPP DEBO ABRIR LA TERMINAL DEL XAMPP Y JECUTAR EL SIGUIENTE COMANDO

cd mysql
mysql -u root

# 1 Sentencia para crear una DB

CREATE DATABASE Empleados;

# 2 Para crear una tabla 

CREATE TABLE Usarios (
    ID INT PRIMARY KEY AUTO_INCRMENT,
    Nombre VARCHAR(50) NOT NULL,
    PaisID INT,
    FOREING KEY (PaisID) REFERENCES Pais(PaisID)
);

# 3 insertar datos a una tabla

INSERT INTO Usuarios (Nombre,Pais) VALUES ('Juan',2);

# 4 Consultar todos los datos de la tabla

SELECT * FROM Usuarios;

# 5 Borrar database

DROP DATABASE Empleados;

# 6 Modificar estructura de una tabla 
ALTER TABLE Usuarios MODIFY COLUMN Nombre Varchar(10);
ALTER TABLE Usuarios ADD edad INT;
ALTER TABLE empleados ADD telefono INT AFTER salario; 
mysql> CREATE TABLE empleados (
    > id INT NOT NULL AUTO_INCREMENT,
    > nombre VARCHAR(255) NOT NULL,
    > apellido VARCHAR(255) NOT NULL,
    > salario DECIMAL(10, 2) NOT NULL,
    > PRIMARY KEY (id)
    > );
Query OK, 0 rows affected (0.19 sec)

mysql> ALTER TABLE empleados
    > ADD edad INT;
Query OK, 0 rows affected (0.19 sec)

mysql> COMMIT;
Query OK, 0 rows affected (0.00 sec)

mysql> DESCRIBE empleados;
+-------+--------------+------+-----+---------+-------+
| Field | Type | Null | Key | Default | Extra |
+-------+--------------+------+-----+---------+-------+
| id | int(11) | NO | PRI | NULL | |
| nombre | varchar(255) | NO | | NULL | |
| apellido | varchar(255) | NO | | NULL | |
| salario | decimal(10,2) | NO | | NULL | |
| edad | int(11) | YES | | NULL | |
+-------+--------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

# 7 BORRAR una tabla
DROP TABLE empleados;
# borrar una columna
ALTER TABLE pedidos DROP COLUMN fechaPedido;
# Cambiar nombre de una columna 
MariaDB [PruebaDb]> ALTER TABLE pedidos CHANGE fedchaPedido FechaPedido DATE;

# 8 Borrar un registro
DELETE FROM usuarios WHERE id = 1;

# 9 Ver la estructura de una tabla
DESCRIBE empleados;
# 10 Modificar Datos (UPDATE)
UPDATE Usuarios SET Nombre='Jose' WHERE id=1;
# 11 INNER JOIN
SELECT Estudiantes.nombre Estudiantes.apellido Notas.asignatura Notas.calificacion FROM Estudiantes INNER JOIN Notas on Estudiantes.id = notas.id_estudiante;
# EJERCICIOS
Consulta para seleccionar usuarios cuyo nombre sea "Ana":
SELECT * FROM Usuarios WHERE Nombre = 'Ana';

Consulta para seleccionar usuarios cuyo correo electrónico contenga "example.com":
SELECT * FROM Usuarios WHERE Email LIKE '%example.com%';

Traer el valor maximo de una columna MariaDB [PruebaDb]> SELECT ID,MAX(Total) AS Max_TOTAL FROM pedidos;


----------------------------------------------------------------------------
CREATE TABLE Pedidos (
    ID INT PRIMARY KEY AUTO_INCREMENT,
    ClienteID INT,
    FechaPedido DATE,
    Total DECIMAL(10, 2)
);
Esta tabla almacena información sobre los pedidos realizados por los clientes. Ahora, se te presenta la tarea de realizar las siguientes consultas SQL:

Mostrar todos los pedidos (ID, ClienteID, FechaPedido, Total) en los que el cliente ha realizado un pedido con un monto total superior a $1000.

Mostrar el ID del cliente que ha realizado el pedido con el monto total más alto.

Mostrar la fecha del pedido más reciente realizado por un cliente específico. Puedes especificar el ID del cliente en la consulta.

Mostrar la cantidad total de dinero gastado por cada cliente. Debes mostrar el ID del cliente y el monto total gastado. Ordena los resultados de mayor a menor gasto.

MariaDB [PruebaDb]> SELECT * from pedidos where total > 1000;
+----+-----------+-------------+----------+
| ID | ClienteID | FechaPedido | Total    |
+----+-----------+-------------+----------+
|  1 |         1 | 2023-10-23  |  1500.00 |
|  2 |         2 | 2023-10-20  | 15000.00 |
|  3 |         3 | 2022-01-01  | 12000.00 |
+----+-----------+-------------+----------+
3 rows in set (0.000 sec)

MariaDB [PruebaDb]> SELECT ClienteID ,MAX(Total) As clienteGasto From pedidos;
+-----------+--------------+
| ClienteID | clienteGasto |
+-----------+--------------+
|         1 |     15000.00 |
+-----------+--------------+
1 row in set (0.001 sec)

MariaDB [PruebaDb]> SELECT ClienteID, MAX(FechaPedido) As PedidoReciente from Pedidos WHERE ID=2;
+-----------+----------------+
| ClienteID | PedidoReciente |
+-----------+----------------+
|         2 | 2023-10-20     |
+-----------+----------------+
1 row in set (0.000 sec)

MariaDB [PruebaDb]> SELECT ClienteID, SUM(Total) As TotalGastado from Pedidos group by ClienteID Order By TotalGastado DESC;
+-----------+--------------+
| ClienteID | TotalGastado |
+-----------+--------------+
|         2 |     15150.00 |
|         3 |     12000.00 |
|         1 |      1500.00 |
|         4 |       150.00 |
+-----------+--------------+
4 rows in set (0.000 sec)