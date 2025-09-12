# Proyecto1
this project 
Proyecto: Venta de libros digitales 

Miembros: Ronquillo, Santillan, Montiel, Navarro 

Base datos 

Usuario 
Edad 
sección 

 

Categorías 
Tipos 
 
Producto 
Cantidad 
Costo 

¿Para qué sirven? 
Sirven para ayudar a dar una práctica a los niños de instituciones 
educativas de 5-15 años y personas de la tercera edad en asilos.  

#Venta de libros
DROP DATABASE IF EXISTS Tienda_digital;
CREATE DATABASE Tienda_digital CHARACTER SET utf8mb4;
USE Tienda_digital;

IMARY KEY, nombre VARCHAR(100) NOT NULL );
CREATE TABLE venta (
id_venta INT UNSIGNED AUTO_INCREMENT PRIMARY KEY,
id_cliente INT UNSIGNED NOT NULL,
id_producto INT UNSIGNED NOT NULL,
cantidad INT UNSIGNED NOT NULL, 
FOREIGN KEY (id_cliente) REFERENCES cliente(id_cliente), FOREIGN KEY (id_producto) REFERENCES producto(id) 
);
DELIMITER //
CREATE PROCEDURE insertar_fabricante(IN nombre_fab VARCHAR(100)) BEGIN 
IF nombre_fab IS NULL OR nombre_fab = '' THEN 
SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Nombre del fabricante no puede estar vacío'; 
ELSE 
INSERT INTO fabricante(nombre) VALUES (nombre_fab); 
END IF;
END; 
// 
CREATE PROCEDURE insertar_producto( 
IN nombre_prod VARCHAR(100), 
IN precio_prod DOUBLE, 
IN id_fab INT 
) 
BEGIN 
IF nombre_prod IS NULL OR nombre_prod = '' THEN 
SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Nombre del producto no puede estar vacío'; 
ELSEIF precio_prod <= 0 THEN 
SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'El precio debe ser mayor a cero'; 
ELSEIF NOT EXISTS (SELECT 1 FROM fabricante WHERE id = id_fab) THEN 
SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Fabricante no existe';
ELSE
INSERT INTO producto(nombre, precio, id_fabricante) 
VALUES (nombre_prod, precio_prod, id_fab);
END IF;
END; 
//

CREATE PROCEDURE insertar_cliente(IN nombre_cli VARCHAR(100))
BEGIN
IF nombre_cli IS NULL OR nombre_cli = '' THEN
SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Nombre del cliente no puede estar vacío';
ELSE 
INSERT INTO cliente(nombre) VALUES (nombre_cli); 
END IF; 
END; 
// 
CREATE PROCEDURE insertar_venta( 
IN id_cli INT,
IN id_prod INT, 
IN cantidad_venta INT 
) 
BEGIN 
IF cantidad_venta <= 0 THEN

¿Qué son? 

Son libros las cuales se caracterizan por ser digítales que mejoren la educación y dar una práctica. Son de varias asignaturas como: Leyendas, cuentos, mitos, audio libros. 

 
