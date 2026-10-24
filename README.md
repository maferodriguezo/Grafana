# Demo Grafana: sismos del mundo en tiempo real

**Autor:** María Fernanda Rodríguez Ospina

**Materia:** Analitica de datos

## Descripción

Demostración de Grafana, una herramienta para visualizar datos, corriendo en un contenedor de Docker. El dashboard muestra los sismos de las últimas 24 horas con datos públicos del USGS (Servicio Geológico de Estados Unidos). No necesita crear ninguna base de datos.

El dashboard incluye:
- Un mapa con los sismos (el tamaño y el color indican la magnitud).
- El total de sismos y la magnitud máxima.
- Una tabla con los sismos más recientes.
- Actualización automática cada 24 horas.

## Contenido de la entrega

```
demo-grafana/
├── docker-compose.yml                  Configuración de Docker (levanta Grafana)
├── provisioning/
│   └── datasources/
│       └── infinity.yml                Fuente de datos que se crea sola al iniciar
├── dashboards/
│   └── Demo Grafana - Sismos.json        Dashboard para importar
└── README.md                           Este archivo
```

## Requisitos

- Docker Desktop instalado y abierto (esperar a que diga "Engine running").
- Conexión a internet.

## Cómo ejecutarlo

1. **Abrir una terminal dentro de la carpeta `demo-grafana`.**
   En Windows: abrir la carpeta en el Explorador, hacer clic en la barra de direcciones, escribir `cmd` y presionar Enter.

2. **Levantar Grafana:**
   ```
   docker compose up -d
   ```
   La primera vez tarda unos minutos porque descarga lo necesario.

3. **Abrir Grafana en el navegador:** http://localhost:3000
   No pide usuario ni contraseña.

4. **Importar el dashboard:**
   - Menú izquierdo: **Dashboards → New → Import**.
   - Clic en **Upload dashboard JSON file** y elegir `dashboards/Demo Grafana - Sismos.json`.
   - En la fuente de datos, seleccionar **Infinity**.
   - Clic en **Import**.

5. **Listo.** Se verá el mapa, los números y la tabla, actualizándose solos cada 24 horas.

## Para apagarlo

```
docker compose down
```

## Si algo falla

- **"error during connect":** Docker Desktop no está abierto. Abrirlo, esperar a que cargue y repetir el paso 2.
- **No aparece "Infinity" al importar:** esperar un minuto y ejecutar `docker compose restart`. Se necesita internet.
- **El puerto 3000 está ocupado:** en `docker-compose.yml` cambiar `"3000:3000"` por `"3001:3000"` y abrir http://localhost:3001.

## Fuente de los datos

USGS Earthquake Hazards Program:
https://earthquake.usgs.gov/earthquakes/feed/v1.0/summary/all_day.geojson

Los datos de sismos recientes son preliminares y pueden ser revisados.

