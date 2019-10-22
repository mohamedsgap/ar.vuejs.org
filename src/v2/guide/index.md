---
title: مقدمة
type: guide
order: 2
---

## ما هي Vue.js؟

Vue (تنطق ڤيو) هي **اطار عمل** لبناء واجهات المستخدم. بعكس اطر العمل الاخرى, Vue تم تصميمها من الالف الى الياء بحيث يمكن اعتمادها تدريجياً. المكتبة الاساسية تركز على طبقة العرض فقط ومن السهل جداً اختيار ودمج مكتبات او مشاريع اخرى. ومن ناحية اخرى فإن Vue قادرة تمام على بناء وتشغيل تطبيقات معقدة من نوع الصفحة الواحدة عند استخدامها مع [الادوات الحديثة](single-file-components.html) و [المكتبات الداعمة](https://github.com/vuejs/awesome-vue#components--libraries).

اذا كنت ترغب في معرفة المزيد عن Vue, فقد قمنا <a id="modal-player"  href="#">بعمل فيديو</a> ليأخذ بيدك ويساعدك على معرفة المبادئ الاساسية وبناء مشروع تجريبي.

اذا كنت مطور واجهات مستخدم ذو خبرة وتريد معرفة كيف يتم مقارنة Vue مع المكتبات و اطر العمل الاخرى, تفحص صفحة [مقارنة Vue مع اطر العمل الاخرى](comparison.html).

<div class="vue-mastery"><a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="noopener" title="Free Vue.js Course">مشاهدة كورس فيديو مجاني على موقع Vue Mastery</a></div>

## البداية

<a class="button" href="installation.html">التنصيب</a>

<p class="tip">هذا الدليل يفترض ان لديك معرفة متوسطة بـHTML و CSS و Javascript. اذا كنت جديد تمام على تطوير واجهات المستخدم, فإنها ليست فكرة جيدة للقفز الى هذه المرحلة والتعامل مع اطار عمل كخطوتك الاولى. قن بتعلم بعض المبادئ الهامة وقم بالرجوع الى هذا الدليل,الخبرة السابقة باطر عمل اخرى قد يساعد ولكنه ليس مطلوب.</p>

اسهل طريقة تجرب بها Vue.js هي باستخدام [  مثال "اهلا بالعالم!" على منصة JSFiddle ](https://jsfiddle.net/chrisvfritz/50wL7mdz/). لك مطلق الحرية في فتح هذا الرابط في تبويب جديد ومتابعة الدليل وتطبيق الامثلة او يمكنك <a href="https://gist.githubusercontent.com/chrisvfritz/7f8d7d63000b48493c336e48b3db3e52/raw/ed60c4e5d5c6fec48b0921edaed0cb60be30e87c/index.html" target="_blank" download="index.html" rel="noopener noreferrer">انشاء ملف <code>index.html</code></a> وتضمين Vue باستخدام الكود التالي:

``` html
<!-- development version, includes helpful console warnings -->
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```

او:

``` html
<!-- production version, optimized for size and speed -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
```

صفحة [التنصيب](installation.html) توفر المزيد من الخيارات لتنصيب واستعمال Vue. ملاحظة: نحن **لا ننصح** المبتدئين بالبدء بـ`vue-cli` "ادوات سطر الاوامر", خاصة اذا لم تكن لديك معرفة بادوات بناء Node.js.

اذا كنت تفضل شيئاً اكثر تفاعلاً, يمكنك القاء نظرة على [هذا الدرس على منصة Scrimba](https://scrimba.com/playlist/pXKqta), والذي يعطيك خليط من دروس الفيديو ومشغل اكواد رائع يمكنك تشغيله وايقافه في اي وقت.

## المعالجة التعريفية

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cQ3QVcr" target="_blank" rel="noopener noreferrer">قم بتجربة الدرس على موقع Scrimba</a></div>

يقع اساس Vue.js على نظام يمكننا من معالجة البيانات وعرضها في الـDOM بالشكل البسيط التالي:

``` html
<div id="app">
  {{ message }}
</div>
```
``` js
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
```
{% raw %}
<div id="app" class="demo">
  {{ message }}
</div>
<script>
var app = new Vue({
  el: '#app',
  data: {
    message: 'Hello Vue!'
  }
})
</script>
{% endraw %}

لقد انشأنا بالفعل اول تطبيق باستخدام Vue. قامت Vue بعمل الكثير من المعالجه لتوفر لنا هذه السلاسة, فالان بيانات حالة التطبيق وعنصر DOM مرتبطين بشكل تام وكل شيء الان **تفاعلي**. كيف نتأكد من ذلك؟ قم بتشغيل وحدة تشغيل الچافاسكريبت الموجودة في المستعرض الخاص بك (في هذه الصفحة) وقم باعادة تخصيص قيمة المتغير `app.message` الى اي قيمة اخرى. من المفترض ان ترى ان القيمة قد تغيرت في نتيجة المثال المعروض بالاعلى.

بالاضافة الى معالجة وعرض النصوص, يمكننا ايضاً ربط خواص العنصر بالشكل التالي:

``` html
<div id="app-2">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds
    to see my dynamically bound title!
  </span>
</div>
```
``` js
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'You loaded this page on ' + new Date().toLocaleString()
  }
})
```
{% raw %}
<div id="app-2" class="demo">
  <span v-bind:title="message">
    Hover your mouse over me for a few seconds to see my dynamically bound title!
  </span>
</div>
<script>
var app2 = new Vue({
  el: '#app-2',
  data: {
    message: 'You loaded this page on ' + new Date().toLocaleString()
  }
})
</script>
{% endraw %}

هنا سوف نتعرض لشيء جديد. خاصية `v-bind` التي تراها يطلق عليها **موجه** او **directive**. الموجهات تبدأ بـ`v-` لتحديد الخواص الخاصة التي يتم توفيرها من قبل Vue, و كما قد تكون توقعت, فان هذه الموجهات تقوم بتطبيق تصرفات متفاعلة خاصة على عنصر DOM المعالج والمعروض. فهنا نقول بشكل بسيط "اجعل خاصية العنوان `title` للعنصر متزامنة مع قيمة الخاصية `message` في هذه النسخة من Vue."

اذا قمت بفتح وحدة تحكم الجافاسكريبت في المستعرض مره اخرى وقمت بادخال `app2.message = 'some new message'`, سوف ترى مرة اخرى ان القيمة انعكست بشكل مباشر على خاصية العنصر `title`.

## الشروط والتكرارات

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQe4SJ" target="_blank" rel="noopener noreferrer">قم بتجربة الدرس على موقع Scrimba</a></div>

من السهل تبديل ظهور العناصر ايضا:

``` html
<div id="app-3">
  <span v-if="seen">Now you see me</span>
</div>
```

``` js
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
```

{% raw %}
<div id="app-3" class="demo">
  <span v-if="seen">Now you see me</span>
</div>
<script>
var app3 = new Vue({
  el: '#app-3',
  data: {
    seen: true
  }
})
</script>
{% endraw %}

قم الان بالتجربة مره اخرى وادخل `app3.seen = false` في وحدة تحكم الجافاسكريبت. الان يجب ان تكون قيمة الخاصية قد اختفت.

هذا المثال يوضح انه يمكننا ربط البيانات ليس فقط بالنصوص والخصائص ولكن ايضا بـ**الهيكل** خالص بعنصر DOM. كما توفر Vue ايضا نظام مؤثرات انتقالات قوي يمكنه تطبيق [مؤثرات الانتقالات](transitions.html) بشكل تلقائي عندما يتم ادخال/تحديث/ازالة العناصر باستخدام Vue.

يوجد ايضا العديد من الموجهات الاخرى والتي لدى كل منها استخدامها الخاص. على سبيل المثال الموجه `v-for` يمكن استخدامه لعرض قائمة من العناصر باستخدام البيانات الموجودة في مصفوفة:

``` html
<div id="app-4">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
```
``` js
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Learn JavaScript' },
      { text: 'Learn Vue' },
      { text: 'Build something awesome' }
    ]
  }
})
```
{% raw %}
<div id="app-4" class="demo">
  <ol>
    <li v-for="todo in todos">
      {{ todo.text }}
    </li>
  </ol>
</div>
<script>
var app4 = new Vue({
  el: '#app-4',
  data: {
    todos: [
      { text: 'Learn JavaScript' },
      { text: 'Learn Vue' },
      { text: 'Build something awesome' }
    ]
  }
})
</script>
{% endraw %}

قم الان بالتجربة في وحدة تحكم الجافاسكريبت وادخل `app4.todos.push({ text: 'New item' })`. الان يجب ان تكون قد رأيت انه تم اضافة عنصر جديد الى القائمة.

## معالجة مدخلات المستخدم

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/czPNaUr" target="_blank" rel="noopener noreferrer">قم بتجربة الدرس على موقع Scrimba</a></div>

للسماح للمستخدمين بالتفاعل مع تطبيقك, يمكنك استخدام الموجه `v-on` لربط افعال المستخدم لتشغيل دوال محددة في تطبيقك:

``` html
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```
``` js
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
```
{% raw %}
<div id="app-5" class="demo">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
<script>
var app5 = new Vue({
  el: '#app-5',
  data: {
    message: 'Hello Vue.js!'
  },
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  }
})
</script>
{% endraw %}

لاحظ ان في هذه الدالة نقوم بتحديث حالة التطبيق بدون لمس عنصر DOM. جميع التعديلات التي تتم على عنصر DOM يتم معالجتها من قبل Vue,  والكود الذي تقوم بكتابته يقوم بالتركيز اكثر على المنطق الاساسي الخاص بالتطبيق.

Vue ايضاً تقوم بتوفير موجه `v-model` والذي يقوم بعمل ربط ثنائي الاتجاه بين اي عناصر نماذج HTML وحالة التطبيق بشكل سهل جداً:

``` html
<div id="app-6">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
```
``` js
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
```
{% raw %}
<div id="app-6" class="demo">
  <p>{{ message }}</p>
  <input v-model="message">
</div>
<script>
var app6 = new Vue({
  el: '#app-6',
  data: {
    message: 'Hello Vue!'
  }
})
</script>
{% endraw %}

## انشاء المكونات

<div class="scrimba"><a href="https://scrimba.com/p/pXKqta/cEQVkA3" target="_blank" rel="noopener noreferrer">قم بتجربة الدرس على موقع Scrimba</a></div>

نظام المكونات هو مبدأ هام في Vue, لانه يسمح لنا ببناء تطبيقات كبيرة الحجم عن طريق تقسيمها الى مكونات صغيرة قائمة بذاتها ويمكن اعادة استخدامها. اذا فكرنا في الامر, فاي نوع تطبيق تقريباً يكون مكون شجرة من المكونات:

![شجرة المكون](/images/components.png)

في Vue, المكون هو بشكل اساسي نسخة من Vue مع مجموعة من الخصائص مسبقة التعريف. تسجيل وتعريف المكونات في Vue يتم بشكل بسيط كالتالي:

``` js
// Define a new component called todo-item
Vue.component('todo-item', {
  template: '<li>This is a todo</li>'
})
```

الان يمكنك استخدام المكون السابق في اي مكون اخر كالتالي:

``` html
<ol>
  <!-- Create an instance of the todo-item component -->
  <todo-item></todo-item>
</ol>
```

ولكن هذا سيتسبب في عرض نفس النصوص لكل عنصر, لذلك يجب ان يكون لدينا امكانية تمرير البيانات من المكون الرئيسي الى المكونات الفرعية. هيا بنا نغير تعريف المكون لنجعله يقبل 'خاصية' [prop](components.html#Props):

``` js
Vue.component('todo-item', {
  // The todo-item component now accepts a
  // "prop", which is like a custom attribute.
  // This prop is called todo.
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
```

الان يمكننا تمرير بيانات العنصر لكل مكون مكرر باستخدام `v-bind`:

``` html
<div id="app-7">
  <ol>
    <!--
      Now we provide each todo-item with the todo object
      it's representing, so that its content can be dynamic.
      We also need to provide each component with a "key",
      which will be explained later.
    -->
    <todo-item
      v-for="item in groceryList"
      v-bind:todo="item"
      v-bind:key="item.id"
    ></todo-item>
  </ol>
</div>
```
``` js
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})

var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
```
{% raw %}
<div id="app-7" class="demo">
  <ol>
    <todo-item v-for="item in groceryList" v-bind:todo="item" :key="item.id"></todo-item>
  </ol>
</div>
<script>
Vue.component('todo-item', {
  props: ['todo'],
  template: '<li>{{ todo.text }}</li>'
})
var app7 = new Vue({
  el: '#app-7',
  data: {
    groceryList: [
      { id: 0, text: 'Vegetables' },
      { id: 1, text: 'Cheese' },
      { id: 2, text: 'Whatever else humans are supposed to eat' }
    ]
  }
})
</script>
{% endraw %}

هذا مثال بسيط ولكن استطعنا ان نقوم بتقسيم التطبيق الى وحدتين صغيرتين وقد تم فصل المكون الفرعي عن المكون الاساسي باستخدام خواص المكونات "props" يمكننا الان تحسين المكون `<todo-item>` باستخدام قالب ومنطق اكثر تعقيداً بدون التأثير على التطبيق الاساسي.

في التطبيقات الكبيرة, من الضروري تقسيم التطبيق الى مكونات او وحدات صغيرة لنجعل عملية التطوير اكثر سهولة. سوف نتكلم اكثر عن المكونات [لاحقاً في هذا الدليل](components.html), ولكن فيما يلي مثال وهي عن شكل القالب المتوقع مع المكونات:

``` html
<div id="app">
  <app-nav></app-nav>
  <app-view>
    <app-sidebar></app-sidebar>
    <app-content></app-content>
  </app-view>
</div>
```

### العلاقة مع العناصر المخصصة

ربما قد لاحظت ان مكونات Vue تشبه الى حد كبير **العناصر المخصصة**, والتي هي جزء من [مواصفات مكونات الويب](https://www.w3.org/wiki/WebComponents/). وهذا لان طريقة كتابة الكود في مكونات Vue تم نمذجتها طبقاً لهذه المواصفات. فمكونات Vue تستخدم [Slot API](https://github.com/w3c/webcomponents/blob/gh-pages/proposals/Slots-Proposal.md) و الخاصية المميزة `is`. على اي حال, يوجد بعض الاختلافات الاساسية:

١. مواصفات مكونات الويب تم الانتهاء منها ويتم استخدامها في كل المستعرضات. Safari 10.1+, Chrome 54+ and Firefox 63+ يقومون بدعم مكونات الويب. وعند الحاجة يمكن وضع مكونات Vue داخل عناصر اساسية مخصصة.

٢.مكونات Vue توفر مميزات هامة والتي ليست موجودة في العناصر المخصصة, نخص بالذكر نقل البيانات من مكون لأخر والاحداث المخصصة وتكامل ادوات البناء.

ايضاً Vue لا تستخدم العناصر المخصصة داخلياً, فانها لديها [امكانية تشغيل متداخلة](https://custom-elements-everywhere.com/#vue) عندما نريد استخدام او توزيع المكونات كعناصر مخصصة. دوات Vue لسطر الاوامر ايضا تدعم بناء مكونات Vue والذين يسجلون نفسهم كعناصر مخصصة.

## هل انت جاهز للمزيد؟

لقد قمنا بشكل مختصر التحدث عن ابسط المميزات في Vue - بقية هذا الدليل سوف تغطي المميزات الاخرى ومميزات اكثر تقدما بشكل تفصيلي اكثر. لذا تأكد جيداً من استكمال قرائتك للدليل بالكامل!

<div id="video-modal" class="modal"><div class="video-space" style="padding: 56.25% 0 0 0; position: relative;"><iframe src="https://player.vimeo.com/video/247494684" style="height: 100%; left: 0; position: absolute; top: 0; width: 100%; margin: 0" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div><script src="https://player.vimeo.com/api/player.js"></script><p class="modal-text">الفيديو بواسطة <a href="https://www.vuemastery.com" target="_blank" rel="noopener" title="Vue.js Courses on Vue Mastery">Vue Mastery</a>. مشاهدة كورس مدرسة ڤيو Vue Mastery المجاني <a href="https://www.vuemastery.com/courses/intro-to-vue-js/vue-instance/" target="_blank" rel="noopener" title="Vue.js Courses on Vue Mastery">مقدمة الى Vue</a>.</div>
