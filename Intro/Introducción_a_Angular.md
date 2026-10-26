# Introducción a Angular

---

## 1. Pilares Fundamentales de Angular

* **Componentes:** Bloque básico de construcción compuesto por un segmento de plantilla HTML y su contraparte de TypeScript. Se busca que los componentes sean bloques de código pequeños, simples y reutilizables.
* **Servicios:** Permiten gestionar y compartir datos o lógica de negocio centralizada a lo largo de toda la aplicación.
* **Directivas:** Modificadores del comportamiento o estructura en el DOM. Se dividen en tres tipos:
  * **De componentes:** Directivas con una plantilla HTML reutilizable asociada.
  * **Estructurales:** Modifican la estructura del DOM añadiendo o eliminando elementos (ej. `*ngIf`, `*ngFor`).
  * **De atributos:** Cambian el comportamiento o aspecto de un elemento, componente o directiva existente (ej. `ngStyle`, `ngClass`).
* **Rutas:** Sistema que permite navegar y mostrar diferentes componentes en función de la URL del navegador.
* **Módulos:** Contenedores utilizados para agrupar componentes, servicios, directivas, rutas e incluso otros módulos relacionados (ej. Módulo de productos, clientes, autenticación, etc.).

---

## 2. Creación del Primer Proyecto

Previamente hay que tener instalado Angular.

Para crear y ejecutar una nueva aplicación en Angular desde la terminal:

```bash
# Crear un nuevo proyecto llamado 'bases'
ng new bases

# Opciones de configuración durante la instalación:
# ? Would you like to add Angular routing? No (para configurarlo manualmente)
# ? Which stylesheet format would you like to use? CSS

# Acceder a la carpeta del proyecto
cd bases

# Compilar y arrancar el servidor de desarrollo (abre automáticamente el navegador)
ng serve -o
```

---

## 3. Estructura del Proyecto

### Archivos Principales de Configuración

* **`tsconfig.json`**: Archivo principal de configuración de TypeScript.
* **`tsconfig.app.json`**: Extensión de la configuración de TypeScript específica para la aplicación.
* **`tsconfig.spec.json`**: Extensión de la configuración de TypeScript para la ejecución de pruebas unitarias.
* **`package.json`**: Archivo donde se declaran las dependencias del proyecto, scripts de ejecución y metadatos.
* **`package-lock.json`**: Registro exacto del árbol de dependencias instaladas.
* **`angular.json`**: Archivo de configuración global de la CLI de Angular (rutas de recursos, *styles* globales, *favicon*, etc.).
* **`.gitignore`**: Especifica los archivos y carpetas que Git debe ignorar (ej. `node_modules/`, `dist/`, `tmp/`).
* **`README.md`**: Documento con información general del proyecto.

### Carpetas Principales

* **`node_modules/`**: Contiene todas las librerías y dependencias instaladas.
* **`src/`**: Carpeta fuente donde se desarrolla el código de la aplicación.

---

## 4. Contenido de la Carpeta `src/`

### Archivos Raíz de `src/`

* **`index.html`**: Archivo HTML principal de la aplicación. Angular incrusta dinámicamente los componentes dentro de la etiqueta `<app-root></app-root>`.
* **`main.ts`**: Punto de entrada principal que arranca (*bootstrap*) el módulo raíz de la aplicación.
* **`polyfills.ts`**: Código para garantizar la compatibilidad entre diferentes navegadores web.
* **`styles.css`**: Hoja de estilos globales aplicables a toda la aplicación.

### Estructura Interna de `src/`

* **`assets/`**: Almacena recursos estáticos como imágenes, iconos, fuentes o archivos de sonido.
* **`environments/`**: Contiene las variables de entorno para los entornos de desarrollo (`environment.ts`) y producción (`environment.prod.ts`).
* **`app/`**: Contiene los componentes, módulos y servicios de la aplicación.

#### Archivos dentro de `src/app/`:

* **`app.component.html`**: Plantilla HTML visible para el usuario asociada al componente principal.
* **`app.component.css`**: Estilos exclusivos para el componente principal.
* **`app.component.ts`**: Clase TypeScript que contiene la lógica del componente principal.
* **`app.component.spec.ts`**: Archivo para pruebas unitarias del componente principal.
* **`app.module.ts`**: Módulo raíz donde se declaran los componentes y se importan los módulos necesarios.

---

## 5. Trabajo con el Componente Principal (`app`)

### Lógica del Componente (`app.component.ts`)

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',             // Etiqueta HTML personalizada para incrustar el componente
  templateUrl: './app.component.html', // Ruta a la plantilla HTML
  styleUrls: ['./app.component.css']  // Ruta a los estilos CSS
})
export class AppComponent {
  title: string = 'Mi primer angular';
  numero: number = 10;

  // Método para incrementar el contador
  Sumar() {
    this.numero += 1;
  }

  // Método parametrizado para incrementar o decrementar
  cambio(valor: number) {
    this.numero += valor;
  }
}
```

### Plantilla HTML (`app.component.html`)

```html
<!-- Interpolación de variables con llaves dobles {{ }} -->
<h1>{{ title }}</h1>

<!-- Event Binding utilizando paréntesis () -->
<button (click)="numero = numero - 1"> - </button>
<span> {{ numero }} </span>
<button (click)="numero = numero + 1"> + </button>

<hr>

<!-- Uso de métodos definidos en la clase -->
<button (click)="cambio(-1)"> Decrementar (-1) </button>
<span> {{ numero }} </span>
<button (click)="cambio(1)"> Incrementar (+1) </button>
```

---

## 6. Organización y Creación de Componentes

1. **Creación Manual de Componentes:**
   * Crear el archivo de plantilla (ej. `contador.component.html`).
   * Crear el archivo de lógica TypeScript (ej. `contador.component.ts`).
   * Registrar el nuevo componente en el array `declarations` dentro de `app.module.ts`.
   * Incluir su *selector* HTML en el componente principal (`app.component.html`).

2. **Organización de Carpetas:**
   * Excepto el componente principal `app.component`, todos los nuevos componentes deben agruparse en subcarpetas dentro de `src/app/`.
   * Si un componente está formado por subcomponentes, se deben organizar mediante subcarpetas internas.

---

## 7. Correspondencia con el Patrón MVC

| Patrón MVC | Elemento principal en Angular | Archivo / Artefacto típico | Función en la aplicación |
| :--- | :--- | :--- | :--- |
| **Vista** | Plantilla HTML + Estilos | `mi-componente.component.html` / `.css` | Muestra la interfaz gráfica al usuario. |
| **Controlador** | Clase del Componente | `mi-componente.component.ts` (`@Component`) | Atiende los eventos de la vista y coordina los datos. |
| **Modelo** | Interfaces + Servicios | `usuario.model.ts` y `usuario.service.ts` | Define tipos de datos, realiza peticiones HTTP y maneja reglas de negocio. |
