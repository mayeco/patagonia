# SaaS Complete Workflow

Genera una aplicación SaaS completa con arquitectura moderna, autenticación, pagos y funcionalidades base. Solo proporciona el objetivo del SaaS y este workflow creará toda la estructura, arquitectura y flujo base.

## ⚠️ REGLAS CRÍTICAS DE EJECUCIÓN

**NO LOOPS DE ANÁLISIS**: Completar en máximo 15 pasos.
**DECISIONES BINARIAS**: Proceder o PARAR con mensaje específico.
**VALIDACIÓN CONTINUA**: Verificar cada fase antes de proceder.
**TERMINACIÓN**: Si objetivo no claro o directorio ocupado → PARAR.

## FASE 0: CAPTURA DE OBJETIVO Y DETECCIÓN DE IDIOMA

### 0.1 Detección de Idioma

- Detectar idioma del usuario (por defecto español si no es claramente inglés)
- Inferir de mensajes previos si no está claro
- Responder en español por defecto salvo indicación contraria

### 0.2 Captura de Objetivo y Tecnologías SaaS

- Solicitar descripción clara del objetivo del SaaS
- Identificar industria/nicho objetivo
- Determinar modelo de monetización preferido
- **VALIDAR STACK TECNOLÓGICO DESEADO:**
  - Frontend: Next.js, React, Vue, etc.
  - Backend: Next.js API, Node.js, Python, etc.
  - Base de datos: Supabase, Firebase, PostgreSQL, etc.
  - Pagos: Stripe, PayPal, etc.
  - Si no especifica, usar stack por defecto
- Si objetivo o stack ambiguo → PARAR y pedir clarificación

## FASE 1: ANÁLISIS Y PLANIFICACIÓN AUTOMÁTICA

### 1.1 Análisis de Mercado y Competencia

- Buscar información sobre el nicho/industria
- Identificar competidores principales
- Analizar modelos de pricing comunes
- Determinar funcionalidades esenciales del mercado

### 1.2 Definición de Arquitectura SaaS Base

**Stack Tecnológico Estándar:**

- Frontend: Next.js 15 + TypeScript + Tailwind CSS
- Backend: Next.js API Routes
- Base de Datos: Supabase (PostgreSQL + Auth + Storage)
- Pagos: Stripe (checkout + webhooks + customer portal)
- UI: Radix UI + Shadcn/ui + Lucide Icons
- Validación: Zod + React Hook Form
- Deployment: Vercel (frontend) + Supabase (backend)

### 1.3 Modelo de Datos Base SaaS

**Tablas Esenciales:**

- users (perfil extendido de auth.users)
- subscriptions (planes y estado de suscripción)
- usage_tracking (métricas de uso por usuario)
- orders/transactions (historial de pagos)
- [tablas específicas del dominio]

### 1.4 Funcionalidades Core SaaS

**Autenticación y Usuarios:**

- Registro/login con email + OAuth (Google)
- Perfiles de usuario completos
- Gestión de sesiones seguras

**Sistema de Pagos:**

- Múltiples planes de suscripción
- Checkout flow completo
- Customer portal para gestión
- Webhooks para sincronización

**Dashboard y Analytics:**

- Panel de usuario con métricas
- Historial de uso y facturación
- Configuración de cuenta

**Funcionalidad Principal:**

- [Específica según objetivo del SaaS]
- API endpoints necesarios
- Validaciones y seguridad

## FASE 2: INICIALIZACIÓN DE PROYECTO

### 2.1 Validación de Directorio

- Verificar directorio vacío (excepto .git, .gitignore, etc.)
- Si no vacío, crear subdirectorio con nombre del proyecto
- Validar permisos de escritura

### 2.2 Verificación de Prerrequisitos

- Node.js (v18+) y npm/pnpm
- Git configurado
- Acceso a internet para dependencias

### 2.3 Inicialización Next.js Optimizada

- Crear proyecto Next.js con TypeScript
- Configurar Tailwind CSS
- Instalar dependencias SaaS esenciales
- Configurar estructura de carpetas estándar

## FASE 3: CONFIGURACIÓN DE INFRAESTRUCTURA

### 3.1 Setup Supabase Automático

- Crear proyecto Supabase
- Configurar variables de entorno
- Generar schema de base de datos
- Aplicar migraciones iniciales
- Configurar RLS policies

### 3.2 Integración Stripe Optimizada

- Configurar Stripe con separación cliente/servidor
- Implementar checkout flow robusto
- Setup webhooks con fallback pattern
- Crear customer portal
- Configurar planes de suscripción

### 3.3 Autenticación Completa

- Configurar Supabase Auth
- Implementar OAuth providers
- Crear middleware de autenticación
- Setup páginas de auth

## FASE 4: DESARROLLO DE FUNCIONALIDADES BASE

### 4.1 Landing Page Profesional

**Secciones Estándar:**

- Hero section con propuesta de valor clara
- Features section con beneficios principales
- Pricing section con planes claros
- Testimonials/social proof
- FAQ section
- Footer completo

**Optimizaciones:**

- Responsive design completo
- SEO optimizado
- Performance optimizado
- Call-to-actions estratégicos

### 4.2 Dashboard de Usuario

**Componentes Esenciales:**

- Sidebar navigation
- Overview/metrics cards
- Usage tracking display
- Billing/subscription management
- Account settings
- Support/help section

### 4.3 Funcionalidad Principal

- Implementar la funcionalidad core específica del SaaS
- API endpoints necesarios
- Validaciones y seguridad
- Estados de carga y error
- Feedback visual apropiado

### 4.4 Sistema de Pagos Completo

**Flujos Implementados:**

- Subscription checkout
- Plan upgrades/downgrades
- Payment method management
- Invoice generation
- Usage-based billing (si aplica)
- Cancellation flow

## FASE 5: SEGURIDAD Y OPTIMIZACIÓN

### 5.1 Seguridad Implementada

- Row Level Security (RLS) en Supabase
- Validación de inputs con Zod
- Rate limiting en API routes
- CSRF protection
- Secure headers configuration
- Environment variables validation

### 5.2 Performance y UX

- Loading states en todas las interacciones
- Error boundaries y manejo de errores
- Optimización de imágenes
- Code splitting automático
- SEO meta tags
- Analytics setup (opcional)

### 5.3 Testing y Validación

- Flujo completo de registro → pago → uso
- Testing de webhooks
- Validación de seguridad
- Performance benchmarks
- Cross-browser testing

## FASE 6: VALIDACIÓN DE CONFIGURACIÓN Y TESTING

### 6.1 Validación de Variables de Entorno

**SOLICITAR CONFIGURACIÓN REQUERIDA:**

- Si usa Supabase: SUPABASE_URL, SUPABASE_ANON_KEY, SUPABASE_SERVICE_ROLE_KEY
- Si usa Stripe: STRIPE_SECRET_KEY, STRIPE_PUBLISHABLE_KEY, STRIPE_WEBHOOK_SECRET
- Si usa OAuth: GOOGLE_CLIENT_ID, GOOGLE_CLIENT_SECRET
- Validar formato y accesibilidad de cada variable
- Crear archivo .env.example con todas las variables necesarias
- **NO PROCEDER** hasta que todas las variables estén configuradas

### 6.2 Testing Funcional Automatizado

**CREAR SCRIPTS DE VALIDACIÓN:**

- `npm run test:env` - Validar todas las variables de entorno
- `npm run test:db` - Verificar conexión a base de datos
- `npm run test:auth` - Validar configuración de autenticación
- `npm run test:payments` - Verificar integración de pagos
- `npm run test:hydration` - Detectar errores de hidratación SSR
- `npm run test:critical` - Ejecutar todos los tests críticos

### 6.3 Validación de Puntos Críticos

**VERIFICACIONES AUTOMÁTICAS:**

- Hidratación SSR sin errores
- Conexiones de base de datos funcionales
- APIs de terceros respondiendo correctamente
- Rutas protegidas funcionando
- Webhooks recibiendo correctamente
- Estados de carga y error manejados

## FASE 7: FINALIZACIÓN Y DOCUMENTACIÓN LOCAL

### 7.1 Servidor de Desarrollo Optimizado

- Configurar `npm run dev` con hot reload
- Optimizar performance en desarrollo
- Configurar puertos y variables locales
- Verificar que todo funcione en localhost

### 7.2 Documentación Completa

- README con instrucciones de setup local
- Guía de configuración de variables de entorno
- Documentación de API endpoints
- Troubleshooting guide para desarrollo local
- Instrucciones para deployment futuro (opcional)

### 7.3 Entrega del Proyecto

- Aplicación funcionando completamente en local
- Todas las funcionalidades validadas
- Scripts de testing configurados
- Proyecto listo para desarrollo continuo

## PATRONES DE IMPLEMENTACIÓN ESPECÍFICOS

### Estructura de Archivos SaaS

```bash
src/
├── app/
│   ├── (auth)/           # Rutas de autenticación
│   ├── (dashboard)/      # Dashboard protegido
│   ├── (marketing)/      # Landing page
│   ├── api/              # API routes
│   └── globals.css
├── components/
│   ├── ui/               # Componentes base (shadcn)
│   ├── auth/             # Componentes de autenticación
│   ├── dashboard/        # Componentes del dashboard
│   ├── marketing/        # Componentes de marketing
│   └── shared/           # Componentes compartidos
├── lib/
│   ├── auth.ts           # Configuración de auth
│   ├── db.ts             # Cliente de Supabase
│   ├── stripe-client.ts  # Stripe cliente
│   ├── stripe-server.ts  # Stripe servidor
│   └── utils.ts          # Utilidades
├── hooks/                # Custom hooks
├── types/                # Definiciones de tipos
└── middleware.ts         # Middleware de autenticación
```

### Variables de Entorno Estándar

```env
# Supabase
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
SUPABASE_SERVICE_ROLE_KEY=

# Stripe
NEXT_PUBLIC_STRIPE_PUBLISHABLE_KEY=
STRIPE_SECRET_KEY=
STRIPE_WEBHOOK_SECRET=

# App
NEXTAUTH_SECRET=
NEXTAUTH_URL=
```

### Schema Base de Datos

**Tablas Esenciales para Todo SaaS:**

- users (perfil extendido)
- subscriptions (gestión de planes)
- usage_tracking (métricas de uso)
- transactions (historial de pagos)
- [tablas específicas del dominio]

**Políticas RLS Estándar:**

- Users solo ven sus propios datos
- Service role acceso completo para webhooks
- Políticas específicas por tabla según necesidad

## VALIDACIÓN AUTOMÁTICA POR FASE

### Checklist Fase 1-2

- [ ] Objetivo claro definido
- [ ] Directorio preparado
- [ ] Prerrequisitos verificados
- [ ] Proyecto Next.js inicializado

### Checklist Fase 3-4

- [ ] Supabase configurado y conectado
- [ ] Stripe integrado y funcionando
- [ ] Autenticación implementada
- [ ] Landing page desplegada

### Checklist Fase 5-6

- [ ] Dashboard funcional
- [ ] Funcionalidad principal implementada
- [ ] Todas las variables de entorno configuradas
- [ ] Tests de validación pasando
- [ ] Conexiones críticas verificadas
- [ ] Hidratación SSR sin errores
- [ ] Documentación de API actualizada

### Checklist Fase 7

- [ ] Aplicación funcionando completamente en localhost
- [ ] Testing automatizado implementado
- [ ] Documentación completa generada
- [ ] Scripts de desarrollo configurados
- [ ] Preparación para despliegue en producción

## COMANDOS DE VALIDACIÓN AUTOMÁTICA

```bash
# Validación completa del sistema
npm run validate:all

# Validar variables de entorno
npm run test:env

# Validar conexiones críticas
npm run test:connections

# Test hidratación SSR
npm run test:hydration

# Test funcionalidad core
npm run test:core

# Test integración pagos end-to-end
npm run test:payments

# Validar seguridad y RLS
npm run test:security

# Iniciar servidor de desarrollo
npm run dev
```

## SCRIPTS DE VALIDACIÓN IMPLEMENTADOS

### Validación de Variables de Entorno

```javascript
// scripts/validate-env.js
// Verifica que todas las variables requeridas estén presentes
// Valida formato de URLs y keys
// Testa conectividad con servicios externos
```

### Testing de Conexiones

```javascript
// scripts/test-connections.js
// Supabase: conexión DB + auth
// Stripe: API keys válidas
// OAuth providers: configuración correcta
```

### Validación de Hidratación

```javascript
// scripts/test-hydration.js
// Detecta diferencias cliente/servidor
// Valida suppressHydrationWarning
// Identifica componentes problemáticos
```

## TIEMPO ESTIMADO CON IA

Total: 40-80 minutos para SaaS completo funcionando en local

- Fase 0-1: 5 minutos (análisis + setup)
- Fase 2-3: 10 minutos (inicialización + infraestructura)
- Fase 4: 20-30 minutos (desarrollo core)
- Fase 5: 5-10 minutos (seguridad + optimización)
- Fase 6: 10-15 minutos (validación + testing)
- Fase 7: 3-5 minutos (finalización local)

## OUTPUTS FINALES

**Aplicación SaaS Completa:**

- Landing page profesional con pricing
- Sistema de autenticación completo
- Dashboard de usuario funcional
- Integración de pagos end-to-end
- Funcionalidad principal implementada
- Aplicación funcionando completamente en localhost

**Documentación:**

- Setup guide completo
- API documentation
- Troubleshooting guide
- Roadmap de mejoras

**Configuración:**

- Todas las variables de entorno configuradas
- Base de datos con schema completo
- Webhooks configurados y funcionando
- Monitoring básico implementado

¿Procedo con la implementación completa del SaaS basado en tu objetivo?
