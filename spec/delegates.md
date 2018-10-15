# <a name="delegates"></a><span data-ttu-id="78eeb-101">Делегаты</span><span class="sxs-lookup"><span data-stu-id="78eeb-101">Delegates</span></span>

<span data-ttu-id="78eeb-102">Делегаты другие языки сценариев, таких как C++, Pascal и Modula, реализуются--решены с помощью указателей функций.</span><span class="sxs-lookup"><span data-stu-id="78eeb-102">Delegates enable scenarios that other languages—such as C++, Pascal, and Modula -- have addressed with function pointers.</span></span> <span data-ttu-id="78eeb-103">Тем не менее, в отличие от указателей функций C++, делегаты являются полностью объектно-ориентированного программирования, и в отличие от C++ указателей на функции-члены, делегаты инкапсулируют и экземпляр объекта и метод.</span><span class="sxs-lookup"><span data-stu-id="78eeb-103">Unlike C++ function pointers, however, delegates are fully object oriented, and unlike C++ pointers to member functions, delegates encapsulate both an object instance and a method.</span></span>

<span data-ttu-id="78eeb-104">Объявление делегата определяет класс, который является производным от класса `System.Delegate`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-104">A delegate declaration defines a class that is derived from the class `System.Delegate`.</span></span> <span data-ttu-id="78eeb-105">Экземпляр делегата инкапсулирует список вызова, который представляет собой список один или несколько методов, каждый из которых называется вызываемым объектом.</span><span class="sxs-lookup"><span data-stu-id="78eeb-105">A delegate instance encapsulates an invocation list, which is a list of one or more methods, each of which is referred to as a callable entity.</span></span> <span data-ttu-id="78eeb-106">Например методы, вызываемая сущность состоит из экземпляра и метод в этом экземпляре.</span><span class="sxs-lookup"><span data-stu-id="78eeb-106">For instance methods, a callable entity consists of an instance and a method on that instance.</span></span> <span data-ttu-id="78eeb-107">Для статических методов вызываемая сущность состоит только из метода.</span><span class="sxs-lookup"><span data-stu-id="78eeb-107">For static methods, a callable entity consists of just a method.</span></span> <span data-ttu-id="78eeb-108">Вызов экземпляра делегата с соответствующим набором аргументов приводит к каждой сущности, вызываемых делегата, вызываемого с указанным набором аргументов.</span><span class="sxs-lookup"><span data-stu-id="78eeb-108">Invoking a delegate instance with an appropriate set of arguments causes each of the delegate's callable entities to be invoked with the given set of arguments.</span></span>

<span data-ttu-id="78eeb-109">Интересной и полезной особенности делегата то, что он не знать или заботится о классах методов, которые она инкапсулирует; все это означает, что эти методы должны совместимы ([объявления делегатов](delegates.md#delegate-declarations)) с типом делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-109">An interesting and useful property of a delegate instance is that it does not know or care about the classes of the methods it encapsulates; all that matters is that those methods be compatible ([Delegate declarations](delegates.md#delegate-declarations)) with the delegate's type.</span></span> <span data-ttu-id="78eeb-110">Это делает делегаты, прекрасно подходят для вызова «anonymous».</span><span class="sxs-lookup"><span data-stu-id="78eeb-110">This makes delegates perfectly suited for "anonymous" invocation.</span></span>

## <a name="delegate-declarations"></a><span data-ttu-id="78eeb-111">Объявления делегатов</span><span class="sxs-lookup"><span data-stu-id="78eeb-111">Delegate declarations</span></span>

<span data-ttu-id="78eeb-112">Объект *delegate_declaration* — *type_declaration* ([объявления типов](namespaces.md#type-declarations)), объявляет новый тип делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-112">A *delegate_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new delegate type.</span></span>

```antlr
delegate_declaration
    : attributes? delegate_modifier* 'delegate' return_type
      identifier variant_type_parameter_list?
      '(' formal_parameter_list? ')' type_parameter_constraints_clause* ';'
    ;

delegate_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | delegate_modifier_unsafe
    ;
```

<span data-ttu-id="78eeb-113">Это ошибка времени компиляции для один и тот же модификатор встречается несколько раз в объявлении делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-113">It is a compile-time error for the same modifier to appear multiple times in a delegate declaration.</span></span>

<span data-ttu-id="78eeb-114">`new` Модификатор допускается только для делегатов объявлена внутри другого типа, в этом случае он указывает, что такой делегат скрывает унаследованный член с тем же именем, как описано в разделе [Модификатор new](classes.md#the-new-modifier).</span><span class="sxs-lookup"><span data-stu-id="78eeb-114">The `new` modifier is only permitted on delegates declared within another type, in which case it specifies that such a delegate hides an inherited member by the same name, as described in [The new modifier](classes.md#the-new-modifier).</span></span>

<span data-ttu-id="78eeb-115">`public`, `protected`, `internal`, И `private` модификаторы определяют доступность типа делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-115">The `public`, `protected`, `internal`, and `private` modifiers control the accessibility of the delegate type.</span></span> <span data-ttu-id="78eeb-116">В зависимости от контекста, в котором производится объявление делегата, некоторые из этих модификаторов запрещены ([объявленную доступность](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="78eeb-116">Depending on the context in which the delegate declaration occurs, some of these modifiers may not be permitted ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

<span data-ttu-id="78eeb-117">Имя типа делегата *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="78eeb-117">The delegate's type name is *identifier*.</span></span>

<span data-ttu-id="78eeb-118">Необязательный *formal_parameter_list* задает параметры делегата, и *return_type* указывает тип возвращаемого значения делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-118">The optional *formal_parameter_list* specifies the parameters of the delegate, and *return_type* indicates the return type of the delegate.</span></span>

<span data-ttu-id="78eeb-119">Необязательный *variant_type_parameter_list* ([списков параметров типа Variant](interfaces.md#variant-type-parameter-lists)) задает параметры типа непосредственно к делегату.</span><span class="sxs-lookup"><span data-stu-id="78eeb-119">The optional *variant_type_parameter_list* ([Variant type parameter lists](interfaces.md#variant-type-parameter-lists)) specifies the type parameters to the delegate itself.</span></span>

<span data-ttu-id="78eeb-120">Тип возвращаемого значения является типом делегата должен быть либо `void`, или безопасным при выводе ([безопасность вариативности](interfaces.md#variance-safety)).</span><span class="sxs-lookup"><span data-stu-id="78eeb-120">The return type of a delegate type must be either `void`, or output-safe ([Variance safety](interfaces.md#variance-safety)).</span></span>

<span data-ttu-id="78eeb-121">Все типы формальных параметров типа делегата должен быть безопасным.</span><span class="sxs-lookup"><span data-stu-id="78eeb-121">All the formal parameter types of a delegate type must be input-safe.</span></span> <span data-ttu-id="78eeb-122">Кроме того, любая `out` или `ref` типы параметров также должны быть безопасным при выводе.</span><span class="sxs-lookup"><span data-stu-id="78eeb-122">Additionally, any `out` or `ref` parameter types must also be output-safe.</span></span> <span data-ttu-id="78eeb-123">Обратите внимание что даже `out` параметры, требуется ли входные данные с точки зрения, из-за ограничений базовой платформы выполнения.</span><span class="sxs-lookup"><span data-stu-id="78eeb-123">Note that even `out` parameters are required to be input-safe, due to a limitation of the underlying execution platform.</span></span>

<span data-ttu-id="78eeb-124">Типы делегатов в C# являются эквивалентом имени, не структурно эквивалентными.</span><span class="sxs-lookup"><span data-stu-id="78eeb-124">Delegate types in C# are name equivalent, not structurally equivalent.</span></span> <span data-ttu-id="78eeb-125">В частности две разные типы делегатов, которые имеют тот же параметр перечислены и типом возвращаемого значения считаются разными типами делегатов.</span><span class="sxs-lookup"><span data-stu-id="78eeb-125">Specifically, two different delegate types that have the same parameter lists and return type are considered different delegate types.</span></span> <span data-ttu-id="78eeb-126">Тем не менее, экземпляров двух типов различных, но структурно эквивалентных делегат может считаться равными ([делегировать операторы равенства](expressions.md#delegate-equality-operators)).</span><span class="sxs-lookup"><span data-stu-id="78eeb-126">However, instances of two distinct but structurally equivalent delegate types may compare as equal ([Delegate equality operators](expressions.md#delegate-equality-operators)).</span></span>

<span data-ttu-id="78eeb-127">Пример:</span><span class="sxs-lookup"><span data-stu-id="78eeb-127">For example:</span></span>

```csharp
delegate int D1(int i, double d);

class A
{
    public static int M1(int a, double b) {...}
}

class B
{
    delegate int D2(int c, double d);
    public static int M1(int f, double g) {...}
    public static void M2(int k, double l) {...}
    public static int M3(int g) {...}
    public static void M4(int g) {...}
}
```

<span data-ttu-id="78eeb-128">Методы `A.M1` и `B.M1 `совместимы с типами делегатов `D1` и `D2` , так как у них есть же возвращают тип и список параметров, однако эти типы делегатов являются два различных типа, поэтому они не взаимозаменяемыми.</span><span class="sxs-lookup"><span data-stu-id="78eeb-128">The methods `A.M1` and `B.M1 `are compatible with both the delegate types `D1` and `D2` , since they have the same return type and parameter list; however, these delegate types are two different types, so they are not interchangeable.</span></span> <span data-ttu-id="78eeb-129">Методы `B.M2`, `B.M3`, и `B.M4` несовместимы с типами делегатов `D1` и `D2`, так как они имеют разные типы возвращаемого значения или списки параметров.</span><span class="sxs-lookup"><span data-stu-id="78eeb-129">The methods `B.M2`, `B.M3`, and `B.M4` are incompatible with the delegate types `D1` and `D2`, since they have different return types or parameter lists.</span></span>

<span data-ttu-id="78eeb-130">Как и других объявлениях универсального типа необходимо предоставить аргументы типа для создания сконструированного типа делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-130">Like other generic type declarations, type arguments must be given to create a constructed delegate type.</span></span> <span data-ttu-id="78eeb-131">Типы параметров и тип возвращаемого значения сконструированного типа делегата создаются путем замены для каждого параметра типа в объявлении делегата, соответствующий аргумент типа из сконструированного типа делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-131">The parameter types and return type of a constructed delegate type are created by substituting, for each type parameter in the delegate declaration, the corresponding type argument of the constructed delegate type.</span></span> <span data-ttu-id="78eeb-132">Результирующий тип возвращаемого значения и типы параметров используются для определения, какие методы совместимы с сконструированного типа делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-132">The resulting return type and parameter types are used in determining what methods are compatible with a constructed delegate type.</span></span> <span data-ttu-id="78eeb-133">Пример:</span><span class="sxs-lookup"><span data-stu-id="78eeb-133">For example:</span></span>

```csharp
delegate bool Predicate<T>(T value);

class X
{
    static bool F(int i) {...}
    static bool G(string s) {...}
}
```

<span data-ttu-id="78eeb-134">Метод `X.F` совместим с типом делегата `Predicate<int>` и метод `X.G` совместим с типом делегата `Predicate<string>` .</span><span class="sxs-lookup"><span data-stu-id="78eeb-134">The method `X.F` is compatible with the delegate type `Predicate<int>` and the method `X.G` is compatible with the delegate type `Predicate<string>` .</span></span>

<span data-ttu-id="78eeb-135">Единственный способ объявления типа делегата — через *delegate_declaration*.</span><span class="sxs-lookup"><span data-stu-id="78eeb-135">The only way to declare a delegate type is via a *delegate_declaration*.</span></span> <span data-ttu-id="78eeb-136">Тип делегата является типом класса, который является производным от `System.Delegate`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-136">A delegate type is a class type that is derived from `System.Delegate`.</span></span> <span data-ttu-id="78eeb-137">Типы делегатов являются неявно `sealed`, поэтому не допускается выполнять наследование любого типа является типом делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-137">Delegate types are implicitly `sealed`, so it is not permissible to derive any type from a delegate type.</span></span> <span data-ttu-id="78eeb-138">Допускается также не являются производными класса не являющийся делегатом тип из `System.Delegate`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-138">It is also not permissible to derive a non-delegate class type from `System.Delegate`.</span></span> <span data-ttu-id="78eeb-139">Обратите внимание, что `System.Delegate` является сам по себе не тип делегата; он является типом класса, от которого наследуются все типы делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-139">Note that `System.Delegate` is not itself a delegate type; it is a class type from which all delegate types are derived.</span></span>

<span data-ttu-id="78eeb-140">C# предоставляет специальный синтаксис для делегата при создании экземпляра и вызов.</span><span class="sxs-lookup"><span data-stu-id="78eeb-140">C# provides special syntax for delegate instantiation and invocation.</span></span> <span data-ttu-id="78eeb-141">За исключением создания экземпляра любая операция, которая может применяться к классу или экземпляру класса могут также применяться к классу делегата или экземпляр, соответственно.</span><span class="sxs-lookup"><span data-stu-id="78eeb-141">Except for instantiation, any operation that can be applied to a class or class instance can also be applied to a delegate class or instance, respectively.</span></span> <span data-ttu-id="78eeb-142">В частности, можно получить доступ к членам `System.Delegate` тип с помощью синтаксиса доступа через обычные члена.</span><span class="sxs-lookup"><span data-stu-id="78eeb-142">In particular, it is possible to access members of the `System.Delegate` type via the usual member access syntax.</span></span>

<span data-ttu-id="78eeb-143">Набор методов, инкапсулированных в экземпляр делегата, называется списком вызовов.</span><span class="sxs-lookup"><span data-stu-id="78eeb-143">The set of methods encapsulated by a delegate instance is called an invocation list.</span></span> <span data-ttu-id="78eeb-144">При создании экземпляра делегата ([совместимость делегатов](delegates.md#delegate-compatibility)) из одного метода, он инкапсулирует этот метод, и списка вызовов содержит только одну запись.</span><span class="sxs-lookup"><span data-stu-id="78eeb-144">When a delegate instance is created ([Delegate compatibility](delegates.md#delegate-compatibility)) from a single method, it encapsulates that method, and its invocation list contains only one entry.</span></span> <span data-ttu-id="78eeb-145">Тем не менее когда объединяются два экземпляра делегата отличное от null, их списки вызовов сцепляются — в порядке слева операнд, а затем правый операнд — для формирования нового списка вызова, который содержит две или несколько записей.</span><span class="sxs-lookup"><span data-stu-id="78eeb-145">However, when two non-null delegate instances are combined, their invocation lists are concatenated -- in the order left operand then right operand -- to form a new invocation list, which contains two or more entries.</span></span>

<span data-ttu-id="78eeb-146">Делегаты объединяются с помощью двоичного файла `+` ([оператор сложения](expressions.md#addition-operator)) и `+=` операторы ([Составное присваивание](expressions.md#compound-assignment)).</span><span class="sxs-lookup"><span data-stu-id="78eeb-146">Delegates are combined using the binary `+` ([Addition operator](expressions.md#addition-operator)) and `+=` operators ([Compound assignment](expressions.md#compound-assignment)).</span></span> <span data-ttu-id="78eeb-147">Делегат можно удалить из нескольких делегатов, с помощью двоичного файла `-` ([оператор вычитания](expressions.md#subtraction-operator)) и `-=` операторы ([Составное присваивание](expressions.md#compound-assignment)).</span><span class="sxs-lookup"><span data-stu-id="78eeb-147">A delegate can be removed from a combination of delegates, using the binary `-` ([Subtraction operator](expressions.md#subtraction-operator)) and `-=` operators ([Compound assignment](expressions.md#compound-assignment)).</span></span> <span data-ttu-id="78eeb-148">Делегаты можно сравнить на равенство ([делегировать операторы равенства](expressions.md#delegate-equality-operators)).</span><span class="sxs-lookup"><span data-stu-id="78eeb-148">Delegates can be compared for equality ([Delegate equality operators](expressions.md#delegate-equality-operators)).</span></span>

<span data-ttu-id="78eeb-149">В следующем примере показано создание нескольких делегатов, и их соответствующие списки вызова:</span><span class="sxs-lookup"><span data-stu-id="78eeb-149">The following example shows the instantiation of a number of delegates, and their corresponding invocation lists:</span></span>

```csharp
delegate void D(int x);

class C
{
    public static void M1(int i) {...}
    public static void M2(int i) {...}

}

class Test
{
    static void Main() {
        D cd1 = new D(C.M1);      // M1
        D cd2 = new D(C.M2);      // M2
        D cd3 = cd1 + cd2;        // M1 + M2
        D cd4 = cd3 + cd1;        // M1 + M2 + M1
        D cd5 = cd4 + cd3;        // M1 + M2 + M1 + M1 + M2
    }

}
```

<span data-ttu-id="78eeb-150">Когда `cd1` и `cd2` являются создан, каждый из них инкапсулирует один метод.</span><span class="sxs-lookup"><span data-stu-id="78eeb-150">When `cd1` and `cd2` are instantiated, they each encapsulate one method.</span></span> <span data-ttu-id="78eeb-151">При `cd3` будет создан, он имеет список вызова из двух методов `M1` и `M2`в этом порядке.</span><span class="sxs-lookup"><span data-stu-id="78eeb-151">When `cd3` is instantiated, it has an invocation list of two methods, `M1` and `M2`, in that order.</span></span> <span data-ttu-id="78eeb-152">`cd4`в список вызова содержит `M1`, `M2`, и `M1`в этом порядке.</span><span class="sxs-lookup"><span data-stu-id="78eeb-152">`cd4`'s invocation list contains `M1`, `M2`, and `M1`, in that order.</span></span> <span data-ttu-id="78eeb-153">Наконец `cd5`в список вызова содержит `M1`, `M2`, `M1`, `M1`, и `M2`в этом порядке.</span><span class="sxs-lookup"><span data-stu-id="78eeb-153">Finally, `cd5`'s invocation list contains `M1`, `M2`, `M1`, `M1`, and `M2`, in that order.</span></span> <span data-ttu-id="78eeb-154">Дополнительные примеры объединения делегатов (а также удаления), см. в разделе [вызов делегата](delegates.md#delegate-invocation).</span><span class="sxs-lookup"><span data-stu-id="78eeb-154">For more examples of combining (as well as removing) delegates, see [Delegate invocation](delegates.md#delegate-invocation).</span></span>

## <a name="delegate-compatibility"></a><span data-ttu-id="78eeb-155">Совместимость делегатов</span><span class="sxs-lookup"><span data-stu-id="78eeb-155">Delegate compatibility</span></span>

<span data-ttu-id="78eeb-156">Метод или делегат `M` — ***совместимых*** с типом делегата `D` если выполняются все следующие условия:</span><span class="sxs-lookup"><span data-stu-id="78eeb-156">A method or delegate `M` is ***compatible*** with a delegate type `D` if all of the following are true:</span></span>

*  <span data-ttu-id="78eeb-157">`D` и `M` имеют одинаковый номер параметров, и каждый параметр в `D` имеет те же `ref` или `out` модификаторы, что и соответствующий параметр в `M`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-157">`D` and `M` have the same number of parameters, and each parameter in `D` has the same `ref` or `out` modifiers as the corresponding parameter in `M`.</span></span>
*  <span data-ttu-id="78eeb-158">Для каждого параметра значения (параметр, не имеющий `ref` или `out` модификатор), преобразование идентификации ([преобразование идентификации](conversions.md#identity-conversion)) или неявное преобразование ссылок ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)) существует от типа параметра в `D` к типу соответствующего параметра в `M`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-158">For each value parameter (a parameter with no `ref` or `out` modifier), an identity conversion ([Identity conversion](conversions.md#identity-conversion)) or implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from the parameter type in `D` to the corresponding parameter type in `M`.</span></span>
*  <span data-ttu-id="78eeb-159">Для каждого `ref` или `out` параметра, тип параметра в `D` совпадает со значением параметра типа в `M`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-159">For each `ref` or `out` parameter, the parameter type in `D` is the same as the parameter type in `M`.</span></span>
*  <span data-ttu-id="78eeb-160">Удостоверение или неявное преобразование ссылок существует тип возвращаемого значения `M` для возвращаемого типа `D`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-160">An identity or implicit reference conversion exists from the return type of `M` to the return type of `D`.</span></span>

## <a name="delegate-instantiation"></a><span data-ttu-id="78eeb-161">Создание экземпляров делегатов</span><span class="sxs-lookup"><span data-stu-id="78eeb-161">Delegate instantiation</span></span>

<span data-ttu-id="78eeb-162">Созданный экземпляр делегата *delegate_creation_expression* ([выражения создания делегата](expressions.md#delegate-creation-expressions)) или преобразование к типу делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-162">An instance of a delegate is created by a *delegate_creation_expression* ([Delegate creation expressions](expressions.md#delegate-creation-expressions)) or a conversion to a delegate type.</span></span> <span data-ttu-id="78eeb-163">Экземпляр созданного делегата затем ссылается один:</span><span class="sxs-lookup"><span data-stu-id="78eeb-163">The newly created delegate instance then refers to either:</span></span>

*  <span data-ttu-id="78eeb-164">Ссылки на статический метод *delegate_creation_expression*, или</span><span class="sxs-lookup"><span data-stu-id="78eeb-164">The static method referenced in the *delegate_creation_expression*, or</span></span>
*  <span data-ttu-id="78eeb-165">Целевой объект (который не может быть `null`) и ссылки на метод экземпляра *delegate_creation_expression*, или</span><span class="sxs-lookup"><span data-stu-id="78eeb-165">The target object (which cannot be `null`) and instance method referenced in the *delegate_creation_expression*, or</span></span>
*  <span data-ttu-id="78eeb-166">Другой делегат.</span><span class="sxs-lookup"><span data-stu-id="78eeb-166">Another delegate.</span></span>

<span data-ttu-id="78eeb-167">Пример:</span><span class="sxs-lookup"><span data-stu-id="78eeb-167">For example:</span></span>

```csharp
delegate void D(int x);

class C
{
    public static void M1(int i) {...}
    public void M2(int i) {...}
}

class Test
{
    static void Main() { 
        D cd1 = new D(C.M1);        // static method
        C t = new C();
        D cd2 = new D(t.M2);        // instance method
        D cd3 = new D(cd2);        // another delegate
    }
}
```

<span data-ttu-id="78eeb-168">После создания экземпляра, экземпляры делегата всегда относятся к тем же целевой объект и метод.</span><span class="sxs-lookup"><span data-stu-id="78eeb-168">Once instantiated, delegate instances always refer to the same target object and method.</span></span> <span data-ttu-id="78eeb-169">Помните, что при объединении двух делегатов или удалении одного из другой, результате создается новый делегат со своим собственным списком вызова; списки вызовов делегатов объединять или удалять остаются неизменными.</span><span class="sxs-lookup"><span data-stu-id="78eeb-169">Remember, when two delegates are combined, or one is removed from another, a new delegate results with its own invocation list; the invocation lists of the delegates combined or removed remain unchanged.</span></span>

## <a name="delegate-invocation"></a><span data-ttu-id="78eeb-170">Вызов делегатов</span><span class="sxs-lookup"><span data-stu-id="78eeb-170">Delegate invocation</span></span>

<span data-ttu-id="78eeb-171">C# предоставляет специальный синтаксис для вызова делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-171">C# provides special syntax for invoking a delegate.</span></span> <span data-ttu-id="78eeb-172">Когда вызывается экземпляр делегата отличное от null, список вызовов которого содержит одну запись, он вызывает один метод с теми же аргументами, он был задан и возвращает то же значение, как указано в метод.</span><span class="sxs-lookup"><span data-stu-id="78eeb-172">When a non-null delegate instance whose invocation list contains one entry is invoked, it invokes the one method with the same arguments it was given, and returns the same value as the referred to method.</span></span> <span data-ttu-id="78eeb-173">(См. в разделе [вызовы делегатов](expressions.md#delegate-invocations) подробные сведения о вызове делегата.) Если исключение возникает при вызове такого делегата, и это исключение не перехватывается в вызванном методе, поиск предложения перехвата исключения продолжается в методе, который вызывается делегат, как если прямой вызов этого метода метод, к которому делегат называется.</span><span class="sxs-lookup"><span data-stu-id="78eeb-173">(See [Delegate invocations](expressions.md#delegate-invocations) for detailed information on delegate invocation.) If an exception occurs during the invocation of such a delegate, and that exception is not caught within the method that was invoked, the search for an exception catch clause continues in the method that called the delegate, as if that method had directly called the method to which that delegate referred.</span></span>

<span data-ttu-id="78eeb-174">Вызов экземпляр делегата, список вызовов которого содержит несколько записей выполняется путем вызова всех методов в списке вызова синхронно, в порядке.</span><span class="sxs-lookup"><span data-stu-id="78eeb-174">Invocation of a delegate instance whose invocation list contains multiple entries proceeds by invoking each of the methods in the invocation list, synchronously, in order.</span></span> <span data-ttu-id="78eeb-175">Каждый метод так называемых передается тот же набор параметров, заданный экземпляру делегата.</span><span class="sxs-lookup"><span data-stu-id="78eeb-175">Each method so called is passed the same set of arguments as was given to the delegate instance.</span></span> <span data-ttu-id="78eeb-176">Если такой вызов делегата включает параметры ссылок ([ссылочные параметры](classes.md#reference-parameters)), каждый вызов метода происходит со ссылкой на той же переменной; изменения в эту переменную в списке вызова одного из методов будут Видимый для дальнейшего методы списке вызова.</span><span class="sxs-lookup"><span data-stu-id="78eeb-176">If such a delegate invocation includes reference parameters ([Reference parameters](classes.md#reference-parameters)), each method invocation will occur with a reference to the same variable; changes to that variable by one method in the invocation list will be visible to methods further down the invocation list.</span></span> <span data-ttu-id="78eeb-177">Если вызов делегата включает выходные параметры или возвращаемое значение, их окончательное значение будет получено от вызова последнего делегата в списке.</span><span class="sxs-lookup"><span data-stu-id="78eeb-177">If the delegate invocation includes output parameters or a return value, their final value will come from the invocation of the last delegate in the list.</span></span>

<span data-ttu-id="78eeb-178">При возникновении исключения во время обработки вызова такого делегата, и это исключение не перехватывается в вызванном методе, продолжает поиск предложения перехвата исключения в методе, который вызывается делегат, а также любые методы, расположенным ниже список вызовов, не вызываются.</span><span class="sxs-lookup"><span data-stu-id="78eeb-178">If an exception occurs during processing of the invocation of such a delegate, and that exception is not caught within the method that was invoked, the search for an exception catch clause continues in the method that called the delegate, and any methods further down the invocation list are not invoked.</span></span>

<span data-ttu-id="78eeb-179">Попытка вызвать экземпляр делегата, значение которого равно null приводят к возникновению исключения типа `System.NullReferenceException`.</span><span class="sxs-lookup"><span data-stu-id="78eeb-179">Attempting to invoke a delegate instance whose value is null results in an exception of type `System.NullReferenceException`.</span></span>

<span data-ttu-id="78eeb-180">В следующем примере показано, как создать экземпляр, объединения, удаления и вызова делегатов:</span><span class="sxs-lookup"><span data-stu-id="78eeb-180">The following example shows how to instantiate, combine, remove, and invoke delegates:</span></span>

```csharp
using System;

delegate void D(int x);

class C
{
    public static void M1(int i) {
        Console.WriteLine("C.M1: " + i);
    }

    public static void M2(int i) {
        Console.WriteLine("C.M2: " + i);
    }

    public void M3(int i) {
        Console.WriteLine("C.M3: " + i);
    }
}

class Test
{
    static void Main() { 
        D cd1 = new D(C.M1);
        cd1(-1);                // call M1

        D cd2 = new D(C.M2);
        cd2(-2);                // call M2

        D cd3 = cd1 + cd2;
        cd3(10);                // call M1 then M2

        cd3 += cd1;
        cd3(20);                // call M1, M2, then M1

        C c = new C();
        D cd4 = new D(c.M3);
        cd3 += cd4;
        cd3(30);                // call M1, M2, M1, then M3

        cd3 -= cd1;             // remove last M1
        cd3(40);                // call M1, M2, then M3

        cd3 -= cd4;
        cd3(50);                // call M1 then M2

        cd3 -= cd2;
        cd3(60);                // call M1

        cd3 -= cd2;             // impossible removal is benign
        cd3(60);                // call M1

        cd3 -= cd1;             // invocation list is empty so cd3 is null

        cd3(70);                // System.NullReferenceException thrown

        cd3 -= cd1;             // impossible removal is benign
    }
}
```

<span data-ttu-id="78eeb-181">Как показано в инструкции `cd3 += cd1;`, делегат могут присутствовать в списке вызова несколько раз.</span><span class="sxs-lookup"><span data-stu-id="78eeb-181">As shown in the statement `cd3 += cd1;`, a delegate can be present in an invocation list multiple times.</span></span> <span data-ttu-id="78eeb-182">В этом случае он просто вызывается один раз за вхождения.</span><span class="sxs-lookup"><span data-stu-id="78eeb-182">In this case, it is simply invoked once per occurrence.</span></span> <span data-ttu-id="78eeb-183">В списке вызова, как это при удалении этого делегата последнего вхождения в списке вызовов является фактически удаляется.</span><span class="sxs-lookup"><span data-stu-id="78eeb-183">In an invocation list such as this, when that delegate is removed, the last occurrence in the invocation list is the one actually removed.</span></span>

<span data-ttu-id="78eeb-184">Немедленно до выполнения последнего оператора `cd3 -= cd1;`, делегат `cd3` ссылается на пустой список вызова.</span><span class="sxs-lookup"><span data-stu-id="78eeb-184">Immediately prior to the execution of the final statement, `cd3 -= cd1;`, the delegate `cd3` refers to an empty invocation list.</span></span> <span data-ttu-id="78eeb-185">Попытка удаления делегата из пустого списка (или удаления несуществующего делегата из списка непустой) не является ошибкой.</span><span class="sxs-lookup"><span data-stu-id="78eeb-185">Attempting to remove a delegate from an empty list (or to remove a non-existent delegate from a non-empty list) is not an error.</span></span>

<span data-ttu-id="78eeb-186">— Выходные данные:</span><span class="sxs-lookup"><span data-stu-id="78eeb-186">The output produced is:</span></span>

```
C.M1: -1
C.M2: -2
C.M1: 10
C.M2: 10
C.M1: 20
C.M2: 20
C.M1: 20
C.M1: 30
C.M2: 30
C.M1: 30
C.M3: 30
C.M1: 40
C.M2: 40
C.M3: 40
C.M1: 50
C.M2: 50
C.M1: 60
C.M1: 60
```
