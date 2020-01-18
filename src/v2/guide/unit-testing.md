---
title: اختبار الوحدة
type: guide
order: 402
---

> يحتوي [Vue CLI](https://cli.vuejs.org) على خيارات مدمجة لاختبار الوحدة باستخدام [Jest](https://github.com/facebook/jest) أو [Mocha](https://mochajs.org/) . لدينا أيضًا [استخدام اختبار Vue](https://vue-test-utils.vuejs.org/) الرسمي الذي يوفر إرشادات أكثر تفصيلًا عن الإعدادات المخصصة.

## تأكيدات بسيطة

ليس عليك القيام بأي شيء خاص في مكوناتك لجعلها قابلة للاختبار. تصدير الخيارات الأولية:

``` html
<template>
  <span>{{ message }}</span>
</template>

<script>
  export default {
    data () {
      return {
        message: 'hello!'
      }
    },
    created () {
      this.message = 'bye!'
    }
  }
</script>
```

بعد ذلك ، قم باستيراد خيارات المكونات إلى جانب Vue ، ويمكنك تقديم العديد من التأكيدات الشائعة (هنا نستخدم تأكيدات Jasmine/Jest style "تتوقع" فقط كمثال):

``` js
// Import Vue and the component being tested
import Vue from 'vue'
import MyComponent from 'path/to/MyComponent.vue'

// Here are some Jasmine 2.0 tests, though you can
// use any test runner / assertion library combo you prefer
describe('MyComponent', () => {
  // Inspect the raw component options
  it('has a created hook', () => {
    expect(typeof MyComponent.created).toBe('function')
  })

  // Evaluate the results of functions in
  // the raw component options
  it('sets the correct default data', () => {
    expect(typeof MyComponent.data).toBe('function')
    const defaultData = MyComponent.data()
    expect(defaultData.message).toBe('hello!')
  })

  // Inspect the component instance on mount
  it('correctly sets the message when created', () => {
    const vm = new Vue(MyComponent).$mount()
    expect(vm.message).toBe('bye!')
  })

  // Mount an instance and inspect the render output
  it('renders the correct message', () => {
    const Constructor = Vue.extend(MyComponent)
    const vm = new Constructor().$mount()
    expect(vm.$el.textContent).toBe('bye!')
  })
})
```

## كتابة مكونات قابلة للاختبار

يتم تحديد ناتج تصيير المكون في المقام الأول عن طريق "props" التي يتلقاها. إذا كان إخراج التجسيد الخاص بالمكون يعتمد فقط على الدعائم الخاصة به، فسيصبح من السهل اختباره، على غرار تأكيد قيمة الإرجاع للدالة الخالصة ذات الوسائط المختلفة. خذ مثالا مبسطا:

``` html
<template>
  <p>{{ msg }}</p>
</template>

<script>
  export default {
    props: ['msg']
  }
</script>
```

يمكنك تأكيد ناتج التجسيد باستخدام الدعائم المختلفة باستخدام خيار `propsData`:

``` js
import Vue from 'vue'
import MyComponent from './MyComponent.vue'

// helper function that mounts and returns the rendered text
function getRenderedText (Component, propsData) {
  const Constructor = Vue.extend(Component)
  const vm = new Constructor({ propsData: propsData }).$mount()
  return vm.$el.textContent
}

describe('MyComponent', () => {
  it('renders correctly with different props', () => {
    expect(getRenderedText(MyComponent, {
      msg: 'Hello'
    })).toBe('Hello')

    expect(getRenderedText(MyComponent, {
      msg: 'Bye'
    })).toBe('Bye')
  })
})
```

## تأكيد التحديثات غير المتزامنة

نظرًا لأن Vue [تنفذ تحديثات DOM بشكل غير متزامن](reactivity.html#Async-Update-Queue)، فيجب إجراء التأكيدات على تحديثات DOM الناتجة عن تغيير الحالة في رد اتصال `Vue.nextTick`:

``` js
// Inspect the generated HTML after a state update
it('updates the rendered message when vm.message updates', done => {
  const vm = new Vue(MyComponent).$mount()
  vm.message = 'foo'

  // wait a "tick" after state change before asserting DOM updates
  Vue.nextTick(() => {
    expect(vm.$el.textContent).toBe('foo')
    done()
  })
})
```

لمزيد من المعلومات المتعمقة حول اختبار الوحدة في Vue، تحقق من [Vue Test Utils](https://vue-test-utils.vuejs.org/), وإدخال كتاب الطبخ الخاص بنا حول [مكونات اختبار وحدة الاختبار](https://vuejs.org/v2/cookbook/unit-testing-vue-components.html).
