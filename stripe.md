---
description: Analyze repository stack, research latest Stripe versions, and implement complete payment integration with phased approach and real-time validation
---

@windsurf Analiza este repositorio y crea una integración Stripe completa. Investiga las versiones más recientes antes de implementar.

## ANÁLISIS AUTOMÁTICO
- Detecta stack (framework, database, API patterns)
- Identifica estructura existente y convenciones
- Busca configuración de pagos previa

## INVESTIGACIÓN REQUERIDA
Busca en internet ANTES de codificar:
- Últimas versiones Stripe SDK para el stack detectado
- Breaking changes recientes y migration guides
- Best practices actualizadas de seguridad
- Nuevas APIs y features disponibles

## CONFIGURACIÓN INTERACTIVA
Pregunta UNA vez y procede:

**Modelo de monetización:**
1. One-time payments ($X productos)
2. Subscriptions (planes recurrentes)  
3. Usage-based (pay-per-use)
4. Hybrid (subscription + usage)

**Configuración:**
- Monedas objetivo
- Regiones de operación
- Tipo de negocio (B2B/B2C)

## IMPLEMENTACIÓN PRIORIZADA

### FASE 1: Foundation (Implementar PRIMERO)
Requirements mínimos viables:

 Stripe SDK setup con versión más reciente
 Environment variables configuration
 Basic checkout flow funcional
 Webhook endpoint con signature verification
 Database schema mínimo para el tipo seleccionado
 Success/error pages básicas

Output: Flujo de pago funcional end-to-end
Test: Completar una transacción exitosa

### FASE 2: Production Ready (Implementar SEGUNDO)
Requirements de producción:

 Error handling robusto + loading states
 Security headers + rate limiting
 Comprehensive webhook events
 Customer portal integration
 Admin dashboard básico
 Logging y monitoring setup

Output: Sistema listo para producción
Test: Manejar todos los casos de error conocidos

### FASE 3: Advanced Features (Implementar TERCERO)
Requirements avanzados:

 Multi-currency support
 Advanced analytics dashboard
 Automated testing suite
 Performance optimizations
 Compliance features (invoicing, tax)

Output: Sistema empresarial completo
Test: Performance benchmark + security audit

## WORKFLOW DE DESARROLLO

**Iteración 1: Quick Prototype**
1. Implementa SOLO Fase 1
2. Test manual completo
3. Muestra demo funcional
4. Pide feedback antes de continuar

**Iteración 2: Production Polish**  
1. Implementa Fase 2 basado en feedback
2. Automated testing setup
3. Security review
4. Performance check

**Iteración 3: Advanced Features**
1. Solo si se requiere Fase 3
2. Implementación incremental
3. Validation continua

## TECHNICAL REQUIREMENTS

**Backend (adaptar al stack detectado):**
Rutas requeridas:

POST /api/checkout - Create session
POST /api/webhook - Process events
GET /api/customer - Customer data
POST /api/portal - Customer portal

Database schema (tipo-específico):

Customers table (stripe_id, metadata)
Transactions table (status, amount, metadata)
[Subscriptions/Usage tables si aplica]


**Frontend (framework detectado):**
Componentes requeridos:

CheckoutButton (loading + error states)
PricingDisplay (planes si aplica)
PaymentStatus (success/error pages)
CustomerPortal (manage subscription)


## VALIDATION AUTOMÁTICA
En cada fase, verificar:
- [ ] Webhook signatures válidas
- [ ] Error scenarios manejados
- [ ] Security headers presentes
- [ ] Database transactions atómicas
- [ ] API responses consistentes

## OUTPUTS ESPECÍFICOS

**Código:**
- Archivos listos para commit
- Environment variables template
- Database migration scripts
- Basic documentation

**Testing:**
- Manual testing checklist
- Automated test examples
- Error scenario validation

**Deployment:**
- Production configuration guide
- Monitoring setup instructions
- Troubleshooting common issues

## WINDSURF-SPECIFIC INSTRUCTIONS

**Development Flow:**
1. Start con analysis de repo existente
2. Research phase con multiple searches
3. Implement en small, testable chunks
4. Validate cada chunk antes de proceder
5. Refactor based on testing results

**Error Handling:**
- Si algo falla, debug paso a paso
- Mostrar debugging process
- Pedir clarificación si requirements ambiguos
- No assumir configuraciones sin validar

**Context Management:**
- Mantén focus en una fase a la vez
- Resume previous work si session interrumpida  
- Document decisions tomadas para consistency

¿Procedo con Fase 1 implementation después del análisis y research?
