<img width="1024" height="1024" alt="project_icon" src="https://github.com/user-attachments/assets/c36d25e4-adfc-4c7b-ac56-1e4097b7b057" />

# 🚪 La Puerta — Proxy Inverso Dinámico

**La Puerta** es un servidor proxy inverso ligero, basado en configuración, que enruta dinámicamente las solicitudes HTTP hacia servicios backend utilizando reglas basadas en rutas.

Está diseñado para ser simple, rápido y flexible, ideal para microservicios y entornos de desarrollo.

---

## ✨ Características

- Enrutamiento dinámico basado en rutas
- Configuración recargable en caliente (no requiere reinicio)
- Soporte para backends HTTP y HTTPS
- Soporte para WebSocket (WS) con transmisión bidireccional completa de solicitudes y respuestas
- Registro detallado (logging)
- Manejo de errores elegante

---

## 🧠 Cómo Funciona

**La Puerta** se sitúa entre los clientes y los servicios backend, reenviando inteligentemente las solicitudes según las reglas de enrutamiento definidas en un archivo de configuración.

### 1. Recepción de Solicitudes
- Escucha solicitudes HTTP en un puerto configurable (por defecto: `3000`)
- Registra cada solicitud entrante con marca de tiempo, método, URL e IP del cliente

### 2. Coincidencia de Rutas
- Extrae la ruta (pathname) de la URL solicitada  
- La compara con las rutas habilitadas
- Utiliza **coincidencia por ruta (path matching)**

### 3. Transformación de URL (Enrutamiento por Prefijo de Ruta)

- Utiliza la **ruta** configurada como un prefijo, no como un único endpoint
- Reenvía de forma transparente todas las subrutas anidadas al backend de destino
- Elimina el prefijo de ruta coincidente y agrega la ruta restante a la URL de destino
- Conserva automáticamente los parámetros de consulta y las rutas profundas

### 4. Reenvío de Solicitudes
- Soporta backends HTTP y HTTPS
- Conserva el método HTTP y el cuerpo de la solicitud
- Agrega encabezados `X-Forwarded-*`

### 5. Manejo de Respuestas
- Transmite las respuestas de vuelta al cliente
- Conserva los códigos de estado y los encabezados

### 6. Manejo de Errores
- `404` – No hay una ruta coincidente
- `502` – Backend inaccesible o tiempo de espera agotado

---

## 🔄 Configuración Dinámica

`config.json` se recarga automáticamente en caliente.  
Solo cambiar el puerto del servicio requiere un reinicio.

---

## ⚙️ Ejemplo de Configuración

```json
{
  "service-port": 3002,
  "routes": [
    {
      "path": "/api/users",
      "target": "http://localhost:3007",
      "enabled": true,
      "description": "API del servicio de usuarios"
    }
  ]
  
}
```

## 🚀 Primeros Pasos

```bash
git clone https://github.com/Melquiceded/La-Puerta---Dynamic-Reverse-Proxy.git
cd La-Puerta---Dynamic-Reverse-Proxy
npm install
npm run dev
```
