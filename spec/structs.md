# <a name="structs"></a><span data-ttu-id="9f53a-101">Структуры</span><span class="sxs-lookup"><span data-stu-id="9f53a-101">Structs</span></span>

<span data-ttu-id="9f53a-102">Структуры похожи на классы, в том, что они представляют структуры данных, которые могут содержать данные-члены и функции-члены.</span><span class="sxs-lookup"><span data-stu-id="9f53a-102">Structs are similar to classes in that they represent data structures that can contain data members and function members.</span></span> <span data-ttu-id="9f53a-103">Тем не менее в отличие от классов, структуры являются типами значений и не требуется выделение кучи.</span><span class="sxs-lookup"><span data-stu-id="9f53a-103">However, unlike classes, structs are value types and do not require heap allocation.</span></span> <span data-ttu-id="9f53a-104">Переменная типа структура непосредственно содержит данные структуры, тогда как переменная типа класса содержит ссылку на данные, ранее известные как объект.</span><span class="sxs-lookup"><span data-stu-id="9f53a-104">A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.</span></span>

<span data-ttu-id="9f53a-105">Структуры особенно удобны для небольших структур данных, имеющих семантику значений.</span><span class="sxs-lookup"><span data-stu-id="9f53a-105">Structs are particularly useful for small data structures that have value semantics.</span></span> <span data-ttu-id="9f53a-106">Хорошими примерами структур можно считать комплексные числа, точки в системе координат или словари с парами ключ-значение.</span><span class="sxs-lookup"><span data-stu-id="9f53a-106">Complex numbers, points in a coordinate system, or key-value pairs in a dictionary are all good examples of structs.</span></span> <span data-ttu-id="9f53a-107">Ключ для этих структур данных является наличие нескольких переменных-членов, что они не требуют использования наследования или ссылочного идентификатора, и что их можно легко реализовать с использованием семантики значения, когда при присваивании копируется значение вместо ссылки на.</span><span class="sxs-lookup"><span data-stu-id="9f53a-107">Key to these data structures is that they have few data members, that they do not require use of inheritance or referential identity, and that they can be conveniently implemented using value semantics where assignment copies the value instead of the reference.</span></span>

<span data-ttu-id="9f53a-108">Как описано в разделе [простых типов](types.md#simple-types), простые типы, предоставляемые языком C#, таких как `int`, `double`, и `bool`, фактически являются все типы структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-108">As described in [Simple types](types.md#simple-types), the simple types provided by C#, such as `int`, `double`, and `bool`, are in fact all struct types.</span></span> <span data-ttu-id="9f53a-109">Так же, как эти предопределенные типы являются структурами, можно также использовать структуры и перегрузки операторов для реализации новых типов «primitive» на языке C#.</span><span class="sxs-lookup"><span data-stu-id="9f53a-109">Just as these predefined types are structs, it is also possible to use structs and operator overloading to implement new "primitive" types in the C# language.</span></span> <span data-ttu-id="9f53a-110">В конце этой главе приведены два примера таких типов ([примеры структур](structs.md#struct-examples)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-110">Two examples of such types are given at the end of this chapter ([Struct examples](structs.md#struct-examples)).</span></span>

## <a name="struct-declarations"></a><span data-ttu-id="9f53a-111">Объявления структур</span><span class="sxs-lookup"><span data-stu-id="9f53a-111">Struct declarations</span></span>

<span data-ttu-id="9f53a-112">Объект *struct_declaration* — *type_declaration* ([объявления типов](namespaces.md#type-declarations)), объявляется новая структура:</span><span class="sxs-lookup"><span data-stu-id="9f53a-112">A *struct_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new struct:</span></span>

```antlr
struct_declaration
    : attributes? struct_modifier* 'partial'? 'struct' identifier type_parameter_list?
      struct_interfaces? type_parameter_constraints_clause* struct_body ';'?
    ;
```

<span data-ttu-id="9f53a-113">Объект *struct_declaration* состоит из необязательного набора *атрибуты* ([атрибуты](attributes.md)), а затем необязательный набор *struct_modifier*s ([модификаторы структуры](structs.md#struct-modifiers)), а затем использовать необязательный `partial` модификатор, а затем с помощью ключевого слова `struct` и *идентификатор* , которая содержит название структуры, за которым следует Необязательный *type_parameter_list* спецификации ([параметры типа](classes.md#type-parameters)), а затем использовать необязательный *struct_interfaces* спецификации ([Модификатор partial](structs.md#partial-modifier))), а затем использовать необязательный *type_parameter_constraints_clause*спецификации s ([ограничения параметров типа](classes.md#type-parameter-constraints)), а затем *struct_body* ([основной части структуры](structs.md#struct-body)), при необходимости, а затем точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="9f53a-113">A *struct_declaration* consists of an optional set of *attributes* ([Attributes](attributes.md)), followed by an optional set of *struct_modifier*s ([Struct modifiers](structs.md#struct-modifiers)), followed by an optional `partial` modifier, followed by the keyword `struct` and an *identifier* that names the struct, followed by an optional *type_parameter_list* specification ([Type parameters](classes.md#type-parameters)), followed by an optional *struct_interfaces* specification ([Partial modifier](structs.md#partial-modifier)) ), followed by an optional *type_parameter_constraints_clause*s specification ([Type parameter constraints](classes.md#type-parameter-constraints)), followed by a *struct_body* ([Struct body](structs.md#struct-body)), optionally followed by a semicolon.</span></span>

### <a name="struct-modifiers"></a><span data-ttu-id="9f53a-114">Модификаторы структуры</span><span class="sxs-lookup"><span data-stu-id="9f53a-114">Struct modifiers</span></span>

<span data-ttu-id="9f53a-115">Объект *struct_declaration* может включать последовательность модификаторов структуры:</span><span class="sxs-lookup"><span data-stu-id="9f53a-115">A *struct_declaration* may optionally include a sequence of struct modifiers:</span></span>

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

<span data-ttu-id="9f53a-116">Это ошибка времени компиляции для один и тот же модификатор встречается несколько раз в объявлении структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-116">It is a compile-time error for the same modifier to appear multiple times in a struct declaration.</span></span>

<span data-ttu-id="9f53a-117">Модификаторы объявления структуры имеют одинаковое значение, что и объявление класса ([объявлений классов](classes.md#class-declarations)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-117">The modifiers of a struct declaration have the same meaning as those of a class declaration ([Class declarations](classes.md#class-declarations)).</span></span>

### <a name="partial-modifier"></a><span data-ttu-id="9f53a-118">Модификатор partial</span><span class="sxs-lookup"><span data-stu-id="9f53a-118">Partial modifier</span></span>

<span data-ttu-id="9f53a-119">`partial` Модификатор указывает, что это *struct_declaration* является объявлением разделяемого типа.</span><span class="sxs-lookup"><span data-stu-id="9f53a-119">The `partial` modifier indicates that this *struct_declaration* is a partial type declaration.</span></span> <span data-ttu-id="9f53a-120">Нескольких объявлениях разделяемой структуры с тем же именем в едином объявлении пространства имен или тип объединения для одно объявление структуры, следуя правилам указан в [разделяемых типов](classes.md#partial-types).</span><span class="sxs-lookup"><span data-stu-id="9f53a-120">Multiple partial struct declarations with the same name within an enclosing namespace or type declaration combine to form one struct declaration, following the rules specified in [Partial types](classes.md#partial-types).</span></span>

### <a name="struct-interfaces"></a><span data-ttu-id="9f53a-121">Интерфейсы структуры</span><span class="sxs-lookup"><span data-stu-id="9f53a-121">Struct interfaces</span></span>

<span data-ttu-id="9f53a-122">Объявление структуры может содержать *struct_interfaces* спецификации, в котором регистр структуры говорят, что прямая реализация заданные типы интерфейса.</span><span class="sxs-lookup"><span data-stu-id="9f53a-122">A struct declaration may include a *struct_interfaces* specification, in which case the struct is said to directly implement the given interface types.</span></span>

```antlr
struct_interfaces
    : ':' interface_type_list
    ;
```

<span data-ttu-id="9f53a-123">Реализация интерфейсов рассматривается далее в [реализации интерфейсов](interfaces.md#interface-implementations).</span><span class="sxs-lookup"><span data-stu-id="9f53a-123">Interface implementations are discussed further in [Interface implementations](interfaces.md#interface-implementations).</span></span>

### <a name="struct-body"></a><span data-ttu-id="9f53a-124">Основной части структуры</span><span class="sxs-lookup"><span data-stu-id="9f53a-124">Struct body</span></span>

<span data-ttu-id="9f53a-125">*Struct_body* структуры определяет членов структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-125">The *struct_body* of a struct defines the members of the struct.</span></span>

```antlr
struct_body
    : '{' struct_member_declaration* '}'
    ;
```

## <a name="struct-members"></a><span data-ttu-id="9f53a-126">Члены структуры</span><span class="sxs-lookup"><span data-stu-id="9f53a-126">Struct members</span></span>

<span data-ttu-id="9f53a-127">Члены структуры состоят из членов, представленных его *struct_member_declaration*s и члены, унаследованные от типа `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-127">The members of a struct consist of the members introduced by its *struct_member_declaration*s and the members inherited from the type `System.ValueType`.</span></span>

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

<span data-ttu-id="9f53a-128">За исключением различий, описанных в [различия классов и структур](structs.md#class-and-struct-differences), описания членов класса в [члены класса](classes.md#class-members) через [итераторы](classes.md#iterators) применяются к структуре а также элементы.</span><span class="sxs-lookup"><span data-stu-id="9f53a-128">Except for the differences noted in [Class and struct differences](structs.md#class-and-struct-differences), the descriptions of class members provided in [Class members](classes.md#class-members) through [Iterators](classes.md#iterators) apply to struct members as well.</span></span>

## <a name="class-and-struct-differences"></a><span data-ttu-id="9f53a-129">Различия классов и структур</span><span class="sxs-lookup"><span data-stu-id="9f53a-129">Class and struct differences</span></span>

<span data-ttu-id="9f53a-130">Структуры отличаются от классов в ряде важных аспектов:</span><span class="sxs-lookup"><span data-stu-id="9f53a-130">Structs differ from classes in several important ways:</span></span>

*  <span data-ttu-id="9f53a-131">Структуры являются типами значений ([значение семантику](structs.md#value-semantics)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-131">Structs are value types ([Value semantics](structs.md#value-semantics)).</span></span>
*  <span data-ttu-id="9f53a-132">Все типы структуры неявно наследуются от класса `System.ValueType` ([наследования](structs.md#inheritance)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-132">All struct types implicitly inherit from the class `System.ValueType` ([Inheritance](structs.md#inheritance)).</span></span>
*  <span data-ttu-id="9f53a-133">Присвоение переменной с типом структуры создается копия значения, присваиваемого ([назначения](structs.md#assignment)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-133">Assignment to a variable of a struct type creates a copy of the value being assigned ([Assignment](structs.md#assignment)).</span></span>
*  <span data-ttu-id="9f53a-134">Значение по умолчанию для структуры является значение, создаваемое путем установки все поля типа значения полей с типом значения по умолчанию и справочник по всем `null` ([значения по умолчанию](structs.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-134">The default value of a struct is the value produced by setting all value type fields to their default value and all reference type fields to `null` ([Default values](structs.md#default-values)).</span></span>
*  <span data-ttu-id="9f53a-135">Операции упаковки и распаковки используются для преобразования между типом структуры и `object` ([упаковка-преобразование и распаковка-преобразование](structs.md#boxing-and-unboxing)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-135">Boxing and unboxing operations are used to convert between a struct type and `object` ([Boxing and unboxing](structs.md#boxing-and-unboxing)).</span></span>
*  <span data-ttu-id="9f53a-136">Значение `this` отличается для структур ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-136">The meaning of `this` is different for structs ([This access](expressions.md#this-access)).</span></span>
*  <span data-ttu-id="9f53a-137">Объявления полей экземпляра для структуры не могут содержать инициализаторы переменных ([поле инициализаторы](structs.md#field-initializers)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-137">Instance field declarations for a struct are not permitted to include variable initializers ([Field initializers](structs.md#field-initializers)).</span></span>
*  <span data-ttu-id="9f53a-138">В структуре не разрешается объявлять конструктор экземпляров ([конструкторы](structs.md#constructors)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-138">A struct is not permitted to declare a parameterless instance constructor ([Constructors](structs.md#constructors)).</span></span>
*  <span data-ttu-id="9f53a-139">В структуре не разрешается объявить деструктор ([деструкторы](structs.md#destructors)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-139">A struct is not permitted to declare a destructor ([Destructors](structs.md#destructors)).</span></span>

### <a name="value-semantics"></a><span data-ttu-id="9f53a-140">Семантика значения</span><span class="sxs-lookup"><span data-stu-id="9f53a-140">Value semantics</span></span>

<span data-ttu-id="9f53a-141">Структуры являются типами значений ([типы значений](types.md#value-types)) к имеющих семантику значений.</span><span class="sxs-lookup"><span data-stu-id="9f53a-141">Structs are value types ([Value types](types.md#value-types)) and are said to have value semantics.</span></span> <span data-ttu-id="9f53a-142">Классы, с другой стороны, являются ссылочными типами ([ссылочные типы](types.md#reference-types)) и к семантики ссылок.</span><span class="sxs-lookup"><span data-stu-id="9f53a-142">Classes, on the other hand, are reference types ([Reference types](types.md#reference-types)) and are said to have reference semantics.</span></span>

<span data-ttu-id="9f53a-143">Переменная типа структура непосредственно содержит данные структуры, тогда как переменная типа класса содержит ссылку на данные, ранее известные как объект.</span><span class="sxs-lookup"><span data-stu-id="9f53a-143">A variable of a struct type directly contains the data of the struct, whereas a variable of a class type contains a reference to the data, the latter known as an object.</span></span> <span data-ttu-id="9f53a-144">Когда структура `B` содержит поле экземпляра типа `A` и `A` является типом структуры, это ошибка времени компиляции для `A` зависят от `B` или тип, сформированный из `B`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-144">When a struct `B` contains an instance field of type `A` and `A` is a struct type, it is a compile-time error for `A` to depend on `B` or a type constructed from `B`.</span></span> <span data-ttu-id="9f53a-145">Структура `X` ***напрямую зависит от*** структуры `Y` Если `X` содержит поле экземпляра типа `Y`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-145">A struct `X` ***directly depends on*** a struct `Y` if `X` contains an instance field of type `Y`.</span></span> <span data-ttu-id="9f53a-146">Рассмотрим следующее определение, полный набор структур, от которого зависит структура является транзитивное замыкание ***напрямую зависит от*** связи.</span><span class="sxs-lookup"><span data-stu-id="9f53a-146">Given this definition, the complete set of structs upon which a struct depends is the transitive closure of the ***directly depends on*** relationship.</span></span>  <span data-ttu-id="9f53a-147">Пример</span><span class="sxs-lookup"><span data-stu-id="9f53a-147">For example</span></span>
```csharp
struct Node
{
    int data;
    Node next; // error, Node directly depends on itself
}
```
<span data-ttu-id="9f53a-148">является ошибкой, поскольку `Node` содержит поле экземпляра его собственного типа.</span><span class="sxs-lookup"><span data-stu-id="9f53a-148">is an error because `Node` contains an instance field of its own type.</span></span>  <span data-ttu-id="9f53a-149">Другой пример</span><span class="sxs-lookup"><span data-stu-id="9f53a-149">Another example</span></span>
```csharp
struct A { B b; }

struct B { C c; }

struct C { A a; }
```
<span data-ttu-id="9f53a-150">является ошибкой, так как каждый из типов `A`, `B`, и `C` зависят друг от друга.</span><span class="sxs-lookup"><span data-stu-id="9f53a-150">is an error because each of the types `A`, `B`, and `C` depend on each other.</span></span>

<span data-ttu-id="9f53a-151">С классами это две переменные могут ссылаться на тот же объект и поэтому может случиться операции над одной переменной затронут объект, который ссылается другая переменная.</span><span class="sxs-lookup"><span data-stu-id="9f53a-151">With classes, it is possible for two variables to reference the same object, and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="9f53a-152">При использовании структур каждая переменная имеет свою собственную копию данных (в частности, за исключением `ref` и `out` переменных параметров), и операции над одной могут затрагивать другую невозможно.</span><span class="sxs-lookup"><span data-stu-id="9f53a-152">With structs, the variables each have their own copy of the data (except in the case of `ref` and `out` parameter variables), and it is not possible for operations on one to affect the other.</span></span> <span data-ttu-id="9f53a-153">Более того, так как структуры не являются ссылочными типами, он не поддерживается для значений типа структуры, чтобы быть `null`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-153">Furthermore, because structs are not reference types, it is not possible for values of a struct type to be `null`.</span></span>

<span data-ttu-id="9f53a-154">При объявлении</span><span class="sxs-lookup"><span data-stu-id="9f53a-154">Given the declaration</span></span>
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
<span data-ttu-id="9f53a-155">фрагмент кода</span><span class="sxs-lookup"><span data-stu-id="9f53a-155">the code fragment</span></span>
```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 100;
System.Console.WriteLine(b.x);
```
<span data-ttu-id="9f53a-156">Выводит значение `10`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-156">outputs the value `10`.</span></span> <span data-ttu-id="9f53a-157">Назначение `a` для `b` создает копию значения, и `b` , таким образом, не влияет на `a.x`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-157">The assignment of `a` to `b` creates a copy of the value, and `b` is thus unaffected by the assignment to `a.x`.</span></span> <span data-ttu-id="9f53a-158">Было `Point` вместо этого был объявлен как класс, выходные данные будут `100` поскольку `a` и `b` будет ссылаться на тот же объект.</span><span class="sxs-lookup"><span data-stu-id="9f53a-158">Had `Point` instead been declared as a class, the output would be `100` because `a` and `b` would reference the same object.</span></span>

### <a name="inheritance"></a><span data-ttu-id="9f53a-159">Наследование</span><span class="sxs-lookup"><span data-stu-id="9f53a-159">Inheritance</span></span>

<span data-ttu-id="9f53a-160">Все типы структуры неявно наследуются от класса `System.ValueType`, который, в свою очередь, наследует от класса `object`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-160">All struct types implicitly inherit from the class `System.ValueType`, which, in turn, inherits from class `object`.</span></span> <span data-ttu-id="9f53a-161">Объявление структуры может указать список реализованных интерфейсов, но он не поддерживается для объявления структуры, чтобы указать базовый класс.</span><span class="sxs-lookup"><span data-stu-id="9f53a-161">A struct declaration may specify a list of implemented interfaces, but it is not possible for a struct declaration to specify a base class.</span></span>

<span data-ttu-id="9f53a-162">Типы структуры никогда не является абстрактным и всегда неявно запечатаны.</span><span class="sxs-lookup"><span data-stu-id="9f53a-162">Struct types are never abstract and are always implicitly sealed.</span></span> <span data-ttu-id="9f53a-163">`abstract` И `sealed` модификаторы таким образом не разрешается использовать в объявлении структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-163">The `abstract` and `sealed` modifiers are therefore not permitted in a struct declaration.</span></span>

<span data-ttu-id="9f53a-164">Так как для структур не поддерживается наследование, объявленным уровнем доступности члена структуры не может быть `protected` или `protected internal`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-164">Since inheritance isn't supported for structs, the declared accessibility of a struct member cannot be `protected` or `protected internal`.</span></span>

<span data-ttu-id="9f53a-165">Функции-члены в структуре не может быть `abstract` или `virtual`и `override` модификатор может быть указан только в переопределите методы, унаследованные от `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-165">Function members in a struct cannot be `abstract` or `virtual`, and the `override` modifier is allowed only to override methods inherited from `System.ValueType`.</span></span>

### <a name="assignment"></a><span data-ttu-id="9f53a-166">Назначение</span><span class="sxs-lookup"><span data-stu-id="9f53a-166">Assignment</span></span>

<span data-ttu-id="9f53a-167">Присвоение переменной типа структуры создает копию значения, присваиваемого.</span><span class="sxs-lookup"><span data-stu-id="9f53a-167">Assignment to a variable of a struct type creates a copy of the value being assigned.</span></span> <span data-ttu-id="9f53a-168">В отличие от назначения переменной типа класса, который копирует ссылка, но не объект, указанный ссылкой.</span><span class="sxs-lookup"><span data-stu-id="9f53a-168">This differs from assignment to a variable of a class type, which copies the reference but not the object identified by the reference.</span></span>

<span data-ttu-id="9f53a-169">Аналогичным образом, переданный в качестве значения параметра или возвращаемые в результате функции-члена структуры, структуры создается копия.</span><span class="sxs-lookup"><span data-stu-id="9f53a-169">Similar to an assignment, when a struct is passed as a value parameter or returned as the result of a function member, a copy of the struct is created.</span></span> <span data-ttu-id="9f53a-170">Структура может передаваться по ссылке, чтобы с помощью функции-члена `ref` или `out` параметра.</span><span class="sxs-lookup"><span data-stu-id="9f53a-170">A struct may be passed by reference to a function member using a `ref` or `out` parameter.</span></span>

<span data-ttu-id="9f53a-171">Если свойство или индексатор структуры является целевым объектом назначения, выражение экземпляра, связанное с правами доступа свойства или индексатора должен классифицироваться как переменную.</span><span class="sxs-lookup"><span data-stu-id="9f53a-171">When a property or indexer of a struct is the target of an assignment, the instance expression associated with the property or indexer access must be classified as a variable.</span></span> <span data-ttu-id="9f53a-172">Если экземпляр выражение классифицируется как значение, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="9f53a-172">If the instance expression is classified as a value, a compile-time error occurs.</span></span> <span data-ttu-id="9f53a-173">Это описано более подробно [простое присваивание](expressions.md#simple-assignment).</span><span class="sxs-lookup"><span data-stu-id="9f53a-173">This is described in further detail in [Simple assignment](expressions.md#simple-assignment).</span></span>

### <a name="default-values"></a><span data-ttu-id="9f53a-174">Значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="9f53a-174">Default values</span></span>

<span data-ttu-id="9f53a-175">Как описано в разделе [значения по умолчанию](variables.md#default-values), несколько типов переменных автоматически инициализируются значениями по умолчанию, при их создании.</span><span class="sxs-lookup"><span data-stu-id="9f53a-175">As described in [Default values](variables.md#default-values), several kinds of variables are automatically initialized to their default value when they are created.</span></span> <span data-ttu-id="9f53a-176">Для переменных типов классов и других ссылочных типов это значение по умолчанию — `null`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-176">For variables of class types and other reference types, this default value is `null`.</span></span> <span data-ttu-id="9f53a-177">Тем не менее поскольку структуры являются типами значений, которые не могут быть `null`, значение по умолчанию для структуры является значение, создаваемое путем установки все поля типа значения полей с типом значения по умолчанию и справочник по всем `null`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-177">However, since structs are value types that cannot be `null`, the default value of a struct is the value produced by setting all value type fields to their default value and all reference type fields to `null`.</span></span>

<span data-ttu-id="9f53a-178">Ссылка на `Point` структуры, объявленные выше, пример</span><span class="sxs-lookup"><span data-stu-id="9f53a-178">Referring to the `Point` struct declared above, the example</span></span>
```csharp
Point[] a = new Point[100];
```
<span data-ttu-id="9f53a-179">присваивает каждой из них `Point` массива значение, создаваемое путем установки `x` и `y` поля до нуля.</span><span class="sxs-lookup"><span data-stu-id="9f53a-179">initializes each `Point` in the array to the value produced by setting the `x` and `y` fields to zero.</span></span>

<span data-ttu-id="9f53a-180">Значение по умолчанию структура соответствует равным значению, возвращенному конструктором по умолчанию структуры ([конструкторы по умолчанию](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-180">The default value of a struct corresponds to the value returned by the default constructor of the struct ([Default constructors](types.md#default-constructors)).</span></span> <span data-ttu-id="9f53a-181">В отличие от класса структуры не допускается объявление конструктора экземпляра без параметров.</span><span class="sxs-lookup"><span data-stu-id="9f53a-181">Unlike a class, a struct is not permitted to declare a parameterless instance constructor.</span></span> <span data-ttu-id="9f53a-182">Вместо этого каждая структура неявно содержит конструктор экземпляра без параметров, который всегда возвращает значение, полученное путем установки значения по умолчанию и справочник по всем все поля типа значения для полей с типом `null`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-182">Instead, every struct implicitly has a parameterless instance constructor which always returns the value that results from setting all value type fields to their default value and all reference type fields to `null`.</span></span>

<span data-ttu-id="9f53a-183">Структуры должны разрабатываться необходимо учитывать состояние инициализации по умолчанию в недопустимом состоянии.</span><span class="sxs-lookup"><span data-stu-id="9f53a-183">Structs should be designed to consider the default initialization state a valid state.</span></span> <span data-ttu-id="9f53a-184">В примере</span><span class="sxs-lookup"><span data-stu-id="9f53a-184">In the example</span></span>
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
<span data-ttu-id="9f53a-185">конструктор экземпляра, определяемые пользователем обеспечивает защиту от значения null, только она была явно вызвана.</span><span class="sxs-lookup"><span data-stu-id="9f53a-185">the user-defined instance constructor protects against null values only where it is explicitly called.</span></span> <span data-ttu-id="9f53a-186">В случаях, где `KeyValuePair` переменной регулируется инициализации значений по умолчанию — `key` и `value` поля будет иметь значение null, и структуры должны быть готовы обрабатывать это состояние.</span><span class="sxs-lookup"><span data-stu-id="9f53a-186">In cases where a `KeyValuePair` variable is subject to default value initialization, the `key` and `value` fields will be null, and the struct must be prepared to handle this state.</span></span>

### <a name="boxing-and-unboxing"></a><span data-ttu-id="9f53a-187">Упаковка-преобразование и распаковка-преобразование</span><span class="sxs-lookup"><span data-stu-id="9f53a-187">Boxing and unboxing</span></span>

<span data-ttu-id="9f53a-188">Значение типа класса можно преобразовать в тип `object` или к типу интерфейса, который реализуется с помощью класса просто обработка ссылки в виде другого типа во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="9f53a-188">A value of a class type can be converted to type `object` or to an interface type that is implemented by the class simply by treating the reference as another type at compile-time.</span></span> <span data-ttu-id="9f53a-189">Аналогичным образом, значение типа `object` или значение типа интерфейса могут преобразовываться к типу класса без изменения ссылки (но безусловно проверку типов во время выполнения необходим в данном случае).</span><span class="sxs-lookup"><span data-stu-id="9f53a-189">Likewise, a value of type `object` or a value of an interface type can be converted back to a class type without changing the reference (but of course a run-time type check is required in this case).</span></span>

<span data-ttu-id="9f53a-190">Так как структуры не являются ссылочными типами, эти операции реализованы по-разному для типов структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-190">Since structs are not reference types, these operations are implemented differently for struct types.</span></span> <span data-ttu-id="9f53a-191">Если значение с типом структуры преобразуется в тип `object` или к типу интерфейса, реализуемого классом структуры, выполняется операция упаковки-преобразования.</span><span class="sxs-lookup"><span data-stu-id="9f53a-191">When a value of a struct type is converted to type `object` or to an interface type that is implemented by the struct, a boxing operation takes place.</span></span> <span data-ttu-id="9f53a-192">Аналогично когда значение типа `object` или значение типа интерфейса преобразуется к типу структуры, выполняется операция распаковки.</span><span class="sxs-lookup"><span data-stu-id="9f53a-192">Likewise, when a value of type `object` or a value of an interface type is converted back to a struct type, an unboxing operation takes place.</span></span> <span data-ttu-id="9f53a-193">Ключевое отличие от одинаковых операций для типов классов является то, что упаковка-преобразование и распаковка-преобразование копирует значение структуры в или из упакованного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="9f53a-193">A key difference from the same operations on class types is that boxing and unboxing copies the struct value either into or out of the boxed instance.</span></span> <span data-ttu-id="9f53a-194">Таким образом после операции упаковки или распаковки, изменения, внесенные в распакованную структуру не отражаются в упакованной структуре.</span><span class="sxs-lookup"><span data-stu-id="9f53a-194">Thus, following a boxing or unboxing operation, changes made to the unboxed struct are not reflected in the boxed struct.</span></span>

<span data-ttu-id="9f53a-195">Когда типом структуры переопределяет виртуальный метод, который наследуется от `System.Object` (такие как `Equals`, `GetHashCode`, или `ToString`), вызов виртуального метода в экземпляре типа структуры не приводит к выполнению упаковки.</span><span class="sxs-lookup"><span data-stu-id="9f53a-195">When a struct type overrides a virtual method inherited from `System.Object` (such as `Equals`, `GetHashCode`, or `ToString`), invocation of the virtual method through an instance of the struct type does not cause boxing to occur.</span></span> <span data-ttu-id="9f53a-196">Это верно даже в том случае, когда структура используется в качестве параметра типа, если вызов происходит через экземпляр параметра типа.</span><span class="sxs-lookup"><span data-stu-id="9f53a-196">This is true even when the struct is used as a type parameter and the invocation occurs through an instance of the type parameter type.</span></span> <span data-ttu-id="9f53a-197">Пример:</span><span class="sxs-lookup"><span data-stu-id="9f53a-197">For example:</span></span>
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

<span data-ttu-id="9f53a-198">Выходные данные программы будут:</span><span class="sxs-lookup"><span data-stu-id="9f53a-198">The output of the program is:</span></span>
```
1
2
3
```

<span data-ttu-id="9f53a-199">Несмотря на то, что он является плохим стилем `ToString` побочными эффектами, в примере показано, что упаковка-преобразование не место для трех вызовов функции `x.ToString()`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-199">Although it is bad style for `ToString` to have side effects, the example demonstrates that no boxing occurred for the three invocations of `x.ToString()`.</span></span>

<span data-ttu-id="9f53a-200">Аналогичным образом выполняется упаковка-преобразование не неявно при доступе к члену в параметр типа с ограничением.</span><span class="sxs-lookup"><span data-stu-id="9f53a-200">Similarly, boxing never implicitly occurs when accessing a member on a constrained type parameter.</span></span> <span data-ttu-id="9f53a-201">Например, предположим, что интерфейс `ICounter` содержит метод `Increment` которого может использоваться для изменения значения.</span><span class="sxs-lookup"><span data-stu-id="9f53a-201">For example, suppose an interface `ICounter` contains a method `Increment` which can be used to modify a value.</span></span> <span data-ttu-id="9f53a-202">Если `ICounter` используется в качестве ограничения, реализация `Increment` метод вызывается со ссылкой на переменную, `Increment` был вызван для никогда не упакованной копии.</span><span class="sxs-lookup"><span data-stu-id="9f53a-202">If `ICounter` is used as a constraint, the implementation of the `Increment` method is called with a reference to the variable that `Increment` was called on, never a boxed copy.</span></span>

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

<span data-ttu-id="9f53a-203">Первый вызов `Increment` изменяет значение в переменной `x`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-203">The first call to `Increment` modifies the value in the variable `x`.</span></span> <span data-ttu-id="9f53a-204">Это эквивалентно не второй вызов `Increment`, который изменяет значение в упакованной копии `x`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-204">This is not equivalent to the second call to `Increment`, which modifies the value in a boxed copy of `x`.</span></span> <span data-ttu-id="9f53a-205">Таким образом программы выводится следующий результат:</span><span class="sxs-lookup"><span data-stu-id="9f53a-205">Thus, the output of the program is:</span></span>
```
0
1
1
```

<span data-ttu-id="9f53a-206">Дополнительные сведения об упаковке и распаковке см. в разделе [упаковка-преобразование и распаковка-преобразование](types.md#boxing-and-unboxing).</span><span class="sxs-lookup"><span data-stu-id="9f53a-206">For further details on boxing and unboxing, see [Boxing and unboxing](types.md#boxing-and-unboxing).</span></span>

### <a name="meaning-of-this"></a><span data-ttu-id="9f53a-207">Это значение</span><span class="sxs-lookup"><span data-stu-id="9f53a-207">Meaning of this</span></span>

<span data-ttu-id="9f53a-208">В конструкторе экземпляра или экземпляра функцию-член класса `this` классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="9f53a-208">Within an instance constructor or instance function member of a class, `this` is classified as a value.</span></span> <span data-ttu-id="9f53a-209">Таким образом, хотя `this` может использоваться для ссылки на экземпляр для которого функция-член вызывается, он уже не сможете назначить `this` в функции-члене класса.</span><span class="sxs-lookup"><span data-stu-id="9f53a-209">Thus, while `this` can be used to refer to the instance for which the function member was invoked, it is not possible to assign to `this` in a function member of a class.</span></span>

<span data-ttu-id="9f53a-210">В конструкторе экземпляра структуры `this` соответствует `out` параметра типа структуры и в функции-члене экземпляра структуры, `this` соответствует `ref` параметр типа структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-210">Within an instance constructor of a struct, `this` corresponds to an `out` parameter of the struct type, and within an instance function member of a struct, `this` corresponds to a `ref` parameter of the struct type.</span></span> <span data-ttu-id="9f53a-211">В обоих случаях `this` классифицируется как переменная, и можно изменить всю структуру, для которого была вызвана функция-член, назначив `this` или путем передачи его в виде `ref` или `out` параметра.</span><span class="sxs-lookup"><span data-stu-id="9f53a-211">In both cases, `this` is classified as a variable, and it is possible to modify the entire struct for which the function member was invoked by assigning to `this` or by passing this as a `ref` or `out` parameter.</span></span>

### <a name="field-initializers"></a><span data-ttu-id="9f53a-212">Инициализаторы полей</span><span class="sxs-lookup"><span data-stu-id="9f53a-212">Field initializers</span></span>

<span data-ttu-id="9f53a-213">Как описано в разделе [значения по умолчанию](structs.md#default-values), значение по умолчанию структура состоит из значения, полученный в результате установки все значения полей с типом значения по умолчанию и справочник по всем полей с типом `null`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-213">As described in [Default values](structs.md#default-values), the default value of a struct consists of the value that results from setting all value type fields to their default value and all reference type fields to `null`.</span></span> <span data-ttu-id="9f53a-214">По этой причине структуры не допускает объявления полей экземпляра содержать инициализаторы переменных.</span><span class="sxs-lookup"><span data-stu-id="9f53a-214">For this reason, a struct does not permit instance field declarations to include variable initializers.</span></span> <span data-ttu-id="9f53a-215">Это ограничение применяется только к полям экземпляра.</span><span class="sxs-lookup"><span data-stu-id="9f53a-215">This restriction applies only to instance fields.</span></span> <span data-ttu-id="9f53a-216">Статические поля структуры могут содержать инициализаторы переменных.</span><span class="sxs-lookup"><span data-stu-id="9f53a-216">Static fields of a struct are permitted to include variable initializers.</span></span>

<span data-ttu-id="9f53a-217">Пример</span><span class="sxs-lookup"><span data-stu-id="9f53a-217">The example</span></span>
```csharp
struct Point
{
    public int x = 1;  // Error, initializer not permitted
    public int y = 1;  // Error, initializer not permitted
}
```
<span data-ttu-id="9f53a-218">— Ошибка, так как объявления полей экземпляра содержат инициализаторы переменных.</span><span class="sxs-lookup"><span data-stu-id="9f53a-218">is in error because the instance field declarations include variable initializers.</span></span>

### <a name="constructors"></a><span data-ttu-id="9f53a-219">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="9f53a-219">Constructors</span></span>

<span data-ttu-id="9f53a-220">В отличие от класса структуры не допускается объявление конструктора экземпляра без параметров.</span><span class="sxs-lookup"><span data-stu-id="9f53a-220">Unlike a class, a struct is not permitted to declare a parameterless instance constructor.</span></span> <span data-ttu-id="9f53a-221">Вместо этого каждая структура неявно содержит конструктор экземпляра без параметров, который всегда возвращает значение, полученное путем установки значения по умолчанию и справочник по всем поля типа значения NULL все поля типа значения ([Конструкторыпоумолчанию](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-221">Instead, every struct implicitly has a parameterless instance constructor which always returns the value that results from setting all value type fields to their default value and all reference type fields to null ([Default constructors](types.md#default-constructors)).</span></span> <span data-ttu-id="9f53a-222">В структуре можно объявлять конструкторы экземпляров с параметрами.</span><span class="sxs-lookup"><span data-stu-id="9f53a-222">A struct can declare instance constructors having parameters.</span></span> <span data-ttu-id="9f53a-223">Пример</span><span class="sxs-lookup"><span data-stu-id="9f53a-223">For example</span></span>
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

<span data-ttu-id="9f53a-224">При объявлении выше, операторы</span><span class="sxs-lookup"><span data-stu-id="9f53a-224">Given the above declaration, the statements</span></span>
```csharp
Point p1 = new Point();
Point p2 = new Point(0, 0);
```
<span data-ttu-id="9f53a-225">они создают `Point` с `x` и `y` приравнивается к нулю.</span><span class="sxs-lookup"><span data-stu-id="9f53a-225">both create a `Point` with `x` and `y` initialized to zero.</span></span>

<span data-ttu-id="9f53a-226">Конструктор экземпляра структуры не может содержать инициализатор конструктора формы `base(...)`.</span><span class="sxs-lookup"><span data-stu-id="9f53a-226">A struct instance constructor is not permitted to include a constructor initializer of the form `base(...)`.</span></span>

<span data-ttu-id="9f53a-227">Если конструктор экземпляра структуры не указан инициализатор конструктора `this` переменная соответствует `out` параметр типа структуры и точно так же `out` параметра `this` должен быть явно присвоен () [Определенного присваивания](variables.md#definite-assignment)) в каждом месте, где Возвращает конструктор.</span><span class="sxs-lookup"><span data-stu-id="9f53a-227">If the struct instance constructor doesn't specify a constructor initializer, the `this` variable corresponds to an `out` parameter of the struct type, and similar to an `out` parameter, `this` must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) at every location where the constructor returns.</span></span> <span data-ttu-id="9f53a-228">Если конструктор экземпляра структуры указан инициализатор конструктора `this` переменная соответствует `ref` параметр типа структуры и точно так же `ref` параметра `this` считается определенно присвоенной на запись в тело конструктора.</span><span class="sxs-lookup"><span data-stu-id="9f53a-228">If the struct instance constructor specifies a constructor initializer, the `this` variable corresponds to a `ref` parameter of the struct type, and similar to a `ref` parameter, `this` is considered definitely assigned on entry to the constructor body.</span></span> <span data-ttu-id="9f53a-229">Рассмотрим приведенную ниже реализацию конструктора:</span><span class="sxs-lookup"><span data-stu-id="9f53a-229">Consider the instance constructor implementation below:</span></span>
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

<span data-ttu-id="9f53a-230">Функция-член не экземпляр (включая методы доступа set для свойства `X` и `Y`) может быть вызван, пока все поля структуры были определенно назначены.</span><span class="sxs-lookup"><span data-stu-id="9f53a-230">No instance member function (including the set accessors for the properties `X` and `Y`) can be called until all fields of the struct being constructed have been definitely assigned.</span></span> <span data-ttu-id="9f53a-231">Единственное исключение включает автоматически реализуемые свойства ([автоматически реализуемые свойства](classes.md#automatically-implemented-properties)).</span><span class="sxs-lookup"><span data-stu-id="9f53a-231">The only exception involves automatically implemented properties ([Automatically implemented properties](classes.md#automatically-implemented-properties)).</span></span> <span data-ttu-id="9f53a-232">Правила определенного назначения ([простые выражения присваивания](variables.md#simple-assignment-expressions)) специально исключать назначения для автосвойства с типом структуры внутри конструктора экземпляра этого типа структуры: такое присваивание считается определенного Назначение скрытые резервное поле свойства автоматически.</span><span class="sxs-lookup"><span data-stu-id="9f53a-232">The definite assignment rules ([Simple assignment expressions](variables.md#simple-assignment-expressions)) specifically exempt assignment to an auto-property of a struct type within an instance constructor of that struct type: such an assignment is considered a definite assignment of the hidden backing field of the auto-property.</span></span> <span data-ttu-id="9f53a-233">Таким образом следующее является допустимым:</span><span class="sxs-lookup"><span data-stu-id="9f53a-233">Thus, the following is allowed:</span></span>

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

### <a name="destructors"></a><span data-ttu-id="9f53a-234">Деструкторы</span><span class="sxs-lookup"><span data-stu-id="9f53a-234">Destructors</span></span>

<span data-ttu-id="9f53a-235">В структуре не разрешается объявить деструктор.</span><span class="sxs-lookup"><span data-stu-id="9f53a-235">A struct is not permitted to declare a destructor.</span></span>

### <a name="static-constructors"></a><span data-ttu-id="9f53a-236">Статические конструкторы</span><span class="sxs-lookup"><span data-stu-id="9f53a-236">Static constructors</span></span>

<span data-ttu-id="9f53a-237">Статические конструкторы для структур выполните большую часть тех же правил, и для классов.</span><span class="sxs-lookup"><span data-stu-id="9f53a-237">Static constructors for structs follow most of the same rules as for classes.</span></span> <span data-ttu-id="9f53a-238">Выполнение статического конструктора структуры запускается первым из следующих событий в домене приложения:</span><span class="sxs-lookup"><span data-stu-id="9f53a-238">The execution of a static constructor for a struct type is triggered by the first of the following events to occur within an application domain:</span></span>

*  <span data-ttu-id="9f53a-239">Статический член типа структуры есть ссылки.</span><span class="sxs-lookup"><span data-stu-id="9f53a-239">A static member of the struct type is referenced.</span></span>
*  <span data-ttu-id="9f53a-240">Вызывается явно объявленный конструктор типа структуры.</span><span class="sxs-lookup"><span data-stu-id="9f53a-240">An explicitly declared constructor of the struct type is called.</span></span>

<span data-ttu-id="9f53a-241">Создание значений по умолчанию ([значения по умолчанию](structs.md#default-values)) типы структуры не вызывает статический конструктор.</span><span class="sxs-lookup"><span data-stu-id="9f53a-241">The creation of default values ([Default values](structs.md#default-values)) of struct types does not trigger the static constructor.</span></span> <span data-ttu-id="9f53a-242">(Примером этого является начальное значение элементов в массиве).</span><span class="sxs-lookup"><span data-stu-id="9f53a-242">(An example of this is the initial value of elements in an array.)</span></span>

## <a name="struct-examples"></a><span data-ttu-id="9f53a-243">Примеры структур</span><span class="sxs-lookup"><span data-stu-id="9f53a-243">Struct examples</span></span>

<span data-ttu-id="9f53a-244">Далее показано два примера использования `struct` типов, которые могут использоваться аналогичным образом в предопределенных типов языка, но имеют измененную семантику типов.</span><span class="sxs-lookup"><span data-stu-id="9f53a-244">The following shows two significant examples of using `struct` types to create types that can be used similarly to the predefined types of the language, but with modified semantics.</span></span>

### <a name="database-integer-type"></a><span data-ttu-id="9f53a-245">Целочисленный тип базы данных</span><span class="sxs-lookup"><span data-stu-id="9f53a-245">Database integer type</span></span>

<span data-ttu-id="9f53a-246">`DBInt` Ниже структура реализует целочисленный тип, который может представлять полный набор значений `int` тип, а также дополнительное состояние, указывающее на неизвестное значение.</span><span class="sxs-lookup"><span data-stu-id="9f53a-246">The `DBInt` struct below implements an integer type that can represent the complete set of values of the `int` type, plus an additional state that indicates an unknown value.</span></span> <span data-ttu-id="9f53a-247">Тип с такими характеристиками обычно используется в базах данных.</span><span class="sxs-lookup"><span data-stu-id="9f53a-247">A type with these characteristics is commonly used in databases.</span></span>

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

### <a name="database-boolean-type"></a><span data-ttu-id="9f53a-248">Логический тип базы данных</span><span class="sxs-lookup"><span data-stu-id="9f53a-248">Database boolean type</span></span>

<span data-ttu-id="9f53a-249">`DBBool` Ниже структура реализует три значения логического типа.</span><span class="sxs-lookup"><span data-stu-id="9f53a-249">The `DBBool` struct below implements a three-valued logical type.</span></span> <span data-ttu-id="9f53a-250">Возможные значения этого типа: `DBBool.True`, `DBBool.False`, и `DBBool.Null`, где `Null` элемент указывает неизвестное значение.</span><span class="sxs-lookup"><span data-stu-id="9f53a-250">The possible values of this type are `DBBool.True`, `DBBool.False`, and `DBBool.Null`, where the `Null` member indicates an unknown value.</span></span> <span data-ttu-id="9f53a-251">Такие троичную логические типы обычно используются в базах данных.</span><span class="sxs-lookup"><span data-stu-id="9f53a-251">Such three-valued logical types are commonly used in databases.</span></span>

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
