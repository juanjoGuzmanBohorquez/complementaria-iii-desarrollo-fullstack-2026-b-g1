# Entity, Repository y CRUD — Sistema de Control de Asistencia

## 1. Modelo Entity

Para el sistema Attendance se utilizará la entidad **Attendance**, la cual representa el registro de asistencia de un estudiante a una clase.

Esta entidad será mapeada a una tabla en PostgreSQL utilizando JPA mediante las anotaciones `@Entity` y `@Id`.

## Entity: Attendance

```java
@Entity
public class Attendance {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private Long studentId;

    private Long classSessionId;

    private LocalDateTime checkInTime;

    private String status;

}
```

---

## Descripción de atributos

| Atributo | Tipo | Descripción |
|---|---|---|
| id | Long | Identificador único del registro de asistencia |
| studentId | Long | Identificador del estudiante que registra asistencia |
| classSessionId | Long | Identificador de la clase donde se registra asistencia |
| checkInTime | LocalDateTime | Fecha y hora del registro |
| status | String | Estado de la asistencia |

---

# 2. Mapeo Entity - Tabla

La entidad `Attendance` representa la siguiente tabla en la base de datos:

## Tabla: attendance

| Columna | Tipo | Descripción |
|---|---|---|
| id | BIGSERIAL | Clave primaria |
| student_id | BIGINT | ID del estudiante |
| class_session_id | BIGINT | ID de la clase |
| check_in_time | TIMESTAMP | Fecha y hora de registro |
| status | VARCHAR | Estado de asistencia |

Relación:

```text
Attendance Entity
        |
        |
        v

attendance Table
```

---

# 3. Repository

El Repository permite acceder a los datos almacenados en la tabla `attendance`.

Utiliza `JpaRepository`, el cual proporciona operaciones CRUD automáticamente.

## AttendanceRepository

```java
@Repository
public interface AttendanceRepository 
        extends JpaRepository<Attendance, Long> {

    List<Attendance> findByStudentId(Long studentId);

}
```

---

## Consulta personalizada por método

Método:

```java
findByStudentId(Long studentId)
```

Función:

Permite consultar todas las asistencias registradas por un estudiante específico.

Ejemplo:

```java
List<Attendance> asistencias =
attendanceRepository.findByStudentId(15L);
```

Resultado:

```text
Estudiante 15

- Clase Programación Móvil
- Clase Sistemas Operativos
- Clase Inteligencia de Negocios
```

---

# 4. Operaciones CRUD

CRUD representa las operaciones básicas que se pueden realizar sobre una entidad:

## Create (Crear)

Permite registrar una nueva asistencia cuando un estudiante escanea un código QR válido.

Ejemplo:

```java
attendanceRepository.save(attendance);
```

Uso:

- Crear un nuevo registro de asistencia.
- Guardar fecha y hora del ingreso.

---

## Read (Consultar)

Permite obtener información almacenada en la base de datos.

Ejemplos:

```java
attendanceRepository.findAll();
```

Obtiene todas las asistencias.

```java
attendanceRepository.findByStudentId(15L);
```

Obtiene el historial de asistencia de un estudiante.

Uso:

- Consultar historial del estudiante.
- Revisar asistencias de una clase.

---

## Update (Actualizar)

Permite modificar información existente de una asistencia.

Ejemplo:

```java
attendanceRepository.save(attendance);
```

Uso:

- Cambiar el estado de una asistencia.
- Corregir información registrada.

---

## Delete (Eliminar)

Permite eliminar un registro de asistencia.

Ejemplo:

```java
attendanceRepository.deleteById(id);
```

Uso:

- Eliminar registros incorrectos.
- Remover información inválida.

---

# Conclusión

La entidad `Attendance` permite representar los registros de asistencia dentro del sistema y mapearlos a una tabla en PostgreSQL.

El `AttendanceRepository`, mediante `JpaRepository`, facilita las operaciones de persistencia y proporciona métodos CRUD para crear, consultar, actualizar y eliminar información.

Esta estructura permite mantener separada la lógica de negocio y el acceso a datos, siguiendo buenas prácticas de desarrollo con Spring Boot y JPA.
