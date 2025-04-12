
# HERRAMIENTA DE AUDITORÍA SSH/TELNET

## Descripción
Esta herramienta permite realizar auditorías de seguridad a servicios SSH y Telnet, mediante la búsqueda de dispositivos expuestos en internet usando la API de Shodan y validación de credenciales por medio de pruebas de autenticación multihilo.

Incluye una interfaz gráfica construida con Tkinter, registro de logs, manejo de errores y carga de configuración por medio de variables de entorno.

---

## Configuración del Entorno

### 1. Crear entorno virtual (opcional pero recomendado)

```bash
# Crear entorno virtual
python -m venv venv

# Activar entorno virtual
source venv/bin/activate    # En Linux/Mac
venv\Scripts\activate       # En Windows

# Instalar bibliotecas clave
pip install -r requirements.txt
```

---

## Requisitos

- Python 3.8+
- API Key de [Shodan](https://account.shodan.io/)

### Dependencias
Instala las dependencias ejecutando:

```bash
pip install -r requirements.txt
```

Contenido de `requirements.txt` sugerido:

```text
tk
shodan
paramiko
python-dotenv
Exscript
tqdm
```

---

## Configuración

1. Crea un archivo `.env` en la misma carpeta del script con el siguiente contenido:

```env
SHODAN_API_KEY=tu_api_key_de_shodan
```

2. Asegúrate de tener conectividad a internet para realizar consultas con Shodan.

3. Verifica que los países permitidos y configuraciones estén definidos en la clase `Config` del código:

```python
ALLOWED_COUNTRIES = ["CO", "MX"]
MAX_THREADS = 15
SSH_TIMEOUT = 10
TELNET_TIMEOUT = 10
```

Puedes modificar estos valores según tu necesidad.

---

## Ejecución

Ejecuta el script principal:

```bash
python main.py
```

Se abrirá una interfaz gráfica con las siguientes opciones:
- Buscar dispositivos (puertos 22 y 23) usando Shodan.
- Cargar listas de IPs, usuarios y contraseñas desde archivos `.txt`.
- Iniciar pruebas de autenticación (SSH o Telnet).

---

## Estructura de Archivos

- `ssh_telnet3` : Script principal con interfaz gráfica.
- `.env` : Contiene la clave de la API de Shodan.
- `ips_encontradas.txt` : Dispositivos encontrados con IP, puerto y organización.
- `credenciales_validas.txt` : Registros exitosos de autenticación.
- `intentos_fallidos.log` : Fallos en autenticación.
- `auditoria.log` : Log completo de la ejecución.

---

## Ejemplo de Uso

### 1. Buscar Dispositivos
Haz clic en el botón "Buscar IPs (shodan)". Los resultados se guardarán en `ips_encontradas.txt`.

Ejemplo de línea en el archivo:

```
192.168.0.10|22|EmpresaX
```

### 2. Cargar Archivos

Prepara archivos `.txt` con una entrada por línea:

- IPs: `ips.txt` (puedes usar `ips_encontradas.txt` generado anteriormente)
- Usuarios: `usuarios.txt`
- Contraseñas: `contraseñas.txt`

Carga cada uno desde la interfaz.

### 3. Ejecutar Auditoría

Presiona el botón correspondiente para iniciar la auditoría SSH o Telnet. La herramienta intentará conectarse usando todas las combinaciones posibles.

Los resultados se guardarán en:
- `credenciales_validas.txt` si la autenticación fue exitosa.
- `intentos_fallidos.log` para errores de credenciales.
- `auditoria.log` : Log completo de la ejecución

---

## Advertencia Legal
Esta herramienta es solo para fines educativos y auditorías autorizadas. El uso no autorizado está penado por la ley. ¡Utiliza siempre con responsabilidad!

---

## Licencia
Software distribuido con fines educativos. Uso bajo tu propio riesgo.
