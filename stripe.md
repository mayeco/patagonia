# Stripe Integration Phases

---
description: Analyze repository stack, research latest Stripe versions, and implement complete payment integration with phased approach and real-time validation
---

## FASE 0: ANÁLISIS PRE-IMPLEMENTACIÓN (CRÍTICO)

### Detección Automática de Stack

```bash
# Detectar arquitectura Next.js
- App Router vs Pages Router (buscar /app vs /pages)
- Componentes client vs server (buscar 'use client')
- Patrones de autenticación existentes
- Estructura de variables de entorno
```

### Validación de Entorno

```bash
# Verificar configuración existente
1. ¿Existe .env.local? Si no, copiar de env.example
2. ¿Están las variables de Stripe? Si no, añadirlas
3. ¿Hay conflictos de puerto? Detectar y ajustar
4. ¿Middleware configurado? Verificar compatibilidad
```

## FASE 1: FOUNDATION - ARQUITECTURA CORRECTA

### 1.1 Separación Cliente/Servidor (INMEDIATO)

**Crear dos archivos separados:**

- `stripe-client.ts` - Solo para componentes cliente con loadStripe
- `stripe-server.ts` - Solo para API routes con Stripe SDK
- Usar variables de entorno apropiadas (NEXT*PUBLIC* para cliente)
- Añadir validación de variables requeridas
- Configurar versión más reciente de API de Stripe

### 1.2 Variables de Entorno Automáticas

**Proceso de configuración automática:**

- Verificar si .env.local existe, si no copiarlo desde env.example
- Validar presencia de variables críticas de Stripe
- Generar secretos faltantes automáticamente
- Mostrar instrucciones claras para variables que requieren configuración manual

### 1.3 Manejo de Hidratación SSR

**Configuración preventiva:**

- Añadir suppressHydrationWarning al elemento html en layout
- Configurar Next.js para manejar diferencias cliente/servidor
- Prevenir errores causados por extensiones del navegador

### 1.4 API Routes con Fallback Pattern

**Implementar patrón robusto:**

- Endpoint order-status que busque orden existente primero
- Si no existe pero pago fue exitoso, crear orden automáticamente
- Webhook como método principal, fallback como respaldo
- Logging completo para debugging

## FASE 2: IMPLEMENTACIÓN ROBUSTA

### 2.1 Checkout Flow Completo

**Componentes con estados robustos:**

- Estados de carga durante procesamiento
- Manejo de errores específicos de Stripe
- Feedback visual claro para el usuario
- Prevención de múltiples clicks durante procesamiento

### 2.2 Webhook + Fallback Strategy

**Estrategia dual robusta:**

- Webhook como método principal para procesamiento inmediato
- Fallback en order-status para casos donde webhook no funciona
- Verificación de signatures para seguridad
- Logging estructurado para debugging efectivo

### 2.3 Validación de Configuración

**Verificación automática de setup:**

- Lista de variables requeridas para Stripe
- Validación al inicio de la aplicación
- Mensajes de error claros para configuración faltante
- Guías de solución para cada variable faltante

## MEJORAS ESPECÍFICAS BASADAS EN NUESTRA EXPERIENCIA

### Problema 1: Cliente/Servidor Mezclados

**Solución:** Crear archivos separados desde el inicio

- `stripe-client.ts` - Solo loadStripe
- `stripe-server.ts` - Solo Stripe SDK

### Problema 2: Variables de Entorno Faltantes

**Solución:** Setup automático de variables

- Detectar si .env.local existe
- Copiar automáticamente desde env.example si es necesario
- Validar que variables críticas estén presentes
- Proporcionar instrucciones claras para completar configuración

### Problema 3: Errores de Hidratación

**Solución:** Configuración preventiva

- Configurar Next.js para manejar diferencias SSR/cliente
- Añadir suppressHydrationWarning en layout
- Prevenir errores causados por extensiones del navegador
- Configuración de React Strict Mode apropiada

### Problema 4: Webhook No Configurado

**Solución:** Patrón de fallback robusto

- Implementar fallback en order-status para cuando webhook no esté configurado
- Polling inteligente en página de éxito
- Documentación clara para configuración de webhook
- App funcional incluso sin webhook configurado

### Problema 5: Debugging Complejo

**Solución:** Logging estructurado

- Logs informativos con contexto completo
- Identificadores únicos para seguimiento
- Estados de pago y metadata visible
- Información de debugging sin exponer datos sensibles

## CHECKLIST DE VALIDACIÓN AUTOMÁTICA

### Pre-Implementation

- [ ] Detectar App Router vs Pages Router
- [ ] Verificar .env.local existe
- [ ] Validar variables de Stripe presentes
- [ ] Identificar patrones de auth existentes

### Post-Implementation

- [ ] Test checkout sin webhook (fallback)
- [ ] Test con webhook configurado
- [ ] Verificar manejo de errores
- [ ] Validar estados de carga
- [ ] Test en diferentes navegadores

## DOCUMENTACIÓN MEJORADA

### Setup Guide

```markdown
1. Variables de entorno configuradas automáticamente
2. Webhook opcional - app funciona sin él
3. Testing con tarjetas específicas
4. Troubleshooting común incluido
```

### Testing Checklist

```markdown
- Pago exitoso: 4242 4242 4242 4242
- Pago fallido: 4000 0000 0000 0002
- 3D Secure: 4000 0025 0000 3155
- Test sin webhook configurado
- Test con webhook configurado
```

## IMPLEMENTACIÓN INCREMENTAL

### Iteración 1: Core Funcional (30 min)

1. Separar cliente/servidor
2. Configurar variables automáticamente
3. Implementar checkout básico
4. Test manual exitoso

### Iteración 2: Robustez (20 min)

1. Añadir fallback pattern
2. Mejorar manejo de errores
3. Configurar hidratación
4. Test casos de error

### Iteración 3: Polish (10 min)

1. Logging y debugging
2. Documentación
3. Checklist de testing
4. Optimizaciones finales

### Total estimado: 60 minutos vs 3+ horas anteriores

## COMANDOS DE VALIDACIÓN

```bash
# Verificar configuración
npm run stripe:validate

# Test checkout flow
npm run stripe:test

# Setup webhook local
npm run stripe:webhook-setup
```