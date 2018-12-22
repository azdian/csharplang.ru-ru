# <a name="interfaces"></a><span data-ttu-id="e39d7-101">интерфейсов,</span><span class="sxs-lookup"><span data-stu-id="e39d7-101">Interfaces</span></span>

<span data-ttu-id="e39d7-102">Интерфейс определяет контракт.</span><span class="sxs-lookup"><span data-stu-id="e39d7-102">An interface defines a contract.</span></span> <span data-ttu-id="e39d7-103">Класс или структура, реализующие интерфейс необходимо придерживаться этого контракта.</span><span class="sxs-lookup"><span data-stu-id="e39d7-103">A class or struct that implements an interface must adhere to its contract.</span></span> <span data-ttu-id="e39d7-104">Интерфейс может наследовать от нескольких базовых интерфейсах и класс или структура может реализовывать несколько интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-104">An interface may inherit from multiple base interfaces, and a class or struct may implement multiple interfaces.</span></span>

<span data-ttu-id="e39d7-105">Интерфейсы могут содержать методы, свойства, события и индексаторы.</span><span class="sxs-lookup"><span data-stu-id="e39d7-105">Interfaces can contain methods, properties, events, and indexers.</span></span> <span data-ttu-id="e39d7-106">Сам интерфейс не предоставляет реализаций для членов, которые он определяет.</span><span class="sxs-lookup"><span data-stu-id="e39d7-106">The interface itself does not provide implementations for the members that it defines.</span></span> <span data-ttu-id="e39d7-107">Интерфейс лишь перечисляет члены, которые должны быть определены в классах или структурах, реализующих этот интерфейс.</span><span class="sxs-lookup"><span data-stu-id="e39d7-107">The interface merely specifies the members that must be supplied by classes or structs that implement the interface.</span></span>

## <a name="interface-declarations"></a><span data-ttu-id="e39d7-108">Объявления интерфейсов</span><span class="sxs-lookup"><span data-stu-id="e39d7-108">Interface declarations</span></span>

<span data-ttu-id="e39d7-109">*Interface_declaration* — *type_declaration* ([объявления типов](namespaces.md#type-declarations)), объявляет новый тип интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-109">An *interface_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new interface type.</span></span>

```antlr
interface_declaration
    : attributes? interface_modifier* 'partial'? 'interface'
      identifier variant_type_parameter_list? interface_base?
      type_parameter_constraints_clause* interface_body ';'?
    ;
```

<span data-ttu-id="e39d7-110">*Interface_declaration* состоит из необязательного набора *атрибуты* ([атрибуты](attributes.md)), а затем необязательный набор *interface_modifier*s ([модификаторы интерфейса](interfaces.md#interface-modifiers)), а затем использовать необязательный `partial` модификатор, а затем с помощью ключевого слова `interface` и *идентификатор* , которая содержит название интерфейса следуют необязательный *variant_type_parameter_list* спецификации ([списков параметров типа Variant](interfaces.md#variant-type-parameter-lists)), а затем использовать необязательный *interface_base* Спецификация ([базовые интерфейсы](interfaces.md#base-interfaces)), а затем использовать необязательный *type_parameter_constraints_clause*спецификации s ([ограничения параметров типа](classes.md#type-parameter-constraints)) , за которым следует *interface_body* ([тело интерфейса](interfaces.md#interface-body)), при необходимости, а затем точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="e39d7-110">An *interface_declaration* consists of an optional set of *attributes* ([Attributes](attributes.md)), followed by an optional set of *interface_modifier*s ([Interface modifiers](interfaces.md#interface-modifiers)), followed by an optional `partial` modifier, followed by the keyword `interface` and an *identifier* that names the interface, followed by an optional *variant_type_parameter_list* specification ([Variant type parameter lists](interfaces.md#variant-type-parameter-lists)), followed by an optional *interface_base* specification ([Base interfaces](interfaces.md#base-interfaces)), followed by an optional *type_parameter_constraints_clause*s specification ([Type parameter constraints](classes.md#type-parameter-constraints)), followed by an *interface_body* ([Interface body](interfaces.md#interface-body)), optionally followed by a semicolon.</span></span>

### <a name="interface-modifiers"></a><span data-ttu-id="e39d7-111">Модификаторы интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-111">Interface modifiers</span></span>

<span data-ttu-id="e39d7-112">*Interface_declaration* может включать последовательность модификаторов интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e39d7-112">An *interface_declaration* may optionally include a sequence of interface modifiers:</span></span>

```antlr
interface_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | interface_modifier_unsafe
    ;
```

<span data-ttu-id="e39d7-113">Это ошибка времени компиляции для один и тот же модификатор встречается несколько раз в объявлении интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-113">It is a compile-time error for the same modifier to appear multiple times in an interface declaration.</span></span>

<span data-ttu-id="e39d7-114">`new` Модификатор должен находиться на интерфейсы, определенные в классе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-114">The `new` modifier is only permitted on interfaces defined within a class.</span></span> <span data-ttu-id="e39d7-115">Он указывает, что интерфейс скрывает унаследованный член с тем же именем, как описано в разделе [Модификатор new](classes.md#the-new-modifier).</span><span class="sxs-lookup"><span data-stu-id="e39d7-115">It specifies that the interface hides an inherited member by the same name, as described in [The new modifier](classes.md#the-new-modifier).</span></span>

<span data-ttu-id="e39d7-116">`public`, `protected`, `internal`, И `private` модификаторы определяют доступность интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-116">The `public`, `protected`, `internal`, and `private` modifiers control the accessibility of the interface.</span></span> <span data-ttu-id="e39d7-117">В зависимости от контекста, в котором производится объявление интерфейса, могут быть разрешены только некоторые из этих модификаторов ([объявленную доступность](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-117">Depending on the context in which the interface declaration occurs, only some of these modifiers may be permitted ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

### <a name="partial-modifier"></a><span data-ttu-id="e39d7-118">Модификатор partial</span><span class="sxs-lookup"><span data-stu-id="e39d7-118">Partial modifier</span></span>

<span data-ttu-id="e39d7-119">`partial` Модификатор указывает, что это *interface_declaration* является объявлением разделяемого типа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-119">The `partial` modifier indicates that this *interface_declaration* is a partial type declaration.</span></span> <span data-ttu-id="e39d7-120">Несколько объявлений частичного интерфейса с тем же именем в едином объявлении пространства имен или типа объединяются в одно объявление интерфейса, следуя правилам указан в [разделяемых типов](classes.md#partial-types).</span><span class="sxs-lookup"><span data-stu-id="e39d7-120">Multiple partial interface declarations with the same name within an enclosing namespace or type declaration combine to form one interface declaration, following the rules specified in [Partial types](classes.md#partial-types).</span></span>

### <a name="variant-type-parameter-lists"></a><span data-ttu-id="e39d7-121">Списки параметров типа варианта</span><span class="sxs-lookup"><span data-stu-id="e39d7-121">Variant type parameter lists</span></span>

<span data-ttu-id="e39d7-122">Списки параметров типа варианта возможна только на типы интерфейсов и делегатов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-122">Variant type parameter lists can only occur on interface and delegate types.</span></span> <span data-ttu-id="e39d7-123">Отличие от обычного *type_parameter_list*s необязателен *variance_annotation* для каждого типа параметра.</span><span class="sxs-lookup"><span data-stu-id="e39d7-123">The difference from ordinary *type_parameter_list*s is the optional *variance_annotation* on each type parameter.</span></span>

```antlr
variant_type_parameter_list
    : '<' variant_type_parameters '>'
    ;

variant_type_parameters
    : attributes? variance_annotation? type_parameter
    | variant_type_parameters ',' attributes? variance_annotation? type_parameter
    ;

variance_annotation
    : 'in'
    | 'out'
    ;
```

<span data-ttu-id="e39d7-124">Значение, если заметка дисперсия `out`, параметр типа считается ***ковариантным***.</span><span class="sxs-lookup"><span data-stu-id="e39d7-124">If the variance annotation is `out`, the type parameter is said to be ***covariant***.</span></span> <span data-ttu-id="e39d7-125">Значение, если заметка дисперсия `in`, параметр типа считается ***контравариантным***.</span><span class="sxs-lookup"><span data-stu-id="e39d7-125">If the variance annotation is `in`, the type parameter is said to be ***contravariant***.</span></span> <span data-ttu-id="e39d7-126">Если ни одна заметка не дисперсия, параметр типа считается ***инвариантного***.</span><span class="sxs-lookup"><span data-stu-id="e39d7-126">If there is no variance annotation, the type parameter is said to be ***invariant***.</span></span>

<span data-ttu-id="e39d7-127">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-127">In the example</span></span>
```csharp
interface C<out X, in Y, Z> 
{
  X M(Y y);
  Z P { get; set; }
}
```
<span data-ttu-id="e39d7-128">`X` является ковариантным, `Y` является контравариантным и `Z` является инвариантным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-128">`X` is covariant, `Y` is contravariant and `Z` is invariant.</span></span>

#### <a name="variance-safety"></a><span data-ttu-id="e39d7-129">Безопасность вариативности</span><span class="sxs-lookup"><span data-stu-id="e39d7-129">Variance safety</span></span>

<span data-ttu-id="e39d7-130">Вхождение вариантные заметки в списке параметров типа ограничивает местах, где может произойти типы в объявлении типа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-130">The occurrence of variance annotations in the type parameter list of a type restricts the places where types can occur within the type declaration.</span></span>

<span data-ttu-id="e39d7-131">Тип `T` — ***небезопасным при выводе*** Если справедливо одно из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="e39d7-131">A type `T` is ***output-unsafe*** if one of the following holds:</span></span>

*  <span data-ttu-id="e39d7-132">`T` является параметром контравариантного типа</span><span class="sxs-lookup"><span data-stu-id="e39d7-132">`T` is a contravariant type parameter</span></span>
*  <span data-ttu-id="e39d7-133">`T` является типом массива с типом элемента небезопасный выходных данных</span><span class="sxs-lookup"><span data-stu-id="e39d7-133">`T` is an array type with an output-unsafe element type</span></span>
*  <span data-ttu-id="e39d7-134">`T` является типом интерфейса или делегата `S<A1,...,Ak>` создан на основе универсального типа `S<X1,...,Xk>` where хотя бы для одного `Ai` содержит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="e39d7-134">`T` is an interface or delegate type `S<A1,...,Ak>` constructed from a generic type `S<X1,...,Xk>` where for at least one `Ai` one of the following holds:</span></span>
   * <span data-ttu-id="e39d7-135">`Xi` является ковариантным или инвариантным и `Ai` является небезопасным при выводе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-135">`Xi` is covariant or invariant and `Ai` is output-unsafe.</span></span>
   * <span data-ttu-id="e39d7-136">`Xi` является ковариантным или инвариантным и `Ai` является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-136">`Xi` is contravariant or invariant and `Ai` is input-safe.</span></span>
   
<span data-ttu-id="e39d7-137">Тип `T` — ***небезопасным*** Если справедливо одно из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="e39d7-137">A type `T` is ***input-unsafe*** if one of the following holds:</span></span>

*  <span data-ttu-id="e39d7-138">`T` параметр ковариантного типа</span><span class="sxs-lookup"><span data-stu-id="e39d7-138">`T` is a covariant type parameter</span></span>
*  <span data-ttu-id="e39d7-139">`T` является типом массива с типом элемента небезопасным</span><span class="sxs-lookup"><span data-stu-id="e39d7-139">`T` is an array type with an input-unsafe element type</span></span>
*  <span data-ttu-id="e39d7-140">`T` является типом интерфейса или делегата `S<A1,...,Ak>` создан на основе универсального типа `S<X1,...,Xk>` where хотя бы для одного `Ai` содержит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="e39d7-140">`T` is an interface or delegate type `S<A1,...,Ak>` constructed from a generic type `S<X1,...,Xk>` where for at least one `Ai` one of the following holds:</span></span>
   * <span data-ttu-id="e39d7-141">`Xi` является ковариантным или инвариантным и `Ai` является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-141">`Xi` is covariant or invariant and `Ai` is input-unsafe.</span></span>
   * <span data-ttu-id="e39d7-142">`Xi` является ковариантным или инвариантным и `Ai` является небезопасным при выводе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-142">`Xi` is contravariant or invariant and `Ai` is output-unsafe.</span></span>

<span data-ttu-id="e39d7-143">Интуитивно понятным образом выходные данные небезопасного типа запрещено использовать в позиции вывода, и является небезопасным типом запрещена в позиции ввода.</span><span class="sxs-lookup"><span data-stu-id="e39d7-143">Intuitively, an output-unsafe type is prohibited in an output position, and an input-unsafe type is prohibited in an input position.</span></span>

<span data-ttu-id="e39d7-144">Тип — ***безопасным при выводе*** в случае вывода unsafe, и ***безопасным*** если он не является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-144">A type is ***output-safe*** if it is not output-unsafe, and ***input-safe*** if it is not input-unsafe.</span></span>

#### <a name="variance-conversion"></a><span data-ttu-id="e39d7-145">Вариантное преобразование</span><span class="sxs-lookup"><span data-stu-id="e39d7-145">Variance conversion</span></span>

<span data-ttu-id="e39d7-146">Вариантные заметки предназначена для обеспечения менее строгую (но по-прежнему типобезопасным) для преобразования в типы интерфейсов и делегатов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-146">The purpose of variance annotations is to provide for more lenient (but still type safe) conversions to interface and delegate types.</span></span> <span data-ttu-id="e39d7-147">К этому окончания определения неявные ([неявные преобразования](conversions.md#implicit-conversions)) и явные преобразования ([явные преобразования](conversions.md#explicit-conversions)) сделать использование понятие вариантного преобразования, который определен следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e39d7-147">To this end the definitions of implicit ([Implicit conversions](conversions.md#implicit-conversions)) and explicit conversions ([Explicit conversions](conversions.md#explicit-conversions)) make use of the notion of variance-convertibility, which is defined as follows:</span></span>

<span data-ttu-id="e39d7-148">Тип `T<A1,...,An>` является вариантно преобразуемым к типу `T<B1,...,Bn>` Если `T` тип делегата, либо интерфейс объявлен с параметрами вариантного типа `T<X1,...,Xn>`и для каждого параметра типа variant `Xi` одно из следующих содержит:</span><span class="sxs-lookup"><span data-stu-id="e39d7-148">A type `T<A1,...,An>` is variance-convertible to a type `T<B1,...,Bn>` if `T` is either an interface or a delegate type declared with the variant type parameters `T<X1,...,Xn>`, and for each variant type parameter `Xi` one of the following holds:</span></span>

*  <span data-ttu-id="e39d7-149">`Xi` является ковариантным и существует неявное преобразование идентификации или ссылки из `Ai` для `Bi`</span><span class="sxs-lookup"><span data-stu-id="e39d7-149">`Xi` is covariant and an implicit reference or identity conversion exists from `Ai` to `Bi`</span></span>
*  <span data-ttu-id="e39d7-150">`Xi` является контравариантным и неявные ссылки, или существует преобразование удостоверения из `Bi` для `Ai`</span><span class="sxs-lookup"><span data-stu-id="e39d7-150">`Xi` is contravariant and an implicit reference or identity conversion exists from `Bi` to `Ai`</span></span>
*  <span data-ttu-id="e39d7-151">`Xi` неизменяемое имя и удостоверение существует преобразования из `Ai` для `Bi`</span><span class="sxs-lookup"><span data-stu-id="e39d7-151">`Xi` is invariant and an identity conversion exists from `Ai` to `Bi`</span></span>

### <a name="base-interfaces"></a><span data-ttu-id="e39d7-152">Базовые интерфейсы</span><span class="sxs-lookup"><span data-stu-id="e39d7-152">Base interfaces</span></span>

<span data-ttu-id="e39d7-153">Интерфейс может наследовать из нуля или более типов интерфейсов, которые называются ***явные базовые интерфейсы*** интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-153">An interface can inherit from zero or more interface types, which are called the ***explicit base interfaces*** of the interface.</span></span> <span data-ttu-id="e39d7-154">Если интерфейс содержит один или несколько явные базовые интерфейсы, затем в объявлении этого интерфейса, идентификатор интерфейса следует двоеточие и запятую с запятыми список типов базового интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-154">When an interface has one or more explicit base interfaces, then in the declaration of that interface, the interface identifier is followed by a colon and a comma separated list of base interface types.</span></span>

```antlr
interface_base
    : ':' interface_type_list
    ;
```

<span data-ttu-id="e39d7-155">Для интерфейса сформированного типа, явные базовые интерфейсы сформированным путем объявления явного базового интерфейса в объявлении универсального типа, замещения для каждого *параметр_типа* в базовом интерфейсе объявления, соответствующего *type_argument* сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-155">For a constructed interface type, the explicit base interfaces are formed by taking the explicit base interface declarations on the generic type declaration, and substituting, for each *type_parameter* in the base interface declaration, the corresponding *type_argument* of the constructed type.</span></span>

<span data-ttu-id="e39d7-156">Явные базовые интерфейсы интерфейса должен быть по крайней мере такой же уровень доступности, как сам интерфейс ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-156">The explicit base interfaces of an interface must be at least as accessible as the interface itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span> <span data-ttu-id="e39d7-157">Например, это ошибка времени компиляции для указания `private` или `internal` интерфейс *interface_base* из `public` интерфейс.</span><span class="sxs-lookup"><span data-stu-id="e39d7-157">For example, it is a compile-time error to specify a `private` or `internal` interface in the *interface_base* of a `public` interface.</span></span>

<span data-ttu-id="e39d7-158">Это ошибка времени компиляции, прямо или косвенно наследовать от себя самого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-158">It is a compile-time error for an interface to directly or indirectly inherit from itself.</span></span>

<span data-ttu-id="e39d7-159">***Базовые интерфейсы*** интерфейса являются явные базовые интерфейсы и их базовые интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="e39d7-159">The ***base interfaces*** of an interface are the explicit base interfaces and their base interfaces.</span></span> <span data-ttu-id="e39d7-160">Другими словами набор базовых интерфейсов является завершения транзитивное замыкание явные базовые интерфейсы, явные базовые интерфейсы и т. д.</span><span class="sxs-lookup"><span data-stu-id="e39d7-160">In other words, the set of base interfaces is the complete transitive closure of the explicit base interfaces, their explicit base interfaces, and so on.</span></span> <span data-ttu-id="e39d7-161">Интерфейс наследует все члены из его базовых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-161">An interface inherits all members of its base interfaces.</span></span> <span data-ttu-id="e39d7-162">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-162">In the example</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

interface IListBox: IControl
{
    void SetItems(string[] items);
}

interface IComboBox: ITextBox, IListBox {}
```
<span data-ttu-id="e39d7-163">базовые интерфейсы `IComboBox` являются `IControl`, `ITextBox`, и `IListBox`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-163">the base interfaces of `IComboBox` are `IControl`, `ITextBox`, and `IListBox`.</span></span>

<span data-ttu-id="e39d7-164">Другими словами `IComboBox` наследует члены `SetText` и `SetItems` производительны `Paint`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-164">In other words, the `IComboBox` interface above inherits members `SetText` and `SetItems` as well as `Paint`.</span></span>

<span data-ttu-id="e39d7-165">Каждый базовый интерфейс интерфейса должен быть безопасным при выводе ([безопасность вариативности](interfaces.md#variance-safety)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-165">Every base interface of an interface must be output-safe ([Variance safety](interfaces.md#variance-safety)).</span></span> <span data-ttu-id="e39d7-166">Класс или структура, реализующие интерфейс, также неявно реализует все интерфейсы базового интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-166">A class or struct that implements an interface also implicitly implements all of the interface's base interfaces.</span></span>

### <a name="interface-body"></a><span data-ttu-id="e39d7-167">Теле интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-167">Interface body</span></span>

<span data-ttu-id="e39d7-168">*Interface_body* интерфейса определяет членов интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-168">The *interface_body* of an interface defines the members of the interface.</span></span>

```antlr
interface_body
    : '{' interface_member_declaration* '}'
    ;
```

## <a name="interface-members"></a><span data-ttu-id="e39d7-169">Члены интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-169">Interface members</span></span>

<span data-ttu-id="e39d7-170">Члены интерфейса являются члены, унаследованные от базовых интерфейсов и элементов, объявленных в самом интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-170">The members of an interface are the members inherited from the base interfaces and the members declared by the interface itself.</span></span>

```antlr
interface_member_declaration
    : interface_method_declaration
    | interface_property_declaration
    | interface_event_declaration
    | interface_indexer_declaration
    ;
```

<span data-ttu-id="e39d7-171">Объявление интерфейса может объявлять ноль или несколько членов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-171">An interface declaration may declare zero or more members.</span></span> <span data-ttu-id="e39d7-172">Члены интерфейса должны быть методы, свойства, события и индексаторы.</span><span class="sxs-lookup"><span data-stu-id="e39d7-172">The members of an interface must be methods, properties, events, or indexers.</span></span> <span data-ttu-id="e39d7-173">Интерфейс не может содержать константы, поля, операторы, конструкторы экземпляров, деструкторы или типы, а также интерфейс должен содержать статические члены любого типа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-173">An interface cannot contain constants, fields, operators, instance constructors, destructors, or types, nor can an interface contain static members of any kind.</span></span>

<span data-ttu-id="e39d7-174">Все члены интерфейса неявно имеют общий доступ.</span><span class="sxs-lookup"><span data-stu-id="e39d7-174">All interface members implicitly have public access.</span></span> <span data-ttu-id="e39d7-175">Это ошибка времени компиляции для объявления членов интерфейса Включение модификаторов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-175">It is a compile-time error for interface member declarations to include any modifiers.</span></span> <span data-ttu-id="e39d7-176">В частности, члены интерфейсов не могут объявляться с модификаторами `abstract`, `public`, `protected`, `internal`, `private`, `virtual`, `override`, или `static`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-176">In particular, interfaces members cannot be declared with the modifiers `abstract`, `public`, `protected`, `internal`, `private`, `virtual`, `override`, or `static`.</span></span>

<span data-ttu-id="e39d7-177">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-177">The example</span></span>
```csharp
public delegate void StringListEvent(IStringList sender);

public interface IStringList
{
    void Add(string s);
    int Count { get; }
    event StringListEvent Changed;
    string this[int index] { get; set; }
}
```
<span data-ttu-id="e39d7-178">объявляет интерфейс, который содержит один каждого из возможных видов членов: Метод, свойство, событие и индексатор.</span><span class="sxs-lookup"><span data-stu-id="e39d7-178">declares an interface that contains one each of the possible kinds of members: A method, a property, an event, and an indexer.</span></span>

<span data-ttu-id="e39d7-179">*Interface_declaration* создает новую область объявления ([объявления](basic-concepts.md#declarations)) и *interface_member_declaration*s, непосредственно содержащиеся в *interface_declaration* представляют новые члены в этой области объявления.</span><span class="sxs-lookup"><span data-stu-id="e39d7-179">An *interface_declaration* creates a new declaration space ([Declarations](basic-concepts.md#declarations)), and the *interface_member_declaration*s immediately contained by the *interface_declaration* introduce new members into this declaration space.</span></span> <span data-ttu-id="e39d7-180">Следующие правила применяются к *interface_member_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="e39d7-180">The following rules apply to *interface_member_declaration*s:</span></span>

*  <span data-ttu-id="e39d7-181">Имя метода должно отличаться от имен всех свойств и событий, объявленных в том же интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-181">The name of a method must differ from the names of all properties and events declared in the same interface.</span></span> <span data-ttu-id="e39d7-182">Кроме того, подпись ([сигнатуры и перегрузка](basic-concepts.md#signatures-and-overloading)) из метода должны отличаться от сигнатур всех других методов, объявленных в тот же интерфейс, и два метода, объявленного в тот же интерфейс, не могут иметь сигнатуры, отличаются только модификаторами `ref` и `out`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-182">In addition, the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of a method must differ from the signatures of all other methods declared in the same interface, and two methods declared in the same interface may not have signatures that differ solely by `ref` and `out`.</span></span>
*  <span data-ttu-id="e39d7-183">Имя свойства или события должно отличаться от имен всех остальных членов, объявленных в тот же интерфейс.</span><span class="sxs-lookup"><span data-stu-id="e39d7-183">The name of a property or event must differ from the names of all other members declared in the same interface.</span></span>
*  <span data-ttu-id="e39d7-184">Сигнатура индексатора должна отличаться от сигнатур любых других индексаторов, объявленных в том же интерфейсе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-184">The signature of an indexer must differ from the signatures of all other indexers declared in the same interface.</span></span>

<span data-ttu-id="e39d7-185">Наследуемые члены интерфейса не относятся области объявления интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-185">The inherited members of an interface are specifically not part of the declaration space of the interface.</span></span> <span data-ttu-id="e39d7-186">Таким образом интерфейс может объявлять элемент с тем же именем или сигнатурой, наследуемого члена.</span><span class="sxs-lookup"><span data-stu-id="e39d7-186">Thus, an interface is allowed to declare a member with the same name or signature as an inherited member.</span></span> <span data-ttu-id="e39d7-187">В этом случае элемент производного интерфейса называется скрывать член базового интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-187">When this occurs, the derived interface member is said to hide the base interface member.</span></span> <span data-ttu-id="e39d7-188">Скрытие унаследованного члена не считается ошибкой, но он приводит к компилятор выдаст предупреждение.</span><span class="sxs-lookup"><span data-stu-id="e39d7-188">Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning.</span></span> <span data-ttu-id="e39d7-189">Чтобы подавить предупреждение, необходимо включить объявление члена производного интерфейса `new` модификатор, чтобы указать, что производный член должен скрыть базовый член.</span><span class="sxs-lookup"><span data-stu-id="e39d7-189">To suppress the warning, the declaration of the derived interface member must include a `new` modifier to indicate that the derived member is intended to hide the base member.</span></span> <span data-ttu-id="e39d7-190">Эта тема будет рассматриваться далее в [скрытие через наследование](basic-concepts.md#hiding-through-inheritance).</span><span class="sxs-lookup"><span data-stu-id="e39d7-190">This topic is discussed further in [Hiding through inheritance](basic-concepts.md#hiding-through-inheritance).</span></span>

<span data-ttu-id="e39d7-191">Если `new` модификатор включен в объявление, которое не скрывает унаследованный член, то выдается предупреждение об этом.</span><span class="sxs-lookup"><span data-stu-id="e39d7-191">If a `new` modifier is included in a declaration that doesn't hide an inherited member, a warning is issued to that effect.</span></span> <span data-ttu-id="e39d7-192">Это предупреждение можно отключить путем удаления `new` модификатор.</span><span class="sxs-lookup"><span data-stu-id="e39d7-192">This warning is suppressed by removing the `new` modifier.</span></span>

<span data-ttu-id="e39d7-193">Обратите внимание, что члены в классе `object` — нет, строго говоря, членами какого-либо интерфейса ([члены интерфейса](interfaces.md#interface-members)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-193">Note that the members in class `object` are not, strictly speaking, members of any interface ([Interface members](interfaces.md#interface-members)).</span></span> <span data-ttu-id="e39d7-194">Тем не менее элементы в классе `object` доступны через поиск члена в любой другой тип интерфейса ([поиск члена](expressions.md#member-lookup)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-194">However, the members in class `object` are available via member lookup in any interface type ([Member lookup](expressions.md#member-lookup)).</span></span>

### <a name="interface-methods"></a><span data-ttu-id="e39d7-195">Методы интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-195">Interface methods</span></span>

<span data-ttu-id="e39d7-196">Методы интерфейса объявляются с помощью *interface_method_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="e39d7-196">Interface methods are declared using *interface_method_declaration*s:</span></span>

```antlr
interface_method_declaration
    : attributes? 'new'? return_type identifier type_parameter_list
      '(' formal_parameter_list? ')' type_parameter_constraints_clause* ';'
    ;
```

<span data-ttu-id="e39d7-197">*Атрибуты*, *return_type*, *идентификатор*, и *formal_parameter_list* объявления метода интерфейса с одинаковыми Это означает, что и объявление метода в классе ([методы](classes.md#methods)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-197">The *attributes*, *return_type*, *identifier*, and *formal_parameter_list* of an interface method declaration have the same meaning as those of a method declaration in a class ([Methods](classes.md#methods)).</span></span> <span data-ttu-id="e39d7-198">В объявлении метода интерфейса не разрешается указывать тело метода и объявление таким образом всегда заканчивается точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="e39d7-198">An interface method declaration is not permitted to specify a method body, and the declaration therefore always ends with a semicolon.</span></span>

<span data-ttu-id="e39d7-199">Каждый тип формальный параметр метода интерфейса должен быть безопасным ([безопасность вариативности](interfaces.md#variance-safety)), и тип возвращаемого значения должен быть либо `void` или типизированные выходные данные.</span><span class="sxs-lookup"><span data-stu-id="e39d7-199">Each formal parameter type of an interface method must be input-safe ([Variance safety](interfaces.md#variance-safety)), and the return type must be either `void` or output-safe.</span></span> <span data-ttu-id="e39d7-200">Кроме того каждый ограничение типа класса, ограничение типа интерфейса и ограничения параметра типа в любой тип параметра метода, должен быть безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-200">Furthermore, each class type constraint, interface type constraint and type parameter constraint on any type parameter of the method must be input-safe.</span></span>

<span data-ttu-id="e39d7-201">Эти правила гарантируют, что все ковариантные или контравариантные использования интерфейса остается строго типизированным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-201">These rules ensure that any covariant or contravariant usage of the interface remains type-safe.</span></span> <span data-ttu-id="e39d7-202">Например, примененная к объекту директива</span><span class="sxs-lookup"><span data-stu-id="e39d7-202">For example,</span></span>
```csharp
interface I<out T> { void M<U>() where U : T; }
```
<span data-ttu-id="e39d7-203">не допускается из-за использования `T` как ограничения параметра типа на `U` не является безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-203">is illegal because the usage of `T` as a type parameter constraint on `U` is not input-safe.</span></span>

<span data-ttu-id="e39d7-204">Это ограничение не имели место возможно нарушение безопасности типа следующим образом:</span><span class="sxs-lookup"><span data-stu-id="e39d7-204">Were this restriction not in place it would be possible to violate type safety in the following manner:</span></span>
```csharp
class B {}
class D : B{}
class E : B {}
class C : I<D> { public void M<U>() {...} }
...
I<B> b = new C();
b.M<E>();
```
<span data-ttu-id="e39d7-205">Это вызов `C.M<E>`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-205">This is actually a call to `C.M<E>`.</span></span> <span data-ttu-id="e39d7-206">Но, что требует вызова `E` являются производными от `D`, поэтому здесь ради безопасности типов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-206">But that call requires that `E` derive from `D`, so type safety would be violated here.</span></span>

### <a name="interface-properties"></a><span data-ttu-id="e39d7-207">Свойства интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-207">Interface properties</span></span>

<span data-ttu-id="e39d7-208">Свойства интерфейса объявляются с помощью *interface_property_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="e39d7-208">Interface properties are declared using *interface_property_declaration*s:</span></span>

```antlr
interface_property_declaration
    : attributes? 'new'? type identifier '{' interface_accessors '}'
    ;

interface_accessors
    : attributes? 'get' ';'
    | attributes? 'set' ';'
    | attributes? 'get' ';' attributes? 'set' ';'
    | attributes? 'set' ';' attributes? 'get' ';'
    ;
```

<span data-ttu-id="e39d7-209">*Атрибуты*, *тип*, и *идентификатор* объявлении свойства интерфейса имеют тот же смысл, что и объявление свойства в классе ([ Свойства](classes.md#properties)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-209">The *attributes*, *type*, and *identifier* of an interface property declaration have the same meaning as those of a property declaration in a class ([Properties](classes.md#properties)).</span></span>

<span data-ttu-id="e39d7-210">Методы доступа в объявлении свойства интерфейса соответствуют методам объявлении свойств класса ([методы доступа](classes.md#accessors)), за исключением того, что тело метода доступа всегда должен быть точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="e39d7-210">The accessors of an interface property declaration correspond to the accessors of a class property declaration ([Accessors](classes.md#accessors)), except that the accessor body must always be a semicolon.</span></span> <span data-ttu-id="e39d7-211">Таким образом методы доступа просто указывают, является ли свойство чтения и записи, только для чтения или только для записи.</span><span class="sxs-lookup"><span data-stu-id="e39d7-211">Thus, the accessors simply indicate whether the property is read-write, read-only, or write-only.</span></span>

<span data-ttu-id="e39d7-212">Тип свойства интерфейса должен быть безопасным при выводе при наличии метода доступа get и должен быть безопасным, если имеется метод доступа set.</span><span class="sxs-lookup"><span data-stu-id="e39d7-212">The type of an interface property must be output-safe if there is a get accessor, and must be input-safe if there is a set accessor.</span></span>

### <a name="interface-events"></a><span data-ttu-id="e39d7-213">События интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-213">Interface events</span></span>

<span data-ttu-id="e39d7-214">События интерфейса объявляются с помощью *interface_event_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="e39d7-214">Interface events are declared using *interface_event_declaration*s:</span></span>

```antlr
interface_event_declaration
    : attributes? 'new'? 'event' type identifier ';'
    ;
```

<span data-ttu-id="e39d7-215">*Атрибуты*, *тип*, и *идентификатор* объявлении события интерфейса имеют тот же смысл, что и объявление события в классе ([события ](classes.md#events)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-215">The *attributes*, *type*, and *identifier* of an interface event declaration have the same meaning as those of an event declaration in a class ([Events](classes.md#events)).</span></span>

<span data-ttu-id="e39d7-216">Тип события интерфейса должен быть безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-216">The type of an interface event must be input-safe.</span></span>

### <a name="interface-indexers"></a><span data-ttu-id="e39d7-217">Индексаторы в интерфейсах</span><span class="sxs-lookup"><span data-stu-id="e39d7-217">Interface indexers</span></span>

<span data-ttu-id="e39d7-218">Индексаторы интерфейса объявляются с помощью *interface_indexer_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="e39d7-218">Interface indexers are declared using *interface_indexer_declaration*s:</span></span>

```antlr
interface_indexer_declaration
    : attributes? 'new'? type 'this' '[' formal_parameter_list ']' '{' interface_accessors '}'
    ;
```

<span data-ttu-id="e39d7-219">*Атрибуты*, *тип*, и *formal_parameter_list* объявлении индексатора интерфейса имеют одинаковое значение как объявление индексатора в классе ([ Индексаторы](classes.md#indexers)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-219">The *attributes*, *type*, and *formal_parameter_list* of an interface indexer declaration have the same meaning as those of an indexer declaration in a class ([Indexers](classes.md#indexers)).</span></span>

<span data-ttu-id="e39d7-220">Методы доступа в объявлении индексатора интерфейса соответствуют методам объявление индексатора класса ([индексаторы](classes.md#indexers)), за исключением того, что тело метода доступа всегда должен быть точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="e39d7-220">The accessors of an interface indexer declaration correspond to the accessors of a class indexer declaration ([Indexers](classes.md#indexers)), except that the accessor body must always be a semicolon.</span></span> <span data-ttu-id="e39d7-221">Таким образом методы доступа просто указать, является ли индексатор для чтения, только для чтения или только для записи.</span><span class="sxs-lookup"><span data-stu-id="e39d7-221">Thus, the accessors simply indicate whether the indexer is read-write, read-only, or write-only.</span></span>

<span data-ttu-id="e39d7-222">Все типы формальных параметров индексатора интерфейса должен быть безопасным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-222">All the formal parameter types of an interface indexer must be input-safe .</span></span> <span data-ttu-id="e39d7-223">Кроме того любой `out` или `ref` типы формальных параметров также должен быть безопасным при выводе.</span><span class="sxs-lookup"><span data-stu-id="e39d7-223">In addition, any `out` or `ref` formal parameter types must also be output-safe.</span></span> <span data-ttu-id="e39d7-224">Обратите внимание что даже `out` параметры, требуется ли входные данные с точки зрения, из-за ограничений базовой платформы выполнения.</span><span class="sxs-lookup"><span data-stu-id="e39d7-224">Note that even `out` parameters are required to be input-safe, due to a limitation of the underlying execution platform.</span></span>

<span data-ttu-id="e39d7-225">Тип индексатора интерфейса должен быть безопасным при выводе при наличии метода доступа get и должен быть безопасным, если имеется метод доступа set.</span><span class="sxs-lookup"><span data-stu-id="e39d7-225">The type of an interface indexer must be output-safe if there is a get accessor, and must be input-safe if there is a set accessor.</span></span>

### <a name="interface-member-access"></a><span data-ttu-id="e39d7-226">Доступ к членам интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-226">Interface member access</span></span>

<span data-ttu-id="e39d7-227">Члены интерфейса осуществляется через доступ к членам ([доступ к членам](expressions.md#member-access)) и доступа к индексатору ([доступа к индексатору](expressions.md#indexer-access)) выражения формы `I.M` и `I[A]`, где `I` является типом интерфейса `M` — это метод, свойство или событие этого типа интерфейса, и `A` — список аргументов индексатора.</span><span class="sxs-lookup"><span data-stu-id="e39d7-227">Interface members are accessed through member access ([Member access](expressions.md#member-access)) and indexer access ([Indexer access](expressions.md#indexer-access)) expressions of the form `I.M` and `I[A]`, where `I` is an interface type, `M` is a method, property, or event of that interface type, and `A` is an indexer argument list.</span></span>

<span data-ttu-id="e39d7-228">Для интерфейсов, которые являются строго одиночного наследования (каждый интерфейс в цепочке наследования имеет ноль или ровно один прямой базовый интерфейс), результаты поиска членов ([поиск члена](expressions.md#member-lookup)), вызов метода ([ Вызовы методов](expressions.md#method-invocations)) и доступ к индексатору ([доступа к индексатору](expressions.md#indexer-access)) правила точно не отличаются от классов и структур: Скрыть члены более производные меньше производном членов с тем же именем или сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="e39d7-228">For interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effects of the member lookup ([Member lookup](expressions.md#member-lookup)), method invocation ([Method invocations](expressions.md#method-invocations)), and indexer access ([Indexer access](expressions.md#indexer-access)) rules are exactly the same as for classes and structs: More derived members hide less derived members with the same name or signature.</span></span> <span data-ttu-id="e39d7-229">Тем не менее для интерфейсов множественного наследования, неоднозначности может возникнуть, когда два или более несвязанных базовые интерфейсы объявления членов с тем же именем или сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="e39d7-229">However, for multiple-inheritance interfaces, ambiguities can occur when two or more unrelated base interfaces declare members with the same name or signature.</span></span> <span data-ttu-id="e39d7-230">В этом разделе приведены несколько примеров таких ситуаций.</span><span class="sxs-lookup"><span data-stu-id="e39d7-230">This section shows several examples of such situations.</span></span> <span data-ttu-id="e39d7-231">Во всех случаях явное приведение типов можно использовать для устранения неоднозначностей.</span><span class="sxs-lookup"><span data-stu-id="e39d7-231">In all cases, explicit casts can be used to resolve the ambiguities.</span></span>

<span data-ttu-id="e39d7-232">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-232">In the example</span></span>
```csharp
interface IList
{
    int Count { get; set; }
}

interface ICounter
{
    void Count(int i);
}

interface IListCounter: IList, ICounter {}

class C
{
    void Test(IListCounter x) {
        x.Count(1);                  // Error
        x.Count = 1;                 // Error
        ((IList)x).Count = 1;        // Ok, invokes IList.Count.set
        ((ICounter)x).Count(1);      // Ok, invokes ICounter.Count
    }
}
```
<span data-ttu-id="e39d7-233">Первые две инструкции вызывают ошибки времени компиляции, поскольку поиск члена ([поиск члена](expressions.md#member-lookup)) из `Count` в `IListCounter` является неоднозначным.</span><span class="sxs-lookup"><span data-stu-id="e39d7-233">the first two statements cause compile-time errors because the member lookup ([Member lookup](expressions.md#member-lookup)) of `Count` in `IListCounter` is ambiguous.</span></span> <span data-ttu-id="e39d7-234">Как показано в примере, неоднозначность разрешается путем приведения `x` к типу соответствующего базового интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-234">As illustrated by the example, the ambiguity is resolved by casting `x` to the appropriate base interface type.</span></span> <span data-ttu-id="e39d7-235">Такого приведения имеют без затрат времени выполнения — они просто состоят из Просмотр экземпляра в виде менее производный тип во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="e39d7-235">Such casts have no run-time costs—they merely consist of viewing the instance as a less derived type at compile-time.</span></span>

<span data-ttu-id="e39d7-236">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-236">In the example</span></span>
```csharp
interface IInteger
{
    void Add(int i);
}

interface IDouble
{
    void Add(double d);
}

interface INumber: IInteger, IDouble {}

class C
{
    void Test(INumber n) {
        n.Add(1);                // Invokes IInteger.Add
        n.Add(1.0);              // Only IDouble.Add is applicable
        ((IInteger)n).Add(1);    // Only IInteger.Add is a candidate
        ((IDouble)n).Add(1);     // Only IDouble.Add is a candidate
    }
}
```
<span data-ttu-id="e39d7-237">вызов `n.Add(1)` выбирает `IInteger.Add` путем применения правил разрешения перегрузки [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="e39d7-237">the invocation `n.Add(1)` selects `IInteger.Add` by applying the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="e39d7-238">Аналогичным образом вызов `n.Add(1.0)` выбирает `IDouble.Add`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-238">Similarly the invocation `n.Add(1.0)` selects `IDouble.Add`.</span></span> <span data-ttu-id="e39d7-239">При вставке явные приведения, имеется только один кандидат метод и что позволяет избежать неоднозначности.</span><span class="sxs-lookup"><span data-stu-id="e39d7-239">When explicit casts are inserted, there is only one candidate method, and thus no ambiguity.</span></span>

<span data-ttu-id="e39d7-240">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-240">In the example</span></span>
```csharp
interface IBase
{
    void F(int i);
}

interface ILeft: IBase
{
    new void F(int i);
}

interface IRight: IBase
{
    void G();
}

interface IDerived: ILeft, IRight {}

class A
{
    void Test(IDerived d) {
        d.F(1);                 // Invokes ILeft.F
        ((IBase)d).F(1);        // Invokes IBase.F
        ((ILeft)d).F(1);        // Invokes ILeft.F
        ((IRight)d).F(1);       // Invokes IBase.F
    }
}
```
<span data-ttu-id="e39d7-241">`IBase.F` член спрятан `ILeft.F` член.</span><span class="sxs-lookup"><span data-stu-id="e39d7-241">the `IBase.F` member is hidden by the `ILeft.F` member.</span></span> <span data-ttu-id="e39d7-242">Вызов `d.F(1)` таким образом выбирает `ILeft.F`, даже если `IBase.F` отображается не скрыт в пути доступа, который проведет через `IRight`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-242">The invocation `d.F(1)` thus selects `ILeft.F`, even though `IBase.F` appears to not be hidden in the access path that leads through `IRight`.</span></span>

<span data-ttu-id="e39d7-243">Интуитивное правило скрытие в интерфейсах с множественным наследованием звучит так: Если элемент скрывается в любом пути доступа, он скрыт во всех путях доступа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-243">The intuitive rule for hiding in multiple-inheritance interfaces is simply this: If a member is hidden in any access path, it is hidden in all access paths.</span></span> <span data-ttu-id="e39d7-244">Так как путь доступа из `IDerived` для `ILeft` для `IBase` скрывает `IBase.F`, элемент также скрывается в пути доступа из `IDerived` для `IRight` для `IBase`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-244">Because the access path from `IDerived` to `ILeft` to `IBase` hides `IBase.F`, the member is also hidden in the access path from `IDerived` to `IRight` to `IBase`.</span></span>

## <a name="fully-qualified-interface-member-names"></a><span data-ttu-id="e39d7-245">Имена членов полный интерфейс</span><span class="sxs-lookup"><span data-stu-id="e39d7-245">Fully qualified interface member names</span></span>

<span data-ttu-id="e39d7-246">Член интерфейса иногда указывается по его ***полное имя***.</span><span class="sxs-lookup"><span data-stu-id="e39d7-246">An interface member is sometimes referred to by its ***fully qualified name***.</span></span> <span data-ttu-id="e39d7-247">Полное имя элемента интерфейса состоит из имени интерфейса, в котором член объявлен, и точку, за которым следует имя члена.</span><span class="sxs-lookup"><span data-stu-id="e39d7-247">The fully qualified name of an interface member consists of the name of the interface in which the member is declared, followed by a dot, followed by the name of the member.</span></span> <span data-ttu-id="e39d7-248">Полное имя элемента ссылается на интерфейс, в котором объявлен этот элемент.</span><span class="sxs-lookup"><span data-stu-id="e39d7-248">The fully qualified name of a member references the interface in which the member is declared.</span></span> <span data-ttu-id="e39d7-249">Например в объявлениях</span><span class="sxs-lookup"><span data-stu-id="e39d7-249">For example, given the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}
```
<span data-ttu-id="e39d7-250">полностью квалифицированное имя `Paint` — `IControl.Paint` и полное имя `SetText` является `ITextBox.SetText`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-250">the fully qualified name of `Paint` is `IControl.Paint` and the fully qualified name of `SetText` is `ITextBox.SetText`.</span></span>

<span data-ttu-id="e39d7-251">В приведенном выше примере, это не можно будет ссылаться в `Paint` как `ITextBox.Paint`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-251">In the example above, it is not possible to refer to `Paint` as `ITextBox.Paint`.</span></span>

<span data-ttu-id="e39d7-252">Если интерфейс является частью пространства имен, полное имя члена интерфейса включает в себя имя пространства имен.</span><span class="sxs-lookup"><span data-stu-id="e39d7-252">When an interface is part of a namespace, the fully qualified name of an interface member includes the namespace name.</span></span> <span data-ttu-id="e39d7-253">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-253">For example</span></span>
```csharp
namespace System
{
    public interface ICloneable
    {
        object Clone();
    }
}
```

<span data-ttu-id="e39d7-254">В данном случае — полное имя `Clone` метод `System.ICloneable.Clone`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-254">Here, the fully qualified name of the `Clone` method is `System.ICloneable.Clone`.</span></span>

## <a name="interface-implementations"></a><span data-ttu-id="e39d7-255">Реализации интерфейсов</span><span class="sxs-lookup"><span data-stu-id="e39d7-255">Interface implementations</span></span>

<span data-ttu-id="e39d7-256">Интерфейсы могут быть реализованы классами и структурами.</span><span class="sxs-lookup"><span data-stu-id="e39d7-256">Interfaces may be implemented by classes and structs.</span></span> <span data-ttu-id="e39d7-257">Чтобы указать, что класс или структура непосредственно реализует интерфейс, идентификатор интерфейса включается в списке базовых классов класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="e39d7-257">To indicate that a class or struct directly implements an interface, the interface identifier is included in the base class list of the class or struct.</span></span> <span data-ttu-id="e39d7-258">Пример:</span><span class="sxs-lookup"><span data-stu-id="e39d7-258">For example:</span></span>
```csharp
interface ICloneable
{
    object Clone();
}

interface IComparable
{
    int CompareTo(object other);
}

class ListEntry: ICloneable, IComparable
{
    public object Clone() {...}
    public int CompareTo(object other) {...}
}
```

<span data-ttu-id="e39d7-259">Класс или структура, непосредственно реализует интерфейс также непосредственно реализует все базовые интерфейсы интерфейса неявно.</span><span class="sxs-lookup"><span data-stu-id="e39d7-259">A class or struct that directly implements an interface also directly implements all of the interface's base interfaces implicitly.</span></span> <span data-ttu-id="e39d7-260">Это справедливо, даже если класса или структуры не указаны явным образом все базовые интерфейсы в списке базовых классов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-260">This is true even if the class or struct doesn't explicitly list all base interfaces in the base class list.</span></span> <span data-ttu-id="e39d7-261">Пример:</span><span class="sxs-lookup"><span data-stu-id="e39d7-261">For example:</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

class TextBox: ITextBox
{
    public void Paint() {...}
    public void SetText(string text) {...}
}
```

<span data-ttu-id="e39d7-262">Здесь класс `TextBox` реализует `IControl` и `ITextBox`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-262">Here, class `TextBox` implements both `IControl` and `ITextBox`.</span></span>

<span data-ttu-id="e39d7-263">Если в классе `C` непосредственно реализует интерфейс, все классы, производные от C, также реализуют интерфейс неявно.</span><span class="sxs-lookup"><span data-stu-id="e39d7-263">When a class `C` directly implements an interface, all classes derived from C also implement the interface implicitly.</span></span> <span data-ttu-id="e39d7-264">Базовые интерфейсы, указанные в объявлении класса может быть построенный интерфейс типов ([создан типы](types.md#constructed-types)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-264">The base interfaces specified in a class declaration can be constructed interface types ([Constructed types](types.md#constructed-types)).</span></span> <span data-ttu-id="e39d7-265">Базовый интерфейс не может быть параметром типа сам по себе, хотя он может включать параметры типа, которые находятся в области действия.</span><span class="sxs-lookup"><span data-stu-id="e39d7-265">A base interface cannot be a type parameter on its own, though it can involve the type parameters that are in scope.</span></span> <span data-ttu-id="e39d7-266">В следующем коде показано, как можно реализовать класс и расширить сконструированных типов:</span><span class="sxs-lookup"><span data-stu-id="e39d7-266">The following code illustrates how a class can implement and extend constructed types:</span></span>
```csharp
class C<U,V> {}

interface I1<V> {}

class D: C<string,int>, I1<string> {}

class E<T>: C<int,T>, I1<T> {}
```

<span data-ttu-id="e39d7-267">Базовые интерфейсы, входящем в объявление универсального класса должны удовлетворять уникальность правила, описанные в [уникальность реализованных интерфейсов](interfaces.md#uniqueness-of-implemented-interfaces).</span><span class="sxs-lookup"><span data-stu-id="e39d7-267">The base interfaces of a generic class declaration must satisfy the uniqueness rule described in [Uniqueness of implemented interfaces](interfaces.md#uniqueness-of-implemented-interfaces).</span></span>

### <a name="explicit-interface-member-implementations"></a><span data-ttu-id="e39d7-268">Явные реализации члена интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-268">Explicit interface member implementations</span></span>

<span data-ttu-id="e39d7-269">Для целей реализации интерфейсов, может объявлять в классе или структуре ***явные реализации члена интерфейса***.</span><span class="sxs-lookup"><span data-stu-id="e39d7-269">For purposes of implementing interfaces, a class or struct may declare ***explicit interface member implementations***.</span></span> <span data-ttu-id="e39d7-270">Явная реализация члена интерфейса является объявление метода, свойства, события или индексатора, которое ссылается на имя члена, полное имя интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-270">An explicit interface member implementation is a method, property, event, or indexer declaration that references a fully qualified interface member name.</span></span> <span data-ttu-id="e39d7-271">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-271">For example</span></span>
```csharp
interface IList<T>
{
    T[] GetElements();
}

interface IDictionary<K,V>
{
    V this[K key];
    void Add(K key, V value);
}

class List<T>: IList<T>, IDictionary<int,T>
{
    T[] IList<T>.GetElements() {...}
    T IDictionary<int,T>.this[int index] {...}
    void IDictionary<int,T>.Add(int index, T value) {...}
}
```

<span data-ttu-id="e39d7-272">Здесь `IDictionary<int,T>.this` и `IDictionary<int,T>.Add` — интерфейс явной реализации членов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-272">Here `IDictionary<int,T>.this` and `IDictionary<int,T>.Add` are explicit interface member implementations.</span></span>

<span data-ttu-id="e39d7-273">В некоторых случаях имя члена интерфейса может оказаться не подходит для реализующего класса, в котором регистр члена интерфейса могут быть реализованы с помощью явная реализация члена интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-273">In some cases, the name of an interface member may not be appropriate for the implementing class, in which case the interface member may be implemented using explicit interface member implementation.</span></span> <span data-ttu-id="e39d7-274">Класс реализует абстракцию файла, например, скорее всего будет реализовывать `Close` функция-член, действует по освобождению ресурсов файл и реализовать `Dispose` метод `IDisposable` интерфейс, с помощью явного интерфейса реализация члена:</span><span class="sxs-lookup"><span data-stu-id="e39d7-274">A class implementing a file abstraction, for example, would likely implement a `Close` member function that has the effect of releasing the file resource, and implement the `Dispose` method of the `IDisposable` interface using explicit interface member implementation:</span></span>
```csharp
interface IDisposable
{
    void Dispose();
}

class MyFile: IDisposable
{
    void IDisposable.Dispose() {
        Close();
    }

    public void Close() {
        // Do what's necessary to close the file
        System.GC.SuppressFinalize(this);
    }
}
```

<span data-ttu-id="e39d7-275">Доступ к явной реализации члена интерфейса через его полное имя в вызов метода, доступ к свойству или индексатору невозможна.</span><span class="sxs-lookup"><span data-stu-id="e39d7-275">It is not possible to access an explicit interface member implementation through its fully qualified name in a method invocation, property access, or indexer access.</span></span> <span data-ttu-id="e39d7-276">Явная реализация члена интерфейса может осуществляться только через экземпляр интерфейса и используется в этом случае просто по имени элемента.</span><span class="sxs-lookup"><span data-stu-id="e39d7-276">An explicit interface member implementation can only be accessed through an interface instance, and is in that case referenced simply by its member name.</span></span>

<span data-ttu-id="e39d7-277">Произошла ошибка во время компиляции, для явной реализации члена интерфейса включать модификаторы доступа и произошла ошибка во время компиляции, чтобы включать модификаторы `abstract`, `virtual`, `override`, или `static`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-277">It is a compile-time error for an explicit interface member implementation to include access modifiers, and it is a compile-time error to include the modifiers `abstract`, `virtual`, `override`, or `static`.</span></span>

<span data-ttu-id="e39d7-278">Явные реализации члена интерфейса имеют разные уровни доступа характеристики других членов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-278">Explicit interface member implementations have different accessibility characteristics than other members.</span></span> <span data-ttu-id="e39d7-279">Поскольку явные реализации члена интерфейса, никогда не доступны через их полное имя в вызове метода или доступ к свойству, они в некотором смысле закрытый.</span><span class="sxs-lookup"><span data-stu-id="e39d7-279">Because explicit interface member implementations are never accessible through their fully qualified name in a method invocation or a property access, they are in a sense private.</span></span> <span data-ttu-id="e39d7-280">Тем не менее так как они может осуществляться через экземпляр интерфейса, они в некотором смысле также общедоступный.</span><span class="sxs-lookup"><span data-stu-id="e39d7-280">However, since they can be accessed through an interface instance, they are in a sense also public.</span></span>

<span data-ttu-id="e39d7-281">Явные реализации члена интерфейса служат двум основным целям.</span><span class="sxs-lookup"><span data-stu-id="e39d7-281">Explicit interface member implementations serve two primary purposes:</span></span>

*  <span data-ttu-id="e39d7-282">Поскольку явные реализации члена интерфейса недоступны через экземпляры класса или структуры, они позволяют реализации интерфейса должны быть исключены из открытого интерфейса класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="e39d7-282">Because explicit interface member implementations are not accessible through class or struct instances, they allow interface implementations to be excluded from the public interface of a class or struct.</span></span> <span data-ttu-id="e39d7-283">Это особенно полезно в том случае, если класс или структура реализует внутренний интерфейс, который не представляет интереса к потребителю этого класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="e39d7-283">This is particularly useful when a class or struct implements an internal interface that is of no interest to a consumer of that class or struct.</span></span>
*  <span data-ttu-id="e39d7-284">Явные реализации члена интерфейса позволяют неоднозначности членов интерфейса с одинаковыми сигнатурами.</span><span class="sxs-lookup"><span data-stu-id="e39d7-284">Explicit interface member implementations allow disambiguation of interface members with the same signature.</span></span> <span data-ttu-id="e39d7-285">Без явные реализации члена интерфейса невозможно для класса или структуры для различных реализаций интерфейсы-члены с одинаковой сигнатурой и типом возвращаемого значения, как было бы невозможно для класса или структуры любые реализации все члены интерфейса с одинаковыми сигнатурами, но разными типами возвращаемых значений.</span><span class="sxs-lookup"><span data-stu-id="e39d7-285">Without explicit interface member implementations it would be impossible for a class or struct to have different implementations of interface members with the same signature and return type, as would it be impossible for a class or struct to have any implementation at all of interface members with the same signature but with different return types.</span></span>

<span data-ttu-id="e39d7-286">Явная реализация члена интерфейса была допустимой класса или структуры необходимо имя интерфейса в списке базовых классов, содержащего элемент, полное доменное имя, тип и типы параметров совпадать члена явный интерфейс Реализация.</span><span class="sxs-lookup"><span data-stu-id="e39d7-286">For an explicit interface member implementation to be valid, the class or struct must name an interface in its base class list that contains a member whose fully qualified name, type, and parameter types exactly match those of the explicit interface member implementation.</span></span> <span data-ttu-id="e39d7-287">Таким образом в следующем классе</span><span class="sxs-lookup"><span data-stu-id="e39d7-287">Thus, in the following class</span></span>
```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
    int IComparable.CompareTo(object other) {...}    // invalid
}
```
<span data-ttu-id="e39d7-288">объявление `IComparable.CompareTo` приводит к ошибке времени компиляции, так как `IComparable` отсутствует в списке базовых классов `Shape` и не является базовым интерфейсом `ICloneable`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-288">the declaration of `IComparable.CompareTo` results in a compile-time error because `IComparable` is not listed in the base class list of `Shape` and is not a base interface of `ICloneable`.</span></span> <span data-ttu-id="e39d7-289">Аналогичным образом в объявлениях</span><span class="sxs-lookup"><span data-stu-id="e39d7-289">Likewise, in the declarations</span></span>
```csharp
class Shape: ICloneable
{
    object ICloneable.Clone() {...}
}

class Ellipse: Shape
{
    object ICloneable.Clone() {...}    // invalid
}
```
<span data-ttu-id="e39d7-290">объявление `ICloneable.Clone` в `Ellipse` приводит к ошибке времени компиляции, так как `ICloneable` явно не указан в списке базовых классов `Ellipse`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-290">the declaration of `ICloneable.Clone` in `Ellipse` results in a compile-time error because `ICloneable` is not explicitly listed in the base class list of `Ellipse`.</span></span>

<span data-ttu-id="e39d7-291">Полное имя члена интерфейса должен ссылаться на интерфейс, в котором был объявлен член.</span><span class="sxs-lookup"><span data-stu-id="e39d7-291">The fully qualified name of an interface member must reference the interface in which the member was declared.</span></span> <span data-ttu-id="e39d7-292">Таким образом в объявлениях</span><span class="sxs-lookup"><span data-stu-id="e39d7-292">Thus, in the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

class TextBox: ITextBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
}
```
<span data-ttu-id="e39d7-293">Явная реализация члена интерфейса из `Paint` должно быть записано как `IControl.Paint`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-293">the explicit interface member implementation of `Paint` must be written as `IControl.Paint`.</span></span>

### <a name="uniqueness-of-implemented-interfaces"></a><span data-ttu-id="e39d7-294">Уникальность реализованных интерфейсов</span><span class="sxs-lookup"><span data-stu-id="e39d7-294">Uniqueness of implemented interfaces</span></span>

<span data-ttu-id="e39d7-295">Интерфейсы, реализованные в объявлении универсального типа должны оставаться уникальными для всех возможных сконструированных типов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-295">The interfaces implemented by a generic type declaration must remain unique for all possible constructed types.</span></span> <span data-ttu-id="e39d7-296">Без этого правило было бы невозможно определить правильный метод для вызова для определенных сконструированных типов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-296">Without this rule, it would be impossible to determine the correct method to call for certain constructed types.</span></span> <span data-ttu-id="e39d7-297">Предположим, например, объявление универсального класса может иметь следующий вид:</span><span class="sxs-lookup"><span data-stu-id="e39d7-297">For example, suppose a generic class declaration were permitted to be written as follows:</span></span>
```csharp
interface I<T>
{
    void F();
}

class X<U,V>: I<U>, I<V>                    // Error: I<U> and I<V> conflict
{
    void I<U>.F() {...}
    void I<V>.F() {...}
}
```

<span data-ttu-id="e39d7-298">Были это разрешено, было бы невозможно определить, какой код должен выполняться в следующем случае:</span><span class="sxs-lookup"><span data-stu-id="e39d7-298">Were this permitted, it would be impossible to determine which code to execute in the following case:</span></span>
```csharp
I<int> x = new X<int,int>();
x.F();
```

<span data-ttu-id="e39d7-299">Для определения допустимости интерфейс список объявление универсального типа, выполняются следующие действия:</span><span class="sxs-lookup"><span data-stu-id="e39d7-299">To determine if the interface list of a generic type declaration is valid, the following steps are performed:</span></span>

*  <span data-ttu-id="e39d7-300">Позвольте `L` быть список интерфейсов, непосредственно указывается в объявлении интерфейса, структуры или универсальный класс `C`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-300">Let `L` be the list of interfaces directly specified in a generic class, struct, or interface declaration `C`.</span></span>
*  <span data-ttu-id="e39d7-301">Добавить `L` любые базовые интерфейсы, которые уже интерфейсов `L`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-301">Add to `L` any base interfaces of the interfaces already in `L`.</span></span>
*  <span data-ttu-id="e39d7-302">Удалить все повторяющиеся значения из `L`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-302">Remove any duplicates from `L`.</span></span>
*  <span data-ttu-id="e39d7-303">Если какой-либо возможной сконструированный тип, созданный из `C` после замены аргументов типа в `L`, вызвать два интерфейса в `L` идентичными, то объявление `C` является недопустимым.</span><span class="sxs-lookup"><span data-stu-id="e39d7-303">If any possible constructed type created from `C` would, after type arguments are substituted into `L`, cause two interfaces in `L` to be identical, then the declaration of `C` is invalid.</span></span> <span data-ttu-id="e39d7-304">Ограничение объявления не учитываются при определении всех возможных сконструированных типов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-304">Constraint declarations are not considered when determining all possible constructed types.</span></span>

<span data-ttu-id="e39d7-305">В объявлении класса `X` выше списке интерфейсов `L` состоит из `I<U>` и `I<V>`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-305">In the class declaration `X` above, the interface list `L` consists of `I<U>` and `I<V>`.</span></span> <span data-ttu-id="e39d7-306">Объявление является недопустимым, поскольку любой сконструированного типа с `U` и `V` имеют одинаковый тип вызовет эти два интерфейса будут иметь одинаковый тип.</span><span class="sxs-lookup"><span data-stu-id="e39d7-306">The declaration is invalid because any constructed type with `U` and `V` being the same type would cause these two interfaces to be identical types.</span></span>

<span data-ttu-id="e39d7-307">Это возможно, интерфейсы, находящиеся на разных уровнях наследования для объединения:</span><span class="sxs-lookup"><span data-stu-id="e39d7-307">It is possible for interfaces specified at different inheritance levels to unify:</span></span>
```csharp
interface I<T>
{
    void F();
}

class Base<U>: I<U>
{
    void I<U>.F() {...}
}

class Derived<U,V>: Base<U>, I<V>    // Ok
{
    void I<V>.F() {...}
}
```

<span data-ttu-id="e39d7-308">Этот код является допустимым, даже если `Derived<U,V>` реализует `I<U>` и `I<V>`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-308">This code is valid even though `Derived<U,V>` implements both `I<U>` and `I<V>`.</span></span> <span data-ttu-id="e39d7-309">Код</span><span class="sxs-lookup"><span data-stu-id="e39d7-309">The code</span></span>
```csharp
I<int> x = new Derived<int,int>();
x.F();
```
<span data-ttu-id="e39d7-310">вызывает метод в `Derived`, так как `Derived<int,int>` фактически выполняет `I<int>` ([повторной реализации интерфейса](interfaces.md#interface-re-implementation)).</span><span class="sxs-lookup"><span data-stu-id="e39d7-310">invokes the method in `Derived`, since `Derived<int,int>` effectively re-implements `I<int>` ([Interface re-implementation](interfaces.md#interface-re-implementation)).</span></span>

### <a name="implementation-of-generic-methods"></a><span data-ttu-id="e39d7-311">Реализация универсальных методов</span><span class="sxs-lookup"><span data-stu-id="e39d7-311">Implementation of generic methods</span></span>

<span data-ttu-id="e39d7-312">Если универсальный метод неявно реализует метод интерфейса, ограничения, заданные для каждого параметра типа метода должны быть эквивалентными в обоих объявлениях (после любой другой тип интерфейса параметры заменяются с соответствующими аргументами типа), где метод параметры типа определяются порядковые, слева направо.</span><span class="sxs-lookup"><span data-stu-id="e39d7-312">When a generic method implicitly implements an interface method, the constraints given for each method type parameter must be equivalent in both declarations (after any interface type parameters are replaced with the appropriate type arguments), where method type parameters are identified by ordinal positions, left to right.</span></span>

<span data-ttu-id="e39d7-313">Если универсальный метод явным образом реализует метод интерфейса, однако нет ограничения разрешены в метод реализации.</span><span class="sxs-lookup"><span data-stu-id="e39d7-313">When a generic method explicitly implements an interface method, however, no constraints are allowed on the implementing method.</span></span> <span data-ttu-id="e39d7-314">Вместо этого ограничения, унаследованные от метода интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-314">Instead, the constraints are inherited from the interface method</span></span>

```csharp
interface I<A,B,C>
{
    void F<T>(T t) where T: A;
    void G<T>(T t) where T: B;
    void H<T>(T t) where T: C;
}

class C: I<object,C,string>
{
    public void F<T>(T t) {...}                    // Ok
    public void G<T>(T t) where T: C {...}         // Ok
    public void H<T>(T t) where T: string {...}    // Error
}
```

<span data-ttu-id="e39d7-315">Метод `C.F<T>` реализует неявно `I<object,C,string>.F<T>`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-315">The method `C.F<T>` implicitly implements `I<object,C,string>.F<T>`.</span></span> <span data-ttu-id="e39d7-316">В этом случае `C.F<T>` не требуется (и не допускается) указывать ограничение `T:object` поскольку `object` неявное ограничение для всех параметров типа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-316">In this case, `C.F<T>` is not required (nor permitted) to specify the constraint `T:object` since `object` is an implicit constraint on all type parameters.</span></span> <span data-ttu-id="e39d7-317">Метод `C.G<T>` реализует неявно `I<object,C,string>.G<T>` из-за ограничений соответствия строкам в интерфейсе после замены параметров типа интерфейса с соответствующими аргументами типа.</span><span class="sxs-lookup"><span data-stu-id="e39d7-317">The method `C.G<T>` implicitly implements `I<object,C,string>.G<T>` because the constraints match those in the interface, after the interface type parameters are replaced with the corresponding type arguments.</span></span> <span data-ttu-id="e39d7-318">Ограничение для метода `C.H<T>` является ошибкой, так как запечатанные типы (`string` в данном случае) нельзя использовать в качестве ограничения.</span><span class="sxs-lookup"><span data-stu-id="e39d7-318">The constraint for method `C.H<T>` is an error because sealed types (`string` in this case) cannot be used as constraints.</span></span> <span data-ttu-id="e39d7-319">Отсутствие ограничения также приведет к ошибке, так как ограничения неявных реализациях метода интерфейса должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="e39d7-319">Omitting the constraint would also be an error since constraints of implicit interface method implementations are required to match.</span></span> <span data-ttu-id="e39d7-320">Таким образом, вы не сможете неявно реализовать `I<object,C,string>.H<T>`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-320">Thus, it is impossible to implicitly implement `I<object,C,string>.H<T>`.</span></span> <span data-ttu-id="e39d7-321">Этот метод интерфейса можно реализовать только с помощью явной реализации члена интерфейса:</span><span class="sxs-lookup"><span data-stu-id="e39d7-321">This interface method can only be implemented using an explicit interface member implementation:</span></span>
```csharp
class C: I<object,C,string>
{
    ...

    public void H<U>(U u) where U: class {...}

    void I<object,C,string>.H<T>(T t) {
        string s = t;    // Ok
        H<T>(t);
    }
}
```

<span data-ttu-id="e39d7-322">В этом примере явная реализация члена интерфейса вызывает открытый метод с применением более мягких ограничений.</span><span class="sxs-lookup"><span data-stu-id="e39d7-322">In this example, the explicit interface member implementation invokes a public method having strictly weaker constraints.</span></span> <span data-ttu-id="e39d7-323">Обратите внимание, что назначение из `t` для `s` действителен с момента `T` наследует ограничение `T:string`, несмотря на то, что это ограничение не указано в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="e39d7-323">Note that the assignment from `t` to `s` is valid since `T` inherits a constraint of `T:string`, even though this constraint is not expressible in source code.</span></span>

### <a name="interface-mapping"></a><span data-ttu-id="e39d7-324">Сопоставление интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-324">Interface mapping</span></span>

<span data-ttu-id="e39d7-325">Класс или структура должны позволяют реализовывать все члены интерфейсов, которые перечислены в списке базовых классов класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="e39d7-325">A class or struct must provide implementations of all members of the interfaces that are listed in the base class list of the class or struct.</span></span> <span data-ttu-id="e39d7-326">Процесс обнаружения реализации члена интерфейса в реализующем классе или структуре называется ***сопоставление интерфейса***.</span><span class="sxs-lookup"><span data-stu-id="e39d7-326">The process of locating implementations of interface members in an implementing class or struct is known as ***interface mapping***.</span></span>

<span data-ttu-id="e39d7-327">Сопоставление интерфейса для класса или структуры `C` находит реализацию для каждого из интерфейсов, указанных в списке базовых классов элементов `C`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-327">Interface mapping for a class or struct `C` locates an implementation for each member of each interface specified in the base class list of `C`.</span></span> <span data-ttu-id="e39d7-328">Реализация конкретного члена интерфейса `I.M`, где `I` — это интерфейс, в котором член `M` объявляется, определяется путем проверки каждого класса или структуры `S`, начиная с `C` и Повторение для каждого последующего базового класса из `C`, пока не находится соответствия:</span><span class="sxs-lookup"><span data-stu-id="e39d7-328">The implementation of a particular interface member `I.M`, where `I` is the interface in which the member `M` is declared, is determined by examining each class or struct `S`, starting with `C` and repeating for each successive base class of `C`, until a match is located:</span></span>

*  <span data-ttu-id="e39d7-329">Если `S` содержит декларацию явная реализация члена интерфейса, соответствующий `I` и `M`, а затем этот член является реализация `I.M`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-329">If `S` contains a declaration of an explicit interface member implementation that matches `I` and `M`, then this member is the implementation of `I.M`.</span></span>
*  <span data-ttu-id="e39d7-330">В противном случае, если `S` содержит объявление открытого члена статическим, который соответствует `M`, а затем этот член является реализация `I.M`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-330">Otherwise, if `S` contains a declaration of a non-static public member that matches `M`, then this member is the implementation of `I.M`.</span></span> <span data-ttu-id="e39d7-331">Если более чем один член совпадений, он не указан какой член является реализацией `I.M`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-331">If more than one member matches, it is unspecified which member is the implementation of `I.M`.</span></span> <span data-ttu-id="e39d7-332">Такая ситуация возможна только в том случае, если `S` является сконструированным типом, где два члена, как объявлено в универсальном типе, иметь разные сигнатуры, но аргументы типа делают их подписи идентичными.</span><span class="sxs-lookup"><span data-stu-id="e39d7-332">This situation can only occur if `S` is a constructed type where the two members as declared in the generic type have different signatures, but the type arguments make their signatures identical.</span></span>

<span data-ttu-id="e39d7-333">Ошибка времени компиляции возникает, если реализации не удалось найти для всех элементов, указанных в списке базовых классов из всех интерфейсов `C`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-333">A compile-time error occurs if implementations cannot be located for all members of all interfaces specified in the base class list of `C`.</span></span> <span data-ttu-id="e39d7-334">Обратите внимание на то, что члены интерфейса содержат члены, унаследованные от базовых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-334">Note that the members of an interface include those members that are inherited from base interfaces.</span></span>

<span data-ttu-id="e39d7-335">Для целей интерфейс сопоставления, член класса `A` соответствует член интерфейса `B` при:</span><span class="sxs-lookup"><span data-stu-id="e39d7-335">For purposes of interface mapping, a class member `A` matches an interface member `B` when:</span></span>

*  <span data-ttu-id="e39d7-336">`A` и `B` методов, и имя, тип, и список формальных параметров `A` и `B` идентичны.</span><span class="sxs-lookup"><span data-stu-id="e39d7-336">`A` and `B` are methods, and the name, type, and formal parameter lists of `A` and `B` are identical.</span></span>
*  <span data-ttu-id="e39d7-337">`A` и `B` только свойства, имя и тип `A` и `B` идентичны, и `A` имеет те же методы доступа как `B` (`A` может иметь дополнительные методы доступа, если это не явный интерфейс реализация члена).</span><span class="sxs-lookup"><span data-stu-id="e39d7-337">`A` and `B` are properties, the name and type of `A` and `B` are identical, and `A` has the same accessors as `B` (`A` is permitted to have additional accessors if it is not an explicit interface member implementation).</span></span>
*  <span data-ttu-id="e39d7-338">`A` и `B` события и имя и тип `A` и `B` идентичны.</span><span class="sxs-lookup"><span data-stu-id="e39d7-338">`A` and `B` are events, and the name and type of `A` and `B` are identical.</span></span>
*  <span data-ttu-id="e39d7-339">`A` и `B` , индексаторы, тип и список формальных параметров `A` и `B` идентичны, и `A` имеет те же методы доступа как `B` (`A` может иметь дополнительные методы доступа, если это не Явная реализация члена интерфейса).</span><span class="sxs-lookup"><span data-stu-id="e39d7-339">`A` and `B` are indexers, the type and formal parameter lists of `A` and `B` are identical, and `A` has the same accessors as `B` (`A` is permitted to have additional accessors if it is not an explicit interface member implementation).</span></span>

<span data-ttu-id="e39d7-340">Ниже приведены важные последствия алгоритм сопоставления интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-340">Notable implications of the interface mapping algorithm are:</span></span>

*  <span data-ttu-id="e39d7-341">При определении члена класса или структуры, который реализует член интерфейса, явные реализации члена интерфейса имеют приоритет над другие члены в том же классе или структуре.</span><span class="sxs-lookup"><span data-stu-id="e39d7-341">Explicit interface member implementations take precedence over other members in the same class or struct when determining the class or struct member that implements an interface member.</span></span>
*  <span data-ttu-id="e39d7-342">Не являющиеся открытыми, ни статические члены участвовать в сопоставление интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-342">Neither non-public nor static members participate in interface mapping.</span></span>

<span data-ttu-id="e39d7-343">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-343">In the example</span></span>
```csharp
interface ICloneable
{
    object Clone();
}

class C: ICloneable
{
    object ICloneable.Clone() {...}
    public object Clone() {...}
}
```
<span data-ttu-id="e39d7-344">`ICloneable.Clone` членом `C` становится реализация `Clone` в `ICloneable` Поскольку явные реализации члена интерфейса имеют приоритет над другими участниками.</span><span class="sxs-lookup"><span data-stu-id="e39d7-344">the `ICloneable.Clone` member of `C` becomes the implementation of `Clone` in `ICloneable` because explicit interface member implementations take precedence over other members.</span></span>

<span data-ttu-id="e39d7-345">Если класс или структура реализует два или большее число интерфейсов содержит член с тем же именем, типом и типы параметров, можно сопоставить каждый из таких членов интерфейса один член класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="e39d7-345">If a class or struct implements two or more interfaces containing a member with the same name, type, and parameter types, it is possible to map each of those interface members onto a single class or struct member.</span></span> <span data-ttu-id="e39d7-346">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-346">For example</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface IForm
{
    void Paint();
}

class Page: IControl, IForm
{
    public void Paint() {...}
}
```

<span data-ttu-id="e39d7-347">Здесь `Paint` методы как `IControl` и `IForm` сопоставляются со `Paint` метод в `Page`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-347">Here, the `Paint` methods of both `IControl` and `IForm` are mapped onto the `Paint` method in `Page`.</span></span> <span data-ttu-id="e39d7-348">Это безусловно также могут существовать отдельные явные реализации члена интерфейса для двух методов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-348">It is of course also possible to have separate explicit interface member implementations for the two methods.</span></span>

<span data-ttu-id="e39d7-349">Если класс или структура реализует интерфейс, который содержит скрытые элементы, то некоторые члены обязательно должен быть реализован через явные реализации члена интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-349">If a class or struct implements an interface that contains hidden members, then some members must necessarily be implemented through explicit interface member implementations.</span></span> <span data-ttu-id="e39d7-350">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-350">For example</span></span>
```csharp
interface IBase
{
    int P { get; }
}

interface IDerived: IBase
{
    new int P();
}
```

<span data-ttu-id="e39d7-351">Реализация этого интерфейса требуется по крайней мере один явная реализация члена интерфейса и может принимать одно из следующих форм</span><span class="sxs-lookup"><span data-stu-id="e39d7-351">An implementation of this interface would require at least one explicit interface member implementation, and would take one of the following forms</span></span>
```csharp
class C: IDerived
{
    int IBase.P { get {...} }
    int IDerived.P() {...}
}

class C: IDerived
{
    public int P { get {...} }
    int IDerived.P() {...}
}

class C: IDerived
{
    int IBase.P { get {...} }
    public int P() {...}
}
```

<span data-ttu-id="e39d7-352">Если класс реализует несколько интерфейсов, которые имеют общий базовый интерфейс, может существовать только одна реализация базового интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-352">When a class implements multiple interfaces that have the same base interface, there can be only one implementation of the base interface.</span></span> <span data-ttu-id="e39d7-353">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-353">In the example</span></span>
```csharp
interface IControl
{
    void Paint();
}

interface ITextBox: IControl
{
    void SetText(string text);
}

interface IListBox: IControl
{
    void SetItems(string[] items);
}

class ComboBox: IControl, ITextBox, IListBox
{
    void IControl.Paint() {...}
    void ITextBox.SetText(string text) {...}
    void IListBox.SetItems(string[] items) {...}
}
```
<span data-ttu-id="e39d7-354">Невозможно иметь отдельные реализации для `IControl` с именем в списке базовых классов, `IControl` унаследованы `ITextBox`и `IControl` унаследованы `IListBox`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-354">it is not possible to have separate implementations for the `IControl` named in the base class list, the `IControl` inherited by `ITextBox`, and the `IControl` inherited by `IListBox`.</span></span> <span data-ttu-id="e39d7-355">Действительно нет понятия отдельные удостоверения для этих интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-355">Indeed, there is no notion of a separate identity for these interfaces.</span></span> <span data-ttu-id="e39d7-356">Вместо этого реализации `ITextBox` и `IListBox` реализована из `IControl`, и `ComboBox` считается просто реализовать три интерфейса `IControl`, `ITextBox`, и `IListBox`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-356">Rather, the implementations of `ITextBox` and `IListBox` share the same implementation of `IControl`, and `ComboBox` is simply considered to implement three interfaces, `IControl`, `ITextBox`, and `IListBox`.</span></span>

<span data-ttu-id="e39d7-357">Члены базового класса участвовать в сопоставлении интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-357">The members of a base class participate in interface mapping.</span></span> <span data-ttu-id="e39d7-358">В примере</span><span class="sxs-lookup"><span data-stu-id="e39d7-358">In the example</span></span>
```csharp
interface Interface1
{
    void F();
}

class Class1
{
    public void F() {}
    public void G() {}
}

class Class2: Class1, Interface1
{
    new public void G() {}
}
```
<span data-ttu-id="e39d7-359">метод `F` в `Class1` используется в `Class2`в реализации `Interface1`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-359">the method `F` in `Class1` is used in `Class2`'s implementation of `Interface1`.</span></span>

### <a name="interface-implementation-inheritance"></a><span data-ttu-id="e39d7-360">Реализация наследования интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-360">Interface implementation inheritance</span></span>

<span data-ttu-id="e39d7-361">Класс наследует все реализации интерфейса, предоставляемые его базовых классов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-361">A class inherits all interface implementations provided by its base classes.</span></span>

<span data-ttu-id="e39d7-362">Без явно ***каждый раз реализовывать*** интерфейс, производном классе невозможно каким-либо образом изменить интерфейс сопоставления, он наследует из его базовых классов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-362">Without explicitly ***re-implementing*** an interface, a derived class cannot in any way alter the interface mappings it inherits from its base classes.</span></span> <span data-ttu-id="e39d7-363">Например в объявлениях</span><span class="sxs-lookup"><span data-stu-id="e39d7-363">For example, in the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    public void Paint() {...}
}

class TextBox: Control
{
    new public void Paint() {...}
}
```
<span data-ttu-id="e39d7-364">`Paint` метод в `TextBox` скрывает `Paint` метод в `Control`, но его не удалось изменить сопоставление `Control.Paint` на `IControl.Paint`и вызовы `Paint` через класс экземпляры и экземпляры интерфейса будут иметь следующие последствия</span><span class="sxs-lookup"><span data-stu-id="e39d7-364">the `Paint` method in `TextBox` hides the `Paint` method in `Control`, but it does not alter the mapping of `Control.Paint` onto `IControl.Paint`, and calls to `Paint` through class instances and interface instances will have the following effects</span></span>
```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // invokes Control.Paint();
t.Paint();            // invokes TextBox.Paint();
ic.Paint();           // invokes Control.Paint();
it.Paint();           // invokes Control.Paint();
```

<span data-ttu-id="e39d7-365">Тем не менее при сопоставлении метода интерфейса виртуального метода в классе, производных классах переопределить виртуальный метод и изменить реализацию интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-365">However, when an interface method is mapped onto a virtual method in a class, it is possible for derived classes to override the virtual method and alter the implementation of the interface.</span></span> <span data-ttu-id="e39d7-366">Например переопределения приведенных выше объявлений на</span><span class="sxs-lookup"><span data-stu-id="e39d7-366">For example, rewriting the declarations above to</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    public virtual void Paint() {...}
}

class TextBox: Control
{
    public override void Paint() {...}
}
```
<span data-ttu-id="e39d7-367">Теперь будет наблюдаться следующие эффекты</span><span class="sxs-lookup"><span data-stu-id="e39d7-367">the following effects will now be observed</span></span>
```csharp
Control c = new Control();
TextBox t = new TextBox();
IControl ic = c;
IControl it = t;
c.Paint();            // invokes Control.Paint();
t.Paint();            // invokes TextBox.Paint();
ic.Paint();           // invokes Control.Paint();
it.Paint();           // invokes TextBox.Paint();
```

<span data-ttu-id="e39d7-368">Поскольку явные реализации члена интерфейса не могут объявляться как виртуальной, не можно переопределить явная реализация члена интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-368">Since explicit interface member implementations cannot be declared virtual, it is not possible to override an explicit interface member implementation.</span></span> <span data-ttu-id="e39d7-369">Тем не менее он идеально подходит для явной реализации члена интерфейса вызывать другой метод, и что другой метод может быть объявлен виртуальным, что позволяет производным классам переопределять его.</span><span class="sxs-lookup"><span data-stu-id="e39d7-369">However, it is perfectly valid for an explicit interface member implementation to call another method, and that other method can be declared virtual to allow derived classes to override it.</span></span> <span data-ttu-id="e39d7-370">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-370">For example</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    void IControl.Paint() { PaintControl(); }
    protected virtual void PaintControl() {...}
}

class TextBox: Control
{
    protected override void PaintControl() {...}
}
```

<span data-ttu-id="e39d7-371">Здесь, классы, производные от `Control` можно specialize реализация `IControl.Paint` путем переопределения `PaintControl` метод.</span><span class="sxs-lookup"><span data-stu-id="e39d7-371">Here, classes derived from `Control` can specialize the implementation of `IControl.Paint` by overriding the `PaintControl` method.</span></span>

### <a name="interface-re-implementation"></a><span data-ttu-id="e39d7-372">Повторная реализация интерфейса</span><span class="sxs-lookup"><span data-stu-id="e39d7-372">Interface re-implementation</span></span>

<span data-ttu-id="e39d7-373">Класс, наследующий реализацию интерфейса разрешено ***повторно реализовать*** интерфейс, включив его в списке базовых классов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-373">A class that inherits an interface implementation is permitted to ***re-implement*** the interface by including it in the base class list.</span></span>

<span data-ttu-id="e39d7-374">Повторная реализация интерфейса работает точно так же интерфейс сопоставления как начальная реализация интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-374">A re-implementation of an interface follows exactly the same interface mapping rules as an initial implementation of an interface.</span></span> <span data-ttu-id="e39d7-375">Таким образом сопоставление наследуемого интерфейса не влияет на сопоставление интерфейса установить в повторной реализации интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-375">Thus, the inherited interface mapping has no effect whatsoever on the interface mapping established for the re-implementation of the interface.</span></span> <span data-ttu-id="e39d7-376">Например в объявлениях</span><span class="sxs-lookup"><span data-stu-id="e39d7-376">For example, in the declarations</span></span>
```csharp
interface IControl
{
    void Paint();
}

class Control: IControl
{
    void IControl.Paint() {...}
}

class MyControl: Control, IControl
{
    public void Paint() {}
}
```
<span data-ttu-id="e39d7-377">тот факт, `Control` сопоставляет `IControl.Paint` на `Control.IControl.Paint` не влияет на повторная реализация в `MyControl`, которое соответствует `IControl.Paint` на `MyControl.Paint`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-377">the fact that `Control` maps `IControl.Paint` onto `Control.IControl.Paint` doesn't affect the re-implementation in `MyControl`, which maps `IControl.Paint` onto `MyControl.Paint`.</span></span>

<span data-ttu-id="e39d7-378">Унаследованные объявления открытых членов и член наследуемого интерфейса явные объявления участвовать в процессе сопоставления интерфейс повторно реализованных интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="e39d7-378">Inherited public member declarations and inherited explicit interface member declarations participate in the interface mapping process for re-implemented interfaces.</span></span> <span data-ttu-id="e39d7-379">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-379">For example</span></span>
```csharp
interface IMethods
{
    void F();
    void G();
    void H();
    void I();
}

class Base: IMethods
{
    void IMethods.F() {}
    void IMethods.G() {}
    public void H() {}
    public void I() {}
}

class Derived: Base, IMethods
{
    public void F() {}
    void IMethods.H() {}
}
```

<span data-ttu-id="e39d7-380">В данном случае — реализация `IMethods` в `Derived` сопоставляет методы интерфейса `Derived.F`, `Base.IMethods.G`, `Derived.IMethods.H`, и `Base.I`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-380">Here, the implementation of `IMethods` in `Derived` maps the interface methods onto `Derived.F`, `Base.IMethods.G`, `Derived.IMethods.H`, and `Base.I`.</span></span>

<span data-ttu-id="e39d7-381">Когда класс реализует интерфейс, он неявно также реализует все базовые интерфейсы этого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-381">When a class implements an interface, it implicitly also implements all of that interface's base interfaces.</span></span> <span data-ttu-id="e39d7-382">Аналогично, повторная реализация интерфейса является также неявно повторная реализация все базовые интерфейсы интерфейса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-382">Likewise, a re-implementation of an interface is also implicitly a re-implementation of all of the interface's base interfaces.</span></span> <span data-ttu-id="e39d7-383">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-383">For example</span></span>
```csharp
interface IBase
{
    void F();
}

interface IDerived: IBase
{
    void G();
}

class C: IDerived
{
    void IBase.F() {...}
    void IDerived.G() {...}
}

class D: C, IDerived
{
    public void F() {...}
    public void G() {...}
}
```

<span data-ttu-id="e39d7-384">В данном случае — повторная реализация `IDerived` также повторно реализует `IBase`, сопоставляя `IBase.F` на `D.F`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-384">Here, the re-implementation of `IDerived` also re-implements `IBase`, mapping `IBase.F` onto `D.F`.</span></span>

### <a name="abstract-classes-and-interfaces"></a><span data-ttu-id="e39d7-385">Абстрактные классы и интерфейсы</span><span class="sxs-lookup"><span data-stu-id="e39d7-385">Abstract classes and interfaces</span></span>

<span data-ttu-id="e39d7-386">Как неабстрактного класса абстрактный класс должен содержать реализации все члены интерфейсов, которые перечислены в списке базовых классов класса.</span><span class="sxs-lookup"><span data-stu-id="e39d7-386">Like a non-abstract class, an abstract class must provide implementations of all members of the interfaces that are listed in the base class list of the class.</span></span> <span data-ttu-id="e39d7-387">Тем не менее абстрактный класс может сопоставлять методы интерфейса абстрактные методы.</span><span class="sxs-lookup"><span data-stu-id="e39d7-387">However, an abstract class is permitted to map interface methods onto abstract methods.</span></span> <span data-ttu-id="e39d7-388">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-388">For example</span></span>
```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    public abstract void F();
    public abstract void G();
}
```

<span data-ttu-id="e39d7-389">В данном случае — реализация `IMethods` сопоставляет `F` и `G` абстрактным методам, который должен быть переопределен в неабстрактных классах, производных от `C`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-389">Here, the implementation of `IMethods` maps `F` and `G` onto abstract methods, which must be overridden in non-abstract classes that derive from `C`.</span></span>

<span data-ttu-id="e39d7-390">Обратите внимание, что явные реализации члена интерфейса не может быть абстрактным, но явные реализации члена интерфейса конечно разрешается вызывать абстрактные методы.</span><span class="sxs-lookup"><span data-stu-id="e39d7-390">Note that explicit interface member implementations cannot be abstract, but explicit interface member implementations are of course permitted to call abstract methods.</span></span> <span data-ttu-id="e39d7-391">Пример</span><span class="sxs-lookup"><span data-stu-id="e39d7-391">For example</span></span>
```csharp
interface IMethods
{
    void F();
    void G();
}

abstract class C: IMethods
{
    void IMethods.F() { FF(); }
    void IMethods.G() { GG(); }
    protected abstract void FF();
    protected abstract void GG();
}
```

<span data-ttu-id="e39d7-392">В данном случае — неабстрактных классах, производных от `C` потребовался бы для переопределения `FF` и `GG`, обеспечивая фактическую реализацию `IMethods`.</span><span class="sxs-lookup"><span data-stu-id="e39d7-392">Here, non-abstract classes that derive from `C` would be required to override `FF` and `GG`, thus providing the actual implementation of `IMethods`.</span></span>
