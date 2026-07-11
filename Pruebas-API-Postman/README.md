# ⚡ Pruebas de API (Backend Testing) con Postman

En este directorio se documenta la estrategia de validación, diseño de escenarios funcionales y ejecución de pruebas sobre la capa de servicios (API REST), garantizando la correcta comunicación entre el frontend, las reglas de negocio y la base de datos.

---

## 🚀 Alcance de las Pruebas (Ecosistema CRUD)

Para validar el ciclo de vida completo de los recursos en el servidor, se diseñó y ejecutó una suite de pruebas manuales organizada mediante colecciones utilizando los siguientes métodos HTTP:

* **POST / Create:** Verificación de la creación de registros, validando el procesamiento de cargas útiles (*payloads* o JSON bodies) correctas y el manejo de excepciones ante datos duplicados o faltantes.
* **GET / Read:** Validación de consultas de datos, asegurando la correcta recuperación de colecciones completas o registros individuales mediante parámetros de ruta (*Path Variables*) o de consulta (*Query Params*).
* **PUT / Update:** Pruebas de modificación o actualización integral de datos existentes, verificando la integridad de la persistencia de datos post-petición.
* **DELETE / Delete:** Confirmación de la eliminación controlada de registros en el servidor, asegurando que los recursos dejen de ser accesibles.

---

## 🛠️ Validaciones y Criterios Técnicos Evaluados

Durante la ejecución de las colecciones en Postman, cada petición fue auditada bajo los siguientes estándares de aceptación:

1. **Códigos de Estado HTTP (Status Codes):**
   * `200 OK` / `201 Created` para flujos exitosos (*Happy Paths*).
   * `400 Bad Request` / `401 Unauthorized` / `404 Not Found` para flujos alternativos y validaciones de frontera.
2. **Estructura y Tipado de Datos:** Verificación de que el cuerpo de la respuesta (*Response Body*) cumpla con el formato JSON requerido y que las claves contengan los tipos de datos correctos (strings, integers, booleans).
3. **Manejo de Errores:** Validación de que los mensajes de error devueltos por la API sean claros, descriptivos y consistentes para evitar comportamientos inesperados en la interfaz de usuario.
4. **Tiempos de Respuesta (Performance Base):** Monitoreo de latencia en los endpoints clave para identificar degradaciones en el servicio.

---

## 📂 Organización de la Suite en Postman
* **Colecciones (Collections):** Segmentadas por módulos lógicos y flujos de negocio (ej. Autenticación, Gestión de Usuarios).
* **Variables de Entorno (Environments):** Uso de variables parametrizadas (como `{{base_url}}` y tokens de autenticación dinámicos) para asegurar la portabilidad y escalabilidad de las pruebas en distintos ambientes (QA, Staging, Dev).
