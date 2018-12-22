# <a name="statements"></a><span data-ttu-id="682e2-101">Операторы</span><span class="sxs-lookup"><span data-stu-id="682e2-101">Statements</span></span>

<span data-ttu-id="682e2-102">C# предоставляет широкий набор инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-102">C# provides a variety of statements.</span></span> <span data-ttu-id="682e2-103">Большинство из них будут знакомы разработчикам, кто имеет опыт программирования на C и C++.</span><span class="sxs-lookup"><span data-stu-id="682e2-103">Most of these statements will be familiar to developers who have programmed in C and C++.</span></span>

```antlr
statement
    : labeled_statement
    | declaration_statement
    | embedded_statement
    ;

embedded_statement
    : block
    | empty_statement
    | expression_statement
    | selection_statement
    | iteration_statement
    | jump_statement
    | try_statement
    | checked_statement
    | unchecked_statement
    | lock_statement
    | using_statement
    | yield_statement
    | embedded_statement_unsafe
    ;
```

<span data-ttu-id="682e2-104">*Embedded_statement* нетерминального символа используется для инструкций, которые отображаются в других инструкциях.</span><span class="sxs-lookup"><span data-stu-id="682e2-104">The *embedded_statement* nonterminal is used for statements that appear within other statements.</span></span> <span data-ttu-id="682e2-105">Использование *embedded_statement* вместо *инструкции* исключает использование операторы объявления и операторы с метками в следующих контекстах.</span><span class="sxs-lookup"><span data-stu-id="682e2-105">The use of *embedded_statement* rather than *statement* excludes the use of declaration statements and labeled statements in these contexts.</span></span> <span data-ttu-id="682e2-106">Пример</span><span class="sxs-lookup"><span data-stu-id="682e2-106">The example</span></span>
```csharp
void F(bool b) {
    if (b)
        int i = 44;
}
```
<span data-ttu-id="682e2-107">приводит к ошибке времени компиляции, так как `if` инструкция требует *embedded_statement* вместо *инструкции* для его Если ветвь.</span><span class="sxs-lookup"><span data-stu-id="682e2-107">results in a compile-time error because an `if` statement requires an *embedded_statement* rather than a *statement* for its if branch.</span></span> <span data-ttu-id="682e2-108">Если этот код был разрешен, то переменная `i` должна быть объявлена, но никогда не может быть использована.</span><span class="sxs-lookup"><span data-stu-id="682e2-108">If this code were permitted, then the variable `i` would be declared, but it could never be used.</span></span> <span data-ttu-id="682e2-109">Тем не менее, поместив `i`объявления в блоке, пример является допустимым.</span><span class="sxs-lookup"><span data-stu-id="682e2-109">Note, however, that by placing `i`'s declaration in a block, the example is valid.</span></span>

## <a name="end-points-and-reachability"></a><span data-ttu-id="682e2-110">Конечные точки и доступность</span><span class="sxs-lookup"><span data-stu-id="682e2-110">End points and reachability</span></span>

<span data-ttu-id="682e2-111">Каждая инструкция имеет ***конечная точка***.</span><span class="sxs-lookup"><span data-stu-id="682e2-111">Every statement has an ***end point***.</span></span> <span data-ttu-id="682e2-112">Интуитивно понятно конечную точку инструкции — это расположение, в который следует сразу за инструкцию.</span><span class="sxs-lookup"><span data-stu-id="682e2-112">In intuitive terms, the end point of a statement is the location that immediately follows the statement.</span></span> <span data-ttu-id="682e2-113">Правила выполнения составных операторов (инструкции, содержащие внедренные операторы) укажите действие, выполняемое, когда управление достигает конечной точки внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-113">The execution rules for composite statements (statements that contain embedded statements) specify the action that is taken when control reaches the end point of an embedded statement.</span></span> <span data-ttu-id="682e2-114">Например когда управление достигает конечной точки оператор в блоке, управление передается следующему оператору в блоке.</span><span class="sxs-lookup"><span data-stu-id="682e2-114">For example, when control reaches the end point of a statement in a block, control is transferred to the next statement in the block.</span></span>

<span data-ttu-id="682e2-115">Если возможно, оператор может получить доступ в процессе выполнения, инструкция считается ***доступен***.</span><span class="sxs-lookup"><span data-stu-id="682e2-115">If a statement can possibly be reached by execution, the statement is said to be ***reachable***.</span></span> <span data-ttu-id="682e2-116">И наоборот, если есть вероятность того, что инструкция будет выполняться, инструкция считается ***недоступен***.</span><span class="sxs-lookup"><span data-stu-id="682e2-116">Conversely, if there is no possibility that a statement will be executed, the statement is said to be ***unreachable***.</span></span>

<span data-ttu-id="682e2-117">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-117">In the example</span></span>
```csharp
void F() {
    Console.WriteLine("reachable");
    goto Label;
    Console.WriteLine("unreachable");
    Label:
    Console.WriteLine("reachable");
}
```
<span data-ttu-id="682e2-118">Второй вызов `Console.WriteLine` недоступен, так как вероятность того, что инструкция будет выполняться.</span><span class="sxs-lookup"><span data-stu-id="682e2-118">the second invocation of `Console.WriteLine` is unreachable because there is no possibility that the statement will be executed.</span></span>

<span data-ttu-id="682e2-119">Выводится предупреждение, если компилятор определяет, что оператор является недоступным.</span><span class="sxs-lookup"><span data-stu-id="682e2-119">A warning is reported if the compiler determines that a statement is unreachable.</span></span> <span data-ttu-id="682e2-120">Это не рассматривается как ошибка для инструкции будет воспринята как недоступная.</span><span class="sxs-lookup"><span data-stu-id="682e2-120">It is specifically not an error for a statement to be unreachable.</span></span>

<span data-ttu-id="682e2-121">Чтобы определить, доступен ли определенной инструкции или конечной точки, компилятор выполняет анализ потока в соответствии с правилами достижимости, определенные для каждой инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-121">To determine whether a particular statement or end point is reachable, the compiler performs flow analysis according to the reachability rules defined for each statement.</span></span> <span data-ttu-id="682e2-122">Анализ потока учитывает значения константных выражений ([константные выражения](expressions.md#constant-expressions)), управления поведением операторов, но возможные значения Неконстантные выражения не учитываются.</span><span class="sxs-lookup"><span data-stu-id="682e2-122">The flow analysis takes into account the values of constant expressions ([Constant expressions](expressions.md#constant-expressions)) that control the behavior of statements, but the possible values of non-constant expressions are not considered.</span></span> <span data-ttu-id="682e2-123">Другими словами для целей анализа потока управления, неконстантное выражение данного типа считается принимать любое значение этого типа.</span><span class="sxs-lookup"><span data-stu-id="682e2-123">In other words, for purposes of control flow analysis, a non-constant expression of a given type is considered to have any possible value of that type.</span></span>

<span data-ttu-id="682e2-124">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-124">In the example</span></span>
```csharp
void F() {
    const int i = 1;
    if (i == 2) Console.WriteLine("unreachable");
}
```
<span data-ttu-id="682e2-125">Логическое выражение `if` инструкция — это константное выражение, так как оба операнда `==` оператор являются константами.</span><span class="sxs-lookup"><span data-stu-id="682e2-125">the boolean expression of the `if` statement is a constant expression because both operands of the `==` operator are constants.</span></span> <span data-ttu-id="682e2-126">Как константное выражение вычисляется во время компиляции, результатом которого является значение `false`, `Console.WriteLine` вызов считается недоступным.</span><span class="sxs-lookup"><span data-stu-id="682e2-126">As the constant expression is evaluated at compile-time, producing the value `false`, the `Console.WriteLine` invocation is considered unreachable.</span></span> <span data-ttu-id="682e2-127">Тем не менее если `i` изменяется на быть локальной переменной</span><span class="sxs-lookup"><span data-stu-id="682e2-127">However, if `i` is changed to be a local variable</span></span>
```csharp
void F() {
    int i = 1;
    if (i == 2) Console.WriteLine("reachable");
}
```
<span data-ttu-id="682e2-128">`Console.WriteLine` вызов считается доступным, несмотря на то что на самом деле он никогда не выполняется.</span><span class="sxs-lookup"><span data-stu-id="682e2-128">the `Console.WriteLine` invocation is considered reachable, even though, in reality, it will never be executed.</span></span>

<span data-ttu-id="682e2-129">*Блок* функции члена всегда считается доступным.</span><span class="sxs-lookup"><span data-stu-id="682e2-129">The *block* of a function member is always considered reachable.</span></span> <span data-ttu-id="682e2-130">Последовательно применяя правила достижимости каждый оператор в блоке, можно определить достижимость любого конкретного оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-130">By successively evaluating the reachability rules of each statement in a block, the reachability of any given statement can be determined.</span></span>

<span data-ttu-id="682e2-131">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-131">In the example</span></span>
```csharp
void F(int x) {
    Console.WriteLine("start");
    if (x < 0) Console.WriteLine("negative");
}
```
<span data-ttu-id="682e2-132">Доступность второго `Console.WriteLine` определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-132">the reachability of the second `Console.WriteLine` is determined as follows:</span></span>

*  <span data-ttu-id="682e2-133">Первый `Console.WriteLine` оператор выражения доступен поскольку блок `F` доступен метод.</span><span class="sxs-lookup"><span data-stu-id="682e2-133">The first `Console.WriteLine` expression statement is reachable because the block of the `F` method is reachable.</span></span>
*  <span data-ttu-id="682e2-134">Конечная точка первого `Console.WriteLine` оператор выражения доступен, поскольку сам оператор достижим.</span><span class="sxs-lookup"><span data-stu-id="682e2-134">The end point of the first `Console.WriteLine` expression statement is reachable because that statement is reachable.</span></span>
*  <span data-ttu-id="682e2-135">`if` Оператор достижим из-за окончания первого `Console.WriteLine` оператор выражения доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-135">The `if` statement is reachable because the end point of the first `Console.WriteLine` expression statement is reachable.</span></span>
*  <span data-ttu-id="682e2-136">Второй `Console.WriteLine` оператор выражения доступен так как логическое выражение `if` оператор не имеет постоянное значение `false`.</span><span class="sxs-lookup"><span data-stu-id="682e2-136">The second `Console.WriteLine` expression statement is reachable because the boolean expression of the `if` statement does not have the constant value `false`.</span></span>

<span data-ttu-id="682e2-137">Существуют две ситуации, в которых это ошибка времени компиляции для конечной точки инструкции быть доступен:</span><span class="sxs-lookup"><span data-stu-id="682e2-137">There are two situations in which it is a compile-time error for the end point of a statement to be reachable:</span></span>

*  <span data-ttu-id="682e2-138">Так как `switch` инструкция не поддерживает раздел switch, который «проваливания» следующий раздел switch, произошла ошибка во время компиляции, для конечной точки списка операторов раздела switch достижимым.</span><span class="sxs-lookup"><span data-stu-id="682e2-138">Because the `switch` statement does not permit a switch section to "fall through" to the next switch section, it is a compile-time error for the end point of the statement list of a switch section to be reachable.</span></span> <span data-ttu-id="682e2-139">Если эта ошибка возникает, это обычно означает, что, `break` отсутствует инструкция.</span><span class="sxs-lookup"><span data-stu-id="682e2-139">If this error occurs, it is typically an indication that a `break` statement is missing.</span></span>
*  <span data-ttu-id="682e2-140">Это ошибка времени компиляции для конечной точки блока функции-члена, которая вычисляет значение достижимым.</span><span class="sxs-lookup"><span data-stu-id="682e2-140">It is a compile-time error for the end point of the block of a function member that computes a value to be reachable.</span></span> <span data-ttu-id="682e2-141">Если эта ошибка возникает, это обычно означает, что, `return` отсутствует инструкция.</span><span class="sxs-lookup"><span data-stu-id="682e2-141">If this error occurs, it typically is an indication that a `return` statement is missing.</span></span>

## <a name="blocks"></a><span data-ttu-id="682e2-142">Blocks</span><span class="sxs-lookup"><span data-stu-id="682e2-142">Blocks</span></span>

<span data-ttu-id="682e2-143">С помощью *блоков* можно использовать несколько операторов в таких контекстах, где ожидается только один оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-143">A *block* permits multiple statements to be written in contexts where a single statement is allowed.</span></span>

```antlr
block
    : '{' statement_list? '}'
    ;
```

<span data-ttu-id="682e2-144">Объект *блок* состоит из необязательного *statement_list* ([инструкция выводит список](statements.md#statement-lists)), заключенный в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="682e2-144">A *block* consists of an optional *statement_list* ([Statement lists](statements.md#statement-lists)), enclosed in braces.</span></span> <span data-ttu-id="682e2-145">Если указан список операторов, блок считается пустым.</span><span class="sxs-lookup"><span data-stu-id="682e2-145">If the statement list is omitted, the block is said to be empty.</span></span>

<span data-ttu-id="682e2-146">Блок может содержать операторы объявления ([операторы объявления](statements.md#declaration-statements)).</span><span class="sxs-lookup"><span data-stu-id="682e2-146">A block may contain declaration statements ([Declaration statements](statements.md#declaration-statements)).</span></span> <span data-ttu-id="682e2-147">Областью видимости локальной переменной или константы, объявленных в блоке является блоком.</span><span class="sxs-lookup"><span data-stu-id="682e2-147">The scope of a local variable or constant declared in a block is the block.</span></span>

<span data-ttu-id="682e2-148">Блок выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-148">A block is executed as follows:</span></span>

*  <span data-ttu-id="682e2-149">Если блок является пустой, управление передается в конечную точку блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-149">If the block is empty, control is transferred to the end point of the block.</span></span>
*  <span data-ttu-id="682e2-150">Если блок не является пустой, управление передается списка операторов.</span><span class="sxs-lookup"><span data-stu-id="682e2-150">If the block is not empty, control is transferred to the statement list.</span></span> <span data-ttu-id="682e2-151">Если управление достигает конца списка операторов, элемент управления передается в конечную точку блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-151">When and if control reaches the end point of the statement list, control is transferred to the end point of the block.</span></span>

<span data-ttu-id="682e2-152">Список операторов в блоке будет доступен в том случае, если доступен сам блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-152">The statement list of a block is reachable if the block itself is reachable.</span></span>

<span data-ttu-id="682e2-153">Конечная точка блок доступен, если блок является пустой, или если конечная точка списка операторов достижима.</span><span class="sxs-lookup"><span data-stu-id="682e2-153">The end point of a block is reachable if the block is empty or if the end point of the statement list is reachable.</span></span>

<span data-ttu-id="682e2-154">Объект *блок* , содержит один или несколько `yield` инструкций ([оператор yield](statements.md#the-yield-statement)) называется блоком итератора.</span><span class="sxs-lookup"><span data-stu-id="682e2-154">A *block* that contains one or more `yield` statements ([The yield statement](statements.md#the-yield-statement)) is called an iterator block.</span></span> <span data-ttu-id="682e2-155">Блоки итераторов используются для реализации функции-члены как итераторы ([итераторы](classes.md#iterators)).</span><span class="sxs-lookup"><span data-stu-id="682e2-155">Iterator blocks are used to implement function members as iterators ([Iterators](classes.md#iterators)).</span></span> <span data-ttu-id="682e2-156">Некоторые дополнительные ограничения применяются к блокам итератора.</span><span class="sxs-lookup"><span data-stu-id="682e2-156">Some additional restrictions apply to iterator blocks:</span></span>

*  <span data-ttu-id="682e2-157">Произошла ошибка во время компиляции для `return` инструкции в блоке итератора (но `yield return` инструкции, разрешены).</span><span class="sxs-lookup"><span data-stu-id="682e2-157">It is a compile-time error for a `return` statement to appear in an iterator block (but `yield return` statements are permitted).</span></span>
*  <span data-ttu-id="682e2-158">Произошла ошибка во время компиляции для блока итератора должен содержать небезопасный контекст ([небезопасных контекстах](unsafe-code.md#unsafe-contexts)).</span><span class="sxs-lookup"><span data-stu-id="682e2-158">It is a compile-time error for an iterator block to contain an unsafe context ([Unsafe contexts](unsafe-code.md#unsafe-contexts)).</span></span> <span data-ttu-id="682e2-159">Блока итератора всегда определяет безопасный контекст, даже в том случае, если объявление является вложенным в небезопасном контексте.</span><span class="sxs-lookup"><span data-stu-id="682e2-159">An iterator block always defines a safe context, even when its declaration is nested in an unsafe context.</span></span>

### <a name="statement-lists"></a><span data-ttu-id="682e2-160">Список операторов</span><span class="sxs-lookup"><span data-stu-id="682e2-160">Statement lists</span></span>

<span data-ttu-id="682e2-161">Объект ***списка операторов*** состоит из одного или нескольких инструкций, созданных в последовательности.</span><span class="sxs-lookup"><span data-stu-id="682e2-161">A ***statement list*** consists of one or more statements written in sequence.</span></span> <span data-ttu-id="682e2-162">Списки инструкций происходят в *блок*s ([блоки](statements.md#blocks)) и в *switch_block*s ([оператора switch](statements.md#the-switch-statement)).</span><span class="sxs-lookup"><span data-stu-id="682e2-162">Statement lists occur in *block*s ([Blocks](statements.md#blocks)) and in *switch_block*s ([The switch statement](statements.md#the-switch-statement)).</span></span>

```antlr
statement_list
    : statement+
    ;
```

<span data-ttu-id="682e2-163">Список инструкций выполняется путем передачи управления в первой инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-163">A statement list is executed by transferring control to the first statement.</span></span> <span data-ttu-id="682e2-164">Если и элемента управления достигает конечной точки оператора, управление передается оператору, следующему.</span><span class="sxs-lookup"><span data-stu-id="682e2-164">When and if control reaches the end point of a statement, control is transferred to the next statement.</span></span> <span data-ttu-id="682e2-165">Если управление достигает конечной точки последнего выполнения инструкции, элемент управления передается в конечную точку списка операторов.</span><span class="sxs-lookup"><span data-stu-id="682e2-165">When and if control reaches the end point of the last statement, control is transferred to the end point of the statement list.</span></span>

<span data-ttu-id="682e2-166">Инструкции в списке инструкции доступен в том случае, если верно хотя бы одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-166">A statement in a statement list is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="682e2-167">Инструкция является первой инструкцией, а сам список операторов доступна.</span><span class="sxs-lookup"><span data-stu-id="682e2-167">The statement is the first statement and the statement list itself is reachable.</span></span>
*  <span data-ttu-id="682e2-168">Конечная точка предыдущего оператора достижима.</span><span class="sxs-lookup"><span data-stu-id="682e2-168">The end point of the preceding statement is reachable.</span></span>
*  <span data-ttu-id="682e2-169">Оператор является оператором с меткой и метка имеет ссылку на доступную `goto` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-169">The statement is a labeled statement and the label is referenced by a reachable `goto` statement.</span></span>

<span data-ttu-id="682e2-170">Конечная точка списка операторов доступен в том случае, если конечная точка последней инструкции в списке доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-170">The end point of a statement list is reachable if the end point of the last statement in the list is reachable.</span></span>

## <a name="the-empty-statement"></a><span data-ttu-id="682e2-171">Пустая инструкция</span><span class="sxs-lookup"><span data-stu-id="682e2-171">The empty statement</span></span>

<span data-ttu-id="682e2-172">*Empty_statement* не выполняет никаких действий.</span><span class="sxs-lookup"><span data-stu-id="682e2-172">An *empty_statement* does nothing.</span></span>

```antlr
empty_statement
    : ';'
    ;
```

<span data-ttu-id="682e2-173">Пустой оператор используется в том случае, когда нет операций для выполнения в контексте, где требуется оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-173">An empty statement is used when there are no operations to perform in a context where a statement is required.</span></span>

<span data-ttu-id="682e2-174">Выполнение пустого оператора просто передает управление конечной точки инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-174">Execution of an empty statement simply transfers control to the end point of the statement.</span></span> <span data-ttu-id="682e2-175">Таким образом конечная точка пустого оператора достижима, если доступен пустой оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-175">Thus, the end point of an empty statement is reachable if the empty statement is reachable.</span></span>

<span data-ttu-id="682e2-176">Пустой оператор можно использовать при написании `while` инструкции с пустым текстом:</span><span class="sxs-lookup"><span data-stu-id="682e2-176">An empty statement can be used when writing a `while` statement with a null body:</span></span>
```csharp
bool ProcessMessage() {...}

void ProcessMessages() {
    while (ProcessMessage())
        ;
}
```

<span data-ttu-id="682e2-177">Кроме того, пустого оператора можно объявить метку непосредственно перед закрывающим "`}`" блока:</span><span class="sxs-lookup"><span data-stu-id="682e2-177">Also, an empty statement can be used to declare a label just before the closing "`}`" of a block:</span></span>
```csharp
void F() {
    ...
    if (done) goto exit;
    ...
    exit: ;
}
```

## <a name="labeled-statements"></a><span data-ttu-id="682e2-178">Инструкции с метками</span><span class="sxs-lookup"><span data-stu-id="682e2-178">Labeled statements</span></span>

<span data-ttu-id="682e2-179">Объект *labeled_statement* позволяет инструкцию, чтобы иметь префикс в метку.</span><span class="sxs-lookup"><span data-stu-id="682e2-179">A *labeled_statement* permits a statement to be prefixed by a label.</span></span> <span data-ttu-id="682e2-180">Операторы с метками, разрешены в блоках, но не допускаются как внедренные операторы.</span><span class="sxs-lookup"><span data-stu-id="682e2-180">Labeled statements are permitted in blocks, but are not permitted as embedded statements.</span></span>

```antlr
labeled_statement
    : identifier ':' statement
    ;
```

<span data-ttu-id="682e2-181">Оператор с меткой объявляет метку, имя, заданное в *идентификатор*.</span><span class="sxs-lookup"><span data-stu-id="682e2-181">A labeled statement declares a label with the name given by the *identifier*.</span></span> <span data-ttu-id="682e2-182">Областью метки является весь блок, в котором она объявлена, включая вложенные блоки.</span><span class="sxs-lookup"><span data-stu-id="682e2-182">The scope of a label is the whole block in which the label is declared, including any nested blocks.</span></span> <span data-ttu-id="682e2-183">Это ошибка времени компиляции для двух меток с тем же именем, чтобы перекрывающиеся области.</span><span class="sxs-lookup"><span data-stu-id="682e2-183">It is a compile-time error for two labels with the same name to have overlapping scopes.</span></span>

<span data-ttu-id="682e2-184">Метку можно ссылаться из `goto` инструкций ([инструкцию goto](statements.md#the-goto-statement)) в пределах метки.</span><span class="sxs-lookup"><span data-stu-id="682e2-184">A label can be referenced from `goto` statements ([The goto statement](statements.md#the-goto-statement)) within the scope of the label.</span></span> <span data-ttu-id="682e2-185">Это означает, что `goto` инструкций может передать контроль в блоках и из блоков, но не внутрь блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-185">This means that `goto` statements can transfer control within blocks and out of blocks, but never into blocks.</span></span>

<span data-ttu-id="682e2-186">Метки имеют собственную область объявления и не конфликтуют с другими идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="682e2-186">Labels have their own declaration space and do not interfere with other identifiers.</span></span> <span data-ttu-id="682e2-187">Пример</span><span class="sxs-lookup"><span data-stu-id="682e2-187">The example</span></span>
```csharp
int F(int x) {
    if (x >= 0) goto x;
    x = -x;
    x: return x;
}
```
<span data-ttu-id="682e2-188">является допустимым именем, `x` как параметр и метку.</span><span class="sxs-lookup"><span data-stu-id="682e2-188">is valid and uses the name `x` as both a parameter and a label.</span></span>

<span data-ttu-id="682e2-189">Выполнение инструкции с метками в точности соответствует выполнение оператору после метки.</span><span class="sxs-lookup"><span data-stu-id="682e2-189">Execution of a labeled statement corresponds exactly to execution of the statement following the label.</span></span>

<span data-ttu-id="682e2-190">Помимо достижимости в рамках обычного потока управления, оператор с меткой доступен, если метка имеет ссылку на доступную `goto` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-190">In addition to the reachability provided by normal flow of control, a labeled statement is reachable if the label is referenced by a reachable `goto` statement.</span></span> <span data-ttu-id="682e2-191">(Исключение: Если `goto` оператор находится внутри `try` , включающий `finally` блока и оператор с меткой за пределами `try`и конечная точка `finally` блок недоступен, то оператор с меткой недостижим из `goto` инструкции.)</span><span class="sxs-lookup"><span data-stu-id="682e2-191">(Exception: If a `goto` statement is inside a `try` that includes a `finally` block, and the labeled statement is outside the `try`, and the end point of the `finally` block is unreachable, then the labeled statement is not reachable from that `goto` statement.)</span></span>

## <a name="declaration-statements"></a><span data-ttu-id="682e2-192">Инструкции объявления</span><span class="sxs-lookup"><span data-stu-id="682e2-192">Declaration statements</span></span>

<span data-ttu-id="682e2-193">Объект *declaration_statement* объявляет локальную переменную или константу.</span><span class="sxs-lookup"><span data-stu-id="682e2-193">A *declaration_statement* declares a local variable or constant.</span></span> <span data-ttu-id="682e2-194">Операторы объявления разрешены в блоках, но не допускаются как внедренные операторы.</span><span class="sxs-lookup"><span data-stu-id="682e2-194">Declaration statements are permitted in blocks, but are not permitted as embedded statements.</span></span>

```antlr
declaration_statement
    : local_variable_declaration ';'
    | local_constant_declaration ';'
    ;
```

### <a name="local-variable-declarations"></a><span data-ttu-id="682e2-195">Объявления локальных переменных</span><span class="sxs-lookup"><span data-stu-id="682e2-195">Local variable declarations</span></span>

<span data-ttu-id="682e2-196">Объект *local_variable_declaration* объявляет один или несколько локальных переменных.</span><span class="sxs-lookup"><span data-stu-id="682e2-196">A *local_variable_declaration* declares one or more local variables.</span></span>

```antlr
local_variable_declaration
    : local_variable_type local_variable_declarators
    ;

local_variable_type
    : type
    | 'var'
    ;

local_variable_declarators
    : local_variable_declarator
    | local_variable_declarators ',' local_variable_declarator
    ;

local_variable_declarator
    : identifier
    | identifier '=' local_variable_initializer
    ;

local_variable_initializer
    : expression
    | array_initializer
    | local_variable_initializer_unsafe
    ;
```

<span data-ttu-id="682e2-197">*Local_variable_type* из *local_variable_declaration* напрямую указывает тип переменных, представленных в объявлении, либо указывает с идентификатором `var` , Тип неявно определяется инициализатором.</span><span class="sxs-lookup"><span data-stu-id="682e2-197">The *local_variable_type* of a *local_variable_declaration* either directly specifies the type of the variables introduced by the declaration, or indicates with the identifier `var` that the type should be inferred based on an initializer.</span></span> <span data-ttu-id="682e2-198">Тип сопровождается список *local_variable_declarator*s, каждый из которых представляет новую переменную.</span><span class="sxs-lookup"><span data-stu-id="682e2-198">The type is followed by a list of *local_variable_declarator*s, each of which introduces a new variable.</span></span> <span data-ttu-id="682e2-199">Объект *local_variable_declarator* состоит из *идентификатор* , которая содержит название переменной, при желании указав через "`=`" токена и *local_variable_initializer* , задающее начальное значение переменной.</span><span class="sxs-lookup"><span data-stu-id="682e2-199">A *local_variable_declarator* consists of an *identifier* that names the variable, optionally followed by an "`=`" token and a *local_variable_initializer* that gives the initial value of the variable.</span></span>

<span data-ttu-id="682e2-200">В контексте объявления локальной переменной, идентификатор var выступает в качестве контекстно-зависимое ключевое слово ([ключевые слова](lexical-structure.md#keywords)). При *local_variable_type* указывается как `var` и тип с именем `var` — в области, объявление является ***неявно типизированные в объявлении локальной переменной***, тип которого является выводится из типа из соответствующего выражения инициализатора.</span><span class="sxs-lookup"><span data-stu-id="682e2-200">In the context of a local variable declaration, the identifier var acts as a contextual keyword ([Keywords](lexical-structure.md#keywords)).When the *local_variable_type* is specified as `var` and no type named `var` is in scope, the declaration is an ***implicitly typed local variable declaration***, whose type is inferred from the type of the associated initializer expression.</span></span> <span data-ttu-id="682e2-201">Неявно типизированные локальные объявления переменных распространяются следующие ограничения:</span><span class="sxs-lookup"><span data-stu-id="682e2-201">Implicitly typed local variable declarations are subject to the following restrictions:</span></span>

*  <span data-ttu-id="682e2-202">*Local_variable_declaration* не может включать несколько *local_variable_declarator*s.</span><span class="sxs-lookup"><span data-stu-id="682e2-202">The *local_variable_declaration* cannot include multiple *local_variable_declarator*s.</span></span>
*  <span data-ttu-id="682e2-203">*Local_variable_declarator* должен включать *local_variable_initializer*.</span><span class="sxs-lookup"><span data-stu-id="682e2-203">The *local_variable_declarator* must include a *local_variable_initializer*.</span></span>
*  <span data-ttu-id="682e2-204">*Local_variable_initializer* должно быть *выражение*.</span><span class="sxs-lookup"><span data-stu-id="682e2-204">The *local_variable_initializer* must be an *expression*.</span></span>
*  <span data-ttu-id="682e2-205">Инициализатор *выражение* должно иметь тип времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-205">The initializer *expression* must have a compile-time type.</span></span>
*  <span data-ttu-id="682e2-206">Инициализатор *выражение* не может ссылаться на сам объявленной переменной</span><span class="sxs-lookup"><span data-stu-id="682e2-206">The initializer *expression* cannot refer to the declared variable itself</span></span>

<span data-ttu-id="682e2-207">Ниже приведены примеры неправильные объявления неявно типизированных локальных переменных.</span><span class="sxs-lookup"><span data-stu-id="682e2-207">The following are examples of incorrect implicitly typed local variable declarations:</span></span>

```csharp
var x;               // Error, no initializer to infer type from
var y = {1, 2, 3};   // Error, array initializer not permitted
var z = null;        // Error, null does not have a type
var u = x => x + 1;  // Error, anonymous functions do not have a type
var v = v++;         // Error, initializer cannot refer to variable itself
```

<span data-ttu-id="682e2-208">Получено значение локальной переменной в выражение, использующее *simple_name* ([простые имена](expressions.md#simple-names)), и изменения значения локальной переменной с помощью *назначения* () [Операторы присваивания](expressions.md#assignment-operators)).</span><span class="sxs-lookup"><span data-stu-id="682e2-208">The value of a local variable is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)), and the value of a local variable is modified using an *assignment* ([Assignment operators](expressions.md#assignment-operators)).</span></span> <span data-ttu-id="682e2-209">Локальной переменной должен быть явно присвоен ([определенного присваивания](variables.md#definite-assignment)) во всех расположениях, где извлекается ее значение.</span><span class="sxs-lookup"><span data-stu-id="682e2-209">A local variable must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) at each location where its value is obtained.</span></span>

<span data-ttu-id="682e2-210">Локальная переменная, объявленная в области *local_variable_declaration* представляет собой блок, в котором содержится объявление.</span><span class="sxs-lookup"><span data-stu-id="682e2-210">The scope of a local variable declared in a *local_variable_declaration* is the block in which the declaration occurs.</span></span> <span data-ttu-id="682e2-211">Это ошибка для ссылки на локальную переменную в позиции текста, который предшествует *local_variable_declarator* локальной переменной.</span><span class="sxs-lookup"><span data-stu-id="682e2-211">It is an error to refer to a local variable in a textual position that precedes the *local_variable_declarator* of the local variable.</span></span> <span data-ttu-id="682e2-212">В области локальной переменной это ошибка времени компиляции, чтобы объявить другой локальной переменной или константы с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="682e2-212">Within the scope of a local variable, it is a compile-time error to declare another local variable or constant with the same name.</span></span>

<span data-ttu-id="682e2-213">Объявление локальной переменной, объявляется несколько переменных соответствует несколько объявлений одного переменных с одним типом.</span><span class="sxs-lookup"><span data-stu-id="682e2-213">A local variable declaration that declares multiple variables is equivalent to multiple declarations of single variables with the same type.</span></span> <span data-ttu-id="682e2-214">Кроме того использование инициализатора в объявлении локальной переменной в точности соответствует оператора присваивания, который вставляется непосредственно после объявления.</span><span class="sxs-lookup"><span data-stu-id="682e2-214">Furthermore, a variable initializer in a local variable declaration corresponds exactly to an assignment statement that is inserted immediately after the declaration.</span></span>

<span data-ttu-id="682e2-215">Пример</span><span class="sxs-lookup"><span data-stu-id="682e2-215">The example</span></span>
```csharp
void F() {
    int x = 1, y, z = x * 2;
}
```
<span data-ttu-id="682e2-216">в точности соответствует</span><span class="sxs-lookup"><span data-stu-id="682e2-216">corresponds exactly to</span></span>
```csharp
void F() {
    int x; x = 1;
    int y;
    int z; z = x * 2;
}
```

<span data-ttu-id="682e2-217">В неявно типизированной локальной объявление переменной тип объявляемой переменной принимается совпадал с типом выражения, используемого для инициализации переменной.</span><span class="sxs-lookup"><span data-stu-id="682e2-217">In an implicitly typed local variable declaration, the type of the local variable being declared is taken to be the same as the type of the expression used to initialize the variable.</span></span> <span data-ttu-id="682e2-218">Пример:</span><span class="sxs-lookup"><span data-stu-id="682e2-218">For example:</span></span>
```csharp
var i = 5;
var s = "Hello";
var d = 1.0;
var numbers = new int[] {1, 2, 3};
var orders = new Dictionary<int,Order>();
```

<span data-ttu-id="682e2-219">Неявно типизированные локальные объявления переменных выше будут точными эквивалентами следующих явно типизированных объявлений:</span><span class="sxs-lookup"><span data-stu-id="682e2-219">The implicitly typed local variable declarations above are precisely equivalent to the following explicitly typed declarations:</span></span>
```csharp
int i = 5;
string s = "Hello";
double d = 1.0;
int[] numbers = new int[] {1, 2, 3};
Dictionary<int,Order> orders = new Dictionary<int,Order>();
```

### <a name="local-constant-declarations"></a><span data-ttu-id="682e2-220">Локальные объявления констант</span><span class="sxs-lookup"><span data-stu-id="682e2-220">Local constant declarations</span></span>

<span data-ttu-id="682e2-221">Объект *local_constant_declaration* объявляет один или несколько локальных констант.</span><span class="sxs-lookup"><span data-stu-id="682e2-221">A *local_constant_declaration* declares one or more local constants.</span></span>

```antlr
local_constant_declaration
    : 'const' type constant_declarators
    ;

constant_declarators
    : constant_declarator (',' constant_declarator)*
    ;

constant_declarator
    : identifier '=' constant_expression
    ;
```

<span data-ttu-id="682e2-222">*Тип* из *local_constant_declaration* указывает тип констант, представленных в объявлении.</span><span class="sxs-lookup"><span data-stu-id="682e2-222">The *type* of a *local_constant_declaration* specifies the type of the constants introduced by the declaration.</span></span> <span data-ttu-id="682e2-223">Тип сопровождается список *constant_declarator*s, каждый из которых представляет новую константу.</span><span class="sxs-lookup"><span data-stu-id="682e2-223">The type is followed by a list of *constant_declarator*s, each of which introduces a new constant.</span></span> <span data-ttu-id="682e2-224">Объект *constant_declarator* состоит из *идентификатор* которых имена следуют константа "`=`" токена, за которым следует *constant_expression* ([ Константные выражения](expressions.md#constant-expressions)), задающее значение константы.</span><span class="sxs-lookup"><span data-stu-id="682e2-224">A *constant_declarator* consists of an *identifier* that names the constant, followed by an "`=`" token, followed by a *constant_expression* ([Constant expressions](expressions.md#constant-expressions)) that gives the value of the constant.</span></span>

<span data-ttu-id="682e2-225">*Тип* и *constant_expression* объявлении локальной константы должны следовать тем же правилам, что и объявление член константы ([константы](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="682e2-225">The *type* and *constant_expression* of a local constant declaration must follow the same rules as those of a constant member declaration ([Constants](classes.md#constants)).</span></span>

<span data-ttu-id="682e2-226">Значение локальной константы получается в выражение, использующее *simple_name* ([простые имена](expressions.md#simple-names)).</span><span class="sxs-lookup"><span data-stu-id="682e2-226">The value of a local constant is obtained in an expression using a *simple_name* ([Simple names](expressions.md#simple-names)).</span></span>

<span data-ttu-id="682e2-227">Областью локальной константы является блок, в котором содержится объявление.</span><span class="sxs-lookup"><span data-stu-id="682e2-227">The scope of a local constant is the block in which the declaration occurs.</span></span> <span data-ttu-id="682e2-228">Это ошибка для ссылки на локальную константу в позиции текста, который предшествует его *constant_declarator*.</span><span class="sxs-lookup"><span data-stu-id="682e2-228">It is an error to refer to a local constant in a textual position that precedes its *constant_declarator*.</span></span> <span data-ttu-id="682e2-229">В области локальной константы это ошибка времени компиляции, чтобы объявить другой локальной переменной или константы с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="682e2-229">Within the scope of a local constant, it is a compile-time error to declare another local variable or constant with the same name.</span></span>

<span data-ttu-id="682e2-230">Объявление локальной константы, объявляющее несколько констант соответствует несколько объявлений из одной константы с тем же типом.</span><span class="sxs-lookup"><span data-stu-id="682e2-230">A local constant declaration that declares multiple constants is equivalent to multiple declarations of single constants with the same type.</span></span>

## <a name="expression-statements"></a><span data-ttu-id="682e2-231">Инструкции выражений</span><span class="sxs-lookup"><span data-stu-id="682e2-231">Expression statements</span></span>

<span data-ttu-id="682e2-232">*Expression_statement* вычисления данного выражения.</span><span class="sxs-lookup"><span data-stu-id="682e2-232">An *expression_statement* evaluates a given expression.</span></span> <span data-ttu-id="682e2-233">Значение, вычисленное с помощью выражения, если таковые имеются, удаляются.</span><span class="sxs-lookup"><span data-stu-id="682e2-233">The value computed by the expression, if any, is discarded.</span></span>

```antlr
expression_statement
    : statement_expression ';'
    ;

statement_expression
    : invocation_expression
    | null_conditional_invocation_expression
    | object_creation_expression
    | assignment
    | post_increment_expression
    | post_decrement_expression
    | pre_increment_expression
    | pre_decrement_expression
    | await_expression
    ;
```

<span data-ttu-id="682e2-234">Не все выражения разрешены как инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-234">Not all expressions are permitted as statements.</span></span> <span data-ttu-id="682e2-235">В частности, выражения, такие как `x + y` и `x == 1` , просто вычислить значение (в который будут отменены), как операторы не разрешены.</span><span class="sxs-lookup"><span data-stu-id="682e2-235">In particular, expressions such as `x + y` and `x == 1` that merely compute a value (which will be discarded), are not permitted as statements.</span></span>

<span data-ttu-id="682e2-236">Выполнение *expression_statement* вычисляет автономной и затем передает управление конечной точки *expression_statement*.</span><span class="sxs-lookup"><span data-stu-id="682e2-236">Execution of an *expression_statement* evaluates the contained expression and then transfers control to the end point of the *expression_statement*.</span></span> <span data-ttu-id="682e2-237">Конечная точка *expression_statement* доступен, если это *expression_statement* доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-237">The end point of an *expression_statement* is reachable if that *expression_statement* is reachable.</span></span>

## <a name="selection-statements"></a><span data-ttu-id="682e2-238">Операторы выбора</span><span class="sxs-lookup"><span data-stu-id="682e2-238">Selection statements</span></span>

<span data-ttu-id="682e2-239">Операторы выбора выберите один из нескольких возможных вариантов для выполнения на основе значения из выражения.</span><span class="sxs-lookup"><span data-stu-id="682e2-239">Selection statements select one of a number of possible statements for execution based on the value of some expression.</span></span>

```antlr
selection_statement
    : if_statement
    | switch_statement
    ;
```

### <a name="the-if-statement"></a><span data-ttu-id="682e2-240">Если инструкция</span><span class="sxs-lookup"><span data-stu-id="682e2-240">The if statement</span></span>

<span data-ttu-id="682e2-241">`if` Инструкция выбирает оператор для выполнения на основе значения логического выражения.</span><span class="sxs-lookup"><span data-stu-id="682e2-241">The `if` statement selects a statement for execution based on the value of a boolean expression.</span></span>

```antlr
if_statement
    : 'if' '(' boolean_expression ')' embedded_statement
    | 'if' '(' boolean_expression ')' embedded_statement 'else' embedded_statement
    ;
```

<span data-ttu-id="682e2-242">`else` Часть связана с лексически ближайшего предшествующего `if` это разрешается с помощью синтаксиса.</span><span class="sxs-lookup"><span data-stu-id="682e2-242">An `else` part is associated with the lexically nearest preceding `if` that is allowed by the syntax.</span></span> <span data-ttu-id="682e2-243">Таким образом `if` инструкцию для формы</span><span class="sxs-lookup"><span data-stu-id="682e2-243">Thus, an `if` statement of the form</span></span>
```csharp
if (x) if (y) F(); else G();
```
<span data-ttu-id="682e2-244">эквивалентно</span><span class="sxs-lookup"><span data-stu-id="682e2-244">is equivalent to</span></span>
```csharp
if (x) {
    if (y) {
        F();
    }
    else {
        G();
    }
}
```

<span data-ttu-id="682e2-245">`if` Инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-245">An `if` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-246">*Boolean_expression* ([логических выражений](expressions.md#boolean-expressions)) вычисляется.</span><span class="sxs-lookup"><span data-stu-id="682e2-246">The *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)) is evaluated.</span></span>
*  <span data-ttu-id="682e2-247">Если логическое выражение дает `true`, управление передается первой инструкции embedded.</span><span class="sxs-lookup"><span data-stu-id="682e2-247">If the boolean expression yields `true`, control is transferred to the first embedded statement.</span></span> <span data-ttu-id="682e2-248">Если и элемента управления достигает конечной точки этого оператора, управление передается конечную точку `if` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-248">When and if control reaches the end point of that statement, control is transferred to the end point of the `if` statement.</span></span>
*  <span data-ttu-id="682e2-249">Если логическое выражение дает `false` и если `else` часть присутствует, управление передается второй внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-249">If the boolean expression yields `false` and if an `else` part is present, control is transferred to the second embedded statement.</span></span> <span data-ttu-id="682e2-250">Если и элемента управления достигает конечной точки этого оператора, управление передается конечную точку `if` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-250">When and if control reaches the end point of that statement, control is transferred to the end point of the `if` statement.</span></span>
*  <span data-ttu-id="682e2-251">Если логическое выражение дает `false` и если `else` часть отсутствует, управление передается в конечную точку `if` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-251">If the boolean expression yields `false` and if an `else` part is not present, control is transferred to the end point of the `if` statement.</span></span>

<span data-ttu-id="682e2-252">Первый внедренный оператор `if` оператор достижим Если `if` оператор достижим и логическое выражение имеет значение константы `false`.</span><span class="sxs-lookup"><span data-stu-id="682e2-252">The first embedded statement of an `if` statement is reachable if the `if` statement is reachable and the boolean expression does not have the constant value `false`.</span></span>

<span data-ttu-id="682e2-253">Второй внедренный оператор `if` инструкции, если он имеется, доступен при `if` оператор достижим и логическое выражение имеет значение константы `true`.</span><span class="sxs-lookup"><span data-stu-id="682e2-253">The second embedded statement of an `if` statement, if present, is reachable if the `if` statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

<span data-ttu-id="682e2-254">Конечная точка `if` инструкции доступен, если конечная точка по крайней мере одного из его встроенных операторов достижима.</span><span class="sxs-lookup"><span data-stu-id="682e2-254">The end point of an `if` statement is reachable if the end point of at least one of its embedded statements is reachable.</span></span> <span data-ttu-id="682e2-255">Кроме того, точка конца `if` инструкции, не имеющий `else` часть доступен Если `if` оператор достижим и логическое выражение имеет значение константы `true`.</span><span class="sxs-lookup"><span data-stu-id="682e2-255">In addition, the end point of an `if` statement with no `else` part is reachable if the `if` statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

### <a name="the-switch-statement"></a><span data-ttu-id="682e2-256">Оператор switch</span><span class="sxs-lookup"><span data-stu-id="682e2-256">The switch statement</span></span>

<span data-ttu-id="682e2-257">Оператор switch выбирает для выполнения список операторов, метка которого соответствует значению выражения switch.</span><span class="sxs-lookup"><span data-stu-id="682e2-257">The switch statement selects for execution a statement list having an associated switch label that corresponds to the value of the switch expression.</span></span>

```antlr
switch_statement
    : 'switch' '(' expression ')' switch_block
    ;

switch_block
    : '{' switch_section* '}'
    ;

switch_section
    : switch_label+ statement_list
    ;

switch_label
    : 'case' constant_expression ':'
    | 'default' ':'
    ;
```

<span data-ttu-id="682e2-258">Объект *switch_statement* состоит из ключевого слова `switch`следуют выражение в скобках (называемых в выражении выбора вариантов), за которыми следует *switch_block*.</span><span class="sxs-lookup"><span data-stu-id="682e2-258">A *switch_statement* consists of the keyword `switch`, followed by a parenthesized expression (called the switch expression), followed by a *switch_block*.</span></span> <span data-ttu-id="682e2-259">*Switch_block* состоит из нуля или более *switch_section*s, заключенный в фигурные скобки.</span><span class="sxs-lookup"><span data-stu-id="682e2-259">The *switch_block* consists of zero or more *switch_section*s, enclosed in braces.</span></span> <span data-ttu-id="682e2-260">Каждый *switch_section* состоит из одного или нескольких *switch_label*s, за которым следует *statement_list* ([инструкция выводит список](statements.md#statement-lists)).</span><span class="sxs-lookup"><span data-stu-id="682e2-260">Each *switch_section* consists of one or more *switch_label*s followed by a *statement_list* ([Statement lists](statements.md#statement-lists)).</span></span>

<span data-ttu-id="682e2-261">***, Управляющие типом*** из `switch` инструкции устанавливается в выражении выбора вариантов.</span><span class="sxs-lookup"><span data-stu-id="682e2-261">The ***governing type*** of a `switch` statement is established by the switch expression.</span></span>

*  <span data-ttu-id="682e2-262">Если тип выражения выбора вариантов `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `bool`, `char`, `string`, или *enum_type*, или если он допускает значения NULL тип, соответствующий одному из этих типов, то это управление тип `switch` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-262">If the type of the switch expression is `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `bool`, `char`, `string`, or an *enum_type*, or if it is the nullable type corresponding to one of these types, then that is the governing type of the `switch` statement.</span></span>
*  <span data-ttu-id="682e2-263">В противном случае ровно один пользовательские неявное преобразование ([заданные пользователем преобразования](conversions.md#user-defined-conversions)) должен существовать из типа в выражении выбора вариантов к одному из следующих возможные типы, управляющие: `sbyte`, `byte`, `short` , `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `string`, или, допускающий значение NULL тип, соответствующий одному из этих типов.</span><span class="sxs-lookup"><span data-stu-id="682e2-263">Otherwise, exactly one user-defined implicit conversion ([User-defined conversions](conversions.md#user-defined-conversions)) must exist from the type of the switch expression to one of the following possible governing types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `string`, or,  a nullable type corresponding to one of those types.</span></span>
*  <span data-ttu-id="682e2-264">В противном случае если такого неявного преобразования не существует или если несколько таких неявных преобразований, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-264">Otherwise, if no such implicit conversion exists, or if more than one such implicit conversion exists, a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-265">Константное выражение каждого `case` метки должно представлять значение, которое может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) в тип `switch` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-265">The constant expression of each `case` label must denote a value that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the governing type of the `switch` statement.</span></span> <span data-ttu-id="682e2-266">Ошибка времени компиляции возникает, если два или более `case` метки в том же `switch` инструкции укажите то же постоянное значение.</span><span class="sxs-lookup"><span data-stu-id="682e2-266">A compile-time error occurs if two or more `case` labels in the same `switch` statement specify the same constant value.</span></span>

<span data-ttu-id="682e2-267">Допускается не более одного `default` метки в операторе switch.</span><span class="sxs-lookup"><span data-stu-id="682e2-267">There can be at most one `default` label in a switch statement.</span></span>

<span data-ttu-id="682e2-268">Объект `switch` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-268">A `switch` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-269">В выражении выбора вариантов вычисляется и преобразуется в тип.</span><span class="sxs-lookup"><span data-stu-id="682e2-269">The switch expression is evaluated and converted to the governing type.</span></span>
*  <span data-ttu-id="682e2-270">Если одна из констант в `case` метки в том же `switch` инструкции равно значению выражения switch, управление передается инструкции списке, приведенном в сопоставленной `case` метки.</span><span class="sxs-lookup"><span data-stu-id="682e2-270">If one of the constants specified in a `case` label in the same `switch` statement is equal to the value of the switch expression, control is transferred to the statement list following the matched `case` label.</span></span>
*  <span data-ttu-id="682e2-271">Если ни одна из констант, указанных в `case` метки в том же `switch` оператор равен значению выражения switch и если `default` метка присутствует, управление передается оператору, следующему списку `default` Метка.</span><span class="sxs-lookup"><span data-stu-id="682e2-271">If none of the constants specified in `case` labels in the same `switch` statement is equal to the value of the switch expression, and if a `default` label is present, control is transferred to the statement list following the `default` label.</span></span>
*  <span data-ttu-id="682e2-272">Если ни одна из констант, указанных в `case` метки в том же `switch` оператор равен значению выражения switch, а если `default` метка присутствует, управление передается в конечную точку `switch` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-272">If none of the constants specified in `case` labels in the same `switch` statement is equal to the value of the switch expression, and if no `default` label is present, control is transferred to the end point of the `switch` statement.</span></span>

<span data-ttu-id="682e2-273">Если доступен конечную точку списка операторов раздела switch, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-273">If the end point of the statement list of a switch section is reachable, a compile-time error occurs.</span></span> <span data-ttu-id="682e2-274">Это называется «без передачи управления дальше» правило.</span><span class="sxs-lookup"><span data-stu-id="682e2-274">This is known as the "no fall through" rule.</span></span> <span data-ttu-id="682e2-275">Пример</span><span class="sxs-lookup"><span data-stu-id="682e2-275">The example</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
    break;
case 1:
    CaseOne();
    break;
default:
    CaseOthers();
    break;
}
```
<span data-ttu-id="682e2-276">является допустимым, поскольку нет раздел switch содержит доступную конечную точку.</span><span class="sxs-lookup"><span data-stu-id="682e2-276">is valid because no switch section has a reachable end point.</span></span> <span data-ttu-id="682e2-277">В отличие от C и C++ выполнение раздела switch не допускается для «проваливания» в следующий раздел switch и в примере</span><span class="sxs-lookup"><span data-stu-id="682e2-277">Unlike C and C++, execution of a switch section is not permitted to "fall through" to the next switch section, and the example</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
case 1:
    CaseZeroOrOne();
default:
    CaseAny();
}
```
<span data-ttu-id="682e2-278">приводит к ошибке времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-278">results in a compile-time error.</span></span> <span data-ttu-id="682e2-279">При выполнении раздела switch должны предшествовать выполнения другого раздела switch, явно `goto case` или `goto default` необходимо использовать оператор:</span><span class="sxs-lookup"><span data-stu-id="682e2-279">When execution of a switch section is to be followed by execution of another switch section, an explicit `goto case` or `goto default` statement must be used:</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
    goto case 1;
case 1:
    CaseZeroOrOne();
    goto default;
default:
    CaseAny();
    break;
}
```

<span data-ttu-id="682e2-280">Несколько меток разрешены в *switch_section*.</span><span class="sxs-lookup"><span data-stu-id="682e2-280">Multiple labels are permitted in a *switch_section*.</span></span> <span data-ttu-id="682e2-281">Пример</span><span class="sxs-lookup"><span data-stu-id="682e2-281">The example</span></span>
```csharp
switch (i) {
case 0:
    CaseZero();
    break;
case 1:
    CaseOne();
    break;
case 2:
default:
    CaseTwo();
    break;
}
```
<span data-ttu-id="682e2-282">является допустимым.</span><span class="sxs-lookup"><span data-stu-id="682e2-282">is valid.</span></span> <span data-ttu-id="682e2-283">Пример не нарушает правило «не пройти через», так как метки `case 2:` и `default:` входят в одной и той же *switch_section*.</span><span class="sxs-lookup"><span data-stu-id="682e2-283">The example does not violate the "no fall through" rule because the labels `case 2:` and `default:` are part of the same *switch_section*.</span></span>

<span data-ttu-id="682e2-284">Правило «не пройти через» запрещает распространенных ошибок, возникающих в C и C++ при `break` случайно опускаются операторы.</span><span class="sxs-lookup"><span data-stu-id="682e2-284">The "no fall through" rule prevents a common class of bugs that occur in C and C++ when `break` statements are accidentally omitted.</span></span> <span data-ttu-id="682e2-285">Кроме того, из-за этого правила из разделов switch `switch` инструкции можно произвольно переупорядочить без влияния на поведение оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-285">In addition, because of this rule, the switch sections of a `switch` statement can be arbitrarily rearranged without affecting the behavior of the statement.</span></span> <span data-ttu-id="682e2-286">Например, разделы `switch` приведенной выше инструкции, которые могли быть отменены без влияния на поведение оператора:</span><span class="sxs-lookup"><span data-stu-id="682e2-286">For example, the sections of the `switch` statement above can be reversed without affecting the behavior of the statement:</span></span>
```csharp
switch (i) {
default:
    CaseAny();
    break;
case 1:
    CaseZeroOrOne();
    goto default;
case 0:
    CaseZero();
    goto case 1;
}
```

<span data-ttu-id="682e2-287">Список операторов в разделе switch, как правило, заканчивается в `break`, `goto case`, или `goto default` разрешено оператора, но любой конструкции отображает конечную точку списка операторов недоступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-287">The statement list of a switch section typically ends in a `break`, `goto case`, or `goto default` statement, but any construct that renders the end point of the statement list unreachable is permitted.</span></span> <span data-ttu-id="682e2-288">Например `while` инструкции, которые управляются логическое выражение `true` известно, что никогда не reach конечной точке.</span><span class="sxs-lookup"><span data-stu-id="682e2-288">For example, a `while` statement controlled by the boolean expression `true` is known to never reach its end point.</span></span> <span data-ttu-id="682e2-289">Аналогичным образом `throw` или `return` инструкции всегда передает управление в другом месте и не достигает конечной точке.</span><span class="sxs-lookup"><span data-stu-id="682e2-289">Likewise, a `throw` or `return` statement always transfers control elsewhere and never reaches its end point.</span></span> <span data-ttu-id="682e2-290">Таким образом следующий пример является допустимым:</span><span class="sxs-lookup"><span data-stu-id="682e2-290">Thus, the following example is valid:</span></span>
```csharp
switch (i) {
case 0:
    while (true) F();
case 1:
    throw new ArgumentException();
case 2:
    return;
}
```

<span data-ttu-id="682e2-291">Тип `switch` оператор может быть тип `string`.</span><span class="sxs-lookup"><span data-stu-id="682e2-291">The governing type of a `switch` statement may be the type `string`.</span></span> <span data-ttu-id="682e2-292">Пример:</span><span class="sxs-lookup"><span data-stu-id="682e2-292">For example:</span></span>
```csharp
void DoCommand(string command) {
    switch (command.ToLower()) {
    case "run":
        DoRun();
        break;
    case "save":
        DoSave();
        break;
    case "quit":
        DoQuit();
        break;
    default:
        InvalidCommand(command);
        break;
    }
}
```

<span data-ttu-id="682e2-293">Операторы равенства строк, такие как ([строковые операторы равенства](expressions.md#string-equality-operators)), `switch` инструкции чувствительно к регистру и будет выполняться данный раздел switch, только в том случае, если строка выражения switch точно соответствует `case` метки Константа.</span><span class="sxs-lookup"><span data-stu-id="682e2-293">Like the string equality operators ([String equality operators](expressions.md#string-equality-operators)), the `switch` statement is case sensitive and will execute a given switch section only if the switch expression string exactly matches a `case` label constant.</span></span>

<span data-ttu-id="682e2-294">Когда управление тип `switch` инструкция является `string`, значение `null` разрешается как константа метка case.</span><span class="sxs-lookup"><span data-stu-id="682e2-294">When the governing type of a `switch` statement is `string`, the value `null` is permitted as a case label constant.</span></span>

<span data-ttu-id="682e2-295">*Statement_list*s из *switch_block* может содержать операторы объявления ([операторы объявления](statements.md#declaration-statements)).</span><span class="sxs-lookup"><span data-stu-id="682e2-295">The *statement_list*s of a *switch_block* may contain declaration statements ([Declaration statements](statements.md#declaration-statements)).</span></span> <span data-ttu-id="682e2-296">Область локальной переменной или константы, объявленные в блоке коммутатора является блоком коммутатора.</span><span class="sxs-lookup"><span data-stu-id="682e2-296">The scope of a local variable or constant declared in a switch block is the switch block.</span></span>

<span data-ttu-id="682e2-297">Список операторов в разделе switch доступен Если `switch` оператор достижим и по крайней мере одно из следующих имеет значение true:</span><span class="sxs-lookup"><span data-stu-id="682e2-297">The statement list of a given switch section is reachable if the `switch` statement is reachable and at least one of the following is true:</span></span>

*  <span data-ttu-id="682e2-298">В выражении выбора вариантов представляет собой Непостоянное значение.</span><span class="sxs-lookup"><span data-stu-id="682e2-298">The switch expression is a non-constant value.</span></span>
*  <span data-ttu-id="682e2-299">Выражение switch является постоянное значение, которое соответствует `case` метки в разделе switch.</span><span class="sxs-lookup"><span data-stu-id="682e2-299">The switch expression is a constant value that matches a `case` label in the switch section.</span></span>
*  <span data-ttu-id="682e2-300">Выражение switch является постоянное значение, которое не соответствует ни одному `case` метки, а раздел switch содержит `default` метки.</span><span class="sxs-lookup"><span data-stu-id="682e2-300">The switch expression is a constant value that doesn't match any `case` label, and the switch section contains the `default` label.</span></span>
*  <span data-ttu-id="682e2-301">Метка switch раздел switch ссылается доступную `goto case` или `goto default` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-301">A switch label of the switch section is referenced by a reachable `goto case` or `goto default` statement.</span></span>

<span data-ttu-id="682e2-302">Конечная точка `switch` инструкции доступен, если верно хотя бы одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-302">The end point of a `switch` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="682e2-303">`switch` Инструкция содержит доступную `break` инструкцию, которая завершает работу `switch` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-303">The `switch` statement contains a reachable `break` statement that exits the `switch` statement.</span></span>
*  <span data-ttu-id="682e2-304">`switch` Доступен инструкции, выражения switch неконстантное значение и нет `default` имеется метка.</span><span class="sxs-lookup"><span data-stu-id="682e2-304">The `switch` statement is reachable, the switch expression is a non-constant value, and no `default` label is present.</span></span>
*  <span data-ttu-id="682e2-305">`switch` Доступен инструкции, выражения switch является постоянное значение, которое не соответствует ни одному `case` метку и нет `default` имеется метка.</span><span class="sxs-lookup"><span data-stu-id="682e2-305">The `switch` statement is reachable, the switch expression is a constant value that doesn't match any `case` label, and no `default` label is present.</span></span>

## <a name="iteration-statements"></a><span data-ttu-id="682e2-306">Операторы итерации</span><span class="sxs-lookup"><span data-stu-id="682e2-306">Iteration statements</span></span>

<span data-ttu-id="682e2-307">Оператор итераций повторно выполняет внедренную инструкцию.</span><span class="sxs-lookup"><span data-stu-id="682e2-307">Iteration statements repeatedly execute an embedded statement.</span></span>

```antlr
iteration_statement
    : while_statement
    | do_statement
    | for_statement
    | foreach_statement
    ;
```

### <a name="the-while-statement"></a><span data-ttu-id="682e2-308">Оператор while</span><span class="sxs-lookup"><span data-stu-id="682e2-308">The while statement</span></span>

<span data-ttu-id="682e2-309">`while` Инструкции условно выполняет внедренную инструкцию ноль или более раз.</span><span class="sxs-lookup"><span data-stu-id="682e2-309">The `while` statement conditionally executes an embedded statement zero or more times.</span></span>

```antlr
while_statement
    : 'while' '(' boolean_expression ')' embedded_statement
    ;
```

<span data-ttu-id="682e2-310">Объект `while` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-310">A `while` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-311">*Boolean_expression* ([логических выражений](expressions.md#boolean-expressions)) вычисляется.</span><span class="sxs-lookup"><span data-stu-id="682e2-311">The *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)) is evaluated.</span></span>
*  <span data-ttu-id="682e2-312">Если логическое выражение дает `true`, управление передается внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-312">If the boolean expression yields `true`, control is transferred to the embedded statement.</span></span> <span data-ttu-id="682e2-313">Если элемент управления достигает конечной точки внедренного оператора (возможно, в результате выполнения `continue` инструкции), управление передается в начале `while` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-313">When and if control reaches the end point of the embedded statement (possibly from execution of a `continue` statement), control is transferred to the beginning of the `while` statement.</span></span>
*  <span data-ttu-id="682e2-314">Если логическое выражение дает `false`, управление передается в конечную точку `while` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-314">If the boolean expression yields `false`, control is transferred to the end point of the `while` statement.</span></span>

<span data-ttu-id="682e2-315">В рамках внедренный оператор в `while` инструкции, `break` инструкции ([оператор break](statements.md#the-break-statement)) может использоваться для передачи управления конечную точку `while` (что приводит к завершению итерации внедренный оператор оператор) и `continue` инструкции ([оператор continue](statements.md#the-continue-statement)) может использоваться для передачи управления в конечную точку внедренного оператора (выполняя другой итерации `while` инструкции).</span><span class="sxs-lookup"><span data-stu-id="682e2-315">Within the embedded statement of a `while` statement, a `break` statement ([The break statement](statements.md#the-break-statement)) may be used to transfer control to the end point of the `while` statement (thus ending iteration of the embedded statement), and a `continue` statement ([The continue statement](statements.md#the-continue-statement)) may be used to transfer control to the end point of the embedded statement (thus performing another iteration of the `while` statement).</span></span>

<span data-ttu-id="682e2-316">Внедренный оператор в `while` оператор достижим Если `while` оператор достижим и логическое выражение имеет значение константы `false`.</span><span class="sxs-lookup"><span data-stu-id="682e2-316">The embedded statement of a `while` statement is reachable if the `while` statement is reachable and the boolean expression does not have the constant value `false`.</span></span>

<span data-ttu-id="682e2-317">Конечная точка `while` инструкции доступен, если верно хотя бы одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-317">The end point of a `while` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="682e2-318">`while` Инструкция содержит доступную `break` инструкцию, которая завершает работу `while` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-318">The `while` statement contains a reachable `break` statement that exits the `while` statement.</span></span>
*  <span data-ttu-id="682e2-319">`while` Оператор достижим и логическое выражение имеет значение константы `true`.</span><span class="sxs-lookup"><span data-stu-id="682e2-319">The `while` statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

### <a name="the-do-statement"></a><span data-ttu-id="682e2-320">Оператор do</span><span class="sxs-lookup"><span data-stu-id="682e2-320">The do statement</span></span>

<span data-ttu-id="682e2-321">`do` Инструкция выполняет ту или иную внедренный оператор один или несколько раз.</span><span class="sxs-lookup"><span data-stu-id="682e2-321">The `do` statement conditionally executes an embedded statement one or more times.</span></span>

```antlr
do_statement
    : 'do' embedded_statement 'while' '(' boolean_expression ')' ';'
    ;
```

<span data-ttu-id="682e2-322">Объект `do` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-322">A `do` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-323">Управление передается внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-323">Control is transferred to the embedded statement.</span></span>
*  <span data-ttu-id="682e2-324">Если элемент управления достигает конечной точки внедренного оператора (возможно, в результате выполнения `continue` инструкции), *boolean_expression* ([логических выражений](expressions.md#boolean-expressions)) вычисляется.</span><span class="sxs-lookup"><span data-stu-id="682e2-324">When and if control reaches the end point of the embedded statement (possibly from execution of a `continue` statement), the *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)) is evaluated.</span></span> <span data-ttu-id="682e2-325">Если логическое выражение дает `true`, управление передается в начале `do` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-325">If the boolean expression yields `true`, control is transferred to the beginning of the `do` statement.</span></span> <span data-ttu-id="682e2-326">В противном случае управление передается в конечную точку `do` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-326">Otherwise, control is transferred to the end point of the `do` statement.</span></span>

<span data-ttu-id="682e2-327">В рамках внедренный оператор в `do` инструкции, `break` инструкции ([оператор break](statements.md#the-break-statement)) может использоваться для передачи управления конечную точку `do` (что приводит к завершению итерации внедренный оператор оператор) и `continue` инструкции ([оператор continue](statements.md#the-continue-statement)) может использоваться для передачи управления в конечную точку внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-327">Within the embedded statement of a `do` statement, a `break` statement ([The break statement](statements.md#the-break-statement)) may be used to transfer control to the end point of the `do` statement (thus ending iteration of the embedded statement), and a `continue` statement ([The continue statement](statements.md#the-continue-statement)) may be used to transfer control to the end point of the embedded statement.</span></span>

<span data-ttu-id="682e2-328">Внедренный оператор в `do` оператор достижим Если `do` оператор достижим.</span><span class="sxs-lookup"><span data-stu-id="682e2-328">The embedded statement of a `do` statement is reachable if the `do` statement is reachable.</span></span>

<span data-ttu-id="682e2-329">Конечная точка `do` инструкции доступен, если верно хотя бы одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-329">The end point of a `do` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="682e2-330">`do` Инструкция содержит доступную `break` инструкцию, которая завершает работу `do` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-330">The `do` statement contains a reachable `break` statement that exits the `do` statement.</span></span>
*  <span data-ttu-id="682e2-331">Конечная точка внедренного оператора достижима и логическое выражение имеет значение константы `true`.</span><span class="sxs-lookup"><span data-stu-id="682e2-331">The end point of the embedded statement is reachable and the boolean expression does not have the constant value `true`.</span></span>

### <a name="the-for-statement"></a><span data-ttu-id="682e2-332">Оператор for</span><span class="sxs-lookup"><span data-stu-id="682e2-332">The for statement</span></span>

<span data-ttu-id="682e2-333">`for` Инструкция вычисляет последовательность выражений инициализации, а затем, пока условие имеет значение true, многократно выполняет внедренную инструкцию и вычисляет последовательность выражений итерации.</span><span class="sxs-lookup"><span data-stu-id="682e2-333">The `for` statement evaluates a sequence of initialization expressions and then, while a condition is true, repeatedly executes an embedded statement and evaluates a sequence of iteration expressions.</span></span>

```antlr
for_statement
    : 'for' '(' for_initializer? ';' for_condition? ';' for_iterator? ')' embedded_statement
    ;

for_initializer
    : local_variable_declaration
    | statement_expression_list
    ;

for_condition
    : boolean_expression
    ;

for_iterator
    : statement_expression_list
    ;

statement_expression_list
    : statement_expression (',' statement_expression)*
    ;
```

<span data-ttu-id="682e2-334">*For_initializer*, если он присутствует, состоит из *local_variable_declaration* ([объявления локальных переменных](statements.md#local-variable-declarations)) или список *statement_ выражение*s ([операторы выражений](statements.md#expression-statements)) через запятую.</span><span class="sxs-lookup"><span data-stu-id="682e2-334">The *for_initializer*, if present, consists of either a *local_variable_declaration* ([Local variable declarations](statements.md#local-variable-declarations)) or a list of *statement_expression*s ([Expression statements](statements.md#expression-statements)) separated by commas.</span></span> <span data-ttu-id="682e2-335">Область локальная переменная, объявленная с *for_initializer* начинается с *local_variable_declarator* для переменной и расширяет в конец внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-335">The scope of a local variable declared by a *for_initializer* starts at the *local_variable_declarator* for the variable and extends to the end of the embedded statement.</span></span> <span data-ttu-id="682e2-336">Область включает *for_condition* и *for_iterator*.</span><span class="sxs-lookup"><span data-stu-id="682e2-336">The scope includes the *for_condition* and the *for_iterator*.</span></span>

<span data-ttu-id="682e2-337">*For_condition*, если он указан, должно быть *boolean_expression* ([логических выражений](expressions.md#boolean-expressions)).</span><span class="sxs-lookup"><span data-stu-id="682e2-337">The *for_condition*, if present, must be a *boolean_expression* ([Boolean expressions](expressions.md#boolean-expressions)).</span></span>

<span data-ttu-id="682e2-338">*For_iterator*, если он присутствует, состоит из списка *statement_expression*s ([операторы выражений](statements.md#expression-statements)) через запятую.</span><span class="sxs-lookup"><span data-stu-id="682e2-338">The *for_iterator*, if present, consists of a list of *statement_expression*s ([Expression statements](statements.md#expression-statements)) separated by commas.</span></span>

<span data-ttu-id="682e2-339">Оператор For выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-339">A for statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-340">Если *for_initializer* отсутствует, инициализаторы переменных или выражения инструкции выполняются в порядке, они записываются.</span><span class="sxs-lookup"><span data-stu-id="682e2-340">If a *for_initializer* is present, the variable initializers or statement expressions are executed in the order they are written.</span></span> <span data-ttu-id="682e2-341">Этот шаг выполняется только один раз.</span><span class="sxs-lookup"><span data-stu-id="682e2-341">This step is only performed once.</span></span>
*  <span data-ttu-id="682e2-342">Если *for_condition* присутствует, оно вычисляется.</span><span class="sxs-lookup"><span data-stu-id="682e2-342">If a *for_condition* is present, it is evaluated.</span></span>
*  <span data-ttu-id="682e2-343">Если *for_condition* отсутствует или если результатом вычисления является `true`, управление передается внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-343">If the *for_condition* is not present or if the evaluation yields `true`, control is transferred to the embedded statement.</span></span> <span data-ttu-id="682e2-344">Если элемент управления достигает конечной точки внедренного оператора (возможно, в результате выполнения `continue` инструкции), выражения *for_iterator*, если имеется, вычисляются в последовательности, а затем другую итерацию выполняется, начиная с ознакомительной версией *for_condition* на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="682e2-344">When and if control reaches the end point of the embedded statement (possibly from execution of a `continue` statement), the expressions of the *for_iterator*, if any, are evaluated in sequence, and then another iteration is performed, starting with evaluation of the *for_condition* in the step above.</span></span>
*  <span data-ttu-id="682e2-345">Если *for_condition* существует и вычисление дает `false`, управление передается в конечную точку `for` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-345">If the *for_condition* is present and the evaluation yields `false`, control is transferred to the end point of the `for` statement.</span></span>

<span data-ttu-id="682e2-346">В рамках внедренный оператор в `for` инструкции, `break` инструкции ([оператор break](statements.md#the-break-statement)) может использоваться для передачи управления конечную точку `for` (что приводит к завершению итерации внедренный оператор оператор) и `continue` инструкции ([оператор continue](statements.md#the-continue-statement)) может использоваться для передачи управления в конечную точку внедренного оператора (выполняя *for_iterator* и выполнение другой итерации `for` инструкции, начиная с *for_condition*).</span><span class="sxs-lookup"><span data-stu-id="682e2-346">Within the embedded statement of a `for` statement, a `break` statement ([The break statement](statements.md#the-break-statement)) may be used to transfer control to the end point of the `for` statement (thus ending iteration of the embedded statement), and a `continue` statement ([The continue statement](statements.md#the-continue-statement)) may be used to transfer control to the end point of the embedded statement (thus executing the *for_iterator* and performing another iteration of the `for` statement, starting with the *for_condition*).</span></span>

<span data-ttu-id="682e2-347">Внедренный оператор в `for` инструкции доступен, если выполняется одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-347">The embedded statement of a `for` statement is reachable if one of the following is true:</span></span>

*  <span data-ttu-id="682e2-348">`for` Оператор достижим и не *for_condition* присутствует.</span><span class="sxs-lookup"><span data-stu-id="682e2-348">The `for` statement is reachable and no *for_condition* is present.</span></span>
*  <span data-ttu-id="682e2-349">`for` Оператор достижим и *for_condition* присутствует и имеет постоянное значение `false`.</span><span class="sxs-lookup"><span data-stu-id="682e2-349">The `for` statement is reachable and a *for_condition* is present and does not have the constant value `false`.</span></span>

<span data-ttu-id="682e2-350">Конечная точка `for` инструкции доступен, если верно хотя бы одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-350">The end point of a `for` statement is reachable if at least one of the following is true:</span></span>

*  <span data-ttu-id="682e2-351">`for` Инструкция содержит доступную `break` инструкцию, которая завершает работу `for` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-351">The `for` statement contains a reachable `break` statement that exits the `for` statement.</span></span>
*  <span data-ttu-id="682e2-352">`for` Оператор достижим и *for_condition* присутствует и имеет постоянное значение `true`.</span><span class="sxs-lookup"><span data-stu-id="682e2-352">The `for` statement is reachable and a *for_condition* is present and does not have the constant value `true`.</span></span>

### <a name="the-foreach-statement"></a><span data-ttu-id="682e2-353">Оператор foreach</span><span class="sxs-lookup"><span data-stu-id="682e2-353">The foreach statement</span></span>

<span data-ttu-id="682e2-354">`foreach` Инструкция перебирает элементы коллекции, выполняя внедренный оператор для каждого элемента коллекции.</span><span class="sxs-lookup"><span data-stu-id="682e2-354">The `foreach` statement enumerates the elements of a collection, executing an embedded statement for each element of the collection.</span></span>

```antlr
foreach_statement
    : 'foreach' '(' local_variable_type identifier 'in' expression ')' embedded_statement
    ;
```

<span data-ttu-id="682e2-355">*Тип* и *идентификатор* из `foreach` оператор объявления ***переменной итерации*** инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-355">The *type* and *identifier* of a `foreach` statement declare the ***iteration variable*** of the statement.</span></span> <span data-ttu-id="682e2-356">Если `var` передан идентификатор *local_variable_type*и тип с именем `var` находится в области видимости, считается переменной итерации ***переменной неявно типизированных итерации***, и его тип воспринимается как тип элемента `foreach` инструкции, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="682e2-356">If the `var` identifier is given as the *local_variable_type*, and no type named `var` is in scope, the iteration variable is said to be an ***implicitly typed iteration variable***, and its type is taken to be the element type of the `foreach` statement, as specified below.</span></span> <span data-ttu-id="682e2-357">Переменная итерации соответствует только для чтения локальную переменную с областью, охватывающей внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-357">The iteration variable corresponds to a read-only local variable with a scope that extends over the embedded statement.</span></span> <span data-ttu-id="682e2-358">Во время выполнения `foreach` инструкции, переменная итерации представляет элемент коллекции, для которого итерации в настоящее время выполняется.</span><span class="sxs-lookup"><span data-stu-id="682e2-358">During execution of a `foreach` statement, the iteration variable represents the collection element for which an iteration is currently being performed.</span></span> <span data-ttu-id="682e2-359">Ошибка времени компиляции возникает, если внедренный оператор пытается изменить переменную итерации (с помощью присваивания или `++` и `--` операторы) или передать ее как `ref` или `out` параметра.</span><span class="sxs-lookup"><span data-stu-id="682e2-359">A compile-time error occurs if the embedded statement attempts to modify the iteration variable (via assignment or the `++` and `--` operators) or pass the iteration variable as a `ref` or `out` parameter.</span></span>

<span data-ttu-id="682e2-360">Далее для краткости `IEnumerable`, `IEnumerator`, `IEnumerable<T>` и `IEnumerator<T>` см. соответствующие типы в пространствах имен `System.Collections` и `System.Collections.Generic`.</span><span class="sxs-lookup"><span data-stu-id="682e2-360">In the following, for brevity, `IEnumerable`, `IEnumerator`, `IEnumerable<T>` and `IEnumerator<T>` refer to the corresponding types in the namespaces `System.Collections` and `System.Collections.Generic`.</span></span>

<span data-ttu-id="682e2-361">Сначала определяет обработку во время компиляции оператора foreach ***тип коллекции***, ***тип перечислителя*** и ***тип элемента*** выражения.</span><span class="sxs-lookup"><span data-stu-id="682e2-361">The compile-time processing of a foreach statement first determines the ***collection type***, ***enumerator type*** and ***element type*** of the expression.</span></span> <span data-ttu-id="682e2-362">Это происходит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-362">This determination proceeds as follows:</span></span>

*  <span data-ttu-id="682e2-363">Если тип `X` из *выражение* является типом массива, то существует и неявное ссылочное преобразование из `X` для `IEnumerable` интерфейса (так как `System.Array` реализует этот интерфейс).</span><span class="sxs-lookup"><span data-stu-id="682e2-363">If the type `X` of *expression* is an array type then there is an implicit reference conversion from `X` to the `IEnumerable` interface (since `System.Array` implements this interface).</span></span> <span data-ttu-id="682e2-364">***Тип коллекции*** — `IEnumerable` интерфейс, ***тип перечислителя*** — `IEnumerator` интерфейс и ***тип элемента*** является тип элемента тип массива `X`.</span><span class="sxs-lookup"><span data-stu-id="682e2-364">The ***collection type*** is the `IEnumerable` interface, the ***enumerator type*** is the `IEnumerator` interface and the ***element type*** is the element type of the array type `X`.</span></span>
*  <span data-ttu-id="682e2-365">Если тип `X` из *выражение* — `dynamic` то существует неявное преобразование из *выражение* для `IEnumerable` интерфейс ([неявное dynamic преобразования](conversions.md#implicit-dynamic-conversions)).</span><span class="sxs-lookup"><span data-stu-id="682e2-365">If the type `X` of *expression* is `dynamic` then there is an implicit conversion from *expression* to the `IEnumerable` interface ([Implicit dynamic conversions](conversions.md#implicit-dynamic-conversions)).</span></span> <span data-ttu-id="682e2-366">***Тип коллекции*** — `IEnumerable` интерфейс и ***тип перечислителя*** является `IEnumerator` интерфейс.</span><span class="sxs-lookup"><span data-stu-id="682e2-366">The ***collection type*** is the `IEnumerable` interface and the ***enumerator type*** is the `IEnumerator` interface.</span></span> <span data-ttu-id="682e2-367">Если `var` передан идентификатор *local_variable_type* то ***тип элемента*** — `dynamic`, в противном случае это `object`.</span><span class="sxs-lookup"><span data-stu-id="682e2-367">If the `var` identifier is given as the *local_variable_type* then the ***element type*** is `dynamic`, otherwise it is `object`.</span></span>
*  <span data-ttu-id="682e2-368">В противном случае определить ли тип `X` имеет соответствующий `GetEnumerator` метод:</span><span class="sxs-lookup"><span data-stu-id="682e2-368">Otherwise, determine whether the type `X` has an appropriate `GetEnumerator` method:</span></span>
   * <span data-ttu-id="682e2-369">Выполните поиск члена типа `X` с идентификатором `GetEnumerator` и аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="682e2-369">Perform member lookup on the type `X` with identifier `GetEnumerator` and no type arguments.</span></span> <span data-ttu-id="682e2-370">Если поиск члена не создает совпадение, или он приводит к неоднозначности, или обнаружено соответствие, который не является группой методов, проверьте наличие перечислимого интерфейса, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="682e2-370">If the member lookup does not produce a match, or it produces an ambiguity, or produces a match that is not a method group, check for an enumerable interface as described below.</span></span> <span data-ttu-id="682e2-371">Выдано предупреждение, если поиск члена дает любой результат, за исключением группу методов или соответствие не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="682e2-371">It is recommended that a warning be issued if member lookup produces anything except a method group or no match.</span></span>
   * <span data-ttu-id="682e2-372">Выполнения разрешения перегрузки, с помощью результирующей группы методов и пустым списком аргументов.</span><span class="sxs-lookup"><span data-stu-id="682e2-372">Perform overload resolution using the resulting method group and an empty argument list.</span></span> <span data-ttu-id="682e2-373">Если разрешение перегрузки в методы не применимо, приводит к неоднозначности, или результатов в подходящий метод, но, что метод является либо статическими, либо не открытый, наличие перечислимого интерфейса, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="682e2-373">If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, check for an enumerable interface as described below.</span></span> <span data-ttu-id="682e2-374">Выдано предупреждение, если разрешение перегрузки дает любой результат, за исключением метода однозначный открытого экземпляра или применимые методы не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="682e2-374">It is recommended that a warning be issued if overload resolution produces anything except an unambiguous public instance method or no applicable methods.</span></span>
   * <span data-ttu-id="682e2-375">Если тип возвращаемого значения, `E` из `GetEnumerator` метод не является классом, тип структуры или интерфейса, ошибка и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="682e2-375">If the return type `E` of the `GetEnumerator` method is not a class, struct or interface type, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="682e2-376">Поиск члена выполняется на `E` с идентификатором `Current` и аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="682e2-376">Member lookup is performed on `E` with the identifier `Current` and no type arguments.</span></span> <span data-ttu-id="682e2-377">Если поиск члена не дает результата, происходит ошибка или результат-либо, кроме открытого свойства экземпляра, разрешающего чтение, ошибка, и никакие дальнейшие действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="682e2-377">If the member lookup produces no match, the result is an error, or the result is anything except a public instance property that permits reading, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="682e2-378">Поиск члена выполняется на `E` с идентификатором `MoveNext` и аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="682e2-378">Member lookup is performed on `E` with the identifier `MoveNext` and no type arguments.</span></span> <span data-ttu-id="682e2-379">Если поиск члена не дает результата, происходит ошибка или результатом является какой-либо кроме группу методов, выдается ошибка и никакие дальнейшие действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="682e2-379">If the member lookup produces no match, the result is an error, or the result is anything except a method group, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="682e2-380">Разрешение перегрузки выполняется на группу методов с пустым списком аргументов.</span><span class="sxs-lookup"><span data-stu-id="682e2-380">Overload resolution is performed on the method group with an empty argument list.</span></span> <span data-ttu-id="682e2-381">Если результаты разрешение перегрузки не применимые методы, приводит к неоднозначности или результаты в подходящий метод, но этот метод является либо статический, либо не открытый или его возвращаемый тип не является `bool`, выдается ошибка и никакие дальнейшие действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="682e2-381">If overload resolution results in no applicable methods, results in an ambiguity, or results in a single best method but that method is either static or not public, or its return type is not `bool`, an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="682e2-382">***Тип коллекции*** — `X`, ***тип перечислителя*** — `E`и ***тип элемента*** — это тип `Current` свойства.</span><span class="sxs-lookup"><span data-stu-id="682e2-382">The ***collection type*** is `X`, the ***enumerator type*** is `E`, and the ***element type*** is the type of the `Current` property.</span></span>

*  <span data-ttu-id="682e2-383">В противном случае проверьте перечислимого интерфейса:</span><span class="sxs-lookup"><span data-stu-id="682e2-383">Otherwise, check for an enumerable interface:</span></span>
   * <span data-ttu-id="682e2-384">Если для всех типов `Ti` для которого существует неявное преобразование из `X` для `IEnumerable<Ti>`, есть уникальный тип `T` таким образом, чтобы `T` не `dynamic` и для всех остальных `Ti` существует неявное преобразование из `IEnumerable<T>` для `IEnumerable<Ti>`, а затем ***тип коллекции*** — это интерфейс `IEnumerable<T>`, ***тип перечислителя*** — это интерфейс `IEnumerator<T>`и ***тип элемента*** является `T`.</span><span class="sxs-lookup"><span data-stu-id="682e2-384">If among all the types `Ti` for which there is an implicit conversion from `X` to `IEnumerable<Ti>`, there is a unique type `T` such that `T` is not `dynamic` and for all the other `Ti` there is an implicit conversion from `IEnumerable<T>` to `IEnumerable<Ti>`, then the ***collection type*** is the interface `IEnumerable<T>`, the ***enumerator type*** is the interface `IEnumerator<T>`, and the ***element type*** is `T`.</span></span>
   * <span data-ttu-id="682e2-385">В противном случае, если имеется более одного типа `T`, выдается ошибка и никакие дальнейшие действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="682e2-385">Otherwise, if there is more than one such type `T`, then an error is produced and no further steps are taken.</span></span>
   * <span data-ttu-id="682e2-386">В противном случае, если отсутствует неявное преобразование из `X` для `System.Collections.IEnumerable` интерфейс, а затем ***тип коллекции*** — это интерфейс ***тип перечислителя*** — это интерфейс `System.Collections.IEnumerator`и ***тип элемента*** является `object`.</span><span class="sxs-lookup"><span data-stu-id="682e2-386">Otherwise, if there is an implicit conversion from `X` to the `System.Collections.IEnumerable` interface, then the ***collection type*** is this interface, the ***enumerator type*** is the interface `System.Collections.IEnumerator`, and the ***element type*** is `object`.</span></span>
   * <span data-ttu-id="682e2-387">В противном случае выдается ошибка и никакие дальнейшие действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="682e2-387">Otherwise, an error is produced and no further steps are taken.</span></span>

<span data-ttu-id="682e2-388">Указанные выше шаги и в случае успешного выполнения однозначно привести к типу коллекции `C`, тип перечислителя `E` и тип элемента `T`.</span><span class="sxs-lookup"><span data-stu-id="682e2-388">The above steps, if successful, unambiguously produce a collection type `C`, enumerator type `E` and element type `T`.</span></span> <span data-ttu-id="682e2-389">Оператор foreach в форме</span><span class="sxs-lookup"><span data-stu-id="682e2-389">A foreach statement of the form</span></span>
```csharp
foreach (V v in x) embedded_statement
```
<span data-ttu-id="682e2-390">затем распространяется на:</span><span class="sxs-lookup"><span data-stu-id="682e2-390">is then expanded to:</span></span>
```csharp
{
    E e = ((C)(x)).GetEnumerator();
    try {
        while (e.MoveNext()) {
            V v = (V)(T)e.Current;
            embedded_statement
        }
    }
    finally {
        ... // Dispose e
    }
}
```

<span data-ttu-id="682e2-391">Переменная `e` не видно, но доступ к выражению `x` или внедренный оператор, или любой другой исходный код программы.</span><span class="sxs-lookup"><span data-stu-id="682e2-391">The variable `e` is not visible to or accessible to the expression `x` or the embedded statement or any other source code of the program.</span></span> <span data-ttu-id="682e2-392">Переменная `v` только для чтения в внедренный оператор.</span><span class="sxs-lookup"><span data-stu-id="682e2-392">The variable `v` is read-only in the embedded statement.</span></span> <span data-ttu-id="682e2-393">Если не существует явное преобразование ([явные преобразования](conversions.md#explicit-conversions)) из `T` (тип элемента) для `V` ( *local_variable_type* в операторе foreach), выдается ошибка и никакие дополнительные действия не предпринимаются.</span><span class="sxs-lookup"><span data-stu-id="682e2-393">If there is not an explicit conversion ([Explicit conversions](conversions.md#explicit-conversions)) from `T` (the element type) to `V` (the *local_variable_type* in the foreach statement), an error is produced and no further steps are taken.</span></span> <span data-ttu-id="682e2-394">Если `x` имеет значение `null`, `System.NullReferenceException` возникает исключение во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="682e2-394">If `x` has the value `null`, a `System.NullReferenceException` is thrown at run-time.</span></span>

<span data-ttu-id="682e2-395">Реализация может реализовать данный оператор foreach по-разному, например, для повышения производительности, до тех пор, пока поведение согласуется с выше расширения.</span><span class="sxs-lookup"><span data-stu-id="682e2-395">An implementation is permitted to implement a given foreach-statement differently, e.g. for performance reasons, as long as the behavior is consistent with the above expansion.</span></span>

<span data-ttu-id="682e2-396">Размещение `v` внутри while цикл важно как записывается по любой анонимной функции в *embedded_statement*.</span><span class="sxs-lookup"><span data-stu-id="682e2-396">The placement of `v` inside the while loop is important for how it is captured by any anonymous function occurring in the *embedded_statement*.</span></span>

<span data-ttu-id="682e2-397">Пример:</span><span class="sxs-lookup"><span data-stu-id="682e2-397">For example:</span></span>
```csharp
int[] values = { 7, 9, 13 };
Action f = null;

foreach (var value in values)
{
    if (f == null) f = () => Console.WriteLine("First value: " + value);
}

f();
```
<span data-ttu-id="682e2-398">Если `v` была объявлена вне while цикла, оно будет совместно использоваться всех итераций, а его значение после для цикла будет окончательное значение, а `13`, который относится к какой вызов `f` распечатает.</span><span class="sxs-lookup"><span data-stu-id="682e2-398">If `v` was declared outside of the while loop, it would be shared among all iterations, and its value after the for loop would be the final value, `13`, which is what the invocation of `f` would print.</span></span> <span data-ttu-id="682e2-399">Вместо этого, так как для каждой итерации задается собственный переменной `v`, одной записанной по `f` в первой итерации будут по-прежнему для хранения значения `7`, который является то, что будут печататься.</span><span class="sxs-lookup"><span data-stu-id="682e2-399">Instead, because each iteration has its own variable `v`, the one captured by `f` in the first iteration will continue to hold the value `7`, which is what will be printed.</span></span> <span data-ttu-id="682e2-400">(Примечание: объявлен в более ранних версиях C# `v` цикл while снаружи.)</span><span class="sxs-lookup"><span data-stu-id="682e2-400">(Note: earlier versions of C# declared `v` outside of the while loop.)</span></span>

<span data-ttu-id="682e2-401">Тело блока finally строится с помощью следующих действий:</span><span class="sxs-lookup"><span data-stu-id="682e2-401">The body of the finally block is constructed according to the following steps:</span></span>

*  <span data-ttu-id="682e2-402">Если неявное преобразование из `E` для `System.IDisposable` интерфейс, затем</span><span class="sxs-lookup"><span data-stu-id="682e2-402">If there is an implicit conversion from `E` to the `System.IDisposable` interface, then</span></span>
   *  <span data-ttu-id="682e2-403">Если `E` является типом значения, не допускающим то предложение finally развертывается в семантический эквивалент следующего:</span><span class="sxs-lookup"><span data-stu-id="682e2-403">If `E` is a non-nullable value type then the finally clause is expanded to the semantic equivalent  of:</span></span>

      ```csharp
      finally {
          ((System.IDisposable)e).Dispose();
      }
      ```

   *  <span data-ttu-id="682e2-404">В противном случае предложение finally развертывается в семантический эквивалент следующего:</span><span class="sxs-lookup"><span data-stu-id="682e2-404">Otherwise the finally clause is expanded to the semantic equivalent of:</span></span>

      ```csharp
      finally {
          if (e != null) ((System.IDisposable)e).Dispose();
      }
      ```

   <span data-ttu-id="682e2-405">Кроме случаев, когда `E` является типом значения или параметра типа, создать экземпляр типа значения, а затем приведение из `e` для `System.IDisposable` не приведет к выполнению упаковки.</span><span class="sxs-lookup"><span data-stu-id="682e2-405">except that if `E` is a value type, or a type parameter instantiated to a value type, then the cast of `e` to `System.IDisposable` will not cause boxing to occur.</span></span>

*  <span data-ttu-id="682e2-406">В противном случае, если `E` является запечатанным типом, предложение finally развертывается в пустой блок:</span><span class="sxs-lookup"><span data-stu-id="682e2-406">Otherwise, if `E` is a sealed type, the finally clause is expanded to an empty block:</span></span>

   ```csharp
   finally {
   }
   ```

*  <span data-ttu-id="682e2-407">В противном случае предложение finally развертывается для:</span><span class="sxs-lookup"><span data-stu-id="682e2-407">Otherwise, the finally clause is expanded to:</span></span>

   ```csharp
   finally {
       System.IDisposable d = e as System.IDisposable;
       if (d != null) d.Dispose();
   }
   ```    

   <span data-ttu-id="682e2-408">Локальная переменная `d` не видно, но доступны для любого пользовательского кода.</span><span class="sxs-lookup"><span data-stu-id="682e2-408">The local variable `d` is not visible to or accessible to any user code.</span></span> <span data-ttu-id="682e2-409">В частности, он не конфликтует с любой другой переменной, область которого входят блок finally.</span><span class="sxs-lookup"><span data-stu-id="682e2-409">In particular, it does not conflict with any other variable whose scope includes the finally block.</span></span>

<span data-ttu-id="682e2-410">Порядок, в котором `foreach` обходит элементы массива, выглядит следующим образом: Для одномерных массивов элементы распространяются по возрастанию индекс, начиная с индекса `0` и заканчивая индексом `Length - 1`.</span><span class="sxs-lookup"><span data-stu-id="682e2-410">The order in which `foreach` traverses the elements of an array, is as follows: For single-dimensional arrays elements are traversed in increasing index order, starting with index `0` and ending with index `Length - 1`.</span></span> <span data-ttu-id="682e2-411">Для многомерных массивов элементы распространяются, индексы самого правого измерения являются сначала, а затем Далее левой измерения, и т. д слева.</span><span class="sxs-lookup"><span data-stu-id="682e2-411">For multi-dimensional arrays, elements are traversed such that the indices of the rightmost dimension are increased first, then the next left dimension, and so on to the left.</span></span>

<span data-ttu-id="682e2-412">В следующем примере выводится из каждого значения в двумерном массиве, по порядку:</span><span class="sxs-lookup"><span data-stu-id="682e2-412">The following example prints out each value in a two-dimensional array, in element order:</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        double[,] values = {
            {1.2, 2.3, 3.4, 4.5},
            {5.6, 6.7, 7.8, 8.9}
        };

        foreach (double elementValue in values)
            Console.Write("{0} ", elementValue);

        Console.WriteLine();
    }
}
```
<span data-ttu-id="682e2-413">Вывод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-413">The output produced is as follows:</span></span>
```csharp
1.2 2.3 3.4 4.5 5.6 6.7 7.8 8.9
```

<span data-ttu-id="682e2-414">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-414">In the example</span></span>
```csharp
int[] numbers = { 1, 3, 5, 7, 9 };
foreach (var n in numbers) Console.WriteLine(n);
```
<span data-ttu-id="682e2-415">Тип `n` выводится как `int`, тип элемента `numbers`.</span><span class="sxs-lookup"><span data-stu-id="682e2-415">the type of `n` is inferred to be `int`, the element type of `numbers`.</span></span>

## <a name="jump-statements"></a><span data-ttu-id="682e2-416">Операторы перехода</span><span class="sxs-lookup"><span data-stu-id="682e2-416">Jump statements</span></span>

<span data-ttu-id="682e2-417">Операторы перехода осуществляют безусловную передачу управления.</span><span class="sxs-lookup"><span data-stu-id="682e2-417">Jump statements unconditionally transfer control.</span></span>

```antlr
jump_statement
    : break_statement
    | continue_statement
    | goto_statement
    | return_statement
    | throw_statement
    ;
```

<span data-ttu-id="682e2-418">Расположение, к которому оператор перехода передает управление называется ***целевой*** оператора перехода.</span><span class="sxs-lookup"><span data-stu-id="682e2-418">The location to which a jump statement transfers control is called the ***target*** of the jump statement.</span></span>

<span data-ttu-id="682e2-419">Если оператор перехода находится в пределах блока, а целевой объект, что оператор перехода находится вне этого блока, оператор jump называется ***выйти из*** блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-419">When a jump statement occurs within a block, and the target of that jump statement is outside that block, the jump statement is said to ***exit*** the block.</span></span> <span data-ttu-id="682e2-420">Хотя оператор перехода может передать управление из блока, он никогда не передает управление в блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-420">While a jump statement may transfer control out of a block, it can never transfer control into a block.</span></span>

<span data-ttu-id="682e2-421">Выполнение оператора перехода усложняется наличием промежуточные `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-421">Execution of jump statements is complicated by the presence of intervening `try` statements.</span></span> <span data-ttu-id="682e2-422">При отсутствии таких `try` операторы, оператор перехода обеспечивает безусловную передачу управления из оператора перехода своей цели.</span><span class="sxs-lookup"><span data-stu-id="682e2-422">In the absence of such `try` statements, a jump statement unconditionally transfers control from the jump statement to its target.</span></span> <span data-ttu-id="682e2-423">При наличии таких промежуточных `try` инструкции, выполнение более сложен.</span><span class="sxs-lookup"><span data-stu-id="682e2-423">In the presence of such intervening `try` statements, execution is more complex.</span></span> <span data-ttu-id="682e2-424">Выход из оператора перехода, один или несколько `try` связанных блоков с `finally` блоки, элемент управления изначально передается `finally` блок самого внутреннего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-424">If the jump statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="682e2-425">Если элемент управления достигает конечной точки `finally` блок, элемент управления передается `finally` блок Далее включающего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-425">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-426">Этот процесс повторяется, пока `finally` блоки всех промежуточных `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-426">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>

<span data-ttu-id="682e2-427">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-427">In the example</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        while (true) {
            try {
                try {
                    Console.WriteLine("Before break");
                    break;
                }
                finally {
                    Console.WriteLine("Innermost finally block");
                }
            }
            finally {
                Console.WriteLine("Outermost finally block");
            }
        }
        Console.WriteLine("After break");
    }
}
```
<span data-ttu-id="682e2-428">`finally` блокировок, сопоставленных с двумя `try` инструкции перед передачей управления в целевой объект оператора перехода.</span><span class="sxs-lookup"><span data-stu-id="682e2-428">the `finally` blocks associated with two `try` statements are executed before control is transferred to the target of the jump statement.</span></span>

<span data-ttu-id="682e2-429">Вывод выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-429">The output produced is as follows:</span></span>
```
Before break
Innermost finally block
Outermost finally block
After break
```

### <a name="the-break-statement"></a><span data-ttu-id="682e2-430">Оператор break</span><span class="sxs-lookup"><span data-stu-id="682e2-430">The break statement</span></span>

<span data-ttu-id="682e2-431">`break` Инструкция завершает работу ближайшего внешнего оператора `switch`, `while`, `do`, `for`, или `foreach` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-431">The `break` statement exits the nearest enclosing `switch`, `while`, `do`, `for`, or `foreach` statement.</span></span>

```antlr
break_statement
    : 'break' ';'
    ;
```

<span data-ttu-id="682e2-432">Цель `break` инструкция является конечной точкой ближайшего внешнего оператора `switch`, `while`, `do`, `for`, или `foreach` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-432">The target of a `break` statement is the end point of the nearest enclosing `switch`, `while`, `do`, `for`, or `foreach` statement.</span></span> <span data-ttu-id="682e2-433">Если `break` оператор не входит в `switch`, `while`, `do`, `for`, или `foreach` инструкции, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-433">If a `break` statement is not enclosed by a `switch`, `while`, `do`, `for`, or `foreach` statement, a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-434">Когда несколько `switch`, `while`, `do`, `for`, или `foreach` инструкций вложены друг в друга, `break` заявление применяется только к самой внутренней инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-434">When multiple `switch`, `while`, `do`, `for`, or `foreach` statements are nested within each other, a `break` statement applies only to the innermost statement.</span></span> <span data-ttu-id="682e2-435">Для передачи управления на нескольких уровнях вложенности, `goto` инструкции ([инструкцию goto](statements.md#the-goto-statement)) необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="682e2-435">To transfer control across multiple nesting levels, a `goto` statement ([The goto statement](statements.md#the-goto-statement)) must be used.</span></span>

<span data-ttu-id="682e2-436">Объект `break` инструкция не может быть закрыто `finally` блока ([оператора try](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="682e2-436">A `break` statement cannot exit a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span> <span data-ttu-id="682e2-437">При `break` оператор находится внутри `finally` block, цель `break` инструкция должна быть в пределах одного `finally` block; в противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-437">When a `break` statement occurs within a `finally` block, the target of the `break` statement must be within the same `finally` block; otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-438">Объект `break` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-438">A `break` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-439">Если `break` инструкция завершает работу, один или несколько `try` связанных блоков с `finally` блоки, элемент управления изначально передается `finally` блок самого внутреннего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-439">If the `break` statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="682e2-440">Если элемент управления достигает конечной точки `finally` блок, элемент управления передается `finally` блок Далее включающего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-440">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-441">Этот процесс повторяется, пока `finally` блоки всех промежуточных `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-441">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>
*  <span data-ttu-id="682e2-442">Управление передается от целевого объекта `break` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-442">Control is transferred to the target of the `break` statement.</span></span>

<span data-ttu-id="682e2-443">Так как `break` инструкции Безусловно передает управление в другом месте, конечная точка `break` инструкции никогда не доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-443">Because a `break` statement unconditionally transfers control elsewhere, the end point of a `break` statement is never reachable.</span></span>

### <a name="the-continue-statement"></a><span data-ttu-id="682e2-444">Оператор continue</span><span class="sxs-lookup"><span data-stu-id="682e2-444">The continue statement</span></span>

<span data-ttu-id="682e2-445">`continue` Инструкция запускает новую итерацию ближайшего внешнего оператора `while`, `do`, `for`, или `foreach` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-445">The `continue` statement starts a new iteration of the nearest enclosing `while`, `do`, `for`, or `foreach` statement.</span></span>

```antlr
continue_statement
    : 'continue' ';'
    ;
```

<span data-ttu-id="682e2-446">Цель `continue` инструкция является конечной точкой внедренного оператора ближайшего внешнего оператора `while`, `do`, `for`, или `foreach` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-446">The target of a `continue` statement is the end point of the embedded statement of the nearest enclosing `while`, `do`, `for`, or `foreach` statement.</span></span> <span data-ttu-id="682e2-447">Если `continue` оператор не входит в `while`, `do`, `for`, или `foreach` инструкции, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-447">If a `continue` statement is not enclosed by a `while`, `do`, `for`, or `foreach` statement, a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-448">Когда несколько `while`, `do`, `for`, или `foreach` инструкций вложены друг в друга, `continue` заявление применяется только к самой внутренней инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-448">When multiple `while`, `do`, `for`, or `foreach` statements are nested within each other, a `continue` statement applies only to the innermost statement.</span></span> <span data-ttu-id="682e2-449">Для передачи управления на нескольких уровнях вложенности, `goto` инструкции ([инструкцию goto](statements.md#the-goto-statement)) необходимо использовать.</span><span class="sxs-lookup"><span data-stu-id="682e2-449">To transfer control across multiple nesting levels, a `goto` statement ([The goto statement](statements.md#the-goto-statement)) must be used.</span></span>

<span data-ttu-id="682e2-450">Объект `continue` инструкция не может быть закрыто `finally` блока ([оператора try](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="682e2-450">A `continue` statement cannot exit a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span> <span data-ttu-id="682e2-451">При `continue` оператор находится внутри `finally` block, цель `continue` инструкция должна быть в пределах одного `finally` block; в противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-451">When a `continue` statement occurs within a `finally` block, the target of the `continue` statement must be within the same `finally` block; otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-452">Объект `continue` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-452">A `continue` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-453">Если `continue` инструкция завершает работу, один или несколько `try` связанных блоков с `finally` блоки, элемент управления изначально передается `finally` блок самого внутреннего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-453">If the `continue` statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="682e2-454">Если элемент управления достигает конечной точки `finally` блок, элемент управления передается `finally` блок Далее включающего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-454">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-455">Этот процесс повторяется, пока `finally` блоки всех промежуточных `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-455">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>
*  <span data-ttu-id="682e2-456">Управление передается от целевого объекта `continue` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-456">Control is transferred to the target of the `continue` statement.</span></span>

<span data-ttu-id="682e2-457">Так как `continue` инструкции Безусловно передает управление в другом месте, конечная точка `continue` инструкции никогда не доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-457">Because a `continue` statement unconditionally transfers control elsewhere, the end point of a `continue` statement is never reachable.</span></span>

### <a name="the-goto-statement"></a><span data-ttu-id="682e2-458">Оператор goto</span><span class="sxs-lookup"><span data-stu-id="682e2-458">The goto statement</span></span>

<span data-ttu-id="682e2-459">`goto` Оператор передает управление в инструкцию, помеченный атрибутом метку.</span><span class="sxs-lookup"><span data-stu-id="682e2-459">The `goto` statement transfers control to a statement that is marked by a label.</span></span>

```antlr
goto_statement
    : 'goto' identifier ';'
    | 'goto' 'case' constant_expression ';'
    | 'goto' 'default' ';'
    ;
```

<span data-ttu-id="682e2-460">Цель `goto` *идентификатор* инструкция является оператор с меткой с указанной меткой.</span><span class="sxs-lookup"><span data-stu-id="682e2-460">The target of a `goto` *identifier* statement is the labeled statement with the given label.</span></span> <span data-ttu-id="682e2-461">Если метку с заданным именем не существует в текущей функции-члене или `goto` инструкции не входит в область метки, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-461">If a label with the given name does not exist in the current function member, or if the `goto` statement is not within the scope of the label, a compile-time error occurs.</span></span> <span data-ttu-id="682e2-462">Это правило позволяет использовать `goto` инструкцию, чтобы передать управление за пределы вложенной области, но не в вложенной области.</span><span class="sxs-lookup"><span data-stu-id="682e2-462">This rule permits the use of a `goto` statement to transfer control out of a nested scope, but not into a nested scope.</span></span> <span data-ttu-id="682e2-463">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-463">In the example</span></span>
```csharp
using System;

class Test
{
    static void Main(string[] args) {
        string[,] table = {
            {"Red", "Blue", "Green"},
            {"Monday", "Wednesday", "Friday"}
        };

        foreach (string str in args) {
            int row, colm;
            for (row = 0; row <= 1; ++row)
                for (colm = 0; colm <= 2; ++colm)
                    if (str == table[row,colm])
                         goto done;

            Console.WriteLine("{0} not found", str);
            continue;
    done:
            Console.WriteLine("Found {0} at [{1}][{2}]", str, row, colm);
        }
    }
}
```
<span data-ttu-id="682e2-464">`goto` оператор используется для передачи управления из вложенной области.</span><span class="sxs-lookup"><span data-stu-id="682e2-464">a `goto` statement is used to transfer control out of a nested scope.</span></span>

<span data-ttu-id="682e2-465">Цель `goto case` инструкция является списка операторов в немедленно включающего `switch` инструкции ([оператора switch](statements.md#the-switch-statement)), который содержит `case` метку с заданным значением константы.</span><span class="sxs-lookup"><span data-stu-id="682e2-465">The target of a `goto case` statement is the statement list in the immediately enclosing `switch` statement ([The switch statement](statements.md#the-switch-statement)), which contains a `case` label with the given constant value.</span></span> <span data-ttu-id="682e2-466">Если `goto case` оператор не входит в `switch` инструкции, если *constant_expression* не может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) на тип ближайшее заключения `switch` инструкции, или если ближайшего внешнего оператора `switch` инструкция не содержит `case` метку с заданным значением константы, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-466">If the `goto case` statement is not enclosed by a `switch` statement, if the *constant_expression* is not implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the governing type of the nearest enclosing `switch` statement, or if the nearest enclosing `switch` statement does not contain a `case` label with the given constant value, a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-467">Цель `goto default` инструкция является списка операторов в немедленно включающего `switch` инструкции ([оператора switch](statements.md#the-switch-statement)), который содержит `default` метки.</span><span class="sxs-lookup"><span data-stu-id="682e2-467">The target of a `goto default` statement is the statement list in the immediately enclosing `switch` statement ([The switch statement](statements.md#the-switch-statement)), which contains a `default` label.</span></span> <span data-ttu-id="682e2-468">Если `goto default` оператор не входит в `switch` инструкции, или если ближайшего внешнего оператора `switch` инструкция не содержит `default` метки, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-468">If the `goto default` statement is not enclosed by a `switch` statement, or if the nearest enclosing `switch` statement does not contain a `default` label, a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-469">Объект `goto` инструкция не может быть закрыто `finally` блока ([оператора try](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="682e2-469">A `goto` statement cannot exit a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span> <span data-ttu-id="682e2-470">При `goto` оператор находится внутри `finally` block, цель `goto` инструкция должна быть в пределах одного `finally` блок, или в противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-470">When a `goto` statement occurs within a `finally` block, the target of the `goto` statement must be within the same `finally` block, or otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-471">Объект `goto` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-471">A `goto` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-472">Если `goto` инструкция завершает работу, один или несколько `try` связанных блоков с `finally` блоки, элемент управления изначально передается `finally` блок самого внутреннего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-472">If the `goto` statement exits one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="682e2-473">Если элемент управления достигает конечной точки `finally` блок, элемент управления передается `finally` блок Далее включающего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-473">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-474">Этот процесс повторяется, пока `finally` блоки всех промежуточных `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-474">This process is repeated until the `finally` blocks of all intervening `try` statements have been executed.</span></span>
*  <span data-ttu-id="682e2-475">Управление передается от целевого объекта `goto` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-475">Control is transferred to the target of the `goto` statement.</span></span>

<span data-ttu-id="682e2-476">Так как `goto` инструкции Безусловно передает управление в другом месте, конечная точка `goto` инструкции никогда не доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-476">Because a `goto` statement unconditionally transfers control elsewhere, the end point of a `goto` statement is never reachable.</span></span>

### <a name="the-return-statement"></a><span data-ttu-id="682e2-477">Оператор return</span><span class="sxs-lookup"><span data-stu-id="682e2-477">The return statement</span></span>

<span data-ttu-id="682e2-478">`return` Оператор возвращает управление вызывающему объекту текущей функции, в котором `return` содержится инструкция.</span><span class="sxs-lookup"><span data-stu-id="682e2-478">The `return` statement returns control to the current caller of the function in which the `return` statement appears.</span></span>

```antlr
return_statement
    : 'return' expression? ';'
    ;
```

<span data-ttu-id="682e2-479">Объект `return` оператор выражение не может использоваться только в функции-члена, не вычисляет значение, то есть метод с типом результата ([тело метода](classes.md#method-body)) `void`, `set` метод доступа свойства или индексатор, `add` и `remove` методы доступа события, конструкторе экземпляра, статический конструктор или деструктор.</span><span class="sxs-lookup"><span data-stu-id="682e2-479">A `return` statement with no expression can be used only in a function member that does not compute a value, that is, a method with the result type ([Method body](classes.md#method-body)) `void`, the `set` accessor of a property or indexer, the `add` and `remove` accessors of an event, an instance constructor, a static constructor, or a destructor.</span></span>

<span data-ttu-id="682e2-480">Объект `return` инструкции с выражением может использоваться только в функции-члена, которая вычисляет значение, то есть метод с типом результата, отличный от void, `get` метод доступа свойства или индексатора или определяемого пользователем оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-480">A `return` statement with an expression can only be used in a function member that computes a value, that is, a method with a non-void result type, the `get` accessor of a property or indexer, or a user-defined operator.</span></span> <span data-ttu-id="682e2-481">Неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) должен существовать в возвращаемый тип, содержащий функции-члена из типа выражения.</span><span class="sxs-lookup"><span data-stu-id="682e2-481">An implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) must exist from the type of the expression to the return type of the containing function member.</span></span>

<span data-ttu-id="682e2-482">Возвращает операторы также могут использоваться в тексте выражения анонимных функций ([выражения анонимных функций](expressions.md#anonymous-function-expressions)) и участвовать в определении того, какие преобразования существует для этих функций.</span><span class="sxs-lookup"><span data-stu-id="682e2-482">Return statements can also be used in the body of anonymous function expressions ([Anonymous function expressions](expressions.md#anonymous-function-expressions)), and participate in determining which conversions exist for those functions.</span></span>

<span data-ttu-id="682e2-483">Произошла ошибка во время компиляции для `return` инструкции в `finally` блока ([оператора try](statements.md#the-try-statement)).</span><span class="sxs-lookup"><span data-stu-id="682e2-483">It is a compile-time error for a `return` statement to appear in a `finally` block ([The try statement](statements.md#the-try-statement)).</span></span>

<span data-ttu-id="682e2-484">Объект `return` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-484">A `return` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-485">Если `return` инструкция указывает выражение, выражение вычисляется, и полученное значение преобразуется в возвращаемый тип, содержащий функции с помощью неявного преобразования.</span><span class="sxs-lookup"><span data-stu-id="682e2-485">If the `return` statement specifies an expression, the expression is evaluated and the resulting value is converted to the return type of the containing function by an implicit conversion.</span></span> <span data-ttu-id="682e2-486">Результат преобразования становится значением результата, созданного функцией.</span><span class="sxs-lookup"><span data-stu-id="682e2-486">The result of the conversion becomes the result value produced by the function.</span></span>
*  <span data-ttu-id="682e2-487">Если `return` оператор входит в один или несколько `try` или `catch` связанных блоков с `finally` блоки, элемент управления изначально передается `finally` блок самого внутреннего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-487">If the `return` statement is enclosed by one or more `try` or `catch` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="682e2-488">Если элемент управления достигает конечной точки `finally` блок, элемент управления передается `finally` блок Далее включающего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-488">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-489">Этот процесс повторяется, пока `finally` блоки, включающего все `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-489">This process is repeated until the `finally` blocks of all enclosing `try` statements have been executed.</span></span>
*  <span data-ttu-id="682e2-490">Если содержащего функция не является асинхронной функции, управление возвращается вызывающему вместе с их результата, содержащего функции, если таковые имеются.</span><span class="sxs-lookup"><span data-stu-id="682e2-490">If the containing function is not an async function, control is returned to the caller of the containing function along with the result value, if any.</span></span>
*  <span data-ttu-id="682e2-491">Если содержащий функция является асинхронной функции, управление возвращается вызывающему объекту текущего и результирующее значение, если таковые имеются, записывается в задача возврата как описано в разделе ([интерфейсы перечислителя](classes.md#enumerator-interfaces)).</span><span class="sxs-lookup"><span data-stu-id="682e2-491">If the containing function is an async function, control is returned to the current caller, and the result value, if any, is recorded in the return task as described in ([Enumerator interfaces](classes.md#enumerator-interfaces)).</span></span>

<span data-ttu-id="682e2-492">Так как `return` инструкции Безусловно передает управление в другом месте, конечная точка `return` инструкции никогда не доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-492">Because a `return` statement unconditionally transfers control elsewhere, the end point of a `return` statement is never reachable.</span></span>

### <a name="the-throw-statement"></a><span data-ttu-id="682e2-493">Оператор throw</span><span class="sxs-lookup"><span data-stu-id="682e2-493">The throw statement</span></span>

<span data-ttu-id="682e2-494">`throw` Оператор создает исключение.</span><span class="sxs-lookup"><span data-stu-id="682e2-494">The `throw` statement throws an exception.</span></span>

```antlr
throw_statement
    : 'throw' expression? ';'
    ;
```

<span data-ttu-id="682e2-495">Объект `throw` оператор с выражение создает значение, полученное путем вычисления выражения.</span><span class="sxs-lookup"><span data-stu-id="682e2-495">A `throw` statement with an expression throws the value produced by evaluating the expression.</span></span> <span data-ttu-id="682e2-496">Выражение должно представлять значение с типом класса `System.Exception`, типа класса, производного от `System.Exception` или типа параметра типа, имеющий `System.Exception` (или его подкласс) как его эффективным базовым классом.</span><span class="sxs-lookup"><span data-stu-id="682e2-496">The expression must denote a value of the class type `System.Exception`, of a class type that derives from `System.Exception` or of a type parameter type that has `System.Exception` (or a subclass thereof) as its effective base class.</span></span> <span data-ttu-id="682e2-497">Если при вычислении выражения создаются `null`, `System.NullReferenceException` вместо этого создается исключение.</span><span class="sxs-lookup"><span data-stu-id="682e2-497">If evaluation of the expression produces `null`, a `System.NullReferenceException` is thrown instead.</span></span>

<span data-ttu-id="682e2-498">Объект `throw` оператор выражения не может использоваться только в `catch` заблокировать, в этом случае этот оператор повторно создает исключение, которое в настоящее время обрабатывается, `catch` блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-498">A `throw` statement with no expression can be used only in a `catch` block, in which case that statement re-throws the exception that is currently being handled by that `catch` block.</span></span>

<span data-ttu-id="682e2-499">Так как `throw` инструкции Безусловно передает управление в другом месте, конечная точка `throw` инструкции никогда не доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-499">Because a `throw` statement unconditionally transfers control elsewhere, the end point of a `throw` statement is never reachable.</span></span>

<span data-ttu-id="682e2-500">При возникновении исключения управление передается первому `catch` предложение в вложенным `try` инструкцию, которая может обработать исключение.</span><span class="sxs-lookup"><span data-stu-id="682e2-500">When an exception is thrown, control is transferred to the first `catch` clause in an enclosing `try` statement that can handle the exception.</span></span> <span data-ttu-id="682e2-501">Процесс, который имеет место, начиная с момента этого исключения в точку передачи управления в подходящий обработчик исключений называется ***распространение исключений***.</span><span class="sxs-lookup"><span data-stu-id="682e2-501">The process that takes place from the point of the exception being thrown to the point of transferring control to a suitable exception handler is known as ***exception propagation***.</span></span> <span data-ttu-id="682e2-502">Распространение исключения сводится к повторению следующее до `catch` найти предложение, которое совпадает с исключением.</span><span class="sxs-lookup"><span data-stu-id="682e2-502">Propagation of an exception consists of repeatedly evaluating the following steps until a `catch` clause that matches the exception is found.</span></span> <span data-ttu-id="682e2-503">В этом описании ***точкой генерации*** изначально — расположение, по которому возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="682e2-503">In this description, the ***throw point*** is initially the location at which the exception is thrown.</span></span>

*  <span data-ttu-id="682e2-504">В текущей функции-члена каждой `try` инструкцию, которая содержит точку генерации проверяется.</span><span class="sxs-lookup"><span data-stu-id="682e2-504">In the current function member, each `try` statement that encloses the throw point is examined.</span></span> <span data-ttu-id="682e2-505">Для каждой инструкции `S`, начиная с самого внутреннего `try` инструкции и заканчивая самым внешним `try` инструкции, следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="682e2-505">For each statement `S`, starting with the innermost `try` statement and ending with the outermost `try` statement, the following steps are evaluated:</span></span>

   * <span data-ttu-id="682e2-506">Если `try` блока `S` содержит точку генерации и если S имеет один или несколько `catch` предложений, `catch` предложения проверяются в порядке их следования в поисках подходящего обработчика для исключения, в соответствии с правилами, заданными в Раздел [оператора try](statements.md#the-try-statement).</span><span class="sxs-lookup"><span data-stu-id="682e2-506">If the `try` block of `S` encloses the throw point and if S has one or more `catch` clauses, the `catch` clauses are examined in order of appearance to locate a suitable handler for the exception, according to the rules specified in Section [The try statement](statements.md#the-try-statement).</span></span> <span data-ttu-id="682e2-507">Если соответствующий `catch` находится предложение, распространение исключения завершается передачей управления в блок, `catch` предложение.</span><span class="sxs-lookup"><span data-stu-id="682e2-507">If a matching `catch` clause is located, the exception propagation is completed by transferring control to the block of that `catch` clause.</span></span>

   * <span data-ttu-id="682e2-508">В противном случае, если `try` блока или `catch` блока `S` содержит точку генерации и если `S` имеет `finally` блок, элемент управления передается `finally` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-508">Otherwise, if the `try` block or a `catch` block of `S` encloses the throw point and if `S` has a `finally` block, control is transferred to the `finally` block.</span></span> <span data-ttu-id="682e2-509">Если `finally` блок создает другое исключение, завершается обработка текущего исключения.</span><span class="sxs-lookup"><span data-stu-id="682e2-509">If the `finally` block throws another exception, processing of the current exception is terminated.</span></span> <span data-ttu-id="682e2-510">В противном случае, когда управление достигает конечной точки `finally` блока, продолжение обработки текущего исключения.</span><span class="sxs-lookup"><span data-stu-id="682e2-510">Otherwise, when control reaches the end point of the `finally` block, processing of the current exception is continued.</span></span>

*  <span data-ttu-id="682e2-511">Если обработчик исключений не находится в текущем вызове функции, вызов функции прекращается и происходит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="682e2-511">If an exception handler was not located in the current function invocation, the function invocation is terminated, and one of the following occurs:</span></span>

   * <span data-ttu-id="682e2-512">Если синхронные текущей функции, описанные выше действия повторяются для вызывающего функции с точкой throw, соответствующий инструкции, из которого была вызвана функция-член.</span><span class="sxs-lookup"><span data-stu-id="682e2-512">If the current function is non-async, the steps above are repeated for the caller of the function with a throw point corresponding to the statement from which the function member was invoked.</span></span>

   * <span data-ttu-id="682e2-513">Если текущая функция ключевых слов async и возвращающий задачу, исключение записывается в возвращаемое задачу, которая помещается в состояние faulted или отменено, как описано в разделе [интерфейсы перечислителя](classes.md#enumerator-interfaces).</span><span class="sxs-lookup"><span data-stu-id="682e2-513">If the current function is async and task-returning, the exception is recorded in the return task, which is put into a faulted or cancelled state as described in [Enumerator interfaces](classes.md#enumerator-interfaces).</span></span>

   * <span data-ttu-id="682e2-514">Если текущая функция ключевых слов async и возвращающие void, контекст синхронизации для текущего потока уведомляется, как описано в разделе [перечисляемые интерфейсы](classes.md#enumerable-interfaces).</span><span class="sxs-lookup"><span data-stu-id="682e2-514">If the current function is async and void-returning, the synchronization context of the current thread is notified as described in [Enumerable interfaces](classes.md#enumerable-interfaces).</span></span>

*  <span data-ttu-id="682e2-515">При обработке исключения, прерывание всех вызовов функций-членов в текущем потоке, указывающее, что поток не имеет обработчика для исключения, затем поток может сам завершен.</span><span class="sxs-lookup"><span data-stu-id="682e2-515">If the exception processing terminates all function member invocations in the current thread, indicating that the thread has no handler for the exception, then the thread is itself terminated.</span></span> <span data-ttu-id="682e2-516">Влияние прекращение их действия определяется реализацией.</span><span class="sxs-lookup"><span data-stu-id="682e2-516">The impact of such termination is implementation-defined.</span></span>

## <a name="the-try-statement"></a><span data-ttu-id="682e2-517">Оператор try</span><span class="sxs-lookup"><span data-stu-id="682e2-517">The try statement</span></span>

<span data-ttu-id="682e2-518">`try` Инструкция предоставляет механизм для перехвата исключений, возникающих во время выполнения блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-518">The `try` statement provides a mechanism for catching exceptions that occur during execution of a block.</span></span> <span data-ttu-id="682e2-519">Кроме того `try` инструкция предоставляет возможность указать блок кода, который выполняется всегда, когда элемент управления покидает `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-519">Furthermore, the `try` statement provides the ability to specify a block of code that is always executed when control leaves the `try` statement.</span></span>

```antlr
try_statement
    : 'try' block catch_clause+
    | 'try' block finally_clause
    | 'try' block catch_clause+ finally_clause
    ;

catch_clause
    : 'catch' exception_specifier? exception_filter?  block
    ;

exception_specifier
    : '(' type identifier? ')'
    ;

exception_filter
    : 'when' '(' expression ')'
    ;

finally_clause
    : 'finally' block
    ;
```

<span data-ttu-id="682e2-520">Существует три возможных форм `try` инструкции:</span><span class="sxs-lookup"><span data-stu-id="682e2-520">There are three possible forms of `try` statements:</span></span>

*  <span data-ttu-id="682e2-521">Объект `try` блока, а затем по одному или нескольким `catch` блоков.</span><span class="sxs-lookup"><span data-stu-id="682e2-521">A `try` block followed by one or more `catch` blocks.</span></span>
*  <span data-ttu-id="682e2-522">Объект `try` блока, за которым следует `finally` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-522">A `try` block followed by a `finally` block.</span></span>
*  <span data-ttu-id="682e2-523">Объект `try` блока, а затем по одному или нескольким `catch` блоки, за которым следует `finally` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-523">A `try` block followed by one or more `catch` blocks followed by a `finally` block.</span></span>

<span data-ttu-id="682e2-524">При `catch` предложение указывает *exception_specifier*, тип должен быть `System.Exception`, тип, который является производным от `System.Exception` или параметра типа, имеющего `System.Exception` (или его подкласс) как его вступают в силу базовый класс.</span><span class="sxs-lookup"><span data-stu-id="682e2-524">When a `catch` clause specifies an *exception_specifier*, the type must be `System.Exception`, a type that derives from `System.Exception` or a type parameter type that has `System.Exception` (or a subclass thereof) as its effective base class.</span></span>

<span data-ttu-id="682e2-525">Когда `catch` предложение указывает оба *exception_specifier* с *идентификатор*, ***переменной исключения*** заданное имя и тип объявлен.</span><span class="sxs-lookup"><span data-stu-id="682e2-525">When a `catch` clause specifies both an *exception_specifier* with an *identifier*, an ***exception variable*** of the given name and type is declared.</span></span> <span data-ttu-id="682e2-526">Переменная исключения соответствует локальной переменной с областью, охватывающей `catch` предложение.</span><span class="sxs-lookup"><span data-stu-id="682e2-526">The exception variable corresponds to a local variable with a scope that extends over the `catch` clause.</span></span> <span data-ttu-id="682e2-527">Во время выполнения *exception_filter* и *блок*, переменная исключения представляет исключение, обрабатываемое в данный момент.</span><span class="sxs-lookup"><span data-stu-id="682e2-527">During execution of the *exception_filter* and *block*, the exception variable represents the exception currently being handled.</span></span> <span data-ttu-id="682e2-528">В целях проверки определенного присваивания переменной исключения считается определенно присвоенной во всей области действия.</span><span class="sxs-lookup"><span data-stu-id="682e2-528">For purposes of definite assignment checking, the exception variable is considered definitely assigned in its entire scope.</span></span>

<span data-ttu-id="682e2-529">Если не `catch` предложение включает в себя имя переменной исключения, вы не сможете получить доступ к объекту исключения в фильтре и `catch` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-529">Unless a `catch` clause includes an exception variable name, it is impossible to access the exception object in the filter and `catch` block.</span></span>

<span data-ttu-id="682e2-530">Объект `catch` предложение, которое не соответствует *exception_specifier* вызывается общего `catch` предложение.</span><span class="sxs-lookup"><span data-stu-id="682e2-530">A `catch` clause that does not specify an *exception_specifier* is called a general `catch` clause.</span></span>

<span data-ttu-id="682e2-531">Некоторые языки программирования могут поддерживать исключения, которые не может быть представлен как объект, производный от `System.Exception`, несмотря на то, что такие исключения не генерируются кодом C#.</span><span class="sxs-lookup"><span data-stu-id="682e2-531">Some programming languages may support exceptions that are not representable as an object derived from `System.Exception`, although such exceptions could never be generated by C# code.</span></span> <span data-ttu-id="682e2-532">Общая `catch` предложение может использоваться для перехвата таких исключений.</span><span class="sxs-lookup"><span data-stu-id="682e2-532">A general `catch` clause may be used to catch such exceptions.</span></span> <span data-ttu-id="682e2-533">Таким образом, общая `catch` предложение является семантически отличной от одного, которое указывает тип `System.Exception`, в том, что первое из них может также перехватывать исключения из других языков.</span><span class="sxs-lookup"><span data-stu-id="682e2-533">Thus, a general `catch` clause is semantically different from one that specifies the type `System.Exception`, in that the former may also catch exceptions from other languages.</span></span>

<span data-ttu-id="682e2-534">Чтобы обнаружить обработчик для исключения, `catch` предложения проверяются в лексическом порядке.</span><span class="sxs-lookup"><span data-stu-id="682e2-534">In order to locate a handler for an exception, `catch` clauses are examined in lexical order.</span></span> <span data-ttu-id="682e2-535">Если `catch` предложение указывает тип, но не фильтр исключений, возникает ошибка времени компиляции для более поздней версии `catch` предложение в том же `try` инструкцию, чтобы указать тип, совпадает или является производным от, что тип.</span><span class="sxs-lookup"><span data-stu-id="682e2-535">If a `catch` clause specifies a type but no exception filter, it is a compile-time error for a later `catch` clause in the same `try` statement to specify a type that is the same as, or is derived from, that type.</span></span> <span data-ttu-id="682e2-536">Если `catch` предложение указывает без типа и без фильтра, он должен находиться в конце `catch` предложение для этого `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-536">If a `catch` clause specifies no type and no filter, it must be the last `catch` clause for that `try` statement.</span></span>

<span data-ttu-id="682e2-537">В рамках `catch` блока, `throw` инструкции ([инструкция throw](statements.md#the-throw-statement)) без выражения может использоваться для повторного вызова исключения, которое было перехвачено `catch` блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-537">Within a `catch` block, a `throw` statement ([The throw statement](statements.md#the-throw-statement)) with no expression can be used to re-throw the exception that was caught by the `catch` block.</span></span> <span data-ttu-id="682e2-538">Назначения переменной исключения не изменяют исключение выдается заново.</span><span class="sxs-lookup"><span data-stu-id="682e2-538">Assignments to an exception variable do not alter the exception that is re-thrown.</span></span>

<span data-ttu-id="682e2-539">В примере</span><span class="sxs-lookup"><span data-stu-id="682e2-539">In the example</span></span>
```csharp
using System;

class Test
{
    static void F() {
        try {
            G();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in F: " + e.Message);
            e = new Exception("F");
            throw;                // re-throw
        }
    }

    static void G() {
        throw new Exception("G");
    }

    static void Main() {
        try {
            F();
        }
        catch (Exception e) {
            Console.WriteLine("Exception in Main: " + e.Message);
        }
    }
}
```
<span data-ttu-id="682e2-540">метод `F` перехватывает исключение, записывает диагностическую информацию в консоль, изменяет переменную исключения и повторно создает исключение.</span><span class="sxs-lookup"><span data-stu-id="682e2-540">the method `F` catches an exception, writes some diagnostic information to the console, alters the exception variable, and re-throws the exception.</span></span> <span data-ttu-id="682e2-541">Исключение, которое выдается повторно является исходное исключение, поэтому выходные данные:</span><span class="sxs-lookup"><span data-stu-id="682e2-541">The exception that is re-thrown is the original exception, so the output produced is:</span></span>
```
Exception in F: G
Exception in Main: G
```

<span data-ttu-id="682e2-542">Если исключение первого блока catch `e` вместо повторного создания текущего исключения, выходные данные будет выглядеть следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-542">If the first catch block had thrown `e` instead of rethrowing the current exception, the output produced would be as follows:</span></span>
```csharp
Exception in F: G
Exception in Main: F
```

<span data-ttu-id="682e2-543">Произошла ошибка во время компиляции для `break`, `continue`, или `goto` инструкции для передачи управления из `finally` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-543">It is a compile-time error for a `break`, `continue`, or `goto` statement to transfer control out of a `finally` block.</span></span> <span data-ttu-id="682e2-544">При `break`, `continue`, или `goto` инструкция `finally` блок целевого объекта инструкции должно быть в пределах одного `finally` блок, или в противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="682e2-544">When a `break`, `continue`, or `goto` statement occurs in a `finally` block, the target of the statement must be within the same `finally` block, or otherwise a compile-time error occurs.</span></span>

<span data-ttu-id="682e2-545">Произошла ошибка во время компиляции для `return` инструкции в `finally` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-545">It is a compile-time error for a `return` statement to occur in a `finally` block.</span></span>

<span data-ttu-id="682e2-546">Объект `try` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-546">A `try` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-547">Управление передается `try` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-547">Control is transferred to the `try` block.</span></span>
*  <span data-ttu-id="682e2-548">Если элемент управления достигает конечной точки `try` блок:</span><span class="sxs-lookup"><span data-stu-id="682e2-548">When and if control reaches the end point of the `try` block:</span></span>
   *  <span data-ttu-id="682e2-549">Если `try` инструкция имеет `finally` блока, `finally` выполняется блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-549">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
   *  <span data-ttu-id="682e2-550">Управление передается в конечную точку `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-550">Control is transferred to the end point of the `try` statement.</span></span>

*  <span data-ttu-id="682e2-551">Если исключение распространяется на `try` инструкции во время выполнения `try` блок:</span><span class="sxs-lookup"><span data-stu-id="682e2-551">If an exception is propagated to the `try` statement during execution of the `try` block:</span></span>
   *  <span data-ttu-id="682e2-552">`catch` Предложения, если таковые имеются, проверяются в порядке их следования в поисках подходящего обработчика для исключения.</span><span class="sxs-lookup"><span data-stu-id="682e2-552">The `catch` clauses, if any, are examined in order of appearance to locate a suitable handler for the exception.</span></span> <span data-ttu-id="682e2-553">Если `catch` предложение не указывать тип или указывает тип исключения или базовый тип типа исключения:</span><span class="sxs-lookup"><span data-stu-id="682e2-553">If a `catch` clause does not specify a type, or specifies the exception type or a base type of the exception type:</span></span>
      *  <span data-ttu-id="682e2-554">Если `catch` предложение объявляет переменную исключения, объект исключения присваивается переменной исключения.</span><span class="sxs-lookup"><span data-stu-id="682e2-554">If the `catch` clause declares an exception variable, the exception object is assigned to the exception variable.</span></span>
      *  <span data-ttu-id="682e2-555">Если `catch` предложение объявляет фильтр исключений, оценка фильтра.</span><span class="sxs-lookup"><span data-stu-id="682e2-555">If the `catch` clause declares an exception filter, the filter is evaluated.</span></span> <span data-ttu-id="682e2-556">Если результат вычисления равен `false`, предложение catch не является результатом того, поиск продолжается через все последующие `catch` предложений для подходящего обработчика.</span><span class="sxs-lookup"><span data-stu-id="682e2-556">If it evaluates to `false`, the catch clause is not a match, and the search continues through any subsequent `catch` clauses for a suitable handler.</span></span>
      *  <span data-ttu-id="682e2-557">В противном случае `catch` предложение считается соответствующим, а управление передается соответствующий `catch` блока.</span><span class="sxs-lookup"><span data-stu-id="682e2-557">Otherwise, the `catch` clause is considered a match, and control is transferred to the matching `catch` block.</span></span>
      *  <span data-ttu-id="682e2-558">Если элемент управления достигает конечной точки `catch` блок:</span><span class="sxs-lookup"><span data-stu-id="682e2-558">When and if control reaches the end point of the `catch` block:</span></span>
         * <span data-ttu-id="682e2-559">Если `try` инструкция имеет `finally` блока, `finally` выполняется блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-559">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
         * <span data-ttu-id="682e2-560">Управление передается в конечную точку `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-560">Control is transferred to the end point of the `try` statement.</span></span>
      *  <span data-ttu-id="682e2-561">Если исключение распространяется на `try` инструкции во время выполнения `catch` блок:</span><span class="sxs-lookup"><span data-stu-id="682e2-561">If an exception is propagated to the `try` statement during execution of the `catch` block:</span></span>
         *  <span data-ttu-id="682e2-562">Если `try` инструкция имеет `finally` блока, `finally` выполняется блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-562">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
         *  <span data-ttu-id="682e2-563">Исключение передается далее заключающему `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-563">The exception is propagated to the next enclosing `try` statement.</span></span>
   *  <span data-ttu-id="682e2-564">Если `try` инструкция не `catch` предложений или нет ни одной `catch` предложение совпадает с исключением:</span><span class="sxs-lookup"><span data-stu-id="682e2-564">If the `try` statement has no `catch` clauses or if no `catch` clause matches the exception:</span></span>
      *  <span data-ttu-id="682e2-565">Если `try` инструкция имеет `finally` блока, `finally` выполняется блок.</span><span class="sxs-lookup"><span data-stu-id="682e2-565">If the `try` statement has a `finally` block, the `finally` block is executed.</span></span>
      *  <span data-ttu-id="682e2-566">Исключение передается далее заключающему `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-566">The exception is propagated to the next enclosing `try` statement.</span></span>

<span data-ttu-id="682e2-567">Операторы `finally` блок всегда выполняются, когда элемент управления покидает `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-567">The statements of a `finally` block are always executed when control leaves a `try` statement.</span></span> <span data-ttu-id="682e2-568">Это верно, происходит ли передачу управления результате нормального выполнения, в результате выполнения `break`, `continue`, `goto`, или `return` инструкции, или в результате распространения исключения из `try` инструкция.</span><span class="sxs-lookup"><span data-stu-id="682e2-568">This is true whether the control transfer occurs as a result of normal execution, as a result of executing a `break`, `continue`, `goto`, or `return` statement, or as a result of propagating an exception out of the `try` statement.</span></span>

<span data-ttu-id="682e2-569">Если возникает исключение во время выполнения `finally` блокировать и не перехватывается внутри того же блока finally, исключение распространяется Далее заключающему `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-569">If an exception is thrown during execution of a `finally` block, and is not caught within the same finally block, the exception is propagated to the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-570">Если в этот момент распространялось другое исключение, это исключение будет потеряно.</span><span class="sxs-lookup"><span data-stu-id="682e2-570">If another exception was in the process of being propagated, that exception is lost.</span></span> <span data-ttu-id="682e2-571">Процесс распространения исключения рассматривается далее в описание `throw` инструкции ([оператор throw](statements.md#the-throw-statement)).</span><span class="sxs-lookup"><span data-stu-id="682e2-571">The process of propagating an exception is discussed further in the description of the `throw` statement ([The throw statement](statements.md#the-throw-statement)).</span></span>

<span data-ttu-id="682e2-572">`try` Блока `try` оператор достижим Если `try` оператор достижим.</span><span class="sxs-lookup"><span data-stu-id="682e2-572">The `try` block of a `try` statement is reachable if the `try` statement is reachable.</span></span>

<span data-ttu-id="682e2-573">Объект `catch` блока `try` оператор достижим Если `try` оператор достижим.</span><span class="sxs-lookup"><span data-stu-id="682e2-573">A `catch` block of a `try` statement is reachable if the `try` statement is reachable.</span></span>

<span data-ttu-id="682e2-574">`finally` Блока `try` оператор достижим Если `try` оператор достижим.</span><span class="sxs-lookup"><span data-stu-id="682e2-574">The `finally` block of a `try` statement is reachable if the `try` statement is reachable.</span></span>

<span data-ttu-id="682e2-575">Конечная точка `try` инструкции доступен, если выполняются оба следующих условия:</span><span class="sxs-lookup"><span data-stu-id="682e2-575">The end point of a `try` statement is reachable if both of the following are true:</span></span>

*  <span data-ttu-id="682e2-576">Конечная точка `try` блок доступен, или точка конца по крайней мере один `catch` блок доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-576">The end point of the `try` block is reachable or the end point of at least one `catch` block is reachable.</span></span>
*  <span data-ttu-id="682e2-577">Если `finally` имеется блок, конечная точка `finally` блок доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-577">If a `finally` block is present, the end point of the `finally` block is reachable.</span></span>

## <a name="the-checked-and-unchecked-statements"></a><span data-ttu-id="682e2-578">Операторы checked и unchecked</span><span class="sxs-lookup"><span data-stu-id="682e2-578">The checked and unchecked statements</span></span>

<span data-ttu-id="682e2-579">`checked` И `unchecked` инструкции используются для управления ***контекстом проверки переполнения*** для целочисленных арифметических операций и преобразований.</span><span class="sxs-lookup"><span data-stu-id="682e2-579">The `checked` and `unchecked` statements are used to control the ***overflow checking context*** for integral-type arithmetic operations and conversions.</span></span>

```antlr
checked_statement
    : 'checked' block
    ;

unchecked_statement
    : 'unchecked' block
    ;
```

<span data-ttu-id="682e2-580">`checked` Инструкция вызывает все выражения в *блок* в проверяемом контексте и `unchecked` инструкция вызывает все выражения в *блок* в непроверенный контекст.</span><span class="sxs-lookup"><span data-stu-id="682e2-580">The `checked` statement causes all expressions in the *block* to be evaluated in a checked context, and the `unchecked` statement causes all expressions in the *block* to be evaluated in an unchecked context.</span></span>

<span data-ttu-id="682e2-581">`checked` И `unchecked` инструкций будут точными эквивалентами `checked` и `unchecked` операторы ([операторы checked и unchecked](expressions.md#the-checked-and-unchecked-operators)), за исключением того, что они работают на блоки вместо выражения .</span><span class="sxs-lookup"><span data-stu-id="682e2-581">The `checked` and `unchecked` statements are precisely equivalent to the `checked` and `unchecked` operators ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)), except that they operate on blocks instead of expressions.</span></span>

## <a name="the-lock-statement"></a><span data-ttu-id="682e2-582">В операторе lock</span><span class="sxs-lookup"><span data-stu-id="682e2-582">The lock statement</span></span>

<span data-ttu-id="682e2-583">`lock` Инструкция получает взаимоисключающую блокировку для заданного объекта, выполняет инструкцию и затем снимает блокировку.</span><span class="sxs-lookup"><span data-stu-id="682e2-583">The `lock` statement obtains the mutual-exclusion lock for a given object, executes a statement, and then releases the lock.</span></span>

```antlr
lock_statement
    : 'lock' '(' expression ')' embedded_statement
    ;
```

<span data-ttu-id="682e2-584">Выражение `lock` инструкции должно представлять значение типа, известные как *reference_type*.</span><span class="sxs-lookup"><span data-stu-id="682e2-584">The expression of a `lock` statement must denote a value of a type known to be a *reference_type*.</span></span> <span data-ttu-id="682e2-585">Преобразование не неявная упаковка-преобразование ([осуществлять преобразования-упаковки](conversions.md#boxing-conversions)) никогда не выполняется для выражения `lock` инструкции и, таким образом является ошибкой во время компиляции, чтобы выражение обозначало значение *value_type*.</span><span class="sxs-lookup"><span data-stu-id="682e2-585">No implicit boxing conversion ([Boxing conversions](conversions.md#boxing-conversions)) is ever performed for the expression of a `lock` statement, and thus it is a compile-time error for the expression to denote a value of a *value_type*.</span></span>

<span data-ttu-id="682e2-586">Объект `lock` инструкции формы</span><span class="sxs-lookup"><span data-stu-id="682e2-586">A `lock` statement of the form</span></span>
```csharp
lock (x) ...
```
<span data-ttu-id="682e2-587">где `x` выражение *reference_type*, является точным эквивалентом</span><span class="sxs-lookup"><span data-stu-id="682e2-587">where `x` is an expression of a *reference_type*, is precisely equivalent to</span></span>
```csharp
bool __lockWasTaken = false;
try {
    System.Threading.Monitor.Enter(x, ref __lockWasTaken);
    ...
}
finally {
    if (__lockWasTaken) System.Threading.Monitor.Exit(x);
}
```
<span data-ttu-id="682e2-588">за исключением того, что `x` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="682e2-588">except that `x` is only evaluated once.</span></span>

<span data-ttu-id="682e2-589">Во время блокировки взаимного исключения, код, выполняемый в одном потоке выполнения можно также получить и снятия блокировки.</span><span class="sxs-lookup"><span data-stu-id="682e2-589">While a mutual-exclusion lock is held, code executing in the same execution thread can also obtain and release the lock.</span></span> <span data-ttu-id="682e2-590">Тем не менее код, выполняемый в других потоках блокируется получение блокировки до снятия блокировки.</span><span class="sxs-lookup"><span data-stu-id="682e2-590">However, code executing in other threads is blocked from obtaining the lock until the lock is released.</span></span>

<span data-ttu-id="682e2-591">Блокировка `System.Type` объекты для синхронизации доступа к статическим данным не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="682e2-591">Locking `System.Type` objects in order to synchronize access to static data is not recommended.</span></span> <span data-ttu-id="682e2-592">Другой код может быть заблокирован тот же тип, что может привести к взаимоблокировке.</span><span class="sxs-lookup"><span data-stu-id="682e2-592">Other code might lock on the same type, which can result in deadlock.</span></span> <span data-ttu-id="682e2-593">Лучшим подходом является для синхронизации доступа к статическим данным, заблокировав закрытый статический объект.</span><span class="sxs-lookup"><span data-stu-id="682e2-593">A better approach is to synchronize access to static data by locking a private static object.</span></span> <span data-ttu-id="682e2-594">Пример:</span><span class="sxs-lookup"><span data-stu-id="682e2-594">For example:</span></span>
```csharp
class Cache
{
    private static readonly object synchronizationObject = new object();

    public static void Add(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }

    public static void Remove(object x) {
        lock (Cache.synchronizationObject) {
            ...
        }
    }
}
```

## <a name="the-using-statement"></a><span data-ttu-id="682e2-595">Оператор using</span><span class="sxs-lookup"><span data-stu-id="682e2-595">The using statement</span></span>

<span data-ttu-id="682e2-596">`using` Инструкция получает один или несколько ресурсов, выполняет инструкцию и затем удаляет ресурс.</span><span class="sxs-lookup"><span data-stu-id="682e2-596">The `using` statement obtains one or more resources, executes a statement, and then disposes of the resource.</span></span>

```antlr
using_statement
    : 'using' '(' resource_acquisition ')' embedded_statement
    ;

resource_acquisition
    : local_variable_declaration
    | expression
    ;
```

<span data-ttu-id="682e2-597">Объект ***ресурсов*** — это класс или структура, реализующие `System.IDisposable`, который включает один метод без параметров, с именем `Dispose`.</span><span class="sxs-lookup"><span data-stu-id="682e2-597">A ***resource*** is a class or struct that implements `System.IDisposable`, which includes a single parameterless method named `Dispose`.</span></span> <span data-ttu-id="682e2-598">Код, использующий ресурс может вызвать `Dispose` для указания, что ресурс больше не нужен.</span><span class="sxs-lookup"><span data-stu-id="682e2-598">Code that is using a resource can call `Dispose` to indicate that the resource is no longer needed.</span></span> <span data-ttu-id="682e2-599">Если `Dispose` не вызывается, то автоматически со временем возникает в результате сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="682e2-599">If `Dispose` is not called, then automatic disposal eventually occurs as a consequence of garbage collection.</span></span>

<span data-ttu-id="682e2-600">Если виде *resource_acquisition* — *local_variable_declaration* то типом *local_variable_declaration* должен быть либо `dynamic` или тип который может быть неявно преобразован в `System.IDisposable`.</span><span class="sxs-lookup"><span data-stu-id="682e2-600">If the form of *resource_acquisition* is *local_variable_declaration* then the type of the *local_variable_declaration* must be either `dynamic` or a type that can be implicitly converted to `System.IDisposable`.</span></span> <span data-ttu-id="682e2-601">Если виде *resource_acquisition* — *выражение* затем этого выражения должны неявно преобразовываться в `System.IDisposable`.</span><span class="sxs-lookup"><span data-stu-id="682e2-601">If the form of *resource_acquisition* is *expression* then this expression must be implicitly convertible to `System.IDisposable`.</span></span>

<span data-ttu-id="682e2-602">Локальные переменные, объявленные в *resource_acquisition* доступны только для чтения и должны включать инициализатор.</span><span class="sxs-lookup"><span data-stu-id="682e2-602">Local variables declared in a *resource_acquisition* are read-only, and must include an initializer.</span></span> <span data-ttu-id="682e2-603">Ошибка времени компиляции возникает, если внедренный оператор пытается изменить эти локальные переменные (с помощью присваивания или `++` и `--` операторы), получить адрес их или передавать их в виде `ref` или `out` параметров.</span><span class="sxs-lookup"><span data-stu-id="682e2-603">A compile-time error occurs if the embedded statement attempts to modify these local variables (via assignment or the `++` and `--` operators) , take the address of them, or pass them as `ref` or `out` parameters.</span></span>

<span data-ttu-id="682e2-604">Объект `using` инструкция преобразуется в состоит из трех частей: приобретения, использование и удаление.</span><span class="sxs-lookup"><span data-stu-id="682e2-604">A `using` statement is translated into three parts: acquisition, usage, and disposal.</span></span> <span data-ttu-id="682e2-605">Использование ресурса неявно включается в `try` инструкция, включающая `finally` предложение.</span><span class="sxs-lookup"><span data-stu-id="682e2-605">Usage of the resource is implicitly enclosed in a `try` statement that includes a `finally` clause.</span></span> <span data-ttu-id="682e2-606">Это `finally` предложение удаляет ресурс.</span><span class="sxs-lookup"><span data-stu-id="682e2-606">This `finally` clause disposes of the resource.</span></span> <span data-ttu-id="682e2-607">Если `null` ресурс запрашивается, затем вызов `Dispose` производится, и исключение не создается.</span><span class="sxs-lookup"><span data-stu-id="682e2-607">If a `null` resource is acquired, then no call to `Dispose` is made, and no exception is thrown.</span></span> <span data-ttu-id="682e2-608">Если ресурс типа `dynamic` преобразуется динамически через неявное преобразование динамических ([неявные преобразования динамических](conversions.md#implicit-dynamic-conversions)) к `IDisposable` во время приобретения, чтобы обеспечить преобразование успешно выполнена до использования и реализации.</span><span class="sxs-lookup"><span data-stu-id="682e2-608">If the resource is of type `dynamic` it is dynamically converted through an implicit dynamic conversion ([Implicit dynamic conversions](conversions.md#implicit-dynamic-conversions)) to `IDisposable` during acquisition in order to ensure that the conversion is successful before the usage and disposal.</span></span>

<span data-ttu-id="682e2-609">Объект `using` инструкции формы</span><span class="sxs-lookup"><span data-stu-id="682e2-609">A `using` statement of the form</span></span>
```csharp
using (ResourceType resource = expression) statement
```
<span data-ttu-id="682e2-610">соответствует одному из тремя способами.</span><span class="sxs-lookup"><span data-stu-id="682e2-610">corresponds to one of three possible expansions.</span></span> <span data-ttu-id="682e2-611">Когда `ResourceType` является типом значения, не допускающие значения NULL, является развертывание</span><span class="sxs-lookup"><span data-stu-id="682e2-611">When `ResourceType` is a non-nullable value type, the expansion is</span></span>
```csharp
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        ((IDisposable)resource).Dispose();
    }
}
```

<span data-ttu-id="682e2-612">В противном случае, если `ResourceType` имеет значение NULL или ссылочным типом, кроме `dynamic`, расширение</span><span class="sxs-lookup"><span data-stu-id="682e2-612">Otherwise, when `ResourceType` is a nullable value type or a reference type other than `dynamic`, the expansion is</span></span>
```csharp
{
    ResourceType resource = expression;
    try {
        statement;
    }
    finally {
        if (resource != null) ((IDisposable)resource).Dispose();
    }
}
```

<span data-ttu-id="682e2-613">В противном случае, если `ResourceType` является `dynamic`, расширение</span><span class="sxs-lookup"><span data-stu-id="682e2-613">Otherwise, when `ResourceType` is `dynamic`, the expansion is</span></span>
```csharp
{
    ResourceType resource = expression;
    IDisposable d = (IDisposable)resource;
    try {
        statement;
    }
    finally {
        if (d != null) d.Dispose();
    }
}
```

<span data-ttu-id="682e2-614">В обоих `resource` переменная доступна только для чтения в внедренный оператор и `d` переменная недоступна и невидимым для внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-614">In either expansion, the `resource` variable is read-only in the embedded statement, and the `d` variable is inaccessible in, and invisible to, the embedded statement.</span></span>

<span data-ttu-id="682e2-615">Реализация может реализовать с помощью инструкциях по-разному, например, для повышения производительности, до тех пор, пока поведение согласуется с выше расширения.</span><span class="sxs-lookup"><span data-stu-id="682e2-615">An implementation is permitted to implement a given using-statement differently, e.g. for performance reasons, as long as the behavior is consistent with the above expansion.</span></span>

<span data-ttu-id="682e2-616">Объект `using` инструкции формы</span><span class="sxs-lookup"><span data-stu-id="682e2-616">A `using` statement of the form</span></span>
```csharp
using (expression) statement
```
<span data-ttu-id="682e2-617">имеет же тремя способами.</span><span class="sxs-lookup"><span data-stu-id="682e2-617">has the same three possible expansions.</span></span> <span data-ttu-id="682e2-618">В этом случае `ResourceType` неявно имеет тип времени компиляции `expression`, если он имеется.</span><span class="sxs-lookup"><span data-stu-id="682e2-618">In this case `ResourceType` is implicitly the compile-time type of the `expression`, if it has one.</span></span> <span data-ttu-id="682e2-619">В противном случае интерфейс `IDisposable` сам используется в качестве `ResourceType`.</span><span class="sxs-lookup"><span data-stu-id="682e2-619">Otherwise the interface `IDisposable` itself is used as the `ResourceType`.</span></span> <span data-ttu-id="682e2-620">`resource` Переменной недоступна и невидимым для внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="682e2-620">The `resource` variable is inaccessible in, and invisible to, the embedded statement.</span></span>

<span data-ttu-id="682e2-621">Когда *resource_acquisition* принимает форму *local_variable_declaration*, имеется возможность присоединять несколько ресурсов данного типа.</span><span class="sxs-lookup"><span data-stu-id="682e2-621">When a *resource_acquisition* takes the form of a *local_variable_declaration*, it is possible to acquire multiple resources of a given type.</span></span> <span data-ttu-id="682e2-622">Объект `using` инструкции формы</span><span class="sxs-lookup"><span data-stu-id="682e2-622">A `using` statement of the form</span></span>
```csharp
using (ResourceType r1 = e1, r2 = e2, ..., rN = eN) statement
```
<span data-ttu-id="682e2-623">вложен точно эквивалентен последовательность `using` инструкции:</span><span class="sxs-lookup"><span data-stu-id="682e2-623">is precisely equivalent to a sequence of nested `using` statements:</span></span>
```csharp
using (ResourceType r1 = e1)
    using (ResourceType r2 = e2)
        ...
            using (ResourceType rN = eN)
                statement
```

<span data-ttu-id="682e2-624">В приведенном ниже примере создается файл с именем `log.txt` и записывает две строки текста в файл.</span><span class="sxs-lookup"><span data-stu-id="682e2-624">The example below creates a file named `log.txt` and writes two lines of text to the file.</span></span> <span data-ttu-id="682e2-625">В примере затем открывается один и тот же файл для чтения и копирует автономной строки текста в консоль.</span><span class="sxs-lookup"><span data-stu-id="682e2-625">The example then opens that same file for reading and copies the contained lines of text to the console.</span></span>
```csharp
using System;
using System.IO;

class Test
{
    static void Main() {
        using (TextWriter w = File.CreateText("log.txt")) {
            w.WriteLine("This is line one");
            w.WriteLine("This is line two");
        }

        using (TextReader r = File.OpenText("log.txt")) {
            string s;
            while ((s = r.ReadLine()) != null) {
                Console.WriteLine(s);
            }

        }
    }
}
```

<span data-ttu-id="682e2-626">Так как `TextWriter` и `TextReader` классы реализуют `IDisposable` интерфейс, можно использовать пример `using` инструкции для операций чтения или убедитесь, что следующие записи в базовый файл правильно закрыты.</span><span class="sxs-lookup"><span data-stu-id="682e2-626">Since the `TextWriter` and `TextReader` classes implement the `IDisposable` interface, the example can use `using` statements to ensure that the underlying file is properly closed following the write or read operations.</span></span>

## <a name="the-yield-statement"></a><span data-ttu-id="682e2-627">Оператор yield</span><span class="sxs-lookup"><span data-stu-id="682e2-627">The yield statement</span></span>

<span data-ttu-id="682e2-628">`yield` Оператор используется в блоке итератора ([блоки](statements.md#blocks)) для объекта перечислителя оператор yield ([объекты перечислителя](classes.md#enumerator-objects)) или перечисляемый объект ([перечисляемых объектов](classes.md#enumerable-objects)) итератор или для обозначения конца итерации.</span><span class="sxs-lookup"><span data-stu-id="682e2-628">The `yield` statement is used in an iterator block ([Blocks](statements.md#blocks)) to yield a value to the enumerator object ([Enumerator objects](classes.md#enumerator-objects)) or enumerable object ([Enumerable objects](classes.md#enumerable-objects)) of an iterator or to signal the end of the iteration.</span></span>

```antlr
yield_statement
    : 'yield' 'return' expression ';'
    | 'yield' 'break' ';'
    ;
```

<span data-ttu-id="682e2-629">`yield` не является зарезервированным словом. он имеет специальное значение только в том случае, когда стоит непосредственно перед `return` или `break` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="682e2-629">`yield` is not a reserved word; it has special meaning only when used immediately before a `return` or `break` keyword.</span></span> <span data-ttu-id="682e2-630">В других контекстах `yield` можно использовать в качестве идентификатора.</span><span class="sxs-lookup"><span data-stu-id="682e2-630">In other contexts, `yield` can be used as an identifier.</span></span>

<span data-ttu-id="682e2-631">Существует ряд ограничений, о том, где `yield` оператор может использоваться, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="682e2-631">There are several restrictions on where a `yield` statement can appear, as described in the following.</span></span>

*  <span data-ttu-id="682e2-632">Произошла ошибка во время компиляции для `yield` инструкции (из двух форм) вне *method_body*, *operator_body* или *accessor_body*</span><span class="sxs-lookup"><span data-stu-id="682e2-632">It is a compile-time error for a `yield` statement (of either form) to appear outside a *method_body*, *operator_body* or *accessor_body*</span></span>
*  <span data-ttu-id="682e2-633">Произошла ошибка во время компиляции для `yield` инструкции (из двух форм) для отображения внутри анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="682e2-633">It is a compile-time error for a `yield` statement (of either form) to appear inside an anonymous function.</span></span>
*  <span data-ttu-id="682e2-634">Произошла ошибка во время компиляции для `yield` инструкции (из двух форм) в `finally` предложении `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-634">It is a compile-time error for a `yield` statement (of either form) to appear in the `finally` clause of a `try` statement.</span></span>
*  <span data-ttu-id="682e2-635">Произошла ошибка во время компиляции для `yield return` инструкцию, чтобы находиться в любом месте `try` инструкцию, которая содержит любые `catch` предложения.</span><span class="sxs-lookup"><span data-stu-id="682e2-635">It is a compile-time error for a `yield return` statement to appear anywhere in a `try` statement that contains any `catch` clauses.</span></span>

<span data-ttu-id="682e2-636">В следующем примере показано несколько допустимых и недопустимых способов использования `yield` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-636">The following example shows some valid and invalid uses of `yield` statements.</span></span>

```csharp
delegate IEnumerable<int> D();

IEnumerator<int> GetEnumerator() {
    try {
        yield return 1;        // Ok
        yield break;           // Ok
    }
    finally {
        yield return 2;        // Error, yield in finally
        yield break;           // Error, yield in finally
    }

    try {
        yield return 3;        // Error, yield return in try...catch
        yield break;           // Ok
    }
    catch {
        yield return 4;        // Error, yield return in try...catch
        yield break;           // Ok
    }

    D d = delegate { 
        yield return 5;        // Error, yield in an anonymous function
    }; 
}

int MyMethod() {
    yield return 1;            // Error, wrong return type for an iterator block
}
```

<span data-ttu-id="682e2-637">Неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) должен существовать из типа выражения в `yield return` инструкции в тип результата ([Yield типа](classes.md#yield-type)) итератора.</span><span class="sxs-lookup"><span data-stu-id="682e2-637">An implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) must exist from the type of the expression in the `yield return` statement to the yield type ([Yield type](classes.md#yield-type)) of the iterator.</span></span>

<span data-ttu-id="682e2-638">Объект `yield return` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-638">A `yield return` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-639">Выражение, заданное в инструкции вычисляется, неявно преобразован в тип результата и назначенные `Current` свойство объекта перечислителя.</span><span class="sxs-lookup"><span data-stu-id="682e2-639">The expression given in the statement is evaluated, implicitly converted to the yield type, and assigned to the `Current` property of the enumerator object.</span></span>
*  <span data-ttu-id="682e2-640">Выполнение блока итератора приостанавливается.</span><span class="sxs-lookup"><span data-stu-id="682e2-640">Execution of the iterator block is suspended.</span></span> <span data-ttu-id="682e2-641">Если `yield return` оператор находится внутри одного или нескольких `try` блокирует, сопоставленного `finally` блоки не выполняются в данный момент.</span><span class="sxs-lookup"><span data-stu-id="682e2-641">If the `yield return` statement is within one or more `try` blocks, the associated `finally` blocks are not executed at this time.</span></span>
*  <span data-ttu-id="682e2-642">`MoveNext` Метод объекта перечислителя возвращает `true` вызвавшему объекту, указывающее, что он успешно перемещен к следующему элементу.</span><span class="sxs-lookup"><span data-stu-id="682e2-642">The `MoveNext` method of the enumerator object returns `true` to its caller, indicating that the enumerator object successfully advanced to the next item.</span></span>

<span data-ttu-id="682e2-643">Следующий вызов объекта-перечислителя `MoveNext` метод возобновляет выполнение блока итератора, из которой оно было приостановлено.</span><span class="sxs-lookup"><span data-stu-id="682e2-643">The next call to the enumerator object's `MoveNext` method resumes execution of the iterator block from where it was last suspended.</span></span>

<span data-ttu-id="682e2-644">Объект `yield break` инструкция выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="682e2-644">A `yield break` statement is executed as follows:</span></span>

*  <span data-ttu-id="682e2-645">Если `yield break` оператор входит в один или несколько `try` связанных блоков с `finally` блоки, элемент управления изначально передается `finally` блок самого внутреннего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-645">If the `yield break` statement is enclosed by one or more `try` blocks with associated `finally` blocks, control is initially transferred to the `finally` block of the innermost `try` statement.</span></span> <span data-ttu-id="682e2-646">Если элемент управления достигает конечной точки `finally` блок, элемент управления передается `finally` блок Далее включающего `try` инструкции.</span><span class="sxs-lookup"><span data-stu-id="682e2-646">When and if control reaches the end point of a `finally` block, control is transferred to the `finally` block of the next enclosing `try` statement.</span></span> <span data-ttu-id="682e2-647">Этот процесс повторяется, пока `finally` блоки, включающего все `try` инструкций.</span><span class="sxs-lookup"><span data-stu-id="682e2-647">This process is repeated until the `finally` blocks of all enclosing `try` statements have been executed.</span></span>
*  <span data-ttu-id="682e2-648">Управление возвращается вызывающему объекту блока итератора.</span><span class="sxs-lookup"><span data-stu-id="682e2-648">Control is returned to the caller of the iterator block.</span></span> <span data-ttu-id="682e2-649">Это может быть либо `MoveNext` метод или `Dispose` метод объекта перечислителя.</span><span class="sxs-lookup"><span data-stu-id="682e2-649">This is either the `MoveNext` method or `Dispose` method of the enumerator object.</span></span>

<span data-ttu-id="682e2-650">Так как `yield break` инструкции Безусловно передает управление в другом месте, конечная точка `yield break` инструкции никогда не доступен.</span><span class="sxs-lookup"><span data-stu-id="682e2-650">Because a `yield break` statement unconditionally transfers control elsewhere, the end point of a `yield break` statement is never reachable.</span></span>
