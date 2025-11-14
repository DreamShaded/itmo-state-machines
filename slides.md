---
theme: ./slidev-theme-vzhyx
transition: slide-left
mdc: true
duration: 35min
meetup: Прозоров Троицкий
date: Исследование экосистем веб-языков и веб-технологий
tags: '#ИТМО'
layout: cover
---

# Паттерн Конечный Автомат (FSM)

---
transition: slide-left
layout: center
---

## Основная проблема фронтенда:

<v-click>

## Состояния! 

![](/images/slides/crying.jpg)

</v-click>

---
transition: slide-left
layout: center
---

## Состояние это:

<v-clicks>
  <div class="state-def">
    Формально: набор переменных и свойств объекта в текущий момент времени
  </div>

  <div class="state-def">Проще: Данные, которые определяют, как выглядит и работает интерфейс прямо сейчас </div>
</v-clicks>


---
transition: slide-left
layout: simple-slide
---

## Простой пример: лампочка

<div class="lamp-layout">
  <div class="lamp-left">
    <v-clicks>
      <ul>
        <li>горит / не горит</li>
        <li>подключена / не подключена</li>
        <li>целая / разбита</li>
        <li>есть электричество / нет электричества</li>
        <li>проходные выключатели</li>
      </ul>
    </v-clicks>
  </div>
  <div class="lamp-right">
    <img src=" " alt="Лампочка" />
  </div>
</div>


---
transition: slide-left
layout: center
---

## Frontend:

<div class="backdrop-layout">
  <div class="backdrop-left">
    <h2>Backdrop</h2>
  </div>
  <div class="backdrop-right">
    <Backdrop />
  </div>
</div>

---
transition: slide-left
layout: simple-slide
---

## Код обычного программиста

<div class="code-small">

````md magic-move
```jsx
function Modal({ 
  isOpen, 
  isLoading, 
  isClosing, 
  hasError, 
  isAnimating,
  shouldShowBackdrop,
  backdropVisible,
  backdropAnimating 
}) {
  return (
    <>
      {shouldShowBackdrop && backdropVisible && (
        <div 
          className={backdropAnimating ? 'backdrop animating' : 'backdrop'}
          onClick={() => !isLoading && !isClosing && handleClose()}
        />
      )}
      
      {(isOpen || isClosing || isAnimating) && (
        <div className={`modal ${isClosing ? 'closing' : ''} ${isAnimating ? 'animating' : ''}`}>
          {isLoading && <Spinner />}
          {hasError && <Error />}
          {!isLoading && !hasError && <Content />}
        </div>
      )}
    </>
  );
}
```

```jsx {13}
function Modal({ 
  isOpen, 
  isLoading, 
  isClosing, 
  hasError, 
  isAnimating,
  shouldShowBackdrop,
  backdropVisible,
  backdropAnimating 
}) {
  return (
    <>
      {shouldShowBackdrop && backdropVisible && (
        <div 
          className={backdropAnimating ? 'backdrop animating' : 'backdrop'}
          onClick={() => !isLoading && !isClosing && handleClose()}
        />
      )}
      
      {(isOpen || isClosing || isAnimating) && (
        <div className={`modal ${isClosing ? 'closing' : ''} ${isAnimating ? 'animating' : ''}`}>
          {isLoading && <Spinner />}
          {hasError && <Error />}
          {!isLoading && !hasError && <Content />}
        </div>
      )}
    </>
  );
}
```

```jsx {13,19,21,22,23,24}
function Modal({ 
  isOpen, 
  isLoading, 
  isClosing, 
  hasError, 
  isAnimating,
  shouldShowBackdrop,
  backdropVisible,
  backdropAnimating 
}) {
  return (
    <>
      {shouldShowBackdrop && backdropVisible && (
        <div 
          className={backdropAnimating ? 'backdrop animating' : 'backdrop'}
          onClick={() => !isLoading && !isClosing && handleClose()}
        />
      )}
      
      {(isOpen || isClosing || isAnimating) && (
        <div className={`modal ${isClosing ? 'closing' : ''} ${isAnimating ? 'animating' : ''}`}>
          {isLoading && <Spinner />}
          {hasError && <Error />}
          {!isLoading && !hasError && <Content />}
        </div>
      )}
    </>
  );
}
```
````

</div>


---
transition: slide-left
layout: center
---

## Почему работа с состояниями вызывает дискомфорт?

---
transition: slide-left
layout: simple-slide
---

## 1. Boolean Explosion 

<div class="explosion-layout">
  <div class="explosion-left">
    <v-clicks>
      <ul>
        <li>1 флаг → 2 состояния</li>
        <li>2 флага → 4 состояния</li>
        <li>3 флага → 8 состояний</li>
        <li>4 флага → 16 состояний</li>
        <li>5 флагов → 32 состояния</li>
        <li>6 флагов → 64 состояния</li>
      </ul>
    </v-clicks>
  </div>
  
  <div class="explosion-right">
    <ExplosionImage :images="[
      '/images/slides/mr_incredrible/1.Cool.jpg',
      '/images/slides/mr_incredrible/2.Norm.jpg',
      '/images/slides/mr_incredrible/3.Norm.jpg',
      '/images/slides/mr_incredrible/4.Bad.jpg',
      '/images/slides/mr_incredrible/5.Worse.jpg',
      '/images/slides/mr_incredrible/6.Worst.jpg'
    ]" />
  </div>
</div>


---
transition: slide-left
layout: simple-slide
---

## 2. Плоское мышление

<div class="flat-thinking-layout">
  <div class="flat-thinking-left">
    <v-clicks>
      <ul>
        <li>Состояния неравны и не независимы</li>
        <li>Лампочка не может быть одновременно «разбитая» и «горит»</li>
        <li>Но при комбинации булевых флагов такое состояние возможно</li>
        <li>Флаги позволяют создать невалидные комбинации</li>
      </ul>
    </v-clicks>
  </div>
  <div class="flat-thinking-right">
    <img src="/images/slides/SHAROEB.jpg" alt="Визуализация" />
  </div>
</div>


---
transition: slide-left
layout: simple-slide
---

## Почему нужно думать не переходами, а состояниями:

<v-clicks>

**Важный момент:**

- Состояние → первично
- Переходы → вторичны

**Если мы чётко определяем:**

- набор возможных состояний
- где они находятся в иерархии
- какие переходы разрешены, какие запрещены

**То мы автоматически избегаем Boolean Explosion, нелегальные состояния и скрытые баги**

</v-clicks>

---
transition: slide-left
layout: simple-slide
---

## Историческая справка

<div class="traffic-light-fsm">
  <svg viewBox="0 0 600 400" xmlns="http://www.w3.org/2000/svg">
    <!-- Состояние: Красный -->
    <circle cx="150" cy="200" r="50" fill="#dc2626" stroke="#991b1b" stroke-width="3"/>
    <!-- Состояние: Жёлтый -->
    <circle cx="300" cy="200" r="50" fill="#fbbf24" stroke="#d97706" stroke-width="3"/>
    <!-- Состояние: Зелёный -->
    <circle cx="450" cy="200" r="50" fill="#16a34a" stroke="#15803d" stroke-width="3"/>
    <!-- Переход: Красный → Жёлтый -->
    <path d="M 200 200 L 250 200" stroke="#4b5563" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>    
    <!-- Переход: Жёлтый → Зелёный -->
    <path d="M 350 200 L 400 200" stroke="#4b5563" stroke-width="3" fill="none" marker-end="url(#arrowhead)"/>
    <!-- Переход: Зелёный → Жёлтый (обратный) -->
    <path d="M 400 200 L 350 200" stroke="#4b5563" stroke-width="3" fill="none" stroke-dasharray="5,5" marker-end="url(#arrowhead-reverse)"/>
    <!-- Переход: Жёлтый → Красный (обратный) -->
    <path d="M 250 200 L 200 200" stroke="#4b5563" stroke-width="3" fill="none" stroke-dasharray="5,5" marker-end="url(#arrowhead-reverse)"/>
    <!-- Определение стрелок -->
    <defs>
      <marker id="arrowhead" markerWidth="10" markerHeight="10" refX="9" refY="3" orient="auto">
        <polygon points="0 0, 10 3, 0 6" fill="#4b5563"/>
      </marker>
      <marker id="arrowhead-reverse" markerWidth="10" markerHeight="10" refX="1" refY="3" orient="auto">
        <polygon points="10 0, 0 3, 10 6" fill="#4b5563"/>
      </marker>
    </defs>
  </svg>
</div>



---
transition: slide-left
layout: simple-slide
---

## Типы state машин

<div class="automata-layout">
  <div class="automata-left">
    <v-clicks>
      <ul>
        <li><strong>Автомат Мура</strong> — новое состояние зависит только от предыдущего состояния</li>
        <li><strong>Автомат Милли</strong> — от предыдущего состояния и входных данных</li>
        <li>Во фронтенде входные данные - события, логичнее всего использовать автоматы Милли </li>
      </ul>
    </v-clicks>
  </div>
  
  <div class="automata-right">
    <AutomataDiagram />
  </div>
</div>

---
transition: slide-left
layout: simple-slide
---

## Redux

<v-clicks>

**Связь с Redux: reducers должны быть стейт-машинами**

В документации Redux прямо говорится:

- reducer — это описание того, как состояние меняется

Но на практике большинство редьюсеров — это просто:

- набор реакций на action,
- без описания валидных состояний,
- без ограничений переходов,
- без структуры.

То есть это не state машины, а "набор переходов".

Из-за этого часто возникают неявные баги.

</v-clicks>

---
transition: slide-left
layout: center
---

## Нужно думать состояниями

---
transition: slide-left
layout: center
---

## Инструменты

<v-clicks>

- Самостоятельный учёт без библиотек
- XState
- Robot
- Statecharts

</v-clicks>