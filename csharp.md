# Методы строк

* `String.Concat(s1,s2);` - возвращает 2 объединенных строки
* `String.Join(separator,string[]);` - возвращает строку в которой все элементы массива будут разделены `separator`
* `s.IndexOf("some");` - Возвращает первое вхождение строки `some` в строку `s`, если не нашёл то возвращает `-1`
* `s.LastIndexOf("some");` - Возвращает последнее вхождение строки `some` в строку `s`, если не нашёл то возвращает `-1`
* `s.StartsWith("some");` - Возвращает `true/false` если строка `s` начинается с `some`
* `s.EndsWith("some");` - Возвращает `true/false` если строка `s` заканчивается строкой `some`
* `s.Split(",");` - Возвращает массив в которой каждый символ строки будет разделен `,`
* `s.Trim();` - Возвращает строку в которой обрезаны лишние пробелы в начале и в конце
* `s.Insert(8,"str");` - Возвращает строку у которой начиная с `8-го` символа вставлена строка `str`
* `s.Remove(index);` - Возвращает строку в которой из строки `s` удален символ под индексом `index`, вторым параметром можно указать количество символов которые нужно удалить
* `s.Replace("some","someNew");` - Возвращает строку в которой все `some` заменены на `someNew`
* `s.ToLower();` - Возвращает новую строку `s` переведнную в нижний регистр
* `s.ToUpper();` - Возвращает новую строку `s` переведнную в верхний регистр

#### Другие полезные методы

* `number.ToString("+# (###) ###-##-##")` - Возвратит строку в указанном формате (`number` = `89133945423`)

# LINQ Методы расширения

* `Select`: определяет проекцию выбранных значений

* `Where`: определяет фильтр выборки

* `OrderBy`: упорядочивает элементы по возрастанию

* `OrderByDescending`: упорядочивает элементы по убыванию

* `Reverse`: располагает элементы в обратном порядке (!!! меняет исходный массив), можно указать с какого с сколько элементов перевернуть `arr.Reverse(2,3);`

* `All`: определяет, все ли элементы коллекции удовлятворяют определенному условию `arr.All(x=>int.Parse(x)>=1)`

* `Any`: определяет, удовлетворяет хотя бы один элемент коллекции определенному условию

* `Contains`: определяет, содержит ли коллекция определенный элемент

* `Distinct`: удаляет дублирующиеся элементы из коллекции

* `Count`: подсчитывает количество элементов коллекции, которые удовлетворяют определенному условию `arr.Count(x=>int.Parse(x) == 1);` или кол-во всех элементов `arr.Count();`

* `Sum`: подсчитывает сумму числовых значений в коллекции, если тип массива `int` то просто `arr.Sum()`, если тип массива `string` то `arr.Sum(x=>int.Parse(x))`

* `Average`: подсчитывает cреднее значение числовых значений в коллекции

* `Min`: находит минимальное значение

* `Max`: находит максимальное значение

* `Except`: возвращает разность двух коллекцию, то есть те элементы, которые содержатся только в одной коллекции

* `Union`: объединяет две однородные коллекции, повторяющиеся значения не дублируются

* `Join`: соединяет две коллекции по определенному признаку

* `GroupBy`: группирует элементы по ключу
``` csharp

List<Phone> phones = new List<Phone>
{
    new Phone {Name="Lumia 430", Company="Microsoft" },
    new Phone {Name="Mi 5", Company="Xiaomi" },
    new Phone {Name="LG G 3", Company="LG" },
    new Phone {Name="iPhone 5", Company="Apple" },
    new Phone {Name="Lumia 930", Company="Microsoft" },
    new Phone {Name="iPhone 6", Company="Apple" },
    new Phone {Name="Lumia 630", Company="Microsoft" },
    new Phone {Name="LG G 4", Company="LG" }
};
 
var phoneGroups = phones.GroupBy(p => p.Company);
 
foreach (IGrouping<string, Phone> g in phoneGroups)
{
    Console.WriteLine(g.Key);
    foreach (var t in g)
        Console.WriteLine(t.Name);
    Console.WriteLine();
}

/* Получится:
Microsoft
Lumia 430
Lumia 930
Lumia 630

Xiaomi
Mi 5

LG
LG G 3
LG G4

Apple
iPhone 5
iPhone 6
*/

// Еще пример
/*
Microsoft : 3
Lumia 430
Lumia 930
Lumia 630

Xiaomi : 1
Mi 5

LG : 2
LG G 3
LG G4

Apple : 2
iPhone 5
iPhone 6
*/
var phoneGroups = phones.GroupBy(p => p.Company)
                        .Select(g => new
                        { 
                            Name = g.Key, 
                            Count = g.Count(), 
                            Phones = g.Select(p =>p) 
                        });
```

* `GroupJoin`: выполняет одновременно соединение коллекций и группировку элементов по ключу

* `Intersect`: возвращает пересечение двух коллекций, то есть те элементы, которые встречаются в обоих коллекциях

* `Take`: выбирает определенное количество элементов

* `Skip`: пропускает определенное количество элементов

* `TakeWhile`: возвращает цепочку элементов последовательности, до тех пор, пока условие истинно

* `SkipWhile`: пропускает элементы в последовательности, пока они удовлетворяют заданному условию, и затем возвращает оставшиеся элементы

* `Concat`: объединяет две коллекции

* `First`: выбирает первый элемент коллекции

* `FirstOrDefault`: выбирает первый элемент коллекции или возвращает значение по умолчанию

* `Single`: выбирает единственный элемент коллекции, если коллекция содердит больше или меньше одного элемента, то генерируется исключение

* `SingleOrDefault`: выбирает первый элемент коллекции или возвращает значение по умолчанию

* `ElementAt`: выбирает элемент последовательности по определенному индексу

* `ElementAtOrDefault`: выбирает элемент коллекции по определенному индексу или возвращает значение по умолчанию, если индекс вне допустимого диапазона

* `Last`: выбирает последний элемент коллекции

* `LastOrDefault`: выбирает последний элемент коллекции или возвращает значение по умолчанию