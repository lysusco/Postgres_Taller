# Postgres_Taller

### **Consultas sobre una tabla**

1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de todos los alumnos. El listado deberá estar ordenado alfabéticamente de menor a mayor por el primer apellido, segundo apellido y nombre.
~~~sql
  SELECT apellido1, apellido2, nombre 
  FROM persona
  WHERE tipo = 'Alumno'
  ORDER BY apellido1, apellido2, nombre;
~~~
3. Averigua el nombre y los dos apellidos de los alumnos que **no** han dado de alta su número de teléfono en la base de datos.
4. Devuelve el listado de los alumnos que nacieron en `1999`.
5. Devuelve el listado de profesores que **no** han dado de alta su número de teléfono en la base de datos y además su nif termina en `K`.
6. Devuelve el listado de las asignaturas que se imparten en el primer cuatrimestre, en el tercer curso del grado que tiene el identificador `7`.
