# Group project. LL(k) syntax analyser for k >=1 .

Для заданої граматики в файлі Grammar.txt можна знайти:
- first_k
- follow_k
- epsilon non terminals
- left recursive non-terminals
- table of control for k = 1 and k > 1
- syntax analyzer of given word for k = 1 and k > 1

Результати виводяться в заданий файл, базове значення - Output.txt

## Example of work

Результати знаходяться в віподвідній папці Tests. В папці TestsResult наведені результати виконання.

Про тести:

- Test 1-1: 

Приклад з книжки для k = 1. Вхідне слово - ( a + a ) * a

Result: 
```
Successfully parsed: Pi chain is - 1 4 7 1 4 8 6 2 4 8 6 3 5 8 6 3 
```

- Test 1-2:

Приклад з книжки для k = 1. Вхідне слово - ( a + a ) * a (

Result: 
``` 
Error! Any rules that could lead us to ( from C 
C in current step except only ) * + eps
Pi chain before error - 1 4 7 1 4 8 6 2 4 8 6 3 5 8 
```

Пояснення: в таблиці контролю немає правила для C яке можна застосувати для `(`. Очікувані символи на цьому кроці тільки - `) * + eps`

- Test 1-3

Приклад з книжки для k = 1. Вхідне слово - ( a + a ) * a ) ) )

Result:
``` 
!!!Error!!! Stack is empty, but chain is not empty yet! Pi chain before last error is - 1 4 7 1 4 8 6 2 4 8 6 3 5 8 6 3 
```

Пояснення: стек закінчився, але слово ні, тому це - синтаксична помилка, бо граматика не очікує продовження у цій комбінації.

- Test 2-1

Приклад з книжки для k = 2. Вхідне слово - a b a b b a a

Result:
``` 
Successfully parsed: Pi chain is - 1 3 1 4 
```

- Test 2-2

Приклад з книжки для k = 2. Вхідне слово - a b a b b a a a

Result:
``` 
!!!Error!!! Stack is empty, but chain is not empty yet! Pi chain before last error is - 1 3 1 4 
```

Пояснення: стек закінчився, але слово ні, тому це - синтаксична помилка, бо граматика не очікує продовження у цій комбінації.

- Test 2-3

Приклад з книжки для k = 2. Вхідне слово - a b a b a a a

Result:
``` 
Lexeme is empty, but stack doesn't!
Pi chain before error - 1 3 1 3 2 
```

Пояснення: стек не закінчився, але слово вже, тому це - синтаксична помилка, бо граматика очікує продовження для цього виводу.

- Test 2-4

Приклад з книжки для k = 2. Вхідне слово - a b a b b b a

Result:
``` 
Error! Any rules that could lead us to bb
Pi chain before error - 1 3 1 
```

Пояснення: немає переходу від bb через правило T_3. 

- Test 3-1

Приклад для k = 3. Вхідне слово - e f f f a

Result:
``` 
Successfully parsed: Pi chain is - 2 8 8 8 9 
```

- Test 3-2

Приклад для k = 3. Вхідне слово - e f f f a a

Result:
``` 
Error! Any rules that could lead us to faa
Pi chain before error - 2 8 8 
```
Пояснення: Так як для faa не очікується ніякий перехід з T_3 це означає синтаксичну помилку.

- Test 4

Приклад для визначення left-recursive non terminals.

Result:
``` 
left-recursive non-terminals: {A, B, C, D, S}
```