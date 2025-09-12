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

Sirven para ayudar a dar una práctica a los niños de instituciones educativas de 5-15 años y personas de la tercera edad en asilos.  

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
SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cantidad debe ser mayor a cero'; 
ELSEIF NOT EXISTS (SELECT 1 FROM cliente WHERE id_cliente = id_cli) THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Cliente no existe'; ELSEIF NOT EXISTS (SELECT 1 FROM producto WHERE id = id_prod) THEN SIGNAL SQLSTATE '45000' SET MESSAGE_TEXT = 'Producto no existe'; ELSE INSERT INTO venta(id_cliente, id_producto, cantidad) VALUES (id_cli, id_prod, cantidad_venta); END IF; END; // DELIMITER ; insert into fabricante (id,nombre) values (1,'Sam McBratney'); insert into fabricante values (2,'Gianni Rodari'); Insert into fabricante values (3, 'L. Frank Baum'); insert into fabricante values (4, 'Horacio Quiroga'),                 (5,'Michael Grejniec'), (6, 'Hervé Tullet'); insert into producto values (1, 'Adivina cuánto te quiero', 15.00, 1); insert into producto values (2, 'Cuentos para jugar', 10.00, 2); insert into producto values (3, 'El maravilloso mago de Oz', 9.99, 3); insert into producto values (4, 'Cuentos de la selva', 5.00, 4); insert into producto values (5, '¿A qué sabe la Luna?', 10.00, 5); insert into producto values (6, '¡Oh! Un libro que hace sonidos', 12.00, 6); insert into cliente values (1, 'Lucía'); insert into cliente values (2, 'Mateo'); insert into cliente values (3, 'Valentina'); insert into venta values (1, 1, 1, 2); insert into venta values (2, 2, 2, 1); insert into venta values (3, 3, 3, 5); insert into venta values (4, 1, 4, 6); insert into venta values (5, 2, 5, 3); insert into venta values (6, 3, 6, 4); select v.id_venta, c.nombre as "Cliente", p.nombre as nombre_producto, v.cantidad, case when v.cantidad < 2 then "poca" when v.cantidad between 2 and 4 then "media" else "mucha" end as "Nivel de compra" from venta v, cliente c, producto p where c.id_cliente = v.id_cliente and p.id = v.id_producto; /La gerencia desea agrupar los productos en categorias de precio economico -> menor a 5 medio -> 5 entre entre 15 caro -> 20/ select nombre as nombre_producto,     precio, case when precio < 5 then "economico" when precio between 5 and 10 then "medio" else "caro" end as "categoria" from producto; select * from producto; select nombre as 'nombre del producto', precio as 'dolares', round(precio * 10, 2) as 'euros' from producto; /Clasificar productos como: poca demanda (menos de 3 ventas) media demanda (3-5 ventas) alta demanda (más de 5 ventas) */ select p.nombre as nombre_producto,     count(v.id_venta) as "cantidades vendidas", case when count(v.id_venta) < 3 then "poca demanda" when count(v.id_venta) between 3 and 5 then "media demanda" else "alta demanda" end as "demanda" from producto p, venta v where p.id = v.id_producto group by p.id; /*Dependiendo de la cantidad comprada se aplicará una política de descuentos de 5% si compra 3-4 unidades 10% si compra más de 5 */ select c.nombre as "Cliente",     p.nombre as "producto", v.cantidad, Case when v.cantidad between 3 and 4 then "0.05" when v.cantidad > 5 then "0.10" else "0.00" end as "descuento" from venta v, cliente c, producto p where c.id_cliente = v.id_cliente and p.id = v.id_producto; /*mostrar información de una tabla/ select * from fabricante;


 

¿Qué son? 

Son libros las cuales se caracterizan por ser digítales que mejoren la educación y dar una práctica. Son de varias asignaturas como: Leyendas, cuentos, mitos, audio libros. 

 
