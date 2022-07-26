### Продукт X Релиз 0.1

Порядок выпуска релизов

```mermaid
graph TD
   st[Старт]
   st-->archi[Архитектура приложения]
   archi-->unit[Юнит-тесты с заглушками]
   unit-->s1[Реализация ввода-вывода `Вася`]
   unit-->os1[Сборка под Windows `Коля`]
   os1-->os2[Сборка под Linux `Коля`]
   s1-->r1[Ревью кода, тесты]
   r1-->dep[Деплой windows, linux]
   dep-->release[[Версия 0.1 Релиз]]
   os2-->dep

   doc[Документация по задачам]

   subgraph legend
   backlog[Беклог]
   inwork[В работе]
   oncheck[На проверке]
   ready[Готов]
   unready[Не готов]

   backlog-->inwork
   inwork-->oncheck
   oncheck-->ready
   ready-->unready
   end

   %%Определения стилей для классов, заливка фоном
   classDef classReady fill:#0f9f;
   classDef classInWork fill:#ff0000;
   classDef classBacklog fill:#7777;
   classDef classOnCheck fill:#882299;
   %%Назначение классов для вершин
   class ready,st,archi,unit classReady;
   class inwork,s1 classInWork;
   class backlog,doc classBacklog;
   class oncheck,os1 classOnCheck;
```

| Задача                  | Описание                                                                  | Ответственный | Результат                                |
| ----------------------- | ------------------------------------------------------------------------- | ------------- | ---------------------------------------- |
| Архитектура приложения  | Выделение классов для работы приложения, вместо реальных модулей заглушки | Петя          | Код классов + заглушки                   |
| Юнит-тесты              | Юнит-тесты для ядра, линковки модулей.                                    | Петя          | Юнит тесты для заглушек                  |
| Сборка под Windows      | Проверить, все ли библиотеки переносимы                                   | Коля          | Бинарник                                 |
| Реализация ввода-вывода | CLI, web                                                                  | Вася          | Бинарник                                 |
| Ревью кода, тесты       | Не забыть оценить покрытие!                                               | Петя          | Процент покрытия, прохождение линтера    |
| Сборка под Linux        | Как обычно                                                                | Петя          | Бинарник                                 |
| Деплой                  | Как обычно                                                                | Петя          | Инсталлер для винды, деб-пакет для Linux |
| Версия 0.1              | Минимальный функционал                                                    | Петя          | Выложили в хранилище артефактов          |

### По беклогу

- Документацию надо вести сразу в markdown!

### Пример вставки блока

- Запуск приложения deviceQuery по пути `c:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v11.2\extras\demo_suite\deviceQuery.exe`, вывод:
  
  ```
  CUDA Device Query (Runtime API) version (CUDART static linking)
  
  Detected 1 CUDA Capable device(s)
  
  Device 0: "GeForce GTX 1660 Ti"
    CUDA Driver Version / Runtime Version          11.2 / 11.2
    CUDA Capability Major/Minor version number:    7.5
    Total amount of global memory:                 6144 MBytes (6442450944 bytes)
  …
  ```

### Пример отрисовки диаграмм в vega-light

Простое решение собирать данные в JSON-структуру и рендерить в статическую веб-страничку с помощью [vega-light](https://vega.github.io/vega-lite/):

```vega-lite
{
  "description": "A simple bar chart with embedded data.",
  "data": {
    "values": [
      {"a": "A", "b": 28}, {"a": "B", "b": 55}, {"a": "C", "b": 43},
      {"a": "D", "b": 91}, {"a": "E", "b": 81}, {"a": "F", "b": 53},
      {"a": "G", "b": 19}, {"a": "H", "b": 87}, {"a": "I", "b": 52}
    ]
  },
  "mark": "bar",
  "encoding": {
    "x": {"field": "a", "type": "nominal", "axis": {"labelAngle": 0}},
    "y": {"field": "b", "type": "quantitative"}
  }
}
```
