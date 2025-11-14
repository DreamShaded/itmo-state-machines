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
    <img src="/images/slides/лампа.png" alt="Лампочка" />
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

```jsx {13,19}
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

```jsx {13,19,21}
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

```jsx {13,19,21,22}
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

```jsx {13,19,21,22,23}
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