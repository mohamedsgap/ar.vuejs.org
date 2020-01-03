---
title: نسخة من HackerNews
type: examples
order: 12
---

> هذا مثال على نسخة من HackerNews مبني على API الرسمي الخاص بـHackerNews مع Vue 2.0،  Vue Router + Vuex، مع تصيير من جهة الخادم.

{% raw %}
<div style="max-width: 600px;">
  <a href="https://github.com/vuejs/vue-hackernews-2.0" target="_blank" rel="noopener noreferrer">
    <img style="width: 100%;" src="../../images/hn.png">
  </a>
</div>
{% endraw %}

> [عرض توضيحي حي](https://vue-hn.herokuapp.com/)
> ملاحظة: قد يحتاج العرض التوضيحي لبعض الوقت في الدوران إذا لم يصل إليه أحد لفترة معينة.
>
> [[المصدر](https://github.com/vuejs/vue-hackernews-2.0)]

## ميزات

- تصيير من جهة الخادم
  - Vue + Vue Router + Vuex للعمل معا
  - بيانات جهة الخادم قبل جلبها
  - حالة جهة المستخدم & إماهة DOM
- مكون Vue للملف الوحيد
  - Hot-reload قيد التطوير
  - استخلاص CSS للانتاج
- الوقت الحقيقي لتحديث قائمة مع تأثير القلب

## نظرة عامة عن هندسة

<img width="973" alt="Hackernew clone architecture overview" src="../../images/hn-architecture.png">
