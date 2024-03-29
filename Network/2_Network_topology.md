# Топологии сетей
Топология сети - это схема объединения устройств в сети - конфигурация графа, где:
+ Вершины - это узлы сети(компьютеры и сет. оборуд.)
+ Ребра - это связи между узлами(вершинами) (физические или информационные)

## Базовые топологии
+ ***Полносвязая*** - в этом случае каждое устройство в сети имеет прямое соединение со всеми другими устройствами
+ ***Ячеистая*** - полносвязая топология в которой удалены некоторые связи(ребра).
+ ***Звезда*** - в этом случае компьютеры подключаются не напрямую друг к другу, к центральному устройству(сетевое оборудование - коммутатор, маршрутизатор, wi-fi)
+ ***Кольцо*** - в этом случае каждый компьютер соединяется с двумя соседними компьютерами. Данные передаются по кольцу
+ ***Дерево*** - в этом случае компьютеры и сетевое оборудование образуют дерево. Для того чтобы передать данные от одного устройства к другому, необходимо пройти через несколько промежуточных устройств.
+ ***Общая шина*** - в этом случе компьютеры в сети подключены к некоторой среде передачи данных, в базовом случае это кабель который идет вдоль всех компьютеров. Данные передающиеся в этой среде доступны всем компьютерам

## Смешанная топология
На практике _отдельные базовые топологии не используются_, а используется ***смешанная топология***. Она включает в себя все  вышеперечисленные топологии.

## Физическая и логическая топология
+ ***Физическая*** - соединения устройств в сети
+ ***Логическая*** - правила распространения сигналов в сети
