# <a name="documentation-comments"></a>Комментарии к документации

C# предоставляет механизм для программистов для документирования кода с помощью специального синтаксиса комментариев, содержащий XML-текст. В файлах исходного кода комментарии, имеющие определенный вид может использоваться для направления инструментом создания XML из этих комментариев и элементов исходного кода, которым они предшествуют. Комментарии с помощью такого синтаксиса, называются ***комментарии к документации***. Они должны непосредственно предшествовать определяемого пользователем типа (например, класс, делегат или интерфейс) или члена (например, поле, событие, свойство или метод). Инструмент создания XML называется ***генератор документации***. (Этот генератор может быть, но не обязательно, компилятор C# сам). Выходные данные, создаваемые генератор документации вызывается ***файл документации***. Файл документации используется в качестве входных данных для ***просмотра документации***; средство для создания своего рода визуальное отображение элемента сведений о типе и соответствующая документация.

Эта спецификация предлагает набор тегов для использования в комментарии к документации, но использование этих тегов не является обязательным и другие теги может использоваться при необходимости, пока соблюдаются правила корректный XML.

## <a name="introduction"></a>Вступление

Комментарии, имеющие это особая форма может использоваться для направления инструментом создания XML из этих комментариев и элементов исходного кода, которым они предшествуют. Такие комментарии являются однострочные комментарии, начинающиеся с трех знаков косой черты (`///`), или комментарии, которые начинаются с косой черты и двумя звездами с разделителями (`/**`). Они должны непосредственно предшествовать определяемого пользователем типа (например, класс, делегат или интерфейс) или члена (например, поле, событие, свойство или метод), к которому они относятся. Атрибут разделы ([спецификация атрибута](attributes.md#attribute-specification)) являются частью объявления, поэтому комментарии к документации должны предшествовать атрибутов, примененных к типу или члену.

__Синтаксис:__

```antlr
single_line_doc_comment
    : '///' input_character*
    ;

delimited_doc_comment
    : '/**' delimited_comment_section* asterisk+ '/'
    ;
```

В *single_line_doc_comment*, если есть *пробелы* следующий `///` символов на каждом из *single_line_doc_comment*смежные s текущему *single_line_doc_comment*, затем, *пробелы* символ не включается в выходные данные XML.

С разделителями doc-комментария Если первый отличный от пробела символ на второй строке является звездочка и та же последовательность необязательные пробелы и знак звездочки повторяется в начале каждой строки в с разделителями комментариев в документации, затем символы повторяющихся шаблона не включаются в выходные данные XML. Шаблон может включать пробелы после, а также перед символом звездочки.

__Пример:__

```csharp
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
///
public class Point 
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```

Текст внутри комментариев документации должны быть сформированы в соответствии с правилами XML (http://www.w3.org/TR/REC-xml). Если XML имеет неправильную форму, сформированном, выдается предупреждение и файл документации содержит комментарий о том, что произошла ошибка.

Несмотря на то, что разработчики могут создавать свои собственные наборы тегов, рекомендуемый набор определяется в [Рекомендуемые теги](documentation-comments.md#recommended-tags). Некоторые рекомендуемые теги имеют особые значения.

*  `<param>` Тег используется для описания параметров. Если используется такой тег, генератор документации необходимо убедиться, что указанный параметр существует и что все параметры описаны в комментариях к документации. Если проверка завершается ошибкой, генератор документации выдает предупреждение.
*  Атрибут `cref` может быть присоединен к любому тегу для предоставления ссылки на элемент кода. Генератор документации необходимо проверить наличие этого элемента кода. Если проверка будет выполнена успешно, генератор документации выдает предупреждение. При поиске имени, описанная в `cref` атрибут, генератор документации должны уважать видимость пространства имен в соответствии с `using` инструкция, находящаяся сразу в исходном коде. Для элементов кода, которые являются обобщенными, обычного синтаксиса универсальных шаблонов (т. е "`List<T>`«) не может использоваться, поскольку он создает недопустимый XML-код. Можно использовать вместо квадратных скобок (ie "`List{T}`«), или можно использовать escape-синтаксис XML (т. е"`List&lt;T&gt;`«).
*  `<summary>` Тег предназначен для использования средством просмотра документации для отображения дополнительных сведений о типе или член.
*  `<include>` Тег содержит сведения из внешнего файла XML.

Нужно понимать, что файл документации не предоставляет полную информацию о типе и членах (например, он не содержит никаких сведений о типе). Для получения таких сведений о типе или член, необходимо использовать файл документации вместе с отражением на текущий тип или член.

## <a name="recommended-tags"></a>Рекомендуемые теги

Генератор документации должен принимать и обрабатывать любые тег, который является допустимым в соответствии с правилами XML. Следующие теги предоставляют часто используемые возможности в документации для пользователей. (Конечно, другие теги возможны.)


| __Тег__          | __Раздел__                                            | __Назначение__                                            |
|------------------|--------------------------------------------------------|--------------------------------------------------------|
| `<c>`            | [`<c>`](documentation-comments.md#c)                   | Задание текста шрифтом кода                           | 
| `<code>`         | [`<code>`](documentation-comments.md#code)             | Задайте один или несколько строк исходного кода или выходных данных программы |
| `<example>`      | [`<example>`](documentation-comments.md#example)       | Указать пример                                    |
| `<exception>`    | [`<exception>`](documentation-comments.md#exception)   | Определяет исключения, которые может выдавать метод           |
| `<include>`      | [`<include>`](documentation-comments.md#include)       | Включает в себя XML из внешнего файла                     |
| `<list>`         | [`<list>`](documentation-comments.md#list)             | Создание списка или таблицы                                 |
| `<para>`         | [`<para>`](documentation-comments.md#para)             | Разрешить добавление к тексту структуры                   |
| `<param>`        | [`<param>`](documentation-comments.md#param)           | Описания параметра для метода или конструктора       |
| `<paramref>`     | [`<paramref>`](documentation-comments.md#paramref)     | Указать, что слово является именем параметра               |
| `<permission>`   | [`<permission>`](documentation-comments.md#permission) | Документ безопасности доступа к члену        |
| `<remark>`       | [`<remark>`](documentation-comments.md#remark)         | Описаны дополнительные сведения о типе           |
| `<returns>`      | [`<returns>`](documentation-comments.md#returns)       | Описания возвращаемого значения метода                  |
| `<see>`          | [`<see>`](documentation-comments.md#see)               | Укажите ссылку                                         |
| `<seealso>`      | [`<seealso>`](documentation-comments.md#seealso)       | Создать запись см. также                              |
| `<summary>`      | [`<summary>`](documentation-comments.md#summary)       | Описания типа или члена типа                  |
| `<value>`        | [`<value>`](documentation-comments.md#value)           | Описания свойств                                    |
| `<typeparam>`    |                                                        | Описания параметра универсального типа                      |
| `<typeparamref>` |                                                        | Указать, что слово является именем параметра типа          |

### `<c>`

Этот тег предоставляет механизм для указания, что фрагмент текст в описании следует установить особый шрифт, которые используются для блока кода. Для строк фактический код, используйте `<code>` ([`<code>`](documentation-comments.md#code)).

__Синтаксис:__

```xml
<c>text</c>
```

__Пример:__

```csharp
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>

public class Point 
{
    // ...
}
```

### `<code>`

Этот тег используется для задания один или несколько строк исходного кода или программного вывода особого шрифта. Для небольших фрагментов кода в комментарии, используйте `<c>` ([`<c>`](documentation-comments.md#c)).

__Синтаксис:__

```xml
<code>source code or program output</code>
```

__Пример:__

```csharp
/// <summary>This method changes the point's location by
///    the given x- and y-offsets.
/// <example>For example:
/// <code>
///    Point p = new Point(3,5);
///    p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>

public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}   
```

### `<example>`

Этот тег позволяет вставить пример кода в комментарий, чтобы указать, каким образом можно использовать метод или другого элемента библиотеки. Как правило, это также включает в себя использование тега `<code>` ([`<code>`](documentation-comments.md#code)) также.

__Синтаксис:__

```xml
<example>description</example>
```

__Пример:__

См. в разделе `<code>` ([`<code>`](documentation-comments.md#code)) в качестве примера.

### `<exception>`

Этот тег позволяет документировать исключения, которые может выдавать метод.

__Синтаксис:__

```xml
<exception cref="member">description</exception>
```

где

* `member` — Имя члена. Генератор документации проверяет, что заданный элемент существует и преобразует `member` к каноническому имени элемента в файле документации.
* `description` представляет собой описание обстоятельства, в которых возникает исключение.

__Пример:__

```csharp
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException"></exception>
    /// <exception cref="MasterFileLockedOpenException"></exception>
    public static void ReadRecord(int flag) {
        if (flag == 1)
            throw new MasterFileFormatCorruptException();
        else if (flag == 2)
            throw new MasterFileLockedOpenException();
        // ...
    } 
}
```

### `<include>`

Этот тег позволяет включать сведения из XML-документа, являющиеся внешними для файла исходного кода. Внешний файл должен быть правильного формата XML-документа, и выражение XPath применяется к этому документу, чтобы указать, какие XML из этого документа, чтобы включить. `<include>` Тега затем они заменяются выбранным XML из внешнего документа.

__Синтаксис:__

```
<include file="filename" path="xpath" />
```

где

* `filename` — Имя файла из внешнего файла XML. Имя файла интерпретируется относительно файла, содержащего тег включения.
* `xpath` Такое выражение XPath, который выбирает один из XML во внешнем файле XML.

__Пример:__

Если исходный код содержится объявление, подобное:

```csharp
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

и внешнего файла «"docs.XML есть следующее содержимое:

```xml
<?xml version="1.0"?>
<extradoc>
  <class name="IntList">
     <summary>
        Contains a list of integers.
     </summary>
  </class>
  <class name="StringList">
     <summary>
        Contains a list of integers.
     </summary>
  </class>
</extradoc>
```

Затем эта же документация выводится как, если исходный код содержится:

```csharp
/// <summary>
///    Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### `<list>`

Этот тег используется для создания списка или таблицы элементов. Он может содержать `<listheader>` блок для определения строки заголовка таблицы или определение списка. (При определении таблицы, только запись `term` в заголовке необходимо предоставить.)

Каждый элемент в списке указывается с помощью `<item>` блока. При создании списка определений, оба `term` и `description` должен быть указан. Тем не менее, для таблицы, маркированного или нумерованного списка, только `description` необходимо задать.

__Синтаксис:__

```xml
<list type="bullet" | "number" | "table">
   <listheader>
      <term>term</term>
      <description>*description*</description>
   </listheader>
   <item>
      <term>term</term>
      <description>*description*</description>
   </item>
    ...
   <item>
      <term>term</term>
      <description>description</description>
   </item>
</list>
```

где

* `term` — это термин для определения, определение которого находится в `description`.
* `description` — Это либо элемент маркированного или нумерованного списка, либо определение `term`.

__Пример:__

```csharp
public class MyClass
{
    /// <summary>Here is an example of a bulleted list:
    /// <list type="bullet">
    /// <item>
    /// <description>Item 1.</description>
    /// </item>
    /// <item>
    /// <description>Item 2.</description>
    /// </item>
    /// </list>
    /// </summary>
    public static void Main () {
        // ...
    }
}
```

### `<para>`

Этот тег используется внутри других тегов, таких как `<summary>` ([`<remark>`](documentation-comments.md#remark)) или `<returns>` ([`<returns>`](documentation-comments.md#returns)) и допускает структуры для добавления текста.

__Синтаксис:__

```xml
<para>content</para>
```

где `content` — это текст абзаца.

__Пример:__

```csharp
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

### `<param>`

Этот тег используется для описания параметра для метода, конструктора или индексатора.

__Синтаксис:__

```xml
<param name="name">description</param>
```

где

* `name` — Имя параметра.
* `description` представляет собой описание параметра.

__Пример:__

```csharp
/// <summary>This method changes the point's location to
///    the given coordinates.</summary>
/// <param name="xor">the new x-coordinate.</param>
/// <param name="yor">the new y-coordinate.</param>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

### `<paramref>`

Этот тег используется для указания, что слово является параметром. Чтобы этот параметр особым образом могут обрабатываться файл документации.

__Синтаксис:__

```xml
<paramref name="name"/>
```

где `name` — это имя параметра.

__Пример:__

```csharp
/// <summary>This constructor initializes the new Point to
///    (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
/// <param name="xor">the new Point's x-coordinate.</param>
/// <param name="yor">the new Point's y-coordinate.</param>

public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

### `<permission>`

Этот тег дает возможность безопасного доступа члена задокументировать.

__Синтаксис:__

```xml
<permission cref="member">description</permission>
```

где

* `member` — Имя члена. Генератор документации проверяет, что данный элемент кода существует и преобразует *член* к каноническому имени элемента в файле документации.
* `description` представляет собой описание доступа к члену.

__Пример:__

```csharp
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>

public static void Test() {
    // ...
}
```

### `<remark>`

Этот тег используется для указания дополнительных сведений о типе. (Используйте `<summary>` ([`<summary>`](documentation-comments.md#summary)) для описания самого типа и членов типа.)

__Синтаксис:__

```xml
<remark>description</remark>
```

где `description` является текст примечания.

__Пример:__

```csharp
/// <summary>Class <c>Point</c> models a point in a 
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point 
{
    // ...
}
```

### `<returns>`

Этот тег используется для описания возвращаемого значения метода.

__Синтаксис:__

```xml
<returns>description</returns>
```

где `description` представляет собой описание возвращаемого значения.

__Пример:__

```csharp
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
///    without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```

### `<see>`

Этот тег дает ссылку, чтобы указать в тексте. Используйте `<seealso>` ([`<seealso>`](documentation-comments.md#seealso)) чтобы указать текст, отображаемый в разделе см. в разделе.

__Синтаксис:__

```xml
<see cref="member"/>
```

где `member` имя члена. Генератор документации проверяет, что данный элемент кода существует и изменяет *член* имени элемента в файле созданную документацию.

__Пример:__

```csharp
/// <summary>This method changes the point's location to
///    the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}

/// <summary>This method changes the point's location by
///    the given x- and y-offsets.
/// </summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### `<seealso>`

Этот тег позволяет запись для см. Используйте `<see>` ([`<see>`](documentation-comments.md#see)) чтобы указать ссылку из текста.

__Синтаксис:__

```xml
<seealso cref="member"/>
```

где `member` имя члена. Генератор документации проверяет, что данный элемент кода существует и изменяет *член* имени элемента в файле созданную документацию.

__Пример:__

```csharp
/// <summary>This method determines whether two Points have the same
///    location.</summary>
/// <seealso cref="operator=="/>
/// <seealso cref="operator!="/>
public override bool Equals(object o) {
    // ...
}
```

### `<summary>`

Этот тег может использоваться для описания типа или члена типа. Используйте `<remark>` ([`<remark>`](documentation-comments.md#remark)) для описания самого типа.

__Синтаксис:__

```xml
<summary>description</summary>
```

где `description` представлена сводка по типу или члену.

__Пример:__

```csharp
/// <summary>This constructor initializes the new Point to (0,0).</summary>
public Point() : this(0,0) {
}
```

### `<value>`

Этот тег позволяет свойство могут существовать описания.

__Синтаксис:__

```xml
<value>property description</value>
```

где `property description` представляет собой описание свойства.

__Пример:__

```csharp
/// <value>Property <c>X</c> represents the point's x-coordinate.</value>
public int X
{
    get { return x; }
    set { x = value; }
}
```

### `<typeparam>`

Этот тег используется для описания параметра универсального типа для класса, структуры, интерфейса, делегата или метод.

__Синтаксис:__

```xml
<typeparam name="name">description</typeparam>
```

где `name` имя параметра типа и `description` является его описанием.

__Пример:__

```csharp
/// <summary>A generic list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
    ...
}
```

### `<typeparamref>`

Этот тег используется для указания, что слово является параметром типа. Файл документации могут обрабатываться для форматирования данного параметра типа определенным образом.

__Синтаксис:__

```xml
<typeparamref name="name"/>
```

где `name` — это имя параметра типа.

__Пример:__

```csharp
/// <summary>This method fetches data and returns a list of <typeparamref name="T"/>.</summary>
/// <param name="query">query to execute</param>
public List<T> FetchData<T>(string query) {
    ...
}
```

## <a name="processing-the-documentation-file"></a>Обработка файла документации

Генератор документации создает строку идентификатора для каждого элемента в исходном коде, помеченного комментарием документации. Строка идентификатора однозначно идентифицирует элемент источника. Средство просмотра документации можно использовать строку идентификатора для идентификации соответствующего элемента метаданных или отражения, к которому применяется документации.

Файл документации не иерархическое представление исходного кода; Скорее это списка со строкой, сгенерированной идентификатор для каждого элемента.

### <a name="id-string-format"></a>Формат строки идентификатора

Генератор документации соблюдает следующие правила при формировании строк Идентификаторов:

*  Пробелы в строку не вставляются.

*  Первая часть строки определяет тип члена задокументированы, через один символ, за которым следует двоеточие. Определены следующие виды членов:

   | __Знак__ | __Описание__                                             |
   |---------------|-------------------------------------------------------------|
   | E             | событие                                                       |
   | C             | Поле                                                       |
   | M             | Метод (включая конструкторы, деструкторы и операторы) |
   | в             | Пространство имен                                                   |
   | С             | Свойство (включая индексаторы)                               |
   | T             | Тип (например, класс, делегат, перечисление, интерфейс и структуры) |
   | !             | Строка ошибки; Остальная часть строки предоставляет сведения об ошибке. Например генератор документации создает сведения об ошибках для ссылок, которые не удается разрешить. |

*  Вторая часть строки — полное имя элемента, начиная с корневого пространства имен. Имя элемента, включающей типы и пространства имен разделяются точками. Если имя самого элемента есть точки, они заменяются `#(U+0023)` символов. (Предполагается, что элемент не имеет этот символ в имени.)
*  Для методов и свойств с аргументами список аргументов, заключенный в круглые скобки. Для тех элементов, которые без аргументов скобки опускаются. Аргументы разделяются запятыми. Кодировка каждого аргумента выглядит так же, как сигнатура CLI следующим образом:
   *  Аргументы представлены своими именами в документации, основанное на их полное имя, изменить следующим образом:
      * Аргументы, представляющие универсальные типы имеют присоединенных `` ` `` символ (обратный апостроф) за которым следует число параметров типа
      * Аргументы, в которых `out` или `ref` модификатор должен `@` за именем типа. Аргументы, передаваемые по значению или через `params` не имеют специального обозначения.
      * Аргументы, которые являются массивы представляются в виде `[lowerbound:size, ... , lowerbound:size]` где число запятых равно рангу минус один, а нижние границы и размер каждого измерения, если известны, представлены в десятичном формате. Если нижняя граница или размер не указан, она опускается. Если нижняя граница и размер для определенной размерности опущены, `:` , опускается. Неравномерные массивы представляются одним `[]` на соответствующем уровне.
      * Аргументы, которые имеют типы указателей, отличный от void, представлены в виде `*` после имени типа. Указатель void представляется с помощью имени типа из `System.Void`.
      * Аргументы, которые ссылаются на параметры универсального типа, определенные для типов должны кодироваться с использованием `` ` `` символ (обратный апостроф) следуют отсчитываемый от нуля индекс параметра типа.
      * Аргументы, которые используют параметры универсального типа, определенные в методах использования — двойной обратный апостроф ``` `` ``` вместо `` ` `` используется для типов.
      * Аргументы, которые ссылаются на сконструированных универсальных типов кодируются при помощи универсального типа, за которым следует `{`следует список разделенных запятыми аргументов типа, за которыми следует `}`.

### <a name="id-string-examples"></a>Примеры строк Идентификаторов

Каждый в следующих примерах показано фрагмент кода C#, вместе с Идентификатором строку, полученную из каждого исходного элемента, комментария документации может:

*  Типы представлены их полное имя, дополненное информация общего характера:

   ```csharp
   enum Color { Red, Blue, Green }

   namespace Acme
   {
       interface IProcess {...}

       struct ValueType {...}

       class Widget: IProcess
       {
           public class NestedClass {...}
           public interface IMenuItem {...}
           public delegate void Del(int i);
           public enum Direction { North, South, East, West }
       }

       class MyList<T>
       {
           class Helper<U,V> {...}
       }
   }

   "T:Color"
   "T:Acme.IProcess"
   "T:Acme.ValueType"
   "T:Acme.Widget"
   "T:Acme.Widget.NestedClass"
   "T:Acme.Widget.IMenuItem"
   "T:Acme.Widget.Del"
   "T:Acme.Widget.Direction"
   "T:Acme.MyList`1"
   "T:Acme.MyList`1.Helper`2"
   ```

*  Поля представлены их полное имя:

   ```csharp
   namespace Acme
   {
       struct ValueType
       {
           private int total;
       }
   
       class Widget: IProcess
       {
           public class NestedClass
           {
               private int value;
           }
   
           private string message;
           private static Color defaultColor;
           private const double PI = 3.14159;
           protected readonly double monthlyAverage;
           private long[] array1;
           private Widget[,] array2;
           private unsafe int *pCount;
           private unsafe float **ppValues;
       }
   }

   "F:Acme.ValueType.total"
   "F:Acme.Widget.NestedClass.value"
   "F:Acme.Widget.message"
   "F:Acme.Widget.defaultColor"
   "F:Acme.Widget.PI"
   "F:Acme.Widget.monthlyAverage"
   "F:Acme.Widget.array1"
   "F:Acme.Widget.array2"
   "F:Acme.Widget.pCount"
   "F:Acme.Widget.ppValues"
   ```

*  Конструкторы.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           static Widget() {...}
           public Widget() {...}
           public Widget(string s) {...}
       }
   }

   "M:Acme.Widget.#cctor"
   "M:Acme.Widget.#ctor"
   "M:Acme.Widget.#ctor(System.String)"
   ```

*  Деструкторы.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           ~Widget() {...}
       }
   }
   
   "M:Acme.Widget.Finalize"
   ```

*  Методы.

   ```csharp
   namespace Acme
   {
       struct ValueType
       {
           public void M(int i) {...}
       }

       class Widget: IProcess
       {
           public class NestedClass
           {
               public void M(int i) {...}
           }

           public static void M0() {...}
           public void M1(char c, out float f, ref ValueType v) {...}
           public void M2(short[] x1, int[,] x2, long[][] x3) {...}
           public void M3(long[][] x3, Widget[][,,] x4) {...}
           public unsafe void M4(char *pc, Color **pf) {...}
           public unsafe void M5(void *pv, double *[][,] pd) {...}
           public void M6(int i, params object[] args) {...}
       }

       class MyList<T>
       {
           public void Test(T t) { }
       }

       class UseList
       {
           public void Process(MyList<int> list) { }
           public MyList<T> GetValues<T>(T inputValue) { return null; }
       }
   }

   "M:Acme.ValueType.M(System.Int32)"
   "M:Acme.Widget.NestedClass.M(System.Int32)"
   "M:Acme.Widget.M0"
   "M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
   "M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
   "M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:][])"
   "M:Acme.Widget.M4(System.Char*,Color**)"
   "M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][])"
   "M:Acme.Widget.M6(System.Int32,System.Object[])"
   "M:Acme.MyList`1.Test(`0)"
   "M:Acme.UseList.Process(Acme.MyList{System.Int32})"
   "M:Acme.UseList.GetValues``(``0)"
   ```

*  Свойства и индексаторы.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public int Width { get {...} set {...} }
           public int this[int i] { get {...} set {...} }
           public int this[string s, int i] { get {...} set {...} }
       }
   }

   "P:Acme.Widget.Width"
   "P:Acme.Widget.Item(System.Int32)"
   "P:Acme.Widget.Item(System.String,System.Int32)"
   ```

*  события.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public event Del AnEvent;
       }
   }

   "E:Acme.Widget.AnEvent"
   ```

*  Унарные операторы.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static Widget operator+(Widget x) {...}
       }
   }

   "M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
   ```

   Полный набор унарный оператор функции, используемых выглядит следующим образом: `op_UnaryPlus`, `op_UnaryNegation`, `op_LogicalNot`, `op_OnesComplement`, `op_Increment`, `op_Decrement`, `op_True`, и `op_False`.

*  Бинарные операторы.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static Widget operator+(Widget x1, Widget x2) {...}
       }
   }

   "M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
   ```

   Полный набор имен функцию бинарного оператора, используемых выглядит следующим образом: `op_Addition`, `op_Subtraction`, `op_Multiply`, `op_Division`, `op_Modulus`, `op_BitwiseAnd`, `op_BitwiseOr`, `op_ExclusiveOr`, `op_LeftShift`, `op_RightShift`, `op_Equality`, `op_Inequality`, `op_LessThan`, `op_LessThanOrEqual`, `op_GreaterThan`, и `op_GreaterThanOrEqual`.

*  Операторы преобразования имеют замыкающие "`~`" и типом возвращаемого значения.

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static explicit operator int(Widget x) {...}
           public static implicit operator long(Widget x) {...}
       }
   }

   "M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
   "M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"
   ```

## <a name="an-example"></a>Пример

### <a name="c-source-code"></a>Исходный код C#

В примере показан исходный код `Point` класса:

```csharp
namespace Graphics
{

/// <summary>Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point 
{

    /// <summary>Instance variable <c>x</c> represents the point's
    ///    x-coordinate.</summary>
    private int x;

    /// <summary>Instance variable <c>y</c> represents the point's
    ///    y-coordinate.</summary>
    private int y;

    /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
    public int X
    {
        get { return x; }
        set { x = value; }
    }

    /// <value>Property <c>Y</c> represents the point's y-coordinate.</value>
    public int Y
    {
        get { return y; }
        set { y = value; }
    }

    /// <summary>This constructor initializes the new Point to
    ///    (0,0).</summary>
    public Point() : this(0,0) {}

    /// <summary>This constructor initializes the new Point to
    ///    (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
    /// <param><c>xor</c> is the new Point's x-coordinate.</param>
    /// <param><c>yor</c> is the new Point's y-coordinate.</param>
    public Point(int xor, int yor) {
        X = xor;
        Y = yor;
    }

    /// <summary>This method changes the point's location to
    ///    the given coordinates.</summary>
    /// <param><c>xor</c> is the new x-coordinate.</param>
    /// <param><c>yor</c> is the new y-coordinate.</param>
    /// <see cref="Translate"/>
    public void Move(int xor, int yor) {
        X = xor;
        Y = yor;
    }

    /// <summary>This method changes the point's location by
    ///    the given x- and y-offsets.
    /// <example>For example:
    /// <code>
    ///    Point p = new Point(3,5);
    ///    p.Translate(-1,3);
    /// </code>
    /// results in <c>p</c>'s having the value (2,8).
    /// </example>
    /// </summary>
    /// <param><c>xor</c> is the relative x-offset.</param>
    /// <param><c>yor</c> is the relative y-offset.</param>
    /// <see cref="Move"/>
    public void Translate(int xor, int yor) {
        X += xor;
        Y += yor;
    }

    /// <summary>This method determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>o</c> is the object to be compared to the current object.
    /// </param>
    /// <returns>True if the Points have the same location and they have
    ///    the exact same type; otherwise, false.</returns>
    /// <seealso cref="operator=="/>
    /// <seealso cref="operator!="/>
    public override bool Equals(object o) {
        if (o == null) {
            return false;
        }

        if (this == o) {
            return true;
        }

        if (GetType() == o.GetType()) {
            Point p = (Point)o;
            return (X == p.X) && (Y == p.Y);
        }
        return false;
    }

    /// <summary>Report a point's location as a string.</summary>
    /// <returns>A string representing a point's location, in the form (x,y),
    ///    without any leading, training, or embedded whitespace.</returns>
    public override string ToString() {
        return "(" + X + "," + Y + ")";
    }

    /// <summary>This operator determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>p1</c> is the first Point to be compared.</param>
    /// <param><c>p2</c> is the second Point to be compared.</param>
    /// <returns>True if the Points have the same location and they have
    ///    the exact same type; otherwise, false.</returns>
    /// <seealso cref="Equals"/>
    /// <seealso cref="operator!="/>
    public static bool operator==(Point p1, Point p2) {
        if ((object)p1 == null || (object)p2 == null) {
            return false;
        }

        if (p1.GetType() == p2.GetType()) {
            return (p1.X == p2.X) && (p1.Y == p2.Y);
        }

        return false;
    }

    /// <summary>This operator determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>p1</c> is the first Point to be compared.</param>
    /// <param><c>p2</c> is the second Point to be compared.</param>
    /// <returns>True if the Points do not have the same location and the
    ///    exact same type; otherwise, false.</returns>
    /// <seealso cref="Equals"/>
    /// <seealso cref="operator=="/>
    public static bool operator!=(Point p1, Point p2) {
        return !(p1 == p2);
    }

    /// <summary>This is the entry point of the Point class testing
    /// program.
    /// <para>This program tests each method and operator, and
    /// is intended to be run after any non-trivial maintenance has
    /// been performed on the Point class.</para></summary>
    public static void Main() {
        // class test code goes here
    }
}
}
```

### <a name="resulting-xml"></a>Результирующий XML

Здесь представлен результат, созданный генератором документации для заданного исходного кода для класса `Point`, как показано выше:

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
    <members>
        <member name="T:Graphics.Point">
            <summary>Class <c>Point</c> models a point in a two-dimensional
            plane.
            </summary>
        </member>

        <member name="F:Graphics.Point.x">
            <summary>Instance variable <c>x</c> represents the point's
            x-coordinate.</summary>
        </member>

        <member name="F:Graphics.Point.y">
            <summary>Instance variable <c>y</c> represents the point's
            y-coordinate.</summary>
        </member>

        <member name="M:Graphics.Point.#ctor">
            <summary>This constructor initializes the new Point to
        (0,0).</summary>
        </member>

        <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
            <summary>This constructor initializes the new Point to
            (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
            <param><c>xor</c> is the new Point's x-coordinate.</param>
            <param><c>yor</c> is the new Point's y-coordinate.</param>
        </member>

        <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
            <summary>This method changes the point's location to
            the given coordinates.</summary>
            <param><c>xor</c> is the new x-coordinate.</param>
            <param><c>yor</c> is the new y-coordinate.</param>
            <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
        </member>

        <member
            name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
            <summary>This method changes the point's location by
            the given x- and y-offsets.
            <example>For example:
            <code>
            Point p = new Point(3,5);
            p.Translate(-1,3);
            </code>
            results in <c>p</c>'s having the value (2,8).
            </example>
            </summary>
            <param><c>xor</c> is the relative x-offset.</param>
            <param><c>yor</c> is the relative y-offset.</param>
            <see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
        </member>

        <member name="M:Graphics.Point.Equals(System.Object)">
            <summary>This method determines whether two Points have the same
            location.</summary>
            <param><c>o</c> is the object to be compared to the current
            object.
            </param>
            <returns>True if the Points have the same location and they have
            the exact same type; otherwise, false.</returns>
            <seealso
      cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
            <seealso
      cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member name="M:Graphics.Point.ToString">
            <summary>Report a point's location as a string.</summary>
            <returns>A string representing a point's location, in the form
            (x,y),
            without any leading, training, or embedded whitespace.</returns>
        </member>

        <member
       name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
            <summary>This operator determines whether two Points have the
            same
            location.</summary>
            <param><c>p1</c> is the first Point to be compared.</param>
            <param><c>p2</c> is the second Point to be compared.</param>
            <returns>True if the Points have the same location and they have
            the exact same type; otherwise, false.</returns>
            <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
            <seealso
     cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member
      name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
            <summary>This operator determines whether two Points have the
            same
            location.</summary>
            <param><c>p1</c> is the first Point to be compared.</param>
            <param><c>p2</c> is the second Point to be compared.</param>
            <returns>True if the Points do not have the same location and
            the
            exact same type; otherwise, false.</returns>
            <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
            <seealso
      cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member name="M:Graphics.Point.Main">
            <summary>This is the entry point of the Point class testing
            program.
            <para>This program tests each method and operator, and
            is intended to be run after any non-trivial maintenance has
            been performed on the Point class.</para></summary>
        </member>

        <member name="P:Graphics.Point.X">
            <value>Property <c>X</c> represents the point's
            x-coordinate.</value>
        </member>

        <member name="P:Graphics.Point.Y">
            <value>Property <c>Y</c> represents the point's
            y-coordinate.</value>
        </member>
    </members>
</doc>
```
