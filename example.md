---
theme: ./slidev-theme-vzhyx
transition: slide-left
mdc: true
duration: 35min
meetup: MoscowCSS 29
date: 06 ноября 2025
tags: '#moscowcss #Школа21'
layout: cover
---

# Данные по ссылке + 4 нюанса

---
transition: slide-left
layout: simple-slide
---

## Кто здесь?
<div class="whoami-layout">
  <div class="whoami-left">
    <v-clicks>
      <ul>
        <li>Соорг самого стильного митапа Москвы</li>
        <li>Влюблён во фронтенд</li>
        <li>Член программного комитета HolyJS</li>
        <li>Участник и контрибьютор сообществ</li>
        <li>Cтудент магистратуры ИТМО</li>
      </ul>
    </v-clicks>
  </div>
  <div class="whoami-right">
    <WhoAmI :images="['/images/whoami/1.jpg', '/images/whoami/2.jpg', '/images/whoami/3.jpg']" alt="Фото докладчика" />
  </div>
</div>


---
transition: slide-left
layout: center
---

## Уметь учиться эффективно


---
transition: slide-left
layout: simple-slide
---

## Жиза?

<div class="tri-grid">
  <v-clicks>
    <div class="tri-item tri-left">Пришёл</div>
    <div class="tri-item tri-right">Всё понял</div>
    <div class="tri-item tri-bottom">Всё забыл</div>
  </v-clicks>
</div>

---
transition: slide-left
layout: center
---

![](/images/slides/obsidian.png)


---
transition: slide-left
layout: simple-slide
---

## Флоу

<TransitionGroup tag="ul" name="ins-flow" class="flow-list">
  <li v-click="1" key="flow-1">Пришёл, чтобы слушать информацию</li>
  <li v-click="5" key="flow-1-2" class="flow-ins">А как понять?</li>
  <li v-click="2" key="flow-2">Понял смысл</li>
  <li v-click="3" key="flow-3">Записал заметку</li>
  <li v-click="6" key="flow-2-3" class="flow-ins">Как записать?</li>
  <li v-click="7" key="flow-2-4" class="flow-ins">Куда положить?</li>
  <li v-click="4" key="flow-4">Вернулся к ней</li>
  
</TransitionGroup>


---
transition: slide-left
layout: center
---

![](/images/slides/barbara_oakly.jpg)

---
transition: slide-left
layout: simple-slide
---

## Тезисы:

<v-clicks>

- Заинтересовать мозг
- Кривая забывания
- Система повторов, Anki
- Сфокусированное и рассеянное мышление
- Развитие памяти
- Мнемоника

</v-clicks>


---
transition: slide-left
layout: center
---

![](/images/slides/zametki.jpg)

---
transition: slide-left
layout: simple-slide
---

## Заметка Zettelkasten:

<v-clicks>

- Личная
- Атомарная
- Цельная
- Имеет ссылки

</v-clicks>

---
transition: slide-left
layout: center
---

<img src="/images/slides/graph.png" class="center-wide" />

---
transition: slide-left
layout: center
---

![](/images/slides/second_brain.jpg)


---
transition: slide-left
layout: simple-slide
---

## Структурирование PARA:

<v-clicks>

- **P**roject - достижимая цель
- **A**rea - долгосрочная цель
- **R**esource - библиотека знаний
- **A**rchive - архив

</v-clicks>

<v-after>

<div class="after-em">1 раз в неделю разбор заметок</div>

</v-after>


---
transition: slide-left
layout: center
---

## Медиазапросы и rem

---
transition: slide-left
layout: simple-slide
---

<div style="height: 3rem"></div>

![](/images/slides/font-size.png)

```css
html {
  font-size: 1rem; /* === 16px */
}
```

<div style="height: 3rem"></div>

<v-click>

![](/images/slides/font-large.png)

```css
html {
  font-size: 1rem; /* === 20px */
}
```

</v-click>


---
transition: slide-left
layout: simple-slide
---

````md magic-move
```css
@media (min-width: 48rem) { /* ??? */
  html: {
    font-size: 1rem /* ??? */
  }
}
```

```css
@media (min-width: 48rem) { /* 16 * 48 = 768 */
  html: {
    font-size: 1rem /* ??? */
  }
}
```

```css
@media (min-width: 48rem) { /* 16 * 48 = 768 */
  html: {
    font-size: 1rem /* 20 */
  }
}
```

````

<div style="height: 3rem"></div>

<v-click>

When used outside the context of an element (such as in media queries), these units refer to the computed font metrics corresponding to the initial values of the font property.

</v-click>

<div style="height: 3rem"></div>

<v-click>

initial = medium 

</v-click>

---
transition: slide-left
layout: simple-slide
---

## Субъективщина:

<v-clicks>

1. Медиазапросы в PX 
2. Шрифты в REM
3. Отступы - в PX

</v-clicks>


---
transition: slide-left
layout: simple-slide
---

## px + medium

<button class="btn btn-px"> Йа кнопко в пыхах! </button>

## rem + medium

<button class="btn btn-rem"> Йа кнопко в Рёмках! </button>


---
transition: slide-left
layout: simple-slide
---

## px + large

<button class="btn btn-px"> Йа кнопко в пыхах! </button>

## rem + large

<button class="btn btn-rem-big"> Йа кнопко в Рёмках! </button>


---
transition: slide-left
layout: simple-slide
---

## Чего заметили?

<v-clicks>

0. Как вести заметки
1. Проект "CSS Units"
2. Как браузер обрабатывает rem в целом
3. Как браузер обрабатывает rem в @media
4. Какие есть варианты комбинаций

</v-clicks>

---
transition: slide-left
layout: cover
meetup: MoscowCSS 29
date: 06 ноября 2025
tags: '#moscowcss #Школа21'
---

# Спасибо! <3 