---
title: استنساخ HackerNews
type: examples
order: 12
---

> هذا هو HackerNews استنساخ مبنية على HackerNews الرسمية Firebase API، Vue 2.0 + Vue Router + Vuex، مع تصيير جهة الخلفية.

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

- تصيير جهة المستخدم
  - Vue + Vue Router + Vuex للعمل معا
  - بيانات جهة المستخدم قبل جلبها
  - حالة جهة المستخدم & إماهة DOM
- مكون Vue للملف الوحيد
  - Hot-reload قيد التطوير
  - إستخلاص CSS للإنتاح
- الوقت الحقيقي لتحديث قائمة مع تأثير القلب

## نظرة عامة عن هندسة

<img width="973" alt="Hackernew clone architecture overview" src="../../images/hn-architecture.png">
