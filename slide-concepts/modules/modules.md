# Angular Module Metadata Properties

## What is an Angular Module?
An Angular module is a logical container for a cohesive block of code that organizes related components, directives, services, pipes, and other code elements. Modules help in organizing an application into manageable sections and allow lazy loading of features to improve performance.

Angular modules are defined using the `@NgModule` decorator, which adds metadata that describes how to compile the module and how to run the application.

## Angular Module Metadata Properties

Below is an explanation of the metadata properties used in the `@NgModule` decorator in Angular:

### 1. **declarations**
- Declares the components, directives, and pipes that belong to this module.
- These are the classes that are instantiated and used within the templates of this module.

### 2. **imports**
- Imports other modules whose exported classes are needed by component templates declared in this module.
- For example, `BrowserModule`, `FormsModule`, etc.

### 3. **providers**
- Registers the services that the module contributes to the global collection of services.
- These services will be available throughout the application unless a child module provides a different version.

### 4. **bootstrap**
- Identifies the root component that Angular should bootstrap when it starts the application.
- This is the entry point for the Angular application, typically the `AppComponent`.

### 5. **entryComponents**
- Specifies components that should be compiled when the module is defined, even if they aren’t referenced in the module’s templates.
- Used mostly for dynamically loaded components.

### 6. **exports**
- Declares the components, directives, and pipes that other modules can use.
- Anything listed here will be available to other modules that import this module.

### 7. **schemas**
- Allows you to define custom schemas.
  - **CUSTOM_ELEMENTS_SCHEMA**: Permits the use of custom elements in the module.
  - **NO_ERRORS_SCHEMA**: Suppresses errors for any unknown elements or attributes.

### 8. **id**
- A unique identifier for the module, used when lazy loading.
- This is optional and not commonly used but is handy for debugging or lazy-loading purposes.

### 9. **jit**
- This is a rarely used property that controls whether Just-in-Time (JIT) compilation is enabled or disabled for the module.

---

### Example Usage:

```typescript
import { NgModule, CUSTOM_ELEMENTS_SCHEMA, NO_ERRORS_SCHEMA } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';
import { AppComponent } from './app.component';
import { MyCustomComponent } from './my-custom/my-custom.component';
import { MyService } from './services/my-service.service';
import { RouterModule, Routes } from '@angular/router';
import { CommonModule } from '@angular/common';

// Routes configuration (example)
const routes: Routes = [
  { path: '', component: AppComponent },
  { path: 'custom', component: MyCustomComponent }
];

@NgModule({
  declarations: [
    AppComponent,          // Components, directives, and pipes that belong to this module
    MyCustomComponent
  ],
  imports: [
    BrowserModule,         // External modules used by this module
    FormsModule,
    HttpClientModule,
    RouterModule.forRoot(routes),
    CommonModule
  ],
  providers: [
    MyService              // Services that this module contributes to the global collection
  ],
  bootstrap: [
    AppComponent           // The main application view, called the root component, that hosts all other app views
  ],
  entryComponents: [
    MyCustomComponent      // Components that are not referenced in the template but are loaded dynamically
  ],
  exports: [
    MyCustomComponent      // Components, directives, and pipes that this module can export to other modules
  ],
  schemas: [
    CUSTOM_ELEMENTS_SCHEMA, // Allows custom elements to be used in the templates
    NO_ERRORS_SCHEMA        // Suppresses errors for any unknown elements or attributes
  ],
  id: 'app-module-id',        // An optional identifier for the module
  // Custom elements can be added here if needed (typically for libraries)
})
export class AppModule { }
