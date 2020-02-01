---
title: نشر الإنتاج
type: guide
order: 404
---

> يتم تمكين معظم النصائح أدناه افتراضيًا إذا كنت تستخدم [Vue CLI](https://cli.vuejs.org). هذا القسم مناسب فقط إذا كنت تستخدم إعداد بناء مخصص.

## تشغيل وضع الإنتاج

أثناء التطوير، تقدم Vue الكثير من التحذيرات لمساعدتك في الأخطاء والمخاطر الشائعة. ومع ذلك، فإن سلاسل التحذير هذه تصبح غير مجدية في الإنتاج وتضخيم حجم حمولة التطبيق. بالإضافة إلى ذلك، تحتوي بعض عمليات التحقق من التحذير هذه على تكاليف وقت تشغيل صغيرة يمكن تجنبها في وضع الإنتاج.

### بدون أدوات البناء

إذا كنت تستخدم البنية الكاملة، أي تضمين Vue مباشرة عبر علامة البرنامج النصي بدون أداة إنشاء، تأكد من استخدام الإصدار المصغر (`vue.min.js`) للإنتاج. يمكن العثور على كلا الإصدارين في [دليل التثبيت](installation.html#Direct-lt-script-gt-Include).

### مع أدوات البناء

عند استخدام أداة إنشاء مثل Webpack أو Browserify، سيتم تحديد وضع الإنتاج بواسطة `process.env.NODE_ENV` داخل شفرة مصدر Vue، وسيكون في وضع التطوير افتراضيًا. توفر كلتا أدوات التصميم طرقًا للكتابة فوق هذا المتغير لتمكين وضع الإنتاج الخاص بـ Vue، وسيتم تجريد التحذيرات بواسطة المصغرات أثناء الإنشاء. تحتوي جميع قوالب vue-cli على هذه التكوينات المسبقة لك، لكن سيكون من المفيد معرفة كيفية القيام بذلك:

#### Webpack

In Webpack 4+, you can use the `mode` option:

``` js
module.exports = {
  mode: 'production'
}
```

But in Webpack 3 and earlier, you'll need to use [DefinePlugin](https://webpack.js.org/plugins/define-plugin/):

``` js
var webpack = require('webpack')

module.exports = {
  // ...
  plugins: [
    // ...
    new webpack.DefinePlugin({
      'process.env.NODE_ENV': JSON.stringify('production')
    })
  ]
}
```

#### Browserify

- Run your bundling command with the actual `NODE_ENV` environment variable set to `"production"`. This tells `vueify` to avoid including hot-reload and development related code.

- Apply a global [envify](https://github.com/hughsk/envify) transform to your bundle. This allows the minifier to strip out all the warnings in Vue's source code wrapped in env variable conditional blocks. For example:

  ``` bash
  NODE_ENV=production browserify -g envify -e main.js | uglifyjs -c -m > build.js
  ```

- Or, using [envify](https://github.com/hughsk/envify) with Gulp:

  ``` js
  // Use the envify custom module to specify environment variables
  var envify = require('envify/custom')

  browserify(browserifyOptions)
    .transform(vueify)
    .transform(
      // Required in order to process node_modules files
      { global: true },
      envify({ NODE_ENV: 'production' })
    )
    .bundle()
  ```

- Or, using [envify](https://github.com/hughsk/envify) with Grunt and [grunt-browserify](https://github.com/jmreidy/grunt-browserify):

  ``` js
  // Use the envify custom module to specify environment variables
  var envify = require('envify/custom')

  browserify: {
    dist: {
      options: {
        // Function to deviate from grunt-browserify's default order
        configure: b => b
          .transform('vueify')
          .transform(
            // Required in order to process node_modules files
            { global: true },
            envify({ NODE_ENV: 'production' })
          )
          .bundle()
      }
    }
  }
  ```

#### Rollup

Use [rollup-plugin-replace](https://github.com/rollup/rollup-plugin-replace):

``` js
const replace = require('rollup-plugin-replace')

rollup({
  // ...
  plugins: [
    replace({
      'process.env.NODE_ENV': JSON.stringify( 'production' )
    })
  ]
}).then(...)
```

## Pre-Compiling Templates

When using in-DOM templates or in-JavaScript template strings, the template-to-render-function compilation is performed on the fly. This is usually fast enough in most cases, but is best avoided if your application is performance-sensitive.

The easiest way to pre-compile templates is using [Single-File Components](single-file-components.html) - the associated build setups automatically performs pre-compilation for you, so the built code contains the already compiled render functions instead of raw template strings.

If you are using Webpack, and prefer separating JavaScript and template files, you can use [vue-template-loader](https://github.com/ktsn/vue-template-loader), which also transforms the template files into JavaScript render functions during the build step.

## Extracting Component CSS

When using Single-File Components, the CSS inside components are injected dynamically as `<style>` tags via JavaScript. This has a small runtime cost, and if you are using server-side rendering it will cause a "flash of unstyled content". Extracting the CSS across all components into the same file will avoid these issues, and also result in better CSS minification and caching.

Refer to the respective build tool documentations to see how it's done:

- [Webpack + vue-loader](https://vue-loader.vuejs.org/en/configurations/extract-css.html) (the `vue-cli` webpack template has this pre-configured)
- [Browserify + vueify](https://github.com/vuejs/vueify#css-extraction)
- [Rollup + rollup-plugin-vue](https://vuejs.github.io/rollup-plugin-vue/#/en/2.3/?id=custom-handler)

## Tracking Runtime Errors

If a runtime error occurs during a component's render, it will be passed to the global `Vue.config.errorHandler` config function if it has been set. It might be a good idea to leverage this hook together with an error-tracking service like [Sentry](https://sentry.io), which provides [an official integration](https://sentry.io/for/vue/) for Vue.
