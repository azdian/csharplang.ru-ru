# <a name="attributes"></a>Атрибуты

Большая часть языка C# позволяет программисту указывать декларативные сведения о сущностях, определенных в программе. Например, доступность метода в классе определяется дополнив его с *method_modifier*s `public`, `protected`, `internal`, и `private`.

C# позволяет программистам создавать новые типы декларативных сведений, называемых ***атрибуты***. Программисты могут присоединения атрибутов для различных сущностей программы и получить сведения об атрибутах в среде выполнения. Например, структура может определить `HelpAttribute` атрибут, который можно поместить на определенные элементы программы (например, классы и методы) для предоставления сопоставление этих элементов программы на документацию.

Атрибуты определяются путем объявления классов атрибутов ([классы атрибутов](attributes.md#attribute-classes)), которые могут иметь позиционные и именованные параметры ([Positional и именованные параметры](attributes.md#positional-and-named-parameters)). Атрибуты присоединяются к сущности в программе C# с помощью спецификаций атрибутов ([спецификация атрибута](attributes.md#attribute-specification)) и могут быть получены во время выполнения как экземпляры атрибута ([экземпляры атрибута](attributes.md#attribute-instances)).

## <a name="attribute-classes"></a>Классы атрибутов

Класс, производный от абстрактного класса `System.Attribute`, прямо или косвенно, является ***класс атрибута***. Объявление класса атрибута определяет новый вид ***атрибут*** , можно поместить в объявлении. По соглашению классы атрибутов именуются с суффиксом `Attribute`. Использовании атрибута может включить или пропустить этот суффикс.

### <a name="attribute-usage"></a>Использование атрибута

Атрибут `AttributeUsage` ([атрибут AttributeUsage](attributes.md#the-attributeusage-attribute)) используется для описания того, как можно использовать класс атрибута.

`AttributeUsage` имеет позиционный параметр ([Positional и именованные параметры](attributes.md#positional-and-named-parameters)), позволяющий класс атрибута указывать типы объявлений, на которых он может использоваться. Пример

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute 
{
    ...
}
```

Определяет класс атрибута с именем `SimpleAttribute` , можно поместить в *class_declaration*s и *interface_declaration*только s. Пример

```csharp
[Simple] class Class1 {...}

[Simple] interface Interface1 {...}
```

показаны несколько способов применения `Simple` атрибута. Несмотря на то, что этот атрибут определен с именем `SimpleAttribute`, если этот атрибут используется, `Attribute` суффикс можно опускать, приводит к короткое имя `Simple`. Таким образом приведенный выше пример взят семантически эквивалентно следующему:

```csharp
[SimpleAttribute] class Class1 {...}

[SimpleAttribute] interface Interface1 {...}
```

`AttributeUsage` имеет именованный параметр ([Positional и именованные параметры](attributes.md#positional-and-named-parameters)) вызывается `AllowMultiple`, которое указывает, является ли атрибут может быть указан более одного раза для данной сущности. Если `AllowMultiple` для атрибута класса имеет значение true, то классу этого атрибута является ***класс атрибута многократного использования***и может быть указан более одного раза в сущности. Если `AllowMultiple` для атрибута класса имеет значение false или не указано, то классу этого атрибута является ***однократного использования класса атрибута***его можно указать не более одного раза в сущности.

Пример

```csharp
using System;

[AttributeUsage(AttributeTargets.Class, AllowMultiple = true)]
public class AuthorAttribute: Attribute
{
    private string name;

    public AuthorAttribute(string name) {
        this.name = name;
    }

    public string Name {
        get { return name; }
    }
}
```

Определяет класс атрибута многократного использования, с именем `AuthorAttribute`. Пример

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")] 
class Class1
{
    ...
}
```

показано объявление класса с два способа использования `Author` атрибута.

`AttributeUsage` имеет другой именованный параметр с именем `Inherited`, который указывает, наследуется ли также атрибут, заданный в базовом классе, классами, производными от этого базового класса. Если `Inherited` для атрибута класса имеет значение true, то этот атрибут является унаследованным. Если `Inherited` для атрибута класса имеет значение false, то этот атрибут не наследуется. Если не указано, значение по умолчанию — true.

Класс атрибута `X` отсутствие `AttributeUsage` атрибут, присоединенный к нему, как показано на

```csharp
using System;

class X: Attribute {...}
```

Эквивалентно следующему:

```csharp
using System;

[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```

### <a name="positional-and-named-parameters"></a>Позиционные и именованные параметры

Классы атрибутов могут иметь ***позиционные параметры*** и ***именованные параметры***. Каждый конструктор открытого экземпляра для класса атрибута определяет допустимую последовательность позиционных параметров для этого класса атрибута. Каждого нестатических открытое поле для чтения и записи и свойства для класса атрибута определяет именованный параметр для класса атрибута.

Пример

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpAttribute: Attribute
{
    public HelpAttribute(string url) {        // Positional parameter
        ...
    }

    public string Topic {                     // Named parameter
        get {...}
        set {...}
    }

    public string Url {
        get {...}
    }
}
```

Определяет класс атрибута с именем `HelpAttribute` с одним позиционным параметром, `url`и один именованный параметр `Topic`. Несмотря на то, что он является статическим и открытым, свойство `Url` не определяет именованный параметр, так как он не чтения и записи.

Этот класс атрибута можно использовать следующим образом:

```csharp
[Help("http://www.mycompany.com/.../Class1.htm")]
class Class1
{
    ...
}

[Help("http://www.mycompany.com/.../Misc.htm", Topic = "Class2")]
class Class2
{
    ...
}
```

### <a name="attribute-parameter-types"></a>Типы параметров атрибутов

Типы позиционных и именованных параметров для класса атрибута ограничены ***типы параметров атрибутов***, которые являются:

*  Один из следующих типов: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`, `sbyte`, `short`, `string`, `uint`, `ulong`, `ushort`.
*  Тип `object`.
*  Тип `System.Type`.
*  Перечисляемый тип, если он имеет общую доступность и типы, в которых он является вложенным (если таковые имеются) также иметь доступность уровня public ([спецификация атрибута](attributes.md#attribute-specification)).
*  Одномерные массивы указанных выше типов.
*  Аргумент конструктора или общее поле, которые не имеет ни одного из этих типов, не может использоваться как позиционные или именованные параметра в спецификации атрибута.

## <a name="attribute-specification"></a>Спецификация атрибута

***Спецификация атрибута*** — это применение предварительно определенного атрибута к объявлению. Атрибут — это часть дополнительные описательные данные, указанный для объявления. Атрибуты могут быть заданы в глобальной области видимости (для указания атрибутов на сборки или модуля, содержащего) и для *type_declaration*s ([объявления типов](namespaces.md#type-declarations)), *class_member_declaration* s ([ограничения параметров типа](classes.md#type-parameter-constraints)), *interface_member_declaration*s ([члены интерфейса](interfaces.md#interface-members)), *struct_member _declaration*s ([члены структуры](structs.md#struct-members)), *enum_member_declaration*s ([члены перечисления](enums.md#enum-members)), *accessor_declarations*  ([Методы доступа](classes.md#accessors)), *event_accessor_declarations* ([подобные полям события](classes.md#field-like-events)), и *formal_parameter_list*s ([параметры метода](classes.md#method-parameters)).

Атрибуты указаны в ***атрибут разделах***. Раздел "атрибут" состоит из пары квадратных скобок, которые окружают разделенный запятыми список из одного или нескольких атрибутов. Порядок, в котором указаны атрибуты в таком списке и расположены порядок, в котором разделы, подключенные к одной и той же сущности программы, не имеет значения. Например, спецификаций атрибутов `[A][B]`, `[B][A]`, `[A,B]`, и `[B,A]` эквивалентны.

```antlr
global_attributes
    : global_attribute_section+
    ;

global_attribute_section
    : '[' global_attribute_target_specifier attribute_list ']'
    | '[' global_attribute_target_specifier attribute_list ',' ']'
    ;

global_attribute_target_specifier
    : global_attribute_target ':'
    ;

global_attribute_target
    : 'assembly'
    | 'module'
    ;

attributes
    : attribute_section+
    ;

attribute_section
    : '[' attribute_target_specifier? attribute_list ']'
    | '[' attribute_target_specifier? attribute_list ',' ']'
    ;

attribute_target_specifier
    : attribute_target ':'
    ;

attribute_target
    : 'field'
    | 'event'
    | 'method'
    | 'param'
    | 'property'
    | 'return'
    | 'type'
    ;

attribute_list
    : attribute (',' attribute)*
    ;

attribute
    : attribute_name attribute_arguments?
    ;

attribute_name
    : type_name
    ;

attribute_arguments
    : '(' positional_argument_list? ')'
    | '(' positional_argument_list ',' named_argument_list ')'
    | '(' named_argument_list ')'
    ;

positional_argument_list
    : positional_argument (',' positional_argument)*
    ;

positional_argument
    : attribute_argument_expression
    ;

named_argument_list
    : named_argument (','  named_argument)*
    ;

named_argument
    : identifier '=' attribute_argument_expression
    ;

attribute_argument_expression
    : expression
    ;
```

Атрибут состоит из *attribute_name* и необязательный список позиционных и именованных аргументов. Позиционные аргументы (если таковые имеются) предшествовать именованные аргументы. Позиционный аргумент состоит из *attribute_argument_expression*; именованный аргумент состоит из имени, а после знака равенства, за которым следует *attribute_argument_expression*, который, вместе , ограничены по тем же правилам, как простое присваивание. Порядок именованных аргументов не имеет значения.

*Attribute_name* идентифицирует класс атрибута. Если виде *attribute_name* — *type_name* затем это имя должно ссылаться на класс атрибута. В противном случае возникает ошибка времени компиляции. Пример

```csharp
class Class1 {}

[Class1] class Class2 {}    // Error
```

приводит к ошибке времени компиляции, так как он пытается использовать `Class1` как атрибут класса, если `Class1` не является классом атрибута.

Определенные контексты разрешают спецификацию атрибута на нескольких целевых объектов. Программы можно явно указать целевой объект, включив *attribute_target_specifier*. Когда атрибут помещается на глобальном уровне, *global_attribute_target_specifier* является обязательным. В других местах, применяется разумного значения по умолчанию, но *attribute_target_specifier* можно использовать для подтверждения или переопределить значение по умолчанию в определенных случаях неоднозначности (или просто для подтверждения по умолчанию в случаях неоднозначные). Таким образом, как правило, *attribute_target_specifier*s может опускаться только на глобальном уровне. Потенциально неоднозначной контексты разрешаются следующим образом:

*  Атрибут, заданный в глобальной области можно применить к целевой сборке или целевому модулю. По умолчанию существует для данного контекста, поэтому *attribute_target_specifier* всегда необходим в данном контексте. Наличие `assembly` *attribute_target_specifier* указывает, что атрибут применяется к целевому объекту сборки; наличие `module` *attribute_target_specifier* Указывает, что атрибут применяется к целевому модулю.
*  Атрибут, заданный в объявлении делегата можно применять к делегату объявляемого или возвращаемому значению. В случае отсутствия *attribute_target_specifier*, атрибут применяется к делегату. Наличие `type` *attribute_target_specifier* указывает, что атрибут применяется к делегату; наличие `return` *attribute_target_specifier* Указывает, что атрибут применяется к возвращаемому значению.
*  Атрибут, заданный в объявлении метода можно применить для объявляемого метода или возвращаемому значению. В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу. Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `return` *attribute_target_specifier* указывает что атрибут применяется к возвращаемому значению.
*  Атрибут, заданный в объявлении оператора можно применить к оператору или возвращаемому значению. В случае отсутствия *attribute_target_specifier*, атрибут применяется к оператору. Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `return` *attribute_target_specifier* Указывает, что атрибут применяется к возвращаемому значению.
*  Атрибут, заданный в объявлении события, который опускает доступа к событиям можно применять к событию, связанному полю (если событие не является абстрактным) или связанные добавить и удалить методы. В случае отсутствия *attribute_target_specifier*, атрибут применяется к событию. Наличие `event` *attribute_target_specifier* указывает, что атрибут применяется к событию; наличие `field` *attribute_target_specifier* указывает что атрибут применяется к полю; и наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методам.
*  Атрибут, заданный в объявлении метода доступа get для объявления свойства или индексатора можно применить для связанного метода или возвращаемому значению. В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу. Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `return` *attribute_target_specifier* указывает что атрибут применяется к возвращаемому значению.
*  Атрибут, заданный в метод доступа set для объявления свойства или индексатора можно применить к связанному методу или к его одиночному неявное параметру. В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу. Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `param` *attribute_target_specifier* указывает что атрибут применяется к параметру; наличие `return` *attribute_target_specifier* указывает, что атрибут применяется к возвращаемому значению.
*  Атрибут, заданный в объявлении метода доступа add или remove, для объявления события можно применить к связанному методу или к его одиночному параметру. В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу. Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `param` *attribute_target_specifier* указывает что атрибут применяется к параметру; наличие `return` *attribute_target_specifier* указывает, что атрибут применяется к возвращаемому значению.

В других контекстах, включение *attribute_target_specifier* разрешено, но ненужные. Например, объявление класса включается или опустить описатель `type`:

```csharp
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

Это ошибка для указано недопустимое *attribute_target_specifier*. Например, описатель `param` не может использоваться в объявлении класса:

```csharp
[param: Author("Brian Kernighan")]        // Error
class Class1 {}
```

По соглашению классы атрибутов именуются с суффиксом `Attribute`. *Attribute_name* формы *type_name* может включить или пропустить этот суффикс. Если класс атрибута находится в том случае, как с и без этого суффикса, присутствует неоднозначность и приводит к ошибке времени компиляции. Если *attribute_name* написано таким образом, чтобы его крайнее правое *идентификатор* является буквальным идентификатором ([идентификаторы](lexical-structure.md#identifiers)), а затем сопоставляется только атрибут без суффикса, Таким образом, включение таких разрешить неоднозначность. Пример

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
public class X: Attribute
{}

[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}

[X]                     // Error: ambiguity
class Class1 {}

[XAttribute]            // Refers to XAttribute
class Class2 {}

[@X]                    // Refers to X
class Class3 {}

[@XAttribute]           // Refers to XAttribute
class Class4 {}
```

Показывает, два атрибута с именем классы `X` и `XAttribute`. Атрибут `[X]` является неоднозначным, так как она может ссылаться на либо `X` или `XAttribute`. С помощью буквальным идентификатором точного указания в таких редких случаях намерения. Атрибут `[XAttribute]` не является неоднозначным (несмотря на то, что было бы Если класс атрибута с именем `XAttributeAttribute`!). Если объявление класса `X` удаляется, а затем оба атрибута ссылаются на класс атрибута с именем `XAttribute`, как показано ниже:

```csharp
using System;

[AttributeUsage(AttributeTargets.All)]
public class XAttribute: Attribute
{}

[X]                     // Refers to XAttribute
class Class1 {}

[XAttribute]            // Refers to XAttribute
class Class2 {}

[@X]                    // Error: no attribute named "X"
class Class3 {}
```

Это ошибка времени компиляции для использования класса атрибутом однократного использования более одного раза на той же сущности. Пример

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class HelpStringAttribute: Attribute
{
    string value;

    public HelpStringAttribute(string value) {
        this.value = value;
    }

    public string Value {
        get {...}
    }
}

[HelpString("Description of Class1")]
[HelpString("Another description of Class1")]
public class Class1 {}
```

приводит к ошибке времени компиляции, так как он пытается использовать `HelpString`, — это класс атрибутом однократного использования, более одного раза в объявлении `Class1`.

Выражение `E` — *attribute_argument_expression* если выполняются все следующие инструкции:

*  Тип `E` является типом параметра атрибута ([типы параметров атрибутов](attributes.md#attribute-parameter-types)).
*  Во время компиляции, значение `E` можно разрешить в одно из следующих:
   * Значение константы.
   * Объект `System.Type`.
   * Одномерный массив *attribute_argument_expression*s.

Пример:

```csharp
using System;

[AttributeUsage(AttributeTargets.Class)]
public class TestAttribute: Attribute
{
    public int P1 {
        get {...}
        set {...}
    }

    public Type P2 {
        get {...}
        set {...}
    }

    public object P3 {
        get {...}
        set {...}
    }
}

[Test(P1 = 1234, P3 = new int[] {1, 3, 5}, P2 = typeof(float))]
class MyClass {}
```

Объект *typeof_expression* ([оператор typeof](expressions.md#the-typeof-operator)) используется как выражения аргумента атрибута можно ссылаться неуниверсального типа, закрытым сконструированным типом или несвязанного универсального типа, но не может ссылаться на открытый тип. Это гарантирует, что выражение может разрешаться во время компиляции.

```csharp
class A: Attribute
{
    public A(Type t) {...}
}

class G<T>
{
    [A(typeof(T))] T t;                  // Error, open type in attribute
}

class X
{
    [A(typeof(List<int>))] int x;        // Ok, closed constructed type
    [A(typeof(List<>))] int y;           // Ok, unbound generic type
}
```

## <a name="attribute-instances"></a>Экземпляры атрибута

***Экземпляра атрибута*** — это экземпляр, который представляет атрибут во время выполнения. Атрибут определяется с помощью класса атрибута, позиционных аргументов и именованные аргументы. Экземпляр атрибута — это экземпляр класса атрибута, который инициализируется с помощью позиционных и именованных аргументов.

Извлечение экземпляра атрибута включает в себя во время компиляции и выполнения обработки, как описано в следующих разделах.

### <a name="compilation-of-an-attribute"></a>Компиляция атрибута

Компиляция *атрибут* с классом атрибута `T`, *positional_argument_list* `P` и *named_argument_list* `N`, состоит из следующих действий:

*  Выполните шаги обработки компиляции для компиляции *object_creation_expression* формы `new T(P)`. Эти действия к ошибке времени компиляции или определить конструктор экземпляра `C` на `T` может вызываться во время выполнения.
*  Если `C` имеет открытый доступ, то возникает ошибка времени компиляции.
*  Для каждого *именованный_аргумент* `Arg` в `N`:
   * Позвольте `Name` быть *идентификатор* из *именованный_аргумент* `Arg`.
   * `Name` необходимо определить нестатические чтения и записи открытое поле или свойство на `T`. Если `T` имеет нет такого поля или свойства, то возникает ошибка времени компиляции.
*  Примите указанные ниже сведения для создания экземпляра атрибута во время выполнения: класс атрибута `T`, конструкторе экземпляра `C` на `T`, *positional_argument_list* `P` и *named_argument_list* `N`.

### <a name="run-time-retrieval-of-an-attribute-instance"></a>Во время выполнения извлечения экземпляра атрибута

Подборка *атрибут* дает класс атрибута `T`, конструкторе экземпляра `C` на `T`, *positional_argument_list* `P`и *named_argument_list* `N`. Учитывая эти сведения, экземпляр атрибута можно получить во время выполнения, выполнив следующие действия:

*  Выполните шаги обработки времени выполнения для выполнения *object_creation_expression* формы `new T(P)`, используя конструктор экземпляра `C` определяется во время компиляции. Следующие действия приводят к исключению, или создавать экземпляр `O` из `T`.
*  Для каждого *именованный_аргумент* `Arg` в `N`, в порядке:
   * Позвольте `Name` быть *идентификатор* из *именованный_аргумент* `Arg`. Если `Name` не определяет нестатических открытое поле для чтения и записи или свойства на `O`, то возникает исключение.
   * Позвольте `Value` быть результатом вычисления *attribute_argument_expression* из `Arg`.
   * Если `Name` определяет поле на `O`, затем выберите значение `Value`.
   * В противном случае `Name` определяет свойство на `O`. Присвойте этому свойству значение `Value`.
   * В результате `O`, экземпляр класса атрибута `T` , инициализирована с помощью *positional_argument_list* `P` и *named_argument_list* `N`.

## <a name="reserved-attributes"></a>Зарезервированные атрибуты

Небольшое количество атрибутов влияет на язык каким-либо образом. Эти атрибуты включают:

*  `System.AttributeUsageAttribute` ([Атрибут AttributeUsage](attributes.md#the-attributeusage-attribute)), который используется для описания способов, в котором можно использовать класс атрибута.
*  `System.Diagnostics.ConditionalAttribute` ([Атрибут Conditional](attributes.md#the-conditional-attribute)), который используется для определения условные методы.
*  `System.ObsoleteAttribute` ([Атрибут Obsolete](attributes.md#the-obsolete-attribute)), который используется для пометки элемента как устаревший.
*  `System.Runtime.CompilerServices.CallerLineNumberAttribute`, `System.Runtime.CompilerServices.CallerFilePathAttribute` и `System.Runtime.CompilerServices.CallerMemberNameAttribute` ([информационные атрибуты вызывающего объекта](attributes.md#caller-info-attributes)), которые используются для предоставления сведений о контексте вызова к необязательным параметрам.

### <a name="the-attributeusage-attribute"></a>Атрибут AttributeUsage

Атрибут `AttributeUsage` используется для описания способа, в котором можно использовать класс атрибута.

Класс, отмеченный атрибутом `AttributeUsage` атрибут должен быть производным от `System.Attribute`, прямо или косвенно. В противном случае возникает ошибка времени компиляции.

```csharp
namespace System
{
    [AttributeUsage(AttributeTargets.Class)]
    public class AttributeUsageAttribute: Attribute
    {
        public AttributeUsageAttribute(AttributeTargets validOn) {...}
        public virtual bool AllowMultiple { get {...} set {...} }
        public virtual bool Inherited { get {...} set {...} }
        public virtual AttributeTargets ValidOn { get {...} }
    }

    public enum AttributeTargets
    {
        Assembly     = 0x0001,
        Module       = 0x0002,
        Class        = 0x0004,
        Struct       = 0x0008,
        Enum         = 0x0010,
        Constructor  = 0x0020,
        Method       = 0x0040,
        Property     = 0x0080,
        Field        = 0x0100,
        Event        = 0x0200,
        Interface    = 0x0400,
        Parameter    = 0x0800,
        Delegate     = 0x1000,
        ReturnValue  = 0x2000,

        All = Assembly | Module | Class | Struct | Enum | Constructor | 
            Method | Property | Field | Event | Interface | Parameter | 
            Delegate | ReturnValue
    }
}
```

### <a name="the-conditional-attribute"></a>Атрибут Conditional

Атрибут `Conditional` позволяет определять ***условные методы*** и ***классы атрибут conditional***.

```csharp
namespace System.Diagnostics
{
    [AttributeUsage(AttributeTargets.Method | AttributeTargets.Class, AllowMultiple = true)]
    public class ConditionalAttribute: Attribute
    {
        public ConditionalAttribute(string conditionString) {...}
        public string ConditionString { get {...} }
    }
}
```

#### <a name="conditional-methods"></a>Условные методы.

Метод с атрибутом `Conditional` атрибут является условный метод. `Conditional` Атрибут указывает условие, тестируя символ условной компиляции. Вызовы условного метода либо включены, либо пропущено в зависимости от того, определен ли этот символ в точке вызова. Если этот символ определен, вызов включается; в противном случае вызов (включая оценки приемника и параметры вызова) опускается.

Условный метод имеет следующие ограничения:

*  Условный метод должен быть методом в *class_declaration* или *struct_declaration*. Ошибка времени компиляции возникает, если `Conditional` атрибут указан для метода в объявлении интерфейса.
*  Условный метод должен иметь тип возвращаемого значения `void`.
*  Условный метод не должен быть помечен с помощью `override` модификатор. Условный метод помечен `virtual` модификатор, тем не менее. Переопределения такого метода неявно условного и не должен быть помечен явно с `Conditional` атрибута.
*  Условный метод не должен быть реализацию метода интерфейса. В противном случае возникает ошибка времени компиляции.

Кроме того, возникает ошибка времени компиляции, если условный метод используется в *delegate_creation_expression*. Пример

```csharp
#define DEBUG

using System;
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public static void M() {
        Console.WriteLine("Executed Class1.M");
    }
}

class Class2
{
    public static void Test() {
        Class1.M();
    }
}
```

объявляет `Class1.M` как условный метод. `Class2`в `Test` метод вызывает этот метод. Так как символ условной компиляции `DEBUG` определено, если `Class2.Test` является именем, он вызывает `M`. Если символ `DEBUG` бы не был определен, затем `Class2.Test` вызовет не `Class1.M`.

Важно отметить, что включение или исключение вызова условного метода управляется символами условной компиляции в точке вызова. В примере

Файл `class1.cs`:

```csharp
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public static void F() {
        Console.WriteLine("Executed Class1.F");
    }
}
```

Файл `class2.cs`:

```csharp
#define DEBUG

class Class2
{
    public static void G() {
        Class1.F();                // F is called
    }
}
```

Файл `class3.cs`:

```csharp
#undef DEBUG

class Class3
{
    public static void H() {
        Class1.F();                // F is not called
    }
}
```

классы `Class2` и `Class3` каждая содержит вызовы условного метода `Class1.F`, который условного основан на ли `DEBUG` определен. Так как этот символ определен в контексте `Class2` , но не `Class3`, вызов `F` в `Class2` включено, а вызов `F` в `Class3` опускается.

Использование условного методов в цепочке наследования могут быть запутанными. Вызовы условного метода через `base`, формы `base.M`, подчиняются правилам обычный метод условного вызова. В примере

Файл `class1.cs`:

```csharp
using System;
using System.Diagnostics;

class Class1 
{
    [Conditional("DEBUG")]
    public virtual void M() {
        Console.WriteLine("Class1.M executed");
    }
}
```

Файл `class2.cs`:

```csharp
using System;

class Class2: Class1
{
    public override void M() {
        Console.WriteLine("Class2.M executed");
        base.M();                        // base.M is not called!
    }
}
```

Файл `class3.cs`:

```csharp
#define DEBUG

using System;

class Class3
{
    public static void Test() {
        Class2 c = new Class2();
        c.M();                            // M is called
    }
}
```

`Class2` включает вызов `M` определенные в базовом классе. Этот вызов опускается, так как базовый метод условного на основе наличия символа `DEBUG`, который не определен. Таким образом, метод выводит на консоль "`Class2.M executed`" только. Разумно использовать *pp_declaration*s может устранить такие проблемы.

#### <a name="conditional-attribute-classes"></a>Атрибут Conditional классы

Класс атрибута ([классы атрибутов](attributes.md#attribute-classes)) декорированные с одним или несколькими `Conditional` атрибутов ***класса атрибут conditional***. Класс атрибут conditional, таким образом, связанные с символы условной компиляции, объявленных в его `Conditional` атрибуты. Этот пример.

```csharp
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

объявляет `TestAttribute` как атрибут conditional класс, связанный с символами условной компиляции `ALPHA` и `BETA`.

Спецификации атрибута ([спецификация атрибута](attributes.md#attribute-specification)) условного атрибута включаются, если один или несколько символов связанные условной компиляции определен точке спецификации, в противном случае атрибут Спецификация опускается.

Это важно отметить, что включение или исключение спецификации атрибута класса атрибут conditional управляется символы условной компиляции точке спецификации. В примере

Файл `test.cs`:

```csharp
using System;
using System.Diagnostics;

[Conditional("DEBUG")]

public class TestAttribute : Attribute {}
```

Файл `class1.cs`:

```csharp
#define DEBUG

[Test]                // TestAttribute is specified

class Class1 {}
```

Файл `class2.cs`:

```csharp
#undef DEBUG

[Test]                 // TestAttribute is not specified

class Class2 {}
```

классы `Class1` и `Class2` являются каждого дополнен атрибутом `Test`, которой условного зависит от того, нужно ли `DEBUG` определен. Так как этот символ определен в контексте `Class1` , но не `Class2`, спецификация `Test` атрибут `Class1` включаются при спецификации `Test` атрибут `Class2` опускается.

### <a name="the-obsolete-attribute"></a>Атрибут Obsolete

Атрибут `Obsolete` используется для пометки типы и члены типов, которые больше не должны использоваться.

```csharp
namespace System
{
    [AttributeUsage(
        AttributeTargets.Class | 
        AttributeTargets.Struct |
        AttributeTargets.Enum | 
        AttributeTargets.Interface | 
        AttributeTargets.Delegate |
        AttributeTargets.Method | 
        AttributeTargets.Constructor |
        AttributeTargets.Property | 
        AttributeTargets.Field |
        AttributeTargets.Event,
        Inherited = false)
    ]
    public class ObsoleteAttribute: Attribute
    {
        public ObsoleteAttribute() {...}
        public ObsoleteAttribute(string message) {...}
        public ObsoleteAttribute(string message, bool error) {...}
        public string Message { get {...} }
        public bool IsError { get {...} }
    }
}
```

Если программа использует тип или член, отмеченный атрибутом `Obsolete` атрибут, компилятор выдает предупреждение или ошибку. В частности, компилятор выдает предупреждение, если указан параметр не ошибка, или если параметр ошибки и имеет значение `false`. Компилятор выдает ошибку, если указан параметр ошибки и имеет значение `true`.

В примере

```csharp
[Obsolete("This class is obsolete; use class B instead")]
class A
{
    public void F() {}
}

class B
{
    public void F() {}
}

class Test
{
    static void Main() {
        A a = new A();         // Warning
        a.F();
    }
}
```

Класс `A` снабжен `Obsolete` атрибута. Каждое использование `A` в `Main` результаты предупреждение с указанным сообщением «этот класс является устаревшим. Используйте класс B.»

### <a name="caller-info-attributes"></a>Информационные атрибуты вызывающего объекта

Для целей, например для ведения журналов и отчетности иногда полезно для функции-члена для получения определенных сведений во время компиляции об вызывающий код. Информационные атрибуты вызывающего объекта предоставить способ передачи таких сведений прозрачно.

Если необязательный параметр помечается с помощью одного из информационные атрибуты вызывающего объекта, пропуск соответствующего аргумента в вызове необязательно вызывают значение параметра по умолчанию должен быть замещен. Вместо этого Если доступен указанный сведения о вызывающем контексте, эти сведения будут переданы как значение аргумента.

Пример:

```csharp
using System.Runtime.CompilerServices

...

public void Log(
    [CallerLineNumber] int line = -1,
    [CallerFilePath]   string path = null,
    [CallerMemberName] string name = null
)
{
    Console.WriteLine((line < 0) ? "No line" : "Line "+ line);
    Console.WriteLine((path == null) ? "No file path" : path);
    Console.WriteLine((name == null) ? "No member name" : name);
}
```

Вызов `Log()` без аргументов выводит строки и номер путь вызова, а также имя члена, в котором произошел вызов.

Информационные атрибуты вызывающего объекта может произойти в любой точке мира, необязательные параметры, включая в объявлениях делегатов. Тем не менее атрибуты сведений о конкретной вызывающей стороны имеют ограничения на типы параметров, которые они могут атрибута, таким образом, чтобы всегда будет существовать неявное преобразование из подставляемого значения к типу параметра.

Это ошибкой в том же информационный атрибут вызывающего объекта для параметра, как определить и реализовать часть объявления разделяемого метода. Применяются только информационные атрибуты вызывающего объекта в определение части, в то время как происходит только в реализации части информационные атрибуты вызывающего объекта учитываются.

Сведения о вызывающем объекте не влияет на разрешение перегрузки. Как по-прежнему с атрибутами возможно использование необязательных параметров опускаются из исходного кода, вызывающего объекта, разрешение перегрузки игнорирует эти параметры таким же образом, он игнорирует другие пропущенный необязательные параметры ([разрешение перегрузки](expressions.md#overload-resolution)).

Сведения о вызывающем объекте подставляется только в том случае, когда функция вызывается явным образом в исходном коде. Неявные вызовы, например неявные родительский конструктор вызывает нет исходного расположения и не производит подстановку сведения о вызывающем объекте. Кроме того вызовы, динамическая привязка не заменит сведения о вызывающем объекте. Если вызывающий объект info, атрибутами параметр опускается в таких случаях, будет использовано указанное значение по умолчанию значение параметра.

Единственное исключение — выражения запроса. Они считаются синтаксические расширения, и если вызовы расширены, чтобы пропустить необязательные параметры с информационные атрибуты вызывающего объекта, будут заменены сведения о вызывающем объекте. Место, используемое находится предложение запроса, что вызов был создан из.

Если указано более одного Информационный атрибут вызывающего объекта на данном параметре, они являются предпочтительными в следующем порядке: `CallerLineNumber`, `CallerFilePath`, `CallerMemberName`.

#### <a name="the-callerlinenumber-attribute"></a>Атрибут CallerLineNumber

`System.Runtime.CompilerServices.CallerLineNumberAttribute` Разрешена для необязательных параметров, при отсутствии стандартного неявные преобразования ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) из значения константы `int.MaxValue` к типу параметра. Это гарантирует, что любое строки неотрицательное число вплоть до это значение можно передать без ошибок.

Если вызов функции из расположения в исходном коде опускает необязательный параметр со `CallerLineNumberAttribute`, а затем числовой литерал, представляющий номер строки в это расположение используется в качестве аргумента вызова вместо значения параметра по умолчанию.

Если вызов занимает несколько строк, выбранной строки зависит от реализации.

Обратите внимание, что номер строки могут быть затронуты `#line` директивы ([строки директивы](lexical-structure.md#line-directives)).

#### <a name="the-callerfilepath-attribute"></a>Атрибут CallerFilePath

`System.Runtime.CompilerServices.CallerFilePathAttribute` Разрешена для необязательных параметров, при отсутствии стандартного неявные преобразования ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) из `string` к типу параметра.

Если вызов функции из расположения в исходном коде опускает необязательный параметр со `CallerFilePathAttribute`, а затем в строковый литерал, представляющий путь к файлу это расположение используется в качестве аргумента вызова вместо значения параметра по умолчанию.

Формат пути к файлу зависит от реализации.

Обратите внимание, что путь к файлу может затронуть `#line` директивы ([строки директивы](lexical-structure.md#line-directives)).

#### <a name="the-callermembername-attribute"></a>Атрибут CallerMemberName

`System.Runtime.CompilerServices.CallerMemberNameAttribute` Разрешена для необязательных параметров, при отсутствии стандартного неявные преобразования ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) из `string` к типу параметра.

Если вызов функции из расположения в теле функции-члена или в атрибут применен к функции-члена, самого или его тип возвращаемого значения, параметров или параметров типа в исходный код опускает необязательный параметр со `CallerMemberNameAttribute`, а затем строковый литерал, представляющий имя этого элемента используется в качестве аргумента вызова вместо значения параметра по умолчанию.

Для вызовов, происходящих в универсальных методах только само имя метода используется без списка параметров типа.

Для вызовов, которые происходят в явные реализации члена интерфейса только само имя метода используется без предыдущем квалификацию интерфейса.

Для вызовов, возникающих в рамках методов доступа свойства или события используется имя члена, свойства или само событие.

Для вызовов, возникающих в рамках методам доступа индексаторов, используется имя члена, предоставляемые `IndexerNameAttribute` ([атрибут IndexerName](attributes.md#the-indexername-attribute)) на элемент индексатора, если он имеется, или имя по умолчанию `Item` в противном случае.

Для вызовов, которые происходят в конструкторы экземпляров, статические конструкторы, деструкторы и операторы объявления члена имя, используемое зависит от реализации.

## <a name="attributes-for-interoperation"></a>Атрибуты для взаимодействия

Примечание. Этот раздел применим только к реализации Microsoft .NET C#.

### <a name="interoperation-with-com-and-win32-components"></a>Взаимодействие с компонентами COM и Win32

Время выполнения .NET предоставляет большое количество атрибутов, которые позволяют программы на C# для взаимодействия с компонентами, написанными на COM и библиотеки DLL Win32. Например `DllImport` атрибут может быть использован для `static extern` методу, чтобы показать, что метод реализуется в библиотеки DLL Win32. Эти атрибуты найдены в `System.Runtime.InteropServices` пространства имен и подробную документацию для этих атрибутов см. в документации среды выполнения .NET.

### <a name="interoperation-with-other-net-languages"></a>Взаимодействие с другими языками .NET

#### <a name="the-indexername-attribute"></a>Атрибут IndexerName

Индексаторы реализованы в .NET с помощью индексированных свойств и иметь имя в метаданных .NET. Если не `IndexerName` присутствует атрибут для индексатора, а затем имя `Item` используется по умолчанию. `IndexerName` Атрибут которой разработчики могут переопределить это поведение по умолчанию и указать другое имя.

```csharp
namespace System.Runtime.CompilerServices.CSharp
{
    [AttributeUsage(AttributeTargets.Property)]
    public class IndexerNameAttribute: Attribute
    {
        public IndexerNameAttribute(string indexerName) {...}
        public string Value { get {...} } 
    }
}
```
