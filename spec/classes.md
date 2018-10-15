# <a name="classes"></a><span data-ttu-id="c51c7-101">Классы</span><span class="sxs-lookup"><span data-stu-id="c51c7-101">Classes</span></span>

<span data-ttu-id="c51c7-102">Класс является структурой данных, которая может содержать данные членов (константы и поля), функции-члены (методы, свойства, события, индексаторы, операторы, конструкторы экземпляров, деструкторы и статические конструкторы) и вложенные типы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-102">A class is a data structure that may contain data members (constants and fields), function members (methods, properties, events, indexers, operators, instance constructors, destructors and static constructors), and nested types.</span></span> <span data-ttu-id="c51c7-103">Типы классов поддерживают наследование — механизм, посредством которого производный класс может расширяющие и уточняющие определения базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-103">Class types support inheritance, a mechanism whereby a derived class can extend and specialize a base class.</span></span>

## <a name="class-declarations"></a><span data-ttu-id="c51c7-104">Объявления классов</span><span class="sxs-lookup"><span data-stu-id="c51c7-104">Class declarations</span></span>

<span data-ttu-id="c51c7-105">Объект *class_declaration* — *type_declaration* ([объявления типов](namespaces.md#type-declarations)), объявляет новый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-105">A *class_declaration* is a *type_declaration* ([Type declarations](namespaces.md#type-declarations)) that declares a new class.</span></span>

```antlr
class_declaration
    : attributes? class_modifier* 'partial'? 'class' identifier type_parameter_list?
      class_base? type_parameter_constraints_clause* class_body ';'?
    ;
```

<span data-ttu-id="c51c7-106">Объект *class_declaration* состоит из необязательного набора *атрибуты* ([атрибуты](attributes.md)), а затем необязательный набор *class_modifier*s ([класса модификаторы](classes.md#class-modifiers)), а затем использовать необязательный `partial` модификатор, а затем с помощью ключевого слова `class` и *идентификатор* , которая содержит название класса, за которым следует Необязательный *type_parameter_list* ([параметры типа](classes.md#type-parameters)), а затем использовать необязательный *class_base* спецификации ([базового класса Спецификация](classes.md#class-base-specification)), а затем необязательный набор *type_parameter_constraints_clause*s ([ограничения параметров типа](classes.md#type-parameter-constraints)), за которым следует *class_body*  ([Класса текст](classes.md#class-body)), при необходимости, а затем точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-106">A *class_declaration* consists of an optional set of *attributes* ([Attributes](attributes.md)), followed by an optional set of *class_modifier*s ([Class modifiers](classes.md#class-modifiers)), followed by an optional `partial` modifier, followed by the keyword `class` and an *identifier* that names the class, followed by an optional *type_parameter_list* ([Type parameters](classes.md#type-parameters)), followed by an optional *class_base* specification ([Class base specification](classes.md#class-base-specification)) , followed by an optional set of *type_parameter_constraints_clause*s ([Type parameter constraints](classes.md#type-parameter-constraints)), followed by a *class_body* ([Class body](classes.md#class-body)), optionally followed by a semicolon.</span></span>

<span data-ttu-id="c51c7-107">Объявление класса не может предоставить *type_parameter_constraints_clause*s Если не предоставляется *type_parameter_list*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-107">A class declaration cannot supply *type_parameter_constraints_clause*s unless it also supplies a *type_parameter_list*.</span></span>

<span data-ttu-id="c51c7-108">Объявление класса, который предоставляет *type_parameter_list* — ***объявление универсального класса***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-108">A class declaration that supplies a *type_parameter_list* is a ***generic class declaration***.</span></span> <span data-ttu-id="c51c7-109">Кроме того любой класс, вложенный в объявлении универсального класса или объявлении универсального структуры является объявление универсального класса, так как параметры типа для содержащего типа должен быть введен для создания сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-109">Additionally, any class nested inside a generic class declaration or a generic struct declaration is itself a generic class declaration, since type parameters for the containing type must be supplied to create a constructed type.</span></span>

### <a name="class-modifiers"></a><span data-ttu-id="c51c7-110">Модификаторы класса</span><span class="sxs-lookup"><span data-stu-id="c51c7-110">Class modifiers</span></span>

<span data-ttu-id="c51c7-111">Объект *class_declaration* может включать последовательность модификаторов класса:</span><span class="sxs-lookup"><span data-stu-id="c51c7-111">A *class_declaration* may optionally include a sequence of class modifiers:</span></span>

```antlr
class_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'abstract'
    | 'sealed'
    | 'static'
    | class_modifier_unsafe
    ;
```

<span data-ttu-id="c51c7-112">Это ошибка времени компиляции для один и тот же модификатор встречается несколько раз в объявлении класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-112">It is a compile-time error for the same modifier to appear multiple times in a class declaration.</span></span>

<span data-ttu-id="c51c7-113">`new` Модификатор может применяться для вложенных классов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-113">The `new` modifier is permitted on nested classes.</span></span> <span data-ttu-id="c51c7-114">Он указывает, что класс скрывает унаследованный член с тем же именем, как описано в разделе [Модификатор new](classes.md#the-new-modifier).</span><span class="sxs-lookup"><span data-stu-id="c51c7-114">It specifies that the class hides an inherited member by the same name, as described in [The new modifier](classes.md#the-new-modifier).</span></span> <span data-ttu-id="c51c7-115">Произошла ошибка во время компиляции для `new` появление в объявлении класса, который не является объявление вложенного класса модификатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-115">It is a compile-time error for the `new` modifier to appear on a class declaration that is not a nested class declaration.</span></span>

<span data-ttu-id="c51c7-116">`public`, `protected`, `internal`, И `private` модификаторы определяют доступность класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-116">The `public`, `protected`, `internal`, and `private` modifiers control the accessibility of the class.</span></span> <span data-ttu-id="c51c7-117">В зависимости от контекста, в котором производится объявление класса, некоторые из этих модификаторов запрещены ([объявленную доступность](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-117">Depending on the context in which the class declaration occurs, some of these modifiers may not be permitted ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

<span data-ttu-id="c51c7-118">`abstract`, `sealed` И `static` модификаторы рассматриваются в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="c51c7-118">The `abstract`, `sealed` and `static` modifiers are discussed in the following sections.</span></span>

#### <a name="abstract-classes"></a><span data-ttu-id="c51c7-119">Абстрактные классы</span><span class="sxs-lookup"><span data-stu-id="c51c7-119">Abstract classes</span></span>

<span data-ttu-id="c51c7-120">`abstract` Модификатор используется для указания, что класс является неполным и что она должна использоваться только в качестве базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-120">The `abstract` modifier is used to indicate that a class is incomplete and that it is intended to be used only as a base class.</span></span> <span data-ttu-id="c51c7-121">Абстрактный класс отличается от неабстрактного класса следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c51c7-121">An abstract class differs from a non-abstract class in the following ways:</span></span>

*  <span data-ttu-id="c51c7-122">Абстрактный класс не может быть создан напрямую, и произошла ошибка во время компиляции, чтобы использовать `new` оператор для абстрактного класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-122">An abstract class cannot be instantiated directly, and it is a compile-time error to use the `new` operator on an abstract class.</span></span> <span data-ttu-id="c51c7-123">Хотя можно иметь переменные и значения, типы которых во время компиляции являются абстрактными, такие переменные и значения обязательно будет `null` или содержать ссылки на экземпляры неабстрактных классов, производных от абстрактных типов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-123">While it is possible to have variables and values whose compile-time types are abstract, such variables and values will necessarily either be `null` or contain references to instances of non-abstract classes derived from the abstract types.</span></span>
*  <span data-ttu-id="c51c7-124">Абстрактный класс разрешены (но не требуются) содержать абстрактные члены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-124">An abstract class is permitted (but not required) to contain abstract members.</span></span>
*  <span data-ttu-id="c51c7-125">Абстрактный класс не может быть запечатанным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-125">An abstract class cannot be sealed.</span></span>

<span data-ttu-id="c51c7-126">Если неабстрактный класс является производным от абстрактного класса, неабстрактный класс должен включать фактические реализации всех наследуемых абстрактных членов, тем самым переопределив эти абстрактные члены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-126">When a non-abstract class is derived from an abstract class, the non-abstract class must include actual implementations of all inherited abstract members, thereby overriding those abstract members.</span></span> <span data-ttu-id="c51c7-127">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-127">In the example</span></span>
```csharp
abstract class A
{
    public abstract void F();
}

abstract class B: A
{
    public void G() {}
}

class C: B
{
    public override void F() {
        // actual implementation of F
    }
}
```
<span data-ttu-id="c51c7-128">Абстрактный класс `A` представляет абстрактный метод `F`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-128">the abstract class `A` introduces an abstract method `F`.</span></span> <span data-ttu-id="c51c7-129">Класс `B` представляет дополнительный метод `G`, но так как он не предоставляет реализацию `F`, `B` должен также быть объявлен как абстрактный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-129">Class `B` introduces an additional method `G`, but since it doesn't provide an implementation of `F`, `B` must also be declared abstract.</span></span> <span data-ttu-id="c51c7-130">Класс `C` переопределяет `F` и предоставляет фактическую реализацию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-130">Class `C` overrides `F` and provides an actual implementation.</span></span> <span data-ttu-id="c51c7-131">Так как нет ни одного абстрактного члена в `C`, `C` разрешены (но не требуются) быть абстрактным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-131">Since there are no abstract members in `C`, `C` is permitted (but not required) to be non-abstract.</span></span>

#### <a name="sealed-classes"></a><span data-ttu-id="c51c7-132">Запечатанные классы</span><span class="sxs-lookup"><span data-stu-id="c51c7-132">Sealed classes</span></span>

<span data-ttu-id="c51c7-133">`sealed` Модификатор используется для предотвращения создания производных от класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-133">The `sealed` modifier is used to prevent derivation from a class.</span></span> <span data-ttu-id="c51c7-134">Ошибка времени компиляции возникает, если указаны запечатанный класс как базовый класс другого класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-134">A compile-time error occurs if a sealed class is specified as the base class of another class.</span></span>

<span data-ttu-id="c51c7-135">Запечатанный класс не может также быть абстрактным классом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-135">A sealed class cannot also be an abstract class.</span></span>

<span data-ttu-id="c51c7-136">`sealed` Модификатор используется главным образом для предотвращения случайного наследования, но она также позволяет определенные оптимизации во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-136">The `sealed` modifier is primarily used to prevent unintended derivation, but it also enables certain run-time optimizations.</span></span> <span data-ttu-id="c51c7-137">В частности поскольку известно, что запечатанный класс не имеет производных классов, возможна для преобразования вызовов виртуальных функций-членов экземпляров запечатанного класса в невиртуальные вызовы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-137">In particular, because a sealed class is known to never have any derived classes, it is possible to transform virtual function member invocations on sealed class instances into non-virtual invocations.</span></span>

#### <a name="static-classes"></a><span data-ttu-id="c51c7-138">Статические классы</span><span class="sxs-lookup"><span data-stu-id="c51c7-138">Static classes</span></span>

<span data-ttu-id="c51c7-139">`static` Модификатор используется для пометки класса, объявленного как ***статический класс***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-139">The `static` modifier is used to mark the class being declared as a ***static class***.</span></span> <span data-ttu-id="c51c7-140">Статический класс не может быть создан, нельзя использовать в качестве типа и может содержать только статические члены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-140">A static class cannot be instantiated, cannot be used as a type and can contain only static members.</span></span> <span data-ttu-id="c51c7-141">Только статический класс может содержать объявления методов расширения ([методы расширения](classes.md#extension-methods)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-141">Only a static class can contain declarations of extension methods ([Extension methods](classes.md#extension-methods)).</span></span>

<span data-ttu-id="c51c7-142">Объявление статического класса, со следующими ограничениями:</span><span class="sxs-lookup"><span data-stu-id="c51c7-142">A static class declaration is subject to the following restrictions:</span></span>

*  <span data-ttu-id="c51c7-143">Статический класс не может содержать `sealed` или `abstract` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-143">A static class may not include a `sealed` or `abstract` modifier.</span></span> <span data-ttu-id="c51c7-144">Обратите внимание, что так как нельзя создать экземпляр или производным от статического класса, он ведет себя как если бы он был запечатанный и абстрактный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-144">Note, however, that since a static class cannot be instantiated or derived from, it behaves as if it was both sealed and abstract.</span></span>
*  <span data-ttu-id="c51c7-145">Статический класс не может содержать *class_base* спецификации ([класса базовой спецификации](classes.md#class-base-specification)) и явно указать базовый класс или списка реализованных интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-145">A static class may not include a *class_base* specification ([Class base specification](classes.md#class-base-specification)) and cannot explicitly specify a base class or a list of implemented interfaces.</span></span> <span data-ttu-id="c51c7-146">Статический класс неявно наследуется от типа `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-146">A static class implicitly inherits from type `object`.</span></span>
*  <span data-ttu-id="c51c7-147">Статический класс может содержать только статические члены ([экземпляра и статические члены](classes.md#static-and-instance-members)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-147">A static class can only contain static members ([Static and instance members](classes.md#static-and-instance-members)).</span></span> <span data-ttu-id="c51c7-148">Обратите внимание на то, что константы и вложенные типы классифицируются как статические члены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-148">Note that constants and nested types are classified as static members.</span></span>
*  <span data-ttu-id="c51c7-149">Статический класс не может иметь члены с `protected` или `protected internal` объявленную доступность.</span><span class="sxs-lookup"><span data-stu-id="c51c7-149">A static class cannot have members with `protected` or `protected internal` declared accessibility.</span></span>

<span data-ttu-id="c51c7-150">Это ошибка времени компиляции, чтобы нарушить эти ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-150">It is a compile-time error to violate any of these restrictions.</span></span>

<span data-ttu-id="c51c7-151">Статический класс не имеет конструкторов экземпляров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-151">A static class has no instance constructors.</span></span> <span data-ttu-id="c51c7-152">Невозможно объявить конструктор экземпляров в статическом классе и нет конструктора по умолчанию экземпляр ([конструкторы по умолчанию](classes.md#default-constructors)) предоставляется для статического класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-152">It is not possible to declare an instance constructor in a static class, and no default instance constructor ([Default constructors](classes.md#default-constructors)) is provided for a static class.</span></span>

<span data-ttu-id="c51c7-153">Члены статического класса автоматически не являются статическими, а объявления членов необходимо явно включить `static` модификатор (за исключением константы и вложенные типы).</span><span class="sxs-lookup"><span data-stu-id="c51c7-153">The members of a static class are not automatically static, and the member declarations must explicitly include a `static` modifier (except for constants and nested types).</span></span> <span data-ttu-id="c51c7-154">Если класс является вложенным внутри статического внешнего класса, вложенный класс не статический класс пока явно не включен `static` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-154">When a class is nested within a static outer class, the nested class is not a static class unless it explicitly includes a `static` modifier.</span></span>

<span data-ttu-id="c51c7-155">__Ссылки на типы статического класса__</span><span class="sxs-lookup"><span data-stu-id="c51c7-155">__Referencing static class types__</span></span>

<span data-ttu-id="c51c7-156">Объект *namespace_or_type_name* ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)) может ссылаться на статический класс, если</span><span class="sxs-lookup"><span data-stu-id="c51c7-156">A *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) is permitted to reference a static class if</span></span>

*  <span data-ttu-id="c51c7-157">*Namespace_or_type_name* — `T` в *namespace_or_type_name* формы `T.I`, или</span><span class="sxs-lookup"><span data-stu-id="c51c7-157">The *namespace_or_type_name* is the `T` in a *namespace_or_type_name* of the form `T.I`, or</span></span>
*  <span data-ttu-id="c51c7-158">*Namespace_or_type_name* — `T` в *typeof_expression* ([списки аргументов](expressions.md#argument-lists)1) формы `typeof(T)`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-158">The *namespace_or_type_name* is the `T` in a *typeof_expression* ([Argument lists](expressions.md#argument-lists)1) of the form `typeof(T)`.</span></span>

<span data-ttu-id="c51c7-159">Объект *primary_expression* ([функции-члены](expressions.md#function-members)) может ссылаться на статический класс, если</span><span class="sxs-lookup"><span data-stu-id="c51c7-159">A *primary_expression* ([Function members](expressions.md#function-members)) is permitted to reference a static class if</span></span>

*  <span data-ttu-id="c51c7-160">*Primary_expression* — `E` в *member_access* ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) формы `E.I`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-160">The *primary_expression* is the `E` in a *member_access* ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) of the form `E.I`.</span></span>

<span data-ttu-id="c51c7-161">В любом другом контексте является ошибкой во время компиляции для ссылки на статический класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-161">In any other context it is a compile-time error to reference a static class.</span></span> <span data-ttu-id="c51c7-162">Например, это ошибка для статического класса для использования в качестве базового класса, составного типа ([вложенные типы](classes.md#nested-types)) члена, аргумента универсального типа или ограничения параметра типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-162">For example, it is an error for a static class to be used as a base class, a constituent type ([Nested types](classes.md#nested-types)) of a member, a generic type argument, or a type parameter constraint.</span></span> <span data-ttu-id="c51c7-163">Аналогичным образом, статический класс не может использоваться в тип массива, тип указателя, `new` выражения, выражения приведения, `is` выражения, `as` выражения, `sizeof` выражение или выражение значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-163">Likewise, a static class cannot be used in an array type, a pointer type, a `new` expression, a cast expression, an `is` expression, an `as` expression, a `sizeof` expression, or a default value expression.</span></span>

### <a name="partial-modifier"></a><span data-ttu-id="c51c7-164">Модификатор partial</span><span class="sxs-lookup"><span data-stu-id="c51c7-164">Partial modifier</span></span>

<span data-ttu-id="c51c7-165">`partial` Модификатор позволяет указать, что этот *class_declaration* является объявлением разделяемого типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-165">The `partial` modifier is used to indicate that this *class_declaration* is a partial type declaration.</span></span> <span data-ttu-id="c51c7-166">Несколько объявлений разделяемого типа с тем же именем в едином объявлении пространства имен или тип объединения для объявления одного типа формы, следуя правилам указан в [разделяемых типов](classes.md#partial-types).</span><span class="sxs-lookup"><span data-stu-id="c51c7-166">Multiple partial type declarations with the same name within an enclosing namespace or type declaration combine to form one type declaration, following the rules specified in [Partial types](classes.md#partial-types).</span></span>

<span data-ttu-id="c51c7-167">Наличие объявление класса, распределенные по отдельные сегменты текста программы, может быть полезным, если эти сегменты производятся или изменяются в разных контекстах.</span><span class="sxs-lookup"><span data-stu-id="c51c7-167">Having the declaration of a class distributed over separate segments of program text can be useful if these segments are produced or maintained in different contexts.</span></span> <span data-ttu-id="c51c7-168">Например одной части объявления класса может быть компьютером, в то время как другой создается вручную.</span><span class="sxs-lookup"><span data-stu-id="c51c7-168">For instance, one part of a class declaration may be machine generated, whereas the other is manually authored.</span></span> <span data-ttu-id="c51c7-169">Текстовое разделение двух запрещает обновление конфликт с обновлениями по другому.</span><span class="sxs-lookup"><span data-stu-id="c51c7-169">Textual separation of the two prevents updates by one from conflicting with updates by the other.</span></span>

### <a name="type-parameters"></a><span data-ttu-id="c51c7-170">Параметры типа</span><span class="sxs-lookup"><span data-stu-id="c51c7-170">Type parameters</span></span>

<span data-ttu-id="c51c7-171">Параметр типа является простой идентификатор, обозначающий заполнитель для аргумент типа, предоставленный для создания сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-171">A type parameter is a simple identifier that denotes a placeholder for a type argument supplied to create a constructed type.</span></span> <span data-ttu-id="c51c7-172">Параметр типа является формальный заполнитель для типа, который будет выдавать более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="c51c7-172">A type parameter is a formal placeholder for a type that will be supplied later.</span></span> <span data-ttu-id="c51c7-173">В отличие от этого, аргумент типа ([аргументы типа](types.md#type-arguments)) — фактический тип, который подставляется для параметра типа, когда создается сконструированный тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-173">By contrast, a type argument ([Type arguments](types.md#type-arguments)) is the actual type that is substituted for the type parameter when a constructed type is created.</span></span>

```antlr
type_parameter_list
    : '<' type_parameters '>'
    ;

type_parameters
    : attributes? type_parameter
    | type_parameters ',' attributes? type_parameter
    ;

type_parameter
    : identifier
    ;
```

<span data-ttu-id="c51c7-174">Каждый параметр типа в объявлении класса определяет имя в области объявления ([объявления](basic-concepts.md#declarations)) этого класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-174">Each type parameter in a class declaration defines a name in the declaration space ([Declarations](basic-concepts.md#declarations)) of that class.</span></span> <span data-ttu-id="c51c7-175">Таким образом он не может иметь имя, совпадающее с именем другого параметра типа, или член объявлен в этом классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-175">Thus, it cannot have the same name as another type parameter or a member declared in that class.</span></span> <span data-ttu-id="c51c7-176">Параметр типа не может иметь имя, совпадающее с именем самого типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-176">A type parameter cannot have the same name as the type itself.</span></span>

### <a name="class-base-specification"></a><span data-ttu-id="c51c7-177">Спецификация базового класса</span><span class="sxs-lookup"><span data-stu-id="c51c7-177">Class base specification</span></span>

<span data-ttu-id="c51c7-178">Объявление класса может содержать *class_base* спецификации, которая определяет прямой базовый класс классов и интерфейсов ([интерфейсы](interfaces.md)) непосредственно, реализуемый классом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-178">A class declaration may include a *class_base* specification, which defines the direct base class of the class and the interfaces ([Interfaces](interfaces.md)) directly implemented by the class.</span></span>

```antlr
class_base
    : ':' class_type
    | ':' interface_type_list
    | ':' class_type ',' interface_type_list
    ;

interface_type_list
    : interface_type (',' interface_type)*
    ;
```

<span data-ttu-id="c51c7-179">Базовый класс, указанный в объявлении класса не может быть типом сконструированного класса ([создан типы](types.md#constructed-types)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-179">The base class specified in a class declaration can be a constructed class type ([Constructed types](types.md#constructed-types)).</span></span> <span data-ttu-id="c51c7-180">Базовый класс не может быть параметром типа сам по себе, хотя он может включать параметры типа, которые находятся в области действия.</span><span class="sxs-lookup"><span data-stu-id="c51c7-180">A base class cannot be a type parameter on its own, though it can involve the type parameters that are in scope.</span></span>

```csharp
class Extend<V>: V {}            // Error, type parameter used as base class
```

#### <a name="base-classes"></a><span data-ttu-id="c51c7-181">базовых классов;</span><span class="sxs-lookup"><span data-stu-id="c51c7-181">Base classes</span></span>

<span data-ttu-id="c51c7-182">Когда *class_type* включается в *class_base*, он указывает прямой базовый класс для класса, объявленного в.</span><span class="sxs-lookup"><span data-stu-id="c51c7-182">When a *class_type* is included in the *class_base*, it specifies the direct base class of the class being declared.</span></span> <span data-ttu-id="c51c7-183">Если в объявлении класса нет *class_base*, или если *class_base* списки только типы интерфейса, прямой базовый класс считается `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-183">If a class declaration has no *class_base*, or if the *class_base* lists only interface types, the direct base class is assumed to be `object`.</span></span> <span data-ttu-id="c51c7-184">Класс наследует члены от прямого базового класса, как описано в разделе [наследования](classes.md#inheritance).</span><span class="sxs-lookup"><span data-stu-id="c51c7-184">A class inherits members from its direct base class, as described in [Inheritance](classes.md#inheritance).</span></span>

<span data-ttu-id="c51c7-185">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-185">In the example</span></span>
```csharp
class A {}

class B: A {}
```
<span data-ttu-id="c51c7-186">Класс `A` считается прямой базовый класс для `B`, и `B` говорят, что быть производным от `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-186">class `A` is said to be the direct base class of `B`, and `B` is said to be derived from `A`.</span></span> <span data-ttu-id="c51c7-187">Так как `A` does явно не указать прямой базовый класс, его непосредственный базовый класс является неявно `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-187">Since `A` does not explicitly specify a direct base class, its direct base class is implicitly `object`.</span></span>

<span data-ttu-id="c51c7-188">Для типа сконструированного класса, если базовый класс указывается в объявлении универсального класса, базовый класс сконструированного типа будет получен путем замены для каждого *параметр_типа* в объявлении базовый класс, соответствующий *type_argument* сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-188">For a constructed class type, if a base class is specified in the generic class declaration, the base class of the constructed type is obtained by substituting, for each *type_parameter* in the base class declaration, the corresponding *type_argument* of the constructed type.</span></span> <span data-ttu-id="c51c7-189">В объявлениях универсального класса</span><span class="sxs-lookup"><span data-stu-id="c51c7-189">Given the generic class declarations</span></span>
```csharp
class B<U,V> {...}

class G<T>: B<string,T[]> {...}
```
<span data-ttu-id="c51c7-190">базовый класс сконструированного типа `G<int>` бы `B<string,int[]>`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-190">the base class of the constructed type `G<int>` would be `B<string,int[]>`.</span></span>

<span data-ttu-id="c51c7-191">Прямой базовый класс типа класса должен быть по крайней мере такой же уровень доступности, как и сам тип класса ([области доступности](basic-concepts.md#accessibility-domains)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-191">The direct base class of a class type must be at least as accessible as the class type itself ([Accessibility domains](basic-concepts.md#accessibility-domains)).</span></span> <span data-ttu-id="c51c7-192">Например, это ошибка времени компиляции для `public` класса для наследования от `private` или `internal` класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-192">For example, it is a compile-time error for a `public` class to derive from a `private` or `internal` class.</span></span>

<span data-ttu-id="c51c7-193">Прямой базовый класс типа класса не должно быть следующих типов: `System.Array`, `System.Delegate`, `System.MulticastDelegate`, `System.Enum`, или `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-193">The direct base class of a class type must not be any of the following types: `System.Array`, `System.Delegate`, `System.MulticastDelegate`, `System.Enum`, or `System.ValueType`.</span></span> <span data-ttu-id="c51c7-194">Кроме того, нельзя использовать объявление универсального класса `System.Attribute` как прямой или косвенный базовый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-194">Furthermore, a generic class declaration cannot use `System.Attribute` as a direct or indirect base class.</span></span>

<span data-ttu-id="c51c7-195">При определении значения в спецификации прямой базовый класс `A` класса `B`, прямой базовый класс для `B` временно предполагается, что `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-195">While determining the meaning of the direct base class specification `A` of a class `B`, the direct base class of `B` is temporarily assumed to be `object`.</span></span> <span data-ttu-id="c51c7-196">Это означает, что значение спецификации базового класса не может рекурсивно зависеть от самого себя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-196">Intuitively this ensures that the meaning of a base class specification cannot recursively depend on itself.</span></span> <span data-ttu-id="c51c7-197">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-197">The example:</span></span>
```csharp
class A<T> {
   public class B {}
}

class C : A<C.B> {}
```
<span data-ttu-id="c51c7-198">является ошибочным, поскольку в спецификации базового класса `A<C.B>` прямой базовый класс для `C` считается `object`и, следовательно (согласно правилам [пространства имен и тип](basic-concepts.md#namespace-and-type-names)) `C` не считается член `B`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-198">is in error since in the base class specification `A<C.B>` the direct base class of `C` is considered to be `object`, and hence (by the rules of [Namespace and type names](basic-concepts.md#namespace-and-type-names))  `C` is not considered to have a member `B`.</span></span>

<span data-ttu-id="c51c7-199">Эти базовые классы типа класса являются прямой базовый класс и его базовых классов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-199">The base classes of a class type are the direct base class and its base classes.</span></span> <span data-ttu-id="c51c7-200">Другими словами набор базовых классов является транзитивное замыкание связи прямой базовый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-200">In other words, the set of base classes is the transitive closure of the direct base class relationship.</span></span> <span data-ttu-id="c51c7-201">Ссылаясь на пример выше, базовые классы для `B` являются `A` и `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-201">Referring to the example above, the base classes of `B` are `A` and `object`.</span></span> <span data-ttu-id="c51c7-202">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-202">In the example</span></span>
```csharp
class A {...}

class B<T>: A {...}

class C<T>: B<IComparable<T>> {...}

class D<T>: C<T[]> {...}
```
<span data-ttu-id="c51c7-203">базовые классы для `D<int>` являются `C<int[]>`, `B<IComparable<int[]>>`, `A`, и `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-203">the base classes of `D<int>` are `C<int[]>`, `B<IComparable<int[]>>`, `A`, and `object`.</span></span>

<span data-ttu-id="c51c7-204">За исключением класса `object`, каждый тип класс имеет только один прямой базовый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-204">Except for class `object`, every class type has exactly one direct base class.</span></span> <span data-ttu-id="c51c7-205">`object` Класс не имеет прямого базового класса и является исходным базовым классом для всех других классов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-205">The `object` class has no direct base class and is the ultimate base class of all other classes.</span></span>

<span data-ttu-id="c51c7-206">Если в классе `B` является производным от класса `A`, это ошибка времени компиляции для `A` зависят от `B`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-206">When a class `B` derives from a class `A`, it is a compile-time error for `A` to depend on `B`.</span></span> <span data-ttu-id="c51c7-207">Класс ***напрямую зависит от*** прямого базового класса (если таковые имеются) и ***напрямую зависит от*** класса, в течение которого он немедленно вложен (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="c51c7-207">A class ***directly depends on*** its direct base class (if any) and ***directly depends on*** the class within which it is immediately nested (if any).</span></span> <span data-ttu-id="c51c7-208">Рассмотрим следующее определение, полный набор классов, от которых зависит класс является рефлексивным и транзитивным замыканием ***напрямую зависит от*** связи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-208">Given this definition, the complete set of classes upon which a class depends is the reflexive and transitive closure of the ***directly depends on*** relationship.</span></span>

<span data-ttu-id="c51c7-209">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-209">The example</span></span>
```csharp
class A: A {}
```
<span data-ttu-id="c51c7-210">является ошибочным, поскольку класс зависит сам от себя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-210">is erroneous because the class depends on itself.</span></span> <span data-ttu-id="c51c7-211">Аналогично в примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-211">Likewise, the example</span></span>
```csharp
class A: B {}
class B: C {}
class C: A {}
```
<span data-ttu-id="c51c7-212">не ошибка, так как классы циклически зависят сами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-212">is in error because the classes circularly depend on themselves.</span></span> <span data-ttu-id="c51c7-213">Наконец пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-213">Finally, the example</span></span>
```csharp
class A: B.C {}

class B: A
{
    public class C {}
}
```
<span data-ttu-id="c51c7-214">приводит к ошибке времени компиляции, так как `A` зависит от `B.C` (его непосредственный базовый класс), который зависит от `B` (немедленно включающего его класса), которые циклически зависят от `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-214">results in a compile-time error because `A` depends on `B.C` (its direct base class), which depends on `B` (its immediately enclosing class), which circularly depends on `A`.</span></span>

<span data-ttu-id="c51c7-215">Обратите внимание на то, что класс не зависит от классов, вложенных в него.</span><span class="sxs-lookup"><span data-stu-id="c51c7-215">Note that a class does not depend on the classes that are nested within it.</span></span> <span data-ttu-id="c51c7-216">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-216">In the example</span></span>
```csharp
class A
{
    class B: A {}
}
```
<span data-ttu-id="c51c7-217">`B` зависит от `A` (так как `A` его непосредственный базовый класс и немедленно включающего его класса), но `A` не зависит от `B` (так как `B` не является ни базовым классом, ни включающего класса `A` ).</span><span class="sxs-lookup"><span data-stu-id="c51c7-217">`B` depends on `A` (because `A` is both its direct base class and its immediately enclosing class), but `A` does not depend on `B` (since `B` is neither a base class nor an enclosing class of `A`).</span></span> <span data-ttu-id="c51c7-218">Таким образом пример является допустимым.</span><span class="sxs-lookup"><span data-stu-id="c51c7-218">Thus, the example is valid.</span></span>

<span data-ttu-id="c51c7-219">Невозможно выполнять наследование `sealed` класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-219">It is not possible to derive from a `sealed` class.</span></span> <span data-ttu-id="c51c7-220">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-220">In the example</span></span>
```csharp
sealed class A {}

class B: A {}            // Error, cannot derive from a sealed class
```
<span data-ttu-id="c51c7-221">Класс `B` является ошибочным, так как оно пытается являются производными от `sealed` класс `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-221">class `B` is in error because it attempts to derive from the `sealed` class `A`.</span></span>

#### <a name="interface-implementations"></a><span data-ttu-id="c51c7-222">Реализации интерфейсов</span><span class="sxs-lookup"><span data-stu-id="c51c7-222">Interface implementations</span></span>

<span data-ttu-id="c51c7-223">Объект *class_base* спецификация может включать список типов интерфейсов, в которых случай класса говорят, что прямая реализация заданные типы интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-223">A *class_base* specification may include a list of interface types, in which case the class is said to directly implement the given interface types.</span></span> <span data-ttu-id="c51c7-224">Реализация интерфейсов рассматривается далее в [реализации интерфейсов](interfaces.md#interface-implementations).</span><span class="sxs-lookup"><span data-stu-id="c51c7-224">Interface implementations are discussed further in [Interface implementations](interfaces.md#interface-implementations).</span></span>

### <a name="type-parameter-constraints"></a><span data-ttu-id="c51c7-225">Ограничения параметров типа</span><span class="sxs-lookup"><span data-stu-id="c51c7-225">Type parameter constraints</span></span>

<span data-ttu-id="c51c7-226">Универсальный тип и объявлениях метода при необходимости можно указать ограничения параметра типа, включив *type_parameter_constraints_clause*s.</span><span class="sxs-lookup"><span data-stu-id="c51c7-226">Generic type and method declarations can optionally specify type parameter constraints by including *type_parameter_constraints_clause*s.</span></span>

```antlr
type_parameter_constraints_clause
    : 'where' type_parameter ':' type_parameter_constraints
    ;

type_parameter_constraints
    : primary_constraint
    | secondary_constraints
    | constructor_constraint
    | primary_constraint ',' secondary_constraints
    | primary_constraint ',' constructor_constraint
    | secondary_constraints ',' constructor_constraint
    | primary_constraint ',' secondary_constraints ',' constructor_constraint
    ;

primary_constraint
    : class_type
    | 'class'
    | 'struct'
    ;

secondary_constraints
    : interface_type
    | type_parameter
    | secondary_constraints ',' interface_type
    | secondary_constraints ',' type_parameter
    ;

constructor_constraint
    : 'new' '(' ')'
    ;
```

<span data-ttu-id="c51c7-227">Каждый *type_parameter_constraints_clause* состоит из маркера `where`, за которым следует имя параметра типа, за которым следует двоеточие и список ограничений для данного параметра типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-227">Each *type_parameter_constraints_clause* consists of the token `where`, followed by the name of a type parameter, followed by a colon and the list of constraints for that type parameter.</span></span> <span data-ttu-id="c51c7-228">Допускается не более одного `where` предложение для каждого параметра типа и `where` предложения могут быть перечислены в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-228">There can be at most one `where` clause for each type parameter, and the `where` clauses can be listed in any order.</span></span> <span data-ttu-id="c51c7-229">Как и `get` и `set` токенов в метод доступа к свойству `where` токен не является ключевым словом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-229">Like the `get` and `set` tokens in a property accessor, the `where` token is not a keyword.</span></span>

<span data-ttu-id="c51c7-230">Список ограничений в `where` предложение может включать любые из следующих компонентов, в следующем порядке: ограничение одного первичного, один или несколько вторичных ограничения и ограничение конструктора, `new()`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-230">The list of constraints given in a `where` clause can include any of the following components, in this order: a single primary constraint, one or more secondary constraints, and the constructor constraint, `new()`.</span></span>

<span data-ttu-id="c51c7-231">Ограничение первичного может быть типом класса или ***ссылаются на ограничение типа*** `class` или ***значение ограничения типа*** `struct`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-231">A primary constraint can be a class type or the ***reference type constraint*** `class` or the ***value type constraint*** `struct`.</span></span> <span data-ttu-id="c51c7-232">Вторичное ограничение может быть *параметр_типа* или *interface_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-232">A secondary constraint can be a *type_parameter* or *interface_type*.</span></span>

<span data-ttu-id="c51c7-233">Ограничение ссылочного типа указывает, что аргумент типа, используемый для параметра типа должен быть ссылочным типом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-233">The reference type constraint specifies that a type argument used for the type parameter must be a reference type.</span></span> <span data-ttu-id="c51c7-234">Все типы классов, типы интерфейсов, типы делегатов, типы массивов и параметры типа, известные как ссылочный тип (как определено ниже) удовлетворяет этому ограничению.</span><span class="sxs-lookup"><span data-stu-id="c51c7-234">All class types, interface types, delegate types, array types, and type parameters known to be a reference type (as defined below) satisfy this constraint.</span></span>

<span data-ttu-id="c51c7-235">Ограничение типа значения указывает, что аргумент типа, используемый для параметра типа должен быть типом значения, не допускающие значения NULL.</span><span class="sxs-lookup"><span data-stu-id="c51c7-235">The value type constraint specifies that a type argument used for the type parameter must be a non-nullable value type.</span></span> <span data-ttu-id="c51c7-236">Все типы структуры не поддерживают значение NULL, типы перечисления и параметры типа с ограничением до значимого типа удовлетворяет этому ограничению.</span><span class="sxs-lookup"><span data-stu-id="c51c7-236">All non-nullable struct types, enum types, and type parameters having the value type constraint satisfy this constraint.</span></span> <span data-ttu-id="c51c7-237">Обратите внимание, что, несмотря на то, что классифицировано как тип значения, допускающие значения NULL типа ([обнуляемые типы](types.md#nullable-types)) не удовлетворяет ограничению типа значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-237">Note that although classified as a value type, a nullable type ([Nullable types](types.md#nullable-types)) does not satisfy the value type constraint.</span></span> <span data-ttu-id="c51c7-238">Параметр типа с ограничением типа значения не может также иметь *constructor_constraint*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-238">A type parameter having the value type constraint cannot also have the *constructor_constraint*.</span></span>

<span data-ttu-id="c51c7-239">Типы указателей никогда не могут иметь аргументы типа и не считаются соответствует либо ссылку типа или значения ограничениям типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-239">Pointer types are never allowed to be type arguments and are not considered to satisfy either the reference type or value type constraints.</span></span>

<span data-ttu-id="c51c7-240">Если ограничение является типом класса, тип интерфейса или параметр типа, этот тип указывает минимальный «базовый тип», должен поддерживать каждый аргумент типа для этого параметра типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-240">If a constraint is a class type, an interface type, or a type parameter, that type specifies a minimal "base type" that every type argument used for that type parameter must support.</span></span> <span data-ttu-id="c51c7-241">При каждом использовании сконструированного типа или универсального метода, аргумент типа проверяются на соответствие ограничениям параметра типа во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-241">Whenever a constructed type or generic method is used, the type argument is checked against the constraints on the type parameter at compile-time.</span></span> <span data-ttu-id="c51c7-242">Аргумент типа, предоставленный должны удовлетворять условиям, описанным в [удовлетворяющий ограничениям](types.md#satisfying-constraints).</span><span class="sxs-lookup"><span data-stu-id="c51c7-242">The type argument supplied must satisfy the conditions described in [Satisfying constraints](types.md#satisfying-constraints).</span></span>

<span data-ttu-id="c51c7-243">Объект *class_type* ограничение должно удовлетворять следующим правилам:</span><span class="sxs-lookup"><span data-stu-id="c51c7-243">A *class_type* constraint must satisfy the following rules:</span></span>

*  <span data-ttu-id="c51c7-244">Тип должен быть типом класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-244">The type must be a class type.</span></span>
*  <span data-ttu-id="c51c7-245">Тип не должен быть `sealed`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-245">The type must not be `sealed`.</span></span>
*  <span data-ttu-id="c51c7-246">Тип не должен быть одним из следующих типов: `System.Array`, `System.Delegate`, `System.Enum`, или `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-246">The type must not be one of the following types: `System.Array`, `System.Delegate`, `System.Enum`, or `System.ValueType`.</span></span>
*  <span data-ttu-id="c51c7-247">Тип не должен быть `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-247">The type must not be `object`.</span></span> <span data-ttu-id="c51c7-248">Так как все типы являются производными от `object`, такое ограничение не окажет никакого влияния, если бы оно было разрешено.</span><span class="sxs-lookup"><span data-stu-id="c51c7-248">Because all types derive from `object`, such a constraint would have no effect if it were permitted.</span></span>
*  <span data-ttu-id="c51c7-249">Не более одного ограничения для данного параметра типа может быть типом класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-249">At most one constraint for a given type parameter can be a class type.</span></span>

<span data-ttu-id="c51c7-250">Тип, указанный как *interface_type* ограничение должно удовлетворять следующим правилам:</span><span class="sxs-lookup"><span data-stu-id="c51c7-250">A type specified as an *interface_type* constraint must satisfy the following rules:</span></span>

*  <span data-ttu-id="c51c7-251">Тип должен быть типом интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-251">The type must be an interface type.</span></span>
*  <span data-ttu-id="c51c7-252">Тип не должен быть указан более одного раза в заданной `where` предложение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-252">A type must not be specified more than once in a given `where` clause.</span></span>

<span data-ttu-id="c51c7-253">В любом случае ограничение может включать любые параметры типа связанный тип или объявление метода в рамках сконструированного типа и может включать в себя объявляемый тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-253">In either case, the constraint can involve any of the type parameters of the associated type or method declaration as part of a constructed type, and can involve the type being declared.</span></span>

<span data-ttu-id="c51c7-254">Любой тип класса или интерфейса, указанный как ограничения параметра типа должен быть по крайней мере такой же уровень доступности ([ограничения доступности](basic-concepts.md#accessibility-constraints)) как универсальный тип или метод объявляется.</span><span class="sxs-lookup"><span data-stu-id="c51c7-254">Any class or interface type specified as a type parameter constraint must be at least as accessible ([Accessibility constraints](basic-concepts.md#accessibility-constraints)) as the generic type or method being declared.</span></span>

<span data-ttu-id="c51c7-255">Тип, указанный как *параметр_типа* ограничение должно удовлетворять следующим правилам:</span><span class="sxs-lookup"><span data-stu-id="c51c7-255">A type specified as a *type_parameter* constraint must satisfy the following rules:</span></span>

*  <span data-ttu-id="c51c7-256">Тип должен быть параметром типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-256">The type must be a type parameter.</span></span>
*  <span data-ttu-id="c51c7-257">Тип не должен быть указан более одного раза в заданной `where` предложение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-257">A type must not be specified more than once in a given `where` clause.</span></span>

<span data-ttu-id="c51c7-258">Кроме должна существовать не было циклов в графе зависимостей параметров типа, где зависимостью является транзитивное отношение, заданное по:</span><span class="sxs-lookup"><span data-stu-id="c51c7-258">In addition there must be no cycles in the dependency graph of type parameters, where dependency is a transitive relation defined by:</span></span>

*  <span data-ttu-id="c51c7-259">Если параметр типа `T` используется в качестве ограничения для параметра типа `S` затем `S` ***зависит от*** `T`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-259">If a type parameter `T` is used as a constraint for type parameter `S` then `S` ***depends on*** `T`.</span></span>
*  <span data-ttu-id="c51c7-260">Если параметр типа `S` зависит от параметра типа `T` и `T` зависит от параметра типа `U` затем `S` ***зависит от*** `U`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-260">If a type parameter `S` depends on a type parameter `T` and `T` depends on a type parameter `U` then `S` ***depends on*** `U`.</span></span>

<span data-ttu-id="c51c7-261">Учитывая это отношение, является ошибкой во время компиляции для параметра типа зависеть от самого себя (прямо или косвенно).</span><span class="sxs-lookup"><span data-stu-id="c51c7-261">Given this relation, it is a compile-time error for a type parameter to depend on itself (directly or indirectly).</span></span>

<span data-ttu-id="c51c7-262">Все ограничения должны быть согласованы среди зависимых параметров типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-262">Any constraints must be consistent among dependent type parameters.</span></span> <span data-ttu-id="c51c7-263">Если параметр типа `S` зависит от параметра типа `T` затем:</span><span class="sxs-lookup"><span data-stu-id="c51c7-263">If type parameter `S` depends on type parameter `T` then:</span></span>

*  <span data-ttu-id="c51c7-264">`T` не должен иметь ограничение типа значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-264">`T` must not have the value type constraint.</span></span> <span data-ttu-id="c51c7-265">В противном случае `T` эффективно запечатан, поэтому `S` будет вынужден иметь тот же тип, что `T`, устраняя необходимость в два параметра типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-265">Otherwise, `T` is effectively sealed so `S` would be forced to be the same type as `T`, eliminating the need for two type parameters.</span></span>
*  <span data-ttu-id="c51c7-266">Если `S` имеет ограничение типа значения, то `T` не должен иметь *class_type* ограничение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-266">If `S` has the value type constraint then `T` must not have a *class_type* constraint.</span></span>
*  <span data-ttu-id="c51c7-267">Если `S` имеет *class_type* ограничение `A` и `T` имеет *class_type* ограничение `B` то должно быть преобразование идентификации или неявные преобразование из ссылок `A` для `B` или и неявное ссылочное преобразование из `B` для `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-267">If `S` has a *class_type* constraint `A` and `T` has a *class_type* constraint `B` then there must be an identity conversion or implicit reference conversion from `A` to `B` or an implicit reference conversion from `B` to `A`.</span></span>
*  <span data-ttu-id="c51c7-268">Если `S` также зависит от параметра типа `U` и `U` имеет *class_type* ограничение `A` и `T` имеет *class_type* ограничение `B` то должно быть преобразование идентификации или неявное преобразование ссылок из `A` для `B` или и неявное ссылочное преобразование из `B` для `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-268">If `S` also depends on type parameter `U` and `U` has a *class_type* constraint `A` and `T` has a *class_type* constraint `B` then there must be an identity conversion or implicit reference conversion from `A` to `B` or an implicit reference conversion from `B` to `A`.</span></span>

<span data-ttu-id="c51c7-269">Он является действительным для `S` иметь ограничение типа значения и `T` иметь ограничение ссылочного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-269">It is valid for `S` to have the value type constraint and `T` to have the reference type constraint.</span></span> <span data-ttu-id="c51c7-270">Фактически это ограничивает `T` типам `System.Object`, `System.ValueType`, `System.Enum`и любой другой тип интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-270">Effectively this limits `T` to the types `System.Object`, `System.ValueType`, `System.Enum`, and any interface type.</span></span>

<span data-ttu-id="c51c7-271">Если `where` предложение для параметра типа включает ограничение конструктора (который имеет форму `new()`), можно использовать `new` оператор для создания экземпляров типа ([выражения созданияобъектов](expressions.md#object-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-271">If the `where` clause for a type parameter includes a constructor constraint (which has the form `new()`), it is possible to use the `new` operator to create instances of the type ([Object creation expressions](expressions.md#object-creation-expressions)).</span></span> <span data-ttu-id="c51c7-272">Любой аргумент типа, используемый для параметра типа с ограничением конструктора должен иметь открытый конструктор без параметров (данный конструктор неявно существует для любого типа значения), или быть параметром типа с ограничением до значимого типа или ограничение конструктора (см. [Ограничения параметров типа](classes.md#type-parameter-constraints) сведения).</span><span class="sxs-lookup"><span data-stu-id="c51c7-272">Any type argument used for a type parameter with a constructor constraint must have a public parameterless constructor (this constructor implicitly exists for any value type) or be a type parameter having the value type constraint or constructor constraint (see [Type parameter constraints](classes.md#type-parameter-constraints) for details).</span></span>

<span data-ttu-id="c51c7-273">Ниже приведены примеры ограничений:</span><span class="sxs-lookup"><span data-stu-id="c51c7-273">The following are examples of constraints:</span></span>
```csharp
interface IPrintable
{
    void Print();
}

interface IComparable<T>
{
    int CompareTo(T value);
}

interface IKeyProvider<T>
{
    T GetKey();
}

class Printer<T> where T: IPrintable {...}

class SortedList<T> where T: IComparable<T> {...}

class Dictionary<K,V>
    where K: IComparable<K>
    where V: IPrintable, IKeyProvider<K>, new()
{
    ...
}
```

<span data-ttu-id="c51c7-274">Следующий пример является по ошибке, так как он вызывает цикличность в графе зависимостей параметров типа:</span><span class="sxs-lookup"><span data-stu-id="c51c7-274">The following example is in error because it causes a circularity in the dependency graph of the type parameters:</span></span>
```csharp
class Circular<S,T>
    where S: T
    where T: S                // Error, circularity in dependency graph
{
    ...
}
```

<span data-ttu-id="c51c7-275">В следующих примерах показаны некоторые недопустимые ситуации:</span><span class="sxs-lookup"><span data-stu-id="c51c7-275">The following examples illustrate additional invalid situations:</span></span>
```csharp
class Sealed<S,T>
    where S: T
    where T: struct        // Error, T is sealed
{
    ...
}

class A {...}

class B {...}

class Incompat<S,T>
    where S: A, T
    where T: B                // Error, incompatible class-type constraints
{
    ...
}

class StructWithClass<S,T,U>
    where S: struct, T
    where T: U
    where U: A                // Error, A incompatible with struct
{
    ...
}
```

<span data-ttu-id="c51c7-276">***Эффективным базовым классом*** параметра типа `T` определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c51c7-276">The ***effective base class*** of a type parameter `T` is defined as follows:</span></span>

*  <span data-ttu-id="c51c7-277">Если `T` без ограничения первичного или ограничения параметра типа, его эффективным базовым классом `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-277">If `T` has no primary constraints or type parameter constraints, its effective base class is `object`.</span></span>
*  <span data-ttu-id="c51c7-278">Если `T` имеет ограничение типа значения, его эффективным базовым классом является `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-278">If `T` has the value type constraint, its effective base class is `System.ValueType`.</span></span>
*  <span data-ttu-id="c51c7-279">Если `T` имеет *class_type* ограничение `C` , но не *параметр_типа* ограничения, его эффективным базовым классом является `C`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-279">If `T` has a *class_type* constraint `C` but no *type_parameter* constraints, its effective base class is `C`.</span></span>
*  <span data-ttu-id="c51c7-280">Если `T` не имеет *class_type* ограничение, но имеет один или несколько *параметр_типа* ограничения, его эффективным базовым классом является включаемый тип ([ликвидированный преобразования операторы](conversions.md#lifted-conversion-operators)) в набор эффективных базовых классов его *параметр_типа* ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-280">If `T` has no *class_type* constraint but has one or more *type_parameter* constraints, its effective base class is the most encompassed type ([Lifted conversion operators](conversions.md#lifted-conversion-operators)) in the set of effective base classes of its *type_parameter* constraints.</span></span> <span data-ttu-id="c51c7-281">Правила целостности убедитесь в наличии включаемый тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-281">The consistency rules ensure that such a most encompassed type exists.</span></span>
*  <span data-ttu-id="c51c7-282">Если `T` имеет оба *class_type* ограничения и один или несколько *параметр_типа* ограничения, его эффективным базовым классом является включаемый тип ([ликвидированный преобразования операторы](conversions.md#lifted-conversion-operators)) в набор, состоящий из *class_type* ограничение `T` и эффективных базовых классов его *параметр_типа* ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-282">If `T` has both a *class_type* constraint and one or more *type_parameter* constraints, its effective base class is the most encompassed type ([Lifted conversion operators](conversions.md#lifted-conversion-operators)) in the set consisting of the *class_type* constraint of `T` and the effective base classes of its *type_parameter* constraints.</span></span> <span data-ttu-id="c51c7-283">Правила целостности убедитесь в наличии включаемый тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-283">The consistency rules ensure that such a most encompassed type exists.</span></span>
*  <span data-ttu-id="c51c7-284">Если `T` имеет ограничение ссылочного типа, но не *class_type* ограничения, его эффективным базовым классом является `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-284">If `T` has the reference type constraint but no *class_type* constraints, its effective base class is `object`.</span></span>

<span data-ttu-id="c51c7-285">Для выполнения этих правил, если T имеет ограничение `V` то есть *value_type*, вместо этого используйте наиболее конкретный базовый тип `V` то есть *class_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-285">For the purpose of these rules, if T has a constraint `V` that is a *value_type*, use instead the most specific base type of `V` that is a *class_type*.</span></span> <span data-ttu-id="c51c7-286">Это не может произойти в явно заданной ограничением, но может возникнуть, когда ограничения универсального метода неявным образом наследуются объявлением метода переопределения или явной реализации метода интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-286">This can never happen in an explicitly given constraint, but may occur when the constraints of a generic method are implicitly inherited by an overriding method declaration or an explicit implementation of an interface method.</span></span>

<span data-ttu-id="c51c7-287">Эти правила гарантируют эффективное базового класса, всегда *class_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-287">These rules ensure that the effective base class is always a *class_type*.</span></span>

<span data-ttu-id="c51c7-288">***Эффективным набором интерфейса*** параметра типа `T` определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c51c7-288">The ***effective interface set*** of a type parameter `T` is defined as follows:</span></span>

*  <span data-ttu-id="c51c7-289">Если `T` не имеет *secondary_constraints*, его эффективным набором интерфейса является пустым.</span><span class="sxs-lookup"><span data-stu-id="c51c7-289">If `T` has no *secondary_constraints*, its effective interface set is empty.</span></span>
*  <span data-ttu-id="c51c7-290">Если `T` имеет *interface_type* ограничения, но не *параметр_типа* ограничения, его эффективным набором интерфейса является его набор *interface_type* ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-290">If `T` has *interface_type* constraints but no *type_parameter* constraints, its effective interface set is its set of *interface_type* constraints.</span></span>
*  <span data-ttu-id="c51c7-291">Если `T` не имеет *interface_type* ограничения, но имеет *параметр_типа* ограничения, его эффективным набором интерфейса — это объединение наборов эффективный интерфейс его *type_ параметр* ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-291">If `T` has no *interface_type* constraints but has *type_parameter* constraints, its effective interface set is the union of the effective interface sets of its *type_parameter* constraints.</span></span>
*  <span data-ttu-id="c51c7-292">Если `T` имеет оба *interface_type* ограничения и *параметр_типа* ограничения, его эффективным набором интерфейса — это объединение свой набор *interface_type* ограничения и эффективный интерфейс наборы его *параметр_типа* ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-292">If `T` has both *interface_type* constraints and *type_parameter* constraints, its effective interface set is the union of its set of *interface_type* constraints and the effective interface sets of its *type_parameter* constraints.</span></span>

<span data-ttu-id="c51c7-293">Параметр типа является ***известно, быть ссылочным типом*** если он имеет ограничение ссылочного типа или его эффективным базовым классом не `object` или `System.ValueType`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-293">A type parameter is ***known to be a reference type*** if it has the reference type constraint or its effective base class is not `object` or `System.ValueType`.</span></span>

<span data-ttu-id="c51c7-294">Значения с ограничением типа параметра типа могут использоваться для доступа к членам экземпляра, который содержится в разрешении ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-294">Values of a constrained type parameter type can be used to access the instance members implied by the constraints.</span></span> <span data-ttu-id="c51c7-295">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-295">In the example</span></span>
```csharp
interface IPrintable
{
    void Print();
}

class Printer<T> where T: IPrintable
{
    void PrintOne(T x) {
        x.Print();
    }
}
```
<span data-ttu-id="c51c7-296">методы `IPrintable` могут вызываться непосредственно на `x` поскольку `T` ограничен для реализации всегда `IPrintable`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-296">the methods of `IPrintable` can be invoked directly on `x` because `T` is constrained to always implement `IPrintable`.</span></span>

### <a name="class-body"></a><span data-ttu-id="c51c7-297">Тело класса</span><span class="sxs-lookup"><span data-stu-id="c51c7-297">Class body</span></span>

<span data-ttu-id="c51c7-298">*Class_body* класса определяет члены этого класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-298">The *class_body* of a class defines the members of that class.</span></span>

```antlr
class_body
    : '{' class_member_declaration* '}'
    ;
```

## <a name="partial-types"></a><span data-ttu-id="c51c7-299">Разделяемые типы</span><span class="sxs-lookup"><span data-stu-id="c51c7-299">Partial types</span></span>

<span data-ttu-id="c51c7-300">Объявление типа могут быть разбиты на несколько ***объявления разделяемого типа***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-300">A type declaration can be split across multiple ***partial type declarations***.</span></span> <span data-ttu-id="c51c7-301">Объявление типа создается из его частей путем согласно правилам, описанным в этом разделе, после чего он рассматривается как одно объявление течение оставшегося времени обработки во время компиляции и во время выполнения программы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-301">The type declaration is constructed from its parts by following the rules in this section, whereupon it is treated as a single declaration during the remainder of the compile-time and run-time processing of the program.</span></span>

<span data-ttu-id="c51c7-302">Объект *class_declaration*, *struct_declaration* или *interface_declaration* представляет объявление разделяемого типа, если он включает `partial` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-302">A *class_declaration*, *struct_declaration* or *interface_declaration* represents a partial type declaration if it includes a `partial` modifier.</span></span> <span data-ttu-id="c51c7-303">`partial` не является ключевым словом и действует только в качестве модификатора, если он отображается непосредственно перед ключевое слово `class`, `struct` или `interface` в объявлении типа или перед типом `void` в объявлении метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-303">`partial` is not a keyword, and only acts as a modifier if it appears immediately before one of the keywords `class`, `struct` or `interface` in a type declaration, or before the type `void` in a method declaration.</span></span> <span data-ttu-id="c51c7-304">В других контекстах он может использоваться в качестве обычного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-304">In other contexts it can be used as a normal identifier.</span></span>

<span data-ttu-id="c51c7-305">Каждая часть объявления разделяемого типа должна включать `partial` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-305">Each part of a partial type declaration must include a `partial` modifier.</span></span> <span data-ttu-id="c51c7-306">Она должна иметь то же имя и быть объявлен в том же пространстве имен или объявление типа, что и другие части.</span><span class="sxs-lookup"><span data-stu-id="c51c7-306">It must have the same name  and be declared in the same namespace or type declaration as the other parts.</span></span> <span data-ttu-id="c51c7-307">`partial` Модификатор указывает, что могут существовать дополнительные части объявления типа, но наличие таких дополнительных компонентов не является обязательным; это недопустимо для типа с одним объявлением для включения `partial` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-307">The `partial` modifier indicates that additional parts of the type declaration may exist elsewhere, but the existence of such additional parts is not a requirement; it is valid for a type with a single declaration to include the `partial` modifier.</span></span>

<span data-ttu-id="c51c7-308">Все части разделяемого типа должны быть скомпилированы вместе, таким образом, чтобы компоненты могут быть объединены во время компиляции в объявления одного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-308">All parts of a partial type must be compiled together such that the parts can be merged at compile-time into a single type declaration.</span></span> <span data-ttu-id="c51c7-309">Разделяемые типы специально не позволяют расширить уже скомпилированных типов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-309">Partial types specifically do not allow already compiled types to be extended.</span></span>

<span data-ttu-id="c51c7-310">Вложенные типы могут быть объявлены в несколько частей с помощью `partial` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-310">Nested types may be declared in multiple parts by using the `partial` modifier.</span></span> <span data-ttu-id="c51c7-311">Как правило, содержащий тип объявляется с помощью `partial` объявив также и каждая часть вложенного типа в другой части содержащего его типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-311">Typically, the containing type is declared using `partial` as well, and each part of the nested type is declared in a different part of the containing type.</span></span>

<span data-ttu-id="c51c7-312">`partial` Модификатора не допускается в объявлениях делегатов или перечислений.</span><span class="sxs-lookup"><span data-stu-id="c51c7-312">The `partial` modifier is not permitted on delegate or enum declarations.</span></span>

### <a name="attributes"></a><span data-ttu-id="c51c7-313">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="c51c7-313">Attributes</span></span>

<span data-ttu-id="c51c7-314">Атрибуты разделяемого типа определяются путем объединения в неопределенном порядке, атрибуты каждой части.</span><span class="sxs-lookup"><span data-stu-id="c51c7-314">The attributes of a partial type are determined by combining, in an unspecified order, the attributes of each of the parts.</span></span> <span data-ttu-id="c51c7-315">Если атрибут помещается на несколько частей, это эквивалентно указании несколько раз для типа атрибута.</span><span class="sxs-lookup"><span data-stu-id="c51c7-315">If an attribute is placed on multiple parts, it is equivalent to specifying the attribute multiple times on the type.</span></span> <span data-ttu-id="c51c7-316">Например две части:</span><span class="sxs-lookup"><span data-stu-id="c51c7-316">For example, the two parts:</span></span>

```csharp
[Attr1, Attr2("hello")]
partial class A {}

[Attr3, Attr2("goodbye")]
partial class A {}
```
<span data-ttu-id="c51c7-317">Например, эквивалентны к объявлению:</span><span class="sxs-lookup"><span data-stu-id="c51c7-317">are equivalent to a declaration such as:</span></span>
```csharp
[Attr1, Attr2("hello"), Attr3, Attr2("goodbye")]
class A {}
```

<span data-ttu-id="c51c7-318">Аналогичным образом объединить атрибуты параметров типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-318">Attributes on type parameters combine in a similar fashion.</span></span>

### <a name="modifiers"></a><span data-ttu-id="c51c7-319">Модификаторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-319">Modifiers</span></span>

<span data-ttu-id="c51c7-320">Если объявление разделяемого типа содержит спецификацию доступности ( `public`, `protected`, `internal`, и `private` модификаторы) оно должно быть согласовано с все остальные составляющие, которые включают спецификацию доступности.</span><span class="sxs-lookup"><span data-stu-id="c51c7-320">When a partial type declaration includes an accessibility specification (the `public`, `protected`, `internal`, and `private` modifiers) it must agree with all other parts that include an accessibility specification.</span></span> <span data-ttu-id="c51c7-321">Если ни одна часть разделяемого типа включает спецификацию доступности, типу задается соответствующая доступность по умолчанию ([объявленную доступность](basic-concepts.md#declared-accessibility)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-321">If no part of a partial type includes an accessibility specification, the type is given the appropriate default accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)).</span></span>

<span data-ttu-id="c51c7-322">Если один или более частичных объявлениях вложенного типа включают `new` модификатор, предупреждение не передается в том случае, если вложенный тип скрывает унаследованный член ([скрытие через наследование](basic-concepts.md#hiding-through-inheritance)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-322">If one or more partial declarations of a nested type include a `new` modifier, no warning is reported if the nested type hides an inherited member ([Hiding through inheritance](basic-concepts.md#hiding-through-inheritance)).</span></span>

<span data-ttu-id="c51c7-323">Если включить один или более частичных объявлениях класса `abstract` модификатор класса будет считаться абстрактным ([абстрактные классы](classes.md#abstract-classes)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-323">If one or more partial declarations of a class include an `abstract` modifier, the class is considered abstract ([Abstract classes](classes.md#abstract-classes)).</span></span> <span data-ttu-id="c51c7-324">В противном случае класс считается абстрактным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-324">Otherwise, the class is considered non-abstract.</span></span>

<span data-ttu-id="c51c7-325">Если включить один или более частичных объявлениях класса `sealed` модификатор класса будет считаться запечатанным ([запечатанных классов](classes.md#sealed-classes)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-325">If one or more partial declarations of a class include a `sealed` modifier, the class is considered sealed ([Sealed classes](classes.md#sealed-classes)).</span></span> <span data-ttu-id="c51c7-326">В противном случае класс считается незапечатанный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-326">Otherwise, the class is considered unsealed.</span></span>

<span data-ttu-id="c51c7-327">Обратите внимание на то, что класс не может быть одновременно абстрактным и запечатанным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-327">Note that a class cannot be both abstract and sealed.</span></span>

<span data-ttu-id="c51c7-328">Когда `unsafe` модификатор используется в объявлении разделяемого типа только соответствующая часть считается небезопасным контекстом ([небезопасных контекстах](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-328">When the `unsafe` modifier is used on a partial type declaration, only that particular part is considered an unsafe context ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span>

### <a name="type-parameters-and-constraints"></a><span data-ttu-id="c51c7-329">Тип параметров и ограничений</span><span class="sxs-lookup"><span data-stu-id="c51c7-329">Type parameters and constraints</span></span>

<span data-ttu-id="c51c7-330">Если универсальный тип объявлен в нескольких частей, каждая часть должна формулировать параметры типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-330">If a generic type is declared in multiple parts, each part must state the type parameters.</span></span> <span data-ttu-id="c51c7-331">Каждая часть должна иметь одинаковое число параметров типа и то же имя для каждого параметра типа в порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-331">Each part must have the same number of type parameters, and the same name for each type parameter, in order.</span></span>

<span data-ttu-id="c51c7-332">Если объявление разделяемого универсального типа содержит ограничения (`where` предложений), ограничения должны быть согласованы со всеми другими частями, которые включают ограничения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-332">When a partial generic type declaration includes constraints (`where` clauses), the constraints must agree with all other parts that include constraints.</span></span> <span data-ttu-id="c51c7-333">В частности каждая часть, содержащая ограничения должны иметь ограничения для одного набора параметров типа, и для каждого параметра типа наборы первичных, вторичная реплика и ограничений конструктора должно изменяться.</span><span class="sxs-lookup"><span data-stu-id="c51c7-333">Specifically, each part that includes constraints must have constraints for the same set of type parameters, and for each type parameter the sets of primary, secondary, and constructor constraints must be equivalent.</span></span> <span data-ttu-id="c51c7-334">Два набора ограничений эквивалентны, если они содержат те же элементы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-334">Two sets of constraints are equivalent if they contain the same members.</span></span> <span data-ttu-id="c51c7-335">Если ни одна часть разделяемого типа универсальный тип ограничения параметра типа, параметры считаются без ограничений.</span><span class="sxs-lookup"><span data-stu-id="c51c7-335">If no part of a partial generic type specifies type parameter constraints, the type parameters are considered unconstrained.</span></span>

<span data-ttu-id="c51c7-336">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-336">The example</span></span>
```csharp
partial class Dictionary<K,V>
    where K: IComparable<K>
    where V: IKeyProvider<K>, IPersistable
{
    ...
}

partial class Dictionary<K,V>
    where V: IPersistable, IKeyProvider<K>
    where K: IComparable<K>
{
    ...
}

partial class Dictionary<K,V>
{
    ...
}
```
<span data-ttu-id="c51c7-337">используется правильная так, как части, включающие ограничения (первые две) эффективно укажите же набор основной, дополнительный и ограничений конструктора для одного набора параметров типа, соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-337">is correct because those parts that include constraints (the first two) effectively specify the same set of primary, secondary, and constructor constraints for the same set of type parameters, respectively.</span></span>

### <a name="base-class"></a><span data-ttu-id="c51c7-338">Базовый класс</span><span class="sxs-lookup"><span data-stu-id="c51c7-338">Base class</span></span>

<span data-ttu-id="c51c7-339">Если объявление разделяемого класса содержит базовый класс должен соответствовать все остальные составляющие, которые включают спецификации базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-339">When a partial class declaration includes a base class specification it must agree with all other parts that include a base class specification.</span></span> <span data-ttu-id="c51c7-340">Если никакая часть разделяемый класс содержит спецификацию базового класса, базовый класс становится `System.Object` ([базовые классы](classes.md#base-classes)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-340">If no part of a partial class includes a base class specification, the base class becomes `System.Object` ([Base classes](classes.md#base-classes)).</span></span>

### <a name="base-interfaces"></a><span data-ttu-id="c51c7-341">Базовые интерфейсы</span><span class="sxs-lookup"><span data-stu-id="c51c7-341">Base interfaces</span></span>

<span data-ttu-id="c51c7-342">Набор базовых интерфейсов для типа, объявленного в нескольких частях является объединение базовые интерфейсы, указанные на каждой из них.</span><span class="sxs-lookup"><span data-stu-id="c51c7-342">The set of base interfaces for a type declared in multiple parts is the union of the base interfaces specified on each part.</span></span> <span data-ttu-id="c51c7-343">Определенный базовый интерфейс может быть имя на каждой из них только один раз, но разрешено несколько частей имени же базовых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-343">A particular base interface may only be named once on each part, but it is permitted for multiple parts to name the same base interface(s).</span></span> <span data-ttu-id="c51c7-344">Должно существовать только одна реализация члены любого заданного базового интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-344">There must only be one implementation of the members of any given base interface.</span></span>

<span data-ttu-id="c51c7-345">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-345">In the example</span></span>
```csharp
partial class C: IA, IB {...}

partial class C: IC {...}

partial class C: IA, IB {...}
```
<span data-ttu-id="c51c7-346">набор базовых интерфейсов для класса `C` — `IA`, `IB`, и `IC`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-346">the set of base interfaces for class `C` is `IA`, `IB`, and `IC`.</span></span>

<span data-ttu-id="c51c7-347">Как правило каждая часть предоставляет реализацию интерфейсов, объявленных в соответствующей стороной; Тем не менее это не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-347">Typically, each part provides an implementation of the interface(s) declared on that part; however, this is not a requirement.</span></span> <span data-ttu-id="c51c7-348">Одна часть может предоставлять реализацию для интерфейса, объявленного в другой части:</span><span class="sxs-lookup"><span data-stu-id="c51c7-348">A part may provide the implementation for an interface declared on a different part:</span></span>
```csharp
partial class X
{
    int IComparable.CompareTo(object o) {...}
}

partial class X: IComparable
{
    ...
}
```

### <a name="members"></a><span data-ttu-id="c51c7-349">Участники</span><span class="sxs-lookup"><span data-stu-id="c51c7-349">Members</span></span>

<span data-ttu-id="c51c7-350">За исключением разделяемые методы ([разделяемые методы](classes.md#partial-methods)), набор элементов типа, объявленного в нескольких частях представляет собой просто объединение набора элементов, объявленных в каждой части.</span><span class="sxs-lookup"><span data-stu-id="c51c7-350">With the exception of partial methods ([Partial methods](classes.md#partial-methods)), the set of members of a type declared in multiple parts is simply the union of the set of members declared in each part.</span></span> <span data-ttu-id="c51c7-351">Тела все части объявления типа совместно используют одно и то же пространство объявления ([объявления](basic-concepts.md#declarations)) и область каждого элемента ([областей](basic-concepts.md#scopes)) распространяется на все части тела.</span><span class="sxs-lookup"><span data-stu-id="c51c7-351">The bodies of all parts of the type declaration share the same declaration space ([Declarations](basic-concepts.md#declarations)), and the scope of each member ([Scopes](basic-concepts.md#scopes)) extends to the bodies of all the parts.</span></span> <span data-ttu-id="c51c7-352">Домен доступности любого члена всегда содержит все части вмещающего типа; `private` член, объявленный в одной из частей, свободно доступен из другой части.</span><span class="sxs-lookup"><span data-stu-id="c51c7-352">The accessibility domain of any member always includes all the parts of the enclosing type; a `private` member declared in one part is freely accessible from another part.</span></span> <span data-ttu-id="c51c7-353">Это ошибка времени компиляции, чтобы объявить один и тот же элемент в более чем одной части типа, если этот член является типом с `partial` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-353">It is a compile-time error to declare the same member in more than one part of the type, unless that member is a type with the `partial` modifier.</span></span>

```csharp
partial class A
{
    int x;                     // Error, cannot declare x more than once

    partial class Inner        // Ok, Inner is a partial type
    {
        int y;
    }
}

partial class A
{
    int x;                     // Error, cannot declare x more than once

    partial class Inner        // Ok, Inner is a partial type
    {
        int z;
    }
}
```

<span data-ttu-id="c51c7-354">Порядок членов типа редко важен для кода C#, но может оказаться слишком дорогим при взаимодействии с другими языками и средами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-354">The ordering of members within a type is rarely significant to C# code, but may be significant when interfacing with other languages and environments.</span></span> <span data-ttu-id="c51c7-355">В таких случаях порядок членов типа, объявленного в нескольких частях не определено.</span><span class="sxs-lookup"><span data-stu-id="c51c7-355">In these cases, the ordering of members within a type declared in multiple parts is undefined.</span></span>

### <a name="partial-methods"></a><span data-ttu-id="c51c7-356">Разделяемые методы</span><span class="sxs-lookup"><span data-stu-id="c51c7-356">Partial methods</span></span>

<span data-ttu-id="c51c7-357">Разделяемые методы могут быть определены в одной части объявления типа и реализованы в другой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-357">Partial methods can be defined in one part of a type declaration and implemented in another.</span></span> <span data-ttu-id="c51c7-358">Реализация является необязательной. Если ни одна частей реализует разделяемого метода, объявления разделяемого метода и все вызовы к нему удаляются из объявления типа, полученного из комбинации из частей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-358">The implementation is optional; if no part implements the partial method, the partial method declaration and all calls to it are removed from the type declaration resulting from the combination of the parts.</span></span>

<span data-ttu-id="c51c7-359">Разделяемые методы не удается определить модификаторы доступа, но являются неявно `private`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-359">Partial methods cannot define access modifiers, but are implicitly `private`.</span></span> <span data-ttu-id="c51c7-360">Возвращаемый тип должен быть `void`, и их параметры не могут иметь `out` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-360">Their return type must be `void`, and their parameters cannot have the `out` modifier.</span></span> <span data-ttu-id="c51c7-361">Идентификатор `partial` распознается как специальное ключевое слово в объявлении метода только в том случае, если он отображается прямо перед `void` типа; в противном случае его можно использовать в качестве обычного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-361">The identifier `partial` is recognized as a special keyword in a method declaration only if it appears right before the `void` type; otherwise it can be used as a normal identifier.</span></span> <span data-ttu-id="c51c7-362">Разделяемый метод не может явно реализовывать методы интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-362">A partial method cannot explicitly implement interface methods.</span></span>

<span data-ttu-id="c51c7-363">Существует два вида объявления разделяемого метода: Если текст объявления метода точки с запятой, объявление считается ***определяющее объявление разделяемого метода***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-363">There are two kinds of partial method declarations: If the body of the method declaration is a semicolon, the declaration is said to be a ***defining partial method declaration***.</span></span> <span data-ttu-id="c51c7-364">Если текст задается как *блок*, объявление считается ***реализующего объявления разделяемого метода***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-364">If the body is given as a *block*, the declaration is said to be an ***implementing partial method declaration***.</span></span> <span data-ttu-id="c51c7-365">Между частями объявление типа может существовать только одно определяющее объявление разделяемого метода с указанным кодом и может использоваться только один, реализующего объявления разделяемого метода с указанным кодом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-365">Across the parts of a type declaration there can be only one defining partial method declaration with a given signature, and there can be only one implementing partial method declaration with a given signature.</span></span> <span data-ttu-id="c51c7-366">Если предоставляется реализующего объявления разделяемого метода, соответствующее определяющее объявление разделяемого метода должна существовать и объявления должны соответствовать как указано ниже:</span><span class="sxs-lookup"><span data-stu-id="c51c7-366">If an implementing partial method declaration is given, a corresponding defining partial method declaration must exist, and the declarations must match as specified in the following:</span></span>

* <span data-ttu-id="c51c7-367">Объявления должны иметь одинаковые модификаторы (не обязательно в том же порядке), имя метода, количество параметров типа и количество параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-367">The declarations must have the same modifiers (although not necessarily in the same order), method name, number of type parameters and number of parameters.</span></span>
* <span data-ttu-id="c51c7-368">Соответствующие параметры в объявлениях должны иметь одинаковые модификаторы (не обязательно в том же порядке) и те же типы (остаток от деления различия в именах параметров типа).</span><span class="sxs-lookup"><span data-stu-id="c51c7-368">Corresponding parameters in the declarations must have the same modifiers (although not necessarily in the same order) and the same types (modulo differences in type parameter names).</span></span>
* <span data-ttu-id="c51c7-369">Соответствующие параметры типа в объявлениях должны иметь те же ограничения (остаток от деления различия в именах параметров типа).</span><span class="sxs-lookup"><span data-stu-id="c51c7-369">Corresponding type parameters in the declarations must have the same constraints (modulo differences in type parameter names).</span></span>

<span data-ttu-id="c51c7-370">Реализующего объявления разделяемого метода могут отображаться в той же части как соответствующие определяющее объявление разделяемого метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-370">An implementing partial method declaration can appear in the same part as the corresponding defining partial method declaration.</span></span>

<span data-ttu-id="c51c7-371">Определение разделяемого метода участвует в разрешении перегрузки.</span><span class="sxs-lookup"><span data-stu-id="c51c7-371">Only a defining partial method participates in overload resolution.</span></span> <span data-ttu-id="c51c7-372">Таким образом независимо от того, имеется ли реализующего объявления задан, то выражения вызова могут обращаться к вызовам разделяемого метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-372">Thus, whether or not an implementing declaration is given, invocation expressions may resolve to invocations of the partial method.</span></span> <span data-ttu-id="c51c7-373">Так как разделяемый метод всегда возвращает `void`, такие выражения вызова всегда будет операторы выражений.</span><span class="sxs-lookup"><span data-stu-id="c51c7-373">Because a partial method always returns `void`, such invocation expressions will always be expression statements.</span></span> <span data-ttu-id="c51c7-374">Кроме того так как разделяемый метод является неявно `private`, такие инструкции будет всегда находятся в одной из частей объявления типа, в котором объявлен разделяемого метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-374">Furthermore, because a partial method is implicitly `private`, such statements will always occur within one of the parts of the type declaration within which the partial method is declared.</span></span>

<span data-ttu-id="c51c7-375">Если ни одна часть объявления разделяемого типа содержит реализующее объявление для заданного разделяемого метода, любой оператор выражения вызова этого метода просто удаляется из комбинированного объявления типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-375">If no part of a partial type declaration contains an implementing declaration for a given partial method, any expression statement invoking it is simply removed from the combined type declaration.</span></span> <span data-ttu-id="c51c7-376">Таким образом, выражение вызова, включая любые групповые выражения, не оказывает влияния во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-376">Thus the invocation expression, including any constituent expressions, has no effect at run-time.</span></span> <span data-ttu-id="c51c7-377">Разделяемый метод сам также удаляется и не будет членом комбинированного объявления типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-377">The partial method itself is also removed and will not be a member of the combined type declaration.</span></span>

<span data-ttu-id="c51c7-378">Если реализующее объявление существует для заданного разделяемого метода, вызовы методов разделяемых методов, будут сохранены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-378">If an implementing declaration exist for a given partial method, the invocations of the partial methods are retained.</span></span> <span data-ttu-id="c51c7-379">Разделяемый метод приводит к возникновению объявление метода, аналогичную реализующего объявления разделяемого метода, за исключением следующих:</span><span class="sxs-lookup"><span data-stu-id="c51c7-379">The partial method gives rise to a method declaration similar to the implementing partial method declaration except for the following:</span></span>

* <span data-ttu-id="c51c7-380">`partial` Модификатор не включено</span><span class="sxs-lookup"><span data-stu-id="c51c7-380">The `partial` modifier is not included</span></span>
* <span data-ttu-id="c51c7-381">Атрибуты в полученный объявление метода, которые объединенный определяющего и реализующего объявления разделяемого метода в неопределенном порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-381">The attributes in the resulting method declaration are the combined attributes of the defining and the implementing partial method declaration in unspecified order.</span></span> <span data-ttu-id="c51c7-382">Не удалять дубликаты.</span><span class="sxs-lookup"><span data-stu-id="c51c7-382">Duplicates are not removed.</span></span>
* <span data-ttu-id="c51c7-383">Атрибуты параметров итоговый объявление метода, которые объединенный соответствующих параметров определяющего и реализующего объявления разделяемого метода в неопределенном порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-383">The attributes on the parameters of the resulting method declaration are the combined attributes of the corresponding parameters of the defining and the implementing partial method declaration in unspecified order.</span></span> <span data-ttu-id="c51c7-384">Не удалять дубликаты.</span><span class="sxs-lookup"><span data-stu-id="c51c7-384">Duplicates are not removed.</span></span>

<span data-ttu-id="c51c7-385">Если определяющее объявление, но не реализующего объявления указан для разделяемого метода M, применяются следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="c51c7-385">If a defining declaration but not an implementing declaration is given for a partial method M, the following restrictions apply:</span></span>

* <span data-ttu-id="c51c7-386">Произошла ошибка во время компиляции, для создания делегата к методу ([выражения создания делегата](expressions.md#delegate-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-386">It is a compile-time error to create a delegate to method ([Delegate creation expressions](expressions.md#delegate-creation-expressions)).</span></span>
* <span data-ttu-id="c51c7-387">Произошла ошибка во время компиляции, для ссылки на `M` внутри анонимную функцию, которая преобразуется в тип дерева выражения ([вычисление анонимной функции преобразования к типы дерева выражений](conversions.md#evaluation-of-anonymous-function-conversions-to-expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-387">It is a compile-time error to refer to `M` inside an anonymous function that is converted to an expression tree type ([Evaluation of anonymous function conversions to expression tree types](conversions.md#evaluation-of-anonymous-function-conversions-to-expression-tree-types)).</span></span>
* <span data-ttu-id="c51c7-388">Выражения, возникающие как часть вызова `M` не влияют на состояние определенного присваивания ([определенного присваивания](variables.md#definite-assignment)), которое может привести к ошибкам во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-388">Expressions occurring as part of an invocation of `M` do not affect the definite assignment state ([Definite assignment](variables.md#definite-assignment)), which can potentially lead to compile-time errors.</span></span>
* <span data-ttu-id="c51c7-389">`M` не может быть точкой входа для приложения ([запуск приложения](basic-concepts.md#application-startup)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-389">`M` cannot be the entry point for an application ([Application Startup](basic-concepts.md#application-startup)).</span></span>

<span data-ttu-id="c51c7-390">Разделяемые методы можно использовать для разрешения одной части объявления типа, для настройки поведения другой части, например, один, который создается с помощью средства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-390">Partial methods are useful for allowing one part of a type declaration to customize the behavior of another part, e.g., one that is generated by a tool.</span></span> <span data-ttu-id="c51c7-391">Рассмотрим следующее объявление разделяемого класса:</span><span class="sxs-lookup"><span data-stu-id="c51c7-391">Consider the following partial class declaration:</span></span>
```csharp
partial class Customer
{
    string name;

    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }

    }

    partial void OnNameChanging(string newName);

    partial void OnNameChanged();
}
```

<span data-ttu-id="c51c7-392">Если этот класс будет скомпилирован без любого из других частей, определяющие объявления разделяемого метода и их вызовы будут удалены, и результирующее комбинированное объявление класса будет эквивалентно следующему:</span><span class="sxs-lookup"><span data-stu-id="c51c7-392">If this class is compiled without any other parts, the defining partial method declarations and their invocations will be removed, and the resulting combined class declaration will be equivalent to the following:</span></span>
```csharp
class Customer
{
    string name;

    public string Name {
        get { return name; }
        set { name = value; }
    }
}
```

<span data-ttu-id="c51c7-393">Предположим, что задана другая часть, тем не менее, который предоставляет реализующего объявления разделяемых методов:</span><span class="sxs-lookup"><span data-stu-id="c51c7-393">Assume that another part is given, however, which provides implementing declarations of the partial methods:</span></span>
```csharp
partial class Customer
{
    partial void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }

    partial void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

<span data-ttu-id="c51c7-394">Затем полученный комбинированное объявление класса будет эквивалентно следующему:</span><span class="sxs-lookup"><span data-stu-id="c51c7-394">Then the resulting combined class declaration will be equivalent to the following:</span></span>
```csharp
class Customer
{
    string name;

    public string Name {
        get { return name; }
        set {
            OnNameChanging(value);
            name = value;
            OnNameChanged();
        }

    }

    void OnNameChanging(string newName)
    {
        Console.WriteLine("Changing " + name + " to " + newName);
    }

    void OnNameChanged()
    {
        Console.WriteLine("Changed to " + name);
    }
}
```

### <a name="name-binding"></a><span data-ttu-id="c51c7-395">Имя привязки</span><span class="sxs-lookup"><span data-stu-id="c51c7-395">Name binding</span></span>

<span data-ttu-id="c51c7-396">Несмотря на то, что каждая часть расширяемого типа должен быть объявлен в том же пространстве имен, части обычно записывается в различных объявлений пространств имен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-396">Although each part of an extensible type must be declared within the same namespace, the parts are typically written within different namespace declarations.</span></span> <span data-ttu-id="c51c7-397">Таким образом разные `using` директивы ([директив Using](namespaces.md#using-directives)) могут присутствовать для каждой части.</span><span class="sxs-lookup"><span data-stu-id="c51c7-397">Thus, different `using` directives ([Using directives](namespaces.md#using-directives)) may be present for each part.</span></span> <span data-ttu-id="c51c7-398">При интерпретации простые имена ([вывод типа](expressions.md#type-inference)) в рамках одной части, только `using` директивы из объявлений пространства имен, содержащего той части считаются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-398">When interpreting simple names ([Type inference](expressions.md#type-inference)) within one part, only the `using` directives of the namespace declaration(s) enclosing that part are considered.</span></span> <span data-ttu-id="c51c7-399">Это может привести к тому же идентификатор, имеет разные значения в различных частей:</span><span class="sxs-lookup"><span data-stu-id="c51c7-399">This may result in the same identifier having different meanings in different parts:</span></span>
```csharp
namespace N
{
    using List = System.Collections.ArrayList;

    partial class A
    {
        List x;                // x has type System.Collections.ArrayList
    }
}

namespace N
{
    using List = Widgets.LinkedList;

    partial class A
    {
        List y;                // y has type Widgets.LinkedList
    }
}
```

## <a name="class-members"></a><span data-ttu-id="c51c7-400">Члены класса</span><span class="sxs-lookup"><span data-stu-id="c51c7-400">Class members</span></span>

<span data-ttu-id="c51c7-401">Члены класса состоят из членов, представленных его *class_member_declaration*s и члены, унаследованные от прямого базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-401">The members of a class consist of the members introduced by its *class_member_declaration*s and the members inherited from the direct base class.</span></span>

```antlr
class_member_declaration
    : constant_declaration
    | field_declaration
    | method_declaration
    | property_declaration
    | event_declaration
    | indexer_declaration
    | operator_declaration
    | constructor_declaration
    | destructor_declaration
    | static_constructor_declaration
    | type_declaration
    ;
```

<span data-ttu-id="c51c7-402">Члены типа класса можно разделить на следующие категории:</span><span class="sxs-lookup"><span data-stu-id="c51c7-402">The members of a class type are divided into the following categories:</span></span>

*  <span data-ttu-id="c51c7-403">Константы, представляющие постоянные значения, связанные с классом ([константы](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-403">Constants, which represent constant values associated with the class ([Constants](classes.md#constants)).</span></span>
*  <span data-ttu-id="c51c7-404">Поля, являющиеся переменные класса ([поля](classes.md#fields)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-404">Fields, which are the variables of the class ([Fields](classes.md#fields)).</span></span>
*  <span data-ttu-id="c51c7-405">Методы, реализующие вычисления и действия, которые могут быть выполнены с помощью класса ([методы](classes.md#methods)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-405">Methods, which implement the computations and actions that can be performed by the class ([Methods](classes.md#methods)).</span></span>
*  <span data-ttu-id="c51c7-406">Свойства, определяющие именованные характеристики и действия, связанные с чтением и записью данных характеристик ([свойства](classes.md#properties)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-406">Properties, which define named characteristics and the actions associated with reading and writing those characteristics ([Properties](classes.md#properties)).</span></span>
*  <span data-ttu-id="c51c7-407">События, которые определяют уведомления, которые могут быть созданы с помощью класса ([события](classes.md#events)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-407">Events, which define notifications that can be generated by the class ([Events](classes.md#events)).</span></span>
*  <span data-ttu-id="c51c7-408">Индексаторы, которые допускают экземпляры класса для индексирования таким же образом (синтаксически), как массивы ([индексаторы](classes.md#indexers)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-408">Indexers, which permit instances of the class to be indexed in the same way (syntactically) as arrays ([Indexers](classes.md#indexers)).</span></span>
*  <span data-ttu-id="c51c7-409">Операторы, которые определяют операторы выражений, которые могут быть применены к экземплярам класса ([операторы](classes.md#operators)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-409">Operators, which define the expression operators that can be applied to instances of the class ([Operators](classes.md#operators)).</span></span>
*  <span data-ttu-id="c51c7-410">Конструкторы экземпляров, которые реализуют действия, необходимые для инициализации экземпляров класса ([конструкторы экземпляров](classes.md#instance-constructors))</span><span class="sxs-lookup"><span data-stu-id="c51c7-410">Instance constructors, which implement the actions required to initialize instances of the class ([Instance constructors](classes.md#instance-constructors))</span></span>
*  <span data-ttu-id="c51c7-411">Деструкторы, реализующие действия, выполняемые перед окончательным удалением экземпляров класса ([деструкторы](classes.md#destructors)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-411">Destructors, which implement the actions to be performed before instances of the class are permanently discarded ([Destructors](classes.md#destructors)).</span></span>
*  <span data-ttu-id="c51c7-412">Статические конструкторы, которые реализуют действия, необходимые для инициализации самого класса ([статические конструкторы](classes.md#static-constructors)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-412">Static constructors, which implement the actions required to initialize the class itself ([Static constructors](classes.md#static-constructors)).</span></span>
*  <span data-ttu-id="c51c7-413">Типы, представляющие типы, которые являются локальными для класса ([вложенные типы](classes.md#nested-types)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-413">Types, which represent the types that are local to the class ([Nested types](classes.md#nested-types)).</span></span>

<span data-ttu-id="c51c7-414">Члены, которые могут содержать исполняемый код, совокупно называются *функции-члены* типа класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-414">Members that can contain executable code are collectively known as the *function members* of the class type.</span></span> <span data-ttu-id="c51c7-415">Функции-члены типа класса имеют методы, свойства, события, индексаторы, операторы, конструкторы экземпляров, деструкторы и статические конструкторы этого типа класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-415">The function members of a class type are the methods, properties, events, indexers, operators, instance constructors,  destructors, and static constructors of that class type.</span></span>

<span data-ttu-id="c51c7-416">Объект *class_declaration* создает новую область объявления ([объявления](basic-concepts.md#declarations)) и *class_member_declaration*s, непосредственно содержащиеся в *класса _declaration* представляют новые члены в этой области объявления.</span><span class="sxs-lookup"><span data-stu-id="c51c7-416">A *class_declaration* creates a new declaration space ([Declarations](basic-concepts.md#declarations)), and the *class_member_declaration*s immediately contained by the *class_declaration* introduce new members into this declaration space.</span></span> <span data-ttu-id="c51c7-417">Следующие правила применяются к *class_member_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-417">The following rules apply to *class_member_declaration*s:</span></span>

*  <span data-ttu-id="c51c7-418">Конструкторы экземпляров, деструкторы и статические конструкторы должны иметь то же имя, что немедленно включающего класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-418">Instance constructors, destructors and static constructors must have the same name as the immediately enclosing class.</span></span> <span data-ttu-id="c51c7-419">Все остальные элементы должны иметь имена, которые отличаются от имени немедленно включающего класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-419">All other members must have names that differ from the name of the immediately enclosing class.</span></span>
*  <span data-ttu-id="c51c7-420">Имя константы, поля, свойства, события или тип должны отличаться от имен всех остальных членов, объявленных в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-420">The name of a constant, field, property, event, or type must differ from the names of all other members declared in the same class.</span></span>
*  <span data-ttu-id="c51c7-421">Имя метода должно отличаться от имен всех остальных не методов, объявленных в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-421">The name of a method must differ from the names of all other non-methods declared in the same class.</span></span> <span data-ttu-id="c51c7-422">Кроме того, подпись ([сигнатуры и перегрузка](basic-concepts.md#signatures-and-overloading)) из метода должны отличаться от сигнатур всех других методов, объявленных в том же классе, и двух методов, объявленных в том же классе не могут иметь сигнатуры, отличающихся только по `ref` и `out`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-422">In addition, the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of a method must differ from the signatures of all other methods declared in the same class, and two methods declared in the same class may not have signatures that differ solely by `ref` and `out`.</span></span>
*  <span data-ttu-id="c51c7-423">Сигнатура конструктора экземпляра должна отличаться от сигнатур всех других конструкторов экземпляров, объявленных в том же классе, и двух конструкторов, объявленных в том же классе может не иметь подписи, которые отличаются только модификаторами `ref` и `out`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-423">The signature of an instance constructor must differ from the signatures of all other instance constructors declared in the same class, and two constructors declared in the same class may not have signatures that differ solely by `ref` and `out`.</span></span>
*  <span data-ttu-id="c51c7-424">Сигнатура индексатора должна отличаться от сигнатур любых других индексаторов, объявленных в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-424">The signature of an indexer must differ from the signatures of all other indexers declared in the same class.</span></span>
*  <span data-ttu-id="c51c7-425">Сигнатура оператора должна отличаться от сигнатур всех других операторов, объявленных в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-425">The signature of an operator must differ from the signatures of all other operators declared in the same class.</span></span>

<span data-ttu-id="c51c7-426">Наследуемые члены типа класса ([наследования](classes.md#inheritance)) не являются частью области объявления класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-426">The inherited members of a class type ([Inheritance](classes.md#inheritance)) are not part of the declaration space of a class.</span></span> <span data-ttu-id="c51c7-427">Таким образом производный класс может объявить элемент с тем же именем или сигнатурой, наследуемого члена (что приводит к скрытию унаследованного члена).</span><span class="sxs-lookup"><span data-stu-id="c51c7-427">Thus, a derived class is allowed to declare a member with the same name or signature as an inherited member (which in effect hides the inherited member).</span></span>

### <a name="the-instance-type"></a><span data-ttu-id="c51c7-428">Тип экземпляра</span><span class="sxs-lookup"><span data-stu-id="c51c7-428">The instance type</span></span>

<span data-ttu-id="c51c7-429">Каждое объявление класса имеет связанный привязанный тип ([привязан и несвязанные типы](types.md#bound-and-unbound-types)), ***тип экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-429">Each class declaration has an associated bound type ([Bound and unbound types](types.md#bound-and-unbound-types)), the ***instance type***.</span></span> <span data-ttu-id="c51c7-430">Для объявления универсального типа, тип экземпляра формируется путем создания сконструированного типа ([создан типы](types.md#constructed-types)) из объявления типа, с каждым из указанного типа аргументов которого соответствующий параметр типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-430">For a generic class declaration, the instance type is formed by creating a constructed type ([Constructed types](types.md#constructed-types)) from the type declaration, with each of the supplied type arguments being the corresponding type parameter.</span></span> <span data-ttu-id="c51c7-431">Так как тип экземпляра использует параметры типа, он может использоваться только где параметров типа находятся в области действия; то есть внутри объявления класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-431">Since the instance type uses the type parameters, it can only be used where the type parameters are in scope; that is, inside the class declaration.</span></span> <span data-ttu-id="c51c7-432">Тип экземпляра является типом `this` для кода, написанного внутри объявления класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-432">The instance type is the type of `this` for code written inside the class declaration.</span></span> <span data-ttu-id="c51c7-433">Для неуниверсальных классов тип экземпляра является просто объявленный класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-433">For non-generic classes, the instance type is simply the declared class.</span></span> <span data-ttu-id="c51c7-434">Ниже представлено несколько объявлений класса вместе с их типами экземпляр:</span><span class="sxs-lookup"><span data-stu-id="c51c7-434">The following shows several class declarations along with their instance types:</span></span> 
```csharp
class A<T>                           // instance type: A<T>
{
    class B {}                       // instance type: A<T>.B
    class C<U> {}                    // instance type: A<T>.C<U>
}

class D {}                           // instance type: D
```

### <a name="members-of-constructed-types"></a><span data-ttu-id="c51c7-435">Членами сконструированные типы</span><span class="sxs-lookup"><span data-stu-id="c51c7-435">Members of constructed types</span></span>

<span data-ttu-id="c51c7-436">Члены Ненаследуемые сконструированного типа получаются путем замещения для каждого *параметр_типа* в объявлении члена, соответствующего *type_argument* сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-436">The non-inherited members of a constructed type are obtained by substituting, for each *type_parameter* in the member declaration, the corresponding *type_argument* of the constructed type.</span></span> <span data-ttu-id="c51c7-437">Процесс подстановки основан на семантическое значение объявлений типов и не является простым текстовым подстановки.</span><span class="sxs-lookup"><span data-stu-id="c51c7-437">The substitution process is based on the semantic meaning of type declarations, and is not simply textual substitution.</span></span>

<span data-ttu-id="c51c7-438">Например при объявлении универсального класса</span><span class="sxs-lookup"><span data-stu-id="c51c7-438">For example, given the generic class declaration</span></span>
```csharp
class Gen<T,U>
{
    public T[,] a;
    public void G(int i, T t, Gen<U,T> gt) {...}
    public U Prop { get {...} set {...} }
    public int H(double d) {...}
}
```
<span data-ttu-id="c51c7-439">сконструированный тип `Gen<int[],IComparable<string>>` имеет следующие члены:</span><span class="sxs-lookup"><span data-stu-id="c51c7-439">the constructed type `Gen<int[],IComparable<string>>` has the following members:</span></span>
```csharp
public int[,][] a;
public void G(int i, int[] t, Gen<IComparable<string>,int[]> gt) {...}
public IComparable<string> Prop { get {...} set {...} }
public int H(double d) {...}
```

<span data-ttu-id="c51c7-440">Тип члена `a` в объявлении универсального класса `Gen` является «двухмерный массив `T`«, поэтому тип члена `a` в сконструированном типе выше является «двухмерный массив одномерный массив `int`«, или `int[,][]`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-440">The type of the member `a` in the generic class declaration `Gen` is "two-dimensional array of `T`", so the type of the member `a` in the constructed type above is "two-dimensional array of one-dimensional array of `int`", or `int[,][]`.</span></span>

<span data-ttu-id="c51c7-441">В функции-члены экземпляра, тип `this` является тип экземпляра ([тип экземпляра](classes.md#the-instance-type)) в содержащем объявлении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-441">Within instance function members, the type of `this` is the instance type ([The instance type](classes.md#the-instance-type)) of the containing declaration.</span></span>

<span data-ttu-id="c51c7-442">Все члены универсального класса можно использовать параметры типа из включающего класса, либо непосредственно, либо в рамках сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-442">All members of a generic class can use type parameters from any enclosing class, either directly or as part of a constructed type.</span></span> <span data-ttu-id="c51c7-443">При закрытии конкретного сконструированного типа ([открытые и закрытые типы](types.md#open-and-closed-types)) используется во время выполнения, каждое использование параметра типа заменяется фактическим типом аргумент, предоставленный для сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-443">When a particular closed constructed type ([Open and closed types](types.md#open-and-closed-types)) is used at run-time, each use of a type parameter is replaced with the actual type argument supplied to the constructed type.</span></span> <span data-ttu-id="c51c7-444">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-444">For example:</span></span>
```csharp
class C<V>
{
    public V f1;
    public C<V> f2 = null;

    public C(V x) {
        this.f1 = x;
        this.f2 = this;
    }
}

class Application
{
    static void Main() {
        C<int> x1 = new C<int>(1);
        Console.WriteLine(x1.f1);        // Prints 1

        C<double> x2 = new C<double>(3.1415);
        Console.WriteLine(x2.f1);        // Prints 3.1415
    }
}
```

### <a name="inheritance"></a><span data-ttu-id="c51c7-445">Наследование</span><span class="sxs-lookup"><span data-stu-id="c51c7-445">Inheritance</span></span>

<span data-ttu-id="c51c7-446">Класс ***наследует*** члены типа его прямой базовый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-446">A class ***inherits*** the members of its direct base class type.</span></span> <span data-ttu-id="c51c7-447">Наследование означает, что класс неявно содержит все члены его прямой базовый класс типа, за исключением конструкторы экземпляров, деструкторы и статические конструкторы базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-447">Inheritance means that a class implicitly contains all members of its direct base class type, except for the instance constructors, destructors and static constructors of the base class.</span></span> <span data-ttu-id="c51c7-448">Ниже приведены некоторые важные аспекты наследования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-448">Some important aspects of inheritance are:</span></span>

*  <span data-ttu-id="c51c7-449">Наследование является транзитивным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-449">Inheritance is transitive.</span></span> <span data-ttu-id="c51c7-450">Если `C` является производным от `B`, и `B` является производным от `A`, затем `C` наследует члены, объявленные в `B` а также членов, объявленных в `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-450">If `C` is derived from `B`, and `B` is derived from `A`, then `C` inherits the members declared in `B` as well as the members declared in `A`.</span></span>
*  <span data-ttu-id="c51c7-451">Производный класс расширяет его непосредственный базовый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-451">A derived class extends its direct base class.</span></span> <span data-ttu-id="c51c7-452">Производный класс может дополнить наследуемые элементы новыми элементами, но он не может удалить определение для наследуемого члена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-452">A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.</span></span>
*  <span data-ttu-id="c51c7-453">Конструкторы экземпляров, деструкторы и статические конструкторы не наследуются, но все другие члены, независимо от их объявленный уровень доступности ([доступ к членам](basic-concepts.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-453">Instance constructors, destructors, and static constructors are not inherited, but all other members are, regardless of their declared accessibility ([Member access](basic-concepts.md#member-access)).</span></span> <span data-ttu-id="c51c7-454">Тем не менее в зависимости от их объявленный уровень доступности, унаследованные члены могут оказаться недоступными в производном классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-454">However, depending on their declared accessibility, inherited members might not be accessible in a derived class.</span></span>
*  <span data-ttu-id="c51c7-455">Производный класс может ***скрыть*** ([скрытие через наследование](basic-concepts.md#hiding-through-inheritance)) унаследованные члены путем объявления новых членов с тем же именем или сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-455">A derived class can ***hide*** ([Hiding through inheritance](basic-concepts.md#hiding-through-inheritance)) inherited members by declaring new members with the same name or signature.</span></span> <span data-ttu-id="c51c7-456">Обратите внимание на то, тем не менее, скрытие унаследованного члена не приводит к удалению этого элемента — просто становятся этот член недоступен напрямую с помощью производного класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-456">Note however that hiding an inherited member does not remove that member—it merely makes that member inaccessible directly through the derived class.</span></span>
*  <span data-ttu-id="c51c7-457">Экземпляр класса содержит набор всех полей экземпляра, объявленных в классе и его базовых классов и неявное преобразование ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)) существует тип производного класса на любой из типов соответствующего базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-457">An instance of a class contains a set of all instance fields declared in the class and its base classes, and an implicit conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from a derived class type to any of its base class types.</span></span> <span data-ttu-id="c51c7-458">Таким образом ссылку на экземпляр некоторого производного класса может рассматриваться как ссылку на экземпляр любого из его базовых классов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-458">Thus, a reference to an instance of some derived class can be treated as a reference to an instance of any of its base classes.</span></span>
*  <span data-ttu-id="c51c7-459">Класс может объявить виртуальные методы, свойства и индексаторы и производные классы могли переопределять реализацию этих функций-членов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-459">A class can declare virtual methods, properties, and indexers, and derived classes can override the implementation of these function members.</span></span> <span data-ttu-id="c51c7-460">Это позволяет классам реализовывать полиморфное поведение, при котором действиям, выполняемым с вызова функции-члена, зависит от типа времени выполнения экземпляра, через который вызывается функция-член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-460">This enables classes to exhibit polymorphic behavior wherein the actions performed by a function member invocation varies depending on the run-time type of the instance through which that function member is invoked.</span></span>

<span data-ttu-id="c51c7-461">Наследуемый член типа сконструированного класса являются членами типа непосредственный базовый класс ([базовые классы](classes.md#base-classes)), который обеспечивается путем замены аргументов типа сконструированного типа для каждого вхождения соответствующего типа параметры в *class_base* спецификации.</span><span class="sxs-lookup"><span data-stu-id="c51c7-461">The inherited member of a constructed class type are the members of the immediate base class type ([Base classes](classes.md#base-classes)), which is found by substituting the type arguments of the constructed type for each occurrence of the corresponding type parameters in the *class_base* specification.</span></span> <span data-ttu-id="c51c7-462">Эти элементы, в свою очередь, преобразование выполняется путем замены для каждого *параметр_типа* в объявлении члена, соответствующего *type_argument* из *class_base* Спецификация.</span><span class="sxs-lookup"><span data-stu-id="c51c7-462">These members, in turn, are transformed by substituting, for each *type_parameter* in the member declaration, the corresponding *type_argument* of the *class_base* specification.</span></span>

```csharp
class B<U>
{
    public U F(long index) {...}
}

class D<T>: B<T[]>
{
    public T G(string s) {...}
}
```

<span data-ttu-id="c51c7-463">В приведенном выше примере, сконструированного типа `D<int>` имеет член Ненаследуемые `public int G(string s)` получен путем замены аргумент типа `int` для параметра типа `T`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-463">In the above example, the constructed type `D<int>` has a non-inherited member `public int G(string s)` obtained by substituting the type argument `int` for the type parameter `T`.</span></span> <span data-ttu-id="c51c7-464">`D<int>` также имеет наследуемый член из объявления класса `B`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-464">`D<int>` also has an inherited member from the class declaration `B`.</span></span> <span data-ttu-id="c51c7-465">Этот унаследованный член определяется путем определения типа базового класса `B<int[]>` из `D<int>` , подставляя `int` для `T` в спецификации базового класса `B<T[]>`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-465">This inherited member is determined by first determining the base class type `B<int[]>` of `D<int>` by substituting `int` for `T` in the base class specification `B<T[]>`.</span></span> <span data-ttu-id="c51c7-466">А затем в качестве аргумента типа для `B`, `int[]` заменяется `U` в `public U F(long index)`, давая наследуемый член `public int[] F(long index)`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-466">Then, as a type argument to `B`, `int[]` is substituted for `U` in `public U F(long index)`, yielding the inherited member `public int[] F(long index)`.</span></span>

### <a name="the-new-modifier"></a><span data-ttu-id="c51c7-467">Модификатор new</span><span class="sxs-lookup"><span data-stu-id="c51c7-467">The new modifier</span></span>

<span data-ttu-id="c51c7-468">Объект *class_member_declaration* может объявить элемент с тем же именем или сигнатурой, наследуемого члена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-468">A *class_member_declaration* is permitted to declare a member with the same name or signature as an inherited member.</span></span> <span data-ttu-id="c51c7-469">Если в этом случае члена производного класса называется ***скрыть*** член базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-469">When this occurs, the derived class member is said to ***hide*** the base class member.</span></span> <span data-ttu-id="c51c7-470">Скрытие унаследованного члена не считается ошибкой, но он приводит к компилятор выдаст предупреждение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-470">Hiding an inherited member is not considered an error, but it does cause the compiler to issue a warning.</span></span> <span data-ttu-id="c51c7-471">Чтобы подавить предупреждение, можно включить объявление члена производного класса `new` модификатор, чтобы указать, что производный член должен скрыть базовый член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-471">To suppress the warning, the declaration of the derived class member can include a `new` modifier to indicate that the derived member is intended to hide the base member.</span></span> <span data-ttu-id="c51c7-472">Эта тема будет рассматриваться далее в [скрытие через наследование](basic-concepts.md#hiding-through-inheritance).</span><span class="sxs-lookup"><span data-stu-id="c51c7-472">This topic is discussed further in [Hiding through inheritance](basic-concepts.md#hiding-through-inheritance).</span></span>

<span data-ttu-id="c51c7-473">Если `new` модификатор включен в объявление, которое не скрывает унаследованный член, соответствующее предупреждение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-473">If a `new` modifier is included in a declaration that doesn't hide an inherited member, a warning to that effect is issued.</span></span> <span data-ttu-id="c51c7-474">Это предупреждение можно отключить путем удаления `new` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-474">This warning is suppressed by removing the `new` modifier.</span></span>

### <a name="access-modifiers"></a><span data-ttu-id="c51c7-475">Модификаторы доступа</span><span class="sxs-lookup"><span data-stu-id="c51c7-475">Access modifiers</span></span>

<span data-ttu-id="c51c7-476">Объект *class_member_declaration* может иметь одно из пяти возможных типов объявленный уровень доступности ([объявленную доступность](basic-concepts.md#declared-accessibility)): `public`, `protected internal`, `protected`, `internal` , или `private`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-476">A *class_member_declaration* can have any one of the five possible kinds of declared accessibility ([Declared accessibility](basic-concepts.md#declared-accessibility)): `public`, `protected internal`, `protected`, `internal`, or `private`.</span></span> <span data-ttu-id="c51c7-477">За исключением `protected internal` сочетания, это ошибка времени компиляции, чтобы указать несколько модификаторов доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-477">Except for the `protected internal` combination, it is a compile-time error to specify more than one access modifier.</span></span> <span data-ttu-id="c51c7-478">Когда *class_member_declaration* не поддерживает модификаторы доступа `private` предполагается, что.</span><span class="sxs-lookup"><span data-stu-id="c51c7-478">When a *class_member_declaration* does not include any access modifiers, `private` is assumed.</span></span>

### <a name="constituent-types"></a><span data-ttu-id="c51c7-479">Составные типы</span><span class="sxs-lookup"><span data-stu-id="c51c7-479">Constituent types</span></span>

<span data-ttu-id="c51c7-480">Типы, используемые в объявлении члена, называются составные типы этого члена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-480">Types that are used in the declaration of a member are called the constituent types of that member.</span></span> <span data-ttu-id="c51c7-481">Возможные типы составных: тип константы, поля, свойства, события или индексатора, тип возвращаемого значения метода или оператора и типы параметров метода, индексатора, оператор или конструктор экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-481">Possible constituent types are the type of a constant, field, property, event, or indexer, the return type of a method or operator, and the parameter types of a method, indexer, operator, or instance constructor.</span></span> <span data-ttu-id="c51c7-482">Составные типы член должен быть по крайней мере такой же уровень доступности, чем сам член ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-482">The constituent types of a member must be at least as accessible as that member itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

### <a name="static-and-instance-members"></a><span data-ttu-id="c51c7-483">Экземпляра и статические члены</span><span class="sxs-lookup"><span data-stu-id="c51c7-483">Static and instance members</span></span>

<span data-ttu-id="c51c7-484">Члены класса являются либо ***статические члены*** или ***члены экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-484">Members of a class are either ***static members*** or ***instance members***.</span></span> <span data-ttu-id="c51c7-485">Вообще говоря это можно представить статические члены принадлежат к типам классов и члены экземпляра принадлежат к объектам (экземпляры типов классов).</span><span class="sxs-lookup"><span data-stu-id="c51c7-485">Generally speaking, it is useful to think of static members as belonging to class types and instance members as belonging to objects (instances of class types).</span></span>

<span data-ttu-id="c51c7-486">Если объявление поля, метода, свойства, события, оператора или конструктора содержит `static` модификатор, он объявляет статический член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-486">When a field, method, property, event, operator, or constructor declaration includes a `static` modifier, it declares a static member.</span></span> <span data-ttu-id="c51c7-487">Кроме того объявление константы или типа неявно объявляет статический член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-487">In addition, a constant or type declaration implicitly declares a static member.</span></span> <span data-ttu-id="c51c7-488">Статические члены имеют следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="c51c7-488">Static members have the following characteristics:</span></span>

*  <span data-ttu-id="c51c7-489">Когда статический член `M` указывается в *member_access* ([доступ к членам](expressions.md#member-access)) формы `E.M`, `E` необходимо обозначить тип, содержащий `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-489">When a static member `M` is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, `E` must denote a type containing `M`.</span></span> <span data-ttu-id="c51c7-490">Произошла ошибка во время компиляции для `E` для обозначения экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-490">It is a compile-time error for `E` to denote an instance.</span></span>
*  <span data-ttu-id="c51c7-491">Статическое поле определяет строго одно место хранения для совместного использования все вхождения заданного закрытого типа класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-491">A static field identifies exactly one storage location to be shared by all instances of a given closed class type.</span></span> <span data-ttu-id="c51c7-492">Независимо от того, сколько экземпляров заданного закрытого типа класса создаются имеется только одна копия статического поля.</span><span class="sxs-lookup"><span data-stu-id="c51c7-492">No matter how many instances of a given closed class type are created, there is only ever one copy of a static field.</span></span>
*  <span data-ttu-id="c51c7-493">Статические функции-члена (метода, свойства, события, оператор или конструктор) не работает в определенном экземпляре, и это ошибка времени компиляции для ссылки на `this` в такой функции-члена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-493">A static function member (method, property, event, operator, or constructor) does not operate on a specific instance, and it is a compile-time error to refer to `this` in such a function member.</span></span>

<span data-ttu-id="c51c7-494">Если объявление поля, метода, свойства, события, индексатора, конструктор или деструктор не содержит `static` модификатор, объявляет член экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-494">When a field, method, property, event, indexer, constructor, or destructor declaration does not include a `static` modifier, it declares an instance member.</span></span> <span data-ttu-id="c51c7-495">(Член экземпляра иногда называется нестатический член). Члены экземпляра имеют следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="c51c7-495">(An instance member is sometimes called a non-static member.) Instance members have the following characteristics:</span></span>

*  <span data-ttu-id="c51c7-496">Если член экземпляра `M` указывается в *member_access* ([доступ к членам](expressions.md#member-access)) формы `E.M`, `E` должно означать экземпляр типа, содержащее `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-496">When an instance member `M` is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, `E` must denote an instance of a type containing `M`.</span></span> <span data-ttu-id="c51c7-497">Произошла ошибка во время привязки для `E` для обозначения типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-497">It is a binding-time error for `E` to denote a type.</span></span>
*  <span data-ttu-id="c51c7-498">Каждый экземпляр класса содержит отдельный набор всех полей экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-498">Every instance of a class contains a separate set of all instance fields of the class.</span></span>
*  <span data-ttu-id="c51c7-499">Функцией-членом экземпляра (метод, свойство, индексатор, конструктор экземпляра или деструктор) работает на данном экземпляре класса, и этот экземпляр может быть доступен как `this` ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-499">An instance function member (method, property, indexer, instance constructor, or destructor) operates on a given instance of the class, and this instance can be accessed as `this` ([This access](expressions.md#this-access)).</span></span>

<span data-ttu-id="c51c7-500">Правила доступа к статическим и члены экземпляра в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="c51c7-500">The following example illustrates the rules for accessing static and instance members:</span></span>
```csharp
class Test
{
    int x;
    static int y;

    void F() {
        x = 1;            // Ok, same as this.x = 1
        y = 1;            // Ok, same as Test.y = 1
    }

    static void G() {
        x = 1;            // Error, cannot access this.x
        y = 1;            // Ok, same as Test.y = 1
    }

    static void Main() {
        Test t = new Test();
        t.x = 1;          // Ok
        t.y = 1;          // Error, cannot access static member through instance
        Test.x = 1;       // Error, cannot access instance member through type
        Test.y = 1;       // Ok
    }
}
```

<span data-ttu-id="c51c7-501">`F` Метод показывает, что в функции-члене экземпляра, *simple_name* ([простые имена](expressions.md#simple-names)) может использоваться для доступа к членам экземпляра и статические члены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-501">The `F` method shows that in an instance function member, a *simple_name* ([Simple names](expressions.md#simple-names)) can be used to access both instance members and static members.</span></span> <span data-ttu-id="c51c7-502">`G` Метод видно, что в статической функцией-членом, ошибка времени компиляции для доступа к члену экземпляра через *simple_name*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-502">The `G` method shows that in a static function member, it is a compile-time error to access an instance member through a *simple_name*.</span></span> <span data-ttu-id="c51c7-503">`Main` Метод показывает, что в *member_access* ([доступ к членам](expressions.md#member-access)), члены экземпляра должен осуществляться через экземпляров и статические члены должны осуществляться через типы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-503">The `Main` method shows that in a *member_access* ([Member access](expressions.md#member-access)), instance members must be accessed through instances, and static members must be accessed through types.</span></span>

### <a name="nested-types"></a><span data-ttu-id="c51c7-504">Вложенные типы</span><span class="sxs-lookup"><span data-stu-id="c51c7-504">Nested types</span></span>

<span data-ttu-id="c51c7-505">Вызов метода типа, объявленные в объявлении класса или структуры ***вложенный тип***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-505">A type declared within a class or struct declaration is called a ***nested type***.</span></span> <span data-ttu-id="c51c7-506">Тип, объявленный в блоке компиляции или пространстве имен, называется ***невложенными тип***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-506">A type that is declared within a compilation unit or namespace is called a ***non-nested type***.</span></span>

<span data-ttu-id="c51c7-507">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-507">In the example</span></span>
```csharp
using System;

class A
{
    class B
    {
        static void F() {
            Console.WriteLine("A.B.F");
        }
    }
}
```
<span data-ttu-id="c51c7-508">Класс `B` является вложенным типом, поскольку он объявлен внутри класса `A`и класс `A` является типом, невложенными, поскольку он объявлен в единице компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-508">class `B` is a nested type because it is declared within class `A`, and class `A` is a non-nested type because it is declared within a compilation unit.</span></span>

#### <a name="fully-qualified-name"></a><span data-ttu-id="c51c7-509">Полное имя</span><span class="sxs-lookup"><span data-stu-id="c51c7-509">Fully qualified name</span></span>

<span data-ttu-id="c51c7-510">Полное доменное имя ([полные имена](basic-concepts.md#fully-qualified-names)) является вложенным типом `S.N` где `S` полное имя типа в тип `N` объявлен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-510">The fully qualified name ([Fully qualified names](basic-concepts.md#fully-qualified-names)) for a nested type is `S.N` where `S` is the fully qualified name of the type in which type `N` is declared.</span></span>

#### <a name="declared-accessibility"></a><span data-ttu-id="c51c7-511">Объявленная доступность</span><span class="sxs-lookup"><span data-stu-id="c51c7-511">Declared accessibility</span></span>

<span data-ttu-id="c51c7-512">Не вложенные типы могут иметь `public` или `internal` объявленную доступность и иметь `internal` объявленную доступность по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-512">Non-nested types can have `public` or `internal` declared accessibility and have `internal` declared accessibility by default.</span></span> <span data-ttu-id="c51c7-513">Вложенные типы могут иметь эти формы объявленный уровень доступности, плюс один или несколько видов объявленный уровень доступности, в зависимости от того, является ли вмещающий тип класса или структуры:</span><span class="sxs-lookup"><span data-stu-id="c51c7-513">Nested types can have these forms of declared accessibility too, plus one or more additional forms of declared accessibility, depending on whether the containing type is a class or struct:</span></span>

*  <span data-ttu-id="c51c7-514">Вложенный тип, который объявлен в классе могут содержать любой из пяти форм объявленный уровень доступности (`public`, `protected internal`, `protected`, `internal`, или `private`) и, как и другие члены класса, по умолчанию `private` объявлен специальные возможности.</span><span class="sxs-lookup"><span data-stu-id="c51c7-514">A nested type that is declared in a class can have any of five forms of declared accessibility (`public`, `protected internal`, `protected`, `internal`, or `private`) and, like other class members, defaults to `private` declared accessibility.</span></span>
*  <span data-ttu-id="c51c7-515">Вложенный тип, который объявлен в структуре могут содержать любой из трех видов объявленный уровень доступности (`public`, `internal`, или `private`) и, как и другие члены структуры, по умолчанию `private` объявленную доступность.</span><span class="sxs-lookup"><span data-stu-id="c51c7-515">A nested type that is declared in a struct can have any of three forms of declared accessibility (`public`, `internal`, or `private`) and, like other struct members, defaults to `private` declared accessibility.</span></span>

<span data-ttu-id="c51c7-516">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-516">The example</span></span>
```csharp
public class List
{
    // Private data structure
    private class Node
    { 
        public object Data;
        public Node Next;

        public Node(object data, Node next) {
            this.Data = data;
            this.Next = next;
        }
    }

    private Node first = null;
    private Node last = null;

    // Public interface
    public void AddToFront(object o) {...}
    public void AddToBack(object o) {...}
    public object RemoveFromFront() {...}
    public object RemoveFromBack() {...}
    public int Count { get {...} }
}
```
<span data-ttu-id="c51c7-517">Объявляет закрытым вложенным классом `Node`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-517">declares a private nested class `Node`.</span></span>

#### <a name="hiding"></a><span data-ttu-id="c51c7-518">Скрытие</span><span class="sxs-lookup"><span data-stu-id="c51c7-518">Hiding</span></span>

<span data-ttu-id="c51c7-519">Вложенный тип может быть скрыта ([Сокрытие имен](basic-concepts.md#name-hiding)) базовый член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-519">A nested type may hide ([Name hiding](basic-concepts.md#name-hiding)) a base member.</span></span> <span data-ttu-id="c51c7-520">`new` Модификатор может применяться в объявлениях вложенных типов, таким образом, чтобы скрытие можно выразить явно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-520">The `new` modifier is permitted on nested type declarations so that hiding can be expressed explicitly.</span></span> <span data-ttu-id="c51c7-521">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-521">The example</span></span>
```csharp
using System;

class Base
{
    public static void M() {
        Console.WriteLine("Base.M");
    }
}

class Derived: Base 
{
    new public class M 
    {
        public static void F() {
            Console.WriteLine("Derived.M.F");
        }
    }
}

class Test 
{
    static void Main() {
        Derived.M.F();
    }
}
```
<span data-ttu-id="c51c7-522">Показывает вложенный класс `M` , скрывает метод `M` определенные в `Base`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-522">shows a nested class `M` that hides the method `M` defined in `Base`.</span></span>

#### <a name="this-access"></a><span data-ttu-id="c51c7-523">Такой доступ</span><span class="sxs-lookup"><span data-stu-id="c51c7-523">this access</span></span>

<span data-ttu-id="c51c7-524">Вложенный тип и его содержащий тип имеют особая связь относится к *this_access* ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-524">A nested type and its containing type do not have a special relationship with regard to *this_access* ([This access](expressions.md#this-access)).</span></span> <span data-ttu-id="c51c7-525">В частности `this` изнутри вложенного типа не может использоваться для обращения к членам экземпляра содержащего типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-525">Specifically, `this` within a nested type cannot be used to refer to instance members of the containing type.</span></span> <span data-ttu-id="c51c7-526">В случаях, где вложенный тип требуется доступ к членам экземпляра его содержащего типа, будет предоставлен доступ, предоставляя `this` для экземпляра типа, содержащего аргумента конструктора для вложенного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-526">In cases where a nested type needs access to the instance members of its containing type, access can be provided by providing the `this` for the instance of the containing type as a constructor argument for the nested type.</span></span> <span data-ttu-id="c51c7-527">Следующий пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-527">The following example</span></span>
```csharp
using System;

class C
{
    int i = 123;

    public void F() {
        Nested n = new Nested(this);
        n.G();
    }

    public class Nested
    {
        C this_c;

        public Nested(C c) {
            this_c = c;
        }

        public void G() {
            Console.WriteLine(this_c.i);
        }
    }
}

class Test
{
    static void Main() {
        C c = new C();
        c.F();
    }
}
```
<span data-ttu-id="c51c7-528">показан этот способ.</span><span class="sxs-lookup"><span data-stu-id="c51c7-528">shows this technique.</span></span> <span data-ttu-id="c51c7-529">Экземпляр `C` создает экземпляр класса `Nested` и передает свой собственный `this` для `Nested`в конструктор, чтобы предоставить последующий доступ к `C`его члены экземпляров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-529">An instance of `C` creates an instance of `Nested` and passes its own `this` to `Nested`'s constructor in order to provide subsequent access to `C`'s instance members.</span></span>

#### <a name="access-to-private-and-protected-members-of-the-containing-type"></a><span data-ttu-id="c51c7-530">Доступ к закрытым и защищенным членам содержащего типа</span><span class="sxs-lookup"><span data-stu-id="c51c7-530">Access to private and protected members of the containing type</span></span>

<span data-ttu-id="c51c7-531">Вложенный тип имеет доступ ко всем членов, которые доступны вмещающему типу, включая элементы содержащего его типа, имеющие `private` и `protected` объявленную доступность.</span><span class="sxs-lookup"><span data-stu-id="c51c7-531">A nested type has access to all of the members that are accessible to its containing type, including members of the containing type that have `private` and `protected` declared accessibility.</span></span> <span data-ttu-id="c51c7-532">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-532">The example</span></span>
```csharp
using System;

class C 
{
    private static void F() {
        Console.WriteLine("C.F");
    }

    public class Nested 
    {
        public static void G() {
            F();
        }
    }
}

class Test 
{
    static void Main() {
        C.Nested.G();
    }
}
```
<span data-ttu-id="c51c7-533">показан класс `C` , содержащий вложенный класс `Nested`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-533">shows a class `C` that contains a nested class `Nested`.</span></span> <span data-ttu-id="c51c7-534">В рамках `Nested`, метод `G` вызывает статический метод `F` определенные в `C`, и `F` private объявило специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-534">Within `Nested`, the method `G` calls the static method `F` defined in `C`, and `F` has private declared accessibility.</span></span>

<span data-ttu-id="c51c7-535">Вложенный тип также может получить доступ к защищенные члены, определенные в базовом типе его содержащего типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-535">A nested type also may access protected members defined in a base type of its containing type.</span></span> <span data-ttu-id="c51c7-536">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-536">In the example</span></span>
```csharp
using System;

class Base 
{
    protected void F() {
        Console.WriteLine("Base.F");
    }
}

class Derived: Base 
{
    public class Nested 
    {
        public void G() {
            Derived d = new Derived();
            d.F();        // ok
        }
    }
}

class Test 
{
    static void Main() {
        Derived.Nested n = new Derived.Nested();
        n.G();
    }
}
```
<span data-ttu-id="c51c7-537">вложенный класс `Derived.Nested` обращается к защищенный метод `F` определенные в `Derived`его базового класса, `Base`, по через экземпляр `Derived`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-537">the nested class `Derived.Nested` accesses the protected method `F` defined in `Derived`'s base class, `Base`, by calling through an instance of `Derived`.</span></span>

#### <a name="nested-types-in-generic-classes"></a><span data-ttu-id="c51c7-538">Вложенные типы в универсальных классах</span><span class="sxs-lookup"><span data-stu-id="c51c7-538">Nested types in generic classes</span></span>

<span data-ttu-id="c51c7-539">Объявление универсального класса может содержать объявления вложенных типов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-539">A generic class declaration can contain nested type declarations.</span></span> <span data-ttu-id="c51c7-540">Параметры типа включающего класса можно использовать внутри вложенных типов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-540">The type parameters of the enclosing class can be used within the nested types.</span></span> <span data-ttu-id="c51c7-541">Объявление вложенного типа может содержать дополнительные параметры типа, которые применяются только к вложенного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-541">A nested type declaration can contain additional type parameters that apply only to the nested type.</span></span>

<span data-ttu-id="c51c7-542">Каждое объявление типа, содержащихся в универсальном объявлении класса неявно является объявлением универсального типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-542">Every type declaration contained within a generic class declaration is implicitly a generic type declaration.</span></span> <span data-ttu-id="c51c7-543">При записи ссылки на тип вложенным в универсальный тип, сформированный тип, включая его аргументы типа должны быть именованными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-543">When writing a reference to a type nested within a generic type, the containing constructed type, including its type arguments, must be named.</span></span> <span data-ttu-id="c51c7-544">Тем не менее с внутри внешнего класса, вложенный тип может использоваться без уточнения; Тип экземпляра внешнего класса неявно используется при создании вложенного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-544">However, from within the outer class, the nested type can be used without qualification; the instance type of the outer class can be implicitly used when constructing the nested type.</span></span> <span data-ttu-id="c51c7-545">В следующем примере показано три разных правильных способа для ссылки на сконструированный тип, созданный из `Inner`; первые два эквивалентны:</span><span class="sxs-lookup"><span data-stu-id="c51c7-545">The following example shows three different correct ways to refer to a constructed type created from `Inner`; the first two are equivalent:</span></span>
```csharp
class Outer<T>
{
    class Inner<U>
    {
        public static void F(T t, U u) {...}
    }

    static void F(T t) {
        Outer<T>.Inner<string>.F(t, "abc");      // These two statements have
        Inner<string>.F(t, "abc");               // the same effect

        Outer<int>.Inner<string>.F(3, "abc");    // This type is different

        Outer.Inner<string>.F(t, "abc");         // Error, Outer needs type arg
    }
}
```

<span data-ttu-id="c51c7-546">Несмотря на то, что это плохо стиль программирования, параметр типа во вложенном типе можно скрыть член или параметр типа, объявленный во внешнем типе:</span><span class="sxs-lookup"><span data-stu-id="c51c7-546">Although it is bad programming style, a type parameter in a nested type can hide a member or type parameter declared in the outer type:</span></span>
```csharp
class Outer<T>
{
    class Inner<T>        // Valid, hides Outer's T
    {
        public T t;       // Refers to Inner's T
    }
}
```

### <a name="reserved-member-names"></a><span data-ttu-id="c51c7-547">Зарезервированные имена членов</span><span class="sxs-lookup"><span data-stu-id="c51c7-547">Reserved member names</span></span>

<span data-ttu-id="c51c7-548">Для упрощения базовой реализации C# во время выполнения, для каждого объявления члена источника, это свойство, событие или индексатора, реализации необходимо зарезервировать два сигнатуры методов в зависимости от типа в объявлении члена, его имя и его тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-548">To facilitate the underlying C# run-time implementation, for each source member declaration that is a property, event, or indexer, the implementation must reserve two method signatures based on the kind of the member declaration, its name, and its type.</span></span> <span data-ttu-id="c51c7-549">Произошла ошибка во время компиляции, для программы для объявления член, сигнатура которого совпадает с одним из этих зарезервированных сигнатур, даже если не вносит в базовой реализации среды выполнения использует эти резервирования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-549">It is a compile-time error for a program to declare a member whose signature matches one of these reserved signatures, even if the underlying run-time implementation does not make use of these reservations.</span></span>

<span data-ttu-id="c51c7-550">Зарезервированные имена не вводят объявления, поэтому они не участвуют в поиске элемента.</span><span class="sxs-lookup"><span data-stu-id="c51c7-550">The reserved names do not introduce declarations, thus they do not participate in member lookup.</span></span> <span data-ttu-id="c51c7-551">Тем не менее, связанные с объявлением зарезервированного метод подписи участвуют в наследовании ([наследования](classes.md#inheritance)) и могут быть скрыты с помощью `new` модификатор ([Модификатор new](classes.md#the-new-modifier)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-551">However, a declaration's associated reserved method signatures do participate in inheritance ([Inheritance](classes.md#inheritance)), and can be hidden with the `new` modifier ([The new modifier](classes.md#the-new-modifier)).</span></span>

<span data-ttu-id="c51c7-552">Резервирование этих имен служит трем целям:</span><span class="sxs-lookup"><span data-stu-id="c51c7-552">The reservation of these names serves three purposes:</span></span>

*  <span data-ttu-id="c51c7-553">Чтобы разрешить базовой реализации использовать обычный идентификатор в качестве имени метода для получения или установки доступа к средствам языка C#.</span><span class="sxs-lookup"><span data-stu-id="c51c7-553">To allow the underlying implementation to use an ordinary identifier as a method name for get or set access to the C# language feature.</span></span>
*  <span data-ttu-id="c51c7-554">Чтобы разрешить другие языки, для взаимодействия, используя обычный идентификатор в качестве имени метода для получения или задания доступа к средствам языка C#.</span><span class="sxs-lookup"><span data-stu-id="c51c7-554">To allow other languages to interoperate using an ordinary identifier as a method name for get or set access to the C# language feature.</span></span>
*  <span data-ttu-id="c51c7-555">Чтобы убедиться, что источник принятые одним соответствующим компилятором принимается на другое, сделав особенности зарезервированных элемента имена согласованность во всех реализациях C#.</span><span class="sxs-lookup"><span data-stu-id="c51c7-555">To help ensure that the source accepted by one conforming compiler is accepted by another, by making the specifics of reserved member names consistent across all C# implementations.</span></span>

<span data-ttu-id="c51c7-556">Объявление деструктора ([деструкторы](classes.md#destructors)) также приводит к сигнатуре резервируемые ([имена членов, зарезервированные для деструкторов](classes.md#member-names-reserved-for-destructors)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-556">The declaration of a destructor ([Destructors](classes.md#destructors)) also causes a signature to be reserved ([Member names reserved for destructors](classes.md#member-names-reserved-for-destructors)).</span></span>

#### <a name="member-names-reserved-for-properties"></a><span data-ttu-id="c51c7-557">Имена членов, зарезервированные для свойств</span><span class="sxs-lookup"><span data-stu-id="c51c7-557">Member names reserved for properties</span></span>

<span data-ttu-id="c51c7-558">Для свойства `P` ([свойства](classes.md#properties)) типа `T`, зарезервированы следующие сигнатуры:</span><span class="sxs-lookup"><span data-stu-id="c51c7-558">For a property `P` ([Properties](classes.md#properties)) of type `T`, the following signatures are reserved:</span></span>

```csharp
T get_P();
void set_P(T value);
```

<span data-ttu-id="c51c7-559">Зарезервированы обе сигнатуры, даже если свойство доступно только для чтения или только для записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-559">Both signatures are reserved, even if the property is read-only or write-only.</span></span>

<span data-ttu-id="c51c7-560">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-560">In the example</span></span>
```csharp
using System;

class A
{
    public int P {
        get { return 123; }
    }
}

class B: A
{
    new public int get_P() {
        return 456;
    }

    new public void set_P(int value) {
    }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        Console.WriteLine(a.P);
        Console.WriteLine(b.P);
        Console.WriteLine(b.get_P());
    }
}
```
<span data-ttu-id="c51c7-561">Класс `A` определяет свойство только для чтения `P`, резервируя тем самым подписи для `get_P` и `set_P` методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-561">a class `A` defines a read-only property `P`, thus reserving signatures for `get_P` and `set_P` methods.</span></span> <span data-ttu-id="c51c7-562">Класс `B` является производным от `A` и скрывает обе эти зарезервированные сигнатуры.</span><span class="sxs-lookup"><span data-stu-id="c51c7-562">A class `B` derives from `A` and hides both of these reserved signatures.</span></span> <span data-ttu-id="c51c7-563">В примере получался результат:</span><span class="sxs-lookup"><span data-stu-id="c51c7-563">The example produces the output:</span></span>
```
123
123
456
```

#### <a name="member-names-reserved-for-events"></a><span data-ttu-id="c51c7-564">Имена членов, зарезервированные для событий</span><span class="sxs-lookup"><span data-stu-id="c51c7-564">Member names reserved for events</span></span>

<span data-ttu-id="c51c7-565">Для события `E` ([события](classes.md#events)) типа делегата `T`, зарезервированы следующие сигнатуры:</span><span class="sxs-lookup"><span data-stu-id="c51c7-565">For an event `E` ([Events](classes.md#events)) of delegate type `T`, the following signatures are reserved:</span></span>
```csharp
void add_E(T handler);
void remove_E(T handler);
```

#### <a name="member-names-reserved-for-indexers"></a><span data-ttu-id="c51c7-566">Имена членов, зарезервированные для индексаторов</span><span class="sxs-lookup"><span data-stu-id="c51c7-566">Member names reserved for indexers</span></span>

<span data-ttu-id="c51c7-567">Для индексатора ([индексаторы](classes.md#indexers)) типа `T` со списком параметров `L`, зарезервированы следующие сигнатуры:</span><span class="sxs-lookup"><span data-stu-id="c51c7-567">For an indexer ([Indexers](classes.md#indexers)) of type `T` with parameter-list `L`, the following signatures are reserved:</span></span>
```csharp
T get_Item(L);
void set_Item(L, T value);
```

<span data-ttu-id="c51c7-568">Зарезервированы обе сигнатуры, даже если индексатор доступен только для чтения или только для записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-568">Both signatures are reserved, even if the indexer is read-only or write-only.</span></span>

<span data-ttu-id="c51c7-569">Кроме того имя члена `Item` зарезервирован.</span><span class="sxs-lookup"><span data-stu-id="c51c7-569">Furthermore the member name `Item` is reserved.</span></span>

#### <a name="member-names-reserved-for-destructors"></a><span data-ttu-id="c51c7-570">Имена членов, зарезервированные для деструкторов</span><span class="sxs-lookup"><span data-stu-id="c51c7-570">Member names reserved for destructors</span></span>

<span data-ttu-id="c51c7-571">Для класса с деструктором ([деструкторы](classes.md#destructors)), зарезервирован следующую сигнатуру:</span><span class="sxs-lookup"><span data-stu-id="c51c7-571">For a class containing a destructor ([Destructors](classes.md#destructors)), the following signature is reserved:</span></span>
```csharp
void Finalize();
```

## <a name="constants"></a><span data-ttu-id="c51c7-572">Константы</span><span class="sxs-lookup"><span data-stu-id="c51c7-572">Constants</span></span>

<span data-ttu-id="c51c7-573">Объект ***константы*** является членом класса, который представляет значение константы: значение, которое может быть вычислено во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-573">A ***constant*** is a class member that represents a constant value: a value that can be computed at compile-time.</span></span> <span data-ttu-id="c51c7-574">Объект *constant_declaration* представлены одной или нескольких констант данного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-574">A *constant_declaration* introduces one or more constants of a given type.</span></span>

```antlr
constant_declaration
    : attributes? constant_modifier* 'const' type constant_declarators ';'
    ;

constant_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;

constant_declarators
    : constant_declarator (',' constant_declarator)*
    ;

constant_declarator
    : identifier '=' constant_expression
    ;
```

<span data-ttu-id="c51c7-575">Объект *constant_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)), `new` модификатор ([Модификатор new](classes.md#the-new-modifier)), и является допустимой комбинацией четырех модификаторов доступа ([модификаторы доступа](classes.md#access-modifiers)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-575">A *constant_declaration* may include a set of *attributes* ([Attributes](attributes.md)), a `new` modifier ([The new modifier](classes.md#the-new-modifier)), and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)).</span></span> <span data-ttu-id="c51c7-576">Атрибуты и модификаторы применяются ко всем членам, объявленным с *constant_declaration*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-576">The attributes and modifiers apply to all of the members declared by the *constant_declaration*.</span></span> <span data-ttu-id="c51c7-577">Несмотря на то, что константы, считаются статические члены *constant_declaration* не требуется ни позволяет `static` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-577">Even though constants are considered static members, a *constant_declaration* neither requires nor allows a `static` modifier.</span></span> <span data-ttu-id="c51c7-578">Является ошибкой один и тот же модификатор встречается несколько раз в объявлении константы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-578">It is an error for the same modifier to appear multiple times in a constant declaration.</span></span>

<span data-ttu-id="c51c7-579">*Тип* из *constant_declaration* указывает тип членов, представленных в объявлении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-579">The *type* of a *constant_declaration* specifies the type of the members introduced by the declaration.</span></span> <span data-ttu-id="c51c7-580">Тип сопровождается список *constant_declarator*s, каждый из которых вводит новый член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-580">The type is followed by a list of *constant_declarator*s, each of which introduces a new member.</span></span> <span data-ttu-id="c51c7-581">Объект *constant_declarator* состоит из *идентификатор* , которая содержит название члена, за которым следует "`=`" токена, за которым следует *constant_expression* ([ Константные выражения](expressions.md#constant-expressions)), задающее значение члена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-581">A *constant_declarator* consists of an *identifier* that names the member, followed by an "`=`" token, followed by a *constant_expression* ([Constant expressions](expressions.md#constant-expressions)) that gives the value of the member.</span></span>

<span data-ttu-id="c51c7-582">*Тип* указан в константе объявление должно быть `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, `string`, *enum_type*, или *reference_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-582">The *type* specified in a constant declaration must be `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, `string`, an *enum_type*, or a *reference_type*.</span></span> <span data-ttu-id="c51c7-583">Каждый *constant_expression* должно выдавать значение целевого типа или типа, который может быть преобразован в целевой тип путем неявного преобразования ([неявные преобразования](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-583">Each *constant_expression* must yield a value of the target type or of a type that can be converted to the target type by an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>

<span data-ttu-id="c51c7-584">*Тип* константы должен быть по крайней мере такой же уровень доступности, как и сама константа ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-584">The *type* of a constant must be at least as accessible as the constant itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-585">Значение константы получается в выражение, использующее *simple_name* ([простые имена](expressions.md#simple-names)) или *member_access* ([доступ к членам](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-585">The value of a constant is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)).</span></span>

<span data-ttu-id="c51c7-586">Константа сама может участвовать в *constant_expression*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-586">A constant can itself participate in a *constant_expression*.</span></span> <span data-ttu-id="c51c7-587">Таким образом, можно использовать в любой конструкции, которая требует константа *constant_expression*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-587">Thus, a constant may be used in any construct that requires a *constant_expression*.</span></span> <span data-ttu-id="c51c7-588">Примеры таких конструкций `case` метки, `goto case` инструкций, `enum` объявления элементов, атрибутов и другие объявления констант.</span><span class="sxs-lookup"><span data-stu-id="c51c7-588">Examples of such constructs include `case` labels, `goto case` statements, `enum` member declarations, attributes, and other constant declarations.</span></span>

<span data-ttu-id="c51c7-589">Как описано в разделе [константные выражения](expressions.md#constant-expressions), *constant_expression* выражение, которое можно полностью вычислить во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-589">As described in [Constant expressions](expressions.md#constant-expressions), a *constant_expression* is an expression that can be fully evaluated at compile-time.</span></span> <span data-ttu-id="c51c7-590">Так как единственный способ создать отличное от null значение *reference_type* отличное от `string` заключается в применении `new` оператор и с момента `new` оператор является недопустимым в *constant_ выражение*, единственным возможным значением для констант *reference_type*s, отличных от `string` является `null`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-590">Since the only way to create a non-null value of a *reference_type* other than `string` is to apply the `new` operator, and since the `new` operator is not permitted in a *constant_expression*, the only possible value for constants of *reference_type*s other than `string` is `null`.</span></span>

<span data-ttu-id="c51c7-591">При необходимости символическое имя для значения константы, но когда тип этого значения не допускается в объявлении константы или если значение не может вычислить во время компиляции, *constant_expression*, `readonly` поле () [Поля только для чтения](classes.md#readonly-fields)) вместо него можно использовать.</span><span class="sxs-lookup"><span data-stu-id="c51c7-591">When a symbolic name for a constant value is desired, but when the type of that value is not permitted in a constant declaration, or when the value cannot be computed at compile-time by a *constant_expression*, a `readonly` field ([Readonly fields](classes.md#readonly-fields)) may be used instead.</span></span>

<span data-ttu-id="c51c7-592">Использовать в объявлении константы, объявляющее несколько констант соответствует несколько объявлений одиночных констант с атрибутами, модификаторы и тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-592">A constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same attributes, modifiers, and type.</span></span> <span data-ttu-id="c51c7-593">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-593">For example</span></span>
```csharp
class A
{
    public const double X = 1.0, Y = 2.0, Z = 3.0;
}
```
<span data-ttu-id="c51c7-594">эквивалентно</span><span class="sxs-lookup"><span data-stu-id="c51c7-594">is equivalent to</span></span>
```csharp
class A
{
    public const double X = 1.0;
    public const double Y = 2.0;
    public const double Z = 3.0;
}
```

<span data-ttu-id="c51c7-595">Константы могут зависеть другие константы в той же программе, до тех пор, пока зависимости не являются циклическими.</span><span class="sxs-lookup"><span data-stu-id="c51c7-595">Constants are permitted to depend on other constants within the same program as long as the dependencies are not of a circular nature.</span></span> <span data-ttu-id="c51c7-596">Компилятор автоматически располагает вычисления объявления констант в соответствующем порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-596">The compiler automatically arranges to evaluate the constant declarations in the appropriate order.</span></span> <span data-ttu-id="c51c7-597">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-597">In the example</span></span>
```csharp
class A
{
    public const int X = B.Z + 1;
    public const int Y = 10;
}

class B
{
    public const int Z = A.Y + 1;
}
```
<span data-ttu-id="c51c7-598">Во-первых, компилятор вычисляет `A.Y`, затем вычисляет `B.Z`и наконец оценивает `A.X`, создавая значения `10`, `11`, и `12`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-598">the compiler first evaluates `A.Y`, then evaluates `B.Z`, and finally evaluates `A.X`, producing the values `10`, `11`, and `12`.</span></span> <span data-ttu-id="c51c7-599">Объявления констант может зависеть от константы из других программ, но такие зависимости возможны только в одном направлении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-599">Constant declarations may depend on constants from other programs, but such dependencies are only possible in one direction.</span></span> <span data-ttu-id="c51c7-600">Задав в примере выше, в том случае, если `A` и `B` были объявлены в отдельных программ, можно было бы для `A.X` зависят от `B.Z`, но `B.Z` затем может одновременно не зависящие от `A.Y`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-600">Referring to the example above, if `A` and `B` were declared in separate programs, it would be possible for `A.X` to depend on `B.Z`, but `B.Z` could then not simultaneously depend on `A.Y`.</span></span>

## <a name="fields"></a><span data-ttu-id="c51c7-601">Поля</span><span class="sxs-lookup"><span data-stu-id="c51c7-601">Fields</span></span>

<span data-ttu-id="c51c7-602">Объект ***поле*** — это член, представляющий переменную, связанную с объектом или классом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-602">A ***field*** is a member that represents a variable associated with an object or class.</span></span> <span data-ttu-id="c51c7-603">Объект *field_declaration* представляет одно или несколько полей заданного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-603">A *field_declaration* introduces one or more fields of a given type.</span></span>

```antlr
field_declaration
    : attributes? field_modifier* type variable_declarators ';'
    ;

field_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'readonly'
    | 'volatile'
    | field_modifier_unsafe
    ;

variable_declarators
    : variable_declarator (',' variable_declarator)*
    ;

variable_declarator
    : identifier ('=' variable_initializer)?
    ;

variable_initializer
    : expression
    | array_initializer
    ;
```

<span data-ttu-id="c51c7-604">Объект *field_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)), `new` модификатор ([Модификатор new](classes.md#the-new-modifier)), допустимое сочетание из четырех модификаторов доступа ([модификаторы доступа](classes.md#access-modifiers)) и `static` модификатор ([экземпляра и статические поля](classes.md#static-and-instance-fields)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-604">A *field_declaration* may include a set of *attributes* ([Attributes](attributes.md)), a `new` modifier ([The new modifier](classes.md#the-new-modifier)), a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), and a `static` modifier ([Static and instance fields](classes.md#static-and-instance-fields)).</span></span> <span data-ttu-id="c51c7-605">Кроме того *field_declaration* может включать `readonly` модификатор ([поля только для чтения](classes.md#readonly-fields)) или `volatile` модификатор ([изменяемые поля](classes.md#volatile-fields)), но не оба.</span><span class="sxs-lookup"><span data-stu-id="c51c7-605">In addition, a *field_declaration* may include a `readonly` modifier ([Readonly fields](classes.md#readonly-fields)) or a `volatile` modifier ([Volatile fields](classes.md#volatile-fields)) but not both.</span></span> <span data-ttu-id="c51c7-606">Атрибуты и модификаторы применяются ко всем членам, объявленным с *field_declaration*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-606">The attributes and modifiers apply to all of the members declared by the *field_declaration*.</span></span> <span data-ttu-id="c51c7-607">Является ошибкой один и тот же модификатор встречается несколько раз в объявлении поля.</span><span class="sxs-lookup"><span data-stu-id="c51c7-607">It is an error for the same modifier to appear multiple times in a field declaration.</span></span>

<span data-ttu-id="c51c7-608">*Тип* из *field_declaration* указывает тип членов, представленных в объявлении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-608">The *type* of a *field_declaration* specifies the type of the members introduced by the declaration.</span></span> <span data-ttu-id="c51c7-609">Тип сопровождается список *variable_declarator*s, каждый из которых вводит новый член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-609">The type is followed by a list of *variable_declarator*s, each of which introduces a new member.</span></span> <span data-ttu-id="c51c7-610">Объект *variable_declarator* состоит из *идентификатор* , которая содержит название члена, за которыми необязательно следует "`=`" токена и *variable_initializer* ([ Инициализаторы переменных](classes.md#variable-initializers)), задающий начальное значение этого члена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-610">A *variable_declarator* consists of an *identifier* that names that member, optionally followed by an "`=`" token and a *variable_initializer* ([Variable initializers](classes.md#variable-initializers)) that gives the initial value of that member.</span></span>

<span data-ttu-id="c51c7-611">*Тип* поля должно быть по крайней мере такой же уровень доступности, как и само поле ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-611">The *type* of a field must be at least as accessible as the field itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-612">Получено значение поля в выражение, использующее *simple_name* ([простые имена](expressions.md#simple-names)) или *member_access* ([доступ к членам](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-612">The value of a field is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)).</span></span> <span data-ttu-id="c51c7-613">Значение поля не только для чтения, изменяется с помощью *назначения* ([операторы присваивания](expressions.md#assignment-operators)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-613">The value of a non-readonly field is modified using an *assignment* ([Assignment operators](expressions.md#assignment-operators)).</span></span> <span data-ttu-id="c51c7-614">Значение поля не только для чтения могут быть получены и изменены с помощью постфиксных инкремента и декремента ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators)) и префиксный инкремент и декремента ([префикс Операторы инкремента и декремента](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-614">The value of a non-readonly field can be both obtained and modified using postfix increment and decrement operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators)) and prefix increment and decrement operators ([Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span>

<span data-ttu-id="c51c7-615">Объявление поля, который объявляет несколько полей соответствует несколько объявлений из одного поля с атрибутами, модификаторы и тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-615">A field declaration that declares multiple fields is equivalent to multiple declarations of single fields with the same attributes, modifiers, and type.</span></span> <span data-ttu-id="c51c7-616">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-616">For example</span></span>
```csharp
class A
{
    public static int X = 1, Y, Z = 100;
}
```
<span data-ttu-id="c51c7-617">эквивалентно</span><span class="sxs-lookup"><span data-stu-id="c51c7-617">is equivalent to</span></span>
```csharp
class A
{
    public static int X = 1;
    public static int Y;
    public static int Z = 100;
}
```

### <a name="static-and-instance-fields"></a><span data-ttu-id="c51c7-618">Экземпляра и статические поля</span><span class="sxs-lookup"><span data-stu-id="c51c7-618">Static and instance fields</span></span>

<span data-ttu-id="c51c7-619">Если объявление поля содержит `static` модификатор, поля, представленные этим определением являются ***статические поля***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-619">When a field declaration includes a `static` modifier, the fields introduced by the declaration are ***static fields***.</span></span> <span data-ttu-id="c51c7-620">Если аргумент `static` модификатора, представленные этим определением поля являются ***полей экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-620">When no `static` modifier is present, the fields introduced by the declaration are ***instance fields***.</span></span> <span data-ttu-id="c51c7-621">Статические поля и поля экземпляра — это два из нескольких видов переменных ([переменных](variables.md)) поддерживается в C#, и в некоторых случаях они называются ***статические переменные*** и ***переменные экземпляра*** , соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-621">Static fields and instance fields are two of the several kinds of variables ([Variables](variables.md)) supported by C#, and at times they are referred to as ***static variables*** and ***instance variables***, respectively.</span></span>

<span data-ttu-id="c51c7-622">Статическое поле не является частью определенного экземпляра; Вместо этого он совместно используют все экземпляры закрытого типа ([открытые и закрытые типы](types.md#open-and-closed-types)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-622">A static field is not part of a specific instance; instead, it is shared amongst all instances of a closed type ([Open and closed types](types.md#open-and-closed-types)).</span></span> <span data-ttu-id="c51c7-623">Независимо от того, сколько экземпляров закрытого типа класса создаются имеется только одна копия статического поля для домена связанные приложения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-623">No matter how many instances of a closed class type are created, there is only ever one copy of a static field for the associated application domain.</span></span>

<span data-ttu-id="c51c7-624">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-624">For example:</span></span>
```csharp
class C<V>
{
    static int count = 0;

    public C() {
        count++;
    }

    public static int Count {
        get { return count; }
    }
}

class Application
{
    static void Main() {
        C<int> x1 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 1

        C<double> x2 = new C<double>();
        Console.WriteLine(C<int>.Count);        // Prints 1

        C<int> x3 = new C<int>();
        Console.WriteLine(C<int>.Count);        // Prints 2
    }
}
```

<span data-ttu-id="c51c7-625">Поле экземпляра принадлежит экземпляру.</span><span class="sxs-lookup"><span data-stu-id="c51c7-625">An instance field belongs to an instance.</span></span> <span data-ttu-id="c51c7-626">В частности каждый экземпляр класса содержит отдельный набор всех полей экземпляра этого класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-626">Specifically, every instance of a class contains a separate set of all the instance fields of that class.</span></span>

<span data-ttu-id="c51c7-627">Если ссылка на поле в *member_access* ([доступ к членам](expressions.md#member-access)) формы `E.M`, если `M` является статическим полем, `E` необходимо обозначить тип, содержащий `M` Если `M` является полем экземпляра E должно означать экземпляр типа, содержащего `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-627">When a field is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static field, `E` must denote a type containing `M`, and if `M` is an instance field, E must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="c51c7-628">Различия между статическими и члены экземпляра рассматриваются далее в [экземпляра и статические члены](classes.md#static-and-instance-members).</span><span class="sxs-lookup"><span data-stu-id="c51c7-628">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="readonly-fields"></a><span data-ttu-id="c51c7-629">Поля только для чтения</span><span class="sxs-lookup"><span data-stu-id="c51c7-629">Readonly fields</span></span>

<span data-ttu-id="c51c7-630">Когда *field_declaration* включает в себя `readonly` модификатор, поля, представленные этим определением являются ***поля только для чтения***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-630">When a *field_declaration* includes a `readonly` modifier, the fields introduced by the declaration are ***readonly fields***.</span></span> <span data-ttu-id="c51c7-631">Прямые назначения только для чтения полям может происходить только как часть этого объявления или в конструкторе экземпляра или статический конструктор, в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-631">Direct assignments to readonly fields can only occur as part of that declaration or in an instance constructor or static constructor in the same class.</span></span> <span data-ttu-id="c51c7-632">(Только для чтения поля могут быть назначены несколько раз в следующих контекстах.) В частности, прямые назначения для `readonly` поля разрешены только в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="c51c7-632">(A readonly field can be assigned to multiple times in these contexts.) Specifically, direct assignments to a `readonly` field are permitted only in the following contexts:</span></span>

*  <span data-ttu-id="c51c7-633">В *variable_declarator* , в которой вводятся поле (путем включения *variable_initializer* в объявлении).</span><span class="sxs-lookup"><span data-stu-id="c51c7-633">In the *variable_declarator* that introduces the field (by including a *variable_initializer* in the declaration).</span></span>
*  <span data-ttu-id="c51c7-634">Для поля экземпляра — в конструкторах экземпляров класса, содержащего объявление поля; для статического поля, в статическом конструкторе класса, содержащего объявление поля.</span><span class="sxs-lookup"><span data-stu-id="c51c7-634">For an instance field, in the instance constructors of the class that contains the field declaration; for a static field, in the static constructor of the class that contains the field declaration.</span></span> <span data-ttu-id="c51c7-635">Это единственно возможные контексты, в которых допускается передача `readonly` как `out` или `ref` параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-635">These are also the only contexts in which it is valid to pass a `readonly` field as an `out` or `ref` parameter.</span></span>

<span data-ttu-id="c51c7-636">Пытается присвоить `readonly` поле или передать в качестве `out` или `ref` в любом другом контексте является ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-636">Attempting to assign to a `readonly` field or pass it as an `out` or `ref` parameter in any other context is a compile-time error.</span></span>

#### <a name="using-static-readonly-fields-for-constants"></a><span data-ttu-id="c51c7-637">С помощью статических только для чтения поля для констант</span><span class="sxs-lookup"><span data-stu-id="c51c7-637">Using static readonly fields for constants</span></span>

<span data-ttu-id="c51c7-638">Объект `static readonly` поле используется, когда требуется символическое имя для значения константы, но когда тип значения не допускается в `const` объявление, или если значение не может вычислить во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-638">A `static readonly` field is useful when a symbolic name for a constant value is desired, but when the type of the value is not permitted in a `const` declaration, or when the value cannot be computed at compile-time.</span></span> <span data-ttu-id="c51c7-639">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-639">In the example</span></span>
```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);

    private byte red, green, blue;

    public Color(byte r, byte g, byte b) {
        red = r;
        green = g;
        blue = b;
    }
}
```
<span data-ttu-id="c51c7-640">`Black`, `White`, `Red`, `Green`, и `Blue` члены не могут объявляться как `const` членов так, как их значения не может быть вычислено во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-640">the `Black`, `White`, `Red`, `Green`, and `Blue` members cannot be declared as `const` members because their values cannot be computed at compile-time.</span></span> <span data-ttu-id="c51c7-641">Тем не менее, их объявления `static readonly` вместо имеет точно такой же эффект.</span><span class="sxs-lookup"><span data-stu-id="c51c7-641">However, declaring them `static readonly` instead has much the same effect.</span></span>

#### <a name="versioning-of-constants-and-static-readonly-fields"></a><span data-ttu-id="c51c7-642">Управление версиями, константы и статические только для чтения полей</span><span class="sxs-lookup"><span data-stu-id="c51c7-642">Versioning of constants and static readonly fields</span></span>

<span data-ttu-id="c51c7-643">Константы и поля только для чтения имеют разные двоичных управление версиями семантику.</span><span class="sxs-lookup"><span data-stu-id="c51c7-643">Constants and readonly fields have different binary versioning semantics.</span></span> <span data-ttu-id="c51c7-644">Если выражение ссылается на константу, значение константы получается во время компиляции, но если выражение ссылается на поле только для чтения, значение поля не получается до времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-644">When an expression references a constant, the value of the constant is obtained at compile-time, but when an expression references a readonly field, the value of the field is not obtained until run-time.</span></span> <span data-ttu-id="c51c7-645">Рассмотрим приложение, которое состоит из двух отдельных программ:</span><span class="sxs-lookup"><span data-stu-id="c51c7-645">Consider an application that consists of two separate programs:</span></span>
```csharp
using System;

namespace Program1
{
    public class Utils
    {
        public static readonly int X = 1;
    }
}

namespace Program2
{
    class Test
    {
        static void Main() {
            Console.WriteLine(Program1.Utils.X);
        }
    }
}
```

<span data-ttu-id="c51c7-646">`Program1` И `Program2` пространства имен указывают две программы, которые компилируются отдельно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-646">The `Program1` and `Program2` namespaces denote two programs that are compiled separately.</span></span> <span data-ttu-id="c51c7-647">Так как `Program1.Utils.X` объявлен как статический только для чтения поле, выходное значение `Console.WriteLine` инструкции не известна во время компиляции, но получается во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-647">Because `Program1.Utils.X` is declared as a static readonly field, the value output by the `Console.WriteLine` statement is not known at compile-time, but rather is obtained at run-time.</span></span> <span data-ttu-id="c51c7-648">Таким образом Если значение `X` изменяется и `Program1` перекомпилируется, `Console.WriteLine` выведет новый значение, даже если `Program2` не компилируется повторно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-648">Thus, if the value of `X` is changed and `Program1` is recompiled, the `Console.WriteLine` statement will output the new value even if `Program2` isn't recompiled.</span></span> <span data-ttu-id="c51c7-649">Однако `X` является константой, значение `X` получается во время `Program2` был скомпилирован, а не изменится, изменяется в `Program1` пока `Program2` перекомпилируется.</span><span class="sxs-lookup"><span data-stu-id="c51c7-649">However, had `X` been a constant, the value of `X` would have been obtained at the time `Program2` was compiled, and would remain unaffected by changes in `Program1` until `Program2` is recompiled.</span></span>

### <a name="volatile-fields"></a><span data-ttu-id="c51c7-650">Изменяемые поля</span><span class="sxs-lookup"><span data-stu-id="c51c7-650">Volatile fields</span></span>

<span data-ttu-id="c51c7-651">Когда *field_declaration* включает в себя `volatile` модификатор, поля, представленное в этом объявлении являются ***изменяемые поля***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-651">When a *field_declaration* includes a `volatile` modifier, the fields introduced by that declaration are ***volatile fields***.</span></span>

<span data-ttu-id="c51c7-652">Для долговременного поля, методы оптимизации, которые способен упорядочить инструкции может привести к непредвиденным и непредсказуемые результаты в многопоточных программах с доступом к полям без синхронизации, например за счет *lock_statement*  ([Инструкция lock](statements.md#the-lock-statement)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-652">For non-volatile fields, optimization techniques that reorder instructions can lead to unexpected and unpredictable results in multi-threaded programs that access fields without synchronization such as that provided by the *lock_statement* ([The lock statement](statements.md#the-lock-statement)).</span></span> <span data-ttu-id="c51c7-653">Эти оптимизации могут выполняться компилятором, система времени выполнения или оборудования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-653">These optimizations can be performed by the compiler, by the run-time system, or by hardware.</span></span> <span data-ttu-id="c51c7-654">Для полей volatile такие изменения порядка оптимизации ограничены.</span><span class="sxs-lookup"><span data-stu-id="c51c7-654">For volatile fields, such reordering optimizations are restricted:</span></span>

*  <span data-ttu-id="c51c7-655">Успешное чтение поле с модификатором volatile называется ***чтения из временного***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-655">A read of a volatile field is called a ***volatile read***.</span></span> <span data-ttu-id="c51c7-656">Volatile чтения имеет «получить семантику»; то есть он гарантированно случаются до ссылок на память, происходящие после него в последовательности инструкций.</span><span class="sxs-lookup"><span data-stu-id="c51c7-656">A volatile read has "acquire semantics"; that is, it is guaranteed to occur prior to any references to memory that occur after it in the instruction sequence.</span></span>
*  <span data-ttu-id="c51c7-657">Операция записи поле с модификатором volatile называется ***записи***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-657">A write of a volatile field is called a ***volatile write***.</span></span> <span data-ttu-id="c51c7-658">Volatile записи имеет «release семантики»; то есть он гарантированно происходят после любой ссылки на память до инструкции по записи в последовательности инструкций.</span><span class="sxs-lookup"><span data-stu-id="c51c7-658">A volatile write has "release semantics"; that is, it is guaranteed to happen after any memory references prior to the write instruction in the instruction sequence.</span></span>

<span data-ttu-id="c51c7-659">Эти ограничения гарантируют, что все потоки будут видеть временные записи, выполняемые другим потоком, в порядке выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-659">These restrictions ensure that all threads will observe volatile writes performed by any other thread in the order in which they were performed.</span></span> <span data-ttu-id="c51c7-660">Соответствующая реализация не требуется для предоставления единого общего упорядочения записей volatile материал из всех потоков выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-660">A conforming implementation is not required to provide a single total ordering of volatile writes as seen from all threads of execution.</span></span> <span data-ttu-id="c51c7-661">Поле с модификатором volatile тип должен быть одним из следующих:</span><span class="sxs-lookup"><span data-stu-id="c51c7-661">The type of a volatile field must be one of the following:</span></span>

*  <span data-ttu-id="c51c7-662">Объект *reference_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-662">A *reference_type*.</span></span>
*  <span data-ttu-id="c51c7-663">Тип `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `char`, `float`, `bool`, `System.IntPtr`, или` System.UIntPtr`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-663">The type `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `char`, `float`, `bool`, `System.IntPtr`, or` System.UIntPtr`.</span></span>
*  <span data-ttu-id="c51c7-664">*Enum_type* необходимости базовый тип перечисления из `byte`, `sbyte`, `short`, `ushort`, `int`, или `uint`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-664">An *enum_type* having an enum base type of `byte`, `sbyte`, `short`, `ushort`, `int`, or `uint`.</span></span>

<span data-ttu-id="c51c7-665">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-665">The example</span></span>
```csharp
using System;
using System.Threading;

class Test
{
    public static int result;   
    public static volatile bool finished;

    static void Thread2() {
        result = 143;    
        finished = true; 
    }

    static void Main() {
        finished = false;

        // Run Thread2() in a new thread
        new Thread(new ThreadStart(Thread2)).Start();

        // Wait for Thread2 to signal that it has a result by setting
        // finished to true.
        for (;;) {
            if (finished) {
                Console.WriteLine("result = {0}", result);
                return;
            }
        }
    }
}
```
<span data-ttu-id="c51c7-666">выводятся следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c51c7-666">produces the output:</span></span>
```
result = 143
```

<span data-ttu-id="c51c7-667">В этом примере метод `Main` запускает новый поток, который выполняет метод `Thread2`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-667">In this example, the method `Main` starts a new thread that runs the method `Thread2`.</span></span> <span data-ttu-id="c51c7-668">Этот метод сохраняет значение в поле с именем долговременного `result`, затем сохраняет `true` в поле с модификатором volatile `finished`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-668">This method stores a value into a non-volatile field called `result`, then stores `true` in the volatile field `finished`.</span></span> <span data-ttu-id="c51c7-669">Основной поток ожидает поле `finished` будет присвоено `true`, затем считывает поле `result`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-669">The main thread waits for the field `finished` to be set to `true`, then reads the field `result`.</span></span> <span data-ttu-id="c51c7-670">Так как `finished` был объявлен `volatile`, основной поток должен считать значение `143` из поля `result`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-670">Since `finished` has been declared `volatile`, the main thread must read the value `143` from the field `result`.</span></span> <span data-ttu-id="c51c7-671">Если поле `finished` не было объявлено как `volatile`, то он будет то сохранение для `result` должен отображаться в основной поток после хранилище для `finished`и, следовательно для основного потока чтения значения `0` из поле `result`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-671">If the field `finished` had not been declared `volatile`, then it would be permissible for the store to `result` to be visible to the main thread after the store to `finished`, and hence for the main thread to read the value `0` from the field `result`.</span></span> <span data-ttu-id="c51c7-672">Объявление `finished` как `volatile` поле предотвращает такие несоответствия.</span><span class="sxs-lookup"><span data-stu-id="c51c7-672">Declaring `finished` as a `volatile` field prevents any such inconsistency.</span></span>

### <a name="field-initialization"></a><span data-ttu-id="c51c7-673">Инициализация поля</span><span class="sxs-lookup"><span data-stu-id="c51c7-673">Field initialization</span></span>

<span data-ttu-id="c51c7-674">Начальное значение поля, будь то статического поля или поля экземпляра, значение по умолчанию ([значения по умолчанию](variables.md#default-values)) в качестве типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-674">The initial value of a field, whether it be a static field or an instance field, is the default value ([Default values](variables.md#default-values)) of the field's type.</span></span> <span data-ttu-id="c51c7-675">Определите значение атрибута поля, прежде чем этот инициализации по умолчанию и поля не таким образом никогда не «инициализирован» невозможна.</span><span class="sxs-lookup"><span data-stu-id="c51c7-675">It is not possible to observe the value of a field before this default initialization has occurred, and a field is thus never "uninitialized".</span></span> <span data-ttu-id="c51c7-676">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-676">The example</span></span>
```csharp
using System;

class Test
{
    static bool b;
    int i;

    static void Main() {
        Test t = new Test();
        Console.WriteLine("b = {0}, i = {1}", b, t.i);
    }
}
```
<span data-ttu-id="c51c7-677">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-677">produces the output</span></span>
```
b = False, i = 0
```
<span data-ttu-id="c51c7-678">так как `b` и `i` автоматически инициализированы значениями по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-678">because `b` and `i` are both automatically initialized to default values.</span></span>

### <a name="variable-initializers"></a><span data-ttu-id="c51c7-679">Инициализаторы переменных</span><span class="sxs-lookup"><span data-stu-id="c51c7-679">Variable initializers</span></span>

<span data-ttu-id="c51c7-680">Объявления полей могут включать *variable_initializer*s.</span><span class="sxs-lookup"><span data-stu-id="c51c7-680">Field declarations may include *variable_initializer*s.</span></span> <span data-ttu-id="c51c7-681">Для статических полей инициализаторы переменных соответствуют операторы присваивания, которые выполняются во время инициализации класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-681">For static fields, variable initializers correspond to assignment statements that are executed during class initialization.</span></span> <span data-ttu-id="c51c7-682">Для экземпляра поля, инициализаторы переменных соответствуют операторы присваивания, которые выполняются при создании экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-682">For instance fields, variable initializers correspond to assignment statements that are executed when an instance of the class is created.</span></span>

<span data-ttu-id="c51c7-683">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-683">The example</span></span>
```csharp
using System;

class Test
{
    static double x = Math.Sqrt(2.0);
    int i = 100;
    string s = "Hello";

    static void Main() {
        Test a = new Test();
        Console.WriteLine("x = {0}, i = {1}, s = {2}", x, a.i, a.s);
    }
}
```
<span data-ttu-id="c51c7-684">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-684">produces the output</span></span>
```
x = 1.4142135623731, i = 100, s = Hello
```
<span data-ttu-id="c51c7-685">так как назначение для `x` возникает при выполнении инициализаторов статического поля и назначений, `i` и `s` происходят при выполнении инициализаторы полей экземпляров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-685">because an assignment to `x` occurs when static field initializers execute and assignments to `i` and `s` occur when the instance field initializers execute.</span></span>

<span data-ttu-id="c51c7-686">Инициализация значения по умолчанию, описанные в [инициализацию поля](classes.md#field-initialization) происходит для всех полей, включая поля, имеющие инициализаторы переменных.</span><span class="sxs-lookup"><span data-stu-id="c51c7-686">The default value initialization described in [Field initialization](classes.md#field-initialization) occurs for all fields, including fields that have variable initializers.</span></span> <span data-ttu-id="c51c7-687">Таким образом при инициализации класса, все статические поля в этом классе сначала инициализируются значениями по умолчанию, и затем выполняются инициализаторы статических полей в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-687">Thus, when a class is initialized, all static fields in that class are first initialized to their default values, and then the static field initializers are executed in textual order.</span></span> <span data-ttu-id="c51c7-688">Аналогичным образом когда создается экземпляр класса, все поля экземпляра в этом экземпляре сначала инициализируются значениями по умолчанию и затем инициализаторы полей экземпляров, выполняются в алфавитном порядке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-688">Likewise, when an instance of a class is created, all instance fields in that instance are first initialized to their default values, and then the instance field initializers are executed in textual order.</span></span>

<span data-ttu-id="c51c7-689">Это статические поля с инициализаторами переменных в их состоянии значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-689">It is possible for static fields with variable initializers to be observed in their default value state.</span></span> <span data-ttu-id="c51c7-690">Тем не менее это настоятельно не рекомендуется, вопрос стиля.</span><span class="sxs-lookup"><span data-stu-id="c51c7-690">However, this is strongly discouraged as a matter of style.</span></span> <span data-ttu-id="c51c7-691">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-691">The example</span></span>
```csharp
using System;

class Test
{
    static int a = b + 1;
    static int b = a + 1;

    static void Main() {
        Console.WriteLine("a = {0}, b = {1}", a, b);
    }
}
```
<span data-ttu-id="c51c7-692">демонстрирует это расширение функциональности.</span><span class="sxs-lookup"><span data-stu-id="c51c7-692">exhibits this behavior.</span></span> <span data-ttu-id="c51c7-693">Несмотря на циклические определения и b, программа является допустимым.</span><span class="sxs-lookup"><span data-stu-id="c51c7-693">Despite the circular definitions of a and b, the program is valid.</span></span> <span data-ttu-id="c51c7-694">Это приводит в выходных данных</span><span class="sxs-lookup"><span data-stu-id="c51c7-694">It results in the output</span></span>
```
a = 1, b = 2
```
<span data-ttu-id="c51c7-695">так как статические поля `a` и `b` инициализируются `0` (значение по умолчанию для `int`) перед их инициализаторов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-695">because the static fields `a` and `b` are initialized to `0` (the default value for `int`) before their initializers are executed.</span></span> <span data-ttu-id="c51c7-696">При инициализатор для `a` выполняется, значение `b` равен нулю и поэтому `a` инициализируется `1`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-696">When the initializer for `a` runs, the value of `b` is zero, and so `a` is initialized to `1`.</span></span> <span data-ttu-id="c51c7-697">Когда инициализатор для `b` выполняется, значение `a` уже `1`и поэтому `b` инициализируется `2`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-697">When the initializer for `b` runs, the value of `a` is already `1`, and so `b` is initialized to `2`.</span></span>

#### <a name="static-field-initialization"></a><span data-ttu-id="c51c7-698">Инициализация статических полей</span><span class="sxs-lookup"><span data-stu-id="c51c7-698">Static field initialization</span></span>

<span data-ttu-id="c51c7-699">Инициализаторы переменных статических полей класса соответствуют последовательности назначений, которые выполняются в порядке, в котором они появляются в объявлении класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-699">The static field variable initializers of a class correspond to a sequence of assignments that are executed in the textual order in which they appear in the class declaration.</span></span> <span data-ttu-id="c51c7-700">Если статический конструктор ([статические конструкторы](classes.md#static-constructors)) существует в классе, выполнение Инициализаторы статических полей, происходит непосредственно перед выполнением этого статического конструктора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-700">If a static constructor ([Static constructors](classes.md#static-constructors)) exists in the class, execution of the static field initializers occurs immediately prior to executing that static constructor.</span></span> <span data-ttu-id="c51c7-701">В противном случае статическое поле инициализаторов в время зависит от реализации перед первым использованием статического поля этого класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-701">Otherwise, the static field initializers are executed at an implementation-dependent time prior to the first use of a static field of that class.</span></span> <span data-ttu-id="c51c7-702">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-702">The example</span></span>
```csharp
using System;

class Test 
{ 
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    public static int X = Test.F("Init A");
}

class B
{
    public static int Y = Test.F("Init B");
}
```
<span data-ttu-id="c51c7-703">может выдавать либо выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c51c7-703">might produce either the output:</span></span>
```
Init A
Init B
1 1
```
<span data-ttu-id="c51c7-704">или выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c51c7-704">or the output:</span></span>
```
Init B
Init A
1 1
```
<span data-ttu-id="c51c7-705">так как выполнение `X`элемента инициализатора и `Y`в инициализатор может возникнуть в любом порядке; они ограничены только по до первого обращения к этим полям.</span><span class="sxs-lookup"><span data-stu-id="c51c7-705">because the execution of `X`'s initializer and `Y`'s initializer could occur in either order; they are only constrained to occur before the references to those fields.</span></span> <span data-ttu-id="c51c7-706">Тем не менее в примере:</span><span class="sxs-lookup"><span data-stu-id="c51c7-706">However, in the example:</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        Console.WriteLine("{0} {1}", B.Y, A.X);
    }

    public static int F(string s) {
        Console.WriteLine(s);
        return 1;
    }
}

class A
{
    static A() {}

    public static int X = Test.F("Init A");
}

class B
{
    static B() {}

    public static int Y = Test.F("Init B");
}
```
<span data-ttu-id="c51c7-707">результат должен быть:</span><span class="sxs-lookup"><span data-stu-id="c51c7-707">the output must be:</span></span>
```
Init B
Init A
1 1
```
<span data-ttu-id="c51c7-708">так как правил для выполнения статических конструкторов (как определено в [статические конструкторы](classes.md#static-constructors)) предоставить ее в `B`в статический конструктор (и, следовательно `B`в статическое поле инициализаторы) должна быть запущена перед `A`в статическом конструкторе и инициализаторы полей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-708">because the rules for when static constructors execute (as defined in [Static constructors](classes.md#static-constructors)) provide that `B`'s static constructor (and hence `B`'s static field initializers) must run before `A`'s static constructor and field initializers.</span></span>

#### <a name="instance-field-initialization"></a><span data-ttu-id="c51c7-709">Инициализация поля экземпляра</span><span class="sxs-lookup"><span data-stu-id="c51c7-709">Instance field initialization</span></span>

<span data-ttu-id="c51c7-710">Инициализаторы полей экземпляров переменной класса соответствуют последовательности назначений, которые выполняются сразу же после входа в любой из конструкторов экземпляров ([инициализаторы конструктора](classes.md#constructor-initializers)) этого класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-710">The instance field variable initializers of a class correspond to a sequence of assignments that are executed immediately upon entry to any one of the instance constructors ([Constructor initializers](classes.md#constructor-initializers)) of that class.</span></span> <span data-ttu-id="c51c7-711">Инициализаторы переменных выполняются в порядке, в котором они появляются в объявлении класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-711">The variable initializers are executed in the textual order in which they appear in the class declaration.</span></span> <span data-ttu-id="c51c7-712">Процесс создания и инициализации экземпляра класса описан далее в [конструкторы экземпляров](classes.md#instance-constructors).</span><span class="sxs-lookup"><span data-stu-id="c51c7-712">The class instance creation and initialization process is described further in [Instance constructors](classes.md#instance-constructors).</span></span>

<span data-ttu-id="c51c7-713">Инициализатор переменной для поля экземпляра не может ссылаться на экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-713">A variable initializer for an instance field cannot reference the instance being created.</span></span> <span data-ttu-id="c51c7-714">Таким образом, это ошибка времени компиляции для ссылки на `this` в инициализаторе переменной, так как он является ошибкой во время компиляции инициализатор переменной для ссылки на любой другой член экземпляра через *simple_name*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-714">Thus, it is a compile-time error to reference `this` in a variable initializer, as it is a compile-time error for a variable initializer to reference any instance member through a *simple_name*.</span></span> <span data-ttu-id="c51c7-715">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-715">In the example</span></span>
```csharp
class A
{
    int x = 1;
    int y = x + 1;        // Error, reference to instance member of this
}
```
<span data-ttu-id="c51c7-716">инициализатор переменной для `y` приводит к ошибке времени компиляции, так как он ссылается на член экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-716">the variable initializer for `y` results in a compile-time error because it references a member of the instance being created.</span></span>

## <a name="methods"></a><span data-ttu-id="c51c7-717">Методы</span><span class="sxs-lookup"><span data-stu-id="c51c7-717">Methods</span></span>

<span data-ttu-id="c51c7-718">***Метод*** — это член, реализующий вычисление или действие, которое может выполнять объект или класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-718">A ***method*** is a member that implements a computation or action that can be performed by an object or class.</span></span> <span data-ttu-id="c51c7-719">Методы объявляются с помощью *method_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-719">Methods are declared using *method_declaration*s:</span></span>

```antlr
method_declaration
    : method_header method_body
    ;

method_header
    : attributes? method_modifier* 'partial'? return_type member_name type_parameter_list?
      '(' formal_parameter_list? ')' type_parameter_constraints_clause*
    ;

method_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | 'async'
    | method_modifier_unsafe
    ;

return_type
    : type
    | 'void'
    ;

member_name
    : identifier
    | interface_type '.' identifier
    ;

method_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

<span data-ttu-id="c51c7-720">Объект *method_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)) и является допустимой комбинацией четырех модификаторов доступа ([модификаторы доступа ](classes.md#access-modifiers)), `new` ([Модификатор new](classes.md#the-new-modifier)), `static` ([экземпляра и статические методы](classes.md#static-and-instance-methods)), `virtual` ([виртуальных методов](classes.md#virtual-methods)), `override` ([Переопределять методы](classes.md#override-methods)), `sealed` ([запечатанные методы](classes.md#sealed-methods)), `abstract` ([абстрактные методы](classes.md#abstract-methods)), и `extern` ([Внешние методы](classes.md#external-methods)) модификаторы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-720">A *method_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)),  `static` ([Static and instance methods](classes.md#static-and-instance-methods)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="c51c7-721">Объявление имеет допустимое сочетание модификаторов, если выполняются все следующие условия:</span><span class="sxs-lookup"><span data-stu-id="c51c7-721">A declaration has a valid combination of modifiers if all of the following are true:</span></span>

*  <span data-ttu-id="c51c7-722">Объявление включает является допустимым сочетанием модификаторы доступа ([модификаторы доступа](classes.md#access-modifiers)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-722">The declaration includes a valid combination of access modifiers ([Access modifiers](classes.md#access-modifiers)).</span></span>
*  <span data-ttu-id="c51c7-723">Объявление содержит тот же модификатор несколько раз.</span><span class="sxs-lookup"><span data-stu-id="c51c7-723">The declaration does not include the same modifier multiple times.</span></span>
*  <span data-ttu-id="c51c7-724">Объявление включает не более одного из следующих модификаторов: `static`, `virtual`, и `override`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-724">The declaration includes at most one of the following modifiers: `static`, `virtual`, and `override`.</span></span>
*  <span data-ttu-id="c51c7-725">Объявление включает не более одного из следующих модификаторов: `new` и `override`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-725">The declaration includes at most one of the following modifiers: `new` and `override`.</span></span>
*  <span data-ttu-id="c51c7-726">Если объявление включает `abstract` модификатор, то объявление не поддерживает ни один из следующих модификаторов: `static`, `virtual`, `sealed` или `extern`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-726">If the declaration includes the `abstract` modifier, then the declaration does not include any of the following modifiers: `static`, `virtual`, `sealed` or `extern`.</span></span>
*  <span data-ttu-id="c51c7-727">Если объявление включает `private` модификатор, то объявление не поддерживает ни один из следующих модификаторов: `virtual`, `override`, или `abstract`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-727">If the declaration includes the `private` modifier, then the declaration does not include any of the following modifiers: `virtual`, `override`, or `abstract`.</span></span>
*  <span data-ttu-id="c51c7-728">Если объявление включает `sealed` модификатор, то объявление также включает в себя `override` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-728">If the declaration includes the `sealed` modifier, then the declaration also includes the `override` modifier.</span></span>
*  <span data-ttu-id="c51c7-729">Если объявление включает `partial` модификатор, то оно не поддерживает ни один из следующих модификаторов: `new`, `public`, `protected`, `internal`, `private`, `virtual`, `sealed`, `override` , `abstract`, или `extern`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-729">If the declaration includes the `partial` modifier, then it does not include any of the following modifiers: `new`, `public`, `protected`, `internal`, `private`, `virtual`, `sealed`, `override`, `abstract`, or `extern`.</span></span>

<span data-ttu-id="c51c7-730">Метод, имеющий `async` модификатор является асинхронной функции и следует правилам, описанным в [асинхронные функции](classes.md#async-functions).</span><span class="sxs-lookup"><span data-stu-id="c51c7-730">A method that has the `async` modifier is an async function and follows the rules described in [Async functions](classes.md#async-functions).</span></span>

<span data-ttu-id="c51c7-731">*Return_type* метода объявление указывает тип значения, вычисляемого и возвращаемого методом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-731">The *return_type* of a method declaration specifies the type of the value computed and returned by the method.</span></span> <span data-ttu-id="c51c7-732">*Return_type* является `void` Если метод не возвращает значение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-732">The *return_type* is `void` if the method does not return a value.</span></span> <span data-ttu-id="c51c7-733">Если объявление включает `partial` модификатор, то тип возвращаемого значения должен быть `void`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-733">If the declaration includes the `partial` modifier, then the return type must be `void`.</span></span>

<span data-ttu-id="c51c7-734">*Member_name* задает имя метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-734">The *member_name* specifies the name of the method.</span></span> <span data-ttu-id="c51c7-735">Если метод не явная реализация члена интерфейса ([явные реализации члена интерфейса](interfaces.md#explicit-interface-member-implementations)), *member_name* является просто *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-735">Unless the method is an explicit interface member implementation ([Explicit interface member implementations](interfaces.md#explicit-interface-member-implementations)), the *member_name* is simply an *identifier*.</span></span> <span data-ttu-id="c51c7-736">Для явной реализации члена интерфейса *member_name* состоит из *interface_type* следуют "`.`" и *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-736">For an explicit interface member implementation, the *member_name* consists of an *interface_type* followed by a "`.`" and an *identifier*.</span></span>

<span data-ttu-id="c51c7-737">Необязательный *type_parameter_list* задает параметры типа метода ([параметры типа](classes.md#type-parameters)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-737">The optional *type_parameter_list* specifies the type parameters of the method ([Type parameters](classes.md#type-parameters)).</span></span> <span data-ttu-id="c51c7-738">Если *type_parameter_list* указан метод ***универсального метода***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-738">If a *type_parameter_list* is specified the method is a ***generic method***.</span></span> <span data-ttu-id="c51c7-739">Если метод имеет `extern` модификатор, *type_parameter_list* нельзя использовать.</span><span class="sxs-lookup"><span data-stu-id="c51c7-739">If the method has an `extern` modifier, a *type_parameter_list* cannot be specified.</span></span>

<span data-ttu-id="c51c7-740">Необязательный *formal_parameter_list* указывает параметры метода ([параметры метода](classes.md#method-parameters)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-740">The optional *formal_parameter_list* specifies the parameters of the method ([Method parameters](classes.md#method-parameters)).</span></span>

<span data-ttu-id="c51c7-741">Необязательный *type_parameter_constraints_clause*определяют ограничения параметров типа отдельных ([ограничения параметров типа](classes.md#type-parameter-constraints)) и может быть задан только если *type_parameter_ список* также предоставляется, и не содержит метод `override` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-741">The optional *type_parameter_constraints_clause*s specify constraints on individual type parameters ([Type parameter constraints](classes.md#type-parameter-constraints)) and may only be specified if a *type_parameter_list* is also supplied, and the method does not have an `override` modifier.</span></span>

<span data-ttu-id="c51c7-742">*Return_type* и каждый из типов, на которые ссылается *formal_parameter_list* метода должен быть по крайней мере такой же уровень доступности, чем сам метод ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-742">The *return_type* and each of the types referenced in the *formal_parameter_list* of a method must be at least as accessible as the method itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-743">*Method_body* либо точкой с запятой, ***тела оператора*** или ***тело выражения***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-743">The *method_body* is either a semicolon, a ***statement body*** or an ***expression body***.</span></span> <span data-ttu-id="c51c7-744">Состоит из тела оператора *блок*, который задает операторы, выполняемые при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-744">A statement body consists of a *block*, which specifies the statements to execute when the method is invoked.</span></span> <span data-ttu-id="c51c7-745">Тело выражения состоит из `=>` следуют *выражение* используйте точку с запятой и обозначает одно выражение для выполнения при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-745">An expression body consists of `=>` followed by an *expression* and a semicolon, and denotes a single expression to perform when the method is invoked.</span></span> 

<span data-ttu-id="c51c7-746">Для `abstract` и `extern` методы, *method_body* состоит просто из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-746">For `abstract` and `extern` methods, the *method_body* consists simply of a semicolon.</span></span> <span data-ttu-id="c51c7-747">Для `partial` методы *method_body* может состоять из точки с запятой, тело блока или тело выражения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-747">For `partial` methods the *method_body* may consist of either a semicolon, a block body or an expression body.</span></span> <span data-ttu-id="c51c7-748">Для всех других методов *method_body* тело блока или тело выражения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-748">For all other methods, the *method_body* is either a block body or an expression body.</span></span>

<span data-ttu-id="c51c7-749">Если *method_body* состоит из точки с запятой, то объявление не может включать `async` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-749">If the *method_body* consists of a semicolon, then the declaration may not include the `async` modifier.</span></span>

<span data-ttu-id="c51c7-750">Имя, список параметров типа и список формальных параметров метода определить сигнатуру ([сигнатуры и перегрузка](basic-concepts.md#signatures-and-overloading)) метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-750">The name, the type parameter list and the formal parameter list of a method define the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of the method.</span></span> <span data-ttu-id="c51c7-751">В частности сигнатура метода состоит из имени, количество параметров типа и числа, модификаторы и типы его формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-751">Specifically, the signature of a method consists of its name, the number of type parameters and the number, modifiers, and types of its formal parameters.</span></span> <span data-ttu-id="c51c7-752">Для этих целей любого параметра типа метода, который происходит в тип формального параметра идентифицируется не по имени, а также по ее порядковому номеру в списке аргументов типа метода. Тип возвращаемого значения не является частью сигнатуры метода, как и имена параметров типа или формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-752">For these purposes, any type parameter of the method that occurs in the type of a formal parameter is identified not by its name, but by its ordinal position in the type argument list of the method.The return type is not part of a method's signature, nor are the names of the type parameters or the formal parameters.</span></span>

<span data-ttu-id="c51c7-753">Имя метода должно отличаться от имен всех остальных не методов, объявленных в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-753">The name of a method must differ from the names of all other non-methods declared in the same class.</span></span> <span data-ttu-id="c51c7-754">Кроме того, подпись метода должна отличаться от сигнатур всех других методов, объявленных в том же классе, и двух методов, объявленных в том же классе может не иметь подписи, которые отличаются только модификаторами `ref` и `out`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-754">In addition, the signature of a method must differ from the signatures of all other methods declared in the same class, and two methods declared in the same class may not have signatures that differ solely by `ref` and `out`.</span></span>

<span data-ttu-id="c51c7-755">Метод *параметр_типа*s находятся в области всего *method_declaration*и может использоваться для формирования типов в этой области в *return_type*, *method_body*, и *type_parameter_constraints_clause*s, но не в *атрибуты*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-755">The method's *type_parameter*s are in scope throughout the *method_declaration*, and can be used to form types throughout that scope in *return_type*, *method_body*, and *type_parameter_constraints_clause*s but not in *attributes*.</span></span>

<span data-ttu-id="c51c7-756">Все формальные параметры и параметры типа должны иметь разные имена.</span><span class="sxs-lookup"><span data-stu-id="c51c7-756">All formal parameters and type parameters must have different names.</span></span>

### <a name="method-parameters"></a><span data-ttu-id="c51c7-757">Параметры методов</span><span class="sxs-lookup"><span data-stu-id="c51c7-757">Method parameters</span></span>

<span data-ttu-id="c51c7-758">Параметры метода, если таковые имеются, объявляются с помощью метода *formal_parameter_list*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-758">The parameters of a method, if any, are declared by the method's *formal_parameter_list*.</span></span>

```antlr
formal_parameter_list
    : fixed_parameters
    | fixed_parameters ',' parameter_array
    | parameter_array
    ;

fixed_parameters
    : fixed_parameter (',' fixed_parameter)*
    ;

fixed_parameter
    : attributes? parameter_modifier? type identifier default_argument?
    ;

default_argument
    : '=' expression
    ;

parameter_modifier
    : 'ref'
    | 'out'
    | 'this'
    ;

parameter_array
    : attributes? 'params' array_type identifier
    ;
```

<span data-ttu-id="c51c7-759">Список формальных параметров состоит из одного или нескольких разделенных запятыми параметров которых может быть только последний *parameter_array*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-759">The formal parameter list consists of one or more comma-separated parameters of which only the last may be a *parameter_array*.</span></span>

<span data-ttu-id="c51c7-760">Объект *fixed_parameter* состоит из необязательного набора *атрибуты* ([атрибуты](attributes.md)), необязательный `ref`, `out` или `this` модификатор, *тип*, *идентификатор* разделителя и необязательного *default_argument*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-760">A *fixed_parameter* consists of an optional set of *attributes* ([Attributes](attributes.md)), an optional `ref`, `out` or `this` modifier, a *type*, an *identifier* and an optional *default_argument*.</span></span> <span data-ttu-id="c51c7-761">Каждый *fixed_parameter* объявляет параметр заданного типа с заданным именем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-761">Each *fixed_parameter* declares a parameter of the given type with the given name.</span></span> <span data-ttu-id="c51c7-762">`this` Модификатор помечает метод как метод расширения, а допускается только для первого параметра статического метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-762">The `this` modifier designates the method as an extension method and is only allowed on the first parameter of a static method.</span></span> <span data-ttu-id="c51c7-763">Методы расширения более подробно описаны в [методы расширения](classes.md#extension-methods).</span><span class="sxs-lookup"><span data-stu-id="c51c7-763">Extension methods are further described in [Extension methods](classes.md#extension-methods).</span></span>

<span data-ttu-id="c51c7-764">Объект *fixed_parameter* с *default_argument* называется ***необязательный параметр***, тогда как *fixed_parameter* без *default_argument* — ***обязательный параметр***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-764">A *fixed_parameter* with a *default_argument* is known as an ***optional parameter***, whereas a *fixed_parameter* without a *default_argument* is a ***required parameter***.</span></span> <span data-ttu-id="c51c7-765">Обязательный параметр может не отображаться после необязательного параметра в *formal_parameter_list*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-765">A required parameter may not appear after an optional parameter in a *formal_parameter_list*.</span></span>

<span data-ttu-id="c51c7-766">Объект `ref` или `out` параметр не может иметь *default_argument*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-766">A `ref` or `out` parameter cannot have a *default_argument*.</span></span> <span data-ttu-id="c51c7-767">*Выражение* в *default_argument* должно быть одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="c51c7-767">The *expression* in a *default_argument* must be one of the following:</span></span>

*  <span data-ttu-id="c51c7-768">*constant_expression*</span><span class="sxs-lookup"><span data-stu-id="c51c7-768">a *constant_expression*</span></span>
*  <span data-ttu-id="c51c7-769">выражение в форме `new S()` где `S` является типом значения</span><span class="sxs-lookup"><span data-stu-id="c51c7-769">an expression of the form `new S()` where `S` is a value type</span></span>
*  <span data-ttu-id="c51c7-770">выражение в форме `default(S)` где `S` является типом значения</span><span class="sxs-lookup"><span data-stu-id="c51c7-770">an expression of the form `default(S)` where `S` is a value type</span></span>

<span data-ttu-id="c51c7-771">*Выражение* должно допускать неявное преобразование удостоверения или допускает значения NULL преобразование к типу параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-771">The *expression* must be implicitly convertible by an identity or nullable conversion to the type of the parameter.</span></span>

<span data-ttu-id="c51c7-772">Появление в реализующего объявления разделяемого метода необязательные параметры ([разделяемые методы](classes.md#partial-methods)), явная реализация члена интерфейса ([явные реализации члена интерфейса](interfaces.md#explicit-interface-member-implementations)) или в объявление индексатора единственного параметра ([индексаторы](classes.md#indexers)) компилятор должен создать предупреждение, поскольку эти члены никогда не могут быть вызваны способом, в котором аргументы могут отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="c51c7-772">If optional parameters occur in an implementing partial method declaration ([Partial methods](classes.md#partial-methods)) , an explicit interface member implementation ([Explicit interface member implementations](interfaces.md#explicit-interface-member-implementations)) or in a single-parameter indexer declaration ([Indexers](classes.md#indexers)) the compiler should give a warning, since these members can never be invoked in a way that permits arguments to be omitted.</span></span>

<span data-ttu-id="c51c7-773">Объект *parameter_array* состоит из необязательного набора *атрибуты* ([атрибуты](attributes.md)), `params` модификатор, *array_type*, и *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-773">A *parameter_array* consists of an optional set of *attributes* ([Attributes](attributes.md)), a `params` modifier, an *array_type*, and an *identifier*.</span></span> <span data-ttu-id="c51c7-774">Массив параметров объявляет один параметр типа заданного массива с заданным именем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-774">A parameter array declares a single parameter of the given array type with the given name.</span></span> <span data-ttu-id="c51c7-775">*Array_type* параметра массив должен быть одномерным массивом ([типы массивов](arrays.md#array-types)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-775">The *array_type* of a parameter array must be a single-dimensional array type ([Array types](arrays.md#array-types)).</span></span> <span data-ttu-id="c51c7-776">При вызове метода массив параметров позволяет либо один аргумент типа указывать заданного массива, или он разрешает ноль или более аргументов типа элемента массива должны быть указаны.</span><span class="sxs-lookup"><span data-stu-id="c51c7-776">In a method invocation, a parameter array permits either a single argument of the given array type to be specified, or it permits zero or more arguments of the array element type to be specified.</span></span> <span data-ttu-id="c51c7-777">Массивы параметров описаны далее в [массивы параметров](classes.md#parameter-arrays).</span><span class="sxs-lookup"><span data-stu-id="c51c7-777">Parameter arrays are described further in [Parameter arrays](classes.md#parameter-arrays).</span></span>

<span data-ttu-id="c51c7-778">Объект *parameter_array* может возникнуть после необязательного параметра, но не может иметь значение по умолчанию — заменяют аргументы для *parameter_array* вместо бы привести к созданию пустого массива.</span><span class="sxs-lookup"><span data-stu-id="c51c7-778">A *parameter_array* may occur after an optional parameter, but cannot have a default value -- the omission of arguments for a *parameter_array* would instead result in the creation of an empty array.</span></span>

<span data-ttu-id="c51c7-779">В следующем примере показано различных типов параметров:</span><span class="sxs-lookup"><span data-stu-id="c51c7-779">The following example illustrates different kinds of parameters:</span></span>
```csharp
public void M(
    ref int      i,
    decimal      d,
    bool         b = false,
    bool?        n = false,
    string       s = "Hello",
    object       o = null,
    T            t = default(T),
    params int[] a
) { }
```

<span data-ttu-id="c51c7-780">В *formal_parameter_list* для `M`, `i` является обязательным параметром, `d` является обязательным параметром, `b`, `s`, `o` и `t` необязательное значение параметров и `a` является массивом параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-780">In the *formal_parameter_list* for `M`, `i` is a required ref parameter, `d` is a required value parameter, `b`, `s`, `o` and `t` are optional value parameters and `a` is a parameter array.</span></span>

<span data-ttu-id="c51c7-781">Объявление метода создает отдельную область объявления для параметров, параметры типа и локальные переменные.</span><span class="sxs-lookup"><span data-stu-id="c51c7-781">A method declaration creates a separate declaration space for parameters, type parameters and local variables.</span></span> <span data-ttu-id="c51c7-782">Имена вводятся в эту область объявления, список параметров типа и список формальных параметров метода и объявлений локальных переменных в *блок* метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-782">Names are introduced into this declaration space by the type parameter list and the formal parameter list of the method and by local variable declarations in the *block* of the method.</span></span> <span data-ttu-id="c51c7-783">Это ошибка для двух участников области объявления метода с одинаковыми именами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-783">It is an error for two members of a method declaration space to have the same name.</span></span> <span data-ttu-id="c51c7-784">Это ошибка для области объявления метода и в объявлении локальной переменной пространство вложенной области объявления могут содержать элементы с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-784">It is an error for the method declaration space and the local variable declaration space of a nested declaration space to contain elements with the same name.</span></span>

<span data-ttu-id="c51c7-785">Вызов метода ([вызовы методов](expressions.md#method-invocations)) создает копию, предназначенную для вызова, формальные параметры и локальные переменные метода и список аргументов вызова назначает значения или ссылки на переменные вновь созданный формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-785">A method invocation ([Method invocations](expressions.md#method-invocations)) creates a copy, specific to that invocation, of the formal parameters and local variables of the method, and the argument list of the invocation assigns values or variable references to the newly created formal parameters.</span></span> <span data-ttu-id="c51c7-786">В рамках *блок* формальных параметров метода, можно ссылаться по их идентификаторам в *simple_name* выражения ([простые имена](expressions.md#simple-names)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-786">Within the *block* of a method, formal parameters can be referenced by their identifiers in *simple_name* expressions ([Simple names](expressions.md#simple-names)).</span></span>

<span data-ttu-id="c51c7-787">Существует четыре вида формальных параметров:</span><span class="sxs-lookup"><span data-stu-id="c51c7-787">There are four kinds of formal parameters:</span></span>

*  <span data-ttu-id="c51c7-788">Параметры значений, которые объявлены без модификаторов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-788">Value parameters, which are declared without any modifiers.</span></span>
*  <span data-ttu-id="c51c7-789">Ссылаться на параметры, которые объявлены с `ref` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-789">Reference parameters, which are declared with the `ref` modifier.</span></span>
*  <span data-ttu-id="c51c7-790">Выходные параметры, которые объявлены с `out` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-790">Output parameters, which are declared with the `out` modifier.</span></span>
*  <span data-ttu-id="c51c7-791">Массивы параметров, которые объявлены с `params` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-791">Parameter arrays, which are declared with the `params` modifier.</span></span>

<span data-ttu-id="c51c7-792">Как описано в разделе [сигнатуры и перегрузка](basic-concepts.md#signatures-and-overloading), `ref` и `out` модификаторы являются частью сигнатуры метода, но `params` модификатор не.</span><span class="sxs-lookup"><span data-stu-id="c51c7-792">As described in [Signatures and overloading](basic-concepts.md#signatures-and-overloading), the `ref` and `out` modifiers are part of a method's signature, but the `params` modifier is not.</span></span>

#### <a name="value-parameters"></a><span data-ttu-id="c51c7-793">Параметры значения</span><span class="sxs-lookup"><span data-stu-id="c51c7-793">Value parameters</span></span>

<span data-ttu-id="c51c7-794">Параметр, объявленный без модификаторов является параметром значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-794">A parameter declared with no modifiers is a value parameter.</span></span> <span data-ttu-id="c51c7-795">Значение параметра соответствует локальной переменной, которая получит начальное значение из соответствующего аргумента, предоставленного при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-795">A value parameter corresponds to a local variable that gets its initial value from the corresponding argument supplied in the method invocation.</span></span>

<span data-ttu-id="c51c7-796">Если формальный параметр является параметром значения, соответствующего аргумента в вызове метода должно быть выражение, которое может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) в тип формального параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-796">When a formal parameter is a value parameter, the corresponding argument in a method invocation must be an expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the formal parameter type.</span></span>

<span data-ttu-id="c51c7-797">Метод разрешено присваивать новые значения для параметра значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-797">A method is permitted to assign new values to a value parameter.</span></span> <span data-ttu-id="c51c7-798">Такие присваивания влияют только на расположение локального хранилища, представленный параметром значения — они не оказывают влияния на фактический аргумент, заданный в вызове метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-798">Such assignments only affect the local storage location represented by the value parameter—they have no effect on the actual argument given in the method invocation.</span></span>

#### <a name="reference-parameters"></a><span data-ttu-id="c51c7-799">Параметры ссылок</span><span class="sxs-lookup"><span data-stu-id="c51c7-799">Reference parameters</span></span>

<span data-ttu-id="c51c7-800">Параметр, объявленный с `ref` модификатор — ссылочный параметр.</span><span class="sxs-lookup"><span data-stu-id="c51c7-800">A parameter declared with a `ref` modifier is a reference parameter.</span></span> <span data-ttu-id="c51c7-801">В отличие от параметра значения ссылочного параметра не создает новое место хранения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-801">Unlike a value parameter, a reference parameter does not create a new storage location.</span></span> <span data-ttu-id="c51c7-802">Вместо этого параметр ссылки представляет то же место хранения переменной, заданной в качестве аргумента в вызове метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-802">Instead, a reference parameter represents the same storage location as the variable given as the argument in the method invocation.</span></span>

<span data-ttu-id="c51c7-803">Если формальный параметр является ссылочный параметр, соответствующий аргумент в вызове метода должен состоять из ключевого слова `ref` следуют *variable_reference* ([точные правила определения определенного присваивания](variables.md#precise-rules-for-determining-definite-assignment)) того же типа как формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-803">When a formal parameter is a reference parameter, the corresponding argument in a method invocation must consist of the keyword `ref` followed by a *variable_reference* ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)) of the same type as the formal parameter.</span></span> <span data-ttu-id="c51c7-804">Переменной должен быть явно присвоен, прежде чем их можно было передать в качестве ссылочного параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-804">A variable must be definitely assigned before it can be passed as a reference parameter.</span></span>

<span data-ttu-id="c51c7-805">Внутри метода ссылочный параметр всегда считается определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="c51c7-805">Within a method, a reference parameter is always considered definitely assigned.</span></span>

<span data-ttu-id="c51c7-806">Метод, объявленный как итератор ([итераторы](classes.md#iterators)) не могут иметь ссылочные параметры.</span><span class="sxs-lookup"><span data-stu-id="c51c7-806">A method declared as an iterator ([Iterators](classes.md#iterators)) cannot have reference parameters.</span></span>

<span data-ttu-id="c51c7-807">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-807">The example</span></span>
```csharp
using System;

class Test
{
    static void Swap(ref int x, ref int y) {
        int temp = x;
        x = y;
        y = temp;
    }

    static void Main() {
        int i = 1, j = 2;
        Swap(ref i, ref j);
        Console.WriteLine("i = {0}, j = {1}", i, j);
    }
}
```
<span data-ttu-id="c51c7-808">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-808">produces the output</span></span>
```
i = 2, j = 1
```

<span data-ttu-id="c51c7-809">Для вызова `Swap` в `Main`, `x` представляет `i` и `y` представляет `j`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-809">For the invocation of `Swap` in `Main`, `x` represents `i` and `y` represents `j`.</span></span> <span data-ttu-id="c51c7-810">Таким образом, вызов действует замену значений `i` и `j`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-810">Thus, the invocation has the effect of swapping the values of `i` and `j`.</span></span>

<span data-ttu-id="c51c7-811">В методе, который принимает ссылочные параметры, возможно несколько имен для представления в одно место хранения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-811">In a method that takes reference parameters it is possible for multiple names to represent the same storage location.</span></span> <span data-ttu-id="c51c7-812">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-812">In the example</span></span>
```csharp
class A
{
    string s;

    void F(ref string a, ref string b) {
        s = "One";
        a = "Two";
        b = "Three";
    }

    void G() {
        F(ref s, ref s);
    }
}
```
<span data-ttu-id="c51c7-813">вызов `F` в `G` передает ссылку на `s` для обоих `a` и `b`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-813">the invocation of `F` in `G` passes a reference to `s` for both `a` and `b`.</span></span> <span data-ttu-id="c51c7-814">Таким образом, для этого вызова имена `s`, `a`, и `b` ссылаются на том же месте хранения, и все три назначения изменения поля экземпляра `s`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-814">Thus, for that invocation, the names `s`, `a`, and `b` all refer to the same storage location, and the three assignments all modify the instance field `s`.</span></span>

#### <a name="output-parameters"></a><span data-ttu-id="c51c7-815">Выходные параметры</span><span class="sxs-lookup"><span data-stu-id="c51c7-815">Output parameters</span></span>

<span data-ttu-id="c51c7-816">Параметр, объявленный с `out` модификатор является выходным параметром.</span><span class="sxs-lookup"><span data-stu-id="c51c7-816">A parameter declared with an `out` modifier is an output parameter.</span></span> <span data-ttu-id="c51c7-817">Как и ссылочный параметр, выходной параметр не создает новое место хранения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-817">Similar to a reference parameter, an output parameter does not create a new storage location.</span></span> <span data-ttu-id="c51c7-818">Вместо этого выходного параметра представляет то же место хранения переменной, заданной в качестве аргумента в вызове метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-818">Instead, an output parameter represents the same storage location as the variable given as the argument in the method invocation.</span></span>

<span data-ttu-id="c51c7-819">Если формальный параметр является выходным параметром, соответствующего аргумента в вызове метода должен состоять из ключевого слова `out` следуют *variable_reference* ([точные правила определения определенного присваивания](variables.md#precise-rules-for-determining-definite-assignment)) того же типа как формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-819">When a formal parameter is an output parameter, the corresponding argument in a method invocation must consist of the keyword `out` followed by a *variable_reference* ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)) of the same type as the formal parameter.</span></span> <span data-ttu-id="c51c7-820">Переменная не нужно назначать определенно прежде, чем их можно передать в качестве выходного параметра, но вслед за вызовом, где переменная была передана в качестве выходного параметра, переменная считается определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="c51c7-820">A variable need not be definitely assigned before it can be passed as an output parameter, but following an invocation where a variable was passed as an output parameter, the variable is considered definitely assigned.</span></span>

<span data-ttu-id="c51c7-821">Внутри метода, так же, как локальной переменной, параметром output изначально считается неназначенных и должен быть явно присвоен перед его значение используется.</span><span class="sxs-lookup"><span data-stu-id="c51c7-821">Within a method, just like a local variable, an output parameter is initially considered unassigned and must be definitely assigned before its value is used.</span></span>

<span data-ttu-id="c51c7-822">Каждый выходной параметр метода должен быть явно присвоен перед возвращением метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-822">Every output parameter of a method must be definitely assigned before the method returns.</span></span>

<span data-ttu-id="c51c7-823">Метод, объявленный как разделяемый метод ([разделяемые методы](classes.md#partial-methods)) или итератор ([итераторы](classes.md#iterators)) не может иметь выходных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-823">A method declared as a partial method ([Partial methods](classes.md#partial-methods)) or an iterator ([Iterators](classes.md#iterators)) cannot have output parameters.</span></span>

<span data-ttu-id="c51c7-824">Выходные параметры обычно используются в методах, которые создают несколькими возвращаемыми значениями.</span><span class="sxs-lookup"><span data-stu-id="c51c7-824">Output parameters are typically used in methods that produce multiple return values.</span></span> <span data-ttu-id="c51c7-825">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-825">For example:</span></span>
```csharp
using System;

class Test
{
    static void SplitPath(string path, out string dir, out string name) {
        int i = path.Length;
        while (i > 0) {
            char ch = path[i - 1];
            if (ch == '\\' || ch == '/' || ch == ':') break;
            i--;
        }
        dir = path.Substring(0, i);
        name = path.Substring(i);
    }

    static void Main() {
        string dir, name;
        SplitPath("c:\\Windows\\System\\hello.txt", out dir, out name);
        Console.WriteLine(dir);
        Console.WriteLine(name);
    }
}
```

<span data-ttu-id="c51c7-826">В примере получался результат:</span><span class="sxs-lookup"><span data-stu-id="c51c7-826">The example produces the output:</span></span>
```
c:\Windows\System\
hello.txt
```

<span data-ttu-id="c51c7-827">Обратите внимание, что `dir` и `name` переменные могут быть неназначенные, прежде чем они будут переданы `SplitPath`, и что они считаются определенно присвоенной, что следующий за вызовом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-827">Note that the `dir` and `name` variables can be unassigned before they are passed to `SplitPath`, and that they are considered definitely assigned following the call.</span></span>

#### <a name="parameter-arrays"></a><span data-ttu-id="c51c7-828">Массивы параметров</span><span class="sxs-lookup"><span data-stu-id="c51c7-828">Parameter arrays</span></span>

<span data-ttu-id="c51c7-829">Параметр, объявленный с `params` модификатор является массивом параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-829">A parameter declared with a `params` modifier is a parameter array.</span></span> <span data-ttu-id="c51c7-830">Если список формальных параметров включает массив параметров, он должен быть последним параметром в списке, и он должен иметь тип одномерного массива.</span><span class="sxs-lookup"><span data-stu-id="c51c7-830">If a formal parameter list includes a parameter array, it must be the last parameter in the list and it must be of a single-dimensional array type.</span></span> <span data-ttu-id="c51c7-831">Например, типы `string[]` и `string[][]` можно использовать в качестве типа массива параметров, но тип `string[,]` не может.</span><span class="sxs-lookup"><span data-stu-id="c51c7-831">For example, the types `string[]` and `string[][]` can be used as the type of a parameter array, but the type `string[,]` can not.</span></span> <span data-ttu-id="c51c7-832">Невозможно объединить `params` модификатор с модификаторами `ref` и `out`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-832">It is not possible to combine the `params` modifier with the modifiers `ref` and `out`.</span></span>

<span data-ttu-id="c51c7-833">Массив параметров позволяет задать одним из двух способов вызова метода аргументы:</span><span class="sxs-lookup"><span data-stu-id="c51c7-833">A parameter array permits arguments to be specified in one of two ways in a method invocation:</span></span>

*  <span data-ttu-id="c51c7-834">Аргумент, заданный для массива параметров может быть одно выражение, которое может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) в тип массива параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-834">The argument given for a parameter array can be a single expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the parameter array type.</span></span> <span data-ttu-id="c51c7-835">В этом случае в массиве параметров выступает точно параметра значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-835">In this case, the parameter array acts precisely like a value parameter.</span></span>
*  <span data-ttu-id="c51c7-836">Кроме того, вызов можно указать ноль или более аргументов для массива параметров, где каждый аргумент является выражение, которое может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) к типу элемента в массиве параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-836">Alternatively, the invocation can specify zero or more arguments for the parameter array, where each argument is an expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the element type of the parameter array.</span></span> <span data-ttu-id="c51c7-837">В этом случае вызов создает экземпляр типа массив с длиной, соответствующей числу аргументов, инициализирует элементы экземпляра массива с заданными значениями аргументов и использует вновь созданный экземпляр массива в качестве фактического аргумент.</span><span class="sxs-lookup"><span data-stu-id="c51c7-837">In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.</span></span>

<span data-ttu-id="c51c7-838">За исключением разрешение переменное число аргументов в вызове, массив параметров эквивалентен параметру значения ([параметры по значению](classes.md#value-parameters)) того же типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-838">Except for allowing a variable number of arguments in an invocation, a parameter array is precisely equivalent to a value parameter ([Value parameters](classes.md#value-parameters)) of the same type.</span></span>

<span data-ttu-id="c51c7-839">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-839">The example</span></span>
```csharp
using System;

class Test
{
    static void F(params int[] args) {
        Console.Write("Array contains {0} elements:", args.Length);
        foreach (int i in args) 
            Console.Write(" {0}", i);
        Console.WriteLine();
    }

    static void Main() {
        int[] arr = {1, 2, 3};
        F(arr);
        F(10, 20, 30, 40);
        F();
    }
}
```
<span data-ttu-id="c51c7-840">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-840">produces the output</span></span>
```
Array contains 3 elements: 1 2 3
Array contains 4 elements: 10 20 30 40
Array contains 0 elements:
```

<span data-ttu-id="c51c7-841">Первый вызов `F` просто передает массив `a` как параметр значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-841">The first invocation of `F` simply passes the array `a` as a value parameter.</span></span> <span data-ttu-id="c51c7-842">Второй вызов `F` автоматически создает элемент четырех `int[]` с заданными значениями элементов и передает этот экземпляр в качестве параметра значения массива.</span><span class="sxs-lookup"><span data-stu-id="c51c7-842">The second invocation of `F` automatically creates a four-element `int[]` with the given element values and passes that array instance as a value parameter.</span></span> <span data-ttu-id="c51c7-843">Аналогично, третий вызов `F` создает элемент нуля `int[]` и передает этот экземпляр в качестве значения параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-843">Likewise, the third invocation of `F` creates a zero-element `int[]` and passes that instance as a value parameter.</span></span> <span data-ttu-id="c51c7-844">Второй и третий вызовы будут точными эквивалентами записи:</span><span class="sxs-lookup"><span data-stu-id="c51c7-844">The second and third invocations are precisely equivalent to writing:</span></span>
```csharp
F(new int[] {10, 20, 30, 40});
F(new int[] {});
```

<span data-ttu-id="c51c7-845">При разрешении перегрузки метода массив параметров могут применяться в нормальной форме или в расширенной форме ([применимого члена функции](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-845">When performing overload resolution, a method with a parameter array may be applicable either in its normal form or in its expanded form ([Applicable function member](expressions.md#applicable-function-member)).</span></span> <span data-ttu-id="c51c7-846">Расширенную форму метод доступен только в том случае, если обычной формой метод не применим и только в том случае, если метод применимо с ту же сигнатуру, что расширенная форма уже не объявлен в тот же тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-846">The expanded form of a method is available only if the normal form of the method is not applicable and only if an applicable method with the same signature as the expanded form is not already declared in the same type.</span></span>

<span data-ttu-id="c51c7-847">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-847">The example</span></span>
```csharp
using System;

class Test
{
    static void F(params object[] a) {
        Console.WriteLine("F(object[])");
    }

    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object a0, object a1) {
        Console.WriteLine("F(object,object)");
    }

    static void Main() {
        F();
        F(1);
        F(1, 2);
        F(1, 2, 3);
        F(1, 2, 3, 4);
    }
}
```
<span data-ttu-id="c51c7-848">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-848">produces the output</span></span>
```
F();
F(object[]);
F(object,object);
F(object[]);
F(object[]);
```

<span data-ttu-id="c51c7-849">В примере две из возможных расширенных видов метода с массивом параметров уже включены в класс как обычные методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-849">In the example, two of the possible expanded forms of the method with a parameter array are already included in the class as regular methods.</span></span> <span data-ttu-id="c51c7-850">Эти развернутой форм таким образом не учитываются при разрешении перегрузки и вызовы методов первый и третий таким образом выберите обычные методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-850">These expanded forms are therefore not considered when performing overload resolution, and the first and third method invocations thus select the regular methods.</span></span> <span data-ttu-id="c51c7-851">Когда класс объявляет метод с массивом параметров, нередко включают и некоторые расширенные формы как обычные методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-851">When a class declares a method with a parameter array, it is not uncommon to also include some of the expanded forms as regular methods.</span></span> <span data-ttu-id="c51c7-852">В результате можно избежать размещения массива вызывается экземпляр, который возникает при вызове расширенной формы метода массив параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-852">By doing so it is possible to avoid the allocation of an array instance that occurs when an expanded form of a method with a parameter array is invoked.</span></span>

<span data-ttu-id="c51c7-853">Если тип массива параметров — `object[]`, возникает потенциальная неоднозначность между обычной формой метода и расширенной формами для одного `object` параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-853">When the type of a parameter array is `object[]`, a potential ambiguity arises between the normal form of the method and the expended form for a single `object` parameter.</span></span> <span data-ttu-id="c51c7-854">Неоднозначность связано, `object[]` сам является неявно преобразовать в тип `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-854">The reason for the ambiguity is that an `object[]` is itself implicitly convertible to type `object`.</span></span> <span data-ttu-id="c51c7-855">Неоднозначность нормально, тем не менее, так как может быть разрешена с помощью приведения, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="c51c7-855">The ambiguity presents no problem, however, since it can be resolved by inserting a cast if needed.</span></span>

<span data-ttu-id="c51c7-856">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-856">The example</span></span>
```csharp
using System;

class Test
{
    static void F(params object[] args) {
        foreach (object o in args) {
            Console.Write(o.GetType().FullName);
            Console.Write(" ");
        }
        Console.WriteLine();
    }

    static void Main() {
        object[] a = {1, "Hello", 123.456};
        object o = a;
        F(a);
        F((object)a);
        F(o);
        F((object[])o);
    }
}
```
<span data-ttu-id="c51c7-857">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-857">produces the output</span></span>
```
System.Int32 System.String System.Double
System.Object[]
System.Object[]
System.Int32 System.String System.Double
```

<span data-ttu-id="c51c7-858">В первый и последний вызовы `F`, обычной формой `F` применяется, так как существует неявное преобразование из типа аргумента в тип параметра (оба имеют тип `object[]`).</span><span class="sxs-lookup"><span data-stu-id="c51c7-858">In the first and last invocations of `F`, the normal form of `F` is applicable because an implicit conversion exists from the argument type to the parameter type (both are of type `object[]`).</span></span> <span data-ttu-id="c51c7-859">Таким образом, механизм разрешения перегрузок выбирает обычной формой `F`, и аргумент, переданный как параметр регулярных значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-859">Thus, overload resolution selects the normal form of `F`, and the argument is passed as a regular value parameter.</span></span> <span data-ttu-id="c51c7-860">На второй и третий вызовы, обычной формой `F` неприменима, так как существует не неявное преобразование из типа аргумента в тип параметра (тип `object` не может быть неявно преобразован в тип `object[]`).</span><span class="sxs-lookup"><span data-stu-id="c51c7-860">In the second and third invocations, the normal form of `F` is not applicable because no implicit conversion exists from the argument type to the parameter type (type `object` cannot be implicitly converted to type `object[]`).</span></span> <span data-ttu-id="c51c7-861">Однако расширенную форму `F` применим, поэтому выбирается при разрешении перегрузки.</span><span class="sxs-lookup"><span data-stu-id="c51c7-861">However, the expanded form of `F` is applicable, so it is selected by overload resolution.</span></span> <span data-ttu-id="c51c7-862">В результате одного элемента `object[]` создается путем вызова, и единственный элемент массива инициализируется со значением данного аргумента (который сам является ссылкой на `object[]`).</span><span class="sxs-lookup"><span data-stu-id="c51c7-862">As a result, a one-element `object[]` is created by the invocation, and the single element of the array is initialized with the given argument value (which itself is a reference to an `object[]`).</span></span>

### <a name="static-and-instance-methods"></a><span data-ttu-id="c51c7-863">Статические методы и методы экземпляра</span><span class="sxs-lookup"><span data-stu-id="c51c7-863">Static and instance methods</span></span>

<span data-ttu-id="c51c7-864">Если объявление метода содержит `static` модификатора, что метод является статическим методом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-864">When a method declaration includes a `static` modifier, that method is said to be a static method.</span></span> <span data-ttu-id="c51c7-865">Если аргумент `static` модификатора, считается, что метод является методом экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-865">When no `static` modifier is present, the method is said to be an instance method.</span></span>

<span data-ttu-id="c51c7-866">Статический метод не работает в определенном экземпляре, и это ошибка времени компиляции для ссылки на `this` в статическом методе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-866">A static method does not operate on a specific instance, and it is a compile-time error to refer to `this` in a static method.</span></span>

<span data-ttu-id="c51c7-867">Метод экземпляра работает на данном экземпляре класса, и этот экземпляр может быть доступен как `this` ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-867">An instance method operates on a given instance of a class, and that instance can be accessed as `this` ([This access](expressions.md#this-access)).</span></span>

<span data-ttu-id="c51c7-868">Если ссылка на метод в *member_access* ([доступ к членам](expressions.md#member-access)) формы `E.M`, если `M` — это статический метод `E` необходимо обозначить тип, содержащий `M`и если `M` является методом экземпляра `E` должно означать экземпляр типа, содержащего `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-868">When a method is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static method, `E` must denote a type containing `M`, and if `M` is an instance method, `E` must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="c51c7-869">Различия между статическими и члены экземпляра рассматриваются далее в [экземпляра и статические члены](classes.md#static-and-instance-members).</span><span class="sxs-lookup"><span data-stu-id="c51c7-869">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="virtual-methods"></a><span data-ttu-id="c51c7-870">Виртуальные методы</span><span class="sxs-lookup"><span data-stu-id="c51c7-870">Virtual methods</span></span>

<span data-ttu-id="c51c7-871">Если объявление метода экземпляра включает `virtual` модификатора, что метод является виртуальным методом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-871">When an instance method declaration includes a `virtual` modifier, that method is said to be a virtual method.</span></span> <span data-ttu-id="c51c7-872">Если аргумент `virtual` модификатора, считается, что метод является невиртуальный метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-872">When no `virtual` modifier is present, the method is said to be a non-virtual method.</span></span>

<span data-ttu-id="c51c7-873">Реализация невиртуальный метод является инвариантным: это та же реализация ли метод вызван на экземпляр класса, в котором он объявлен, или экземпляр производного класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-873">The implementation of a non-virtual method is invariant: The implementation is the same whether the method is invoked on an instance of the class in which it is declared or an instance of a derived class.</span></span> <span data-ttu-id="c51c7-874">Напротив производные классы могут быть заменены реализацию виртуального метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-874">In contrast, the implementation of a virtual method can be superseded by derived classes.</span></span> <span data-ttu-id="c51c7-875">Процесс замены реализации унаследованного виртуального метода называется ***переопределение*** этого метода ([переопределять методы](classes.md#override-methods)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-875">The process of superseding the implementation of an inherited virtual method is known as ***overriding*** that method ([Override methods](classes.md#override-methods)).</span></span>

<span data-ttu-id="c51c7-876">При вызове виртуального метода ***тип времени выполнения*** экземпляра, для которой вызов занимает место определяет фактическую реализацию метода для вызова.</span><span class="sxs-lookup"><span data-stu-id="c51c7-876">In a virtual method invocation, the ***run-time type*** of the instance for which that invocation takes place determines the actual method implementation to invoke.</span></span> <span data-ttu-id="c51c7-877">При вызове невиртуального метода ***типов во время компиляции*** экземпляра является определяющим фактором.</span><span class="sxs-lookup"><span data-stu-id="c51c7-877">In a non-virtual method invocation, the ***compile-time type*** of the instance is the determining factor.</span></span> <span data-ttu-id="c51c7-878">Точнее говоря, когда метод с именем `N` вызывается со списком аргументов `A` в экземпляре с типом времени компиляции `C` и типом времени выполнения `R` (где `R` либо `C` или класс, производный из `C`), вызов обрабатывается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c51c7-878">In precise terms, when a method named `N` is invoked with an argument list `A` on an instance with a compile-time type `C` and a run-time type `R` (where `R` is either `C` or a class derived from `C`), the invocation is processed as follows:</span></span>

*  <span data-ttu-id="c51c7-879">Во-первых, разрешение перегрузки применяется к `C`, `N`, и `A`, чтобы выбрать конкретный метод `M` из набора методов, объявленных и наследуются `C`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-879">First, overload resolution is applied to `C`, `N`, and `A`, to select a specific method `M` from the set of methods declared in and inherited by `C`.</span></span> <span data-ttu-id="c51c7-880">Это описывается в [вызовы методов](expressions.md#method-invocations).</span><span class="sxs-lookup"><span data-stu-id="c51c7-880">This is described in [Method invocations](expressions.md#method-invocations).</span></span>
*  <span data-ttu-id="c51c7-881">Затем, если `M` — это невиртуальный метод `M` вызывается.</span><span class="sxs-lookup"><span data-stu-id="c51c7-881">Then, if `M` is a non-virtual method, `M` is invoked.</span></span>
*  <span data-ttu-id="c51c7-882">В противном случае `M` является виртуальным методом и наиболее производный реализация `M` по отношению к `R` вызывается.</span><span class="sxs-lookup"><span data-stu-id="c51c7-882">Otherwise, `M` is a virtual method, and the most derived implementation of `M` with respect to `R` is invoked.</span></span>

<span data-ttu-id="c51c7-883">Для каждого виртуального метода, объявленные в или наследуемого классом, существует ***самый производный реализации*** метода по отношению к этому классу.</span><span class="sxs-lookup"><span data-stu-id="c51c7-883">For every virtual method declared in or inherited by a class, there exists a ***most derived implementation*** of the method with respect to that class.</span></span> <span data-ttu-id="c51c7-884">Наиболее производный реализацию виртуального метода `M` по отношению к класс `R` определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c51c7-884">The most derived implementation of a virtual method `M` with respect to a class `R` is determined as follows:</span></span>

*  <span data-ttu-id="c51c7-885">Если `R` содержит общие сведения о `virtual` объявление `M`, то это наиболее производный реализация `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-885">If `R` contains the introducing `virtual` declaration of `M`, then this is the most derived implementation of `M`.</span></span>
*  <span data-ttu-id="c51c7-886">В противном случае, если `R` содержит `override` из `M`, то это наиболее производный реализация `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-886">Otherwise, if `R` contains an `override` of `M`, then this is the most derived implementation of `M`.</span></span>
*  <span data-ttu-id="c51c7-887">В противном случае наиболее производный реализация `M` по отношению к `R` совпадает со значением в наиболее производного метода `M` по отношению к прямой базовый класс для `R`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-887">Otherwise, the most derived implementation of `M` with respect to `R` is the same as the most derived implementation of `M` with respect to the direct base class of `R`.</span></span>

<span data-ttu-id="c51c7-888">В следующем примере показано различия между виртуальные и невиртуальные методы:</span><span class="sxs-lookup"><span data-stu-id="c51c7-888">The following example illustrates the differences between virtual and non-virtual methods:</span></span>
```csharp
using System;

class A
{
    public void F() { Console.WriteLine("A.F"); }

    public virtual void G() { Console.WriteLine("A.G"); }
}

class B: A
{
    new public void F() { Console.WriteLine("B.F"); }

    public override void G() { Console.WriteLine("B.G"); }
}

class Test
{
    static void Main() {
        B b = new B();
        A a = b;
        a.F();
        b.F();
        a.G();
        b.G();
    }
}
```

<span data-ttu-id="c51c7-889">В примере `A` представляет невиртуальный метод `F` и виртуальный метод `G`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-889">In the example, `A` introduces a non-virtual method `F` and a virtual method `G`.</span></span> <span data-ttu-id="c51c7-890">Класс `B` появился новый невиртуальный метод `F`, таким образом скрытие наследуемых `F`, а также переопределяет унаследованный метод `G`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-890">The class `B` introduces a new non-virtual method `F`, thus hiding the inherited `F`, and also overrides the inherited method `G`.</span></span> <span data-ttu-id="c51c7-891">В примере получался результат:</span><span class="sxs-lookup"><span data-stu-id="c51c7-891">The example produces the output:</span></span>
```
A.F
B.F
B.G
B.G
```

<span data-ttu-id="c51c7-892">Обратите внимание, что инструкция `a.G()` вызывает `B.G`, а не `A.G`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-892">Notice that the statement `a.G()` invokes `B.G`, not `A.G`.</span></span> <span data-ttu-id="c51c7-893">Это, так как тип времени выполнения экземпляра (который является `B`), не во время компиляции тип экземпляра (который является `A`), определяет фактическую реализацию метода для вызова.</span><span class="sxs-lookup"><span data-stu-id="c51c7-893">This is because the run-time type of the instance (which is `B`), not the compile-time type of the instance (which is `A`), determines the actual method implementation to invoke.</span></span>

<span data-ttu-id="c51c7-894">Поскольку методы разрешено скрывать унаследованные методы, класс может содержать несколько виртуальных методов с одинаковыми сигнатурами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-894">Because methods are allowed to hide inherited methods, it is possible for a class to contain several virtual methods with the same signature.</span></span> <span data-ttu-id="c51c7-895">При этом не возникает проблема неоднозначности, так как все, кроме самый производный метод скрыты.</span><span class="sxs-lookup"><span data-stu-id="c51c7-895">This does not present an ambiguity problem, since all but the most derived method are hidden.</span></span> <span data-ttu-id="c51c7-896">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-896">In the example</span></span>
```csharp
using System;

class A
{
    public virtual void F() { Console.WriteLine("A.F"); }
}

class B: A
{
    public override void F() { Console.WriteLine("B.F"); }
}

class C: B
{
    new public virtual void F() { Console.WriteLine("C.F"); }
}

class D: C
{
    public override void F() { Console.WriteLine("D.F"); }
}

class Test
{
    static void Main() {
        D d = new D();
        A a = d;
        B b = d;
        C c = d;
        a.F();
        b.F();
        c.F();
        d.F();
    }
}
```
<span data-ttu-id="c51c7-897">`C` и `D` классы содержат два виртуальных метода с одинаковыми сигнатурами: один представлен `A` , а второй — с `C`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-897">the `C` and `D` classes contain two virtual methods with the same signature: The one introduced by `A` and the one introduced by `C`.</span></span> <span data-ttu-id="c51c7-898">Метод, представленный `C` скрывает метод, унаследованный от `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-898">The method introduced by `C` hides the method inherited from `A`.</span></span> <span data-ttu-id="c51c7-899">Таким образом, объявление переопределения в `D` переопределяет метод, представленный `C`, и он не поддерживается для `D` в Переопределите метод, представленный `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-899">Thus, the override declaration in `D` overrides the method introduced by `C`, and it is not possible for `D` to override the method introduced by `A`.</span></span> <span data-ttu-id="c51c7-900">В примере получался результат:</span><span class="sxs-lookup"><span data-stu-id="c51c7-900">The example produces the output:</span></span>
```
B.F
B.F
D.F
D.F
```

<span data-ttu-id="c51c7-901">Обратите внимание, что можно вызвать скрытые виртуальный метод путем обращения к экземпляру `D` через менее производный тип, в котором метод не скрыт.</span><span class="sxs-lookup"><span data-stu-id="c51c7-901">Note that it is possible to invoke the hidden virtual method by accessing an instance of `D` through a less derived type in which the method is not hidden.</span></span>

### <a name="override-methods"></a><span data-ttu-id="c51c7-902">Переопределение методов</span><span class="sxs-lookup"><span data-stu-id="c51c7-902">Override methods</span></span>

<span data-ttu-id="c51c7-903">Если объявление метода экземпляра включает `override` модификатор, метод считается ***переопределить метод***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-903">When an instance method declaration includes an `override` modifier, the method is said to be an ***override method***.</span></span> <span data-ttu-id="c51c7-904">Метод переопределяет унаследованный виртуальный метод с такой же сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-904">An override method overrides an inherited virtual method with the same signature.</span></span> <span data-ttu-id="c51c7-905">Изначальное объявление виртуального метода создает новый метод, а переопределение этого метода создает специализированный виртуальный метод с новой реализацией взамен унаследованного виртуального метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-905">Whereas a virtual method declaration introduces a new method, an override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.</span></span>

<span data-ttu-id="c51c7-906">Метод переопределяется `override` объявление называется ***переопределенным базовым методом***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-906">The method overridden by an `override` declaration is known as the ***overridden base method***.</span></span> <span data-ttu-id="c51c7-907">Для переопределения метода `M` объявлять в классе `C`, переопределенный базовый метод определяется путем проверки каждого типа базового класса `C`, начиная с типом прямой базовый класс `C` и продолжая с каждым последовательных Тип прямой базовый класс, до в типе некоторого базового класса находится по крайней мере один доступный метод является, который имеет ту же сигнатуру, что `M` после подстановки аргументов типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-907">For an override method `M` declared in a class `C`, the overridden base method is determined by examining each base class type of `C`, starting with the direct base class type of `C` and continuing with each successive direct base class type, until in a given base class type at least one accessible method is located which has the same signature as `M` after substitution of type arguments.</span></span> <span data-ttu-id="c51c7-908">В целях обнаружения переопределенным базовым методом, метод считается доступным, если это `public`, если оно уже `protected`, если оно уже `protected internal`, или если это `internal` и объявленные в той же программе, как `C`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-908">For the purposes of locating the overridden base method, a method is considered accessible if it is `public`, if it is `protected`, if it is `protected internal`, or if it is `internal` and declared in the same program as `C`.</span></span>

<span data-ttu-id="c51c7-909">Если не выполняются все следующие условия для объявления переопределения, возникает ошибка времени компиляции:</span><span class="sxs-lookup"><span data-stu-id="c51c7-909">A compile-time error occurs unless all of the following are true for an override declaration:</span></span>

*  <span data-ttu-id="c51c7-910">Переопределенный базовый метод может быть размещена в том случае, как описано выше.</span><span class="sxs-lookup"><span data-stu-id="c51c7-910">An overridden base method can be located as described above.</span></span>
*  <span data-ttu-id="c51c7-911">Имеется ровно один переопределенный базовый метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-911">There is exactly one such overridden base method.</span></span> <span data-ttu-id="c51c7-912">Это ограничение действует только в том случае, если тип базового класса — сконструированный тип, в котором подстановки аргументов типа обеспечивает сигнатуры двух методов же.</span><span class="sxs-lookup"><span data-stu-id="c51c7-912">This restriction has effect only if the base class type is a constructed type where the substitution of type arguments makes the signature of two methods the same.</span></span>
*  <span data-ttu-id="c51c7-913">Переопределенный базовый метод является виртуальным, абстрактным или переопределять метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-913">The overridden base method is a virtual, abstract, or override method.</span></span> <span data-ttu-id="c51c7-914">Другими словами переопределенный базовый метод не может быть статическим или невиртуальный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-914">In other words, the overridden base method cannot be static or non-virtual.</span></span>
*  <span data-ttu-id="c51c7-915">Переопределенный базовый метод не является запечатанным методом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-915">The overridden base method is not a sealed method.</span></span>
*  <span data-ttu-id="c51c7-916">Метод переопределения и переопределенным базовым методом имеют тот же тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-916">The override method and the overridden base method have the same return type.</span></span>
*  <span data-ttu-id="c51c7-917">Объявление переопределения и переопределенным базовым методом имеют же объявленный уровень доступности.</span><span class="sxs-lookup"><span data-stu-id="c51c7-917">The override declaration and the overridden base method have the same declared accessibility.</span></span> <span data-ttu-id="c51c7-918">Другими словами объявление переопределения не может изменить доступность виртуального метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-918">In other words, an override declaration cannot change the accessibility of the virtual method.</span></span> <span data-ttu-id="c51c7-919">Тем не менее если переопределенный базовый метод protected internal, и он объявлен в другой сборке, не объявленные сборки, содержащей метод переопределения, а затем метод переопределения должны быть защищены специальных возможностей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-919">However, if the overridden base method is protected internal and it is declared in a different assembly than the assembly containing the override method then the override method's declared accessibility must be protected.</span></span>
*  <span data-ttu-id="c51c7-920">Объявление переопределения не задает тип параметра — ограничения предложения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-920">The override declaration does not specify type-parameter-constraints-clauses.</span></span> <span data-ttu-id="c51c7-921">Вместо этого ограничения наследуются от переопределенным базовым методом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-921">Instead the constraints are inherited from the overridden base method.</span></span> <span data-ttu-id="c51c7-922">Обратите внимание на то, что ограничения, которые являются параметрами типа в переопределенном методе может быть заменен аргументы типа в унаследованном ограничении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-922">Note that constraints that are type parameters in the overridden method may be replaced by type arguments in the inherited constraint.</span></span> <span data-ttu-id="c51c7-923">Это может привести к ограничениям, которые не являются законными при явном задании, например типы значений или запечатанные типы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-923">This can lead to constraints that are not legal when explicitly specified, such as value types or sealed types.</span></span>

<span data-ttu-id="c51c7-924">В следующем примере показано, как работают правил переопределения для универсальных классов:</span><span class="sxs-lookup"><span data-stu-id="c51c7-924">The following example demonstrates how the overriding rules work for generic classes:</span></span>
```csharp
abstract class C<T>
{
    public virtual T F() {...}
    public virtual C<T> G() {...}
    public virtual void H(C<T> x) {...}
}

class D: C<string>
{
    public override string F() {...}            // Ok
    public override C<string> G() {...}         // Ok
    public override void H(C<T> x) {...}        // Error, should be C<string>
}

class E<T,U>: C<U>
{
    public override U F() {...}                 // Ok
    public override C<U> G() {...}              // Ok
    public override void H(C<T> x) {...}        // Error, should be C<U>
}
```

<span data-ttu-id="c51c7-925">Объявление переопределения доступны переопределенным базовым методом с помощью *base_access* ([базового доступа](expressions.md#base-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-925">An override declaration can access the overridden base method using a *base_access* ([Base access](expressions.md#base-access)).</span></span> <span data-ttu-id="c51c7-926">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-926">In the example</span></span>
```csharp
class A
{
    int x;

    public virtual void PrintFields() {
        Console.WriteLine("x = {0}", x);
    }
}

class B: A
{
    int y;

    public override void PrintFields() {
        base.PrintFields();
        Console.WriteLine("y = {0}", y);
    }
}
```
<span data-ttu-id="c51c7-927">`base.PrintFields()` вызова в `B` вызывает `PrintFields` метод объявлен в `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-927">the `base.PrintFields()` invocation in `B` invokes the `PrintFields` method declared in `A`.</span></span> <span data-ttu-id="c51c7-928">Объект *base_access* отключает механизм виртуального вызова и просто рассматривает базовый метод как невиртуальный метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-928">A *base_access* disables the virtual invocation mechanism and simply treats the base method as a non-virtual method.</span></span> <span data-ttu-id="c51c7-929">Бы вызов `B` были записаны `((A)this).PrintFields()`, бы рекурсивно вызывать `PrintFields` метод объявлен в `B`, не объявлен в `A`, так как `PrintFields` является виртуальным и тип времени выполнения `((A)this)` — `B`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-929">Had the invocation in `B` been written `((A)this).PrintFields()`, it would recursively invoke the `PrintFields` method declared in `B`, not the one declared in `A`, since `PrintFields` is virtual and the run-time type of `((A)this)` is `B`.</span></span>

<span data-ttu-id="c51c7-930">Только включив `override` can модификатор метода переопределяющих другие методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-930">Only by including an `override` modifier can a method override another method.</span></span> <span data-ttu-id="c51c7-931">Во всех остальных случаях метод с сигнатурой унаследованный метод просто скрывает унаследованный метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-931">In all other cases, a method with the same signature as an inherited method simply hides the inherited method.</span></span> <span data-ttu-id="c51c7-932">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-932">In the example</span></span>
```csharp
class A
{
    public virtual void F() {}
}

class B: A
{
    public virtual void F() {}        // Warning, hiding inherited F()
}
```
<span data-ttu-id="c51c7-933">`F` метод в `B` не включает `override` модификатор и поэтому не переопределяет `F` метод в `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-933">the `F` method in `B` does not include an `override` modifier and therefore does not override the `F` method in `A`.</span></span> <span data-ttu-id="c51c7-934">Вместо этого `F` метод в `B` скрывает метод в `A`, и выводится предупреждение, поскольку объявление не содержит `new` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-934">Rather, the `F` method in `B` hides the method in `A`, and a warning is reported because the declaration does not include a `new` modifier.</span></span>

<span data-ttu-id="c51c7-935">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-935">In the example</span></span>
```csharp
class A
{
    public virtual void F() {}
}

class B: A
{
    new private void F() {}        // Hides A.F within body of B
}

class C: B
{
    public override void F() {}    // Ok, overrides A.F
}
```
<span data-ttu-id="c51c7-936">`F` метод в `B` скрывает виртуальный `F` метод наследуется от `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-936">the `F` method in `B` hides the virtual `F` method inherited from `A`.</span></span> <span data-ttu-id="c51c7-937">Так как новый `F` в `B` закрытый доступ к его область содержит только тело класса `B` и не распространяется на `C`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-937">Since the new `F` in `B` has private access, its scope only includes the class body of `B` and does not extend to `C`.</span></span> <span data-ttu-id="c51c7-938">Таким образом, объявление `F` в `C` допускается переопределение `F` наследуется от `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-938">Therefore, the declaration of `F` in `C` is permitted to override the `F` inherited from `A`.</span></span>

### <a name="sealed-methods"></a><span data-ttu-id="c51c7-939">Запечатанные методы</span><span class="sxs-lookup"><span data-stu-id="c51c7-939">Sealed methods</span></span>

<span data-ttu-id="c51c7-940">Если объявление метода экземпляра включает `sealed` модификатора, что метод считается ***запечатанные метод***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-940">When an instance method declaration includes a `sealed` modifier, that method is said to be a ***sealed method***.</span></span> <span data-ttu-id="c51c7-941">Если объявление метода экземпляра включает `sealed` модификатор, она должна также содержать `override` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-941">If an instance method declaration includes the  `sealed` modifier, it must also include the `override` modifier.</span></span> <span data-ttu-id="c51c7-942">Использование `sealed` модификатор препятствует дальнейшей переопределение метода производного класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-942">Use of the `sealed` modifier prevents a derived class from further overriding the method.</span></span>

<span data-ttu-id="c51c7-943">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-943">In the example</span></span>
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }

    public virtual void G() {
        Console.WriteLine("A.G");
    }
}

class B: A
{
    sealed override public void F() {
        Console.WriteLine("B.F");
    } 

    override public void G() {
        Console.WriteLine("B.G");
    } 
}

class C: B
{
    override public void G() {
        Console.WriteLine("C.G");
    } 
}
```
<span data-ttu-id="c51c7-944">Класс `B` предоставляет два переопределения методов: `F` метод, который имеет `sealed` модификатор и `G` метод, который не поддерживает.</span><span class="sxs-lookup"><span data-stu-id="c51c7-944">the class `B` provides two override methods: an `F` method that has the `sealed` modifier and a `G` method that does not.</span></span> <span data-ttu-id="c51c7-945">`B`на использование запечатанных `modifier` предотвращает `C` дальнейшей переопределять `F`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-945">`B`'s use of the sealed `modifier` prevents `C` from further overriding `F`.</span></span>

### <a name="abstract-methods"></a><span data-ttu-id="c51c7-946">Абстрактные методы</span><span class="sxs-lookup"><span data-stu-id="c51c7-946">Abstract methods</span></span>

<span data-ttu-id="c51c7-947">Если объявление метода экземпляра включает `abstract` модификатора, что метод считается ***абстрактный метод***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-947">When an instance method declaration includes an `abstract` modifier, that method is said to be an ***abstract method***.</span></span> <span data-ttu-id="c51c7-948">Несмотря на то, что абстрактный метод неявно является также виртуальный метод, он не может иметь модификатор `virtual`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-948">Although an abstract method is implicitly also a virtual method, it cannot have the modifier `virtual`.</span></span>

<span data-ttu-id="c51c7-949">Объявление абстрактного метода появился новый виртуальный метод, но не предоставляет реализацию этого метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-949">An abstract method declaration introduces a new virtual method but does not provide an implementation of that method.</span></span> <span data-ttu-id="c51c7-950">Вместо этого неабстрактные производные классы, обязаны предоставлять собственную реализацию путем переопределения этого метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-950">Instead, non-abstract derived classes are required to provide their own implementation by overriding that method.</span></span> <span data-ttu-id="c51c7-951">Так как абстрактный метод не предоставляет фактической реализации, *method_body* абстрактного метода состоит всего лишь из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-951">Because an abstract method provides no actual implementation, the *method_body* of an abstract method simply consists of a semicolon.</span></span>

<span data-ttu-id="c51c7-952">Объявления абстрактных методов допускаются только в абстрактных классах ([абстрактные классы](classes.md#abstract-classes)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-952">Abstract method declarations are only permitted in abstract classes ([Abstract classes](classes.md#abstract-classes)).</span></span>

<span data-ttu-id="c51c7-953">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-953">In the example</span></span>
```csharp
public abstract class Shape
{
    public abstract void Paint(Graphics g, Rectangle r);
}

public class Ellipse: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawEllipse(r);
    }
}

public class Box: Shape
{
    public override void Paint(Graphics g, Rectangle r) {
        g.DrawRect(r);
    }
}
```
<span data-ttu-id="c51c7-954">`Shape` класс определяет абстрактное представление объекта геометрической фигуры для рисования самого.</span><span class="sxs-lookup"><span data-stu-id="c51c7-954">the `Shape` class defines the abstract notion of a geometrical shape object that can paint itself.</span></span> <span data-ttu-id="c51c7-955">`Paint` Метод является абстрактным, так как нет смысл реализация по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-955">The `Paint` method is abstract because there is no meaningful default implementation.</span></span> <span data-ttu-id="c51c7-956">`Ellipse` И `Box` являются конкретными реализациями `Shape` реализаций.</span><span class="sxs-lookup"><span data-stu-id="c51c7-956">The `Ellipse` and `Box` classes are concrete `Shape` implementations.</span></span> <span data-ttu-id="c51c7-957">Так как эти классы являются не являющиеся абстрактными, должны переопределить `Paint` метод и предоставить фактическую реализацию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-957">Because these classes are non-abstract, they are required to override the `Paint` method and provide an actual implementation.</span></span>

<span data-ttu-id="c51c7-958">Произошла ошибка во время компиляции для *base_access* ([базового доступа](expressions.md#base-access)) для ссылки на абстрактный метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-958">It is a compile-time error for a *base_access* ([Base access](expressions.md#base-access)) to reference an abstract method.</span></span> <span data-ttu-id="c51c7-959">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-959">In the example</span></span>
```csharp
abstract class A
{
    public abstract void F();
}

class B: A
{
    public override void F() {
        base.F();                        // Error, base.F is abstract
    }
}
```
<span data-ttu-id="c51c7-960">выдается ошибка компиляции `base.F()` вызова, так как он ссылается на абстрактный метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-960">a compile-time error is reported for the `base.F()` invocation because it references an abstract method.</span></span>

<span data-ttu-id="c51c7-961">Объявление абстрактного метода может переопределить виртуальный метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-961">An abstract method declaration is permitted to override a virtual method.</span></span> <span data-ttu-id="c51c7-962">Это позволяет абстрактный класс для принудительной повторной реализации метода в производных классах и делает недоступным исходной реализации метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-962">This allows an abstract class to force re-implementation of the method in derived classes, and makes the original implementation of the method unavailable.</span></span> <span data-ttu-id="c51c7-963">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-963">In the example</span></span>
```csharp
using System;

class A
{
    public virtual void F() {
        Console.WriteLine("A.F");
    }
}

abstract class B: A
{
    public abstract override void F();
}

class C: B
{
    public override void F() {
        Console.WriteLine("C.F");
    }
}
```
<span data-ttu-id="c51c7-964">Класс `A` объявляет виртуальный метод класса `B` переопределяется в абстрактный метод, а класс `C` переопределяет абстрактный метод, чтобы предоставить собственную реализацию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-964">class `A` declares a virtual method, class `B` overrides this method with an abstract method, and class `C` overrides the abstract method to provide its own implementation.</span></span>

### <a name="external-methods"></a><span data-ttu-id="c51c7-965">Внешние методы</span><span class="sxs-lookup"><span data-stu-id="c51c7-965">External methods</span></span>

<span data-ttu-id="c51c7-966">Если объявление метода содержит `extern` модификатора, что метод считается ***внешнего метода***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-966">When a method declaration includes an `extern` modifier, that method is said to be an ***external method***.</span></span> <span data-ttu-id="c51c7-967">Внешние методы реализуются во внешней системе, обычно с помощью языка, отличного от C#.</span><span class="sxs-lookup"><span data-stu-id="c51c7-967">External methods are implemented externally, typically using a language other than C#.</span></span> <span data-ttu-id="c51c7-968">Поскольку объявление внешнего метода не предоставляет фактической реализации, *method_body* внешнего метода состоит всего лишь из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-968">Because an external method declaration provides no actual implementation, the *method_body* of an external method simply consists of a semicolon.</span></span> <span data-ttu-id="c51c7-969">Внешний метод не могут быть универсальными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-969">An external method may not be generic.</span></span>

<span data-ttu-id="c51c7-970">`extern` Модификатор обычно используется в сочетании с `DllImport` атрибут ([взаимодействие с компонентами COM и Win32](attributes.md#interoperation-with-com-and-win32-components)), позволяя внешние методы для реализации библиотеки DLL (библиотек динамической компоновки).</span><span class="sxs-lookup"><span data-stu-id="c51c7-970">The `extern` modifier is typically used in conjunction with a `DllImport` attribute ([Interoperation with COM and Win32 components](attributes.md#interoperation-with-com-and-win32-components)), allowing external methods to be implemented by DLLs (Dynamic Link Libraries).</span></span> <span data-ttu-id="c51c7-971">Среда выполнения может поддерживать другие механизмы, при котором могут быть предоставлены реализации внешних методов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-971">The execution environment may support other mechanisms whereby implementations of external methods can be provided.</span></span>

<span data-ttu-id="c51c7-972">Если внешний метод включает `DllImport` атрибут, в объявлении метода должен также содержать `static` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-972">When an external method includes a `DllImport` attribute, the method declaration must also include a `static` modifier.</span></span> <span data-ttu-id="c51c7-973">В этом примере демонстрируется использование `extern` модификатор и `DllImport` атрибут:</span><span class="sxs-lookup"><span data-stu-id="c51c7-973">This example demonstrates the use of the `extern` modifier and the `DllImport` attribute:</span></span>
```csharp
using System.Text;
using System.Security.Permissions;
using System.Runtime.InteropServices;

class Path
{
    [DllImport("kernel32", SetLastError=true)]
    static extern bool CreateDirectory(string name, SecurityAttribute sa);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool RemoveDirectory(string name);

    [DllImport("kernel32", SetLastError=true)]
    static extern int GetCurrentDirectory(int bufSize, StringBuilder buf);

    [DllImport("kernel32", SetLastError=true)]
    static extern bool SetCurrentDirectory(string name);
}
```

### <a name="partial-methods-recap"></a><span data-ttu-id="c51c7-974">Разделяемые методы (Обзор)</span><span class="sxs-lookup"><span data-stu-id="c51c7-974">Partial methods (recap)</span></span>

<span data-ttu-id="c51c7-975">Если объявление метода содержит `partial` модификатора, что метод считается ***разделяемого метода***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-975">When a method declaration includes a `partial` modifier, that method is said to be a ***partial method***.</span></span> <span data-ttu-id="c51c7-976">Разделяемые методы можно объявлять только как члены разделяемых типов ([разделяемых типов](classes.md#partial-types)) и их использование регулируется ряд ограничений.</span><span class="sxs-lookup"><span data-stu-id="c51c7-976">Partial methods can only be declared as members of partial types ([Partial types](classes.md#partial-types)), and are subject to a number of restrictions.</span></span> <span data-ttu-id="c51c7-977">Разделяемые методы более подробно описаны в [разделяемые методы](classes.md#partial-methods).</span><span class="sxs-lookup"><span data-stu-id="c51c7-977">Partial methods are further described in [Partial methods](classes.md#partial-methods).</span></span>

### <a name="extension-methods"></a><span data-ttu-id="c51c7-978">Методы расширения</span><span class="sxs-lookup"><span data-stu-id="c51c7-978">Extension methods</span></span>

<span data-ttu-id="c51c7-979">Если первый параметр метода содержит `this` модификатора, что метод считается ***метод расширения***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-979">When the first parameter of a method includes the `this` modifier, that method is said to be an ***extension method***.</span></span> <span data-ttu-id="c51c7-980">Методы расширения могут объявляться только в статических классах, не являющегося универсальным, невложенными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-980">Extension methods can only be declared in non-generic, non-nested static classes.</span></span> <span data-ttu-id="c51c7-981">Первый параметр метода расширения не может иметь модификаторы `this`, и тип параметра не может быть типом указателя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-981">The first parameter of an extension method can have no modifiers other than `this`, and the parameter type cannot be a pointer type.</span></span>

<span data-ttu-id="c51c7-982">Ниже приведен пример статического класса, который объявляет два метода расширения:</span><span class="sxs-lookup"><span data-stu-id="c51c7-982">The following is an example of a static class that declares two extension methods:</span></span>
```csharp
public static class Extensions
{
    public static int ToInt32(this string s) {
        return Int32.Parse(s);
    }

    public static T[] Slice<T>(this T[] source, int index, int count) {
        if (index < 0 || count < 0 || source.Length - index < count)
            throw new ArgumentException();
        T[] result = new T[count];
        Array.Copy(source, index, result, 0, count);
        return result;
    }
}
```

<span data-ttu-id="c51c7-983">Метод расширения — это обычный статический метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-983">An extension method is a regular static method.</span></span> <span data-ttu-id="c51c7-984">Кроме того, когда в области включающего его статистического класса, метод расширения может вызываться с помощью синтаксиса вызова метода экземпляра ([вызовы методов расширения](expressions.md#extension-method-invocations)), используя выражение получателя в качестве первого аргумента.</span><span class="sxs-lookup"><span data-stu-id="c51c7-984">In addition, where its enclosing static class is in scope, an extension method can be invoked using instance method invocation syntax ([Extension method invocations](expressions.md#extension-method-invocations)), using the receiver expression as the first argument.</span></span>

<span data-ttu-id="c51c7-985">В следующей программе используются методы расширения, объявленный над:</span><span class="sxs-lookup"><span data-stu-id="c51c7-985">The following program uses the extension methods declared above:</span></span>
```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in strings.Slice(1, 2)) {
            Console.WriteLine(s.ToInt32());
        }
    }
}
```

<span data-ttu-id="c51c7-986">`Slice` Метод доступен для `string[]`и `ToInt32` метод доступен для `string`, так как они были объявлены как методы расширения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-986">The `Slice` method is available on the `string[]`, and the `ToInt32` method is available on `string`, because they have been declared as extension methods.</span></span> <span data-ttu-id="c51c7-987">Значение программы совпадает со значением ниже, с использованием обычный статический метод:</span><span class="sxs-lookup"><span data-stu-id="c51c7-987">The meaning of the program is the same as the following, using ordinary static method calls:</span></span>
```csharp
static class Program
{
    static void Main() {
        string[] strings = { "1", "22", "333", "4444" };
        foreach (string s in Extensions.Slice(strings, 1, 2)) {
            Console.WriteLine(Extensions.ToInt32(s));
        }
    }
}
```

### <a name="method-body"></a><span data-ttu-id="c51c7-988">Тело метода</span><span class="sxs-lookup"><span data-stu-id="c51c7-988">Method body</span></span>

<span data-ttu-id="c51c7-989">*Method_body* метода объявление состоит из тело блока, тело выражения или точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-989">The *method_body* of a method declaration consists of either a block body, an expression body or a semicolon.</span></span>

<span data-ttu-id="c51c7-990">***Тип результата*** метода является `void` если возвращаемый тип — `void`, или если метод является асинхронным и возвращаемый тип — `System.Threading.Tasks.Task`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-990">The ***result type*** of a method is `void` if the return type is `void`, or if the method is async and the return type is `System.Threading.Tasks.Task`.</span></span> <span data-ttu-id="c51c7-991">В противном случае — тип результата метода синхронные — это тип его возвращаемого значения и тип результата асинхронного метода с типом возвращаемого значения `System.Threading.Tasks.Task<T>` является `T`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-991">Otherwise, the result type of a non-async method is its return type, and the result type of an async method with return type `System.Threading.Tasks.Task<T>` is `T`.</span></span>

<span data-ttu-id="c51c7-992">Если метод имеет `void` привести тип и тело блока, `return` инструкций ([оператор return](statements.md#the-return-statement)) в блоке не могут указать выражение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-992">When a method has a `void` result type and a block body, `return` statements ([The return statement](statements.md#the-return-statement)) in the block are not permitted to specify an expression.</span></span> <span data-ttu-id="c51c7-993">Обычно если завершения выполнения блока метода типа void (т. е. управление передается из конечной точки тела метода), этот метод просто возвращается вызвавшему ее текущей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-993">If execution of the block of a void method completes normally (that is, control flows off the end of the method body), that method simply returns to its current caller.</span></span>
    
<span data-ttu-id="c51c7-994">Если метод имеет `void` результат и тело выражения, выражения `E` должно быть *statement_expression*, и тело полностью эквивалентен тело блока формы `{ E; }`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-994">When a method has a `void` result and an expression body, the expression `E` must be a *statement_expression*, and the body is exactly equivalent to a block body of the form `{ E; }`.</span></span>
    
<span data-ttu-id="c51c7-995">Если метод имеет тип результата, отличный от void и блок текста, каждый `return` инструкции в блоке необходимо указать выражение, которое может быть неявно преобразован в тип результата.</span><span class="sxs-lookup"><span data-stu-id="c51c7-995">When a method has a non-void result type and a block body, each `return` statement in the block must specify an expression that is implicitly convertible to the result type.</span></span> <span data-ttu-id="c51c7-996">Конечная точка тело блока метода, возвращающего значение, не должен быть доступен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-996">The endpoint of a block body of a value-returning method must not be reachable.</span></span> <span data-ttu-id="c51c7-997">Другими словами в методе с тело блока, возвращающих значение, элемент управления не допускается для передачи из конечной точки тела метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-997">In other words, in a value-returning method with a block body, control is not permitted to flow off the end of the method body.</span></span>
    
<span data-ttu-id="c51c7-998">Если метод имеет тип результата, отличный от void и тело выражения, выражения должны неявно преобразовываться в тип результата и текст полностью эквивалентен тело блока формы `{ return E; }`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-998">When a method has a non-void result type and an expression body, the expression must be implicitly convertible to the result type, and the body is exactly equivalent to a block body of the form `{ return E; }`.</span></span>
    
<span data-ttu-id="c51c7-999">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-999">In the example</span></span>
```csharp
class A
{
    public int F() {}            // Error, return value required

    public int G() {
        return 1;
    }

    public int H(bool b) {
        if (b) {
            return 1;
        }
        else {
            return 0;
        }
    }

    public int I(bool b) => b ? 1 : 0;
}
```
<span data-ttu-id="c51c7-1000">Возвращает значение `F` метод приводит к ошибке времени компиляции, так как поток управления можно из конечной точки тела метода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1000">the value-returning `F` method results in a compile-time error because control can flow off the end of the method body.</span></span> <span data-ttu-id="c51c7-1001">`G` И `H` методы верны, так как все возможные пути выполнения в оператор return, который указывает возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1001">The `G` and `H` methods are correct because all possible execution paths end in a return statement that specifies a return value.</span></span> <span data-ttu-id="c51c7-1002">`I` Метод указан правильно, поскольку его основной части эквивалентен блока инструкций с помощью только один оператор return в нем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1002">The `I` method is correct, because its body is equivalent to a statement block with just a single return statement in it.</span></span>

### <a name="method-overloading"></a><span data-ttu-id="c51c7-1003">Перегрузка методов</span><span class="sxs-lookup"><span data-stu-id="c51c7-1003">Method overloading</span></span>

<span data-ttu-id="c51c7-1004">Правила разрешения перегрузки метода описаны в [вывод типа](expressions.md#type-inference).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1004">The method overload resolution rules are described in [Type inference](expressions.md#type-inference).</span></span>

## <a name="properties"></a><span data-ttu-id="c51c7-1005">Свойства</span><span class="sxs-lookup"><span data-stu-id="c51c7-1005">Properties</span></span>

<span data-ttu-id="c51c7-1006">Объект ***свойство*** является членом, который предоставляет доступ к характеристикам объекта или класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1006">A ***property*** is a member that provides access to a characteristic of an object or a class.</span></span> <span data-ttu-id="c51c7-1007">Примеры свойств включают длину строки, размер шрифта, заголовок окна, имя клиента и так далее.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1007">Examples of properties include the length of a string, the size of a font, the caption of a window, the name of a customer, and so on.</span></span> <span data-ttu-id="c51c7-1008">Свойства являются естественным расширением полей — другие являются именованными членами со связанными типами и используется одинаковый синтаксис для доступа к полям и свойствам.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1008">Properties are a natural extension of fields—both are named members with associated types, and the syntax for accessing fields and properties is the same.</span></span> <span data-ttu-id="c51c7-1009">Однако свойства, в отличие от полей, не указывают места хранения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1009">However, unlike fields, properties do not denote storage locations.</span></span> <span data-ttu-id="c51c7-1010">Вместо этого свойства содержат ***методы доступа***, в которых описаны инструкции для выполнения при чтении или записи значений.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1010">Instead, properties have ***accessors*** that specify the statements to be executed when their values are read or written.</span></span> <span data-ttu-id="c51c7-1011">Свойства таким образом предоставляют механизм для связи действия с считывать и записывать атрибуты объекта; Кроме того разрешают такие атрибуты нужно вычислить.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1011">Properties thus provide a mechanism for associating actions with the reading and writing of an object's attributes; furthermore, they permit such attributes to be computed.</span></span>

<span data-ttu-id="c51c7-1012">Свойства объявляются с помощью *property_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1012">Properties are declared using *property_declaration*s:</span></span>

```antlr
property_declaration
    : attributes? property_modifier* type member_name property_body
    ;

property_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | property_modifier_unsafe
    ;

property_body
    : '{' accessor_declarations '}' property_initializer?
    | '=>' expression ';'
    ;

property_initializer
    : '=' variable_initializer ';'
    ;
```

<span data-ttu-id="c51c7-1013">Объект *property_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)) и является допустимой комбинацией четырех модификаторов доступа ([модификаторы доступа ](classes.md#access-modifiers)), `new` ([Модификатор new](classes.md#the-new-modifier)), `static` ([экземпляра и статические методы](classes.md#static-and-instance-methods)), `virtual` ([виртуальных методов](classes.md#virtual-methods)), `override` ([Переопределять методы](classes.md#override-methods)), `sealed` ([запечатанные методы](classes.md#sealed-methods)), `abstract` ([абстрактные методы](classes.md#abstract-methods)), и `extern` ([Внешние методы](classes.md#external-methods)) модификаторы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1013">A *property_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)),  `static` ([Static and instance methods](classes.md#static-and-instance-methods)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="c51c7-1014">Объявления свойств подчиняются тем же правилам, что и объявления методов ([методы](classes.md#methods)) по отношению к допустимые сочетания модификаторов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1014">Property declarations are subject to the same rules as method declarations ([Methods](classes.md#methods)) with regard to valid combinations of modifiers.</span></span>

<span data-ttu-id="c51c7-1015">*Тип* свойства объявление указывает тип свойства, представленные этим определением и *member_name* указывает имя свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1015">The *type* of a property declaration specifies the type of the property introduced by the declaration, and the *member_name* specifies the name of the property.</span></span> <span data-ttu-id="c51c7-1016">Если свойство не явная реализация члена интерфейса, *member_name* является просто *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1016">Unless the property is an explicit interface member implementation, the *member_name* is simply an *identifier*.</span></span> <span data-ttu-id="c51c7-1017">Для явной реализации члена интерфейса ([явные реализации члена интерфейса](interfaces.md#explicit-interface-member-implementations)), *member_name* состоит из *interface_type* следуют " `.`"и *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1017">For an explicit interface member implementation ([Explicit interface member implementations](interfaces.md#explicit-interface-member-implementations)), the *member_name* consists of an *interface_type* followed by a "`.`" and an *identifier*.</span></span>

<span data-ttu-id="c51c7-1018">*Тип* свойства должно быть по крайней мере такой же уровень доступности, как и само свойство ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1018">The *type* of a property must be at least as accessible as the property itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-1019">Объект *property_body* может либо состоять из ***тела метода доступа*** или ***тело выражения***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1019">A *property_body* may either consist of an ***accessor body*** or an ***expression body***.</span></span> <span data-ttu-id="c51c7-1020">В тело метода доступа *accessor_declarations*, которые должны быть заключены в "`{`«и»`}`" токены, объявите методы доступа ([методы доступа](classes.md#accessors)) свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1020">In an accessor body,  *accessor_declarations*, which must be enclosed in "`{`" and "`}`" tokens, declare the accessors ([Accessors](classes.md#accessors)) of the property.</span></span> <span data-ttu-id="c51c7-1021">Методы доступа укажите исполняемые операторы, связанные с чтением и записью свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1021">The accessors specify the executable statements associated with reading and writing the property.</span></span>

<span data-ttu-id="c51c7-1022">Тело выражения, состоящий из `=>` следуют *выражение* `E` и точку с запятой полностью эквивалентен тела оператора `{ get { return E; } }`и поэтому только можно указать только для считывания свойства, где результат метод считывания задается с помощью одного выражения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1022">An expression body consisting of `=>` followed by an *expression* `E` and a semicolon is exactly equivalent to the statement body `{ get { return E; } }`, and can therefore only be used to specify getter-only properties where the result of the getter is given by a single expression.</span></span>

<span data-ttu-id="c51c7-1023">Объект *property_initializer* может предоставляться только для автоматически реализованного свойства ([автоматически реализуемые свойства](classes.md#automatically-implemented-properties)) и приводит к инициализации базового поля таких свойства со значением, предоставленным выражением *выражение*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1023">A *property_initializer* may only be given for an automatically implemented property ([Automatically implemented properties](classes.md#automatically-implemented-properties)), and causes the initialization of the underlying field of such properties with the value given by the *expression*.</span></span>

<span data-ttu-id="c51c7-1024">Несмотря на то, что синтаксис доступ к свойству такой же, что и поле, свойство не классифицируется как переменная.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1024">Even though the syntax for accessing a property is the same as that for a field, a property is not classified as a variable.</span></span> <span data-ttu-id="c51c7-1025">Таким образом, он уже не сможете передать свойство в качестве `ref` или `out` аргумент.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1025">Thus, it is not possible to pass a property as a `ref` or `out` argument.</span></span>

<span data-ttu-id="c51c7-1026">Если объявление свойства содержит `extern` модификатор, свойство считается ***внешним свойством***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1026">When a property declaration includes an `extern` modifier, the property is said to be an ***external property***.</span></span> <span data-ttu-id="c51c7-1027">Поскольку объявление внешнего свойства не предоставляет фактической реализации, каждый из его *accessor_declarations* состоит из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1027">Because an external property declaration provides no actual implementation, each of its *accessor_declarations* consists of a semicolon.</span></span>

### <a name="static-and-instance-properties"></a><span data-ttu-id="c51c7-1028">Экземпляра и статические свойства</span><span class="sxs-lookup"><span data-stu-id="c51c7-1028">Static and instance properties</span></span>

<span data-ttu-id="c51c7-1029">Если объявление свойства содержит `static` модификатор, свойство считается ***статическое свойство***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1029">When a property declaration includes a `static` modifier, the property is said to be a ***static property***.</span></span> <span data-ttu-id="c51c7-1030">Если аргумент `static` модификатор присутствует, свойство считается ***свойства экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1030">When no `static` modifier is present, the property is said to be an ***instance property***.</span></span>

<span data-ttu-id="c51c7-1031">Статическое свойство не связан с конкретным экземпляром, и произошла ошибка во время компиляции, для ссылки на `this` в методах доступа статического свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1031">A static property is not associated with a specific instance, and it is a compile-time error to refer to `this` in the accessors of a static property.</span></span>

<span data-ttu-id="c51c7-1032">Свойство экземпляра связан с данным экземпляром класса, и этот экземпляр может быть доступен как `this` ([такой доступ](expressions.md#this-access)) в методах доступа этого свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1032">An instance property is associated with a given instance of a class, and that instance can be accessed as `this` ([This access](expressions.md#this-access)) in the accessors of that property.</span></span>

<span data-ttu-id="c51c7-1033">Если ссылка на свойство в *member_access* ([доступ к членам](expressions.md#member-access)) формы `E.M`, если `M` является статическим свойством, `E` необходимо обозначить тип, содержащий `M`и если `M` является свойством экземпляра, E должно означать экземпляр типа, содержащего `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1033">When a property is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static property, `E` must denote a type containing `M`, and if `M` is an instance property, E must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="c51c7-1034">Различия между статическими и члены экземпляра рассматриваются далее в [экземпляра и статические члены](classes.md#static-and-instance-members).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1034">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="accessors"></a><span data-ttu-id="c51c7-1035">Методы доступа</span><span class="sxs-lookup"><span data-stu-id="c51c7-1035">Accessors</span></span>

<span data-ttu-id="c51c7-1036">*Accessor_declarations* свойства укажите исполняемые операторы, связанные с чтением и записью этого свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1036">The *accessor_declarations* of a property specify the executable statements associated with reading and writing that property.</span></span>

```antlr
accessor_declarations
    : get_accessor_declaration set_accessor_declaration?
    | set_accessor_declaration get_accessor_declaration?
    ;

get_accessor_declaration
    : attributes? accessor_modifier? 'get' accessor_body
    ;

set_accessor_declaration
    : attributes? accessor_modifier? 'set' accessor_body
    ;

accessor_modifier
    : 'protected'
    | 'internal'
    | 'private'
    | 'protected' 'internal'
    | 'internal' 'protected'
    ;

accessor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="c51c7-1037">Объявления методов доступа состоят из *get_accessor_declaration*, *set_accessor_declaration*, или оба.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1037">The accessor declarations consist of a *get_accessor_declaration*, a *set_accessor_declaration*, or both.</span></span> <span data-ttu-id="c51c7-1038">Каждое объявление метода доступа состоит из маркера `get` или `set` следуют необязательный *accessor_modifier* и *accessor_body*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1038">Each accessor declaration consists of the token `get` or `set` followed by an optional *accessor_modifier* and an *accessor_body*.</span></span>

<span data-ttu-id="c51c7-1039">Использование *accessor_modifier*s регулируется следующими ограничениями:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1039">The use of *accessor_modifier*s is governed by the following restrictions:</span></span>

*  <span data-ttu-id="c51c7-1040">*Accessor_modifier* не может использоваться в интерфейсе или явной реализации члена интерфейса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1040">An *accessor_modifier* may not be used in an interface or in an explicit interface member implementation.</span></span>
*  <span data-ttu-id="c51c7-1041">Для свойства или индексатора, который не имеет `override` модификатор, *accessor_modifier* разрешался только в том случае, если свойство или индексатор имеет оба `get` и `set` метод доступа и применяется только к одному из них методы доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1041">For a property or indexer that has no `override` modifier, an *accessor_modifier* is permitted only if the property or indexer has both a `get` and `set` accessor, and then is permitted only on one of those accessors.</span></span>
*  <span data-ttu-id="c51c7-1042">Для свойства или индексатора, который включает в себя `override` , метод доступа должен соответствовать *accessor_modifier*, если таковое имеется, переопределение метода доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1042">For a property or indexer that includes an `override` modifier, an accessor must match the *accessor_modifier*, if any, of the accessor being overridden.</span></span>
*  <span data-ttu-id="c51c7-1043">*Accessor_modifier* должен объявлять, является более строгим, чем объявленный уровень доступности свойства или сам индексатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1043">The *accessor_modifier* must declare an accessibility that is strictly more restrictive than the declared accessibility of the property or indexer itself.</span></span> <span data-ttu-id="c51c7-1044">Точнее:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1044">To be precise:</span></span>
   * <span data-ttu-id="c51c7-1045">Если свойство или индексатор имеет объявленный уровень доступности `public`, *accessor_modifier* может быть либо `protected internal`, `internal`, `protected`, или `private`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1045">If the property or indexer has a declared accessibility of `public`, the *accessor_modifier* may be either `protected internal`, `internal`, `protected`, or `private`.</span></span>
   * <span data-ttu-id="c51c7-1046">Если свойство или индексатор имеет объявленный уровень доступности `protected internal`, *accessor_modifier* может быть либо `internal`, `protected`, или `private`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1046">If the property or indexer has a declared accessibility of `protected internal`, the *accessor_modifier* may be either `internal`, `protected`, or `private`.</span></span>
   * <span data-ttu-id="c51c7-1047">Если свойство или индексатор имеет объявленный уровень доступности `internal` или `protected`, *accessor_modifier* должно быть `private`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1047">If the property or indexer has a declared accessibility of `internal` or `protected`, the *accessor_modifier* must be `private`.</span></span>
   * <span data-ttu-id="c51c7-1048">Если свойство или индексатор имеет объявленный уровень доступности `private`, не *accessor_modifier* может использоваться.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1048">If the property or indexer has a declared accessibility of `private`, no *accessor_modifier* may be used.</span></span>

<span data-ttu-id="c51c7-1049">Для `abstract` и `extern` свойства, *accessor_body* для каждого метода доступа указан — только точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1049">For `abstract` and `extern` properties, the *accessor_body* for each accessor specified is simply a semicolon.</span></span> <span data-ttu-id="c51c7-1050">Не являющиеся абстрактными, или внешними свойства могут иметь каждый *accessor_body* быть точкой с запятой, в противном случае это ***автоматически реализованное свойство*** ([автоматически реализуемые свойства ](classes.md#automatically-implemented-properties)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1050">A non-abstract, non-extern property may have each *accessor_body* be a semicolon, in which case it is an ***automatically implemented property*** ([Automatically implemented properties](classes.md#automatically-implemented-properties)).</span></span> <span data-ttu-id="c51c7-1051">Автоматически реализуемого свойства должен иметь по крайней мере метод доступа get.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1051">An automatically implemented property must have at least a get accessor.</span></span> <span data-ttu-id="c51c7-1052">Для любого другого неабстрактного, или внешними свойства, методы доступа *accessor_body* — *блок* определяющий операторы, которые будут выполняться при вызове соответствующего метода доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1052">For the accessors of any other non-abstract, non-extern property, the *accessor_body* is a *block* which specifies the statements to be executed when the corresponding accessor is invoked.</span></span>

<span data-ttu-id="c51c7-1053">Объект `get` метод доступа соответствует оформляется как метод с возвращаемым значением типа свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1053">A `get` accessor corresponds to a parameterless method with a return value of the property type.</span></span> <span data-ttu-id="c51c7-1054">За исключением случаев, целевым объектом назначения, при ссылке на свойство в выражении, `get` для вычисления значения свойства вызывается метод доступа свойства ([значения выражений](expressions.md#values-of-expressions)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1054">Except as the target of an assignment, when a property is referenced in an expression, the `get` accessor of the property is invoked to compute the value of the property ([Values of expressions](expressions.md#values-of-expressions)).</span></span> <span data-ttu-id="c51c7-1055">Тело `get` доступа должны соответствовать правилам для возвращающих значения методов, описанных в [тело метода](classes.md#method-body).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1055">The body of a `get` accessor must conform to the rules for value-returning methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="c51c7-1056">В частности все `return` инструкции в теле `get` доступа необходимо указать выражение, которое может быть неявно преобразован в тип свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1056">In particular, all `return` statements in the body of a `get` accessor must specify an expression that is implicitly convertible to the property type.</span></span> <span data-ttu-id="c51c7-1057">Кроме того конечная точка `get` метод доступа не должен быть доступен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1057">Furthermore, the endpoint of a `get` accessor must not be reachable.</span></span>

<span data-ttu-id="c51c7-1058">Объект `set` соответствует методу с параметром одиночное значение типа свойства метода доступа и `void` тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1058">A `set` accessor corresponds to a method with a single value parameter of the property type and a `void` return type.</span></span> <span data-ttu-id="c51c7-1059">Неявный параметр `set` доступа всегда имеет имя `value`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1059">The implicit parameter of a `set` accessor is always named `value`.</span></span> <span data-ttu-id="c51c7-1060">Если ссылка на свойство как целевым объектом назначения ([операторы присваивания](expressions.md#assignment-operators)), или в качестве операнда `++` или `--` ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators), [ Префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)), `set` с аргументом вызывается метод доступа (значение которого равно правой части назначения или операнд `++` или `--` оператор), предоставляет новое значение ([простое присваивание](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1060">When a property is referenced as the target of an assignment ([Assignment operators](expressions.md#assignment-operators)), or as the operand of `++` or `--` ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators), [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)), the `set` accessor is invoked with an argument (whose value is that of the right-hand side of the assignment or the operand of the `++` or `--` operator) that provides the new value ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="c51c7-1061">Тело `set` доступа должны соответствовать правилам для `void` методов, описанных в [тело метода](classes.md#method-body).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1061">The body of a `set` accessor must conform to the rules for `void` methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="c51c7-1062">В частности `return` инструкций в `set` тела метода доступа не допускаются и ввести выражение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1062">In particular, `return` statements in the `set` accessor body are not permitted to specify an expression.</span></span> <span data-ttu-id="c51c7-1063">Так как `set` доступа неявно имеет параметр с именем `value`, произошла ошибка во время компиляции, для объявления локальной переменной или константы в `set` метод доступа, такое имя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1063">Since a `set` accessor implicitly has a parameter named `value`, it is a compile-time error for a local variable or constant declaration in a `set` accessor to have that name.</span></span>

<span data-ttu-id="c51c7-1064">Зависимости от наличия или отсутствия `get` и `set` методы доступа, свойство классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1064">Based on the presence or absence of the `get` and `set` accessors, a property is classified as follows:</span></span>

*  <span data-ttu-id="c51c7-1065">Свойство, которое включает в себя `get` метода доступа и `set` доступа считается ***чтения и записи*** свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1065">A property that includes both a `get` accessor and a `set` accessor is said to be a ***read-write*** property.</span></span>
*  <span data-ttu-id="c51c7-1066">Свойство, имеющее только `get` доступа считается ***только для чтения*** свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1066">A property that has only a `get` accessor is said to be a ***read-only*** property.</span></span> <span data-ttu-id="c51c7-1067">Это ошибка времени компиляции для свойства только для чтения в качестве целевого назначения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1067">It is a compile-time error for a read-only property to be the target of an assignment.</span></span>
*  <span data-ttu-id="c51c7-1068">Свойство, имеющее только `set` доступа считается ***только для записи*** свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1068">A property that has only a `set` accessor is said to be a ***write-only*** property.</span></span> <span data-ttu-id="c51c7-1069">За исключением того, что целевым объектом назначения, это ошибка времени компиляции для ссылки на свойство только для записи в выражении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1069">Except as the target of an assignment, it is a compile-time error to reference a write-only property in an expression.</span></span>

<span data-ttu-id="c51c7-1070">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1070">In the example</span></span>
```csharp
public class Button: Control
{
    private string caption;

    public string Caption {
        get {
            return caption;
        }
        set {
            if (caption != value) {
                caption = value;
                Repaint();
            }
        }
    }

    public override void Paint(Graphics g, Rectangle r) {
        // Painting code goes here
    }
}
```
<span data-ttu-id="c51c7-1071">`Button` управления объявляет открытое `Caption` свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1071">the `Button` control declares a public `Caption` property.</span></span> <span data-ttu-id="c51c7-1072">`get` Метод доступа `Caption` свойство возвращает строку, хранится в закрытом `caption` поля.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1072">The `get` accessor of the `Caption` property returns the string stored in the private `caption` field.</span></span> <span data-ttu-id="c51c7-1073">`set` Метод доступа, проверяет ли новое значение отличается от текущего значения, и если да, он сохраняет новое значение и обновляет элемент управления.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1073">The `set` accessor checks if the new value is different from the current value, and if so, it stores the new value and repaints the control.</span></span> <span data-ttu-id="c51c7-1074">Свойства часто следовать шаблону, приведенному выше: `get` доступа просто возвращает значение, хранящееся в скрытом поле и `set` доступа изменяет закрытого поля, а затем выполняет дополнительных действий, необходимых для полного обновления состояния объекта.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1074">Properties often follow the pattern shown above: The `get` accessor simply returns a value stored in a private field, and the `set` accessor modifies that private field and then performs any additional actions required to fully update the state of the object.</span></span>

<span data-ttu-id="c51c7-1075">Учитывая `Button` класс выше, ниже приведен пример использования `Caption` свойство:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1075">Given the `Button` class above, the following is an example of use of the `Caption` property:</span></span>
```csharp
Button okButton = new Button();
okButton.Caption = "OK";            // Invokes set accessor
string s = okButton.Caption;        // Invokes get accessor
```

<span data-ttu-id="c51c7-1076">Здесь `set` путем присвоения значения свойству вызывается метод доступа и `get` путем ссылки на свойство в выражении вызывается метод доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1076">Here, the `set` accessor is invoked by assigning a value to the property, and the `get` accessor is invoked by referencing the property in an expression.</span></span>

<span data-ttu-id="c51c7-1077">`get` И `set` методы доступа свойства не являются различными членами, и невозможно объявить методы доступа свойства отдельно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1077">The `get` and `set` accessors of a property are not distinct members, and it is not possible to declare the accessors of a property separately.</span></span> <span data-ttu-id="c51c7-1078">Таким образом он не поддерживается для двух методов доступа свойства чтения и записи иметь разные уровни доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1078">As such, it is not possible for the two accessors of a read-write property to have different accessibility.</span></span> <span data-ttu-id="c51c7-1079">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-1079">The example</span></span>
```csharp
class A
{
    private string name;

    public string Name {                // Error, duplicate member name
        get { return name; }
    }

    public string Name {                // Error, duplicate member name
        set { name = value; }
    }
}
```
<span data-ttu-id="c51c7-1080">не объявляет одно свойство чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1080">does not declare a single read-write property.</span></span> <span data-ttu-id="c51c7-1081">Вместо этого он объявляет два свойства с тем же именем, один только для чтения и только для записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1081">Rather, it declares two properties with the same name, one read-only and one write-only.</span></span> <span data-ttu-id="c51c7-1082">Поскольку двух членов, объявленных в том же классе, не могут иметь тем же именем, в примере возникает ошибка времени компиляции возникает.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1082">Since two members declared in the same class cannot have the same name, the example causes a compile-time error to occur.</span></span>

<span data-ttu-id="c51c7-1083">Когда производный класс не объявляет свойство с тем же именем, что унаследованное свойство, производное свойство скрывает унаследованное свойство по отношению к операциям чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1083">When a derived class declares a property by the same name as an inherited property, the derived property hides the inherited property with respect to both reading and writing.</span></span> <span data-ttu-id="c51c7-1084">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1084">In the example</span></span>
```csharp
class A
{
    public int P {
        set {...}
    }
}

class B: A
{
    new public int P {
        get {...}
    }
}
```
<span data-ttu-id="c51c7-1085">`P` свойство в `B` скрывает `P` свойство в `A` по отношению к операциям чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1085">the `P` property in `B` hides the `P` property in `A` with respect to both reading and writing.</span></span> <span data-ttu-id="c51c7-1086">Таким образом в инструкциях</span><span class="sxs-lookup"><span data-stu-id="c51c7-1086">Thus, in the statements</span></span>
```csharp
B b = new B();
b.P = 1;          // Error, B.P is read-only
((A)b).P = 1;     // Ok, reference to A.P
```
<span data-ttu-id="c51c7-1087">Назначение `b.P` приводит к ошибке времени компиляции для включаются в отчет, так как только для чтения `P` свойство в `B` скрывает только запись `P` свойство в `A`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1087">the assignment to `b.P` causes a compile-time error to be reported, since the read-only `P` property in `B` hides the write-only `P` property in `A`.</span></span> <span data-ttu-id="c51c7-1088">Обратите внимание, что приведение может использоваться для доступа к скрытого `P` свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1088">Note, however, that a cast can be used to access the hidden `P` property.</span></span>

<span data-ttu-id="c51c7-1089">В отличие от открытых полей свойства обеспечивают разделение между внутреннее состояние объекта и его открытому интерфейсу.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1089">Unlike public fields, properties provide a separation between an object's internal state and its public interface.</span></span> <span data-ttu-id="c51c7-1090">Рассмотрим пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1090">Consider the example:</span></span>
```csharp
class Label
{
    private int x, y;
    private string caption;

    public Label(int x, int y, string caption) {
        this.x = x;
        this.y = y;
        this.caption = caption;
    }

    public int X {
        get { return x; }
    }

    public int Y {
        get { return y; }
    }

    public Point Location {
        get { return new Point(x, y); }
    }

    public string Caption {
        get { return caption; }
    }
}
```

<span data-ttu-id="c51c7-1091">Здесь `Label` класс использует два `int` поля, `x` и `y`для хранения его расположение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1091">Here, the `Label` class uses two `int` fields, `x` and `y`, to store its location.</span></span> <span data-ttu-id="c51c7-1092">Расположение является публично доступны только в качестве `X` и `Y` свойства и в качестве `Location` свойство типа `Point`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1092">The location is publicly exposed both as an `X` and a `Y` property and as a `Location` property of type `Point`.</span></span> <span data-ttu-id="c51c7-1093">Если в будущих версиях `Label`, он становится более удобным для хранения в расположении, что `Point` на внутреннем уровне можно произвести изменения без влияния на открытый интерфейс класса:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1093">If, in a future version of `Label`, it becomes more convenient to store the location as a `Point` internally, the change can be made without affecting the public interface of the class:</span></span>
```csharp
class Label
{
    private Point location;
    private string caption;

    public Label(int x, int y, string caption) {
        this.location = new Point(x, y);
        this.caption = caption;
    }

    public int X {
        get { return location.x; }
    }

    public int Y {
        get { return location.y; }
    }

    public Point Location {
        get { return location; }
    }

    public string Caption {
        get { return caption; }
    }
}
```

<span data-ttu-id="c51c7-1094">Было `x` и `y` были `public readonly` поля, было бы невозможно внести изменения в `Label` класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1094">Had `x` and `y` instead been `public readonly` fields, it would have been impossible to make such a change to the `Label` class.</span></span>

<span data-ttu-id="c51c7-1095">Предоставление состояния с помощью свойства не обязательно менее эффективным, чем непосредственное предоставление полей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1095">Exposing state through properties is not necessarily any less efficient than exposing fields directly.</span></span> <span data-ttu-id="c51c7-1096">В частности Если свойство не является виртуальным и содержит только небольшой объем кода, среда выполнения может заменить вызовы методов доступа фактический код методов доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1096">In particular, when a property is non-virtual and contains only a small amount of code, the execution environment may replace calls to accessors with the actual code of the accessors.</span></span> <span data-ttu-id="c51c7-1097">Этот процесс известен как ***встраивание***, и он обеспечивает доступ к свойству так эффективно, как доступ к полям, сохраняя при повышенную гибкость свойств.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1097">This process is known as ***inlining***, and it makes property access as efficient as field access, yet preserves the increased flexibility of properties.</span></span>

<span data-ttu-id="c51c7-1098">С момента вызова `get` доступа концептуально эквивалентна считывания значения свойства поля, он считается плохим стилем программирования `get` наблюдаемый стороне-эффектов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1098">Since invoking a `get` accessor is conceptually equivalent to reading the value of a field, it is considered bad programming style for `get` accessors to have observable side-effects.</span></span> <span data-ttu-id="c51c7-1099">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1099">In the example</span></span>
```csharp
class Counter
{
    private int next;

    public int Next {
        get { return next++; }
    }
}
```
<span data-ttu-id="c51c7-1100">Значение `Next` свойства зависит от числа обращений свойство ранее.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1100">the value of the `Next` property depends on the number of times the property has previously been accessed.</span></span> <span data-ttu-id="c51c7-1101">Таким образом обращение к свойству создает наблюдаемый побочный эффект, а свойство должен вместо этого реализован как метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1101">Thus, accessing the property produces an observable side-effect, and the property should be implemented as a method instead.</span></span>

<span data-ttu-id="c51c7-1102">Соглашение «без побочных эффектов», `get` методы доступа не означает, что `get` методы доступа всегда должны использоваться только для возвращения значений, хранящихся в полях.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1102">The "no side-effects" convention for `get` accessors doesn't mean that `get` accessors should always be written to simply return values stored in fields.</span></span> <span data-ttu-id="c51c7-1103">Действительно `get` методы доступа часто используются для вычисления значения свойства, доступ к нескольким полям или вызова методов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1103">Indeed, `get` accessors often compute the value of a property by accessing multiple fields or invoking methods.</span></span> <span data-ttu-id="c51c7-1104">Тем не менее правильно спроектированное `get` метод доступа не выполняет действия, вызывающие заметные изменения в состоянии объекта.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1104">However, a properly designed `get` accessor performs no actions that cause observable changes in the state of the object.</span></span>

<span data-ttu-id="c51c7-1105">Свойства можно отложить инициализацию ресурса вплоть до момента его первом обращении.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1105">Properties can be used to delay initialization of a resource until the moment it is first referenced.</span></span> <span data-ttu-id="c51c7-1106">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1106">For example:</span></span>
```csharp
using System.IO;

public class Console
{
    private static TextReader reader;
    private static TextWriter writer;
    private static TextWriter error;

    public static TextReader In {
        get {
            if (reader == null) {
                reader = new StreamReader(Console.OpenStandardInput());
            }
            return reader;
        }
    }

    public static TextWriter Out {
        get {
            if (writer == null) {
                writer = new StreamWriter(Console.OpenStandardOutput());
            }
            return writer;
        }
    }

    public static TextWriter Error {
        get {
            if (error == null) {
                error = new StreamWriter(Console.OpenStandardError());
            }
            return error;
        }
    }
}
```

<span data-ttu-id="c51c7-1107">`Console` Класс содержит три свойства `In`, `Out`, и `Error`, представляющие стандартного ввода, вывода и ошибка устройств, соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1107">The `Console` class contains three properties, `In`, `Out`, and `Error`, that represent the standard input, output, and error devices, respectively.</span></span> <span data-ttu-id="c51c7-1108">Благодаря предоставлению этих членов, как свойства, `Console` класса можно отложить их инициализацию до их фактического использования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1108">By exposing these members as properties, the `Console` class can delay their initialization until they are actually used.</span></span> <span data-ttu-id="c51c7-1109">Например, при первой ссылке на `Out` свойства, как и в</span><span class="sxs-lookup"><span data-stu-id="c51c7-1109">For example, upon first referencing the `Out` property, as in</span></span>
```csharp
Console.Out.WriteLine("hello, world");
```
<span data-ttu-id="c51c7-1110">базовый `TextWriter` для созданных устройстве вывода.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1110">the underlying `TextWriter` for the output device is created.</span></span> <span data-ttu-id="c51c7-1111">Но если приложение не ссылается на `In` и `Error` свойств, то объекты не создаются для этих устройств.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1111">But if the application makes no reference to the `In` and `Error` properties, then no objects are created for those devices.</span></span>

### <a name="automatically-implemented-properties"></a><span data-ttu-id="c51c7-1112">Автоматически реализованные свойства</span><span class="sxs-lookup"><span data-stu-id="c51c7-1112">Automatically implemented properties</span></span>

<span data-ttu-id="c51c7-1113">Автоматически реализуемое свойство (или ***автосвойств*** для краткости), не являющиеся абстрактными или внешними свойство с тела методов доступа только для точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1113">An automatically implemented property (or ***auto-property*** for short), is a non-abstract non-extern property with semicolon-only accessor bodies.</span></span> <span data-ttu-id="c51c7-1114">Автосвойства должен иметь метод доступа get и может иметь метод доступа set.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1114">Auto-properties must have a get accessor and can optionally have a set accessor.</span></span>

<span data-ttu-id="c51c7-1115">Когда свойство указано как автоматически реализуемое свойство, скрытое резервное поле автоматически доступен для свойства и реализуются методы доступа для чтения и записи к этому полю поддержки.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1115">When a property is specified as an automatically implemented property, a hidden backing field is automatically available for the property, and the accessors are implemented to read from and write to that backing field.</span></span> <span data-ttu-id="c51c7-1116">Если автоматическое свойство без метода доступа set, считается резервное поле `readonly` ([поля только для чтения](classes.md#readonly-fields)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1116">If the auto-property has no set accessor, the backing field is considered `readonly` ([Readonly fields](classes.md#readonly-fields)).</span></span> <span data-ttu-id="c51c7-1117">Так же, как `readonly` поля, автосвойства только для считывания могут также назначаться в теле конструктора включающего класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1117">Just like a `readonly` field, a getter-only auto-property can also be assigned to in the body of a constructor of the enclosing class.</span></span> <span data-ttu-id="c51c7-1118">Такое присваивание назначает непосредственно к резервному полю только для чтения свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1118">Such an assignment assigns directly to the readonly backing field of the property.</span></span>

<span data-ttu-id="c51c7-1119">Автосвойства могут содержать *property_initializer*, который применяется непосредственно к резервному полю как *variable_initializer* ([инициализаторы переменных](classes.md#variable-initializers)) .</span><span class="sxs-lookup"><span data-stu-id="c51c7-1119">An auto-property may optionally have a *property_initializer*, which is applied directly to the backing field as a *variable_initializer* ([Variable initializers](classes.md#variable-initializers)).</span></span>

<span data-ttu-id="c51c7-1120">Следующий пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1120">The following example:</span></span>
```csharp
public class Point {
    public int X { get; set; } = 0;
    public int Y { get; set; } = 0;
}
```
<span data-ttu-id="c51c7-1121">эквивалентно следующему объявлению:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1121">is equivalent to the following declaration:</span></span>
```csharp
public class Point {
    private int __x = 0;
    private int __y = 0;
    public int X { get { return __x; } set { __x = value; } }
    public int Y { get { return __y; } set { __y = value; } }
}
```

<span data-ttu-id="c51c7-1122">Следующий пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1122">The following example:</span></span>
```csharp
public class ReadOnlyPoint
{
    public int X { get; }
    public int Y { get; }
    public ReadOnlyPoint(int x, int y) { X = x; Y = y; }
}
```
<span data-ttu-id="c51c7-1123">эквивалентно следующему объявлению:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1123">is equivalent to the following declaration:</span></span>
```csharp
public class ReadOnlyPoint
{
    private readonly int __x;
    private readonly int __y;
    public int X { get { return __x; } }
    public int Y { get { return __y; } }
    public ReadOnlyPoint(int x, int y) { __x = x; __y = y; }
}
```

<span data-ttu-id="c51c7-1124">Обратите внимание на то, что назначения, которые только для чтения поля допустимы, так как они встречаются в конструкторе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1124">Notice that the assignments to the readonly field are legal, because they occur within the constructor.</span></span>


### <a name="accessibility"></a><span data-ttu-id="c51c7-1125">Специальные возможности</span><span class="sxs-lookup"><span data-stu-id="c51c7-1125">Accessibility</span></span>

<span data-ttu-id="c51c7-1126">Если метод доступа *accessor_modifier*, то домен доступности ([области доступности](basic-concepts.md#accessibility-domains)) метода доступа определяется объявленным уровнем доступности *accessor_modifier* .</span><span class="sxs-lookup"><span data-stu-id="c51c7-1126">If an accessor has an *accessor_modifier*, the accessibility domain ([Accessibility domains](basic-concepts.md#accessibility-domains)) of the accessor is determined using the declared accessibility of the *accessor_modifier*.</span></span> <span data-ttu-id="c51c7-1127">Если метод доступа не является *accessor_modifier*, то домен доступности метода доступа определяется объявленным уровнем доступности свойства или индексатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1127">If an accessor does not have an *accessor_modifier*, the accessibility domain of the accessor is determined from the declared accessibility of the property or indexer.</span></span>

<span data-ttu-id="c51c7-1128">Наличие *accessor_modifier* никогда не влияет на поиск члена ([операторы](expressions.md#operators)) или разрешение перегрузки ([разрешение перегрузки](expressions.md#overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1128">The presence of an *accessor_modifier* never affects member lookup ([Operators](expressions.md#operators)) or overload resolution ([Overload resolution](expressions.md#overload-resolution)).</span></span> <span data-ttu-id="c51c7-1129">Модификаторы для свойства или индексатора всегда определяют, какое свойство или индексатор связан, вне зависимости от контекста доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1129">The modifiers on the property or indexer always determine which property or indexer is bound to, regardless of the context of the access.</span></span>

<span data-ttu-id="c51c7-1130">После выбора конкретного свойства или индексатора области доступности для задействованных методов доступа, используемые для определения допустимости использования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1130">Once a particular property or indexer has been selected, the accessibility domains of the specific accessors involved are used to determine if that usage is valid:</span></span>

*  <span data-ttu-id="c51c7-1131">Если оно используется как значение ([значения выражений](expressions.md#values-of-expressions)), `get` метод доступа должен существовать и быть доступен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1131">If the usage is as a value ([Values of expressions](expressions.md#values-of-expressions)), the `get` accessor must exist and be accessible.</span></span>
*  <span data-ttu-id="c51c7-1132">Если оно используется в качестве целевого объекта простого присваивания ([простое присваивание](expressions.md#simple-assignment)), `set` метод доступа должен существовать и быть доступен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1132">If the usage is as the target of a simple assignment ([Simple assignment](expressions.md#simple-assignment)), the `set` accessor must exist and be accessible.</span></span>
*  <span data-ttu-id="c51c7-1133">Если оно используется как целевой составного оператора присваивания ([Составное присваивание](expressions.md#compound-assignment)), или в качестве целевого объекта `++` или `--` операторы ([функции-члены](expressions.md#function-members).9, [ Выражения вызова](expressions.md#invocation-expressions)), оба `get` методы доступа и `set` доступа должен существовать и быть доступен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1133">If the usage is as the target of compound assignment ([Compound assignment](expressions.md#compound-assignment)), or as the target of the `++` or `--` operators ([Function members](expressions.md#function-members).9, [Invocation expressions](expressions.md#invocation-expressions)), both the `get` accessors and the `set` accessor must exist and be accessible.</span></span>

<span data-ttu-id="c51c7-1134">В следующем примере свойство `A.Text` скрыто свойством `B.Text`, даже в контекстах, где это только `set` вызывается метод доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1134">In the following example, the property `A.Text` is hidden by the property `B.Text`, even in contexts where only the `set` accessor is called.</span></span> <span data-ttu-id="c51c7-1135">В отличие от этого, свойство `B.Count` доступен не для класса `M`, поэтому доступное свойство `A.Count` вместо него используется.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1135">In contrast, the property `B.Count` is not accessible to class `M`, so the accessible property `A.Count` is used instead.</span></span>

```csharp
class A
{
    public string Text {
        get { return "hello"; }
        set { }
    }

    public int Count {
        get { return 5; }
        set { }
    }
}

class B: A
{
    private string text = "goodbye"; 
    private int count = 0;

    new public string Text {
        get { return text; }
        protected set { text = value; }
    }

    new protected int Count { 
        get { return count; }
        set { count = value; }
    }
}

class M
{
    static void Main() {
        B b = new B();
        b.Count = 12;             // Calls A.Count set accessor
        int i = b.Count;          // Calls A.Count get accessor
        b.Text = "howdy";         // Error, B.Text set accessor not accessible
        string s = b.Text;        // Calls B.Text get accessor
    }
}
```

<span data-ttu-id="c51c7-1136">Метод доступа, который используется для реализации интерфейса может не иметь *accessor_modifier*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1136">An accessor that is used to implement an interface may not have an *accessor_modifier*.</span></span> <span data-ttu-id="c51c7-1137">Если только один метод доступа используется для реализации интерфейса, другой метод доступа может быть объявлен с *accessor_modifier*:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1137">If only one accessor is used to implement an interface, the other accessor may be declared with an *accessor_modifier*:</span></span>
```csharp
public interface I
{
    string Prop { get; }
}

public class C: I
{
    public Prop {
        get { return "April"; }       // Must not have a modifier here
        internal set {...}            // Ok, because I.Prop has no set accessor
    }
}
```

### <a name="virtual-sealed-override-and-abstract-property-accessors"></a><span data-ttu-id="c51c7-1138">Виртуальные, запечатанные, переопределяющие и абстрактные доступа к свойствам</span><span class="sxs-lookup"><span data-stu-id="c51c7-1138">Virtual, sealed, override, and abstract property accessors</span></span>

<span data-ttu-id="c51c7-1139">Объект `virtual` объявление свойства указывает, что виртуальные методы доступа к свойству.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1139">A `virtual` property declaration specifies that the accessors of the property are virtual.</span></span> <span data-ttu-id="c51c7-1140">`virtual` Модификатор применяется для обоих методов доступа свойства чтения и записи — это невозможно для только один метод доступа свойства чтения и записи, должен быть виртуальным.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1140">The `virtual` modifier applies to both accessors of a read-write property—it is not possible for only one accessor of a read-write property to be virtual.</span></span>

<span data-ttu-id="c51c7-1141">`abstract` Объявление свойства задает, что виртуальные методы доступа к свойству, но не предоставляет фактической реализации методов доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1141">An `abstract` property declaration specifies that the accessors of the property are virtual, but does not provide an actual implementation of the accessors.</span></span> <span data-ttu-id="c51c7-1142">Вместо этого неабстрактные производные классы, обязаны предоставлять собственную реализацию для методов доступа посредством переопределения свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1142">Instead, non-abstract derived classes are required to provide their own implementation for the accessors by overriding the property.</span></span> <span data-ttu-id="c51c7-1143">Так как метод доступа для в объявлении абстрактного свойства не предоставляет фактической реализации, его *accessor_body* состоит всего лишь из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1143">Because an accessor for an abstract property declaration provides no actual implementation, its *accessor_body* simply consists of a semicolon.</span></span>

<span data-ttu-id="c51c7-1144">Объявление свойства, которое включает в себя `abstract` и `override` модификаторов указывает, что свойство является абстрактным и переопределяет базовое свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1144">A property declaration that includes both the `abstract` and `override` modifiers specifies that the property is abstract and overrides a base property.</span></span> <span data-ttu-id="c51c7-1145">Методы доступа такого свойства также являются абстрактными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1145">The accessors of such a property are also abstract.</span></span>

<span data-ttu-id="c51c7-1146">Абстрактное свойство объявления допускаются только в абстрактных классах ([абстрактные классы](classes.md#abstract-classes)). Методы доступа унаследованного виртуального свойства можно переопределить в производном классе путем включения объявления свойства, которое указывает `override` директива.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1146">Abstract property declarations are only permitted in abstract classes ([Abstract classes](classes.md#abstract-classes)).The accessors of an inherited virtual property can be overridden in a derived class by including a property declaration that specifies an `override` directive.</span></span> <span data-ttu-id="c51c7-1147">Этот процесс называется ***переопределение объявление свойства***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1147">This is known as an ***overriding property declaration***.</span></span> <span data-ttu-id="c51c7-1148">Переопределяющее объявление свойства не объявляет новое свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1148">An overriding property declaration does not declare a new property.</span></span> <span data-ttu-id="c51c7-1149">Вместо этого он просто специализирует реализации методов доступа существующего виртуального свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1149">Instead, it simply specializes the implementations of the accessors of an existing virtual property.</span></span>

<span data-ttu-id="c51c7-1150">Переопределяющее объявление свойства необходимо указать в качестве унаследованного свойства точно такие же модификаторы доступа, тип и имя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1150">An overriding property declaration must specify the exact same accessibility modifiers, type, and name as the inherited property.</span></span> <span data-ttu-id="c51c7-1151">Если наследуемое свойство имеет только один метод доступа (т. е. Если наследуемое свойство только для чтения или только для записи), переопределяющее свойство должно включать только этот метод доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1151">If the inherited property has only a single accessor (i.e., if the inherited property is read-only or write-only), the overriding property must include only that accessor.</span></span> <span data-ttu-id="c51c7-1152">Если унаследованное свойство содержит оба метода доступа (т. е. Если наследуемое свойство доступно для чтения записи), переопределяющее свойство может включать один или оба метода доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1152">If the inherited property includes both accessors (i.e., if the inherited property is read-write), the overriding property can include either a single accessor or both accessors.</span></span>

<span data-ttu-id="c51c7-1153">Переопределяющее объявление свойства могут включать `sealed` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1153">An overriding property declaration may include the `sealed` modifier.</span></span> <span data-ttu-id="c51c7-1154">Использование этот модификатор предотвращает последующее переопределение свойства производного класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1154">Use of this modifier prevents a derived class from further overriding the property.</span></span> <span data-ttu-id="c51c7-1155">Методы доступа запечатанного свойства также являются запечатанными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1155">The accessors of a sealed property are also sealed.</span></span>

<span data-ttu-id="c51c7-1156">За исключением отличий в объявление и вызов синтаксиса, виртуальных, запечатанных, переопределяющие и абстрактные методы доступа ведут себя так же, как виртуальный, запечатанных, переопределение и абстрактные методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1156">Except for differences in declaration and invocation syntax, virtual, sealed, override, and abstract accessors behave exactly like virtual, sealed, override and abstract methods.</span></span> <span data-ttu-id="c51c7-1157">В частности, правила описываются в [виртуальных методов](classes.md#virtual-methods), [переопределять методы](classes.md#override-methods), [запечатанные методы](classes.md#sealed-methods), и [абстрактные методы](classes.md#abstract-methods) применяются так, как если методы доступа были методы из соответствующей формы:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1157">Specifically, the rules described in [Virtual methods](classes.md#virtual-methods), [Override methods](classes.md#override-methods), [Sealed methods](classes.md#sealed-methods), and [Abstract methods](classes.md#abstract-methods) apply as if accessors were methods of a corresponding form:</span></span>

*  <span data-ttu-id="c51c7-1158">Объект `get` метод доступа соответствует оформляется как метод с возвращаемым значением типа свойства и те же модификаторы, содержащего его свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1158">A `get` accessor corresponds to a parameterless method with a return value of the property type and the same modifiers as the containing property.</span></span>
*  <span data-ttu-id="c51c7-1159">Объект `set` доступа соответствует методу с параметром одиночное значение типа свойства, `void` возвращают тип и одинаковые модификаторы содержащего его свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1159">A `set` accessor corresponds to a method with a single value parameter of the property type, a `void` return type, and the same modifiers as the containing property.</span></span>

<span data-ttu-id="c51c7-1160">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1160">In the example</span></span>
```csharp
abstract class A
{
    int y;

    public virtual int X {
        get { return 0; }
    }

    public virtual int Y {
        get { return y; }
        set { y = value; }
    }

    public abstract int Z { get; set; }
}
```
<span data-ttu-id="c51c7-1161">`X` — это виртуальное свойство только для чтения, `Y` — это виртуальное свойство чтения и записи, и `Z` является абстрактным свойством чтения и записи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1161">`X` is a virtual read-only property, `Y` is a virtual read-write property, and `Z` is an abstract read-write property.</span></span> <span data-ttu-id="c51c7-1162">Так как `Z` является абстрактным, содержащего класса `A` должен также быть объявлен как абстрактный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1162">Because `Z` is abstract, the containing class `A` must also be declared abstract.</span></span>

<span data-ttu-id="c51c7-1163">Класс, производный от `A` будет показано на следующем рисунке:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1163">A class that derives from `A` is show below:</span></span>
```csharp
class B: A
{
    int z;

    public override int X {
        get { return base.X + 1; }
    }

    public override int Y {
        set { base.Y = value < 0? 0: value; }
    }

    public override int Z {
        get { return z; }
        set { z = value; }
    }
}
```

<span data-ttu-id="c51c7-1164">В данном случае — объявления `X`, `Y`, и `Z` переопределяют объявления свойств.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1164">Here, the declarations of `X`, `Y`, and `Z` are overriding property declarations.</span></span> <span data-ttu-id="c51c7-1165">Каждое объявление свойства точно соответствует модификаторы доступа, тип и имя соответствующего наследуемого свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1165">Each property declaration exactly matches the accessibility modifiers, type, and name of the corresponding inherited property.</span></span> <span data-ttu-id="c51c7-1166">`get` Метод доступа `X` и `set` метод доступа `Y` использовать `base` ключевое слово для доступа к унаследованным методам доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1166">The `get` accessor of `X` and the `set` accessor of `Y` use the `base` keyword to access the inherited accessors.</span></span> <span data-ttu-id="c51c7-1167">Объявление `Z` переопределяет оба абстрактного метода доступа — таким образом, нет ожидающих абстрактной функции членов в `B`, и `B` , может быть неабстрактным классом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1167">The declaration of `Z` overrides both abstract accessors—thus, there are no outstanding abstract function members in `B`, and `B` is permitted to be a non-abstract class.</span></span>

<span data-ttu-id="c51c7-1168">Если свойство объявлено как `override`, все переопределенные методы доступа должны быть доступны коду переопределения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1168">When a property is declared as an `override`, any overridden accessors must be accessible to the overriding code.</span></span> <span data-ttu-id="c51c7-1169">Кроме того объявленный уровень доступности свойства или сам индексатор и методы доступа, должна соответствовать переопределенному члену и методы доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1169">In addition, the declared accessibility of both the property or indexer itself, and of the accessors, must match that of the overridden member and accessors.</span></span> <span data-ttu-id="c51c7-1170">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1170">For example:</span></span>
```csharp
public class B
{
    public virtual int P {
        protected set {...}
        get {...}
    }
}

public class D: B
{
    public override int P {
        protected set {...}            // Must specify protected here
        get {...}                      // Must not have a modifier here
    }
}
```

## <a name="events"></a><span data-ttu-id="c51c7-1171">События</span><span class="sxs-lookup"><span data-stu-id="c51c7-1171">Events</span></span>

<span data-ttu-id="c51c7-1172">***Событий*** — это член, включает объект или класс для предоставления уведомления.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1172">An ***event*** is a member that enables an object or class to provide notifications.</span></span> <span data-ttu-id="c51c7-1173">Клиенты могли подключаться к событиям исполняемый код, указав ***обработчики событий***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1173">Clients can attach executable code for events by supplying ***event handlers***.</span></span>

<span data-ttu-id="c51c7-1174">События объявляются с помощью *event_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1174">Events are declared using *event_declaration*s:</span></span>

```antlr
event_declaration
    : attributes? event_modifier* 'event' type variable_declarators ';'
    | attributes? event_modifier* 'event' type member_name '{' event_accessor_declarations '}'
    ;

event_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'static'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | event_modifier_unsafe
    ;

event_accessor_declarations
    : add_accessor_declaration remove_accessor_declaration
    | remove_accessor_declaration add_accessor_declaration
    ;

add_accessor_declaration
    : attributes? 'add' block
    ;

remove_accessor_declaration
    : attributes? 'remove' block
    ;
```

<span data-ttu-id="c51c7-1175">*Event_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)) и является допустимой комбинацией четырех модификаторов доступа ([модификаторы доступа ](classes.md#access-modifiers)), `new` ([Модификатор new](classes.md#the-new-modifier)), `static` ([экземпляра и статические методы](classes.md#static-and-instance-methods)), `virtual` ([виртуальных методов](classes.md#virtual-methods)), `override` ([Переопределять методы](classes.md#override-methods)), `sealed` ([запечатанные методы](classes.md#sealed-methods)), `abstract` ([абстрактные методы](classes.md#abstract-methods)), и `extern` ([Внешние методы](classes.md#external-methods)) модификаторы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1175">An *event_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)),  `static` ([Static and instance methods](classes.md#static-and-instance-methods)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="c51c7-1176">Объявления событий подчиняются тем же правилам, что и объявления методов ([методы](classes.md#methods)) по отношению к допустимые сочетания модификаторов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1176">Event declarations are subject to the same rules as method declarations ([Methods](classes.md#methods)) with regard to valid combinations of modifiers.</span></span>

<span data-ttu-id="c51c7-1177">*Тип* события объявление должно быть *delegate_type* ([ссылочные типы](types.md#reference-types)) и что *delegate_type* необходимо по крайней мере как уровень доступности, как самого события ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1177">The *type* of an event declaration must be a *delegate_type* ([Reference types](types.md#reference-types)), and that *delegate_type* must be at least as accessible as the event itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-1178">Объявление события может включать *event_accessor_declarations*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1178">An event declaration may include *event_accessor_declarations*.</span></span> <span data-ttu-id="c51c7-1179">Тем не менее, если это не так, для или внешними, не являющиеся абстрактными событий, компилятор автоматически предоставляет их ([подобные полям события](classes.md#field-like-events)); для внешних событий методы доступа предоставляются извне.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1179">However, if it does not, for non-extern, non-abstract events, the compiler supplies them automatically ([Field-like events](classes.md#field-like-events)); for extern events, the accessors are provided externally.</span></span>

<span data-ttu-id="c51c7-1180">Объявление события, в котором пропущены *event_accessor_declarations* определяет одно или несколько событий — один для каждого из *variable_declarator*s.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1180">An event declaration that omits *event_accessor_declarations* defines one or more events—one for each of the *variable_declarator*s.</span></span> <span data-ttu-id="c51c7-1181">Атрибуты и модификаторы применяются ко всем членам, объявленным такой *event_declaration*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1181">The attributes and modifiers apply to all of the members declared by such an *event_declaration*.</span></span>

<span data-ttu-id="c51c7-1182">Произошла ошибка во время компиляции для *event_declaration* обоих `abstract` модификатор и разделенных фигурную скобку *event_accessor_declarations*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1182">It is a compile-time error for an *event_declaration* to include both the `abstract` modifier and brace-delimited *event_accessor_declarations*.</span></span>

<span data-ttu-id="c51c7-1183">Если объявление события содержит `extern` модификатор, событие считается ***внешнее событие***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1183">When an event declaration includes an `extern` modifier, the event is said to be an ***external event***.</span></span> <span data-ttu-id="c51c7-1184">Поскольку объявления внешних событий не предоставляет фактической реализации, является ошибкой для включения оба `extern` модификатор и *event_accessor_declarations*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1184">Because an external event declaration provides no actual implementation, it is an error for it to include both the `extern` modifier and *event_accessor_declarations*.</span></span>

<span data-ttu-id="c51c7-1185">Произошла ошибка во время компиляции для *variable_declarator* объявления события с `abstract` или `external` модификатор для включения *variable_initializer*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1185">It is a compile-time error for a *variable_declarator* of an event declaration with an `abstract` or `external` modifier to include a *variable_initializer*.</span></span>

<span data-ttu-id="c51c7-1186">События можно использовать как левый операнд `+=` и `-=` операторы ([назначения события](expressions.md#event-assignment)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1186">An event can be used as the left-hand operand of the `+=` and `-=` operators ([Event assignment](expressions.md#event-assignment)).</span></span> <span data-ttu-id="c51c7-1187">Эти операторы используются, соответственно, чтобы присоединить обработчики событий или удаления обработчиков событий из события, и модификаторы доступа события управления контексты, в которых разрешены такие операции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1187">These operators are used, respectively, to attach event handlers to or to remove event handlers from an event, and the access modifiers of the event control the contexts in which such operations are permitted.</span></span>

<span data-ttu-id="c51c7-1188">Так как `+=` и `-=` являются только операции, разрешенные для событий за пределами тип, объявляющий событие, внешний код можно добавить и удаления обработчиков событий, но нельзя любым другим способом получения или изменения базового списка событий обработчики.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1188">Since `+=` and `-=` are the only operations that are permitted on an event outside the type that declares the event, external code can add and remove handlers for an event, but cannot in any other way obtain or modify the underlying list of event handlers.</span></span>

<span data-ttu-id="c51c7-1189">В операции формы `x += y` или `x -= y`, когда `x` — это событие, а ссылки выполняется за пределами типа, содержащего объявление `x`, результат операции имеет тип `void` (в отличие от необходимости Тип `x`, со значением `x` после назначения).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1189">In an operation of the form `x += y` or `x -= y`, when `x` is an event and the reference takes place outside the type that contains the declaration of `x`, the result of the operation has type `void` (as opposed to having the type of `x`, with the value of `x` after the assignment).</span></span> <span data-ttu-id="c51c7-1190">Это правило запрещает внешний код непосредственного просмотра базового делегата события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1190">This rule prohibits external code from indirectly examining the underlying delegate of an event.</span></span>

<span data-ttu-id="c51c7-1191">В следующем примере показано, как обработчики событий можно подключать к экземплярам `Button` класса:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1191">The following example shows how event handlers are attached to instances of the `Button` class:</span></span>
```csharp
public delegate void EventHandler(object sender, EventArgs e);

public class Button: Control
{
    public event EventHandler Click;
}

public class LoginDialog: Form
{
    Button OkButton;
    Button CancelButton;

    public LoginDialog() {
        OkButton = new Button(...);
        OkButton.Click += new EventHandler(OkButtonClick);
        CancelButton = new Button(...);
        CancelButton.Click += new EventHandler(CancelButtonClick);
    }

    void OkButtonClick(object sender, EventArgs e) {
        // Handle OkButton.Click event
    }

    void CancelButtonClick(object sender, EventArgs e) {
        // Handle CancelButton.Click event
    }
}
```

<span data-ttu-id="c51c7-1192">Здесь `LoginDialog` конструктор экземпляра создает два `Button` экземпляров и присоединяет обработчики событий к `Click` события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1192">Here, the `LoginDialog` instance constructor creates two `Button` instances and attaches event handlers to the `Click` events.</span></span>

### <a name="field-like-events"></a><span data-ttu-id="c51c7-1193">Подобные полям события</span><span class="sxs-lookup"><span data-stu-id="c51c7-1193">Field-like events</span></span>

<span data-ttu-id="c51c7-1194">В тексте программы элемента класса или структуры, который содержит объявление события определенные события, можно использовать как поля.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1194">Within the program text of the class or struct that contains the declaration of an event, certain events can be used like fields.</span></span> <span data-ttu-id="c51c7-1195">Для использования таким образом, событие не должно быть `abstract` или `extern`и явным образом не должны содержать *event_accessor_declarations*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1195">To be used in this way, an event must not be `abstract` or `extern`, and must not explicitly include *event_accessor_declarations*.</span></span> <span data-ttu-id="c51c7-1196">Такое событие может использоваться в любом контексте, который разрешает поле.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1196">Such an event can be used in any context that permits a field.</span></span> <span data-ttu-id="c51c7-1197">Поле содержит делегат ([делегаты](delegates.md)) который ссылается на список обработчиков событий, которые были добавлены к событию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1197">The field contains a delegate ([Delegates](delegates.md)) which refers to the list of event handlers that have been added to the event.</span></span> <span data-ttu-id="c51c7-1198">Если обработчики событий не будут добавлены, поле содержит `null`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1198">If no event handlers have been added, the field contains `null`.</span></span>

<span data-ttu-id="c51c7-1199">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1199">In the example</span></span>
```csharp
public delegate void EventHandler(object sender, EventArgs e);

public class Button: Control
{
    public event EventHandler Click;

    protected void OnClick(EventArgs e) {
        if (Click != null) Click(this, e);
    }

    public void Reset() {
        Click = null;
    }
}
```
<span data-ttu-id="c51c7-1200">`Click` используется в качестве поля в `Button` класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1200">`Click` is used as a field within the `Button` class.</span></span> <span data-ttu-id="c51c7-1201">Как показано в примере, поле можно проверить, изменяется и используется в выражениях вызова делегата.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1201">As the example demonstrates, the field can be examined, modified, and used in delegate invocation expressions.</span></span> <span data-ttu-id="c51c7-1202">`OnClick` Метод в `Button` класса «вызывает» `Click` событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1202">The `OnClick` method in the `Button` class "raises" the `Click` event.</span></span> <span data-ttu-id="c51c7-1203">Концепция создания события в точности соответствует вызову делегата, представленного этим событием. Это позволяет обойтись без особой языковой конструкции для создания событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1203">The notion of raising an event is precisely equivalent to invoking the delegate represented by the event—thus, there are no special language constructs for raising events.</span></span> <span data-ttu-id="c51c7-1204">Обратите внимание на то, что вызов делегата предшествует проверка, что делегат не равно null.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1204">Note that the delegate invocation is preceded by a check that ensures the delegate is non-null.</span></span>

<span data-ttu-id="c51c7-1205">За пределами объявления `Button` класс, `Click` член может использоваться только в левой части `+=` и `-=` операторы, как и в</span><span class="sxs-lookup"><span data-stu-id="c51c7-1205">Outside the declaration of the `Button` class, the `Click` member can only be used on the left-hand side of the `+=` and `-=` operators, as in</span></span>
```csharp
b.Click += new EventHandler(...);
```
<span data-ttu-id="c51c7-1206">который добавляет делегат в список вызова `Click` событий, и</span><span class="sxs-lookup"><span data-stu-id="c51c7-1206">which appends a delegate to the invocation list of the `Click` event, and</span></span>
```csharp
b.Click -= new EventHandler(...);
```
<span data-ttu-id="c51c7-1207">который удаляет делегат из списка вызовов `Click` событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1207">which removes a delegate from the invocation list of the `Click` event.</span></span>

<span data-ttu-id="c51c7-1208">При компиляции события, подобного полю, компилятор автоматически создает хранилище для хранения делегата и создает методы доступа для события, которые добавляют или удаляют обработчики событий поля делегата.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1208">When compiling a field-like event, the compiler automatically creates storage to hold the delegate, and creates accessors for the event that add or remove event handlers to the delegate field.</span></span> <span data-ttu-id="c51c7-1209">Операции добавления и удаления являются потокобезопасными и может (но не обязательно) быть выполняются при блокировке ([инструкция lock](statements.md#the-lock-statement)) на содержащего его объекта для события экземпляра, либо этого объекта типа ([анонимный доступ выражения создания объектов](expressions.md#anonymous-object-creation-expressions)) для статическое событие.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1209">The addition and removal operations are thread safe, and may (but are not required to) be done while holding the lock ([The lock statement](statements.md#the-lock-statement)) on the containing object for an instance event, or the type object ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) for a static event.</span></span>

<span data-ttu-id="c51c7-1210">Таким образом объявление события экземпляра формы:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1210">Thus, an instance event declaration of the form:</span></span>
```csharp
class X
{
    public event D Ev;
}
```
<span data-ttu-id="c51c7-1211">компилируется в нечто, эквивалентное:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1211">will be compiled to something equivalent to:</span></span>
```csharp
class X
{
    private D __Ev;  // field to hold the delegate

    public event D Ev {
        add {
            /* add the delegate in a thread safe way */
        }

        remove {
            /* remove the delegate in a thread safe way */
        }
    }
}
```
<span data-ttu-id="c51c7-1212">В классе `X`, ссылки на `Ev` в левой части `+=` и `-=` операторы вызывают добавить и удалить методы доступа для вызова.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1212">Within the class `X`, references to `Ev` on the left-hand side of the `+=` and `-=` operators cause the add and remove accessors to be invoked.</span></span> <span data-ttu-id="c51c7-1213">Все ссылки на `Ev` компилируются для ссылки на скрытое поле `__Ev` вместо ([доступ к членам](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1213">All other references to `Ev` are compiled to reference the hidden field `__Ev` instead ([Member access](expressions.md#member-access)).</span></span> <span data-ttu-id="c51c7-1214">Имя "`__Ev`" может быть произвольным; скрытое поле может иметь любое имя или имя не вообще.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1214">The name "`__Ev`" is arbitrary; the hidden field could have any name or no name at all.</span></span>

### <a name="event-accessors"></a><span data-ttu-id="c51c7-1215">Методы доступа событий</span><span class="sxs-lookup"><span data-stu-id="c51c7-1215">Event accessors</span></span>

<span data-ttu-id="c51c7-1216">Объявления событий обычно опускаются *event_accessor_declarations*, как в `Button` приведенном выше примере.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1216">Event declarations typically omit *event_accessor_declarations*, as in the `Button` example above.</span></span> <span data-ttu-id="c51c7-1217">Причин для этого входит случай, в котором стоимость хранения одного поля на событие не допускается.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1217">One situation for doing so involves the case in which the storage cost of one field per event is not acceptable.</span></span> <span data-ttu-id="c51c7-1218">В таких случаях класс может содержать *event_accessor_declarations* и используют закрытый механизм для хранения списка обработчиков событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1218">In such cases, a class can include *event_accessor_declarations* and use a private mechanism for storing the list of event handlers.</span></span>

<span data-ttu-id="c51c7-1219">*Event_accessor_declarations* события укажите исполняемые операторы, связанные с добавления и удаления обработчиков событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1219">The *event_accessor_declarations* of an event specify the executable statements associated with adding and removing event handlers.</span></span>

<span data-ttu-id="c51c7-1220">Объявления методов доступа состоят из *add_accessor_declaration* и *remove_accessor_declaration*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1220">The accessor declarations consist of an *add_accessor_declaration* and a *remove_accessor_declaration*.</span></span> <span data-ttu-id="c51c7-1221">Каждое объявление метода доступа состоит из маркера `add` или `remove` следуют *блок*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1221">Each accessor declaration consists of the token `add` or `remove` followed by a *block*.</span></span> <span data-ttu-id="c51c7-1222">*Блок* связанные с *add_accessor_declaration* задает операторы, выполняемые при добавлении обработчика событий и *блок* связанных с *remove_accessor_declaration* задает операторы, выполняемые при удалении обработчика событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1222">The *block* associated with an *add_accessor_declaration* specifies the statements to execute when an event handler is added, and the *block* associated with a *remove_accessor_declaration* specifies the statements to execute when an event handler is removed.</span></span>

<span data-ttu-id="c51c7-1223">Каждый *add_accessor_declaration* и *remove_accessor_declaration* соответствует методу с параметром одиночное значение типа события и `void` тип возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1223">Each *add_accessor_declaration* and *remove_accessor_declaration* corresponds to a method with a single value parameter of the event type and a `void` return type.</span></span> <span data-ttu-id="c51c7-1224">Неявный параметр метода доступа к событию называется `value`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1224">The implicit parameter of an event accessor is named `value`.</span></span> <span data-ttu-id="c51c7-1225">Когда событие используется в назначении события, используется доступа соответствующего события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1225">When an event is used in an event assignment, the appropriate event accessor is used.</span></span> <span data-ttu-id="c51c7-1226">В частности Если оператор присваивания `+=` затем используется метод доступа add и оператор присваивания имеет `-=` затем используется метод доступа remove.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1226">Specifically, if the assignment operator is `+=` then the add accessor is used, and if the assignment operator is `-=` then the remove accessor is used.</span></span> <span data-ttu-id="c51c7-1227">В любом случае правый операнд оператора присваивания используется в качестве аргумента для доступа к событию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1227">In either case, the right-hand operand of the assignment operator is used as the argument to the event accessor.</span></span> <span data-ttu-id="c51c7-1228">Блок *add_accessor_declaration* или *remove_accessor_declaration* должны соответствовать правилам для `void` методов, описанных в [тело метода](classes.md#method-body).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1228">The block of an *add_accessor_declaration* or a *remove_accessor_declaration* must conform to the rules for `void` methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="c51c7-1229">В частности `return` инструкций в этот блок не допускаются и ввести выражение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1229">In particular, `return` statements in such a block are not permitted to specify an expression.</span></span>

<span data-ttu-id="c51c7-1230">Так как метод доступа события неявно имеет параметр с именем `value`, возникает ошибка времени компиляции для локальной переменной или константы, объявленные в методе доступа к событию таким именем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1230">Since an event accessor implicitly has a parameter named `value`, it is a compile-time error for a local variable or constant declared in an event accessor to have that name.</span></span>

<span data-ttu-id="c51c7-1231">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1231">In the example</span></span>
```csharp
class Control: Component
{
    // Unique keys for events
    static readonly object mouseDownEventKey = new object();
    static readonly object mouseUpEventKey = new object();

    // Return event handler associated with key
    protected Delegate GetEventHandler(object key) {...}

    // Add event handler associated with key
    protected void AddEventHandler(object key, Delegate handler) {...}

    // Remove event handler associated with key
    protected void RemoveEventHandler(object key, Delegate handler) {...}

    // MouseDown event
    public event MouseEventHandler MouseDown {
        add { AddEventHandler(mouseDownEventKey, value); }
        remove { RemoveEventHandler(mouseDownEventKey, value); }
    }

    // MouseUp event
    public event MouseEventHandler MouseUp {
        add { AddEventHandler(mouseUpEventKey, value); }
        remove { RemoveEventHandler(mouseUpEventKey, value); }
    }

    // Invoke the MouseUp event
    protected void OnMouseUp(MouseEventArgs args) {
        MouseEventHandler handler; 
        handler = (MouseEventHandler)GetEventHandler(mouseUpEventKey);
        if (handler != null)
            handler(this, args);
    }
}
```
<span data-ttu-id="c51c7-1232">`Control` класс реализует механизм внутреннего хранилища для событий.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1232">the `Control` class implements an internal storage mechanism for events.</span></span> <span data-ttu-id="c51c7-1233">`AddEventHandler` Метод связывает значение делегата с ключом, `GetEventHandler` метод возвращает делегат, который сейчас связан с ключом и `RemoveEventHandler` метод удаляет делегат в качестве обработчика событий для указанного события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1233">The `AddEventHandler` method associates a delegate value with a key, the `GetEventHandler` method returns the delegate currently associated with a key, and the `RemoveEventHandler` method removes a delegate as an event handler for the specified event.</span></span> <span data-ttu-id="c51c7-1234">Предположительно, базовый механизм хранения разработан таким образом, что плата не для связывания `null` делегировать значение с ключом, и таким образом необработанные события использования места для хранения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1234">Presumably, the underlying storage mechanism is designed such that there is no cost for associating a `null` delegate value with a key, and thus unhandled events consume no storage.</span></span>

### <a name="static-and-instance-events"></a><span data-ttu-id="c51c7-1235">Экземпляра и статические события</span><span class="sxs-lookup"><span data-stu-id="c51c7-1235">Static and instance events</span></span>

<span data-ttu-id="c51c7-1236">Если объявление события содержит `static` модификатор, событие считается ***статическое событие***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1236">When an event declaration includes a `static` modifier, the event is said to be a ***static event***.</span></span> <span data-ttu-id="c51c7-1237">Если аргумент `static` модификатор присутствует, событие считается ***события экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1237">When no `static` modifier is present, the event is said to be an ***instance event***.</span></span>

<span data-ttu-id="c51c7-1238">Статическое событие не связан с конкретным экземпляром, и произошла ошибка во время компиляции, для ссылки на `this` в методах доступа статическое событие.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1238">A static event is not associated with a specific instance, and it is a compile-time error to refer to `this` in the accessors of a static event.</span></span>

<span data-ttu-id="c51c7-1239">Событие экземпляра связан с данным экземпляром класса, и этот экземпляр может быть доступен как `this` ([такой доступ](expressions.md#this-access)) в методах доступа этого события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1239">An instance event is associated with a given instance of a class, and this instance can be accessed as `this` ([This access](expressions.md#this-access)) in the accessors of that event.</span></span>

<span data-ttu-id="c51c7-1240">Если ссылка на событие в *member_access* ([доступ к членам](expressions.md#member-access)) формы `E.M`, если `M` — это статическое событие, `E` необходимо обозначить тип, содержащий `M`и если `M` — это событие экземпляра E должно означать экземпляр типа, содержащего `M`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1240">When an event is referenced in a *member_access* ([Member access](expressions.md#member-access)) of the form `E.M`, if `M` is a static event, `E` must denote a type containing `M`, and if `M` is an instance event, E must denote an instance of a type containing `M`.</span></span>

<span data-ttu-id="c51c7-1241">Различия между статическими и члены экземпляра рассматриваются далее в [экземпляра и статические члены](classes.md#static-and-instance-members).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1241">The differences between static and instance members are discussed further in [Static and instance members](classes.md#static-and-instance-members).</span></span>

### <a name="virtual-sealed-override-and-abstract-event-accessors"></a><span data-ttu-id="c51c7-1242">Виртуальные, запечатанные, переопределяющие и абстрактные доступа к событиям</span><span class="sxs-lookup"><span data-stu-id="c51c7-1242">Virtual, sealed, override, and abstract event accessors</span></span>

<span data-ttu-id="c51c7-1243">Объект `virtual` объявление события указывает, что виртуальные методы доступа этого события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1243">A `virtual` event declaration specifies that the accessors of that event are virtual.</span></span> <span data-ttu-id="c51c7-1244">`virtual` Модификатор применяется к оба метода доступа события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1244">The `virtual` modifier applies to both accessors of an event.</span></span>

<span data-ttu-id="c51c7-1245">`abstract` Объявление события указывает, что виртуальные методы доступа события, но не предоставляет фактической реализации методов доступа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1245">An `abstract` event declaration specifies that the accessors of the event are virtual, but does not provide an actual implementation of the accessors.</span></span> <span data-ttu-id="c51c7-1246">Вместо этого неабстрактные производные классы, обязаны предоставлять собственную реализацию для методов доступа посредством переопределения события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1246">Instead, non-abstract derived classes are required to provide their own implementation for the accessors by overriding the event.</span></span> <span data-ttu-id="c51c7-1247">Поскольку объявление абстрактного события не предоставляет фактической реализации, он не может предоставить разделенный фигурную скобку *event_accessor_declarations*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1247">Because an abstract event declaration provides no actual implementation, it cannot provide brace-delimited *event_accessor_declarations*.</span></span>

<span data-ttu-id="c51c7-1248">Объявление события, который включает в себя `abstract` и `override` модификаторов указывает, что событие является абстрактным и переопределяет базовое событие.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1248">An event declaration that includes both the `abstract` and `override` modifiers specifies that the event is abstract and overrides a base event.</span></span> <span data-ttu-id="c51c7-1249">Методы доступа такого события также являются абстрактными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1249">The accessors of such an event are also abstract.</span></span>

<span data-ttu-id="c51c7-1250">Объявления абстрактных событий разрешены только в абстрактных классах ([абстрактные классы](classes.md#abstract-classes)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1250">Abstract event declarations are only permitted in abstract classes ([Abstract classes](classes.md#abstract-classes)).</span></span>

<span data-ttu-id="c51c7-1251">Методы доступа унаследованного виртуального события могут переопределяться в производном классе, включив объявление события, которое указывает `override` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1251">The accessors of an inherited virtual event can be overridden in a derived class by including an event declaration that specifies an `override` modifier.</span></span> <span data-ttu-id="c51c7-1252">Этот процесс называется ***переопределение объявление события***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1252">This is known as an ***overriding event declaration***.</span></span> <span data-ttu-id="c51c7-1253">Переопределяющее объявление события не объявляет новое событие.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1253">An overriding event declaration does not declare a new event.</span></span> <span data-ttu-id="c51c7-1254">Вместо этого он просто специализирует реализации методов доступа существующего виртуального события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1254">Instead, it simply specializes the implementations of the accessors of an existing virtual event.</span></span>

<span data-ttu-id="c51c7-1255">Переопределяющее объявление событий необходимо указать точно такие же модификаторы доступа, тип и имя как переопределенный событие.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1255">An overriding event declaration must specify the exact same accessibility modifiers, type, and name as the overridden event.</span></span>

<span data-ttu-id="c51c7-1256">Переопределяющее объявление события может включать `sealed` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1256">An overriding event declaration may include the `sealed` modifier.</span></span> <span data-ttu-id="c51c7-1257">Использование этот модификатор препятствует дальнейшей переопределения события производном классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1257">Use of this modifier prevents a derived class from further overriding the event.</span></span> <span data-ttu-id="c51c7-1258">Методы доступа запечатанного события также являются запечатанными.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1258">The accessors of a sealed event are also sealed.</span></span>

<span data-ttu-id="c51c7-1259">Произошла ошибка во время компиляции для Переопределяющее объявление событий для включения `new` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1259">It is a compile-time error for an overriding event declaration to include a `new` modifier.</span></span>

<span data-ttu-id="c51c7-1260">За исключением отличий в объявление и вызов синтаксиса, виртуальных, запечатанных, переопределяющие и абстрактные методы доступа ведут себя так же, как виртуальный, запечатанных, переопределение и абстрактные методы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1260">Except for differences in declaration and invocation syntax, virtual, sealed, override, and abstract accessors behave exactly like virtual, sealed, override and abstract methods.</span></span> <span data-ttu-id="c51c7-1261">В частности, правила описываются в [виртуальных методов](classes.md#virtual-methods), [переопределять методы](classes.md#override-methods), [запечатанные методы](classes.md#sealed-methods), и [абстрактные методы](classes.md#abstract-methods) применяются так, как если методы доступа были методы из соответствующей формы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1261">Specifically, the rules described in [Virtual methods](classes.md#virtual-methods), [Override methods](classes.md#override-methods), [Sealed methods](classes.md#sealed-methods), and [Abstract methods](classes.md#abstract-methods) apply as if accessors were methods of a corresponding form.</span></span> <span data-ttu-id="c51c7-1262">Каждый метод доступа соответствует методу с параметром одиночное значение типа события `void` возвращают тип и модификаторов содержащего события.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1262">Each accessor corresponds to a method with a single value parameter of the event type, a `void` return type, and the same modifiers as the containing event.</span></span>

## <a name="indexers"></a><span data-ttu-id="c51c7-1263">Индексаторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1263">Indexers</span></span>

<span data-ttu-id="c51c7-1264">***Индексатора*** является членом, который позволяет объекту индексировать так же, как массив.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1264">An ***indexer*** is a member that enables an object to be indexed in the same way as an array.</span></span> <span data-ttu-id="c51c7-1265">Индексаторы объявляются с помощью *indexer_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1265">Indexers are declared using *indexer_declaration*s:</span></span>

```antlr
indexer_declaration
    : attributes? indexer_modifier* indexer_declarator indexer_body
    ;

indexer_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'virtual'
    | 'sealed'
    | 'override'
    | 'abstract'
    | 'extern'
    | indexer_modifier_unsafe
    ;

indexer_declarator
    : type 'this' '[' formal_parameter_list ']'
    | type interface_type '.' 'this' '[' formal_parameter_list ']'
    ;

indexer_body
    : '{' accessor_declarations '}' 
    | '=>' expression ';'
    ;
```

<span data-ttu-id="c51c7-1266">*Indexer_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)) и является допустимой комбинацией четырех модификаторов доступа ([модификаторы доступа ](classes.md#access-modifiers)), `new` ([Модификатор new](classes.md#the-new-modifier)), `virtual` ([виртуальных методов](classes.md#virtual-methods)), `override` ([переопределять методы](classes.md#override-methods) ), `sealed` ([Запечатанные методы](classes.md#sealed-methods)), `abstract` ([абстрактные методы](classes.md#abstract-methods)), и `extern` ([внешние методы](classes.md#external-methods)) модификаторы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1266">An *indexer_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), the `new` ([The new modifier](classes.md#the-new-modifier)), `virtual` ([Virtual methods](classes.md#virtual-methods)), `override` ([Override methods](classes.md#override-methods)), `sealed` ([Sealed methods](classes.md#sealed-methods)), `abstract` ([Abstract methods](classes.md#abstract-methods)), and `extern` ([External methods](classes.md#external-methods)) modifiers.</span></span>

<span data-ttu-id="c51c7-1267">Объявления индексаторов подчиняются тем же правилам, что и объявления методов ([методы](classes.md#methods)) по отношению к допустимые сочетания модификаторов, за одним исключением, что модификатор static не допускается в объявлении индексатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1267">Indexer declarations are subject to the same rules as method declarations ([Methods](classes.md#methods)) with regard to valid combinations of modifiers, with the one exception being that the static modifier is not permitted on an indexer declaration.</span></span>

<span data-ttu-id="c51c7-1268">Модификаторы `virtual`, `override`, и `abstract` являются взаимоисключающими, за исключением одного случая.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1268">The modifiers `virtual`, `override`, and `abstract` are mutually exclusive except in one case.</span></span> <span data-ttu-id="c51c7-1269">`abstract` И `override` модификаторы могут быть использованы вместе, таким образом, абстрактный индексатор может переопределить виртуальный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1269">The `abstract` and `override` modifiers may be used together so that an abstract indexer can override a virtual one.</span></span>

<span data-ttu-id="c51c7-1270">*Тип* индексатора объявление задает тип элемента индексатора, представленные этим определением.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1270">The *type* of an indexer declaration specifies the element type of the indexer introduced by the declaration.</span></span> <span data-ttu-id="c51c7-1271">Если индексатор не явная реализация члена интерфейса, *тип* следовать ключевое слово `this`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1271">Unless the indexer is an explicit interface member implementation, the *type* is followed by the keyword `this`.</span></span> <span data-ttu-id="c51c7-1272">Для явной реализации члена интерфейса *тип* следуют *interface_type*, "`.`«и ключевое слово `this`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1272">For an explicit interface member implementation, the *type* is followed by an *interface_type*, a "`.`", and the keyword `this`.</span></span> <span data-ttu-id="c51c7-1273">В отличие от других членов индексаторы не имеют пользовательских имен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1273">Unlike other members, indexers do not have user-defined names.</span></span>

<span data-ttu-id="c51c7-1274">*Formal_parameter_list* указывает параметры индексатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1274">The *formal_parameter_list* specifies the parameters of the indexer.</span></span> <span data-ttu-id="c51c7-1275">Список формальных параметров индексатора соответствует сигнатуре метода ([параметры метода](classes.md#method-parameters)), за исключением того, что по крайней мере один параметр должен быть указан и что `ref` и `out` модификаторов параметров не разрешены. .</span><span class="sxs-lookup"><span data-stu-id="c51c7-1275">The formal parameter list of an indexer corresponds to that of a method ([Method parameters](classes.md#method-parameters)), except that at least one parameter must be specified, and that the `ref` and `out` parameter modifiers are not permitted.</span></span>

<span data-ttu-id="c51c7-1276">*Тип* индексатор, и каждый из типов, на которые ссылается *formal_parameter_list* должен иметь по крайней мере такой же уровень доступности, как и сам индексатор ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1276">The *type* of an indexer and each of the types referenced in the *formal_parameter_list* must be at least as accessible as the indexer itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-1277">*Indexer_body* может либо состоять из ***тела метода доступа*** или ***тело выражения***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1277">An *indexer_body* may either consist of an ***accessor body*** or an ***expression body***.</span></span> <span data-ttu-id="c51c7-1278">В тело метода доступа *accessor_declarations*, которые должны быть заключены в "`{`«и»`}`" токены, объявите методы доступа ([методы доступа](classes.md#accessors)) свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1278">In an accessor body, *accessor_declarations*, which must be enclosed in "`{`" and "`}`" tokens, declare the accessors ([Accessors](classes.md#accessors)) of the property.</span></span> <span data-ttu-id="c51c7-1279">Методы доступа укажите исполняемые операторы, связанные с чтением и записью свойство.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1279">The accessors specify the executable statements associated with reading and writing the property.</span></span>

<span data-ttu-id="c51c7-1280">Тело выражения, состоящий из "`=>`" за которым следует выражение `E` и точку с запятой полностью эквивалентен тела оператора `{ get { return E; } }`и поэтому только позволяют указать индексаторы только для считывания результат метода получения Указывает одно выражение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1280">An expression body consisting of "`=>`" followed by an expression `E` and a semicolon is exactly equivalent to the statement body `{ get { return E; } }`, and can therefore only be used to specify getter-only indexers where the result of the getter is given by a single expression.</span></span>

<span data-ttu-id="c51c7-1281">Несмотря на то, что синтаксис для доступа к элементу индексатора такой же, что и элемент массива, элемент индексатора не классифицируется как переменная.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1281">Even though the syntax for accessing an indexer element is the same as that for an array element, an indexer element is not classified as a variable.</span></span> <span data-ttu-id="c51c7-1282">Таким образом, он не поддерживается для передачи элемента индексатора в качестве `ref` или `out` аргумент.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1282">Thus, it is not possible to pass an indexer element as a `ref` or `out` argument.</span></span>

<span data-ttu-id="c51c7-1283">Список формальных параметров индексатора определяет подпись ([сигнатуры и перегрузка](basic-concepts.md#signatures-and-overloading)) индексатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1283">The formal parameter list of an indexer defines the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of the indexer.</span></span> <span data-ttu-id="c51c7-1284">В частности Сигнатура индексатора состоит из количество и типы его формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1284">Specifically, the signature of an indexer consists of the number and types of its formal parameters.</span></span> <span data-ttu-id="c51c7-1285">Тип элементов и имена формальных параметров не являются частью сигнатуры индексатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1285">The element type and names of the formal parameters are not part of an indexer's signature.</span></span>

<span data-ttu-id="c51c7-1286">Сигнатура индексатора должна отличаться от сигнатур любых других индексаторов, объявленных в том же классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1286">The signature of an indexer must differ from the signatures of all other indexers declared in the same class.</span></span>

<span data-ttu-id="c51c7-1287">Индексаторы и свойства очень похожи на концепцию, но отличаются следующими способами:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1287">Indexers and properties are very similar in concept, but differ in the following ways:</span></span>

*  <span data-ttu-id="c51c7-1288">Свойство определяется по его имени, тогда как индексатор, который идентифицируется по его подпись.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1288">A property is identified by its name, whereas an indexer is identified by its signature.</span></span>
*  <span data-ttu-id="c51c7-1289">Свойство осуществляется через *simple_name* ([простые имена](expressions.md#simple-names)) или *member_access* ([доступ к членам](expressions.md#member-access)), тогда как индексатор доступ к элементу через *element_access* ([доступа к индексатору](expressions.md#indexer-access)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1289">A property is accessed through a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)), whereas an indexer element is accessed through an *element_access* ([Indexer access](expressions.md#indexer-access)).</span></span>
*  <span data-ttu-id="c51c7-1290">Свойство может быть `static` член, тогда как индексатор, который всегда является членом экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1290">A property can be a `static` member, whereas an indexer is always an instance member.</span></span>
*  <span data-ttu-id="c51c7-1291">Объект `get` метод доступа свойства соответствует методу без параметров, тогда как `get` метода доступа индексатора соответствует методу с тот же список формальных параметров, что и сам индексатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1291">A `get` accessor of a property corresponds to a method with no parameters, whereas a `get` accessor of an indexer corresponds to a method with the same formal parameter list as the indexer.</span></span>
*  <span data-ttu-id="c51c7-1292">Объект `set` метод доступа свойства соответствует методу с одним параметром с именем `value`, тогда как `set` соответствует методу с такой же список формальных параметров, как индексатор, а также дополнительный параметр метода доступа индексатора с именем `value`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1292">A `set` accessor of a property corresponds to a method with a single parameter named `value`, whereas a `set` accessor of an indexer corresponds to a method with the same formal parameter list as the indexer, plus an additional parameter named `value`.</span></span>
*  <span data-ttu-id="c51c7-1293">Это ошибка времени компиляции для метода доступа индексатора для объявления локальной переменной с тем же именем, что и параметр индексатора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1293">It is a compile-time error for an indexer accessor to declare a local variable with the same name as an indexer parameter.</span></span>
*  <span data-ttu-id="c51c7-1294">В Переопределяющее объявление свойства, наследуемое свойство осуществляется с помощью синтаксиса `base.P`, где `P` является именем свойства.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1294">In an overriding property declaration, the inherited property is accessed using the syntax `base.P`, where `P` is the property name.</span></span> <span data-ttu-id="c51c7-1295">В индексатор объявление переопределения наследуемых индексатор осуществляется с помощью синтаксиса `base[E]`, где `E` — это список выражений с разделителями-запятыми.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1295">In an overriding indexer declaration, the inherited indexer is accessed using the syntax `base[E]`, where `E` is a comma separated list of expressions.</span></span>
*  <span data-ttu-id="c51c7-1296">Отсутствует понятие «автоматически реализованного индексатора».</span><span class="sxs-lookup"><span data-stu-id="c51c7-1296">There is no concept of an "automatically implemented indexer".</span></span> <span data-ttu-id="c51c7-1297">Является ошибкой иметь абстрактным, не внешние индексатора с помощью методов доступа точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1297">It is an error to have a non-abstract, non-external indexer with semicolon accessors.</span></span>

<span data-ttu-id="c51c7-1298">Помимо этих различий, все правила, определенные в [методы доступа](classes.md#accessors) и [автоматически реализуемые свойства](classes.md#automatically-implemented-properties) применяются к методам доступа индексаторов также для доступа к свойствам.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1298">Aside from these differences, all rules defined in [Accessors](classes.md#accessors) and [Automatically implemented properties](classes.md#automatically-implemented-properties) apply to indexer accessors as well as to property accessors.</span></span>

<span data-ttu-id="c51c7-1299">Если объявление индексатора содержит `extern` модификатор, индексатор считается ***внешних индексатора***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1299">When an indexer declaration includes an `extern` modifier, the indexer is said to be an ***external indexer***.</span></span> <span data-ttu-id="c51c7-1300">Поскольку объявление внешнего индексатора не предоставляет фактической реализации, каждый из его *accessor_declarations* состоит из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1300">Because an external indexer declaration provides no actual implementation, each of its *accessor_declarations* consists of a semicolon.</span></span>

<span data-ttu-id="c51c7-1301">В приведенном ниже примере объявляется `BitArray` класса, реализующего индексатор для доступа к отдельным битам в битовом массиве.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1301">The example below declares a `BitArray` class that implements an indexer for accessing the individual bits in the bit array.</span></span>
```csharp
using System;

class BitArray
{
    int[] bits;
    int length;

    public BitArray(int length) {
        if (length < 0) throw new ArgumentException();
        bits = new int[((length - 1) >> 5) + 1];
        this.length = length;
    }

    public int Length {
        get { return length; }
    }

    public bool this[int index] {
        get {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            return (bits[index >> 5] & 1 << index) != 0;
        }
        set {
            if (index < 0 || index >= length) {
                throw new IndexOutOfRangeException();
            }
            if (value) {
                bits[index >> 5] |= 1 << index;
            }
            else {
                bits[index >> 5] &= ~(1 << index);
            }
        }
    }
}
```

<span data-ttu-id="c51c7-1302">Экземпляр `BitArray` класса занимает значительно меньше памяти, чем соответствующий `bool[]` (так как каждое значение первого занимает только один бит, а не последнее – один байт), но позволяет выполнять те же операции `bool[]`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1302">An instance of the `BitArray` class consumes substantially less memory than a corresponding `bool[]` (since each value of the former occupies only one bit instead of the latter's one byte), but it permits the same operations as a `bool[]`.</span></span>

<span data-ttu-id="c51c7-1303">Следующие `CountPrimes` класс использует `BitArray` и классические алгоритма «решето» для вычисления количества простых чисел от 1 до заданного максимального:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1303">The following `CountPrimes` class uses a `BitArray` and the classical "sieve" algorithm to compute the number of primes between 1 and a given maximum:</span></span>
```csharp
class CountPrimes
{
    static int Count(int max) {
        BitArray flags = new BitArray(max + 1);
        int count = 1;
        for (int i = 2; i <= max; i++) {
            if (!flags[i]) {
                for (int j = i * 2; j <= max; j += i) flags[j] = true;
                count++;
            }
        }
        return count;
    }

    static void Main(string[] args) {
        int max = int.Parse(args[0]);
        int count = Count(max);
        Console.WriteLine("Found {0} primes between 1 and {1}", count, max);
    }
}
```

<span data-ttu-id="c51c7-1304">Обратите внимание, что синтаксис для доступа к элементам `BitArray` именно так же, как `bool[]`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1304">Note that the syntax for accessing elements of the `BitArray` is precisely the same as for a `bool[]`.</span></span>

<span data-ttu-id="c51c7-1305">В следующем примере показан класс сетки 26 \* 10 с индексатором с двумя параметрами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1305">The following example shows a 26 \* 10 grid class that has an indexer with two parameters.</span></span> <span data-ttu-id="c51c7-1306">Первый параметр должен быть верхнего или нижнего регистра в диапазоне A-Z, а второй должен быть целым числом в диапазоне 0 – 9.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1306">The first parameter is required to be an upper- or lowercase letter in the range A-Z, and the second is required to be an integer in the range 0-9.</span></span>

```csharp
using System;

class Grid
{
    const int NumRows = 26;
    const int NumCols = 10;

    int[,] cells = new int[NumRows, NumCols];

    public int this[char c, int col] {
        get {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            return cells[c - 'A', col];
        }

        set {
            c = Char.ToUpper(c);
            if (c < 'A' || c > 'Z') {
                throw new ArgumentException();
            }
            if (col < 0 || col >= NumCols) {
                throw new IndexOutOfRangeException();
            }
            cells[c - 'A', col] = value;
        }
    }
}
```

### <a name="indexer-overloading"></a><span data-ttu-id="c51c7-1307">Перегрузка индексатора</span><span class="sxs-lookup"><span data-stu-id="c51c7-1307">Indexer overloading</span></span>

<span data-ttu-id="c51c7-1308">Правила разрешения перегрузки индексаторов описаны в [вывод типа](expressions.md#type-inference).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1308">The indexer overload resolution rules are described in [Type inference](expressions.md#type-inference).</span></span>

## <a name="operators"></a><span data-ttu-id="c51c7-1309">Операторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1309">Operators</span></span>

<span data-ttu-id="c51c7-1310">***Оператор*** является членом, который определяет значение оператора выражения, которые могут применяться к экземплярам класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1310">An ***operator*** is a member that defines the meaning of an expression operator that can be applied to instances of the class.</span></span> <span data-ttu-id="c51c7-1311">Операторы объявляются с помощью *operator_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1311">Operators are declared using *operator_declaration*s:</span></span>

```antlr
operator_declaration
    : attributes? operator_modifier+ operator_declarator operator_body
    ;

operator_modifier
    : 'public'
    | 'static'
    | 'extern'
    | operator_modifier_unsafe
    ;

operator_declarator
    : unary_operator_declarator
    | binary_operator_declarator
    | conversion_operator_declarator
    ;

unary_operator_declarator
    : type 'operator' overloadable_unary_operator '(' type identifier ')'
    ;

overloadable_unary_operator
    : '+' | '-' | '!' | '~' | '++' | '--' | 'true' | 'false'
    ;

binary_operator_declarator
    : type 'operator' overloadable_binary_operator '(' type identifier ',' type identifier ')'
    ;

overloadable_binary_operator
    : '+'   | '-'   | '*'   | '/'   | '%'   | '&'   | '|'   | '^'   | '<<'
    | 'right_shift' | '=='  | '!='  | '>'   | '<'   | '>='  | '<='
    ;

conversion_operator_declarator
    : 'implicit' 'operator' type '(' type identifier ')'
    | 'explicit' 'operator' type '(' type identifier ')'
    ;

operator_body
    : block
    | '=>' expression ';'
    | ';'
    ;
```

<span data-ttu-id="c51c7-1312">Существует три категории перегружаемых операторов: унарные операторы ([унарные операторы](classes.md#unary-operators)), бинарные операторы ([бинарные операторы](classes.md#binary-operators)) и операторы преобразования ([операторы преобразования ](classes.md#conversion-operators)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1312">There are three categories of overloadable operators: Unary operators ([Unary operators](classes.md#unary-operators)), binary operators ([Binary operators](classes.md#binary-operators)), and conversion operators ([Conversion operators](classes.md#conversion-operators)).</span></span>

<span data-ttu-id="c51c7-1313">*Operator_body* либо точкой с запятой, ***тела оператора*** или ***тело выражения***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1313">The *operator_body* is either a semicolon, a ***statement body*** or an ***expression body***.</span></span> <span data-ttu-id="c51c7-1314">Состоит из тела оператора *блок*, который задает операторы, выполняемые при вызове оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1314">A statement body consists of a *block*, which specifies the statements to execute when the operator is invoked.</span></span> <span data-ttu-id="c51c7-1315">*Блок* должны соответствовать правилам для возвращающих значения методов, описанных в [тело метода](classes.md#method-body).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1315">The *block* must conform to the rules for value-returning methods described in [Method body](classes.md#method-body).</span></span> <span data-ttu-id="c51c7-1316">Тело выражения состоит из `=>` за которым следует выражение и точку с запятой и обозначает одно выражение для выполнения при вызове этого оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1316">An expression body consists of `=>` followed by an expression and a semicolon, and denotes a single expression to perform when the operator is invoked.</span></span>

<span data-ttu-id="c51c7-1317">Для `extern` операторы, *operator_body* состоит просто из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1317">For `extern` operators, the *operator_body* consists simply of a semicolon.</span></span> <span data-ttu-id="c51c7-1318">Для всех других операторов *operator_body* тело блока или тело выражения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1318">For all other operators, the *operator_body* is either a block body or an expression body.</span></span>

<span data-ttu-id="c51c7-1319">Следующие правила применяются ко всем объявлениям оператор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1319">The following rules apply to all operator declarations:</span></span>

*  <span data-ttu-id="c51c7-1320">В объявлении оператора должен содержать два `public` и `static` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1320">An operator declaration must include both a `public` and a `static` modifier.</span></span>
*  <span data-ttu-id="c51c7-1321">Параметры оператора должны быть параметрами значений ([параметры по значению](variables.md#value-parameters)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1321">The parameter(s) of an operator must be value parameters ([Value parameters](variables.md#value-parameters)).</span></span> <span data-ttu-id="c51c7-1322">Произошла ошибка во время компиляции, оператор объявления для указания `ref` или `out` параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1322">It is a compile-time error for an operator declaration to specify `ref` or `out` parameters.</span></span>
*  <span data-ttu-id="c51c7-1323">Сигнатура оператора ([унарные операторы](classes.md#unary-operators), [бинарные операторы](classes.md#binary-operators), [операторы преобразования](classes.md#conversion-operators)) должен отличаться от сигнатур все операторы, объявленные в того же класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1323">The signature of an operator ([Unary operators](classes.md#unary-operators), [Binary operators](classes.md#binary-operators), [Conversion operators](classes.md#conversion-operators)) must differ from the signatures of all other operators declared in the same class.</span></span>
*  <span data-ttu-id="c51c7-1324">Все типы, упоминаемые в объявлении оператора должен быть по крайней мере такой же уровень доступности, как и сам оператор ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1324">All types referenced in an operator declaration must be at least as accessible as the operator itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>
*  <span data-ttu-id="c51c7-1325">Является ошибкой один и тот же модификатор встречается несколько раз в объявлении оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1325">It is an error for the same modifier to appear multiple times in an operator declaration.</span></span>

<span data-ttu-id="c51c7-1326">Каждая категория операторов налагаются дополнительные ограничения, как описано в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1326">Each operator category imposes additional restrictions, as described in the following sections.</span></span>

<span data-ttu-id="c51c7-1327">Как и другие члены операторы, объявленные в базовом классе, наследуются производными классами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1327">Like other members, operators declared in a base class are inherited by derived classes.</span></span> <span data-ttu-id="c51c7-1328">Поскольку объявления операторов всегда требуют класса или структуры, в котором объявлен оператор, для участия в сигнатуре оператор, он не поддерживается оператор объявлен в производном классе может скрыть оператор, объявленный в базовом классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1328">Because operator declarations always require the class or struct in which the operator is declared to participate in the signature of the operator, it is not possible for an operator declared in a derived class to hide an operator declared in a base class.</span></span> <span data-ttu-id="c51c7-1329">Таким образом `new` модификатор никогда не требуется и поэтому никогда не допускается в объявлении оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1329">Thus, the `new` modifier is never required, and therefore never permitted, in an operator declaration.</span></span>

<span data-ttu-id="c51c7-1330">Дополнительные сведения о унарные и бинарные операторы можно найти в [операторы](expressions.md#operators).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1330">Additional information on unary and binary operators can be found in [Operators](expressions.md#operators).</span></span>

<span data-ttu-id="c51c7-1331">Дополнительные сведения об операторах преобразования можно найти в [заданные пользователем преобразования](conversions.md#user-defined-conversions).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1331">Additional information on conversion operators can be found in [User-defined conversions](conversions.md#user-defined-conversions).</span></span>

### <a name="unary-operators"></a><span data-ttu-id="c51c7-1332">Унарные операторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1332">Unary operators</span></span>

<span data-ttu-id="c51c7-1333">Применяются следующие правила для унарного оператора объявления, где `T` обозначает тип экземпляра класса или структуры, который содержит объявление оператора:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1333">The following rules apply to unary operator declarations, where `T` denotes the instance type of the class or struct that contains the operator declaration:</span></span>

*  <span data-ttu-id="c51c7-1334">Унарное `+`, `-`, `!`, или `~` оператор должен принимать один параметр типа `T` или `T?` и могут возвращать любой тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1334">A unary `+`, `-`, `!`, or `~` operator must take a single parameter of type `T` or `T?` and can return any type.</span></span>
*  <span data-ttu-id="c51c7-1335">Унарное `++` или `--` оператор должен принимать один параметр типа `T` или `T?` и должен возвращать что же тип или тип, производный от него.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1335">A unary `++` or `--` operator must take a single parameter of type `T` or `T?` and must return that same type or a type derived from it.</span></span>
*  <span data-ttu-id="c51c7-1336">Унарное `true` или `false` оператор должен принимать один параметр типа `T` или `T?` и должен возвращать тип `bool`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1336">A unary `true` or `false` operator must take a single parameter of type `T` or `T?` and must return type `bool`.</span></span>

<span data-ttu-id="c51c7-1337">Подпись унарного оператора состоит из лексема оператора (`+`, `-`, `!`, `~`, `++`, `--`, `true`, или `false`) и одним формальным параметром типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1337">The signature of a unary operator consists of the operator token (`+`, `-`, `!`, `~`, `++`, `--`, `true`, or `false`) and the type of the single formal parameter.</span></span> <span data-ttu-id="c51c7-1338">Тип возвращаемого значения не является частью сигнатуры унарного оператора, ни имя формального параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1338">The return type is not part of a unary operator's signature, nor is the name of the formal parameter.</span></span>

<span data-ttu-id="c51c7-1339">`true` И `false` унарные операторы требуется попарное объявление.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1339">The `true` and `false` unary operators require pair-wise declaration.</span></span> <span data-ttu-id="c51c7-1340">Ошибка времени компиляции возникает, если класс объявляет один из этих операторов без объявления другого.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1340">A compile-time error occurs if a class declares one of these operators without also declaring the other.</span></span> <span data-ttu-id="c51c7-1341">`true` И `false` операторы описаны далее в [пользовательские условные логические операторы](expressions.md#user-defined-conditional-logical-operators) и [логических выражений](expressions.md#boolean-expressions).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1341">The `true` and `false` operators are described further in [User-defined conditional logical operators](expressions.md#user-defined-conditional-logical-operators) and [Boolean expressions](expressions.md#boolean-expressions).</span></span>

<span data-ttu-id="c51c7-1342">В следующем примере показано, реализация и последующее применение `operator ++` для класса целочисленного вектора:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1342">The following example shows an implementation and subsequent usage of `operator ++` for an integer vector class:</span></span>
```csharp
public class IntVector
{
    public IntVector(int length) {...}

    public int Length {...}                 // read-only property

    public int this[int index] {...}        // read-write indexer

    public static IntVector operator ++(IntVector iv) {
        IntVector temp = new IntVector(iv.Length);
        for (int i = 0; i < iv.Length; i++)
            temp[i] = iv[i] + 1;
        return temp;
    }
}

class Test
{
    static void Main() {
        IntVector iv1 = new IntVector(4);    // vector of 4 x 0
        IntVector iv2;

        iv2 = iv1++;    // iv2 contains 4 x 0, iv1 contains 4 x 1
        iv2 = ++iv1;    // iv2 contains 4 x 2, iv1 contains 4 x 2
    }
}
```

<span data-ttu-id="c51c7-1343">Обратите внимание на то, как метод оператора возвращает значение, полученное путем прибавления единицы к операнду, так же, как постфиксного инкремента и декремента ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators)) и префикс инкремента и декремента операторы ([префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1343">Note how the operator method returns the value produced by adding 1 to the operand, just like the  postfix increment and decrement operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators)), and the prefix increment and decrement operators ([Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span> <span data-ttu-id="c51c7-1344">В отличие от в C++, этот метод нужен не изменяйте значение своего операнда напрямую.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1344">Unlike in C++, this method need not modify the value of its operand directly.</span></span> <span data-ttu-id="c51c7-1345">На самом деле изменение значения операнда нарушило бы стандартной семантики постфиксного оператора инкремента.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1345">In fact, modifying the operand value would violate the standard semantics of the postfix increment operator.</span></span>

### <a name="binary-operators"></a><span data-ttu-id="c51c7-1346">Бинарные операторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1346">Binary operators</span></span>

<span data-ttu-id="c51c7-1347">Применяются следующие правила для бинарного оператора объявления, где `T` обозначает тип экземпляра класса или структуры, который содержит объявление оператора:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1347">The following rules apply to binary operator declarations, where `T` denotes the instance type of the class or struct that contains the operator declaration:</span></span>

*  <span data-ttu-id="c51c7-1348">Бинарный оператор сдвига не должно принимать два параметра, по крайней мере один из которых должен иметь тип `T` или `T?`и могут возвращать любой тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1348">A binary non-shift operator must take two parameters, at least one of which must have type `T` or `T?`, and can return any type.</span></span>
*  <span data-ttu-id="c51c7-1349">Двоичный файл `<<` или `>>` оператор должен принимать два параметра, первая из которых должен иметь тип `T` или `T?` и второй из которых должен иметь тип `int` или `int?`и могут возвращать любой тип.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1349">A binary `<<` or `>>` operator must take two parameters, the first of which must have type `T` or `T?` and the second of which must have type `int` or `int?`, and can return any type.</span></span>

<span data-ttu-id="c51c7-1350">Подпись бинарного оператора состоит из лексема оператора (`+`, `-`, `*`, `/`, `%`, `&`, `|`, `^`, `<<`, `>>`, `==`, `!=`, `>`, `<`, `>=`, или `<=`) и типы двух формальных параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1350">The signature of a binary operator consists of the operator token (`+`, `-`, `*`, `/`, `%`, `&`, `|`, `^`, `<<`, `>>`, `==`, `!=`, `>`, `<`, `>=`, or `<=`) and the types of the two formal parameters.</span></span> <span data-ttu-id="c51c7-1351">Тип возвращаемого значения и имена формальных параметров не являются частью сигнатуры бинарного оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1351">The return type and the names of the formal parameters are not part of a binary operator's signature.</span></span>

<span data-ttu-id="c51c7-1352">Для некоторых бинарных операторов требуется попарное объявление.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1352">Certain binary operators require pair-wise declaration.</span></span> <span data-ttu-id="c51c7-1353">Для каждого объявления одного из операторов пары необходимо соответствующее объявление оператора другие пары.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1353">For every declaration of either operator of a pair, there must be a matching declaration of the other operator of the pair.</span></span> <span data-ttu-id="c51c7-1354">Два объявления оператора совпадать, если они имеют тот же тип возвращаемого значения и тот же тип для каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1354">Two operator declarations match when they have the same return type and the same type for each parameter.</span></span> <span data-ttu-id="c51c7-1355">Следующие операторы требуется попарное объявление:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1355">The following operators require pair-wise declaration:</span></span>

*  <span data-ttu-id="c51c7-1356">`operator ==` и `operator !=`</span><span class="sxs-lookup"><span data-stu-id="c51c7-1356">`operator ==` and `operator !=`</span></span>
*  <span data-ttu-id="c51c7-1357">`operator >` и `operator <`</span><span class="sxs-lookup"><span data-stu-id="c51c7-1357">`operator >` and `operator <`</span></span>
*  <span data-ttu-id="c51c7-1358">`operator >=` и `operator <=`</span><span class="sxs-lookup"><span data-stu-id="c51c7-1358">`operator >=` and `operator <=`</span></span>

### <a name="conversion-operators"></a><span data-ttu-id="c51c7-1359">Операторы преобразования</span><span class="sxs-lookup"><span data-stu-id="c51c7-1359">Conversion operators</span></span>

<span data-ttu-id="c51c7-1360">Объявление оператора преобразования вводит ***определенное пользователем преобразование*** ([заданные пользователем преобразования](conversions.md#user-defined-conversions)) которое дополняет предопределенные явные и неявные преобразования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1360">A conversion operator declaration introduces a ***user-defined conversion*** ([User-defined conversions](conversions.md#user-defined-conversions)) which augments the pre-defined implicit and explicit conversions.</span></span>

<span data-ttu-id="c51c7-1361">Объявление оператора преобразования, который включает в себя `implicit` ключевое слово представляет неявное преобразование, определяемые пользователем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1361">A conversion operator declaration that includes the `implicit` keyword introduces a user-defined implicit conversion.</span></span> <span data-ttu-id="c51c7-1362">Неявные преобразования могут происходить в разнообразных ситуациях, включая вызовы членов функций, выражения приведения и назначения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1362">Implicit conversions can occur in a variety of situations, including function member invocations, cast expressions, and assignments.</span></span> <span data-ttu-id="c51c7-1363">Это описано далее в [неявные преобразования](conversions.md#implicit-conversions).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1363">This is described further in [Implicit conversions](conversions.md#implicit-conversions).</span></span>

<span data-ttu-id="c51c7-1364">Объявление оператора преобразования, который включает в себя `explicit` ключевое слово представляет явное преобразование, определяемые пользователем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1364">A conversion operator declaration that includes the `explicit` keyword introduces a user-defined explicit conversion.</span></span> <span data-ttu-id="c51c7-1365">Явные преобразования могут возникать в выражения приведения, а также описаны далее в [явные преобразования](conversions.md#explicit-conversions).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1365">Explicit conversions can occur in cast expressions, and are described further in [Explicit conversions](conversions.md#explicit-conversions).</span></span>

<span data-ttu-id="c51c7-1366">Оператор преобразования преобразует из исходного типа, указанного по типу параметра оператор преобразования в целевой тип, указанный типом возвращаемого значения оператора преобразования.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1366">A conversion operator converts from a source type, indicated by the parameter type of the conversion operator, to a target type, indicated by the return type of the conversion operator.</span></span>

<span data-ttu-id="c51c7-1367">Для заданного исходного типа `S` и целевого типа `T`, если `S` или `T` являются обнуляемые типы позволяют `S0` и `T0` называть их базовые типы, в противном случае `S0` и `T0` являются равным `S` и `T` соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1367">For a given source type `S` and target type `T`, if `S` or `T` are nullable types, let `S0` and `T0` refer to their underlying types, otherwise `S0` and `T0` are equal to `S` and `T` respectively.</span></span> <span data-ttu-id="c51c7-1368">Класс или структура может объявлять преобразование из типа источника `S` с целевым типом `T` только в том случае, если выполняются все следующие условия:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1368">A class or struct is permitted to declare a conversion from a source type `S` to a target type `T` only if all of the following are true:</span></span>

*  <span data-ttu-id="c51c7-1369">`S0` и `T0` различных типов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1369">`S0` and `T0` are different types.</span></span>
*  <span data-ttu-id="c51c7-1370">Либо `S0` или `T0` — это тип класса или структуры, в котором происходит объявление оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1370">Either `S0` or `T0` is the class or struct type in which the operator declaration takes place.</span></span>
*  <span data-ttu-id="c51c7-1371">Ни `S0` , ни `T0` — *interface_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1371">Neither `S0` nor `T0` is an *interface_type*.</span></span>
*  <span data-ttu-id="c51c7-1372">За исключением определенных пользователем преобразований, не существует преобразования из `S` для `T` или из `T` для `S`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1372">Excluding user-defined conversions, a conversion does not exist from `S` to `T` or from `T` to `S`.</span></span>

<span data-ttu-id="c51c7-1373">В рамках этих правил, любой тип, параметры, связанные с `S` или `T` считаются уникальных типов, имеющих отсутствует отношение наследования с другими типами и все ограничения на тип, эти параметры игнорируются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1373">For the purposes of these rules, any type parameters associated with `S` or `T` are considered to be unique types that have no inheritance relationship with other types, and any constraints on those type parameters are ignored.</span></span>

<span data-ttu-id="c51c7-1374">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1374">In the example</span></span>
```csharp
class C<T> {...}

class D<T>: C<T>
{
    public static implicit operator C<int>(D<T> value) {...}      // Ok
    public static implicit operator C<string>(D<T> value) {...}   // Ok
    public static implicit operator C<T>(D<T> value) {...}        // Error
}
```
<span data-ttu-id="c51c7-1375">Первые два объявления операторов разрешены, так, как в рамках [индексаторы](classes.md#indexers).3, `T` и `int` и `string` соответственно, считаются уникальными типами без отношений.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1375">the first two operator declarations are permitted because, for the purposes of [Indexers](classes.md#indexers).3, `T` and `int` and `string` respectively are considered unique types with no relationship.</span></span> <span data-ttu-id="c51c7-1376">Тем не менее, третий оператор является ошибкой, так как `C<T>` является базовым классом для `D<T>`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1376">However, the third operator is an error because `C<T>` is the base class of `D<T>`.</span></span>

<span data-ttu-id="c51c7-1377">Из второго правила следует, что оператор преобразования необходимо преобразовать в или из типа класса или структуры, в котором объявлен оператор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1377">From the second rule it follows that a conversion operator must convert either to or from the class or struct type in which the operator is declared.</span></span> <span data-ttu-id="c51c7-1378">К примеру, это возможно для типа класса или структуры `C` определить преобразование из `C` для `int` и из `int` для `C`, но не из `int` для `bool`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1378">For example, it is possible for a class or struct type `C` to define a conversion from `C` to `int` and from `int` to `C`, but not from `int` to `bool`.</span></span>

<span data-ttu-id="c51c7-1379">Это не невозможно непосредственно переопределить предопределенное преобразование.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1379">It is not possible to directly redefine a pre-defined conversion.</span></span> <span data-ttu-id="c51c7-1380">Таким образом, операторы преобразования не допускаются для преобразования в или из него `object` так, как явные и неявные преобразования, уже существующих между `object` и всех других типов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1380">Thus, conversion operators are not allowed to convert from or to `object` because implicit and explicit conversions already exist between `object` and all other types.</span></span> <span data-ttu-id="c51c7-1381">Аналогичным образом ни источник, ни типы целевых объектов преобразования может быть базовый тип, поскольку преобразование уже существует.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1381">Likewise, neither the source nor the target types of a conversion can be a base type of the other, since a conversion would then already exist.</span></span>

<span data-ttu-id="c51c7-1382">Тем не менее можно объявить операторы в универсальных типах, которые для определенного типа аргументов, указать преобразования, которые уже существуют в качестве предварительно определенных преобразований.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1382">However, it is possible to declare operators on generic types that, for particular type arguments, specify conversions that already exist as pre-defined conversions.</span></span> <span data-ttu-id="c51c7-1383">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1383">In the example</span></span>
```csharp
struct Convertible<T>
{
    public static implicit operator Convertible<T>(T value) {...}
    public static explicit operator T(Convertible<T> value) {...}
}
```
<span data-ttu-id="c51c7-1384">Если тип `object` указывается как аргумент типа для `T`, второй оператор объявляет преобразование, которое уже существует (неявным и поэтому также явно, существует преобразования из любой тип `object`).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1384">when type `object` is specified as a type argument for `T`, the second operator declares a conversion that already exists (an implicit, and therefore also an explicit, conversion exists from any type to type `object`).</span></span>

<span data-ttu-id="c51c7-1385">В случаях, где существует предопределенное преобразование между двумя типами пропускаются любые заданные пользователем преобразования между этими типами.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1385">In cases where a pre-defined conversion exists between two types, any user-defined conversions between those types are ignored.</span></span> <span data-ttu-id="c51c7-1386">В частности:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1386">Specifically:</span></span>

*  <span data-ttu-id="c51c7-1387">Если предопределенное неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) из типа `S` ввода `T`, все заданные пользователем преобразования (неявные или явные) из `S` для `T` игнорируются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1387">If a pre-defined implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from type `S` to type `T`, all user-defined conversions (implicit or explicit) from `S` to `T` are ignored.</span></span>
*  <span data-ttu-id="c51c7-1388">Если предварительно определенных явное преобразование ([явные преобразования](conversions.md#explicit-conversions)) из типа `S` ввода `T`, пользовательские явные преобразования из `S` для `T` игнорируются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1388">If a pre-defined explicit conversion ([Explicit conversions](conversions.md#explicit-conversions)) exists from type `S` to type `T`, any user-defined explicit conversions from `S` to `T` are ignored.</span></span> <span data-ttu-id="c51c7-1389">Более того:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1389">Furthermore:</span></span>

<span data-ttu-id="c51c7-1390">Если `T` является типом интерфейса, определяемые пользователем неявные преобразования из `S` для `T` игнорируются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1390">If `T` is an interface type, user-defined implicit conversions from `S` to `T` are ignored.</span></span>

<span data-ttu-id="c51c7-1391">В противном случае — определяемые пользователем неявные преобразования из `S` для `T` по-прежнему считаются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1391">Otherwise, user-defined implicit conversions from `S` to `T` are still considered.</span></span>

<span data-ttu-id="c51c7-1392">Для всех типов, но `object`, операторы, объявленные `Convertible<T>` выше тип не конфликтуют с предварительно определенных преобразований.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1392">For all types but `object`, the operators declared by the `Convertible<T>` type above do not conflict with pre-defined conversions.</span></span> <span data-ttu-id="c51c7-1393">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1393">For example:</span></span>
```csharp
void F(int i, Convertible<int> n) {
    i = n;                          // Error
    i = (int)n;                     // User-defined explicit conversion
    n = i;                          // User-defined implicit conversion
    n = (Convertible<int>)i;        // User-defined implicit conversion
}
```

<span data-ttu-id="c51c7-1394">Тем не менее, для типа `object`, предопределенные преобразования скрывают пользовательские преобразования в случаях все, кроме одного:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1394">However, for type `object`, pre-defined conversions hide the user-defined conversions in all cases but one:</span></span>

```csharp
void F(object o, Convertible<object> n) {
    o = n;                         // Pre-defined boxing conversion
    o = (object)n;                 // Pre-defined boxing conversion
    n = o;                         // User-defined implicit conversion
    n = (Convertible<object>)o;    // Pre-defined unboxing conversion
}
```

<span data-ttu-id="c51c7-1395">Заданные пользователем преобразования не допускаются для преобразования в или из него *interface_type*s.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1395">User-defined conversions are not allowed to convert from or to *interface_type*s.</span></span> <span data-ttu-id="c51c7-1396">В частности, это ограничение гарантирует, что без пользовательских преобразований возникают при преобразовании в *interface_type*и что преобразование *interface_type* завершается успешно только в том случае, если объект Преобразуемый действительно реализует указанный *interface_type*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1396">In particular, this restriction ensures that no user-defined transformations occur when converting to an *interface_type*, and that a conversion to an *interface_type* succeeds only if the object being converted actually implements the specified *interface_type*.</span></span>

<span data-ttu-id="c51c7-1397">Сигнатура оператора преобразования состоит из типа источника и целевого типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1397">The signature of a conversion operator consists of the source type and the target type.</span></span> <span data-ttu-id="c51c7-1398">(Обратите внимание, что это единственная форма, для которого тип возвращаемого значения участвует в сигнатуре члена). `implicit` Или `explicit` классификации оператора преобразования не является частью сигнатуры оператора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1398">(Note that this is the only form of member for which the return type participates in the signature.) The `implicit` or `explicit` classification of a conversion operator is not part of the operator's signature.</span></span> <span data-ttu-id="c51c7-1399">Таким образом, класс или структура не допускает объявления обоих `implicit` и `explicit` оператор преобразования с теми же типами исходной и целевой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1399">Thus, a class or struct cannot declare both an `implicit` and an `explicit` conversion operator with the same source and target types.</span></span>

<span data-ttu-id="c51c7-1400">Как правило определяемые пользователем неявные преобразования должны разрабатываться никогда не вызывать исключения и не должны терять данные.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1400">In general, user-defined implicit conversions should be designed to never throw exceptions and never lose information.</span></span> <span data-ttu-id="c51c7-1401">Если определенное пользователем преобразование может привести к появлению исключения (например, так как исходный аргумент выходит за пределы диапазона) или потере данных (например, Отмена старшие разряды), то такое преобразование должен быть определен как явное преобразование.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1401">If a user-defined conversion can give rise to exceptions (for example, because the source argument is out of range) or loss of information (such as discarding high-order bits), then that conversion should be defined as an explicit conversion.</span></span>

<span data-ttu-id="c51c7-1402">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1402">In the example</span></span>
```csharp
using System;

public struct Digit
{
    byte value;

    public Digit(byte value) {
        if (value < 0 || value > 9) throw new ArgumentException();
        this.value = value;
    }

    public static implicit operator byte(Digit d) {
        return d.value;
    }

    public static explicit operator Digit(byte b) {
        return new Digit(b);
    }
}
```
<span data-ttu-id="c51c7-1403">преобразование из `Digit` для `byte` является неявным, так как она никогда не создает исключения или теряет информацию, но преобразование из `byte` для `Digit` является явным с момента `Digit` может представлять только подмножество возможных значения `byte`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1403">the conversion from `Digit` to `byte` is implicit because it never throws exceptions or loses information, but the conversion from `byte` to `Digit` is explicit since `Digit` can only represent a subset of the possible values of a `byte`.</span></span>

## <a name="instance-constructors"></a><span data-ttu-id="c51c7-1404">Конструкторы экземпляров</span><span class="sxs-lookup"><span data-stu-id="c51c7-1404">Instance constructors</span></span>

<span data-ttu-id="c51c7-1405">***Конструктор экземпляра*** является членом, который реализует действия для инициализации нового экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1405">An ***instance constructor*** is a member that implements the actions required to initialize an instance of a class.</span></span> <span data-ttu-id="c51c7-1406">Конструкторы экземпляров объявляются с помощью *constructor_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1406">Instance constructors are declared using *constructor_declaration*s:</span></span>

```antlr
constructor_declaration
    : attributes? constructor_modifier* constructor_declarator constructor_body
    ;

constructor_modifier
    : 'public'
    | 'protected'
    | 'internal'
    | 'private'
    | 'extern'
    | constructor_modifier_unsafe
    ;

constructor_declarator
    : identifier '(' formal_parameter_list? ')' constructor_initializer?
    ;

constructor_initializer
    : ':' 'base' '(' argument_list? ')'
    | ':' 'this' '(' argument_list? ')'
    ;

constructor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="c51c7-1407">Объект *constructor_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)), является допустимым сочетанием четырех модификаторов доступа ([модификаторы доступа ](classes.md#access-modifiers)) и `extern` ([внешние методы](classes.md#external-methods)) модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1407">A *constructor_declaration* may include a set of *attributes* ([Attributes](attributes.md)), a valid combination of the four access modifiers ([Access modifiers](classes.md#access-modifiers)), and an `extern` ([External methods](classes.md#external-methods)) modifier.</span></span> <span data-ttu-id="c51c7-1408">Объявление конструктора запрещено включать один и тот же модификатор несколько раз.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1408">A constructor declaration is not permitted to include the same modifier multiple times.</span></span>

<span data-ttu-id="c51c7-1409">*Идентификатор* из *constructor_declarator* должен указывать имя класса, в котором объявлен конструктор экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1409">The *identifier* of a *constructor_declarator* must name the class in which the instance constructor is declared.</span></span> <span data-ttu-id="c51c7-1410">Если указано любое другое имя, происходит ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1410">If any other name is specified, a compile-time error occurs.</span></span>

<span data-ttu-id="c51c7-1411">Необязательный *formal_parameter_list* экземпляра конструктор подчиняется тем же правилам, что *formal_parameter_list* метода ([методы](classes.md#methods)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1411">The optional *formal_parameter_list* of an instance constructor is subject to the same rules as the *formal_parameter_list* of a method ([Methods](classes.md#methods)).</span></span> <span data-ttu-id="c51c7-1412">Список формальных параметров определяет подпись ([сигнатуры и перегрузка](basic-concepts.md#signatures-and-overloading)) конструктора экземпляра и управляет процессом, при котором разрешение перегрузки ([вывод типа](expressions.md#type-inference)) выбирает определенный конструктор экземпляра в вызове.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1412">The formal parameter list defines the signature ([Signatures and overloading](basic-concepts.md#signatures-and-overloading)) of an instance constructor and governs the process whereby overload resolution ([Type inference](expressions.md#type-inference)) selects a particular instance constructor in an invocation.</span></span>

<span data-ttu-id="c51c7-1413">Каждый из типов, на которые ссылается *formal_parameter_list* экземпляра конструктор не должен иметь по крайней мере такой же уровень доступности, как и сам конструктор ([ограничения доступности](basic-concepts.md#accessibility-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1413">Each of the types referenced in the *formal_parameter_list* of an instance constructor must be at least as accessible as the constructor itself ([Accessibility constraints](basic-concepts.md#accessibility-constraints)).</span></span>

<span data-ttu-id="c51c7-1414">Необязательный *constructor_initializer* указывает другой конструктор экземпляров для вызова перед выполнением инструкции, приведенные в *constructor_body* этого конструктора экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1414">The optional *constructor_initializer* specifies another instance constructor to invoke before executing the statements given in the *constructor_body* of this instance constructor.</span></span> <span data-ttu-id="c51c7-1415">Это описано далее в [инициализаторы конструктора](classes.md#constructor-initializers).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1415">This is described further in [Constructor initializers](classes.md#constructor-initializers).</span></span>

<span data-ttu-id="c51c7-1416">Если объявление конструктора содержит `extern` модификатор, конструктор считается ***внешнего конструктора***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1416">When a constructor declaration includes an `extern` modifier, the constructor is said to be an ***external constructor***.</span></span> <span data-ttu-id="c51c7-1417">Поскольку объявление внешнего конструктора не предоставляет фактической реализации, его *constructor_body* состоит из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1417">Because an external constructor declaration provides no actual implementation, its *constructor_body* consists of a semicolon.</span></span> <span data-ttu-id="c51c7-1418">Для других конструкторов *constructor_body* состоит из *блок* которого указывает операторы для инициализации нового экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1418">For all other constructors, the *constructor_body* consists of a *block* which specifies the statements to initialize a new instance of the class.</span></span> <span data-ttu-id="c51c7-1419">Это в точности соответствует *блок* экземпляр метода с `void` тип возвращаемого значения ([тело метода](classes.md#method-body)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1419">This corresponds exactly to the *block* of an instance method with a `void` return type ([Method body](classes.md#method-body)).</span></span>

<span data-ttu-id="c51c7-1420">Конструкторы экземпляров не наследуются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1420">Instance constructors are not inherited.</span></span> <span data-ttu-id="c51c7-1421">Таким образом класс не имеет конструкторов экземпляров не фактически объявленных в классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1421">Thus, a class has no instance constructors other than those actually declared in the class.</span></span> <span data-ttu-id="c51c7-1422">Если класс содержит объявления конструкторов не экземпляра, автоматически предоставляется конструктор экземпляра по умолчанию ([конструкторы по умолчанию](classes.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1422">If a class contains no instance constructor declarations, a default instance constructor is automatically provided ([Default constructors](classes.md#default-constructors)).</span></span>

<span data-ttu-id="c51c7-1423">Конструкторы экземпляров вызываются *object_creation_expression*s ([выражения создания объектов](expressions.md#object-creation-expressions)) и проходят через *constructor_initializer*s.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1423">Instance constructors are invoked by *object_creation_expression*s ([Object creation expressions](expressions.md#object-creation-expressions)) and through *constructor_initializer*s.</span></span>

### <a name="constructor-initializers"></a><span data-ttu-id="c51c7-1424">Инициализаторы конструктора</span><span class="sxs-lookup"><span data-stu-id="c51c7-1424">Constructor initializers</span></span>

<span data-ttu-id="c51c7-1425">Все конструкторы экземпляров (за исключением тех, для класса `object`) непосредственно перед неявно включать вызов другого конструктора экземпляра *constructor_body*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1425">All instance constructors (except those for class `object`) implicitly include an invocation of another instance constructor immediately before the *constructor_body*.</span></span> <span data-ttu-id="c51c7-1426">Конструктор для вызова неявно определяется *constructor_initializer*:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1426">The constructor to implicitly invoke is determined by the *constructor_initializer*:</span></span>

*  <span data-ttu-id="c51c7-1427">Инициализатор конструктора экземпляра формы `base(argument_list)` или `base()` вызывает конструктор экземпляров от прямого базового класса для вызова.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1427">An instance constructor initializer of the form `base(argument_list)` or `base()` causes an instance constructor from the direct base class to be invoked.</span></span> <span data-ttu-id="c51c7-1428">Этот конструктор выбирается с помощью *argument_list* Если присутствует и правил разрешения перегрузки [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1428">That constructor is selected using *argument_list* if present and the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="c51c7-1429">Набор кандидатов конструкторов экземпляров содержит все доступные конструкторы экземпляров содержится в прямой базовый класс, или конструктор по умолчанию ([конструкторы по умолчанию](classes.md#default-constructors)), если конструкторы экземпляров не объявляются в прямой базовый класс.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1429">The set of candidate instance constructors consists of all accessible instance constructors contained in the direct base class, or the default constructor ([Default constructors](classes.md#default-constructors)), if no instance constructors are declared in the direct base class.</span></span> <span data-ttu-id="c51c7-1430">Если этот набор пуст или не может быть определен один лучший конструктор экземпляра, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1430">If this set is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs.</span></span>
*  <span data-ttu-id="c51c7-1431">Инициализатор конструктора экземпляра формы `this(argument-list)` или `this()` вызывает конструктор экземпляра непосредственно для вызова в классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1431">An instance constructor initializer of the form `this(argument-list)` or `this()` causes an instance constructor from the class itself to be invoked.</span></span> <span data-ttu-id="c51c7-1432">Конструктор выбирается с помощью *argument_list* Если присутствует и правил разрешения перегрузки [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1432">The constructor is selected using *argument_list* if present and the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="c51c7-1433">Набор кандидатов конструкторов экземпляров состоит из всех доступный экземпляр конструкторов, объявленных в самом классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1433">The set of candidate instance constructors consists of all accessible instance constructors declared in the class itself.</span></span> <span data-ttu-id="c51c7-1434">Если этот набор пуст или не может быть определен один лучший конструктор экземпляра, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1434">If this set is empty, or if a single best instance constructor cannot be identified, a compile-time error occurs.</span></span> <span data-ttu-id="c51c7-1435">Если объявление конструктора экземпляра включает инициализатор конструктора, который вызывает сам конструктор, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1435">If an instance constructor declaration includes a constructor initializer that invokes the constructor itself, a compile-time error occurs.</span></span>

<span data-ttu-id="c51c7-1436">Если у конструктора экземпляра нет инициализатора конструктора, инициализатор конструктора формы `base()` неявно предоставляется.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1436">If an instance constructor has no constructor initializer, a constructor initializer of the form `base()` is implicitly provided.</span></span> <span data-ttu-id="c51c7-1437">Таким образом объявление конструктора экземпляра формы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1437">Thus, an instance constructor declaration of the form</span></span>
```csharp
C(...) {...}
```
<span data-ttu-id="c51c7-1438">полностью эквивалентен</span><span class="sxs-lookup"><span data-stu-id="c51c7-1438">is exactly equivalent to</span></span>
```csharp
C(...): base() {...}
```

<span data-ttu-id="c51c7-1439">Область параметров, заданных *formal_parameter_list* конструктора экземпляра объявление включает в себя инициализатор конструктора этого объявления.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1439">The scope of the parameters given by the *formal_parameter_list* of an instance constructor declaration includes the constructor initializer of that declaration.</span></span> <span data-ttu-id="c51c7-1440">Таким образом инициализатор конструктора разрешен доступ к параметрам вызываемого конструктора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1440">Thus, a constructor initializer is permitted to access the parameters of the constructor.</span></span> <span data-ttu-id="c51c7-1441">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1441">For example:</span></span>
```csharp
class A
{
    public A(int x, int y) {}
}

class B: A
{
    public B(int x, int y): base(x + y, x - y) {}
}
```

<span data-ttu-id="c51c7-1442">Инициализатор конструктора экземпляров не может получить доступ к создаваемому экземпляру.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1442">An instance constructor initializer cannot access the instance being created.</span></span> <span data-ttu-id="c51c7-1443">Таким образом, является ошибкой во время компиляции для ссылки на `this` в выражении аргумента инициализатора конструктора, как это ошибка времени компиляции для при вычислении выражения аргумента для ссылки на любой другой член экземпляра через *simple_name*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1443">Therefore it is a compile-time error to reference `this` in an argument expression of the constructor initializer, as is it a compile-time error for an argument expression to reference any instance member through a *simple_name*.</span></span>

### <a name="instance-variable-initializers"></a><span data-ttu-id="c51c7-1444">Инициализаторы переменных экземпляров</span><span class="sxs-lookup"><span data-stu-id="c51c7-1444">Instance variable initializers</span></span>

<span data-ttu-id="c51c7-1445">Когда у конструктора экземпляра нет инициализатора конструктора или содержит инициализатор конструктора формы `base(...)`, этот конструктор неявно выполняет операции инициализации, заданные по *variable_initializer*процесса поля экземпляра, объявленные в классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1445">When an instance constructor has no constructor initializer, or it has a constructor initializer of the form `base(...)`, that constructor implicitly performs the initializations specified by the *variable_initializer*s of the instance fields declared in its class.</span></span> <span data-ttu-id="c51c7-1446">Это соответствует последовательности назначений, которые выполняются сразу же после входа в конструктор и перед неявным вызовом конструктора прямого базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1446">This corresponds to a sequence of assignments that are executed immediately upon entry to the constructor and before the implicit invocation of the direct base class constructor.</span></span> <span data-ttu-id="c51c7-1447">Инициализаторы переменных выполняются в порядке, в котором они появляются в объявлении класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1447">The variable initializers are executed in the textual order in which they appear in the class declaration.</span></span>

### <a name="constructor-execution"></a><span data-ttu-id="c51c7-1448">Выполнение конструктора</span><span class="sxs-lookup"><span data-stu-id="c51c7-1448">Constructor execution</span></span>

<span data-ttu-id="c51c7-1449">Инициализаторы переменных преобразуются в операторы присваивания, и эти операторы присваивания выполняются перед вызовом конструктора базового класса экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1449">Variable initializers are transformed into assignment statements, and these assignment statements are executed before the invocation of the base class instance constructor.</span></span> <span data-ttu-id="c51c7-1450">Такой порядок гарантирует, что все поля экземпляра инициализируются их инициализаторами переменных до выполнения любых операторов, которые имеют доступ к этому экземпляру.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1450">This ordering ensures that all instance fields are initialized by their variable initializers before any statements that have access to that instance are executed.</span></span>

<span data-ttu-id="c51c7-1451">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-1451">Given the example</span></span>
```csharp
using System;

class A
{
    public A() {
        PrintFields();
    }

    public virtual void PrintFields() {}
}

class B: A
{
    int x = 1;
    int y;

    public B() {
        y = -1;
    }

    public override void PrintFields() {
        Console.WriteLine("x = {0}, y = {1}", x, y);
    }
}
```
<span data-ttu-id="c51c7-1452">Когда `new B()` используется для создания экземпляра `B`, получается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1452">when `new B()` is used to create an instance of `B`, the following output is produced:</span></span>
```
x = 1, y = 0
```

<span data-ttu-id="c51c7-1453">Значение `x` -1, поскольку инициализатор переменной выполняется до вызова конструктора базового класса экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1453">The value of `x` is 1 because the variable initializer is executed before the base class instance constructor is invoked.</span></span> <span data-ttu-id="c51c7-1454">Тем не менее значение `y` равно 0 (значение по умолчанию `int`) так как назначение `y` не выполняется до после возвращения в конструктор базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1454">However, the value of `y` is 0 (the default value of an `int`) because the assignment to `y` is not executed until after the base class constructor returns.</span></span>

<span data-ttu-id="c51c7-1455">Это можно представить инициализаторы переменных экземпляров и инициализаторы конструктора как операторы, которые автоматически вставляются перед *constructor_body*.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1455">It is useful to think of instance variable initializers and constructor initializers as statements that are automatically inserted before the *constructor_body*.</span></span> <span data-ttu-id="c51c7-1456">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-1456">The example</span></span>
```csharp
using System;
using System.Collections;

class A
{
    int x = 1, y = -1, count;

    public A() {
        count = 0;
    }

    public A(int n) {
        count = n;
    }
}

class B: A
{
    double sqrt2 = Math.Sqrt(2.0);
    ArrayList items = new ArrayList(100);
    int max;

    public B(): this(100) {
        items.Add("default");
    }

    public B(int n): base(n - 1) {
        max = n;
    }
}
```
<span data-ttu-id="c51c7-1457">содержит несколько инициализаторов переменных; Он также содержит инициализаторы конструктора в обеих формах (`base` и `this`).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1457">contains several variable initializers; it also contains constructor initializers of both forms (`base` and `this`).</span></span> <span data-ttu-id="c51c7-1458">Этот пример соответствует код, показанный ниже, где каждый комментарий указывает автоматически вставленный оператор (синтаксис, используемый для вызовов автоматически вставленный конструктора является недопустимым, но служит только для иллюстрации механизма).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1458">The example corresponds to the code shown below, where each comment indicates an automatically inserted statement (the syntax used for the automatically inserted constructor invocations isn't valid, but merely serves to illustrate the mechanism).</span></span>

```csharp
using System.Collections;

class A
{
    int x, y, count;

    public A() {
        x = 1;                       // Variable initializer
        y = -1;                      // Variable initializer
        object();                    // Invoke object() constructor
        count = 0;
    }

    public A(int n) {
        x = 1;                       // Variable initializer
        y = -1;                      // Variable initializer
        object();                    // Invoke object() constructor
        count = n;
    }
}

class B: A
{
    double sqrt2;
    ArrayList items;
    int max;

    public B(): this(100) {
        B(100);                      // Invoke B(int) constructor
        items.Add("default");
    }

    public B(int n): base(n - 1) {
        sqrt2 = Math.Sqrt(2.0);      // Variable initializer
        items = new ArrayList(100);  // Variable initializer
        A(n - 1);                    // Invoke A(int) constructor
        max = n;
    }
}
```

### <a name="default-constructors"></a><span data-ttu-id="c51c7-1459">Конструкторы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="c51c7-1459">Default constructors</span></span>

<span data-ttu-id="c51c7-1460">Если класс содержит объявления конструкторов не экземпляра, автоматически предоставляется конструктор экземпляра по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1460">If a class contains no instance constructor declarations, a default instance constructor is automatically provided.</span></span> <span data-ttu-id="c51c7-1461">Конструктор по умолчанию просто вызывает конструктор без параметров прямого базового класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1461">That default constructor simply invokes the parameterless constructor of the direct base class.</span></span> <span data-ttu-id="c51c7-1462">Если этот класс является абстрактным, защищена объявленный уровень доступности для конструктора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1462">If the class is abstract then the declared accessibility for the default constructor is protected.</span></span> <span data-ttu-id="c51c7-1463">В противном случае объявленный уровень доступности для конструктора по умолчанию является открытым.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1463">Otherwise, the declared accessibility for the default constructor is public.</span></span> <span data-ttu-id="c51c7-1464">Таким образом конструктор по умолчанию всегда указывается в формате</span><span class="sxs-lookup"><span data-stu-id="c51c7-1464">Thus, the default constructor is always of the form</span></span>

```csharp
protected C(): base() {}
```
<span data-ttu-id="c51c7-1465">или</span><span class="sxs-lookup"><span data-stu-id="c51c7-1465">or</span></span>
```csharp
public C(): base() {}
```
<span data-ttu-id="c51c7-1466">где `C` — это имя класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1466">where `C` is the name of the class.</span></span> <span data-ttu-id="c51c7-1467">Если разрешение перегрузки не удалось определить уникальный лучшим кандидатом для инициализатора конструктора базового класса возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1467">If overload resolution is unable to determine a unique best candidate for the base class constructor initializer then a compile-time error occurs.</span></span>

<span data-ttu-id="c51c7-1468">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1468">In the example</span></span>
```csharp
class Message
{
    object sender;
    string text;
}
```
<span data-ttu-id="c51c7-1469">конструктор по умолчанию предоставляется в том случае, поскольку класс не содержит экземпляр объявления конструкторов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1469">a default constructor is provided because the class contains no instance constructor declarations.</span></span> <span data-ttu-id="c51c7-1470">Таким образом пример является точным эквивалентом</span><span class="sxs-lookup"><span data-stu-id="c51c7-1470">Thus, the example is precisely equivalent to</span></span>
```csharp
class Message
{
    object sender;
    string text;

    public Message(): base() {}
}
```

### <a name="private-constructors"></a><span data-ttu-id="c51c7-1471">Закрытые конструкторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1471">Private constructors</span></span>

<span data-ttu-id="c51c7-1472">Если в классе `T` объявляет только закрытые конструкторы экземпляров, невозможно для классов за пределами текста программы `T` для наследования от `T` или напрямую создавать экземпляры `T`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1472">When a class `T` declares only private instance constructors, it is not possible for classes outside the program text of `T` to derive from `T` or to directly create instances of `T`.</span></span> <span data-ttu-id="c51c7-1473">Таким образом Если класс содержит только статические члены и не предназначен для создания экземпляра, Добавление пустой закрытый конструктор экземпляров предотвратит создание экземпляров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1473">Thus, if a class contains only static members and isn't intended to be instantiated, adding an empty private instance constructor will prevent instantiation.</span></span> <span data-ttu-id="c51c7-1474">Пример:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1474">For example:</span></span>
```csharp
public class Trig
{
    private Trig() {}        // Prevent instantiation

    public const double PI = 3.14159265358979323846;

    public static double Sin(double x) {...}
    public static double Cos(double x) {...}
    public static double Tan(double x) {...}
}
```

<span data-ttu-id="c51c7-1475">`Trig` Класс группирует связанные методы и константы, но не предназначен для создания экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1475">The `Trig` class groups related methods and constants, but is not intended to be instantiated.</span></span> <span data-ttu-id="c51c7-1476">Поэтому он объявляет единственных пустой частный конструктор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1476">Therefore it declares a single empty private instance constructor.</span></span> <span data-ttu-id="c51c7-1477">Хотя бы один экземпляр конструктор должен быть объявлен таким образом, чтобы отключить автоматическое создание конструктора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1477">At least one instance constructor must be declared to suppress the automatic generation of a default constructor.</span></span>

### <a name="optional-instance-constructor-parameters"></a><span data-ttu-id="c51c7-1478">Необязательные параметры конструктора экземпляров</span><span class="sxs-lookup"><span data-stu-id="c51c7-1478">Optional instance constructor parameters</span></span>

<span data-ttu-id="c51c7-1479">`this(...)` Инициализатора конструктора обычно используется в сочетании с перегрузкой для реализации необязательных параметров конструктора экземпляров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1479">The `this(...)` form of constructor initializer is commonly used in conjunction with overloading to implement optional instance constructor parameters.</span></span> <span data-ttu-id="c51c7-1480">В примере</span><span class="sxs-lookup"><span data-stu-id="c51c7-1480">In the example</span></span>
```csharp
class Text
{
    public Text(): this(0, 0, null) {}

    public Text(int x, int y): this(x, y, null) {}

    public Text(int x, int y, string s) {
        // Actual constructor implementation
    }
}
```
<span data-ttu-id="c51c7-1481">Первый конструкторы два экземпляра просто предоставить значения по умолчанию для отсутствующие аргументы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1481">the first two instance constructors merely provide the default values for the missing arguments.</span></span> <span data-ttu-id="c51c7-1482">Используют `this(...)` инициализатора конструктора для вызова Третий конструктор экземпляра, который фактически выполняет работу по инициализации нового экземпляра.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1482">Both use a `this(...)` constructor initializer to invoke the third instance constructor, which actually does the work of initializing the new instance.</span></span> <span data-ttu-id="c51c7-1483">Это действие соответствует необязательных параметров конструктора:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1483">The effect is that of optional constructor parameters:</span></span>
```csharp
Text t1 = new Text();                    // Same as Text(0, 0, null)
Text t2 = new Text(5, 10);               // Same as Text(5, 10, null)
Text t3 = new Text(5, 20, "Hello");
```

## <a name="static-constructors"></a><span data-ttu-id="c51c7-1484">Статические конструкторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1484">Static constructors</span></span>

<span data-ttu-id="c51c7-1485">Объект ***статический конструктор*** является членом, который реализует действия, необходимые для инициализации закрытого типа класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1485">A ***static constructor*** is a member that implements the actions required to initialize a closed class type.</span></span> <span data-ttu-id="c51c7-1486">Статические конструкторы объявляются с помощью *static_constructor_declaration*s:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1486">Static constructors are declared using *static_constructor_declaration*s:</span></span>

```antlr
static_constructor_declaration
    : attributes? static_constructor_modifiers identifier '(' ')' static_constructor_body
    ;

static_constructor_modifiers
    : 'extern'? 'static'
    | 'static' 'extern'?
    | static_constructor_modifiers_unsafe
    ;

static_constructor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="c51c7-1487">Объект *static_constructor_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)) и `extern` модификатор ([внешние методы](classes.md#external-methods)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1487">A *static_constructor_declaration* may include a set of *attributes* ([Attributes](attributes.md)) and an `extern` modifier ([External methods](classes.md#external-methods)).</span></span>

<span data-ttu-id="c51c7-1488">*Идентификатор* из *static_constructor_declaration* должен указывать имя класса, в котором объявлен статический конструктор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1488">The *identifier* of a *static_constructor_declaration* must name the class in which the static constructor is declared.</span></span> <span data-ttu-id="c51c7-1489">Если указано любое другое имя, происходит ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1489">If any other name is specified, a compile-time error occurs.</span></span>

<span data-ttu-id="c51c7-1490">Если объявление статического конструктора содержит `extern` модификатор, статический конструктор называется ***внешних статический конструктор***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1490">When a static constructor declaration includes an `extern` modifier, the static constructor is said to be an ***external static constructor***.</span></span> <span data-ttu-id="c51c7-1491">Поскольку объявление внешнего статического конструктора не предоставляет фактической реализации, его *static_constructor_body* состоит из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1491">Because an external static constructor declaration provides no actual implementation, its *static_constructor_body* consists of a semicolon.</span></span> <span data-ttu-id="c51c7-1492">Для всех объявлений статический конструктор *static_constructor_body* состоит из *блок* которого указывает операторы для инициализации класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1492">For all other static constructor declarations, the *static_constructor_body* consists of a *block* which specifies the statements to execute in order to initialize the class.</span></span> <span data-ttu-id="c51c7-1493">Это в точности соответствует *method_body* статического метода с `void` тип возвращаемого значения ([тело метода](classes.md#method-body)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1493">This corresponds exactly to the *method_body* of a static method with a `void` return type ([Method body](classes.md#method-body)).</span></span>

<span data-ttu-id="c51c7-1494">Статические конструкторы не наследуются и не может вызываться напрямую.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1494">Static constructors are not inherited, and cannot be called directly.</span></span>

<span data-ttu-id="c51c7-1495">Статический конструктор для закрытого типа класса выполняет не более одного раза в домене данного приложения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1495">The static constructor for a closed class type executes at most once in a given application domain.</span></span> <span data-ttu-id="c51c7-1496">Выполнение статического конструктора запускается первым из следующих событий в домене приложения:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1496">The execution of a static constructor is triggered by the first of the following events to occur within an application domain:</span></span>

*  <span data-ttu-id="c51c7-1497">Создать экземпляр типа класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1497">An instance of the class type is created.</span></span>
*  <span data-ttu-id="c51c7-1498">Статические члены типа класса ссылки.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1498">Any of the static members of the class type are referenced.</span></span>

<span data-ttu-id="c51c7-1499">Если класс содержит `Main` метод ([запуск приложения](basic-concepts.md#application-startup)), в котором начинается исполнение, статический конструктор для этого класса выполняется перед `Main` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1499">If a class contains the `Main` method ([Application Startup](basic-concepts.md#application-startup)) in which execution begins, the static constructor for that class executes before the `Main` method is called.</span></span>

<span data-ttu-id="c51c7-1500">Для инициализации нового закрытого типа класса, сначала новый набор статических полей ([экземпляра и статические поля](classes.md#static-and-instance-fields)) для создания этого закрытого типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1500">To initialize a new closed class type, first a new set of static fields ([Static and instance fields](classes.md#static-and-instance-fields)) for that particular closed type is created.</span></span> <span data-ttu-id="c51c7-1501">Все статические поля устанавливается равным значению по умолчанию ([значения по умолчанию](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1501">Each of the static fields is initialized to its default value ([Default values](variables.md#default-values)).</span></span> <span data-ttu-id="c51c7-1502">Далее, инициализаторы статических полей ([инициализации статического поля](classes.md#static-field-initialization)) выполняются этих статических полей.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1502">Next, the static field initializers ([Static field initialization](classes.md#static-field-initialization)) are executed for those static fields.</span></span> <span data-ttu-id="c51c7-1503">Наконец выполняется статический конструктор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1503">Finally, the static constructor is executed.</span></span>

<span data-ttu-id="c51c7-1504">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-1504">The example</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        A.F();
        B.F();
    }
}

class A
{
    static A() {
        Console.WriteLine("Init A");
    }
    public static void F() {
        Console.WriteLine("A.F");
    }
}

class B
{
    static B() {
        Console.WriteLine("Init B");
    }
    public static void F() {
        Console.WriteLine("B.F");
    }
}
```
<span data-ttu-id="c51c7-1505">должен создавать выходные данные:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1505">must produce the output:</span></span>
```
Init A
A.F
Init B
B.F
```
<span data-ttu-id="c51c7-1506">так как выполнение `A`в статический конструктор инициируется вызов `A.F`и выполнение `B`в статический конструктор инициируется вызов `B.F`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1506">because the execution of `A`'s static constructor is triggered by the call to `A.F`, and the execution of `B`'s static constructor is triggered by the call to `B.F`.</span></span>

<span data-ttu-id="c51c7-1507">Имеется возможность создать циклические зависимости, позволяющие статические поля с инициализаторами переменных в их состоянии значения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1507">It is possible to construct circular dependencies that allow static fields with variable initializers to be observed in their default value state.</span></span>

<span data-ttu-id="c51c7-1508">Пример</span><span class="sxs-lookup"><span data-stu-id="c51c7-1508">The example</span></span>
```csharp
using System;

class A
{
    public static int X;

    static A() {
        X = B.Y + 1;
    }
}

class B
{
    public static int Y = A.X + 1;

    static B() {}

    static void Main() {
        Console.WriteLine("X = {0}, Y = {1}", A.X, B.Y);
    }
}
```
<span data-ttu-id="c51c7-1509">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="c51c7-1509">produces the output</span></span>
```
X = 1, Y = 2
```

<span data-ttu-id="c51c7-1510">Для выполнения `Main` метода, система сначала выполняет инициализатор для `B.Y`до того, как класс `B`в статическом конструкторе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1510">To execute the `Main` method, the system first runs the initializer for `B.Y`, prior to class `B`'s static constructor.</span></span> <span data-ttu-id="c51c7-1511">`Y`в инициализатор вызывает `A`в статический конструктор для запуска, так как значение `A.X` на который приведена ссылка.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1511">`Y`'s initializer causes `A`'s static constructor to be run because the value of `A.X` is referenced.</span></span> <span data-ttu-id="c51c7-1512">Статический конструктор `A` в свою очередь продолжает вычислять значение `X`и извлекает при этом значение по умолчанию `Y`, которое равно нулю.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1512">The static constructor of `A` in turn proceeds to compute the value of `X`, and in doing so fetches the default value of `Y`, which is zero.</span></span> <span data-ttu-id="c51c7-1513">`A.X` При этом инициализируется значением 1.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1513">`A.X` is thus initialized to 1.</span></span> <span data-ttu-id="c51c7-1514">Процесс выполнения `A`Инициализаторы статических полей и статического конструктора, а затем завершается, возвращая к вычислению начальное значение `Y`, результат которого становится 2.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1514">The process of running `A`'s static field initializers and static constructor then completes, returning to the calculation of the initial value of `Y`, the result of which becomes 2.</span></span>

<span data-ttu-id="c51c7-1515">Так как статический конструктор выполняется только один раз для каждого закрыто сформированного типа класса, это удобно для принудительного применения проверки времени выполнения, которые не удается проверить во время компиляции с помощью ограничения параметра типа ([параметр типа ограничения](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1515">Because the static constructor is executed exactly once for each closed constructed class type, it is a convenient place to enforce run-time checks on the type parameter that cannot be checked at compile-time via constraints ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="c51c7-1516">Например следующий тип использует статический конструктор для принудительного применения, что аргумент типа является перечислением:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1516">For example, the following type uses a static constructor to enforce that the type argument is an enum:</span></span>
```csharp
class Gen<T> where T: struct
{
    static Gen() {
        if (!typeof(T).IsEnum) {
            throw new ArgumentException("T must be an enum");
        }
    }
}
```

## <a name="destructors"></a><span data-ttu-id="c51c7-1517">Деструкторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1517">Destructors</span></span>

<span data-ttu-id="c51c7-1518">Объект ***деструктор*** является членом, который реализует действия для уничтожения экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1518">A ***destructor*** is a member that implements the actions required to destruct an instance of a class.</span></span> <span data-ttu-id="c51c7-1519">Деструктор был объявлен с помощью *destructor_declaration*:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1519">A destructor is declared using a *destructor_declaration*:</span></span>

```antlr
destructor_declaration
    : attributes? 'extern'? '~' identifier '(' ')' destructor_body
    | destructor_declaration_unsafe
    ;

destructor_body
    : block
    | ';'
    ;
```

<span data-ttu-id="c51c7-1520">Объект *destructor_declaration* может включать набор *атрибуты* ([атрибуты](attributes.md)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1520">A *destructor_declaration* may include a set of *attributes* ([Attributes](attributes.md)).</span></span>

<span data-ttu-id="c51c7-1521">*Идентификатор* из *destructor_declaration* должен указывать имя класса, в котором объявлен деструктор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1521">The *identifier* of a *destructor_declaration* must name the class in which the destructor is declared.</span></span> <span data-ttu-id="c51c7-1522">Если указано любое другое имя, происходит ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1522">If any other name is specified, a compile-time error occurs.</span></span>

<span data-ttu-id="c51c7-1523">Если объявление деструктора содержит `extern` модификатор, деструктор считается ***внешних деструктор***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1523">When a destructor declaration includes an `extern` modifier, the destructor is said to be an ***external destructor***.</span></span> <span data-ttu-id="c51c7-1524">Поскольку объявление внешнего деструктора не предоставляет фактической реализации, его *destructor_body* состоит из точки с запятой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1524">Because an external destructor declaration provides no actual implementation, its *destructor_body* consists of a semicolon.</span></span> <span data-ttu-id="c51c7-1525">Для всех других деструкторах *destructor_body* состоит из *блок* определяющий операторы, выполняемые для уничтожения экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1525">For all other destructors, the *destructor_body* consists of a *block* which specifies the statements to execute in order to destruct an instance of the class.</span></span> <span data-ttu-id="c51c7-1526">Объект *destructor_body* в точности соответствует *method_body* экземпляр метода с `void` тип возвращаемого значения ([тело метода](classes.md#method-body)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1526">A *destructor_body* corresponds exactly to the *method_body* of an instance method with a `void` return type ([Method body](classes.md#method-body)).</span></span>

<span data-ttu-id="c51c7-1527">Деструкторы не наследуются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1527">Destructors are not inherited.</span></span> <span data-ttu-id="c51c7-1528">Таким образом класс имеет никакие деструкторы, отличном от того, который может быть объявлен в этом классе.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1528">Thus, a class has no destructors other than the one which may be declared in that class.</span></span>

<span data-ttu-id="c51c7-1529">Так как деструктор должен не имеют параметров, не может быть перегружен, поэтому класс можно использовать максимум, один деструктор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1529">Since a destructor is required to have no parameters, it cannot be overloaded, so a class can have, at most, one destructor.</span></span>

<span data-ttu-id="c51c7-1530">Деструкторы вызываются автоматически и не может вызываться явным образом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1530">Destructors are invoked automatically, and cannot be invoked explicitly.</span></span> <span data-ttu-id="c51c7-1531">Экземпляр становится пригодным для уничтожения, когда он больше не любой код может использовать этот экземпляр.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1531">An instance becomes eligible for destruction when it is no longer possible for any code to use that instance.</span></span> <span data-ttu-id="c51c7-1532">Выполнение деструктора для экземпляра может произойти в любое время после он становится пригодным для уничтожения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1532">Execution of the destructor for the instance may occur at any time after the instance becomes eligible for destruction.</span></span> <span data-ttu-id="c51c7-1533">Если экземпляр уничтожается, вызываются деструкторы в цепочке наследования этого экземпляра, в порядке, от большинства производного к младшему.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1533">When an instance is destructed, the destructors in that instance's inheritance chain are called, in order, from most derived to least derived.</span></span> <span data-ttu-id="c51c7-1534">Деструктор может выполняться в любом потоке.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1534">A destructor may be executed on any thread.</span></span> <span data-ttu-id="c51c7-1535">Дальнейшее обсуждение правил, определяющих, когда и как выполняется деструктор, см. в разделе [автоматическое управление памятью](basic-concepts.md#automatic-memory-management).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1535">For further discussion of the rules that govern when and how a destructor is executed, see [Automatic memory management](basic-concepts.md#automatic-memory-management).</span></span>

<span data-ttu-id="c51c7-1536">Выходные данные примера</span><span class="sxs-lookup"><span data-stu-id="c51c7-1536">The output of the example</span></span>
```csharp
using System;

class A
{
    ~A() {
        Console.WriteLine("A's destructor");
    }
}

class B: A
{
    ~B() {
        Console.WriteLine("B's destructor");
    }
}

class Test
{
   static void Main() {
        B b = new B();
        b = null;
        GC.Collect();
        GC.WaitForPendingFinalizers();
   }
}
```
<span data-ttu-id="c51c7-1537">является</span><span class="sxs-lookup"><span data-stu-id="c51c7-1537">is</span></span>
```
B's destructor
A's destructor
```
<span data-ttu-id="c51c7-1538">Поскольку деструкторы в цепочке наследования вызываются в порядке, от большинства производного к младшему.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1538">since destructors in an inheritance chain are called in order, from most derived to least derived.</span></span>

<span data-ttu-id="c51c7-1539">Деструкторы реализуются путем переопределения виртуального метода `Finalize` на `System.Object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1539">Destructors are implemented by overriding the virtual method `Finalize` on `System.Object`.</span></span> <span data-ttu-id="c51c7-1540">Программы на C# не могут переопределять этот метод или вызывать его (или его переопределения) непосредственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1540">C# programs are not permitted to override this method or call it (or overrides of it) directly.</span></span> <span data-ttu-id="c51c7-1541">Например программа</span><span class="sxs-lookup"><span data-stu-id="c51c7-1541">For instance, the program</span></span>
```csharp
class A 
{
    override protected void Finalize() {}    // error

    public void F() {
        this.Finalize();                     // error
    }
}
```
<span data-ttu-id="c51c7-1542">содержит две ошибки.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1542">contains two errors.</span></span>

<span data-ttu-id="c51c7-1543">Компилятор действует так, будто этот метод и переопределений, вообще не существуют.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1543">The compiler behaves as if this method, and overrides of it, do not exist at all.</span></span> <span data-ttu-id="c51c7-1544">Таким образом эта программа:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1544">Thus, this program:</span></span>
```csharp
class A 
{
    void Finalize() {}                            // permitted
}
```
<span data-ttu-id="c51c7-1545">является допустимым, и метод показано скрытие `System.Object` `Finalize` метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1545">is valid, and the method shown hides `System.Object`'s `Finalize` method.</span></span>

<span data-ttu-id="c51c7-1546">Описание поведения при возникновении исключения из деструктора, см. в разделе [обработке исключений](exceptions.md#how-exceptions-are-handled).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1546">For a discussion of the behavior when an exception is thrown from a destructor, see [How exceptions are handled](exceptions.md#how-exceptions-are-handled).</span></span>

## <a name="iterators"></a><span data-ttu-id="c51c7-1547">Итераторы</span><span class="sxs-lookup"><span data-stu-id="c51c7-1547">Iterators</span></span>

<span data-ttu-id="c51c7-1548">Функция-член ([функции-члены](expressions.md#function-members)) реализованы с помощью блока итератора ([блоки](statements.md#blocks)) называется ***итератор***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1548">A function member ([Function members](expressions.md#function-members)) implemented using an iterator block ([Blocks](statements.md#blocks)) is called an ***iterator***.</span></span>

<span data-ttu-id="c51c7-1549">Блока итератора может использоваться в теле функции-члена, до тех пор, пока тип возвращаемого значения соответствующего члена функции является одним из интерфейсов перечислителя ([интерфейсы перечислителя](classes.md#enumerator-interfaces)) или один из IEnumerable-интерфейс ([Перечисляемые интерфейсы](classes.md#enumerable-interfaces)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1549">An iterator block may be used as the body of a function member as long as the return type of the corresponding function member is one of the enumerator interfaces ([Enumerator interfaces](classes.md#enumerator-interfaces)) or one of the enumerable interfaces ([Enumerable interfaces](classes.md#enumerable-interfaces)).</span></span> <span data-ttu-id="c51c7-1550">Он может использоваться как *method_body*, *operator_body* или *accessor_body*, тогда как события, конструкторы экземпляров, статические конструкторы и деструкторы не может быть реализованы как итераторы.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1550">It can occur as a *method_body*, *operator_body* or *accessor_body*, whereas events, instance constructors, static constructors and destructors cannot be implemented as iterators.</span></span>

<span data-ttu-id="c51c7-1551">Когда функция-член реализуется с помощью блока итератора, это ошибка времени компиляции для списка формальных параметров функции-члена, задающих `ref` или `out` параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1551">When a function member is implemented using an iterator block, it is a compile-time error for the formal parameter list of the function member to specify any `ref` or `out` parameters.</span></span>

### <a name="enumerator-interfaces"></a><span data-ttu-id="c51c7-1552">Интерфейсы перечислителя</span><span class="sxs-lookup"><span data-stu-id="c51c7-1552">Enumerator interfaces</span></span>

<span data-ttu-id="c51c7-1553">***Интерфейсы перечислителя*** являются неуниверсальный интерфейс `System.Collections.IEnumerator` и всех экземпляров универсального интерфейса `System.Collections.Generic.IEnumerator<T>`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1553">The ***enumerator interfaces*** are the non-generic interface `System.Collections.IEnumerator` and all instantiations of the generic interface `System.Collections.Generic.IEnumerator<T>`.</span></span> <span data-ttu-id="c51c7-1554">Для краткости в этой главе эти интерфейсы ссылаются как на `IEnumerator` и `IEnumerator<T>`, соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1554">For the sake of brevity, in this chapter these interfaces are referenced as `IEnumerator` and `IEnumerator<T>`, respectively.</span></span>

### <a name="enumerable-interfaces"></a><span data-ttu-id="c51c7-1555">IEnumerable-интерфейс</span><span class="sxs-lookup"><span data-stu-id="c51c7-1555">Enumerable interfaces</span></span>

<span data-ttu-id="c51c7-1556">***Перечисляемые интерфейсы*** являются неуниверсальный интерфейс `System.Collections.IEnumerable` и всех экземпляров универсального интерфейса `System.Collections.Generic.IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1556">The ***enumerable interfaces*** are the non-generic interface `System.Collections.IEnumerable` and all instantiations of the generic interface `System.Collections.Generic.IEnumerable<T>`.</span></span> <span data-ttu-id="c51c7-1557">Для краткости в этой главе эти интерфейсы ссылаются как на `IEnumerable` и `IEnumerable<T>`, соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1557">For the sake of brevity, in this chapter these interfaces are referenced as `IEnumerable` and `IEnumerable<T>`, respectively.</span></span>

### <a name="yield-type"></a><span data-ttu-id="c51c7-1558">Тип результата</span><span class="sxs-lookup"><span data-stu-id="c51c7-1558">Yield type</span></span>

<span data-ttu-id="c51c7-1559">Итератор, который создает последовательность значений одного типа.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1559">An iterator produces a sequence of values, all of the same type.</span></span> <span data-ttu-id="c51c7-1560">Этот тип называется ***yield тип*** итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1560">This type is called the ***yield type*** of the iterator.</span></span>

*  <span data-ttu-id="c51c7-1561">Тип итератора, который возвращает yield `IEnumerator` или `IEnumerable` является `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1561">The yield type of an iterator that returns `IEnumerator` or `IEnumerable` is `object`.</span></span>
*  <span data-ttu-id="c51c7-1562">Тип итератора, который возвращает yield `IEnumerator<T>` или `IEnumerable<T>` является `T`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1562">The yield type of an iterator that returns `IEnumerator<T>` or `IEnumerable<T>` is `T`.</span></span>

### <a name="enumerator-objects"></a><span data-ttu-id="c51c7-1563">Объекты перечислителя</span><span class="sxs-lookup"><span data-stu-id="c51c7-1563">Enumerator objects</span></span>

<span data-ttu-id="c51c7-1564">Когда функция-член, возвращающую перечислитель тип интерфейса реализуется с помощью блока итератора, вызова функции-члена не выполняется код в блоке итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1564">When a function member returning an enumerator interface type is implemented using an iterator block, invoking the function member does not immediately execute the code in the iterator block.</span></span> <span data-ttu-id="c51c7-1565">Вместо этого ***объекта-перечислителя*** создается и возвращается.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1565">Instead, an ***enumerator object*** is created and returned.</span></span> <span data-ttu-id="c51c7-1566">Этот объект инкапсулирует код, указанный в блоке итератора, а выполнение кода в блоке итератора происходит при объекта-перечислителя `MoveNext` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1566">This object encapsulates the code specified in the iterator block, and execution of the code in the iterator block occurs when the enumerator object's `MoveNext` method is invoked.</span></span> <span data-ttu-id="c51c7-1567">Объект перечислителя имеет следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1567">An enumerator object has the following characteristics:</span></span>

*  <span data-ttu-id="c51c7-1568">Он реализует `IEnumerator` и `IEnumerator<T>`, где `T` yield тип итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1568">It implements `IEnumerator` and `IEnumerator<T>`, where `T` is the yield type of the iterator.</span></span>
*  <span data-ttu-id="c51c7-1569">Он реализует `System.IDisposable`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1569">It implements `System.IDisposable`.</span></span>
*  <span data-ttu-id="c51c7-1570">Она инициализируется с копией значения аргументов (если таковые имеются) и экземпляр значение, передаваемое в функцию-член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1570">It is initialized with a copy of the argument values (if any) and instance value passed to the function member.</span></span>
*  <span data-ttu-id="c51c7-1571">Он имеет четыре потенциальных состояний, ***перед***, ***под управлением***, ***приостановлено***, и ***после***и изначально находится в ***перед***  состояние.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1571">It has four potential states, ***before***, ***running***, ***suspended***, and ***after***, and is initially in the ***before*** state.</span></span>

<span data-ttu-id="c51c7-1572">Объект перечислителя, обычно является экземпляром класса перечислителя, созданного компилятором, который инкапсулирует код в блоке итератора и реализует интерфейсы перечислителя, но возможны и другие методы реализации.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1572">An enumerator object is typically an instance of a compiler-generated enumerator class that encapsulates the code in the iterator block and implements the enumerator interfaces, but other methods of implementation are possible.</span></span> <span data-ttu-id="c51c7-1573">Если класс перечислителя, создается компилятором, этот класс будет вложен, прямо или косвенно, в класс, содержащий функцию-член, он будет иметь режим доступа private и он будет иметь имя зарезервировано для внутреннего использования компиляторами ([идентификаторы ](lexical-structure.md#identifiers)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1573">If an enumerator class is generated by the compiler, that class will be nested, directly or indirectly, in the class containing the function member, it will have private accessibility, and it will have a name reserved for compiler use ([Identifiers](lexical-structure.md#identifiers)).</span></span>

<span data-ttu-id="c51c7-1574">Объект перечислителя может реализовывать несколько интерфейсов, чем указано выше.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1574">An enumerator object may implement more interfaces than those specified above.</span></span>

<span data-ttu-id="c51c7-1575">В следующих разделах описываются точное поведение `MoveNext`, `Current`, и `Dispose` членами `IEnumerable` и `IEnumerable<T>` объект перечислителя, предоставляемые реализации интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1575">The following sections describe the exact behavior of the `MoveNext`, `Current`, and `Dispose` members of the `IEnumerable` and `IEnumerable<T>` interface implementations provided by an enumerator object.</span></span>

<span data-ttu-id="c51c7-1576">Обратите внимание, что объекты перечислителя не поддерживают `IEnumerator.Reset` метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1576">Note that enumerator objects do not support the `IEnumerator.Reset` method.</span></span> <span data-ttu-id="c51c7-1577">Вызов этого метода приводит к `System.NotSupportedException` исключение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1577">Invoking this method causes a `System.NotSupportedException` to be thrown.</span></span>

#### <a name="the-movenext-method"></a><span data-ttu-id="c51c7-1578">Метод MoveNext</span><span class="sxs-lookup"><span data-stu-id="c51c7-1578">The MoveNext method</span></span>

<span data-ttu-id="c51c7-1579">`MoveNext` Метод объекта перечислителя инкапсулирует код блока итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1579">The `MoveNext` method of an enumerator object encapsulates the code of an iterator block.</span></span> <span data-ttu-id="c51c7-1580">Вызов `MoveNext` метод выполняет код в блоке итератора и задает `Current` свойства объекта-перечислителя соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1580">Invoking the `MoveNext` method executes code in the iterator block and sets the `Current` property of the enumerator object as appropriate.</span></span> <span data-ttu-id="c51c7-1581">Точные действия `MoveNext` зависит от состояния объекта перечислителя при `MoveNext` вызывается:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1581">The precise action performed by `MoveNext` depends on the state of the enumerator object when `MoveNext` is invoked:</span></span>

*  <span data-ttu-id="c51c7-1582">Если состояние объекта перечислителя ***перед***, вызов `MoveNext`:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1582">If the state of the enumerator object is ***before***, invoking `MoveNext`:</span></span>
   * <span data-ttu-id="c51c7-1583">Задает состояние ***под управлением***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1583">Changes the state to ***running***.</span></span>
   * <span data-ttu-id="c51c7-1584">Инициализирует параметры (включая `this`) итератора блока для значения аргументов и значением экземпляра, сохраненными при инициализации объекта-перечислителя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1584">Initializes the parameters (including `this`) of the iterator block to the argument values and instance value saved when the enumerator object was initialized.</span></span>
   * <span data-ttu-id="c51c7-1585">Выполняет блок итератора с самого начала, пока выполнение прерывается (как описано ниже).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1585">Executes the iterator block from the beginning until execution is interrupted (as described below).</span></span>
*  <span data-ttu-id="c51c7-1586">Если состояние объекта перечислителя ***под управлением***, в результате вызова `MoveNext` не определен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1586">If the state of the enumerator object is ***running***, the result of invoking `MoveNext` is unspecified.</span></span>
*  <span data-ttu-id="c51c7-1587">Если состояние объекта перечислителя ***приостановлено***, вызов `MoveNext`:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1587">If the state of the enumerator object is ***suspended***, invoking `MoveNext`:</span></span>
   * <span data-ttu-id="c51c7-1588">Задает состояние ***под управлением***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1588">Changes the state to ***running***.</span></span>
   * <span data-ttu-id="c51c7-1589">Восстанавливает значения по для всех локальных переменных и параметров (включая this) к значениям, сохраненным при последней приостановки выполнения блока итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1589">Restores the values of all local variables and parameters (including this) to the values saved when execution of the iterator block was last suspended.</span></span> <span data-ttu-id="c51c7-1590">Обратите внимание, что содержимое любые объекты, на которые ссылается эти переменные могут были изменены с момента предыдущего вызова MoveNext.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1590">Note that the contents of any objects referenced by these variables may have changed since the previous call to MoveNext.</span></span>
   * <span data-ttu-id="c51c7-1591">Возобновляет выполнение блока итератора сразу после `yield return` оператор, который вызвал приостановку выполнения и продолжается, пока выполнение прерывается (как описано ниже).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1591">Resumes execution of the iterator block immediately following the `yield return` statement that caused the suspension of execution and continues until execution is interrupted (as described below).</span></span>
*  <span data-ttu-id="c51c7-1592">Если состояние объекта перечислителя ***после***, вызов `MoveNext` возвращает `false`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1592">If the state of the enumerator object is ***after***, invoking `MoveNext` returns `false`.</span></span>


<span data-ttu-id="c51c7-1593">При `MoveNext` выполняет блока итератора, выполнение может быть прервано четырьмя способами: С `yield return` инструкции, по `yield break` инструкции по концу блока итератора и это исключение исключение и распространяется из блока итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1593">When `MoveNext` executes the iterator block, execution can be interrupted in four ways: By a `yield return` statement, by a `yield break` statement, by encountering the end of the iterator block, and by an exception being thrown and propagated out of the iterator block.</span></span>

*  <span data-ttu-id="c51c7-1594">Когда `yield return` встречается ([оператор yield](statements.md#the-yield-statement)):</span><span class="sxs-lookup"><span data-stu-id="c51c7-1594">When a `yield return` statement is encountered ([The yield statement](statements.md#the-yield-statement)):</span></span>
   * <span data-ttu-id="c51c7-1595">Выражение, заданное в инструкции вычисляется, неявно преобразован в тип результата и назначенные `Current` свойство объекта перечислителя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1595">The expression given in the statement is evaluated, implicitly converted to the yield type, and assigned to the `Current` property of the enumerator object.</span></span>
   * <span data-ttu-id="c51c7-1596">Выполнение тела итератора приостанавливается.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1596">Execution of the iterator body is suspended.</span></span> <span data-ttu-id="c51c7-1597">Значения всех локальных переменных и параметров (включая `this`) сохраняются, как это расположение `yield return` инструкции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1597">The values of all local variables and parameters (including `this`) are saved, as is the location of this `yield return` statement.</span></span> <span data-ttu-id="c51c7-1598">Если `yield return` оператор находится внутри одного или нескольких `try` блокирует, сопоставленного `finally` блоки не выполняются в данный момент.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1598">If the `yield return` statement is within one or more `try` blocks, the associated `finally` blocks are not executed at this time.</span></span>
   * <span data-ttu-id="c51c7-1599">Изменения состояния объекта перечислителя на ***приостановлено***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1599">The state of the enumerator object is changed to ***suspended***.</span></span>
   * <span data-ttu-id="c51c7-1600">`MoveNext` Возвращает метод `true` для своего вызывающего объекта, указывающее, что итерация успешно перемещен к следующему значению.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1600">The `MoveNext` method returns `true` to its caller, indicating that the iteration successfully advanced to the next value.</span></span>
*  <span data-ttu-id="c51c7-1601">Когда `yield break` встречается ([оператор yield](statements.md#the-yield-statement)):</span><span class="sxs-lookup"><span data-stu-id="c51c7-1601">When a `yield break` statement is encountered ([The yield statement](statements.md#the-yield-statement)):</span></span>
   * <span data-ttu-id="c51c7-1602">Если `yield break` оператор находится внутри одного или нескольких `try` блокирует, сопоставленного `finally` блоки выполняются.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1602">If the `yield break` statement is within one or more `try` blocks, the associated `finally` blocks are executed.</span></span>
   * <span data-ttu-id="c51c7-1603">Изменения состояния объекта перечислителя на ***после***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1603">The state of the enumerator object is changed to ***after***.</span></span>
   * <span data-ttu-id="c51c7-1604">`MoveNext` Возвращает метод `false` его вызывающему, в том, что итерации не полный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1604">The `MoveNext` method returns `false` to its caller, indicating that the iteration is complete.</span></span>
*  <span data-ttu-id="c51c7-1605">При обнаружении конец тела итератора:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1605">When the end of the iterator body is encountered:</span></span>
   * <span data-ttu-id="c51c7-1606">Изменения состояния объекта перечислителя на ***после***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1606">The state of the enumerator object is changed to ***after***.</span></span>
   * <span data-ttu-id="c51c7-1607">`MoveNext` Возвращает метод `false` его вызывающему, в том, что итерации не полный.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1607">The `MoveNext` method returns `false` to its caller, indicating that the iteration is complete.</span></span>
*  <span data-ttu-id="c51c7-1608">Если создаваемое исключение и отсылается из блока итератора:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1608">When an exception is thrown and propagated out of the iterator block:</span></span>
   * <span data-ttu-id="c51c7-1609">Соответствующие `finally` будет, блоков в тела итератора были выполнены посредством распространение исключения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1609">Appropriate `finally` blocks in the iterator body will have been executed by the exception propagation.</span></span>
   * <span data-ttu-id="c51c7-1610">Изменения состояния объекта перечислителя на ***после***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1610">The state of the enumerator object is changed to ***after***.</span></span>
   * <span data-ttu-id="c51c7-1611">Распространение исключения продолжается вызывающему объекту `MoveNext` метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1611">The exception propagation continues to the caller of the `MoveNext` method.</span></span>

#### <a name="the-current-property"></a><span data-ttu-id="c51c7-1612">Свойство Current</span><span class="sxs-lookup"><span data-stu-id="c51c7-1612">The Current property</span></span>

<span data-ttu-id="c51c7-1613">Объект перечислителя `Current` влияет свойство `yield return` инструкций в блоке итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1613">An enumerator object's `Current` property is affected by `yield return` statements in the iterator block.</span></span>

<span data-ttu-id="c51c7-1614">Когда объект-перечислитель находится в ***приостановлено*** state, значение `Current` является значение, заданное параметром предыдущего вызова `MoveNext`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1614">When an enumerator object is in the ***suspended*** state, the value of `Current` is the value set by the previous call to `MoveNext`.</span></span> <span data-ttu-id="c51c7-1615">Когда объект-перечислитель находится в ***перед***, ***под управлением***, или ***после*** состояния, результат обращения к `Current` не определен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1615">When an enumerator object is in the ***before***, ***running***, or ***after*** states, the result of accessing `Current` is unspecified.</span></span>

<span data-ttu-id="c51c7-1616">Для итератора с yield типы, отличные от `object`, результат обращения к `Current` посредством объекта-перечислителя `IEnumerable` соответствующий доступ к реализации `Current` посредством объекта-перечислителя `IEnumerator<T>` Реализация, а также преобразование результата для `object`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1616">For an iterator with a yield type other than `object`, the result of accessing `Current` through the enumerator object's `IEnumerable` implementation corresponds to accessing `Current` through the enumerator object's `IEnumerator<T>` implementation and casting the result to `object`.</span></span>

#### <a name="the-dispose-method"></a><span data-ttu-id="c51c7-1617">Метод Dispose</span><span class="sxs-lookup"><span data-stu-id="c51c7-1617">The Dispose method</span></span>

<span data-ttu-id="c51c7-1618">`Dispose` Метод используется для очистки итерации, разместив объекта-перечислителя в ***после*** состояния.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1618">The `Dispose` method is used to clean up the iteration by bringing the enumerator object to the ***after*** state.</span></span>

*  <span data-ttu-id="c51c7-1619">Если состояние объекта перечислителя ***перед***, вызов `Dispose` изменяет состояние на ***после***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1619">If the state of the enumerator object is ***before***, invoking `Dispose` changes the state to ***after***.</span></span>
*  <span data-ttu-id="c51c7-1620">Если состояние объекта перечислителя ***под управлением***, в результате вызова `Dispose` не определен.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1620">If the state of the enumerator object is ***running***, the result of invoking `Dispose` is unspecified.</span></span>
*  <span data-ttu-id="c51c7-1621">Если состояние объекта перечислителя ***приостановлено***, вызов `Dispose`:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1621">If the state of the enumerator object is ***suspended***, invoking `Dispose`:</span></span>
   * <span data-ttu-id="c51c7-1622">Задает состояние ***под управлением***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1622">Changes the state to ***running***.</span></span>
   * <span data-ttu-id="c51c7-1623">Выполняет любую наконец блоки так, как если бы последнего выполненного `yield return` инструкции были `yield break` инструкции.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1623">Executes any finally blocks as if the last executed `yield return` statement were a `yield break` statement.</span></span> <span data-ttu-id="c51c7-1624">Если это приводит к инициированию и распространению за пределами тела итератора исключения, состояние объекта-перечислителя присваивается ***после*** и исключение передается вызывающему объекту `Dispose` метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1624">If this causes an exception to be thrown and propagated out of the iterator body, the state of the enumerator object is set to ***after*** and the exception is propagated to the caller of the `Dispose` method.</span></span>
   * <span data-ttu-id="c51c7-1625">Задает состояние ***после***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1625">Changes the state to ***after***.</span></span>
*  <span data-ttu-id="c51c7-1626">Если состояние объекта перечислителя ***после***, вызов `Dispose` не оказывает влияния.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1626">If the state of the enumerator object is ***after***, invoking `Dispose` has no affect.</span></span>

### <a name="enumerable-objects"></a><span data-ttu-id="c51c7-1627">Перечисляемые объекты</span><span class="sxs-lookup"><span data-stu-id="c51c7-1627">Enumerable objects</span></span>

<span data-ttu-id="c51c7-1628">Когда функция-член, возвращая типа enumerable интерфейса реализуется с помощью блока итератора, вызова функции-члена не выполняется код в блоке итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1628">When a function member returning an enumerable interface type is implemented using an iterator block, invoking the function member does not immediately execute the code in the iterator block.</span></span> <span data-ttu-id="c51c7-1629">Вместо этого ***перечисляемый объект*** создается и возвращается.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1629">Instead, an ***enumerable object*** is created and returned.</span></span> <span data-ttu-id="c51c7-1630">Перечисляемый объект `GetEnumerator` метод возвращает объект перечислителя, который инкапсулирует код, указанный в блоке итератора, а выполнение кода в блоке итератора происходит при объекта-перечислителя `MoveNext` вызывается метод.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1630">The enumerable object's `GetEnumerator` method returns an enumerator object that encapsulates the code specified in the iterator block, and execution of the code in the iterator block occurs when the enumerator object's `MoveNext` method is invoked.</span></span> <span data-ttu-id="c51c7-1631">Перечислимый объект имеет следующие характеристики:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1631">An enumerable object has the following characteristics:</span></span>

*  <span data-ttu-id="c51c7-1632">Он реализует `IEnumerable` и `IEnumerable<T>`, где `T` yield тип итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1632">It implements `IEnumerable` and `IEnumerable<T>`, where `T` is the yield type of the iterator.</span></span>
*  <span data-ttu-id="c51c7-1633">Она инициализируется с копией значения аргументов (если таковые имеются) и экземпляр значение, передаваемое в функцию-член.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1633">It is initialized with a copy of the argument values (if any) and instance value passed to the function member.</span></span>

<span data-ttu-id="c51c7-1634">Перечисляемый объект обычно является экземпляром созданного компилятором класса enumerable, который инкапсулирует код в блоке итератора и реализует IEnumerable-интерфейс, но возможны и другие методы реализации.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1634">An enumerable object is typically an instance of a compiler-generated enumerable class that encapsulates the code in the iterator block and implements the enumerable interfaces, but other methods of implementation are possible.</span></span> <span data-ttu-id="c51c7-1635">Если перечислимый класс создан компилятором, этот класс будет вложен, прямо или косвенно, в класс, содержащий функцию-член, он будет иметь режим доступа private и он будет иметь имя зарезервировано для внутреннего использования компиляторами ([идентификаторы ](lexical-structure.md#identifiers)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1635">If an enumerable class is generated by the compiler, that class will be nested, directly or indirectly, in the class containing the function member, it will have private accessibility, and it will have a name reserved for compiler use ([Identifiers](lexical-structure.md#identifiers)).</span></span>

<span data-ttu-id="c51c7-1636">Перечислимый объект может реализовывать несколько интерфейсов, чем указано выше.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1636">An enumerable object may implement more interfaces than those specified above.</span></span> <span data-ttu-id="c51c7-1637">В частности, перечислимый объект может также реализовать `IEnumerator` и `IEnumerator<T>`, позволяя ей обслуживать как перечислимый объект и перечислитель.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1637">In particular, an enumerable object may also implement `IEnumerator` and `IEnumerator<T>`, enabling it to serve as both an enumerable and an enumerator.</span></span> <span data-ttu-id="c51c7-1638">В этом типе реализации первой перечисляемый объект `GetEnumerator` вызывается метод, возвращается сам перечислимый объект.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1638">In that type of implementation, the first time an enumerable object's `GetEnumerator` method is invoked, the enumerable object itself is returned.</span></span> <span data-ttu-id="c51c7-1639">Последующие вызовы функции перечисляемый объект `GetEnumerator`, если имеется, возвращает копию перечисляемый объект.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1639">Subsequent invocations of the enumerable object's `GetEnumerator`, if any, return a copy of the enumerable object.</span></span> <span data-ttu-id="c51c7-1640">Таким образом каждый возвращенный перечислитель имеет собственное состояние, и изменения в одном перечислителе не повлияет на другую.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1640">Thus, each returned enumerator has its own state and changes in one enumerator will not affect another.</span></span>

#### <a name="the-getenumerator-method"></a><span data-ttu-id="c51c7-1641">Метод GetEnumerator</span><span class="sxs-lookup"><span data-stu-id="c51c7-1641">The GetEnumerator method</span></span>

<span data-ttu-id="c51c7-1642">Перечисляемый объект предоставляет реализацию `GetEnumerator` методы `IEnumerable` и `IEnumerable<T>` интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1642">An enumerable object provides an implementation of the `GetEnumerator` methods of the `IEnumerable` and `IEnumerable<T>` interfaces.</span></span> <span data-ttu-id="c51c7-1643">Два `GetEnumerator` методы совместно используют общую реализацию, которая получает и возвращает доступный объект перечислителя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1643">The two `GetEnumerator` methods share a common implementation that acquires and returns an available enumerator object.</span></span> <span data-ttu-id="c51c7-1644">Объект перечислителя инициализируется со значениями аргументов и значением экземпляра, сохраненными при перечисляемый объект был инициализирован, но в других функций объект перечислителя, как описано в разделе [объекты перечислителя](classes.md#enumerator-objects).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1644">The enumerator object is initialized with the argument values and instance value saved when the enumerable object was initialized, but otherwise the enumerator object functions as described in [Enumerator objects](classes.md#enumerator-objects).</span></span>

### <a name="implementation-example"></a><span data-ttu-id="c51c7-1645">Пример реализации</span><span class="sxs-lookup"><span data-stu-id="c51c7-1645">Implementation example</span></span>

<span data-ttu-id="c51c7-1646">В этом разделе описывается возможная реализация итераторов с точки зрения стандартные конструкции C#.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1646">This section describes a possible implementation of iterators in terms of standard C# constructs.</span></span> <span data-ttu-id="c51c7-1647">Описанные здесь реализация основана на принципах, используемых компилятором Microsoft C#, но это отнюдь не является обязательной или единственной возможной.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1647">The implementation described here is based on the same principles used by the Microsoft C# compiler, but it is by no means a mandated implementation or the only one possible.</span></span>

<span data-ttu-id="c51c7-1648">Следующие `Stack<T>` класс реализует его `GetEnumerator` метод, с помощью итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1648">The following `Stack<T>` class implements its `GetEnumerator` method using an iterator.</span></span> <span data-ttu-id="c51c7-1649">Итератор перечисляет элементы коллекции в стек в порядке сверху вниз.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1649">The iterator enumerates the elements of the stack in top to bottom order.</span></span>

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

class Stack<T>: IEnumerable<T>
{
    T[] items;
    int count;

    public void Push(T item) {
        if (items == null) {
            items = new T[4];
        }
        else if (items.Length == count) {
            T[] newItems = new T[count * 2];
            Array.Copy(items, 0, newItems, 0, count);
            items = newItems;
        }
        items[count++] = item;
    }

    public T Pop() {
        T result = items[--count];
        items[count] = default(T);
        return result;
    }

    public IEnumerator<T> GetEnumerator() {
        for (int i = count - 1; i >= 0; --i) yield return items[i];
    }
}
```

<span data-ttu-id="c51c7-1650">`GetEnumerator` Метод может транслировать в экземпляр класса перечислителя, созданного компилятором, который инкапсулирует код в блоке итератора, как показано в следующем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1650">The `GetEnumerator` method can be translated into an instantiation of a compiler-generated enumerator class that encapsulates the code in the iterator block, as shown in the following.</span></span>

```csharp
class Stack<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }

    class __Enumerator1: IEnumerator<T>, IEnumerator
    {
        int __state;
        T __current;
        Stack<T> __this;
        int i;

        public __Enumerator1(Stack<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            switch (__state) {
                case 1: goto __state1;
                case 2: goto __state2;
            }
            i = __this.count - 1;
        __loop:
            if (i < 0) goto __state2;
            __current = __this.items[i];
            __state = 1;
            return true;
        __state1:
            --i;
            goto __loop;
        __state2:
            __state = 2;
            return false;
        }

        public void Dispose() {
            __state = 2;
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

<span data-ttu-id="c51c7-1651">В предыдущей трансляции включается в конечный автомат и поместить в код в блоке итератора `MoveNext` метод класса перечислителя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1651">In the preceding translation, the code in the iterator block is turned into a state machine and placed in the `MoveNext` method of the enumerator class.</span></span> <span data-ttu-id="c51c7-1652">Кроме того локальной переменной `i` включен в поле объекта-перечислителя, чтобы оно могло продолжать существовать при последующих вызовах `MoveNext`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1652">Furthermore, the local variable `i` is turned into a field in the enumerator object so it can continue to exist across invocations of `MoveNext`.</span></span>

<span data-ttu-id="c51c7-1653">В следующем примере выводится, простые таблицы умножения целых чисел от 1 до 10.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1653">The following example prints a simple multiplication table of the integers 1 through 10.</span></span> <span data-ttu-id="c51c7-1654">`FromTo` Метод в этом примере Возвращает перечислимый объект и реализуется с помощью итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1654">The `FromTo` method in the example returns an enumerable object and is implemented using an iterator.</span></span>

```csharp
using System;
using System.Collections.Generic;

class Test
{
    static IEnumerable<int> FromTo(int from, int to) {
        while (from <= to) yield return from++;
    }

    static void Main() {
        IEnumerable<int> e = FromTo(1, 10);
        foreach (int x in e) {
            foreach (int y in e) {
                Console.Write("{0,3} ", x * y);
            }
            Console.WriteLine();
        }
    }
}
```

<span data-ttu-id="c51c7-1655">`FromTo` Метод, транслируются в экземпляр компилятором класса enumerable, который инкапсулирует код в блоке итератора, как показано в следующем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1655">The `FromTo` method can be translated into an instantiation of a compiler-generated enumerable class that encapsulates the code in the iterator block, as shown in the following.</span></span>

```csharp
using System;
using System.Threading;
using System.Collections;
using System.Collections.Generic;

class Test
{
    ...

    static IEnumerable<int> FromTo(int from, int to) {
        return new __Enumerable1(from, to);
    }

    class __Enumerable1:
        IEnumerable<int>, IEnumerable,
        IEnumerator<int>, IEnumerator
    {
        int __state;
        int __current;
        int __from;
        int from;
        int to;
        int i;

        public __Enumerable1(int __from, int to) {
            this.__from = __from;
            this.to = to;
        }

        public IEnumerator<int> GetEnumerator() {
            __Enumerable1 result = this;
            if (Interlocked.CompareExchange(ref __state, 1, 0) != 0) {
                result = new __Enumerable1(__from, to);
                result.__state = 1;
            }
            result.from = result.__from;
            return result;
        }

        IEnumerator IEnumerable.GetEnumerator() {
            return (IEnumerator)GetEnumerator();
        }

        public int Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            switch (__state) {
            case 1:
                if (from > to) goto case 2;
                __current = from++;
                __state = 1;
                return true;
            case 2:
                __state = 2;
                return false;
            default:
                throw new InvalidOperationException();
            }
        }

        public void Dispose() {
            __state = 2;
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

<span data-ttu-id="c51c7-1656">Класс enumerable реализует IEnumerable-интерфейс и интерфейсы перечислителя, позволяя ей обслуживать как перечислимый объект и перечислитель.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1656">The enumerable class implements both the enumerable interfaces and the enumerator interfaces, enabling it to serve as both an enumerable and an enumerator.</span></span> <span data-ttu-id="c51c7-1657">В первый раз `GetEnumerator` вызывается метод, возвращается сам перечислимый объект.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1657">The first time the `GetEnumerator` method is invoked, the enumerable object itself is returned.</span></span> <span data-ttu-id="c51c7-1658">Последующие вызовы функции перечисляемый объект `GetEnumerator`, если имеется, возвращает копию перечисляемый объект.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1658">Subsequent invocations of the enumerable object's `GetEnumerator`, if any, return a copy of the enumerable object.</span></span> <span data-ttu-id="c51c7-1659">Таким образом каждый возвращенный перечислитель имеет собственное состояние, и изменения в одном перечислителе не повлияет на другую.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1659">Thus, each returned enumerator has its own state and changes in one enumerator will not affect another.</span></span> <span data-ttu-id="c51c7-1660">`Interlocked.CompareExchange` Метод используется для работы с потоками.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1660">The `Interlocked.CompareExchange` method is used to ensure thread-safe operation.</span></span>

<span data-ttu-id="c51c7-1661">`from` И `to` параметров преобразуются в поля в класс enumerable.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1661">The `from` and `to` parameters are turned into fields in the enumerable class.</span></span> <span data-ttu-id="c51c7-1662">Так как `from` изменяется в блоке итератора, дополнительный `__from` поле впервые появилось в начальное значение, присваиваемое `from` в каждого перечислителя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1662">Because `from` is modified in the iterator block, an additional `__from` field is introduced to hold the initial value given to `from` in each enumerator.</span></span>

<span data-ttu-id="c51c7-1663">`MoveNext` Вызывает метод `InvalidOperationException` если он вызывается, когда `__state` является `0`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1663">The `MoveNext` method throws an `InvalidOperationException` if it is called when `__state` is `0`.</span></span> <span data-ttu-id="c51c7-1664">Это обеспечивает защиту от использования перечислимого объекта в качестве объекта перечислителя без предварительного вызова функции `GetEnumerator`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1664">This protects against use of the enumerable object as an enumerator object without first calling `GetEnumerator`.</span></span>

<span data-ttu-id="c51c7-1665">В следующем примере показан класс простого дерева.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1665">The following example shows a simple tree class.</span></span> <span data-ttu-id="c51c7-1666">`Tree<T>` Класс реализует его `GetEnumerator` метод, с помощью итератора.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1666">The `Tree<T>` class implements its `GetEnumerator` method using an iterator.</span></span> <span data-ttu-id="c51c7-1667">Итератор перечисляет элементы дерева в порядке инфиксные.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1667">The iterator enumerates the elements of the tree in infix order.</span></span>

```csharp
using System;
using System.Collections.Generic;

class Tree<T>: IEnumerable<T>
{
    T value;
    Tree<T> left;
    Tree<T> right;

    public Tree(T value, Tree<T> left, Tree<T> right) {
        this.value = value;
        this.left = left;
        this.right = right;
    }

    public IEnumerator<T> GetEnumerator() {
        if (left != null) foreach (T x in left) yield x;
        yield value;
        if (right != null) foreach (T x in right) yield x;
    }
}

class Program
{
    static Tree<T> MakeTree<T>(T[] items, int left, int right) {
        if (left > right) return null;
        int i = (left + right) / 2;
        return new Tree<T>(items[i], 
            MakeTree(items, left, i - 1),
            MakeTree(items, i + 1, right));
    }

    static Tree<T> MakeTree<T>(params T[] items) {
        return MakeTree(items, 0, items.Length - 1);
    }

    // The output of the program is:
    // 1 2 3 4 5 6 7 8 9
    // Mon Tue Wed Thu Fri Sat Sun

    static void Main() {
        Tree<int> ints = MakeTree(1, 2, 3, 4, 5, 6, 7, 8, 9);
        foreach (int i in ints) Console.Write("{0} ", i);
        Console.WriteLine();

        Tree<string> strings = MakeTree(
            "Mon", "Tue", "Wed", "Thu", "Fri", "Sat", "Sun");
        foreach (string s in strings) Console.Write("{0} ", s);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="c51c7-1668">`GetEnumerator` Метод может транслировать в экземпляр класса перечислителя, созданного компилятором, который инкапсулирует код в блоке итератора, как показано в следующем.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1668">The `GetEnumerator` method can be translated into an instantiation of a compiler-generated enumerator class that encapsulates the code in the iterator block, as shown in the following.</span></span>

```csharp
class Tree<T>: IEnumerable<T>
{
    ...

    public IEnumerator<T> GetEnumerator() {
        return new __Enumerator1(this);
    }

    class __Enumerator1 : IEnumerator<T>, IEnumerator
    {
        Node<T> __this;
        IEnumerator<T> __left, __right;
        int __state;
        T __current;

        public __Enumerator1(Node<T> __this) {
            this.__this = __this;
        }

        public T Current {
            get { return __current; }
        }

        object IEnumerator.Current {
            get { return __current; }
        }

        public bool MoveNext() {
            try {
                switch (__state) {

                case 0:
                    __state = -1;
                    if (__this.left == null) goto __yield_value;
                    __left = __this.left.GetEnumerator();
                    goto case 1;

                case 1:
                    __state = -2;
                    if (!__left.MoveNext()) goto __left_dispose;
                    __current = __left.Current;
                    __state = 1;
                    return true;

                __left_dispose:
                    __state = -1;
                    __left.Dispose();

                __yield_value:
                    __current = __this.value;
                    __state = 2;
                    return true;

                case 2:
                    __state = -1;
                    if (__this.right == null) goto __end;
                    __right = __this.right.GetEnumerator();
                    goto case 3;

                case 3:
                    __state = -3;
                    if (!__right.MoveNext()) goto __right_dispose;
                    __current = __right.Current;
                    __state = 3;
                    return true;

                __right_dispose:
                    __state = -1;
                    __right.Dispose();

                __end:
                    __state = 4;
                    break;

                }
            }
            finally {
                if (__state < 0) Dispose();
            }
            return false;
        }

        public void Dispose() {
            try {
                switch (__state) {

                case 1:
                case -2:
                    __left.Dispose();
                    break;

                case 3:
                case -3:
                    __right.Dispose();
                    break;

                }
            }
            finally {
                __state = 4;
            }
        }

        void IEnumerator.Reset() {
            throw new NotSupportedException();
        }
    }
}
```

<span data-ttu-id="c51c7-1669">Созданный компилятором временных переменных, используемых в `foreach` инструкций будет снято в `__left` и `__right` поля объекта перечислителя.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1669">The compiler generated temporaries used in the `foreach` statements are lifted into the `__left` and `__right` fields of the enumerator object.</span></span> <span data-ttu-id="c51c7-1670">`__state` Объекта-перечислителя тщательно обновляется таким образом, правильный `Dispose()` метод будет вызываться правильно, если возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1670">The `__state` field of the enumerator object is carefully updated so that the correct `Dispose()` method will be called correctly if an exception is thrown.</span></span> <span data-ttu-id="c51c7-1671">Обратите внимание на то, что он не поддерживается для записи преобразованного кода с простыми `foreach` инструкций.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1671">Note that it is not possible to write the translated code with simple `foreach` statements.</span></span>

## <a name="async-functions"></a><span data-ttu-id="c51c7-1672">Асинхронные функции</span><span class="sxs-lookup"><span data-stu-id="c51c7-1672">Async functions</span></span>

<span data-ttu-id="c51c7-1673">Метод ([методы](classes.md#methods)) или анонимная функция ([выражения анонимных функций](expressions.md#anonymous-function-expressions)) с `async` модификатор называется ***асинхронной функции***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1673">A method ([Methods](classes.md#methods)) or anonymous function ([Anonymous function expressions](expressions.md#anonymous-function-expressions)) with the `async` modifier is called an ***async function***.</span></span> <span data-ttu-id="c51c7-1674">Как правило термин ***async*** используется для описания любого вида функции, которая имеет `async` модификатор.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1674">In general, the term ***async*** is used to describe any kind of function that has the `async` modifier.</span></span>

<span data-ttu-id="c51c7-1675">Произошла ошибка во время компиляции, список формальных параметров асинхронной функции задающих `ref` или `out` параметров.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1675">It is a compile-time error for the formal parameter list of an async function to specify any `ref` or `out` parameters.</span></span>

<span data-ttu-id="c51c7-1676">*Return_type* асинхронный метод должен быть либо `void` или ***задачи типа***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1676">The *return_type* of an async method must be either `void` or a ***task type***.</span></span> <span data-ttu-id="c51c7-1677">Типы задач, `System.Threading.Tasks.Task` и конструировать типы из `System.Threading.Tasks.Task<T>`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1677">The task types are `System.Threading.Tasks.Task` and types constructed from `System.Threading.Tasks.Task<T>`.</span></span> <span data-ttu-id="c51c7-1678">Для краткости в этой главе эти ссылки на типы как `Task` и `Task<T>`, соответственно.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1678">For the sake of brevity, in this chapter these types are referenced as `Task` and `Task<T>`, respectively.</span></span> <span data-ttu-id="c51c7-1679">Асинхронный метод возвращает тип задачи считается возвращения задачи.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1679">An async method returning a task type is said to be task-returning.</span></span>

<span data-ttu-id="c51c7-1680">Точное определение типов задач. Это определяется реализацией, но с точки зрения языка типом задачи в одном из состояний неполные данные, успешно или произошел сбой.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1680">The exact definition of the task types is implementation defined, but from the language's point of view a task type is in one of the states incomplete, succeeded or faulted.</span></span> <span data-ttu-id="c51c7-1681">Задача, завершившаяся сбоем записывает соответствующие исключения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1681">A faulted task records a pertinent exception.</span></span> <span data-ttu-id="c51c7-1682">Успешно `Task<T>` записывает результат типа `T`.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1682">A succeeded `Task<T>` records a result of type `T`.</span></span> <span data-ttu-id="c51c7-1683">Типы задач awaitable и поэтому может быть операндов выражения await ([выражениях Await](expressions.md#await-expressions)).</span><span class="sxs-lookup"><span data-stu-id="c51c7-1683">Task types are awaitable, and can therefore be the operands of await expressions ([Await expressions](expressions.md#await-expressions)).</span></span>

<span data-ttu-id="c51c7-1684">Вызов функции async имеет возможность приостанавливать оценки с помощью параметра выражениях await ([выражениях Await](expressions.md#await-expressions)) в его тексте.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1684">An async function invocation has the ability to suspend evaluation by means of await expressions ([Await expressions](expressions.md#await-expressions)) in its body.</span></span> <span data-ttu-id="c51c7-1685">Оценки позже может быть возобновить в точке приостановки выражение с помощью параметра await ***делегат возобновления***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1685">Evaluation may later be resumed at the point of the suspending await expression by means of a ***resumption delegate***.</span></span> <span data-ttu-id="c51c7-1686">Возобновление делегат имеет тип `System.Action`, и при его вызове, вычисление функции асинхронного вызова будет возобновлена с выражение await, в котором она остановилась.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1686">The resumption delegate is of type `System.Action`, and when it is invoked, evaluation of the async function invocation will resume from the await expression where it left off.</span></span> <span data-ttu-id="c51c7-1687">***Текущего вызывающего пользователя*** значения асинхронной функции вызова не данные первоначального вызывающего объекта, если вызов функции никогда не было приостановлено или самой последней вызывающий объект делегата возобновления.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1687">The ***current caller*** of an async function invocation is the original caller if the function invocation has never been suspended, or the most recent caller of the resumption delegate otherwise.</span></span>

### <a name="evaluation-of-a-task-returning-async-function"></a><span data-ttu-id="c51c7-1688">Вычисления функции async возвращающий задачу</span><span class="sxs-lookup"><span data-stu-id="c51c7-1688">Evaluation of a task-returning async function</span></span>

<span data-ttu-id="c51c7-1689">Вызов функции возвращающий задачу асинхронный вызывает экземпляр типа Возвращенная задача будет создан.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1689">Invocation of a task-returning async function causes an instance of the returned task type to be generated.</span></span> <span data-ttu-id="c51c7-1690">Это называется ***задача возврата*** функции async.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1690">This is called the ***return task*** of the async function.</span></span> <span data-ttu-id="c51c7-1691">Задача изначально находится в незавершенном состоянии.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1691">The task is initially in an incomplete state.</span></span>

<span data-ttu-id="c51c7-1692">Тело функции async затем вычисляется до (по достижении выражения await) либо приостанавливается или завершается, по которому точки управления возвращается вызывающему объекту, а также задача возврата.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1692">The async function body is then evaluated until it is either suspended (by reaching an await expression) or terminates, at which point control is returned to the caller, along with the return task.</span></span>

<span data-ttu-id="c51c7-1693">При завершении тело функции async задача возврата перемещается за пределы неполный:</span><span class="sxs-lookup"><span data-stu-id="c51c7-1693">When the body of the async function terminates, the return task is moved out of the incomplete state:</span></span>

*  <span data-ttu-id="c51c7-1694">Если в результате достижения оператор return или конец тела завершает тело функции, любой результат записывается в возвращаемое задачу, которая помещается в состоянии успешного выполнения.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1694">If the function body terminates as the result of reaching a return statement or the end of the body, any result value is recorded in the return task, which is put into a succeeded state.</span></span>
*  <span data-ttu-id="c51c7-1695">Если тело функции завершается в результате неперехваченное исключение ([инструкция throw](statements.md#the-throw-statement)) записано исключение в возвращаемое задачу, которая переходит в состояние faulted.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1695">If the function body terminates as the result of an uncaught exception ([The throw statement](statements.md#the-throw-statement)) the exception is recorded in the return task which is put into a faulted state.</span></span>

### <a name="evaluation-of-a-void-returning-async-function"></a><span data-ttu-id="c51c7-1696">Вычисления функции async возвращающие void</span><span class="sxs-lookup"><span data-stu-id="c51c7-1696">Evaluation of a void-returning async function</span></span>

<span data-ttu-id="c51c7-1697">Если тип возвращаемого значения асинхронной функции `void`, оценки отличается от приведенного выше следующим образом: так как возвращается ни одна задача, функция вместо этого взаимодействует завершения и исключения из текущего потока ***синхронизации контекст***.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1697">If the return type of the async function is `void`, evaluation differs from the above in the following way: Because no task is returned, the function instead communicates completion and exceptions to the current thread's ***synchronization context***.</span></span> <span data-ttu-id="c51c7-1698">Точное определение контекст синхронизации, зависит от реализации, но является представлением элемента «where» выполняется текущий поток.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1698">The exact definition of synchronization context is implementation-dependent, but is a representation of "where" the current thread is running.</span></span> <span data-ttu-id="c51c7-1699">Контекст синхронизации уведомляется при вычисления функции async возвращающую начинается, завершается успешно или вызывает исключение исключение.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1699">The synchronization context is notified when evaluation of a void-returning async function commences, completes successfully, or causes an uncaught exception to be thrown.</span></span>

<span data-ttu-id="c51c7-1700">Это обеспечивает контекст для отслеживания количества асинхронные функции, возвращающие void запускается под его управлением и принятия решения о том, как распространить исключения, поступающие из них.</span><span class="sxs-lookup"><span data-stu-id="c51c7-1700">This allows the context to keep track of how many void-returning async functions are running under it, and to decide how to propagate exceptions coming out of them.</span></span>
