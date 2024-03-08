# Postgres_Taller

## BASE DE DATOS
~~~SQL
  CREATE TYPE sexos AS ENUM ('H','M');
  CREATE TYPE tipos_persona AS ENUM ('Profesor', 'Alumno');
  CREATE TYPE tipos_asignatura AS ENUM ('Basica', 'Obligatoria', 'Optativa');
  
  CREATE TABLE persona(
  	id SERIAL PRIMARY KEY,
  	nif VARCHAR(9),
  	nombre VARCHAR(25),
  	apellido1 VARCHAR(50),
  	apellido2 VARCHAR(50),
  	ciudad VARCHAR(25),
  	direccion VARCHAR(50),
  	telefono VARCHAR(9),
  	fecha_nacimiento DATE,
  	sexo sexos,
  	tipo tipos_persona
  );
  
  CREATE TABLE departamento (
  	id SERIAL PRIMARY KEY,
  	nombre VARCHAR(50)
  );
  
  CREATE TABLE profesor (
  	departamento_id INTEGER REFERENCES departamento(id),
  	profesor_id INTEGER REFERENCES persona(id)
  );
  
  CREATE TABLE grado (
  	id SERIAL PRIMARY KEY,
  	nombre_grado VARCHAR(100)
  );
  
  CREATE TABLE asignatura (
  	id SERIAL PRIMARY KEY,
  	nombre VARCHAR(100),
  	creditos FLOAT,
  	tipos tipos_asignatura,
  	curso SMALLINT,
  	cuatrimeste SMALLINT,
  	id_profesor INTEGER REFERENCES persona(id),
  	grado_id INTEGER REFERENCES grado(id)
  );
  
  CREATE TABLE curso_escolar(
  	id SERIAL PRIMARY KEY,
  	anyo_inicio INTEGER,
  	anyo_fin INTEGER
  );
  
  CREATE TABLE alumno_matricula_asignatura (
  	alumno_id INTEGER REFERENCES persona(id),
  	asignatura_id INTEGER REFERENCES asignatura(id),
  	curso_id INTEGER REFERENCES curso_escolar(id)
  );
~~~

## INSERT
~~~SQL
   /* Departamento */
  INSERT INTO departamento VALUES (1, 'Informática');
  INSERT INTO departamento VALUES (2, 'Matemáticas');
  INSERT INTO departamento VALUES (3, 'Economía y Empresa');
  INSERT INTO departamento VALUES (4, 'Educación');
  INSERT INTO departamento VALUES (5, 'Agronomía');
  INSERT INTO departamento VALUES (6, 'Química y Física');
  INSERT INTO departamento VALUES (7, 'Filología');
  INSERT INTO departamento VALUES (8, 'Derecho');
  INSERT INTO departamento VALUES (9, 'Biología y Geología');
   
   /* Persona */
  INSERT INTO persona VALUES (1, '26902806M', 'Salvador', 'Sánchez', 'Pérez', 'Almería', 'C/ Real del barrio alto', '950254837', '1991/03/28', 'H', 'Alumno');
  INSERT INTO persona VALUES (2, '89542419S', 'Juan', 'Saez', 'Vega', 'Almería', 'C/ Mercurio', '618253876', '1992/08/08', 'H', 'Alumno');
  INSERT INTO persona VALUES (3, '11105554G', 'Zoe', 'Ramirez', 'Gea', 'Almería', 'C/ Marte', '618223876', '1979/08/19', 'M', 'Profesor');
  INSERT INTO persona VALUES (4, '17105885A', 'Pedro', 'Heller', 'Pagac', 'Almería', 'C/ Estrella fugaz', NULL, '2000/10/05', 'H', 'Alumno');
  INSERT INTO persona VALUES (5, '38223286T', 'David', 'Schmidt', 'Fisher', 'Almería', 'C/ Venus', '678516294', '1978/01/19', 'H', 'Profesor');
  INSERT INTO persona VALUES (6, '04233869Y', 'José', 'Koss', 'Bayer', 'Almería', 'C/ Júpiter', '628349590', '1998/01/28', 'H', 'Alumno');
  INSERT INTO persona VALUES (7, '97258166K', 'Ismael', 'Strosin', 'Turcotte', 'Almería', 'C/ Neptuno', NULL, '1999/05/24', 'H', 'Alumno');
  INSERT INTO persona VALUES (8, '79503962T', 'Cristina', 'Lemke', 'Rutherford', 'Almería', 'C/ Saturno', '669162534', '1977/08/21', 'M', 'Profesor');
  INSERT INTO persona VALUES (9, '82842571K', 'Ramón', 'Herzog', 'Tremblay', 'Almería', 'C/ Urano', '626351429', '1996/11/21', 'H', 'Alumno');
  INSERT INTO persona VALUES (10, '61142000L', 'Esther', 'Spencer', 'Lakin', 'Almería', 'C/ Plutón', NULL, '1977/05/19', 'M', 'Profesor');
  INSERT INTO persona VALUES (11, '46900725E', 'Daniel', 'Herman', 'Pacocha', 'Almería', 'C/ Andarax', '679837625', '1997/04/26', 'H', 'Alumno');
  INSERT INTO persona VALUES (12, '85366986W', 'Carmen', 'Streich', 'Hirthe', 'Almería', 'C/ Almanzora', NULL, '1971-04-29', 'M', 'Profesor');
  INSERT INTO persona VALUES (13, '73571384L', 'Alfredo', 'Stiedemann', 'Morissette', 'Almería', 'C/ Guadalquivir', '950896725', '1980/02/01', 'H', 'Profesor');
  INSERT INTO persona VALUES (14, '82937751G', 'Manolo', 'Hamill', 'Kozey', 'Almería', 'C/ Duero', '950263514', '1977/01/02', 'H', 'Profesor');
  INSERT INTO persona VALUES (15, '80502866Z', 'Alejandro', 'Kohler', 'Schoen', 'Almería', 'C/ Tajo', '668726354', '1980/03/14', 'H', 'Profesor');
  INSERT INTO persona VALUES (16, '10485008K', 'Antonio', 'Fahey', 'Considine', 'Almería', 'C/ Sierra de los Filabres', NULL, '1982/03/18', 'H', 'Profesor');
  INSERT INTO persona VALUES (17, '85869555K', 'Guillermo', 'Ruecker', 'Upton', 'Almería', 'C/ Sierra de Gádor', NULL, '1973/05/05', 'H', 'Profesor');
  INSERT INTO persona VALUES (18, '04326833G', 'Micaela', 'Monahan', 'Murray', 'Almería', 'C/ Veleta', '662765413', '1976/02/25', 'H', 'Profesor');
  INSERT INTO persona VALUES (19, '11578526G', 'Inma', 'Lakin', 'Yundt', 'Almería', 'C/ Picos de Europa', '678652431', '1998/09/01', 'M', 'Alumno');
  INSERT INTO persona VALUES (20, '79221403L', 'Francesca', 'Schowalter', 'Muller', 'Almería', 'C/ Quinto pino', NULL, '1980/10/31', 'H', 'Profesor');
  INSERT INTO persona VALUES (21, '79089577Y', 'Juan', 'Gutiérrez', 'López', 'Almería', 'C/ Los pinos', '678652431', '1998/01/01', 'H', 'Alumno');
  INSERT INTO persona VALUES (22, '41491230N', 'Antonio', 'Domínguez', 'Guerrero', 'Almería', 'C/ Cabo de Gata', '626652498', '1999/02/11', 'H', 'Alumno');
  INSERT INTO persona VALUES (23, '64753215G', 'Irene', 'Hernández', 'Martínez', 'Almería', 'C/ Zapillo', '628452384', '1996/03/12', 'M', 'Alumno');
  INSERT INTO persona VALUES (24, '85135690V', 'Sonia', 'Gea', 'Ruiz', 'Almería', 'C/ Mercurio', '678812017', '1995/04/13', 'M', 'Alumno');
   
  /* Profesor */
  INSERT INTO profesor VALUES (1, 3);
  INSERT INTO profesor VALUES (2, 5);
  INSERT INTO profesor VALUES (3, 8);
  INSERT INTO profesor VALUES (4, 10);
  INSERT INTO profesor VALUES (4, 12);
  INSERT INTO profesor VALUES (6, 13);
  INSERT INTO profesor VALUES (1, 14);
  INSERT INTO profesor VALUES (2, 15);
  INSERT INTO profesor VALUES (3, 16);
  INSERT INTO profesor VALUES (4, 17);
  INSERT INTO profesor VALUES (5, 18);
  INSERT INTO profesor VALUES (6, 20);
  
   
   /* Grado */
  INSERT INTO grado VALUES (1, 'Grado en Ingeniería Agrícola (Plan 2015)');
  INSERT INTO grado VALUES (2, 'Grado en Ingeniería Eléctrica (Plan 2014)');
  INSERT INTO grado VALUES (3, 'Grado en Ingeniería Electrónica Industrial (Plan 2010)');
  INSERT INTO grado VALUES (4, 'Grado en Ingeniería Informática (Plan 2015)');
  INSERT INTO grado VALUES (5, 'Grado en Ingeniería Mecánica (Plan 2010)');
  INSERT INTO grado VALUES (6, 'Grado en Ingeniería Química Industrial (Plan 2010)');
  INSERT INTO grado VALUES (7, 'Grado en Biotecnología (Plan 2015)');
  INSERT INTO grado VALUES (8, 'Grado en Ciencias Ambientales (Plan 2009)');
  INSERT INTO grado VALUES (9, 'Grado en Matemáticas (Plan 2010)');
  INSERT INTO grado VALUES (10, 'Grado en Química (Plan 2009)');
   
  /* Asignatura */
  INSERT INTO asignatura VALUES (1, 'Álgegra lineal y matemática discreta', 6, 'Basica', 1, 1, 3, 4);
  INSERT INTO asignatura VALUES (2, 'Cálculo', 6, 'Basica', 1, 1, 14, 4);
  INSERT INTO asignatura VALUES (3, 'Física para informática', 6, 'Basica', 1, 1, 3, 4);
  INSERT INTO asignatura VALUES (4, 'Introducción a la programación', 6, 'Basica', 1, 1, 14, 4);
  INSERT INTO asignatura VALUES (5, 'Organización y gestión de empresas', 6, 'Basica', 1, 1, 3, 4);
  INSERT INTO asignatura VALUES (6, 'Estadística', 6, 'Basica', 1, 2, 14, 4);
  INSERT INTO asignatura VALUES (7, 'Estructura y tecnología de computadores', 6, 'Basica', 1, 2, 3, 4);
  INSERT INTO asignatura VALUES (8, 'Fundamentos de electrónica', 6, 'Basica', 1, 2, 14, 4);
  INSERT INTO asignatura VALUES (9, 'Lógica y algorítmica', 6, 'Basica', 1, 2, 3, 4);
  INSERT INTO asignatura VALUES (10, 'Metodología de la programación', 6, 'Basica', 1, 2, 14, 4);
  INSERT INTO asignatura VALUES (11, 'Arquitectura de Computadores', 6, 'Basica', 2, 1, 3, 4);
  INSERT INTO asignatura VALUES (12, 'Estructura de Datos y Algoritmos I', 6, 'Obligatoria', 2, 1, 3, 4);
  INSERT INTO asignatura VALUES (13, 'Ingeniería del Software', 6, 'Obligatoria', 2, 1, 14, 4);
  INSERT INTO asignatura VALUES (14, 'Sistemas Inteligentes', 6, 'Obligatoria', 2, 1, 3, 4);
  INSERT INTO asignatura VALUES (15, 'Sistemas Operativos', 6, 'Obligatoria', 2, 1, 14, 4);
  INSERT INTO asignatura VALUES (16, 'Bases de Datos', 6, 'Basica', 2, 2, 14, 4);
  INSERT INTO asignatura VALUES (17, 'Estructura de Datos y Algoritmos II', 6, 'Obligatoria', 2, 2, 14, 4);
  INSERT INTO asignatura VALUES (18, 'Fundamentos de Redes de Computadores', 6 ,'Obligatoria', 2, 2, 3, 4);
  INSERT INTO asignatura VALUES (19, 'Planificación y Gestión de Proyectos Informáticos', 6, 'Obligatoria', 2, 2, 3, 4);
  INSERT INTO asignatura VALUES (20, 'Programación de Servicios Software', 6, 'Obligatoria', 2, 2, 14, 4);
  INSERT INTO asignatura VALUES (21, 'Desarrollo de interfaces de usuario', 6, 'Obligatoria', 3, 1, 14, 4);
  INSERT INTO asignatura VALUES (22, 'Ingeniería de Requisitos', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (23, 'Integración de las Tecnologías de la Información en las Organizaciones', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (24, 'Modelado y Diseño del Software 1', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (25, 'Multiprocesadores', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (26, 'Seguridad y cumplimiento normativo', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (27, 'Sistema de Información para las Organizaciones', 6, 'Optativa', 3, 1, NULL, 4); 
  INSERT INTO asignatura VALUES (28, 'Tecnologías web', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (29, 'Teoría de códigos y criptografía', 6, 'Optativa', 3, 1, NULL, 4);
  INSERT INTO asignatura VALUES (30, 'Administración de bases de datos', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (31, 'Herramientas y Métodos de Ingeniería del Software', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (32, 'Informática industrial y robótica', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (33, 'Ingeniería de Sistemas de Información', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (34, 'Modelado y Diseño del Software 2', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (35, 'Negocio Electrónico', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (36, 'Periféricos e interfaces', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (37, 'Sistemas de tiempo real', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (38, 'Tecnologías de acceso a red', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (39, 'Tratamiento digital de imágenes', 6, 'Optativa', 3, 2, NULL, 4);
  INSERT INTO asignatura VALUES (40, 'Administración de redes y sistemas operativos', 6, 'Optativa', 4, 1, NULL, 4);
  INSERT INTO asignatura VALUES (41, 'Almacenes de Datos', 6, 'Optativa', 4, 1, NULL, 4);
  INSERT INTO asignatura VALUES (42, 'Fiabilidad y Gestión de Riesgos', 6, 'Optativa', 4, 1, NULL, 4);
  INSERT INTO asignatura VALUES (43, 'Líneas de Productos Software', 6, 'Optativa', 4, 1, NULL, 4);
  INSERT INTO asignatura VALUES (44, 'Procesos de Ingeniería del Software 1', 6, 'Optativa', 4, 1, NULL, 4);
  INSERT INTO asignatura VALUES (45, 'Tecnologías multimedia', 6, 'Optativa', 4, 1, NULL, 4);
  INSERT INTO asignatura VALUES (46, 'Análisis y planificación de las TI', 6, 'Optativa', 4, 2, NULL, 4);
  INSERT INTO asignatura VALUES (47, 'Desarrollo Rápido de Aplicaciones', 6, 'Optativa', 4, 2, NULL, 4);
  INSERT INTO asignatura VALUES (48, 'Gestión de la Calidad y de la Innovación Tecnológica', 6, 'Optativa', 4, 2, NULL, 4);
  INSERT INTO asignatura VALUES (49, 'Inteligencia del Negocio', 6, 'Optativa', 4, 2, NULL, 4);
  INSERT INTO asignatura VALUES (50, 'Procesos de Ingeniería del Software 2', 6, 'Optativa', 4, 2, NULL, 4);
  INSERT INTO asignatura VALUES (51, 'Seguridad Informática', 6, 'Optativa', 4, 2, NULL, 4);
  INSERT INTO asignatura VALUES (52, 'Biologia celular', 6, 'Basica', 1, 1, NULL, 7);
  INSERT INTO asignatura VALUES (53, 'Física', 6, 'Basica', 1, 1, NULL, 7);
  INSERT INTO asignatura VALUES (54, 'Matemáticas I', 6, 'Basica', 1, 1, NULL, 7);
  INSERT INTO asignatura VALUES (55, 'Química general', 6, 'Basica', 1, 1, NULL, 7);
  INSERT INTO asignatura VALUES (56, 'Química orgánica', 6, 'Basica', 1, 1, NULL, 7);
  INSERT INTO asignatura VALUES (57, 'Biología vegetal y animal', 6, 'Basica', 1, 2, NULL, 7);
  INSERT INTO asignatura VALUES (58, 'Bioquímica', 6, 'Basica', 1, 2, NULL, 7);
  INSERT INTO asignatura VALUES (59, 'Genética', 6, 'Basica', 1, 2, NULL, 7);
  INSERT INTO asignatura VALUES (60, 'Matemáticas II', 6, 'Basica', 1, 2, NULL, 7);
  INSERT INTO asignatura VALUES (61, 'Microbiología', 6, 'Basica', 1, 2, NULL, 7);
  INSERT INTO asignatura VALUES (62, 'Botánica agrícola', 6, 'Obligatoria', 2, 1, NULL, 7);
  INSERT INTO asignatura VALUES (63, 'Fisiología vegetal', 6, 'Obligatoria', 2, 1, NULL, 7);
  INSERT INTO asignatura VALUES (64, 'Genética molecular', 6, 'Obligatoria', 2, 1, NULL, 7);
  INSERT INTO asignatura VALUES (65, 'Ingeniería bioquímica', 6, 'Obligatoria', 2, 1, NULL, 7);
  INSERT INTO asignatura VALUES (66, 'Termodinámica y cinética química aplicada', 6, 'Obligatoria', 2, 1, NULL, 7);
  INSERT INTO asignatura VALUES (67, 'Biorreactores', 6, 'Obligatoria', 2, 2, NULL, 7);
  INSERT INTO asignatura VALUES (68, 'Biotecnología microbiana', 6, 'Obligatoria', 2, 2, NULL, 7);
  INSERT INTO asignatura VALUES (69, 'Ingeniería genética', 6, 'Obligatoria', 2, 2, NULL, 7);
  INSERT INTO asignatura VALUES (70, 'Inmunología', 6, 'Obligatoria', 2, 2, NULL, 7);
  INSERT INTO asignatura VALUES (71, 'Virología', 6, 'Obligatoria', 2, 2, NULL, 7);
  INSERT INTO asignatura VALUES (72, 'Bases moleculares del desarrollo vegetal', 4.5, 'Obligatoria', 3, 1, NULL, 7);
  INSERT INTO asignatura VALUES (73, 'Fisiología animal', 4.5, 'Obligatoria', 3, 1, NULL, 7);
  INSERT INTO asignatura VALUES (74, 'Metabolismo y biosíntesis de biomoléculas', 6, 'Obligatoria', 3, 1, NULL, 7);
  INSERT INTO asignatura VALUES (75, 'Operaciones de separación', 6, 'Obligatoria', 3, 1, NULL, 7);
  INSERT INTO asignatura VALUES (76, 'Patología molecular de plantas', 4.5, 'Obligatoria', 3, 1, NULL, 7);
  INSERT INTO asignatura VALUES (77, 'Técnicas instrumentales básicas', 4.5, 'Obligatoria', 3, 1, NULL, 7);
  INSERT INTO asignatura VALUES (78, 'Bioinformática', 4.5, 'Obligatoria', 3, 2, NULL, 7);
  INSERT INTO asignatura VALUES (79, 'Biotecnología de los productos hortofrutículas', 4.5, 'Obligatoria', 3, 2, NULL, 7);
  INSERT INTO asignatura VALUES (80, 'Biotecnología vegetal', 6, 'Obligatoria', 3, 2, NULL, 7);
  INSERT INTO asignatura VALUES (81, 'Genómica y proteómica', 4.5, 'Obligatoria', 3, 2, NULL, 7);
  INSERT INTO asignatura VALUES (82, 'Procesos biotecnológicos', 6, 'Obligatoria', 3, 2, NULL, 7);
  INSERT INTO asignatura VALUES (83, 'Técnicas instrumentales avanzadas', 4.5, 'Obligatoria', 3, 2, NULL, 7);
  
  /* Curso escolar */
  INSERT INTO curso_escolar VALUES (1, 2014, 2015);
  INSERT INTO curso_escolar VALUES (2, 2015, 2016);
  INSERT INTO curso_escolar VALUES (3, 2016, 2017);
  INSERT INTO curso_escolar VALUES (4, 2017, 2018);
  INSERT INTO curso_escolar VALUES (5, 2018, 2019);
  
  /* Alumno se matricula en asignatura */
  INSERT INTO alumno_matricula_asignatura VALUES (1, 1, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (1, 2, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (1, 3, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (2, 1, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (2, 2, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (2, 3, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (4, 1, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (4, 2, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (4, 3, 1);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 1, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 2, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 3, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 4, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 5, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 6, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 7, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 8, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 9, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (24, 10, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 1, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 2, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 3, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 4, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 5, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 6, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 7, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 8, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 9, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (23, 10, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 1, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 2, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 3, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 4, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 5, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 6, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 7, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 8, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 9, 5);
  INSERT INTO alumno_matricula_asignatura VALUES (19, 10, 5);
~~~

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
  SELECT d.nombre, p.apellido1, p.apellido2, p.nombre
  FROM persona p
  LEFT JOIN profesor pr ON pr.profesor_id = p.id
  LEFT JOIN departamento d ON pr.departamento_id = d.id
  WHERE p.tipo = 'Profesor' AND d.id IS NULL
  ORDER BY d.nombre, p.apellido1, p.apellido2, p.nombre;
~~~
3. Devuelve un listado con los departamentos que no tienen profesores asociados.
~~~SQL
  SELECT d.nombre
  FROM departamento d
  LEFT JOIN profesor p ON d.id = p.departamento_id
  WHERE p.departamento_id IS NULL;
~~~
4. Devuelve un listado con los profesores que no imparten ninguna asignatura.
~~~SQL
  SELECT pr.nombre, pr.apellido1, pr.apellido2
  FROM persona pr
  LEFT JOIN profesor p ON p.profesor_id = pr.id
  LEFT JOIN asignatura a ON p.profesor_id = a.id_profesor
  WHERE a.id_profesor IS NULL AND pr.tipo = 'Profesor';
~~~
5. Devuelve un listado con las asignaturas que no tienen un profesor asignado.
~~~SQL
  SELECT a.nombre
  FROM profesor pr
  RIGHT JOIN asignatura a ON a.id_profesor = pr.profesor_id
  WHERE a.id_profesor IS NULL;
~~~
6. Devuelve un listado con todos los departamentos que tienen alguna asignatura que no se haya impartido en ningún curso escolar. El resultado debe mostrar el nombre del departamento y el nombre de la asignatura que no se haya impartido nunca.
~~~SQL
  SELECT DISTINCT d.nombre, d.id
  FROM departamento d
  INNER JOIN profesor pr ON pr.departamento_id = d.id
  INNER JOIN asignatura a ON pr.profesor_id = a.id_profesor
  INNER JOIN alumno_matricula_asignatura al ON al.asignatura_id = a.id
  LEFT JOIN curso_escolar c ON al.curso_id = c.id;
~~~

### **Consultas resumen**

1. Devuelve el número total de **alumnas** que hay.
~~~SQL
  SELECT COUNT(sexo) AS numero_alumnas
  FROM persona
  WHERE tipo = 'Alumno' AND sexo = 'M';
~~~
2. Calcula cuántos alumnos nacieron en 2005.
~~~SQL
  SELECT COUNT(tipo) AS numero_alumnos_nacidos_2005
  FROM persona
  WHERE tipo = 'Alumno' AND fecha_nacimiento > '2004/12/31' AND fecha_nacimiento < '2006/12/31';
~~~
3. Calcula cuántos profesores hay en cada departamento. El resultado sólo debe mostrar dos columnas, una con el nombre del departamento y otra con el número de profesores que hay en ese departamento. El resultado sólo debe incluir los departamentos que tienen profesores asociados y deberá estar ordenado de mayor a menor por el número de profesores.
~~~SQL
  SELECT COUNT(*), d.nombre
  FROM profesor p
  INNER JOIN departamento d ON d.id = p.departamento_id
  GROUP BY d.nombre
  ORDER BY COUNT(*) DESC;
~~~
4. Devuelve un listado con todos los departamentos y el número de profesores que hay en cada uno de ellos. Tenga en cuenta que pueden existir departamentos que no tienen profesores asociados. Estos departamentos también tienen que aparecer en el listado.
~~~SQL
  SELECT d.nombre, COUNT(p.departamento_id) 
  FROM departamento d
  LEFT JOIN profesor p ON d.id = p.departamento_id
  GROUP BY d.nombre
  ORDER BY COUNT(p.departamento_id) DESC;
~~~
5. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno. Tenga en cuenta que pueden existir grados que no tienen asignaturas asociadas. Estos grados también tienen que aparecer en el listado. El resultado deberá estar ordenado de mayor a menor por el número de asignaturas.
~~~SQL
~~~
6. Devuelve un listado con el nombre de todos los grados existentes en la base de datos y el número de asignaturas que tiene cada uno, de los grados que tengan más de `40` asignaturas asociadas.
~~~SQL
~~~
7. Devuelve un listado que muestre el nombre de los grados y la suma del número total de créditos que hay para cada tipo de asignatura. El resultado debe tener tres columnas: nombre del grado, tipo de asignatura y la suma de los créditos de todas las asignaturas que hay de ese tipo. Ordene el resultado de mayor a menor por el número total de crédidos.
~~~SQL
~~~
8. Devuelve un listado que muestre cuántos alumnos se han matriculado de alguna asignatura en cada uno de los cursos escolares. El resultado deberá mostrar dos columnas, una columna con el año de inicio del curso escolar y otra con el número de alumnos matriculados.
~~~SQL
~~~
9. Devuelve un listado con el número de asignaturas que imparte cada profesor. El listado debe tener en cuenta aquellos profesores que no imparten ninguna asignatura. El resultado mostrará cinco columnas: id, nombre, primer apellido, segundo apellido y número de asignaturas. El resultado estará ordenado de mayor a menor por el número de asignaturas.
~~~SQL
~~~
