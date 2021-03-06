
> Я предпочитаю обеспечить много путей, если это возможно,  
но поощрять или вести пользователей, чтобы выбрать лучший путь, если это возможно.  
**Юкихиро Мацумото**

# Занятие: 2

## `Ruby`: Ещё раз о стиле оформления
- https://github.com/arbox/ruby-style-guide/blob/master/README-ruRU.md -
по-русски
- https://github.com/styleguide/ruby
- https://github.com/airbnb/ruby

gem `Rubocop` (https://github.com/bbatsov/rubocop) - всем поставить и сдавать домашки только при 100% pass.

<br>

### Массивы

Коллекцией называется любой набор элементов. Коллекция представляет
собой объект определенного типа (экземпляр определенного класса),
который состоит из других объектов. Если коллекция содержит в себе
другие коллекции, то такая коллекция называется ветвящейся коллекцией
или деревом, или root-коллекцией (корневой коллекцией), так как из
нее происходит ветвление. Двумя основными коллекциями в `Ruby`
являются массивы и хэши.

Данные представленные в массиве имеют парную структуру
"ключ - значение", в которой ключ служит для идентификации элемента
в массиве и может быть только целым числом. Стоит заметить, что
ключей (индексов) у каждого элемента массива имеется целых два:
левосторонний и правосторонний, как и у строк.

Так как `Ruby` язык высокого уровня, в котором в отличие от,
например, `С` не нужно заранее определять размерность массива и тип
хранимых в нем данных.

**Особенности:**  
- доступ по уникальному числовому ключу
- индексация с `0`
- не ограничены (лишь оперативной памятью)
- упорядочены
- может хранить данные разных типов
- поэлементное сравнение
- `include Enumerable`

**Инициализация:**

```ruby
[ ] # лучше всего (пробел не нужен)
Array.new(size = 0, default = nil) # объектный подход
%w{} # массив строкразберём отдельно
Array[]
Array.[](args*)
```

**Примеры:**

`[]` - пустой массив  
`[1, 2, 3]`  
`["hello", "my", "cruel", "world"]`  
`[1, "cat", 2, "dog"]` - смешанные типы  
`[1, [1, 2], "dog", ["duck"], nil]` - и даже так  

```ruby
array = [1, [1, 2], "dog", ["duck"], nil, true]
array[0] # => 1
array[-1] # => true

array[100] # доступ к несуществующему элементу
=> nil

array[10] = "test" # => "test"

array.inspect
=> [1, [1, 2], "dog", ["duck"], nil, true, nil, nil, nil, nil, "test"]
array[0] = false # => false
array.inspect
=> [false, [1, 2], "dog", ["duck"], nil, true, nil, nil, nil, nil, "test"]
array[2] = [3, 4]
array.inspect
=> [false, [1, 2], [3, 4], ["duck"], nil, true, nil, nil, nil, nil, "test"]

array[1, 3] # => [[1, 2], [3, 4], ["duck"]]
array[2..3] # => [[3, 4], ["duck"]]
array[2...3] # => [[3, 4]]
```

**Полезные методы:**

`<< (.push)` - добавление в конец (`object_id` не меняется)  
`#pop` - удалить из конца и вывести  
`#shift` - удалить сначала и вывести  
`#unshift` - добавление в начало  
`+` - приклеить в конец (по-элементно, сам не меняется)  
`*` - повторить несколько раз  
`A - B`, в результате этой операции возвращается массив уникальных
элементов `A`  
`#concat (+=)` - добавить в конец и изменить (меняется `object_id`)  
`#compact` - удаляет все `nil`  
`#flatten(level)` - понизить уровень (рекурсивно)  
`#uniq` - только уникальные  
`#each {|e| puts e}` - итерация по каждому элементу, вывод

`#join()` - соеденить все элементы массивы в строку  
`#sample(3, random: rng)` - произвольная выборка (без повторов если
в самом массиве их нет)  
`#sort` (если элементы сравнимы)  и `#sort_by`  
`#reverse` - обратный порядок  
`#size` - количество элементов  
`#count` - количество элементов (может принимать блок)  
`#first` - первый элемент  
`#last` - последний элемент  
`#values_at(1, 2, 3)` - значения по индексам (может принимать
несколько индексов)  
`#index(1)` - индекс первого найденного  
`#delete(1)` - удаление по значению  
`#delete_at(1)` - удаление по индексу  
`#insert(index, value)` - вставка значения на место индекса со сдвигом  
`#shuffle` - перетусовать порядок элементов  
`#include?(value)` - проверка на включение  

> Рассмотрим чуть позже:  
`#map/collect`  
`#select / reject`  
`#inject`  
`#with_index`

<br>
Сравнение массивов происхожит по-элементно (порядок важен).

Операции как над множествами: `&`, `|`, `<=>`

`%w` vs `%W`
```ruby
a = Array.new(10) {| elem| elem.odd? ? elem ** 2 : elem ** 3 }
=> [0, 1, 8, 9, 64, 25, 216, 49, 512, 81]
```

**Задание:**
- Дан 10-ти элементный массив. В одну строку удалить 5 последних
элементов.
- Посчитать сумму 5-значного массива

Массивы часто используются для обработки строк и даже хэшей:  
`#join` / `#split` / `#sort`

```ruby
a = 1 # => 1
b = 2 # => 2
c = [a, b] # => [1, 2]
c # => [1, 2]
a += 1 # => 2
a # => 2
c # => [1, 2]
```

```ruby
a = '1' # => "1"
c = [a, b] # => ["1", 2]
a << '1' # => "11"
c # => ["11", 2]
```

<br>

### Хэши

- они же ассоциативные массивы (почему), они же словари
- не упорядочены
- саморасширяемы, по-умолчанию - `nil`
- может хранить данные разных типов
- похожи на массивы

Ключами могут быть сложные объекты, но лучше всего использовать
символы. Почему?

**Инициализация:** 
`{}`  
`{a: 1}`  
`{:a => 1}`  
`Hash.new`  
`Hash[]`  

Синтаксис создания хэша с `Hash.new` позволяет принимать блок кода,
который выполняется при обращении к несуществующщему ключу,
создает егiо и соответствующее ему значение по правилам определенным
в блоке кода:

```ruby
hash = Hash.new { |h,k| h[k] = k } # => {}
hash[:a] # => :a
hash # => { :a => :a }
```

Другими словами, в такой способ можно создать значение по умолчанию.  
Синтаксис `Hash[]` позволяет создавать хэш из предоставляемого
массива. Такой синтаксис создания хэша, как бы просит у переданного
массива расчитаться на 1й — 2й, где 1й — ключ, 2й — значение:

```ruby
hash = Hash[1, 2, 3, 4, 5, 6] # => { 1=>2, 3=>4, 5=>6 }
hash = Hash[:a, 1, :b, 2, :array, [1, 2, 3, 4]]
=> { :a=>1, :b=>2, :array=>[1, 2, 3, 4] }
```

**Полезные методы:**

`#each { |key, value| ... }` - итерация по парам ключ-значение  
`#keys` / `#values` - массив ключей / массив значений  
`#to_a` - конвертация в массив  
`#merge(hash2)` - объединие с другим хэшем  
`#default` - данный метод позволяет установить хэшу значение
по-умолчанию. В массивах значение по умолчанию всегда `nil`, а в
хэшах его можно очень просто установить:

```ruby
h= Hash.new # => {}
h[:a] # => nil
h.default = 'ruby'
h[:a] # => "ruby"
h[:b] # => "ruby"
```

`#invert` — данный метод позволяет преобразовать структуру хэша так,
что ключи и значения меняются местами:

```ruby
h = { a: 100, b: 200, c: 300 }
h.invert # => { 100=>:a, 200=>:b, 300=>:c }
```

Хотя массивы и позволяют хранить элементы различных типов, это не
является самым хорошим стилем. Вам следует использовать массивы для
хранения более-менее одинаковых элементов или вложенных структур,
которые в свою очередь так же могут быть массивами или хэшами.

**Массив -> Хэш -> Массив**  
Для преобразования массива в хэш достаточно воспользоваться
специальным синтаксисом создания хэша: `Hash[]`, который разбивает
массив на пары ключ — значение, примеры:

```ruby
array = [1, 2, 3, 4]
hash = Hash[*array]
=> { 1=>2, 3=>4 }
```

Обратите внимание на символ `*` — это оператор носит название
`"splat"` или `"asterisk"` и используется для преобразования массива
в набор аргументов, пример:

```ruby
array # => [1, 2, 3, 4]
[array] # => [[1, 2, 3, 4]]
[*array] # => [1, 2, 3, 4]
```

Для преобразования хэша в массив имеется специальный метод `to_a`:

```ruby
hash # => { 1=>2, 3=>4 }
hash.to_a # => [[1, 2], [3, 4]]
```

Ещё массив пар массивов можно привести к хэшу с помощью метода `.to_h`:

```ruby
ar = [[:a, 1], [b: 2]]
ar.to_h # => { :a=>1, :b=>2 }
```

**Немного о строковых ключах:**
  
```ruby
h.keys.last
=> "f"
h.keys.last << '1'
=> RuntimeError: can't modify frozen String
```

```ruby
hash = {:a => 1}
=> {:a=>1}
 b = :a
=> :a
b.object_id
=> 361768
hash.keys.first.object_id
=> 361768
```

```ruby
Symbol.all_symbols.size
=> 5210
a = :tort
=> :tort
Symbol.all_symbols.size
=> 5211
h = {:tort => 1}
=> {:tort=>1}
Symbol.all_symbols.size
=> 5211
```

<br>

### Диапазоны

- они же интервалы: набор значений с началом и концом
- class == `Range`
- достаточно уникальный тип данных, не в каждом языке есть

**Инициализация:**  
`(1..10)`  
`(1...10)`  
`('a'..'z')` - и даже так

**Полезные методы:**  
`#min` / `#max`  
`#include?` / `#member?`  
`#to_a`

Между `#min` и `#first`, а также `#max` и `#last` существует
маленькое, но очень важное различие, незнание которого может привести
к ошибкам в коде! Это различие проявляется тогда, когда используются
обратные диапазоны, пример:

```ruby
(1..100).first
=> 1
(1..100).min
=> 1
(100..1).min
=> nil
(100..1).first
=> 100
(1..100).max
=> 100
(1..100).last
=> 100
(100..1).max
=> nil
(100..1).last
=> 1
```

Как видите, `#min` и `#max` при обратных диапазонах возвращают
значение `nil`, этим можно пользоваться, когда вам необходимо узнать,
диапазон прямой или обратный, во всех остальных случаях я бы
рекомендовал использовать методы `#last` и `#first`, если разумеется
нет ограничения на то, каким должен быть диапазон (обязательно ли он
должен быть прямым?).

**Итерация по диапазону:**  
`#each` — сей метод позволяет вам проходить по каждому элементу
входящему в диапазон и выполнять с ним определенные действия:

```ruby
(1..10).each { |e|  print(e, ', ') }
1, 2, 3, 4, 5, 6, 7, 8, 9, 10,
=> 1..10
```

`#step` — данный метод нам уже знаком, так как мы уже сталкивались с
ним, когда разбирались с целыми числами. Его отличие от
целочисленного `#step` состоит в том, что обе границы заданы и нам
необходимо задать лишь шаг итерации:

```ruby
('a'..'z').step(2) { |ch| print ch, ", " }
a, c, e, g, i, k, m, o, q, s, u, w, y,
=> "a".."z"
```

Диапазоны очень полезны, например, они могут здорово помочь тогда,
когда нам необходимо создать массив последовательных элементов:

```ruby
(1..10).to_a
=> [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

Представьте, что элементов не 10, а тысяча и вы поймете, что
диапазоны действительно удобны. Разумеется, такой массив можно было
бы создать при помощи цикла, однако это лишний, ухудшающий
читабельность код и менее экономно с точки зрения памяти.

Диапазоны очень удобны в использовании, с выражением `case`:

```ruby
a = 101
case a
when 1...50
  puts "0 < a < 50"
when 50...100
  puts "50 <= a < 100"
when 100...150
  puts "100 <= a < 150"
else
  puts "a > 150"
end
=> "100 <= a < 150"
```

Если бы не диапазон, вы бы не смогли написать такой простой и
красивый код.


<br>

### Nil

- `nil`
- тоже объект :smile:

**Полезные методы:**  
`#nil?`  
`#to_s`  
`#inspect`


<br>

### Regexp

- тоже объект :smile:
- `//` - инициализация
- возвращает `nil`, если не нашло
- стандартный синтаксис: `?`, `+`, `*`, `[]`, `\d`, `\s` и тд...
- http://rubular.com/ - очень классный online-проверяльщик

```ruby
s = "strintg"
s =~ /t/
=> 1
s.scan(/t/)
=> ["t", "t"]
```

### Управляющие структуры

- позволяют регулировать процесс выполнения программы, задавать
условия и разветвления исполнения кода
- конструкция `if-else-end` выводит результат последнего выражения
- `[ then ]` - для однострочников
- `Ruby`: всё что может выводить – выводит. Тобешь фактически
вызов = выражение
- всё что не `nil` и не `false` – есть истина
- `0`, `''`, `[]`, `{}` - всё истина :open_mouth:

**Прямая форма (если):**

```ruby
if < conditions > [ then ]
  < code >
elsif < conditions >  [ then ]
  < code >
elsif < conditions >  [ then ]
  < code >
else
  < code >
end
```

**Обратная (если НЕ):**

```ruby
unless < conditions >  [ then ]
  < code >
else
  < code >
end
```

Например:

```ruby
number = 10
if number > 10 then puts ">5"
elsif (number > 8 && number < 20)
  puts "bigger than 8"
  puts "lest than 20"
else
  puts "less than 8"
end
```

**Пример использования результа:**

```ruby
result = if 5 > 10
  "first"
elsif 5 > 2
  "second"
else
  "third"
end

puts result # => second
```

**Краткая форма:**

```ruby
< code > if < conditions >
< code > unless < conditions >
< code-условие > ? что делать если `true` :  что делать если `false`
```

Примеры:

```ruby
before = 1
puts before # => 1
before = 5 if true
puts before # => 5
```

```ruby
word = "word"
word = "new word" unless 5 > 10 && 5 > 20
puts word # => new word
```

```ruby
puts 10 > 0 ? "big" : "small" # => big
```

Когда `elsif`-ов становится слишком много, или нужно неявное
сравнение, используется конструкция `case`.

- использует `===` в сравнениях
- выводит последнее исполнение

```ruby
case < переменная или значение (объект на входе)>
when сравнение1 [, сравнение2 и тд через запятую ]* [ then ]
  < code >
when сравнение3 [, сравнение4 ]* [ then ]
  < code >
  ...
[ else < code > ]
end
```

- результат высчитывается сравнение `===` объект на входе,
не наоборот, сверху вниз
- как только истина – выполняет код
- если ничего нет – заходит в `else` (если он есть)
- если совсем ничего нет – то `nil`
- `[ then ]` - для онлайнеров


**Пример:**

```ruby
number = 13

case number
when 10 then puts "number is 10"
when 20, 13
  puts "number is 20 or 13"
else
  puts "uknown"
end
# => number is 20 or 13
```

Важно заметить возможную ошибку:

```ruby
number = 10

case number
when number > 4
  puts "more than 4"
when number > 6, number > 8 then puts "more than 6"
else
  puts "unknown"
end
# => unknown
```

Подумайте почему.

И ещё:

```ruby
1 === Fixnum # => false
Fixnum === 1 # => true
```

Так происходит потому, что метод `===` на объекте самого
класса `Fixnum` переопределен, а на объекте экземпляра
класса `Fixnum` - единице - нет.


### Домашнее задание: 2
#### Теория:
- прочесть заметки лекции ещё раз, два, три...
- изучить следующие ссылки:
  - https://ru.wikibooks.org/wiki/Ruby/%D0%9F%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%B5%D0%B5_%D0%BE_%D0%BC%D0%B0%D1%81%D1%81%D0%B8%D0%B2%D0%B0%D1%85
  - https://ru.wikibooks.org/wiki/Ruby/%D0%9F%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%B5%D0%B5_%D0%BE%D0%B1_%D0%B0%D1%81%D1%81%D0%BE%D1%86%D0%B8%D0%B0%D1%82%D0%B8%D0%B2%D0%BD%D1%8B%D1%85_%D0%BC%D0%B0%D1%81%D1%81%D0%B8%D0%B2%D0%B0%D1%85

- Осмотреться в документации:
  - http://www.ruby-doc.org/core-2.2.0/Array.html
  - http://ruby-doc.org/core-2.1.5/Hash.html
  - http://ruby-doc.org/core-2.2.0/Range.html
  - http://ruby-doc.org/core-2.1.1/Regexp.html
- составить список вопросов
- выделить одну интересную и запомнившуюся особенность/метод/факт связанный с `Ruby`


#### Практика:

- **def task_2_1(n)**: написать метод, который выводит последовательность чисел [Фибонначи](https://en.wikipedia.org/wiki/Fibonacci_number) для переданного числа n:  
  - n - аргумент, указывающий на число элементов в последовательности  
  
Начиная с 1. Выводит 0, если передан 0.

Пример работы:

```ruby
task_1(5) # => 1, 1, 2, 3, 5
```

- **def task_2_2(input)**: дан текст в формате YAML (http://www.yaml.org/).
Распарсить его вручную или используя http://ruby-doc.org/stdlib-2.5.0/libdoc/yaml/rdoc/YAML.html. Формат файл следующий (начиная с # - мои комменты):

```yaml
stage: # название env
  adapter: mysql2 # обязательный
  encoding: utf8  # не обязательный
  reconnect: false # не обязательный
  database: test-mysql2_development # обязательный
  pool: 5 # не обязательный, считаем 1 по-умолчанию
  timeout: 5000 # не обязательный, считаем 1000 по-умолчанию
  username: root # не обязательный
  password: password # не обязательный
  socket: /tmp/mysql.sock # не обязательный

development:
  adapter: sqlite3
  database: db/development.sqlite3
  pool: 5
  timeout: 1000
  
production:
  adapter: postgresql
  encoding: unicode
  database: test-postgres_production
  pool: 5
  username: test-postgres
  password: x123
```

Необходимо вернуть массив всех конфигураций (пустой, если их нет), каждая в виде хэша следующего формата:
```ruby
{
  env_name: {
    db: database value,
    user: username value если есть,
    password: password value если есть,
    magic_number: pool * timeout, используя значения по-умолчанию,если они отсутствуют
  }
}
```

Для примера выше это будет:

```ruby
[
  { stage: { db: "test-mysql2_development", user: "root", password: "password", magic_number: 25000 } },
  { development: { db: "db/development.sqlite3", magic_number: 5000 } },
  { production: { db: "test-postgres_production", user: "test-postgres", password: "x123", magic_number: 5 } },
 ]
 ```

- **def task_2_3(array)**: дан многоуровневый массив. Вернуть отсортированный по убыванию массив из уникальных элементов начального массива. Начальный должен быть НЕ изменен.

```ruby
task_2_3([7, 3, [4, 5, 1], 1, 9, [2, 8, 1]]) # => [9, 8, 7, 5, 4, 3, 2, 1]
```


- **def task_2_4(string)**: Дана строка. Проверить, является ли она палиндромом (https://ru.wikipedia.org/wiki/%D0%9F%D0%B0%D0%BB%D0%B8%D0%BD%D0%B4%D1%80%D0%BE%D0%BC)

```ruby
task_2_4("hello") # => false
task_2_4("Sum summus mus") # => true
```

Домашку сабмитить в виде PR в репу https://github.com/aliaksandrb/mtn18, под названием `NAME_SURNAME L2`.
Это должен быть 1 комит (git squash) в котом в папку `/homeworks` кладется руби файл названный `name_surname_l2.rb` и в котором реализованы методы из описания выше.


Спасибо!

#### На этом всё, жду вас на следующем занятии!
