# RBA-Sim · Simulador de autenticación basada en riesgo

Proyecto del curso **Ingeniería de Software (CIB02)** · UNI-FIEE · 2026

Aplicación de escritorio que autentica usuarios evaluando el riesgo de cada intento de inicio de sesión (intentos fallidos, hora, IP y dispositivo simulados) y decide entre **permitir**, **pedir verificación adicional (OTP)** o **bloquear**.

## Integrantes

| Rol | Integrante | Módulo |
|-----|-----------|--------|
| I1 · Líder técnico y Base de datos | _(margaret porras)_ | Repo, BD, entidades, DAO |
| I2 · Criptografía y Registro | _(franco espinoza)_ | HashService, PasswordPolicy, registro |
| I3 · Motor de riesgo | _(arisky soto)_ | RiskEngine y 5 reglas |
| I4 · Sesiones y Auditoría | _(lindher)_ | AuthFacade, sesiones, OTP, auditoría |
| I5 · Interfaz JavaFX y Simulador | _(nombre)_ | UI y panel simulador |

## Tecnologías

| Aspecto | Detalle |
|---------|---------|
| Lenguaje / JDK | Java, JDK 21 |
| Interfaz | JavaFX (aplicación de escritorio) |
| Arquitectura | MVC + capa de servicios + DAO |
| Build | Maven |
| IDE | IntelliJ IDEA _(indicar versión exacta, ej. 2025.x)_ |
| Base de datos | Microsoft SQL Server, vía `mssql-jdbc` y `PreparedStatement` |
| Pruebas | JUnit 5 |
| Diagramas | Visual Paradigm (`.vpp` en `/docs`) |

## Estructura del repositorio

```
Simulador_RBA/
├── pom.xml
├── README.md
├── db-backup/     Backup .bak de SQL Server (o RUTA.txt con el enlace)
├── database/      01_schema.sql, 02_seed.sql
├── docs/          Documento de sustentación y diagramas (.vpp)
└── src/           Código fuente (main y test)
```

## Backup de la base de datos

- Carpeta: [`/db-backup`](db-backup/)
- Archivo: `RBA_SIM.bak` _(o el enlace de descarga dentro de `db-backup/RUTA.txt` si supera el límite de GitHub)_
- Motor: Microsoft SQL Server. Base de datos: `RBA_SIM`.

Para restaurarlo con T-SQL (ajusta la ruta):

```sql
RESTORE DATABASE RBA_SIM
FROM DISK = 'C:\ruta\al\RBA_SIM.bak'
WITH REPLACE;
```

También puede restaurarse desde SSMS: clic derecho en *Databases* → *Restore Database…* → *Device*.

## Crear la base de datos desde cero (desarrollo)

1. Abrir **SQL Server Management Studio** y conectarse a la instancia local.
2. Ejecutar `database/01_schema.sql` (crea `RBA_SIM` y las 9 tablas).
3. Ejecutar `database/02_seed.sql` (2 admins, 5 usuarios, 3 IP en lista negra, 5 reglas).
4. Copiar `src/main/resources/pe/uni/fiee/rbasim/config.properties.example` como `config.properties` y completar la URL y el usuario de tu instancia.

Usuarios de prueba: ver el encabezado de `database/02_seed.sql`.

## Cómo ejecutar

_(Se completa al cierre del Sprint 4: `mvn clean package` y `java -jar target/rba-sim.jar`.)_

## Flujo de ramas

`main` (estable) ← `develop` (integración, solo por Pull Request) ← `feature/<modulo>` (trabajo diario de cada integrante).
Commits con prefijo `feat:`, `fix:`, `test:` o `docs:`.
