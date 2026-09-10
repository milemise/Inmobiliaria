Sistema de Gestión Inmobiliaria
Plataforma integral de administración de propiedades basada en el patrón Modelo-Vista-Controlador (MVC). Este sistema automatiza la gestión de propietarios, inquilinos, inmuebles y alquileres, garantizando la integridad de los datos mediante validaciones cruzadas y un flujo de seguridad estricto. El proyecto fue diseñado con un enfoque fuerte en la experiencia de usuario (UX) y la escalabilidad del backend.

Tecnologías Utilizadas
Backend: C#, ASP.NET Core MVC 8.0

Persistencia de Datos: MySQL 8.0+, Entity Framework Core 9.0 (Code-First)

Arquitectura: Patrón Repositorio Genérico, Inyección de Dependencias.

Frontend: HTML5, CSS3, JavaScript (Vanilla), Bootstrap 5, FontAwesome.

Funcionalidades Implementadas (Fase 1)
Prevención de Superposición de Fechas: Algoritmo lógico en el controlador que intercepta las peticiones de nuevos alquileres, evaluando si el inmueble ya posee un registro activo en el rango de fechas seleccionado.

Trazabilidad y Auditoría Automática: Captura invisible del contexto de sesión (User.Identity.Name) para registrar de manera automática qué usuario crea o modifica entidades en la base de datos.

Seguridad Interactiva (UX): Interfaz que exige la confirmación manual explícita (ingresando comandos de seguridad como "ELIMINAR") antes de ejecutar operaciones destructivas.

Validación de Integridad: Bloqueo automático de eliminación de inmuebles o inquilinos que posean un historial de operaciones o pagos activos.

Roadmap y Refactorización (Fase 2)
Actualmente, el sistema se encuentra en un ciclo de refactorización arquitectónica para optimizar el rendimiento y adaptarse al modelo de alquileres temporales. Las siguientes mejoras están en desarrollo activo:

Migración a Sistema de Reservas: Refactorización del módulo histórico de Contratos hacia Reservas temporales, ajustando la lógica de fechas y cálculo de montos para estadías cortas.

Vistas Dinámicas (ABM): Reemplazo de formularios estáticos por carga dinámica desde la base de datos (Ej: Entidad TipoInmueble), utilizando ViewBag para permitir una escalabilidad total sin necesidad de modificar el código fuente HTML.

Optimización de Rendimiento (LINQ): Modificación del Repositorio Genérico para utilizar IQueryable en lugar de materializar los datos en memoria (GetAllAsync). Esto delegará el filtrado y la paginación al motor SQL, evitando picos de consumo de RAM en el servidor.

Eager Loading: Implementación del método .Include() de Entity Framework para solucionar el problema de consultas N+1 en las vistas de listado, obteniendo las entidades relacionadas en una sola petición SQL optimizada.

Instalación y Despliegue Local
Clonar el repositorio.

Actualizar la cadena de conexión (DefaultConnection) en el archivo appsettings.json con las credenciales de tu servidor MySQL.

Abrir la terminal en la raíz del proyecto y ejecutar las migraciones para construir la base de datos:

Bash
dotnet ef database update
Ejecutar la aplicación:

Bash
dotnet run
