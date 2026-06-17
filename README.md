# ProVerif - modelo formal 5G EAP-TLS

## Introducción

Este Trabajo de Fin de Grado aborda el diseño y la validación formal de un modelo de seguridad para el protocolo de autenticación EAP-TLS en arquitecturas 5G. La evolución hacia sistemas 5G introduce una arquitectura mas flexible, virtualizada y basada en servicios, donde aparecen nuevas funciones de red encargadas de la autenticación, la protección y la validación de la identidad del usuario, asi como de la gestion del material criptografico.

El objetivo de este repositorio es ofrecer una versión simplificada y simbólica del protocolo, implementada en ProVerif, para analizar propiedades de confidencialidad, autenticación y acuerdo mutuo entre las entidades participantes.

## Estructura del repositorio

- `5G_EAP_TLS.pv`: modelo principal del protocolo.
- `test.pv` y `test2.pv`: modelos de prueba.
- `graphs_5G_TLS/`: grafos de trazas generados por ProVerif.
- `outputs/`: salidas de ejecución y resultados.

## Requisitos previos

Antes de trabajar con el modelo es recomendable usar WSL y acceder al directorio de trabajo del usuario en Linux, por ejemplo:

```bash
cd /home/usuario
mkdir -p Workspace/Proverif
cd Workspace/Proverif
```

## Instalación de ProVerif

Una vez ubicados en el directorio de trabajo, ejecuta los siguientes comandos:

```bash
sudo apt update
sudo apt install opam
opam init
eval $(opam env)
opam install proverif
opam depext proverif
```

Si es necesario, vuelve a cargar el entorno de opam con:

```bash
eval $(opam env)
```

## Ejecución del modelo

Para analizar el archivo principal del modelo, ejecuta ProVerif sobre el fichero `.pv`:

```bash
proverif 5G_EAP_TLS.pv
```

También puedes probar con los ficheros de ejemplo incluidos en el repositorio:

```bash
proverif test.pv
proverif test2.pv
```

## Generación de trazas y grafos

Cuando una `query` devuelve `false`, ProVerif permite generar grafos de la traza para inspeccionar el ataque o el contraejemplo encontrado. Para ello, usa la opción `-graph` indicando el directorio de salida y el archivo de entrada:

```bash
proverif -graph graphs_5G_TLS 5G_EAP_TLS.pv
```

El directorio `graphs_5G_TLS/` contiene ejemplos de grafos generados a partir de trazas (`trace1.dot`, `trace2.dot`).

## Nota sobre el modelo

El modelo no pretende reproducir al detalle la implementación real de EAP-TLS, sino modelar los elementos necesarios para el análisis simbólico de seguridad: entidades, canales, certificados, eventos, mensajes frescos y derivación de claves.

## Referencias

- ProVerif Manual: https://bblanche.gitlabpages.inria.fr/proverif/manual.pdf
- 3GPP TS 23.501 v19.6.0: https://www.etsi.org/deliver/etsi_ts/123500_123599/123501/19.06.00_60/ts_123501v190600p.pdf
