# 🔧 Configuración de Firebase para VOCCA

## Paso 1: Crear Proyecto Firebase

1. Ve a **https://console.firebase.google.com**
2. Haz clic en **"Crear proyecto"**
3. Nombre del proyecto: `vocca-pedidos` (o el que prefieras)
4. Acepta los términos y crea el proyecto

## Paso 2: Activar Realtime Database

1. En la consola Firebase, busca **"Realtime Database"** en el menú izquierdo
2. Haz clic en **"Crear base de datos"**
3. Selecciona región: **`europe-west1`** (Europa)
4. Modo de seguridad: **`Iniciar en modo de prueba`** (para desarrollo)
5. Haz clic en **"Habilitar"**

## Paso 3: Obtener Credenciales

1. Ve a **Configuración del proyecto** (⚙️ en la esquina superior)
2. Ve a la pestaña **"Mis aplicaciones"**
3. En la sección de Web apps, busca tu aplicación o crea una nueva (click en `</> Web`)
4. Copia el objeto `firebaseConfig` que aparece en el código

Debería verse así:
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyDxxxxxxxxxxxxxxxxxxxxxxx",
  authDomain: "tu-proyecto.firebaseapp.com",
  databaseURL: "https://tu-proyecto.firebaseio.com",
  projectId: "tu-proyecto-id",
  storageBucket: "tu-proyecto.appspot.com",
  messagingSenderId: "1234567890",
  appId: "1:1234567890:web:abcdefg1234567"
};
```

## Paso 4: Actualizar el Código

1. Abre tu archivo `index.html`
2. Busca la sección **"`Firebase Config`"** (alrededor de la línea 1263)
3. Reemplaza el `firebaseConfig` completo con el que copiaste
4. **Guarda el archivo**

## Paso 5: Deploy en Vercel

1. Haz commit de los cambios:
```bash
git add index.html
git commit -m "Configurar Firebase credentials"
git push
```

2. Vercel redesplegará automáticamente

## Paso 6: Crear Reglas de Seguridad (Opcional pero recomendado)

1. En Firebase Console, ve a **"Realtime Database"** → **"Reglas"**
2. Reemplaza con esto para desarrollo seguro:
```json
{
  "rules": {
    "orders": {
      ".read": true,
      ".write": true,
      ".indexOn": ["status", "createdAt"]
    }
  }
}
```

3. Haz clic en **"Publicar"**

## ✅ ¡Listo!

Ahora cuando:
- ✔️ Hagas un pedido desde el móvil → se guardará en Firebase
- ✔️ Abras el admin panel en el ordenador → verás los pedidos en tiempo real
- ✔️ Cambies el status de un pedido → se sincronizará automáticamente

> **🔒 Nota:** Para producción, implementa autenticación y reglas de seguridad más estrictas.

## 🆘 Solución de Problemas

**Problema:** "Firebase is not defined"
- **Solución:** Asegúrate de que los scripts de Firebase estén cargados en el `<head>`

**Problema:** "Pedidos no aparecen en el admin"
- **Solución:** Abre la consola del navegador (F12) y busca errores de Firebase
- Verifica que tu `apiKey` y `projectId` sean correctos

**Problema:** "Error de CORS"
- **Solución:** Las credenciales de Firebase incluyen restricciones automáticas, pero si tienes este problema, ve a Google Cloud Console y configura las restricciones de API correctamente
