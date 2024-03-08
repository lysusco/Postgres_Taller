# Postgres_Taller

### **Consultas sobre una tabla**

1. Devuelve un listado con el primer apellido, segundo apellido y el nombre de todos los alumnos. El listado deberá estar ordenado alfabéticamente de menor a mayor por el primer apellido, segundo apellido y nombre.
~~~sql
  SELECT apellido1, apellido2, nombre 
  FROM persona
  WHERE tipo = 'Alumno'
  ORDER BY apellido1, apellido2, nombre;
~~~
2. Averigua el nombre y los dos apellidos de los alumnos que **no** han dado de alta su número de teléfono en la base de datos.
~~~SQL
  SELECT apellido1, apellido2, nombre 
  FROM persona
  WHERE tipo = 'Alumno' AND telefono IS NULL;
~~~
3. Devuelve el listado de los alumnos que nacieron en `1999`.
~~~SQL
  SELECT *
  FROM persona
  WHERE tipo = 'Alumno' AND fecha_nacimiento > '1998/12/31' AND fecha_nacimiento < '2000/01/01';
~~~
4. Devuelve el listado de profesores que **no** han dado de alta su número de teléfono en la base de datos y además su nif termina en `K`.
~~~SQL
  SELECT *
  FROM persona
  WHERE tipo = 'Profesor' AND telefono IS NULL AND nif LIKE '%K';
~~~
5. Devuelve el listado de las asignaturas que se imparten en el primer cuatrimestre, en el tercer curso del grado que tiene el identificador `7`.
~~~SQL
  SELECT * 
  FROM asignatura 
  WHERE cuatrimeste = 1 AND curso = 3 AND grado_id = 7;
~~~

### **Consultas multitabla (Composición interna)**

1. Devuelve un listado con los datos de todas las **alumnas** que se han matriculado alguna vez en el `Grado en Ingeniería Informática (Plan 2015)`.
~~~SQL
  SELECT * 
  FROM persona p 
  INNER JOIN alumno_matricula_asignatura a ON a.alumno_id = p.id 
  INNER JOIN asignatura c ON a.asignatura_id = c.id
  WHERE sexo = 'M' AND c.grado_id = 4;
~~~
2. Devuelve un listado con todas las asignaturas ofertadas en el `Grado en Ingeniería Informática (Plan 2015)`.
~~~SQL
  SELECT a.nombre, t.nombre_grado 
  FROM asignatura a
  INNER JOIN grado t ON a.grado_id = t.id
  WHERE t.id = 4;
~~~
3. Devuelve un listado de los profesores junto con el nombre del departamento al que están vinculados. El listado debe devolver cuatro columnas, primer apellido, segundo apellido, nombre y nombre del departamento. El resultado estará ordenado alfabéticamente de menor a mayor por los apellidos y el nombre.
~~~SQL
  SELECT p.apellido1, p.apellido2, p.nombre, c.nombre
  FROM persona p
  INNER JOIN profesor t ON t.profesor_id = p.id
  INNER JOIN departamento c ON c.id = t.departamento_id
  WHERE tipo = 'Profesor'
  ORDER BY p.apellido1,p.apellido2,p.nombre;
~~~
4. Devuelve un listado con el nombre de las asignaturas, año de inicio y año de fin del curso escolar del alumno con nif `26902806M`.
~~~SQL
  SELECT p.nombre, a.nombre, c.anyo_inicio, c.anyo_fin
  FROM curso_escolar c
  INNER JOIN alumno_matricula_asignatura t ON t.curso_id = c.id
  INNER JOIN asignatura a ON t.asignatura_id = a.id
  INNER JOIN persona p ON t.alumno_id = p.id
  WHERE p.nif = '26902806M' AND p.tipo = 'Alumno';
~~~
5. Devuelve un listado con el nombre de todos los departamentos que tienen profesores que imparten alguna asignatura en el `Grado en Ingeniería Informática (Plan 2015)`.
~~~SQL
  SELECT c.nombre
  FROM departamento c
  INNER JOIN profesor p ON c.id = p.departamento_id
  INNER JOIN asignatura a ON p.profesor_id = a.id_profesor
  WHERE a.id = 4;
~~~
6. Devuelve un listado con todos los alumnos que se han matriculado en alguna asignatura durante el curso escolar 2018/2019.
~~~SQL
  SELECT DISTINCT p.nombre, p.apellido1, p.apellido2, c.anyo_inicio, c.anyo_fin
  FROM persona p
  INNER JOIN alumno_matricula_asignatura a ON p.id = a.alumno_id
  INNER JOIN curso_escolar c ON c.id = a.curso_id
  WHERE c.id = 5 AND p.tipo = 'Alumno';
~~~

### **Consultas multitabla (Composición externa)**

Resuelva todas las consultas utilizando las cláusulas `LEFT JOIN` y `RIGHT JOIN`.

1. Devuelve un listado con los nombres de **todos** los profesores y los departamentos que tienen vinculados. El listado también debe mostrar aquellos profesores que no tienen ningún departamento asociado. El listado debe devolver cuatro columnas, nombre del departamento, primer apellido, segundo apellido y nombre del profesor. El resultado estará ordenado alfabéticamente de menor a mayor por el nombre del departamento, apellidos y el nombre.
~~~SQL
  INSERT INTO persona VALUES (25, '26902899M', 'Rut', 'Ortega', 'Velasco', 'Piedecuesta', 'C/ Bajando por el centro comercial xd', '30000000', '2005/07/05', 'M', 'Profesor');
  
  SELECT d.nombre, p.apellido1, p.apellido2, p.nombre
  FROM persona p
  LEFT JOIN profesor pr ON pr.profesor_id = p.id
  LEFT JOIN departamento d ON pr.departamento_id = d.id
  WHERE p.tipo = 'Profesor'
  ORDER BY d.nombre, p.apellido1, p.apellido2, p.nombre;
~~~
2. Devuelve un listado con los profesores que no están asociados a un departamento.
~~~SQL
~~~
3. Devuelve un listado con los departamentos que no tienen profesores asociados.
~~~SQL
~~~
4. Devuelve un listado con los profesores que no imparten ninguna asignatura.
~~~SQL
~~~
5. Devuelve un listado con las asignaturas que no tienen un profesor asignado.
~~~SQL
~~~
6. Devuelve un listado con todos los departamentos que tienen alguna asignatura que no se haya impartido en ningún curso escolar. El resultado debe mostrar el nombre del departamento y el nombre de la asignatura que no se haya impartido nunca.
~~~SQL
~~~
