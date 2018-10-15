# <a name="enums"></a><span data-ttu-id="2b387-101">перечислениям;</span><span class="sxs-lookup"><span data-stu-id="2b387-101">Enums</span></span>

<span data-ttu-id="2b387-102">***Тип перечисления*** является особым типом значения ([типы значений](types.md#value-types)), объявляет набор именованных констант.</span><span class="sxs-lookup"><span data-stu-id="2b387-102">An ***enum type*** is a distinct value type ([Value types](types.md#value-types)) that declares a set of named constants.</span></span>

<span data-ttu-id="2b387-103">Пример</span><span class="sxs-lookup"><span data-stu-id="2b387-103">The example</span></span>

```csharp
enum Color
{
    Red,
    Green,
    Blue
}
```

<span data-ttu-id="2b387-104">Объявляет тип перечисления с именем `Color` с членами `Red`, `Green`, и `Blue`.</span><span class="sxs-lookup"><span data-stu-id="2b387-104">declares an enum type named `Color` with members `Red`, `Green`, and `Blue`.</span></span>

## <a name="enum-declarations"></a><span data-ttu-id="2b387-105">Объявления перечислений</span><span class="sxs-lookup"><span data-stu-id="2b387-105">Enum declarations</span></span>

<span data-ttu-id="2b387-106">Объявление перечисления объявляет новый тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-106">An enum declaration declares a new enum type.</span></span> <span data-ttu-id="2b387-107">Объявление перечисления начинается с ключевого слова `enum`и определяет имя, специальных возможностей, базового типа и членов перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-107">An enum declaration begins with the keyword `enum`, and defines the name, accessibility, underlying type, and members of the enum.</span></span>

```antlr
enum_declaration
    : attributes? enum_modifier* 'enum' identifier enum_base? enum_body ';'?
    ;

enum_base
    : ':' integral_type
    ;

enum_body
    : '{' enum_member_declarations? '}'
    | '{' enum_member_declarations ',' '}'
    ;
```

<span data-ttu-id="2b387-108">Каждый тип перечисления имеет соответствующий целочисленных типов, который ***базовый тип*** типа перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-108">Each enum type has a corresponding integral type called the ***underlying type*** of the enum type.</span></span> <span data-ttu-id="2b387-109">Этот базовый тип должен иметь возможность представлять все значения перечислителя, определенных в перечислении.</span><span class="sxs-lookup"><span data-stu-id="2b387-109">This underlying type must be able to represent all the enumerator values defined in the enumeration.</span></span> <span data-ttu-id="2b387-110">Объявление перечисления может явно объявлять является базовым типом `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long` или `ulong`.</span><span class="sxs-lookup"><span data-stu-id="2b387-110">An enum declaration may explicitly declare an underlying type of `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long` or `ulong`.</span></span> <span data-ttu-id="2b387-111">Обратите внимание, что `char` нельзя использовать в качестве базового типа.</span><span class="sxs-lookup"><span data-stu-id="2b387-111">Note that `char` cannot be used as an underlying type.</span></span> <span data-ttu-id="2b387-112">Объявления явно объявляет базовый тип перечисления имеет базовый тип из `int`.</span><span class="sxs-lookup"><span data-stu-id="2b387-112">An enum declaration that does not explicitly declare an underlying type has an underlying type of `int`.</span></span>

<span data-ttu-id="2b387-113">Пример</span><span class="sxs-lookup"><span data-stu-id="2b387-113">The example</span></span>

```csharp
enum Color: long
{
    Red,
    Green,
    Blue
}
```

<span data-ttu-id="2b387-114">Объявляет перечисление с базовым типом `long`.</span><span class="sxs-lookup"><span data-stu-id="2b387-114">declares an enum with an underlying type of `long`.</span></span> <span data-ttu-id="2b387-115">Разработчик может выбрать для использования является базовым типом `long`, как показано в примере, чтобы включить использование значений, которые находятся в диапазоне от `long` , но не в диапазоне от `int`, или сохранить этот параметр в будущем.</span><span class="sxs-lookup"><span data-stu-id="2b387-115">A developer might choose to use an underlying type of `long`, as in the example, to enable the use of values that are in the range of `long` but not in the range of `int`, or to preserve this option for the future.</span></span>

## <a name="enum-modifiers"></a><span data-ttu-id="2b387-116">Модификаторы перечислений</span><span class="sxs-lookup"><span data-stu-id="2b387-116">Enum modifiers</span></span>

<span data-ttu-id="2b387-117">*Enum_declaration* может включать последовательность модификаторов перечисления:</span><span class="sxs-lookup"><span data-stu-id="2b387-117">An *enum_declaration* may optionally include a sequence of enum modifiers:</span></span>

```antlr
enum_modifier
    : 'new'
    | 'public'
    | 'protected'
    | 'internal'
    | 'private'
    ;
```

<span data-ttu-id="2b387-118">Это ошибка времени компиляции для один и тот же модификатор встречается несколько раз в объявлении перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-118">It is a compile-time error for the same modifier to appear multiple times in an enum declaration.</span></span>

<span data-ttu-id="2b387-119">Модификаторы объявления перечисления имеют одинаковое значение, что и объявление класса ([класса модификаторы](classes.md#class-modifiers)).</span><span class="sxs-lookup"><span data-stu-id="2b387-119">The modifiers of an enum declaration have the same meaning as those of a class declaration ([Class modifiers](classes.md#class-modifiers)).</span></span> <span data-ttu-id="2b387-120">Обратите внимание, что `abstract` и `sealed` модификаторы не разрешается использовать в объявлении перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-120">Note, however, that the `abstract` and `sealed` modifiers are not permitted in an enum declaration.</span></span> <span data-ttu-id="2b387-121">Перечисления не может быть абстрактным и не допускают наследование.</span><span class="sxs-lookup"><span data-stu-id="2b387-121">Enums cannot be abstract and do not permit derivation.</span></span>

## <a name="enum-members"></a><span data-ttu-id="2b387-122">Члены перечисления</span><span class="sxs-lookup"><span data-stu-id="2b387-122">Enum members</span></span>

<span data-ttu-id="2b387-123">Текст объявления типа перечисления определяет ноль или несколько членов перечисления, которые являются именованными константами перечисляемого типа.</span><span class="sxs-lookup"><span data-stu-id="2b387-123">The body of an enum type declaration defines zero or more enum members, which are the named constants of the enum type.</span></span> <span data-ttu-id="2b387-124">Два члена не может иметь тем же именем.</span><span class="sxs-lookup"><span data-stu-id="2b387-124">No two enum members can have the same name.</span></span>

```antlr
enum_member_declarations
    : enum_member_declaration (',' enum_member_declaration)*
    ;

enum_member_declaration
    : attributes? identifier ('=' constant_expression)?
    ;
```

<span data-ttu-id="2b387-125">Каждый член перечисления имеет связанное значение константы.</span><span class="sxs-lookup"><span data-stu-id="2b387-125">Each enum member has an associated constant value.</span></span> <span data-ttu-id="2b387-126">Тип этого значения является базовым типом для содержащего его перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-126">The type of this value is the underlying type for the containing enum.</span></span> <span data-ttu-id="2b387-127">Постоянное значение для каждого члена перечисления должен быть в диапазоне базового типа для перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-127">The constant value for each enum member must be in the range of the underlying type for the enum.</span></span> <span data-ttu-id="2b387-128">Пример</span><span class="sxs-lookup"><span data-stu-id="2b387-128">The example</span></span>

```csharp
enum Color: uint
{
    Red = -1,
    Green = -2,
    Blue = -3
}
```

<span data-ttu-id="2b387-129">приводит к ошибке времени компиляции, так как значения констант `-1`, `-2`, и `-3` не находятся в диапазоне базового целочисленного типа `uint`.</span><span class="sxs-lookup"><span data-stu-id="2b387-129">results in a compile-time error because the constant values `-1`, `-2`, and `-3` are not in the range of the underlying integral type `uint`.</span></span>

<span data-ttu-id="2b387-130">Несколько членов перечисления могут совместно использовать то же связанное значение.</span><span class="sxs-lookup"><span data-stu-id="2b387-130">Multiple enum members may share the same associated value.</span></span> <span data-ttu-id="2b387-131">Пример</span><span class="sxs-lookup"><span data-stu-id="2b387-131">The example</span></span>

```csharp
enum Color 
{
    Red,
    Green,
    Blue,

    Max = Blue
}
```

<span data-ttu-id="2b387-132">показано перечисление, в какие два члена перечисления-- `Blue` и `Max` --имеют же связанное значение.</span><span class="sxs-lookup"><span data-stu-id="2b387-132">shows an enum in which two enum members -- `Blue` and `Max` -- have the same associated value.</span></span>

<span data-ttu-id="2b387-133">Связанное значение члена перечисления назначается явно или неявно.</span><span class="sxs-lookup"><span data-stu-id="2b387-133">The associated value of an enum member is assigned either implicitly or explicitly.</span></span> <span data-ttu-id="2b387-134">Если объявление члена перечисления содержит *constant_expression* инициализатор, значение константного выражения, неявно преобразуется в базовый тип перечисления, является связанное значение члена перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-134">If the declaration of the enum member has a *constant_expression* initializer, the value of that constant expression, implicitly converted to the underlying type of the enum, is the associated value of the enum member.</span></span> <span data-ttu-id="2b387-135">Если объявление члена перечисления не содержится инициализатор, связанное с ним значение задано, неявно, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="2b387-135">If the declaration of the enum member has no initializer, its associated value is set implicitly, as follows:</span></span>

*  <span data-ttu-id="2b387-136">Если член перечисления является первым членом перечисления, объявленных в типе перечисления, связанное с ним значение равно нулю.</span><span class="sxs-lookup"><span data-stu-id="2b387-136">If the enum member is the first enum member declared in the enum type, its associated value is zero.</span></span>
*  <span data-ttu-id="2b387-137">В противном случае связанное значение члена перечисления получается путем увеличения на единицу связанное значение объявленного члена перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-137">Otherwise, the associated value of the enum member is obtained by increasing the associated value of the textually preceding enum member by one.</span></span> <span data-ttu-id="2b387-138">Это увеличенное значение должно быть в диапазоне значений, которые могут быть представлены в базовый тип, иначе возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="2b387-138">This increased value must be within the range of values that can be represented by the underlying type, otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="2b387-139">Пример</span><span class="sxs-lookup"><span data-stu-id="2b387-139">The example</span></span>

```csharp
using System;

enum Color
{
    Red,
    Green = 10,
    Blue
}

class Test
{
    static void Main() {
        Console.WriteLine(StringFromColor(Color.Red));
        Console.WriteLine(StringFromColor(Color.Green));
        Console.WriteLine(StringFromColor(Color.Blue));
    }

    static string StringFromColor(Color c) {
        switch (c) {
            case Color.Red: 
                return String.Format("Red = {0}", (int) c);

            case Color.Green:
                return String.Format("Green = {0}", (int) c);

            case Color.Blue:
                return String.Format("Blue = {0}", (int) c);

            default:
                return "Invalid color";
        }
    }
}
```

<span data-ttu-id="2b387-140">Выводит имена членов перечисления и связанных с ними значений.</span><span class="sxs-lookup"><span data-stu-id="2b387-140">prints out the enum member names and their associated values.</span></span> <span data-ttu-id="2b387-141">Результат.</span><span class="sxs-lookup"><span data-stu-id="2b387-141">The output is:</span></span>

```
Red = 0
Green = 10
Blue = 11
```

<span data-ttu-id="2b387-142">по следующим причинам:</span><span class="sxs-lookup"><span data-stu-id="2b387-142">for the following reasons:</span></span>

*  <span data-ttu-id="2b387-143">член перечисления `Red` автоматически присваивается значение ноль (так как он не содержится инициализатор и является первым членом перечисления);</span><span class="sxs-lookup"><span data-stu-id="2b387-143">the enum member `Red` is automatically assigned the value zero (since it has no initializer and is the first enum member);</span></span>
*  <span data-ttu-id="2b387-144">член перечисления `Green` явным образом присваивается значение `10`;</span><span class="sxs-lookup"><span data-stu-id="2b387-144">the enum member `Green` is explicitly given the value `10`;</span></span>
*  <span data-ttu-id="2b387-145">и член перечисления `Blue` автоматически присваивается значение больше, чем элемента, превышающее один.</span><span class="sxs-lookup"><span data-stu-id="2b387-145">and the enum member `Blue` is automatically assigned the value one greater than the member that textually precedes it.</span></span>

<span data-ttu-id="2b387-146">Связанное значение члена перечисления не может, прямо или косвенно, используйте значение свой собственный связанного члена перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-146">The associated value of an enum member may not, directly or indirectly, use the value of its own associated enum member.</span></span> <span data-ttu-id="2b387-147">Кроме этого ограничения зацикливания инициализаторы членов перечисления могут свободно ссылаться на другие инициализаторы членов перечисления, независимо от их положения в тексте.</span><span class="sxs-lookup"><span data-stu-id="2b387-147">Other than this circularity restriction, enum member initializers may freely refer to other enum member initializers, regardless of their textual position.</span></span> <span data-ttu-id="2b387-148">В инициализаторе члена перечисления значения других членов перечисления всегда обрабатываются как имеющие тип их базового типа, таким образом, чтобы приведения не обязательны, при ссылке на другие члены перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-148">Within an enum member initializer, values of other enum members are always treated as having the type of their underlying type, so that casts are not necessary when referring to other enum members.</span></span>

<span data-ttu-id="2b387-149">Пример</span><span class="sxs-lookup"><span data-stu-id="2b387-149">The example</span></span>

```csharp
enum Circular
{
    A = B,
    B
}
```

<span data-ttu-id="2b387-150">приводит к ошибке времени компиляции, так как объявления `A` и `B` являются циклическими.</span><span class="sxs-lookup"><span data-stu-id="2b387-150">results in a compile-time error because the declarations of `A` and `B` are circular.</span></span> <span data-ttu-id="2b387-151">`A` зависит от `B` явным образом, и `B` зависит от `A` неявно.</span><span class="sxs-lookup"><span data-stu-id="2b387-151">`A` depends on `B` explicitly, and `B` depends on `A` implicitly.</span></span>

<span data-ttu-id="2b387-152">Члены перечисления с именем и в совершенно аналогично полям в классах с заданной областью.</span><span class="sxs-lookup"><span data-stu-id="2b387-152">Enum members are named and scoped in a manner exactly analogous to fields within classes.</span></span> <span data-ttu-id="2b387-153">Областью члена перечисления является тело его содержащий тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-153">The scope of an enum member is the body of its containing enum type.</span></span> <span data-ttu-id="2b387-154">Внутри этой области Члены перечисления можно ссылаться по их простому имени.</span><span class="sxs-lookup"><span data-stu-id="2b387-154">Within that scope, enum members can be referred to by their simple name.</span></span> <span data-ttu-id="2b387-155">Из другого кода имя члена перечисления должно уточняться именем его перечисляемого типа.</span><span class="sxs-lookup"><span data-stu-id="2b387-155">From all other code, the name of an enum member must be qualified with the name of its enum type.</span></span> <span data-ttu-id="2b387-156">Члены перечисления не любой объявленный уровень доступности — члена перечисления доступен, если его содержащий тип перечисления доступен.</span><span class="sxs-lookup"><span data-stu-id="2b387-156">Enum members do not have any declared accessibility -- an enum member is accessible if its containing enum type is accessible.</span></span>

## <a name="the-systemenum-type"></a><span data-ttu-id="2b387-157">Тип System.Enum</span><span class="sxs-lookup"><span data-stu-id="2b387-157">The System.Enum type</span></span>

<span data-ttu-id="2b387-158">Тип `System.Enum` — это абстрактный базовый класс для всех типов перечисления (это distinct и отличается от типа базового типа перечисления) и члены, унаследованные от `System.Enum` доступны в любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-158">The type `System.Enum` is the abstract base class of all enum types (this is distinct and different from the underlying type of the enum type), and the members inherited from `System.Enum` are available in any enum type.</span></span> <span data-ttu-id="2b387-159">Упаковка-преобразование ([осуществлять преобразования-упаковки](types.md#boxing-conversions)) из любой тип перечисления для существует `System.Enum`и распаковки-преобразования ([преобразования, распаковки-преобразования](types.md#unboxing-conversions)) существует `System.Enum` в любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-159">A boxing conversion ([Boxing conversions](types.md#boxing-conversions)) exists from any enum type to `System.Enum`, and an unboxing conversion ([Unboxing conversions](types.md#unboxing-conversions)) exists from `System.Enum` to any enum type.</span></span>

<span data-ttu-id="2b387-160">Обратите внимание, что `System.Enum` сам не *enum_type*.</span><span class="sxs-lookup"><span data-stu-id="2b387-160">Note that `System.Enum` is not itself an *enum_type*.</span></span> <span data-ttu-id="2b387-161">Кроме того, это *class_type* из которой все *enum_type*s являются производными.</span><span class="sxs-lookup"><span data-stu-id="2b387-161">Rather, it is a *class_type* from which all *enum_type*s are derived.</span></span> <span data-ttu-id="2b387-162">Тип `System.Enum` наследует от типа `System.ValueType` ([типа System.ValueType](types.md#the-systemvaluetype-type)), который, в свою очередь, наследует от типа `object`.</span><span class="sxs-lookup"><span data-stu-id="2b387-162">The type `System.Enum` inherits from the type `System.ValueType` ([The System.ValueType type](types.md#the-systemvaluetype-type)), which, in turn, inherits from type `object`.</span></span> <span data-ttu-id="2b387-163">Во время выполнения, значение типа `System.Enum` может быть `null` или ссылка на упакованное значение любого типа enum.</span><span class="sxs-lookup"><span data-stu-id="2b387-163">At run-time, a value of type `System.Enum` can be `null` or a reference to a boxed value of any enum type.</span></span>

## <a name="enum-values-and-operations"></a><span data-ttu-id="2b387-164">Значения перечислений и операции</span><span class="sxs-lookup"><span data-stu-id="2b387-164">Enum values and operations</span></span>

<span data-ttu-id="2b387-165">Каждый тип перечисления определяет отдельный тип; явное преобразование ([явные преобразования перечисляемых типов](conversions.md#explicit-enumeration-conversions)) необходима для преобразования между типом enum и целочисленный тип или между двумя типами перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-165">Each enum type defines a distinct type; an explicit enumeration conversion ([Explicit enumeration conversions](conversions.md#explicit-enumeration-conversions)) is required to convert between an enum type and an integral type, or between two enum types.</span></span> <span data-ttu-id="2b387-166">Набор значений, которые может принимать тип перечисления не ограничивается его членами перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-166">The set of values that an enum type can take on is not limited by its enum members.</span></span> <span data-ttu-id="2b387-167">В частности любое значение базового типа перечисления может быть приведен к типу перечисления и будет являться допустимым дискретным значением этого типа перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-167">In particular, any value of the underlying type of an enum can be cast to the enum type, and is a distinct valid value of that enum type.</span></span>

<span data-ttu-id="2b387-168">Члены перечисления имеют тип содержащего их перечисляемого типа (за исключением в другие инициализаторы членов перечисления: см. в разделе [члены перечисления](enums.md#enum-members)).</span><span class="sxs-lookup"><span data-stu-id="2b387-168">Enum members have the type of their containing enum type (except within other enum member initializers: see [Enum members](enums.md#enum-members)).</span></span> <span data-ttu-id="2b387-169">Значение элемента перечисления, объявленного в перечисляемом типе `E` со связанным значением `v` является `(E)v`.</span><span class="sxs-lookup"><span data-stu-id="2b387-169">The value of an enum member declared in enum type `E` with associated value `v` is `(E)v`.</span></span>

<span data-ttu-id="2b387-170">Для значений типов перечисления можно использовать следующие операторы: `==`, `!=`, `<`, `>`, `<=`, `>=` ([операторы сравнения перечисления](expressions.md#enumeration-comparison-operators)), двоичный файл `+` ([Оператор сложения](expressions.md#addition-operator)), двоичная `-` ([оператор вычитания](expressions.md#subtraction-operator)), `^`, `&`, `|` ([перечисления логических операторы](expressions.md#enumeration-logical-operators)), `~` ([оператор поразрядного дополнения](expressions.md#bitwise-complement-operator)), `++` и `--` ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators) и [ Префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="2b387-170">The following operators can be used on values of enum types: `==`, `!=`, `<`, `>`, `<=`, `>=` ([Enumeration comparison operators](expressions.md#enumeration-comparison-operators)), binary `+` ([Addition operator](expressions.md#addition-operator)), binary `-` ([Subtraction operator](expressions.md#subtraction-operator)), `^`, `&`, `|` ([Enumeration logical operators](expressions.md#enumeration-logical-operators)), `~` ([Bitwise complement operator](expressions.md#bitwise-complement-operator)), `++` and `--` ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators) and [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span>

<span data-ttu-id="2b387-171">Каждый тип перечисления автоматически является производным от класса `System.Enum` (который, в свою очередь, является производным от `System.ValueType` и `object`).</span><span class="sxs-lookup"><span data-stu-id="2b387-171">Every enum type automatically derives from the class `System.Enum` (which, in turn, derives from `System.ValueType` and `object`).</span></span> <span data-ttu-id="2b387-172">Таким образом унаследованные методы и свойства этого класса может использоваться для значений типа перечисления.</span><span class="sxs-lookup"><span data-stu-id="2b387-172">Thus, inherited methods and properties of this class can be used on values of an enum type.</span></span>
