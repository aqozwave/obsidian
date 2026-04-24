
> [!info] Registro > Permite la creacion de un usuario que tendra accesos definidos como admin o user [[ROLES]].Debera tener asociada una empresa y ubicacion, ademas necesita confirmacion por correo para acceder

> [!warning] Atención > Si existe un tripulante con el mismo run , se enviara una notificacion donde se puede asociar con dicho tripulante o no

> [!warning] Atención > La foto de profile se podra cargar en el modulo de profile o modulo de actualizacion del usuario


**importante**  
*Correos Validos*

[[Controllers]]
[[Routes]]
[[Services]]
[[Model]]
[[Middlewares]]
 
## [[Functions Auth]]

## Associate
Este modulo depende del [[Modulo User]] valida que exista el usuario regitrado
Al Crear un usuario se enviara un #SendEmailNotifications notificando y solicitando confirmacion para habilitar esta cuenta


1.-Primero, el flujo de **registro y confirmación de cuenta**, que es el más complejo porque involucra un email de verificación
![[Pasted image 20260424124903.png]]

2.-Ahora el flujo de **login y logout**, que es el más usado en el día a día:
![[Pasted image 20260424124947.png]]

Y por último el flujo de **reseteo de clave**, que tiene su propia lógica con token temporal

![[Pasted image 20260424125018.png]]


**Seguridad crítica:** La respuesta al reseteo de clave siempre debe ser la misma ("Si el email existe, recibirás un enlace"), independiente de si el email está registrado o no. Esto evita que un atacante pueda enumerar usuarios registrados.

**Tokens:** Tanto el de confirmación de cuenta como el de reseteo deben ser de un solo uso — una vez usados, se eliminan o marcan como consumidos. El de confirmación puede durar 24h; el de reseteo conviene reducirlo a 1h.

**JWT en login:** Lo recomendable es manejar un `access_token` de vida corta (ej. 15 min) y un `refresh_token` de vida larga (ej. 7 días). El logout puede ser solo cliente (eliminar tokens del storage) o también invalidar el refresh token en el servidor usando una lista negra o tabla de tokens revocados.

**Rate limiting:** En el endpoint de login es importante limitar intentos fallidos por IP para evitar ataques de fuerza bruta.

[[API - REST  -Nachipa Wellboats🔥🚀]]