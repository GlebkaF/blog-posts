### Переосмысливая JS: Отказываемся от switch.
Перевод [Rethinking JavaScript: Eliminate the switch statement for better code](https://hackernoon.com/rethinking-javascript-eliminate-the-switch-statement-for-better-code-5c81c044716d)

![enter image description here](https://cdn-images-1.medium.com/max/800/1*1APKslCDoGX0ho-klL5PbQ.png)

В моих предыдущих статьях я пытался убедить вас отказаться от if, for и break. Теперь я попробую объяснить почему хорошо бы нам отказаться и от оператора switch. 

Несмотря на то, что switch достаточно полезный, он плохо вписывается в наш остальной функциональный код. Switch - не иммутабельный, не совместим с композицией, и 

К сожалению, switch совсем не сочетается с остальным нашим функциональным кодом.  Switch не иммутабельный, мы не можем совмещать его с другими функциям, а еще он приводит к сайд эффектам. 

Switch также использует break, что несовместимо с функциональным подходом в целом (читайте об этом в статье [Rethinking JavaScript: Replace break by going functional](https://hackernoon.com/rethinking-javascript-break-is-the-goto-of-loops-51b27b1c85f8)).

Мне хотелось бы использовать что-то иммутабельное и не создающее сайд эффекты. Что-то, где при одинаковых входных параметрах я всегда получу одинаковые результаты, что-то функциональное!
(Что-то, куда я смогу передавать параметры и получать одинаковые результат на выходе - что-то функциональное!) 

Давайте посмотрим на пример из документации к Redux.
```
function counter(state = 0, action) {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1
    case 'DECREMENT':
      return state - 1
    default:
      return state
  }
```
Я немного поигрался с кодом, и, в итоге, получился набор вложенных тернарных операторов:
```
const counter = (state = 0, action) =>
  action.type === 'INCREMENT' ? state + 1 :
  action.type === 'DECREMENT' ? state - 1
                              : state
```
(Если вас смущает синтаксис, посмотрите статью [Rethinking JavaScript: The if statement](https://medium.com/@joelthoms/rethinking-javascript-the-if-statement-b158a61cd6cb))






