---
layout: post
title: "Angular + Polymer Bridge"
date: 2017-08-08 20:14:09
description: ¡Usa webcomponents de Polymer en tu app Angular!
tags: Angular Polymer
categories: Frontend Samples
twitter_text: Angular + Polymer Bridge
author: aaron
---

Si siempre te ha gustado el enfoque de **Angular como Framework** FrontEnd para aplicaciones web pero no quieres renunciar
a la gran comunidad de los **Webcomponents de Polymer**, ¡Tengo una buena noticia para ti!

[@codebakery/origami](https://www.npmjs.com/package/@codebakery/origami) es un módulo de NPM que a partir de ahora puedes
 incluir en tus aplicaciones Angular 4 (o superior) para usar webcomponents de Polymer 2 con soporte para:
- Two-Way [( )] Databinding ✅
- Angular Template/Reactive Form Support ✅
- Polymer Templates (<iron-list>) ✅
- Angular Components in Polymer Templates ❌
- New Polymer elements defined in-project ✅
- OnPush Change Detection ✅
- Object/Array mutation detection ✅
- CSS custom property/mixin support ✅
- Ahead-of-Time Compliant ✅
- Bundled production-ready builds ✅

## Code
La guia de uso viene muy bien explicada en la documentación del modulo, pero si queréis verlo funcionando
he montado un ejemplo de uso en este [Plunk](https://plnkr.co/edit/Jb0b8lGjNpd5m1p8bIhM?p=preview).

[![Pluk Screenshot](/assets/img/Angular4+Polymer2Bridge/screenshot.png "Pluk Screenshot")](https://plnkr.co/edit/Jb0b8lGjNpd5m1p8bIhM?p=preview)

He añadido algunas notas con los aspectos que considero más relevantes en cuanto a su integración y uso en una app Angular.
Los he marcado con la tag ```@note```.

## Notes
- dependencia ```webcomponents-loader.js``` a incluir en el ```index.html``` de la app.
```html
  <script src="https://cdnjs.cloudflare.com/ajax/libs/webcomponentsjs/1.0.6/webcomponents-loader.js"></script>
```
- EL codigo fuente de los webcomponents, tiene que importarse tambien desde ```index.html```,
en la version actual no es posible cargarlo desde la template de los componentes angular de la app.
```html
<!-- must be in index.html -->
<link href="WEB_COMPONENT/WEB_COMPONENT.html" rel="import">
```
- El modulo ```@codebakery/origami``` ha de importarse en el modulo principal de la aplicación Angular.
```CUSTOM_ELEMENTS_SCHEMA``` de ```@angular/core``` debe definirse como schema del modulo para evitar errores cuando
Angular no encuentre algún componente, es en ese momento cuando el modulo ```@codebakery/origami``` lo buscará y tratará como webcomponent de Polymer,
informando de un error por consola si no lo halla.

```javascript
import { PolymerModule } from '@codebakery/origami';
...

@NgModule({
  imports: [
    PolymerModule.forRoot(),// Only import .forRoot() once and at the highest level
...
  schemas: [CUSTOM_ELEMENTS_SCHEMA],
...
})
export class AppModule {}
```

- Para **bindear** propiedades o eventos, hay que especificarlo en el webcomponent mediante los atributos:
    - ```ironControl``` angular property --> polymer attribute

    - ```emitChanges```  polymer attribute <-- angular property
```html
<paper-input emitChanges ironControl [(ngModel)]="myComponentVar">
</paper-input>
```

___
Espero que os sirva y pronto pongáis en comunión estos 2 maravillosos mundos en vuestras aplicaciones webs!
