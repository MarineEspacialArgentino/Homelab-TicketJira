# Caso 01: Cuenta bloqueada y reseteo de contraseña

**Tipo:** Incidente | **Prioridad:** Media

## Resumen
Un usuario de Contabilidad no puede iniciar sesión. Tras diagnosticar, se confirma
que la cuenta quedó bloqueada por intentos fallidos de contraseña. Se verifica su
identidad, se desbloquea la cuenta y se restablece la contraseña.

## Problema reportado
El usuario escribió: "No puedo entrar a mi cuenta, creo que me olvidé de la contraseña."

![Ticket](img/01-Informacion-del-Ticket.png)

## Diagnóstico
1. Pedí al usuario más información y una verificación de identidad (legajo y jefe directo).
2. Una vez validada la identidad, revisé el estado de la cuenta en Active Directory.
3. Confirmé que estaba bloqueada (`LockedOut: True`).
4. En el Visor de eventos del controlador de dominio encontré el evento 4740, que
   indica el bloqueo y desde qué equipo se originó.

![Verificación de identidad y Conversacion con el Usuario](img/02-Verificación-de-identidad-y-Conversacion-con-el-Usuario.png)
![Cuenta bloqueada en AD](img/03-Cuenta-del-Usuario-Bloqueada.png)
![Evento 4740](img/04-Visor-de-Eventos-de-la-cuenta-bloqueada.png)

## Solución
1. Desbloqueé la cuenta desde Usuarios y equipos de Active Directory.
2. Restablecí la contraseña con la opción de cambio obligatorio en el próximo inicio de sesión.

![Desbloqueo y Reseteo de la Contraseña](img/05-Desbloqueando-Cuenta.png)

## Resultado
Probé el inicio de sesión desde la VM cliente: el sistema pidió cambiar la contraseña
y el acceso funcionó. El ticket se cerró con resolución **Done**.


## Aprendizaje
- Un "olvidé mi contraseña" no siempre es lo que parece: conviene verificar el estado de la cuenta.
- Verifiqué la identidad antes de modificar la cuenta.
