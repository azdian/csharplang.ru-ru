# <a name="variables"></a><span data-ttu-id="b645a-101">Переменные</span><span class="sxs-lookup"><span data-stu-id="b645a-101">Variables</span></span>

<span data-ttu-id="b645a-102">Переменные представляют места хранения.</span><span class="sxs-lookup"><span data-stu-id="b645a-102">Variables represent storage locations.</span></span> <span data-ttu-id="b645a-103">Каждая переменная имеет тип, который определяет значения, которые могут быть сохранены в переменной.</span><span class="sxs-lookup"><span data-stu-id="b645a-103">Every variable has a type that determines what values can be stored in the variable.</span></span> <span data-ttu-id="b645a-104">C# — это строго типизированный язык и компилятор C# гарантирует, что значения, хранящиеся в переменных, всегда будут соответствующего типа.</span><span class="sxs-lookup"><span data-stu-id="b645a-104">C# is a type-safe language, and the C# compiler guarantees that values stored in variables are always of the appropriate type.</span></span> <span data-ttu-id="b645a-105">Значение переменной можно изменить путем назначения или с помощью `++` и `--` операторы.</span><span class="sxs-lookup"><span data-stu-id="b645a-105">The value of a variable can be changed through assignment or through use of the `++` and `--` operators.</span></span>

<span data-ttu-id="b645a-106">Переменная должна быть ***определенно присвоенной*** ([определенного присваивания](variables.md#definite-assignment)) перед его значение можно получить.</span><span class="sxs-lookup"><span data-stu-id="b645a-106">A variable must be ***definitely assigned*** ([Definite assignment](variables.md#definite-assignment)) before its value can be obtained.</span></span>

<span data-ttu-id="b645a-107">Как описано в следующих разделах, переменные, либо ***начальным значением*** или ***изначально не присвоены значения***.</span><span class="sxs-lookup"><span data-stu-id="b645a-107">As described in the following sections, variables are either ***initially assigned*** or ***initially unassigned***.</span></span> <span data-ttu-id="b645a-108">Переменная с начальным значением имеет четко определенные начальное значение и всегда считается определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="b645a-108">An initially assigned variable has a well-defined initial value and is always considered definitely assigned.</span></span> <span data-ttu-id="b645a-109">У переменной без начального значения.</span><span class="sxs-lookup"><span data-stu-id="b645a-109">An initially unassigned variable has no initial value.</span></span> <span data-ttu-id="b645a-110">Для переменной считается определенно присвоенной в конкретном месте присвоения значения переменной должно находиться в каждом возможном пути исполнения приведет к этому расположению.</span><span class="sxs-lookup"><span data-stu-id="b645a-110">For an initially unassigned variable to be considered definitely assigned at a certain location, an assignment to the variable must occur in every possible execution path leading to that location.</span></span>

## <a name="variable-categories"></a><span data-ttu-id="b645a-111">Категории переменных</span><span class="sxs-lookup"><span data-stu-id="b645a-111">Variable categories</span></span>

<span data-ttu-id="b645a-112">C# определяет семь категорий переменных: статические переменные, переменные экземпляра, элементы массива, параметры значений, ссылочные параметры, выходные параметры и локальные переменные.</span><span class="sxs-lookup"><span data-stu-id="b645a-112">C# defines seven categories of variables: static variables, instance variables, array elements, value parameters, reference parameters, output parameters, and local variables.</span></span> <span data-ttu-id="b645a-113">В последующих разделах описан каждый из этих категорий.</span><span class="sxs-lookup"><span data-stu-id="b645a-113">The sections that follow describe each of these categories.</span></span>

<span data-ttu-id="b645a-114">В примере</span><span class="sxs-lookup"><span data-stu-id="b645a-114">In the example</span></span>
```csharp
class A
{
    public static int x;
    int y;

    void F(int[] v, int a, ref int b, out int c) {
        int i = 1;
        c = a + b++;
    }
}
```
<span data-ttu-id="b645a-115">`x` Статическая переменная, `y` является переменной экземпляра `v[0]` является элементом массива `a` является значение параметра, `b` — это ссылочный параметр, `c` является параметром output и `i` является локальной переменной.</span><span class="sxs-lookup"><span data-stu-id="b645a-115">`x` is a static variable, `y` is an instance variable, `v[0]` is an array element, `a` is a value parameter, `b` is a reference parameter, `c` is an output parameter, and `i` is a local variable.</span></span>

### <a name="static-variables"></a><span data-ttu-id="b645a-116">Статические переменные</span><span class="sxs-lookup"><span data-stu-id="b645a-116">Static variables</span></span>

<span data-ttu-id="b645a-117">Поле объявлено с `static` модификатор называется ***статической переменной***.</span><span class="sxs-lookup"><span data-stu-id="b645a-117">A field declared with the `static` modifier is called a ***static variable***.</span></span> <span data-ttu-id="b645a-118">Статическая переменная появляется перед выполнением статического конструктора ([статические конструкторы](classes.md#static-constructors)) для его содержащего типа и создается в соответствующем домене приложения перестает существовать.</span><span class="sxs-lookup"><span data-stu-id="b645a-118">A static variable comes into existence before execution of the static constructor ([Static constructors](classes.md#static-constructors)) for its containing type, and ceases to exist when the associated application domain ceases to exist.</span></span>

<span data-ttu-id="b645a-119">Начальное значение статической переменной является значением по умолчанию ([значения по умолчанию](variables.md#default-values)) типа переменной.</span><span class="sxs-lookup"><span data-stu-id="b645a-119">The initial value of a static variable is the default value ([Default values](variables.md#default-values)) of the variable's type.</span></span>

<span data-ttu-id="b645a-120">В целях проверки определенного присваивания статическая переменная считается начальным значением.</span><span class="sxs-lookup"><span data-stu-id="b645a-120">For purposes of definite assignment checking, a static variable is considered initially assigned.</span></span>

### <a name="instance-variables"></a><span data-ttu-id="b645a-121">Переменные экземпляра</span><span class="sxs-lookup"><span data-stu-id="b645a-121">Instance variables</span></span>

<span data-ttu-id="b645a-122">Поле объявлено без `static` модификатор называется ***переменная экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="b645a-122">A field declared without the `static` modifier is called an ***instance variable***.</span></span>

#### <a name="instance-variables-in-classes"></a><span data-ttu-id="b645a-123">Переменные экземпляра в классах</span><span class="sxs-lookup"><span data-stu-id="b645a-123">Instance variables in classes</span></span>

<span data-ttu-id="b645a-124">Переменная экземпляра класса появляется, когда создается новый экземпляр этого класса и перестает существовать при отсутствии ссылок на этот экземпляр и выполнен деструктор экземпляра (если таковые имеются).</span><span class="sxs-lookup"><span data-stu-id="b645a-124">An instance variable of a class comes into existence when a new instance of that class is created, and ceases to exist when there are no references to that instance and the instance's destructor (if any) has executed.</span></span>

<span data-ttu-id="b645a-125">Начальное значение переменной экземпляра класса является значением по умолчанию ([значения по умолчанию](variables.md#default-values)) типа переменной.</span><span class="sxs-lookup"><span data-stu-id="b645a-125">The initial value of an instance variable of a class is the default value ([Default values](variables.md#default-values)) of the variable's type.</span></span>

<span data-ttu-id="b645a-126">Для целей проверки определенного присваивания переменной экземпляра класса считается начальным значением.</span><span class="sxs-lookup"><span data-stu-id="b645a-126">For the purpose of definite assignment checking, an instance variable of a class is considered initially assigned.</span></span>

#### <a name="instance-variables-in-structs"></a><span data-ttu-id="b645a-127">Переменные экземпляра в структурах</span><span class="sxs-lookup"><span data-stu-id="b645a-127">Instance variables in structs</span></span>

<span data-ttu-id="b645a-128">Переменная экземпляра структуры имеет такое же время жизни, как переменную структуры, к которой он принадлежит.</span><span class="sxs-lookup"><span data-stu-id="b645a-128">An instance variable of a struct has exactly the same lifetime as the struct variable to which it belongs.</span></span> <span data-ttu-id="b645a-129">Другими словами, когда переменную с типом структуры создается или прекращает свое существование, поэтому слишком у переменных экземпляра структуры.</span><span class="sxs-lookup"><span data-stu-id="b645a-129">In other words, when a variable of a struct type comes into existence or ceases to exist, so too do the instance variables of the struct.</span></span>

<span data-ttu-id="b645a-130">Состояние первоначального назначения переменной экземпляра структуры совпадает, содержащего переменной структуры.</span><span class="sxs-lookup"><span data-stu-id="b645a-130">The initial assignment state of an instance variable of a struct is the same as that of the containing struct variable.</span></span> <span data-ttu-id="b645a-131">Другими словами, когда переменная структуры имеющей, поэтому слишком переменные экземпляров, а когда переменная структуры, считается изначально не присвоены значения, переменные экземпляров — аналогично неназначенные.</span><span class="sxs-lookup"><span data-stu-id="b645a-131">In other words, when a struct variable is considered initially assigned, so too are its instance variables, and when a struct variable is considered initially unassigned, its instance variables are likewise unassigned.</span></span>

### <a name="array-elements"></a><span data-ttu-id="b645a-132">Элементы массива</span><span class="sxs-lookup"><span data-stu-id="b645a-132">Array elements</span></span>

<span data-ttu-id="b645a-133">Элементы массива появляются при создании экземпляра массива и исчезают при отсутствии ссылок на этот экземпляр массива.</span><span class="sxs-lookup"><span data-stu-id="b645a-133">The elements of an array come into existence when an array instance is created, and cease to exist when there are no references to that array instance.</span></span>

<span data-ttu-id="b645a-134">Начальное значение каждого из элементов массива является значением по умолчанию ([значения по умолчанию](variables.md#default-values)) типа элементов массива.</span><span class="sxs-lookup"><span data-stu-id="b645a-134">The initial value of each of the elements of an array is the default value ([Default values](variables.md#default-values)) of the type of the array elements.</span></span>

<span data-ttu-id="b645a-135">Для целей проверки определенного присваивания элемент массива считается начальным значением.</span><span class="sxs-lookup"><span data-stu-id="b645a-135">For the purpose of definite assignment checking, an array element is considered initially assigned.</span></span>

### <a name="value-parameters"></a><span data-ttu-id="b645a-136">Параметры значения</span><span class="sxs-lookup"><span data-stu-id="b645a-136">Value parameters</span></span>

<span data-ttu-id="b645a-137">Параметр, объявленный без `ref` или `out` модификатор ***значение параметра***.</span><span class="sxs-lookup"><span data-stu-id="b645a-137">A parameter declared without a `ref` or `out` modifier is a ***value parameter***.</span></span>

<span data-ttu-id="b645a-138">Значение параметра поступает при вызове функции-члена (метод, конструктор экземпляра, метод доступа или оператора) или анонимной функции которой параметр принадлежит и инициализируется со значением аргумента, указанного в вызове.</span><span class="sxs-lookup"><span data-stu-id="b645a-138">A value parameter comes into existence upon invocation of the function member (method, instance constructor, accessor, or operator) or anonymous function to which the parameter belongs, and is initialized with the value of the argument given in the invocation.</span></span> <span data-ttu-id="b645a-139">Значение параметра обычно перестает существовать при возврате из функции-члена или анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="b645a-139">A value parameter normally ceases to exist upon return of the function member or anonymous function.</span></span> <span data-ttu-id="b645a-140">Тем не менее если значение параметра записанным анонимная функция ([выражения анонимных функций](expressions.md#anonymous-function-expressions)), его время жизни увеличивается по крайней мере до делегат или дерево выражения, созданного из этого анонимная функция подходит для сборка мусора.</span><span class="sxs-lookup"><span data-stu-id="b645a-140">However, if the value parameter is captured by an anonymous function ([Anonymous function expressions](expressions.md#anonymous-function-expressions)), its life time extends at least until the delegate or expression tree created from that anonymous function is eligible for garbage collection.</span></span>

<span data-ttu-id="b645a-141">Для целей проверки определенного присваивания параметр значение считается начальным значением.</span><span class="sxs-lookup"><span data-stu-id="b645a-141">For the purpose of definite assignment checking, a value parameter is considered initially assigned.</span></span>

### <a name="reference-parameters"></a><span data-ttu-id="b645a-142">Параметры ссылок</span><span class="sxs-lookup"><span data-stu-id="b645a-142">Reference parameters</span></span>

<span data-ttu-id="b645a-143">Параметр, объявленный с `ref` модификатор ***ссылочный параметр***.</span><span class="sxs-lookup"><span data-stu-id="b645a-143">A parameter declared with a `ref` modifier is a ***reference parameter***.</span></span>

<span data-ttu-id="b645a-144">Ссылочный параметр не создает новое место хранения.</span><span class="sxs-lookup"><span data-stu-id="b645a-144">A reference parameter does not create a new storage location.</span></span> <span data-ttu-id="b645a-145">Вместо этого параметр ссылки представляет место хранения переменной, заданной в качестве аргумента в функцию-член или анонимной функции вызова.</span><span class="sxs-lookup"><span data-stu-id="b645a-145">Instead, a reference parameter represents the same storage location as the variable given as the argument in the function member or anonymous function invocation.</span></span> <span data-ttu-id="b645a-146">Таким образом значение параметра ссылки — это всегда совпадает с базовой переменной.</span><span class="sxs-lookup"><span data-stu-id="b645a-146">Thus, the value of a reference parameter is always the same as the underlying variable.</span></span>

<span data-ttu-id="b645a-147">Справочник по параметрам применяются следующие правила определенного назначения.</span><span class="sxs-lookup"><span data-stu-id="b645a-147">The following definite assignment rules apply to reference parameters.</span></span> <span data-ttu-id="b645a-148">Обратите внимание на разные правила для выходных параметров, описанных в [выходных параметров](variables.md#output-parameters).</span><span class="sxs-lookup"><span data-stu-id="b645a-148">Note the different rules for output parameters described in [Output parameters](variables.md#output-parameters).</span></span>

*  <span data-ttu-id="b645a-149">Переменной должен быть явно присвоен ([определенного присваивания](variables.md#definite-assignment)), прежде чем их можно было передать в качестве ссылочного параметра при вызове функции члена или делегата.</span><span class="sxs-lookup"><span data-stu-id="b645a-149">A variable must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) before it can be passed as a reference parameter in a function member or delegate invocation.</span></span>
*  <span data-ttu-id="b645a-150">Внутри функции-члена или анонимной функции считается начальным значением ссылочного параметра.</span><span class="sxs-lookup"><span data-stu-id="b645a-150">Within a function member or anonymous function, a reference parameter is considered initially assigned.</span></span>

<span data-ttu-id="b645a-151">Внутри метода экземпляра или методе доступа экземпляра типа структуры `this` ключевое слово ведет себя точно так, как ссылочный параметр типа структуры ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="b645a-151">Within an instance method or instance accessor of a struct type, the `this` keyword behaves exactly as a reference parameter of the struct type ([This access](expressions.md#this-access)).</span></span>

### <a name="output-parameters"></a><span data-ttu-id="b645a-152">Выходные параметры</span><span class="sxs-lookup"><span data-stu-id="b645a-152">Output parameters</span></span>

<span data-ttu-id="b645a-153">Параметр, объявленный с `out` модификатор ***выходной параметр***.</span><span class="sxs-lookup"><span data-stu-id="b645a-153">A parameter declared with an `out` modifier is an ***output parameter***.</span></span>

<span data-ttu-id="b645a-154">Выходной параметр не создает новое место хранения.</span><span class="sxs-lookup"><span data-stu-id="b645a-154">An output parameter does not create a new storage location.</span></span> <span data-ttu-id="b645a-155">Вместо этого выходного параметра представляет то же место хранения переменной, заданной в качестве аргумента при вызове функции-члена или делегата.</span><span class="sxs-lookup"><span data-stu-id="b645a-155">Instead, an output parameter represents the same storage location as the variable given as the argument in the function member or delegate invocation.</span></span> <span data-ttu-id="b645a-156">Таким образом значение выходного параметра является всегда совпадает с базовой переменной.</span><span class="sxs-lookup"><span data-stu-id="b645a-156">Thus, the value of an output parameter is always the same as the underlying variable.</span></span>

<span data-ttu-id="b645a-157">Применяются следующие правила определенного назначения для выходных параметров.</span><span class="sxs-lookup"><span data-stu-id="b645a-157">The following definite assignment rules apply to output parameters.</span></span> <span data-ttu-id="b645a-158">Обратите внимание на разные правила для выходных параметров, описанные в [ссылочные параметры](variables.md#reference-parameters).</span><span class="sxs-lookup"><span data-stu-id="b645a-158">Note the different rules for reference parameters described in [Reference parameters](variables.md#reference-parameters).</span></span>

*  <span data-ttu-id="b645a-159">Переменная не нужно назначать определенно могут передаваться в качестве выходного параметра в функции-члене или вызов делегата.</span><span class="sxs-lookup"><span data-stu-id="b645a-159">A variable need not be definitely assigned before it can be passed as an output parameter in a function member or delegate invocation.</span></span>
*  <span data-ttu-id="b645a-160">После нормального завершения вызова функции-члена или делегата каждой переменной, который был передан как выходной параметр считается назначить в этом пути выполнения.</span><span class="sxs-lookup"><span data-stu-id="b645a-160">Following the normal completion of a function member or delegate invocation, each variable that was passed as an output parameter is considered assigned in that execution path.</span></span>
*  <span data-ttu-id="b645a-161">Внутри функции-члена или анонимной функции считается изначально не присвоены значения выходного параметра.</span><span class="sxs-lookup"><span data-stu-id="b645a-161">Within a function member or anonymous function, an output parameter is considered initially unassigned.</span></span>
*  <span data-ttu-id="b645a-162">Каждый выходной параметр функции-члена или анонимной функции должен быть явно присвоен ([определенного присваивания](variables.md#definite-assignment)) перед функцией члена или анонимной функции завершается нормально.</span><span class="sxs-lookup"><span data-stu-id="b645a-162">Every output parameter of a function member or anonymous function must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) before the function member or anonymous function returns normally.</span></span>

<span data-ttu-id="b645a-163">Внутри конструктора экземпляра типа структуры `this` ключевое слово ведет себя точно так, как выходной параметр типа структуры ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="b645a-163">Within an instance constructor of a struct type, the `this` keyword behaves exactly as an output parameter of the struct type ([This access](expressions.md#this-access)).</span></span>

### <a name="local-variables"></a><span data-ttu-id="b645a-164">Локальные переменные</span><span class="sxs-lookup"><span data-stu-id="b645a-164">Local variables</span></span>

<span data-ttu-id="b645a-165">Объект ***локальной переменной*** объявляется с *local_variable_declaration*, который могут возникать в *блок*, *for_statement*, *switch_statement* или *using_statement*; или *foreach_statement* или *specific_catch_clause* для *try_statement*.</span><span class="sxs-lookup"><span data-stu-id="b645a-165">A ***local variable*** is declared by a *local_variable_declaration*, which may occur in a *block*, a *for_statement*, a *switch_statement* or a *using_statement*; or by a *foreach_statement* or a *specific_catch_clause* for a *try_statement*.</span></span>

<span data-ttu-id="b645a-166">Время существования локальной переменной — это часть во время которого хранилища гарантированно будет зарезервирован для его выполнения программы.</span><span class="sxs-lookup"><span data-stu-id="b645a-166">The lifetime of a local variable is the portion of program execution during which storage is guaranteed to be reserved for it.</span></span> <span data-ttu-id="b645a-167">Это время существования расширяет по крайней мере из записи в *блок*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, или *specific_catch_clause* с которым он связан, откладывается до времени выполнения, *блок*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, или *specific_catch_clause* окончания никак.</span><span class="sxs-lookup"><span data-stu-id="b645a-167">This lifetime extends at least from entry into the *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause* with which it is associated, until execution of that *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause* ends in any way.</span></span> <span data-ttu-id="b645a-168">(Ввод закрытой *блок* или вызов метода приостанавливается, но не завершает выполнение текущего *блок*, *for_statement*, *switch_statement* , *using_statement*, *foreach_statement*, или *specific_catch_clause*.) Если локальная переменная перехватывается анонимная функция ([захваченные внешние переменные](expressions.md#captured-outer-variables)), его времени существования расширяет по крайней мере до дерева, делегата или выражения, создаваемую из анонимной функции, а также другие объекты, ссылаться на захваченной переменной, подходящие для сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="b645a-168">(Entering an enclosed *block* or calling a method suspends, but does not end, execution of the current *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause*.) If the local variable is captured by an anonymous function ([Captured outer variables](expressions.md#captured-outer-variables)), its lifetime extends at least until the delegate or expression tree created from the anonymous function, along with any other objects that come to reference the captured variable, are eligible for garbage collection.</span></span>

<span data-ttu-id="b645a-169">Если родительский *блок*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, или *specific_catch_clause* вводится рекурсивно, новый экземпляр локальной переменной создается каждый раз и его *local_variable_initializer*, если имеется, вычисляется Каждый раз.</span><span class="sxs-lookup"><span data-stu-id="b645a-169">If the parent *block*, *for_statement*, *switch_statement*, *using_statement*, *foreach_statement*, or *specific_catch_clause* is entered recursively, a new instance of the local variable is created each time, and its *local_variable_initializer*, if any, is evaluated each time.</span></span>

<span data-ttu-id="b645a-170">Локальная переменная, созданная по *local_variable_declaration* автоматически не инициализирован, и поэтому имеет значение по умолчанию отсутствует.</span><span class="sxs-lookup"><span data-stu-id="b645a-170">A local variable introduced by a *local_variable_declaration* is not automatically initialized and thus has no default value.</span></span> <span data-ttu-id="b645a-171">Для целей проверки определенного присваивания локальной переменной представленные *local_variable_declaration* считается изначально не присвоены значения.</span><span class="sxs-lookup"><span data-stu-id="b645a-171">For the purpose of definite assignment checking, a local variable introduced by a *local_variable_declaration* is considered initially unassigned.</span></span> <span data-ttu-id="b645a-172">Объект *local_variable_declaration* может включать *local_variable_initializer*, в этом случае переменная считается определенно присвоенной только после инициализирующего выражения ([ Операторы объявления](variables.md#declaration-statements)).</span><span class="sxs-lookup"><span data-stu-id="b645a-172">A *local_variable_declaration* may include a *local_variable_initializer*, in which case the variable is considered definitely assigned only after the initializing expression ([Declaration statements](variables.md#declaration-statements)).</span></span>

<span data-ttu-id="b645a-173">В области действия локальной переменной, вызванные *local_variable_declaration*, произошла ошибка во время компиляции, для ссылки на эту локальную переменную в позиции текста, который предшествует его *local_variable_declarator*.</span><span class="sxs-lookup"><span data-stu-id="b645a-173">Within the scope of a local variable introduced by a *local_variable_declaration*, it is a compile-time error to refer to that local variable in a textual position that precedes its *local_variable_declarator*.</span></span> <span data-ttu-id="b645a-174">Если объявление локальной переменной является неявным ([объявления локальных переменных](statements.md#local-variable-declarations)), это также ошибка при ссылке на эту переменную в его *local_variable_declarator*.</span><span class="sxs-lookup"><span data-stu-id="b645a-174">If the local variable declaration is implicit ([Local variable declarations](statements.md#local-variable-declarations)), it is also an error to refer to the variable within its *local_variable_declarator*.</span></span>

<span data-ttu-id="b645a-175">Локальная переменная, созданная по *foreach_statement* или *specific_catch_clause* считается определенно присвоенной в пределах всей области видимости.</span><span class="sxs-lookup"><span data-stu-id="b645a-175">A local variable introduced by a *foreach_statement* or a *specific_catch_clause* is considered definitely assigned in its entire scope.</span></span>

<span data-ttu-id="b645a-176">Фактическое время жизни локальной переменной зависит от реализации.</span><span class="sxs-lookup"><span data-stu-id="b645a-176">The actual lifetime of a local variable is implementation-dependent.</span></span> <span data-ttu-id="b645a-177">К примеру, компилятор может статически определить, что локальной переменной в блоке используется только для небольших часть этого блока.</span><span class="sxs-lookup"><span data-stu-id="b645a-177">For example, a compiler might statically determine that a local variable in a block is only used for a small portion of that block.</span></span> <span data-ttu-id="b645a-178">С помощью этого анализа, компилятор может создать код, получаемый в места хранения переменной короче, чем время жизни содержащего его блока.</span><span class="sxs-lookup"><span data-stu-id="b645a-178">Using this analysis, the compiler could generate code that results in the variable's storage having a shorter lifetime than its containing block.</span></span>

<span data-ttu-id="b645a-179">Хранилище, на который ссылается локальная ссылочная переменная освобождается независимо от времени существования этого локальную ссылочную переменную ([автоматическое управление памятью](basic-concepts.md#automatic-memory-management)).</span><span class="sxs-lookup"><span data-stu-id="b645a-179">The storage referred to by a local reference variable is reclaimed independently of the lifetime of that local reference variable ([Automatic memory management](basic-concepts.md#automatic-memory-management)).</span></span>

## <a name="default-values"></a><span data-ttu-id="b645a-180">Значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="b645a-180">Default values</span></span>

<span data-ttu-id="b645a-181">Следующие категории переменных автоматически инициализируются значениями по умолчанию:</span><span class="sxs-lookup"><span data-stu-id="b645a-181">The following categories of variables are automatically initialized to their default values:</span></span>

*  <span data-ttu-id="b645a-182">Статические переменные.</span><span class="sxs-lookup"><span data-stu-id="b645a-182">Static variables.</span></span>
*  <span data-ttu-id="b645a-183">Переменные экземпляров класса экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b645a-183">Instance variables of class instances.</span></span>
*  <span data-ttu-id="b645a-184">Элементы массива.</span><span class="sxs-lookup"><span data-stu-id="b645a-184">Array elements.</span></span>

<span data-ttu-id="b645a-185">Значение по умолчанию переменной зависит от типа переменной и определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b645a-185">The default value of a variable depends on the type of the variable and is determined as follows:</span></span>

*  <span data-ttu-id="b645a-186">Для переменной *value_type*, значение по умолчанию является таким же, как значение, вычисленное *value_type*в конструктор по умолчанию ([конструкторы по умолчанию](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="b645a-186">For a variable of a *value_type*, the default value is the same as the value computed by the *value_type*'s default constructor ([Default constructors](types.md#default-constructors)).</span></span>
*  <span data-ttu-id="b645a-187">Для переменной *reference_type*, значение по умолчанию — `null`.</span><span class="sxs-lookup"><span data-stu-id="b645a-187">For a variable of a *reference_type*, the default value is `null`.</span></span>

<span data-ttu-id="b645a-188">Инициализация значения по умолчанию обычно выполняется, если диспетчер памяти или сборщик мусора инициализации памяти, все биты нулями, прежде чем он выделяется для использования.</span><span class="sxs-lookup"><span data-stu-id="b645a-188">Initialization to default values is typically done by having the memory manager or garbage collector initialize memory to all-bits-zero before it is allocated for use.</span></span> <span data-ttu-id="b645a-189">По этой причине удобно использовать все биты нулями для представления пустая ссылка.</span><span class="sxs-lookup"><span data-stu-id="b645a-189">For this reason, it is convenient to use all-bits-zero to represent the null reference.</span></span>

## <a name="definite-assignment"></a><span data-ttu-id="b645a-190">Определенного присваивания</span><span class="sxs-lookup"><span data-stu-id="b645a-190">Definite assignment</span></span>

<span data-ttu-id="b645a-191">В заданном расположении в исполняемый код функции-члена, переменная считается ***определенно присвоенной*** Если компилятор может подтвердить, с отдельного статического анализа потока ([точные правила определения определенного Назначение](variables.md#precise-rules-for-determining-definite-assignment)), переменная автоматически инициализируется или по крайней мере один назначения.</span><span class="sxs-lookup"><span data-stu-id="b645a-191">At a given location in the executable code of a function member, a variable is said to be ***definitely assigned*** if the compiler can prove, by a particular static flow analysis ([Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment)), that the variable has been automatically initialized or has been the target of at least one assignment.</span></span> <span data-ttu-id="b645a-192">Другими словами, ниже приведены правила определенного присваивания.</span><span class="sxs-lookup"><span data-stu-id="b645a-192">Informally stated, the rules of definite assignment are:</span></span>

*  <span data-ttu-id="b645a-193">Переменная с начальным значением ([изначально назначается переменные](variables.md#initially-assigned-variables)) всегда считается определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="b645a-193">An initially assigned variable ([Initially assigned variables](variables.md#initially-assigned-variables)) is always considered definitely assigned.</span></span>
*  <span data-ttu-id="b645a-194">Переменной ([без начального значения переменных](variables.md#initially-unassigned-variables)) считается определенно присвоенной в заданную позицию, если все возможные пути выполнения приводит к этому расположению содержать по крайней мере одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="b645a-194">An initially unassigned variable ([Initially unassigned variables](variables.md#initially-unassigned-variables)) is considered definitely assigned at a given location if all possible execution paths leading to that location contain at least one of the following:</span></span>
    * <span data-ttu-id="b645a-195">Простое назначение ([простое присваивание](expressions.md#simple-assignment)), в котором переменная является левым операндом.</span><span class="sxs-lookup"><span data-stu-id="b645a-195">A simple assignment ([Simple assignment](expressions.md#simple-assignment)) in which the variable is the left operand.</span></span>
    * <span data-ttu-id="b645a-196">Выражения вызова ([выражения вызова](expressions.md#invocation-expressions)) или выражение создания объекта ([выражения создания объектов](expressions.md#object-creation-expressions)), передает переменную в качестве выходного параметра.</span><span class="sxs-lookup"><span data-stu-id="b645a-196">An invocation expression ([Invocation expressions](expressions.md#invocation-expressions)) or object creation expression ([Object creation expressions](expressions.md#object-creation-expressions)) that passes the variable as an output parameter.</span></span>
    * <span data-ttu-id="b645a-197">Для локальной переменной, в объявлении локальной переменной ([объявления локальных переменных](statements.md#local-variable-declarations)), включающий инициализаторе переменных.</span><span class="sxs-lookup"><span data-stu-id="b645a-197">For a local variable, a local variable declaration ([Local variable declarations](statements.md#local-variable-declarations)) that includes a variable initializer.</span></span>

<span data-ttu-id="b645a-198">Формальная спецификация, определяющая изложенные выше правила описан в [изначально назначается переменные](variables.md#initially-assigned-variables), [без начального значения переменных](variables.md#initially-unassigned-variables), и [точные правила определения определенного присваивания](variables.md#precise-rules-for-determining-definite-assignment).</span><span class="sxs-lookup"><span data-stu-id="b645a-198">The formal specification underlying the above informal rules is described in [Initially assigned variables](variables.md#initially-assigned-variables), [Initially unassigned variables](variables.md#initially-unassigned-variables), and [Precise rules for determining definite assignment](variables.md#precise-rules-for-determining-definite-assignment).</span></span>

<span data-ttu-id="b645a-199">Состояния определенного присваивания переменных экземпляра *struct_type* переменной отслеживаются как по отдельности, так и в совокупности.</span><span class="sxs-lookup"><span data-stu-id="b645a-199">The definite assignment states of instance variables of a *struct_type* variable are tracked individually as well as collectively.</span></span> <span data-ttu-id="b645a-200">В дополнительных выше правилам применяются следующие правила для *struct_type* переменные и их переменные экземпляра:</span><span class="sxs-lookup"><span data-stu-id="b645a-200">In additional to the rules above, the following rules apply to *struct_type* variables and their instance variables:</span></span>

*  <span data-ttu-id="b645a-201">Переменная экземпляра считается определенно присвоенной, если содержащий его *struct_type* переменная считается определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="b645a-201">An instance variable is considered definitely assigned if its containing *struct_type* variable is considered definitely assigned.</span></span>
*  <span data-ttu-id="b645a-202">Объект *struct_type* переменная считается определенно присвоенной, если каждая из его переменных экземпляра считается определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="b645a-202">A *struct_type* variable is considered definitely assigned if each of its instance variables is considered definitely assigned.</span></span>

<span data-ttu-id="b645a-203">Определенного присваивания является обязательным в следующих контекстах:</span><span class="sxs-lookup"><span data-stu-id="b645a-203">Definite assignment is a requirement in the following contexts:</span></span>

*  <span data-ttu-id="b645a-204">Переменной должен быть явно присвоен во всех расположениях, где извлекается ее значение.</span><span class="sxs-lookup"><span data-stu-id="b645a-204">A variable must be definitely assigned at each location where its value is obtained.</span></span> <span data-ttu-id="b645a-205">Это гарантирует, что неопределенные значения никогда не возникают.</span><span class="sxs-lookup"><span data-stu-id="b645a-205">This ensures that undefined values never occur.</span></span> <span data-ttu-id="b645a-206">Чтобы получить значение переменной, за исключением случаев считается вхождения переменной в выражении</span><span class="sxs-lookup"><span data-stu-id="b645a-206">The occurrence of a variable in an expression is considered to obtain the value of the variable, except when</span></span>
    * <span data-ttu-id="b645a-207">переменная является левый операнд простого присваивания,</span><span class="sxs-lookup"><span data-stu-id="b645a-207">the variable is the left operand of a simple assignment,</span></span>
    * <span data-ttu-id="b645a-208">переменная передается в качестве выходного параметра, или</span><span class="sxs-lookup"><span data-stu-id="b645a-208">the variable is passed as an output parameter, or</span></span>
    * <span data-ttu-id="b645a-209">переменная является *struct_type* переменной и указана как левый операнд доступ к члену.</span><span class="sxs-lookup"><span data-stu-id="b645a-209">the variable is a *struct_type* variable and occurs as the left operand of a member access.</span></span>
*  <span data-ttu-id="b645a-210">Переменной должен быть явно присвоен во всех расположениях, где он передается в качестве ссылочного параметра.</span><span class="sxs-lookup"><span data-stu-id="b645a-210">A variable must be definitely assigned at each location where it is passed as a reference parameter.</span></span> <span data-ttu-id="b645a-211">Это гарантирует, что функцию-член вызван метод, можно изначально назначается ссылочный параметр.</span><span class="sxs-lookup"><span data-stu-id="b645a-211">This ensures that the function member being invoked can consider the reference parameter initially assigned.</span></span>
*  <span data-ttu-id="b645a-212">Все выходные параметры функции-члена должен быть явно присвоен во всех расположениях, где функцию-член возвращает (через `return` инструкции или с помощью выполнения достигнут конец тела функции-члена).</span><span class="sxs-lookup"><span data-stu-id="b645a-212">All output parameters of a function member must be definitely assigned at each location where the function member returns (through a `return` statement or through execution reaching the end of the function member body).</span></span> <span data-ttu-id="b645a-213">Это гарантирует, что функции-члены не возвращают неопределенные значения в выходных параметров, позволяя таким образом компилятор рассматривал вызова функции-члена, принимающий эквивалентно присвоения значения переменной переменную в качестве выходного параметра.</span><span class="sxs-lookup"><span data-stu-id="b645a-213">This ensures that function members do not return undefined values in output parameters, thus enabling the compiler to consider a function member invocation that takes a variable as an output parameter equivalent to an assignment to the variable.</span></span>
*  <span data-ttu-id="b645a-214">`this` Переменной *struct_type* конструктор экземпляра должен быть явно присвоен во всех расположениях, где возвращает этот конструктор экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b645a-214">The `this` variable of a *struct_type* instance constructor must be definitely assigned at each location where that instance constructor returns.</span></span>

### <a name="initially-assigned-variables"></a><span data-ttu-id="b645a-215">Переменные с начальным значением</span><span class="sxs-lookup"><span data-stu-id="b645a-215">Initially assigned variables</span></span>

<span data-ttu-id="b645a-216">Следующие категории переменных классифицируются с начальным значением:</span><span class="sxs-lookup"><span data-stu-id="b645a-216">The following categories of variables are classified as initially assigned:</span></span>

*  <span data-ttu-id="b645a-217">Статические переменные.</span><span class="sxs-lookup"><span data-stu-id="b645a-217">Static variables.</span></span>
*  <span data-ttu-id="b645a-218">Переменные экземпляров класса экземпляра.</span><span class="sxs-lookup"><span data-stu-id="b645a-218">Instance variables of class instances.</span></span>
*  <span data-ttu-id="b645a-219">Переменные экземпляра переменных начальным значением структуры.</span><span class="sxs-lookup"><span data-stu-id="b645a-219">Instance variables of initially assigned struct variables.</span></span>
*  <span data-ttu-id="b645a-220">Элементы массива.</span><span class="sxs-lookup"><span data-stu-id="b645a-220">Array elements.</span></span>
*  <span data-ttu-id="b645a-221">Параметры по значению.</span><span class="sxs-lookup"><span data-stu-id="b645a-221">Value parameters.</span></span>
*  <span data-ttu-id="b645a-222">Ссылочные параметры.</span><span class="sxs-lookup"><span data-stu-id="b645a-222">Reference parameters.</span></span>
*  <span data-ttu-id="b645a-223">Переменные, объявленные в `catch` предложение или `foreach` инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-223">Variables declared in a `catch` clause or a `foreach` statement.</span></span>

### <a name="initially-unassigned-variables"></a><span data-ttu-id="b645a-224">Изначально не присвоены значения переменных</span><span class="sxs-lookup"><span data-stu-id="b645a-224">Initially unassigned variables</span></span>

<span data-ttu-id="b645a-225">Без начального значения, относятся следующие категории переменных:</span><span class="sxs-lookup"><span data-stu-id="b645a-225">The following categories of variables are classified as initially unassigned:</span></span>

*  <span data-ttu-id="b645a-226">Переменные экземпляра структуры изначально не присвоены значения переменных.</span><span class="sxs-lookup"><span data-stu-id="b645a-226">Instance variables of initially unassigned struct variables.</span></span>
*  <span data-ttu-id="b645a-227">Выходные параметры, включая `this` переменной конструкторов экземпляров структуры.</span><span class="sxs-lookup"><span data-stu-id="b645a-227">Output parameters, including the `this` variable of struct instance constructors.</span></span>
*  <span data-ttu-id="b645a-228">За исключением локальных переменных, объявленных в `catch` предложение или `foreach` инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-228">Local variables, except those declared in a `catch` clause or a `foreach` statement.</span></span>

### <a name="precise-rules-for-determining-definite-assignment"></a><span data-ttu-id="b645a-229">Точные правила для выявления определенного присваивания</span><span class="sxs-lookup"><span data-stu-id="b645a-229">Precise rules for determining definite assignment</span></span>

<span data-ttu-id="b645a-230">Чтобы определить, что каждая из используемых переменных определенно присвоенной, компилятор должен использовать процесс, который эквивалентен, описанный в этом разделе.</span><span class="sxs-lookup"><span data-stu-id="b645a-230">In order to determine that each used variable is definitely assigned, the compiler must use a process that is equivalent to the one described in this section.</span></span>

<span data-ttu-id="b645a-231">Компилятор обрабатывает тело каждого функция-член, имеющий один или несколько переменных без начального значения.</span><span class="sxs-lookup"><span data-stu-id="b645a-231">The compiler processes the body of each function member that has one or more initially unassigned variables.</span></span> <span data-ttu-id="b645a-232">Для каждой переменной *v*, компилятор определяет ***состояние определенного присваивания*** для *v* в каждой из следующих точек в функцию-член:</span><span class="sxs-lookup"><span data-stu-id="b645a-232">For each initially unassigned variable *v*, the compiler determines a ***definite assignment state*** for *v* at each of the following points in the function member:</span></span>

*  <span data-ttu-id="b645a-233">В начале каждой инструкции</span><span class="sxs-lookup"><span data-stu-id="b645a-233">At the beginning of each statement</span></span>
*  <span data-ttu-id="b645a-234">В конечной точке ([конечные точки и доступность](statements.md#end-points-and-reachability)) каждой инструкции</span><span class="sxs-lookup"><span data-stu-id="b645a-234">At the end point ([End points and reachability](statements.md#end-points-and-reachability)) of each statement</span></span>
*  <span data-ttu-id="b645a-235">В каждой ветке, где управление передается в другой оператор или в конечную точку, инструкции</span><span class="sxs-lookup"><span data-stu-id="b645a-235">On each arc which transfers control to another statement or to the end point of a statement</span></span>
*  <span data-ttu-id="b645a-236">В начале каждого выражения</span><span class="sxs-lookup"><span data-stu-id="b645a-236">At the beginning of each expression</span></span>
*  <span data-ttu-id="b645a-237">В конце каждого выражения</span><span class="sxs-lookup"><span data-stu-id="b645a-237">At the end of each expression</span></span>

<span data-ttu-id="b645a-238">Состояние определенного присваивания *v* может быть либо:</span><span class="sxs-lookup"><span data-stu-id="b645a-238">The definite assignment state of *v* can be either:</span></span>

*  <span data-ttu-id="b645a-239">Определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="b645a-239">Definitely assigned.</span></span> <span data-ttu-id="b645a-240">Это означает, что на всех возможных потоках управления к этому моменту *v* было назначено значение.</span><span class="sxs-lookup"><span data-stu-id="b645a-240">This indicates that on all possible control flows to this point, *v* has been assigned a value.</span></span>
*  <span data-ttu-id="b645a-241">Определенно присвоенной.</span><span class="sxs-lookup"><span data-stu-id="b645a-241">Not definitely assigned.</span></span> <span data-ttu-id="b645a-242">Для состояния переменной в конце выражения типа `bool`, состояние переменной, которая не определенно присвоенной мая (но не обязательно), относятся к одной из следующих вложенных состояний:</span><span class="sxs-lookup"><span data-stu-id="b645a-242">For the state of a variable at the end of an expression of type `bool`, the state of a variable that isn't definitely assigned may (but doesn't necessarily) fall into one of the following sub-states:</span></span>
    * <span data-ttu-id="b645a-243">Определенно присвоенной после выражения значение true.</span><span class="sxs-lookup"><span data-stu-id="b645a-243">Definitely assigned after true expression.</span></span> <span data-ttu-id="b645a-244">Это состояние указывает, что *v* присваивается определенным образом в том случае, если логическое выражение возвращает значение true, но не назначен обязательно, если логическое выражение вычислено как false.</span><span class="sxs-lookup"><span data-stu-id="b645a-244">This state indicates that *v* is definitely assigned if the boolean expression evaluated as true, but is not necessarily assigned if the boolean expression evaluated as false.</span></span>
    * <span data-ttu-id="b645a-245">Определенно присвоенной после выражения false.</span><span class="sxs-lookup"><span data-stu-id="b645a-245">Definitely assigned after false expression.</span></span> <span data-ttu-id="b645a-246">Это состояние указывает, что *v* присваивается определенным образом в том случае, если логическое выражение вычислено как false, но присваивается не обязательно, если логическое выражение вычисляется как true.</span><span class="sxs-lookup"><span data-stu-id="b645a-246">This state indicates that *v* is definitely assigned if the boolean expression evaluated as false, but is not necessarily assigned if the boolean expression evaluated as true.</span></span>

<span data-ttu-id="b645a-247">Следующие правила определяют как состояние переменной *v* определяется в каждом расположении.</span><span class="sxs-lookup"><span data-stu-id="b645a-247">The following rules govern how the state of a variable *v* is determined at each location.</span></span>

#### <a name="general-rules-for-statements"></a><span data-ttu-id="b645a-248">Общие правила для операторов</span><span class="sxs-lookup"><span data-stu-id="b645a-248">General rules for statements</span></span>

*  <span data-ttu-id="b645a-249">*v* не является определенно присвоенной в начале тела функции-члена.</span><span class="sxs-lookup"><span data-stu-id="b645a-249">*v* is not definitely assigned at the beginning of a function member body.</span></span>
*  <span data-ttu-id="b645a-250">*v* определенно присвоенной в начале каждой недостижимого оператора.</span><span class="sxs-lookup"><span data-stu-id="b645a-250">*v* is definitely assigned at the beginning of any unreachable statement.</span></span>
*  <span data-ttu-id="b645a-251">Состояние определенного присваивания *v* в начале любой другой инструкции, определяется путем проверки состояния определенного присваивания *v* на все передачи потока управления, предназначенных для начала, инструкция.</span><span class="sxs-lookup"><span data-stu-id="b645a-251">The definite assignment state of *v* at the beginning of any other statement is determined by checking the definite assignment state of *v* on all control flow transfers that target the beginning of that statement.</span></span> <span data-ttu-id="b645a-252">Если (и только в том случае, если) *v* определенно назначается на все ветвях потоков управления, затем *v* определенно присвоенной в начале инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-252">If (and only if) *v* is definitely assigned on all such control flow transfers, then *v* is definitely assigned at the beginning of the statement.</span></span> <span data-ttu-id="b645a-253">Набор возможных ветвлений потоков управления определяется так же как и для проверки достижимости операторов ([конечные точки и доступность](statements.md#end-points-and-reachability)).</span><span class="sxs-lookup"><span data-stu-id="b645a-253">The set of possible control flow transfers is determined in the same way as for checking statement reachability ([End points and reachability](statements.md#end-points-and-reachability)).</span></span>
*  <span data-ttu-id="b645a-254">Состояние определенного присваивания *v* в конечной точке блока, `checked`, `unchecked`, `if`, `while`, `do`, `for`, `foreach`, `lock`, `using`, или `switch` определяется путем проверки состояния определенного присваивания *v* на все передачи потока управления, предназначенных для конечной точки этой инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-254">The definite assignment state of *v* at the end point of a block, `checked`, `unchecked`, `if`, `while`, `do`, `for`, `foreach`, `lock`, `using`, or `switch` statement is determined by checking the definite assignment state of *v* on all control flow transfers that target the end point of that statement.</span></span> <span data-ttu-id="b645a-255">Если *v* определенно назначается на все ветвях потоков управления, затем *v* определенно присвоенной в конечной точке инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-255">If *v* is definitely assigned on all such control flow transfers, then *v* is definitely assigned at the end point of the statement.</span></span> <span data-ttu-id="b645a-256">В противном случае; *v* не является определенно присвоенной в конечной точке инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-256">Otherwise; *v* is not definitely assigned at the end point of the statement.</span></span> <span data-ttu-id="b645a-257">Набор возможных ветвлений потоков управления определяется так же как и для проверки достижимости операторов ([конечные точки и доступность](statements.md#end-points-and-reachability)).</span><span class="sxs-lookup"><span data-stu-id="b645a-257">The set of possible control flow transfers is determined in the same way as for checking statement reachability ([End points and reachability](statements.md#end-points-and-reachability)).</span></span>

#### <a name="block-statements-checked-and-unchecked-statements"></a><span data-ttu-id="b645a-258">Блок операторов, этот флажок установлен и снят флажок операторов</span><span class="sxs-lookup"><span data-stu-id="b645a-258">Block statements, checked, and unchecked statements</span></span>

<span data-ttu-id="b645a-259">Состояние определенного присваивания *v* на элементе управления передачи для первой инструкции списка операторов в блоке (или в конечную точку блока, если список операторов пуст) совпадает со значением определенного присваивания переменной *v* перед блоком, `checked`, или `unchecked` инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-259">The definite assignment state of *v* on the control transfer to the first statement of the statement list in the block (or to the end point of the block, if the statement list is empty) is the same as the definite assignment statement of *v* before the block, `checked`, or `unchecked` statement.</span></span>

#### <a name="expression-statements"></a><span data-ttu-id="b645a-260">Инструкции выражений</span><span class="sxs-lookup"><span data-stu-id="b645a-260">Expression statements</span></span>

<span data-ttu-id="b645a-261">Для инструкции выражение *stmt* , состоящий из выражения *expr*:</span><span class="sxs-lookup"><span data-stu-id="b645a-261">For an expression statement *stmt* that consists of the expression *expr*:</span></span>

*  <span data-ttu-id="b645a-262">*v* имеющий то же состояние определенного присваивания в начале *expr* как в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-262">*v* has the same definite assignment state at the beginning of *expr* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-263">Если *v* Если определенно присвоенной в конце *expr*, он считается определенно присвоенной в конечную точку *stmt*; в противном случае; определенно не назначен в конечную точку *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-263">If *v* if definitely assigned at the end of *expr*, it is definitely assigned at the end point of *stmt*; otherwise; it is not definitely assigned at the end point of *stmt*.</span></span>

#### <a name="declaration-statements"></a><span data-ttu-id="b645a-264">Инструкции объявления</span><span class="sxs-lookup"><span data-stu-id="b645a-264">Declaration statements</span></span>

*  <span data-ttu-id="b645a-265">Если *stmt* является оператором объявления без инициализаторов, затем *v* имеет такое же состояние определенного присваивания в конечную точку *stmt* как в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-265">If *stmt* is a declaration statement without initializers, then *v* has the same definite assignment state at the end point of *stmt* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-266">Если *stmt* является оператором объявления с инициализаторами, затем состояние определенного присваивания для *v* определяется так, как если *stmt* списка операторов, с помощью одно назначение инструкции для каждого объявления с инициализатором (в порядке объявления).</span><span class="sxs-lookup"><span data-stu-id="b645a-266">If *stmt* is a declaration statement with initializers, then the definite assignment state for *v* is determined as if *stmt* were a statement list, with one assignment statement for each declaration with an initializer (in the order of declaration).</span></span>

#### <a name="if-statements"></a><span data-ttu-id="b645a-267">Если инструкции</span><span class="sxs-lookup"><span data-stu-id="b645a-267">If statements</span></span>

<span data-ttu-id="b645a-268">Для `if` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-268">For an `if` statement *stmt* of the form:</span></span>
```csharp
if ( expr ) then_stmt else else_stmt
```

*  <span data-ttu-id="b645a-269">*v* имеющий то же состояние определенного присваивания в начале *expr* как в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-269">*v* has the same definite assignment state at the beginning of *expr* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-270">Если *v* определенно присвоенной в конце *expr*, а затем она определенно присвоенной передачу потока управления в *then_stmt* и либо *else_stmt*  или в конечной точке *stmt* Если отсутствует предложение else.</span><span class="sxs-lookup"><span data-stu-id="b645a-270">If *v* is definitely assigned at the end of *expr*, then it is definitely assigned on the control flow transfer to *then_stmt* and to either *else_stmt* or to the end-point of *stmt* if there is no else clause.</span></span>
*  <span data-ttu-id="b645a-271">Если *v* имеет состояние «определенно назначены после выражения true» в конце *expr*, а затем она определенно присвоенной передачу потока управления в *then_stmt*и не определенно присвоенной ветви потока управления, либо *else_stmt* или в конечной точке *stmt* Если отсутствует предложение else.</span><span class="sxs-lookup"><span data-stu-id="b645a-271">If *v* has the state "definitely assigned after true expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to *then_stmt*, and not definitely assigned on the control flow transfer to either *else_stmt* or to the end-point of *stmt* if there is no else clause.</span></span>
*  <span data-ttu-id="b645a-272">Если *v* имеет состояние «определенно назначены после выражения false» в конце *expr*, а затем она определенно присвоенной передачу потока управления в *else_stmt*и не определенно присвоенной передачу потока управления в *then_stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-272">If *v* has the state "definitely assigned after false expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to *else_stmt*, and not definitely assigned on the control flow transfer to *then_stmt*.</span></span> <span data-ttu-id="b645a-273">Она является определенно присвоенной в конечной точке *stmt* только в том случае, если она является определенно присвоенной в конечной точке *then_stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-273">It is definitely assigned at the end-point of *stmt* if and only if it is definitely assigned at the end-point of *then_stmt*.</span></span>
*  <span data-ttu-id="b645a-274">В противном случае *v* считается определенно присвоенной ветви потока управления, либо *then_stmt* или *else_stmt*, или в конечной точке  *stmt* Если отсутствует предложение else.</span><span class="sxs-lookup"><span data-stu-id="b645a-274">Otherwise, *v* is considered not definitely assigned on the control flow transfer to either the *then_stmt* or *else_stmt*, or to the end-point of *stmt* if there is no else clause.</span></span>

#### <a name="switch-statements"></a><span data-ttu-id="b645a-275">Операторы switch</span><span class="sxs-lookup"><span data-stu-id="b645a-275">Switch statements</span></span>

<span data-ttu-id="b645a-276">В `switch` инструкции *stmt* с управляющее выражение *expr*:</span><span class="sxs-lookup"><span data-stu-id="b645a-276">In a `switch` statement *stmt* with a controlling expression *expr*:</span></span>

*  <span data-ttu-id="b645a-277">Состояние определенного присваивания *v* в начале *expr* совпадает со значением состояния *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-277">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-278">Состояние определенного присваивания *v* в потоке управления передача в список доступен коммутатор блок инструкций является таким же, как состояние определенного присваивания *v* в конце *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-278">The definite assignment state of *v* on the control flow transfer to a reachable switch block statement list is the same as the definite assignment state of *v* at the end of *expr*.</span></span>

#### <a name="while-statements"></a><span data-ttu-id="b645a-279">While-операторы</span><span class="sxs-lookup"><span data-stu-id="b645a-279">While statements</span></span>

<span data-ttu-id="b645a-280">Для `while` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-280">For a `while` statement *stmt* of the form:</span></span>
```csharp
while ( expr ) while_body
```

*  <span data-ttu-id="b645a-281">*v* имеющий то же состояние определенного присваивания в начале *expr* как в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-281">*v* has the same definite assignment state at the beginning of *expr* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-282">Если *v* определенно присвоенной в конце *expr*, а затем она определенно присвоенной передачу потока управления в *while_body* и конечную точку  *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-282">If *v* is definitely assigned at the end of *expr*, then it is definitely assigned on the control flow transfer to *while_body* and to the end point of *stmt*.</span></span>
*  <span data-ttu-id="b645a-283">Если *v* имеет состояние «определенно назначены после выражения true» в конце *expr*, то определенно присвоенной передачу потока управления в *while_body*, но не определенно присвоенной в конечной точке *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-283">If *v* has the state "definitely assigned after true expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to *while_body*, but not definitely assigned at the end-point of *stmt*.</span></span>
*  <span data-ttu-id="b645a-284">Если *v* имеет состояние «определенно назначены после выражения false» в конце *expr*, а затем она определенно присвоенной передачу потока управления в конечную точку *stmt* , но определенно присвоенной ветви потока управления для *while_body*.</span><span class="sxs-lookup"><span data-stu-id="b645a-284">If *v* has the state "definitely assigned after false expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to the end point of *stmt*, but not definitely assigned on the control flow transfer to *while_body*.</span></span>

#### <a name="do-statements"></a><span data-ttu-id="b645a-285">Инструкции</span><span class="sxs-lookup"><span data-stu-id="b645a-285">Do statements</span></span>

<span data-ttu-id="b645a-286">Для `do` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-286">For a `do` statement *stmt* of the form:</span></span>
```csharp
do do_body while ( expr ) ;
```

*  <span data-ttu-id="b645a-287">*v* имеющий то же состояние определенного присваивания ветви потока управления в начале *stmt* для *do_body* как в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-287">*v* has the same definite assignment state on the control flow transfer from the beginning of *stmt* to *do_body* as at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-288">*v* имеющий то же состояние определенного присваивания в начале *expr* на конечную точку *do_body*.</span><span class="sxs-lookup"><span data-stu-id="b645a-288">*v* has the same definite assignment state at the beginning of *expr* as at the end point of *do_body*.</span></span>
*  <span data-ttu-id="b645a-289">Если *v* определенно присвоенной в конце *expr*, а затем она определенно присвоенной передачу потока управления в конечную точку *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-289">If *v* is definitely assigned at the end of *expr*, then it is definitely assigned on the control flow transfer to the end point of *stmt*.</span></span>
*  <span data-ttu-id="b645a-290">Если *v* имеет состояние «определенно назначены после выражения false» в конце *expr*, а затем она определенно присвоенной передачу потока управления в конечную точку *stmt* .</span><span class="sxs-lookup"><span data-stu-id="b645a-290">If *v* has the state "definitely assigned after false expression" at the end of *expr*, then it is definitely assigned on the control flow transfer to the end point of *stmt*.</span></span>

#### <a name="for-statements"></a><span data-ttu-id="b645a-291">Для инструкций</span><span class="sxs-lookup"><span data-stu-id="b645a-291">For statements</span></span>

<span data-ttu-id="b645a-292">Проверка наличия определенного присваивания `for` инструкцию для формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-292">Definite assignment checking for a `for` statement of the form:</span></span>
```csharp
for ( for_initializer ; for_condition ; for_iterator ) embedded_statement
```
<span data-ttu-id="b645a-293">выполняется для оператора:</span><span class="sxs-lookup"><span data-stu-id="b645a-293">is done as if the statement were written:</span></span>
```csharp
{
    for_initializer ;
    while ( for_condition ) {
        embedded_statement ;
        for_iterator ;
    }
}
```

<span data-ttu-id="b645a-294">Если *for_condition* исключается из `for` инструкции, а затем вычисление определенного присваивания продолжается так, как если *for_condition* были заменены `true` в выше расширения .</span><span class="sxs-lookup"><span data-stu-id="b645a-294">If the *for_condition* is omitted from the `for` statement, then evaluation of definite assignment proceeds as if *for_condition* were replaced with `true` in the above expansion.</span></span>

#### <a name="break-continue-and-goto-statements"></a><span data-ttu-id="b645a-295">Прервать, продолжить работу и операторы "goto"</span><span class="sxs-lookup"><span data-stu-id="b645a-295">Break, continue, and goto statements</span></span>

<span data-ttu-id="b645a-296">Состояние определенного присваивания *v* ветви потока управления, из-за `break`, `continue`, или `goto` инструкция является таким же, как состояние определенного присваивания *v* в начало оператора.</span><span class="sxs-lookup"><span data-stu-id="b645a-296">The definite assignment state of *v* on the control flow transfer caused by a `break`, `continue`, or `goto` statement is the same as the definite assignment state of *v* at the beginning of the statement.</span></span>

#### <a name="throw-statements"></a><span data-ttu-id="b645a-297">Операторы throw</span><span class="sxs-lookup"><span data-stu-id="b645a-297">Throw statements</span></span>

<span data-ttu-id="b645a-298">Для инструкции *stmt* формы</span><span class="sxs-lookup"><span data-stu-id="b645a-298">For a statement *stmt* of the form</span></span>
```csharp
throw expr ;
```

<span data-ttu-id="b645a-299">Состояние определенного присваивания *v* в начале *expr* совпадает со значением состояния определенного присваивания *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-299">The definite assignment state of *v* at the beginning of *expr* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>

#### <a name="return-statements"></a><span data-ttu-id="b645a-300">Операторы "Return"</span><span class="sxs-lookup"><span data-stu-id="b645a-300">Return statements</span></span>

<span data-ttu-id="b645a-301">Для инструкции *stmt* формы</span><span class="sxs-lookup"><span data-stu-id="b645a-301">For a statement *stmt* of the form</span></span>
```csharp
return expr ;
```

*  <span data-ttu-id="b645a-302">Состояние определенного присваивания *v* в начале *expr* совпадает со значением состояния определенного присваивания *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-302">The definite assignment state of *v* at the beginning of *expr* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-303">Если *v* является выходным параметром, то он должен быть явно присвоен либо:</span><span class="sxs-lookup"><span data-stu-id="b645a-303">If *v* is an output parameter, then it must be definitely assigned either:</span></span>
    * <span data-ttu-id="b645a-304">После *expr*</span><span class="sxs-lookup"><span data-stu-id="b645a-304">after *expr*</span></span>
    * <span data-ttu-id="b645a-305">или в конце `finally` блока `try` - `finally` или `try` - `catch` - `finally` , ограничивающий `return` инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-305">or at the end of the `finally` block of a `try`-`finally` or `try`-`catch`-`finally` that encloses the `return` statement.</span></span>

<span data-ttu-id="b645a-306">Для оператора stmt формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-306">For a statement stmt of the form:</span></span>
```csharp
return ;
```

*  <span data-ttu-id="b645a-307">Если *v* является выходным параметром, то он должен быть явно присвоен либо:</span><span class="sxs-lookup"><span data-stu-id="b645a-307">If *v* is an output parameter, then it must be definitely assigned either:</span></span>
    * <span data-ttu-id="b645a-308">Прежде чем *stmt*</span><span class="sxs-lookup"><span data-stu-id="b645a-308">before *stmt*</span></span>
    * <span data-ttu-id="b645a-309">или в конце `finally` блока `try` - `finally` или `try` - `catch` - `finally` , ограничивающий `return` инструкции.</span><span class="sxs-lookup"><span data-stu-id="b645a-309">or at the end of the `finally` block of a `try`-`finally` or `try`-`catch`-`finally` that encloses the `return` statement.</span></span>

#### <a name="try-catch-statements"></a><span data-ttu-id="b645a-310">Операторы try-catch</span><span class="sxs-lookup"><span data-stu-id="b645a-310">Try-catch statements</span></span>

<span data-ttu-id="b645a-311">Для инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-311">For a statement *stmt* of the form:</span></span>
```csharp
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
```

*  <span data-ttu-id="b645a-312">Состояние определенного присваивания *v* в начале *try_block* совпадает со значением состояния определенного присваивания *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-312">The definite assignment state of *v* at the beginning of *try_block* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-313">Состояние определенного присваивания *v* в начале *catch_block_i* (для любого *я*) совпадает со значением состояния определенного присваивания *v*в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-313">The definite assignment state of *v* at the beginning of *catch_block_i* (for any *i*) is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-314">Состояние определенного присваивания *v* в конечной точке *stmt* определенно присвоенной (и только если) *v* определенно присвоенной в конечной точке  *try_block* и каждый *catch_block_i* (для каждого *я* от 1 до *n*).</span><span class="sxs-lookup"><span data-stu-id="b645a-314">The definite assignment state of *v* at the end-point of *stmt* is definitely assigned if (and only if) *v* is definitely assigned at the end-point of *try_block* and every *catch_block_i* (for every *i* from 1 to *n*).</span></span>

#### <a name="try-finally-statements"></a><span data-ttu-id="b645a-315">Операторы try-finally</span><span class="sxs-lookup"><span data-stu-id="b645a-315">Try-finally statements</span></span>

<span data-ttu-id="b645a-316">Для `try` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-316">For a `try` statement *stmt* of the form:</span></span>
```csharp
try try_block finally finally_block
```

*  <span data-ttu-id="b645a-317">Состояние определенного присваивания *v* в начале *try_block* совпадает со значением состояния определенного присваивания *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-317">The definite assignment state of *v* at the beginning of *try_block* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-318">Состояние определенного присваивания *v* в начале *finally_block* совпадает со значением состояния определенного присваивания *v* в начале *stmt* .</span><span class="sxs-lookup"><span data-stu-id="b645a-318">The definite assignment state of *v* at the beginning of *finally_block* is the same as the definite assignment state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-319">Состояние определенного присваивания *v* в конечной точке *stmt* определенно присвоенной (и только если) по крайней мере одно из следующих имеет значение true:</span><span class="sxs-lookup"><span data-stu-id="b645a-319">The definite assignment state of *v* at the end-point of *stmt* is definitely assigned if (and only if) at least one of the following is true:</span></span>
    * <span data-ttu-id="b645a-320">*v* определенно присвоенной в конечной точке *try_block*</span><span class="sxs-lookup"><span data-stu-id="b645a-320">*v* is definitely assigned at the end-point of *try_block*</span></span>
    * <span data-ttu-id="b645a-321">*v* определенно присвоенной в конечной точке *finally_block*</span><span class="sxs-lookup"><span data-stu-id="b645a-321">*v* is definitely assigned at the end-point of *finally_block*</span></span>

<span data-ttu-id="b645a-322">При переключении потока управления (например, `goto` инструкции), которое начинается в *try_block*и заканчивается за пределами *try_block*, затем *v* также считается определенно присвоенной в ветви потока управления, если *v* определенно присвоенной в конечной точке *finally_block*.</span><span class="sxs-lookup"><span data-stu-id="b645a-322">If a control flow transfer (for example, a `goto` statement) is made that begins within *try_block*, and ends outside of *try_block*, then *v* is also considered definitely assigned on that control flow transfer if *v* is definitely assigned at the end-point of *finally_block*.</span></span> <span data-ttu-id="b645a-323">(Это не единственная — Если *v* определенно присвоенной по другой причине этой ветви потока управления, то он по-прежнему считается определенно присвоенной.)</span><span class="sxs-lookup"><span data-stu-id="b645a-323">(This is not an only if—if *v* is definitely assigned for another reason on this control flow transfer, then it is still considered definitely assigned.)</span></span>

#### <a name="try-catch-finally-statements"></a><span data-ttu-id="b645a-324">Операторы try-catch-finally</span><span class="sxs-lookup"><span data-stu-id="b645a-324">Try-catch-finally statements</span></span>

<span data-ttu-id="b645a-325">Анализ определенного присваивания для `try` - `catch` - `finally` инструкцию для формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-325">Definite assignment analysis for a `try`-`catch`-`finally` statement of the form:</span></span>
```csharp
try try_block
catch(...) catch_block_1
...
catch(...) catch_block_n
finally *finally_block*
```
<span data-ttu-id="b645a-326">выполняется, как если бы были инструкция `try` - `finally` заключения инструкции `try` - `catch` инструкции:</span><span class="sxs-lookup"><span data-stu-id="b645a-326">is done as if the statement were a `try`-`finally` statement enclosing a `try`-`catch` statement:</span></span>
```csharp
try {
    try try_block
    catch(...) catch_block_1
    ...
    catch(...) catch_block_n
}
finally finally_block
```

<span data-ttu-id="b645a-327">В следующем примере показано, как разные блоки `try` инструкции ([оператора try](statements.md#the-try-statement)) влияют на определенного присваивания.</span><span class="sxs-lookup"><span data-stu-id="b645a-327">The following example demonstrates how the different blocks of a `try` statement ([The try statement](statements.md#the-try-statement)) affect definite assignment.</span></span>
```csharp
class A
{
    static void F() {
        int i, j;
        try {
            goto LABEL;
            // neither i nor j definitely assigned
            i = 1;
            // i definitely assigned
        }

        catch {
            // neither i nor j definitely assigned
            i = 3;
            // i definitely assigned
        }

        finally {
            // neither i nor j definitely assigned
            j = 5;
            // j definitely assigned
            }
        // i and j definitely assigned
        LABEL:;
        // j definitely assigned

    }
}
```

#### <a name="foreach-statements"></a><span data-ttu-id="b645a-328">Инструкции по каждому элементу</span><span class="sxs-lookup"><span data-stu-id="b645a-328">Foreach statements</span></span>

<span data-ttu-id="b645a-329">Для `foreach` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-329">For a `foreach` statement *stmt* of the form:</span></span>
```csharp
foreach ( type identifier in expr ) embedded_statement
```

*  <span data-ttu-id="b645a-330">Состояние определенного присваивания *v* в начале *expr* совпадает со значением состояния *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-330">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-331">Состояние определенного присваивания *v* ветви потока управления для *embedded_statement* или конечную точку *stmt* совпадает со значением состояния *v* в конце *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-331">The definite assignment state of *v* on the control flow transfer to *embedded_statement* or to the end point of *stmt* is the same as the state of *v* at the end of *expr*.</span></span>

#### <a name="using-statements"></a><span data-ttu-id="b645a-332">С помощью инструкций</span><span class="sxs-lookup"><span data-stu-id="b645a-332">Using statements</span></span>

<span data-ttu-id="b645a-333">Для `using` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-333">For a `using` statement *stmt* of the form:</span></span>
```csharp
using ( resource_acquisition ) embedded_statement
```

*  <span data-ttu-id="b645a-334">Состояние определенного присваивания *v* в начале *resource_acquisition* совпадает со значением состояния *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-334">The definite assignment state of *v* at the beginning of *resource_acquisition* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-335">Состояние определенного присваивания *v* ветви потока управления для *embedded_statement* совпадает со значением состояния *v* в конце *resource_ Приобретение*.</span><span class="sxs-lookup"><span data-stu-id="b645a-335">The definite assignment state of *v* on the control flow transfer to *embedded_statement* is the same as the state of *v* at the end of *resource_acquisition*.</span></span>

#### <a name="lock-statements"></a><span data-ttu-id="b645a-336">Инструкции блокировки</span><span class="sxs-lookup"><span data-stu-id="b645a-336">Lock statements</span></span>

<span data-ttu-id="b645a-337">Для `lock` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-337">For a `lock` statement *stmt* of the form:</span></span>
```csharp
lock ( expr ) embedded_statement
```

*  <span data-ttu-id="b645a-338">Состояние определенного присваивания *v* в начале *expr* совпадает со значением состояния *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-338">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-339">Состояние определенного присваивания *v* ветви потока управления для *embedded_statement* совпадает со значением состояния *v* в конце *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-339">The definite assignment state of *v* on the control flow transfer to *embedded_statement* is the same as the state of *v* at the end of *expr*.</span></span>

#### <a name="yield-statements"></a><span data-ttu-id="b645a-340">Операторы yield</span><span class="sxs-lookup"><span data-stu-id="b645a-340">Yield statements</span></span>

<span data-ttu-id="b645a-341">Для `yield return` инструкции *stmt* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-341">For a `yield return` statement *stmt* of the form:</span></span>
```csharp
yield return expr ;
```

*  <span data-ttu-id="b645a-342">Состояние определенного присваивания *v* в начале *expr* совпадает со значением состояния *v* в начале *stmt*.</span><span class="sxs-lookup"><span data-stu-id="b645a-342">The definite assignment state of *v* at the beginning of *expr* is the same as the state of *v* at the beginning of *stmt*.</span></span>
*  <span data-ttu-id="b645a-343">Состояние определенного присваивания *v* в конце *stmt* совпадает со значением состояния *v* в конце *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-343">The definite assignment state of *v* at the end of *stmt* is the same as the state of *v* at the end of *expr*.</span></span>
*  <span data-ttu-id="b645a-344">Объект `yield break` инструкции не влияет на состояние определенного присваивания.</span><span class="sxs-lookup"><span data-stu-id="b645a-344">A `yield break` statement has no effect on the definite assignment state.</span></span>

#### <a name="general-rules-for-simple-expressions"></a><span data-ttu-id="b645a-345">Общие правила для простых выражений</span><span class="sxs-lookup"><span data-stu-id="b645a-345">General rules for simple expressions</span></span>

<span data-ttu-id="b645a-346">Следующее правило применяется для этих видов выражений: литералы ([литералы](expressions.md#literals)), простые имена ([простые имена](expressions.md#simple-names)), выражения доступа к членам ([доступ к членам](expressions.md#member-access)), выражения неиндексированных доступ к базовым членам ([базового доступа](expressions.md#base-access)), `typeof` выражения ([оператор typeof](expressions.md#the-typeof-operator)), выражения значения по умолчанию ([выражения значения по умолчанию ](expressions.md#default-value-expressions)) и `nameof` выражения ([выражения Nameof](expressions.md#nameof-expressions)).</span><span class="sxs-lookup"><span data-stu-id="b645a-346">The following rule applies to these kinds of expressions: literals ([Literals](expressions.md#literals)), simple names ([Simple names](expressions.md#simple-names)), member access expressions ([Member access](expressions.md#member-access)), non-indexed base access expressions ([Base access](expressions.md#base-access)), `typeof` expressions ([The typeof operator](expressions.md#the-typeof-operator)), default value expressions ([Default value expressions](expressions.md#default-value-expressions)) and `nameof` expressions ([Nameof expressions](expressions.md#nameof-expressions)).</span></span>

*  <span data-ttu-id="b645a-347">Состояние определенного присваивания *v* в конце такого выражения совпадает со значением состояния определенного присваивания *v* в начале выражения.</span><span class="sxs-lookup"><span data-stu-id="b645a-347">The definite assignment state of *v* at the end of such an expression is the same as the definite assignment state of *v* at the beginning of the expression.</span></span>

#### <a name="general-rules-for-expressions-with-embedded-expressions"></a><span data-ttu-id="b645a-348">Общие правила для выражений с внедренными выражениями</span><span class="sxs-lookup"><span data-stu-id="b645a-348">General rules for expressions with embedded expressions</span></span>

<span data-ttu-id="b645a-349">Применяются следующие правила для этих видов выражений: выражения в скобках ([выражения в скобках](expressions.md#parenthesized-expressions)), выражения доступа к элементу ([доступ к элементам](expressions.md#element-access)), базовый доступ к выражения с Индексирование ([базового доступа](expressions.md#base-access)), увеличения и уменьшения выражения ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators), [префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)), выражения приведения ([выражения приведения](expressions.md#cast-expressions)), унарный `+`, `-`, `~`, `*` выражения, двоичный `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `<`, `<=`, `>`, `>=`, `==`, `!=`, `is`, `as`, `&`, `|`, `^` выражения ([арифметические операторы](expressions.md#arithmetic-operators), [операторы сдвига](expressions.md#shift-operators), [отношения и операторы тестирования типа](expressions.md#relational-and-type-testing-operators) [Логические операторы](expressions.md#logical-operators)), составные выражения присваивания ([Составное присваивание](expressions.md#compound-assignment)), `checked` и `unchecked` выражения ([checked и unchecked операторы](expressions.md#the-checked-and-unchecked-operators)), а также массив и делегат выражения для создания ([оператор new](expressions.md#the-new-operator)).</span><span class="sxs-lookup"><span data-stu-id="b645a-349">The following rules apply to these kinds of expressions: parenthesized expressions ([Parenthesized expressions](expressions.md#parenthesized-expressions)), element access expressions ([Element access](expressions.md#element-access)), base access expressions with indexing ([Base access](expressions.md#base-access)), increment and decrement expressions ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators), [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)), cast expressions ([Cast expressions](expressions.md#cast-expressions)), unary `+`, `-`, `~`, `*` expressions, binary `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `<`, `<=`, `>`, `>=`, `==`, `!=`, `is`, `as`, `&`, `|`, `^` expressions ([Arithmetic operators](expressions.md#arithmetic-operators), [Shift operators](expressions.md#shift-operators), [Relational and type-testing operators](expressions.md#relational-and-type-testing-operators), [Logical operators](expressions.md#logical-operators)), compound assignment expressions ([Compound assignment](expressions.md#compound-assignment)), `checked` and `unchecked` expressions ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)), plus array and delegate creation expressions ([The new operator](expressions.md#the-new-operator)).</span></span>

<span data-ttu-id="b645a-350">Каждый из этих выражений имеет один или несколько вложенных выражений, которые оцениваются, безусловно, в определенном порядке.</span><span class="sxs-lookup"><span data-stu-id="b645a-350">Each of these expressions has one or more sub-expressions that are unconditionally evaluated in a fixed order.</span></span> <span data-ttu-id="b645a-351">Например, двоичный файл `%` оператор вычисляет левой части оператора, а затем правой части.</span><span class="sxs-lookup"><span data-stu-id="b645a-351">For example, the binary `%` operator evaluates the left hand side of the operator, then the right hand side.</span></span> <span data-ttu-id="b645a-352">Операция индексирования вычисляет индексированным выражением, а затем каждое из выражений индекса, в порядке слева направо.</span><span class="sxs-lookup"><span data-stu-id="b645a-352">An indexing operation evaluates the indexed expression, and then evaluates each of the index expressions, in order from left to right.</span></span> <span data-ttu-id="b645a-353">Для выражения *expr*, который имеет вложенных выражений *e1, e2,..., eN*, вычисленное в указанном порядке:</span><span class="sxs-lookup"><span data-stu-id="b645a-353">For an expression *expr*, which has sub-expressions *e1, e2, ..., eN*, evaluated in that order:</span></span>

*  <span data-ttu-id="b645a-354">Состояние определенного присваивания *v* в начале *e1* совпадает со значением состояние определенного присваивания в начале *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-354">The definite assignment state of *v* at the beginning of *e1* is the same as the definite assignment state at the beginning of *expr*.</span></span>
*  <span data-ttu-id="b645a-355">Состояние определенного присваивания *v* в начале *ei* (*я* больше единицы) совпадает со значением состояние определенного присваивания в конце предыдущего подвыражения.</span><span class="sxs-lookup"><span data-stu-id="b645a-355">The definite assignment state of *v* at the beginning of *ei* (*i* greater than one) is the same as the definite assignment state at the end of the previous sub-expression.</span></span>
*  <span data-ttu-id="b645a-356">Состояние определенного присваивания *v* в конце *expr* совпадает со значением состояние определенного присваивания в конце *eN*</span><span class="sxs-lookup"><span data-stu-id="b645a-356">The definite assignment state of *v* at the end of *expr* is the same as the definite assignment state at the end of *eN*</span></span>

#### <a name="invocation-expressions-and-object-creation-expressions"></a><span data-ttu-id="b645a-357">Выражения вызова и выражения создания объекта</span><span class="sxs-lookup"><span data-stu-id="b645a-357">Invocation expressions and object creation expressions</span></span>

<span data-ttu-id="b645a-358">Для выражения вызова *expr* формы:</span><span class="sxs-lookup"><span data-stu-id="b645a-358">For an invocation expression *expr* of the form:</span></span>
```csharp
primary_expression ( arg1 , arg2 , ... , argN )
```
<span data-ttu-id="b645a-359">или выражение создания объекта в форме:</span><span class="sxs-lookup"><span data-stu-id="b645a-359">or an object creation expression of the form:</span></span>
```csharp
new type ( arg1 , arg2 , ... , argN )
```

*  <span data-ttu-id="b645a-360">Для выражения вызова состояние определенного присваивания *v* перед *primary_expression* совпадает со значением состояния *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-360">For an invocation expression, the definite assignment state of *v* before *primary_expression* is the same as the state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-361">Для выражения вызова состояние определенного присваивания *v* перед *arg1* совпадает со значением состояния *v* после *primary_expression*.</span><span class="sxs-lookup"><span data-stu-id="b645a-361">For an invocation expression, the definite assignment state of *v* before *arg1* is the same as the state of *v* after *primary_expression*.</span></span>
*  <span data-ttu-id="b645a-362">Для выражения создания объекта, состояние определенного присваивания *v* перед *arg1* совпадает со значением состояния *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-362">For an object creation expression, the definite assignment state of *v* before *arg1* is the same as the state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-363">Для каждого аргумента *argi*, состояние определенного присваивания *v* после *argi* определяется правилами обычным выражением, пропуская любой `ref` или `out`модификаторы.</span><span class="sxs-lookup"><span data-stu-id="b645a-363">For each argument *argi*, the definite assignment state of *v* after *argi* is determined by the normal expression rules, ignoring any `ref` or `out` modifiers.</span></span>
*  <span data-ttu-id="b645a-364">Для каждого аргумента *argi* для любого *я* больше единицы, состояние определенного присваивания *v* перед *argi* совпадает со значением состояния *v* после предыдущего *arg*.</span><span class="sxs-lookup"><span data-stu-id="b645a-364">For each argument *argi* for any *i* greater than one, the definite assignment state of *v* before *argi* is the same as the state of *v* after the previous *arg*.</span></span>
*  <span data-ttu-id="b645a-365">Если переменная *v* передается в качестве `out` аргумента (т. е. аргумент формы `out v`) в любом из аргументов, а затем состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-365">If the variable *v* is passed as an `out` argument (i.e., an argument of the form `out v`) in any of the arguments, then the state of *v* after *expr* is definitely assigned.</span></span> <span data-ttu-id="b645a-366">В противном случае; состояние *v* после *expr* совпадает со значением состояния *v* после *argN*.</span><span class="sxs-lookup"><span data-stu-id="b645a-366">Otherwise; the state of *v* after *expr* is the same as the state of *v* after *argN*.</span></span>
*  <span data-ttu-id="b645a-367">Для инициализаторов массива ([выражениях создания массива](expressions.md#array-creation-expressions)), инициализаторы объектов ([инициализаторы объектов](expressions.md#object-initializers)), инициализаторы коллекций ([инициализаторы](expressions.md#collection-initializers)) и Инициализаторы анонимных объектов ([выражения создания анонимных объектов](expressions.md#anonymous-object-creation-expressions)), состояние определенного присваивания определяется расширения, определенные на основе этих конструкций.</span><span class="sxs-lookup"><span data-stu-id="b645a-367">For array initializers ([Array creation expressions](expressions.md#array-creation-expressions)), object initializers ([Object initializers](expressions.md#object-initializers)), collection initializers ([Collection initializers](expressions.md#collection-initializers)) and anonymous object initializers ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)), the definite assignment state is determined by the expansion that these constructs are defined in terms of.</span></span>

#### <a name="simple-assignment-expressions"></a><span data-ttu-id="b645a-368">Простые выражения присваивания</span><span class="sxs-lookup"><span data-stu-id="b645a-368">Simple assignment expressions</span></span>

<span data-ttu-id="b645a-369">Для выражения *expr* формы `w = expr_rhs`:</span><span class="sxs-lookup"><span data-stu-id="b645a-369">For an expression *expr* of the form `w = expr_rhs`:</span></span>

*  <span data-ttu-id="b645a-370">Состояние определенного присваивания *v* перед *expr_rhs* совпадает со значением состояния определенного присваивания *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-370">The definite assignment state of *v* before *expr_rhs* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-371">Состояние определенного присваивания *v* после *expr* определяется:</span><span class="sxs-lookup"><span data-stu-id="b645a-371">The definite assignment state of *v* after *expr* is determined by:</span></span>
   * <span data-ttu-id="b645a-372">Если *w* — это та же переменная, как *v*, состояние определенного присваивания переменной *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-372">If *w* is the same variable as *v*, then the definite assignment state of *v* after *expr* is definitely assigned.</span></span>
   * <span data-ttu-id="b645a-373">В противном случае, если назначение происходит в конструкторе экземпляра типа структуры, если *w* имеет доступ к свойству, обозначающий автоматически реализуемого свойства *P* конструируемого экземпляра и *v* является скрытым резервное поле *P*, состояние определенного присваивания переменной *v* после *expr* определенно назначить.</span><span class="sxs-lookup"><span data-stu-id="b645a-373">Otherwise, if the assignment occurs within the instance constructor of a struct type, if *w* is a property access designating an automatically implemented property *P* on the instance being constructed and *v* is the hidden backing field of *P*, then the definite assignment state of *v* after *expr* is definitely assigned.</span></span>
   * <span data-ttu-id="b645a-374">В противном случае состояние определенного присваивания *v* после *expr* совпадает со значением состояния определенного присваивания *v* после *expr_rhs*.</span><span class="sxs-lookup"><span data-stu-id="b645a-374">Otherwise, the definite assignment state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_rhs*.</span></span>

#### <a name="-conditional-and-expressions"></a><span data-ttu-id="b645a-375">& & (условный оператор AND) выражения</span><span class="sxs-lookup"><span data-stu-id="b645a-375">&& (conditional AND) expressions</span></span>

<span data-ttu-id="b645a-376">Для выражения *expr* формы `expr_first && expr_second`:</span><span class="sxs-lookup"><span data-stu-id="b645a-376">For an expression *expr* of the form `expr_first && expr_second`:</span></span>

*  <span data-ttu-id="b645a-377">Состояние определенного присваивания *v* перед *expr_first* совпадает со значением состояния определенного присваивания *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-377">The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-378">Состояние определенного присваивания *v* перед *expr_second* определенно присвоенной, если состояние *v* после *expr_first* либо определенно присвоенной или «определенно присвоенной после выражения true».</span><span class="sxs-lookup"><span data-stu-id="b645a-378">The definite assignment state of *v* before *expr_second* is definitely assigned if the state of *v* after *expr_first* is either definitely assigned or "definitely assigned after true expression".</span></span> <span data-ttu-id="b645a-379">В противном случае он не назначается явно.</span><span class="sxs-lookup"><span data-stu-id="b645a-379">Otherwise, it is not definitely assigned.</span></span>
*  <span data-ttu-id="b645a-380">Состояние определенного присваивания *v* после *expr* определяется:</span><span class="sxs-lookup"><span data-stu-id="b645a-380">The definite assignment state of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b645a-381">Если *expr_first* является константным выражением со значением `false`, состояние определенного присваивания переменной *v* после *expr* совпадает со значением определенного присваивания состояние *v* после *expr_first*.</span><span class="sxs-lookup"><span data-stu-id="b645a-381">If *expr_first* is a constant expression with the value `false`, then the definite assignment state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_first*.</span></span>
    * <span data-ttu-id="b645a-382">В противном случае, если состояние *v* после *expr_first* является определенно присвоенной, то состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-382">Otherwise, if the state of *v* after *expr_first* is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b645a-383">В противном случае, если состояние *v* после *expr_second* определенно присвоенной и состояние *v* после *expr_first* определенно « назначенные после выражения false», а затем состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-383">Otherwise, if the state of *v* after *expr_second* is definitely assigned, and the state of *v* after *expr_first* is "definitely assigned after false expression", then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b645a-384">В противном случае, если состояние *v* после *expr_second* определенно присвоенной или «определенно присвоенной после значение true, выражение», а затем состояние *v* после  *expr* «присваивается определенным образом после выражения true».</span><span class="sxs-lookup"><span data-stu-id="b645a-384">Otherwise, if the state of *v* after *expr_second* is definitely assigned or "definitely assigned after true expression", then the state of *v* after *expr* is "definitely assigned after true expression".</span></span>
    * <span data-ttu-id="b645a-385">В противном случае, если состояние *v* после *expr_first* «определенно присвоенной после выражения false», а состояние *v* после *expr_second* «определенно присвоенной после выражения false», то состояние *v* после *expr* «присваивается определенным образом после выражения false».</span><span class="sxs-lookup"><span data-stu-id="b645a-385">Otherwise, if the state of *v* after *expr_first* is "definitely assigned after false expression", and the state of *v* after *expr_second* is "definitely assigned after false expression", then the state of *v* after *expr* is "definitely assigned after false expression".</span></span>
    * <span data-ttu-id="b645a-386">В противном случае состояние *v* после *expr* определенно не назначается.</span><span class="sxs-lookup"><span data-stu-id="b645a-386">Otherwise, the state of *v* after *expr* is not definitely assigned.</span></span>

<span data-ttu-id="b645a-387">В примере</span><span class="sxs-lookup"><span data-stu-id="b645a-387">In the example</span></span>
```csharp
class A
{
    static void F(int x, int y) {
        int i;
        if (x >= 0 && (i = y) >= 0) {
            // i definitely assigned
        }
        else {
            // i not definitely assigned
        }
        // i not definitely assigned
    }
}
```
<span data-ttu-id="b645a-388">переменная `i` считается определенно присвоенной в одном из внедренных операторов `if` инструкции, но не в другой.</span><span class="sxs-lookup"><span data-stu-id="b645a-388">the variable `i` is considered definitely assigned in one of the embedded statements of an `if` statement but not in the other.</span></span> <span data-ttu-id="b645a-389">В `if` инструкция в методе `F`, переменная `i` определенно присвоенной первый внедренный оператор, поскольку выполнение выражения `(i = y)` всегда предшествует выполнению этого внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="b645a-389">In the `if` statement in method `F`, the variable `i` is definitely assigned in the first embedded statement because execution of the expression `(i = y)` always precedes execution of this embedded statement.</span></span> <span data-ttu-id="b645a-390">Напротив, переменная `i` не является определенно присвоенной во втором операторе внедренных, так как `x >= 0` может завершиться с итогом false, приводит к переменной `i` не назначены.</span><span class="sxs-lookup"><span data-stu-id="b645a-390">In contrast, the variable `i` is not definitely assigned in the second embedded statement, since `x >= 0` might have tested false, resulting in the variable `i` being unassigned.</span></span>

#### <a name="-conditional-or-expressions"></a><span data-ttu-id="b645a-391">|| (условный оператор OR) выражения</span><span class="sxs-lookup"><span data-stu-id="b645a-391">|| (conditional OR) expressions</span></span>

<span data-ttu-id="b645a-392">Для выражения *expr* формы `expr_first || expr_second`:</span><span class="sxs-lookup"><span data-stu-id="b645a-392">For an expression *expr* of the form `expr_first || expr_second`:</span></span>

*  <span data-ttu-id="b645a-393">Состояние определенного присваивания *v* перед *expr_first* совпадает со значением состояния определенного присваивания *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-393">The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-394">Состояние определенного присваивания *v* перед *expr_second* определенно присвоенной, если состояние *v* после *expr_first* либо определенно присвоенной или «определенно присвоенной после выражения false».</span><span class="sxs-lookup"><span data-stu-id="b645a-394">The definite assignment state of *v* before *expr_second* is definitely assigned if the state of *v* after *expr_first* is either definitely assigned or "definitely assigned after false expression".</span></span> <span data-ttu-id="b645a-395">В противном случае он не назначается явно.</span><span class="sxs-lookup"><span data-stu-id="b645a-395">Otherwise, it is not definitely assigned.</span></span>
*  <span data-ttu-id="b645a-396">Определенного присваивания переменной *v* после *expr* определяется:</span><span class="sxs-lookup"><span data-stu-id="b645a-396">The definite assignment statement of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b645a-397">Если *expr_first* является константным выражением со значением `true`, состояние определенного присваивания переменной *v* после *expr* совпадает со значением определенного присваивания состояние *v* после *expr_first*.</span><span class="sxs-lookup"><span data-stu-id="b645a-397">If *expr_first* is a constant expression with the value `true`, then the definite assignment state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_first*.</span></span>
    * <span data-ttu-id="b645a-398">В противном случае, если состояние *v* после *expr_first* является определенно присвоенной, то состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-398">Otherwise, if the state of *v* after *expr_first* is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b645a-399">В противном случае, если состояние *v* после *expr_second* определенно присвоенной и состояние *v* после *expr_first* определенно « назначенные после выражения true», а затем состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-399">Otherwise, if the state of *v* after *expr_second* is definitely assigned, and the state of *v* after *expr_first* is "definitely assigned after true expression", then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b645a-400">В противном случае, если состояние *v* после *expr_second* определенно присвоенной или «определенно присвоенной после выражения false», а затем состояние *v* после *expr* «присваивается определенным образом после выражения false».</span><span class="sxs-lookup"><span data-stu-id="b645a-400">Otherwise, if the state of *v* after *expr_second* is definitely assigned or "definitely assigned after false expression", then the state of *v* after *expr* is "definitely assigned after false expression".</span></span>
    * <span data-ttu-id="b645a-401">В противном случае, если состояние *v* после *expr_first* «определенно присвоенной после выражения true», а состояние *v* после *expr_second*«определенно присвоенной после выражения true», то состояние *v* после *expr* «присваивается определенным образом после выражения true».</span><span class="sxs-lookup"><span data-stu-id="b645a-401">Otherwise, if the state of *v* after *expr_first* is "definitely assigned after true expression", and the state of *v* after *expr_second* is "definitely assigned after true expression", then the state of *v* after *expr* is "definitely assigned after true expression".</span></span>
    * <span data-ttu-id="b645a-402">В противном случае состояние *v* после *expr* определенно не назначается.</span><span class="sxs-lookup"><span data-stu-id="b645a-402">Otherwise, the state of *v* after *expr* is not definitely assigned.</span></span>

<span data-ttu-id="b645a-403">В примере</span><span class="sxs-lookup"><span data-stu-id="b645a-403">In the example</span></span>
```csharp
class A
{
    static void G(int x, int y) {
        int i;
        if (x >= 0 || (i = y) >= 0) {
            // i not definitely assigned
        }
        else {
            // i definitely assigned
        }
        // i not definitely assigned
    }
}
```
<span data-ttu-id="b645a-404">переменная `i` считается определенно присвоенной в одном из внедренных операторов `if` инструкции, но не в другой.</span><span class="sxs-lookup"><span data-stu-id="b645a-404">the variable `i` is considered definitely assigned in one of the embedded statements of an `if` statement but not in the other.</span></span> <span data-ttu-id="b645a-405">В `if` инструкция в методе `G`, переменная `i` определенно присвоенной второй внедренный оператор, поскольку выполнение выражения `(i = y)` всегда предшествует выполнению этого внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="b645a-405">In the `if` statement in method `G`, the variable `i` is definitely assigned in the second embedded statement because execution of the expression `(i = y)` always precedes execution of this embedded statement.</span></span> <span data-ttu-id="b645a-406">Напротив, переменная `i` не является определенно присвоенной в первом внедренный оператор, поскольку `x >= 0` может завершиться с итогом значение true, приводит к переменной `i` не назначены.</span><span class="sxs-lookup"><span data-stu-id="b645a-406">In contrast, the variable `i` is not definitely assigned in the first embedded statement, since `x >= 0` might have tested true, resulting in the variable `i` being unassigned.</span></span>

#### <a name="-logical-negation-expressions"></a><span data-ttu-id="b645a-407">!</span><span class="sxs-lookup"><span data-stu-id="b645a-407">!</span></span> <span data-ttu-id="b645a-408">выражения (логическое отрицание)</span><span class="sxs-lookup"><span data-stu-id="b645a-408">(logical negation) expressions</span></span>

<span data-ttu-id="b645a-409">Для выражения *expr* формы `! expr_operand`:</span><span class="sxs-lookup"><span data-stu-id="b645a-409">For an expression *expr* of the form `! expr_operand`:</span></span>

*  <span data-ttu-id="b645a-410">Состояние определенного присваивания *v* перед *expr_operand* совпадает со значением состояния определенного присваивания *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-410">The definite assignment state of *v* before *expr_operand* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-411">Состояние определенного присваивания *v* после *expr* определяется:</span><span class="sxs-lookup"><span data-stu-id="b645a-411">The definite assignment state of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b645a-412">Если состояние *v* после \* expr_operand \* является определенно присвоенной, то состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-412">If the state of *v* after \*expr_operand \*is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b645a-413">Если состояние *v* после \* expr_operand \* не является определенно присвоенной, то состояние *v* после *expr* определенно не назначается.</span><span class="sxs-lookup"><span data-stu-id="b645a-413">If the state of *v* after \*expr_operand \*is not definitely assigned, then the state of *v* after *expr* is not definitely assigned.</span></span>
    * <span data-ttu-id="b645a-414">Если состояние *v* после \* expr_operand \* «определенно присвоенной после выражения false», то состояние *v* после *expr* «присваивается определенным образом после true выражение».</span><span class="sxs-lookup"><span data-stu-id="b645a-414">If the state of *v* after \*expr_operand \*is "definitely assigned after false expression", then the state of *v* after *expr* is "definitely assigned after true expression".</span></span>
    * <span data-ttu-id="b645a-415">Если состояние *v* после \* expr_operand \* «определенно присвоенной после выражения true», то состояние *v* после *expr* «присваивается определенным образом после false выражение».</span><span class="sxs-lookup"><span data-stu-id="b645a-415">If the state of *v* after \*expr_operand \*is "definitely assigned after true expression", then the state of *v* after *expr* is "definitely assigned after false expression".</span></span>

#### <a name="-null-coalescing-expressions"></a><span data-ttu-id="b645a-416">??</span><span class="sxs-lookup"><span data-stu-id="b645a-416">??</span></span> <span data-ttu-id="b645a-417">выражения (нулем)</span><span class="sxs-lookup"><span data-stu-id="b645a-417">(null coalescing) expressions</span></span>

<span data-ttu-id="b645a-418">Для выражения *expr* формы `expr_first ?? expr_second`:</span><span class="sxs-lookup"><span data-stu-id="b645a-418">For an expression *expr* of the form `expr_first ?? expr_second`:</span></span>

*  <span data-ttu-id="b645a-419">Состояние определенного присваивания *v* перед *expr_first* совпадает со значением состояния определенного присваивания *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-419">The definite assignment state of *v* before *expr_first* is the same as the definite assignment state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-420">Состояние определенного присваивания *v* перед *expr_second* совпадает со значением состояния определенного присваивания *v* после *expr_first*.</span><span class="sxs-lookup"><span data-stu-id="b645a-420">The definite assignment state of *v* before *expr_second* is the same as the definite assignment state of *v* after *expr_first*.</span></span>
*  <span data-ttu-id="b645a-421">Определенного присваивания переменной *v* после *expr* определяется:</span><span class="sxs-lookup"><span data-stu-id="b645a-421">The definite assignment statement of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b645a-422">Если *expr_first* является константным выражением ([константные выражения](expressions.md#constant-expressions)) со значением null, то состояние *v* после *expr* совпадает состоянию *v* после *expr_second*.</span><span class="sxs-lookup"><span data-stu-id="b645a-422">If *expr_first* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) with value null, then the the state of *v* after *expr* is the same as the state of *v* after *expr_second*.</span></span>
*  <span data-ttu-id="b645a-423">В противном случае состояние *v* после *expr* совпадает со значением состояния определенного присваивания *v* после *expr_first*.</span><span class="sxs-lookup"><span data-stu-id="b645a-423">Otherwise, the state of *v* after *expr* is the same as the definite assignment state of *v* after *expr_first*.</span></span>

#### <a name="-conditional-expressions"></a><span data-ttu-id="b645a-424">?: (условный) выражения</span><span class="sxs-lookup"><span data-stu-id="b645a-424">?: (conditional) expressions</span></span>

<span data-ttu-id="b645a-425">Для выражения *expr* формы `expr_cond ? expr_true : expr_false`:</span><span class="sxs-lookup"><span data-stu-id="b645a-425">For an expression *expr* of the form `expr_cond ? expr_true : expr_false`:</span></span>

*  <span data-ttu-id="b645a-426">Состояние определенного присваивания *v* перед *expr_cond* совпадает со значением состояния *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-426">The definite assignment state of *v* before *expr_cond* is the same as the state of *v* before *expr*.</span></span>
*  <span data-ttu-id="b645a-427">Состояние определенного присваивания *v* перед *expr_true* является определенно присвоенной только в том случае, если содержит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="b645a-427">The definite assignment state of *v* before *expr_true* is definitely assigned if and only if one of the following holds:</span></span>
    * <span data-ttu-id="b645a-428">*expr_cond* является константным выражением со значением `false`</span><span class="sxs-lookup"><span data-stu-id="b645a-428">*expr_cond* is a constant expression with the value `false`</span></span>
    * <span data-ttu-id="b645a-429">состояние *v* после *expr_cond* имеет определенно присвоенной или «определенно назначены после выражения true».</span><span class="sxs-lookup"><span data-stu-id="b645a-429">the state of *v* after *expr_cond* is definitely assigned or "definitely assigned after true expression".</span></span>
*  <span data-ttu-id="b645a-430">Состояние определенного присваивания *v* перед *expr_false* является определенно присвоенной только в том случае, если содержит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="b645a-430">The definite assignment state of *v* before *expr_false* is definitely assigned if and only if one of the following holds:</span></span>
    * <span data-ttu-id="b645a-431">*expr_cond* является константным выражением со значением `true`</span><span class="sxs-lookup"><span data-stu-id="b645a-431">*expr_cond* is a constant expression with the value `true`</span></span>
*  <span data-ttu-id="b645a-432">состояние *v* после *expr_cond* имеет определенно присвоенной или «определенно присвоенной после выражения false».</span><span class="sxs-lookup"><span data-stu-id="b645a-432">the state of *v* after *expr_cond* is definitely assigned or "definitely assigned after false expression".</span></span>
*  <span data-ttu-id="b645a-433">Состояние определенного присваивания *v* после *expr* определяется:</span><span class="sxs-lookup"><span data-stu-id="b645a-433">The definite assignment state of *v* after *expr* is determined by:</span></span>
    * <span data-ttu-id="b645a-434">Если *expr_cond* является константным выражением ([константные выражения](expressions.md#constant-expressions)) со значением `true` состояние переменной *v* после *expr* совпадает со значением состояния *v* после *expr_true*.</span><span class="sxs-lookup"><span data-stu-id="b645a-434">If *expr_cond* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) with value `true` then the state of *v* after *expr* is the same as the state of *v* after *expr_true*.</span></span>
    * <span data-ttu-id="b645a-435">В противном случае, если *expr_cond* является константным выражением ([константные выражения](expressions.md#constant-expressions)) со значением `false` состояние переменной *v* после *expr* совпадает со значением состояния *v* после *expr_false*.</span><span class="sxs-lookup"><span data-stu-id="b645a-435">Otherwise, if *expr_cond* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) with value `false` then the state of *v* after *expr* is the same as the state of *v* after *expr_false*.</span></span>
    * <span data-ttu-id="b645a-436">В противном случае, если состояние *v* после *expr_true* присваивается определенным образом и состояние *v* после *expr_false* определенно назначена, состояние *v* после *expr* присваивается определенным образом.</span><span class="sxs-lookup"><span data-stu-id="b645a-436">Otherwise, if the state of *v* after *expr_true* is definitely assigned and the state of *v* after *expr_false* is definitely assigned, then the state of *v* after *expr* is definitely assigned.</span></span>
    * <span data-ttu-id="b645a-437">В противном случае состояние *v* после *expr* определенно не назначается.</span><span class="sxs-lookup"><span data-stu-id="b645a-437">Otherwise, the state of *v* after *expr* is not definitely assigned.</span></span>

#### <a name="anonymous-functions"></a><span data-ttu-id="b645a-438">Анонимные функции</span><span class="sxs-lookup"><span data-stu-id="b645a-438">Anonymous functions</span></span>

<span data-ttu-id="b645a-439">Для *lambda_expression* или *anonymous_method_expression* *expr* с текстом (либо *блок* или *выражение* ) *текст*:</span><span class="sxs-lookup"><span data-stu-id="b645a-439">For a *lambda_expression* or *anonymous_method_expression* *expr* with a body (either *block* or *expression*) *body*:</span></span>

*  <span data-ttu-id="b645a-440">Состояние определенного присваивания внешней переменной *v* перед *текст* совпадает со значением состояния *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-440">The definite assignment state of an outer variable *v* before *body* is the same as the state of *v* before *expr*.</span></span> <span data-ttu-id="b645a-441">То есть состояние определенного присваивания внешних переменных наследуется из контекста анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="b645a-441">That is, definite assignment state of outer variables is inherited from the context of the anonymous function.</span></span>
*  <span data-ttu-id="b645a-442">Состояние определенного присваивания внешней переменной *v* после *expr* совпадает со значением состояния *v* перед *expr*.</span><span class="sxs-lookup"><span data-stu-id="b645a-442">The definite assignment state of an outer variable *v* after *expr* is the same as the state of *v* before *expr*.</span></span>

<span data-ttu-id="b645a-443">Пример</span><span class="sxs-lookup"><span data-stu-id="b645a-443">The example</span></span>
```csharp
delegate bool Filter(int i);

void F() {
    int max;

    // Error, max is not definitely assigned
    Filter f = (int n) => n < max;

    max = 5;
    DoWork(f);
}
```
<span data-ttu-id="b645a-444">вызывает ошибку времени компиляции с момента `max` не является определенно присвоенной где объявлен анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="b645a-444">generates a compile-time error since `max` is not definitely assigned where the anonymous function is declared.</span></span> <span data-ttu-id="b645a-445">Пример</span><span class="sxs-lookup"><span data-stu-id="b645a-445">The example</span></span>
```csharp
delegate void D();

void F() {
    int n;
    D d = () => { n = 1; };

    d();

    // Error, n is not definitely assigned
    Console.WriteLine(n);
}
```
<span data-ttu-id="b645a-446">также вызывает ошибку времени компиляции с момента назначения `n` в анонимной функции не влияет на состояние определенного присваивания `n` вне анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="b645a-446">also generates a compile-time error since the assignment to `n` in the anonymous function has no affect on the definite assignment state of `n` outside the anonymous function.</span></span>

## <a name="variable-references"></a><span data-ttu-id="b645a-447">Ссылки на переменные</span><span class="sxs-lookup"><span data-stu-id="b645a-447">Variable references</span></span>

<span data-ttu-id="b645a-448">Объект *variable_reference* — *выражение* , классифицируется как переменная.</span><span class="sxs-lookup"><span data-stu-id="b645a-448">A *variable_reference* is an *expression* that is classified as a variable.</span></span> <span data-ttu-id="b645a-449">Объект *variable_reference* обозначает место хранения, может осуществляться как получить текущее значение и сохранить новое значение.</span><span class="sxs-lookup"><span data-stu-id="b645a-449">A *variable_reference* denotes a storage location that can be accessed both to fetch the current value and to store a new value.</span></span>

```antlr
variable_reference
    : expression
    ;
```

<span data-ttu-id="b645a-450">В C и C++ *variable_reference* называется *lvalue*.</span><span class="sxs-lookup"><span data-stu-id="b645a-450">In C and C++, a *variable_reference* is known as an *lvalue*.</span></span>

## <a name="atomicity-of-variable-references"></a><span data-ttu-id="b645a-451">Атомарность ссылок на переменные</span><span class="sxs-lookup"><span data-stu-id="b645a-451">Atomicity of variable references</span></span>

<span data-ttu-id="b645a-452">Операции чтения и записи из следующих типов данных являются атомарными: `bool`, `char`, `byte`, `sbyte`, `short`, `ushort`, `uint`, `int`, `float`и ссылочные типы.</span><span class="sxs-lookup"><span data-stu-id="b645a-452">Reads and writes of the following data types are atomic: `bool`, `char`, `byte`, `sbyte`, `short`, `ushort`, `uint`, `int`, `float`, and reference types.</span></span> <span data-ttu-id="b645a-453">Кроме того чтение и запись типов перечисления с базовым типом, в списке выше также являются атомарными.</span><span class="sxs-lookup"><span data-stu-id="b645a-453">In addition, reads and writes of enum types with an underlying type in the previous list are also atomic.</span></span> <span data-ttu-id="b645a-454">Выполняет чтение и запись других типов, включая `long`, `ulong`, `double`, и `decimal`, а также определяемые пользователем типы, не гарантируется атомарным.</span><span class="sxs-lookup"><span data-stu-id="b645a-454">Reads and writes of other types, including `long`, `ulong`, `double`, and `decimal`, as well as user-defined types, are not guaranteed to be atomic.</span></span> <span data-ttu-id="b645a-455">Помимо функций библиотеки, предназначенных для этой цели нет никакой гарантии из атомарных чтения, изменения и записи, такие как в случае инкремента или декремента.</span><span class="sxs-lookup"><span data-stu-id="b645a-455">Aside from the library functions designed for that purpose, there is no guarantee of atomic read-modify-write, such as in the case of increment or decrement.</span></span>

