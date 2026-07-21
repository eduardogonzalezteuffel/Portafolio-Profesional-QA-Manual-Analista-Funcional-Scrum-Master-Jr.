# 📑 Historia de Usuario: Registro de Nuevo Usuario

**ID:** US-001  
**Título:** Implementación de registro con validación de seguridad.

---

## 📝 Descripción
**Como** usuario interesado en el portal,  
**Quiero** registrarme mediante un formulario ingresando mi nombre, email y contraseña,  
**Para** acceder a las funcionalidades exclusivas de la plataforma.

---

## ✅ Criterios de Aceptación (Formato BDD / Gherkin)

### Escenario 1: Validación de formato de Email invalido
* **Dado** que el usuario se encuentra en la pantalla de registro,
* **Cuando** ingresa un correo con formato inválido (ej: "usuario@dominio") e intenta registrarse,
* **Entonces** el sistema debe impedir el registro y mostrar el mensaje de validación correspondiente.

### Escenario 2: Robustez de la Contraseña
* **Dado** que el usuario completa el formulario,
* **Cuando** ingresa una contraseña que no cumple con el mínimo de 8 caracteres, una mayúscula y un número,
* **Entonces** el sistema debe deshabilitar el botón de envío y alertar los requisitos faltantes.

### Escenario 3: Registro Exitoso y Redirección (Happy Path)
* **Dado** que el usuario ingresa todos los campos con datos válidos y únicos,
* **Cuando** hace clic en el botón "Registrarse",
* **Entonces** el sistema debe procesar la solicitud, redirigir al Dashboard en menos de 2 segundos y enviar el correo de bienvenida.

### Escenario 4: Control de Duplicidad (Email existente)
* **Dado** que el correo ingresado ya se encuentra registrado en el sistema,
* **Cuando** el usuario intenta enviar el formulario,
* **Entonces** el sistema debe abortar la operación y mostrar el mensaje de alerta: *"Este correo ya se encuentra registrado"*.

* ![Diagrama BPMN 2.0 - Registro de Usuario](./Diagramapng)

---

## ⚙️ Notas Técnicas y Persistencia (Backend & SQL)
* **Cifrado:** Las contraseñas deben persistir en la base de datos aplicando algoritmos de hash seguros (SHA-256 o bcrypt) antes de su inserción.
* **Verificación de Persistencia (QA/SQL):** Para validar que el registro se realizó correctamente en la base de datos, ejecutar el siguiente query de verificación:
  ```sql
  SELECT id, nombre, email, creado_en 
  FROM usuarios 
  WHERE email = 'usuario@dominio.com';
