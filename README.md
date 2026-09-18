# Prueba Técnica SQL Server

Solución de prueba técnica desarrollada en **SQL Server**, orientada a la gestión de departamentos, empleados y proyectos.

El proyecto incluye creación de base de datos, tablas relacionadas, datos de prueba, consultas SQL, procedimiento almacenado, función escalar e índice no clusterizado.

## Tecnologías

- SQL Server
- SQL Server Management Studio (SSMS)
- T-SQL

## Base de datos

Nombre de la base de datos:

```text
EmpresaDB
```

## Estructura de la base de datos

La base de datos está compuesta por las siguientes tablas:

```text
EmpresaDB
│
├── Departamentos
├── Empleados
├── Proyectos
└── EmpleadoProyecto
```

### Departamentos

Contiene los departamentos de la empresa.

| Campo | Tipo | Descripción |
|---|---|---|
| IdDepartamento | INT | Identificador del departamento |
| Nombre | VARCHAR(100) | Nombre del departamento |

### Empleados

Contiene la información de los empleados.

| Campo | Tipo | Descripción |
|---|---|---|
| IdEmpleado | INT | Identificador del empleado |
| Nombre | VARCHAR(100) | Nombre |
| Apellido | VARCHAR(100) | Apellido |
| Email | VARCHAR(150) | Correo electrónico |
| FechaIngreso | DATE | Fecha de ingreso |
| IdDepartamento | INT | Departamento al que pertenece |

### Proyectos

Contiene los proyectos de la empresa.

| Campo | Tipo | Descripción |
|---|---|---|
| IdProyecto | INT | Identificador del proyecto |
| Nombre | VARCHAR(150) | Nombre del proyecto |
| Presupuesto | DECIMAL(18,2) | Presupuesto asignado |
| FechaInicio | DATE | Fecha de inicio |

### EmpleadoProyecto

Tabla intermedia que representa la relación muchos a muchos entre empleados y proyectos.

| Campo | Tipo | Descripción |
|---|---|---|
| IdEmpleado | INT | Identificador del empleado |
| IdProyecto | INT | Identificador del proyecto |

La clave primaria está compuesta por:

```text
(IdEmpleado, IdProyecto)
```

## Datos de prueba

La solución incluye datos de prueba para:

- 6 departamentos.
- 5 empleados.
- 5 proyectos.
- 10 relaciones entre empleados y proyectos.

## Consultas SQL

El script incluye las siguientes consultas requeridas:

### 1. Empleados con su departamento

Obtiene todos los empleados junto con el departamento al que pertenecen.

### 2. Proyectos y cantidad de empleados

Obtiene cada proyecto, su presupuesto y la cantidad de empleados asociados.

### 3. Top 3 empleados con más proyectos

Obtiene los tres empleados con mayor cantidad de proyectos asignados.

### 4. Departamentos sin empleados

Identifica los departamentos que actualmente no tienen empleados asociados.

### 5. Empleados con más de un proyecto

Obtiene los empleados que participan en más de un proyecto.

## Procedimiento almacenado

Se implementó:

```text
sp_buscar_empleado
```

Recibe como parámetro el nombre del empleado y devuelve:

- IdEmpleado
- Nombre
- Apellido
- Email
- FechaIngreso
- IdDepartamento
- Departamento

Ejemplo de ejecución:

```sql
EXEC sp_buscar_empleado 'Carlos';
```

La búsqueda permite coincidencias parciales en el nombre.

## Función escalar

Se implementó:

```text
fn_total_proyectos
```

Recibe el `IdEmpleado` y devuelve la cantidad de proyectos en los que participa.

Ejemplo:

```sql
SELECT dbo.fn_total_proyectos(1) AS TotalProyectos;
```

## Índice

Se creó un índice no clusterizado sobre el campo `Apellido` de la tabla `Empleados`:

```text
IX_Empleados_Apellido
```

Esto permite optimizar consultas que realicen búsquedas o filtrados por apellido.

## Backup y Restore

Se recomienda realizar backups periódicos de la base de datos mediante `BACKUP DATABASE`, almacenando los archivos `.bak` en una ubicación segura.

Para recuperación se utilizaría `RESTORE DATABASE` a partir del backup disponible. Según la criticidad de la información, se pueden complementar los backups completos con diferenciales y de log.

Los backups deben validarse periódicamente mediante restauraciones de prueba y mantenerse copias fuera del servidor principal.

## Instalación y ejecución

### Requisitos

- SQL Server 2019 o superior.
- SQL Server Management Studio (SSMS).

### 1. Descargar o clonar el repositorio

```bash
git clone URL_DEL_REPOSITORIO
```

### 2. Abrir el script

Abrir el archivo:

```text
EmpresaDB.sql
```

utilizando SQL Server Management Studio.

### 3. Ejecutar el script

Ejecutar el script completo desde SSMS.

El script se encarga de crear:

- Base de datos `EmpresaDB`.
- Tablas.
- Relaciones entre tablas.
- Datos de prueba.
- Consultas solicitadas.
- Procedimiento almacenado.
- Función escalar.
- Índice no clusterizado.

## Estructura del repositorio

```text
prueba-tecnica-sql
│
├── EmpresaDB.sql
└── README.md
```

## Nota

La solución está orientada a cumplir los requerimientos funcionales de la prueba técnica y puede ejecutarse directamente sobre una instancia de SQL Server compatible.

## Autor

Carlos Toro
