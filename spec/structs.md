# <a name="structs"></a>Структуры

Структуры похожи на классы, в том, что они представляют структуры данных, которые могут содержать данные-члены и функции-члены. Тем не менее в отличие от классов, структуры являются типами значений и не требуется выделение кучи. Переменная типа структура непосредственно содержит данные структуры, тогда как переменная типа класса содержит ссылку на данные, ранее известные как объект.

Структуры особенно удобны для небольших структур данных, имеющих семантику значений. Хорошими примерами структур можно считать комплексные числа, точки в системе координат или словари с парами ключ-значение. Ключ для этих структур данных является наличие нескольких переменных-членов, что они не требуют использования наследования или ссылочного идентификатора, и что их можно легко реализовать с использованием семантики значения, когда при присваивании копируется значение вместо ссылки на.

Как описано в разделе [простых типов](types.md#simple-types), простые типы, предоставляемые языком C#, таких как `int`, `double`, и `bool`, фактически являются все типы структуры. Так же, как эти предопределенные типы являются структурами, можно также использовать структуры и перегрузки операторов для реализации новых типов «primitive» на языке C#. В конце этой главе приведены два примера таких типов ([примеры структур](structs.md#struct-examples)).

## <a name="struct-declarations"></a>Объявления структур

Объект *struct_declaration* — *type_declaration* ([объявления типов](namespaces.md#type-declarations)), объявляется новая структура:

```antlr
struct_declaration
    : attributes? struct_modifier* 'partial'? 'struct' identifier type_parameter_list?
      struct_interfaces? type_parameter_constraints_clause* struct_body ';'?
    ;
```

Объект *struct_declaration* состоит из необязательного набора *атрибуты* ([атрибуты](attributes.md)), а затем необязательный набор *struct_modifier*s ([модификаторы структуры](structs.md#struct-modifiers)), а затем использовать необязательный `partial` модификатор, а затем с помощью ключевого слова `struct` и *идентификатор* , которая содержит название структуры, за которым следует Необязательный *type_parameter_list* спецификации ([параметры типа](classes.md#type-parameters)), а затем использовать необязательный *struct_interfaces* спецификации ([Модификатор partial](structs.md#partial-modifier))), а затем использовать необязательный *type_parameter_constraints_clause*спецификации s ([ограничения параметров типа](classes.md#type-parameter-constraints)), а затем *struct_body* ([основной части структуры](structs.md#struct-body)), при необходимости, а затем точкой с запятой.

### <a name="struct-modifiers"></a>Модификаторы структуры

Объект *struct_declaration* может включать последовательность модификаторов структуры:

```antlr
struct_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | struct_modifier_unsafe
    ;
```

Это ошибка времени компиляции для один и тот же модификатор встречается несколько раз в объявлении структуры.

Модификаторы объявления структуры имеют одинаковое значение, что и объявление класса ([объявлений классов](classes.md#class-declarations)).

### <a name="partial-modifier"></a>Модификатор partial

`partial` Модификатор указывает, что это *struct_declaration* является объявлением разделяемого типа. Нескольких объявлениях разделяемой структуры с тем же именем в едином объявлении пространства имен или тип объединения для одно объявление структуры, следуя правилам указан в [разделяемых типов](classes.md#partial-types).

### <a name="struct-interfaces"></a>Интерфейсы структуры

Объявление структуры может содержать *struct_interfaces* спецификации, в котором регистр структуры говорят, что прямая реализация заданные типы интерфейса.

```antlr
struct_interfaces
    : ':' interface_type_list
    ;
```

Реализация интерфейсов рассматривается далее в [реализации интерфейсов](interfaces.md#interface-implementations).

### <a name="struct-body"></a>Основной части структуры

*Struct_body* структуры определяет членов структуры.

```antlr
struct_body
    : '{' struct_member_declaration* '}'
    ;
```

## <a name="struct-members"></a>Члены структуры

Члены структуры состоят из членов, представленных его *struct_member_declaration*s и члены, унаследованные от типа `System.ValueType`.

```antlr
struct_member_declaration
    : constant_declaration
    | field_declaration
    | method_declaration
    | property_declaration
    | event_declaration
    | indexer_declaration
    | operator_declaration
    | constructor_declaration
    | static_constructor_declaration
    | type_declaration
    | struct_member_declaration_unsafe
    ;
```

За исключением различий, описанных в [различия классов и структур](structs.md#class-and-struct-differences), описания членов класса в [члены класса](classes.md#class-members) через [итераторы](classes.md#iterators) применяются к структуре а также элементы.

## <a name="class-and-struct-differences"></a>Различия классов и структур

Структуры отличаются от классов в ряде важных аспектов:

*  Структуры являются типами значений ([значение семантику](structs.md#value-semantics)).
*  Все типы структуры неявно наследуются от класса `System.ValueType` ([наследования](structs.md#inheritance)).
*  Присвоение переменной с типом структуры создается копия значения, присваиваемого ([назначения](structs.md#assignment)).
*  Значение по умолчанию для структуры является значение, создаваемое путем установки все поля типа значения полей с типом значения по умолчанию и справочник по всем `null` ([значения по умолчанию](structs.md#default-values)).
*  Операции упаковки и распаковки используются для преобразования между типом структуры и `object` ([упаковка-преобразование и распаковка-преобразование](structs.md#boxing-and-unboxing)).
*  Значение `this` отличается для структур ([такой доступ](expressions.md#this-access)).
*  Объявления полей экземпляра для структуры не могут содержать инициализаторы переменных ([поле инициализаторы](structs.md#field-initializers)).
*  В структуре не разрешается объявлять конструктор экземпляров ([конструкторы](structs.md#constructors)).
*  В структуре не разрешается объявить деструктор ([деструкторы](structs.md#destructors)).

### <a name="value-semantics"></a>Семантика значения

Структуры являются типами значений ([типы значений](types.md#value-types)) к имеющих семантику значений. Классы, с другой стороны, являются ссылочными типами ([ссылочные типы](types.md#reference-types)) и к семантики ссылок.

Переменная типа структура непосредственно содержит данные структуры, тогда как переменная типа класса содержит ссылку на данные, ранее известные как объект. Когда структура `B` содержит поле экземпляра типа `A` и `A` является типом структуры, это ошибка времени компиляции для `A` зависят от `B` или тип, сформированный из `B`. Структура `X` ***напрямую зависит от*** структуры `Y` Если `X` содержит поле экземпляра типа `Y`. Рассмотрим следующее определение, полный набор структур, от которого зависит структура является транзитивное замыкание ***напрямую зависит от*** связи.  Пример
```csharp
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```
является ошибкой, поскольку `Node` содержит поле экземпляра его собственного типа.  Другой пример
```csharp
struct A { B b; }

struct B { C c; }

struct C { A a; }
```
является ошибкой, так как каждый из типов `A`, `B`, и `C` зависят друг от друга.

С классами это две переменные могут ссылаться на тот же объект и поэтому может случиться операции над одной переменной затронут объект, который ссылается другая переменная. При использовании структур каждая переменная имеет свою собственную копию данных (в частности, за исключением `ref` и `out` переменных параметров), и операции над одной могут затрагивать другую невозможно. Более того, так как структуры не являются ссылочными типами, он не поддерживается для значений типа структуры, чтобы быть `null`.

При объявлении
```csharp
struct Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
фрагмент кода
```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```
Выводит значение `10`. Назначение `a` для `b` создает копию значения, и `b` , таким образом, не влияет на `a.x`. Было `Point` вместо этого был объявлен как класс, выходные данные будут `100` поскольку `a` и `b` будет ссылаться на тот же объект.

### <a name="inheritance"></a>Наследование

Все типы структуры неявно наследуются от класса `System.ValueType`, который, в свою очередь, наследует от класса `object`. Объявление структуры может указать список реализованных интерфейсов, но он не поддерживается для объявления структуры, чтобы указать базовый класс.

Типы структуры никогда не является абстрактным и всегда неявно запечатаны. `abstract` И `sealed` модификаторы таким образом не разрешается использовать в объявлении структуры.

Так как для структур не поддерживается наследование, объявленным уровнем доступности члена структуры не может быть `protected` или `protected internal`.

Функции-члены в структуре не может быть `abstract` или `virtual`и `override` модификатор может быть указан только в переопределите методы, унаследованные от `System.ValueType`.

### <a name="assignment"></a>Назначение

Присвоение переменной типа структуры создает копию значения, присваиваемого. В отличие от назначения переменной типа класса, который копирует ссылка, но не объект, указанный ссылкой.

Аналогичным образом, переданный в качестве значения параметра или возвращаемые в результате функции-члена структуры, структуры создается копия. Структура может передаваться по ссылке, чтобы с помощью функции-члена `ref` или `out` параметра.

Если свойство или индексатор структуры является целевым объектом назначения, выражение экземпляра, связанное с правами доступа свойства или индексатора должен классифицироваться как переменную. Если экземпляр выражение классифицируется как значение, возникает ошибка времени компиляции. Это описано более подробно [простое присваивание](expressions.md#simple-assignment).

### <a name="default-values"></a>Значения по умолчанию

Как описано в разделе [значения по умолчанию](variables.md#default-values), несколько типов переменных автоматически инициализируются значениями по умолчанию, при их создании. Для переменных типов классов и других ссылочных типов это значение по умолчанию — `null`. Тем не менее поскольку структуры являются типами значений, которые не могут быть `null`, значение по умолчанию для структуры является значение, создаваемое путем установки все поля типа значения полей с типом значения по умолчанию и справочник по всем `null`.

Ссылка на `Point` структуры, объявленные выше, пример
```csharp
Point[] a = new Point[100];
```
присваивает каждой из них `Point` массива значение, создаваемое путем установки `x` и `y` поля до нуля.

Значение по умолчанию структура соответствует равным значению, возвращенному конструктором по умолчанию структуры ([конструкторы по умолчанию](types.md#default-constructors)). В отличие от класса структуры не допускается объявление конструктора экземпляра без параметров. Вместо этого каждая структура неявно содержит конструктор экземпляра без параметров, который всегда возвращает значение, полученное путем установки значения по умолчанию и справочник по всем все поля типа значения для полей с типом `null`.

Структуры должны разрабатываться необходимо учитывать состояние инициализации по умолчанию в недопустимом состоянии. В примере
```csharp
using System;

struct KeyValuePair
{
    string key;
    string value;

    public KeyValuePair(string key, string value) {
        if (key == null || value == null) throw new ArgumentException();
        this.key = key;
        this.value = value;
    }
}
```
конструктор экземпляра, определяемые пользователем обеспечивает защиту от значения null, только она была явно вызвана. В случаях, где `KeyValuePair` переменной регулируется инициализации значений по умолчанию — `key` и `value` поля будет иметь значение null, и структуры должны быть готовы обрабатывать это состояние.

### <a name="boxing-and-unboxing"></a>Упаковка-преобразование и распаковка-преобразование

Значение типа класса можно преобразовать в тип `object` или к типу интерфейса, который реализуется с помощью класса просто обработка ссылки в виде другого типа во время компиляции. Аналогичным образом, значение типа `object` или значение типа интерфейса могут преобразовываться к типу класса без изменения ссылки (но безусловно проверку типов во время выполнения необходим в данном случае).

Так как структуры не являются ссылочными типами, эти операции реализованы по-разному для типов структуры. Если значение с типом структуры преобразуется в тип `object` или к типу интерфейса, реализуемого классом структуры, выполняется операция упаковки-преобразования. Аналогично когда значение типа `object` или значение типа интерфейса преобразуется к типу структуры, выполняется операция распаковки. Ключевое отличие от одинаковых операций для типов классов является то, что упаковка-преобразование и распаковка-преобразование копирует значение структуры в или из упакованного экземпляра. Таким образом после операции упаковки или распаковки, изменения, внесенные в распакованную структуру не отражаются в упакованной структуре.

Когда типом структуры переопределяет виртуальный метод, который наследуется от `System.Object` (такие как `Equals`, `GetHashCode`, или `ToString`), вызов виртуального метода в экземпляре типа структуры не приводит к выполнению упаковки. Это верно даже в том случае, когда структура используется в качестве параметра типа, если вызов происходит через экземпляр параметра типа. Пример:
```csharp
using System;

struct Counter
{
    int value;

    public override string ToString() {
        value++;
        return value.ToString();
    }
}

class Program
{
    static void Test<T>() where T: new() {
        T x = new T();
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
        Console.WriteLine(x.ToString());
    }

    static void Main() {
        Test<Counter>();
    }
}
```

Выходные данные программы будут:
```
1
2
3
```

Несмотря на то, что он является плохим стилем `ToString` побочными эффектами, в примере показано, что упаковка-преобразование не место для трех вызовов функции `x.ToString()`.

Аналогичным образом выполняется упаковка-преобразование не неявно при доступе к члену в параметр типа с ограничением. Например, предположим, что интерфейс `ICounter` содержит метод `Increment` которого может использоваться для изменения значения. Если `ICounter` используется в качестве ограничения, реализация `Increment` метод вызывается со ссылкой на переменную, `Increment` был вызван для никогда не упакованной копии.

```csharp
using System;

interface ICounter
{
    void Increment();
}

struct Counter: ICounter
{
    int value;

    public override string ToString() {
        return value.ToString();
    }

    void ICounter.Increment() {
        value++;
    }
}

class Program
{
    static void Test<T>() where T: ICounter, new() {
        T x = new T();
        Console.WriteLine(x);
        x.Increment();                    // Modify x
        Console.WriteLine(x);
        ((ICounter)x).Increment();        // Modify boxed copy of x
        Console.WriteLine(x);
    }

    static void Main() {
        Test<Counter>();
    }
}
```

Первый вызов `Increment` изменяет значение в переменной `x`. Это эквивалентно не второй вызов `Increment`, который изменяет значение в упакованной копии `x`. Таким образом программы выводится следующий результат:
```
0
1
1
```

Дополнительные сведения об упаковке и распаковке см. в разделе [упаковка-преобразование и распаковка-преобразование](types.md#boxing-and-unboxing).

### <a name="meaning-of-this"></a>Это значение

В конструкторе экземпляра или экземпляра функцию-член класса `this` классифицируется как значение. Таким образом, хотя `this` может использоваться для ссылки на экземпляр для которого функция-член вызывается, он уже не сможете назначить `this` в функции-члене класса.

В конструкторе экземпляра структуры `this` соответствует `out` параметра типа структуры и в функции-члене экземпляра структуры, `this` соответствует `ref` параметр типа структуры. В обоих случаях `this` классифицируется как переменная, и можно изменить всю структуру, для которого была вызвана функция-член, назначив `this` или путем передачи его в виде `ref` или `out` параметра.

### <a name="field-initializers"></a>Инициализаторы полей

Как описано в разделе [значения по умолчанию](structs.md#default-values), значение по умолчанию структура состоит из значения, полученный в результате установки все значения полей с типом значения по умолчанию и справочник по всем полей с типом `null`. По этой причине структуры не допускает объявления полей экземпляра содержать инициализаторы переменных. Это ограничение применяется только к полям экземпляра. Статические поля структуры могут содержать инициализаторы переменных.

Пример
```csharp
struct Point
{
    public int x = 1;  // Error, initializer not permitted
    public int y = 1;  // Error, initializer not permitted
}
```
— Ошибка, так как объявления полей экземпляра содержат инициализаторы переменных.

### <a name="constructors"></a>Конструкторы

В отличие от класса структуры не допускается объявление конструктора экземпляра без параметров. Вместо этого каждая структура неявно содержит конструктор экземпляра без параметров, который всегда возвращает значение, полученное путем установки значения по умолчанию и справочник по всем поля типа значения NULL все поля типа значения ([Конструкторыпоумолчанию](types.md#default-constructors)). В структуре можно объявлять конструкторы экземпляров с параметрами. Пример
```csharp
struct Point
{
    int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

При объявлении выше, операторы
```csharp
Point p1 = new Point();
Point p2 = new Point(0, 0);
```
они создают `Point` с `x` и `y` приравнивается к нулю.

Конструктор экземпляра структуры не может содержать инициализатор конструктора формы `base(...)`.

Если конструктор экземпляра структуры не указан инициализатор конструктора `this` переменная соответствует `out` параметр типа структуры и точно так же `out` параметра `this` должен быть явно присвоен () [Определенного присваивания](variables.md#definite-assignment)) в каждом месте, где Возвращает конструктор. Если конструктор экземпляра структуры указан инициализатор конструктора `this` переменная соответствует `ref` параметр типа структуры и точно так же `ref` параметра `this` считается определенно присвоенной на запись в тело конструктора. Рассмотрим приведенную ниже реализацию конструктора:
```csharp
struct Point
{
    int x, y;

    public int X {
        set { x = value; }
    }

    public int Y {
        set { y = value; }
    }

    public Point(int x, int y) {
        X = x;        // error, this is not yet definitely assigned
        Y = y;        // error, this is not yet definitely assigned
    }
}
```

Функция-член не экземпляр (включая методы доступа set для свойства `X` и `Y`) может быть вызван, пока все поля структуры были определенно назначены. Единственное исключение включает автоматически реализуемые свойства ([автоматически реализуемые свойства](classes.md#automatically-implemented-properties)). Правила определенного назначения ([простые выражения присваивания](variables.md#simple-assignment-expressions)) специально исключать назначения для автосвойства с типом структуры внутри конструктора экземпляра этого типа структуры: такое присваивание считается определенного Назначение скрытые резервное поле свойства автоматически. Таким образом следующее является допустимым:

```csharp
struct Point
{
    public int X { get; set; }
    public int Y { get; set; }

    public Point(int x, int y) {
        X = x;      // allowed, definitely assigns backing field
        Y = y;      // allowed, definitely assigns backing field
    }
```

### <a name="destructors"></a>Деструкторы

В структуре не разрешается объявить деструктор.

### <a name="static-constructors"></a>Статические конструкторы

Статические конструкторы для структур выполните большую часть тех же правил, и для классов. Выполнение статического конструктора структуры запускается первым из следующих событий в домене приложения:

*  Статический член типа структуры есть ссылки.
*  Вызывается явно объявленный конструктор типа структуры.

Создание значений по умолчанию ([значения по умолчанию](structs.md#default-values)) типы структуры не вызывает статический конструктор. (Примером этого является начальное значение элементов в массиве).

## <a name="struct-examples"></a>Примеры структур

Далее показано два примера использования `struct` типов, которые могут использоваться аналогичным образом в предопределенных типов языка, но имеют измененную семантику типов.

### <a name="database-integer-type"></a>Целочисленный тип базы данных

`DBInt` Ниже структура реализует целочисленный тип, который может представлять полный набор значений `int` тип, а также дополнительное состояние, указывающее на неизвестное значение. Тип с такими характеристиками обычно используется в базах данных.

```csharp
using System;

public struct DBInt
{
    // The Null member represents an unknown DBInt value.

    public static readonly DBInt Null = new DBInt();

    // When the defined field is true, this DBInt represents a known value
    // which is stored in the value field. When the defined field is false,
    // this DBInt represents an unknown value, and the value field is 0.

    int value;
    bool defined;

    // Private instance constructor. Creates a DBInt with a known value.

    DBInt(int value) {
        this.value = value;
        this.defined = true;
    }

    // The IsNull property is true if this DBInt represents an unknown value.

    public bool IsNull { get { return !defined; } }

    // The Value property is the known value of this DBInt, or 0 if this
    // DBInt represents an unknown value.

    public int Value { get { return value; } }

    // Implicit conversion from int to DBInt.

    public static implicit operator DBInt(int x) {
        return new DBInt(x);
    }

    // Explicit conversion from DBInt to int. Throws an exception if the
    // given DBInt represents an unknown value.

    public static explicit operator int(DBInt x) {
        if (!x.defined) throw new InvalidOperationException();
        return x.value;
    }

    public static DBInt operator +(DBInt x) {
        return x;
    }

    public static DBInt operator -(DBInt x) {
        return x.defined ? -x.value : Null;
    }

    public static DBInt operator +(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value + y.value: Null;
    }

    public static DBInt operator -(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value - y.value: Null;
    }

    public static DBInt operator *(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value * y.value: Null;
    }

    public static DBInt operator /(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value / y.value: Null;
    }

    public static DBInt operator %(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value % y.value: Null;
    }

    public static DBBool operator ==(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value == y.value: DBBool.Null;
    }

    public static DBBool operator !=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value != y.value: DBBool.Null;
    }

    public static DBBool operator >(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value > y.value: DBBool.Null;
    }

    public static DBBool operator <(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value < y.value: DBBool.Null;
    }

    public static DBBool operator >=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value >= y.value: DBBool.Null;
    }

    public static DBBool operator <=(DBInt x, DBInt y) {
        return x.defined && y.defined? x.value <= y.value: DBBool.Null;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBInt)) return false;
        DBInt x = (DBInt)obj;
        return value == x.value && defined == x.defined;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        return defined? value.ToString(): "DBInt.Null";
    }
}
```

### <a name="database-boolean-type"></a>Логический тип базы данных

`DBBool` Ниже структура реализует три значения логического типа. Возможные значения этого типа: `DBBool.True`, `DBBool.False`, и `DBBool.Null`, где `Null` элемент указывает неизвестное значение. Такие троичную логические типы обычно используются в базах данных.

```csharp
using System;

public struct DBBool
{
    // The three possible DBBool values.

    public static readonly DBBool Null = new DBBool(0);
    public static readonly DBBool False = new DBBool(-1);
    public static readonly DBBool True = new DBBool(1);

    // Private field that stores -1, 0, 1 for False, Null, True.

    sbyte value;

    // Private instance constructor. The value parameter must be -1, 0, or 1.

    DBBool(int value) {
        this.value = (sbyte)value;
    }

    // Properties to examine the value of a DBBool. Return true if this
    // DBBool has the given value, false otherwise.

    public bool IsNull { get { return value == 0; } }

    public bool IsFalse { get { return value < 0; } }

    public bool IsTrue { get { return value > 0; } }

    // Implicit conversion from bool to DBBool. Maps true to DBBool.True and
    // false to DBBool.False.

    public static implicit operator DBBool(bool x) {
        return x? True: False;
    }

    // Explicit conversion from DBBool to bool. Throws an exception if the
    // given DBBool is Null, otherwise returns true or false.

    public static explicit operator bool(DBBool x) {
        if (x.value == 0) throw new InvalidOperationException();
        return x.value > 0;
    }

    // Equality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.

    public static DBBool operator ==(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value == y.value? True: False;
    }

    // Inequality operator. Returns Null if either operand is Null, otherwise
    // returns True or False.

    public static DBBool operator !=(DBBool x, DBBool y) {
        if (x.value == 0 || y.value == 0) return Null;
        return x.value != y.value? True: False;
    }

    // Logical negation operator. Returns True if the operand is False, Null
    // if the operand is Null, or False if the operand is True.

    public static DBBool operator !(DBBool x) {
        return new DBBool(-x.value);
    }

    // Logical AND operator. Returns False if either operand is False,
    // otherwise Null if either operand is Null, otherwise True.

    public static DBBool operator &(DBBool x, DBBool y) {
        return new DBBool(x.value < y.value? x.value: y.value);
    }

    // Logical OR operator. Returns True if either operand is True, otherwise
    // Null if either operand is Null, otherwise False.

    public static DBBool operator |(DBBool x, DBBool y) {
        return new DBBool(x.value > y.value? x.value: y.value);
    }

    // Definitely true operator. Returns true if the operand is True, false
    // otherwise.

    public static bool operator true(DBBool x) {
        return x.value > 0;
    }

    // Definitely false operator. Returns true if the operand is False, false
    // otherwise.

    public static bool operator false(DBBool x) {
        return x.value < 0;
    }

    public override bool Equals(object obj) {
        if (!(obj is DBBool)) return false;
        return value == ((DBBool)obj).value;
    }

    public override int GetHashCode() {
        return value;
    }

    public override string ToString() {
        if (value > 0) return "DBBool.True";
        if (value < 0) return "DBBool.False";
        return "DBBool.Null";
    }
}
```
