# CLAUDE.md

Este archivo proporciona una guía completa a Claude Code cuando trabaja con el proyecto de este repositorio.

## Filosofía Central de Desarrollo

### KISS (Keep It Simple, Stupid)

La simplicidad debe ser un objetivo clave en el diseño. Elige soluciones sencillas sobre soluciones complejas siempre que sea posible. Las soluciones simples son más fáciles de entender, mantener y depurar.

### YAGNI (You Aren't Gonna Need It)

Evita construir funcionalidad por especulación. Implementa características solo cuando sean necesarias, no cuando anticipes que podrían ser útiles en el futuro.

### 🧱 Estructura del Código y Modularidad
### Refactorizar cuando la legibilidad se vea afectada, no por números arbitrarios
### Estructura de Carpetas y Módulos
Una estructura de carpetas clara es fundamental para la mantenibilidad y la colaboración. Aplicaremos el principio de "separación de responsabilidades" tanto a nivel de capas lógicas como de organización física. Asumiremos un proyecto con un frontend en React y un backend gestionado por Supabase.
Estructura Lógica (Capas):
1.	Capa de Presentación (UI/Frontend):
o	Responsabilidad: Todo lo relacionado con la interfaz de usuario.
o	Componentes: Vistas, componentes reutilizables, hooks de UI, estilos.
o	Comunicación: Interactúa con la Capa de Lógica de Negocio.
2.	Capa de Lógica de Negocio (Application/Services):
o	Responsabilidad: Contiene las reglas de negocio, validaciones complejas, orquestación de operaciones y la lógica central de la aplicación.
o	Servicios: Funciones que encapsulan la lógica de cómo se procesan los datos y las operaciones.
o	Comunicación: Se comunica con la Capa de Datos y expone métodos a la Capa de Presentación.
3.	Capa de Datos (Data Access/Repositories):
o	Responsabilidad: Abstracción del acceso a la base de datos (Supabase en tu caso).
o	Repositorios: Métodos para interactuar con las tablas de la base de datos (CRUD: Crear, Leer, Actualizar, Borrar).
o	Comunicación: Interactúa directamente con Supabase y es utilizada por la Capa de Lógica de Negocio.
### Organización Física (Carpetas):
Esta estructura se basa en un proyecto React típico, pero con énfasis en la modularidad.
/tu-proyecto-gastronomico
├── .env                       # Variables de entorno (desarrollo, producción)
├── .gitignore                 # Archivos a ignorar por Git
├── package.json               # Dependencias del proyecto
├── README.md                  # Documentación del proyecto
├── public/                    # Archivos estáticos (index.html, favicon, etc.)
│   └── index.html
│   └── ...
└── src/                       # Código fuente de la aplicación
    ├── api/                   # Clientes API para interactuar con Supabase (o cualquier otro backend)
    │   └── supabaseClient.js  # Configuración inicial de Supabase
    │   └── auth.js            # Funciones de autenticación con Supabase
    │   └── dataAccess.js      # Funciones genéricas de acceso a datos de Supabase
    ├── assets/                # Imágenes, íconos, fuentes, etc.
    │   ├── images/
    │   └── icons/
    ├── components/            # Componentes reutilizables y genéricos de UI (botones, modales, inputs)
    │   ├── Button/
    │   │   └── Button.jsx
    │   │   └── Button.module.css (o .scss, .tailwind.css)
    │   ├── Modal/
    │   │   └── Modal.jsx
    │   └── ...
    ├── config/                # Archivos de configuración de la aplicación
    │   └── appConfig.js       # Constantes, configuraciones globales
    ├── hooks/                 # Custom React Hooks reutilizables (ej. useAuth, useForm)
    │   └── useAuth.js
    │   └── useForm.js
    ├── layouts/               # Estructuras de diseño de página (ej. DashboardLayout, AuthLayout)
    │   └── DashboardLayout.jsx
    ├── modules/                # Módulos de la aplicación (separación por característica/dominio)
    │   ├── inventario/
    │   │   ├── components/    # Componentes específicos del módulo (ej. InventarioList, InsumoForm)
    │   │   │   └── InsumoForm.jsx
    │   │   ├── services/      # Lógica de negocio del módulo (ej. gestionInsumos.js)
    │   │   │   └── insumoService.js
    │   │   ├── api/           # Funciones de interacción con Supabase específicas de insumos
    │   │   │   └── insumoApi.js
    │   │   ├── pages/         # Vistas/páginas del módulo (ej. InventarioPage, DetalleInsumoPage)
    │   │   │   └── InventarioPage.jsx
    │   │   ├── types/         # Definiciones de tipos/interfaces (ej. Insumo.js)
    │   │   │   └── Insumo.js
    │   │   └── utils/         # Utilidades específicas del módulo (ej. conversionesUnidades.js)
    │   │       └── conversionesUnidades.js
    │   ├── pos/
    │   │   ├── components/
    │   │   ├── services/
    │   │   ├── api/
    │   │   ├── pages/
    │   │   ├── types/
    │   │   └── utils/
    │   ├── recetas/            # Módulo de Gestión de Platos y Recetas
    │   │   ├── components/
    │   │   ├── services/
    │   │   ├── api/
    │   │   ├── pages/
    │   │   ├── types/
    │   │   └── utils/
    │   └── reportes/
    │       ├── components/
    │       ├── services/
    │       ├── api/
    │       ├── pages/
    │       ├── types/
    │       └── utils/
    ├── pages/                 # Páginas principales (ej. HomePage, LoginPage)
    │   ├── HomePage.jsx
    │   └── LoginPage.jsx
    ├── routes/                # Definición de rutas de la aplicación
    │   └── AppRoutes.jsx
    ├── services/              # Servicios globales o utilidades de lógica de negocio que no pertenecen a un módulo específico
    │   └── authService.js
    │   └── userService.js
    ├── store/                 # Gestión de estado global (ej. usando React Context o Zustand)
    │   ├── AuthContext.js
    │   └── uiStore.js
    ├── styles/                # Estilos globales, variables CSS, Tailwind CSS base
    │   ├── index.css
    │   └── variables.css
    ├── utils/                 # Utilidades genéricas (ej. formatters, validators)
    │   └── helpers.js
    │   └── validators.js
    ├── App.jsx                # Componente principal de la aplicación
    └── main.jsx               # Punto de entrada de la aplicación

### Mejores Prácticas de Desarrollo y Estructuración ###
Aplicar estos principios desde el inicio es fundamental para un código limpio y escalable.
### Principios de Diseño de Software:
•	SOLID:
o	SRP (Single Responsibility Principle - Principio de Responsabilidad Única): Cada módulo, clase o función debe tener una única razón para cambiar.
	Aplicación: Un componente React solo se encarga de la UI; un servicio se encarga de la lógica de negocio; una función de la capa api solo interactúa con Supabase. Por ejemplo, insumoService.js contendrá la lógica de negocio para los insumos (validaciones, cálculos), mientras que insumoApi.js solo contendrá las llamadas CRUD a la tabla insumos en Supabase.
o	OCP (Open/Closed Principle - Principio Abierto/Cerrado): Las entidades de software (clases, módulos, funciones) deben estar abiertas para extensión, pero cerradas para modificación.
	Aplicación: Si necesitas añadir una nueva forma de pago, extiendes la funcionalidad sin modificar el código existente del proceso de cobro principal.
o	DIP (Dependency Inversion Principle - Principio de Inversión de Dependencias): Los módulos de alto nivel no deben depender de módulos de bajo nivel. Ambos deben depender de abstracciones.
	Aplicación: Tu insumoService no debe depender directamente de supabaseClient.js. En cambio, ambos dependerían de una interfaz (implícita en JS) o de funciones pasadas como dependencias, facilitando el cambio de base de datos o la simulación para pruebas.
•	DRY (Don't Repeat Yourself - No te Repitas): Evitar la duplicación de código.
o	Aplicación:
	Componentes Reutilizables: Crea componentes genéricos en src/components (ej., Input, Button, Table) que se puedan usar en múltiples módulos.
	Hooks Personalizados: Para lógica de UI reutilizable (ej., useForm para manejar formularios en diferentes módulos).
	Funciones de Utilidad: Para operaciones comunes (ej., formateo de fechas, validaciones genéricas) en src/utils.
	Tipos Compartidos: Define interfaces o tipos de datos en src/types o dentro de modules/*/types para asegurar consistencia.
### Patrones de Diseño:
•	Service Layer (Capa de Servicios):
o	Descripción: Encapsula la lógica de negocio compleja, orquesta las operaciones y maneja las validaciones. Los componentes de la UI interactúan con los servicios, no directamente con la capa de datos.
o	Aplicación: src/modules/inventario/services/insumoService.js contendría funciones como crearInsumo(data), actualizarStock(insumoId, cantidad, tipoMovimiento), que a su vez usarían funciones de src/modules/inventario/api/insumoApi.js para interactuar con Supabase.
•	Repository Pattern (Patrón Repositorio):
o	Descripción: Abstrae la lógica de acceso a datos, proporcionando una interfaz limpia para que la capa de negocio interactúe con la base de datos sin conocer los detalles de implementación (ej., si es SQL o NoSQL).
o	Aplicación (con Supabase): Las funciones en src/modules/*/api/*.js actuarían como tus repositorios. Por ejemplo, insumoApi.js tendría getInsumos(), addInsumo(data), updateInsumo(id, data). Esto te permitiría, en teoría, cambiar de Supabase a otro backend sin reescribir la lógica de negocio en insumoService.js.
 ## Gestión de Estado:
Para un Plan BÁSICO-PLUS con React, la gestión de estado puede ser eficiente sin la complejidad de Redux.
•	React Context API: Ideal para el estado global que es necesario en muchas partes de la aplicación (ej., autenticación de usuario, información del negocio actual, configuraciones globales de UI).
o	Ubicación: src/store/AuthContext.js, src/store/BusinessConfigContext.js.
•	Zustand (o similar librería ligera): Para un estado más complejo y localizado que necesita ser compartido entre componentes que no están directamente relacionados por el árbol de componentes, o para manejar el estado de formularios grandes. Es más simple que Redux pero potente.
o	Ubicación: src/store/uiStore.js para el estado de la interfaz de usuario, o dentro de modules/*/store para estados específicos del módulo.
•	Estado Local de Componentes: Para el estado que solo afecta a un componente y sus hijos inmediatos.
### Manejo de Errores y Validaciones:
•	Validaciones:
o	Frontend (UI): Implementar validaciones del lado del cliente para proporcionar feedback inmediato al usuario (ej., "Este campo es obligatorio", "Formato de email inválido"). Esto mejora la experiencia del usuario y reduce llamadas innecesarias al servidor.
o	Backend (Supabase/RLS/Database Constraints): Supabase te permite definir reglas de validación a nivel de base de datos (constraints) y Row Level Security (RLS) para asegurar que los datos sean válidos y que los usuarios solo accedan a lo que deben. Esta es la validación crítica que garantiza la integridad de los datos.
•	Manejo de Errores Centralizado:
o	Utiliza bloques try-catch en tus funciones de servicio y API para capturar errores.
o	Implementa un mecanismo global de notificación de errores en el frontend (ej., un componente de Toast o Snackbar) para mostrar mensajes amigables al usuario en caso de fallos.
o	Registro de Errores: En el backend (Supabase Functions si las usas, o directamente en tu lógica de API si es un servidor Node.js aparte), registra los errores en un servicio de logging para depuración.
### Documentación:
•	Comentarios en el Código: Esenciales para explicar la lógica compleja, el propósito de las funciones y las decisiones de diseño.
•	README.md del Proyecto: Debe contener instrucciones claras para la configuración del entorno, la ejecución del proyecto, scripts útiles y una descripción general de la arquitectura.
•	Documentación de la API (Interna): Describe las funciones de tu capa api (ej., insumoApi.js), sus parámetros y lo que retornan. Esto es crucial para que otros desarrolladores entiendan cómo interactuar con la base de datos.
•	Wiki del Proyecto (Opcional): Para documentar decisiones de arquitectura, flujos de negocio complejos y guías de contribución.
### Estándares de Docstrings

Usa docstrings estilo Google para todas las funciones, clases y módulos públicos:

```python  (pongo python para un ejemplo rapido)
def calculate_discount(
    price: Decimal,
    discount_percent: float,
    min_amount: Decimal = Decimal("0.01")
) -> Decimal:
    """
    Calcula el precio con descuento para un producto.

    Args:
        price: Precio original del producto
        discount_percent: Porcentaje de descuento (0-100)
        min_amount: Precio mínimo permitido final

    Returns:
        Precio final después de aplicar el descuento

    Raises:
        ValueError: Si discount_percent no está entre 0 y 100
        ValueError: Si el precio final sería menor que min_amount

    Example:
        >>> calculate_discount(Decimal("100"), 20)
        Decimal('80.00')
    """
```
### Desarrollo Guiado por Pruebas (TDD)

1. **Escribe la prueba primero** - Define el comportamiento esperado antes de la implementación
2. **Observa que falle** - Asegúrate de que la prueba realmente prueba algo
3. **Escribe el código mínimo** - Solo lo necesario para que la prueba pase
4. **Refactoriza** - Mejora el código manteniendo las pruebas verdes
5. **Repite** - Una prueba a la vez

### Estrategia de Pruebas y Manejo de Errores para el Proyecto Gastronómico BÁSICO-PLUS

#### 🧪 Estrategia de Pruebas (Adaptada a React/TypeScript/Supabase)

**Desarrollo Guiado por Pruebas (TDD)**
1. **Pruebas Unitarias (Jest)**
```typescript
// Ejemplo: Prueba para el servicio de inventario
describe('InventarioService', () => {
  let service: InventarioService;
  let supabaseMock: jest.Mocked<SupabaseClient>;

  beforeEach(() => {
    supabaseMock = mockSupabaseClient();
    service = new InventarioService(supabaseMock);
  });

  test('debe actualizar stock usando FIFO', async () => {
    // 1. Configurar mock
    supabaseMock.from.mockReturnValue({
      select: jest.fn().mockResolvedValue({ data: mockInsumos, error: null })
    });

    // 2. Ejecutar
    await service.actualizarStockFIFO('insumo123', 5);

    // 3. Verificar
    expect(supabaseMock.from).toHaveBeenCalledWith('lotes_insumos');
  });
});
```

**Pruebas de Integración (Cypress)**
```typescript
// Ejemplo: Flujo completo de venta en POS
describe('Flujo POS', () => {
  it('debe registrar venta y descontar inventario', () => {
    // 1. Iniciar sesión
    cy.login('mesero@restaurante.com', 'password');

    // 2. Seleccionar mesa
    cy.selectTable(5);

    // 3. Añadir platos
    cy.addMenuItem('Hamburguesa Clásica', 2);
    cy.addMenuItem('Coca-Cola', 1);

    // 4. Verificar que el stock se actualizó
    cy.checkStock('Carne Molida', 8); // Stock inicial: 10
  });
});
```
#### 🚨 Manejo de Errores (Adaptado a Frontend)

**Excepciones Personalizadas**
```typescript
// src/core/errors.ts
export class InventarioError extends Error {
  constructor(message: string, public readonly code: string) {
    super(message);
    this.name = 'InventarioError';
  }
}

export class StockInsuficienteError extends InventarioError {
  constructor(public readonly insumoId: string, public readonly cantidadFaltante: number) {
    super(`Stock insuficiente para insumo ${insumoId}`, 'STOCK_INSUFICIENTE');
  }
}
```

**Manejo Centralizado**
```typescript
// src/utils/errorHandler.ts
export function handleAPIError(error: unknown): void {
  if (error instanceof StockInsuficienteError) {
    showToast('error', `No hay suficiente stock (Faltan: ${error.cantidadFaltante})`);
    navigate('/inventario');
  } else if (error instanceof Error) {
    logger.error('Error no controlado', error);
    showToast('error', 'Ocurrió un error inesperado');
  }
}

// Uso en componentes
const ajustarStock = async () => {
  try {
    await InventarioService.ajustarStock(insumoId, cantidad);
  } catch (error) {
    handleAPIError(error);
  }
};
```

**Logging Estructurado**
```typescript
// src/core/logger.ts
import { pino } from 'pino';

const logger = pino({
  level: import.meta.env.VITE_LOG_LEVEL || 'info',
  formatters: {
    bindings: () => ({ context: 'frontend' }),
  },
  timestamp: () => `,"time":"${new Date().toISOString()}"`
});

// Ejemplo de uso
logger.info({ module: 'inventario', action: 'ajuste_stock' }, 'Ajuste realizado');
logger.error(error, 'Error en flujo POS');
```

#### 🔧 Gestión de Configuración (Frontend + Supabase)

**Variables de Entorno**
```typescript
// src/config/env.ts
import { z } from 'zod';

const envSchema = z.object({
  VITE_SUPABASE_URL: z.string().url(),
  VITE_SUPABASE_KEY: z.string(),
  VITE_API_TIMEOUT: z.coerce.number().default(5000),
});

export const env = envSchema.parse(import.meta.env);
```

**Configuración Supabase**
```typescript
// src/api/supabaseClient.ts
import { createClient } from '@supabase/supabase-js';
import { env } from '../config/env';

export const supabase = createClient(
  env.VITE_SUPABASE_URL,
  env.VITE_SUPABASE_KEY,
  {
    auth: {
      persistSession: true,
      autoRefreshToken: true,
    },
    db: {
      schema: 'public',
    },
  }
);
```

#### 🏗️ Modelos de Datos (TypeScript + Zod)

**Modelos TypeScript**
```typescript
// src/modules/inventario/types/insumo.ts
import { z } from 'zod';

export const InsumoSchema = z.object({
  id: z.string().uuid(),
  nombre: z.string().min(3).max(100),
  stockActual: z.number().min(0),
  costoPromedio: z.number().positive(),
  esPerecedero: z.boolean(),
  fechaVencimiento: z.date().optional(),
});

export type Insumo = z.infer<typeof InsumoSchema>;

// Ejemplo de uso en formularios
const form = useForm<Insumo>({
  resolver: zodResolver(InsumoSchema),
});
```

**Modelos para Operaciones**
```typescript
// src/modules/pos/types/venta.ts
export const ItemVentaSchema = z.object({
  platoId: z.string().uuid(),
  cantidad: z.number().min(1),
  precioUnitario: z.number().positive(),
  notas: z.string().max(200).optional(),
});

export type Venta = {
  id?: string;
  items: z.infer<typeof ItemVentaSchema>[];
  total: number;
  metodoPago: 'efectivo' | 'tarjeta';
};
```

#### 🔄 Integración con Supabase

**Ejemplo de Repositorio**
```typescript
// src/modules/inventario/api/insumoRepository.ts
export const InsumoRepository = {
  async getById(id: string): Promise<Insumo> {
    const { data, error } = await supabase
      .from('insumos')
      .select('*')
      .eq('id', id)
      .single();

    if (error) throw new DatabaseError('INSUMO_NOT_FOUND');
    return InsumoSchema.parse(data);
  },

  async updateStock(id: string, cantidad: number): Promise<void> {
    const { error } = await supabase.rpc('ajustar_stock', {
      insumo_id: id,
      cantidad,
    });

    if (error) throw new DatabaseError('STOCK_UPDATE_FAILED');
  },
};
```

**Transacciones**
```typescript
// src/modules/pos/services/ventaService.ts
export const VentaService = {
  async procesarVenta(venta: Venta): Promise<void> {
    try {
      // 1. Registrar venta
      const { data, error } = await supabase
        .from('ventas')
        .insert(venta)
        .select();

      if (error) throw error;

      // 2. Descontar inventario
      await Promise.all(
        venta.items.map(item => 
          InventarioService.descontarStock(item.platoId, item.cantidad)
        )
      );

    } catch (error) {
      logger.error(error);
      throw new VentaError('PROCESO_VENTA_FALLIDO');
    }
  },
};
```

### Buenas Prácticas Clave

1. **Pruebas**:
   - Mockea Supabase en pruebas unitarias
   - Usa datos reales (en staging) para pruebas E2E
   - Cubre flujos críticos: ventas, ajustes de inventario

2. **Errores**:
   - Clasifica errores por módulo (InventarioError, POSError)
   - Usa códigos de error consistentes
   - Registra errores antes de mostrarlos al usuario

3. **Configuración**:
   - Valida variables de entorno con Zod
   - Usa diferentes proyectos Supabase para dev/staging/prod

4. **Modelos**:
   - Valida todos los datos al entrar/salir de Supabase
   - Usa tipos estrictos para operaciones financieras

5. **Performance**:
   - Usa transacciones RPC para operaciones complejas
   - Implementa paginación en consultas grandes
   - Cachea datos maestros (insumos, platos)
### Aclaracion del uso de Supabase
solo aplica las buenas practicas de integracion a supabase o en general practicas que incluyan el uso de Supabase si yo doy la orden y conecto el un MCP de supabase a ti

## 🔄 Flujo de Trabajo con Git

### Estrategia de Ramas

- `main` - Código listo para producción
- `develop` - Rama de integración para características
- `feature/*` - Nuevas características
- `fix/*` - Corrección de errores
- `docs/*` - Actualizaciones de documentación
- `refactor/*` - Refactorización de código
- `test/*` - Adiciones o correcciones de pruebas

### Formato de Mensajes de Commit

Nunca incluyas código claude, o escrito por código claude en los mensajes de commit

```
<tipo>(<ámbito>): <asunto>

<cuerpo>

<pie>
``
Tipos: feat, fix, docs, style, refactor, test, chore

Ejemplo:
```

feat(auth): añadir autenticación de dos factores

- Implementar generación y validación TOTP
- Añadir generación de código QR para apps autenticadoras
- Actualizar modelo de usuario con campos 2FA

Cierra #123

### Resumen de Flujo de Trabajo GitHub Flow

main (protegida) ←── PR ←── feature/tu-característica
↓ ↑
deploy development

### Flujo de Trabajo Diario:

1. git checkout main && git pull origin main
2. git checkout -b feature/nueva-característica
3. Haz cambios + pruebas
4. git push origin feature/nueva-característica
5. Crea PR → Revisión → Merge a main

#### Prioridad: Alta (Seguridad y Estabilidad)
1. **Gestión de secretos y entorno**
   - Añadir archivo `env.example` con únicamente las variables públicas documentadas y ejemplos de formato.
   - **Prohibir** el commit de archivos `.env` reales mediante un hook `pre-commit` y una regla en `.gitignore`.
   - Documentar explícitamente qué variables son públicas (frontend) y cuáles son secretas (backend). Ejemplo:
     - `VITE_SUPABASE_URL` — pública (frontend)
     - `VITE_SUPABASE_KEY` — **anon/public** (frontend). **Nunca** colocar `service_role` en el cliente.
     - `SUPABASE_SERVICE_ROLE` — secreta (solo en backend / funciones / CI).
   - Añadir script de CI que escanee secrets (ej. `git-secrets`) y bloquee merges si se detectan claves en commits.

2. **Row Level Security (RLS) y permisos**
   - Añadir checklist obligatorio antes de producción:
     - Definir RLS por tabla (leer, insertar, actualizar, borrar).
     - Incluir tests automatizados que verifiquen accesos (integration/e2e) para roles estándar (anon, authenticated, admin).
     - Versionar y documentar las políticas RLS en `db/rls/` junto con ejemplos de roles y casos de prueba.
   - Recomendar prácticas: minimizar permisos por defecto, conceder permisos por funciones server-side cuando se requieran privilegios.

3. **Migraciones, seeds y backups**
   - Añadir carpeta `db/migrations/` con migraciones versionadas (ej.: formato `YYYYMMDDHHMM_descripcion.sql`).
   - Incluir `db/seeds/` para datos de staging y `db/fixtures/` para pruebas e2e.
   - Política de backups: respaldos diarios automatizados, retención mínima 30 días y verificación de restauración anual documentada.

#### Prioridad: Media (Calidad de Código y Colaboración)
4. **CI y calidad de código**
   - Agregar pipeline CI (GitHub Actions) con pasos mínimos:
     1. Lint (ESLint + Prettier)
     2. Type-check (tsc) si aplica
     3. Tests unitarios (Jest)
     4. Tests E2E en staging (Cypress) — opcional por PR grande
     5. Escaneo de secretos
     6. Generación de artefactos / build
   - Usar `husky` + `lint-staged` para hooks locales (formateo y lint antes de commit).

5. **Convenciones de stack y nombres**
   - Declarar el stack oficial en la cabecera del repo: `React + TypeScript + Supabase`.
   - Convenciones:
     - Carpetas: `kebab-case` → `modules/inventario/`
     - Componentes React: `PascalCase` → `InventarioPage.tsx`
     - Hooks: `useCamelCase` → `useAuth.ts`
     - Servicios/Repositorios/Utils: `camelCase` → `insumoService.ts`
     - Tipos/Interfaces: `PascalCase` → `Insumo.ts`
     - Constantes: `SCREAMING_SNAKE_CASE`
   - Añadir tabla de ejemplos rápida en el doc para referencia.
7. **Documentación técnica**
   - Incluir ERD (diagrama entidad-relación) en `docs/erd.png` y Data Dictionary en `docs/data-dictionary.md`.
   - Añadir `API_CONTRACT.md` con shapes/ejemplos (OpenAPI o JSON Schema) para RPCs y endpoints críticos.
   - README: pasos de setup claros (dev/staging/prod), cómo ejecutar migraciones y cómo restaurar backups.

8. **Observabilidad**
   - Integrar logging estructurado (pino/winston) y Sentry (errors + performance) con instrucciones para desactivar en dev.
   - Definir métricas mínimas: errores 5xx, latencia de RPC críticas, tasa de ventas por minuto.

9. **Tests y coverage**
   - Objetivo de coverage: ≥ 70% en servicios críticos (ventas, inventario).
   - Mocks de Supabase para unit tests; E2E en staging con datos controlados; evitar ejecutar tests con la DB de producción.

#### Plantillas y artifacts (copiar en el repo)
- `env.example`
- `db/migrations/README.md` (cómo crear y aplicar migraciones)
- `CONTRIBUTING.md`
- `PULL_REQUEST_TEMPLATE.md`
- `CODEOWNERS`
- `ci/github-actions.yml` (ejemplo pipeline mínimo)
### si ves que la estructura del proyecto (sus nombres) no coinciden con las convenciones de nomeclaturas que usamos pues cambialas, estas convenciones deben de ser globales