# Тестовое задание 3itech-frontend / interview-tasks

![Описание задания](https://github.com/3itech-frontend/interview-tasks/)

## 1. Верстка

### Дополнил scss правила так, чтобы представленная html разметка приобрела ![нужный](https://raw.githubusercontent.com/3itech-frontend/interview-tasks/main/example.png) вид.

![Результат](https://andrey-trofimov.github.io/3itech-frontend__interview-tasks/)

```SCSS
.dialog-container {
    position: fixed;
    left: 0;
    top: 0;
    width: 100vw;
    height: 100vh;
    background-color: #777;
    display: flex;
    justify-content: center;
    align-items: center;
}

.dialog {
    background-color: #fff;
    max-height: 500px;
    max-width: 350px;

    &__header {
        background-color: #ddd;
        display: flex;
        flex-direction: row;
    }

    &__header-title-container {
        width: 65%;
    }

    &__header-title {
        white-space: nowrap;
        overflow: hidden;
        margin-right: 7px;
        position: relative;

        &::after {
            content: "...";
            position: absolute;
            display: inline-block;
            right: 0px;
            background-color: #ddd;
        }
    }

    &__header-button {
        width: 35%;
    }

    &__content {
        display: flex;
        flex-direction: row;
        height: 320px;
    }

    &__content-block {
        &_left {
            width: 30%;
            border-right: 1px solid #ccc;
        }

        &_right {
            width: 70%;
            overflow-y: scroll;
        }
    }

    &__footer {
        background-color: #ddd;
        text-align: center;
        word-wrap: break-word;
    }
}

.content {
    display: flex;
    justify-content: space-between;
    flex-direction: column;
    height: 500px;
    width: 100%;
}
```

## 2. JS

### Написал функцию `decode` в том же стиле, что и функция `encode` (вытянутой в цепочку). Переменная `input` равна коду, полученному после повторного кодирования выражения "i love puzzles".

```javascript
let decode = (input) =>
  input
    .match(/\d+/g)
    .concat(1)
    .map((x) => +x / 2 - 1)
    .reduce(
      (newX, x, i, arr) =>
        x < 0
          ? newX.concat(
              arr
                .slice(
                  newX.length + newX.reduce((sum, x) => sum + x.length, 0),
                  i
                )
                .join("")
            )
          : newX,
      []
    )
    .map((x) => +x)
    .reduce(
      (newX, _, i, arr) => (i % 2 ? newX : [...newX, arr.slice(i, i + 2)]),
      []
    )
    .sort((a, b) => +a[1] - b[1])
    .map((x) => String.fromCodePoint(x[0]))
    .join("");
```

#### `decode(decode(input))`:

```
i love puzzles
```
