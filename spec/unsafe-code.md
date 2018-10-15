# <a name="unsafe-code"></a><span data-ttu-id="bcef1-101">Небезопасный код</span><span class="sxs-lookup"><span data-stu-id="bcef1-101">Unsafe code</span></span>

<span data-ttu-id="bcef1-102">Core язык C#, как определено в предыдущих главах, заметно отличается от C и C++ в нем не используются указателей с типом данных.</span><span class="sxs-lookup"><span data-stu-id="bcef1-102">The core C# language, as defined in the preceding chapters, differs notably from C and C++ in its omission of pointers as a data type.</span></span> <span data-ttu-id="bcef1-103">Вместо этого C# предоставляет ссылки и возможность создавать объекты, которые управляются сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="bcef1-103">Instead, C# provides references and the ability to create objects that are managed by a garbage collector.</span></span> <span data-ttu-id="bcef1-104">Эта разработка в сочетании с другими компонентами, делает C# гораздо безопаснее язык, чем C или C++.</span><span class="sxs-lookup"><span data-stu-id="bcef1-104">This design, coupled with other features, makes C# a much safer language than C or C++.</span></span> <span data-ttu-id="bcef1-105">В базовом языке C# это просто не могут существовать неинициализированной переменной, «несвязанные» указатель или выражение, который индексирует массив за пределами границ элемента.</span><span class="sxs-lookup"><span data-stu-id="bcef1-105">In the core C# language it is simply not possible to have an uninitialized variable, a "dangling" pointer, or an expression that indexes an array beyond its bounds.</span></span> <span data-ttu-id="bcef1-106">Целые категории ошибок, регулярно подвержены C и C++ программы таким образом устраняются.</span><span class="sxs-lookup"><span data-stu-id="bcef1-106">Whole categories of bugs that routinely plague C and C++ programs are thus eliminated.</span></span>

<span data-ttu-id="bcef1-107">Хотя практически любого конструкции с типом указателя в C или C++ имеет аналог ссылочного типа в C#, тем не менее, существуют ситуации, где доступ к типам указатель становится необходимостью.</span><span class="sxs-lookup"><span data-stu-id="bcef1-107">While practically every pointer type construct in C or C++ has a reference type counterpart in C#, nonetheless, there are situations where access to pointer types becomes a necessity.</span></span> <span data-ttu-id="bcef1-108">Например взаимодействие с базовой операционной системы, доступ к устройству, размещенный в памяти или реализации критичных по времени алгоритм может оказаться возможно или целесообразно без доступа к указателям.</span><span class="sxs-lookup"><span data-stu-id="bcef1-108">For example, interfacing with the underlying operating system, accessing a memory-mapped device, or implementing a time-critical algorithm may not be possible or practical without access to pointers.</span></span> <span data-ttu-id="bcef1-109">Для решения этой задачи, C# предоставляет возможность записи ***небезопасный код***.</span><span class="sxs-lookup"><span data-stu-id="bcef1-109">To address this need, C# provides the ability to write ***unsafe code***.</span></span>

<span data-ttu-id="bcef1-110">В небезопасном коде можно объявить и использовать для указателей, для выполнения преобразований между указателями и целочисленных типов, для получения адреса переменных и т. д.</span><span class="sxs-lookup"><span data-stu-id="bcef1-110">In unsafe code it is possible to declare and operate on pointers, to perform conversions between pointers and integral types, to take the address of variables, and so forth.</span></span> <span data-ttu-id="bcef1-111">В некотором смысле написание небезопасного кода аналогично написание кода C помощью программы C#.</span><span class="sxs-lookup"><span data-stu-id="bcef1-111">In a sense, writing unsafe code is much like writing C code within a C# program.</span></span>

<span data-ttu-id="bcef1-112">Небезопасный код на самом деле является компонентом «безопасных» с точки зрения разработчиков и пользователей.</span><span class="sxs-lookup"><span data-stu-id="bcef1-112">Unsafe code is in fact a "safe" feature from the perspective of both developers and users.</span></span> <span data-ttu-id="bcef1-113">Небезопасный код должен быть явно помечен модификатором `unsafe`, поэтому разработчики не может использовать небезопасные возможности случайно и механизм выполнения убедитесь, что небезопасный код не может быть выполнена в ненадежной среде.</span><span class="sxs-lookup"><span data-stu-id="bcef1-113">Unsafe code must be clearly marked with the modifier `unsafe`, so developers can't possibly use unsafe features accidentally, and the execution engine works to ensure that unsafe code cannot be executed in an untrusted environment.</span></span>

## <a name="unsafe-contexts"></a><span data-ttu-id="bcef1-114">Небезопасные контексты</span><span class="sxs-lookup"><span data-stu-id="bcef1-114">Unsafe contexts</span></span>

<span data-ttu-id="bcef1-115">Небезопасные возможности C# доступны только в небезопасных контекстах.</span><span class="sxs-lookup"><span data-stu-id="bcef1-115">The unsafe features of C# are available only in unsafe contexts.</span></span> <span data-ttu-id="bcef1-116">Небезопасный контекст вводится путем включения `unsafe` модификатор в объявлении типа или члена, или создав *unsafe_statement*:</span><span class="sxs-lookup"><span data-stu-id="bcef1-116">An unsafe context is introduced by including an `unsafe` modifier in the declaration of a type or member, or by employing an *unsafe_statement*:</span></span>

*  <span data-ttu-id="bcef1-117">Объявление класса, структуры, интерфейса или делегата может включать `unsafe` модификатор, в этом случае все текстовое пространство этого объявления (включая тело класса, структуры или интерфейса) считается небезопасным контекстом.</span><span class="sxs-lookup"><span data-stu-id="bcef1-117">A declaration of a class, struct, interface, or delegate may include an `unsafe` modifier, in which case the entire textual extent of that type declaration (including the body of the class, struct, or interface) is considered an unsafe context.</span></span>
*  <span data-ttu-id="bcef1-118">Объявление поля, метода, свойства, события, индексатор, оператор, конструктор экземпляра, деструктор или статический конструктор может включать `unsafe` модификатор, в этом случае все текстовое пространство этого объявления члена считается небезопасный контекст.</span><span class="sxs-lookup"><span data-stu-id="bcef1-118">A declaration of a field, method, property, event, indexer, operator, instance constructor, destructor, or static constructor may include an `unsafe` modifier, in which case the entire textual extent of that member declaration is considered an unsafe context.</span></span>
*  <span data-ttu-id="bcef1-119">*Unsafe_statement* позволяет использовать в небезопасном контексте *блок*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-119">An *unsafe_statement* enables the use of an unsafe context within a *block*.</span></span> <span data-ttu-id="bcef1-120">Все текстовое пространство связанного *блок* считается небезопасным контекстом.</span><span class="sxs-lookup"><span data-stu-id="bcef1-120">The entire textual extent of the associated *block* is considered an unsafe context.</span></span>

<span data-ttu-id="bcef1-121">Ниже приведены соответствующие грамматические производства.</span><span class="sxs-lookup"><span data-stu-id="bcef1-121">The associated grammar productions are shown below.</span></span>

```antlr
class_modifier_unsafe
    : 'unsafe'
    ;

struct_modifier_unsafe
    : 'unsafe'
    ;

interface_modifier_unsafe
    : 'unsafe'
    ;

delegate_modifier_unsafe
    : 'unsafe'
    ;

field_modifier_unsafe
    : 'unsafe'
    ;

method_modifier_unsafe
    : 'unsafe'
    ;

property_modifier_unsafe
    : 'unsafe'
    ;

event_modifier_unsafe
    : 'unsafe'
    ;

indexer_modifier_unsafe
    : 'unsafe'
    ;

operator_modifier_unsafe
    : 'unsafe'
    ;

constructor_modifier_unsafe
    : 'unsafe'
    ;

destructor_declaration_unsafe
    : attributes? 'extern'? 'unsafe'? '~' identifier '(' ')' destructor_body
    | attributes? 'unsafe'? 'extern'? '~' identifier '(' ')' destructor_body
    ;

static_constructor_modifiers_unsafe
    : 'extern'? 'unsafe'? 'static'
    | 'unsafe'? 'extern'? 'static'
    | 'extern'? 'static' 'unsafe'?
    | 'unsafe'? 'static' 'extern'?
    | 'static' 'extern'? 'unsafe'?
    | 'static' 'unsafe'? 'extern'?
    ;

embedded_statement_unsafe
    : unsafe_statement
    | fixed_statement
    ;

unsafe_statement
    : 'unsafe' block
    ;
```

<span data-ttu-id="bcef1-122">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-122">In the example</span></span>

```csharp
public unsafe struct Node
{
    public int Value;
    public Node* Left;
    public Node* Right;
}
```

<span data-ttu-id="bcef1-123">`unsafe` модификатор, указанный в объявлении структуры вызывает все текстовое пространство объявления структуры небезопасным контекстом.</span><span class="sxs-lookup"><span data-stu-id="bcef1-123">the `unsafe` modifier specified in the struct declaration causes the entire textual extent of the struct declaration to become an unsafe context.</span></span> <span data-ttu-id="bcef1-124">Таким образом, можно объявить `Left` и `Right` поля с типом указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-124">Thus, it is possible to declare the `Left` and `Right` fields to be of a pointer type.</span></span> <span data-ttu-id="bcef1-125">Приведенный выше пример можно переписать</span><span class="sxs-lookup"><span data-stu-id="bcef1-125">The example above could also be written</span></span>

```csharp
public struct Node
{
    public int Value;
    public unsafe Node* Left;
    public unsafe Node* Right;
}
```

<span data-ttu-id="bcef1-126">Здесь `unsafe` модификаторы в объявлениях полей делают эти объявления небезопасными контекстами.</span><span class="sxs-lookup"><span data-stu-id="bcef1-126">Here, the `unsafe` modifiers in the field declarations cause those declarations to be considered unsafe contexts.</span></span>

<span data-ttu-id="bcef1-127">Кроме установки небезопасный контекст, дающего возможность использования типов указателей, `unsafe` модификатор не оказывает влияния на тип или член.</span><span class="sxs-lookup"><span data-stu-id="bcef1-127">Other than establishing an unsafe context, thus permitting the use of pointer types, the `unsafe` modifier has no effect on a type or a member.</span></span> <span data-ttu-id="bcef1-128">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-128">In the example</span></span>

```csharp
public class A
{
    public unsafe virtual void F() {
        char* p;
        ...
    }
}

public class B: A
{
    public override void F() {
        base.F();
        ...
    }
}
```

<span data-ttu-id="bcef1-129">`unsafe` модификатор `F` метод в `A` просто вызывает текстовое пространство `F` к небезопасным контекстом, в котором можно использовать небезопасные возможности языка.</span><span class="sxs-lookup"><span data-stu-id="bcef1-129">the `unsafe` modifier on the `F` method in `A` simply causes the textual extent of `F` to become an unsafe context in which the unsafe features of the language can be used.</span></span> <span data-ttu-id="bcef1-130">В переопределении `F` в `B`, нет необходимости повторно определить `unsafe` модификатор--Если, конечно, `F` метод в `B` сам должен иметь доступ к небезопасных функций.</span><span class="sxs-lookup"><span data-stu-id="bcef1-130">In the override of `F` in `B`, there is no need to re-specify the `unsafe` modifier -- unless, of course, the `F` method in `B` itself needs access to unsafe features.</span></span>

<span data-ttu-id="bcef1-131">Ситуация немного отличается, если тип указателя является частью сигнатуры метода</span><span class="sxs-lookup"><span data-stu-id="bcef1-131">The situation is slightly different when a pointer type is part of the method's signature</span></span>

```csharp
public unsafe class A
{
    public virtual void F(char* p) {...}
}

public class B: A
{
    public unsafe override void F(char* p) {...}
}
```

<span data-ttu-id="bcef1-132">Здесь так как `F`его сигнатура включает тип указателя, он может быть записано только в небезопасном контексте.</span><span class="sxs-lookup"><span data-stu-id="bcef1-132">Here, because `F`'s signature includes a pointer type, it can only be written in an unsafe context.</span></span> <span data-ttu-id="bcef1-133">Тем не менее, могут быть введены небезопасного контекста либо сделав весь класс unsafe, как в случае `A`, или путем включения `unsafe` модификатор в объявлении метода, как в случае `B`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-133">However, the unsafe context can be introduced by either making the entire class unsafe, as is the case in `A`, or by including an `unsafe` modifier in the method declaration, as is the case in `B`.</span></span>

## <a name="pointer-types"></a><span data-ttu-id="bcef1-134">типы указателей;</span><span class="sxs-lookup"><span data-stu-id="bcef1-134">Pointer types</span></span>

<span data-ttu-id="bcef1-135">В небезопасном контексте *тип* ([типы](types.md)) может быть *"тип указателя"* , а также *value_type* или *reference_type* .</span><span class="sxs-lookup"><span data-stu-id="bcef1-135">In an unsafe context, a *type* ([Types](types.md)) may be a *pointer_type* as well as a *value_type* or a *reference_type*.</span></span> <span data-ttu-id="bcef1-136">Тем не менее *"тип указателя"* также может использоваться в `typeof` выражение ([выражения создания анонимных объектов](expressions.md#anonymous-object-creation-expressions)) за пределами небезопасного контекста таким образом использование не является небезопасным.</span><span class="sxs-lookup"><span data-stu-id="bcef1-136">However, a *pointer_type* may also be used in a `typeof` expression ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) outside of an unsafe context as such usage is not unsafe.</span></span>

```antlr
type_unsafe
    : pointer_type
    ;
```

<span data-ttu-id="bcef1-137">Объект *"тип указателя"* записывается как *unmanaged_type* или ключевое слово `void`, за которым следует `*` маркера:</span><span class="sxs-lookup"><span data-stu-id="bcef1-137">A *pointer_type* is written as an *unmanaged_type* or the keyword `void`, followed by a `*` token:</span></span>

```antlr
pointer_type
    : unmanaged_type '*'
    | 'void' '*'
    ;

unmanaged_type
    : type
    ;
```

<span data-ttu-id="bcef1-138">Тип, указанный до `*` в указатель типа называется ***тип референта*** типа указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-138">The type specified before the `*` in a pointer type is called the ***referent type*** of the pointer type.</span></span> <span data-ttu-id="bcef1-139">Он представляет тип переменной, на который указывает значение типа указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-139">It represents the type of the variable to which a value of the pointer type points.</span></span>

<span data-ttu-id="bcef1-140">В отличие от ссылок (значений ссылочных типов) указатели не отслеживаются сборщиком мусора — сборщик мусора не имеет сведений о указатели и данных, на которые они указывают.</span><span class="sxs-lookup"><span data-stu-id="bcef1-140">Unlike references (values of reference types), pointers are not tracked by the garbage collector -- the garbage collector has no knowledge of pointers and the data to which they point.</span></span> <span data-ttu-id="bcef1-141">Для этой причине указателем не разрешается указывать на ссылку или на структуру, содержащую ссылки, а тип референта указателя должен быть *unmanaged_type*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-141">For this reason a pointer is not permitted to point to a reference or to a struct that contains references, and the referent type of a pointer must be an *unmanaged_type*.</span></span>

<span data-ttu-id="bcef1-142">*Unmanaged_type* является любым типом, не *reference_type* сконструированный тип и не содержит *reference_type* или сконструированный тип поля на любом уровне вложение.</span><span class="sxs-lookup"><span data-stu-id="bcef1-142">An *unmanaged_type* is any type that isn't a *reference_type* or constructed type, and doesn't contain *reference_type* or constructed type fields at any level of nesting.</span></span> <span data-ttu-id="bcef1-143">Другими словами *unmanaged_type* является одним из следующих:</span><span class="sxs-lookup"><span data-stu-id="bcef1-143">In other words, an *unmanaged_type* is one of the following:</span></span>

*  <span data-ttu-id="bcef1-144">`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, или `bool`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-144">`sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, or `bool`.</span></span>
*  <span data-ttu-id="bcef1-145">Любой *enum_type*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-145">Any *enum_type*.</span></span>
*  <span data-ttu-id="bcef1-146">Любой *"тип указателя"*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-146">Any *pointer_type*.</span></span>
*  <span data-ttu-id="bcef1-147">Любые пользовательские *struct_type* , не являющийся сконструированный тип и содержит поля *unmanaged_type*только s.</span><span class="sxs-lookup"><span data-stu-id="bcef1-147">Any user-defined *struct_type* that is not a constructed type and contains fields of *unmanaged_type*s only.</span></span>

<span data-ttu-id="bcef1-148">Интуитивно понятный для сочетания указателей и ссылок на правила — что референты ссылок (объекты) могут содержать указатели, но референты указателей не могут содержать ссылки.</span><span class="sxs-lookup"><span data-stu-id="bcef1-148">The intuitive rule for mixing of pointers and references is that referents of references (objects) are permitted to contain pointers, but referents of pointers are not permitted to contain references.</span></span>

<span data-ttu-id="bcef1-149">В следующей таблице приведены некоторые примеры типов указателей:</span><span class="sxs-lookup"><span data-stu-id="bcef1-149">Some examples of pointer types are given in the table below:</span></span>

| <span data-ttu-id="bcef1-150">__Пример__</span><span class="sxs-lookup"><span data-stu-id="bcef1-150">__Example__</span></span> | <span data-ttu-id="bcef1-151">__Описание__</span><span class="sxs-lookup"><span data-stu-id="bcef1-151">__Description__</span></span>                               |
|-------------|-----------------------------------------------|
| `byte*`     | <span data-ttu-id="bcef1-152">указатель на `byte`</span><span class="sxs-lookup"><span data-stu-id="bcef1-152">Pointer to `byte`</span></span>                             |
| `char*`     | <span data-ttu-id="bcef1-153">указатель на `char`</span><span class="sxs-lookup"><span data-stu-id="bcef1-153">Pointer to `char`</span></span>                             |
| `int**`     | <span data-ttu-id="bcef1-154">Указатель на указатель на `int`</span><span class="sxs-lookup"><span data-stu-id="bcef1-154">Pointer to pointer to `int`</span></span>                   |
| `int*[]`    | <span data-ttu-id="bcef1-155">Одномерный массив указателей на `int`</span><span class="sxs-lookup"><span data-stu-id="bcef1-155">Single-dimensional array of pointers to `int`</span></span> |
| `void*`     | <span data-ttu-id="bcef1-156">Указатель на неизвестный тип</span><span class="sxs-lookup"><span data-stu-id="bcef1-156">Pointer to unknown type</span></span>                       |

<span data-ttu-id="bcef1-157">В данной реализации все типы указателя должны иметь одинаковый размер и представление.</span><span class="sxs-lookup"><span data-stu-id="bcef1-157">For a given implementation, all pointer types must have the same size and representation.</span></span>

<span data-ttu-id="bcef1-158">В отличие от C и C++, при объявлении нескольких указателей в одном объявлении, в C# `*` записывается вместе с базовым типом, не как префиксный знак пунктуации с каждым именем указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-158">Unlike C and C++, when multiple pointers are declared in the same declaration, in C# the `*` is written along with the underlying type only, not as a prefix punctuator on each pointer name.</span></span> <span data-ttu-id="bcef1-159">Пример</span><span class="sxs-lookup"><span data-stu-id="bcef1-159">For example</span></span>

```csharp
int* pi, pj;    // NOT as int *pi, *pj;
```

<span data-ttu-id="bcef1-160">Значение указателя, тип которых `T*` представляет собой адрес переменной типа `T`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-160">The value of a pointer having type `T*` represents the address of a variable of type `T`.</span></span> <span data-ttu-id="bcef1-161">Оператор косвенного обращения указателя `*` ([косвенного обращения указателя](unsafe-code.md#pointer-indirection)) может использоваться для доступа к этой переменной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-161">The pointer indirection operator `*` ([Pointer indirection](unsafe-code.md#pointer-indirection)) may be used to access this variable.</span></span> <span data-ttu-id="bcef1-162">Например, если переменная `P` типа `int*`, выражение `*P` обозначает `int` переменная найдена по адресу, содержащемуся в `P`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-162">For example, given a variable `P` of type `int*`, the expression `*P` denotes the `int` variable found at the address contained in `P`.</span></span>

<span data-ttu-id="bcef1-163">Как и ссылку на объект, указатель может быть `null`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-163">Like an object reference, a pointer may be `null`.</span></span> <span data-ttu-id="bcef1-164">Косвенное обращение к `null` указатель приводит к поведению, определяемого реализацией.</span><span class="sxs-lookup"><span data-stu-id="bcef1-164">Applying the indirection operator to a `null` pointer results in implementation-defined behavior.</span></span> <span data-ttu-id="bcef1-165">Указатель со значением `null` представленного все биты нулями.</span><span class="sxs-lookup"><span data-stu-id="bcef1-165">A pointer with value `null` is represented by all-bits-zero.</span></span>

<span data-ttu-id="bcef1-166">`void*` Тип представляет указатель на неизвестный тип.</span><span class="sxs-lookup"><span data-stu-id="bcef1-166">The `void*` type represents a pointer to an unknown type.</span></span> <span data-ttu-id="bcef1-167">Поскольку тип референта неизвестен, оператор косвенного обращения не может использоваться для указателя типа `void*`, и не может быть выполнена никакие вычисления на такой указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-167">Because the referent type is unknown, the indirection operator cannot be applied to a pointer of type `void*`, nor can any arithmetic be performed on such a pointer.</span></span> <span data-ttu-id="bcef1-168">Однако указатель типа `void*` может быть приведен к любому другому типу указателя (и наоборот).</span><span class="sxs-lookup"><span data-stu-id="bcef1-168">However, a pointer of type `void*` can be cast to any other pointer type (and vice versa).</span></span>

<span data-ttu-id="bcef1-169">Типы указателей являются отдельной категорией типов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-169">Pointer types are a separate category of types.</span></span> <span data-ttu-id="bcef1-170">В отличие от ссылочных типов и типов значений, типы указателей не наследуют от `object` , не существует преобразований между типами указателей и `object`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-170">Unlike reference types and value types, pointer types do not inherit from `object` and no conversions exist between pointer types and `object`.</span></span> <span data-ttu-id="bcef1-171">В частности, упаковка-преобразование и распаковка-преобразование ([упаковка-преобразование и распаковка-преобразование](types.md#boxing-and-unboxing)) не поддерживаются для указателей.</span><span class="sxs-lookup"><span data-stu-id="bcef1-171">In particular, boxing and unboxing ([Boxing and unboxing](types.md#boxing-and-unboxing)) are not supported for pointers.</span></span> <span data-ttu-id="bcef1-172">Однако преобразования могут быть между различными типами указателей и типы указателей и целочисленными типами.</span><span class="sxs-lookup"><span data-stu-id="bcef1-172">However, conversions are permitted between different pointer types and between pointer types and the integral types.</span></span> <span data-ttu-id="bcef1-173">Это описывается в [преобразования указателей](unsafe-code.md#pointer-conversions).</span><span class="sxs-lookup"><span data-stu-id="bcef1-173">This is described in [Pointer conversions](unsafe-code.md#pointer-conversions).</span></span>

<span data-ttu-id="bcef1-174">Объект *"тип указателя"* нельзя использовать в качестве аргумента типа ([создан типы](types.md#constructed-types)) и определения типов ([вывод типа](expressions.md#type-inference)) происходит сбой при вызове универсального метода, будет выведен Аргумент должен иметь тип указателя типа.</span><span class="sxs-lookup"><span data-stu-id="bcef1-174">A *pointer_type* cannot be used as a type argument ([Constructed types](types.md#constructed-types)), and type inference ([Type inference](expressions.md#type-inference)) fails on generic method calls that would have inferred a type argument to be a pointer type.</span></span>

<span data-ttu-id="bcef1-175">Объект *"тип указателя"* может использоваться в качестве типа поле с модификатором volatile ([изменяемые поля](classes.md#volatile-fields)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-175">A *pointer_type* may be used as the type of a volatile field ([Volatile fields](classes.md#volatile-fields)).</span></span>

<span data-ttu-id="bcef1-176">Несмотря на то, что указатели могут передаваться как `ref` или `out` параметры, это может привести к неопределенному поведению, так как указатель может также устанавливаться на локальную переменную, которой больше не существует, при возврате вызываемый метод или основного объекта, на которое он Указывает, больше не является фиксированным.</span><span class="sxs-lookup"><span data-stu-id="bcef1-176">Although pointers can be passed as `ref` or `out` parameters, doing so can cause undefined behavior, since the pointer may well be set to point to a local variable which no longer exists when the called method returns, or the fixed object to which it used to point, is no longer fixed.</span></span> <span data-ttu-id="bcef1-177">Пример:</span><span class="sxs-lookup"><span data-stu-id="bcef1-177">For example:</span></span>

```csharp
using System;

class Test
{
    static int value = 20;

    unsafe static void F(out int* pi1, ref int* pi2) {
        int i = 10;
        pi1 = &i;

        fixed (int* pj = &value) {
            // ...
            pi2 = pj;
        }
    }

    static void Main() {
        int i = 10;
        unsafe {
            int* px1;
            int* px2 = &i;

            F(out px1, ref px2);

            Console.WriteLine("*px1 = {0}, *px2 = {1}",
                *px1, *px2);    // undefined behavior
        }
    }
}
```

<span data-ttu-id="bcef1-178">Метод может возвращать значение некоторого типа, и этот тип может быть указателем.</span><span class="sxs-lookup"><span data-stu-id="bcef1-178">A method can return a value of some type, and that type can be a pointer.</span></span> <span data-ttu-id="bcef1-179">Например, когда получает указатель на непрерывная последовательность из `int`s, количество элементов в этой последовательности и некоторые другие `int` значение, следующий метод возвращает адрес этого значения в этой последовательности, если они совпадают; в противном случае возвращается `null`:</span><span class="sxs-lookup"><span data-stu-id="bcef1-179">For example, when given a pointer to a contiguous sequence of `int`s, that sequence's element count, and some other `int` value, the following method returns the address of that value in that sequence, if a match occurs; otherwise it returns `null`:</span></span>

```csharp
unsafe static int* Find(int* pi, int size, int value) {
    for (int i = 0; i < size; ++i) {
        if (*pi == value) 
            return pi;
        ++pi;
    }
    return null;
}
```

<span data-ttu-id="bcef1-180">В небезопасном контексте для операций с указателями имеется несколько конструкций:</span><span class="sxs-lookup"><span data-stu-id="bcef1-180">In an unsafe context, several constructs are available for operating on pointers:</span></span>

*  <span data-ttu-id="bcef1-181">`*` Оператор можно использовать для выполнения косвенного обращения указателя ([косвенного обращения указателя](unsafe-code.md#pointer-indirection)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-181">The `*` operator may be used to perform pointer indirection ([Pointer indirection](unsafe-code.md#pointer-indirection)).</span></span>
*  <span data-ttu-id="bcef1-182">`->` Оператор может использоваться для доступа к члену структуры через указатель ([доступа к членам указателей](unsafe-code.md#pointer-member-access)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-182">The `->` operator may be used to access a member of a struct through a pointer ([Pointer member access](unsafe-code.md#pointer-member-access)).</span></span>
*  <span data-ttu-id="bcef1-183">`[]` Оператор может использоваться для индексации указатель ([доступ к элементу указателя](unsafe-code.md#pointer-element-access)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-183">The `[]` operator may be used to index a pointer ([Pointer element access](unsafe-code.md#pointer-element-access)).</span></span>
*  <span data-ttu-id="bcef1-184">`&` Оператор может использоваться для получения адреса переменной ([оператор address-of](unsafe-code.md#the-address-of-operator)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-184">The `&` operator may be used to obtain the address of a variable ([The address-of operator](unsafe-code.md#the-address-of-operator)).</span></span>
*  <span data-ttu-id="bcef1-185">`++` И `--` операторы могут использоваться для увеличения и уменьшения указателей ([указатель инкремента и декремента](unsafe-code.md#pointer-increment-and-decrement)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-185">The `++` and `--` operators may be used to increment and decrement pointers ([Pointer increment and decrement](unsafe-code.md#pointer-increment-and-decrement)).</span></span>
*  <span data-ttu-id="bcef1-186">`+` И `-` операторы могут использоваться для выполнения арифметических операций над указателями ([указателями](unsafe-code.md#pointer-arithmetic)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-186">The `+` and `-` operators may be used to perform pointer arithmetic ([Pointer arithmetic](unsafe-code.md#pointer-arithmetic)).</span></span>
*  <span data-ttu-id="bcef1-187">`==`, `!=`, `<`, `>`, `<=`, И `=>` операторы могут использоваться для сравнения указателей ([Сравнение указателей](unsafe-code.md#pointer-comparison)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-187">The `==`, `!=`, `<`, `>`, `<=`, and `=>` operators may be used to compare pointers ([Pointer comparison](unsafe-code.md#pointer-comparison)).</span></span>
*  <span data-ttu-id="bcef1-188">`stackalloc` Оператор можно использовать для выделения памяти из стека вызовов ([буферы фиксированного размера](unsafe-code.md#fixed-size-buffers)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-188">The `stackalloc` operator may be used to allocate memory from the call stack ([Fixed size buffers](unsafe-code.md#fixed-size-buffers)).</span></span>
*  <span data-ttu-id="bcef1-189">`fixed` Инструкция может использоваться, чтобы временно зафиксировать переменную, поэтому можно получить его адрес ([оператор fixed](unsafe-code.md#the-fixed-statement)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-189">The `fixed` statement may be used to temporarily fix a variable so its address can be obtained ([The fixed statement](unsafe-code.md#the-fixed-statement)).</span></span>

## <a name="fixed-and-moveable-variables"></a><span data-ttu-id="bcef1-190">Фиксированные и перемещаемые переменные</span><span class="sxs-lookup"><span data-stu-id="bcef1-190">Fixed and moveable variables</span></span>

<span data-ttu-id="bcef1-191">Оператор address-of ([оператор address-of](unsafe-code.md#the-address-of-operator)) и `fixed` инструкции ([оператор fixed](unsafe-code.md#the-fixed-statement)) разделить переменные на две категории: ***предопределенных переменных***и ***перемещаемые переменные***.</span><span class="sxs-lookup"><span data-stu-id="bcef1-191">The address-of operator ([The address-of operator](unsafe-code.md#the-address-of-operator)) and the `fixed` statement ([The fixed statement](unsafe-code.md#the-fixed-statement)) divide variables into two categories: ***Fixed variables*** and ***moveable variables***.</span></span>

<span data-ttu-id="bcef1-192">Фиксированные переменные находятся в местах хранения, не влияет на операции сборщика мусора.</span><span class="sxs-lookup"><span data-stu-id="bcef1-192">Fixed variables reside in storage locations that are unaffected by operation of the garbage collector.</span></span> <span data-ttu-id="bcef1-193">(Фиксированные переменные примеры локальные переменные, значения параметров и переменных, созданных с разыменования указателей.) С другой стороны перемещаемые переменные находятся в местах хранения, которые могут быть перемещены или удалены сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="bcef1-193">(Examples of fixed variables include local variables, value parameters, and variables created by dereferencing pointers.) On the other hand, moveable variables reside in storage locations that are subject to relocation or disposal by the garbage collector.</span></span> <span data-ttu-id="bcef1-194">(Примерами перемещаемые переменные являются поля в объекты и элементы массивов).</span><span class="sxs-lookup"><span data-stu-id="bcef1-194">(Examples of moveable variables include fields in objects and elements of arrays.)</span></span>

<span data-ttu-id="bcef1-195">`&` Оператор ([оператор address-of](unsafe-code.md#the-address-of-operator)) разрешает адрес фиксированная переменная может быть получена без ограничений.</span><span class="sxs-lookup"><span data-stu-id="bcef1-195">The `&` operator ([The address-of operator](unsafe-code.md#the-address-of-operator)) permits the address of a fixed variable to be obtained without restrictions.</span></span> <span data-ttu-id="bcef1-196">Тем не менее, поскольку перемещаемой переменной может быть перемещена или удалена сборщиком мусора, адрес перемещаемой переменной может быть получен только с помощью `fixed` инструкции ([оператор fixed](unsafe-code.md#the-fixed-statement)) и этот адрес действителен только в течение этого `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-196">However, because a moveable variable is subject to relocation or disposal by the garbage collector, the address of a moveable variable can only be obtained using a `fixed` statement ([The fixed statement](unsafe-code.md#the-fixed-statement)), and that address remains valid only for the duration of that `fixed` statement.</span></span>

<span data-ttu-id="bcef1-197">Точнее говоря фиксированная переменная является одним из следующих:</span><span class="sxs-lookup"><span data-stu-id="bcef1-197">In precise terms, a fixed variable is one of the following:</span></span>

*  <span data-ttu-id="bcef1-198">Переменной полученный в результате *simple_name* ([простые имена](expressions.md#simple-names)), ссылающийся на локальную переменную или параметр по значению, если переменная перехватывается анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-198">A variable resulting from a *simple_name* ([Simple names](expressions.md#simple-names)) that refers to a local variable or a value parameter, unless the variable is captured by an anonymous function.</span></span>
*  <span data-ttu-id="bcef1-199">Переменной полученный в результате *member_access* ([доступ к членам](expressions.md#member-access)) формы `V.I`, где `V` предопределенной переменная *struct_type*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-199">A variable resulting from a *member_access* ([Member access](expressions.md#member-access)) of the form `V.I`, where `V` is a fixed variable of a *struct_type*.</span></span>
*  <span data-ttu-id="bcef1-200">Переменной полученный в результате *pointer_indirection_expression* ([косвенного обращения указателя](unsafe-code.md#pointer-indirection)) формы `*P`, *pointer_member_access* ([Доступа к членам указателей](unsafe-code.md#pointer-member-access)) формы `P->I`, или *pointer_element_access* ([доступ к элементу указателя](unsafe-code.md#pointer-element-access)) формы `P[E]`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-200">A variable resulting from a *pointer_indirection_expression* ([Pointer indirection](unsafe-code.md#pointer-indirection)) of the form `*P`, a *pointer_member_access* ([Pointer member access](unsafe-code.md#pointer-member-access)) of the form `P->I`, or a *pointer_element_access* ([Pointer element access](unsafe-code.md#pointer-element-access)) of the form `P[E]`.</span></span>

<span data-ttu-id="bcef1-201">Все остальные переменные классифицируются как перемещаемые переменные.</span><span class="sxs-lookup"><span data-stu-id="bcef1-201">All other variables are classified as moveable variables.</span></span>

<span data-ttu-id="bcef1-202">Обратите внимание на то, что статическое поле классифицируется как перемещаемой переменной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-202">Note that a static field is classified as a moveable variable.</span></span> <span data-ttu-id="bcef1-203">Также Обратите внимание, что `ref` или `out` параметр классифицируется как перемещаемой переменной, даже если аргумент, заданный в параметре фиксированная переменная.</span><span class="sxs-lookup"><span data-stu-id="bcef1-203">Also note that a `ref` or `out` parameter is classified as a moveable variable, even if the argument given for the parameter is a fixed variable.</span></span> <span data-ttu-id="bcef1-204">Наконец Обратите внимание на то, что переменная, созданная с разыменования указателя всегда классифицируется как фиксированная переменная.</span><span class="sxs-lookup"><span data-stu-id="bcef1-204">Finally, note that a variable produced by dereferencing a pointer is always classified as a fixed variable.</span></span>

## <a name="pointer-conversions"></a><span data-ttu-id="bcef1-205">Преобразования указателей</span><span class="sxs-lookup"><span data-stu-id="bcef1-205">Pointer conversions</span></span>

<span data-ttu-id="bcef1-206">В небезопасном контексте, набор доступных неявных преобразований ([неявные преобразования](conversions.md#implicit-conversions)) расширена для включения следующих неявные преобразования указателей:</span><span class="sxs-lookup"><span data-stu-id="bcef1-206">In an unsafe context, the set of available implicit conversions ([Implicit conversions](conversions.md#implicit-conversions)) is extended to include the following implicit pointer conversions:</span></span>

*  <span data-ttu-id="bcef1-207">Из любого *"тип указателя"* к типу `void*`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-207">From any *pointer_type* to the type `void*`.</span></span>
*  <span data-ttu-id="bcef1-208">Из `null` литерала к любому *"тип указателя"*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-208">From the `null` literal to any *pointer_type*.</span></span>

<span data-ttu-id="bcef1-209">Кроме того, в небезопасном контексте, набор доступных явные преобразования ([явные преобразования](conversions.md#explicit-conversions)) расширена для включения следующих явные преобразования указателей:</span><span class="sxs-lookup"><span data-stu-id="bcef1-209">Additionally, in an unsafe context, the set of available explicit conversions ([Explicit conversions](conversions.md#explicit-conversions)) is extended to include the following explicit pointer conversions:</span></span>

*  <span data-ttu-id="bcef1-210">Из любого *"тип указателя"* любым другим *"тип указателя"*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-210">From any *pointer_type* to any other *pointer_type*.</span></span>
*  <span data-ttu-id="bcef1-211">Из `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, или `ulong` к любому *"тип указателя"*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-211">From `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, or `ulong` to any *pointer_type*.</span></span>
*  <span data-ttu-id="bcef1-212">Из любого *"тип указателя"* для `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, или `ulong`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-212">From any *pointer_type* to `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, or `ulong`.</span></span>

<span data-ttu-id="bcef1-213">Наконец, в небезопасном контексте набор стандартных неявных преобразований ([стандартные неявные преобразования](conversions.md#standard-implicit-conversions)) включает в себя следующие преобразования указателей:</span><span class="sxs-lookup"><span data-stu-id="bcef1-213">Finally, in an unsafe context, the set of standard implicit conversions ([Standard implicit conversions](conversions.md#standard-implicit-conversions)) includes the following pointer conversion:</span></span>

*  <span data-ttu-id="bcef1-214">Из любого *"тип указателя"* к типу `void*`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-214">From any *pointer_type* to the type `void*`.</span></span>

<span data-ttu-id="bcef1-215">Преобразования между двумя типами указателей никогда не изменяют фактическое значение указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-215">Conversions between two pointer types never change the actual pointer value.</span></span> <span data-ttu-id="bcef1-216">Другими словами это преобразование из типа одного указателя в другой не влияет на базовый адрес, выделенный указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-216">In other words, a conversion from one pointer type to another has no effect on the underlying address given by the pointer.</span></span>

<span data-ttu-id="bcef1-217">Если один тип указателя преобразуется в другой, если полученный в результате указатель не выровнено для типа, который указывает, поведение не определено, если результат при разыменовывании.</span><span class="sxs-lookup"><span data-stu-id="bcef1-217">When one pointer type is converted to another, if the resulting pointer is not correctly aligned for the pointed-to type, the behavior is undefined if the result is dereferenced.</span></span> <span data-ttu-id="bcef1-218">Как правило, понятие «правильно» является транзитивным: если указатель на тип `A` выровнен для указателя на тип `B`, который, в свою очередь, выровнен для указателя на тип `C`, затем указатель на тип `A`выровнен для указателя на тип `C`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-218">In general, the concept "correctly aligned" is transitive: if a pointer to type `A` is correctly aligned for a pointer to type `B`, which, in turn, is correctly aligned for a pointer to type `C`, then a pointer to type `A` is correctly aligned for a pointer to type `C`.</span></span>

<span data-ttu-id="bcef1-219">Рассмотрим следующий случай, в котором переменная одного типа осуществляется через указатель на другой тип:</span><span class="sxs-lookup"><span data-stu-id="bcef1-219">Consider the following case in which a variable having one type is accessed via a pointer to a different type:</span></span>

```csharp
char c = 'A';
char* pc = &c;
void* pv = pc;
int* pi = (int*)pv;
int i = *pi;         // undefined
*pi = 123456;        // undefined
```

<span data-ttu-id="bcef1-220">Если тип указателя преобразуется указатель байт, результат указывает на наименьший адресуемый байт переменной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-220">When a pointer type is converted to a pointer to byte, the result points to the lowest addressed byte of the variable.</span></span> <span data-ttu-id="bcef1-221">Последовательными приращениями этого результата до размера переменной, дают указатели оставшиеся байты переменной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-221">Successive increments of the result, up to the size of the variable, yield pointers to the remaining bytes of that variable.</span></span> <span data-ttu-id="bcef1-222">Например следующий метод отображает каждый из восьми байтов в значение типа double как шестнадцатеричное значение:</span><span class="sxs-lookup"><span data-stu-id="bcef1-222">For example, the following method displays each of the eight bytes in a double as a hexadecimal value:</span></span>

```csharp
using System;

class Test
{
    unsafe static void Main() {
      double d = 123.456e23;
        unsafe {
           byte* pb = (byte*)&d;
            for (int i = 0; i < sizeof(double); ++i)
               Console.Write("{0:X2} ", *pb++);
            Console.WriteLine();
        }
    }
}
```

<span data-ttu-id="bcef1-223">Само собой выходные данные зависит от порядка следования байтов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-223">Of course, the output produced depends on endianness.</span></span>

<span data-ttu-id="bcef1-224">Сопоставления между указателями и целых чисел, определяемого реализацией.</span><span class="sxs-lookup"><span data-stu-id="bcef1-224">Mappings between pointers and integers are implementation-defined.</span></span> <span data-ttu-id="bcef1-225">Однако на 32 \* и 64-разрядных архитектур ЦП с линейного адресного пространства, преобразование указателей или из целочисленных типов обычно ведут себя так же, как преобразования `uint` или `ulong` значения, соответственно, или из этих целочисленных типов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-225">However, on 32\* and 64-bit CPU architectures with a linear address space, conversions of pointers to or from integral types typically behave exactly like conversions of `uint` or `ulong` values, respectively, to or from those integral types.</span></span>

### <a name="pointer-arrays"></a><span data-ttu-id="bcef1-226">Массивы указателей</span><span class="sxs-lookup"><span data-stu-id="bcef1-226">Pointer arrays</span></span>

<span data-ttu-id="bcef1-227">В небезопасном контексте могут создаваться массивы указателей.</span><span class="sxs-lookup"><span data-stu-id="bcef1-227">In an unsafe context, arrays of pointers can be constructed.</span></span> <span data-ttu-id="bcef1-228">Только некоторые преобразования, которые применяются к другим типам массива можно использовать в массивах указателей:</span><span class="sxs-lookup"><span data-stu-id="bcef1-228">Only some of the conversions that apply to other array types are allowed on pointer arrays:</span></span>

*  <span data-ttu-id="bcef1-229">Неявное преобразование ссылок ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)) из любого *array_type* для `System.Array` и интерфейсов, реализуемых им также относятся к массивам указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-229">The implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) from any *array_type* to `System.Array` and the interfaces it implements also applies to pointer arrays.</span></span> <span data-ttu-id="bcef1-230">Тем не менее, любая попытка доступа к элементам массива через `System.Array` или он реализует интерфейсы приведет к возникновению исключения во время выполнения, как типы указателей не преобразовываются `object`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-230">However, any attempt to access the array elements through `System.Array` or the interfaces it implements will result in an exception at run-time, as pointer types are not convertible to `object`.</span></span>
*  <span data-ttu-id="bcef1-231">Явное и неявное преобразование ссылочных типов ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions), [явные преобразования ссылочных типов](conversions.md#explicit-reference-conversions)) из типа одномерного массива `S[]` для `System.Collections.Generic.IList<T>` и его универсальных базовых интерфейсов никогда не применяются к массивам указателей, поскольку типы указателей не может использоваться в качестве аргументов типа, а не поддерживается преобразование из типов указателей в типы, не являющихся указателями.</span><span class="sxs-lookup"><span data-stu-id="bcef1-231">The implicit and explicit reference conversions ([Implicit reference conversions](conversions.md#implicit-reference-conversions), [Explicit reference conversions](conversions.md#explicit-reference-conversions)) from a single-dimensional array type `S[]` to `System.Collections.Generic.IList<T>` and its generic base interfaces never apply to pointer arrays, since pointer types cannot be used as type arguments, and there are no conversions from pointer types to non-pointer types.</span></span>
*  <span data-ttu-id="bcef1-232">Преобразование явной ссылки ([явные преобразования ссылочных типов](conversions.md#explicit-reference-conversions)) из `System.Array` и интерфейсы, который реализуется, чтобы любой *array_type* относятся к массивам указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-232">The explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) from `System.Array` and the interfaces it implements to any *array_type* applies to pointer arrays.</span></span>
*  <span data-ttu-id="bcef1-233">Явных преобразований ([явные преобразования ссылочных типов](conversions.md#explicit-reference-conversions)) из `System.Collections.Generic.IList<S>` и его базовых интерфейсов в тип одномерного массива `T[]` никогда не применяется к массивам указателей, поскольку типы указателей не может быть использовать как аргументы типа и не поддерживается преобразование из типов указателей в типы, не являющихся указателями.</span><span class="sxs-lookup"><span data-stu-id="bcef1-233">The explicit reference conversions ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) from `System.Collections.Generic.IList<S>` and its base interfaces to a single-dimensional array type `T[]` never applies to pointer arrays, since pointer types cannot be used as type arguments, and there are no conversions from pointer types to non-pointer types.</span></span>

<span data-ttu-id="bcef1-234">Эти ограничения означают, что расширение для `foreach` описано в разделе инструкции, обрабатывающие массивы [оператор foreach](statements.md#the-foreach-statement) не может применяться к массивам указателей.</span><span class="sxs-lookup"><span data-stu-id="bcef1-234">These restrictions mean that the expansion for the `foreach` statement over arrays described in [The foreach statement](statements.md#the-foreach-statement) cannot be applied to pointer arrays.</span></span> <span data-ttu-id="bcef1-235">Вместо этого оператор foreach в форме</span><span class="sxs-lookup"><span data-stu-id="bcef1-235">Instead, a foreach statement of the form</span></span>

```csharp
foreach (V v in x) embedded_statement
```

<span data-ttu-id="bcef1-236">где тип `x` является типом массива формы `T[,,...,]`, `N` является размерность за вычетом 1 и `T` или `V` является типом указателя, развернут с помощью вложенных циклов for, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bcef1-236">where the type of `x` is an array type of the form `T[,,...,]`, `N` is the number of dimensions minus 1 and `T` or `V` is a pointer type, is expanded using nested for-loops as follows:</span></span>

```csharp
{
    T[,,...,] a = x;
    for (int i0 = a.GetLowerBound(0); i0 <= a.GetUpperBound(0); i0++)
    for (int i1 = a.GetLowerBound(1); i1 <= a.GetUpperBound(1); i1++)
    ...
    for (int iN = a.GetLowerBound(N); iN <= a.GetUpperBound(N); iN++) {
        V v = (V)a.GetValue(i0,i1,...,iN);
        embedded_statement
    }
}
```

<span data-ttu-id="bcef1-237">Переменные `a`, `i0`, `i1`,..., `iN` не видно, но доступной для `x` или *embedded_statement* или любой другой исходный код программы.</span><span class="sxs-lookup"><span data-stu-id="bcef1-237">The variables `a`, `i0`, `i1`, ..., `iN` are not visible to or accessible to `x` or the *embedded_statement* or any other source code of the program.</span></span> <span data-ttu-id="bcef1-238">Переменная `v` только для чтения в внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="bcef1-238">The variable `v` is read-only in the embedded statement.</span></span> <span data-ttu-id="bcef1-239">Если не существует явное преобразование ([преобразования указателей](unsafe-code.md#pointer-conversions)) из `T` (тип элемента) для `V`, выдается ошибка и никакие дальнейшие действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="bcef1-239">If there is not an explicit conversion ([Pointer conversions](unsafe-code.md#pointer-conversions)) from `T` (the element type) to `V`, an error is produced and no further steps are taken.</span></span> <span data-ttu-id="bcef1-240">Если `x` имеет значение `null`, `System.NullReferenceException` возникает исключение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="bcef1-240">If `x` has the value `null`, a `System.NullReferenceException` is thrown at run-time.</span></span>

## <a name="pointers-in-expressions"></a><span data-ttu-id="bcef1-241">Указатели в выражениях</span><span class="sxs-lookup"><span data-stu-id="bcef1-241">Pointers in expressions</span></span>

<span data-ttu-id="bcef1-242">В небезопасном контексте выражение может давать результат типа указателя, но за пределами небезопасного контекста является ошибкой во время компиляции, чтобы выражение имело тип указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-242">In an unsafe context, an expression may yield a result of a pointer type, but outside an unsafe context it is a compile-time error for an expression to be of a pointer type.</span></span> <span data-ttu-id="bcef1-243">Точнее говоря, за пределами небезопасного контекста ошибка времени компиляции возникает, если любой *simple_name* ([простые имена](expressions.md#simple-names)), *member_access* ([доступ к членам ](expressions.md#member-access)), *invocation_expression* ([выражения вызова](expressions.md#invocation-expressions)), или *element_access* ([доступ к элементам](expressions.md#element-access)) является типом указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-243">In precise terms, outside an unsafe context a compile-time error occurs if any *simple_name* ([Simple names](expressions.md#simple-names)), *member_access* ([Member access](expressions.md#member-access)), *invocation_expression* ([Invocation expressions](expressions.md#invocation-expressions)), or *element_access* ([Element access](expressions.md#element-access)) is of a pointer type.</span></span>

<span data-ttu-id="bcef1-244">В небезопасном контексте *primary_no_array_creation_expression* ([основные выражения](expressions.md#primary-expressions)) и *unary_expression* ([унарные операторы](expressions.md#unary-operators)) производства разрешить следующие дополнительные конструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-244">In an unsafe context, the *primary_no_array_creation_expression* ([Primary expressions](expressions.md#primary-expressions)) and *unary_expression* ([Unary operators](expressions.md#unary-operators)) productions permit the following additional constructs:</span></span>

```antlr
primary_no_array_creation_expression_unsafe
    : pointer_member_access
    | pointer_element_access
    | sizeof_expression
    ;

unary_expression_unsafe
    : pointer_indirection_expression
    | addressof_expression
    ;
```

<span data-ttu-id="bcef1-245">В следующих разделах описываются эти конструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-245">These constructs are described in the following sections.</span></span> <span data-ttu-id="bcef1-246">Приоритет и ассоциативность операторов небезопасный подразумевается грамматикой.</span><span class="sxs-lookup"><span data-stu-id="bcef1-246">The precedence and associativity of the unsafe operators is implied by the grammar.</span></span>

### <a name="pointer-indirection"></a><span data-ttu-id="bcef1-247">Косвенное обращение по указателю</span><span class="sxs-lookup"><span data-stu-id="bcef1-247">Pointer indirection</span></span>

<span data-ttu-id="bcef1-248">Объект *pointer_indirection_expression* состоит в виде звездочки (`*`) следуют *unary_expression*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-248">A *pointer_indirection_expression* consists of an asterisk (`*`) followed by a *unary_expression*.</span></span>

```antlr
pointer_indirection_expression
    : '*' unary_expression
    ;
```

<span data-ttu-id="bcef1-249">Унарный `*` оператор обозначает косвенного обращения указателя и используется для получения переменной, на который указывает указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-249">The unary `*` operator denotes pointer indirection and is used to obtain the variable to which a pointer points.</span></span> <span data-ttu-id="bcef1-250">Результат вычисления `*P`, где `P` — это выражение типа указателя `T*`, является переменной типа `T`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-250">The result of evaluating `*P`, where `P` is an expression of a pointer type `T*`, is a variable of type `T`.</span></span> <span data-ttu-id="bcef1-251">Произошла ошибка во время компиляции, чтобы применить унарный `*` оператор для выражения типа `void*` или выражение, не типа указателя.</span><span class="sxs-lookup"><span data-stu-id="bcef1-251">It is a compile-time error to apply the unary `*` operator to an expression of type `void*` or to an expression that isn't of a pointer type.</span></span>

<span data-ttu-id="bcef1-252">В результате применения унарного `*` оператор `null` указатель определяется реализацией.</span><span class="sxs-lookup"><span data-stu-id="bcef1-252">The effect of applying the unary `*` operator to a `null` pointer is implementation-defined.</span></span> <span data-ttu-id="bcef1-253">В частности, нет никакой гарантии, что эта операция создает исключение `System.NullReferenceException`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-253">In particular, there is no guarantee that this operation throws a `System.NullReferenceException`.</span></span>

<span data-ttu-id="bcef1-254">Если недопустимое значение был назначен указателем, поведение унарный `*` оператор не определен.</span><span class="sxs-lookup"><span data-stu-id="bcef1-254">If an invalid value has been assigned to the pointer, the behavior of the unary `*` operator is undefined.</span></span> <span data-ttu-id="bcef1-255">Среди недопустимых значений для разыменования указателя, унарный `*` имеют выровненный адрес указываемого для типа (см. пример в [преобразования указателей](unsafe-code.md#pointer-conversions)) и адрес переменной после окончания срока действия.</span><span class="sxs-lookup"><span data-stu-id="bcef1-255">Among the invalid values for dereferencing a pointer by the unary `*` operator are an address inappropriately aligned for the type pointed to (see example in [Pointer conversions](unsafe-code.md#pointer-conversions)), and the address of a variable after the end of its lifetime.</span></span>

<span data-ttu-id="bcef1-256">В целях анализа определенного присваивания переменной, полученным путем вычисления выражения формы `*P` считается начальным значением ([изначально назначается переменные](variables.md#initially-assigned-variables)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-256">For purposes of definite assignment analysis, a variable produced by evaluating an expression of the form `*P` is considered initially assigned ([Initially assigned variables](variables.md#initially-assigned-variables)).</span></span>

### <a name="pointer-member-access"></a><span data-ttu-id="bcef1-257">Доступа к членам указателей</span><span class="sxs-lookup"><span data-stu-id="bcef1-257">Pointer member access</span></span>

<span data-ttu-id="bcef1-258">Объект *pointer_member_access* состоит из *primary_expression*, за которым следует "`->`" токена, за которым следует *идентификатор* и необязательно *type_argument_list*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-258">A *pointer_member_access* consists of a *primary_expression*, followed by a "`->`" token, followed by an *identifier* and an optional *type_argument_list*.</span></span>

```antlr
pointer_member_access
    : primary_expression '->' identifier
    ;
```

<span data-ttu-id="bcef1-259">В доступа к членам указателей формы `P->I`, `P` должно быть выражением типа указателя, отличное от `void*`, и `I` необходимо обозначить доступного члена типа, к которому `P` точек.</span><span class="sxs-lookup"><span data-stu-id="bcef1-259">In a pointer member access of the form `P->I`, `P` must be an expression of a pointer type other than `void*`, and `I` must denote an accessible member of the type to which `P` points.</span></span>

<span data-ttu-id="bcef1-260">Доступа к членам указателей формы `P->I` вычисляется точно так, как `(*P).I`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-260">A pointer member access of the form `P->I` is evaluated exactly as `(*P).I`.</span></span> <span data-ttu-id="bcef1-261">Описание оператора косвенного обращения указателя (`*`), см. в разделе [косвенного обращения указателя](unsafe-code.md#pointer-indirection).</span><span class="sxs-lookup"><span data-stu-id="bcef1-261">For a description of the pointer indirection operator (`*`), see [Pointer indirection](unsafe-code.md#pointer-indirection).</span></span> <span data-ttu-id="bcef1-262">Описание оператора доступа члена (`.`), см. в разделе [доступ к членам](expressions.md#member-access).</span><span class="sxs-lookup"><span data-stu-id="bcef1-262">For a description of the member access operator (`.`), see [Member access](expressions.md#member-access).</span></span>

<span data-ttu-id="bcef1-263">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-263">In the example</span></span>

```csharp
using System;

struct Point
{
    public int x;
    public int y;

    public override string ToString() {
        return "(" + x + "," + y + ")";
    }
}

class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            p->x = 10;
            p->y = 20;
            Console.WriteLine(p->ToString());
        }
    }
}
```

<span data-ttu-id="bcef1-264">`->` оператор используется для доступа к полям и вызвать метод структуры через указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-264">the `->` operator is used to access fields and invoke a method of a struct through a pointer.</span></span> <span data-ttu-id="bcef1-265">Так как операция `P->I` является точным эквивалентом `(*P).I`, `Main` метод можно было записать так:</span><span class="sxs-lookup"><span data-stu-id="bcef1-265">Because the operation `P->I` is precisely equivalent to `(*P).I`, the `Main` method could equally well have been written:</span></span>

```csharp
class Test
{
    static void Main() {
        Point point;
        unsafe {
            Point* p = &point;
            (*p).x = 10;
            (*p).y = 20;
            Console.WriteLine((*p).ToString());
        }
    }
}
```

### <a name="pointer-element-access"></a><span data-ttu-id="bcef1-266">Доступ к элементу указателя</span><span class="sxs-lookup"><span data-stu-id="bcef1-266">Pointer element access</span></span>

<span data-ttu-id="bcef1-267">Объект *pointer_element_access* состоит из *primary_no_array_creation_expression* следуют выражение, заключенное в "`[`«и»`]`«.</span><span class="sxs-lookup"><span data-stu-id="bcef1-267">A *pointer_element_access* consists of a *primary_no_array_creation_expression* followed by an expression enclosed in "`[`" and "`]`".</span></span>

```antlr
pointer_element_access
    : primary_no_array_creation_expression '[' expression ']'
    ;
```

<span data-ttu-id="bcef1-268">В доступе к элементу указателя формы `P[E]`, `P` должно быть выражением типа указателя, отличное от `void*`, и `E` должно быть выражением, которое может быть неявно преобразован в `int`, `uint`, `long`, или `ulong`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-268">In a pointer element access of the form `P[E]`, `P` must be an expression of a pointer type other than `void*`, and `E` must be an expression that can be implicitly converted to `int`, `uint`, `long`, or `ulong`.</span></span>

<span data-ttu-id="bcef1-269">Доступ к элементу указателя формы `P[E]` вычисляется точно так, как `*(P + E)`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-269">A pointer element access of the form `P[E]` is evaluated exactly as `*(P + E)`.</span></span> <span data-ttu-id="bcef1-270">Описание оператора косвенного обращения указателя (`*`), см. в разделе [косвенного обращения указателя](unsafe-code.md#pointer-indirection).</span><span class="sxs-lookup"><span data-stu-id="bcef1-270">For a description of the pointer indirection operator (`*`), see [Pointer indirection](unsafe-code.md#pointer-indirection).</span></span> <span data-ttu-id="bcef1-271">Описание оператора сложения указатель (`+`), см. в разделе [указателями](unsafe-code.md#pointer-arithmetic).</span><span class="sxs-lookup"><span data-stu-id="bcef1-271">For a description of the pointer addition operator (`+`), see [Pointer arithmetic](unsafe-code.md#pointer-arithmetic).</span></span>

<span data-ttu-id="bcef1-272">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-272">In the example</span></span>

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) p[i] = (char)i;
        }
    }
}
```

<span data-ttu-id="bcef1-273">доступ к элементу указателя используется для инициализации символьного буфера в `for` цикла.</span><span class="sxs-lookup"><span data-stu-id="bcef1-273">a pointer element access is used to initialize the character buffer in a `for` loop.</span></span> <span data-ttu-id="bcef1-274">Так как операция `P[E]` является точным эквивалентом `*(P + E)`, пример можно было записать так:</span><span class="sxs-lookup"><span data-stu-id="bcef1-274">Because the operation `P[E]` is precisely equivalent to `*(P + E)`, the example could equally well have been written:</span></span>

```csharp
class Test
{
    static void Main() {
        unsafe {
            char* p = stackalloc char[256];
            for (int i = 0; i < 256; i++) *(p + i) = (char)i;
        }
    }
}
```

<span data-ttu-id="bcef1-275">Оператор доступа к элементу указателя не проверяет, выходящие за пределы области ошибки и поведение при доступе к элементу вне границ является неопределенным.</span><span class="sxs-lookup"><span data-stu-id="bcef1-275">The pointer element access operator does not check for out-of-bounds errors and the behavior when accessing an out-of-bounds element is undefined.</span></span> <span data-ttu-id="bcef1-276">Это так же, как C и C++.</span><span class="sxs-lookup"><span data-stu-id="bcef1-276">This is the same as C and C++.</span></span>

### <a name="the-address-of-operator"></a><span data-ttu-id="bcef1-277">Оператор address-of</span><span class="sxs-lookup"><span data-stu-id="bcef1-277">The address-of operator</span></span>

<span data-ttu-id="bcef1-278">*Addressof_expression* состоит из амперсанда (`&`) следуют *unary_expression*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-278">An *addressof_expression* consists of an ampersand (`&`) followed by a *unary_expression*.</span></span>

```antlr
addressof_expression
    : '&' unary_expression
    ;
```

<span data-ttu-id="bcef1-279">Если выражение `E` которого имеет тип `T` и классифицируется как фиксированная переменная ([атрибутов неизменности и перемещаемые переменные](unsafe-code.md#fixed-and-moveable-variables)), конструкция `&E` вычисляет адрес переменной, заданной по `E`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-279">Given an expression `E` which is of a type `T` and is classified as a fixed variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)), the construct `&E` computes the address of the variable given by `E`.</span></span> <span data-ttu-id="bcef1-280">Тип результата — `T*` и классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="bcef1-280">The type of the result is `T*` and is classified as a value.</span></span> <span data-ttu-id="bcef1-281">Ошибка времени компиляции возникает, если `E` не классифицируется как переменная, если `E` классифицируется как только для чтения локальной переменной, или если `E` обозначает перемещаемую переменную.</span><span class="sxs-lookup"><span data-stu-id="bcef1-281">A compile-time error occurs if `E` is not classified as a variable, if `E` is classified as a read-only local variable, or if `E` denotes a moveable variable.</span></span> <span data-ttu-id="bcef1-282">В последнем случае оператор fixed ([оператор fixed](unsafe-code.md#the-fixed-statement)) может использоваться для временно «зафиксировать» переменную перед получением ее адреса.</span><span class="sxs-lookup"><span data-stu-id="bcef1-282">In the last case, a fixed statement ([The fixed statement](unsafe-code.md#the-fixed-statement)) can be used to temporarily "fix" the variable before obtaining its address.</span></span> <span data-ttu-id="bcef1-283">Как уже говорилось в [доступ к членам](expressions.md#member-access), за пределами конструкторе экземпляра или статический конструктор для структуры или класса, определяющего `readonly` поле, это поле считается значение, а не переменной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-283">As stated in [Member access](expressions.md#member-access), outside an instance constructor or static constructor for a struct or class that defines a `readonly` field, that field is considered a value, not a variable.</span></span> <span data-ttu-id="bcef1-284">Таким образом его адрес не может быть выполнено.</span><span class="sxs-lookup"><span data-stu-id="bcef1-284">As such, its address cannot be taken.</span></span> <span data-ttu-id="bcef1-285">Аналогичным образом нельзя получить адрес константы.</span><span class="sxs-lookup"><span data-stu-id="bcef1-285">Similarly, the address of a constant cannot be taken.</span></span>

<span data-ttu-id="bcef1-286">`&` Оператор не требует аргумента определенно присвоенной, но следующие `&` операции, переменной, к которому применяется оператор считается определенно присвоенной, в ходе выполнения, в которой выполняется операция.</span><span class="sxs-lookup"><span data-stu-id="bcef1-286">The `&` operator does not require its argument to be definitely assigned, but following an `&` operation, the variable to which the operator is applied is considered definitely assigned in the execution path in which the operation occurs.</span></span> <span data-ttu-id="bcef1-287">Это отвечает программист должен убедиться, чтобы правильная инициализация переменной выполняются на самом деле в этой ситуации.</span><span class="sxs-lookup"><span data-stu-id="bcef1-287">It is the responsibility of the programmer to ensure that correct initialization of the variable actually does take place in this situation.</span></span>

<span data-ttu-id="bcef1-288">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-288">In the example</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        int i;
        unsafe {
            int* p = &i;
            *p = 123;
        }
        Console.WriteLine(i);
    }
}
```

<span data-ttu-id="bcef1-289">`i` считается определенно присвоенной следуя `&i` операции, используемой для инициализации `p`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-289">`i` is considered definitely assigned following the `&i` operation used to initialize `p`.</span></span> <span data-ttu-id="bcef1-290">Назначение `*p` фактически инициализирует `i`, включение этой инициализации является обязанностью программиста, но ошибка во время компиляции не произойдет в том случае, если назначением был удален.</span><span class="sxs-lookup"><span data-stu-id="bcef1-290">The assignment to `*p` in effect initializes `i`, but the inclusion of this initialization is the responsibility of the programmer, and no compile-time error would occur if the assignment was removed.</span></span>

<span data-ttu-id="bcef1-291">Правила определенного присваивания для `&` существует оператор таким образом, что можно избежать избыточной инициализации локальных переменных.</span><span class="sxs-lookup"><span data-stu-id="bcef1-291">The rules of definite assignment for the `&` operator exist such that redundant initialization of local variables can be avoided.</span></span> <span data-ttu-id="bcef1-292">Например многие внешние API принимают указатель на структуру, в которой содержатся API-интерфейсом.</span><span class="sxs-lookup"><span data-stu-id="bcef1-292">For example, many external APIs take a pointer to a structure which is filled in by the API.</span></span> <span data-ttu-id="bcef1-293">Вызовы таких интерфейсов API обычно передается адрес структуры локальной переменной и без этого правила избыточная инициализация переменной структуры не требуются.</span><span class="sxs-lookup"><span data-stu-id="bcef1-293">Calls to such APIs typically pass the address of a local struct variable, and without the rule, redundant initialization of the struct variable would be required.</span></span>

### <a name="pointer-increment-and-decrement"></a><span data-ttu-id="bcef1-294">Увеличение и уменьшение указателя</span><span class="sxs-lookup"><span data-stu-id="bcef1-294">Pointer increment and decrement</span></span>

<span data-ttu-id="bcef1-295">В небезопасном контексте `++` и `--` операторы ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators) и [префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)) могут применяться к указателю переменные для всех типов, за исключением `void*`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-295">In an unsafe context, the `++` and `--` operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators) and [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)) can be applied to pointer variables of all types except `void*`.</span></span> <span data-ttu-id="bcef1-296">Таким образом, для каждого типа указателя `T*`, неявно определены следующие операторы:</span><span class="sxs-lookup"><span data-stu-id="bcef1-296">Thus, for every pointer type `T*`, the following operators are implicitly defined:</span></span>

```csharp
T* operator ++(T* x);
T* operator --(T* x);
```

<span data-ttu-id="bcef1-297">Эти операторы дают те же результаты, что `x + 1` и `x - 1`соответственно ([указателями](unsafe-code.md#pointer-arithmetic)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-297">The operators produce the same results as `x + 1` and `x - 1`, respectively ([Pointer arithmetic](unsafe-code.md#pointer-arithmetic)).</span></span> <span data-ttu-id="bcef1-298">Другими словами, для переменной указателя типа `T*`, `++` добавляет оператор `sizeof(T)` к адресу, содержащемуся в переменной и `--` оператор вычитает `sizeof(T)` из адреса, содержащегося в переменной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-298">In other words, for a pointer variable of type `T*`, the `++` operator adds `sizeof(T)` to the address contained in the variable, and the `--` operator subtracts `sizeof(T)` from the address contained in the variable.</span></span>

<span data-ttu-id="bcef1-299">Если указатель инкремента или декремента операция переполняет домен типа указателя, результат определяется реализацией, но исключения не создаются.</span><span class="sxs-lookup"><span data-stu-id="bcef1-299">If a pointer increment or decrement operation overflows the domain of the pointer type, the result is implementation-defined, but no exceptions are produced.</span></span>

### <a name="pointer-arithmetic"></a><span data-ttu-id="bcef1-300">Расчеты с указателями</span><span class="sxs-lookup"><span data-stu-id="bcef1-300">Pointer arithmetic</span></span>

<span data-ttu-id="bcef1-301">В небезопасном контексте `+` и `-` операторы ([оператор сложения](expressions.md#addition-operator) и [оператор вычитания](expressions.md#subtraction-operator)) могут применяться к значениям всех типов указателей, за исключением `void*`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-301">In an unsafe context, the `+` and `-` operators ([Addition operator](expressions.md#addition-operator) and [Subtraction operator](expressions.md#subtraction-operator)) can be applied to values of all pointer types except `void*`.</span></span> <span data-ttu-id="bcef1-302">Таким образом, для каждого типа указателя `T*`, неявно определены следующие операторы:</span><span class="sxs-lookup"><span data-stu-id="bcef1-302">Thus, for every pointer type `T*`, the following operators are implicitly defined:</span></span>

```csharp
T* operator +(T* x, int y);
T* operator +(T* x, uint y);
T* operator +(T* x, long y);
T* operator +(T* x, ulong y);

T* operator +(int x, T* y);
T* operator +(uint x, T* y);
T* operator +(long x, T* y);
T* operator +(ulong x, T* y);

T* operator -(T* x, int y);
T* operator -(T* x, uint y);
T* operator -(T* x, long y);
T* operator -(T* x, ulong y);

long operator -(T* x, T* y);
```

<span data-ttu-id="bcef1-303">Если выражение `P` типа указателя `T*` и выражение `N` типа `int`, `uint`, `long`, или `ulong`, выражения `P + N` и `N + P` вычислений значение указателя типа `T*` , полученный добавлением `N * sizeof(T)` по адресу `P`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-303">Given an expression `P` of a pointer type `T*` and an expression `N` of type `int`, `uint`, `long`, or `ulong`, the expressions `P + N` and `N + P` compute the pointer value of type `T*` that results from adding `N * sizeof(T)` to the address given by `P`.</span></span> <span data-ttu-id="bcef1-304">Аналогичным образом, выражение `P - N` вычисляет значение указателя типа `T*` , полученный в результате вычитания `N * sizeof(T)` из адреса, заданного выражением `P`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-304">Likewise, the expression `P - N` computes the pointer value of type `T*` that results from subtracting `N * sizeof(T)` from the address given by `P`.</span></span>

<span data-ttu-id="bcef1-305">Если даны два выражения `P` и `Q`, типа указателя `T*`, выражение `P - Q` вычисляет разницу между адресами, заданными `P` и `Q` и затем делитэтойразницы`sizeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-305">Given two expressions, `P` and `Q`, of a pointer type `T*`, the expression `P - Q` computes the difference between the addresses given by `P` and `Q` and then divides that difference by `sizeof(T)`.</span></span> <span data-ttu-id="bcef1-306">Тип результата — всегда `long`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-306">The type of the result is always `long`.</span></span> <span data-ttu-id="bcef1-307">По сути `P - Q` вычисляется как `((long)(P) - (long)(Q)) / sizeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-307">In effect, `P - Q` is computed as `((long)(P) - (long)(Q)) / sizeof(T)`.</span></span>

<span data-ttu-id="bcef1-308">Пример:</span><span class="sxs-lookup"><span data-stu-id="bcef1-308">For example:</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        unsafe {
            int* values = stackalloc int[20];
            int* p = &values[1];
            int* q = &values[15];
            Console.WriteLine("p - q = {0}", p - q);
            Console.WriteLine("q - p = {0}", q - p);
        }
    }
}
```

<span data-ttu-id="bcef1-309">в результате получается:</span><span class="sxs-lookup"><span data-stu-id="bcef1-309">which produces the output:</span></span>

```
p - q = -14
q - p = 14
```

<span data-ttu-id="bcef1-310">Если указатель арифметическая операция переполняет домен типа указателя, результат усекается в виде реализации, но исключения не создаются.</span><span class="sxs-lookup"><span data-stu-id="bcef1-310">If a pointer arithmetic operation overflows the domain of the pointer type, the result is truncated in an implementation-defined fashion, but no exceptions are produced.</span></span>

### <a name="pointer-comparison"></a><span data-ttu-id="bcef1-311">Сравнение указателей</span><span class="sxs-lookup"><span data-stu-id="bcef1-311">Pointer comparison</span></span>

<span data-ttu-id="bcef1-312">В небезопасном контексте `==`, `!=`, `<`, `>`, `<=`, и `=>` операторы ([отношения и операторы тестирования типа](expressions.md#relational-and-type-testing-operators)) могут применяться к значениям всех типы указателей.</span><span class="sxs-lookup"><span data-stu-id="bcef1-312">In an unsafe context, the `==`, `!=`, `<`, `>`, `<=`, and `=>` operators ([Relational and type-testing operators](expressions.md#relational-and-type-testing-operators)) can be applied to values of all pointer types.</span></span> <span data-ttu-id="bcef1-313">Ниже перечислены операторы сравнения указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-313">The pointer comparison operators are:</span></span>

```csharp
bool operator ==(void* x, void* y);
bool operator !=(void* x, void* y);
bool operator <(void* x, void* y);
bool operator >(void* x, void* y);
bool operator <=(void* x, void* y);
bool operator >=(void* x, void* y);
```

<span data-ttu-id="bcef1-314">Поскольку существует неявное преобразование из любой тип указателя на `void*` тип операнда любого типа указателя можно сравнивать с помощью этих операторов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-314">Because an implicit conversion exists from any pointer type to the `void*` type, operands of any pointer type can be compared using these operators.</span></span> <span data-ttu-id="bcef1-315">Операторы сравнения сравнивают адреса, заданные двух операндов, как если бы они были целых чисел без знака.</span><span class="sxs-lookup"><span data-stu-id="bcef1-315">The comparison operators compare the addresses given by the two operands as if they were unsigned integers.</span></span>

### <a name="the-sizeof-operator"></a><span data-ttu-id="bcef1-316">Оператор sizeof</span><span class="sxs-lookup"><span data-stu-id="bcef1-316">The sizeof operator</span></span>

<span data-ttu-id="bcef1-317">`sizeof` Оператор возвращает число байтов, занимаемых переменной заданного типа.</span><span class="sxs-lookup"><span data-stu-id="bcef1-317">The `sizeof` operator returns the number of bytes occupied by a variable of a given type.</span></span> <span data-ttu-id="bcef1-318">Тип, указанный в качестве операнда для `sizeof` должно быть *unmanaged_type* ([типы указателей](unsafe-code.md#pointer-types)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-318">The type specified as an operand to `sizeof` must be an *unmanaged_type* ([Pointer types](unsafe-code.md#pointer-types)).</span></span>

```antlr
sizeof_expression
    : 'sizeof' '(' unmanaged_type ')'
    ;
```

<span data-ttu-id="bcef1-319">Результат `sizeof` оператор является значение типа `int`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-319">The result of the `sizeof` operator is a value of type `int`.</span></span> <span data-ttu-id="bcef1-320">Для некоторых предопределенных типов `sizeof` оператор возвращает значение константы, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="bcef1-320">For certain predefined types, the `sizeof` operator yields a constant value as shown in the table below.</span></span>


| <span data-ttu-id="bcef1-321">__Выражение__</span><span class="sxs-lookup"><span data-stu-id="bcef1-321">__Expression__</span></span>   | <span data-ttu-id="bcef1-322">__Результат__</span><span class="sxs-lookup"><span data-stu-id="bcef1-322">__Result__</span></span> |
|------------------|------------|
| `sizeof(sbyte)`  | `1`        |
| `sizeof(byte)`   | `1`        |
| `sizeof(short)`  | `2`        |
| `sizeof(ushort)` | `2`        |
| `sizeof(int)`    | `4`        |
| `sizeof(uint)`   | `4`        |
| `sizeof(long)`   | `8`        |
| `sizeof(ulong)`  | `8`        |
| `sizeof(char)`   | `2`        |
| `sizeof(float)`  | `4`        |
| `sizeof(double)` | `8`        |
| `sizeof(bool)`   | `1`        |

<span data-ttu-id="bcef1-323">Для всех других типов, результат `sizeof` оператор определяется реализацией и классифицируется как значение, а не как константа.</span><span class="sxs-lookup"><span data-stu-id="bcef1-323">For all other types, the result of the `sizeof` operator is implementation-defined and is classified as a value, not a constant.</span></span>

<span data-ttu-id="bcef1-324">Порядок, в котором членов в структуры не задан.</span><span class="sxs-lookup"><span data-stu-id="bcef1-324">The order in which members are packed into a struct is unspecified.</span></span>

<span data-ttu-id="bcef1-325">Для целей выравнивания могут существовать безымянные заполнения в начале структуры, в рамках структуры и в конце структуры.</span><span class="sxs-lookup"><span data-stu-id="bcef1-325">For alignment purposes, there may be unnamed padding at the beginning of a struct, within a struct, and at the end of the struct.</span></span> <span data-ttu-id="bcef1-326">Значения битов, используемых в качестве заполнителя, не определено.</span><span class="sxs-lookup"><span data-stu-id="bcef1-326">The contents of the bits used as padding are indeterminate.</span></span>

<span data-ttu-id="bcef1-327">При применении к операнду, имеющему тип структуры, результат — общее количество байтов в переменной этого типа, включая заполнения.</span><span class="sxs-lookup"><span data-stu-id="bcef1-327">When applied to an operand that has struct type, the result is the total number of bytes in a variable of that type, including any padding.</span></span>

## <a name="the-fixed-statement"></a><span data-ttu-id="bcef1-328">Оператор fixed</span><span class="sxs-lookup"><span data-stu-id="bcef1-328">The fixed statement</span></span>

<span data-ttu-id="bcef1-329">В небезопасном контексте *embedded_statement* ([инструкций](statements.md)) рабочей среде позволяет порождение `fixed` инструкцию, которая используется для «починки» перемещаемой таким образом, чтобы его адрес остается неизменным в течение инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-329">In an unsafe context, the *embedded_statement* ([Statements](statements.md)) production permits an additional construct, the `fixed` statement, which is used to "fix" a moveable variable such that its address remains constant for the duration of the statement.</span></span>

```antlr
fixed_statement
    : 'fixed' '(' pointer_type fixed_pointer_declarators ')' embedded_statement
    ;

fixed_pointer_declarators
    : fixed_pointer_declarator (','  fixed_pointer_declarator)*
    ;

fixed_pointer_declarator
    : identifier '=' fixed_pointer_initializer
    ;

fixed_pointer_initializer
    : '&' variable_reference
    | expression
    ;
```

<span data-ttu-id="bcef1-330">Каждый *fixed_pointer_declarator* объявляет локальную переменную с заданной *"тип указателя"* и инициализирует эту локальную переменную с адресом, вычисленные поиском решения для соответствующего *fixed_ pointer_initializer*.</span><span class="sxs-lookup"><span data-stu-id="bcef1-330">Each *fixed_pointer_declarator* declares a local variable of the given *pointer_type* and initializes that local variable with the address computed by the corresponding *fixed_pointer_initializer*.</span></span> <span data-ttu-id="bcef1-331">Локальная переменная, объявленная в `fixed` инструкция доступна в любом *fixed_pointer_initializer*s, находящемся справа объявления этой переменной, а в *embedded_statement* из `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-331">A local variable declared in a `fixed` statement is accessible in any *fixed_pointer_initializer*s occurring to the right of that variable's declaration, and in the *embedded_statement* of the `fixed` statement.</span></span> <span data-ttu-id="bcef1-332">Локальная переменная, объявленная с `fixed` оператор считается только для чтения.</span><span class="sxs-lookup"><span data-stu-id="bcef1-332">A local variable declared by a `fixed` statement is considered read-only.</span></span> <span data-ttu-id="bcef1-333">Ошибка времени компиляции возникает, если внедренный оператор пытается изменить эту локальную переменную (с помощью присваивания или `++` и `--` операторы) или передать в качестве `ref` или `out` параметра.</span><span class="sxs-lookup"><span data-stu-id="bcef1-333">A compile-time error occurs if the embedded statement attempts to modify this local variable (via assignment or the `++` and `--` operators) or pass it as a `ref` or `out` parameter.</span></span>

<span data-ttu-id="bcef1-334">Объект *fixed_pointer_initializer* может принимать одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="bcef1-334">A *fixed_pointer_initializer* can be one of the following:</span></span>

*  <span data-ttu-id="bcef1-335">Токен "`&`" следуют *variable_reference* ([точные правила для выявления определенного присваивания](variables.md#precise-rules-for-determining-definite-assignment)) для перемещаемой переменной ([атрибутов неизменности и перемещаемые переменные](unsafe-code.md#fixed-and-moveable-variables)) неуправляемого типа `T`, предоставленный тип `T*` неявно преобразуется к типу указателя, заданному в `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-335">The token "`&`" followed by a *variable_reference* ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)) to a moveable variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)) of an unmanaged type `T`, provided the type `T*` is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="bcef1-336">В этом случае инициализатор вычисляет адрес заданной переменной и переменной гарантированно остается по фиксированному адресу в течение `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-336">In this case, the initializer computes the address of the given variable, and the variable is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span>
*  <span data-ttu-id="bcef1-337">Выражение *array_type* с элементами неуправляемого типа `T`, предоставленный тип `T*` неявно преобразуется к типу указателя, заданному в `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-337">An expression of an *array_type* with elements of an unmanaged type `T`, provided the type `T*` is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="bcef1-338">В этом случае инициализатор вычисляет адрес первого элемента в массиве, и весь массив гарантированно остается по фиксированному адресу в течение `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-338">In this case, the initializer computes the address of the first element in the array, and the entire array is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span> <span data-ttu-id="bcef1-339">Если выражение массива имеет значение null или массив не содержит элементов, инициализатор вычисляет адрес, равным нулю.</span><span class="sxs-lookup"><span data-stu-id="bcef1-339">If the array expression is null or if the array has zero elements, the initializer computes an address equal to zero.</span></span>
*  <span data-ttu-id="bcef1-340">Выражение типа `string`, предоставленный тип `char*` неявно преобразуется к типу указателя, заданному в `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-340">An expression of type `string`, provided the type `char*` is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="bcef1-341">В этом случае инициализатор вычисляет адрес первого символа в строке, и вся строка гарантированно остается по фиксированному адресу в течение `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-341">In this case, the initializer computes the address of the first character in the string, and the entire string is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span> <span data-ttu-id="bcef1-342">Поведение `fixed` инструкции определяется реализацией, если строковое выражение имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="bcef1-342">The behavior of the `fixed` statement is implementation-defined if the string expression is null.</span></span>
*  <span data-ttu-id="bcef1-343">Объект *simple_name* или *member_access* , ссылается на элемент буфера фиксированного размера, перемещаемой переменной, указанный тип элемента буфера фиксированного размера не может быть неявно преобразован к типу указателя, заданному в `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-343">A *simple_name* or *member_access* that references a fixed size buffer member of a moveable variable, provided the type of the fixed size buffer member is implicitly convertible to the pointer type given in the `fixed` statement.</span></span> <span data-ttu-id="bcef1-344">В этом случае инициализатор вычисляет указатель на первый элемент буфера фиксированного размера ([буферы фиксированного размера в выражениях](unsafe-code.md#fixed-size-buffers-in-expressions)), и буфер фиксированного размера гарантированно остается по фиксированному адресу в течение `fixed`инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-344">In this case, the initializer computes a pointer to the first element of the fixed size buffer ([Fixed size buffers in expressions](unsafe-code.md#fixed-size-buffers-in-expressions)), and the fixed size buffer is guaranteed to remain at a fixed address for the duration of the `fixed` statement.</span></span>

<span data-ttu-id="bcef1-345">Для каждого адреса, вычисленные поиском решения *fixed_pointer_initializer* `fixed` оператор гарантирует, что переменная ссылается на адрес не быть перемещены или удалены сборщиком мусора до конца `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-345">For each address computed by a *fixed_pointer_initializer* the `fixed` statement ensures that the variable referenced by the address is not subject to relocation or disposal by the garbage collector for the duration of the `fixed` statement.</span></span> <span data-ttu-id="bcef1-346">Например, если адрес вычисляется по *fixed_pointer_initializer* ссылается на поле объекта или элемента экземпляра массива, `fixed` инструкции гарантирует, что содержащий экземпляр объекта не перемещаются или удален в течение времени существования инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-346">For example, if the address computed by a *fixed_pointer_initializer* references a field of an object or an element of an array instance, the `fixed` statement guarantees that the containing object instance is not relocated or disposed of during the lifetime of the statement.</span></span>

<span data-ttu-id="bcef1-347">Это программист должен убедиться, что указатели, созданных `fixed` инструкций не доживают Помимо выполнения этих операторов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-347">It is the programmer's responsibility to ensure that pointers created by `fixed` statements do not survive beyond execution of those statements.</span></span> <span data-ttu-id="bcef1-348">Например, если указатели созданные `fixed` инструкции передаются внешних интерфейсов API, что программист должен убедиться, что API-интерфейсы сохранить недостаточно памяти эти указатели.</span><span class="sxs-lookup"><span data-stu-id="bcef1-348">For example, when pointers created by `fixed` statements are passed to external APIs, it is the programmer's responsibility to ensure that the APIs retain no memory of these pointers.</span></span>

<span data-ttu-id="bcef1-349">Объекты основного может привести к фрагментации кучи (так как их нельзя перемещать).</span><span class="sxs-lookup"><span data-stu-id="bcef1-349">Fixed objects may cause fragmentation of the heap (because they can't be moved).</span></span> <span data-ttu-id="bcef1-350">По этой причине объекты должны быть исправлены только при необходимости и только после этого минимальный интервал времени.</span><span class="sxs-lookup"><span data-stu-id="bcef1-350">For that reason, objects should be fixed only when absolutely necessary and then only for the shortest amount of time possible.</span></span>

<span data-ttu-id="bcef1-351">Пример</span><span class="sxs-lookup"><span data-stu-id="bcef1-351">The example</span></span>

```csharp
class Test
{
    static int x;
    int y;

    unsafe static void F(int* p) {
        *p = 1;
    }

    static void Main() {
        Test t = new Test();
        int[] a = new int[10];
        unsafe {
            fixed (int* p = &x) F(p);
            fixed (int* p = &t.y) F(p);
            fixed (int* p = &a[0]) F(p);
            fixed (int* p = a) F(p);
        }
    }
}
```

<span data-ttu-id="bcef1-352">Демонстрирует несколько раз используется `fixed` инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-352">demonstrates several uses of the `fixed` statement.</span></span> <span data-ttu-id="bcef1-353">Первый оператор исправления и получает адрес статического поля, вторая инструкция исправления ошибок и получает адрес поля экземпляра и третья инструкция исправления и извлекает адрес элемента массива.</span><span class="sxs-lookup"><span data-stu-id="bcef1-353">The first statement fixes and obtains the address of a static field, the second statement fixes and obtains the address of an instance field, and the third statement fixes and obtains the address of an array element.</span></span> <span data-ttu-id="bcef1-354">В каждом случае было бы использовать обычные `&` оператор, так как переменные классифицируются как перемещаемые переменные.</span><span class="sxs-lookup"><span data-stu-id="bcef1-354">In each case it would have been an error to use the regular `&` operator since the variables are all classified as moveable variables.</span></span>

<span data-ttu-id="bcef1-355">Четвертый `fixed` инструкцию в приведенном выше примере дает тот же результат, третьей.</span><span class="sxs-lookup"><span data-stu-id="bcef1-355">The fourth `fixed` statement in the example above produces a similar result to the third.</span></span>

<span data-ttu-id="bcef1-356">Этот пример `fixed` использует инструкцию `string`:</span><span class="sxs-lookup"><span data-stu-id="bcef1-356">This example of the `fixed` statement uses `string`:</span></span>

```csharp
class Test
{
    static string name = "xx";

    unsafe static void F(char* p) {
        for (int i = 0; p[i] != '\0'; ++i)
            Console.WriteLine(p[i]);
    }

    static void Main() {
        unsafe {
            fixed (char* p = name) F(p);
            fixed (char* p = "xx") F(p);
        }
    }
}
```

<span data-ttu-id="bcef1-357">В небезопасном контексте элементов одномерные массивы хранятся в порядке возрастания индекса, начиная с индекса `0` и заканчивая индексом `Length - 1`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-357">In an unsafe context array elements of single-dimensional arrays are stored in increasing index order, starting with index `0` and ending with index `Length - 1`.</span></span> <span data-ttu-id="bcef1-358">Для многомерных массивов, массив, элементы хранятся таким образом, во-первых, увеличиваются индексы самого правого измерения затем следующего слева измерения, и т. д слева.</span><span class="sxs-lookup"><span data-stu-id="bcef1-358">For multi-dimensional arrays, array elements are stored such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.</span></span> <span data-ttu-id="bcef1-359">В рамках `fixed` инструкции, которая получает указатель `p` на экземпляр массива `a`, значения указателя в диапазоне от `p` для `p + a.Length - 1` представляют адреса элементов в массиве.</span><span class="sxs-lookup"><span data-stu-id="bcef1-359">Within a `fixed` statement that obtains a pointer `p` to an array instance `a`, the pointer values ranging from `p` to `p + a.Length - 1` represent addresses of the elements in the array.</span></span> <span data-ttu-id="bcef1-360">Аналогично, переменные в диапазоне от `p[0]` для `p[a.Length - 1]` представляют фактические элементы массива.</span><span class="sxs-lookup"><span data-stu-id="bcef1-360">Likewise, the variables ranging from `p[0]` to `p[a.Length - 1]` represent the actual array elements.</span></span> <span data-ttu-id="bcef1-361">Учитывая способом, в которой хранятся массивы, мы можно обращаться с массивом любого измерения как если бы оно было линейной.</span><span class="sxs-lookup"><span data-stu-id="bcef1-361">Given the way in which arrays are stored, we can treat an array of any dimension as though it were linear.</span></span>

<span data-ttu-id="bcef1-362">Пример:</span><span class="sxs-lookup"><span data-stu-id="bcef1-362">For example:</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        int[,,] a = new int[2,3,4];
        unsafe {
            fixed (int* p = a) {
                for (int i = 0; i < a.Length; ++i)    // treat as linear
                    p[i] = i;
            }
        }

        for (int i = 0; i < 2; ++i)
            for (int j = 0; j < 3; ++j) {
                for (int k = 0; k < 4; ++k)
                    Console.Write("[{0},{1},{2}] = {3,2} ", i, j, k, a[i,j,k]);
                Console.WriteLine();
            }
    }
}
```

<span data-ttu-id="bcef1-363">в результате получается:</span><span class="sxs-lookup"><span data-stu-id="bcef1-363">which produces the output:</span></span>

```
[0,0,0] =  0 [0,0,1] =  1 [0,0,2] =  2 [0,0,3] =  3
[0,1,0] =  4 [0,1,1] =  5 [0,1,2] =  6 [0,1,3] =  7
[0,2,0] =  8 [0,2,1] =  9 [0,2,2] = 10 [0,2,3] = 11
[1,0,0] = 12 [1,0,1] = 13 [1,0,2] = 14 [1,0,3] = 15
[1,1,0] = 16 [1,1,1] = 17 [1,1,2] = 18 [1,1,3] = 19
[1,2,0] = 20 [1,2,1] = 21 [1,2,2] = 22 [1,2,3] = 23
```

<span data-ttu-id="bcef1-364">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-364">In the example</span></span>

```csharp
class Test
{
    unsafe static void Fill(int* p, int count, int value) {
        for (; count != 0; count--) *p++ = value;
    }

    static void Main() {
        int[] a = new int[100];
        unsafe {
            fixed (int* p = a) Fill(p, 100, -1);
        }
    }
}
```

<span data-ttu-id="bcef1-365">`fixed` можно исправить массива, чтобы его адрес может передаваться методу, который принимает указатель инструкции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-365">a `fixed` statement is used to fix an array so its address can be passed to a method that takes a pointer.</span></span>

<span data-ttu-id="bcef1-366">В данном примере:</span><span class="sxs-lookup"><span data-stu-id="bcef1-366">In the example:</span></span>

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    Font f;

    unsafe static void Main()
    {
        Test test = new Test();
        test.f.size = 10;
        fixed (char* p = test.f.name) {
            PutString("Times New Roman", p, 32);
        }
    }
}
```

<span data-ttu-id="bcef1-367">оператор fixed позволяет исправить буфер фиксированного размера структуры, чтобы его адрес может использоваться как указатель.</span><span class="sxs-lookup"><span data-stu-id="bcef1-367">a fixed statement is used to fix a fixed size buffer of a struct so its address can be used as a pointer.</span></span>

<span data-ttu-id="bcef1-368">Объект `char*` значение, созданное фиксацией экземпляра строки, всегда указывает на строку, завершающуюся символом null.</span><span class="sxs-lookup"><span data-stu-id="bcef1-368">A `char*` value produced by fixing a string instance always points to a null-terminated string.</span></span> <span data-ttu-id="bcef1-369">В операторе fixed, которая получает указатель `p` экземпляр строки `s`, значения указателя в диапазоне от `p` для `p + s.Length - 1` представления адресов символов в строке, а значение указателя `p + s.Length` всегда указывает на символ null (символ со значением `'\0'`).</span><span class="sxs-lookup"><span data-stu-id="bcef1-369">Within a fixed statement that obtains a pointer `p` to a string instance `s`, the pointer values ranging from `p` to `p + s.Length - 1` represent addresses of the characters in the string, and the pointer value `p + s.Length` always points to a null character (the character with value `'\0'`).</span></span>

<span data-ttu-id="bcef1-370">Изменение объектов управляемого типа посредством фиксированных указателей может привести к неопределенному поведению.</span><span class="sxs-lookup"><span data-stu-id="bcef1-370">Modifying objects of managed type through fixed pointers can results in undefined behavior.</span></span> <span data-ttu-id="bcef1-371">Например поскольку строки являются неизменяемыми, это программист должен убедиться, что ссылается указатель в строку фиксированной символы не изменяются.</span><span class="sxs-lookup"><span data-stu-id="bcef1-371">For example, because strings are immutable, it is the programmer's responsibility to ensure that the characters referenced by a pointer to a fixed string are not modified.</span></span>

<span data-ttu-id="bcef1-372">Автоматическое завершение null строк особенно удобно, если вызов внешних API, ожидающих строки «В стиле».</span><span class="sxs-lookup"><span data-stu-id="bcef1-372">The automatic null-termination of strings is particularly convenient when calling external APIs that expect "C-style" strings.</span></span> <span data-ttu-id="bcef1-373">Обратите внимание, что экземпляр string может содержать символы null.</span><span class="sxs-lookup"><span data-stu-id="bcef1-373">Note, however, that a string instance is permitted to contain null characters.</span></span> <span data-ttu-id="bcef1-374">Если присутствуют символы null, строка будет выглядеть усеченный обрабатываются как заканчивающаяся нулевым символом `char*`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-374">If such null characters are present, the string will appear truncated when treated as a null-terminated `char*`.</span></span>

## <a name="fixed-size-buffers"></a><span data-ttu-id="bcef1-375">Буферы фиксированного размера</span><span class="sxs-lookup"><span data-stu-id="bcef1-375">Fixed size buffers</span></span>

<span data-ttu-id="bcef1-376">Буферы фиксированного размера используются для объявления массивов в строке «C style» как члены структур и главным образом используются для связи с неуправляемыми API.</span><span class="sxs-lookup"><span data-stu-id="bcef1-376">Fixed size buffers are used to declare "C style" in-line arrays as members of structs, and are primarily useful for interfacing with unmanaged APIs.</span></span>

### <a name="fixed-size-buffer-declarations"></a><span data-ttu-id="bcef1-377">Объявления буферов фиксированного размера</span><span class="sxs-lookup"><span data-stu-id="bcef1-377">Fixed size buffer declarations</span></span>

<span data-ttu-id="bcef1-378">Объект ***буфера фиксированного размера*** является членом, который представляет хранилище для буфера фиксированной длины переменных данного типа.</span><span class="sxs-lookup"><span data-stu-id="bcef1-378">A ***fixed size buffer*** is a member that represents storage for a fixed length buffer of variables of a given type.</span></span> <span data-ttu-id="bcef1-379">Объявление буфера фиксированного размера включает один или несколько буферов фиксированного размера с заданным типом элементов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-379">A fixed size buffer declaration introduces one or more fixed size buffers of a given element type.</span></span> <span data-ttu-id="bcef1-380">Буферы фиксированного размера допускаются только в объявлениях структур и могут возникать только в небезопасных контекстах ([небезопасных контекстах](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-380">Fixed size buffers are only permitted in struct declarations and can only occur in unsafe contexts ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span>

```antlr
struct_member_declaration_unsafe
    : fixed_size_buffer_declaration
    ;

fixed_size_buffer_declaration
    : attributes? fixed_size_buffer_modifier* 'fixed' buffer_element_type fixed_size_buffer_declarator+ ';'
    ;

fixed_size_buffer_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'unsafe'
    ;

buffer_element_type
    : type
    ;

fixed_size_buffer_declarator
    : identifier '[' constant_expression ']'
    ;
```

<span data-ttu-id="bcef1-381">Объявление буфера фиксированного размера может включать набор атрибутов ([атрибуты](attributes.md)), `new` модификатор ([модификаторы](classes.md#modifiers)), является допустимым сочетанием четырех модификаторов доступа ([типа параметров и ограничений](classes.md#type-parameters-and-constraints)) и `unsafe` модификатор ([небезопасных контекстах](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-381">A fixed size buffer declaration may include a set of attributes ([Attributes](attributes.md)), a `new` modifier ([Modifiers](classes.md#modifiers)), a valid combination of the four access modifiers ([Type parameters and constraints](classes.md#type-parameters-and-constraints)) and an `unsafe` modifier ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span> <span data-ttu-id="bcef1-382">Атрибуты и модификаторы применяются ко всем членам, объявленным с помощью объявления буфера фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="bcef1-382">The attributes and modifiers apply to all of the members declared by the fixed size buffer declaration.</span></span> <span data-ttu-id="bcef1-383">Является ошибкой один и тот же модификатор встречается несколько раз в объявлении буфера фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="bcef1-383">It is an error for the same modifier to appear multiple times in a fixed size buffer declaration.</span></span>

<span data-ttu-id="bcef1-384">Объявление буфера фиксированного размера не может содержать `static` модификатор.</span><span class="sxs-lookup"><span data-stu-id="bcef1-384">A fixed size buffer declaration is not permitted to include the `static` modifier.</span></span>

<span data-ttu-id="bcef1-385">Тип элемента буфера объявление буфера фиксированного размера указывает тип элемента буферов, представленные этим определением.</span><span class="sxs-lookup"><span data-stu-id="bcef1-385">The buffer element type of a fixed size buffer declaration specifies the element type of the buffer(s) introduced by the declaration.</span></span> <span data-ttu-id="bcef1-386">Тип элемента буфера должен быть один из предопределенных типов `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, или `bool`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-386">The buffer element type must be one of the predefined types `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, or `bool`.</span></span>

<span data-ttu-id="bcef1-387">Тип элемента буфера следует список деклараторов буфера фиксированного размера, каждый из которых вводит новый член.</span><span class="sxs-lookup"><span data-stu-id="bcef1-387">The buffer element type is followed by a list of fixed size buffer declarators, each of which introduces a new member.</span></span> <span data-ttu-id="bcef1-388">Декларатор буфера фиксированного размера состоит из идентификатора с именем члена, а затем константное выражение, заключенное в `[` и `]` маркеров.</span><span class="sxs-lookup"><span data-stu-id="bcef1-388">A fixed size buffer declarator consists of an identifier that names the member, followed by a constant expression enclosed in `[` and `]` tokens.</span></span> <span data-ttu-id="bcef1-389">Константное выражение указывает число элементов в члена, представленного этой декларатор буфера фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="bcef1-389">The constant expression denotes the number of elements in the member introduced by that fixed size buffer declarator.</span></span> <span data-ttu-id="bcef1-390">Тип константного выражения должен быть неявно преобразовать в тип `int`, и значение должно быть положительным целым числом ненулевое значение.</span><span class="sxs-lookup"><span data-stu-id="bcef1-390">The type of the constant expression must be implicitly convertible to type `int`, and the value must be a non-zero positive integer.</span></span>

<span data-ttu-id="bcef1-391">Элементы буфера фиксированного размера гарантированно размещались последовательно в памяти.</span><span class="sxs-lookup"><span data-stu-id="bcef1-391">The elements of a fixed size buffer are guaranteed to be laid out sequentially in memory.</span></span>

<span data-ttu-id="bcef1-392">Объявление буфера фиксированного размера, который объявляет несколько буферов фиксированного размера соответствует несколько объявлений, входящем в объявление один фиксированный размер буфера с те же атрибуты и типы элементов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-392">A fixed size buffer declaration that declares multiple fixed size buffers is equivalent to multiple declarations of a single fixed size buffer declaration with the same attributes, and element types.</span></span> <span data-ttu-id="bcef1-393">Пример</span><span class="sxs-lookup"><span data-stu-id="bcef1-393">For example</span></span>

```csharp
unsafe struct A
{
   public fixed int x[5], y[10], z[100];
}
```

<span data-ttu-id="bcef1-394">эквивалентно</span><span class="sxs-lookup"><span data-stu-id="bcef1-394">is equivalent to</span></span>

```csharp
unsafe struct A
{
   public fixed int x[5];
   public fixed int y[10];
   public fixed int z[100];
}
```

### <a name="fixed-size-buffers-in-expressions"></a><span data-ttu-id="bcef1-395">Буферы фиксированного размера в выражениях</span><span class="sxs-lookup"><span data-stu-id="bcef1-395">Fixed size buffers in expressions</span></span>

<span data-ttu-id="bcef1-396">Поиск члена ([операторы](expressions.md#operators)) фиксированного размера буфера члена выполняется так же, как поиск члена поля.</span><span class="sxs-lookup"><span data-stu-id="bcef1-396">Member lookup ([Operators](expressions.md#operators)) of a fixed size buffer member proceeds exactly like member lookup of a field.</span></span>

<span data-ttu-id="bcef1-397">Буфер фиксированного размера можно ссылаться в выражение, использующее *simple_name* ([вывод типа](expressions.md#type-inference)) или *member_access* ([проверки во время компиляции динамического разрешения перегрузки](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-397">A fixed size buffer can be referenced in an expression using a *simple_name* ([Type inference](expressions.md#type-inference)) or a *member_access* ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span>

<span data-ttu-id="bcef1-398">При ссылке на член буфера фиксированного размера по простому имени действует так же, как доступ к члену в форме `this.I`, где `I` входит буфера фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="bcef1-398">When a fixed size buffer member is referenced as a simple name, the effect is the same as a member access of the form `this.I`, where `I` is the fixed size buffer member.</span></span>

<span data-ttu-id="bcef1-399">В доступ к члену в форме `E.I`, если `E` является типом структуры и поиск члена `I` тем, что тип структуры определяет член фиксированного размера, затем `E.I` является вычисляется и классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="bcef1-399">In a member access of the form `E.I`, if `E` is of a struct type and a member lookup of `I` in that struct type identifies a fixed size member, then `E.I` is evaluated an classified as follows:</span></span>

*  <span data-ttu-id="bcef1-400">Если выражение `E.I` не происходит в небезопасном контексте, то возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-400">If the expression `E.I` does not occur in an unsafe context, a compile-time error occurs.</span></span>
*  <span data-ttu-id="bcef1-401">Если `E` классифицируется как значение, то возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-401">If `E` is classified as a value, a compile-time error occurs.</span></span>
*  <span data-ttu-id="bcef1-402">В противном случае, если `E` является перемещаемой ([атрибутов неизменности и перемещаемые переменные](unsafe-code.md#fixed-and-moveable-variables)) и выражение `E.I` не *fixed_pointer_initializer* ([фиксированной Инструкция](unsafe-code.md#the-fixed-statement)), возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="bcef1-402">Otherwise, if `E` is a moveable variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)) and the expression `E.I` is not a *fixed_pointer_initializer* ([The fixed statement](unsafe-code.md#the-fixed-statement)), a compile-time error occurs.</span></span>
*  <span data-ttu-id="bcef1-403">В противном случае `E` ссылается на переменную, основных и результатом выражения является указатель на первый элемент члена буфера фиксированного размера `I` в `E`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-403">Otherwise, `E` references a fixed variable and the result of the expression is a pointer to the first element of the fixed size buffer member `I` in `E`.</span></span> <span data-ttu-id="bcef1-404">Результат имеет тип `S*`, где `S` является тип элемента `I`и классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="bcef1-404">The result is of type `S*`, where `S` is the element type of `I`, and is classified as a value.</span></span>

<span data-ttu-id="bcef1-405">Последующие элементы буфера фиксированного размера может осуществляться с помощью операции с указателем с первого элемента.</span><span class="sxs-lookup"><span data-stu-id="bcef1-405">The subsequent elements of the fixed size buffer can be accessed using pointer operations from the first element.</span></span> <span data-ttu-id="bcef1-406">В отличие от доступа к массивам доступ к элементам буфера фиксированного размера является небезопасной операцией и не проверки диапазона.</span><span class="sxs-lookup"><span data-stu-id="bcef1-406">Unlike access to arrays, access to the elements of a fixed size buffer is an unsafe operation and is not range checked.</span></span>

<span data-ttu-id="bcef1-407">В следующем примере объявляется и используется структура с членом буфера фиксированного размера.</span><span class="sxs-lookup"><span data-stu-id="bcef1-407">The following example declares and uses a struct with a fixed size buffer member.</span></span>

```csharp
unsafe struct Font
{
    public int size;
    public fixed char name[32];
}

class Test
{
    unsafe static void PutString(string s, char* buffer, int bufSize) {
        int len = s.Length;
        if (len > bufSize) len = bufSize;
        for (int i = 0; i < len; i++) buffer[i] = s[i];
        for (int i = len; i < bufSize; i++) buffer[i] = (char)0;
    }

    unsafe static void Main()
    {
        Font f;
        f.size = 10;
        PutString("Times New Roman", f.name, 32);
    }
}
```

### <a name="definite-assignment-checking"></a><span data-ttu-id="bcef1-408">Проверка определенного присваивания</span><span class="sxs-lookup"><span data-stu-id="bcef1-408">Definite assignment checking</span></span>

<span data-ttu-id="bcef1-409">Буферы фиксированного размера, не подвергаются проверке определенного присваивания ([определенного присваивания](variables.md#definite-assignment)), а члены буфера фиксированного размера игнорируются для определенного присваивания, проверка переменным типа структуры.</span><span class="sxs-lookup"><span data-stu-id="bcef1-409">Fixed size buffers are not subject to definite assignment checking ([Definite assignment](variables.md#definite-assignment)), and fixed size buffer members are ignored for purposes of definite assignment checking of struct type variables.</span></span>

<span data-ttu-id="bcef1-410">Когда Дальняя переменная члена буфера фиксированного размера является статической переменной, экземпляр переменной экземпляра класса или элемента массива, элементы буфера фиксированного размера автоматически инициализируются значениями по умолчанию ([Значения по умолчанию](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-410">When the outermost containing struct variable of a fixed size buffer member is a static variable, an instance variable of a class instance, or an array element, the elements of the fixed size buffer are automatically initialized to their default values ([Default values](variables.md#default-values)).</span></span> <span data-ttu-id="bcef1-411">Во всех остальных случаях начальное содержимое буфера фиксированного размера не определено.</span><span class="sxs-lookup"><span data-stu-id="bcef1-411">In all other cases, the initial content of a fixed size buffer is undefined.</span></span>

## <a name="stack-allocation"></a><span data-ttu-id="bcef1-412">Выделение памяти в стеке</span><span class="sxs-lookup"><span data-stu-id="bcef1-412">Stack allocation</span></span>

<span data-ttu-id="bcef1-413">В небезопасном контексте объявления локальной переменной ([объявления локальных переменных](statements.md#local-variable-declarations)) может включать инициализатор выделения стека, который выделяет память из стека вызовов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-413">In an unsafe context, a local variable declaration ([Local variable declarations](statements.md#local-variable-declarations)) may include a stack allocation initializer which allocates memory from the call stack.</span></span>

```antlr
local_variable_initializer_unsafe
    : stackalloc_initializer
    ;

stackalloc_initializer
    : 'stackalloc' unmanaged_type '[' expression ']'
    ;
```

<span data-ttu-id="bcef1-414">*Unmanaged_type* указывает тип элементов, которые будут храниться в каталоге во вновь выделенный и *выражение* показывает некоторые из этих элементов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-414">The *unmanaged_type* indicates the type of the items that will be stored in the newly allocated location, and the *expression* indicates the number of these items.</span></span> <span data-ttu-id="bcef1-415">Взятые вместе, они указывают необходимый размер выделения.</span><span class="sxs-lookup"><span data-stu-id="bcef1-415">Taken together, these specify the required allocation size.</span></span> <span data-ttu-id="bcef1-416">Так как размер выделения стека не может быть отрицательным, это ошибка времени компиляции, чтобы указать число элементов в качестве *constant_expression* , результатом которого является отрицательное значение.</span><span class="sxs-lookup"><span data-stu-id="bcef1-416">Since the size of a stack allocation cannot be negative, it is a compile-time error to specify the number of items as a *constant_expression* that evaluates to a negative value.</span></span>

<span data-ttu-id="bcef1-417">Инициализатора выделения стека формы `stackalloc T[E]` требует `T` неуправляемый тип ([типы указателей](unsafe-code.md#pointer-types)) и `E` является выражением типа `int`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-417">A stack allocation initializer of the form `stackalloc T[E]` requires `T` to be an unmanaged type ([Pointer types](unsafe-code.md#pointer-types)) and `E` to be an expression of type `int`.</span></span> <span data-ttu-id="bcef1-418">Конструкция выделяет `E * sizeof(T)` байт из вызова стек и возвращает указатель типа `T*`, на вновь выделенный блок.</span><span class="sxs-lookup"><span data-stu-id="bcef1-418">The construct allocates `E * sizeof(T)` bytes from the call stack and returns a pointer, of type `T*`, to the newly allocated block.</span></span> <span data-ttu-id="bcef1-419">Если `E` имеет отрицательное значение, то поведение не определено.</span><span class="sxs-lookup"><span data-stu-id="bcef1-419">If `E` is a negative value, then the behavior is undefined.</span></span> <span data-ttu-id="bcef1-420">Если `E` равно нулю, то выделение не производится, а также указатель, возвращенный определяется реализацией.</span><span class="sxs-lookup"><span data-stu-id="bcef1-420">If `E` is zero, then no allocation is made, and the pointer returned is implementation-defined.</span></span> <span data-ttu-id="bcef1-421">Если не хватает памяти для выделения блока заданного размера, `System.StackOverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="bcef1-421">If there is not enough memory available to allocate a block of the given size, a `System.StackOverflowException` is thrown.</span></span>

<span data-ttu-id="bcef1-422">Содержимое только что выделенную память не определено.</span><span class="sxs-lookup"><span data-stu-id="bcef1-422">The content of the newly allocated memory is undefined.</span></span>

<span data-ttu-id="bcef1-423">Инициализаторы выделения стека не разрешены в `catch` или `finally` блоки ([оператора try](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="bcef1-423">Stack allocation initializers are not permitted in `catch` or `finally` blocks ([The try statement](statements.md#the-try-statement)).</span></span>

<span data-ttu-id="bcef1-424">Невозможно явно освобождать память, выделенную с помощью `stackalloc`.</span><span class="sxs-lookup"><span data-stu-id="bcef1-424">There is no way to explicitly free memory allocated using `stackalloc`.</span></span> <span data-ttu-id="bcef1-425">Все блоки памяти в стеке, созданному в ходе выполнения функции-члена, автоматически удаляются при возврате функции-члена.</span><span class="sxs-lookup"><span data-stu-id="bcef1-425">All stack allocated memory blocks created during the execution of a function member are automatically discarded when that function member returns.</span></span> <span data-ttu-id="bcef1-426">Это соответствует `alloca` функция, это расширение, часто встречаются в реализации C и C++.</span><span class="sxs-lookup"><span data-stu-id="bcef1-426">This corresponds to the `alloca` function, an extension commonly found in C and C++ implementations.</span></span>

<span data-ttu-id="bcef1-427">В примере</span><span class="sxs-lookup"><span data-stu-id="bcef1-427">In the example</span></span>

```csharp
using System;

class Test
{
    static string IntToString(int value) {
        int n = value >= 0? value: -value;
        unsafe {
            char* buffer = stackalloc char[16];
            char* p = buffer + 16;
            do {
                *--p = (char)(n % 10 + '0');
                n /= 10;
            } while (n != 0);
            if (value < 0) *--p = '-';
            return new string(p, 0, (int)(buffer + 16 - p));
        }
    }

    static void Main() {
        Console.WriteLine(IntToString(12345));
        Console.WriteLine(IntToString(-999));
    }
}
```

<span data-ttu-id="bcef1-428">`stackalloc` используется инициализатор в `IntToString` метод, чтобы выделить буфер 16 символов в стеке.</span><span class="sxs-lookup"><span data-stu-id="bcef1-428">a `stackalloc` initializer is used in the `IntToString` method to allocate a buffer of 16 characters on the stack.</span></span> <span data-ttu-id="bcef1-429">Чего буфер очищается автоматически при возврате метода.</span><span class="sxs-lookup"><span data-stu-id="bcef1-429">The buffer is automatically discarded when the method returns.</span></span>

## <a name="dynamic-memory-allocation"></a><span data-ttu-id="bcef1-430">Динамическое выделение памяти</span><span class="sxs-lookup"><span data-stu-id="bcef1-430">Dynamic memory allocation</span></span>

<span data-ttu-id="bcef1-431">За исключением `stackalloc` оператор, C# не предоставляет предопределенные конструкции для управления собранных памяти не сборщиком мусора.</span><span class="sxs-lookup"><span data-stu-id="bcef1-431">Except for the `stackalloc` operator, C# provides no predefined constructs for managing non-garbage collected memory.</span></span> <span data-ttu-id="bcef1-432">Обычно такие службы, предоставляемые библиотек классов или импортировать непосредственно из операционной системы.</span><span class="sxs-lookup"><span data-stu-id="bcef1-432">Such services are typically provided by supporting class libraries or imported directly from the underlying operating system.</span></span> <span data-ttu-id="bcef1-433">Например `Memory` класс ниже показано, как функции кучи операционной системы может осуществляться с помощью C#:</span><span class="sxs-lookup"><span data-stu-id="bcef1-433">For example, the `Memory` class below illustrates how the heap functions of an underlying operating system might be accessed from C#:</span></span>

```csharp
using System;
using System.Runtime.InteropServices;

public unsafe class Memory
{
    // Handle for the process heap. This handle is used in all calls to the
    // HeapXXX APIs in the methods below.
    static int ph = GetProcessHeap();

    // Private instance constructor to prevent instantiation.
    private Memory() {}

    // Allocates a memory block of the given size. The allocated memory is
    // automatically initialized to zero.
    public static void* Alloc(int size) {
        void* result = HeapAlloc(ph, HEAP_ZERO_MEMORY, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Copies count bytes from src to dst. The source and destination
    // blocks are permitted to overlap.
    public static void Copy(void* src, void* dst, int count) {
        byte* ps = (byte*)src;
        byte* pd = (byte*)dst;
        if (ps > pd) {
            for (; count != 0; count--) *pd++ = *ps++;
        }
        else if (ps < pd) {
            for (ps += count, pd += count; count != 0; count--) *--pd = *--ps;
        }
    }

    // Frees a memory block.
    public static void Free(void* block) {
        if (!HeapFree(ph, 0, block)) throw new InvalidOperationException();
    }

    // Re-allocates a memory block. If the reallocation request is for a
    // larger size, the additional region of memory is automatically
    // initialized to zero.
    public static void* ReAlloc(void* block, int size) {
        void* result = HeapReAlloc(ph, HEAP_ZERO_MEMORY, block, size);
        if (result == null) throw new OutOfMemoryException();
        return result;
    }

    // Returns the size of a memory block.
    public static int SizeOf(void* block) {
        int result = HeapSize(ph, 0, block);
        if (result == -1) throw new InvalidOperationException();
        return result;
    }

    // Heap API flags
    const int HEAP_ZERO_MEMORY = 0x00000008;

    // Heap API functions
    [DllImport("kernel32")]
    static extern int GetProcessHeap();

    [DllImport("kernel32")]
    static extern void* HeapAlloc(int hHeap, int flags, int size);

    [DllImport("kernel32")]
    static extern bool HeapFree(int hHeap, int flags, void* block);

    [DllImport("kernel32")]
    static extern void* HeapReAlloc(int hHeap, int flags, void* block, int size);

    [DllImport("kernel32")]
    static extern int HeapSize(int hHeap, int flags, void* block);
}
```

<span data-ttu-id="bcef1-434">Пример, использующий `Memory` классов приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="bcef1-434">An example that uses the `Memory` class is given below:</span></span>

```csharp
class Test
{
    static void Main() {
        unsafe {
            byte* buffer = (byte*)Memory.Alloc(256);
            try {
                for (int i = 0; i < 256; i++) buffer[i] = (byte)i;
                byte[] array = new byte[256];
                fixed (byte* p = array) Memory.Copy(buffer, p, 256); 
            }
            finally {
                Memory.Free(buffer);
            }
            for (int i = 0; i < 256; i++) Console.WriteLine(array[i]);
        }
    }
}
```

<span data-ttu-id="bcef1-435">Пример кода поочередно 256 байт памяти `Memory.Alloc` и инициализирует блок памяти со значениями, увеличение от 0 до 255.</span><span class="sxs-lookup"><span data-stu-id="bcef1-435">The example allocates 256 bytes of memory through `Memory.Alloc` and initializes the memory block with values increasing from 0 to 255.</span></span> <span data-ttu-id="bcef1-436">Он выделяет массив байтов 256 элемент и использует `Memory.Copy` следует скопировать содержимое блока памяти в массив байтов.</span><span class="sxs-lookup"><span data-stu-id="bcef1-436">It then allocates a 256 element byte array and uses `Memory.Copy` to copy the contents of the memory block into the byte array.</span></span> <span data-ttu-id="bcef1-437">Наконец, блок памяти освобождается с помощью `Memory.Free` и содержимое байтового массива выводится на консоль.</span><span class="sxs-lookup"><span data-stu-id="bcef1-437">Finally, the memory block is freed using `Memory.Free` and the contents of the byte array are output on the console.</span></span>
