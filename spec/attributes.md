# <a name="attributes"></a><span data-ttu-id="280fe-101">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="280fe-101">Attributes</span></span>

<span data-ttu-id="280fe-102">Большая часть языка C# позволяет программисту указывать декларативные сведения о сущностях, определенных в программе.</span><span class="sxs-lookup"><span data-stu-id="280fe-102">Much of the C# language enables the programmer to specify declarative information about the entities defined in the program.</span></span> <span data-ttu-id="280fe-103">Например, доступность метода в классе определяется дополнив его с *method_modifier*s `public`, `protected`, `internal`, и `private`.</span><span class="sxs-lookup"><span data-stu-id="280fe-103">For example, the accessibility of a method in a class is specified by decorating it with the *method_modifier*s `public`, `protected`, `internal`, and `private`.</span></span>

<span data-ttu-id="280fe-104">C# позволяет программистам создавать новые типы декларативных сведений, называемых ***атрибуты***.</span><span class="sxs-lookup"><span data-stu-id="280fe-104">C# enables programmers to invent new kinds of declarative information, called ***attributes***.</span></span> <span data-ttu-id="280fe-105">Программисты могут присоединения атрибутов для различных сущностей программы и получить сведения об атрибутах в среде выполнения.</span><span class="sxs-lookup"><span data-stu-id="280fe-105">Programmers can then attach attributes to various program entities, and retrieve attribute information in a run-time environment.</span></span> <span data-ttu-id="280fe-106">Например, структура может определить `HelpAttribute` атрибут, который можно поместить на определенные элементы программы (например, классы и методы) для предоставления сопоставление этих элементов программы на документацию.</span><span class="sxs-lookup"><span data-stu-id="280fe-106">For instance, a framework might define a `HelpAttribute` attribute that can be placed on certain program elements (such as classes and methods) to provide a mapping from those program elements to their documentation.</span></span>

<span data-ttu-id="280fe-107">Атрибуты определяются путем объявления классов атрибутов ([классы атрибутов](attributes.md#attribute-classes)), которые могут иметь позиционные и именованные параметры ([Positional и именованные параметры](attributes.md#positional-and-named-parameters)).</span><span class="sxs-lookup"><span data-stu-id="280fe-107">Attributes are defined through the declaration of attribute classes ([Attribute classes](attributes.md#attribute-classes)), which may have positional and named parameters ([Positional and named parameters](attributes.md#positional-and-named-parameters)).</span></span> <span data-ttu-id="280fe-108">Атрибуты присоединяются к сущности в программе C# с помощью спецификаций атрибутов ([спецификация атрибута](attributes.md#attribute-specification)) и могут быть получены во время выполнения как экземпляры атрибута ([экземпляры атрибута](attributes.md#attribute-instances)).</span><span class="sxs-lookup"><span data-stu-id="280fe-108">Attributes are attached to entities in a C# program using attribute specifications ([Attribute specification](attributes.md#attribute-specification)), and can be retrieved at run-time as attribute instances ([Attribute instances](attributes.md#attribute-instances)).</span></span>

## <a name="attribute-classes"></a><span data-ttu-id="280fe-109">Классы атрибутов</span><span class="sxs-lookup"><span data-stu-id="280fe-109">Attribute classes</span></span>

<span data-ttu-id="280fe-110">Класс, производный от абстрактного класса `System.Attribute`, прямо или косвенно, является ***класс атрибута***.</span><span class="sxs-lookup"><span data-stu-id="280fe-110">A class that derives from the abstract class `System.Attribute`, whether directly or indirectly, is an ***attribute class***.</span></span> <span data-ttu-id="280fe-111">Объявление класса атрибута определяет новый вид ***атрибут*** , можно поместить в объявлении.</span><span class="sxs-lookup"><span data-stu-id="280fe-111">The declaration of an attribute class defines a new kind of ***attribute*** that can be placed on a declaration.</span></span> <span data-ttu-id="280fe-112">По соглашению классы атрибутов именуются с суффиксом `Attribute`.</span><span class="sxs-lookup"><span data-stu-id="280fe-112">By convention, attribute classes are named with a suffix of `Attribute`.</span></span> <span data-ttu-id="280fe-113">Использовании атрибута может включить или пропустить этот суффикс.</span><span class="sxs-lookup"><span data-stu-id="280fe-113">Uses of an attribute may either include or omit this suffix.</span></span>

### <a name="attribute-usage"></a><span data-ttu-id="280fe-114">Использование атрибута</span><span class="sxs-lookup"><span data-stu-id="280fe-114">Attribute usage</span></span>

<span data-ttu-id="280fe-115">Атрибут `AttributeUsage` ([атрибут AttributeUsage](attributes.md#the-attributeusage-attribute)) используется для описания того, как можно использовать класс атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-115">The attribute `AttributeUsage` ([The AttributeUsage attribute](attributes.md#the-attributeusage-attribute)) is used to describe how an attribute class can be used.</span></span>

<span data-ttu-id="280fe-116">`AttributeUsage` имеет позиционный параметр ([Positional и именованные параметры](attributes.md#positional-and-named-parameters)), позволяющий класс атрибута указывать типы объявлений, на которых он может использоваться.</span><span class="sxs-lookup"><span data-stu-id="280fe-116">`AttributeUsage` has a positional parameter ([Positional and named parameters](attributes.md#positional-and-named-parameters)) that enables an attribute class to specify the kinds of declarations on which it can be used.</span></span> <span data-ttu-id="280fe-117">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-117">The example</span></span>

```csharp
using System;

[AttributeUsage(AttributeTargets.Class | AttributeTargets.Interface)]
public class SimpleAttribute: Attribute 
{
    ...
}
```

<span data-ttu-id="280fe-118">Определяет класс атрибута с именем `SimpleAttribute` , можно поместить в *class_declaration*s и *interface_declaration*только s.</span><span class="sxs-lookup"><span data-stu-id="280fe-118">defines an attribute class named `SimpleAttribute` that can be placed on *class_declaration*s and *interface_declaration*s only.</span></span> <span data-ttu-id="280fe-119">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-119">The example</span></span>

```csharp
[Simple] class Class1 {...}

[Simple] interface Interface1 {...}
```

<span data-ttu-id="280fe-120">показаны несколько способов применения `Simple` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-120">shows several uses of the `Simple` attribute.</span></span> <span data-ttu-id="280fe-121">Несмотря на то, что этот атрибут определен с именем `SimpleAttribute`, если этот атрибут используется, `Attribute` суффикс можно опускать, приводит к короткое имя `Simple`.</span><span class="sxs-lookup"><span data-stu-id="280fe-121">Although this attribute is defined with the name `SimpleAttribute`, when this attribute is used, the `Attribute` suffix may be omitted, resulting in the short name `Simple`.</span></span> <span data-ttu-id="280fe-122">Таким образом приведенный выше пример взят семантически эквивалентно следующему:</span><span class="sxs-lookup"><span data-stu-id="280fe-122">Thus, the example above is semantically equivalent to the following:</span></span>

```csharp
[SimpleAttribute] class Class1 {...}

[SimpleAttribute] interface Interface1 {...}
```

<span data-ttu-id="280fe-123">`AttributeUsage` имеет именованный параметр ([Positional и именованные параметры](attributes.md#positional-and-named-parameters)) вызывается `AllowMultiple`, которое указывает, является ли атрибут может быть указан более одного раза для данной сущности.</span><span class="sxs-lookup"><span data-stu-id="280fe-123">`AttributeUsage` has a named parameter ([Positional and named parameters](attributes.md#positional-and-named-parameters)) called `AllowMultiple`, which indicates whether the attribute can be specified more than once for a given entity.</span></span> <span data-ttu-id="280fe-124">Если `AllowMultiple` для атрибута класса имеет значение true, то классу этого атрибута является ***класс атрибута многократного использования***и может быть указан более одного раза в сущности.</span><span class="sxs-lookup"><span data-stu-id="280fe-124">If `AllowMultiple` for an attribute class is true, then that attribute class is a ***multi-use attribute class***, and can be specified more than once on an entity.</span></span> <span data-ttu-id="280fe-125">Если `AllowMultiple` для атрибута класса имеет значение false или не указано, то классу этого атрибута является ***однократного использования класса атрибута***его можно указать не более одного раза в сущности.</span><span class="sxs-lookup"><span data-stu-id="280fe-125">If `AllowMultiple` for an attribute class is false or it is unspecified, then that attribute class is a ***single-use attribute class***, and can be specified at most once on an entity.</span></span>

<span data-ttu-id="280fe-126">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-126">The example</span></span>

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

<span data-ttu-id="280fe-127">Определяет класс атрибута многократного использования, с именем `AuthorAttribute`.</span><span class="sxs-lookup"><span data-stu-id="280fe-127">defines a multi-use attribute class named `AuthorAttribute`.</span></span> <span data-ttu-id="280fe-128">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-128">The example</span></span>

```csharp
[Author("Brian Kernighan"), Author("Dennis Ritchie")] 
class Class1
{
    ...
}
```

<span data-ttu-id="280fe-129">показано объявление класса с два способа использования `Author` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-129">shows a class declaration with two uses of the `Author` attribute.</span></span>

<span data-ttu-id="280fe-130">`AttributeUsage` имеет другой именованный параметр с именем `Inherited`, который указывает, наследуется ли также атрибут, заданный в базовом классе, классами, производными от этого базового класса.</span><span class="sxs-lookup"><span data-stu-id="280fe-130">`AttributeUsage` has another named parameter called `Inherited`, which indicates whether the attribute, when specified on a base class, is also inherited by classes that derive from that base class.</span></span> <span data-ttu-id="280fe-131">Если `Inherited` для атрибута класса имеет значение true, то этот атрибут является унаследованным.</span><span class="sxs-lookup"><span data-stu-id="280fe-131">If `Inherited` for an attribute class is true, then that attribute is inherited.</span></span> <span data-ttu-id="280fe-132">Если `Inherited` для атрибута класса имеет значение false, то этот атрибут не наследуется.</span><span class="sxs-lookup"><span data-stu-id="280fe-132">If `Inherited` for an attribute class is false then that attribute is not inherited.</span></span> <span data-ttu-id="280fe-133">Если не указано, значение по умолчанию — true.</span><span class="sxs-lookup"><span data-stu-id="280fe-133">If it is unspecified, its default value is true.</span></span>

<span data-ttu-id="280fe-134">Класс атрибута `X` отсутствие `AttributeUsage` атрибут, присоединенный к нему, как показано на</span><span class="sxs-lookup"><span data-stu-id="280fe-134">An attribute class `X` not having an `AttributeUsage` attribute attached to it, as in</span></span>

```csharp
using System;

class X: Attribute {...}
```

<span data-ttu-id="280fe-135">Эквивалентно следующему:</span><span class="sxs-lookup"><span data-stu-id="280fe-135">is equivalent to the following:</span></span>

```csharp
using System;

[AttributeUsage(
    AttributeTargets.All,
    AllowMultiple = false,
    Inherited = true)
]
class X: Attribute {...}
```

### <a name="positional-and-named-parameters"></a><span data-ttu-id="280fe-136">Позиционные и именованные параметры</span><span class="sxs-lookup"><span data-stu-id="280fe-136">Positional and named parameters</span></span>

<span data-ttu-id="280fe-137">Классы атрибутов могут иметь ***позиционные параметры*** и ***именованные параметры***.</span><span class="sxs-lookup"><span data-stu-id="280fe-137">Attribute classes can have ***positional parameters*** and ***named parameters***.</span></span> <span data-ttu-id="280fe-138">Каждый конструктор открытого экземпляра для класса атрибута определяет допустимую последовательность позиционных параметров для этого класса атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-138">Each public instance constructor for an attribute class defines a valid sequence of positional parameters for that attribute class.</span></span> <span data-ttu-id="280fe-139">Каждого нестатических открытое поле для чтения и записи и свойства для класса атрибута определяет именованный параметр для класса атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-139">Each non-static public read-write field and property for an attribute class defines a named parameter for the attribute class.</span></span>

<span data-ttu-id="280fe-140">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-140">The example</span></span>

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

<span data-ttu-id="280fe-141">Определяет класс атрибута с именем `HelpAttribute` с одним позиционным параметром, `url`и один именованный параметр `Topic`.</span><span class="sxs-lookup"><span data-stu-id="280fe-141">defines an attribute class named `HelpAttribute` that has one positional parameter, `url`, and one named parameter, `Topic`.</span></span> <span data-ttu-id="280fe-142">Несмотря на то, что он является статическим и открытым, свойство `Url` не определяет именованный параметр, так как он не чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="280fe-142">Although it is non-static and public, the property `Url` does not define a named parameter, since it is not read-write.</span></span>

<span data-ttu-id="280fe-143">Этот класс атрибута можно использовать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="280fe-143">This attribute class might be used as follows:</span></span>

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

### <a name="attribute-parameter-types"></a><span data-ttu-id="280fe-144">Типы параметров атрибутов</span><span class="sxs-lookup"><span data-stu-id="280fe-144">Attribute parameter types</span></span>

<span data-ttu-id="280fe-145">Типы позиционных и именованных параметров для класса атрибута ограничены ***типы параметров атрибутов***, которые являются:</span><span class="sxs-lookup"><span data-stu-id="280fe-145">The types of positional and named parameters for an attribute class are limited to the ***attribute parameter types***, which are:</span></span>

*  <span data-ttu-id="280fe-146">Один из следующих типов: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`, `sbyte`, `short`, `string`, `uint`, `ulong`, `ushort`.</span><span class="sxs-lookup"><span data-stu-id="280fe-146">One of the following types: `bool`, `byte`, `char`, `double`, `float`, `int`, `long`, `sbyte`, `short`, `string`, `uint`, `ulong`, `ushort`.</span></span>
*  <span data-ttu-id="280fe-147">Тип `object`.</span><span class="sxs-lookup"><span data-stu-id="280fe-147">The type `object`.</span></span>
*  <span data-ttu-id="280fe-148">Тип `System.Type`.</span><span class="sxs-lookup"><span data-stu-id="280fe-148">The type `System.Type`.</span></span>
*  <span data-ttu-id="280fe-149">Перечисляемый тип, если он имеет общую доступность и типы, в которых он является вложенным (если таковые имеются) также иметь доступность уровня public ([спецификация атрибута](attributes.md#attribute-specification)).</span><span class="sxs-lookup"><span data-stu-id="280fe-149">An enum type, provided it has public accessibility and the types in which it is nested (if any) also have public accessibility ([Attribute specification](attributes.md#attribute-specification)).</span></span>
*  <span data-ttu-id="280fe-150">Одномерные массивы указанных выше типов.</span><span class="sxs-lookup"><span data-stu-id="280fe-150">Single-dimensional arrays of the above types.</span></span>
*  <span data-ttu-id="280fe-151">Аргумент конструктора или общее поле, которые не имеет ни одного из этих типов, не может использоваться как позиционные или именованные параметра в спецификации атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-151">A constructor argument or public field which does not have one of these types, cannot be used as a positional or named parameter in an attribute specification.</span></span>

## <a name="attribute-specification"></a><span data-ttu-id="280fe-152">Спецификация атрибута</span><span class="sxs-lookup"><span data-stu-id="280fe-152">Attribute specification</span></span>

<span data-ttu-id="280fe-153">***Спецификация атрибута*** — это применение предварительно определенного атрибута к объявлению.</span><span class="sxs-lookup"><span data-stu-id="280fe-153">***Attribute specification*** is the application of a previously defined attribute to a declaration.</span></span> <span data-ttu-id="280fe-154">Атрибут — это часть дополнительные описательные данные, указанный для объявления.</span><span class="sxs-lookup"><span data-stu-id="280fe-154">An attribute is a piece of additional declarative information that is specified for a declaration.</span></span> <span data-ttu-id="280fe-155">Атрибуты могут быть заданы в глобальной области видимости (для указания атрибутов на сборки или модуля, содержащего) и для *type_declaration*s ([объявления типов](namespaces.md#type-declarations)), *class_member_declaration* s ([ограничения параметров типа](classes.md#type-parameter-constraints)), *interface_member_declaration*s ([члены интерфейса](interfaces.md#interface-members)), *struct_member _declaration*s ([члены структуры](structs.md#struct-members)), *enum_member_declaration*s ([члены перечисления](enums.md#enum-members)), *accessor_declarations*  ([Методы доступа](classes.md#accessors)), *event_accessor_declarations* ([подобные полям события](classes.md#field-like-events)), и *formal_parameter_list*s ([параметры метода](classes.md#method-parameters)).</span><span class="sxs-lookup"><span data-stu-id="280fe-155">Attributes can be specified at global scope (to specify attributes on the containing assembly or module) and for *type_declaration*s ([Type declarations](namespaces.md#type-declarations)), *class_member_declaration*s ([Type parameter constraints](classes.md#type-parameter-constraints)), *interface_member_declaration*s ([Interface members](interfaces.md#interface-members)), *struct_member_declaration*s ([Struct members](structs.md#struct-members)), *enum_member_declaration*s ([Enum members](enums.md#enum-members)), *accessor_declarations* ([Accessors](classes.md#accessors)), *event_accessor_declarations* ([Field-like events](classes.md#field-like-events)), and *formal_parameter_list*s ([Method parameters](classes.md#method-parameters)).</span></span>

<span data-ttu-id="280fe-156">Атрибуты указаны в ***атрибут разделах***.</span><span class="sxs-lookup"><span data-stu-id="280fe-156">Attributes are specified in ***attribute sections***.</span></span> <span data-ttu-id="280fe-157">Раздел "атрибут" состоит из пары квадратных скобок, которые окружают разделенный запятыми список из одного или нескольких атрибутов.</span><span class="sxs-lookup"><span data-stu-id="280fe-157">An attribute section consists of a pair of square brackets, which surround a comma-separated list of one or more attributes.</span></span> <span data-ttu-id="280fe-158">Порядок, в котором указаны атрибуты в таком списке и расположены порядок, в котором разделы, подключенные к одной и той же сущности программы, не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="280fe-158">The order in which attributes are specified in such a list, and the order in which sections attached to the same program entity are arranged, is not significant.</span></span> <span data-ttu-id="280fe-159">Например, спецификаций атрибутов `[A][B]`, `[B][A]`, `[A,B]`, и `[B,A]` эквивалентны.</span><span class="sxs-lookup"><span data-stu-id="280fe-159">For instance, the attribute specifications `[A][B]`, `[B][A]`, `[A,B]`, and `[B,A]` are equivalent.</span></span>

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

<span data-ttu-id="280fe-160">Атрибут состоит из *attribute_name* и необязательный список позиционных и именованных аргументов.</span><span class="sxs-lookup"><span data-stu-id="280fe-160">An attribute consists of an *attribute_name* and an optional list of positional and named arguments.</span></span> <span data-ttu-id="280fe-161">Позиционные аргументы (если таковые имеются) предшествовать именованные аргументы.</span><span class="sxs-lookup"><span data-stu-id="280fe-161">The positional arguments (if any) precede the named arguments.</span></span> <span data-ttu-id="280fe-162">Позиционный аргумент состоит из *attribute_argument_expression*; именованный аргумент состоит из имени, а после знака равенства, за которым следует *attribute_argument_expression*, который, вместе , ограничены по тем же правилам, как простое присваивание.</span><span class="sxs-lookup"><span data-stu-id="280fe-162">A positional argument consists of an *attribute_argument_expression*; a named argument consists of a name, followed by an equal sign, followed by an *attribute_argument_expression*, which, together, are constrained by the same rules as simple assignment.</span></span> <span data-ttu-id="280fe-163">Порядок именованных аргументов не имеет значения.</span><span class="sxs-lookup"><span data-stu-id="280fe-163">The order of named arguments is not significant.</span></span>

<span data-ttu-id="280fe-164">*Attribute_name* идентифицирует класс атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-164">The *attribute_name* identifies an attribute class.</span></span> <span data-ttu-id="280fe-165">Если виде *attribute_name* — *type_name* затем это имя должно ссылаться на класс атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-165">If the form of *attribute_name* is *type_name* then this name must refer to an attribute class.</span></span> <span data-ttu-id="280fe-166">В противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-166">Otherwise, a compile-time error occurs.</span></span> <span data-ttu-id="280fe-167">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-167">The example</span></span>

```csharp
class Class1 {}

[Class1] class Class2 {}    // Error
```

<span data-ttu-id="280fe-168">приводит к ошибке времени компиляции, так как он пытается использовать `Class1` как атрибут класса, если `Class1` не является классом атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-168">results in a compile-time error because it attempts to use `Class1` as an attribute class when `Class1` is not an attribute class.</span></span>

<span data-ttu-id="280fe-169">Определенные контексты разрешают спецификацию атрибута на нескольких целевых объектов.</span><span class="sxs-lookup"><span data-stu-id="280fe-169">Certain contexts permit the specification of an attribute on more than one target.</span></span> <span data-ttu-id="280fe-170">Программы можно явно указать целевой объект, включив *attribute_target_specifier*.</span><span class="sxs-lookup"><span data-stu-id="280fe-170">A program can explicitly specify the target by including an *attribute_target_specifier*.</span></span> <span data-ttu-id="280fe-171">Когда атрибут помещается на глобальном уровне, *global_attribute_target_specifier* является обязательным.</span><span class="sxs-lookup"><span data-stu-id="280fe-171">When an attribute is placed at the global level, a *global_attribute_target_specifier* is required.</span></span> <span data-ttu-id="280fe-172">В других местах, применяется разумного значения по умолчанию, но *attribute_target_specifier* можно использовать для подтверждения или переопределить значение по умолчанию в определенных случаях неоднозначности (или просто для подтверждения по умолчанию в случаях неоднозначные).</span><span class="sxs-lookup"><span data-stu-id="280fe-172">In all other locations, a reasonable default is applied, but an *attribute_target_specifier* can be used to affirm or override the default in certain ambiguous cases (or to just affirm the default in non-ambiguous cases).</span></span> <span data-ttu-id="280fe-173">Таким образом, как правило, *attribute_target_specifier*s может опускаться только на глобальном уровне.</span><span class="sxs-lookup"><span data-stu-id="280fe-173">Thus, typically, *attribute_target_specifier*s can be omitted except at the global level.</span></span> <span data-ttu-id="280fe-174">Потенциально неоднозначной контексты разрешаются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="280fe-174">The potentially ambiguous contexts are resolved as follows:</span></span>

*  <span data-ttu-id="280fe-175">Атрибут, заданный в глобальной области можно применить к целевой сборке или целевому модулю.</span><span class="sxs-lookup"><span data-stu-id="280fe-175">An attribute specified at global scope can apply either to the target assembly or the target module.</span></span> <span data-ttu-id="280fe-176">По умолчанию существует для данного контекста, поэтому *attribute_target_specifier* всегда необходим в данном контексте.</span><span class="sxs-lookup"><span data-stu-id="280fe-176">No default exists for this context, so an *attribute_target_specifier* is always required in this context.</span></span> <span data-ttu-id="280fe-177">Наличие `assembly` *attribute_target_specifier* указывает, что атрибут применяется к целевому объекту сборки; наличие `module` *attribute_target_specifier* Указывает, что атрибут применяется к целевому модулю.</span><span class="sxs-lookup"><span data-stu-id="280fe-177">The presence of the `assembly` *attribute_target_specifier* indicates that the attribute applies to the target assembly; the presence of the `module` *attribute_target_specifier* indicates that the attribute applies to the target module.</span></span>
*  <span data-ttu-id="280fe-178">Атрибут, заданный в объявлении делегата можно применять к делегату объявляемого или возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-178">An attribute specified on a delegate declaration can apply either to the delegate being declared or to its return value.</span></span> <span data-ttu-id="280fe-179">В случае отсутствия *attribute_target_specifier*, атрибут применяется к делегату.</span><span class="sxs-lookup"><span data-stu-id="280fe-179">In the absence of an *attribute_target_specifier*, the attribute applies to the delegate.</span></span> <span data-ttu-id="280fe-180">Наличие `type` *attribute_target_specifier* указывает, что атрибут применяется к делегату; наличие `return` *attribute_target_specifier* Указывает, что атрибут применяется к возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-180">The presence of the `type` *attribute_target_specifier* indicates that the attribute applies to the delegate; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="280fe-181">Атрибут, заданный в объявлении метода можно применить для объявляемого метода или возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-181">An attribute specified on a method declaration can apply either to the method being declared or to its return value.</span></span> <span data-ttu-id="280fe-182">В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу.</span><span class="sxs-lookup"><span data-stu-id="280fe-182">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="280fe-183">Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `return` *attribute_target_specifier* указывает что атрибут применяется к возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-183">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="280fe-184">Атрибут, заданный в объявлении оператора можно применить к оператору или возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-184">An attribute specified on an operator declaration can apply either to the operator being declared or to its return value.</span></span> <span data-ttu-id="280fe-185">В случае отсутствия *attribute_target_specifier*, атрибут применяется к оператору.</span><span class="sxs-lookup"><span data-stu-id="280fe-185">In the absence of an *attribute_target_specifier*, the attribute applies to the operator.</span></span> <span data-ttu-id="280fe-186">Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `return` *attribute_target_specifier* Указывает, что атрибут применяется к возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-186">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the operator; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="280fe-187">Атрибут, заданный в объявлении события, который опускает доступа к событиям можно применять к событию, связанному полю (если событие не является абстрактным) или связанные добавить и удалить методы.</span><span class="sxs-lookup"><span data-stu-id="280fe-187">An attribute specified on an event declaration that omits event accessors can apply to the event being declared, to the associated field (if the event is not abstract), or to the associated add and remove methods.</span></span> <span data-ttu-id="280fe-188">В случае отсутствия *attribute_target_specifier*, атрибут применяется к событию.</span><span class="sxs-lookup"><span data-stu-id="280fe-188">In the absence of an *attribute_target_specifier*, the attribute applies to the event.</span></span> <span data-ttu-id="280fe-189">Наличие `event` *attribute_target_specifier* указывает, что атрибут применяется к событию; наличие `field` *attribute_target_specifier* указывает что атрибут применяется к полю; и наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методам.</span><span class="sxs-lookup"><span data-stu-id="280fe-189">The presence of the `event` *attribute_target_specifier* indicates that the attribute applies to the event; the presence of the `field` *attribute_target_specifier* indicates that the attribute applies to the field; and the presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the methods.</span></span>
*  <span data-ttu-id="280fe-190">Атрибут, заданный в объявлении метода доступа get для объявления свойства или индексатора можно применить для связанного метода или возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-190">An attribute specified on a get accessor declaration for a property or indexer declaration can apply either to the associated method or to its return value.</span></span> <span data-ttu-id="280fe-191">В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу.</span><span class="sxs-lookup"><span data-stu-id="280fe-191">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="280fe-192">Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `return` *attribute_target_specifier* указывает что атрибут применяется к возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-192">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="280fe-193">Атрибут, заданный в метод доступа set для объявления свойства или индексатора можно применить к связанному методу или к его одиночному неявное параметру.</span><span class="sxs-lookup"><span data-stu-id="280fe-193">An attribute specified on a set accessor for a property or indexer declaration can apply either to the associated method or to its lone implicit parameter.</span></span> <span data-ttu-id="280fe-194">В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу.</span><span class="sxs-lookup"><span data-stu-id="280fe-194">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="280fe-195">Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `param` *attribute_target_specifier* указывает что атрибут применяется к параметру; наличие `return` *attribute_target_specifier* указывает, что атрибут применяется к возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-195">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `param` *attribute_target_specifier* indicates that the attribute applies to the parameter; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>
*  <span data-ttu-id="280fe-196">Атрибут, заданный в объявлении метода доступа add или remove, для объявления события можно применить к связанному методу или к его одиночному параметру.</span><span class="sxs-lookup"><span data-stu-id="280fe-196">An attribute specified on an add or remove accessor declaration for an event declaration can apply either to the associated method or to its lone parameter.</span></span> <span data-ttu-id="280fe-197">В случае отсутствия *attribute_target_specifier*, атрибут применяется к методу.</span><span class="sxs-lookup"><span data-stu-id="280fe-197">In the absence of an *attribute_target_specifier*, the attribute applies to the method.</span></span> <span data-ttu-id="280fe-198">Наличие `method` *attribute_target_specifier* указывает, что атрибут применяется к методу; наличие `param` *attribute_target_specifier* указывает что атрибут применяется к параметру; наличие `return` *attribute_target_specifier* указывает, что атрибут применяется к возвращаемому значению.</span><span class="sxs-lookup"><span data-stu-id="280fe-198">The presence of the `method` *attribute_target_specifier* indicates that the attribute applies to the method; the presence of the `param` *attribute_target_specifier* indicates that the attribute applies to the parameter; the presence of the `return` *attribute_target_specifier* indicates that the attribute applies to the return value.</span></span>

<span data-ttu-id="280fe-199">В других контекстах, включение *attribute_target_specifier* разрешено, но ненужные.</span><span class="sxs-lookup"><span data-stu-id="280fe-199">In other contexts, inclusion of an *attribute_target_specifier* is permitted but unnecessary.</span></span> <span data-ttu-id="280fe-200">Например, объявление класса включается или опустить описатель `type`:</span><span class="sxs-lookup"><span data-stu-id="280fe-200">For instance, a class declaration may either include or omit the specifier `type`:</span></span>

```csharp
[type: Author("Brian Kernighan")]
class Class1 {}

[Author("Dennis Ritchie")]
class Class2 {}
```

<span data-ttu-id="280fe-201">Это ошибка для указано недопустимое *attribute_target_specifier*.</span><span class="sxs-lookup"><span data-stu-id="280fe-201">It is an error to specify an invalid *attribute_target_specifier*.</span></span> <span data-ttu-id="280fe-202">Например, описатель `param` не может использоваться в объявлении класса:</span><span class="sxs-lookup"><span data-stu-id="280fe-202">For instance, the specifier `param` cannot be used on a class declaration:</span></span>

```csharp
[param: Author("Brian Kernighan")]        // Error
class Class1 {}
```

<span data-ttu-id="280fe-203">По соглашению классы атрибутов именуются с суффиксом `Attribute`.</span><span class="sxs-lookup"><span data-stu-id="280fe-203">By convention, attribute classes are named with a suffix of `Attribute`.</span></span> <span data-ttu-id="280fe-204">*Attribute_name* формы *type_name* может включить или пропустить этот суффикс.</span><span class="sxs-lookup"><span data-stu-id="280fe-204">An *attribute_name* of the form *type_name* may either include or omit this suffix.</span></span> <span data-ttu-id="280fe-205">Если класс атрибута находится в том случае, как с и без этого суффикса, присутствует неоднозначность и приводит к ошибке времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-205">If an attribute class is found both with and without this suffix, an ambiguity is present, and a compile-time error results.</span></span> <span data-ttu-id="280fe-206">Если *attribute_name* написано таким образом, чтобы его крайнее правое *идентификатор* является буквальным идентификатором ([идентификаторы](lexical-structure.md#identifiers)), а затем сопоставляется только атрибут без суффикса, Таким образом, включение таких разрешить неоднозначность.</span><span class="sxs-lookup"><span data-stu-id="280fe-206">If the *attribute_name* is spelled such that its right-most *identifier* is a verbatim identifier ([Identifiers](lexical-structure.md#identifiers)), then only an attribute without a suffix is matched, thus enabling such an ambiguity to be resolved.</span></span> <span data-ttu-id="280fe-207">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-207">The example</span></span>

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

<span data-ttu-id="280fe-208">Показывает, два атрибута с именем классы `X` и `XAttribute`.</span><span class="sxs-lookup"><span data-stu-id="280fe-208">shows two attribute classes named `X` and `XAttribute`.</span></span> <span data-ttu-id="280fe-209">Атрибут `[X]` является неоднозначным, так как она может ссылаться на либо `X` или `XAttribute`.</span><span class="sxs-lookup"><span data-stu-id="280fe-209">The attribute `[X]` is ambiguous, since it could refer to either `X` or `XAttribute`.</span></span> <span data-ttu-id="280fe-210">С помощью буквальным идентификатором точного указания в таких редких случаях намерения.</span><span class="sxs-lookup"><span data-stu-id="280fe-210">Using a verbatim identifier allows the exact intent to be specified in such rare cases.</span></span> <span data-ttu-id="280fe-211">Атрибут `[XAttribute]` не является неоднозначным (несмотря на то, что было бы Если класс атрибута с именем `XAttributeAttribute`!).</span><span class="sxs-lookup"><span data-stu-id="280fe-211">The attribute `[XAttribute]` is not ambiguous (although it would be if there was an attribute class named `XAttributeAttribute`!).</span></span> <span data-ttu-id="280fe-212">Если объявление класса `X` удаляется, а затем оба атрибута ссылаются на класс атрибута с именем `XAttribute`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="280fe-212">If the declaration for class `X` is removed, then both attributes refer to the attribute class named `XAttribute`, as follows:</span></span>

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

<span data-ttu-id="280fe-213">Это ошибка времени компиляции для использования класса атрибутом однократного использования более одного раза на той же сущности.</span><span class="sxs-lookup"><span data-stu-id="280fe-213">It is a compile-time error to use a single-use attribute class more than once on the same entity.</span></span> <span data-ttu-id="280fe-214">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-214">The example</span></span>

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

<span data-ttu-id="280fe-215">приводит к ошибке времени компиляции, так как он пытается использовать `HelpString`, — это класс атрибутом однократного использования, более одного раза в объявлении `Class1`.</span><span class="sxs-lookup"><span data-stu-id="280fe-215">results in a compile-time error because it attempts to use `HelpString`, which is a single-use attribute class, more than once on the declaration of `Class1`.</span></span>

<span data-ttu-id="280fe-216">Выражение `E` — *attribute_argument_expression* если выполняются все следующие инструкции:</span><span class="sxs-lookup"><span data-stu-id="280fe-216">An expression `E` is an *attribute_argument_expression* if all of the following statements are true:</span></span>

*  <span data-ttu-id="280fe-217">Тип `E` является типом параметра атрибута ([типы параметров атрибутов](attributes.md#attribute-parameter-types)).</span><span class="sxs-lookup"><span data-stu-id="280fe-217">The type of `E` is an attribute parameter type ([Attribute parameter types](attributes.md#attribute-parameter-types)).</span></span>
*  <span data-ttu-id="280fe-218">Во время компиляции, значение `E` можно разрешить в одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="280fe-218">At compile-time, the value of `E` can be resolved to one of the following:</span></span>
   * <span data-ttu-id="280fe-219">Значение константы.</span><span class="sxs-lookup"><span data-stu-id="280fe-219">A constant value.</span></span>
   * <span data-ttu-id="280fe-220">Объект `System.Type`.</span><span class="sxs-lookup"><span data-stu-id="280fe-220">A `System.Type` object.</span></span>
   * <span data-ttu-id="280fe-221">Одномерный массив *attribute_argument_expression*s.</span><span class="sxs-lookup"><span data-stu-id="280fe-221">A one-dimensional array of *attribute_argument_expression*s.</span></span>

<span data-ttu-id="280fe-222">Пример:</span><span class="sxs-lookup"><span data-stu-id="280fe-222">For example:</span></span>

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

<span data-ttu-id="280fe-223">Объект *typeof_expression* ([оператор typeof](expressions.md#the-typeof-operator)) используется как выражения аргумента атрибута можно ссылаться неуниверсального типа, закрытым сконструированным типом или несвязанного универсального типа, но не может ссылаться на открытый тип.</span><span class="sxs-lookup"><span data-stu-id="280fe-223">A *typeof_expression* ([The typeof operator](expressions.md#the-typeof-operator)) used as an attribute argument expression can reference a non-generic type, a closed constructed type, or an unbound generic type, but it cannot reference an open type.</span></span> <span data-ttu-id="280fe-224">Это гарантирует, что выражение может разрешаться во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-224">This is to ensure that the expression can be resolved at compile-time.</span></span>

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

## <a name="attribute-instances"></a><span data-ttu-id="280fe-225">Экземпляры атрибута</span><span class="sxs-lookup"><span data-stu-id="280fe-225">Attribute instances</span></span>

<span data-ttu-id="280fe-226">***Экземпляра атрибута*** — это экземпляр, который представляет атрибут во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="280fe-226">An ***attribute instance*** is an instance that represents an attribute at run-time.</span></span> <span data-ttu-id="280fe-227">Атрибут определяется с помощью класса атрибута, позиционных аргументов и именованные аргументы.</span><span class="sxs-lookup"><span data-stu-id="280fe-227">An attribute is defined with an attribute class, positional arguments, and named arguments.</span></span> <span data-ttu-id="280fe-228">Экземпляр атрибута — это экземпляр класса атрибута, который инициализируется с помощью позиционных и именованных аргументов.</span><span class="sxs-lookup"><span data-stu-id="280fe-228">An attribute instance is an instance of the attribute class that is initialized with the positional and named arguments.</span></span>

<span data-ttu-id="280fe-229">Извлечение экземпляра атрибута включает в себя во время компиляции и выполнения обработки, как описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="280fe-229">Retrieval of an attribute instance involves both compile-time and run-time processing, as described in the following sections.</span></span>

### <a name="compilation-of-an-attribute"></a><span data-ttu-id="280fe-230">Компиляция атрибута</span><span class="sxs-lookup"><span data-stu-id="280fe-230">Compilation of an attribute</span></span>

<span data-ttu-id="280fe-231">Компиляция *атрибут* с классом атрибута `T`, *positional_argument_list* `P` и *named_argument_list* `N`, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="280fe-231">The compilation of an *attribute* with attribute class `T`, *positional_argument_list* `P` and *named_argument_list* `N`, consists of the following steps:</span></span>

*  <span data-ttu-id="280fe-232">Выполните шаги обработки компиляции для компиляции *object_creation_expression* формы `new T(P)`.</span><span class="sxs-lookup"><span data-stu-id="280fe-232">Follow the compile-time processing steps for compiling an *object_creation_expression* of the form `new T(P)`.</span></span> <span data-ttu-id="280fe-233">Эти действия к ошибке времени компиляции или определить конструктор экземпляра `C` на `T` может вызываться во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="280fe-233">These steps either result in a compile-time error, or determine an instance constructor `C` on `T` that can be invoked at run-time.</span></span>
*  <span data-ttu-id="280fe-234">Если `C` имеет открытый доступ, то возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-234">If `C` does not have public accessibility, then a compile-time error occurs.</span></span>
*  <span data-ttu-id="280fe-235">Для каждого *именованный_аргумент* `Arg` в `N`:</span><span class="sxs-lookup"><span data-stu-id="280fe-235">For each *named_argument* `Arg` in `N`:</span></span>
   * <span data-ttu-id="280fe-236">Позвольте `Name` быть *идентификатор* из *именованный_аргумент* `Arg`.</span><span class="sxs-lookup"><span data-stu-id="280fe-236">Let `Name` be the *identifier* of the *named_argument* `Arg`.</span></span>
   * <span data-ttu-id="280fe-237">`Name` необходимо определить нестатические чтения и записи открытое поле или свойство на `T`.</span><span class="sxs-lookup"><span data-stu-id="280fe-237">`Name` must identify a non-static read-write public field or property on `T`.</span></span> <span data-ttu-id="280fe-238">Если `T` имеет нет такого поля или свойства, то возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-238">If `T` has no such field or property, then a compile-time error occurs.</span></span>
*  <span data-ttu-id="280fe-239">Примите указанные ниже сведения для создания экземпляра атрибута во время выполнения: класс атрибута `T`, конструкторе экземпляра `C` на `T`, *positional_argument_list* `P` и *named_argument_list* `N`.</span><span class="sxs-lookup"><span data-stu-id="280fe-239">Keep the following information for run-time instantiation of the attribute: the attribute class `T`, the instance constructor `C` on `T`, the *positional_argument_list* `P` and the *named_argument_list* `N`.</span></span>

### <a name="run-time-retrieval-of-an-attribute-instance"></a><span data-ttu-id="280fe-240">Во время выполнения извлечения экземпляра атрибута</span><span class="sxs-lookup"><span data-stu-id="280fe-240">Run-time retrieval of an attribute instance</span></span>

<span data-ttu-id="280fe-241">Подборка *атрибут* дает класс атрибута `T`, конструкторе экземпляра `C` на `T`, *positional_argument_list* `P`и *named_argument_list* `N`.</span><span class="sxs-lookup"><span data-stu-id="280fe-241">Compilation of an *attribute* yields an attribute class `T`, an instance constructor `C` on `T`, a *positional_argument_list* `P`, and a *named_argument_list* `N`.</span></span> <span data-ttu-id="280fe-242">Учитывая эти сведения, экземпляр атрибута можно получить во время выполнения, выполнив следующие действия:</span><span class="sxs-lookup"><span data-stu-id="280fe-242">Given this information, an attribute instance can be retrieved at run-time using the following steps:</span></span>

*  <span data-ttu-id="280fe-243">Выполните шаги обработки времени выполнения для выполнения *object_creation_expression* формы `new T(P)`, используя конструктор экземпляра `C` определяется во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-243">Follow the run-time processing steps for executing an *object_creation_expression* of the form `new T(P)`, using the instance constructor `C` as determined at compile-time.</span></span> <span data-ttu-id="280fe-244">Следующие действия приводят к исключению, или создавать экземпляр `O` из `T`.</span><span class="sxs-lookup"><span data-stu-id="280fe-244">These steps either result in an exception, or produce an instance `O` of `T`.</span></span>
*  <span data-ttu-id="280fe-245">Для каждого *именованный_аргумент* `Arg` в `N`, в порядке:</span><span class="sxs-lookup"><span data-stu-id="280fe-245">For each *named_argument* `Arg` in `N`, in order:</span></span>
   * <span data-ttu-id="280fe-246">Позвольте `Name` быть *идентификатор* из *именованный_аргумент* `Arg`.</span><span class="sxs-lookup"><span data-stu-id="280fe-246">Let `Name` be the *identifier* of the *named_argument* `Arg`.</span></span> <span data-ttu-id="280fe-247">Если `Name` не определяет нестатических открытое поле для чтения и записи или свойства на `O`, то возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="280fe-247">If `Name` does not identify a non-static public read-write field or property on `O`, then an exception is thrown.</span></span>
   * <span data-ttu-id="280fe-248">Позвольте `Value` быть результатом вычисления *attribute_argument_expression* из `Arg`.</span><span class="sxs-lookup"><span data-stu-id="280fe-248">Let `Value` be the result of evaluating the *attribute_argument_expression* of `Arg`.</span></span>
   * <span data-ttu-id="280fe-249">Если `Name` определяет поле на `O`, затем выберите значение `Value`.</span><span class="sxs-lookup"><span data-stu-id="280fe-249">If `Name` identifies a field on `O`, then set this field to `Value`.</span></span>
   * <span data-ttu-id="280fe-250">В противном случае `Name` определяет свойство на `O`.</span><span class="sxs-lookup"><span data-stu-id="280fe-250">Otherwise, `Name` identifies a property on `O`.</span></span> <span data-ttu-id="280fe-251">Присвойте этому свойству значение `Value`.</span><span class="sxs-lookup"><span data-stu-id="280fe-251">Set this property to `Value`.</span></span>
   * <span data-ttu-id="280fe-252">В результате `O`, экземпляр класса атрибута `T` , инициализирована с помощью *positional_argument_list* `P` и *named_argument_list* `N`.</span><span class="sxs-lookup"><span data-stu-id="280fe-252">The result is `O`, an instance of the attribute class `T` that has been initialized with the *positional_argument_list* `P` and the *named_argument_list* `N`.</span></span>

## <a name="reserved-attributes"></a><span data-ttu-id="280fe-253">Зарезервированные атрибуты</span><span class="sxs-lookup"><span data-stu-id="280fe-253">Reserved attributes</span></span>

<span data-ttu-id="280fe-254">Небольшое количество атрибутов влияет на язык каким-либо образом.</span><span class="sxs-lookup"><span data-stu-id="280fe-254">A small number of attributes affect the language in some way.</span></span> <span data-ttu-id="280fe-255">Эти атрибуты включают:</span><span class="sxs-lookup"><span data-stu-id="280fe-255">These attributes include:</span></span>

*  <span data-ttu-id="280fe-256">`System.AttributeUsageAttribute` ([Атрибут AttributeUsage](attributes.md#the-attributeusage-attribute)), который используется для описания способов, в котором можно использовать класс атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-256">`System.AttributeUsageAttribute` ([The AttributeUsage attribute](attributes.md#the-attributeusage-attribute)), which is used to describe the ways in which an attribute class can be used.</span></span>
*  <span data-ttu-id="280fe-257">`System.Diagnostics.ConditionalAttribute` ([Атрибут Conditional](attributes.md#the-conditional-attribute)), который используется для определения условные методы.</span><span class="sxs-lookup"><span data-stu-id="280fe-257">`System.Diagnostics.ConditionalAttribute` ([The Conditional attribute](attributes.md#the-conditional-attribute)), which is used to define conditional methods.</span></span>
*  <span data-ttu-id="280fe-258">`System.ObsoleteAttribute` ([Атрибут Obsolete](attributes.md#the-obsolete-attribute)), который используется для пометки элемента как устаревший.</span><span class="sxs-lookup"><span data-stu-id="280fe-258">`System.ObsoleteAttribute` ([The Obsolete attribute](attributes.md#the-obsolete-attribute)), which is used to mark a member as obsolete.</span></span>
*  <span data-ttu-id="280fe-259">`System.Runtime.CompilerServices.CallerLineNumberAttribute`, `System.Runtime.CompilerServices.CallerFilePathAttribute` и `System.Runtime.CompilerServices.CallerMemberNameAttribute` ([информационные атрибуты вызывающего объекта](attributes.md#caller-info-attributes)), которые используются для предоставления сведений о контексте вызова к необязательным параметрам.</span><span class="sxs-lookup"><span data-stu-id="280fe-259">`System.Runtime.CompilerServices.CallerLineNumberAttribute`, `System.Runtime.CompilerServices.CallerFilePathAttribute` and `System.Runtime.CompilerServices.CallerMemberNameAttribute` ([Caller info attributes](attributes.md#caller-info-attributes)), which are used to supply information about the calling context to optional parameters.</span></span>

### <a name="the-attributeusage-attribute"></a><span data-ttu-id="280fe-260">Атрибут AttributeUsage</span><span class="sxs-lookup"><span data-stu-id="280fe-260">The AttributeUsage attribute</span></span>

<span data-ttu-id="280fe-261">Атрибут `AttributeUsage` используется для описания способа, в котором можно использовать класс атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-261">The attribute `AttributeUsage` is used to describe the manner in which the attribute class can be used.</span></span>

<span data-ttu-id="280fe-262">Класс, отмеченный атрибутом `AttributeUsage` атрибут должен быть производным от `System.Attribute`, прямо или косвенно.</span><span class="sxs-lookup"><span data-stu-id="280fe-262">A class that is decorated with the `AttributeUsage` attribute must derive from `System.Attribute`, either directly or indirectly.</span></span> <span data-ttu-id="280fe-263">В противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-263">Otherwise, a compile-time error occurs.</span></span>

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

### <a name="the-conditional-attribute"></a><span data-ttu-id="280fe-264">Атрибут Conditional</span><span class="sxs-lookup"><span data-stu-id="280fe-264">The Conditional attribute</span></span>

<span data-ttu-id="280fe-265">Атрибут `Conditional` позволяет определять ***условные методы*** и ***классы атрибут conditional***.</span><span class="sxs-lookup"><span data-stu-id="280fe-265">The attribute `Conditional` enables the definition of ***conditional methods*** and ***conditional attribute classes***.</span></span>

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

#### <a name="conditional-methods"></a><span data-ttu-id="280fe-266">Условные методы.</span><span class="sxs-lookup"><span data-stu-id="280fe-266">Conditional methods</span></span>

<span data-ttu-id="280fe-267">Метод с атрибутом `Conditional` атрибут является условный метод.</span><span class="sxs-lookup"><span data-stu-id="280fe-267">A method decorated with the `Conditional` attribute is a conditional method.</span></span> <span data-ttu-id="280fe-268">`Conditional` Атрибут указывает условие, тестируя символ условной компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-268">The `Conditional` attribute indicates a condition by testing a conditional compilation symbol.</span></span> <span data-ttu-id="280fe-269">Вызовы условного метода либо включены, либо пропущено в зависимости от того, определен ли этот символ в точке вызова.</span><span class="sxs-lookup"><span data-stu-id="280fe-269">Calls to a conditional method are either included or omitted depending on whether this symbol is defined at the point of the call.</span></span> <span data-ttu-id="280fe-270">Если этот символ определен, вызов включается; в противном случае вызов (включая оценки приемника и параметры вызова) опускается.</span><span class="sxs-lookup"><span data-stu-id="280fe-270">If the symbol is defined, the call is included; otherwise, the call (including evaluation of the receiver and parameters of the call) is omitted.</span></span>

<span data-ttu-id="280fe-271">Условный метод имеет следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="280fe-271">A conditional method is subject to the following restrictions:</span></span>

*  <span data-ttu-id="280fe-272">Условный метод должен быть методом в *class_declaration* или *struct_declaration*.</span><span class="sxs-lookup"><span data-stu-id="280fe-272">The conditional method must be a method in a *class_declaration* or *struct_declaration*.</span></span> <span data-ttu-id="280fe-273">Ошибка времени компиляции возникает, если `Conditional` атрибут указан для метода в объявлении интерфейса.</span><span class="sxs-lookup"><span data-stu-id="280fe-273">A compile-time error occurs if the `Conditional` attribute is specified on a method in an interface declaration.</span></span>
*  <span data-ttu-id="280fe-274">Условный метод должен иметь тип возвращаемого значения `void`.</span><span class="sxs-lookup"><span data-stu-id="280fe-274">The conditional method must have a return type of `void`.</span></span>
*  <span data-ttu-id="280fe-275">Условный метод не должен быть помечен с помощью `override` модификатор.</span><span class="sxs-lookup"><span data-stu-id="280fe-275">The conditional method must not be marked with the `override` modifier.</span></span> <span data-ttu-id="280fe-276">Условный метод помечен `virtual` модификатор, тем не менее.</span><span class="sxs-lookup"><span data-stu-id="280fe-276">A conditional method may be marked with the `virtual` modifier, however.</span></span> <span data-ttu-id="280fe-277">Переопределения такого метода неявно условного и не должен быть помечен явно с `Conditional` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-277">Overrides of such a method are implicitly conditional, and must not be explicitly marked with a `Conditional` attribute.</span></span>
*  <span data-ttu-id="280fe-278">Условный метод не должен быть реализацию метода интерфейса.</span><span class="sxs-lookup"><span data-stu-id="280fe-278">The conditional method must not be an implementation of an interface method.</span></span> <span data-ttu-id="280fe-279">В противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="280fe-279">Otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="280fe-280">Кроме того, возникает ошибка времени компиляции, если условный метод используется в *delegate_creation_expression*.</span><span class="sxs-lookup"><span data-stu-id="280fe-280">In addition, a compile-time error occurs if a conditional method is used in a *delegate_creation_expression*.</span></span> <span data-ttu-id="280fe-281">Пример</span><span class="sxs-lookup"><span data-stu-id="280fe-281">The example</span></span>

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

<span data-ttu-id="280fe-282">объявляет `Class1.M` как условный метод.</span><span class="sxs-lookup"><span data-stu-id="280fe-282">declares `Class1.M` as a conditional method.</span></span> <span data-ttu-id="280fe-283">`Class2`в `Test` метод вызывает этот метод.</span><span class="sxs-lookup"><span data-stu-id="280fe-283">`Class2`'s `Test` method calls this method.</span></span> <span data-ttu-id="280fe-284">Так как символ условной компиляции `DEBUG` определено, если `Class2.Test` является именем, он вызывает `M`.</span><span class="sxs-lookup"><span data-stu-id="280fe-284">Since the conditional compilation symbol `DEBUG` is defined, if `Class2.Test` is called, it will call `M`.</span></span> <span data-ttu-id="280fe-285">Если символ `DEBUG` бы не был определен, затем `Class2.Test` вызовет не `Class1.M`.</span><span class="sxs-lookup"><span data-stu-id="280fe-285">If the symbol `DEBUG` had not been defined, then `Class2.Test` would not call `Class1.M`.</span></span>

<span data-ttu-id="280fe-286">Важно отметить, что включение или исключение вызова условного метода управляется символами условной компиляции в точке вызова.</span><span class="sxs-lookup"><span data-stu-id="280fe-286">It is important to note that the inclusion or exclusion of a call to a conditional method is controlled by the conditional compilation symbols at the point of the call.</span></span> <span data-ttu-id="280fe-287">В примере</span><span class="sxs-lookup"><span data-stu-id="280fe-287">In the example</span></span>

<span data-ttu-id="280fe-288">Файл `class1.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-288">File `class1.cs`:</span></span>

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

<span data-ttu-id="280fe-289">Файл `class2.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-289">File `class2.cs`:</span></span>

```csharp
#define DEBUG

class Class2
{
    public static void G() {
        Class1.F();                // F is called
    }
}
```

<span data-ttu-id="280fe-290">Файл `class3.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-290">File `class3.cs`:</span></span>

```csharp
#undef DEBUG

class Class3
{
    public static void H() {
        Class1.F();                // F is not called
    }
}
```

<span data-ttu-id="280fe-291">классы `Class2` и `Class3` каждая содержит вызовы условного метода `Class1.F`, который условного основан на ли `DEBUG` определен.</span><span class="sxs-lookup"><span data-stu-id="280fe-291">the classes `Class2` and `Class3` each contain calls to the conditional method `Class1.F`, which is conditional based on whether or not `DEBUG` is defined.</span></span> <span data-ttu-id="280fe-292">Так как этот символ определен в контексте `Class2` , но не `Class3`, вызов `F` в `Class2` включено, а вызов `F` в `Class3` опускается.</span><span class="sxs-lookup"><span data-stu-id="280fe-292">Since this symbol is defined in the context of `Class2` but not `Class3`, the call to `F` in `Class2` is included, while the call to `F` in `Class3` is omitted.</span></span>

<span data-ttu-id="280fe-293">Использование условного методов в цепочке наследования могут быть запутанными.</span><span class="sxs-lookup"><span data-stu-id="280fe-293">The use of conditional methods in an inheritance chain can be confusing.</span></span> <span data-ttu-id="280fe-294">Вызовы условного метода через `base`, формы `base.M`, подчиняются правилам обычный метод условного вызова.</span><span class="sxs-lookup"><span data-stu-id="280fe-294">Calls made to a conditional method through `base`, of the form `base.M`, are subject to the normal conditional method call rules.</span></span> <span data-ttu-id="280fe-295">В примере</span><span class="sxs-lookup"><span data-stu-id="280fe-295">In the example</span></span>

<span data-ttu-id="280fe-296">Файл `class1.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-296">File `class1.cs`:</span></span>

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

<span data-ttu-id="280fe-297">Файл `class2.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-297">File `class2.cs`:</span></span>

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

<span data-ttu-id="280fe-298">Файл `class3.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-298">File `class3.cs`:</span></span>

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

<span data-ttu-id="280fe-299">`Class2` включает вызов `M` определенные в базовом классе.</span><span class="sxs-lookup"><span data-stu-id="280fe-299">`Class2` includes a call to the `M` defined in its base class.</span></span> <span data-ttu-id="280fe-300">Этот вызов опускается, так как базовый метод условного на основе наличия символа `DEBUG`, который не определен.</span><span class="sxs-lookup"><span data-stu-id="280fe-300">This call is omitted because the base method is conditional based on the presence of the symbol `DEBUG`, which is undefined.</span></span> <span data-ttu-id="280fe-301">Таким образом, метод выводит на консоль "`Class2.M executed`" только.</span><span class="sxs-lookup"><span data-stu-id="280fe-301">Thus, the method writes to the console "`Class2.M executed`" only.</span></span> <span data-ttu-id="280fe-302">Разумно использовать *pp_declaration*s может устранить такие проблемы.</span><span class="sxs-lookup"><span data-stu-id="280fe-302">Judicious use of *pp_declaration*s can eliminate such problems.</span></span>

#### <a name="conditional-attribute-classes"></a><span data-ttu-id="280fe-303">Атрибут Conditional классы</span><span class="sxs-lookup"><span data-stu-id="280fe-303">Conditional attribute classes</span></span>

<span data-ttu-id="280fe-304">Класс атрибута ([классы атрибутов](attributes.md#attribute-classes)) декорированные с одним или несколькими `Conditional` атрибутов ***класса атрибут conditional***.</span><span class="sxs-lookup"><span data-stu-id="280fe-304">An attribute class ([Attribute classes](attributes.md#attribute-classes)) decorated with one or more `Conditional` attributes is a ***conditional attribute class***.</span></span> <span data-ttu-id="280fe-305">Класс атрибут conditional, таким образом, связанные с символы условной компиляции, объявленных в его `Conditional` атрибуты.</span><span class="sxs-lookup"><span data-stu-id="280fe-305">A conditional attribute class is thus associated with the conditional compilation symbols declared in its `Conditional` attributes.</span></span> <span data-ttu-id="280fe-306">Этот пример.</span><span class="sxs-lookup"><span data-stu-id="280fe-306">This example:</span></span>

```csharp
using System;
using System.Diagnostics;
[Conditional("ALPHA")]
[Conditional("BETA")]
public class TestAttribute : Attribute {}
```

<span data-ttu-id="280fe-307">объявляет `TestAttribute` как атрибут conditional класс, связанный с символами условной компиляции `ALPHA` и `BETA`.</span><span class="sxs-lookup"><span data-stu-id="280fe-307">declares `TestAttribute` as a conditional attribute class associated with the conditional compilations symbols `ALPHA` and `BETA`.</span></span>

<span data-ttu-id="280fe-308">Спецификации атрибута ([спецификация атрибута](attributes.md#attribute-specification)) условного атрибута включаются, если один или несколько символов связанные условной компиляции определен точке спецификации, в противном случае атрибут Спецификация опускается.</span><span class="sxs-lookup"><span data-stu-id="280fe-308">Attribute specifications ([Attribute specification](attributes.md#attribute-specification)) of a conditional attribute are included if one or more of its associated conditional compilation symbols is defined at the point of specification, otherwise the attribute specification is omitted.</span></span>

<span data-ttu-id="280fe-309">Это важно отметить, что включение или исключение спецификации атрибута класса атрибут conditional управляется символы условной компиляции точке спецификации.</span><span class="sxs-lookup"><span data-stu-id="280fe-309">It is important to note that the inclusion or exclusion of an attribute specification of a conditional attribute class is controlled by the conditional compilation symbols at the point of the specification.</span></span> <span data-ttu-id="280fe-310">В примере</span><span class="sxs-lookup"><span data-stu-id="280fe-310">In the example</span></span>

<span data-ttu-id="280fe-311">Файл `test.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-311">File `test.cs`:</span></span>

```csharp
using System;
using System.Diagnostics;

[Conditional("DEBUG")]

public class TestAttribute : Attribute {}
```

<span data-ttu-id="280fe-312">Файл `class1.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-312">File `class1.cs`:</span></span>

```csharp
#define DEBUG

[Test]                // TestAttribute is specified

class Class1 {}
```

<span data-ttu-id="280fe-313">Файл `class2.cs`:</span><span class="sxs-lookup"><span data-stu-id="280fe-313">File `class2.cs`:</span></span>

```csharp
#undef DEBUG

[Test]                 // TestAttribute is not specified

class Class2 {}
```

<span data-ttu-id="280fe-314">классы `Class1` и `Class2` являются каждого дополнен атрибутом `Test`, которой условного зависит от того, нужно ли `DEBUG` определен.</span><span class="sxs-lookup"><span data-stu-id="280fe-314">the classes `Class1` and `Class2` are each decorated with attribute `Test`, which is conditional based on whether or not `DEBUG` is defined.</span></span> <span data-ttu-id="280fe-315">Так как этот символ определен в контексте `Class1` , но не `Class2`, спецификация `Test` атрибут `Class1` включаются при спецификации `Test` атрибут `Class2` опускается.</span><span class="sxs-lookup"><span data-stu-id="280fe-315">Since this symbol is defined in the context of `Class1` but not `Class2`, the specification of the `Test` attribute on `Class1` is included, while the specification of the `Test` attribute on `Class2` is omitted.</span></span>

### <a name="the-obsolete-attribute"></a><span data-ttu-id="280fe-316">Атрибут Obsolete</span><span class="sxs-lookup"><span data-stu-id="280fe-316">The Obsolete attribute</span></span>

<span data-ttu-id="280fe-317">Атрибут `Obsolete` используется для пометки типы и члены типов, которые больше не должны использоваться.</span><span class="sxs-lookup"><span data-stu-id="280fe-317">The attribute `Obsolete` is used to mark types and members of types that should no longer be used.</span></span>

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

<span data-ttu-id="280fe-318">Если программа использует тип или член, отмеченный атрибутом `Obsolete` атрибут, компилятор выдает предупреждение или ошибку.</span><span class="sxs-lookup"><span data-stu-id="280fe-318">If a program uses a type or member that is decorated with the `Obsolete` attribute, the compiler issues a warning or an error.</span></span> <span data-ttu-id="280fe-319">В частности, компилятор выдает предупреждение, если указан параметр не ошибка, или если параметр ошибки и имеет значение `false`.</span><span class="sxs-lookup"><span data-stu-id="280fe-319">Specifically, the compiler issues a warning if no error parameter is provided, or if the error parameter is provided and has the value `false`.</span></span> <span data-ttu-id="280fe-320">Компилятор выдает ошибку, если указан параметр ошибки и имеет значение `true`.</span><span class="sxs-lookup"><span data-stu-id="280fe-320">The compiler issues an error if the error parameter is specified and has the value `true`.</span></span>

<span data-ttu-id="280fe-321">В примере</span><span class="sxs-lookup"><span data-stu-id="280fe-321">In the example</span></span>

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

<span data-ttu-id="280fe-322">Класс `A` снабжен `Obsolete` атрибута.</span><span class="sxs-lookup"><span data-stu-id="280fe-322">the class `A` is decorated with the `Obsolete` attribute.</span></span> <span data-ttu-id="280fe-323">Каждое использование `A` в `Main` результаты предупреждение с указанным сообщением «этот класс является устаревшим. Используйте класс B.»</span><span class="sxs-lookup"><span data-stu-id="280fe-323">Each use of `A` in `Main` results in a warning that includes the specified message, "This class is obsolete; use class B instead."</span></span>

### <a name="caller-info-attributes"></a><span data-ttu-id="280fe-324">Информационные атрибуты вызывающего объекта</span><span class="sxs-lookup"><span data-stu-id="280fe-324">Caller info attributes</span></span>

<span data-ttu-id="280fe-325">Для целей, например для ведения журналов и отчетности иногда полезно для функции-члена для получения определенных сведений во время компиляции об вызывающий код.</span><span class="sxs-lookup"><span data-stu-id="280fe-325">For purposes such as logging and reporting, it is sometimes useful for a function member to obtain certain compile-time information about the calling code.</span></span> <span data-ttu-id="280fe-326">Информационные атрибуты вызывающего объекта предоставить способ передачи таких сведений прозрачно.</span><span class="sxs-lookup"><span data-stu-id="280fe-326">The caller info attributes provide a way to pass such information transparently.</span></span>

<span data-ttu-id="280fe-327">Если необязательный параметр помечается с помощью одного из информационные атрибуты вызывающего объекта, пропуск соответствующего аргумента в вызове необязательно вызывают значение параметра по умолчанию должен быть замещен.</span><span class="sxs-lookup"><span data-stu-id="280fe-327">When an optional parameter is annotated with one of the caller info attributes, omitting the corresponding argument in a call does not necessarily cause the default parameter value to be substituted.</span></span> <span data-ttu-id="280fe-328">Вместо этого Если доступен указанный сведения о вызывающем контексте, эти сведения будут переданы как значение аргумента.</span><span class="sxs-lookup"><span data-stu-id="280fe-328">Instead, if the specified information about the calling context is available, that information will be passed as the argument value.</span></span>

<span data-ttu-id="280fe-329">Пример:</span><span class="sxs-lookup"><span data-stu-id="280fe-329">For example:</span></span>

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

<span data-ttu-id="280fe-330">Вызов `Log()` без аргументов выводит строки и номер путь вызова, а также имя члена, в котором произошел вызов.</span><span class="sxs-lookup"><span data-stu-id="280fe-330">A call to `Log()` with no arguments would print the line number and file path of the call, as well as the name of the member within which the call occurred.</span></span>

<span data-ttu-id="280fe-331">Информационные атрибуты вызывающего объекта может произойти в любой точке мира, необязательные параметры, включая в объявлениях делегатов.</span><span class="sxs-lookup"><span data-stu-id="280fe-331">Caller info attributes can occur on optional parameters anywhere, including in delegate declarations.</span></span> <span data-ttu-id="280fe-332">Тем не менее атрибуты сведений о конкретной вызывающей стороны имеют ограничения на типы параметров, которые они могут атрибута, таким образом, чтобы всегда будет существовать неявное преобразование из подставляемого значения к типу параметра.</span><span class="sxs-lookup"><span data-stu-id="280fe-332">However, the specific caller info attributes have restrictions on the types of the parameters they can attribute, so that there will always be an implicit conversion from a substituted value to the parameter type.</span></span>

<span data-ttu-id="280fe-333">Это ошибкой в том же информационный атрибут вызывающего объекта для параметра, как определить и реализовать часть объявления разделяемого метода.</span><span class="sxs-lookup"><span data-stu-id="280fe-333">It is an error to have the same caller info attribute on a parameter of both the defining and implementing part of a partial method declaration.</span></span> <span data-ttu-id="280fe-334">Применяются только информационные атрибуты вызывающего объекта в определение части, в то время как происходит только в реализации части информационные атрибуты вызывающего объекта учитываются.</span><span class="sxs-lookup"><span data-stu-id="280fe-334">Only caller info attributes in the defining part are applied, whereas caller info attributes occurring only in the implementing part are ignored.</span></span>

<span data-ttu-id="280fe-335">Сведения о вызывающем объекте не влияет на разрешение перегрузки.</span><span class="sxs-lookup"><span data-stu-id="280fe-335">Caller information does not affect overload resolution.</span></span> <span data-ttu-id="280fe-336">Как по-прежнему с атрибутами возможно использование необязательных параметров опускаются из исходного кода, вызывающего объекта, разрешение перегрузки игнорирует эти параметры таким же образом, он игнорирует другие пропущенный необязательные параметры ([разрешение перегрузки](expressions.md#overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="280fe-336">As the attributed optional parameters are still omitted from the source code of the caller, overload resolution ignores those parameters in the same way it ignores other omitted optional parameters ([Overload resolution](expressions.md#overload-resolution)).</span></span>

<span data-ttu-id="280fe-337">Сведения о вызывающем объекте подставляется только в том случае, когда функция вызывается явным образом в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="280fe-337">Caller information is only substituted when a function is explicitly invoked in source code.</span></span> <span data-ttu-id="280fe-338">Неявные вызовы, например неявные родительский конструктор вызывает нет исходного расположения и не производит подстановку сведения о вызывающем объекте.</span><span class="sxs-lookup"><span data-stu-id="280fe-338">Implicit invocations such as implicit parent constructor calls do not have a source location and will not substitute caller information.</span></span> <span data-ttu-id="280fe-339">Кроме того вызовы, динамическая привязка не заменит сведения о вызывающем объекте.</span><span class="sxs-lookup"><span data-stu-id="280fe-339">Also, calls that are dynamically bound will not substitute caller information.</span></span> <span data-ttu-id="280fe-340">Если вызывающий объект info, атрибутами параметр опускается в таких случаях, будет использовано указанное значение по умолчанию значение параметра.</span><span class="sxs-lookup"><span data-stu-id="280fe-340">When a caller info attributed parameter is omitted in such cases, the specified default value of the parameter is used instead.</span></span>

<span data-ttu-id="280fe-341">Единственное исключение — выражения запроса.</span><span class="sxs-lookup"><span data-stu-id="280fe-341">One exception is query-expressions.</span></span> <span data-ttu-id="280fe-342">Они считаются синтаксические расширения, и если вызовы расширены, чтобы пропустить необязательные параметры с информационные атрибуты вызывающего объекта, будут заменены сведения о вызывающем объекте.</span><span class="sxs-lookup"><span data-stu-id="280fe-342">These are considered syntactic expansions, and if the calls they expand to omit optional parameters with caller info attributes, caller information will be substituted.</span></span> <span data-ttu-id="280fe-343">Место, используемое находится предложение запроса, что вызов был создан из.</span><span class="sxs-lookup"><span data-stu-id="280fe-343">The location used is the location of the query clause which the call was generated from.</span></span>

<span data-ttu-id="280fe-344">Если указано более одного Информационный атрибут вызывающего объекта на данном параметре, они являются предпочтительными в следующем порядке: `CallerLineNumber`, `CallerFilePath`, `CallerMemberName`.</span><span class="sxs-lookup"><span data-stu-id="280fe-344">If more than one caller info attribute is specified on a given parameter, they are preferred in the following order: `CallerLineNumber`, `CallerFilePath`, `CallerMemberName`.</span></span>

#### <a name="the-callerlinenumber-attribute"></a><span data-ttu-id="280fe-345">Атрибут CallerLineNumber</span><span class="sxs-lookup"><span data-stu-id="280fe-345">The CallerLineNumber attribute</span></span>

<span data-ttu-id="280fe-346">`System.Runtime.CompilerServices.CallerLineNumberAttribute` Разрешена для необязательных параметров, при отсутствии стандартного неявные преобразования ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) из значения константы `int.MaxValue` к типу параметра.</span><span class="sxs-lookup"><span data-stu-id="280fe-346">The `System.Runtime.CompilerServices.CallerLineNumberAttribute` is allowed on optional parameters when there is a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) from the constant value `int.MaxValue` to the parameter's type.</span></span> <span data-ttu-id="280fe-347">Это гарантирует, что любое строки неотрицательное число вплоть до это значение можно передать без ошибок.</span><span class="sxs-lookup"><span data-stu-id="280fe-347">This ensures that any non-negative line number up to that value can be passed without error.</span></span>

<span data-ttu-id="280fe-348">Если вызов функции из расположения в исходном коде опускает необязательный параметр со `CallerLineNumberAttribute`, а затем числовой литерал, представляющий номер строки в это расположение используется в качестве аргумента вызова вместо значения параметра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="280fe-348">If a function invocation from a location in source code omits an optional parameter with the `CallerLineNumberAttribute`, then a numeric literal representing that location's line number is used as an argument to the invocation instead of the default parameter value.</span></span>

<span data-ttu-id="280fe-349">Если вызов занимает несколько строк, выбранной строки зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="280fe-349">If the invocation spans multiple lines, the line chosen is implementation-dependent.</span></span>

<span data-ttu-id="280fe-350">Обратите внимание, что номер строки могут быть затронуты `#line` директивы ([строки директивы](lexical-structure.md#line-directives)).</span><span class="sxs-lookup"><span data-stu-id="280fe-350">Note that the line number may be affected by `#line` directives ([Line directives](lexical-structure.md#line-directives)).</span></span>

#### <a name="the-callerfilepath-attribute"></a><span data-ttu-id="280fe-351">Атрибут CallerFilePath</span><span class="sxs-lookup"><span data-stu-id="280fe-351">The CallerFilePath attribute</span></span>

<span data-ttu-id="280fe-352">`System.Runtime.CompilerServices.CallerFilePathAttribute` Разрешена для необязательных параметров, при отсутствии стандартного неявные преобразования ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) из `string` к типу параметра.</span><span class="sxs-lookup"><span data-stu-id="280fe-352">The `System.Runtime.CompilerServices.CallerFilePathAttribute` is allowed on optional parameters when there is a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) from `string` to the parameter's type.</span></span>

<span data-ttu-id="280fe-353">Если вызов функции из расположения в исходном коде опускает необязательный параметр со `CallerFilePathAttribute`, а затем в строковый литерал, представляющий путь к файлу это расположение используется в качестве аргумента вызова вместо значения параметра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="280fe-353">If a function invocation from a location in source code omits an optional parameter with the `CallerFilePathAttribute`, then a string literal representing that location's file path is used as an argument to the invocation instead of the default parameter value.</span></span>

<span data-ttu-id="280fe-354">Формат пути к файлу зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="280fe-354">The format of the file path is implementation-dependent.</span></span>

<span data-ttu-id="280fe-355">Обратите внимание, что путь к файлу может затронуть `#line` директивы ([строки директивы](lexical-structure.md#line-directives)).</span><span class="sxs-lookup"><span data-stu-id="280fe-355">Note that the file path may be affected by `#line` directives ([Line directives](lexical-structure.md#line-directives)).</span></span>

#### <a name="the-callermembername-attribute"></a><span data-ttu-id="280fe-356">Атрибут CallerMemberName</span><span class="sxs-lookup"><span data-stu-id="280fe-356">The CallerMemberName attribute</span></span>

<span data-ttu-id="280fe-357">`System.Runtime.CompilerServices.CallerMemberNameAttribute` Разрешена для необязательных параметров, при отсутствии стандартного неявные преобразования ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) из `string` к типу параметра.</span><span class="sxs-lookup"><span data-stu-id="280fe-357">The `System.Runtime.CompilerServices.CallerMemberNameAttribute` is allowed on optional parameters when there is a standard implicit conversion ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) from `string` to the parameter's type.</span></span>

<span data-ttu-id="280fe-358">Если вызов функции из расположения в теле функции-члена или в атрибут применен к функции-члена, самого или его тип возвращаемого значения, параметров или параметров типа в исходный код опускает необязательный параметр со `CallerMemberNameAttribute`, а затем строковый литерал, представляющий имя этого элемента используется в качестве аргумента вызова вместо значения параметра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="280fe-358">If a function invocation from a location within the body of a function member or within an attribute applied to the function member itself or its return type, parameters or type parameters in source code omits an optional parameter with the `CallerMemberNameAttribute`, then a string literal representing the name of that member is used as an argument to the invocation instead of the default parameter value.</span></span>

<span data-ttu-id="280fe-359">Для вызовов, происходящих в универсальных методах только само имя метода используется без списка параметров типа.</span><span class="sxs-lookup"><span data-stu-id="280fe-359">For invocations that occur within generic methods, only the method name itself is used, without the type parameter list.</span></span>

<span data-ttu-id="280fe-360">Для вызовов, которые происходят в явные реализации члена интерфейса только само имя метода используется без предыдущем квалификацию интерфейса.</span><span class="sxs-lookup"><span data-stu-id="280fe-360">For invocations that occur within explicit interface member implementations, only the method name itself is used, without the preceding interface qualification.</span></span>

<span data-ttu-id="280fe-361">Для вызовов, возникающих в рамках методов доступа свойства или события используется имя члена, свойства или само событие.</span><span class="sxs-lookup"><span data-stu-id="280fe-361">For invocations that occur within property or event accessors, the member name used is that of the property or event itself.</span></span>

<span data-ttu-id="280fe-362">Для вызовов, возникающих в рамках методам доступа индексаторов, используется имя члена, предоставляемые `IndexerNameAttribute` ([атрибут IndexerName](attributes.md#the-indexername-attribute)) на элемент индексатора, если он имеется, или имя по умолчанию `Item` в противном случае.</span><span class="sxs-lookup"><span data-stu-id="280fe-362">For invocations that occur within indexer accessors, the member name used is that supplied by an `IndexerNameAttribute` ([The IndexerName attribute](attributes.md#the-indexername-attribute)) on the indexer member, if present, or the default name `Item` otherwise.</span></span>

<span data-ttu-id="280fe-363">Для вызовов, которые происходят в конструкторы экземпляров, статические конструкторы, деструкторы и операторы объявления члена имя, используемое зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="280fe-363">For invocations that occur within declarations of instance constructors, static constructors, destructors and operators the member name used is implementation-dependent.</span></span>

## <a name="attributes-for-interoperation"></a><span data-ttu-id="280fe-364">Атрибуты для взаимодействия</span><span class="sxs-lookup"><span data-stu-id="280fe-364">Attributes for Interoperation</span></span>

<span data-ttu-id="280fe-365">Примечание: Этот раздел применим только к реализации Microsoft .NET, C#.</span><span class="sxs-lookup"><span data-stu-id="280fe-365">Note: This section is applicable only to the Microsoft .NET implementation of C#.</span></span>

### <a name="interoperation-with-com-and-win32-components"></a><span data-ttu-id="280fe-366">Взаимодействие с компонентами COM и Win32</span><span class="sxs-lookup"><span data-stu-id="280fe-366">Interoperation with COM and Win32 components</span></span>

<span data-ttu-id="280fe-367">Время выполнения .NET предоставляет большое количество атрибутов, которые позволяют программы на C# для взаимодействия с компонентами, написанными на COM и библиотеки DLL Win32.</span><span class="sxs-lookup"><span data-stu-id="280fe-367">The .NET run-time provides a large number of attributes that enable C# programs to interoperate with components written using COM and Win32 DLLs.</span></span> <span data-ttu-id="280fe-368">Например `DllImport` атрибут может быть использован для `static extern` методу, чтобы показать, что метод реализуется в библиотеки DLL Win32.</span><span class="sxs-lookup"><span data-stu-id="280fe-368">For example, the `DllImport` attribute can be used on a `static extern` method to indicate that the implementation of the method is to be found in a Win32 DLL.</span></span> <span data-ttu-id="280fe-369">Эти атрибуты найдены в `System.Runtime.InteropServices` пространства имен и подробную документацию для этих атрибутов см. в документации среды выполнения .NET.</span><span class="sxs-lookup"><span data-stu-id="280fe-369">These attributes are found in the `System.Runtime.InteropServices` namespace, and detailed documentation for these attributes is found in the .NET runtime documentation.</span></span>

### <a name="interoperation-with-other-net-languages"></a><span data-ttu-id="280fe-370">Взаимодействие с другими языками .NET</span><span class="sxs-lookup"><span data-stu-id="280fe-370">Interoperation with other .NET languages</span></span>

#### <a name="the-indexername-attribute"></a><span data-ttu-id="280fe-371">Атрибут IndexerName</span><span class="sxs-lookup"><span data-stu-id="280fe-371">The IndexerName attribute</span></span>

<span data-ttu-id="280fe-372">Индексаторы реализованы в .NET с помощью индексированных свойств и иметь имя в метаданных .NET.</span><span class="sxs-lookup"><span data-stu-id="280fe-372">Indexers are implemented in .NET using indexed properties, and have a name in the .NET metadata.</span></span> <span data-ttu-id="280fe-373">Если не `IndexerName` присутствует атрибут для индексатора, а затем имя `Item` используется по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="280fe-373">If no `IndexerName` attribute is present for an indexer, then the name `Item` is used by default.</span></span> <span data-ttu-id="280fe-374">`IndexerName` Атрибут которой разработчики могут переопределить это поведение по умолчанию и указать другое имя.</span><span class="sxs-lookup"><span data-stu-id="280fe-374">The `IndexerName` attribute enables a developer to override this default and specify a different name.</span></span>

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
