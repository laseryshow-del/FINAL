# Guía de Configuración de Google Tag Manager (GTM)

## 📋 Índice

1. [Descripción General](#descripción-general)
2. [Archivos de Configuración](#archivos-de-configuración)
3. [Requisitos Previos](#requisitos-previos)
4. [Valores de Configuración](#valores-de-configuración)
5. [Eventos Configurados](#eventos-configurados)
6. [Variables y Constantes](#variables-y-constantes)
7. [Triggers (Disparadores)](#triggers-disparadores)
8. [Instrucciones de Implementación](#instrucciones-de-implementación)
9. [Personalización para Tu Proyecto](#personalización-para-tu-proyecto)
10. [Validación y Pruebas](#validación-y-pruebas)

---

## 📖 Descripción General

Esta configuración de Google Tag Manager incluye dos contenedores:

- **Contenedor del Servidor** (`GTM-T2ZQP7WV`): Maneja el seguimiento server-side para Meta Conversion API, Google Analytics 4 y Google Ads
- **Contenedor Web** (`GTM-TNM9JZ3S`): Maneja el seguimiento client-side en el navegador del usuario

La configuración utiliza [Stape.io](https://stape.io) como servidor de GTM para procesar eventos server-side, mejorando la precisión del seguimiento y reduciendo el impacto de bloqueadores de anuncios.

---

## 📁 Archivos de Configuración

### 1. GTM-T2ZQP7WV_workspace77.json
**Tipo:** Contenedor del Servidor
**Contenido:**
- 21 Tags (etiquetas)
- 32 Variables
- 18 Triggers (disparadores)
- 5 Clients (clientes)
- 4 Folders (carpetas organizativas)

### 2. GTM-TNM9JZ3S_v46.json
**Tipo:** Contenedor Web
**Contenido:**
- 56 Tags (etiquetas)
- 35 Variables
- 18 Triggers (disparadores)
- 5 Folders (carpetas organizativas)

---

## ✅ Requisitos Previos

Para implementar esta configuración necesitas:

### Cuentas y Accesos
1. **Cuenta de Google Tag Manager**
   - Acceso a nivel de contenedor (editar/publicar)

2. **Cuenta de Meta/Facebook Business**
   - Facebook Pixel ID
   - Meta Conversion API Access Token
   - Permisos de administrador en el Pixel

3. **Cuenta de Google Analytics 4**
   - Measurement ID (formato: G-XXXXXXXXXX)
   - Permisos de administrador

4. **Cuenta de Google Ads** (opcional)
   - Conversion ID (formato: AW-XXXXXXXXXX)
   - Conversion Labels para cada tipo de evento

5. **Servidor GTM (Stape.io o Custom)**
   - URL del servidor configurada
   - Dominio personalizado configurado (recomendado)

### Conocimientos Técnicos
- Conceptos básicos de Google Tag Manager
- Comprensión de eventos web y tracking
- Acceso al código fuente del sitio web para implementar dataLayer

---

## 🔧 Valores de Configuración

### Valores Reales Configurados

Estos valores ya están configurados en los archivos JSON. **IMPORTANTE:** Son valores de ejemplo/producción que debes reemplazar con tus propios valores:

| Variable | Valor Actual | Descripción | Ubicación |
|----------|-------------|-------------|-----------|
| **Facebook Pixel ID** | `25699472449663830` | ID del Pixel de Meta/Facebook | Variable ID: 106, 166 |
| **Meta CAPI Token** | `EAA0D5fYG7HQ...` | Token de acceso para Conversion API | Variable ID: 109, 165 |
| **GA4 Measurement ID** | `G-J4JTN4JRE0` | ID de medición de Google Analytics 4 | Variable ID: 129 |
| **Cookie Domain** | `laserman.com.ar` | Dominio para cookies de seguimiento | Variable ID: 107 |
| **Stape Server URL** | `https://marremix.laserman.com.ar` | URL del servidor GTM | Variable ID: 103 |
| **Currency Default** | `ARS` | Moneda predeterminada (Pesos Argentinos) | Web Container |

⚠️ **ADVERTENCIA DE SEGURIDAD:** Los tokens y IDs mostrados arriba son ejemplos reales que deben ser reemplazados con tus propios valores. Nunca compartas tokens de acceso públicamente.

### Valores de Ejemplo para Google Ads

Estos valores han sido configurados como ejemplos y **DEBEN ser reemplazados** con tus propios valores de Google Ads:

| Variable | Valor de Ejemplo | Descripción | Variable ID |
|----------|-----------------|-------------|-------------|
| **Google Ads Conversion ID** | `AW-1234567890` | ID de conversión de Google Ads | 164 |
| **Schedule Conversion Label** | `aBcDeFgHiJkLmNoPqR` | Etiqueta para conversiones programadas | 163 |
| **Lead Conversion Label** | `xYzAbC1234dEfGh5Ij` | Etiqueta para eventos de Lead | 167 |
| **Contact Conversion Label** | `kLmN6oPqR789sTuVwX` | Etiqueta para eventos de Contacto | 168 |

#### ¿Dónde encontrar tus valores de Google Ads?

1. Inicia sesión en [Google Ads](https://ads.google.com)
2. Ve a **Herramientas y configuración** > **Medición** > **Conversiones**
3. Selecciona la conversión que deseas rastrear
4. En los detalles, encontrarás:
   - **Conversion ID:** Formato `AW-XXXXXXXXXX`
   - **Conversion Label:** Una cadena alfanumérica única

---

## 🎯 Eventos Configurados

### Contenedor del Servidor (Server-Side)

#### Meta Conversion API (CAPI) Tags

| Tag ID | Nombre | Evento | Trigger | Descripción |
|--------|--------|--------|---------|-------------|
| 111 | Meta CAPI - Lead | `Lead` | CE - generate_lead | Envía evento de generación de lead a Meta |
| 116 | Meta CAPI - Lead DK | `Lead` | CE - generate_lead | Versión alternativa con configuración DK |
| 122 | Meta CAPI - Contact | `Contact` | CE - contact | Envía evento de contacto a Meta |
| 124 | Meta CAPI - PageView | `PageView` | CE - page_view | Envía vistas de página a Meta |
| 128 | Meta CAPI - Purchase | `Purchase` | CE - purchase | Envía evento de compra a Meta |
| 130 | Meta CAPI - ViewContent Home | `ViewContent` | CE - view_content_home | Vista de contenido (página principal) |
| 120 | Meta CAPI - ViewContent Show | `ViewContent` | CE - view_content_show | Vista de contenido (página de show) |
| 133 | Meta CAPI - Video Play | Custom | CE - video_play | Reproducción de video |
| 136 | Meta CAPI - Video Complete | Custom | CE - video_complete | Video completado |
| 140 | Meta CAPI - Section View | Custom | CE - section_view | Vista de sección |
| 141 | Meta CAPI - Segment Click | Custom | CE - segment_click | Click en segmento |

#### Google Ads Tags (Stape)

| Tag ID | Nombre | Evento | Descripción |
|--------|--------|--------|-------------|
| 169 | [Stape] GADS - Schedule | Schedule | Conversión programada de Google Ads |
| 173 | [Stape] GADS - Lead | Lead | Conversión de Lead |
| 178 | [Stape] GADS - Contact | Contact | Conversión de Contacto |
| 174 | [Stape] GADS - Conversion Linker | All | Vinculador de conversiones |
| 176 | [Stape] GADS - Remarketing | All | Tag de remarketing |

#### Google Analytics 4 Tags (Stape)

| Tag ID | Nombre | Evento | Descripción |
|--------|--------|--------|-------------|
| 171 | [Stape] GA4 - Base | All | Configuración base de GA4 |

#### Meta Tags (Stape)

| Tag ID | Nombre | Evento | Descripción |
|--------|--------|--------|-------------|
| 170 | [Stape] Meta - Lead | Lead | Lead a través de Stape |
| 175 | [Stape] Meta - PageView | PageView | PageView a través de Stape |
| 177 | [Stape] Meta - Contact | Contact | Contact a través de Stape |
| 172 | [Stape] Meta - Schedule | Schedule | Evento programado |

### Contenedor Web (Client-Side)

El contenedor web contiene 56 tags que incluyen:
- Tags de Google Analytics 4 para eventos principales
- Tags de Facebook Pixel
- Eventos personalizados del dataLayer
- Tags de remarketing
- Configuraciones de consentimiento

---

## 📊 Variables y Constantes

### Variables de Event Data (ED)

Estas variables extraen datos del evento recibido:

| Variable ID | Nombre | Tipo | Extrae |
|------------|--------|------|---------|
| 50 | ED - em | Event Data | Email del usuario |
| 51 | ED - ph | Event Data | Teléfono del usuario |
| 52 | ED - fn | Event Data | Nombre (first name) |
| 53 | ED - ln | Event Data | Apellido (last name) |
| 55 | ED - fbp | Event Data | Facebook Browser Pixel cookie |
| 56 | ED - User Agent | Event Data | User Agent del navegador |
| 63 | ED - fbc | Event Data | Facebook Click ID cookie |
| 104 | ED - page_location | Event Data | URL de la página |
| 105 | ED - currency | Event Data | Código de moneda |
| 110 | ED - event_id | Event Data | ID único del evento |
| 123 | ED - value | Event Data | Valor monetario del evento |
| 126 | ED - IP Address | Event Data | Dirección IP del usuario |
| 127 | ED - content_name | Event Data | Nombre del contenido |
| 132 | ED - video_id | Event Data | ID del video |
| 135 | ED - video_percent | Event Data | Porcentaje de video visto |
| 138 | ED - segment_type | Event Data | Tipo de segmento |

### Constantes (CONST)

Valores de configuración estáticos:

| Variable ID | Nombre | Valor | Uso |
|------------|--------|-------|-----|
| 103 | CONST - Stape Server URL | `https://marremix.laserman.com.ar` | URL del servidor Stape |
| 106 | CONST - Facebook Pixel ID | `25699472449663830` | ID del Pixel de Facebook |
| 107 | CONST - Cookie Domain | `laserman.com.ar` | Dominio para cookies |
| 109 | CONST - FB API Access Token | `EAA0D5fYG7HQ...` | Token de Meta CAPI |
| 129 | CONST - GA4 Measurement ID | `G-J4JTN4JRE0` | ID de GA4 |

### Constantes de Google Ads (const - lowercase)

| Variable ID | Nombre | Valor (Ejemplo) | Descripción |
|------------|--------|----------------|-------------|
| 163 | const - gads_schedule_conversion_label | `aBcDeFgHiJkLmNoPqR` | Etiqueta de conversión programada |
| 164 | const - gads_conversion_id | `AW-1234567890` | ID de conversión de Google Ads |
| 165 | const - meta_capi_token | `EAA0D5fYG7HQ...` | Token de Meta CAPI (duplicado) |
| 166 | const - meta_pixel_id | `25699472449663830` | Pixel ID de Meta (duplicado) |
| 167 | const - gads_lead_conversion_label | `xYzAbC1234dEfGh5Ij` | Etiqueta de Lead |
| 168 | const - gads_contact_conversion_label | `kLmN6oPqR789sTuVwX` | Etiqueta de Contact |

---

## 🎚️ Triggers (Disparadores)

Los triggers determinan cuándo se activan los tags. Los principales son:

### Triggers de Eventos Personalizados (CE)

| Trigger ID | Nombre | Condición | Evento |
|-----------|--------|-----------|---------|
| 108 | CE - generate_lead | Event = `generate_lead` | Lead generado |
| -- | CE - contact | Event = `contact` | Formulario de contacto enviado |
| -- | CE - purchase | Event = `purchase` | Compra completada |
| -- | CE - page_view | Event = `page_view` | Vista de página |
| -- | CE - view_content_home | Event = `view_content_home` | Vista de home |
| -- | CE - view_content_show | Event = `view_content_show` | Vista de show/producto |
| -- | CE - video_play | Event = `video_play` | Video iniciado |
| -- | CE - video_complete | Event = `video_complete` | Video completado |
| -- | CE - section_view | Event = `section_view` | Sección visualizada |
| -- | CE - segment_click | Event = `segment_click` | Click en segmento |

---

## 📥 Instrucciones de Implementación

### Paso 1: Importar Contenedores

#### Importar Contenedor del Servidor

1. Inicia sesión en [Google Tag Manager](https://tagmanager.google.com)
2. Ve a **Admin** > **Import Container**
3. Selecciona el archivo `GTM-T2ZQP7WV_workspace77.json`
4. Selecciona un workspace (espacio de trabajo)
5. Opciones de importación:
   - **Merge** (Combinar): Si ya tienes configuración existente
   - **Overwrite** (Sobrescribir): Para empezar desde cero
6. Haz clic en **Confirm**

#### Importar Contenedor Web

1. Repite el proceso anterior con `GTM-TNM9JZ3S_v46.json`
2. Asegúrate de seleccionar el contenedor web correcto (tipo: Web)

### Paso 2: Actualizar Valores de Configuración

#### Valores Obligatorios a Actualizar

Navega a **Variables** en GTM y actualiza:

1. **Facebook Pixel ID** (Variables 106, 166)
   - Reemplaza con tu Pixel ID de Facebook

2. **Meta CAPI Token** (Variables 109, 165)
   - Obtén un nuevo token desde Facebook Business Manager
   - Settings > Event Manager > Your Pixel > Settings > Generate Access Token

3. **GA4 Measurement ID** (Variable 129)
   - Obtén desde Google Analytics 4 > Admin > Data Streams

4. **Cookie Domain** (Variable 107)
   - Actualiza con tu dominio (ejemplo: `tudominio.com`)

5. **Stape Server URL** (Variable 103)
   - Si usas Stape.io, obtén tu URL del servidor
   - Si usas servidor propio, actualiza con tu URL

6. **Google Ads Conversion ID** (Variable 164)
   - Actualiza con tu ID real de Google Ads

7. **Google Ads Conversion Labels** (Variables 163, 167, 168)
   - Actualiza con tus etiquetas reales de conversión

### Paso 3: Configurar el DataLayer

En tu sitio web, implementa el dataLayer para enviar eventos. Ejemplo:

```html
<!-- Inicializar dataLayer antes del código GTM -->
<script>
  window.dataLayer = window.dataLayer || [];
</script>

<!-- Código del contenedor GTM -->
<!-- Google Tag Manager -->
<script>(function(w,d,s,l,i){w[l]=w[l]||[];w[l].push({'gtm.start':
new Date().getTime(),event:'gtm.js'});var f=d.getElementsByTagName(s)[0],
j=d.createElement(s),dl=l!='dataLayer'?'&l='+l:'';j.async=true;j.src=
'https://www.googletagmanager.com/gtm.js?id='+i+dl;f.parentNode.insertBefore(j,f);
})(window,document,'script','dataLayer','GTM-TNM9JZ3S');</script>
<!-- End Google Tag Manager -->
```

#### Enviar Eventos al DataLayer

```javascript
// Ejemplo: Evento de Lead
dataLayer.push({
  'event': 'generate_lead',
  'em': 'usuario@ejemplo.com',
  'ph': '+5491123456789',
  'fn': 'Juan',
  'ln': 'Pérez',
  'event_id': 'unique_event_id_' + Date.now(),
  'value': 100,
  'currency': 'ARS'
});

// Ejemplo: Evento de Compra
dataLayer.push({
  'event': 'purchase',
  'em': 'usuario@ejemplo.com',
  'ph': '+5491123456789',
  'transaction_id': 'T12345',
  'value': 1500.00,
  'currency': 'ARS',
  'event_id': 'purchase_' + Date.now()
});

// Ejemplo: Video Play
dataLayer.push({
  'event': 'video_play',
  'video_id': 'video_123',
  'video_percent': 0
});

// Ejemplo: Video Complete
dataLayer.push({
  'event': 'video_complete',
  'video_id': 'video_123',
  'video_percent': 100
});
```

### Paso 4: Configurar el Servidor GTM

Si usas Stape.io:
1. Crea una cuenta en [Stape.io](https://stape.io)
2. Configura un nuevo servidor GTM
3. Configura un dominio personalizado (altamente recomendado)
4. Actualiza la variable "CONST - Stape Server URL" con tu URL

Si usas servidor propio:
1. Despliega Google Tag Manager Server-side en tu infraestructura
2. Configura el contenedor del servidor
3. Actualiza la URL en las variables correspondientes

### Paso 5: Probar la Configuración

1. En GTM, haz clic en **Preview** (Vista previa)
2. Ingresa la URL de tu sitio web
3. Realiza acciones que disparen eventos
4. Verifica en el panel de debug que los eventos se disparen correctamente
5. Usa las herramientas de debug:
   - **Meta Pixel Helper** (extensión de Chrome)
   - **Google Analytics DebugView**
   - **Google Tag Assistant**

### Paso 6: Publicar

1. Revisa todos los cambios en el workspace
2. Haz clic en **Submit** (Enviar)
3. Agrega un nombre y descripción a la versión
4. Haz clic en **Publish** (Publicar)

---

## 🎨 Personalización para Tu Proyecto

### Agregar Nuevos Eventos

1. **Definir el Evento**
   - Decide qué acción del usuario quieres rastrear
   - Ejemplo: `add_to_cart`, `start_checkout`, `form_submit`

2. **Crear el Trigger**
   - En GTM: **Triggers** > **New**
   - Tipo: **Custom Event**
   - Event name: nombre de tu evento

3. **Crear las Variables** (si es necesario)
   - Para extraer datos adicionales del evento
   - Tipo: **Data Layer Variable**

4. **Crear los Tags**
   - Meta CAPI Tag: Duplica un tag existente y modifica
   - GA4 Tag: Crea un nuevo evento de GA4
   - Google Ads Tag: Si necesitas rastrear conversión

5. **Implementar en el Sitio**
   ```javascript
   dataLayer.push({
     'event': 'tu_evento_personalizado',
     'parametro1': 'valor1',
     'parametro2': 'valor2'
   });
   ```

### Modificar Eventos Existentes

1. Navega al tag que quieres modificar
2. Ajusta los parámetros según necesites
3. Guarda y prueba en modo Preview
4. Publica cuando estés seguro

### Agregar Conversiones de Google Ads

1. Ve a **Variables** en GTM
2. Duplica una variable const de conversion_label existente
3. Nómbrala descriptivamente (ej: `const - gads_signup_conversion_label`)
4. Ingresa tu conversion label de Google Ads
5. Duplica un tag de Google Ads
6. Actualiza las referencias a la nueva variable
7. Asigna el trigger apropiado

---

## ✅ Validación y Pruebas

### Checklist de Validación

- [ ] **JSON Válido**: Ambos archivos se importan sin errores
- [ ] **Variables Actualizadas**: Todos los valores personales están configurados
- [ ] **Servidor GTM Funcionando**: El servidor responde correctamente
- [ ] **DataLayer Implementado**: Los eventos se envían desde el sitio
- [ ] **Meta Pixel Helper**: Muestra eventos correctamente
- [ ] **GA4 DebugView**: Los eventos aparecen en tiempo real
- [ ] **Google Ads**: Las conversiones se registran (si aplicable)
- [ ] **Consentimiento**: Los tags respetan las preferencias de consentimiento
- [ ] **Cross-domain Tracking**: Funciona entre subdominios (si aplicable)
- [ ] **Mobile Testing**: Funciona correctamente en dispositivos móviles

### Herramientas de Debug

1. **GTM Preview Mode**
   - Activa el modo preview en GTM
   - Verifica que los triggers se disparen
   - Confirma que los tags se ejecuten

2. **Meta Pixel Helper**
   - Extensión de Chrome: [Meta Pixel Helper](https://chrome.google.com/webstore/detail/meta-pixel-helper/)
   - Verifica eventos de Meta/Facebook
   - Revisa parámetros enviados

3. **Google Analytics DebugView**
   - En GA4: **Admin** > **DebugView**
   - Verifica eventos en tiempo real
   - Confirma parámetros de evento

4. **Network Tab (DevTools)**
   - Abre Chrome DevTools (F12)
   - Pestaña Network
   - Filtra por "gtm", "facebook", "google-analytics"
   - Verifica que las solicitudes se envíen correctamente

5. **GTM Server-Side Debug**
   - En el contenedor del servidor, activa Preview
   - Verifica que los eventos lleguen al servidor
   - Confirma que se reenvíen a las plataformas destino

### Solución de Problemas Comunes

#### Los eventos no se disparan

- Verifica que el dataLayer esté correctamente implementado
- Confirma que los nombres de eventos coincidan exactamente
- Revisa los triggers en modo Preview de GTM

#### Meta Conversion API no envía eventos

- Verifica que el Access Token sea válido
- Confirma que el Pixel ID sea correcto
- Revisa la URL del servidor GTM
- Verifica los parámetros de usuario (em, ph, fn, ln)

#### Google Ads no registra conversiones

- Verifica el Conversion ID y Labels
- Confirma que el Google Ads Conversion Linker esté activo
- Revisa el attribution window en Google Ads
- Espera hasta 24 horas para que aparezcan datos

#### Problemas con Cookies

- Verifica que Cookie Domain esté configurado correctamente
- Confirma que el dominio del servidor GTM sea de primer nivel
- Revisa las políticas de SameSite cookies

---

## 📞 Soporte y Referencias

### Documentación Oficial

- [Google Tag Manager](https://support.google.com/tagmanager)
- [Meta Conversion API](https://developers.facebook.com/docs/marketing-api/conversions-api)
- [Google Analytics 4](https://support.google.com/analytics/answer/9304153)
- [Google Ads Conversions](https://support.google.com/google-ads/answer/6331304)
- [Stape.io Documentation](https://stape.io/documentation)

### Recursos Adicionales

- [GTM Server-Side Tagging](https://developers.google.com/tag-platform/tag-manager/server-side)
- [dataLayer Best Practices](https://www.simoahava.com/analytics/data-layer/)
- [Meta Pixel Events](https://developers.facebook.com/docs/meta-pixel/reference)

---

## 📄 Licencia y Notas

Esta configuración de GTM es una guía de ejemplo. Los valores deben ser personalizados para cada proyecto específico.

**Última actualización:** 2026-02-11

**Versión del contenedor:**
- Server: GTM-T2ZQP7WV (workspace77)
- Web: GTM-TNM9JZ3S (v46)

---

## 🔒 Seguridad y Privacidad

### Mejores Prácticas

1. **Nunca expongas tokens o claves API en el código client-side**
   - Los tokens deben estar solo en el contenedor del servidor
   - Usa variables de entorno para tokens sensibles

2. **Implementa Consent Mode**
   - Respeta las preferencias de consentimiento del usuario
   - Implementa Google Consent Mode v2

3. **Hash de Datos Personales**
   - Los datos como email y teléfono deben hashearse (SHA256)
   - Meta CAPI acepta datos hasheados y no hasheados

4. **Protege el acceso a GTM**
   - Usa autenticación de dos factores
   - Limita los permisos de usuarios
   - Revisa regularmente los accesos

5. **GDPR y Privacidad**
   - Implementa una política de privacidad clara
   - Obtén consentimiento antes de rastrear
   - Permite a usuarios opt-out

---

**¿Preguntas o problemas?** Consulta la documentación oficial de cada plataforma o busca ayuda en la comunidad de GTM.
