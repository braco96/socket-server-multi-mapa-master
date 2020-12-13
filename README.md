# Mapa‑Socket‑Angular

Cliente frontend en **Angular** que utiliza Socket.IO para mostrar ubicaciones en tiempo real sobre mapas, conectado a un backend de sockets (por ejemplo el proyecto “socket‑server”).

> Aplicación de mapas del curso «Sockets con mapas» de Fernando Herrera.

---

## 🏗️ Características principales

- Visualización de usuarios/objetos en un mapa en tiempo real usando websockets.  
- Emisión de eventos de ubicación desde el cliente hacia el servidor y recepción de ubicaciones de otros usuarios desde el servidor.  
- Integración con Angular, socket‑io cliente (`ngx‑socket‑io`) y módulo de mapas (por ejemplo Google Maps, Mapbox o Leaflet).  
- Interfaz reactiva: cuando un usuario se mueve, todos los clientes conectados lo ven.

---

## 🚀 Cómo ejecutar (desarrollo)

```bash
git clone https://github.com/Klerith/mapa-socket-angular.git
cd mapa-socket-angular
npm install
ng serve
```

La aplicación arrancará en `http://localhost:4200`.  
El backend de sockets debe estar corriendo simultáneamente (por ejemplo en `http://localhost:5000`).

---

## 📁 Estructura del proyecto

```
src/
├─ app/
│  ├─ app.module.ts                # Configuración principal (socket + mapas)
│  ├─ services/
│  │   └─ websocket.service.ts     # Servicio de conexión con Socket.IO
│  └─ components/
│      └─ mapa/
│          ├─ mapa.component.ts
│          ├─ mapa.component.html
│          └─ mapa.component.css
├─ assets/
├─ environments/
│  ├─ environment.ts
│  └─ environment.prod.ts
├─ index.html                        # Incluye CDN de mapas o configuración de clave API
├─ styles.css
└─ …                                 # Otros archivos generados por Angular CLI
```

---

## 🔌 Configuración de socket + mapas

### Socket.IO

En `app/app.module.ts` encontrarás algo como:

```ts
import { SocketIoModule, SocketIoConfig } from 'ngx-socket-io';

const config: SocketIoConfig = {
  url: 'http://localhost:5000',     // Cambia al URL de tu backend
  options: {}
};
```

Asegúrate de ajustar el `url` al servidor de sockets que uses.

### Mapas

- El proyecto puede usar una librería de mapas como Mapbox, Leaflet o Google Maps.  
- Necesitas una **clave de API** si usas Google Maps o Mapbox.  
- Asegúrate de configurar los estilos, centrar el mapa, y suscribirte a eventos de ubicación desde el socket.

---

## 🔁 Flujo típico de uso

1. Cliente se conecta al backend de sockets.  
2. Cliente obtiene su ubicación (o ingresa manualmente).  
3. Cliente emite un evento con su ubicación, por ejemplo `ubicacion-nueva`.  
4. Backend difunde la ubicación a todos los clientes conectados.  
5. En la UI del cliente, se muestra el marcador de cada usuario en el mapa y se actualiza en tiempo real.

---

## 🧪 Prueba manual

- Asegúrate de que el backend está corriendo y conectado al cliente.  
- Desde otro dispositivo o pestaña del navegador accede al mismo cliente; realiza movimientos o cambios de ubicación.  
- Verifica que ambos clientes vean los marcadores de ubicación en tiempo real.

---

## ❗ Problemas comunes

- **El mapa no se muestra:** verifica la clave API, la importación del módulo de mapas, y que el contenedor `<div>` tenga estilo de altura definido.  
- **No hay conexión de socket:** revisa que la URL sea correcta, que CORS esté habilitado en el backend y que el puerto esté accesible.  
- **No aparecen otros usuarios en el mapa:** asegúrate de que el evento de ubicación se emita correctamente y que el cliente esté escuchando el evento adecuado.

---

## 📝 Licencia

MIT — Puedes usar, modificar y distribuir este proyecto libremente.

---
© 2025 Klerith
