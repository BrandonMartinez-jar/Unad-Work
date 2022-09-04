# Solución actividad - Fase 1

## ¿Qué es una entidad y sus características?: 
una entidad consiste en la representación de un sujeto, ya sea una persona, organización, objeto o concepto, esto, en bases de datos se relaciona a una o varias tablas relacionadas entre sí a través de sus atributos principales (PK o FK).  

## ¿Qué es un atributo?: 
Los atributos son valores que representan a una entidad, estos se pueden dividir en:

- Atributos simples: Este tipo de atributo hace referencia a un valor simple para una entidad en particular, por ejemplo, el atributo "cargo" en una entidad "empleado".
![image](https://user-images.githubusercontent.com/76891236/188294450-72892246-e4e0-4ff4-8472-8c06cc567c53.png)

- Atributos de valores compuestos: Este tipo de atributo hace referencia a un valor que se compone de otros atributos concatenados, por ejemplo, la dirección, esta se compone de atributos como calle, cod_postal, localidad, etc...
![image](https://user-images.githubusercontent.com/76891236/188294543-d58b3e4f-8601-404e-bee4-2d9720fff354.png)

- Atributos de valores multivaluados: Este tipo de atributo hace referencia a un valor que se compone de multiples valores que referencian a algo específico, por ejemplo, una persona puede tener varios números de teléfono.

- Atributos de valores derivados: Este tipo de atributo hace referancia a un valor que deriva de otro, por ejemplo, la edad puede derivarse del atributo "fecha_nacimiento".

## ¿Que es una relación y cómo se articula con los terminos, llave foránea y llave primaria?

### ¿Qué es una relación?:

Una relación se puede definir como un vínculo a través de una tributo que define una dependencia entre entidades.

### ¿Que es llave primaria y llave foránea?:

- Llave primaria (PK): Este tipo de atributo hace referencia a aquello que hace unico a cada individuo en particular dentro de una entidad, por ejemplo, en una entidad "empleados" cada empleado tiene su numero de identificación, o cedula que permite diferenciarse de forma particular de los demás empleados dentro de su organización.

- Llave foránea (FK): Este tipo de atributo hace referencia a aquello que relaciona a una entidad con otra, por ejemplo, dentro de una organización cada empleado puede tener una o varias oficinas asignadas, tanto el empleado como la oficina tienen su numero de identificación, para relacionarlos entre sí se utiliza el numero de identifiación (o llave primaria) de la entidad "empleados" como atributo dentro de la entidad "oficinas", así se diferenciaría que oficina está asignada a cada empleado.

### ¿Que tipos de relaciones hay?:

- Relación uno a uno (1:1): Es la relación donde cada registro de una entidad se puede relacionar con un solo registro de la otra, por ejemplo, para asigar un computador a un empleado puedo usar la llave primaria de la entidad empleado como llave primaria y llave foránea en la entidad computador.

- Relación uno a muchos (1:N): Es la relación donde cada registro de una entidad se puede relacionar con varios registros de otra, porejemplo, un colegio tiene muchos estudiantes, para relacionar estas dos entidades entre sí usaría el numero de identificación (PK) de la entidad "colegios" en la entidad "estudiantes", esto permitiría asignarle un colegio a cada estudiante pero multiples estudiantes a un colegio, esta misma relación en sentido contrario se podría representar como una relación muchos a uno (M:1).
![image](https://user-images.githubusercontent.com/76891236/188294943-f4be16a6-50e2-4d78-92c3-d172abc5b03c.png)

- Relación muchos a muchos (M:N): Es la relación donde varios registros de una entidad se puede relacionar a varios registros de otra a travez de una entidad auxiliar, por ejemplo, cada alumno puede matricular varios cursos y cada curso puede tener varios estudiantes, para relacionarlos entre sí se utilizaría una entidad "matricula" que utilizaría la llave primaria de las entidades "alumnos" y "cursos" como llave foranea, cabe resaltar que estas entidades auxiliares pueden tener atributos, en el ejemplo anterior un atributo podría ser la nota del estudiante al realizar el curso
![image](https://user-images.githubusercontent.com/76891236/188295053-bfdefecc-a59a-4155-a8de-5afa379c2fd5.png)

- Relación reflexiva: Es la relación donde un registro de una entidad puede relacionar a otro de la misma entidad, por ejemplo, la entidad alquiler renueva sus atributos cuando el arrendatario renueva su contrato de alquiler, esto se puede hacer utilizando la llave primaria del registro anterior como llave foranea, cabe resaltar que este tipo de relación pueden ser 1:1, 1:N y M:N.
![image](https://user-images.githubusercontent.com/76891236/188295226-6dfce278-473b-434e-9868-4fe9540d7214.png)

Es importante resaltar que las relaciones pueden ser configuradas de tal manera que no es obligatorio para una entidad participar en la relación, haciendo que el campo que funciona como llave foranea pueda quedarse vacío

### ¿En que consiste la cardinalidad?:
La cardinalidad hace referencia a la manera de relacionarse las entidades entre sí, los tipos de relaciones. 

### ¿Qué es un modelo entidad relación?:
Es una manera gráfica de representar el planeamiento de una base de datos exponiendo las entidades que participaran, sus atributos y de qué manera se relacionan.

## Solución al caso:

### Modelo relacional:
- Producto(id (PK), descripcion, categoria, cantidad_disponible, precio, fecha_actualizacion)
- Vendedor(num_identificacion (PK), nombre, direccion, fecha_nacimiento, sueldo, teléfono, email, fecha_actualizacion)
- Cliente(num_identificacion (PK), nombres, ciudad, direccion, fecha_nacimiento, telefono, email)
- Pedido(id (PK), num_identificacion (Cliente_FK), fecha, estado, total)
- Pedido_Producto(id_pedido (PK, Pedido_FK), id_producto (PK, Producto_FK), cantidad)
- Factura(id PK, id_pedido (Pedido_FK), id_vendedor (Vendedor_FK), id_cliente (Cliente_FK), estado, fecha)

### Modelo Entidad Relación:
![Untitled Diagram drawio](https://user-images.githubusercontent.com/76891236/188297262-fe618d62-be58-4747-9578-925d742f750a.png)


### Justificación:
- Las entidades producto, vendedor y cliente son entidades independientes.
- La entidad pedido tiene relación muchos a uno con la entidad cliente, de tal manera que el pedido pertenece a un cliente pero el cliente puede hacer multiples pedidos
- La entidad pedido tiene relación muchos a muchos con la entidad producto, de tal manera que un pedido puede tener muchos productos y los productos pueden estar en muchos pedidos, usando la entidad auxiliar (pedido_producto), la cual tiene un atibuto adicional que hace referencia a la lista de productos que se pide, la cantidad de cada producto que se pidió y esto permite después realizar el calculo utilizando el precio actual que contiene la entidad producto.
- Así mismo la entidad factura tiene una relación muchos a uno con las entidades pedido, vendedor y cliente, (como el enunciado lo pide, aunque yo en vez de darle un id auto generado con un numero consecutivo usaría una relación uno a uno con la entidad pedido, de tal manera que un pedido no se pueda facturar más de una vez), al relacionarse con la tabla pedido se puede acceder a su relación con la tabla producto y calcular el precio total como lo había explicado antes.

## Referencias bibliográficas

- Curso de Fundamentos de Bases de Datos. (s. f.). http://platzi.com/cursos/bd/. Recuperado 3 de septiembre de 2022, de http://platzi.com/cursos/bd/
- Database_foundations_course_es.pdf. (s. f.). Recuperado 3 de septiembre de 2022, de https://academy.oracle.com/pages/database_foundations_course_es.pdf
- Guia-Normas-APA-7ma-edicion.pdf. (s. f.). Recuperado 3 de septiembre de 2022, de https://normas-apa.org/wp-content/uploads/Guia-Normas-APA-7ma-edicion.pdf
- José Juan Sánchez Hernández. Recuperado 3 de septiembre de 2022, de https://josejuansanchez.org/bd/

