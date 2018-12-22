# <a name="arrays"></a><span data-ttu-id="1d824-101">Массивы</span><span class="sxs-lookup"><span data-stu-id="1d824-101">Arrays</span></span>

<span data-ttu-id="1d824-102">Массив — это структура данных, который содержит ряд переменных, к которым осуществляется по вычисляемым индексам.</span><span class="sxs-lookup"><span data-stu-id="1d824-102">An array is a data structure that contains a number of variables which are accessed through computed indices.</span></span> <span data-ttu-id="1d824-103">Этот тип называется типом элемента массива и переменными, содержащимися в массиве, также называются элементами массива, имеют тот же тип.</span><span class="sxs-lookup"><span data-stu-id="1d824-103">The variables contained in an array, also called the elements of the array, are all of the same type, and this type is called the element type of the array.</span></span>

<span data-ttu-id="1d824-104">Массив имеет ранг, определяющий количество индексов, связанных с каждым элементом массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-104">An array has a rank which determines the number of indices associated with each array element.</span></span> <span data-ttu-id="1d824-105">Ранг массива также называют измерений массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-105">The rank of an array is also referred to as the dimensions of the array.</span></span> <span data-ttu-id="1d824-106">Массив с рангом, называется ***одномерный массив***.</span><span class="sxs-lookup"><span data-stu-id="1d824-106">An array with a rank of one is called a ***single-dimensional array***.</span></span> <span data-ttu-id="1d824-107">Массив с рангом, превышающее один называется ***многомерного массива***.</span><span class="sxs-lookup"><span data-stu-id="1d824-107">An array with a rank greater than one is called a ***multi-dimensional array***.</span></span> <span data-ttu-id="1d824-108">Определенного размера многомерных массивов, часто называются двумерные массивы, трехмерные массивы и т. д.</span><span class="sxs-lookup"><span data-stu-id="1d824-108">Specific sized multi-dimensional arrays are often referred to as two-dimensional arrays, three-dimensional arrays, and so on.</span></span>

<span data-ttu-id="1d824-109">Каждое измерение массива имеет соответствующую длину которого является целое число больше или равно нулю.</span><span class="sxs-lookup"><span data-stu-id="1d824-109">Each dimension of an array has an associated length which is an integral number greater than or equal to zero.</span></span> <span data-ttu-id="1d824-110">Длины по измерениям не являются частью типа массива, но устанавливаются при создании экземпляра типа массива во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="1d824-110">The dimension lengths are not part of the type of the array, but rather are established when an instance of the array type is created at run-time.</span></span> <span data-ttu-id="1d824-111">Длина измерения определяет допустимый диапазон индексов для этого измерения: Для измерения длины `N`, индексы могут варьироваться от `0` для `N - 1` включительно.</span><span class="sxs-lookup"><span data-stu-id="1d824-111">The length of a dimension determines the valid range of indices for that dimension: For a dimension of length `N`, indices can range from `0` to `N - 1` inclusive.</span></span> <span data-ttu-id="1d824-112">Общее число элементов в массиве — это совокупность длину каждого измерения в массиве.</span><span class="sxs-lookup"><span data-stu-id="1d824-112">The total number of elements in an array is the product of the lengths of each dimension in the array.</span></span> <span data-ttu-id="1d824-113">Если один или несколько измерений массива имеют нулевую длину, массив считается пустым.</span><span class="sxs-lookup"><span data-stu-id="1d824-113">If one or more of the dimensions of an array have a length of zero, the array is said to be empty.</span></span>

<span data-ttu-id="1d824-114">Элементы массива могут иметь любой тип, в том числе тип массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-114">The element type of an array can be any type, including an array type.</span></span>

## <a name="array-types"></a><span data-ttu-id="1d824-115">Типы массивов</span><span class="sxs-lookup"><span data-stu-id="1d824-115">Array types</span></span>

<span data-ttu-id="1d824-116">Тип массива записывается как *non_array_type* следуют одна или несколько *rank_specifier*s:</span><span class="sxs-lookup"><span data-stu-id="1d824-116">An array type is written as a *non_array_type* followed by one or more *rank_specifier*s:</span></span>

```antlr
array_type
    : non_array_type rank_specifier+
    ;

non_array_type
    : type
    ;

rank_specifier
    : '[' dim_separator* ']'
    ;

dim_separator
    : ','
    ;
```

<span data-ttu-id="1d824-117">Объект *non_array_type* любой *тип* это сам по себе не *array_type*.</span><span class="sxs-lookup"><span data-stu-id="1d824-117">A *non_array_type* is any *type* that is not itself an *array_type*.</span></span>

<span data-ttu-id="1d824-118">Ранг типа массива задается крайнее левое *rank_specifier* в *array_type*: Объект *rank_specifier* указывает, что массив является массивом с рангом 1 + число из "`,`" токены *rank_specifier*.</span><span class="sxs-lookup"><span data-stu-id="1d824-118">The rank of an array type is given by the leftmost *rank_specifier* in the *array_type*: A *rank_specifier* indicates that the array is an array with a rank of one plus the number of "`,`" tokens in the *rank_specifier*.</span></span>

<span data-ttu-id="1d824-119">Тип элемента типа массива является типом, полученный в результате удаления в крайней левой позиции *rank_specifier*:</span><span class="sxs-lookup"><span data-stu-id="1d824-119">The element type of an array type is the type that results from deleting the leftmost *rank_specifier*:</span></span>

*  <span data-ttu-id="1d824-120">Тип массива в форме `T[R]` является массивом с рангом `R` и является типом элемента, не являющимся массивом `T`.</span><span class="sxs-lookup"><span data-stu-id="1d824-120">An array type of the form `T[R]` is an array with rank `R` and a non-array element type `T`.</span></span>
*  <span data-ttu-id="1d824-121">Тип массива в форме `T[R][R1]...[Rn]` является массивом с рангом `R` и типа элемента `T[R1]...[Rn]`.</span><span class="sxs-lookup"><span data-stu-id="1d824-121">An array type of the form `T[R][R1]...[Rn]` is an array with rank `R` and an element type `T[R1]...[Rn]`.</span></span>

<span data-ttu-id="1d824-122">По сути *rank_specifier*s читаются слева направо, перед типом последним элементом вектора.</span><span class="sxs-lookup"><span data-stu-id="1d824-122">In effect, the *rank_specifier*s are read from left to right before the final non-array element type.</span></span> <span data-ttu-id="1d824-123">Тип `int[][,,][,]` представляет собой одномерный массив трехмерные массивы двумерных массивов `int`.</span><span class="sxs-lookup"><span data-stu-id="1d824-123">The type `int[][,,][,]` is a single-dimensional array of three-dimensional arrays of two-dimensional arrays of `int`.</span></span>

<span data-ttu-id="1d824-124">Во время выполнения, может быть значение типа массива `null` или ссылка на экземпляр такого типа массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-124">At run-time, a value of an array type can be `null` or a reference to an instance of that array type.</span></span>

### <a name="the-systemarray-type"></a><span data-ttu-id="1d824-125">Типа System.Array</span><span class="sxs-lookup"><span data-stu-id="1d824-125">The System.Array type</span></span>

<span data-ttu-id="1d824-126">Тип `System.Array` является абстрактным базовым типом для всех этих типов.</span><span class="sxs-lookup"><span data-stu-id="1d824-126">The type `System.Array` is the abstract base type of all array types.</span></span> <span data-ttu-id="1d824-127">И неявное ссылочное преобразование ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)) из любого типа массива для `System.Array`и преобразования явной ссылки ([явные преобразования ссылочных типов](conversions.md#explicit-reference-conversions)) существует из `System.Array` для любого типа массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-127">An implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from any array type to `System.Array`, and an explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) exists from `System.Array` to any array type.</span></span> <span data-ttu-id="1d824-128">Обратите внимание, что `System.Array` сам не *array_type*.</span><span class="sxs-lookup"><span data-stu-id="1d824-128">Note that `System.Array` is not itself an *array_type*.</span></span> <span data-ttu-id="1d824-129">Кроме того, это *class_type* из которой все *array_type*s являются производными.</span><span class="sxs-lookup"><span data-stu-id="1d824-129">Rather, it is a *class_type* from which all *array_type*s are derived.</span></span>

<span data-ttu-id="1d824-130">Во время выполнения, значение типа `System.Array` может быть `null` или ссылка на экземпляр любого типа массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-130">At run-time, a value of type `System.Array` can be `null` or a reference to an instance of any array type.</span></span>

### <a name="arrays-and-the-generic-ilist-interface"></a><span data-ttu-id="1d824-131">Массивы и универсальный интерфейс IList</span><span class="sxs-lookup"><span data-stu-id="1d824-131">Arrays and the generic IList interface</span></span>

<span data-ttu-id="1d824-132">Одномерный массив `T[]` реализует интерфейс `System.Collections.Generic.IList<T>` (`IList<T>` для краткости) и его базовых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="1d824-132">A one-dimensional array `T[]` implements the interface `System.Collections.Generic.IList<T>` (`IList<T>` for short) and its base interfaces.</span></span> <span data-ttu-id="1d824-133">Соответственно, отсутствует неявное преобразование из `T[]` для `IList<T>` и его базовых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="1d824-133">Accordingly, there is an implicit conversion from `T[]` to `IList<T>` and its base interfaces.</span></span> <span data-ttu-id="1d824-134">Кроме того, если имеется и неявное ссылочное преобразование из `S` для `T` затем `S[]` реализует `IList<T>` и нет и неявное ссылочное преобразование из `S[]` для `IList<T>` и его базовых интерфейсов () [Неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="1d824-134">In addition, if there is an implicit reference conversion from `S` to `T` then `S[]` implements `IList<T>` and there is an implicit reference conversion from `S[]` to `IList<T>` and its base interfaces ([Implicit reference conversions](conversions.md#implicit-reference-conversions)).</span></span> <span data-ttu-id="1d824-135">Если выполняется преобразование явной ссылки из `S` для `T` то существует неявное преобразование из `S[]` для `IList<T>` и его базовых интерфейсов ([преобразования явной ссылки](conversions.md#explicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="1d824-135">If there is an explicit reference conversion from `S` to `T` then there is an explicit reference conversion from `S[]` to `IList<T>` and its base interfaces ([Explicit reference conversions](conversions.md#explicit-reference-conversions)).</span></span> <span data-ttu-id="1d824-136">Пример:</span><span class="sxs-lookup"><span data-stu-id="1d824-136">For example:</span></span>
```csharp
using System.Collections.Generic;

class Test
{
    static void Main() {
        string[] sa = new string[5];
        object[] oa1 = new object[5];
        object[] oa2 = sa;

        IList<string> lst1 = sa;                    // Ok
        IList<string> lst2 = oa1;                   // Error, cast needed
        IList<object> lst3 = sa;                    // Ok
        IList<object> lst4 = oa1;                   // Ok

        IList<string> lst5 = (IList<string>)oa1;    // Exception
        IList<string> lst6 = (IList<string>)oa2;    // Ok
    }
}
```

<span data-ttu-id="1d824-137">Назначение `lst2 = oa1` приводит к ошибке времени компиляции с момента преобразование из `object[]` для `IList<string>` является явным преобразованием, не неявное.</span><span class="sxs-lookup"><span data-stu-id="1d824-137">The assignment `lst2 = oa1` generates a compile-time error since the conversion from `object[]` to `IList<string>` is an explicit conversion, not implicit.</span></span> <span data-ttu-id="1d824-138">Приведение `(IList<string>)oa1` вызовет исключение во время выполнения с момента `oa1` ссылки `object[]` и не `string[]`.</span><span class="sxs-lookup"><span data-stu-id="1d824-138">The cast `(IList<string>)oa1` will cause an exception to be thrown at run-time since `oa1` references an `object[]` and not a `string[]`.</span></span> <span data-ttu-id="1d824-139">Однако приведение `(IList<string>)oa2` не вызывает исключение, поскольку у `oa2` ссылки `string[]`.</span><span class="sxs-lookup"><span data-stu-id="1d824-139">However the cast `(IList<string>)oa2` will not cause an exception to be thrown since `oa2` references a `string[]`.</span></span>

<span data-ttu-id="1d824-140">Каждый раз, когда выполняется преобразование ссылку, явного или неявного из `S[]` для `IList<T>`, имеется также неявное преобразование из `IList<T>` и его базовых интерфейсов для `S[]` ([явной ссылки преобразования](conversions.md#explicit-reference-conversions)).</span><span class="sxs-lookup"><span data-stu-id="1d824-140">Whenever there is an implicit or explicit reference conversion from `S[]` to `IList<T>`, there is also an explicit reference conversion from `IList<T>` and its base interfaces to `S[]` ([Explicit reference conversions](conversions.md#explicit-reference-conversions)).</span></span>

<span data-ttu-id="1d824-141">Если в типе массива `S[]` реализует `IList<T>`, некоторые из членов реализованного интерфейса могут вызывать исключения.</span><span class="sxs-lookup"><span data-stu-id="1d824-141">When an array type `S[]` implements `IList<T>`, some of the members of the implemented interface may throw exceptions.</span></span> <span data-ttu-id="1d824-142">Точное поведение реализации интерфейса выходит за рамки этой спецификации.</span><span class="sxs-lookup"><span data-stu-id="1d824-142">The precise behavior of the implementation of the interface is beyond the scope of this specification.</span></span>

## <a name="array-creation"></a><span data-ttu-id="1d824-143">Создание массива</span><span class="sxs-lookup"><span data-stu-id="1d824-143">Array creation</span></span>

<span data-ttu-id="1d824-144">Экземпляры массива создаются с *array_creation_expression*s ([выражениях создания массива](expressions.md#array-creation-expressions)), поле или объявления локальных переменных, которые включают *array_initializer*([Инициализаторы массивов](arrays.md#array-initializers)).</span><span class="sxs-lookup"><span data-stu-id="1d824-144">Array instances are created by *array_creation_expression*s ([Array creation expressions](expressions.md#array-creation-expressions)) or by field or local variable declarations that include an *array_initializer* ([Array initializers](arrays.md#array-initializers)).</span></span>

<span data-ttu-id="1d824-145">Когда создается экземпляр массива, ранг и длина каждого из измерений, устанавливаются и остаются неизменными в течение всего времени жизни экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1d824-145">When an array instance is created, the rank and length of each dimension are established and then remain constant for the entire lifetime of the instance.</span></span> <span data-ttu-id="1d824-146">Другими словами невозможно изменить ранг массива, а также можно ли изменить размер его измерений.</span><span class="sxs-lookup"><span data-stu-id="1d824-146">In other words, it is not possible to change the rank of an existing array instance, nor is it possible to resize its dimensions.</span></span>

<span data-ttu-id="1d824-147">Экземпляр массива всегда имеет тип массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-147">An array instance is always of an array type.</span></span> <span data-ttu-id="1d824-148">`System.Array` Тип является абстрактным типом, не может быть создан.</span><span class="sxs-lookup"><span data-stu-id="1d824-148">The `System.Array` type is an abstract type that cannot be instantiated.</span></span>

<span data-ttu-id="1d824-149">Элементы массивов, созданных *array_creation_expression*s всегда инициализируются значениями по умолчанию ([значения по умолчанию](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="1d824-149">Elements of arrays created by *array_creation_expression*s are always initialized to their default value ([Default values](variables.md#default-values)).</span></span>

## <a name="array-element-access"></a><span data-ttu-id="1d824-150">Доступ к элементам массива</span><span class="sxs-lookup"><span data-stu-id="1d824-150">Array element access</span></span>

<span data-ttu-id="1d824-151">Элементы массива осуществляется с помощью *element_access* выражения ([массива доступа](expressions.md#array-access)) формы `A[I1, I2, ..., In]`, где `A` представляет собой выражение из типа массива и каждый `Ix` — Выражение типа `int`, `uint`, `long`, `ulong`, или может быть неявно преобразован в один или несколько из этих типов.</span><span class="sxs-lookup"><span data-stu-id="1d824-151">Array elements are accessed using *element_access* expressions ([Array access](expressions.md#array-access)) of the form `A[I1, I2, ..., In]`, where `A` is an expression of an array type and each `Ix` is an expression of type `int`, `uint`, `long`, `ulong`, or can be implicitly converted to one or more of these types.</span></span> <span data-ttu-id="1d824-152">Доступ к элементам массива образом переменной, а именно элемент массива, выбранный по индексу.</span><span class="sxs-lookup"><span data-stu-id="1d824-152">The result of an array element access is a variable, namely the array element selected by the indices.</span></span>

<span data-ttu-id="1d824-153">Элементы массива могут быть перечислены с помощью `foreach` инструкции ([оператор foreach](statements.md#the-foreach-statement)).</span><span class="sxs-lookup"><span data-stu-id="1d824-153">The elements of an array can be enumerated using a `foreach` statement ([The foreach statement](statements.md#the-foreach-statement)).</span></span>

## <a name="array-members"></a><span data-ttu-id="1d824-154">Члены массива</span><span class="sxs-lookup"><span data-stu-id="1d824-154">Array members</span></span>

<span data-ttu-id="1d824-155">Каждый тип массива наследует члены, объявленные `System.Array` типа.</span><span class="sxs-lookup"><span data-stu-id="1d824-155">Every array type inherits the members declared by the `System.Array` type.</span></span>

## <a name="array-covariance"></a><span data-ttu-id="1d824-156">Ковариация массивов</span><span class="sxs-lookup"><span data-stu-id="1d824-156">Array covariance</span></span>

<span data-ttu-id="1d824-157">Для любой двух *reference_type*s `A` и `B`, если и неявное ссылочное преобразование ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)) или явное преобразование ссылок ([ Явные преобразования ссылочных типов](conversions.md#explicit-reference-conversions)) существует `A` для `B`, то же преобразование ссылок из типа массива также существует `A[R]` в тип массива `B[R]`, где `R` любой заданный *rank_specifier* (но одинаковым для обоих типы массивов).</span><span class="sxs-lookup"><span data-stu-id="1d824-157">For any two *reference_type*s `A` and `B`, if an implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) or explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) exists from `A` to `B`, then the same reference conversion also exists from the array type `A[R]` to the array type `B[R]`, where `R` is any given *rank_specifier* (but the same for both array types).</span></span> <span data-ttu-id="1d824-158">Эта связь называется ***ковариацией***.</span><span class="sxs-lookup"><span data-stu-id="1d824-158">This relationship is known as ***array covariance***.</span></span> <span data-ttu-id="1d824-159">Ковариация массивов в частности означает, что значение типа массива `A[R]` фактически может представлять собой ссылку на экземпляр типа массива `B[R]`, если существует неявное преобразование ссылок из `B` для `A`.</span><span class="sxs-lookup"><span data-stu-id="1d824-159">Array covariance in particular means that a value of an array type `A[R]` may actually be a reference to an instance of an array type `B[R]`, provided an implicit reference conversion exists from `B` to `A`.</span></span>

<span data-ttu-id="1d824-160">Из-за ковариантность массивов, присваивание к элементам массива ссылочного типа включает проверку во время выполнения, что гарантирует, что значение, назначаемое элементу массива фактически разрешенный тип ([простое присваивание](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="1d824-160">Because of array covariance, assignments to elements of reference type arrays include a run-time check which ensures that the value being assigned to the array element is actually of a permitted type ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="1d824-161">Пример:</span><span class="sxs-lookup"><span data-stu-id="1d824-161">For example:</span></span>
```csharp
class Test
{
    static void Fill(object[] array, int index, int count, object value) {
        for (int i = index; i < index + count; i++) array[i] = value;
    }

    static void Main() {
        string[] strings = new string[100];
        Fill(strings, 0, 100, "Undefined");
        Fill(strings, 0, 10, null);
        Fill(strings, 90, 10, 0);
    }
}
```

<span data-ttu-id="1d824-162">Назначение `array[i]` в `Fill` метод неявно включает в себя проверку во время выполнения, который гарантирует, что объект, упоминаемый в `value` либо `null` или экземпляр, который совместим с фактическим типом элемента `array`.</span><span class="sxs-lookup"><span data-stu-id="1d824-162">The assignment to `array[i]` in the `Fill` method implicitly includes a run-time check which ensures that the object referenced by `value` is either `null` or an instance that is compatible with the actual element type of `array`.</span></span> <span data-ttu-id="1d824-163">В `Main`, первые два вызова `Fill` выполниться успешно, но третий причины вызова `System.ArrayTypeMismatchException` исключение при выполнении первое присваивание `array[i]`.</span><span class="sxs-lookup"><span data-stu-id="1d824-163">In `Main`, the first two invocations of `Fill` succeed, but the third invocation causes a `System.ArrayTypeMismatchException` to be thrown upon executing the first assignment to `array[i]`.</span></span> <span data-ttu-id="1d824-164">Исключение возникает, так как упакованное `int` не могут храниться в `string` массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-164">The exception occurs because a boxed `int` cannot be stored in a `string` array.</span></span>

<span data-ttu-id="1d824-165">Ковариация массивов специально не распространяется на массивы *value_type*s.</span><span class="sxs-lookup"><span data-stu-id="1d824-165">Array covariance specifically does not extend to arrays of *value_type*s.</span></span> <span data-ttu-id="1d824-166">Например, не существует преобразования, подходящее `int[]` будет считаться `object[]`.</span><span class="sxs-lookup"><span data-stu-id="1d824-166">For example, no conversion exists that permits an `int[]` to be treated as an `object[]`.</span></span>

## <a name="array-initializers"></a><span data-ttu-id="1d824-167">Инициализаторы массивов</span><span class="sxs-lookup"><span data-stu-id="1d824-167">Array initializers</span></span>

<span data-ttu-id="1d824-168">Инициализаторы массивов могут быть указаны в объявления поля ([поля](classes.md#fields)), объявлений локальных переменных ([объявления локальных переменных](statements.md#local-variable-declarations)) и выражения создания массива ([создания массива выражения](expressions.md#array-creation-expressions)):</span><span class="sxs-lookup"><span data-stu-id="1d824-168">Array initializers may be specified in field declarations ([Fields](classes.md#fields)), local variable declarations ([Local variable declarations](statements.md#local-variable-declarations)), and array creation expressions ([Array creation expressions](expressions.md#array-creation-expressions)):</span></span>

```antlr
array_initializer
    : '{' variable_initializer_list? '}'
    | '{' variable_initializer_list ',' '}'
    ;

variable_initializer_list
    : variable_initializer (',' variable_initializer)*
    ;

variable_initializer
    : expression
    | array_initializer
    ;
```

<span data-ttu-id="1d824-169">Инициализатор массива состоит из последовательности переменных инициализаторов, заключенных между "`{`«и»`}`«маркеров и разделенных»`,`" маркеров.</span><span class="sxs-lookup"><span data-stu-id="1d824-169">An array initializer consists of a sequence of variable initializers, enclosed by "`{`" and "`}`" tokens and separated by "`,`" tokens.</span></span> <span data-ttu-id="1d824-170">Каждый инициализатор переменной представляет собой выражение или, в случае многомерного массива, инициализатор вложенного массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-170">Each variable initializer is an expression or, in the case of a multi-dimensional array, a nested array initializer.</span></span>

<span data-ttu-id="1d824-171">Контекст, в котором используется инициализатор массива определяет тип инициализируемого массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-171">The context in which an array initializer is used determines the type of the array being initialized.</span></span> <span data-ttu-id="1d824-172">В выражение создания массива тип массива непосредственно предшествует инициализатору или выводится из выражения в инициализаторе массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-172">In an array creation expression, the array type immediately precedes the initializer, or is inferred from the expressions in the array initializer.</span></span> <span data-ttu-id="1d824-173">В поле или объявление переменной тип массива — тип поля или объявляемой переменной.</span><span class="sxs-lookup"><span data-stu-id="1d824-173">In a field or variable declaration, the array type is the type of the field or variable being declared.</span></span> <span data-ttu-id="1d824-174">Когда инициализатор массива используется в поле или объявления переменной, такие как:</span><span class="sxs-lookup"><span data-stu-id="1d824-174">When an array initializer is used in a field or variable declaration, such as:</span></span>
```csharp
int[] a = {0, 2, 4, 6, 8};
```
<span data-ttu-id="1d824-175">Это просто сокращением для соответствующего выражения создания массива:</span><span class="sxs-lookup"><span data-stu-id="1d824-175">it is simply shorthand for an equivalent array creation expression:</span></span>
```csharp
int[] a = new int[] {0, 2, 4, 6, 8};
```

<span data-ttu-id="1d824-176">Одномерный массив инициализатор массива должны состоять из последовательности выражений, совместимого с типом элемента массива назначения.</span><span class="sxs-lookup"><span data-stu-id="1d824-176">For a single-dimensional array, the array initializer must consist of a sequence of expressions that are assignment compatible with the element type of the array.</span></span> <span data-ttu-id="1d824-177">Выражения инициализации элементов массива в порядке по возрастанию, начиная с элемента с нулевым индексом.</span><span class="sxs-lookup"><span data-stu-id="1d824-177">The expressions initialize array elements in increasing order, starting with the element at index zero.</span></span> <span data-ttu-id="1d824-178">Количество выражений в инициализаторе массива определяет длину массива экземпляра.</span><span class="sxs-lookup"><span data-stu-id="1d824-178">The number of expressions in the array initializer determines the length of the array instance being created.</span></span> <span data-ttu-id="1d824-179">Например, приведенный выше инициализатор массива создает `int[]` экземпляр длиной 5 и инициализирует экземпляр со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="1d824-179">For example, the array initializer above creates an `int[]` instance of length 5 and then initializes the instance with the following values:</span></span>
```csharp
a[0] = 0; a[1] = 2; a[2] = 4; a[3] = 6; a[4] = 8;
```

<span data-ttu-id="1d824-180">Многомерный массив инициализатор массива должен иметь столько уровней вложенности, сколько измерений в массиве.</span><span class="sxs-lookup"><span data-stu-id="1d824-180">For a multi-dimensional array, the array initializer must have as many levels of nesting as there are dimensions in the array.</span></span> <span data-ttu-id="1d824-181">Правой размерности верхнего уровня вложенности соответствует левой размерности а внутреннего уровня вложения.</span><span class="sxs-lookup"><span data-stu-id="1d824-181">The outermost nesting level corresponds to the leftmost dimension and the innermost nesting level corresponds to the rightmost dimension.</span></span> <span data-ttu-id="1d824-182">Длина каждого измерения массива определяется количество элементов на соответствующем уровне вложенности в инициализаторе массива.</span><span class="sxs-lookup"><span data-stu-id="1d824-182">The length of each dimension of the array is determined by the number of elements at the corresponding nesting level in the array initializer.</span></span> <span data-ttu-id="1d824-183">Каждый инициализатор вложенного массива номер элементов должен быть таким же, как другие Инициализаторы массивов того же уровня.</span><span class="sxs-lookup"><span data-stu-id="1d824-183">For each nested array initializer, the number of elements must be the same as the other array initializers at the same level.</span></span> <span data-ttu-id="1d824-184">Пример:</span><span class="sxs-lookup"><span data-stu-id="1d824-184">The example:</span></span>
```csharp
int[,] b = {{0, 1}, {2, 3}, {4, 5}, {6, 7}, {8, 9}};
```
<span data-ttu-id="1d824-185">создает двумерный массив с длиной пять для левого измерения и длину, равную 2 для правого измерения:</span><span class="sxs-lookup"><span data-stu-id="1d824-185">creates a two-dimensional array with a length of five for the leftmost dimension and a length of two for the rightmost dimension:</span></span>
```csharp
int[,] b = new int[5, 2];
```
<span data-ttu-id="1d824-186">и затем инициализирует экземпляр массива со следующими значениями:</span><span class="sxs-lookup"><span data-stu-id="1d824-186">and then initializes the array instance with the following values:</span></span>
```csharp
b[0, 0] = 0; b[0, 1] = 1;
b[1, 0] = 2; b[1, 1] = 3;
b[2, 0] = 4; b[2, 1] = 5;
b[3, 0] = 6; b[3, 1] = 7;
b[4, 0] = 8; b[4, 1] = 9;
```

<span data-ttu-id="1d824-187">Если измерения, отличного от самым правым имеет нулевую длину, последующие измерения предполагается, что также имеет нулевую длину.</span><span class="sxs-lookup"><span data-stu-id="1d824-187">If a dimension other than the rightmost is given with length zero, the subsequent dimensions are assumed to also have length zero.</span></span> <span data-ttu-id="1d824-188">Пример:</span><span class="sxs-lookup"><span data-stu-id="1d824-188">The example:</span></span>
```csharp
int[,] c = {};
```
<span data-ttu-id="1d824-189">создает двумерный массив с длиной ноль для левого и правого измерения:</span><span class="sxs-lookup"><span data-stu-id="1d824-189">creates a two-dimensional array with a length of zero for both the leftmost and the rightmost dimension:</span></span>
```csharp
int[,] c = new int[0, 0];
```

<span data-ttu-id="1d824-190">Если выражение создания массива включает явное длины по измерениям и инициализатора массива, длины должны быть константными выражениями, и количество элементов на каждом уровне вложенности должно совпадать с длиной соответствующего измерения.</span><span class="sxs-lookup"><span data-stu-id="1d824-190">When an array creation expression includes both explicit dimension lengths and an array initializer, the lengths must be constant expressions and the number of elements at each nesting level must match the corresponding dimension length.</span></span> <span data-ttu-id="1d824-191">Далее приводятся некоторые примеры.</span><span class="sxs-lookup"><span data-stu-id="1d824-191">Here are some examples:</span></span>
```csharp
int i = 3;
int[] x = new int[3] {0, 1, 2};        // OK
int[] y = new int[i] {0, 1, 2};        // Error, i not a constant
int[] z = new int[3] {0, 1, 2, 3};     // Error, length/initializer mismatch
```

<span data-ttu-id="1d824-192">Здесь инициализатор для `y` приводит к ошибке времени компиляции, так как выражение длины массива не является константой и инициализатор `z` приводит к ошибке времени компиляции, так как длина и количество элементов в Инициализатор не согласны.</span><span class="sxs-lookup"><span data-stu-id="1d824-192">Here, the initializer for `y` results in a compile-time error because the dimension length expression is not a constant, and the initializer for `z` results in a compile-time error because the length and the number of elements in the initializer do not agree.</span></span>
