# <a name="expressions"></a><span data-ttu-id="04edb-101">Выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-101">Expressions</span></span>

<span data-ttu-id="04edb-102">Выражение — это последовательность операторов и операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-102">An expression is a sequence of operators and operands.</span></span> <span data-ttu-id="04edb-103">В этой главе описывается синтаксис, порядок вычисления операндов и операторов, а также смысл выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-103">This chapter defines the syntax, order of evaluation of operands and operators, and meaning of expressions.</span></span>

## <a name="expression-classifications"></a><span data-ttu-id="04edb-104">Классификации выражений</span><span class="sxs-lookup"><span data-stu-id="04edb-104">Expression classifications</span></span>

<span data-ttu-id="04edb-105">Выражение может иметь один из следующих типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-105">An expression is classified as one of the following:</span></span>

*  <span data-ttu-id="04edb-106">Значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-106">A value.</span></span> <span data-ttu-id="04edb-107">У каждого значения есть связанный с ним тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-107">Every value has an associated type.</span></span>
*  <span data-ttu-id="04edb-108">Переменная.</span><span class="sxs-lookup"><span data-stu-id="04edb-108">A variable.</span></span> <span data-ttu-id="04edb-109">Каждая переменная имеет связанный тип, а именно объявленный тип переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-109">Every variable has an associated type, namely the declared type of the variable.</span></span>
*  <span data-ttu-id="04edb-110">Пространство имен.</span><span class="sxs-lookup"><span data-stu-id="04edb-110">A namespace.</span></span> <span data-ttu-id="04edb-111">Выражение с этой классификацией может появляться только в левой части *member_access* ([доступ к членам](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-111">An expression with this classification can only appear as the left hand side of a *member_access* ([Member access](expressions.md#member-access)).</span></span> <span data-ttu-id="04edb-112">В любом другом контексте выражение классифицируется как пространство имен вызывает ошибку времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-112">In any other context, an expression classified as a namespace causes a compile-time error.</span></span>
*  <span data-ttu-id="04edb-113">Тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-113">A type.</span></span> <span data-ttu-id="04edb-114">Выражение с этой классификацией может появляться только в левой части *member_access* ([доступ к членам](expressions.md#member-access)), или в качестве операнда для `as` оператор ([оператор As ](expressions.md#the-as-operator)), `is` оператор ([является оператором](expressions.md#the-is-operator)), или `typeof` оператор ([оператор typeof](expressions.md#the-typeof-operator)).</span><span class="sxs-lookup"><span data-stu-id="04edb-114">An expression with this classification can only appear as the left hand side of a *member_access* ([Member access](expressions.md#member-access)), or as an operand for the `as` operator ([The as operator](expressions.md#the-as-operator)), the `is` operator ([The is operator](expressions.md#the-is-operator)), or the `typeof` operator ([The typeof operator](expressions.md#the-typeof-operator)).</span></span> <span data-ttu-id="04edb-115">В любом другом контексте выражение классифицируется как тип вызывает ошибку времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-115">In any other context, an expression classified as a type causes a compile-time error.</span></span>
*  <span data-ttu-id="04edb-116">Метод группу, которая представляет собой набор перегруженных методов, полученный в результате поиска члена ([поиск члена](expressions.md#member-lookup)).</span><span class="sxs-lookup"><span data-stu-id="04edb-116">A method group, which is a set of overloaded methods resulting from a member lookup ([Member lookup](expressions.md#member-lookup)).</span></span> <span data-ttu-id="04edb-117">Группа методов может иметь связанное выражение экземпляра и связанный список аргументов типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-117">A method group may have an associated instance expression and an associated type argument list.</span></span> <span data-ttu-id="04edb-118">При вызове метода экземпляра, результат вычисления выражения экземпляра становится экземпляра, представленного `this` ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-118">When an instance method is invoked, the result of evaluating the instance expression becomes the instance represented by `this` ([This access](expressions.md#this-access)).</span></span> <span data-ttu-id="04edb-119">Группа метод *invocation_expression* ([выражения вызова](expressions.md#invocation-expressions)), *delegate_creation_expression* ([делегировать создание выражения](expressions.md#delegate-creation-expressions)) и в качестве левой части операций является оператором и может быть неявно преобразован в совместимого типа делегата ([преобразования групп методов](conversions.md#method-group-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-119">A method group is permitted in an *invocation_expression* ([Invocation expressions](expressions.md#invocation-expressions)) , a *delegate_creation_expression* ([Delegate creation expressions](expressions.md#delegate-creation-expressions)) and as the left hand side of an is operator, and can be implicitly converted to a compatible delegate type ([Method group conversions](conversions.md#method-group-conversions)).</span></span> <span data-ttu-id="04edb-120">В любом другом контексте выражение классифицировано как группа метод вызывает ошибку времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-120">In any other context, an expression classified as a method group causes a compile-time error.</span></span>
*  <span data-ttu-id="04edb-121">Литерал null.</span><span class="sxs-lookup"><span data-stu-id="04edb-121">A null literal.</span></span> <span data-ttu-id="04edb-122">Выражение с этой классификацией может неявно преобразовываться в ссылочный тип или тип, допускающий значение NULL.</span><span class="sxs-lookup"><span data-stu-id="04edb-122">An expression with this classification can be implicitly converted to a reference type or nullable type.</span></span>
*  <span data-ttu-id="04edb-123">Анонимная функция.</span><span class="sxs-lookup"><span data-stu-id="04edb-123">An anonymous function.</span></span> <span data-ttu-id="04edb-124">Выражение с этой классификацией может неявно преобразовываться в совместимый тип делегата или тип дерева выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-124">An expression with this classification can be implicitly converted to a compatible delegate type or expression tree type.</span></span>
*  <span data-ttu-id="04edb-125">Доступ к свойству.</span><span class="sxs-lookup"><span data-stu-id="04edb-125">A property access.</span></span> <span data-ttu-id="04edb-126">Каждый доступ к свойству имеет связанный тип, а именно тип свойства.</span><span class="sxs-lookup"><span data-stu-id="04edb-126">Every property access has an associated type, namely the type of the property.</span></span> <span data-ttu-id="04edb-127">Кроме того доступ к свойству может быть связанным выражением экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-127">Furthermore, a property access may have an associated instance expression.</span></span> <span data-ttu-id="04edb-128">Если метод доступа ( `get` или `set` блок) экземпляра вызывается доступ к свойству, результат вычисления выражения экземпляра становится экземпляра, представленного `this` ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-128">When an accessor (the `get` or `set` block) of an instance property access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` ([This access](expressions.md#this-access)).</span></span>
*  <span data-ttu-id="04edb-129">Доступ к событию.</span><span class="sxs-lookup"><span data-stu-id="04edb-129">An event access.</span></span> <span data-ttu-id="04edb-130">Каждого доступа к событию имеет связанный тип, а именно тип события.</span><span class="sxs-lookup"><span data-stu-id="04edb-130">Every event access has an associated type, namely the type of the event.</span></span> <span data-ttu-id="04edb-131">Кроме того доступ к событию может быть связанным выражением экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-131">Furthermore, an event access may have an associated instance expression.</span></span> <span data-ttu-id="04edb-132">Доступ к событию может выглядеть как левый операнд `+=` и `-=` операторы ([назначения события](expressions.md#event-assignment)).</span><span class="sxs-lookup"><span data-stu-id="04edb-132">An event access may appear as the left hand operand of the `+=` and `-=` operators ([Event assignment](expressions.md#event-assignment)).</span></span> <span data-ttu-id="04edb-133">В любом другом контексте выражение доступа к событию вызывает ошибку времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-133">In any other context, an expression classified as an event access causes a compile-time error.</span></span>
*  <span data-ttu-id="04edb-134">Доступ к индексатору.</span><span class="sxs-lookup"><span data-stu-id="04edb-134">An indexer access.</span></span> <span data-ttu-id="04edb-135">Каждого доступа к индексатору имеет связанный тип, а именно тип элемента индексатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-135">Every indexer access has an associated type, namely the element type of the indexer.</span></span> <span data-ttu-id="04edb-136">Кроме того доступ к индексатору имеет связанное выражение экземпляра и связанный список аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-136">Furthermore, an indexer access has an associated instance expression and an associated argument list.</span></span> <span data-ttu-id="04edb-137">Если метод доступа ( `get` или `set` блок) индексатора вызывается доступ, результат вычисления выражения экземпляра становится экземпляра, представленного `this` ([такой доступ](expressions.md#this-access)) и результат вычисления списка аргументов становится списком параметров вызова.</span><span class="sxs-lookup"><span data-stu-id="04edb-137">When an accessor (the `get` or `set` block) of an indexer access is invoked, the result of evaluating the instance expression becomes the instance represented by `this` ([This access](expressions.md#this-access)), and the result of evaluating the argument list becomes the parameter list of the invocation.</span></span>
*  <span data-ttu-id="04edb-138">никаких действий.</span><span class="sxs-lookup"><span data-stu-id="04edb-138">Nothing.</span></span> <span data-ttu-id="04edb-139">Это происходит, если выражение является вызов метода с типом возвращаемого значения `void`.</span><span class="sxs-lookup"><span data-stu-id="04edb-139">This occurs when the expression is an invocation of a method with a return type of `void`.</span></span> <span data-ttu-id="04edb-140">Выражение классифицируется как допустимо только в контексте *statement_expression* ([операторы выражений](statements.md#expression-statements)).</span><span class="sxs-lookup"><span data-stu-id="04edb-140">An expression classified as nothing is only valid in the context of a *statement_expression* ([Expression statements](statements.md#expression-statements)).</span></span>

<span data-ttu-id="04edb-141">Результат выражения никогда не является пространство имен, тип, группу методов или доступа к событиям.</span><span class="sxs-lookup"><span data-stu-id="04edb-141">The final result of an expression is never a namespace, type, method group, or event access.</span></span> <span data-ttu-id="04edb-142">Скорее как указано выше, эти категории выражений представляют собой промежуточные конструкции, которые допускаются только в определенных контекстах.</span><span class="sxs-lookup"><span data-stu-id="04edb-142">Rather, as noted above, these categories of expressions are intermediate constructs that are only permitted in certain contexts.</span></span>

<span data-ttu-id="04edb-143">Доступ к свойству или индексатору всегда менять свой тип значение при вызове *метод доступа get* или *метода доступа set*.</span><span class="sxs-lookup"><span data-stu-id="04edb-143">A property access or indexer access is always reclassified as a value by performing an invocation of the *get accessor* or the *set accessor*.</span></span> <span data-ttu-id="04edb-144">Определенный метод доступа определяется в контексте доступа свойства или индексатора: Если доступ является целевым объектом назначения, *метода доступа set* вызывается для присвоения нового значения ([простое присваивание](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="04edb-144">The particular accessor is determined by the context of the property or indexer access: If the access is the target of an assignment, the *set accessor* is invoked to assign a new value ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="04edb-145">В противном случае *метод доступа get* вызывается для получения текущего значения ([значения выражений](expressions.md#values-of-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-145">Otherwise, the *get accessor* is invoked to obtain the current value ([Values of expressions](expressions.md#values-of-expressions)).</span></span>

### <a name="values-of-expressions"></a><span data-ttu-id="04edb-146">Значения выражений</span><span class="sxs-lookup"><span data-stu-id="04edb-146">Values of expressions</span></span>

<span data-ttu-id="04edb-147">Большинство конструкций, в которых участвует выражение, это требует, чтобы выражение обозначало ***значение***.</span><span class="sxs-lookup"><span data-stu-id="04edb-147">Most of the constructs that involve an expression ultimately require the expression to denote a ***value***.</span></span> <span data-ttu-id="04edb-148">В таких случаях если фактическое выражение обозначает пространство имен, типом, группой методов или nothing, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-148">In such cases, if the actual expression denotes a namespace, a type, a method group, or nothing, a compile-time error occurs.</span></span> <span data-ttu-id="04edb-149">Тем не менее если выражение обозначает доступ к свойству, индексатору или переменной, значение свойства, индексатора или переменной неявно заменяется:</span><span class="sxs-lookup"><span data-stu-id="04edb-149">However, if the expression denotes a property access, an indexer access, or a variable, the value of the property, indexer, or variable is implicitly substituted:</span></span>

*  <span data-ttu-id="04edb-150">Значение переменной является просто значение, хранящихся в расположении, указанном переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-150">The value of a variable is simply the value currently stored in the storage location identified by the variable.</span></span> <span data-ttu-id="04edb-151">Переменная должна быть считается определенно присвоенной ([определенного присваивания](variables.md#definite-assignment)) перед его значение можно получить, или в противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-151">A variable must be considered definitely assigned ([Definite assignment](variables.md#definite-assignment)) before its value can be obtained, or otherwise a compile-time error occurs.</span></span>
*  <span data-ttu-id="04edb-152">Значение выражения доступа к свойству получается путем вызова *метод доступа get* свойства.</span><span class="sxs-lookup"><span data-stu-id="04edb-152">The value of a property access expression is obtained by invoking the *get accessor* of the property.</span></span> <span data-ttu-id="04edb-153">Если свойство не имеет *метод доступа get*, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-153">If the property has no *get accessor*, a compile-time error occurs.</span></span> <span data-ttu-id="04edb-154">В противном случае вызов функции-члена ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) выполняется, и результат вызова становится значением выражения доступа к свойству.</span><span class="sxs-lookup"><span data-stu-id="04edb-154">Otherwise, a function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) is performed, and the result of the invocation becomes the value of the property access expression.</span></span>
*  <span data-ttu-id="04edb-155">Значение выражения доступа индексатора получается путем вызова *метод доступа get* индексатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-155">The value of an indexer access expression is obtained by invoking the *get accessor* of the indexer.</span></span> <span data-ttu-id="04edb-156">Если не имеет индексатора *метод доступа get*, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-156">If the indexer has no *get accessor*, a compile-time error occurs.</span></span> <span data-ttu-id="04edb-157">В противном случае вызов функции-члена ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) выполняется с аргументом списка, связанное с выражением доступа индексатора, а результат вызова становится значение выражения доступа индексатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-157">Otherwise, a function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) is performed with the argument list associated with the indexer access expression, and the result of the invocation becomes the value of the indexer access expression.</span></span>

## <a name="static-and-dynamic-binding"></a><span data-ttu-id="04edb-158">Статическая и динамическая привязка</span><span class="sxs-lookup"><span data-stu-id="04edb-158">Static and Dynamic Binding</span></span>

<span data-ttu-id="04edb-159">Процесс определения значения операцию на основании типа или значения составляющих выражений (аргументы, операнды, приемники) часто называется ***привязки***.</span><span class="sxs-lookup"><span data-stu-id="04edb-159">The process of determining the meaning of an operation based on the type or value of constituent expressions (arguments, operands, receivers) is often referred to as ***binding***.</span></span> <span data-ttu-id="04edb-160">Для экземпляра значение вызова метода определяется на основе приемника и аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-160">For instance the meaning of a method call is determined based on the type of the receiver and arguments.</span></span> <span data-ttu-id="04edb-161">Значение оператора определяется исходя из своих операндов типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-161">The meaning of an operator is determined based on the type of its operands.</span></span>

<span data-ttu-id="04edb-162">В C#, значение операции обычно определяется во время компиляции, исходя из его составляющих выражений типа во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-162">In C# the meaning of an operation is usually determined at compile-time, based on the compile-time type of its constituent expressions.</span></span> <span data-ttu-id="04edb-163">Аналогично Если выражение содержит ошибку, ошибка обнаружена и компилятор сообщает.</span><span class="sxs-lookup"><span data-stu-id="04edb-163">Likewise, if an expression contains an error, the error is detected and reported by the compiler.</span></span> <span data-ttu-id="04edb-164">Этот подход известен как ***статической привязки***.</span><span class="sxs-lookup"><span data-stu-id="04edb-164">This approach is known as ***static binding***.</span></span>

<span data-ttu-id="04edb-165">Тем не менее если выражение является динамическим выражением (т. е. имеет тип `dynamic`) это означает, что любой привязки, который участвует в должны быть основаны на типе времени выполнения (т. е. фактический тип объекта, он обозначает во время выполнения) вместо того, чтобы на тип При компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-165">However, if an expression is a dynamic expression (i.e. has the type `dynamic`) this indicates that any binding that it participates in should be based on its run-time type (i.e. the actual type of the object it denotes at run-time) rather than the type it has at compile-time.</span></span> <span data-ttu-id="04edb-166">Таким образом привязку такая операция откладывается до времени, которого операция, выполняемая во время выполнения программы.</span><span class="sxs-lookup"><span data-stu-id="04edb-166">The binding of such an operation is therefore deferred until the time where the operation is to be executed during the running of the program.</span></span> <span data-ttu-id="04edb-167">Это называется ***динамической привязки***.</span><span class="sxs-lookup"><span data-stu-id="04edb-167">This is referred to as ***dynamic binding***.</span></span>

<span data-ttu-id="04edb-168">Если операция является динамическим, практически не проверка выполняется компилятором.</span><span class="sxs-lookup"><span data-stu-id="04edb-168">When an operation is dynamically bound, little or no checking is performed by the compiler.</span></span> <span data-ttu-id="04edb-169">Вместо этого при сбое привязки времени выполнения, ошибки выводятся как исключения во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-169">Instead if the run-time binding fails, errors are reported as exceptions at run-time.</span></span>

<span data-ttu-id="04edb-170">Следующие операции в C# регулируются привязки:</span><span class="sxs-lookup"><span data-stu-id="04edb-170">The following operations in C# are subject to binding:</span></span>

*  <span data-ttu-id="04edb-171">Доступ к членам: `e.M`</span><span class="sxs-lookup"><span data-stu-id="04edb-171">Member access: `e.M`</span></span>
*  <span data-ttu-id="04edb-172">Вызов метода: `e.M(e1, ..., eN)`</span><span class="sxs-lookup"><span data-stu-id="04edb-172">Method invocation: `e.M(e1, ..., eN)`</span></span>
*  <span data-ttu-id="04edb-173">Вызов делегата:`e(e1, ..., eN)`</span><span class="sxs-lookup"><span data-stu-id="04edb-173">Delegate invocation:`e(e1, ..., eN)`</span></span>
*  <span data-ttu-id="04edb-174">Доступ к элементам: `e[e1, ..., eN]`</span><span class="sxs-lookup"><span data-stu-id="04edb-174">Element access: `e[e1, ..., eN]`</span></span>
*  <span data-ttu-id="04edb-175">Создание объекта: `new C(e1, ..., eN)`</span><span class="sxs-lookup"><span data-stu-id="04edb-175">Object creation: `new C(e1, ..., eN)`</span></span>
*  <span data-ttu-id="04edb-176">Перегрузка унарных операторов: `+`, `-`, `!`, `~`, `++`, `--`, `true`, `false`</span><span class="sxs-lookup"><span data-stu-id="04edb-176">Overloaded unary operators: `+`, `-`, `!`, `~`, `++`, `--`, `true`, `false`</span></span>
*  <span data-ttu-id="04edb-177">Перегруженные бинарные операторы: `+`, `-`, `*`, `/`, `%`, `&`, `&&`, `|`, `||`, `??`, `^`, `<<` , `>>`, `==`,`!=`, `>`, `<`, `>=`, `<=`</span><span class="sxs-lookup"><span data-stu-id="04edb-177">Overloaded binary operators: `+`, `-`, `*`, `/`, `%`, `&`, `&&`, `|`, `||`, `??`, `^`, `<<`, `>>`, `==`,`!=`, `>`, `<`, `>=`, `<=`</span></span>
*  <span data-ttu-id="04edb-178">Операторы присваивания: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`</span><span class="sxs-lookup"><span data-stu-id="04edb-178">Assignment operators: `=`, `+=`, `-=`, `*=`, `/=`, `%=`, `&=`, `|=`, `^=`, `<<=`, `>>=`</span></span>
*  <span data-ttu-id="04edb-179">Явные и неявные преобразования</span><span class="sxs-lookup"><span data-stu-id="04edb-179">Implicit and explicit conversions</span></span>

<span data-ttu-id="04edb-180">При использовании динамические выражения, C# по умолчанию статической привязки, это означает, что в процесс выбора используются типы составных выражений во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-180">When no dynamic expressions are involved, C# defaults to static binding, which means that the compile-time types of constituent expressions are used in the selection process.</span></span> <span data-ttu-id="04edb-181">Тем не менее если одна из составляющих выражений в приведенных выше операций динамического выражения, операция привязывается динамически.</span><span class="sxs-lookup"><span data-stu-id="04edb-181">However, when one of the constituent expressions in the operations listed above is a dynamic expression, the operation is instead dynamically bound.</span></span>

### <a name="binding-time"></a><span data-ttu-id="04edb-182">Во время привязки</span><span class="sxs-lookup"><span data-stu-id="04edb-182">Binding-time</span></span>

<span data-ttu-id="04edb-183">Статическая привязка выполняется во время компиляции, а динамическая привязка происходит во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-183">Static binding takes place at compile-time, whereas dynamic binding takes place at run-time.</span></span> <span data-ttu-id="04edb-184">В следующих разделах термин ***времени привязки*** ссылается на время компиляции или выполнения, в зависимости от того, когда выполняется привязка.</span><span class="sxs-lookup"><span data-stu-id="04edb-184">In the following sections, the term ***binding-time*** refers to either compile-time or run-time, depending on when the binding takes place.</span></span>

<span data-ttu-id="04edb-185">Следующий пример иллюстрирует уведомления статическая и динамическая привязка и во время привязки:</span><span class="sxs-lookup"><span data-stu-id="04edb-185">The following example illustrates the notions of static and dynamic binding and of binding-time:</span></span>
```csharp
object  o = 5;
dynamic d = 5;

Console.WriteLine(5);  // static  binding to Console.WriteLine(int)
Console.WriteLine(o);  // static  binding to Console.WriteLine(object)
Console.WriteLine(d);  // dynamic binding to Console.WriteLine(int)
```

<span data-ttu-id="04edb-186">Первые два вызова являются статическими: перегрузка `Console.WriteLine` выбирается на основе типа времени компиляции аргумента.</span><span class="sxs-lookup"><span data-stu-id="04edb-186">The first two calls are statically bound: the overload of `Console.WriteLine` is picked based on the compile-time type of their argument.</span></span> <span data-ttu-id="04edb-187">Таким образом время привязки во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-187">Thus, the binding-time is compile-time.</span></span>

<span data-ttu-id="04edb-188">Третий вызов является динамическим: перегрузка `Console.WriteLine` выбирается на основе типа среды выполнения своего аргумента.</span><span class="sxs-lookup"><span data-stu-id="04edb-188">The third call is dynamically bound: the overload of `Console.WriteLine` is picked based on the run-time type of its argument.</span></span> <span data-ttu-id="04edb-189">Это происходит потому, что аргумент является динамическим выражением--его тип времени компиляции — `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-189">This happens because the argument is a dynamic expression -- its compile-time type is `dynamic`.</span></span> <span data-ttu-id="04edb-190">Таким образом время привязки третьего вызова во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-190">Thus, the binding-time for the third call is run-time.</span></span>

### <a name="dynamic-binding"></a><span data-ttu-id="04edb-191">Динамическая привязка</span><span class="sxs-lookup"><span data-stu-id="04edb-191">Dynamic binding</span></span>

<span data-ttu-id="04edb-192">Динамическая привязка предназначена для разрешить программы на C# для взаимодействия с ***динамические объекты***, т. е. система типов объектов, которые не следовать нормальным правилам C#.</span><span class="sxs-lookup"><span data-stu-id="04edb-192">The purpose of dynamic binding is to allow C# programs to interact with ***dynamic objects***, i.e. objects that do not follow the normal rules of the C# type system.</span></span> <span data-ttu-id="04edb-193">Динамические объекты могут быть объекты из других языков программирования с системами различных типов, или они могут быть объекты, которые запрограммированы для реализации собственной семантики привязки для различных операций.</span><span class="sxs-lookup"><span data-stu-id="04edb-193">Dynamic objects may be objects from other programming languages with different types systems, or they may be objects that are programmatically setup to implement their own binding semantics for different operations.</span></span>

<span data-ttu-id="04edb-194">Механизм, по которому динамический объект реализует собственную семантику это определяется реализацией.</span><span class="sxs-lookup"><span data-stu-id="04edb-194">The mechanism by which a dynamic object implements its own semantics is implementation defined.</span></span> <span data-ttu-id="04edb-195">--Снова определяется реализацией--данный интерфейс реализуется динамическими объектами для указания для C# времени выполнения, что они имеют особой семантики.</span><span class="sxs-lookup"><span data-stu-id="04edb-195">A given interface -- again implementation defined -- is implemented by dynamic objects to signal to the C# run-time that they have special semantics.</span></span> <span data-ttu-id="04edb-196">Таким образом каждый раз, когда операции на динамический объект динамически связываются, собственную семантику привязки, а не те, C#, как указано в этом документе, перехватить.</span><span class="sxs-lookup"><span data-stu-id="04edb-196">Thus, whenever operations on a dynamic object are dynamically bound, their own binding semantics, rather than those of C# as specified in this document, take over.</span></span>

<span data-ttu-id="04edb-197">Хотя динамической привязки предназначена для того, чтобы разрешить взаимодействие с динамическими объектами, C# позволяет динамической привязки для всех объектов ли они являются динамическими, или нет.</span><span class="sxs-lookup"><span data-stu-id="04edb-197">While the purpose of dynamic binding is to allow interoperation with dynamic objects, C# allows dynamic binding on all objects, whether they are dynamic or not.</span></span> <span data-ttu-id="04edb-198">Это обеспечивает более тесную интеграцию динамические объекты, как результаты выполнения операций над их сами по себе не может быть динамических объектов, но по-прежнему имеют тип неизвестного программисту во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-198">This allows for a smoother integration of dynamic objects, as the results of operations on them may not themselves be dynamic objects, but are still of a type unknown to the programmer at compile-time.</span></span> <span data-ttu-id="04edb-199">Также динамической привязки может помочь устранить подверженного ошибкам кода на основе отражения, даже в том случае, если не участвующие объекты динамических объектов.</span><span class="sxs-lookup"><span data-stu-id="04edb-199">Also dynamic binding can help eliminate error-prone reflection-based code even when no objects involved are dynamic objects.</span></span>

<span data-ttu-id="04edb-200">В следующих разделах для каждой конструкции в языке точно при динамической привязки применяется, что компиляция проверки во время--если любой--применяется, и какие компиляции результат и выражение классификацией.</span><span class="sxs-lookup"><span data-stu-id="04edb-200">The following sections describe for each construct in the language exactly when dynamic binding is applied, what compile time checking -- if any -- is applied, and what the compile-time result and expression classification is.</span></span>

### <a name="types-of-constituent-expressions"></a><span data-ttu-id="04edb-201">Типы составных выражений</span><span class="sxs-lookup"><span data-stu-id="04edb-201">Types of constituent expressions</span></span>

<span data-ttu-id="04edb-202">Если операция статически привязку, тип составного выражения (например, получатель и аргумент, индекса или операнд) всегда считается типов во время компиляции этого выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-202">When an operation is statically bound, the type of a constituent expression (e.g. a receiver, and argument, an index or an operand) is always considered to be the compile-time type of that expression.</span></span>

<span data-ttu-id="04edb-203">Если операция является динамическим, тип составного выражения определяется по-разному в зависимости от типа во время компиляции составного выражения:</span><span class="sxs-lookup"><span data-stu-id="04edb-203">When an operation is dynamically bound, the type of a constituent expression is determined in different ways depending on the compile-time type of the constituent expression:</span></span>

*  <span data-ttu-id="04edb-204">Составное выражение типов во время компиляции `dynamic` должно иметь тип фактического значения, выражение принимает значение во время выполнения</span><span class="sxs-lookup"><span data-stu-id="04edb-204">A constituent expression of compile-time type `dynamic` is considered to have the type of the actual value that the expression evaluates to at runtime</span></span>
*  <span data-ttu-id="04edb-205">Считается, что составное выражение, тип которого во время компиляции является параметром типа является тип, который параметр типа привязан к во время выполнения</span><span class="sxs-lookup"><span data-stu-id="04edb-205">A constituent expression whose compile-time type is a type parameter is considered to have the type which the type parameter is bound to at runtime</span></span>
*  <span data-ttu-id="04edb-206">В противном случае составное выражение считается тип времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-206">Otherwise the constituent expression is considered to have its compile-time type.</span></span>

## <a name="operators"></a><span data-ttu-id="04edb-207">Операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-207">Operators</span></span>

<span data-ttu-id="04edb-208">Выражения, построенные на основе ***операндов*** и ***операторы***.</span><span class="sxs-lookup"><span data-stu-id="04edb-208">Expressions are constructed from ***operands*** and ***operators***.</span></span> <span data-ttu-id="04edb-209">Операторы в выражении указывают, какие действия нужно применить к операндам.</span><span class="sxs-lookup"><span data-stu-id="04edb-209">The operators of an expression indicate which operations to apply to the operands.</span></span> <span data-ttu-id="04edb-210">Примеры операторов: `+`, `-`, `*`, `/` и `new`.</span><span class="sxs-lookup"><span data-stu-id="04edb-210">Examples of operators include `+`, `-`, `*`, `/`, and `new`.</span></span> <span data-ttu-id="04edb-211">Операндами могут являться литералы, поля, локальные переменные, выражения и т. п.</span><span class="sxs-lookup"><span data-stu-id="04edb-211">Examples of operands include literals, fields, local variables, and expressions.</span></span>

<span data-ttu-id="04edb-212">Существует три типа операторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-212">There are three kinds of operators:</span></span>

*  <span data-ttu-id="04edb-213">Унарные операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-213">Unary operators.</span></span> <span data-ttu-id="04edb-214">Унарные операторы принимают один операнд и используют префиксной (такие как `--x`) или почтовый индекс (такие как `x++`).</span><span class="sxs-lookup"><span data-stu-id="04edb-214">The unary operators take one operand and use either prefix notation (such as `--x`) or postfix notation (such as `x++`).</span></span>
*  <span data-ttu-id="04edb-215">Бинарные операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-215">Binary operators.</span></span> <span data-ttu-id="04edb-216">Бинарные операторы используются два операнда, и в виде инфикса (такие как `x + y`).</span><span class="sxs-lookup"><span data-stu-id="04edb-216">The binary operators take two operands and all use infix notation (such as `x + y`).</span></span>
*  <span data-ttu-id="04edb-217">троичный оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-217">Ternary operator.</span></span> <span data-ttu-id="04edb-218">Только один Тернарный оператор `?:`, существует; он принимает три операнда и используется инфиксная запись (`c ? x : y`).</span><span class="sxs-lookup"><span data-stu-id="04edb-218">Only one ternary operator, `?:`, exists; it takes three operands and uses infix notation (`c ? x : y`).</span></span>

<span data-ttu-id="04edb-219">Порядок вычисления операторов в выражении определяется ***приоритет*** и ***ассоциативность*** операторов ([приоритет и ассоциативность операторов](expressions.md#operator-precedence-and-associativity)) .</span><span class="sxs-lookup"><span data-stu-id="04edb-219">The order of evaluation of operators in an expression is determined by the ***precedence*** and ***associativity*** of the operators ([Operator precedence and associativity](expressions.md#operator-precedence-and-associativity)).</span></span>

<span data-ttu-id="04edb-220">Операнды в выражении вычисляются слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-220">Operands in an expression are evaluated from left to right.</span></span> <span data-ttu-id="04edb-221">Например, в `F(i) + G(i++) * H(i)`, метод `F` вызывается с помощью старое значение `i`, затем метод `G` вызывается с старое значение `i`и, наконец, метод `H` вызывается с новым значением `i`.</span><span class="sxs-lookup"><span data-stu-id="04edb-221">For example, in `F(i) + G(i++) * H(i)`, method `F` is called using the old value of `i`, then method `G` is called with the old value of `i`, and, finally, method `H` is called with the new value of `i`.</span></span> <span data-ttu-id="04edb-222">Это отдельно от и не связана с приоритетом операторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-222">This is separate from and unrelated to operator precedence.</span></span>

<span data-ttu-id="04edb-223">Некоторые операторы могут быть ***перегружены***.</span><span class="sxs-lookup"><span data-stu-id="04edb-223">Certain operators can be ***overloaded***.</span></span> <span data-ttu-id="04edb-224">Перегрузка операторов позволяет создать определяемый пользователем оператор реализацию для операций там, где один или оба операнда имеют определяемый пользователем тип класса или структуры ([перегрузка операторов](expressions.md#operator-overloading)).</span><span class="sxs-lookup"><span data-stu-id="04edb-224">Operator overloading permits user-defined operator implementations to be specified for operations where one or both of the operands are of a user-defined class or struct type ([Operator overloading](expressions.md#operator-overloading)).</span></span>

### <a name="operator-precedence-and-associativity"></a><span data-ttu-id="04edb-225">Приоритет и ассоциативность операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-225">Operator precedence and associativity</span></span>

<span data-ttu-id="04edb-226">Если выражение содержит несколько операторов, порядок вычисления этих операторов определяется их ***приоритетом***.</span><span class="sxs-lookup"><span data-stu-id="04edb-226">When an expression contains multiple operators, the ***precedence*** of the operators controls the order in which the individual operators are evaluated.</span></span> <span data-ttu-id="04edb-227">Например, выражение `x + y * z` вычисляется как `x + (y * z)` поскольку `*` оператор имеет более высокий приоритет, чем двоичные `+` оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-227">For example, the expression `x + y * z` is evaluated as `x + (y * z)` because the `*` operator has higher precedence than the binary `+` operator.</span></span> <span data-ttu-id="04edb-228">Приоритет оператора устанавливается для определения его связанные грамматики производства.</span><span class="sxs-lookup"><span data-stu-id="04edb-228">The precedence of an operator is established by the definition of its associated grammar production.</span></span> <span data-ttu-id="04edb-229">Например *additive_expression* состоит из последовательности *multiplicative_expression*s, разделенных точкой `+` или `-` операторы, тем самым предоставляя `+` и `-` операторы имеют более низкий приоритет, чем `*`, `/`, и `%` операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-229">For example, an *additive_expression* consists of a sequence of *multiplicative_expression*s separated by `+` or `-` operators, thus giving the `+` and `-` operators lower precedence than the `*`, `/`, and `%` operators.</span></span>

<span data-ttu-id="04edb-230">В следующей таблице перечислены все операторы в порядке от самого высокого до самого низкого:</span><span class="sxs-lookup"><span data-stu-id="04edb-230">The following table summarizes all operators in order of precedence from highest to lowest:</span></span>

| <span data-ttu-id="04edb-231">__Раздел__</span><span class="sxs-lookup"><span data-stu-id="04edb-231">__Section__</span></span>                                                                                   | <span data-ttu-id="04edb-232">__Категория__</span><span class="sxs-lookup"><span data-stu-id="04edb-232">__Category__</span></span>                | <span data-ttu-id="04edb-233">__Инструкции__</span><span class="sxs-lookup"><span data-stu-id="04edb-233">__Operators__</span></span> | 
|-----------------------------------------------------------------------------------------------|-----------------------------|---------------|
| [<span data-ttu-id="04edb-234">Первичные выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-234">Primary expressions</span></span>](expressions.md#primary-expressions)                                     | <span data-ttu-id="04edb-235">Первичный</span><span class="sxs-lookup"><span data-stu-id="04edb-235">Primary</span></span>                     | <span data-ttu-id="04edb-236">`x.y`  `f(x)`  `a[x]`  `x++`  `x--`  `new`  `typeof`  `default`  `checked`  `unchecked`  `delegate`</span><span class="sxs-lookup"><span data-stu-id="04edb-236">`x.y`  `f(x)`  `a[x]`  `x++`  `x--`  `new`  `typeof`  `default`  `checked`  `unchecked`  `delegate`</span></span> | 
| [<span data-ttu-id="04edb-237">Унарные операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-237">Unary operators</span></span>](expressions.md#unary-operators)                                             | <span data-ttu-id="04edb-238">Унарный</span><span class="sxs-lookup"><span data-stu-id="04edb-238">Unary</span></span>                       | <span data-ttu-id="04edb-239">`+`  `-`  `!`  `~`  `++x`  `--x`  `(T)x`</span><span class="sxs-lookup"><span data-stu-id="04edb-239">`+`  `-`  `!`  `~`  `++x`  `--x`  `(T)x`</span></span> | 
| [<span data-ttu-id="04edb-240">Арифметические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-240">Arithmetic operators</span></span>](expressions.md#arithmetic-operators)                                   | <span data-ttu-id="04edb-241">Мультипликативный</span><span class="sxs-lookup"><span data-stu-id="04edb-241">Multiplicative</span></span>              | <span data-ttu-id="04edb-242">`*`  `/`  `%`</span><span class="sxs-lookup"><span data-stu-id="04edb-242">`*`  `/`  `%`</span></span> | 
| [<span data-ttu-id="04edb-243">Арифметические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-243">Arithmetic operators</span></span>](expressions.md#arithmetic-operators)                                   | <span data-ttu-id="04edb-244">Аддитивный</span><span class="sxs-lookup"><span data-stu-id="04edb-244">Additive</span></span>                    | <span data-ttu-id="04edb-245">`+`  `-`</span><span class="sxs-lookup"><span data-stu-id="04edb-245">`+`  `-`</span></span>      | 
| [<span data-ttu-id="04edb-246">Операторы сдвига</span><span class="sxs-lookup"><span data-stu-id="04edb-246">Shift operators</span></span>](expressions.md#shift-operators)                                             | <span data-ttu-id="04edb-247">Сдвиг</span><span class="sxs-lookup"><span data-stu-id="04edb-247">Shift</span></span>                       | <span data-ttu-id="04edb-248">`<<`  `>>`</span><span class="sxs-lookup"><span data-stu-id="04edb-248">`<<`  `>>`</span></span>    | 
| [<span data-ttu-id="04edb-249">Реляционные операторы и операторы тестирования типа</span><span class="sxs-lookup"><span data-stu-id="04edb-249">Relational and type-testing operators</span></span>](expressions.md#relational-and-type-testing-operators) | <span data-ttu-id="04edb-250">Тестирования типа и относительные</span><span class="sxs-lookup"><span data-stu-id="04edb-250">Relational and type testing</span></span> | <span data-ttu-id="04edb-251">`<`  `>`  `<=`  `>=`  `is`  `as`</span><span class="sxs-lookup"><span data-stu-id="04edb-251">`<`  `>`  `<=`  `>=`  `is`  `as`</span></span> | 
| [<span data-ttu-id="04edb-252">Реляционные операторы и операторы тестирования типа</span><span class="sxs-lookup"><span data-stu-id="04edb-252">Relational and type-testing operators</span></span>](expressions.md#relational-and-type-testing-operators) | <span data-ttu-id="04edb-253">Равенство</span><span class="sxs-lookup"><span data-stu-id="04edb-253">Equality</span></span>                    | <span data-ttu-id="04edb-254">`==`  `!=`</span><span class="sxs-lookup"><span data-stu-id="04edb-254">`==`  `!=`</span></span>    | 
| [<span data-ttu-id="04edb-255">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-255">Logical operators</span></span>](expressions.md#logical-operators)                                         | <span data-ttu-id="04edb-256">Логическое И</span><span class="sxs-lookup"><span data-stu-id="04edb-256">Logical AND</span></span>                 | `&`           | 
| [<span data-ttu-id="04edb-257">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-257">Logical operators</span></span>](expressions.md#logical-operators)                                         | <span data-ttu-id="04edb-258">Логическое исключающее ИЛИ</span><span class="sxs-lookup"><span data-stu-id="04edb-258">Logical XOR</span></span>                 | `^`           | 
| [<span data-ttu-id="04edb-259">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-259">Logical operators</span></span>](expressions.md#logical-operators)                                         | <span data-ttu-id="04edb-260">Логическое ИЛИ</span><span class="sxs-lookup"><span data-stu-id="04edb-260">Logical OR</span></span>                  | <code>&#124;</code>           |
| [<span data-ttu-id="04edb-261">Условные логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-261">Conditional logical operators</span></span>](expressions.md#conditional-logical-operators)                 | <span data-ttu-id="04edb-262">Условное И</span><span class="sxs-lookup"><span data-stu-id="04edb-262">Conditional AND</span></span>             | `&&`          | 
| [<span data-ttu-id="04edb-263">Условные логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-263">Conditional logical operators</span></span>](expressions.md#conditional-logical-operators)                 | <span data-ttu-id="04edb-264">Условное ИЛИ</span><span class="sxs-lookup"><span data-stu-id="04edb-264">Conditional OR</span></span>              | <code>&#124;&#124;</code>          | 
| [<span data-ttu-id="04edb-265">Оператор объединения со значением NULL</span><span class="sxs-lookup"><span data-stu-id="04edb-265">The null coalescing operator</span></span>](expressions.md#the-null-coalescing-operator)                   | <span data-ttu-id="04edb-266">Объединение со значением NULL</span><span class="sxs-lookup"><span data-stu-id="04edb-266">Null coalescing</span></span>             | `??`          | 
| [<span data-ttu-id="04edb-267">Условный оператор</span><span class="sxs-lookup"><span data-stu-id="04edb-267">Conditional operator</span></span>](expressions.md#conditional-operator)                                   | <span data-ttu-id="04edb-268">Условие</span><span class="sxs-lookup"><span data-stu-id="04edb-268">Conditional</span></span>                 | `?:`          | 
| <span data-ttu-id="04edb-269">[Операторы присваивания](expressions.md#assignment-operators), [выражения анонимных функций](expressions.md#anonymous-function-expressions)</span><span class="sxs-lookup"><span data-stu-id="04edb-269">[Assignment operators](expressions.md#assignment-operators), [Anonymous function expressions](expressions.md#anonymous-function-expressions)</span></span>  | <span data-ttu-id="04edb-270">Присвоение и лямбда-выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-270">Assignment and lambda expression</span></span> | <span data-ttu-id="04edb-271">`=`  `*=`  `/=`  `%=`  `+=`  `-=`  `<<=`  `>>=`  `&=`  `^=`  <code>&#124;=</code>  `=>`</span><span class="sxs-lookup"><span data-stu-id="04edb-271">`=`  `*=`  `/=`  `%=`  `+=`  `-=`  `<<=`  `>>=`  `&=`  `^=`  <code>&#124;=</code>  `=>`</span></span> | 

<span data-ttu-id="04edb-272">Если операнд располагается между двумя операторами с одинаковым приоритетом, ассоциативностью операторов управляет порядком, в котором выполняются операции:</span><span class="sxs-lookup"><span data-stu-id="04edb-272">When an operand occurs between two operators with the same precedence, the associativity of the operators controls the order in which the operations are performed:</span></span>

*  <span data-ttu-id="04edb-273">Кроме операторы присваивания и оператор объединения со значением null, все бинарные операторы имеют ***левую ассоциативность***, это означает, что операции выполняются слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-273">Except for the assignment operators and the null coalescing operator, all binary operators are ***left-associative***, meaning that operations are performed from left to right.</span></span> <span data-ttu-id="04edb-274">Например, выражение `x + y + z` вычисляется как `(x + y) + z`.</span><span class="sxs-lookup"><span data-stu-id="04edb-274">For example, `x + y + z` is evaluated as `(x + y) + z`.</span></span>
*  <span data-ttu-id="04edb-275">Операторы присваивания, оператор объединения со значением null и условный оператор (`?:`) являются ***правоассоциативным***, это означает, что операции выполняются слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-275">The assignment operators, the null coalescing operator and the conditional operator (`?:`) are ***right-associative***, meaning that operations are performed from right to left.</span></span> <span data-ttu-id="04edb-276">Например, выражение `x = y = z` вычисляется как `x = (y = z)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-276">For example, `x = y = z` is evaluated as `x = (y = z)`.</span></span>

<span data-ttu-id="04edb-277">Приоритет и ассоциативность операторов можно изменять, используя скобки.</span><span class="sxs-lookup"><span data-stu-id="04edb-277">Precedence and associativity can be controlled using parentheses.</span></span> <span data-ttu-id="04edb-278">Например, в выражении `x + y * z` сначала `y` умножается на `z`, а результат прибавляется к `x`, а в выражении `(x + y) * z` сначала суммируются `x` и `y`, а результат умножается на `z`.</span><span class="sxs-lookup"><span data-stu-id="04edb-278">For example, `x + y * z` first multiplies `y` by `z` and then adds the result to `x`, but `(x + y) * z` first adds `x` and `y` and then multiplies the result by `z`.</span></span>

### <a name="operator-overloading"></a><span data-ttu-id="04edb-279">Перегрузка операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-279">Operator overloading</span></span>

<span data-ttu-id="04edb-280">Все унарные и бинарные операторы имеют предварительно определенные реализации, которые автоматически становятся доступными в любом выражении.</span><span class="sxs-lookup"><span data-stu-id="04edb-280">All unary and binary operators have predefined implementations that are automatically available in any expression.</span></span> <span data-ttu-id="04edb-281">В дополнение к стандартным реализациям определенные пользователем реализации могут быть введены, включив `operator` объявления в классы и структуры ([операторы](classes.md#operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-281">In addition to the predefined implementations, user-defined implementations can be introduced by including `operator` declarations in classes and structs ([Operators](classes.md#operators)).</span></span> <span data-ttu-id="04edb-282">Реализации определяемых пользователем операторов всегда имеют приоритет над реализации стандартных операторов: Только если не применимо определяемого пользователем оператора существует считаться реализации стандартных операторов, как описано в разделе [разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution) и [перегрузку бинарного оператора разрешение](expressions.md#binary-operator-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-282">User-defined operator implementations always take precedence over predefined operator implementations: Only when no applicable user-defined operator implementations exist will the predefined operator implementations be considered, as described in [Unary operator overload resolution](expressions.md#unary-operator-overload-resolution) and [Binary operator overload resolution](expressions.md#binary-operator-overload-resolution).</span></span>

<span data-ttu-id="04edb-283">***Перегружаемые унарные операторы*** являются:</span><span class="sxs-lookup"><span data-stu-id="04edb-283">The ***overloadable unary operators*** are:</span></span>
```csharp
+   -   !   ~   ++   --   true   false
```

<span data-ttu-id="04edb-284">Несмотря на то что `true` и `false` явным образом не используются в выражениях (и поэтому не включены в таблице приоритетов в [приоритет и ассоциативность операторов](expressions.md#operator-precedence-and-associativity)), они считаются операторами, поскольку они являются вызывается в нескольких контекстах выражения: логические выражения ([логических выражений](expressions.md#boolean-expressions)) и выражения, включающие условия ([условный оператор](expressions.md#conditional-operator)) и логического условия операторы ([условные логические операторы](expressions.md#conditional-logical-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-284">Although `true` and `false` are not used explicitly in expressions (and therefore are not included in the precedence table in [Operator precedence and associativity](expressions.md#operator-precedence-and-associativity)), they are considered operators because they are invoked in several expression contexts: boolean expressions ([Boolean expressions](expressions.md#boolean-expressions)) and expressions involving the conditional ([Conditional operator](expressions.md#conditional-operator)), and conditional logical operators ([Conditional logical operators](expressions.md#conditional-logical-operators)).</span></span>

<span data-ttu-id="04edb-285">***Перегружаемые бинарные операторы*** являются:</span><span class="sxs-lookup"><span data-stu-id="04edb-285">The ***overloadable binary operators*** are:</span></span>
```csharp
+   -   *   /   %   &   |   ^   <<   >>   ==   !=   >   <   >=   <=
```

<span data-ttu-id="04edb-286">Только перечисленные выше операторы могут быть перегружены.</span><span class="sxs-lookup"><span data-stu-id="04edb-286">Only the operators listed above can be overloaded.</span></span> <span data-ttu-id="04edb-287">В частности, это невозможно перегрузить доступ к членам, вызов метода или `=`, `&&`, `||`, `??`, `?:`, `=>`, `checked`, `unchecked`, `new`, `typeof`, `default`, `as`, и `is` операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-287">In particular, it is not possible to overload member access, method invocation, or the `=`, `&&`, `||`, `??`, `?:`, `=>`, `checked`, `unchecked`, `new`, `typeof`, `default`, `as`, and `is` operators.</span></span>

<span data-ttu-id="04edb-288">При перегрузке бинарного оператора соответствующий оператор присвоения (если таковой имеется) также неявно перегружается.</span><span class="sxs-lookup"><span data-stu-id="04edb-288">When a binary operator is overloaded, the corresponding assignment operator, if any, is also implicitly overloaded.</span></span> <span data-ttu-id="04edb-289">Например, при перегрузке оператора `*` также является перегрузкой оператора `*=`.</span><span class="sxs-lookup"><span data-stu-id="04edb-289">For example, an overload of operator `*` is also an overload of operator `*=`.</span></span> <span data-ttu-id="04edb-290">Это описано далее в [Составное присваивание](expressions.md#compound-assignment).</span><span class="sxs-lookup"><span data-stu-id="04edb-290">This is described further in [Compound assignment](expressions.md#compound-assignment).</span></span> <span data-ttu-id="04edb-291">Обратите внимание, что сам оператор присваивания (`=`) не могут быть перегружены.</span><span class="sxs-lookup"><span data-stu-id="04edb-291">Note that the assignment operator itself (`=`) cannot be overloaded.</span></span> <span data-ttu-id="04edb-292">Назначения всегда выполняет простое побитовое копирование значения в переменную.</span><span class="sxs-lookup"><span data-stu-id="04edb-292">An assignment always performs a simple bit-wise copy of a value into a variable.</span></span>

<span data-ttu-id="04edb-293">Операций приведения типов, таких как `(T)x`, являются перегруженными, предоставляя заданные пользователем преобразования ([заданные пользователем преобразования](conversions.md#user-defined-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-293">Cast operations, such as `(T)x`, are overloaded by providing user-defined conversions ([User-defined conversions](conversions.md#user-defined-conversions)).</span></span>

<span data-ttu-id="04edb-294">Доступ к элементу, такие как `a[x]`, не считается перегружаемый оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-294">Element access, such as `a[x]`, is not considered an overloadable operator.</span></span> <span data-ttu-id="04edb-295">Вместо этого пользовательские индексирования поддерживается с помощью индексаторов ([индексаторы](classes.md#indexers)).</span><span class="sxs-lookup"><span data-stu-id="04edb-295">Instead, user-defined indexing is supported through indexers ([Indexers](classes.md#indexers)).</span></span>

<span data-ttu-id="04edb-296">В выражениях операторы, указываются нотация оператора, а в объявлениях, операторы, указываются функциональная нотация.</span><span class="sxs-lookup"><span data-stu-id="04edb-296">In expressions, operators are referenced using operator notation, and in declarations, operators are referenced using functional notation.</span></span> <span data-ttu-id="04edb-297">В следующей таблице показана связь между оператором и записью для унарные и бинарные операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-297">The following table shows the relationship between operator and functional notations for unary and binary operators.</span></span> <span data-ttu-id="04edb-298">В первой записи *op* обозначает перегружаемый унарный оператор, префикс.</span><span class="sxs-lookup"><span data-stu-id="04edb-298">In the first entry, *op* denotes any overloadable unary prefix operator.</span></span> <span data-ttu-id="04edb-299">Во второй строке *op* обозначает унарное Постфиксное `++` и `--` операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-299">In the second entry, *op* denotes the unary postfix `++` and `--` operators.</span></span> <span data-ttu-id="04edb-300">В третьей записи *op* обозначает любой требуется перегружаемый бинарный оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-300">In the third entry, *op* denotes any overloadable binary operator.</span></span>


| <span data-ttu-id="04edb-301">__Нотация оператора__</span><span class="sxs-lookup"><span data-stu-id="04edb-301">__Operator notation__</span></span> | <span data-ttu-id="04edb-302">__Функциональная нотация__</span><span class="sxs-lookup"><span data-stu-id="04edb-302">__Functional notation__</span></span> |
|-----------------------|-------------------------|
| `op x`                | `operator op(x)`        | 
| `x op`                | `operator op(x)`        | 
| `x op y`              | `operator op(x,y)`      | 

<span data-ttu-id="04edb-303">Определяемый пользователем оператор объявления всегда требуется хотя бы один параметр типа класса или структуры, содержащий объявления оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-303">User-defined operator declarations always require at least one of the parameters to be of the class or struct type that contains the operator declaration.</span></span> <span data-ttu-id="04edb-304">Таким образом он не поддерживается для определяемого пользователем оператора иметь ту же сигнатуру, что встроенному оператору.</span><span class="sxs-lookup"><span data-stu-id="04edb-304">Thus, it is not possible for a user-defined operator to have the same signature as a predefined operator.</span></span>

<span data-ttu-id="04edb-305">Определяемый пользователем оператор объявления не может изменить синтаксис, приоритет и ассоциативность оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-305">User-defined operator declarations cannot modify the syntax, precedence, or associativity of an operator.</span></span> <span data-ttu-id="04edb-306">Например `/` оператор всегда является бинарным оператором, всегда имеет уровень приоритета, указанное в [приоритет и ассоциативность операторов](expressions.md#operator-precedence-and-associativity)и всегда левую ассоциативность.</span><span class="sxs-lookup"><span data-stu-id="04edb-306">For example, the `/` operator is always a binary operator, always has the precedence level specified in [Operator precedence and associativity](expressions.md#operator-precedence-and-associativity), and is always left-associative.</span></span>

<span data-ttu-id="04edb-307">Хотя для определяемого пользователем оператора для выполнения любых вычислений, что, реализаций, которые формируют результаты, отличные от тех, которые ожидаются интуитивно понятным образом не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="04edb-307">While it is possible for a user-defined operator to perform any computation it pleases, implementations that produce results other than those that are intuitively expected are strongly discouraged.</span></span> <span data-ttu-id="04edb-308">Например, реализация `operator ==` следует сравнить два операнда на предмет равенства и возвращает соответствующий `bool` результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-308">For example, an implementation of `operator ==` should compare the two operands for equality and return an appropriate `bool` result.</span></span>

<span data-ttu-id="04edb-309">Описания отдельных операторов в [основные выражения](expressions.md#primary-expressions) через [условные логические операторы](expressions.md#conditional-logical-operators) указать операторы и любые дополнительные правила, которые применяются стандартные реализации для каждого оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-309">The descriptions of individual operators in [Primary expressions](expressions.md#primary-expressions) through [Conditional logical operators](expressions.md#conditional-logical-operators) specify the predefined implementations of the operators and any additional rules that apply to each operator.</span></span> <span data-ttu-id="04edb-310">Описания использовать условий ***разрешение перегрузки унарного оператора***, ***разрешить перегрузку бинарного оператора***, и ***Числовое расширение***, определения элементов найти в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="04edb-310">The descriptions make use of the terms ***unary operator overload resolution***, ***binary operator overload resolution***, and ***numeric promotion***, definitions of which are found in the following sections.</span></span>

### <a name="unary-operator-overload-resolution"></a><span data-ttu-id="04edb-311">Разрешение перегрузки унарного оператора</span><span class="sxs-lookup"><span data-stu-id="04edb-311">Unary operator overload resolution</span></span>

<span data-ttu-id="04edb-312">Операции формы `op x` или `x op`, где `op` перегружаемый унарный оператор, и `x` является выражением типа `X`, обрабатывается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-312">An operation of the form `op x` or `x op`, where `op` is an overloadable unary operator, and `x` is an expression of type `X`, is processed as follows:</span></span>

*  <span data-ttu-id="04edb-313">Набор кандидатов определяемые пользователем операторы, предоставляемые `X` для операции `operator op(x)` определяется с использованием правил [кандидата определяемых пользователем операторов](expressions.md#candidate-user-defined-operators).</span><span class="sxs-lookup"><span data-stu-id="04edb-313">The set of candidate user-defined operators provided by `X` for the operation `operator op(x)` is determined using the rules of [Candidate user-defined operators](expressions.md#candidate-user-defined-operators).</span></span>
*  <span data-ttu-id="04edb-314">Если набор кандидатов определяемые пользователем операторы не пустой, это становится набор операторов-кандидатов для операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-314">If the set of candidate user-defined operators is not empty, then this becomes the set of candidate operators for the operation.</span></span> <span data-ttu-id="04edb-315">В противном случае заранее определенной унарной `operator op` становятся реализации, поднятые формы, включая набор операторов-кандидатов для операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-315">Otherwise, the predefined unary `operator op` implementations, including their lifted forms, become the set of candidate operators for the operation.</span></span> <span data-ttu-id="04edb-316">Стандартные реализации данного оператора указаны в описании оператора ([основные выражения](expressions.md#primary-expressions) и [унарные операторы](expressions.md#unary-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-316">The predefined implementations of a given operator are specified in the description of the operator ([Primary expressions](expressions.md#primary-expressions) and [Unary operators](expressions.md#unary-operators)).</span></span>
*  <span data-ttu-id="04edb-317">Правила разрешения перегрузки из [разрешение перегрузки](expressions.md#overload-resolution) применяются к набору операторов кандидатов, чтобы выбрать подходящий оператор списка аргументов `(x)`, и этот оператор становится результатом перегрузки процесс разрешения.</span><span class="sxs-lookup"><span data-stu-id="04edb-317">The overload resolution rules of [Overload resolution](expressions.md#overload-resolution) are applied to the set of candidate operators to select the best operator with respect to the argument list `(x)`, and this operator becomes the result of the overload resolution process.</span></span> <span data-ttu-id="04edb-318">Если разрешение перегрузки оканчивается неудачей выбрать один подходящий оператор, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-318">If overload resolution fails to select a single best operator, a binding-time error occurs.</span></span>

### <a name="binary-operator-overload-resolution"></a><span data-ttu-id="04edb-319">Разрешение перегрузки бинарного оператора</span><span class="sxs-lookup"><span data-stu-id="04edb-319">Binary operator overload resolution</span></span>

<span data-ttu-id="04edb-320">Операции формы `x op y`, где `op` является требуется перегружаемый бинарный оператор `x` является выражением типа `X`, и `y` является выражением типа `Y`, обрабатывается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-320">An operation of the form `x op y`, where `op` is an overloadable binary operator, `x` is an expression of type `X`, and `y` is an expression of type `Y`, is processed as follows:</span></span>

*  <span data-ttu-id="04edb-321">Набор кандидатов определяемые пользователем операторы, предоставляемые `X` и `Y` для операции `operator op(x,y)` определяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-321">The set of candidate user-defined operators provided by `X` and `Y` for the operation `operator op(x,y)` is determined.</span></span> <span data-ttu-id="04edb-322">Набор состоит из объединения операторов-кандидатов, предоставляемые `X` и потенциальных операторы, предоставляемые `Y`, каждый определенный, используя правила [кандидата определяемых пользователем операторов](expressions.md#candidate-user-defined-operators).</span><span class="sxs-lookup"><span data-stu-id="04edb-322">The set consists of the union of the candidate operators provided by `X` and the candidate operators provided by `Y`, each determined using the rules of [Candidate user-defined operators](expressions.md#candidate-user-defined-operators).</span></span> <span data-ttu-id="04edb-323">Если `X` и `Y` относятся к одному типу, или если `X` и `Y` являются производными от общего базового типа, а затем Общие операторы-кандидаты произведен только в объединенном наборе один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-323">If `X` and `Y` are the same type, or if `X` and `Y` are derived from a common base type, then shared candidate operators only occur in the combined set once.</span></span>
*  <span data-ttu-id="04edb-324">Если набор кандидатов определяемые пользователем операторы не пустой, это становится набор операторов-кандидатов для операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-324">If the set of candidate user-defined operators is not empty, then this becomes the set of candidate operators for the operation.</span></span> <span data-ttu-id="04edb-325">В противном случае двоичные стандартные `operator op` становятся реализации, поднятые формы, включая набор операторов-кандидатов для операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-325">Otherwise, the predefined binary `operator op` implementations, including their lifted forms,  become the set of candidate operators for the operation.</span></span> <span data-ttu-id="04edb-326">Стандартные реализации данного оператора указаны в описании оператора ([арифметические операторы](expressions.md#arithmetic-operators) через [условные логические операторы](expressions.md#conditional-logical-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-326">The predefined implementations of a given operator are specified in the description of the operator ([Arithmetic operators](expressions.md#arithmetic-operators) through [Conditional logical operators](expressions.md#conditional-logical-operators)).</span></span> <span data-ttu-id="04edb-327">Для стандартных операторов перечислений и делегатов Единственными операторами считается определяются перечисление или делегат типа, который является типом времени привязки одного из операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-327">For predefined enum and delegate operators, the only operators considered are those defined by an enum or delegate type that is the binding-time type of one of the operands.</span></span>
*  <span data-ttu-id="04edb-328">Правила разрешения перегрузки из [разрешение перегрузки](expressions.md#overload-resolution) применяются к набору операторов кандидатов, чтобы выбрать подходящий оператор списка аргументов `(x,y)`, и этот оператор становится результатом перегрузки процесс разрешения.</span><span class="sxs-lookup"><span data-stu-id="04edb-328">The overload resolution rules of [Overload resolution](expressions.md#overload-resolution) are applied to the set of candidate operators to select the best operator with respect to the argument list `(x,y)`, and this operator becomes the result of the overload resolution process.</span></span> <span data-ttu-id="04edb-329">Если разрешение перегрузки оканчивается неудачей выбрать один подходящий оператор, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-329">If overload resolution fails to select a single best operator, a binding-time error occurs.</span></span>

### <a name="candidate-user-defined-operators"></a><span data-ttu-id="04edb-330">Определяемые пользователем операторы кандидатов</span><span class="sxs-lookup"><span data-stu-id="04edb-330">Candidate user-defined operators</span></span>

<span data-ttu-id="04edb-331">Типом `T` , операция `operator op(A)`, где `op` перегружаемый оператор и `A` является список аргументов, набор кандидатов, определяемые пользователем операторы, предоставляемые `T` для `operator op(A)` определяется как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="04edb-331">Given a type `T` and an operation `operator op(A)`, where `op` is an overloadable operator and `A` is an argument list, the set of candidate user-defined operators provided by `T` for `operator op(A)` is determined as follows:</span></span>

*  <span data-ttu-id="04edb-332">Определить тип `T0`.</span><span class="sxs-lookup"><span data-stu-id="04edb-332">Determine the type `T0`.</span></span> <span data-ttu-id="04edb-333">Если `T` является тип nullable `T0` является его базовым типом, в противном случае `T0` равен `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-333">If `T` is a nullable type, `T0` is its underlying type, otherwise `T0` is equal to `T`.</span></span>
*  <span data-ttu-id="04edb-334">Для всех `operator op` объявления в `T0` и все удален виды таких операторов, если хотя бы один оператор ([применимого члена функции](expressions.md#applicable-function-member)) списка аргументов `A`, то набор операторы кандидатов состоит из таких применимых операторов в `T0`.</span><span class="sxs-lookup"><span data-stu-id="04edb-334">For all `operator op` declarations in `T0` and all lifted forms of such operators, if at least one operator is applicable ([Applicable function member](expressions.md#applicable-function-member)) with respect to the argument list `A`, then the set of candidate operators consists of all such applicable operators in `T0`.</span></span>
*  <span data-ttu-id="04edb-335">В противном случае, если `T0` является `object`, набор операторов-кандидатов пуст.</span><span class="sxs-lookup"><span data-stu-id="04edb-335">Otherwise, if `T0` is `object`, the set of candidate operators is empty.</span></span>
*  <span data-ttu-id="04edb-336">В противном случае набор операторов кандидатов, предоставляемые `T0` — это набор операторов-кандидатов, предоставляемые прямой базовый класс для `T0`, или эффективный базовый класс `T0` Если `T0` является параметром типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-336">Otherwise, the set of candidate operators provided by `T0` is the set of candidate operators provided by the direct base class of `T0`, or the effective base class of `T0` if `T0` is a type parameter.</span></span>

### <a name="numeric-promotions"></a><span data-ttu-id="04edb-337">Восходящие приведения числовых типов</span><span class="sxs-lookup"><span data-stu-id="04edb-337">Numeric promotions</span></span>

<span data-ttu-id="04edb-338">Числовое расширение состоит из автоматически выполняет определенные неявные преобразования предопределенные унарные и бинарные операторы числовых операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-338">Numeric promotion consists of automatically performing certain implicit conversions of the operands of the predefined unary and binary numeric operators.</span></span> <span data-ttu-id="04edb-339">Числовое расширение — это не отдельный механизм, а скорее эффект применения разрешения перегрузки для стандартных операторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-339">Numeric promotion is not a distinct mechanism, but rather an effect of applying overload resolution to the predefined operators.</span></span> <span data-ttu-id="04edb-340">Числовое расширение специально не влияет на вычисления определяемых пользователем операторов, несмотря на то, что определяемые пользователем операторы можно реализовать для получения похожих эффектов.</span><span class="sxs-lookup"><span data-stu-id="04edb-340">Numeric promotion specifically does not affect evaluation of user-defined operators, although user-defined operators can be implemented to exhibit similar effects.</span></span>

<span data-ttu-id="04edb-341">В качестве примера числовых повышения роли, рассмотрим стандартные реализации двоичного файла `*` оператор:</span><span class="sxs-lookup"><span data-stu-id="04edb-341">As an example of numeric promotion, consider the predefined implementations of the binary `*` operator:</span></span>

```csharp
int operator *(int x, int y);
uint operator *(uint x, uint y);
long operator *(long x, long y);
ulong operator *(ulong x, ulong y);
float operator *(float x, float y);
double operator *(double x, double y);
decimal operator *(decimal x, decimal y);
```

<span data-ttu-id="04edb-342">Когда правила разрешения перегрузки ([разрешение перегрузки](expressions.md#overload-resolution)) применяются к этому набору операторов, применяется для выбора первого из операторов, для которых существуют неявные преобразования из типы операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-342">When overload resolution rules ([Overload resolution](expressions.md#overload-resolution)) are applied to this set of operators, the effect is to select the first of the operators for which implicit conversions exist from the operand types.</span></span> <span data-ttu-id="04edb-343">Например, для операции `b * s`, где `b` — `byte` и `s` — `short`, разрешения перегрузки выбирается `operator *(int,int)` как оператор рекомендации.</span><span class="sxs-lookup"><span data-stu-id="04edb-343">For example, for the operation `b * s`, where `b` is a `byte` and `s` is a `short`, overload resolution selects `operator *(int,int)` as the best operator.</span></span> <span data-ttu-id="04edb-344">Таким образом, это действие соответствует `b` и `s` преобразуются в `int`, а тип результата — `int`.</span><span class="sxs-lookup"><span data-stu-id="04edb-344">Thus, the effect is that `b` and `s` are converted to `int`, and the type of the result is `int`.</span></span> <span data-ttu-id="04edb-345">Аналогичным образом, для операции `i * d`, где `i` — `int` и `d` — `double`, разрешения перегрузки выбирается `operator *(double,double)` как оператор рекомендации.</span><span class="sxs-lookup"><span data-stu-id="04edb-345">Likewise, for the operation `i * d`, where `i` is an `int` and `d` is a `double`, overload resolution selects `operator *(double,double)` as the best operator.</span></span>

#### <a name="unary-numeric-promotions"></a><span data-ttu-id="04edb-346">Числовое расширение унарных операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-346">Unary numeric promotions</span></span>

<span data-ttu-id="04edb-347">Унарный Числовое расширение выполняется для операндов предопределенного `+`, `-`, и `~` унарные операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-347">Unary numeric promotion occurs for the operands of the predefined `+`, `-`, and `~` unary operators.</span></span> <span data-ttu-id="04edb-348">Числовое расширение унарный состоит всего лишь преобразования операндов типа `sbyte`, `byte`, `short`, `ushort`, или `char` ввода `int`.</span><span class="sxs-lookup"><span data-stu-id="04edb-348">Unary numeric promotion simply consists of converting operands of type `sbyte`, `byte`, `short`, `ushort`, or `char` to type `int`.</span></span> <span data-ttu-id="04edb-349">Кроме того, для унарных `-` оператор, унарный Числовое расширение преобразует операнды типа `uint` ввода `long`.</span><span class="sxs-lookup"><span data-stu-id="04edb-349">Additionally, for the unary `-` operator, unary numeric promotion converts operands of type `uint` to type `long`.</span></span>

#### <a name="binary-numeric-promotions"></a><span data-ttu-id="04edb-350">Числовое расширение бинарных операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-350">Binary numeric promotions</span></span>

<span data-ttu-id="04edb-351">Числовое расширение выполняется для операндов предопределенного `+`, `-`, `*`, `/`, `%`, `&`, `|`, `^`, `==`, `!=`, `>`, `<`, `>=`, и `<=` бинарных операторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-351">Binary numeric promotion occurs for the operands of the predefined `+`, `-`, `*`, `/`, `%`, `&`, `|`, `^`, `==`, `!=`, `>`, `<`, `>=`, and `<=` binary operators.</span></span> <span data-ttu-id="04edb-352">Числовое расширение оба операнда преобразуются в общий тип, который в случае операторов, также становится тип результата операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-352">Binary numeric promotion implicitly converts both operands to a common type which, in case of the non-relational operators, also becomes the result type of the operation.</span></span> <span data-ttu-id="04edb-353">Числовое расширение состоит в применении следующие правила, в порядке, в котором они отображаются здесь:</span><span class="sxs-lookup"><span data-stu-id="04edb-353">Binary numeric promotion consists of applying the following rules, in the order they appear here:</span></span>

*  <span data-ttu-id="04edb-354">Если один из операндов имеет тип `decimal`, то другой операнд преобразуется в тип `decimal`, или возникает ошибка времени привязки, если другой операнд имеет тип `float` или `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-354">If either operand is of type `decimal`, the other operand is converted to type `decimal`, or a binding-time error occurs if the other operand is of type `float` or `double`.</span></span>
*  <span data-ttu-id="04edb-355">В противном случае, если один из операндов имеет тип `double`, то другой операнд преобразуется в тип `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-355">Otherwise, if either operand is of type `double`, the other operand is converted to type `double`.</span></span>
*  <span data-ttu-id="04edb-356">В противном случае, если один из операндов имеет тип `float`, то другой операнд преобразуется в тип `float`.</span><span class="sxs-lookup"><span data-stu-id="04edb-356">Otherwise, if either operand is of type `float`, the other operand is converted to type `float`.</span></span>
*  <span data-ttu-id="04edb-357">В противном случае, если один из операндов имеет тип `ulong`, то другой операнд преобразуется в тип `ulong`, или возникает ошибка времени привязки, если другой операнд имеет тип `sbyte`, `short`, `int`, или `long`.</span><span class="sxs-lookup"><span data-stu-id="04edb-357">Otherwise, if either operand is of type `ulong`, the other operand is converted to type `ulong`, or a binding-time error occurs if the other operand is of type `sbyte`, `short`, `int`, or `long`.</span></span>
*  <span data-ttu-id="04edb-358">В противном случае, если один из операндов имеет тип `long`, то другой операнд преобразуется в тип `long`.</span><span class="sxs-lookup"><span data-stu-id="04edb-358">Otherwise, if either operand is of type `long`, the other operand is converted to type `long`.</span></span>
*  <span data-ttu-id="04edb-359">В противном случае, если один из операндов имеет тип `uint` и другой операнд имеет тип `sbyte`, `short`, или `int`, оба операнда преобразуются в тип `long`.</span><span class="sxs-lookup"><span data-stu-id="04edb-359">Otherwise, if either operand is of type `uint` and the other operand is of type `sbyte`, `short`, or `int`, both operands are converted to type `long`.</span></span>
*  <span data-ttu-id="04edb-360">В противном случае, если один из операндов имеет тип `uint`, то другой операнд преобразуется в тип `uint`.</span><span class="sxs-lookup"><span data-stu-id="04edb-360">Otherwise, if either operand is of type `uint`, the other operand is converted to type `uint`.</span></span>
*  <span data-ttu-id="04edb-361">В противном случае оба операнда преобразуются в тип `int`.</span><span class="sxs-lookup"><span data-stu-id="04edb-361">Otherwise, both operands are converted to type `int`.</span></span>

<span data-ttu-id="04edb-362">Обратите внимание, что первое правило запрещает любые операции, сочетающие в себе `decimal` тип с `double` и `float` типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-362">Note that the first rule disallows any operations that mix the `decimal` type with the `double` and `float` types.</span></span> <span data-ttu-id="04edb-363">Это правило вытекает из тот факт, что отсутствуют неявные преобразования между `decimal` типа и `double` и `float` типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-363">The rule follows from the fact that there are no implicit conversions between the `decimal` type and the `double` and `float` types.</span></span>

<span data-ttu-id="04edb-364">Также Обратите внимание, что операнд типа `ulong` Если другой операнд относится целочисленным типом со знаком.</span><span class="sxs-lookup"><span data-stu-id="04edb-364">Also note that it is not possible for an operand to be of type `ulong` when the other operand is of a signed integral type.</span></span> <span data-ttu-id="04edb-365">Причина в том, что целочисленный тип не существует, может представлять весь спектр `ulong` и целочисленных типов со знаком.</span><span class="sxs-lookup"><span data-stu-id="04edb-365">The reason is that no integral type exists that can represent the full range of `ulong` as well as the signed integral types.</span></span>

<span data-ttu-id="04edb-366">В обоих указанных случаях можно использовать для явного преобразования один операнд с типом, который совместим с другой операнд выражения приведения.</span><span class="sxs-lookup"><span data-stu-id="04edb-366">In both of the above cases, a cast expression can be used to explicitly convert one operand to a type that is compatible with the other operand.</span></span>

<span data-ttu-id="04edb-367">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-367">In the example</span></span>
```csharp
decimal AddPercent(decimal x, double percent) {
    return x * (1.0 + percent / 100.0);
}
```
<span data-ttu-id="04edb-368">во время привязки возникает из-за `decimal` нельзя будет умножено на `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-368">a binding-time error occurs because a `decimal` cannot be multiplied by a `double`.</span></span> <span data-ttu-id="04edb-369">Эта ошибка устраняется путем явного преобразования второго операнда `decimal`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="04edb-369">The error is resolved by explicitly converting the second operand to `decimal`, as follows:</span></span>

```csharp
decimal AddPercent(decimal x, double percent) {
    return x * (decimal)(1.0 + percent / 100.0);
}
```

### <a name="lifted-operators"></a><span data-ttu-id="04edb-370">Поднятые операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-370">Lifted operators</span></span>

<span data-ttu-id="04edb-371">***Снято операторы*** разрешить стандартные и определяемые пользователем операторы, которые работают с типами не поддерживающий значение NULL, также можно использовать с обнуляемых типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-371">***Lifted operators*** permit predefined and user-defined operators that operate on non-nullable value types to also be used with nullable forms of those types.</span></span> <span data-ttu-id="04edb-372">Поднятые операторы формируются на основе предопределенных и определяемых пользователем операторов, которые соответствуют определенным требованиям, как описано в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="04edb-372">Lifted operators are constructed from predefined and user-defined operators that meet certain requirements, as described in the following:</span></span>

*   <span data-ttu-id="04edb-373">Для унарных операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-373">For the unary operators</span></span>

    ```csharp
    +  ++  -  --  !  ~
    ```

    <span data-ttu-id="04edb-374">поднятые форма оператора существует, если типы операнд и результат обоих типов не поддерживающий значение NULL.</span><span class="sxs-lookup"><span data-stu-id="04edb-374">a lifted form of an operator exists if the operand and result types are both non-nullable value types.</span></span> <span data-ttu-id="04edb-375">Поднятые формы строится путем добавления одного `?` модификатор типы операнд и результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-375">The lifted form is constructed by adding a single `?` modifier to the operand and result types.</span></span> <span data-ttu-id="04edb-376">Поднятые оператор создает значение null, если операнд имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="04edb-376">The lifted operator produces a null value if the operand is null.</span></span> <span data-ttu-id="04edb-377">В противном случае оператор ликвидированный распаковывает операнд, применяется базовый оператор и заключает результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-377">Otherwise, the lifted operator unwraps the operand, applies the underlying operator, and wraps the result.</span></span>

*   <span data-ttu-id="04edb-378">Для бинарных операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-378">For the binary operators</span></span>

    ```csharp
    +  -  *  /  %  &  |  ^  <<  >>
    ```

    <span data-ttu-id="04edb-379">поднятые форма оператора существует, если операнд и результат типы являются все типы значений, не допускающие значения NULL.</span><span class="sxs-lookup"><span data-stu-id="04edb-379">a lifted form of an operator exists if the operand and result types are all non-nullable value types.</span></span> <span data-ttu-id="04edb-380">Поднятые формы строится путем добавления одного `?` модификатор к каждому типу операнд и результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-380">The lifted form is constructed by adding a single `?` modifier to each operand and result type.</span></span> <span data-ttu-id="04edb-381">Поднятые оператор создает значение null, если один или оба операнда имеют значение null (исключением `&` и `|` операторы `bool?` типов, как описано в [логические операторы](expressions.md#boolean-logical-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-381">The lifted operator produces a null value if one or both operands are null (an exception being the `&` and `|` operators of the `bool?` type, as described in [Boolean logical operators](expressions.md#boolean-logical-operators)).</span></span> <span data-ttu-id="04edb-382">В противном случае оператор ликвидированный распаковывает операндов, применяется базовый оператор и заключает результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-382">Otherwise, the lifted operator unwraps the operands, applies the underlying operator, and wraps the result.</span></span>

*   <span data-ttu-id="04edb-383">Для операторов равенства</span><span class="sxs-lookup"><span data-stu-id="04edb-383">For the equality operators</span></span>

    ```csharp
    ==  !=
    ```

    <span data-ttu-id="04edb-384">поднятые форма оператора существует, если доступны типы операндов не поддерживающий значение NULL типов и если тип результата — `bool`.</span><span class="sxs-lookup"><span data-stu-id="04edb-384">a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is `bool`.</span></span> <span data-ttu-id="04edb-385">Поднятые формы строится путем добавления одного `?` модификатор для каждого типа операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-385">The lifted form is constructed by adding a single `?` modifier to each operand type.</span></span> <span data-ttu-id="04edb-386">Оператор ликвидированный считает, что два значения null равны и значение null не равны, если любое значение, отличное от null.</span><span class="sxs-lookup"><span data-stu-id="04edb-386">The lifted operator considers two null values equal, and a null value unequal to any non-null value.</span></span> <span data-ttu-id="04edb-387">Если оба операнда не равны null, оператор ликвидированный распаковывает операнды и применяется базовый оператор для создания `bool` результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-387">If both operands are non-null, the lifted operator unwraps the operands and applies the underlying operator to produce the `bool` result.</span></span>

*   <span data-ttu-id="04edb-388">Для операторов отношения</span><span class="sxs-lookup"><span data-stu-id="04edb-388">For the relational operators</span></span>

    ```csharp
    <  >  <=  >=
    ```

    <span data-ttu-id="04edb-389">поднятые форма оператора существует, если доступны типы операндов не поддерживающий значение NULL типов и если тип результата — `bool`.</span><span class="sxs-lookup"><span data-stu-id="04edb-389">a lifted form of an operator exists if the operand types are both non-nullable value types and if the result type is `bool`.</span></span> <span data-ttu-id="04edb-390">Поднятые формы строится путем добавления одного `?` модификатор для каждого типа операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-390">The lifted form is constructed by adding a single `?` modifier to each operand type.</span></span> <span data-ttu-id="04edb-391">Оператор ликвидированный создающее значение `false` Если один или оба операнда имеют значение null.</span><span class="sxs-lookup"><span data-stu-id="04edb-391">The lifted operator produces the value `false` if one or both operands are null.</span></span> <span data-ttu-id="04edb-392">В противном случае оператор ликвидированный распаковывает операнды и применяется базовый оператор для создания `bool` результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-392">Otherwise, the lifted operator unwraps the operands and applies the underlying operator to produce the `bool` result.</span></span>

## <a name="member-lookup"></a><span data-ttu-id="04edb-393">Поиск члена</span><span class="sxs-lookup"><span data-stu-id="04edb-393">Member lookup</span></span>

<span data-ttu-id="04edb-394">Поиск члена — это процесс, посредством которого определяется значение имени в контексте типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-394">A member lookup is the process whereby the meaning of a name in the context of a type is determined.</span></span> <span data-ttu-id="04edb-395">Поиск членов может выполняться как часть оценки *simple_name* ([простые имена](expressions.md#simple-names)) или *member_access* ([доступ к членам](expressions.md#member-access)) в выражение.</span><span class="sxs-lookup"><span data-stu-id="04edb-395">A member lookup can occur as part of evaluating a *simple_name* ([Simple names](expressions.md#simple-names)) or a *member_access* ([Member access](expressions.md#member-access)) in an expression.</span></span> <span data-ttu-id="04edb-396">Если *simple_name* или *member_access* возникает как *primary_expression* из *invocation_expression* ([ Вызовы методов](expressions.md#method-invocations)), говорят, что член должен быть вызван.</span><span class="sxs-lookup"><span data-stu-id="04edb-396">If the *simple_name* or *member_access* occurs as the *primary_expression* of an *invocation_expression* ([Method invocations](expressions.md#method-invocations)), the member is said to be invoked.</span></span>

<span data-ttu-id="04edb-397">Если элемент является метод или событие, или в том случае, если это константа, поле или свойство типа делегата ([делегаты](delegates.md)) или тип `dynamic` ([динамический тип](types.md#the-dynamic-type)), то считается, что член является *invocable*.</span><span class="sxs-lookup"><span data-stu-id="04edb-397">If a member is a method or event, or if it is a constant, field or property of either a delegate type ([Delegates](delegates.md)) or the type `dynamic` ([The dynamic type](types.md#the-dynamic-type)), then the member is said to be *invocable*.</span></span>

<span data-ttu-id="04edb-398">Поиск члена считает, что не только имя члена, но число параметров типа, элемента и доступен ли элемент.</span><span class="sxs-lookup"><span data-stu-id="04edb-398">Member lookup considers not only the name of a member but also the number of type parameters the member has and whether the member is accessible.</span></span> <span data-ttu-id="04edb-399">В целях поиска членов универсальные методы и вложенные универсальные типы имеют число параметров типа, указанного в соответствующих объявлениях, и у всех остальных членов параметров типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-399">For the purposes of member lookup, generic methods and nested generic types have the number of type parameters indicated in their respective declarations and all other members have zero type parameters.</span></span>

<span data-ttu-id="04edb-400">Поиск члена с именем `N` с `K`  параметры типа в типе `T` обрабатывается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-400">A member lookup of a name `N` with `K` type parameters in a type `T` is processed as follows:</span></span>

*  <span data-ttu-id="04edb-401">Во-первых, набор доступных членов с именем `N` определяется:</span><span class="sxs-lookup"><span data-stu-id="04edb-401">First, a set of accessible members named `N` is determined:</span></span>
    * <span data-ttu-id="04edb-402">Если `T` является параметром типа, а затем набор представляет собой объединение наборов доступных членов с именем `N` в каждом из типов, заданный как ограничение первичного или вторичного ограничения ([ограничения параметров типа](classes.md#type-parameter-constraints)) для  `T`, а также набор доступных членов с именем `N` в `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-402">If `T` is a type parameter, then the set is the union of the sets of accessible members named `N` in each of the types specified as a primary constraint or secondary constraint ([Type parameter constraints](classes.md#type-parameter-constraints)) for `T`, along with the set of accessible members named `N` in `object`.</span></span>
    * <span data-ttu-id="04edb-403">В противном случае набор включает все эти возможности доступны ([доступ к членам](basic-concepts.md#member-access)) члены с именем `N` в `T`, включая унаследованные члены и доступные члены с именем `N` в `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-403">Otherwise, the set consists of all accessible ([Member access](basic-concepts.md#member-access)) members named `N` in `T`, including inherited members and the accessible members named `N` in `object`.</span></span> <span data-ttu-id="04edb-404">Если `T` — сконструированный тип, набор элементов получается путем замены аргументов типа, как описано в разделе [члены сконструированных типов](classes.md#members-of-constructed-types).</span><span class="sxs-lookup"><span data-stu-id="04edb-404">If `T` is a constructed type, the set of members is obtained by substituting type arguments as described in [Members of constructed types](classes.md#members-of-constructed-types).</span></span> <span data-ttu-id="04edb-405">Члены, включающие `override` модификатор исключаются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-405">Members that include an `override` modifier are excluded from the set.</span></span>
*  <span data-ttu-id="04edb-406">Далее, если `K` равно нулю, все вложенные типы, чьи объявления содержат параметры типа удаляются.</span><span class="sxs-lookup"><span data-stu-id="04edb-406">Next, if `K` is zero, all nested types whose declarations include type parameters are removed.</span></span> <span data-ttu-id="04edb-407">Если `K` не равно 0, все члены с различным числом удалены параметры типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-407">If `K` is not zero, all members with a different number of type parameters are removed.</span></span> <span data-ttu-id="04edb-408">Обратите внимание, что при `K` равно нулю, методы не тип параметров, не удаляются, так как процесс определения типа ([вывод типа](expressions.md#type-inference)) можно попытаться определить аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-408">Note that when `K` is zero, methods having type parameters are not removed, since the type inference process ([Type inference](expressions.md#type-inference)) might be able to infer the type arguments.</span></span>
*  <span data-ttu-id="04edb-409">Затем, если член является *вызывается*, все-*invocable* элементы удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-409">Next, if the member is *invoked*, all non-*invocable* members are removed from the set.</span></span>
*  <span data-ttu-id="04edb-410">Затем члены, которые скрыты другими членами удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-410">Next, members that are hidden by other members are removed from the set.</span></span> <span data-ttu-id="04edb-411">Для каждого члена `S.M` в наборе, где `S` — это тип, в которой элемент `M` был объявлен, применяются следующие правила:</span><span class="sxs-lookup"><span data-stu-id="04edb-411">For every member `S.M` in the set, where `S` is the type in which the member `M` is declared, the following rules are applied:</span></span>
    * <span data-ttu-id="04edb-412">Если `M` является константой, поля, свойства, события или член перечисления, то все члены, объявленные в базовом типе `S` удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-412">If `M` is a constant, field, property, event, or enumeration member, then all members declared in a base type of `S` are removed from the set.</span></span>
    * <span data-ttu-id="04edb-413">Если `M` объявление типа, то все не типы, объявленные в базовом типе `S` удаляются из набора, и все объявления, с числом параметров типа в качестве типов `M` объявленный в базовом типе `S` удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-413">If `M` is a type declaration, then all non-types declared in a base type of `S` are removed from the set, and all type declarations with the same number of type parameters as `M` declared in a base type of `S` are removed from the set.</span></span>
    * <span data-ttu-id="04edb-414">Если `M` является методом, а затем все не являющийся методом члены, объявленные в базовом типе `S` удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-414">If `M` is a method, then all non-method members declared in a base type of `S` are removed from the set.</span></span>
*  <span data-ttu-id="04edb-415">После этого члены интерфейса, скрытые члены класса, удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-415">Next, interface members that are hidden by class members are removed from the set.</span></span> <span data-ttu-id="04edb-416">Этот шаг действует только если `T` является параметром типа и `T` имеет оба действительного базового класса, отличное от `object` и эффективный интерфейс непустое значение ([ограничения параметров типа](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="04edb-416">This step only has an effect if `T` is a type parameter and `T` has both an effective base class other than `object` and a non-empty effective interface set ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="04edb-417">Для каждого члена `S.M` в наборе, где `S` — это тип, в которой элемент `M` был объявлен, следующие правила применяются в том случае, если `S` является объявлением класса, отличного от `object`:</span><span class="sxs-lookup"><span data-stu-id="04edb-417">For every member `S.M` in the set, where `S` is the type in which the member `M` is declared, the following rules are applied if `S` is a class declaration other than `object`:</span></span>
    * <span data-ttu-id="04edb-418">Если `M` является константой, поля, свойства, события, члена перечисления или объявление типа, то все члены, объявленные в объявлении интерфейса удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-418">If `M` is a constant, field, property, event, enumeration member, or type declaration, then all members declared in an interface declaration are removed from the set.</span></span>
    * <span data-ttu-id="04edb-419">Если `M` является методом, а затем из набора, а также все методы, имеющие ту же сигнатуру, что удаляются все не являющийся методом члены, объявленные в объявлении интерфейса `M` объявлен в интерфейсе объявления удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-419">If `M` is a method, then all non-method members declared in an interface declaration are removed from the set, and all methods with the same signature as `M` declared in an interface declaration are removed from the set.</span></span>
*  <span data-ttu-id="04edb-420">Наконец после удаления скрытых членов, определяется результат уточняющего запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-420">Finally, having removed hidden members, the result of the lookup is determined:</span></span>
    * <span data-ttu-id="04edb-421">Если набор состоит из одного члена, который не является методом, этот член является результатом поиска.</span><span class="sxs-lookup"><span data-stu-id="04edb-421">If the set consists of a single member that is not a method, then this member is the result of the lookup.</span></span>
    * <span data-ttu-id="04edb-422">В противном случае если набор содержит только методы, эта группа методов является результатом поиска.</span><span class="sxs-lookup"><span data-stu-id="04edb-422">Otherwise, if the set contains only methods, then this group of methods is the result of the lookup.</span></span>
    * <span data-ttu-id="04edb-423">В противном случае уточняющего запроса является неоднозначным, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-423">Otherwise, the lookup is ambiguous, and a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-424">Для поиска элемента в типы, отличные от параметров типов и интерфейсов и член уточняющих запросов в интерфейсы, которые являются строго одиночным наследованием (каждый интерфейс в цепочке наследования имеет точно ноль или один прямой базовый интерфейс), в результате правила просто, производным скрыть члены базовых членов с тем же именем или сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="04edb-424">For member lookups in types other than type parameters and interfaces, and member lookups in interfaces that are strictly single-inheritance (each interface in the inheritance chain has exactly zero or one direct base interface), the effect of the lookup rules is simply that derived members hide base members with the same name or signature.</span></span> <span data-ttu-id="04edb-425">Такой поиск одиночного наследования никогда не являются неоднозначными.</span><span class="sxs-lookup"><span data-stu-id="04edb-425">Such single-inheritance lookups are never ambiguous.</span></span> <span data-ttu-id="04edb-426">Неоднозначности, которые могут возникать из члена уточняющих запросов в интерфейсы множественного наследования, описаны в [доступ к членам интерфейса](interfaces.md#interface-member-access).</span><span class="sxs-lookup"><span data-stu-id="04edb-426">The ambiguities that can possibly arise from member lookups in multiple-inheritance interfaces are described in [Interface member access](interfaces.md#interface-member-access).</span></span>

### <a name="base-types"></a><span data-ttu-id="04edb-427">Базовые типы</span><span class="sxs-lookup"><span data-stu-id="04edb-427">Base types</span></span>

<span data-ttu-id="04edb-428">Для поиска членов, тип `T` видимости, имеет следующие базовые типы:</span><span class="sxs-lookup"><span data-stu-id="04edb-428">For purposes of member lookup, a type `T` is considered to have the following base types:</span></span>

*  <span data-ttu-id="04edb-429">Если `T` — `object`, затем `T` не имеет базового типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-429">If `T` is `object`, then `T` has no base type.</span></span>
*  <span data-ttu-id="04edb-430">Если `T` — *enum_type*, базовые типы `T` относятся к типам классов `System.Enum`, `System.ValueType`, и `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-430">If `T` is an *enum_type*, the base types of `T` are the class types `System.Enum`, `System.ValueType`, and `object`.</span></span>
*  <span data-ttu-id="04edb-431">Если `T` — *struct_type*, базовые типы `T` относятся к типам классов `System.ValueType` и `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-431">If `T` is a *struct_type*, the base types of `T` are the class types `System.ValueType` and `object`.</span></span>
*  <span data-ttu-id="04edb-432">Если `T` — *class_type*, базовые типы `T` являются базовыми классами из `T`, включая тип класса `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-432">If `T` is a *class_type*, the base types of `T` are the base classes of `T`, including the class type `object`.</span></span>
*  <span data-ttu-id="04edb-433">Если `T` — *interface_type*, базовые типы `T` являются базовые интерфейсы `T` и тип класса `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-433">If `T` is an *interface_type*, the base types of `T` are the base interfaces of `T` and the class type `object`.</span></span>
*  <span data-ttu-id="04edb-434">Если `T` — *array_type*, базовые типы `T` относятся к типам классов `System.Array` и `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-434">If `T` is an *array_type*, the base types of `T` are the class types `System.Array` and `object`.</span></span>
*  <span data-ttu-id="04edb-435">Если `T` — *delegate_type*, базовые типы `T` относятся к типам классов `System.Delegate` и `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-435">If `T` is a *delegate_type*, the base types of `T` are the class types `System.Delegate` and `object`.</span></span>

## <a name="function-members"></a><span data-ttu-id="04edb-436">Функции-члены</span><span class="sxs-lookup"><span data-stu-id="04edb-436">Function members</span></span>

<span data-ttu-id="04edb-437">Функции-члены — члены, содержащие исполняемые операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-437">Function members are members that contain executable statements.</span></span> <span data-ttu-id="04edb-438">Функции-члены всегда являются членами типов и не может быть членами пространства имен.</span><span class="sxs-lookup"><span data-stu-id="04edb-438">Function members are always members of types and cannot be members of namespaces.</span></span> <span data-ttu-id="04edb-439">C# определяет следующие категории функций-членов:</span><span class="sxs-lookup"><span data-stu-id="04edb-439">C# defines the following categories of function members:</span></span>

*  <span data-ttu-id="04edb-440">Методы</span><span class="sxs-lookup"><span data-stu-id="04edb-440">Methods</span></span>
*  <span data-ttu-id="04edb-441">Свойства</span><span class="sxs-lookup"><span data-stu-id="04edb-441">Properties</span></span>
*  <span data-ttu-id="04edb-442">События</span><span class="sxs-lookup"><span data-stu-id="04edb-442">Events</span></span>
*  <span data-ttu-id="04edb-443">Индексаторы</span><span class="sxs-lookup"><span data-stu-id="04edb-443">Indexers</span></span>
*  <span data-ttu-id="04edb-444">Определяемые пользователем операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-444">User-defined operators</span></span>
*  <span data-ttu-id="04edb-445">Конструкторы экземпляров</span><span class="sxs-lookup"><span data-stu-id="04edb-445">Instance constructors</span></span>
*  <span data-ttu-id="04edb-446">Статические конструкторы</span><span class="sxs-lookup"><span data-stu-id="04edb-446">Static constructors</span></span>
*  <span data-ttu-id="04edb-447">Деструкторы</span><span class="sxs-lookup"><span data-stu-id="04edb-447">Destructors</span></span>

<span data-ttu-id="04edb-448">За исключением деструкторы и статические конструкторы (которые могут быть вызваны явно) инструкций, содержащихся в функции-члены, выполняются через вызовов функций-членов.</span><span class="sxs-lookup"><span data-stu-id="04edb-448">Except for destructors and static constructors (which cannot be invoked explicitly), the statements contained in function members are executed through function member invocations.</span></span> <span data-ttu-id="04edb-449">Фактический синтаксис вызова функции-члена зависит от категории конкретной функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-449">The actual syntax for writing a function member invocation depends on the particular function member category.</span></span>

<span data-ttu-id="04edb-450">Список аргументов ([списки аргументов](expressions.md#argument-lists)) функции-члена вызова предоставляет фактические значения или ссылки на переменные для параметров функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-450">The argument list ([Argument lists](expressions.md#argument-lists)) of a function member invocation provides actual values or variable references for the parameters of the function member.</span></span>

<span data-ttu-id="04edb-451">Вызовы универсальных методов, могут использовать определение типа для определения набора аргументов типа для передачи в метод.</span><span class="sxs-lookup"><span data-stu-id="04edb-451">Invocations of generic methods may employ type inference to determine the set of type arguments to pass to the method.</span></span> <span data-ttu-id="04edb-452">Этот процесс описан в [вывод типа](expressions.md#type-inference).</span><span class="sxs-lookup"><span data-stu-id="04edb-452">This process is described in [Type inference](expressions.md#type-inference).</span></span>

<span data-ttu-id="04edb-453">Вызовы методов, индексаторов, операторов и конструкторов экземпляров использовать разрешение перегрузки, чтобы определить, какой набор кандидатов для вызова функций-членов.</span><span class="sxs-lookup"><span data-stu-id="04edb-453">Invocations of methods, indexers, operators and instance constructors employ overload resolution to determine which of a candidate set of function members to invoke.</span></span> <span data-ttu-id="04edb-454">Этот процесс описан в [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-454">This process is described in [Overload resolution](expressions.md#overload-resolution).</span></span>

<span data-ttu-id="04edb-455">После определения конкретной функции-члена во время привязки, возможно через разрешения перегрузки, фактический процесс выполнения вызова функции-члена описан в [Проверка динамического разрешения перегрузкивовремякомпиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-455">Once a particular function member has been identified at binding-time, possibly through overload resolution, the actual run-time process of invoking the function member is described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="04edb-456">В следующей таблице перечислены обработку, которая выполняется в конструкции, включающих шесть категорий функций-членов, которые можно вызвать явным образом.</span><span class="sxs-lookup"><span data-stu-id="04edb-456">The following table summarizes the processing that takes place in constructs involving the six categories of function members that can be explicitly invoked.</span></span> <span data-ttu-id="04edb-457">В таблице `e`, `x`, `y`, и `value` указания выражений, которые классифицируются как переменные или значения, `T` означает выражение как тип, `F` — простое имя метода и `P` — это простое имя свойства.</span><span class="sxs-lookup"><span data-stu-id="04edb-457">In the table, `e`, `x`, `y`, and `value` indicate expressions classified as variables or values, `T` indicates an expression classified as a type, `F` is the simple name of a method, and `P` is the simple name of a property.</span></span>


| <span data-ttu-id="04edb-458">__Конструкция__</span><span class="sxs-lookup"><span data-stu-id="04edb-458">__Construct__</span></span>     | <span data-ttu-id="04edb-459">__Пример__</span><span class="sxs-lookup"><span data-stu-id="04edb-459">__Example__</span></span>    | <span data-ttu-id="04edb-460">__Описание__</span><span class="sxs-lookup"><span data-stu-id="04edb-460">__Description__</span></span> |
|-------------------|----------------|-----------------|
| <span data-ttu-id="04edb-461">Вызов метода</span><span class="sxs-lookup"><span data-stu-id="04edb-461">Method invocation</span></span> | `F(x,y)`       | <span data-ttu-id="04edb-462">Разрешение перегрузки применяется для выбора подходящего метода `F` в содержащем классе или структуре.</span><span class="sxs-lookup"><span data-stu-id="04edb-462">Overload resolution is applied to select the best method `F` in the containing class or struct.</span></span> <span data-ttu-id="04edb-463">Метод вызывается со списком аргументов `(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-463">The method is invoked with the argument list `(x,y)`.</span></span> <span data-ttu-id="04edb-464">Если метод не является `static`, выражение экземпляра имеет `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-464">If the method is not `static`, the instance expression is `this`.</span></span> | 
|                   | `T.F(x,y)`     | <span data-ttu-id="04edb-465">Разрешение перегрузки применяется для выбора подходящего метода `F` в классе или структуре `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-465">Overload resolution is applied to select the best method `F` in the class or struct `T`.</span></span> <span data-ttu-id="04edb-466">Ошибка времени привязки возникает, если метод не является `static`.</span><span class="sxs-lookup"><span data-stu-id="04edb-466">A binding-time error occurs if the method is not `static`.</span></span> <span data-ttu-id="04edb-467">Метод вызывается со списком аргументов `(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-467">The method is invoked with the argument list `(x,y)`.</span></span> | 
|                   | `e.F(x,y)`     | <span data-ttu-id="04edb-468">Разрешение перегрузки применяется для выбора наиболее подходящего метода F в класса, структуры или интерфейса, передаваемом типе `e`.</span><span class="sxs-lookup"><span data-stu-id="04edb-468">Overload resolution is applied to select the best method F in the class, struct, or interface given by the type of `e`.</span></span> <span data-ttu-id="04edb-469">Возникает ошибка времени привязки, если метод `static`.</span><span class="sxs-lookup"><span data-stu-id="04edb-469">A binding-time error occurs if the method is `static`.</span></span> <span data-ttu-id="04edb-470">Метод вызывается с выражением экземпляра `e` и список аргументов `(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-470">The method is invoked with the instance expression `e` and the argument list `(x,y)`.</span></span> | 
| <span data-ttu-id="04edb-471">Доступ к свойству</span><span class="sxs-lookup"><span data-stu-id="04edb-471">Property access</span></span>   | `P`            | <span data-ttu-id="04edb-472">`get` Метод доступа свойства `P` вызывается в содержащем классе или структуре.</span><span class="sxs-lookup"><span data-stu-id="04edb-472">The `get` accessor of the property `P` in the containing class or struct is invoked.</span></span> <span data-ttu-id="04edb-473">Ошибка времени компиляции возникает, если `P` доступен только для записи.</span><span class="sxs-lookup"><span data-stu-id="04edb-473">A compile-time error occurs if `P` is write-only.</span></span> <span data-ttu-id="04edb-474">Если `P` не `static`, выражение экземпляра имеет `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-474">If `P` is not `static`, the instance expression is `this`.</span></span> | 
|                   | `P = value`    | <span data-ttu-id="04edb-475">`set` Метод доступа свойства `P` в содержащем классе или структуре вызывается со списком аргументов `(value)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-475">The `set` accessor of the property `P` in the containing class or struct is invoked with the argument list `(value)`.</span></span> <span data-ttu-id="04edb-476">Ошибка времени компиляции возникает, если `P` доступен только для чтения.</span><span class="sxs-lookup"><span data-stu-id="04edb-476">A compile-time error occurs if `P` is read-only.</span></span> <span data-ttu-id="04edb-477">Если `P` не `static`, выражение экземпляра имеет `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-477">If `P` is not `static`, the instance expression is `this`.</span></span> | 
|                   | `T.P`          | <span data-ttu-id="04edb-478">`get` Метод доступа свойства `P` в классе или структуре `T` вызывается.</span><span class="sxs-lookup"><span data-stu-id="04edb-478">The `get` accessor of the property `P` in the class or struct `T` is invoked.</span></span> <span data-ttu-id="04edb-479">Ошибка времени компиляции возникает, если `P` не `static` или, если `P` доступен только для записи.</span><span class="sxs-lookup"><span data-stu-id="04edb-479">A compile-time error occurs if `P` is not `static` or if `P` is write-only.</span></span> | 
|                   | `T.P = value`  | <span data-ttu-id="04edb-480">`set` Метод доступа свойства `P` в классе или структуре `T` вызывается со списком аргументов `(value)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-480">The `set` accessor of the property `P` in the class or struct `T` is invoked with the argument list `(value)`.</span></span> <span data-ttu-id="04edb-481">Ошибка времени компиляции возникает, если `P` не `static` или, если `P` доступен только для чтения.</span><span class="sxs-lookup"><span data-stu-id="04edb-481">A compile-time error occurs if `P` is not `static` or if `P` is read-only.</span></span> | 
|                   | `e.P`          | <span data-ttu-id="04edb-482">`get` Метод доступа свойства `P` в класса, структуры или интерфейса, передаваемом типе `e` вызывается с выражением экземпляра `e`.</span><span class="sxs-lookup"><span data-stu-id="04edb-482">The `get` accessor of the property `P` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e`.</span></span> <span data-ttu-id="04edb-483">Ошибка во время привязки возникает, если `P` — `static` или, если `P` доступен только для записи.</span><span class="sxs-lookup"><span data-stu-id="04edb-483">A binding-time error occurs if `P` is `static` or if `P` is write-only.</span></span> | 
|                   | `e.P = value`  | <span data-ttu-id="04edb-484">`set` Метод доступа свойства `P` в класса, структуры или интерфейса, передаваемом типе `e` вызывается с выражением экземпляра `e` и список аргументов `(value)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-484">The `set` accessor of the property `P` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e` and the argument list `(value)`.</span></span> <span data-ttu-id="04edb-485">Ошибка во время привязки возникает, если `P` — `static` или, если `P` доступен только для чтения.</span><span class="sxs-lookup"><span data-stu-id="04edb-485">A binding-time error occurs if `P` is `static` or if `P` is read-only.</span></span> | 
| <span data-ttu-id="04edb-486">Доступ к событиям</span><span class="sxs-lookup"><span data-stu-id="04edb-486">Event access</span></span>      | `E += value`   | <span data-ttu-id="04edb-487">`add` Метод доступа события `E` вызывается в содержащем классе или структуре.</span><span class="sxs-lookup"><span data-stu-id="04edb-487">The `add` accessor of the event `E` in the containing class or struct is invoked.</span></span> <span data-ttu-id="04edb-488">Если `E` является не статическим, выражение экземпляра имеет `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-488">If `E` is not static, the instance expression is `this`.</span></span> | 
|                   | `E -= value`   | <span data-ttu-id="04edb-489">`remove` Метод доступа события `E` вызывается в содержащем классе или структуре.</span><span class="sxs-lookup"><span data-stu-id="04edb-489">The `remove` accessor of the event `E` in the containing class or struct is invoked.</span></span> <span data-ttu-id="04edb-490">Если `E` является не статическим, выражение экземпляра имеет `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-490">If `E` is not static, the instance expression is `this`.</span></span> | 
|                   | `T.E += value` | <span data-ttu-id="04edb-491">`add` Метод доступа события `E` в классе или структуре `T` вызывается.</span><span class="sxs-lookup"><span data-stu-id="04edb-491">The `add` accessor of the event `E` in the class or struct `T` is invoked.</span></span> <span data-ttu-id="04edb-492">Ошибка во время привязки возникает, если `E` не является статическим.</span><span class="sxs-lookup"><span data-stu-id="04edb-492">A binding-time error occurs if `E` is not static.</span></span> | 
|                   | `T.E -= value` | <span data-ttu-id="04edb-493">`remove` Метод доступа события `E` в классе или структуре `T` вызывается.</span><span class="sxs-lookup"><span data-stu-id="04edb-493">The `remove` accessor of the event `E` in the class or struct `T` is invoked.</span></span> <span data-ttu-id="04edb-494">Ошибка во время привязки возникает, если `E` не является статическим.</span><span class="sxs-lookup"><span data-stu-id="04edb-494">A binding-time error occurs if `E` is not static.</span></span> | 
|                   | `e.E += value` | <span data-ttu-id="04edb-495">`add` Метод доступа события `E` в класса, структуры или интерфейса, передаваемом типе `e` вызывается с выражением экземпляра `e`.</span><span class="sxs-lookup"><span data-stu-id="04edb-495">The `add` accessor of the event `E` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e`.</span></span> <span data-ttu-id="04edb-496">Ошибка во время привязки возникает, если `E` является статическим.</span><span class="sxs-lookup"><span data-stu-id="04edb-496">A binding-time error occurs if `E` is static.</span></span> | 
|                   | `e.E -= value` | <span data-ttu-id="04edb-497">`remove` Метод доступа события `E` в класса, структуры или интерфейса, передаваемом типе `e` вызывается с выражением экземпляра `e`.</span><span class="sxs-lookup"><span data-stu-id="04edb-497">The `remove` accessor of the event `E` in the class, struct, or interface given by the type of `e` is invoked with the instance expression `e`.</span></span> <span data-ttu-id="04edb-498">Ошибка во время привязки возникает, если `E` является статическим.</span><span class="sxs-lookup"><span data-stu-id="04edb-498">A binding-time error occurs if `E` is static.</span></span> | 
| <span data-ttu-id="04edb-499">Доступ к индексатору</span><span class="sxs-lookup"><span data-stu-id="04edb-499">Indexer access</span></span>    | `e[x,y]`       | <span data-ttu-id="04edb-500">Разрешение перегрузки применяется для выбора наиболее подходящего индексатора в класса, структуры или интерфейса, передаваемом типе e.</span><span class="sxs-lookup"><span data-stu-id="04edb-500">Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of e.</span></span> <span data-ttu-id="04edb-501">`get` С выражением экземпляра вызывается метод доступа индексатора `e` и список аргументов `(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-501">The `get` accessor of the indexer is invoked with the instance expression `e` and the argument list `(x,y)`.</span></span> <span data-ttu-id="04edb-502">Ошибка времени привязки возникает, если индексатор доступен только для записи.</span><span class="sxs-lookup"><span data-stu-id="04edb-502">A binding-time error occurs if the indexer is write-only.</span></span> | 
|                   | `e[x,y] = value` | <span data-ttu-id="04edb-503">Разрешение перегрузки применяется для выбора наиболее подходящего индексатора в класса, структуры или интерфейса, передаваемом типе `e`.</span><span class="sxs-lookup"><span data-stu-id="04edb-503">Overload resolution is applied to select the best indexer in the class, struct, or interface given by the type of `e`.</span></span> <span data-ttu-id="04edb-504">`set` С выражением экземпляра вызывается метод доступа индексатора `e` и список аргументов `(x,y,value)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-504">The `set` accessor of the indexer is invoked with the instance expression `e` and the argument list `(x,y,value)`.</span></span> <span data-ttu-id="04edb-505">Ошибка времени привязки возникает, если индексатор доступен только для чтения.</span><span class="sxs-lookup"><span data-stu-id="04edb-505">A binding-time error occurs if the indexer is read-only.</span></span> | 
| <span data-ttu-id="04edb-506">Вызов оператора</span><span class="sxs-lookup"><span data-stu-id="04edb-506">Operator invocation</span></span> | `-x`         | <span data-ttu-id="04edb-507">Разрешение перегрузки применяется для выбора наиболее подходящего унарного оператора в классе или структуре, передаваемой по типу `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-507">Overload resolution is applied to select the best unary operator in the class or struct given by the type of `x`.</span></span> <span data-ttu-id="04edb-508">Выбранный оператор вызывается со списком аргументов `(x)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-508">The selected operator is invoked with the argument list `(x)`.</span></span> | 
|                     | `x + y`      | <span data-ttu-id="04edb-509">Разрешение перегрузки применяется для выбора наиболее подходящего бинарного оператора в классах или структурах, передаваемых типы `x` и `y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-509">Overload resolution is applied to select the best binary operator in the classes or structs given by the types of `x` and `y`.</span></span> <span data-ttu-id="04edb-510">Выбранный оператор вызывается со списком аргументов `(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-510">The selected operator is invoked with the argument list `(x,y)`.</span></span> | 
| <span data-ttu-id="04edb-511">Вызов конструктора экземпляра</span><span class="sxs-lookup"><span data-stu-id="04edb-511">Instance constructor invocation</span></span> | `new T(x,y)` | <span data-ttu-id="04edb-512">Разрешение перегрузки применяется для выбора наиболее конструктор экземпляра в классе или структуре `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-512">Overload resolution is applied to select the best instance constructor in the class or struct `T`.</span></span> <span data-ttu-id="04edb-513">Конструктор экземпляра вызывается со списком аргументов `(x,y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-513">The instance constructor is invoked with the argument list `(x,y)`.</span></span> | 

### <a name="argument-lists"></a><span data-ttu-id="04edb-514">Списки аргументов</span><span class="sxs-lookup"><span data-stu-id="04edb-514">Argument lists</span></span>

<span data-ttu-id="04edb-515">Каждый вызов функции члена и делегат содержит список аргументов, который предоставляет фактические значения или ссылки на переменные для параметров функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-515">Every function member and delegate invocation includes an argument list which provides actual values or variable references for the parameters of the function member.</span></span> <span data-ttu-id="04edb-516">Синтаксис для указания списка аргументов вызова функции-члена зависит от категории функции-члена:</span><span class="sxs-lookup"><span data-stu-id="04edb-516">The syntax for specifying the argument list of a function member invocation depends on the function member category:</span></span>

*  <span data-ttu-id="04edb-517">Для экземпляра конструкторов, методов, индексаторов и делегатов, аргументы указываются как *argument_list*, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-517">For instance constructors, methods, indexers and delegates, the arguments are specified as an *argument_list*, as described below.</span></span> <span data-ttu-id="04edb-518">Для индексаторов, при вызове `set` метода доступа, список аргументов дополнительно включает выражение, указанное в качестве правого операнда оператора присваивания.</span><span class="sxs-lookup"><span data-stu-id="04edb-518">For indexers, when invoking the `set` accessor, the argument list additionally includes the expression specified as the right operand of the assignment operator.</span></span>
*  <span data-ttu-id="04edb-519">Для свойств, список аргументов пуст, при вызове `get` метод доступа и состоит из выражения, указанного в качестве правого операнда оператора присваивания, при вызове `set` метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-519">For properties, the argument list is empty when invoking the `get` accessor, and consists of the expression specified as the right operand of the assignment operator when invoking the `set` accessor.</span></span>
*  <span data-ttu-id="04edb-520">Для событий, список аргументов, состоит из выражения, указанного в качестве правого операнда оператора `+=` или `-=` оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-520">For events, the argument list consists of the expression specified as the right operand of the `+=` or `-=` operator.</span></span>
*  <span data-ttu-id="04edb-521">Для определяемых пользователем операторов список аргументов состоит из одного операнда унарный оператор или два операнда бинарного оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-521">For user-defined operators, the argument list consists of the single operand of the unary operator or the two operands of the binary operator.</span></span>

<span data-ttu-id="04edb-522">Аргументы свойств ([свойства](classes.md#properties)), события ([события](classes.md#events)) и определяемые пользователем операторы ([операторы](classes.md#operators)), всегда передаются в качестве значения параметров ([ Параметры по значению](classes.md#value-parameters)).</span><span class="sxs-lookup"><span data-stu-id="04edb-522">The arguments of properties ([Properties](classes.md#properties)), events ([Events](classes.md#events)), and user-defined operators ([Operators](classes.md#operators)) are always passed as value parameters ([Value parameters](classes.md#value-parameters)).</span></span> <span data-ttu-id="04edb-523">Аргументы индексаторов ([индексаторы](classes.md#indexers)), всегда передаются в качестве значения параметров ([параметры по значению](classes.md#value-parameters)) или массивы параметров ([массивы параметров](classes.md#parameter-arrays)).</span><span class="sxs-lookup"><span data-stu-id="04edb-523">The arguments of indexers ([Indexers](classes.md#indexers)) are always passed as value parameters ([Value parameters](classes.md#value-parameters)) or parameter arrays ([Parameter arrays](classes.md#parameter-arrays)).</span></span> <span data-ttu-id="04edb-524">Ссылки и выходные параметры не поддерживаются для следующих категорий функций-членов.</span><span class="sxs-lookup"><span data-stu-id="04edb-524">Reference and output parameters are not supported for these categories of function members.</span></span>

<span data-ttu-id="04edb-525">Аргументы вызова конструктора, метода, индексатора или делегата экземпляр указываются как *argument_list*:</span><span class="sxs-lookup"><span data-stu-id="04edb-525">The arguments of an instance constructor, method, indexer or delegate invocation are specified as an *argument_list*:</span></span>

```antlr
argument_list
    : argument (',' argument)*
    ;

argument
    : argument_name? argument_value
    ;

argument_name
    : identifier ':'
    ;

argument_value
    : expression
    | 'ref' variable_reference
    | 'out' variable_reference
    ;
```

<span data-ttu-id="04edb-526">*Argument_list* состоит из одного или нескольких *аргумент*s, разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-526">An *argument_list* consists of one or more *argument*s, separated by commas.</span></span> <span data-ttu-id="04edb-527">Каждый аргумент состоит из необязательного *имя_аргумента* следуют *argument_value*.</span><span class="sxs-lookup"><span data-stu-id="04edb-527">Each argument consists of an optional  *argument_name* followed by an *argument_value*.</span></span> <span data-ttu-id="04edb-528">*Аргумент* с *имя_аргумента* называется ***именованный аргумент***, тогда как *аргумент* без  *имя_аргумента* — ***позиционный аргумент***.</span><span class="sxs-lookup"><span data-stu-id="04edb-528">An *argument* with an *argument_name* is referred to as a ***named argument***, whereas an *argument* without an *argument_name* is a ***positional argument***.</span></span> <span data-ttu-id="04edb-529">Это ошибка для позиционного аргумента отображения после именованный аргумент в *argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-529">It is an error for a positional argument to appear after a named argument in an *argument_list*.</span></span>

<span data-ttu-id="04edb-530">*Argument_value* может принимать одно из следующих форм:</span><span class="sxs-lookup"><span data-stu-id="04edb-530">The *argument_value* can take one of the following forms:</span></span>

*  <span data-ttu-id="04edb-531">*Выражение*, означает, что аргумент передается как параметр значения ([параметры по значению](classes.md#value-parameters)).</span><span class="sxs-lookup"><span data-stu-id="04edb-531">An *expression*, indicating that the argument is passed as a value parameter ([Value parameters](classes.md#value-parameters)).</span></span>
*  <span data-ttu-id="04edb-532">Ключевое слово `ref` следуют *variable_reference* ([ссылки на переменные](variables.md#variable-references)), означает, что аргумент передается как параметр по ссылке ([ссылочные параметры ](classes.md#reference-parameters)).</span><span class="sxs-lookup"><span data-stu-id="04edb-532">The keyword `ref` followed by a *variable_reference* ([Variable references](variables.md#variable-references)), indicating that the argument is passed as a reference parameter ([Reference parameters](classes.md#reference-parameters)).</span></span> <span data-ttu-id="04edb-533">Переменной должен быть явно присвоен ([определенного присваивания](variables.md#definite-assignment)), прежде чем их можно было передать в качестве ссылочного параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-533">A variable must be definitely assigned ([Definite assignment](variables.md#definite-assignment)) before it can be passed as a reference parameter.</span></span> <span data-ttu-id="04edb-534">Ключевое слово `out` следуют *variable_reference* ([ссылки на переменные](variables.md#variable-references)), означает, что аргумент передается как выходной параметр ([выходных параметров](classes.md#output-parameters)).</span><span class="sxs-lookup"><span data-stu-id="04edb-534">The keyword `out` followed by a *variable_reference* ([Variable references](variables.md#variable-references)), indicating that the argument is passed as an output parameter ([Output parameters](classes.md#output-parameters)).</span></span> <span data-ttu-id="04edb-535">Переменная считается определенно присвоенной ([определенного присваивания](variables.md#definite-assignment)) следующий вызов члена функции, в котором переменная передается в качестве выходного параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-535">A variable is considered definitely assigned ([Definite assignment](variables.md#definite-assignment)) following a function member invocation in which the variable is passed as an output parameter.</span></span>

#### <a name="corresponding-parameters"></a><span data-ttu-id="04edb-536">Соответствующие параметры</span><span class="sxs-lookup"><span data-stu-id="04edb-536">Corresponding parameters</span></span>

<span data-ttu-id="04edb-537">Для каждого аргумента в списке аргументов должен быть соответствующего параметра в функции-члена или вызываемого делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-537">For each argument in an argument list there has to be a corresponding parameter in the function member or delegate being invoked.</span></span>

<span data-ttu-id="04edb-538">Список параметров, используемые в следующем примере определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-538">The parameter list used in the following is determined as follows:</span></span>

*  <span data-ttu-id="04edb-539">Виртуальные методы и индексаторы, определенные в классах список параметров выбирается из наиболее подходящего объявления или переопределить функции-члена, начиная с статический тип получателя и поиск в его базовых классов.</span><span class="sxs-lookup"><span data-stu-id="04edb-539">For virtual methods and indexers defined in classes, the parameter list is picked from the most specific declaration or override of the function member, starting with the static type of the receiver, and searching through its base classes.</span></span>
*  <span data-ttu-id="04edb-540">Методы интерфейса и индексаторы, выбирается в списке параметров формирования определение наиболее конкретный элемент, начиная с типом интерфейса и поиск в базовых интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="04edb-540">For interface methods and indexers, the parameter list is picked form the most specific definition of the member, starting with the interface type and searching through the base interfaces.</span></span> <span data-ttu-id="04edb-541">Если список уникальных параметров найден, создается список параметров с недоступными именами и без необязательных параметров, таким образом, чтобы вызовы нельзя использовать именованные параметры или пропустить необязательные аргументы.</span><span class="sxs-lookup"><span data-stu-id="04edb-541">If no unique parameter list is found, a parameter list with inaccessible names and no optional parameters is constructed, so that invocations cannot use named parameters or omit optional arguments.</span></span>
*  <span data-ttu-id="04edb-542">Для разделяемых методов используется список параметров определяющее объявление разделяемого метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-542">For partial methods, the parameter list of the defining partial method declaration is used.</span></span>
*  <span data-ttu-id="04edb-543">Для всех других функций-членов и делегаты имеется только один список параметров, который будет использоваться.</span><span class="sxs-lookup"><span data-stu-id="04edb-543">For all other function members and delegates there is only a single parameter list, which is the one used.</span></span>

<span data-ttu-id="04edb-544">Позиция аргумента или параметра определяется как число аргументов или параметров, предшествует ей в списке аргументов или списка параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-544">The position of an argument or parameter is defined as the number of arguments or parameters preceding it in the argument list or parameter list.</span></span>

<span data-ttu-id="04edb-545">Соответствующие параметры для аргументов членов функции устанавливаются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-545">The corresponding parameters for function member arguments are established as follows:</span></span>

*  <span data-ttu-id="04edb-546">Аргументы в *argument_list* конструкторы экземпляров, методов, индексаторов и делегатов:</span><span class="sxs-lookup"><span data-stu-id="04edb-546">Arguments in the *argument_list* of instance constructors, methods, indexers and delegates:</span></span>
    * <span data-ttu-id="04edb-547">Позиционные аргументы, где происходит фиксированный параметр в той же позиции в списке параметров соответствует этому параметру.</span><span class="sxs-lookup"><span data-stu-id="04edb-547">A positional argument where a fixed parameter occurs at the same position in the parameter list corresponds to that parameter.</span></span>
    * <span data-ttu-id="04edb-548">Позиционный аргумент функции-члена с массивом параметров вызван в обычной форме соответствует в массив параметров, который должен находиться в той же позиции в списке параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-548">A positional argument of a function member with a parameter array invoked in its normal form corresponds to the parameter  array, which must occur at the same position in the parameter list.</span></span>
    * <span data-ttu-id="04edb-549">Позиционный аргумент функции-члена с массивом параметров вызывается в расширенной форме, где нет фиксированного параметра происходит в той же позиции в списке параметров, соответствующий элемент в массиве параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-549">A positional argument of a function member with a parameter array invoked in its expanded form, where no fixed parameter occurs at the same position in the parameter list, corresponds to an element in the parameter array.</span></span>
    * <span data-ttu-id="04edb-550">Именованный аргумент соответствует параметру с тем же именем в списке параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-550">A named argument corresponds to the parameter of the same name in the parameter list.</span></span>
    * <span data-ttu-id="04edb-551">Для индексаторов, при вызове `set` метод доступа, выражение, указанное как правый операнд оператора присваивания соответствует неявный `value` параметр `set` объявление метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-551">For indexers, when invoking the `set` accessor, the expression specified as the right operand of the assignment operator corresponds to the implicit `value` parameter of the `set` accessor declaration.</span></span>
*  <span data-ttu-id="04edb-552">Для свойств, при вызове `get` существует метода доступа — без аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-552">For properties, when invoking the `get` accessor there are no arguments.</span></span> <span data-ttu-id="04edb-553">При вызове `set` метод доступа, выражение, указанное как правый операнд оператора присваивания соответствует неявный `value` параметр `set` объявление метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-553">When invoking the `set` accessor, the expression specified as the right operand of the assignment operator corresponds to the implicit `value` parameter of the `set` accessor declaration.</span></span>
*  <span data-ttu-id="04edb-554">Для пользовательских унарных операторов (включая преобразования) один операнд соответствует одному параметру объявления оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-554">For user-defined unary operators (including conversions), the single operand corresponds to the single parameter of the operator declaration.</span></span>
*  <span data-ttu-id="04edb-555">Для пользовательских бинарных операторов левый операнд соответствует первому параметру, а правый операнд соответствует значению второго параметра объявления оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-555">For user-defined binary operators, the left operand corresponds to the first parameter, and the right operand corresponds to the second parameter of the operator declaration.</span></span>

#### <a name="run-time-evaluation-of-argument-lists"></a><span data-ttu-id="04edb-556">Вычисление во время выполнения списков аргументов</span><span class="sxs-lookup"><span data-stu-id="04edb-556">Run-time evaluation of argument lists</span></span>

<span data-ttu-id="04edb-557">Во время выполнения обработки вызова функции-члена ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), выражения или ссылки на переменные из списка аргументов оцениваются в порядке слева направо, как выглядит следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-557">During the run-time processing of a function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), the expressions or variable references of an argument list are evaluated in order, from left to right, as follows:</span></span>

*  <span data-ttu-id="04edb-558">Для параметра значения, вычисляется выражение аргумента и неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) для соответствующего параметра типа выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-558">For a value parameter, the argument expression is evaluated and an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) to the corresponding parameter type is performed.</span></span> <span data-ttu-id="04edb-559">Результирующее значение становится начальное значение параметра в вызове функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-559">The resulting value becomes the initial value of the value parameter in the function member invocation.</span></span>
*  <span data-ttu-id="04edb-560">Для параметра ссылки или вывода вычисляется ссылка на переменную, и итоговое расположение хранилища становится место хранения, представленное параметром в вызове функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-560">For a reference or output parameter, the variable reference is evaluated and the resulting storage location becomes the storage location represented by the parameter in the function member invocation.</span></span> <span data-ttu-id="04edb-561">Если ссылка на переменную, заданной в качестве параметра ссылки или вывода является элементом массива *reference_type*, выполняется проверка во время выполнения, чтобы убедитесь, что тип элемента массива отличается от типа параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-561">If the variable reference given as a reference or output parameter is an array element of a *reference_type*, a run-time check is performed to ensure that the element type of the array is identical to the type of the parameter.</span></span> <span data-ttu-id="04edb-562">Если эта проверка завершается неудачно, `System.ArrayTypeMismatchException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-562">If this check fails, a `System.ArrayTypeMismatchException` is thrown.</span></span>

<span data-ttu-id="04edb-563">Методов, индексаторов и конструкторы экземпляров может объявлять их крайнее правое параметр будет массивом параметров ([массивы параметров](classes.md#parameter-arrays)).</span><span class="sxs-lookup"><span data-stu-id="04edb-563">Methods, indexers, and instance constructors may declare their right-most parameter to be a parameter array ([Parameter arrays](classes.md#parameter-arrays)).</span></span> <span data-ttu-id="04edb-564">Такие функции-члены вызываются нормальной форме или в их расширенными формами, в зависимости от того, который применяется ([применимого члена функции](expressions.md#applicable-function-member)):</span><span class="sxs-lookup"><span data-stu-id="04edb-564">Such function members are invoked either in their normal form or in their expanded form depending on which is applicable ([Applicable function member](expressions.md#applicable-function-member)):</span></span>

*  <span data-ttu-id="04edb-565">Когда функция-член с массивом параметров вызывается в нормальной форме, аргумент массива параметров должно быть одно выражение, которое может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) в тип массива параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-565">When a function member with a parameter array is invoked in its normal form, the argument given for the parameter array must be a single expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the parameter array type.</span></span> <span data-ttu-id="04edb-566">В этом случае в массиве параметров выступает точно параметра значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-566">In this case, the parameter array acts precisely like a value parameter.</span></span>
*  <span data-ttu-id="04edb-567">Когда функция-член с массивом параметров вызывается в расширенной форме, при вызове необходимо указать ноль или более позиционные аргументы для массива параметров, где каждый аргумент является выражение, которое может быть неявно преобразован ([неявные преобразования](conversions.md#implicit-conversions)) к типу элемента в массиве параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-567">When a function member with a parameter array is invoked in its expanded form, the invocation must specify zero or more positional arguments for the parameter array, where each argument is an expression that is implicitly convertible ([Implicit conversions](conversions.md#implicit-conversions)) to the element type of the parameter array.</span></span> <span data-ttu-id="04edb-568">В этом случае вызов создает экземпляр типа массив с длиной, соответствующей числу аргументов, инициализирует элементы экземпляра массива с заданными значениями аргументов и использует вновь созданный экземпляр массива в качестве фактического аргумент.</span><span class="sxs-lookup"><span data-stu-id="04edb-568">In this case, the invocation creates an instance of the parameter array type with a length corresponding to the number of arguments, initializes the elements of the array instance with the given argument values, and uses the newly created array instance as the actual argument.</span></span>

<span data-ttu-id="04edb-569">Из списка аргументов всегда вычисляются в порядке, в котором они написаны.</span><span class="sxs-lookup"><span data-stu-id="04edb-569">The expressions of an argument list are always evaluated in the order they are written.</span></span> <span data-ttu-id="04edb-570">Таким образом пример</span><span class="sxs-lookup"><span data-stu-id="04edb-570">Thus, the example</span></span>
```csharp
class Test
{
    static void F(int x, int y = -1, int z = -2) {
        System.Console.WriteLine("x = {0}, y = {1}, z = {2}", x, y, z);
    }

    static void Main() {
        int i = 0;
        F(i++, i++, i++);
        F(z: i++, x: i++);
    }
}
```
<span data-ttu-id="04edb-571">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="04edb-571">produces the output</span></span>
```
x = 0, y = 1, z = 2
x = 4, y = -1, z = 3
```

<span data-ttu-id="04edb-572">Правила совместного расхождения массива ([ковариацией](arrays.md#array-covariance)) разрешает значение типа массива `A[]` чтобы ссылаться на экземпляр типа массива `B[]`, если существует неявное преобразование ссылок из `B` для `A`.</span><span class="sxs-lookup"><span data-stu-id="04edb-572">The array co-variance rules ([Array covariance](arrays.md#array-covariance)) permit a value of an array type `A[]` to be a reference to an instance of an array type `B[]`, provided an implicit reference conversion exists from `B` to `A`.</span></span> <span data-ttu-id="04edb-573">Из-за этих правил, когда элемент массива значений *reference_type* передается как параметр ссылки или вывода, необходимо обеспечить, что фактическим типом элемента массива идентична параметра проверки во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-573">Because of these rules, when an array element of a *reference_type* is passed as a reference or output parameter, a run-time check is required to ensure that the actual element type of the array is identical to that of the parameter.</span></span> <span data-ttu-id="04edb-574">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-574">In the example</span></span>
```csharp
class Test
{
    static void F(ref object x) {...}

    static void Main() {
        object[] a = new object[10];
        object[] b = new string[10];
        F(ref a[0]);        // Ok
        F(ref b[1]);        // ArrayTypeMismatchException
    }
}
```
<span data-ttu-id="04edb-575">Второй вызов `F` вызывает `System.ArrayTypeMismatchException` исключение, так как тип фактического элемент `b` — `string` и не `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-575">the second invocation of `F` causes a `System.ArrayTypeMismatchException` to be thrown because the actual element type of `b` is `string` and not `object`.</span></span>

<span data-ttu-id="04edb-576">Когда функция-член с массивом параметров вызывается в расширенной форме, вызов обрабатывается точно так, как если выражение создания массива с помощью инициализатора массива ([выражениях создания массива](expressions.md#array-creation-expressions)) была вставлена вокруг Расширенные параметры.</span><span class="sxs-lookup"><span data-stu-id="04edb-576">When a function member with a parameter array is invoked in its expanded form, the invocation is processed exactly as if an array creation expression with an array initializer ([Array creation expressions](expressions.md#array-creation-expressions)) was inserted around the expanded parameters.</span></span> <span data-ttu-id="04edb-577">Например при объявлении</span><span class="sxs-lookup"><span data-stu-id="04edb-577">For example, given the declaration</span></span>
```csharp
void F(int x, int y, params object[] args);
```
<span data-ttu-id="04edb-578">следующие вызовы расширенной формы метода</span><span class="sxs-lookup"><span data-stu-id="04edb-578">the following invocations of the expanded form of the method</span></span>
```csharp
F(10, 20);
F(10, 20, 30, 40);
F(10, 20, 1, "hello", 3.0);
```
<span data-ttu-id="04edb-579">в точности соответствуют</span><span class="sxs-lookup"><span data-stu-id="04edb-579">correspond exactly to</span></span>
```csharp
F(10, 20, new object[] {});
F(10, 20, new object[] {30, 40});
F(10, 20, new object[] {1, "hello", 3.0});
```

<span data-ttu-id="04edb-580">В частности Обратите внимание на то, что создается пустой массив, при наличии ноль аргументов, вводимых для массива параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-580">In particular, note that an empty array is created when there are zero arguments given for the parameter array.</span></span>

<span data-ttu-id="04edb-581">Если аргументов опущены из функции-члена с соответствующими необязательными параметрами, неявно передаются аргументов по умолчанию объявления функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-581">When arguments are omitted from a function member with corresponding optional parameters, the default arguments of the function member declaration are implicitly passed.</span></span> <span data-ttu-id="04edb-582">Так как они всегда постоянны, их оценки не влияет на порядок вычисления остальных аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-582">Because these are always constant, their evaluation will not impact the evaluation order of the remaining arguments.</span></span>

### <a name="type-inference"></a><span data-ttu-id="04edb-583">Вывод типа</span><span class="sxs-lookup"><span data-stu-id="04edb-583">Type inference</span></span>

<span data-ttu-id="04edb-584">При вызове универсального метода без указания аргументов типа, ***вывод типа*** процесс пытается определить аргументы типа для вызова.</span><span class="sxs-lookup"><span data-stu-id="04edb-584">When a generic method is called without specifying type arguments, a ***type inference*** process attempts to infer type arguments for the call.</span></span> <span data-ttu-id="04edb-585">Наличие вывода типа позволяет использовать более удобный синтаксис для вызова универсального метода и позволяет программисту не указывать избыточных данных о типе.</span><span class="sxs-lookup"><span data-stu-id="04edb-585">The presence of type inference allows a more convenient syntax to be used for calling a generic method, and allows the programmer to avoid specifying redundant type information.</span></span> <span data-ttu-id="04edb-586">Например при объявлении метода:</span><span class="sxs-lookup"><span data-stu-id="04edb-586">For example, given the method declaration:</span></span>
```csharp
class Chooser
{
    static Random rand = new Random();

    public static T Choose<T>(T first, T second) {
        return (rand.Next(2) == 0)? first: second;
    }
}
```
<span data-ttu-id="04edb-587">можно вызвать `Choose` метод без явного указания аргумента типа:</span><span class="sxs-lookup"><span data-stu-id="04edb-587">it is possible to invoke the `Choose` method without explicitly specifying a type argument:</span></span>
```csharp
int i = Chooser.Choose(5, 213);                 // Calls Choose<int>

string s = Chooser.Choose("foo", "bar");        // Calls Choose<string>
```

<span data-ttu-id="04edb-588">Через вывод типа, аргументы типа `int` и `string` определяются из аргументов метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-588">Through type inference, the type arguments `int` and `string` are determined from the arguments to the method.</span></span>

<span data-ttu-id="04edb-589">Вывод типа происходит в процессе обработки привязки во время вызова метода ([вызовы методов](expressions.md#method-invocations)) и выполняется до вызова этапе разрешения перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-589">Type inference occurs as part of the binding-time processing of a method invocation ([Method invocations](expressions.md#method-invocations)) and takes place before the overload resolution step of the invocation.</span></span> <span data-ttu-id="04edb-590">Если группа конкретного метода указывается в вызове метода и аргументы типа указаны как часть вызова метода, вывод типа применяется к каждый универсальный метод, в группу методов.</span><span class="sxs-lookup"><span data-stu-id="04edb-590">When a particular method group is specified in a method invocation, and no type arguments are specified as part of the method invocation, type inference is applied to each generic method in the method group.</span></span> <span data-ttu-id="04edb-591">Если вывод типа завершается успешно, выводимыми аргументами типа используются для определения типов аргументов для последующего разрешения перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-591">If type inference succeeds, then the inferred type arguments are used to determine the types of arguments for subsequent overload resolution.</span></span> <span data-ttu-id="04edb-592">Если разрешение перегрузки выбирает в качестве вызов универсального метода, выведенный тип аргументы используются как фактических аргументов для вызова.</span><span class="sxs-lookup"><span data-stu-id="04edb-592">If overload resolution chooses a generic method as the one to invoke, then the inferred type arguments are used as the actual type arguments for the invocation.</span></span> <span data-ttu-id="04edb-593">Если не удается вывести тип для конкретного метода, этот метод не участвует в разрешении перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-593">If type inference for a particular method fails, that method does not participate in overload resolution.</span></span> <span data-ttu-id="04edb-594">Сбой определения типа, само по себе, не вызывает ошибку во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-594">The failure of type inference, in and of itself, does not cause a binding-time error.</span></span> <span data-ttu-id="04edb-595">Тем не менее оно часто ведет к ошибке во время привязки при разрешении перегрузки не удается найти применимые методы.</span><span class="sxs-lookup"><span data-stu-id="04edb-595">However, it often leads to a binding-time error when overload resolution then fails to find any applicable methods.</span></span>

<span data-ttu-id="04edb-596">Если предоставленное число аргументов отличается, чем число параметров в методе, затем определение немедленно завершается со сбоем.</span><span class="sxs-lookup"><span data-stu-id="04edb-596">If the supplied number of arguments is different than the number of parameters in the method, then inference immediately fails.</span></span> <span data-ttu-id="04edb-597">В противном случае предполагается, что универсальный метод имеет следующую сигнатуру:</span><span class="sxs-lookup"><span data-stu-id="04edb-597">Otherwise, assume that the generic method has the following signature:</span></span>
```csharp
Tr M<X1,...,Xn>(T1 x1, ..., Tm xm)
```

<span data-ttu-id="04edb-598">При вызове метода формы `M(E1...Em)` задачей вывода типа является поиск аргументов уникальный тип `S1...Sn` для каждого параметра типа `X1...Xn` таким образом, вызов `M<S1...Sn>(E1...Em)` становится действительным.</span><span class="sxs-lookup"><span data-stu-id="04edb-598">With a method call of the form `M(E1...Em)` the task of type inference is to find unique type arguments `S1...Sn` for each of the type parameters `X1...Xn` so that the call `M<S1...Sn>(E1...Em)` becomes valid.</span></span>

<span data-ttu-id="04edb-599">Во время вывода каждый параметр типа `Xi` либо *фиксированной* к определенному типу `Si` или *нефиксированных* с связан набор *границы*.</span><span class="sxs-lookup"><span data-stu-id="04edb-599">During the process of inference each type parameter `Xi` is either *fixed* to a particular type `Si` or *unfixed* with an associated set of *bounds*.</span></span> <span data-ttu-id="04edb-600">Каждая граница представляет собой определенный тип `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-600">Each of the bounds is some type `T`.</span></span> <span data-ttu-id="04edb-601">Изначально каждая переменная типа `Xi` является репликой с пустой набор границ.</span><span class="sxs-lookup"><span data-stu-id="04edb-601">Initially each type variable `Xi` is unfixed with an empty set of bounds.</span></span>

<span data-ttu-id="04edb-602">Вывод типа происходит поэтапно.</span><span class="sxs-lookup"><span data-stu-id="04edb-602">Type inference takes place in phases.</span></span> <span data-ttu-id="04edb-603">Каждый этап попытается определить аргументы типа для дополнительные переменные типа на основании результатов предыдущего этапа.</span><span class="sxs-lookup"><span data-stu-id="04edb-603">Each phase will try to infer type arguments for more type variables based on the findings of the previous phase.</span></span> <span data-ttu-id="04edb-604">На первом этапе делает некоторые начальной выводы границ, тогда как второй этап исправления переменных типа для конкретных типов и дополнительно определяет границы.</span><span class="sxs-lookup"><span data-stu-id="04edb-604">The first phase makes some initial inferences of bounds, whereas the second phase fixes type variables to specific types and infers further bounds.</span></span> <span data-ttu-id="04edb-605">Второй этап может потребоваться повторить несколько раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-605">The second phase may have to be repeated a number of times.</span></span>

<span data-ttu-id="04edb-606">*Примечание.* Тип вывода происходит не только в том случае, при вызове универсального метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-606">*Note:* Type inference takes place not only when a generic method is called.</span></span> <span data-ttu-id="04edb-607">Определение типа для преобразования групп методов описан в [вывод типа при преобразовании групп методов](expressions.md#type-inference-for-conversion-of-method-groups) и поиск это наиболее распространенный тип набора выражений, описан в [поиск это наиболее распространенный тип набора выражений](expressions.md#finding-the-best-common-type-of-a-set-of-expressions).</span><span class="sxs-lookup"><span data-stu-id="04edb-607">Type inference for conversion of method groups is described in [Type inference for conversion of method groups](expressions.md#type-inference-for-conversion-of-method-groups) and finding the best common type of a set of expressions is described in [Finding the best common type of a set of expressions](expressions.md#finding-the-best-common-type-of-a-set-of-expressions).</span></span>

#### <a name="the-first-phase"></a><span data-ttu-id="04edb-608">На первом этапе</span><span class="sxs-lookup"><span data-stu-id="04edb-608">The first phase</span></span>

<span data-ttu-id="04edb-609">Для каждого из аргументов метода `Ei`:</span><span class="sxs-lookup"><span data-stu-id="04edb-609">For each of the method arguments `Ei`:</span></span>

*   <span data-ttu-id="04edb-610">Если `Ei` представляет собой анонимную функцию, *явный вывод типа параметра* ([Вывод явных типов параметров](expressions.md#explicit-parameter-type-inferences)) осуществляется из `Ei` для `Ti`</span><span class="sxs-lookup"><span data-stu-id="04edb-610">If `Ei` is an anonymous function, an *explicit parameter type inference* ([Explicit parameter type inferences](expressions.md#explicit-parameter-type-inferences)) is made from `Ei` to `Ti`</span></span>
*   <span data-ttu-id="04edb-611">В противном случае, если `Ei` с типом `U` и `xi` является параметром значения то *вывод по нижней границе* становится *из* `U` *для* `Ti`.</span><span class="sxs-lookup"><span data-stu-id="04edb-611">Otherwise, if `Ei` has a type `U` and `xi` is a value parameter then a *lower-bound inference* is made *from* `U` *to* `Ti`.</span></span>
*   <span data-ttu-id="04edb-612">В противном случае, если `Ei` с типом `U` и `xi` — `ref` или `out` параметр исключение *точное определение* становится *из* `U` *для* `Ti`.</span><span class="sxs-lookup"><span data-stu-id="04edb-612">Otherwise, if `Ei` has a type `U` and `xi` is a `ref` or `out` parameter then an *exact inference* is made *from* `U` *to* `Ti`.</span></span>
*   <span data-ttu-id="04edb-613">В противном случае — сделать вывод для этого аргумента.</span><span class="sxs-lookup"><span data-stu-id="04edb-613">Otherwise, no inference is made for this argument.</span></span>


#### <a name="the-second-phase"></a><span data-ttu-id="04edb-614">Второй этап</span><span class="sxs-lookup"><span data-stu-id="04edb-614">The second phase</span></span>

<span data-ttu-id="04edb-615">Второй этап выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-615">The second phase proceeds as follows:</span></span>

*   <span data-ttu-id="04edb-616">Все *нефиксированных* переменных типа `Xi` какие не поддерживают *зависят от* ([зависимость](expressions.md#dependence)) любой `Xj` исправленные ([устранению](expressions.md#fixing)).</span><span class="sxs-lookup"><span data-stu-id="04edb-616">All *unfixed* type variables `Xi` which do not *depend on* ([Dependence](expressions.md#dependence)) any `Xj` are fixed ([Fixing](expressions.md#fixing)).</span></span>
*   <span data-ttu-id="04edb-617">Если таких переменных типа не существует, все *нефиксированных* переменных типа `Xi` являются *фиксированной* для которого все указанные ниже хранения:</span><span class="sxs-lookup"><span data-stu-id="04edb-617">If no such type variables exist, all *unfixed* type variables `Xi` are *fixed* for which all of the following hold:</span></span>
    *   <span data-ttu-id="04edb-618">Не существует по крайней мере один тип переменной `Xj` , зависящий от `Xi`</span><span class="sxs-lookup"><span data-stu-id="04edb-618">There is at least one type variable `Xj` that depends on `Xi`</span></span>
    *   <span data-ttu-id="04edb-619">`Xi` имеет непустой набор границ</span><span class="sxs-lookup"><span data-stu-id="04edb-619">`Xi` has a non-empty set of bounds</span></span>
*   <span data-ttu-id="04edb-620">Если таких переменных типа не существует и все еще существуют *нефиксированных* переменных типа, вывод типа завершается сбоем.</span><span class="sxs-lookup"><span data-stu-id="04edb-620">If no such type variables exist and there are still *unfixed* type variables, type inference fails.</span></span>
*   <span data-ttu-id="04edb-621">В противном случае, если нет ничего *нефиксированных* переменных типа существует, вывод типа завершается успешно.</span><span class="sxs-lookup"><span data-stu-id="04edb-621">Otherwise, if no further *unfixed* type variables exist, type inference succeeds.</span></span>
*   <span data-ttu-id="04edb-622">В противном случае — для всех аргументов `Ei` с соответствующим типом параметра `Ti` где *выходных типов* ([выходных типов](expressions.md#output-types)) содержат *нефиксированных* переменные типа `Xj` , но *входных типов* ([входных типов](expressions.md#input-types)) этого не сделать, *вывода вывод типа* ([вывод типа вывода ](expressions.md#output-type-inferences)) становится *из* `Ei` *для* `Ti`.</span><span class="sxs-lookup"><span data-stu-id="04edb-622">Otherwise, for all arguments `Ei` with corresponding parameter type `Ti` where the *output types* ([Output types](expressions.md#output-types)) contain *unfixed* type variables `Xj` but the *input types* ([Input types](expressions.md#input-types)) do not, an *output type inference* ([Output type inferences](expressions.md#output-type-inferences)) is made *from* `Ei` *to* `Ti`.</span></span> <span data-ttu-id="04edb-623">Затем второй этап повторяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-623">Then the second phase is repeated.</span></span>

#### <a name="input-types"></a><span data-ttu-id="04edb-624">Типы входных данных</span><span class="sxs-lookup"><span data-stu-id="04edb-624">Input types</span></span>

<span data-ttu-id="04edb-625">Если `E` является группой методов или неявно типизированные анонимная функция и `T` — это делегат, тип или тип дерева выражения, а затем все типы параметров `T` являются *входных типов* из `E` *с типом* `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-625">If `E` is a method group or implicitly typed anonymous function and `T` is a delegate type or expression tree type then all the parameter types of `T` are *input types* of `E` *with type* `T`.</span></span>

####  <a name="output-types"></a><span data-ttu-id="04edb-626">Типы выходных данных</span><span class="sxs-lookup"><span data-stu-id="04edb-626">Output types</span></span>

<span data-ttu-id="04edb-627">Если `E` группу методов или анонимной функции и `T` — это делегат, тип или тип дерева выражения, то тип возвращаемого значения `T` — *тип выходных данных* `E` *с типом*  `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-627">If `E` is a method group or an anonymous function and `T` is a delegate type or expression tree type then the return type of `T` is an *output type of* `E` *with type* `T`.</span></span>

#### <a name="dependence"></a><span data-ttu-id="04edb-628">Зависимость</span><span class="sxs-lookup"><span data-stu-id="04edb-628">Dependence</span></span>

<span data-ttu-id="04edb-629">*Нефиксированных* переменной типа `Xi` *напрямую зависит от* переменной нефиксированных типа `Xj` if для некоторых аргументов `Ek` с типом `Tk` `Xj` происходит в *тип входного* из `Ek` с типом `Tk` и `Xi` происходит в *тип выходных данных* из `Ek` с типом `Tk`.</span><span class="sxs-lookup"><span data-stu-id="04edb-629">An *unfixed* type variable `Xi` *depends directly on* an unfixed type variable `Xj` if for some argument `Ek` with type `Tk` `Xj` occurs in an *input type* of `Ek` with type `Tk` and `Xi` occurs in an *output type* of `Ek` with type `Tk`.</span></span>

<span data-ttu-id="04edb-630">`Xj` *зависит от* `Xi` Если `Xj` *напрямую зависит от* `Xi` или, если `Xi` *напрямую зависит от* `Xk` и `Xk` *зависит от* `Xj`.</span><span class="sxs-lookup"><span data-stu-id="04edb-630">`Xj` *depends on* `Xi` if `Xj` *depends directly on* `Xi` or if `Xi` *depends directly on* `Xk` and `Xk` *depends on* `Xj`.</span></span> <span data-ttu-id="04edb-631">Таким образом, «зависит» является транзитивным, но не извлечение рефлексивных замыкание «напрямую зависит от».</span><span class="sxs-lookup"><span data-stu-id="04edb-631">Thus "depends on" is the transitive but not reflexive closure of "depends directly on".</span></span>

#### <a name="output-type-inferences"></a><span data-ttu-id="04edb-632">Вывод типа вывода</span><span class="sxs-lookup"><span data-stu-id="04edb-632">Output type inferences</span></span>

<span data-ttu-id="04edb-633">*Вывода вывод типа* становится *из* выражение `E` *для* типом `T` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-633">An *output type inference* is made *from* an expression `E` *to* a type `T` in the following way:</span></span>

*  <span data-ttu-id="04edb-634">Если `E` представляет собой анонимную функцию с возвращаемым типом, выводимым `U` ([выводимого возвращаемый тип](expressions.md#inferred-return-type)) и `T` — это тип делегата или тип дерева выражения с типом возвращаемого значения `Tb`, затем *вывод по нижней границе* ([нижней границам](expressions.md#lower-bound-inferences)) становится *из* `U` *для* `Tb`.</span><span class="sxs-lookup"><span data-stu-id="04edb-634">If `E` is an anonymous function with inferred return type  `U` ([Inferred return type](expressions.md#inferred-return-type)) and `T` is a delegate type or expression tree type with return type `Tb`, then a *lower-bound inference* ([Lower-bound inferences](expressions.md#lower-bound-inferences)) is made *from* `U` *to* `Tb`.</span></span>
*  <span data-ttu-id="04edb-635">В противном случае, если `E` является группой методов и `T` — это тип делегата или тип дерева выражения с типами параметров `T1...Tk` и типом возвращаемого значения `Tb`и разрешение перегрузки `E` с типами `T1...Tk` дает единый метод с возвращаемым типом `U`, а затем *вывод по нижней границе* становится *из* `U` *для* `Tb`.</span><span class="sxs-lookup"><span data-stu-id="04edb-635">Otherwise, if `E` is a method group and `T` is a delegate type or expression tree type with parameter types `T1...Tk` and return type `Tb`, and overload resolution of `E` with the types `T1...Tk` yields a single method with return type `U`, then a *lower-bound inference* is made *from* `U` *to* `Tb`.</span></span>
*  <span data-ttu-id="04edb-636">В противном случае, если `E` представляет собой выражение с типом `U`, а затем *вывод по нижней границе* становится *из* `U` *для* `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-636">Otherwise, if `E` is an expression with type `U`, then a *lower-bound inference* is made *from* `U` *to* `T`.</span></span>
*  <span data-ttu-id="04edb-637">В противном случае вывод не производится.</span><span class="sxs-lookup"><span data-stu-id="04edb-637">Otherwise, no inferences are made.</span></span>

#### <a name="explicit-parameter-type-inferences"></a><span data-ttu-id="04edb-638">Вывод явных типов параметров</span><span class="sxs-lookup"><span data-stu-id="04edb-638">Explicit parameter type inferences</span></span>

<span data-ttu-id="04edb-639">*Явный вывод типа параметра* становится *из* выражение `E` *для* типом `T` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-639">An *explicit parameter type inference* is made *from* an expression `E` *to* a type `T` in the following way:</span></span>

*  <span data-ttu-id="04edb-640">Если `E` является явным образом типизированной анонимной функцией с типами параметров `U1...Uk` и `T` — это тип делегата или тип дерева выражения с типами параметров `V1...Vk` затем для каждого `Ui` *точное Вывод* ([точные выводы](expressions.md#exact-inferences)) становится *из* `Ui` *для* соответствующего `Vi`.</span><span class="sxs-lookup"><span data-stu-id="04edb-640">If `E` is an explicitly typed anonymous function with parameter types `U1...Uk` and `T` is a delegate type or expression tree type with parameter types `V1...Vk` then for each `Ui` an *exact inference* ([Exact inferences](expressions.md#exact-inferences)) is made *from* `Ui` *to* the corresponding `Vi`.</span></span>

#### <a name="exact-inferences"></a><span data-ttu-id="04edb-641">Точный вывод</span><span class="sxs-lookup"><span data-stu-id="04edb-641">Exact inferences</span></span>

<span data-ttu-id="04edb-642">*Точное определение* *из* типом `U` *для* типом `V` выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-642">An *exact inference* *from* a type `U` *to* a type `V` is made as follows:</span></span>

*  <span data-ttu-id="04edb-643">Если `V` является одним из *нефиксированных* `Xi` затем `U` добавляется к набору точное границы для `Xi`.</span><span class="sxs-lookup"><span data-stu-id="04edb-643">If `V` is one of the *unfixed* `Xi` then `U` is added to the set of exact bounds for `Xi`.</span></span>

*  <span data-ttu-id="04edb-644">В противном случае задает `V1...Vk` и `U1...Uk` определяются путем проверки, если применим один из следующих случаев:</span><span class="sxs-lookup"><span data-stu-id="04edb-644">Otherwise, sets `V1...Vk` and `U1...Uk` are determined by checking if any of the following cases apply:</span></span>

   *  <span data-ttu-id="04edb-645">`V` является типом массива `V1[...]` и `U` является типом массива `U1[...]` одинакового ранга кортежам</span><span class="sxs-lookup"><span data-stu-id="04edb-645">`V` is an array type `V1[...]` and `U` is an array type `U1[...]`  of the same rank</span></span>
   *  <span data-ttu-id="04edb-646">`V` — Это тип `V1?` и `U` является типом `U1?`</span><span class="sxs-lookup"><span data-stu-id="04edb-646">`V` is the type `V1?` and `U` is the type `U1?`</span></span>
   *  <span data-ttu-id="04edb-647">`V` — сконструированный тип `C<V1...Vk>`и `U` — сконструированный тип `C<U1...Uk>`</span><span class="sxs-lookup"><span data-stu-id="04edb-647">`V` is a constructed type `C<V1...Vk>`and `U` is a constructed type `C<U1...Uk>`</span></span>

   <span data-ttu-id="04edb-648">Если какие-либо из этих случаев применимы затем *точное определение* становится *из* каждого `Ui` *для* соответствующего `Vi`.</span><span class="sxs-lookup"><span data-stu-id="04edb-648">If any of these cases apply then an *exact inference* is made *from* each `Ui` *to* the corresponding `Vi`.</span></span>

*  <span data-ttu-id="04edb-649">В противном случае вывод не производится.</span><span class="sxs-lookup"><span data-stu-id="04edb-649">Otherwise no inferences are made.</span></span>

#### <a name="lower-bound-inferences"></a><span data-ttu-id="04edb-650">Нижняя граница выводы</span><span class="sxs-lookup"><span data-stu-id="04edb-650">Lower-bound inferences</span></span>

<span data-ttu-id="04edb-651">Объект *вывод по нижней границе* *из* типом `U` *для* типом `V` выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-651">A *lower-bound inference* *from* a type `U` *to* a type `V` is made as follows:</span></span>

*  <span data-ttu-id="04edb-652">Если `V` является одним из *нефиксированных* `Xi` затем `U` добавляется к набору нижней границы для `Xi`.</span><span class="sxs-lookup"><span data-stu-id="04edb-652">If `V` is one of the *unfixed* `Xi` then `U` is added to the set of lower bounds for `Xi`.</span></span>
*  <span data-ttu-id="04edb-653">В противном случае, если `V` — это тип `V1?`и `U` — это тип `U1?` то нижняя граница вывод выполняется из `U1` для `V1`.</span><span class="sxs-lookup"><span data-stu-id="04edb-653">Otherwise, if `V` is the type `V1?`and `U` is the type `U1?` then a lower bound inference is made from `U1` to `V1`.</span></span>
*  <span data-ttu-id="04edb-654">В противном случае задает `U1...Uk` и `V1...Vk` определяются путем проверки, если применим один из следующих случаев:</span><span class="sxs-lookup"><span data-stu-id="04edb-654">Otherwise, sets `U1...Uk` and `V1...Vk` are determined by checking if any of the following cases apply:</span></span>
   *  <span data-ttu-id="04edb-655">`V` является типом массива `V1[...]` и `U` является типом массива `U1[...]` (или эффективный базовый тип которого является параметром-типом `U1[...]`) одинакового ранга кортежам</span><span class="sxs-lookup"><span data-stu-id="04edb-655">`V` is an array type `V1[...]` and `U` is an array type `U1[...]` (or a type parameter whose effective base type is `U1[...]`) of the same rank</span></span>
   *  <span data-ttu-id="04edb-656">`V` является одним из `IEnumerable<V1>`, `ICollection<V1>` или `IList<V1>` и `U` является одномерным массивом `U1[]`(или эффективный базовый тип которого является параметром-типом `U1[]`)</span><span class="sxs-lookup"><span data-stu-id="04edb-656">`V` is one of `IEnumerable<V1>`, `ICollection<V1>` or `IList<V1>` and `U` is a one-dimensional array type `U1[]`(or a type parameter whose effective base type is `U1[]`)</span></span>
   *  <span data-ttu-id="04edb-657">`V` — сконструированный тип класса, структуры, интерфейса или делегата `C<V1...Vk>` и есть уникальный тип `C<U1...Uk>` таким образом, чтобы `U` (или, если `U` является параметром типа, его эффективным базовым классом или любым членом его эффективным набором интерфейса) — идентичен, наследует от (напрямую или косвенно), или реализует (напрямую или косвенно) `C<U1...Uk>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-657">`V` is a constructed class, struct, interface or delegate type `C<V1...Vk>` and there is a unique type `C<U1...Uk>` such that `U` (or, if `U` is a type parameter, its effective base class or any member of its effective interface set) is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) `C<U1...Uk>`.</span></span>

      <span data-ttu-id="04edb-658">(Ограничение «уникальности» означает, что в интерфейсе вариантов `C<T> {} class U: C<X>, C<Y> {}`, а затем сделать вывод, при выводе из `U` для `C<T>` поскольку `U1` может быть `X` или `Y`.)</span><span class="sxs-lookup"><span data-stu-id="04edb-658">(The "uniqueness" restriction means that in the case interface `C<T> {} class U: C<X>, C<Y> {}`, then no inference is made when inferring from `U` to `C<T>` because `U1` could be `X` or `Y`.)</span></span>

   <span data-ttu-id="04edb-659">Если какие-либо из этих случаев применимы, а затем выполняется вывод *из* каждого `Ui` *для* соответствующего `Vi` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-659">If any of these cases apply then an inference is made *from* each `Ui` *to* the corresponding `Vi` as follows:</span></span>

   *  <span data-ttu-id="04edb-660">Если `Ui` неизвестен быть ссылочным типом исключение *точное определение* выполняется</span><span class="sxs-lookup"><span data-stu-id="04edb-660">If `Ui` is not known to be a reference type then an *exact inference* is made</span></span>
   *  <span data-ttu-id="04edb-661">В противном случае, если `U` является типом массива то *вывод по нижней границе* выполняется</span><span class="sxs-lookup"><span data-stu-id="04edb-661">Otherwise, if `U` is an array type then a *lower-bound inference* is made</span></span>
   *  <span data-ttu-id="04edb-662">В противном случае, если `V` — `C<V1...Vk>` вывод зависит от параметра типа i й `C`:</span><span class="sxs-lookup"><span data-stu-id="04edb-662">Otherwise, if `V` is `C<V1...Vk>` then inference depends on the i-th type parameter of `C`:</span></span>
      *  <span data-ttu-id="04edb-663">Если он является ковариантным то *вывод по нижней границе* выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-663">If it is covariant then a *lower-bound inference* is made.</span></span>
      *  <span data-ttu-id="04edb-664">Если он является контравариантным, а затем *вывод по верхней границе* выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-664">If it is contravariant then an *upper-bound inference* is made.</span></span>
      *  <span data-ttu-id="04edb-665">Если он является инвариантным исключение *точное определение* выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-665">If it is invariant then an *exact inference* is made.</span></span>
*  <span data-ttu-id="04edb-666">В противном случае вывод не производится.</span><span class="sxs-lookup"><span data-stu-id="04edb-666">Otherwise, no inferences are made.</span></span>

#### <a name="upper-bound-inferences"></a><span data-ttu-id="04edb-667">Вывод верхней границы</span><span class="sxs-lookup"><span data-stu-id="04edb-667">Upper-bound inferences</span></span>

<span data-ttu-id="04edb-668">*Вывод по верхней границе* *из* типом `U` *для* типом `V` выполняется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-668">An *upper-bound inference* *from* a type `U` *to* a type `V` is made as follows:</span></span>

*  <span data-ttu-id="04edb-669">Если `V` является одним из *нефиксированных* `Xi` затем `U` добавляется к набору верхней границы для `Xi`.</span><span class="sxs-lookup"><span data-stu-id="04edb-669">If `V` is one of the *unfixed* `Xi` then `U` is added to the set of upper bounds for `Xi`.</span></span>
*  <span data-ttu-id="04edb-670">В противном случае задает `V1...Vk` и `U1...Uk` определяются путем проверки, если применим один из следующих случаев:</span><span class="sxs-lookup"><span data-stu-id="04edb-670">Otherwise, sets `V1...Vk` and `U1...Uk` are determined by checking if any of the following cases apply:</span></span>
   *  <span data-ttu-id="04edb-671">`U` является типом массива `U1[...]` и `V` является типом массива `V1[...]` одинакового ранга кортежам</span><span class="sxs-lookup"><span data-stu-id="04edb-671">`U` is an array type `U1[...]` and `V` is an array type `V1[...]` of the same rank</span></span>
   *  <span data-ttu-id="04edb-672">`U` является одним из `IEnumerable<Ue>`, `ICollection<Ue>` или `IList<Ue>` и `V` является одномерным массивом `Ve[]`</span><span class="sxs-lookup"><span data-stu-id="04edb-672">`U` is one of `IEnumerable<Ue>`, `ICollection<Ue>` or `IList<Ue>` and `V` is a one-dimensional array type `Ve[]`</span></span>
   *  <span data-ttu-id="04edb-673">`U` — Это тип `U1?` и `V` является типом `V1?`</span><span class="sxs-lookup"><span data-stu-id="04edb-673">`U` is the type `U1?` and `V` is the type `V1?`</span></span>
   *  <span data-ttu-id="04edb-674">`U` — сконструированный класс, структура, интерфейс или делегат типа `C<U1...Uk>` и `V` — это класс, структура, интерфейс или делегат тип, который идентичен, наследует от (напрямую или косвенно) или реализует (напрямую или косвенно) уникальный тип `C<V1...Vk>`</span><span class="sxs-lookup"><span data-stu-id="04edb-674">`U` is constructed class, struct, interface or delegate type `C<U1...Uk>` and `V` is a class, struct, interface or delegate type which is identical to, inherits from (directly or indirectly), or implements (directly or indirectly) a unique type `C<V1...Vk>`</span></span>

      <span data-ttu-id="04edb-675">(Ограничение «уникальности» означает, что если у нас есть `interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}`, а затем сделать вывод, при выводе из `C<U1>` для `V<Q>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-675">(The "uniqueness" restriction means that if we have `interface C<T>{} class V<Z>: C<X<Z>>, C<Y<Z>>{}`, then no inference is made when inferring from `C<U1>` to `V<Q>`.</span></span> <span data-ttu-id="04edb-676">Вывод не выполняется из `U1` либо `X<Q>` или `Y<Q>`.)</span><span class="sxs-lookup"><span data-stu-id="04edb-676">Inferences are not made from `U1` to either `X<Q>` or `Y<Q>`.)</span></span>

   <span data-ttu-id="04edb-677">Если какие-либо из этих случаев применимы, а затем выполняется вывод *из* каждого `Ui` *для* соответствующего `Vi` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-677">If any of these cases apply then an inference is made *from* each `Ui` *to* the corresponding `Vi` as follows:</span></span>
   *  <span data-ttu-id="04edb-678">Если `Ui` неизвестен быть ссылочным типом исключение *точное определение* выполняется</span><span class="sxs-lookup"><span data-stu-id="04edb-678">If  `Ui` is not known to be a reference type then an *exact inference* is made</span></span>
   *  <span data-ttu-id="04edb-679">В противном случае, если `V` является типом массива элемент *вывод по верхней границе* выполняется</span><span class="sxs-lookup"><span data-stu-id="04edb-679">Otherwise, if `V` is an array type then an *upper-bound inference* is made</span></span>
   *  <span data-ttu-id="04edb-680">В противном случае, если `U` — `C<U1...Uk>` вывод зависит от параметра типа i й `C`:</span><span class="sxs-lookup"><span data-stu-id="04edb-680">Otherwise, if `U` is `C<U1...Uk>` then inference depends on the i-th type parameter of `C`:</span></span>
      *  <span data-ttu-id="04edb-681">Если он является ковариантным типом *вывод по верхней границе* выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-681">If it is covariant then an *upper-bound inference* is made.</span></span>
      *  <span data-ttu-id="04edb-682">Если он является контравариантным, а затем *вывод по нижней границе* выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-682">If it is contravariant then a *lower-bound inference* is made.</span></span>
      *  <span data-ttu-id="04edb-683">Если он является инвариантным исключение *точное определение* выполняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-683">If it is invariant then an *exact inference* is made.</span></span>
*  <span data-ttu-id="04edb-684">В противном случае вывод не производится.</span><span class="sxs-lookup"><span data-stu-id="04edb-684">Otherwise, no inferences are made.</span></span>   

#### <a name="fixing"></a><span data-ttu-id="04edb-685">Исправления</span><span class="sxs-lookup"><span data-stu-id="04edb-685">Fixing</span></span>

<span data-ttu-id="04edb-686">*Нефиксированных* переменной типа `Xi` с набором границ — *фиксированной* следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-686">An *unfixed* type variable `Xi` with a set of bounds is *fixed* as follows:</span></span>

*  <span data-ttu-id="04edb-687">Набор *потенциальных типов* `Uj` начинается как набор всех типов в набор границ для `Xi`.</span><span class="sxs-lookup"><span data-stu-id="04edb-687">The set of *candidate types* `Uj` starts out as the set of all types in the set of bounds for `Xi`.</span></span>
*  <span data-ttu-id="04edb-688">После этого будут рассмотрены каждая граница для `Xi` в свою очередь: Для каждого точного границы `U` из `Xi` все типы `Uj` которого не идентичны `U` удаляются из набора кандидатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-688">We then examine each bound for `Xi` in turn: For each exact bound `U` of `Xi` all types `Uj` which are not identical to `U` are removed from the candidate set.</span></span> <span data-ttu-id="04edb-689">Для каждой нижней границы `U` из `Xi` все типы `Uj` которых является *не* неявное преобразование из `U` удаляются из набора кандидатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-689">For each lower bound `U` of `Xi` all types `Uj` to which there is *not* an implicit conversion from `U` are removed from the candidate set.</span></span> <span data-ttu-id="04edb-690">Для каждой верхней границы `U` из `Xi` все типы `Uj` из которых является *не* неявное преобразование в `U` удаляются из набора кандидатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-690">For each upper bound `U` of `Xi` all types `Uj` from which there is *not* an implicit conversion to `U` are removed from the candidate set.</span></span>
*  <span data-ttu-id="04edb-691">Если среди оставшихся типов-кандидатов `Uj` есть уникальный тип `V` из которой отсутствует неявное преобразование в все остальные типы-кандидаты, затем `Xi` Фиксированная `V`.</span><span class="sxs-lookup"><span data-stu-id="04edb-691">If among the remaining candidate types `Uj` there is a unique type `V` from which there is an implicit conversion to all the other candidate types, then `Xi` is fixed to `V`.</span></span>
*  <span data-ttu-id="04edb-692">В противном случае — не удается вывести тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-692">Otherwise, type inference fails.</span></span>

#### <a name="inferred-return-type"></a><span data-ttu-id="04edb-693">Выведенный тип возвращаемого значения</span><span class="sxs-lookup"><span data-stu-id="04edb-693">Inferred return type</span></span>

<span data-ttu-id="04edb-694">Выведенный тип возвращаемого значения анонимная функция `F` используется при разрешении типа вывода и перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-694">The inferred return type of an anonymous function `F` is used during type inference and overload resolution.</span></span> <span data-ttu-id="04edb-695">Выведенный тип возвращаемого значения можно определить только для анонимной функции, где все параметров, либо типы известны, так как они заданы явно, предоставляются через преобразование анонимной функции или определен во время вывода типа на во внешнем универсальный вызов метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-695">The inferred return type can only be determined for an anonymous function where all parameter types are known, either because they are explicitly given, provided through an anonymous function conversion or inferred during type inference on an enclosing generic method invocation.</span></span>

<span data-ttu-id="04edb-696">***Выведен тип результата*** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-696">The ***inferred result type*** is determined as follows:</span></span>

*  <span data-ttu-id="04edb-697">Если тело `F` — *выражение* с типом, то типом результата, выводимого `F` тип этого выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-697">If the body of `F` is an *expression* that has a type, then the inferred result type of `F` is the type of that expression.</span></span>
*  <span data-ttu-id="04edb-698">Если тело `F` — *блок* и набор выражений в блоке `return` инструкции с типом наиболее распространенных `T` ([поиск это наиболее распространенный тип набора выражений](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)), то типом результата, выводимого `F` является `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-698">If the body of `F` is a *block* and the set of expressions in the block's `return` statements has a best common type `T` ([Finding the best common type of a set of expressions](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)), then the inferred result type of `F` is `T`.</span></span>
*  <span data-ttu-id="04edb-699">В противном случае — тип результата не может быть определен для `F`.</span><span class="sxs-lookup"><span data-stu-id="04edb-699">Otherwise, a result type cannot be inferred for `F`.</span></span>

<span data-ttu-id="04edb-700">***Вывести тип возвращаемого значения*** определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-700">The ***inferred return type*** is determined as follows:</span></span>

*  <span data-ttu-id="04edb-701">Если `F` является асинхронной и текст `F` является либо выражение классифицировано как nothing ([классификации выражений](expressions.md#expression-classifications)), или блок операторов, где нет операторов return содержат выражения, выводимые возвращаемого типа `System.Threading.Tasks.Task`</span><span class="sxs-lookup"><span data-stu-id="04edb-701">If `F` is async and the body of `F` is either an expression classified as nothing ([Expression classifications](expressions.md#expression-classifications)), or a statement block where no return statements have expressions, the inferred return type is `System.Threading.Tasks.Task`</span></span>
*  <span data-ttu-id="04edb-702">Если `F` является асинхронной и имеет тип результата, выводимого `T`, выводимые возвращаемого типа `System.Threading.Tasks.Task<T>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-702">If `F` is async and has an inferred result type `T`, the inferred return type is `System.Threading.Tasks.Task<T>`.</span></span>
*  <span data-ttu-id="04edb-703">Если `F` синхронные и имеет тип результата, выводимого `T`, выводимые возвращаемого типа `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-703">If `F` is non-async and has an inferred result type `T`, the inferred return type is `T`.</span></span>
*  <span data-ttu-id="04edb-704">В противном случае тип возвращаемого значения не может быть определен для `F`.</span><span class="sxs-lookup"><span data-stu-id="04edb-704">Otherwise a return type cannot be inferred for `F`.</span></span>

<span data-ttu-id="04edb-705">В качестве примера вывода типа с анонимных функций, рассмотрим `Select` метод расширения, объявленный в `System.Linq.Enumerable` класса:</span><span class="sxs-lookup"><span data-stu-id="04edb-705">As an example of type inference involving anonymous functions, consider the `Select` extension method declared in the `System.Linq.Enumerable` class:</span></span>
```csharp
namespace System.Linq
{
    public static class Enumerable
    {
        public static IEnumerable<TResult> Select<TSource,TResult>(
            this IEnumerable<TSource> source,
            Func<TSource,TResult> selector)
        {
            foreach (TSource element in source) yield return selector(element);
        }
    }
}
```

<span data-ttu-id="04edb-706">При условии, что `System.Linq` пространство имен была импортирована с `using` предложение и имеется класс `Customer` с `Name` свойство типа `string`, `Select` метод может использоваться для выбора имен список клиентов:</span><span class="sxs-lookup"><span data-stu-id="04edb-706">Assuming the `System.Linq` namespace was imported with a `using` clause, and given a class `Customer` with a `Name` property of type `string`, the `Select` method can be used to select the names of a list of customers:</span></span>
```csharp
List<Customer> customers = GetCustomerList();
IEnumerable<string> names = customers.Select(c => c.Name);
```

<span data-ttu-id="04edb-707">Вызов метода расширения ([вызовы методов расширения](expressions.md#extension-method-invocations)) из `Select` обрабатывается, переписав вызова для вызова статического метода:</span><span class="sxs-lookup"><span data-stu-id="04edb-707">The extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)) of `Select` is processed by rewriting the invocation to a static method invocation:</span></span>
```csharp
IEnumerable<string> names = Enumerable.Select(customers, c => c.Name);
```

<span data-ttu-id="04edb-708">Так как аргументы типа не указаны явным образом, вывод типа позволяет определить аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-708">Since type arguments were not explicitly specified, type inference is used to infer the type arguments.</span></span> <span data-ttu-id="04edb-709">Во-первых, `customers` аргумент относится к `source` параметра, вывод типа `T` быть `Customer`.</span><span class="sxs-lookup"><span data-stu-id="04edb-709">First, the `customers` argument is related to the `source` parameter, inferring `T` to be `Customer`.</span></span> <span data-ttu-id="04edb-710">С помощью анонимной функции введите вывод процесс, описанный выше, `c` присваивается тип `Customer`и выражение `c.Name` связана с типом возвращаемого значения `selector` параметра, вывод типа `S` быть `string`.</span><span class="sxs-lookup"><span data-stu-id="04edb-710">Then, using the anonymous function type inference process described above, `c` is given type `Customer`, and the expression `c.Name` is related to the return type of the `selector` parameter, inferring `S` to be `string`.</span></span> <span data-ttu-id="04edb-711">Таким образом вызов эквивалентен</span><span class="sxs-lookup"><span data-stu-id="04edb-711">Thus, the invocation is equivalent to</span></span>
```csharp
Sequence.Select<Customer,string>(customers, (Customer c) => c.Name)
```
<span data-ttu-id="04edb-712">и результат имеет тип `IEnumerable<string>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-712">and the result is of type `IEnumerable<string>`.</span></span>

<span data-ttu-id="04edb-713">В следующем примере показано, как анонимный тип функции вывода позволяет информацию о типе для «поток» между аргументами в вызове универсального метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-713">The following example demonstrates how anonymous function type inference allows type information to "flow" between arguments in a generic method invocation.</span></span> <span data-ttu-id="04edb-714">Если метод:</span><span class="sxs-lookup"><span data-stu-id="04edb-714">Given the method:</span></span>
```csharp
static Z F<X,Y,Z>(X value, Func<X,Y> f1, Func<Y,Z> f2) {
    return f2(f1(value));
}
```

<span data-ttu-id="04edb-715">Определение типа для вызова:</span><span class="sxs-lookup"><span data-stu-id="04edb-715">Type inference for the invocation:</span></span>
```csharp
double seconds = F("1:15:30", s => TimeSpan.Parse(s), t => t.TotalSeconds);
```
<span data-ttu-id="04edb-716">продолжается следующим образом. Во-первых, аргумент `"1:15:30"` связана с `value` параметра, вывод типа `X` быть `string`.</span><span class="sxs-lookup"><span data-stu-id="04edb-716">proceeds as follows: First, the argument `"1:15:30"` is related to the `value` parameter, inferring `X` to be `string`.</span></span> <span data-ttu-id="04edb-717">Затем, параметр первого анонимной функции, `s`, предоставляется выведенный тип `string`и выражение `TimeSpan.Parse(s)` связана с типом возвращаемого значения `f1`, выведения `Y` быть `System.TimeSpan`.</span><span class="sxs-lookup"><span data-stu-id="04edb-717">Then, the parameter of the first anonymous function, `s`, is given the inferred type `string`, and the expression `TimeSpan.Parse(s)` is related to the return type of `f1`, inferring `Y` to be `System.TimeSpan`.</span></span> <span data-ttu-id="04edb-718">Наконец, параметр второй анонимной функции, `t`, предоставляется выведенный тип `System.TimeSpan`и выражение `t.TotalSeconds` связана с типом возвращаемого значения `f2`, выведения `Z` быть `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-718">Finally, the parameter of the second anonymous function, `t`, is given the inferred type `System.TimeSpan`, and the expression `t.TotalSeconds` is related to the return type of `f2`, inferring `Z` to be `double`.</span></span> <span data-ttu-id="04edb-719">Таким образом, результат вызова имеет тип `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-719">Thus, the result of the invocation is of type `double`.</span></span>

#### <a name="type-inference-for-conversion-of-method-groups"></a><span data-ttu-id="04edb-720">Определение типа для преобразования групп методов</span><span class="sxs-lookup"><span data-stu-id="04edb-720">Type inference for conversion of method groups</span></span>

<span data-ttu-id="04edb-721">Как и вызовы универсальных методов, вывод типа также должен применяться при группу методов `M` содержащий универсальный метод, преобразуется в данный тип делегата `D` ([преобразования групп методов](conversions.md#method-group-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-721">Similar to calls of generic methods, type inference must also be applied when a method group `M` containing a generic method is converted to a given delegate type `D` ([Method group conversions](conversions.md#method-group-conversions)).</span></span> <span data-ttu-id="04edb-722">Данного метода</span><span class="sxs-lookup"><span data-stu-id="04edb-722">Given a method</span></span>
```csharp
Tr M<X1...Xn>(T1 x1 ... Tm xm)
```
<span data-ttu-id="04edb-723">и группа методов `M` присваивается тип делегата `D` задачей вывода типа является поиск аргументов типа `S1...Sn` таким образом, выражение:</span><span class="sxs-lookup"><span data-stu-id="04edb-723">and the method group `M` being assigned to the delegate type `D` the task of type inference is to find type arguments `S1...Sn` so that the expression:</span></span>
```csharp
M<S1...Sn>
```
<span data-ttu-id="04edb-724">становится совместимый ([объявления делегатов](delegates.md#delegate-declarations)) с `D`.</span><span class="sxs-lookup"><span data-stu-id="04edb-724">becomes compatible ([Delegate declarations](delegates.md#delegate-declarations)) with `D`.</span></span>

<span data-ttu-id="04edb-725">В отличие от алгоритма вывода для вызовов универсального метода, в этом случае существует только аргумент *типы*, аргумент *выражения*.</span><span class="sxs-lookup"><span data-stu-id="04edb-725">Unlike the type inference algorithm for generic method calls, in this case there are only argument *types*, no argument *expressions*.</span></span> <span data-ttu-id="04edb-726">В частности, нет анонимных функций и тем самым устраняет потребность в нескольких этапах вывода.</span><span class="sxs-lookup"><span data-stu-id="04edb-726">In particular, there are no anonymous functions and hence no need for multiple phases of inference.</span></span>

<span data-ttu-id="04edb-727">Вместо этого все `Xi` считаются *нефиксированных*и *вывод по нижней границе* становится *из* тип каждого аргумента `Uj` из `D` *для* соответствующего типа параметра `Tj` из `M`.</span><span class="sxs-lookup"><span data-stu-id="04edb-727">Instead, all `Xi` are considered *unfixed*, and a *lower-bound inference* is made *from* each argument type `Uj` of `D` *to* the corresponding parameter type `Tj` of `M`.</span></span> <span data-ttu-id="04edb-728">Если для любого из `Xi` границы не найдены, не удается вывести тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-728">If for any of the `Xi` no bounds were found, type inference fails.</span></span> <span data-ttu-id="04edb-729">В противном случае все `Xi` являются *фиксированной* соответствующий `Si`, которой получены в результате вывода типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-729">Otherwise, all `Xi` are *fixed* to corresponding `Si`, which are the result of type inference.</span></span>

#### <a name="finding-the-best-common-type-of-a-set-of-expressions"></a><span data-ttu-id="04edb-730">Это наиболее распространенный тип набора выражений, поиск</span><span class="sxs-lookup"><span data-stu-id="04edb-730">Finding the best common type of a set of expressions</span></span>

<span data-ttu-id="04edb-731">В некоторых случаях тип необходимо вывести для набора выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-731">In some cases, a common type needs to be inferred for a set of expressions.</span></span> <span data-ttu-id="04edb-732">В частности, типы элементов этих неявно типизированные массивы и типы возвращаемого значения анонимных функций с *блок* тел находятся таким образом.</span><span class="sxs-lookup"><span data-stu-id="04edb-732">In particular, the element types of implicitly typed arrays and the return types of anonymous functions with *block* bodies are found in this way.</span></span>

<span data-ttu-id="04edb-733">Интуитивно, исходя из набора выражений `E1...Em` этот вывод должен быть эквивалентен вызову метода</span><span class="sxs-lookup"><span data-stu-id="04edb-733">Intuitively, given a set of expressions `E1...Em` this inference should be equivalent to calling a method</span></span>
```csharp
Tr M<X>(X x1 ... X xm)
```
<span data-ttu-id="04edb-734">с помощью `Ei` как аргументы.</span><span class="sxs-lookup"><span data-stu-id="04edb-734">with the `Ei` as arguments.</span></span>

<span data-ttu-id="04edb-735">Точнее, вывод начинается с *нефиксированных* переменной типа `X`.</span><span class="sxs-lookup"><span data-stu-id="04edb-735">More precisely, the inference starts out with an *unfixed* type variable `X`.</span></span> <span data-ttu-id="04edb-736">*Вывод типа вывода* становятся *из* каждого `Ei` *для* `X`.</span><span class="sxs-lookup"><span data-stu-id="04edb-736">*Output type inferences* are then made *from* each `Ei` *to* `X`.</span></span> <span data-ttu-id="04edb-737">Наконец `X` является *фиксированной* и в случае успеха, полученный в результате введите `S` является итоговый наиболее распространенным типом для выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-737">Finally, `X` is *fixed* and, if successful, the resulting type `S` is the resulting best common type for the expressions.</span></span> <span data-ttu-id="04edb-738">Если нет такого `S` существует, выражения содержат наиболее общий тип отсутствует.</span><span class="sxs-lookup"><span data-stu-id="04edb-738">If no such `S` exists, the expressions have no best common type.</span></span>

### <a name="overload-resolution"></a><span data-ttu-id="04edb-739">Разрешение перегрузки</span><span class="sxs-lookup"><span data-stu-id="04edb-739">Overload resolution</span></span>

<span data-ttu-id="04edb-740">Разрешение перегрузки — это механизм времени привязки для выбора наилучший член функции для вызова при наличии списка аргументов и набора потенциальных членов функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-740">Overload resolution is a binding-time mechanism for selecting the best function member to invoke given an argument list and a set of candidate function members.</span></span> <span data-ttu-id="04edb-741">Разрешение перегрузки выбирает функцию-член для вызова в следующих отдельных контекстах в C#:</span><span class="sxs-lookup"><span data-stu-id="04edb-741">Overload resolution selects the function member to invoke in the following distinct contexts within C#:</span></span>

*  <span data-ttu-id="04edb-742">Вызов метода с именем в *invocation_expression* ([вызовы методов](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-742">Invocation of a method named in an *invocation_expression* ([Method invocations](expressions.md#method-invocations)).</span></span>
*  <span data-ttu-id="04edb-743">Вызов конструктора экземпляра с именем в *object_creation_expression* ([выражения создания объектов](expressions.md#object-creation-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-743">Invocation of an instance constructor named in an *object_creation_expression* ([Object creation expressions](expressions.md#object-creation-expressions)).</span></span>
*  <span data-ttu-id="04edb-744">Вызов метода доступа индексатора через *element_access* ([доступ к элементам](expressions.md#element-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-744">Invocation of an indexer accessor through an *element_access* ([Element access](expressions.md#element-access)).</span></span>
*  <span data-ttu-id="04edb-745">Вызов оператора предопределенные или определяемые пользователем, на которые ссылается выражение ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution) и [разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="04edb-745">Invocation of a predefined or user-defined operator referenced in an expression ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution) and [Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)).</span></span>

<span data-ttu-id="04edb-746">Каждый из этих контекстов определяет набор потенциальных членов функции и список аргументов в своим уникальным способом, как подробно описывается в разделах, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="04edb-746">Each of these contexts defines the set of candidate function members and the list of arguments in its own unique way, as described in detail in the sections listed above.</span></span> <span data-ttu-id="04edb-747">Например, набор кандидатов для вызова метода не включает методы, помеченные `override` ([поиск члена](expressions.md#member-lookup)), и методов в базовом классе не являются кандидатами, если применимо любой метод в производном классе ([ Вызовы методов](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-747">For example, the set of candidates for a method invocation does not include methods marked `override` ([Member lookup](expressions.md#member-lookup)), and methods in a base class are not candidates if any method in a derived class is applicable ([Method invocations](expressions.md#method-invocations)).</span></span>

<span data-ttu-id="04edb-748">После определения потенциальных членов функции и список аргументов выбора наилучшего члена функции одинаков во всех случаях:</span><span class="sxs-lookup"><span data-stu-id="04edb-748">Once the candidate function members and the argument list have been identified, the selection of the best function member is the same in all cases:</span></span>

*  <span data-ttu-id="04edb-749">Имея набор применимых потенциальных членов функции, лучшие функции-члена в том, что находится набор.</span><span class="sxs-lookup"><span data-stu-id="04edb-749">Given the set of applicable candidate function members, the best function member in that set is located.</span></span> <span data-ttu-id="04edb-750">Если набор содержит только одну функцию-член, функция-член является наилучшим членом функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-750">If the set contains only one function member, then that function member is the best function member.</span></span> <span data-ttu-id="04edb-751">В противном случае наилучшим членом функции является функция-член, который лучше, чем все другие функции-члены по отношению к списку аргументов при условии, что каждый член функции сравнивается со всех других функций-членов с помощью правил в [ Наилучший член функции](expressions.md#better-function-member).</span><span class="sxs-lookup"><span data-stu-id="04edb-751">Otherwise, the best function member is the one function member that is better than all other function members with respect to the given argument list, provided that each function member is compared to all other function members using the rules in [Better function member](expressions.md#better-function-member).</span></span> <span data-ttu-id="04edb-752">Если отсутствия ровно одну функцию-член, который лучше, чем все другие функции-члены, то вызов функции-члена является неоднозначным и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-752">If there is not exactly one function member that is better than all other function members, then the function member invocation is ambiguous and a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-753">В следующих разделах описывается значение условия ***применимого члена функции*** и ***наилучший член функции***.</span><span class="sxs-lookup"><span data-stu-id="04edb-753">The following sections define the exact meanings of the terms ***applicable function member*** and ***better function member***.</span></span>

#### <a name="applicable-function-member"></a><span data-ttu-id="04edb-754">Применимый член функции</span><span class="sxs-lookup"><span data-stu-id="04edb-754">Applicable function member</span></span>

<span data-ttu-id="04edb-755">Функция-член считается ***применимого члена функции*** по отношению к список аргументов `A` если выполняются все следующие условия:</span><span class="sxs-lookup"><span data-stu-id="04edb-755">A function member is said to be an ***applicable function member*** with respect to an argument list `A` when all of the following are true:</span></span>

*  <span data-ttu-id="04edb-756">Каждый аргумент в `A` соответствует параметру в объявлении функции-члена, как описано в разделе [параметры соответствующий](expressions.md#corresponding-parameters), и любой параметр, которому соответствует аргумент является необязательным параметром.</span><span class="sxs-lookup"><span data-stu-id="04edb-756">Each argument in `A` corresponds to a parameter in the function member declaration as described in [Corresponding parameters](expressions.md#corresponding-parameters), and any parameter to which no argument corresponds is an optional parameter.</span></span>
*  <span data-ttu-id="04edb-757">Для каждого аргумента в `A`, передача режим для аргумента параметров (т. е. значение `ref`, или `out`) идентичен режиму передачи параметра для соответствующего параметра, и</span><span class="sxs-lookup"><span data-stu-id="04edb-757">For each argument in `A`, the parameter passing mode of the argument (i.e., value, `ref`, or `out`) is identical to the parameter passing mode of the corresponding parameter, and</span></span>
   *  <span data-ttu-id="04edb-758">для параметра значение или массив параметров, неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) существует аргумент к типу соответствующего параметра, или</span><span class="sxs-lookup"><span data-stu-id="04edb-758">for a value parameter or a parameter array, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from the argument to the type of the corresponding parameter, or</span></span>
   *  <span data-ttu-id="04edb-759">для `ref` или `out` параметра, тип аргумента отличается от типа соответствующего параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-759">for a `ref` or `out` parameter, the type of the argument is identical to the type of the corresponding parameter.</span></span> <span data-ttu-id="04edb-760">В конце концов `ref` или `out` является псевдонимом для передаваемых аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-760">After all, a `ref` or `out` parameter is an alias for the argument passed.</span></span>

<span data-ttu-id="04edb-761">Для функции-члена, который включает массив параметров если применимо, приведенных выше правил функцию-член, он считается применимо в его ***обычной формой***.</span><span class="sxs-lookup"><span data-stu-id="04edb-761">For a function member that includes a parameter array, if the function member is applicable by the above rules, it is said to be applicable in its ***normal form***.</span></span> <span data-ttu-id="04edb-762">Если функция-член, которая включает массив параметров не применим в нормальной форме, функцию-член может быть применима в его ***расширенной форме***:</span><span class="sxs-lookup"><span data-stu-id="04edb-762">If a function member that includes a parameter array is not applicable in its normal form, the function member may instead be applicable in its ***expanded form***:</span></span>

*  <span data-ttu-id="04edb-763">Расширенная форма создается путем замены массива параметров в объявлении функции-члена с нуля или больше параметров значение параметра типа элемента массива, например, число аргументов в списке аргументов `A` соответствует итог число параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-763">The expanded form is constructed by replacing the parameter array in the function member declaration with zero or more value parameters of the element type of the parameter array such that the number of arguments in the argument list `A` matches the total number of parameters.</span></span> <span data-ttu-id="04edb-764">Если `A` меньшее число аргументов, чем число основных параметров в объявлении функции-члена, расширенную форму функцию-член не может быть создан и таким образом не применяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-764">If `A` has fewer arguments than the number of fixed parameters in the function member declaration, the expanded form of the function member cannot be constructed and is thus not applicable.</span></span>
*  <span data-ttu-id="04edb-765">В противном случае — расширенная форма применимо, если для каждого аргумента в `A` режим передачи параметра аргумента идентичен режиму передачи параметра для соответствующего параметра, и</span><span class="sxs-lookup"><span data-stu-id="04edb-765">Otherwise, the expanded form is applicable if for each argument in `A` the parameter passing mode of the argument is identical to the parameter passing mode of the corresponding parameter, and</span></span>
   *  <span data-ttu-id="04edb-766">для параметра фиксированное значение или значение параметра, созданного при расширении, неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) существует из типа аргумента в тип соответствующего параметра, или</span><span class="sxs-lookup"><span data-stu-id="04edb-766">for a fixed value parameter or a value parameter created by the expansion, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from the type of the argument to the type of the corresponding parameter, or</span></span>
   *  <span data-ttu-id="04edb-767">для `ref` или `out` параметра, тип аргумента отличается от типа соответствующего параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-767">for a `ref` or `out` parameter, the type of the argument is identical to the type of the corresponding parameter.</span></span>

#### <a name="better-function-member"></a><span data-ttu-id="04edb-768">Наилучший член функции</span><span class="sxs-lookup"><span data-stu-id="04edb-768">Better function member</span></span>

<span data-ttu-id="04edb-769">В целях определения наилучшего члена функции список урезанная аргументов типа создается содержащий только сами выражения аргументов в порядке их следования в исходном списке аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-769">For the purposes of determining the better function member, a stripped-down argument list A is constructed containing just the argument expressions themselves in the order they appear in the original argument list.</span></span>

<span data-ttu-id="04edb-770">Списки параметров для каждого кандидата функции-члена формируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-770">Parameter lists for each of the candidate function members are constructed in the following way:</span></span>

*  <span data-ttu-id="04edb-771">Расширенная форма используется в том случае, если функция-член была применимо только в расширенной форме.</span><span class="sxs-lookup"><span data-stu-id="04edb-771">The expanded form is used if the function member was applicable only in the expanded form.</span></span>
*  <span data-ttu-id="04edb-772">Необязательные параметры без соответствующих аргументов удаляются из списка параметров</span><span class="sxs-lookup"><span data-stu-id="04edb-772">Optional parameters with no corresponding arguments are removed from the parameter list</span></span>
*  <span data-ttu-id="04edb-773">Параметры переупорядочиваются, чтобы они встречаются в той же позиции, что соответствующий аргумент в списке аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-773">The parameters are reordered so that they occur at the same position as the corresponding argument in the argument list.</span></span>

<span data-ttu-id="04edb-774">Получает список аргументов `A` с набором выражений аргумента `{E1, E2, ..., En}` и два применимых члена функции `Mp` и `Mq` с типами параметров `{P1, P2, ..., Pn}` и `{Q1, Q2, ..., Qn}`, `Mp` определяется как ***наилучший член функции*** чем `Mq` Если</span><span class="sxs-lookup"><span data-stu-id="04edb-774">Given an argument list `A` with a set of argument expressions `{E1, E2, ..., En}` and two applicable function members `Mp` and `Mq` with parameter types `{P1, P2, ..., Pn}` and `{Q1, Q2, ..., Qn}`, `Mp` is defined to be a ***better function member*** than `Mq` if</span></span>

*  <span data-ttu-id="04edb-775">для каждого аргумента неявное преобразование из `Ex` для `Qx` не лучше, чем неявное преобразование из `Ex` для `Px`, и</span><span class="sxs-lookup"><span data-stu-id="04edb-775">for each argument, the implicit conversion from `Ex` to `Qx` is not better than the implicit conversion from `Ex` to `Px`, and</span></span>
*  <span data-ttu-id="04edb-776">для по крайней мере один аргумент, преобразование из `Ex` для `Px` лучше, чем преобразование из `Ex` для `Qx`.</span><span class="sxs-lookup"><span data-stu-id="04edb-776">for at least one argument, the conversion from `Ex` to `Px` is better than the conversion from `Ex` to `Qx`.</span></span>

<span data-ttu-id="04edb-777">При проведении этой оценки, в том случае, если `Mp` или `Mq` применима в расширенной форме, затем `Px` или `Qx` ссылается на параметр в расширенной форме списка параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-777">When performing this evaluation, if `Mp` or `Mq` is applicable in its expanded form, then `Px` or `Qx` refers to a parameter in the expanded form of the parameter list.</span></span>

<span data-ttu-id="04edb-778">В случае, если параметр типа последовательности `{P1, P2, ..., Pn}` и `{Q1, Q2, ..., Qn}` эквивалентны (т. е. каждый `Pi` имеет преобразование удостоверения в соответствующий `Qi`), применяются следующие правила разрешения ничьих, в порядке, чтобы определить, тем лучше функция-член.</span><span class="sxs-lookup"><span data-stu-id="04edb-778">In case the parameter type sequences `{P1, P2, ..., Pn}` and `{Q1, Q2, ..., Qn}` are equivalent (i.e. each `Pi` has an identity conversion to the corresponding `Qi`), the following tie-breaking rules are applied, in order, to determine the better function member.</span></span>

*  <span data-ttu-id="04edb-779">Если `Mp` — это метод, не являющегося универсальным и `Mq` является универсальным методом, затем `Mp` лучше, чем `Mq`.</span><span class="sxs-lookup"><span data-stu-id="04edb-779">If `Mp` is a non-generic method and `Mq` is a generic method, then `Mp` is better than `Mq`.</span></span>
*  <span data-ttu-id="04edb-780">В противном случае, если `Mp` применима в нормальной форме и `Mq` имеет `params` массива и применяется только в расширенной форме, затем `Mp` лучше, чем `Mq`.</span><span class="sxs-lookup"><span data-stu-id="04edb-780">Otherwise, if `Mp` is applicable in its normal form and `Mq` has a `params` array and is applicable only in its expanded form, then `Mp` is better than `Mq`.</span></span>
*  <span data-ttu-id="04edb-781">В противном случае, если `Mp` объявил ли несколько параметров, чем `Mq`, затем `Mp` лучше, чем `Mq`.</span><span class="sxs-lookup"><span data-stu-id="04edb-781">Otherwise, if `Mp` has more declared parameters than `Mq`, then `Mp` is better than `Mq`.</span></span> <span data-ttu-id="04edb-782">Это может произойти, если оба метода имеют `params` массивов того на них применимо только в расширенных формах.</span><span class="sxs-lookup"><span data-stu-id="04edb-782">This can occur if both methods have `params` arrays and are applicable only in their expanded forms.</span></span>
*  <span data-ttu-id="04edb-783">В противном случае если все параметры `Mp` есть соответствующий аргумент, тогда как аргументы по умолчанию должны быть заменены для по крайней мере один необязательный параметр в `Mq` затем `Mp` лучше, чем `Mq`.</span><span class="sxs-lookup"><span data-stu-id="04edb-783">Otherwise if all parameters of `Mp` have a corresponding argument whereas default arguments need to be substituted for at least one optional parameter in `Mq` then `Mp` is better than `Mq`.</span></span>
*  <span data-ttu-id="04edb-784">В противном случае, если `Mp` имеет более конкретные типы параметров, чем `Mq`, затем `Mp` лучше, чем `Mq`.</span><span class="sxs-lookup"><span data-stu-id="04edb-784">Otherwise, if `Mp` has more specific parameter types than `Mq`, then `Mp` is better than `Mq`.</span></span> <span data-ttu-id="04edb-785">Позвольте `{R1, R2, ..., Rn}` и `{S1, S2, ..., Sn}` представляют типы параметров, у которого отсутствуют экземпляры и нерасширенных `Mp` и `Mq`.</span><span class="sxs-lookup"><span data-stu-id="04edb-785">Let `{R1, R2, ..., Rn}` and `{S1, S2, ..., Sn}` represent the uninstantiated and unexpanded parameter types of `Mp` and `Mq`.</span></span> <span data-ttu-id="04edb-786">`Mp`в типы параметров: более специфичен, чем `Mq`Если для каждого параметра `Rx` не менее точно, чем `Sx`и по крайней мере один параметр `Rx` более специфичен, чем `Sx`:</span><span class="sxs-lookup"><span data-stu-id="04edb-786">`Mp`'s parameter types are more specific than `Mq`'s if, for each parameter, `Rx` is not less specific than `Sx`, and, for at least one parameter, `Rx` is more specific than `Sx`:</span></span>
   *  <span data-ttu-id="04edb-787">Параметр типа является менее точно, чем не являющегося типом параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-787">A type parameter is less specific than a non-type parameter.</span></span>
   *  <span data-ttu-id="04edb-788">Рекурсивно, сконструированный тип является более точным, чем другой сконструированный тип (с одинаковым числом аргументов типа) Если хотя бы один аргумент типа является более точным и менее точно, чем соответствующий аргумент типа в другой аргумент типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-788">Recursively, a constructed type is more specific than another constructed type (with the same number of type arguments) if at least one type argument is more specific and no type argument is less specific than the corresponding type argument in the other.</span></span>
   *  <span data-ttu-id="04edb-789">Тип массива указывается более специфичен, чем другой тип массива (с таким же числом измерений), если точнее, чем тип элементов второй тип первого элемента.</span><span class="sxs-lookup"><span data-stu-id="04edb-789">An array type is more specific than another array type (with the same number of dimensions) if the element type of the first is more specific than the element type of the second.</span></span>
*  <span data-ttu-id="04edb-790">В противном случае если один член — это оператор не удален, а другой — то оператор, лучше один не удален.</span><span class="sxs-lookup"><span data-stu-id="04edb-790">Otherwise if one member is a non-lifted operator and  the other is a lifted operator, the non-lifted one is better.</span></span>
*  <span data-ttu-id="04edb-791">В противном случае лучше подходящую функцию-член.</span><span class="sxs-lookup"><span data-stu-id="04edb-791">Otherwise, neither function member is better.</span></span>

#### <a name="better-conversion-from-expression"></a><span data-ttu-id="04edb-792">Лучшее преобразование из выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-792">Better conversion from expression</span></span>

<span data-ttu-id="04edb-793">Неявного преобразования `C1` , преобразующий из выражения `E` к типу `T1`и неявное преобразование `C2` , преобразующий из выражения `E` к типу `T2`, `C1` — ***лучше преобразования*** чем `C2` Если `E` полностью соответствует `T2` и содержит по крайней мере одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-793">Given an implicit conversion `C1` that converts from an expression `E` to a type `T1`, and an implicit conversion `C2` that converts from an expression `E` to a type `T2`, `C1` is a ***better conversion*** than `C2` if `E` does not exactly match `T2` and at least one of the following holds:</span></span>

* <span data-ttu-id="04edb-794">`E` точно соответствует `T1` ([точно выражении](expressions.md#exactly-matching-expression))</span><span class="sxs-lookup"><span data-stu-id="04edb-794">`E` exactly matches `T1` ([Exactly matching Expression](expressions.md#exactly-matching-expression))</span></span>
* <span data-ttu-id="04edb-795">`T1` является целью преобразования, лучше, чем `T2` ([подходящей целью преобразования](expressions.md#better-conversion-target))</span><span class="sxs-lookup"><span data-stu-id="04edb-795">`T1` is a better conversion target than `T2` ([Better conversion target](expressions.md#better-conversion-target))</span></span>

#### <a name="exactly-matching-expression"></a><span data-ttu-id="04edb-796">Точно соответствующее выражение</span><span class="sxs-lookup"><span data-stu-id="04edb-796">Exactly matching Expression</span></span>

<span data-ttu-id="04edb-797">Если выражение `E` и типом `T`, `E` точности соответствует `T` Если справедливо одно из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="04edb-797">Given an expression `E` and a type `T`, `E` exactly matches `T` if one of the following holds:</span></span>

*  <span data-ttu-id="04edb-798">`E` имеет тип `S`, и существует преобразование удостоверения из `S` для `T`</span><span class="sxs-lookup"><span data-stu-id="04edb-798">`E` has a type `S`, and an identity conversion exists from `S` to `T`</span></span>
*  <span data-ttu-id="04edb-799">`E` представляет собой анонимную функцию, `T` является типом делегата `D` или тип дерева выражения `Expression<D>` и содержит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-799">`E` is an anonymous function, `T` is either a delegate type `D` or an expression tree type `Expression<D>` and one of the following holds:</span></span>
   *  <span data-ttu-id="04edb-800">Выведенный тип возвращаемого значения `X` существует для `E` в контексте в список параметров `D` ([выводимого возвращаемый тип](expressions.md#inferred-return-type)), и существует преобразование удостоверения из `X` в тип возвращаемого значения `D`</span><span class="sxs-lookup"><span data-stu-id="04edb-800">An inferred return type `X` exists for `E` in the context of the parameter list of `D` ([Inferred return type](expressions.md#inferred-return-type)), and an identity conversion exists from `X` to the return type of `D`</span></span>
   *  <span data-ttu-id="04edb-801">Либо `E` является синхронные и `D` с типом возврата `Y` или `E` является асинхронной и `D` с типом возврата `Task<Y>`, и содержит одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-801">Either `E` is non-async and `D` has a return type `Y` or `E` is async and `D` has a return type `Task<Y>`, and one of the following holds:</span></span>
      * <span data-ttu-id="04edb-802">Тело `E` представляет собой выражение, в точности соответствующего `Y`</span><span class="sxs-lookup"><span data-stu-id="04edb-802">The body of `E` is an expression that exactly matches `Y`</span></span>
      * <span data-ttu-id="04edb-803">Тело `E` — это блок операторов, где каждый оператор return Возвращает выражение, в точности соответствующего `Y`</span><span class="sxs-lookup"><span data-stu-id="04edb-803">The body of `E` is a statement block where every return statement returns an expression that exactly matches `Y`</span></span>

#### <a name="better-conversion-target"></a><span data-ttu-id="04edb-804">Лучшая цель для преобразования</span><span class="sxs-lookup"><span data-stu-id="04edb-804">Better conversion target</span></span>

<span data-ttu-id="04edb-805">Учитывая два разных типа `T1` и `T2`, `T1` является целью преобразования, лучше, чем `T2` Если неявное преобразование из `T2` для `T1` существует, и содержит по крайней мере одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-805">Given two different types `T1` and `T2`, `T1` is a better conversion target than `T2` if no implicit conversion from `T2` to `T1` exists, and at least one of the following holds:</span></span>

*  <span data-ttu-id="04edb-806">Неявное преобразование из `T1` для `T2` существует</span><span class="sxs-lookup"><span data-stu-id="04edb-806">An implicit conversion from `T1` to `T2` exists</span></span>
*  <span data-ttu-id="04edb-807">`T1` является типом делегата `D1` или тип дерева выражения `Expression<D1>`, `T2` является типом делегата `D2` или тип дерева выражения `Expression<D2>`, `D1` с типом возврата `S1` и одну из содержит следующие:</span><span class="sxs-lookup"><span data-stu-id="04edb-807">`T1` is either a delegate type `D1` or an expression tree type `Expression<D1>`, `T2` is either a delegate type `D2` or an expression tree type `Expression<D2>`, `D1` has a return type `S1` and one of the following holds:</span></span>
   * <span data-ttu-id="04edb-808">`D2` Возвращает ли void</span><span class="sxs-lookup"><span data-stu-id="04edb-808">`D2` is void returning</span></span>
   * <span data-ttu-id="04edb-809">`D2` имеет тип возвращаемого значения `S2`, и `S1` является целью преобразования, лучше, чем `S2`</span><span class="sxs-lookup"><span data-stu-id="04edb-809">`D2` has a return type `S2`, and `S1` is a better conversion target than `S2`</span></span>
*  <span data-ttu-id="04edb-810">`T1` — `Task<S1>`, `T2` — `Task<S2>`, и `S1` является целью преобразования, лучше, чем `S2`</span><span class="sxs-lookup"><span data-stu-id="04edb-810">`T1` is `Task<S1>`, `T2` is `Task<S2>`, and `S1` is a better conversion target than `S2`</span></span>
*  <span data-ttu-id="04edb-811">`T1` — `S1` или `S1?` где `S1` является целочисленным типом со знаком, и `T2` — `S2` или `S2?` где `S2` является целочисленным типом без знака.</span><span class="sxs-lookup"><span data-stu-id="04edb-811">`T1` is `S1` or `S1?` where `S1` is a signed integral type, and `T2` is `S2` or `S2?` where `S2` is an unsigned integral type.</span></span> <span data-ttu-id="04edb-812">В частности:</span><span class="sxs-lookup"><span data-stu-id="04edb-812">Specifically:</span></span>
   * <span data-ttu-id="04edb-813">`S1` — `sbyte` и `S2` — `byte`, `ushort`, `uint`, или `ulong`</span><span class="sxs-lookup"><span data-stu-id="04edb-813">`S1` is `sbyte` and `S2` is `byte`, `ushort`, `uint`, or `ulong`</span></span>
   * <span data-ttu-id="04edb-814">`S1` — `short` и `S2` — `ushort`, `uint`, или `ulong`</span><span class="sxs-lookup"><span data-stu-id="04edb-814">`S1` is `short` and `S2` is `ushort`, `uint`, or `ulong`</span></span>
   * <span data-ttu-id="04edb-815">`S1` — `int` и `S2` является `uint`, или `ulong`</span><span class="sxs-lookup"><span data-stu-id="04edb-815">`S1` is `int` and `S2` is `uint`, or `ulong`</span></span>
   * <span data-ttu-id="04edb-816">`S1` — `long` и `S2` — `ulong`</span><span class="sxs-lookup"><span data-stu-id="04edb-816">`S1` is `long` and `S2` is `ulong`</span></span>

#### <a name="overloading-in-generic-classes"></a><span data-ttu-id="04edb-817">Перегрузка в универсальных классах</span><span class="sxs-lookup"><span data-stu-id="04edb-817">Overloading in generic classes</span></span>

<span data-ttu-id="04edb-818">Хотя сигнатуры при объявлении должно быть уникальным, вполне возможно, что подстановки аргументов типа приводит к одинаковые сигнатуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-818">While signatures as declared must be unique, it is possible that substitution of type arguments results in identical signatures.</span></span> <span data-ttu-id="04edb-819">В таких случаях конечные правила разрешения перегрузки выше выберет конкретный член.</span><span class="sxs-lookup"><span data-stu-id="04edb-819">In such cases, the tie-breaking rules of overload resolution above will pick the most specific member.</span></span>

<span data-ttu-id="04edb-820">Ниже приведены примеры допустимых и недопустимых согласно этому правилу перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-820">The following examples show overloads that are valid and invalid according to this rule:</span></span>

```csharp
interface I1<T> {...}

interface I2<T> {...}

class G1<U>
{
    int F1(U u);                  // Overload resolution for G<int>.F1
    int F1(int i);                // will pick non-generic

    void F2(I1<U> a);             // Valid overload
    void F2(I2<U> a);
}

class G2<U,V>
{
    void F3(U u, V v);            // Valid, but overload resolution for
    void F3(V v, U u);            // G2<int,int>.F3 will fail

    void F4(U u, I1<V> v);        // Valid, but overload resolution for    
    void F4(I1<V> v, U u);        // G2<I1<int>,int>.F4 will fail

    void F5(U u1, I1<V> v2);      // Valid overload
    void F5(V v1, U u2);

    void F6(ref U u);             // valid overload
    void F6(out V v);
}
```

### <a name="compile-time-checking-of-dynamic-overload-resolution"></a><span data-ttu-id="04edb-821">Проверка динамического разрешения перегрузки во время компиляции</span><span class="sxs-lookup"><span data-stu-id="04edb-821">Compile-time checking of dynamic overload resolution</span></span>

<span data-ttu-id="04edb-822">Для наиболее динамически связанных операций набор возможных кандидатов для разрешения во время компиляции неизвестен.</span><span class="sxs-lookup"><span data-stu-id="04edb-822">For most dynamically bound operations the set of possible candidates for resolution is unknown at compile-time.</span></span> <span data-ttu-id="04edb-823">В некоторых случаях Однако набор кандидатов известен во время компиляции:</span><span class="sxs-lookup"><span data-stu-id="04edb-823">In certain cases, however the candidate set is known at compile-time:</span></span>

*  <span data-ttu-id="04edb-824">Вызовов статических методов с динамическими аргументами</span><span class="sxs-lookup"><span data-stu-id="04edb-824">Static method calls with dynamic arguments</span></span>
*  <span data-ttu-id="04edb-825">Вызовы методов экземпляра, когда получатель не является динамическим выражением</span><span class="sxs-lookup"><span data-stu-id="04edb-825">Instance method calls where the receiver is not a dynamic expression</span></span>
*  <span data-ttu-id="04edb-826">Вызовы индексатора, когда получатель не является динамическим выражением</span><span class="sxs-lookup"><span data-stu-id="04edb-826">Indexer calls where the receiver is not a dynamic expression</span></span>
*  <span data-ttu-id="04edb-827">Вызовы конструктора с динамическими аргументами</span><span class="sxs-lookup"><span data-stu-id="04edb-827">Constructor calls with dynamic arguments</span></span>

<span data-ttu-id="04edb-828">В таких случаях проверку только во время компиляции выполняется для каждого кандидата см. в разделе, если любой из них возможно применить во время выполнения. Эта проверка состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-828">In these cases a limited compile-time check is performed for each candidate to see if any of them could possibly apply at run-time.This check consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-829">Определение разделяемого типа: Любой тип, аргумент, который не зависит от прямо или косвенно аргумент типа `dynamic` определяется с помощью правил [вывод типа](expressions.md#type-inference).</span><span class="sxs-lookup"><span data-stu-id="04edb-829">Partial type inference: Any type argument that does not depend directly or indirectly on an argument of type `dynamic` is inferred using the rules of [Type inference](expressions.md#type-inference).</span></span> <span data-ttu-id="04edb-830">Остальные аргументы типа неизвестны.</span><span class="sxs-lookup"><span data-stu-id="04edb-830">The remaining type arguments are unknown.</span></span>
*  <span data-ttu-id="04edb-831">Частичная проверка: Применимость проверяется в соответствии с [применимого члена функции](expressions.md#applicable-function-member), но параметры, типы которых неизвестны.</span><span class="sxs-lookup"><span data-stu-id="04edb-831">Partial applicability check: Applicability is checked according to [Applicable function member](expressions.md#applicable-function-member), but ignoring parameters whose types are unknown.</span></span>
*  <span data-ttu-id="04edb-832">Если нет кандидата проходит этот тест, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-832">If no candidate passes this test, a compile-time error occurs.</span></span>

### <a name="function-member-invocation"></a><span data-ttu-id="04edb-833">Вызов функции-члена</span><span class="sxs-lookup"><span data-stu-id="04edb-833">Function member invocation</span></span>

<span data-ttu-id="04edb-834">В этом разделе описывается процесс, который происходит во время выполнения для вызова определенной функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-834">This section describes the process that takes place at run-time to invoke a particular function member.</span></span> <span data-ttu-id="04edb-835">Предполагается, что во время компиляции уже определил конкретный член для вызова, возможно, применив разрешения перегрузки для набора потенциальных членов функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-835">It is assumed that a binding-time process has already determined the particular member to invoke, possibly by applying overload resolution to a set of candidate function members.</span></span>

<span data-ttu-id="04edb-836">В целях описания процесса вызова функции-члены можно разделить на две категории:</span><span class="sxs-lookup"><span data-stu-id="04edb-836">For purposes of describing the invocation process, function members are divided into two categories:</span></span>

*  <span data-ttu-id="04edb-837">Статические функции-члены.</span><span class="sxs-lookup"><span data-stu-id="04edb-837">Static function members.</span></span> <span data-ttu-id="04edb-838">Это конструкторы экземпляров, статические методы, статическим свойствам и определяемые пользователем операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-838">These are instance constructors, static methods, static property accessors, and user-defined operators.</span></span> <span data-ttu-id="04edb-839">Статические функции-члены всегда не являются виртуальными.</span><span class="sxs-lookup"><span data-stu-id="04edb-839">Static function members are always non-virtual.</span></span>
*  <span data-ttu-id="04edb-840">Функции-члены экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-840">Instance function members.</span></span> <span data-ttu-id="04edb-841">Это методы экземпляра, экземпляр доступа к свойствам и методам доступа индексаторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-841">These are instance methods, instance property accessors, and indexer accessors.</span></span> <span data-ttu-id="04edb-842">Экземпляр функции-члены как физическую, так и виртуальным и всегда вызываются для конкретного экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-842">Instance function members are either non-virtual or virtual, and are always invoked on a particular instance.</span></span> <span data-ttu-id="04edb-843">Экземпляр вычисляется выражение экземпляра, и он станет доступным в функции-члена с `this` ([такой доступ](expressions.md#this-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-843">The instance is computed by an instance expression, and it becomes accessible within the function member as `this` ([This access](expressions.md#this-access)).</span></span>

<span data-ttu-id="04edb-844">Во время выполнения обработки вызова функции-члена состоит из следующих действий, где `M` является функцией-членом и, если `M` является членом экземпляра, `E` выражение экземпляра:</span><span class="sxs-lookup"><span data-stu-id="04edb-844">The run-time processing of a function member invocation consists of the following steps, where `M` is the function member and, if `M` is an instance member, `E` is the instance expression:</span></span>

*  <span data-ttu-id="04edb-845">Если `M` является статической функцией-членом:</span><span class="sxs-lookup"><span data-stu-id="04edb-845">If `M` is a static function member:</span></span>
   * <span data-ttu-id="04edb-846">Список аргументов вычисляется, как описано в разделе [списки аргументов](expressions.md#argument-lists).</span><span class="sxs-lookup"><span data-stu-id="04edb-846">The argument list is evaluated as described in [Argument lists](expressions.md#argument-lists).</span></span>
   * <span data-ttu-id="04edb-847">`M` вызывается.</span><span class="sxs-lookup"><span data-stu-id="04edb-847">`M` is invoked.</span></span>

*  <span data-ttu-id="04edb-848">Если `M` объявляется в функции-члене экземпляра *value_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-848">If `M` is an instance function member declared in a *value_type*:</span></span>
   * <span data-ttu-id="04edb-849">`E` выполняется оценка.</span><span class="sxs-lookup"><span data-stu-id="04edb-849">`E` is evaluated.</span></span> <span data-ttu-id="04edb-850">Если эта оценка вызывает исключение, никакие дополнительные действия выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-850">If this evaluation causes an exception, then no further steps are executed.</span></span>
   * <span data-ttu-id="04edb-851">Если `E` не классифицируется как переменная, а затем временные локальную переменную с `E`элемента создается тип и значение `E` присваивается этой переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-851">If `E` is not classified as a variable, then a temporary local variable of `E`'s type is created and the value of `E` is assigned to that variable.</span></span> <span data-ttu-id="04edb-852">`E` затем реклассифицировать как ссылку на временный локальная переменная.</span><span class="sxs-lookup"><span data-stu-id="04edb-852">`E` is then reclassified as a reference to that temporary local variable.</span></span> <span data-ttu-id="04edb-853">Временная переменная доступна в виде `this` в `M`, но не в любом другом.</span><span class="sxs-lookup"><span data-stu-id="04edb-853">The temporary variable is accessible as `this` within `M`, but not in any other way.</span></span> <span data-ttu-id="04edb-854">Таким образом, только если `E` является true переменной является возможным для вызывающего объекта увидеть изменения, `M` вносит `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-854">Thus, only when `E` is a true variable is it possible for the caller to observe the changes that `M` makes to `this`.</span></span>
   * <span data-ttu-id="04edb-855">Список аргументов вычисляется, как описано в разделе [списки аргументов](expressions.md#argument-lists).</span><span class="sxs-lookup"><span data-stu-id="04edb-855">The argument list is evaluated as described in [Argument lists](expressions.md#argument-lists).</span></span>
   * <span data-ttu-id="04edb-856">`M` вызывается.</span><span class="sxs-lookup"><span data-stu-id="04edb-856">`M` is invoked.</span></span> <span data-ttu-id="04edb-857">Переменная ссылается `E` становится ссылается переменная `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-857">The variable referenced by `E` becomes the variable referenced by `this`.</span></span>

*  <span data-ttu-id="04edb-858">Если `M` объявляется в функции-члене экземпляра *reference_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-858">If `M` is an instance function member declared in a *reference_type*:</span></span>
   * <span data-ttu-id="04edb-859">`E` выполняется оценка.</span><span class="sxs-lookup"><span data-stu-id="04edb-859">`E` is evaluated.</span></span> <span data-ttu-id="04edb-860">Если эта оценка вызывает исключение, никакие дополнительные действия выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-860">If this evaluation causes an exception, then no further steps are executed.</span></span>
   * <span data-ttu-id="04edb-861">Список аргументов вычисляется, как описано в разделе [списки аргументов](expressions.md#argument-lists).</span><span class="sxs-lookup"><span data-stu-id="04edb-861">The argument list is evaluated as described in [Argument lists](expressions.md#argument-lists).</span></span>
   * <span data-ttu-id="04edb-862">Если тип `E` — *value_type*, упаковка-преобразование ([осуществлять преобразования-упаковки](types.md#boxing-conversions)) выполняется, чтобы преобразовать `E` ввода `object`, и `E` считается Тип `object` в следующих шагах.</span><span class="sxs-lookup"><span data-stu-id="04edb-862">If the type of `E` is a *value_type*, a boxing conversion ([Boxing conversions](types.md#boxing-conversions)) is performed to convert `E` to type `object`, and `E` is considered to be of type `object` in the following steps.</span></span> <span data-ttu-id="04edb-863">В этом случае `M` может быть только членом `System.Object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-863">In this case, `M` could only be a member of `System.Object`.</span></span>
   * <span data-ttu-id="04edb-864">Значение `E` проверяется, чтобы быть допустимыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-864">The value of `E` is checked to be valid.</span></span> <span data-ttu-id="04edb-865">Если значение `E` — `null`, `System.NullReferenceException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-865">If the value of `E` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
   * <span data-ttu-id="04edb-866">Реализация функции-члена для вызова определяется:</span><span class="sxs-lookup"><span data-stu-id="04edb-866">The function member implementation to invoke is determined:</span></span>
     * <span data-ttu-id="04edb-867">Если тип времени привязки `E` является интерфейсом, функция-член является реализацией `M` предоставляемые типом времени выполнения экземпляра ссылается `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-867">If the binding-time type of `E` is an interface, the function member to invoke is the implementation of `M` provided by the run-time type of the instance referenced by `E`.</span></span> <span data-ttu-id="04edb-868">Эта функция-член определяется применением правил сопоставления интерфейса ([сопоставление интерфейса](interfaces.md#interface-mapping)) для определения реализации `M` предоставляемые типом времени выполнения экземпляра ссылается `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-868">This function member is determined by applying the interface mapping rules ([Interface mapping](interfaces.md#interface-mapping)) to determine the implementation of `M` provided by the run-time type of the instance referenced by `E`.</span></span>
     * <span data-ttu-id="04edb-869">В противном случае, если `M` входит виртуальная функция, вызываемая функция-член является реализацией `M` предоставляемые типом времени выполнения экземпляра, на который указывает `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-869">Otherwise, if `M` is a virtual function member, the function member to invoke is the implementation of `M` provided by the run-time type of the instance referenced by `E`.</span></span> <span data-ttu-id="04edb-870">Эта функция-член определяется применением правил для определения наиболее производной реализацией ([виртуальных методов](classes.md#virtual-methods)) из `M` по отношению к времени выполнения тип экземпляра, `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-870">This function member is determined by applying the rules for determining the most derived implementation ([Virtual methods](classes.md#virtual-methods)) of `M` with respect to the run-time type of the instance referenced by `E`.</span></span>
     * <span data-ttu-id="04edb-871">В противном случае `M` является членом невиртуальной функции, а функция-член для вызова `M` сам.</span><span class="sxs-lookup"><span data-stu-id="04edb-871">Otherwise, `M` is a non-virtual function member, and the function member to invoke is `M` itself.</span></span>
   * <span data-ttu-id="04edb-872">Вызывается реализация функции-члена, определенный на предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="04edb-872">The function member implementation determined in the step above is invoked.</span></span> <span data-ttu-id="04edb-873">Объект, упоминаемый в `E` становится объект, упоминаемый в `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-873">The object referenced by `E` becomes the object referenced by `this`.</span></span>

#### <a name="invocations-on-boxed-instances"></a><span data-ttu-id="04edb-874">Вызов в упакованных экземплярах</span><span class="sxs-lookup"><span data-stu-id="04edb-874">Invocations on boxed instances</span></span>

<span data-ttu-id="04edb-875">Функция-член реализуется в *value_type* можно вызывать с помощью упакованный экземпляр, *value_type* в следующих ситуациях:</span><span class="sxs-lookup"><span data-stu-id="04edb-875">A function member implemented in a *value_type* can be invoked through a boxed instance of that *value_type* in the following situations:</span></span>

*  <span data-ttu-id="04edb-876">Если функция-член имеет `override` метода, унаследованного от типа `object` и вызывается через выражение экземпляра типа `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-876">When the function member is an `override` of a method inherited from type `object` and is invoked through an instance expression of type `object`.</span></span>
*  <span data-ttu-id="04edb-877">Когда функция-член представляет собой реализацию функции-члена и вызывается через выражение экземпляра *interface_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-877">When the function member is an implementation of an interface function member and is invoked through an instance expression of an *interface_type*.</span></span>
*  <span data-ttu-id="04edb-878">Когда функция-член вызывается через делегат.</span><span class="sxs-lookup"><span data-stu-id="04edb-878">When the function member is invoked through a delegate.</span></span>

<span data-ttu-id="04edb-879">В таких ситуациях упакованный экземпляр считается содержит переменную *value_type*, и эта переменная становится ссылается переменная `this` в вызове функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-879">In these situations, the boxed instance is considered to contain a variable of the *value_type*, and this variable becomes the variable referenced by `this` within the function member invocation.</span></span> <span data-ttu-id="04edb-880">В частности это означает, что при вызове функции-члена на упакованный экземпляр возможна функцию-член изменить значение, содержащееся в упакованный экземпляр.</span><span class="sxs-lookup"><span data-stu-id="04edb-880">In particular, this means that when a function member is invoked on a boxed instance, it is possible for the function member to modify the value contained in the boxed instance.</span></span>

## <a name="primary-expressions"></a><span data-ttu-id="04edb-881">Основные выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-881">Primary expressions</span></span>

<span data-ttu-id="04edb-882">Первичные выражения включают простые формы выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-882">Primary expressions include the simplest forms of expressions.</span></span>

```antlr
primary_expression
    : primary_no_array_creation_expression
    | array_creation_expression
    ;

primary_no_array_creation_expression
    : literal
    | interpolated_string_expression
    | simple_name
    | parenthesized_expression
    | member_access
    | invocation_expression
    | element_access
    | this_access
    | base_access
    | post_increment_expression
    | post_decrement_expression
    | object_creation_expression
    | delegate_creation_expression
    | anonymous_object_creation_expression
    | typeof_expression
    | checked_expression
    | unchecked_expression
    | default_value_expression
    | nameof_expression
    | anonymous_method_expression
    | primary_no_array_creation_expression_unsafe
    ;
```

<span data-ttu-id="04edb-883">Первичные выражения разделяются между *array_creation_expression*s и *primary_no_array_creation_expression*s.</span><span class="sxs-lookup"><span data-stu-id="04edb-883">Primary expressions are divided between *array_creation_expression*s and *primary_no_array_creation_expression*s.</span></span> <span data-ttu-id="04edb-884">Рассматривая выражение создания массива таким образом, вместо того чтобы, добавив его вместе с других форм простое выражение, позволяет в грамматике запретить может ввести в заблуждение кода, такие как</span><span class="sxs-lookup"><span data-stu-id="04edb-884">Treating array-creation-expression in this way, rather than listing it along with the other simple expression forms, enables the grammar to disallow potentially confusing code such as</span></span>
```csharp
object o = new int[3][1];
```
<span data-ttu-id="04edb-885">который в противном случае будет интерпретироваться как</span><span class="sxs-lookup"><span data-stu-id="04edb-885">which would otherwise be interpreted as</span></span>
```csharp
object o = (new int[3])[1];
```

### <a name="literals"></a><span data-ttu-id="04edb-886">Литералы</span><span class="sxs-lookup"><span data-stu-id="04edb-886">Literals</span></span>

<span data-ttu-id="04edb-887">Объект *primary_expression* , состоящий из *литерала* ([литералы](lexical-structure.md#literals)) классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-887">A *primary_expression* that consists of a *literal* ([Literals](lexical-structure.md#literals)) is classified as a value.</span></span>


### <a name="interpolated-strings"></a><span data-ttu-id="04edb-888">Интерполированные строки</span><span class="sxs-lookup"><span data-stu-id="04edb-888">Interpolated strings</span></span>

<span data-ttu-id="04edb-889">*Interpolated_string_expression* состоит из `$` входа следуют обычный или буквального строкового литерала, при котором бреши в системе, разделяемых строками `{` и `}`, заключите выражения и форматирование спецификации.</span><span class="sxs-lookup"><span data-stu-id="04edb-889">An *interpolated_string_expression* consists of a `$` sign followed by a regular or verbatim string literal, wherein holes, delimited by `{` and `}`, enclose expressions and formatting specifications.</span></span> <span data-ttu-id="04edb-890">Интерполированное строковое выражение является результатом *interpolated_string_literal* , был разбит на отдельные части, как описано в разделе [интерполированные строковые литералы](lexical-structure.md#interpolated-string-literals).</span><span class="sxs-lookup"><span data-stu-id="04edb-890">An interpolated string expression is the result of an *interpolated_string_literal* that has been broken up into individual tokens, as described in [Interpolated string literals](lexical-structure.md#interpolated-string-literals).</span></span>

```antlr
interpolated_string_expression
    : '$' interpolated_regular_string
    | '$' interpolated_verbatim_string
    ;

interpolated_regular_string
    : interpolated_regular_string_whole
    | interpolated_regular_string_start interpolated_regular_string_body interpolated_regular_string_end
    ;

interpolated_regular_string_body
    : interpolation (interpolated_regular_string_mid interpolation)*
    ;

interpolation
    : expression
    | expression ',' constant_expression
    ;

interpolated_verbatim_string
    : interpolated_verbatim_string_whole
    | interpolated_verbatim_string_start interpolated_verbatim_string_body interpolated_verbatim_string_end
    ;

interpolated_verbatim_string_body
    : interpolation (interpolated_verbatim_string_mid interpolation)+
    ;
```

<span data-ttu-id="04edb-891">*Constant_expression* интерполяции должен иметь неявное преобразование в `int`.</span><span class="sxs-lookup"><span data-stu-id="04edb-891">The *constant_expression* in an interpolation must have an implicit conversion to `int`.</span></span>

<span data-ttu-id="04edb-892">*Interpolated_string_expression* классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-892">An *interpolated_string_expression* is classified as a value.</span></span> <span data-ttu-id="04edb-893">Если сразу же он преобразуется в `System.IFormattable` или `System.FormattableString` с преобразование неявных интерполированной строки ([неявные интерполированные преобразования строк](conversions.md#implicit-interpolated-string-conversions)), интерполированного строкового выражения имеет этот тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-893">If it is immediately converted to `System.IFormattable` or `System.FormattableString` with an implicit interpolated string conversion ([Implicit interpolated string conversions](conversions.md#implicit-interpolated-string-conversions)), the interpolated string expression has that type.</span></span> <span data-ttu-id="04edb-894">В противном случае он имеет тип `string`.</span><span class="sxs-lookup"><span data-stu-id="04edb-894">Otherwise, it has the type `string`.</span></span>

<span data-ttu-id="04edb-895">Если тип интерполированной строки `System.IFormattable` или `System.FormattableString`, значение представляет собой вызов `System.Runtime.CompilerServices.FormattableStringFactory.Create`.</span><span class="sxs-lookup"><span data-stu-id="04edb-895">If the type of an interpolated string is `System.IFormattable` or `System.FormattableString`, the meaning is a call to `System.Runtime.CompilerServices.FormattableStringFactory.Create`.</span></span> <span data-ttu-id="04edb-896">Если тип является `string`, значение выражения представляет собой вызов `string.Format`.</span><span class="sxs-lookup"><span data-stu-id="04edb-896">If the type is `string`, the meaning of the expression is a call to `string.Format`.</span></span> <span data-ttu-id="04edb-897">В обоих случаях списке аргументов вызова состоит из строковый литерал с заполнителями для каждого интерполяции и аргумент для каждого выражения, соответствующего заполнители формата.</span><span class="sxs-lookup"><span data-stu-id="04edb-897">In both cases, the argument list of the call consists of a format string literal with placeholders for each interpolation, and an argument for each expression corresponding to the place holders.</span></span>

<span data-ttu-id="04edb-898">Формат строкового литерала составляется следующим образом, где `N` число интерполяции в *interpolated_string_expression*:</span><span class="sxs-lookup"><span data-stu-id="04edb-898">The format string literal is constructed as follows, where `N` is the number of interpolations in the *interpolated_string_expression*:</span></span>

*  <span data-ttu-id="04edb-899">Если *interpolated_regular_string_whole* или *interpolated_verbatim_string_whole* соответствует `$` подписать, строковый литерал формата, то этот маркер.</span><span class="sxs-lookup"><span data-stu-id="04edb-899">If an *interpolated_regular_string_whole* or an *interpolated_verbatim_string_whole* follows the `$` sign, then the format string literal is that token.</span></span>
*  <span data-ttu-id="04edb-900">В противном случае формат строковый литерал состоит из:</span><span class="sxs-lookup"><span data-stu-id="04edb-900">Otherwise, the format string literal consists of:</span></span> 
   *  <span data-ttu-id="04edb-901">Первый *interpolated_regular_string_start* или *interpolated_verbatim_string_start*</span><span class="sxs-lookup"><span data-stu-id="04edb-901">First the *interpolated_regular_string_start* or *interpolated_verbatim_string_start*</span></span>
   *  <span data-ttu-id="04edb-902">Затем для каждого номера `I` из `0` для `N-1`:</span><span class="sxs-lookup"><span data-stu-id="04edb-902">Then for each number `I` from `0` to `N-1`:</span></span> 
      * <span data-ttu-id="04edb-903">Десятичное представление `I`</span><span class="sxs-lookup"><span data-stu-id="04edb-903">The decimal representation of `I`</span></span>
      * <span data-ttu-id="04edb-904">Затем, если соответствующий *интерполяции* имеет *constant_expression*, `,` (запятая) следуют десятичное представление значение *constant_expression*</span><span class="sxs-lookup"><span data-stu-id="04edb-904">Then, if the corresponding *interpolation* has a *constant_expression*, a `,` (comma) followed by the decimal representation of the value of the *constant_expression*</span></span>
      * <span data-ttu-id="04edb-905">Затем *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_mid* или *interpolated_ verbatim_string_end* сразу после соответствующего интерполяции.</span><span class="sxs-lookup"><span data-stu-id="04edb-905">Then the *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_mid* or *interpolated_verbatim_string_end* immediately following the corresponding interpolation.</span></span>

<span data-ttu-id="04edb-906">Последующие аргументы представляют собой *выражения* из *интерполяций* (если таковые имеются), в порядке.</span><span class="sxs-lookup"><span data-stu-id="04edb-906">The subsequent arguments are simply the *expressions* from the *interpolations* (if any), in order.</span></span>

<span data-ttu-id="04edb-907">TODO: примеры.</span><span class="sxs-lookup"><span data-stu-id="04edb-907">TODO: examples.</span></span>


### <a name="simple-names"></a><span data-ttu-id="04edb-908">Простые имена</span><span class="sxs-lookup"><span data-stu-id="04edb-908">Simple names</span></span>

<span data-ttu-id="04edb-909">Объект *simple_name* состоит из идентификатора, необязательно следует список аргументов типа:</span><span class="sxs-lookup"><span data-stu-id="04edb-909">A *simple_name* consists of an identifier, optionally followed by a type argument list:</span></span>

```antlr
simple_name
    : identifier type_argument_list?
    ;
```

<span data-ttu-id="04edb-910">Объект *simple_name* либо формы `I` или формы `I<A1,...,Ak>`, где `I` — отдельный идентификатор и `<A1,...,Ak>` не является обязательной *type_argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-910">A *simple_name* is either of the form `I` or of the form `I<A1,...,Ak>`, where `I` is a single identifier and `<A1,...,Ak>` is an optional *type_argument_list*.</span></span> <span data-ttu-id="04edb-911">Если аргумент *type_argument_list* будет указано, рассмотрите возможность `K` должно быть равно нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-911">When no *type_argument_list* is specified, consider `K` to be zero.</span></span> <span data-ttu-id="04edb-912">*Simple_name* вычисляется и классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-912">The *simple_name* is evaluated and classified as follows:</span></span>

*  <span data-ttu-id="04edb-913">Если `K` равно нулю и *simple_name* отображается в *блок* и, если *блок*элемента (или во внешнем *блок*в) локальный объявление переменной пространства ([объявления](basic-concepts.md#declarations)) содержит локальную переменную, параметр или константа с именем `I`, а затем *simple_name* ссылается локальная переменная, параметр или константа и классифицируется как переменная или значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-913">If `K` is zero and the *simple_name* appears within a *block* and if the *block*'s (or an enclosing *block*'s) local variable declaration space ([Declarations](basic-concepts.md#declarations)) contains a local variable, parameter or constant with name `I`, then the *simple_name* refers to that local variable, parameter or constant and is classified as a variable or value.</span></span>
*  <span data-ttu-id="04edb-914">Если `K` равно нулю и *simple_name* отображается в основном тексте, входящем в объявление универсального метода и если это объявление включает параметр типа с именем `I`, а затем *simple_name*ссылается на этот параметр типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-914">If `K` is zero and the *simple_name* appears within the body of a generic method declaration and if that declaration includes a type parameter with name `I`, then the *simple_name* refers to that type parameter.</span></span>
*  <span data-ttu-id="04edb-915">В противном случае — для каждого типа экземпляра `T` ([тип экземпляра](classes.md#the-instance-type)), начиная с типом экземпляра немедленно включающего объявления типа и продолжить с типом экземпляра каждого включающего класса или структуры объявления (при его наличии):</span><span class="sxs-lookup"><span data-stu-id="04edb-915">Otherwise, for each instance type `T` ([The instance type](classes.md#the-instance-type)), starting with the instance type of the immediately enclosing type declaration and continuing with the instance type of each enclosing class or struct declaration (if any):</span></span>
   *  <span data-ttu-id="04edb-916">Если `K` равно нулю и объявление `T` включает параметр типа с именем `I`, а затем *simple_name* ссылается на этот параметр типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-916">If `K` is zero and the declaration of `T` includes a type parameter with name `I`, then the *simple_name* refers to that type parameter.</span></span>
   *  <span data-ttu-id="04edb-917">В противном случае, если поиск члена ([поиск члена](expressions.md#member-lookup)) из `I` в `T` с `K`  аргументы типа найдено соответствие:</span><span class="sxs-lookup"><span data-stu-id="04edb-917">Otherwise, if a member lookup ([Member lookup](expressions.md#member-lookup)) of `I` in `T` with `K` type arguments produces a match:</span></span>
      * <span data-ttu-id="04edb-918">Если `T` является тип экземпляра немедленно включающего типа класса или структуры и уточняющего запроса определяет одну или несколько методов, результат — это группа методов со связанным выражением экземпляра `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-918">If `T` is the instance type of the immediately enclosing class or struct type and the lookup identifies one or more methods, the result is a method group with an associated instance expression of `this`.</span></span> <span data-ttu-id="04edb-919">Если указан список аргументов типа, он используется в вызове универсального метода ([вызовы методов](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-919">If a type argument list was specified, it is used in calling a generic method ([Method invocations](expressions.md#method-invocations)).</span></span>
      * <span data-ttu-id="04edb-920">В противном случае, если `T` не тип экземпляра немедленно включающего типа класса или структуры, в том случае, если уточняющего запроса определяет член экземпляра, и в том случае, если возникает в теле конструктора экземпляра, методе экземпляра или метода доступа к экземпляру Результатом является таким же, как доступ к члену ([доступ к членам](expressions.md#member-access)) формы `this.I`.</span><span class="sxs-lookup"><span data-stu-id="04edb-920">Otherwise, if `T` is the instance type of the immediately enclosing class or struct type, if the lookup identifies an instance member, and if the reference occurs within the body of an instance constructor, an instance method, or an instance accessor, the result is the same as a member access ([Member access](expressions.md#member-access)) of the form `this.I`.</span></span> <span data-ttu-id="04edb-921">Это может произойти, только когда `K` равно нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-921">This can only happen when `K` is zero.</span></span>
      * <span data-ttu-id="04edb-922">В противном случае результат является таким же, как доступ к члену ([доступ к членам](expressions.md#member-access)) формы `T.I` или `T.I<A1,...,Ak>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-922">Otherwise, the result is the same as a member access ([Member access](expressions.md#member-access)) of the form `T.I` or `T.I<A1,...,Ak>`.</span></span> <span data-ttu-id="04edb-923">В этом случае является ошибкой времени привязки для *simple_name* для ссылки на член экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-923">In this case, it is a binding-time error for the *simple_name* to refer to an instance member.</span></span>

*  <span data-ttu-id="04edb-924">В противном случае — для каждого пространства имен `N`, начиная с пространством имен, в котором *simple_name* происходит, продолжая каждого включающего пространства имен (если таковые имеются) и заканчивая глобальное пространство имен, выполнив следующие действия вычисления, пока не будет обнаружена сущность:</span><span class="sxs-lookup"><span data-stu-id="04edb-924">Otherwise, for each namespace `N`, starting with the namespace in which the *simple_name* occurs, continuing with each enclosing namespace (if any), and ending with the global namespace, the following steps are evaluated until an entity is located:</span></span>
   *  <span data-ttu-id="04edb-925">Если `K` равно нулю и `I` имя пространства имен в `N`, затем:</span><span class="sxs-lookup"><span data-stu-id="04edb-925">If `K` is zero and `I` is the name of a namespace in `N`, then:</span></span>
      * <span data-ttu-id="04edb-926">Если расположение где *simple_name* происходит заключен в объявление пространства имен для `N` и содержит объявление пространства имен *extern_alias_directive* или  *using_alias_directive* , связывает имя `I` пространства имен или тип, а затем *simple_name* является неоднозначным и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-926">If the location where the *simple_name* occurs is enclosed by a namespace declaration for `N` and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with a namespace or type, then the *simple_name* is ambiguous and a compile-time error occurs.</span></span>
      * <span data-ttu-id="04edb-927">В противном случае *simple_name* ссылается на пространство имен с именем `I` в `N`.</span><span class="sxs-lookup"><span data-stu-id="04edb-927">Otherwise, the *simple_name* refers to the namespace named `I` in `N`.</span></span>
   *  <span data-ttu-id="04edb-928">В противном случае, если `N` содержит доступный тип с именем `I` и `K`  параметрами типа, то:</span><span class="sxs-lookup"><span data-stu-id="04edb-928">Otherwise, if `N` contains an accessible type having name `I` and `K` type parameters, then:</span></span>
      * <span data-ttu-id="04edb-929">Если `K` равно нулю и расположение где *simple_name* происходит заключен в объявление пространства имен для `N` и содержит объявление пространства имен *extern_alias_directive*или *using_alias_directive* , связывает имя `I` пространства имен или тип, а затем *simple_name* является неоднозначным и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-929">If `K` is zero and the location where the *simple_name* occurs is enclosed by a namespace declaration for `N` and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with a namespace or type, then the *simple_name* is ambiguous and a compile-time error occurs.</span></span>
      * <span data-ttu-id="04edb-930">В противном случае *namespace_or_type_name* ссылается на тип, сформированный с заданными аргументами типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-930">Otherwise, the *namespace_or_type_name* refers to the type constructed with the given type arguments.</span></span>
   *  <span data-ttu-id="04edb-931">В противном случае, если расположение где *simple_name* происходит заключен в объявление пространства имен для `N`:</span><span class="sxs-lookup"><span data-stu-id="04edb-931">Otherwise, if the location where the *simple_name* occurs is enclosed by a namespace declaration for `N`:</span></span>
      * <span data-ttu-id="04edb-932">Если `K` равен нулю и содержит объявление пространства имен *extern_alias_directive* или *using_alias_directive* , связывает имя `I` с импортированное пространство имен или тип, а затем *simple_name* ссылается на это пространство имен или тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-932">If `K` is zero and the namespace declaration contains an *extern_alias_directive* or *using_alias_directive* that associates the name `I` with an imported namespace or type, then the *simple_name* refers to that namespace or type.</span></span>
      * <span data-ttu-id="04edb-933">В противном случае, если объявления типов и пространств имен, импортированные с *using_namespace_directive*s и *using_static_directive*объявления пространства имен содержат ровно один доступный тип или не являющийся расширением статический член, имеющий имя `I` и `K`  параметры типа, а затем *simple_name* ссылается на этот тип или член, сформированный с заданными аргументами типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-933">Otherwise, if the namespaces and type declarations imported by the *using_namespace_directive*s and *using_static_directive*s of the namespace declaration contain exactly one accessible type or non-extension static member having name `I` and `K` type parameters, then the *simple_name* refers to that type or member constructed with the given type arguments.</span></span>
      * <span data-ttu-id="04edb-934">В противном случае, если пространства имен и типы, импортированные с *using_namespace_directive*объявления пространства имен содержат более чем один доступный тип или расширение метод статический член, имеющий имя `I` и `K`  параметры типа, а затем *simple_name* является неоднозначным и возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="04edb-934">Otherwise, if the namespaces and types imported by the *using_namespace_directive*s of the namespace declaration contain more than one accessible type or non-extension-method static member having name `I` and `K` type parameters, then the *simple_name* is ambiguous and an error occurs.</span></span>

   <span data-ttu-id="04edb-935">Обратите внимание, что этот этап полностью повторяет соответствующий шаг в обработке *namespace_or_type_name* ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)).</span><span class="sxs-lookup"><span data-stu-id="04edb-935">Note that this entire step is exactly parallel to the corresponding step in the processing of a *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)).</span></span>

*  <span data-ttu-id="04edb-936">В противном случае *simple_name* — не определено и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-936">Otherwise, the *simple_name* is undefined and a compile-time error occurs.</span></span>


### <a name="parenthesized-expressions"></a><span data-ttu-id="04edb-937">Выражения в скобках</span><span class="sxs-lookup"><span data-stu-id="04edb-937">Parenthesized expressions</span></span>

<span data-ttu-id="04edb-938">Объект *parenthesized_expression* состоит из *выражение* заключены в круглые скобки.</span><span class="sxs-lookup"><span data-stu-id="04edb-938">A *parenthesized_expression* consists of an *expression* enclosed in parentheses.</span></span>

```antlr
parenthesized_expression
    : '(' expression ')'
    ;
```

<span data-ttu-id="04edb-939">Объект *parenthesized_expression* вычисляется путем вычисления *выражение* в круглых скобках.</span><span class="sxs-lookup"><span data-stu-id="04edb-939">A *parenthesized_expression* is evaluated by evaluating the *expression* within the parentheses.</span></span> <span data-ttu-id="04edb-940">Если *выражение* в круглых скобках обозначает пространство имен или тип, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-940">If the *expression* within the parentheses denotes a namespace or type, a compile-time error occurs.</span></span> <span data-ttu-id="04edb-941">В противном случае результат *parenthesized_expression* является результатом вычисления содержащегося *выражение*.</span><span class="sxs-lookup"><span data-stu-id="04edb-941">Otherwise, the result of the *parenthesized_expression* is the result of the evaluation of the contained *expression*.</span></span>

### <a name="member-access"></a><span data-ttu-id="04edb-942">Доступ к членам</span><span class="sxs-lookup"><span data-stu-id="04edb-942">Member access</span></span>

<span data-ttu-id="04edb-943">Объект *member_access* состоит из *primary_expression*, *predefined_type*, или *qualified_alias_member*, а затем«`.`"токена, за которым следует *идентификатор*, при необходимости за которым следует *type_argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-943">A *member_access* consists of a *primary_expression*, a *predefined_type*, or a *qualified_alias_member*, followed by a "`.`" token, followed by an *identifier*, optionally followed by a *type_argument_list*.</span></span>

```antlr
member_access
    : primary_expression '.' identifier type_argument_list?
    | predefined_type '.' identifier type_argument_list?
    | qualified_alias_member '.' identifier
    ;

predefined_type
    : 'bool'   | 'byte'  | 'char'  | 'decimal' | 'double' | 'float' | 'int' | 'long'
    | 'object' | 'sbyte' | 'short' | 'string'  | 'uint'   | 'ulong' | 'ushort'
    ;
```

<span data-ttu-id="04edb-944">*Qualified_alias_member* рабочей определяется в [Квалификаторы псевдонима пространства имен](namespaces.md#namespace-alias-qualifiers).</span><span class="sxs-lookup"><span data-stu-id="04edb-944">The *qualified_alias_member* production is defined in [Namespace alias qualifiers](namespaces.md#namespace-alias-qualifiers).</span></span>

<span data-ttu-id="04edb-945">Объект *member_access* либо формы `E.I` или формы `E.I<A1, ..., Ak>`, где `E` — это основное выражение, `I` — отдельный идентификатор и `<A1, ..., Ak>` не является обязательной  *type_argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-945">A *member_access* is either of the form `E.I` or of the form `E.I<A1, ..., Ak>`, where `E` is a primary-expression, `I` is a single identifier and `<A1, ..., Ak>` is an optional *type_argument_list*.</span></span> <span data-ttu-id="04edb-946">Если аргумент *type_argument_list* будет указано, рассмотрите возможность `K` должно быть равно нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-946">When no *type_argument_list* is specified, consider `K` to be zero.</span></span>

<span data-ttu-id="04edb-947">Объект *member_access* с *primary_expression* типа `dynamic` является динамическим ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-947">A *member_access* with a *primary_expression* of type `dynamic` is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-948">В этом случае компилятор классифицирует доступ к члену, как доступ к свойству типа `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-948">In this case the compiler classifies the member access as a property access of type `dynamic`.</span></span> <span data-ttu-id="04edb-949">Правила для определения значения *member_access* применяются во время выполнения, используя тип времени выполнения вместо во время компиляции тип *primary_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-949">The rules below to determine the meaning of the *member_access* are then applied at run-time, using the run-time type instead of the compile-time type of the *primary_expression*.</span></span> <span data-ttu-id="04edb-950">Если эта классификация во время выполнения приводит к группу методов, то должен быть доступ к членам *primary_expression* из *invocation_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-950">If this run-time classification leads to a method group, then the member access must be the *primary_expression* of an *invocation_expression*.</span></span>

<span data-ttu-id="04edb-951">*Member_access* вычисляется и классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-951">The *member_access* is evaluated and classified as follows:</span></span>

*  <span data-ttu-id="04edb-952">Если `K` равно нулю и `E` — это пространство имен и `E` содержит вложенное пространство имен с именем `I`, то результат этого пространства имен.</span><span class="sxs-lookup"><span data-stu-id="04edb-952">If `K` is zero and `E` is a namespace and `E` contains a nested namespace with name `I`, then the result is that namespace.</span></span>
*  <span data-ttu-id="04edb-953">В противном случае, если `E` — это пространство имен и `E` содержит доступный тип с именем `I` и `K`  параметры типа, то результат тоже этот тип, сформированный с заданными аргументами типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-953">Otherwise, if `E` is a namespace and `E` contains an accessible type having name `I` and `K` type parameters, then the result is that type constructed with the given type arguments.</span></span>
*  <span data-ttu-id="04edb-954">Если `E` — *predefined_type* или *primary_expression* классифицируется как тип, если `E` не является параметром типа и при поиске элемента ([поиск члена](expressions.md#member-lookup)) из `I` в `E` с `K`  параметров типа найдено соответствие, затем `E.I` вычисляется и классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-954">If `E` is a *predefined_type* or a *primary_expression* classified as a type, if `E` is not a type parameter, and if a member lookup ([Member lookup](expressions.md#member-lookup)) of `I` in `E` with `K` type parameters produces a match, then `E.I` is evaluated and classified as follows:</span></span>
   *  <span data-ttu-id="04edb-955">Если `I` определяет тип, то результат тоже этот тип, сформированный с заданными аргументами типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-955">If `I` identifies a type, then the result is that type constructed with the given type arguments.</span></span>
   *  <span data-ttu-id="04edb-956">Если `I` определяет один или несколько методов, то результат тоже группу методов с без связанного выражения экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-956">If `I` identifies one or more methods, then the result is a method group with no associated instance expression.</span></span> <span data-ttu-id="04edb-957">Если указан список аргументов типа, он используется в вызове универсального метода ([вызовы методов](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-957">If a type argument list was specified, it is used in calling a generic method ([Method invocations](expressions.md#method-invocations)).</span></span>
   *  <span data-ttu-id="04edb-958">Если `I` идентифицирует `static` свойство, то результат будет доступ к свойству без связанного экземпляра выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-958">If `I` identifies a `static` property, then the result is a property access with no associated instance expression.</span></span>
   *  <span data-ttu-id="04edb-959">Если `I` идентифицирует `static` поля:</span><span class="sxs-lookup"><span data-stu-id="04edb-959">If `I` identifies a `static` field:</span></span>
      * <span data-ttu-id="04edb-960">Если поле является `readonly` и возникает за пределами статическом конструкторе класса или структуры, в котором объявляется поле, то результатом является значение, а именно значение статического поля `I` в `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-960">If the field is `readonly` and the reference occurs outside the static constructor of the class or struct in which the field is declared, then the result is a value, namely the value of the static field `I` in `E`.</span></span>
      * <span data-ttu-id="04edb-961">В противном случае результат является переменная, а именно статическое поле `I` в `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-961">Otherwise, the result is a variable, namely the static field `I` in `E`.</span></span>
   *  <span data-ttu-id="04edb-962">Если `I` идентифицирует `static` событий:</span><span class="sxs-lookup"><span data-stu-id="04edb-962">If `I` identifies a `static` event:</span></span>
      * <span data-ttu-id="04edb-963">Если возникает внутри класса или структуры, в котором объявлено событие, и это событие было объявлено без *event_accessor_declarations* ([события](classes.md#events)), затем `E.I` обрабатывается точно так, как если `I` были статического поля.</span><span class="sxs-lookup"><span data-stu-id="04edb-963">If the reference occurs within the class or struct in which the event is declared, and the event was declared without *event_accessor_declarations* ([Events](classes.md#events)), then `E.I` is processed exactly as if `I` were a static field.</span></span>
      * <span data-ttu-id="04edb-964">В противном случае результатом является доступ к событию с без связанного выражения экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-964">Otherwise, the result is an event access with no associated instance expression.</span></span>
   *  <span data-ttu-id="04edb-965">Если `I` определяет константу, то результатом является значение, а именно значение этой константы.</span><span class="sxs-lookup"><span data-stu-id="04edb-965">If `I` identifies a constant, then the result is a value, namely the value of that constant.</span></span>
    * <span data-ttu-id="04edb-966">Если `I` идентифицирует элемент перечисления, то результатом является значение, а именно значение этого члена перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-966">If `I` identifies an enumeration member, then the result is a value, namely the value of that enumeration member.</span></span>
    * <span data-ttu-id="04edb-967">В противном случае `E.I` является недопустимой ссылкой на член, и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-967">Otherwise, `E.I` is an invalid member reference, and a compile-time error occurs.</span></span>
*  <span data-ttu-id="04edb-968">Если `E` доступ к свойству, индексатору, переменная или значение, тип которого — `T`и поиск члена ([поиск члена](expressions.md#member-lookup)) из `I` в `T` с `K`  аргументы типа найдено соответствие, затем `E.I` вычисляется и классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-968">If `E` is a property access, indexer access, variable, or value, the type of which is `T`, and a member lookup ([Member lookup](expressions.md#member-lookup)) of `I` in `T` with `K` type arguments produces a match, then `E.I` is evaluated and classified as follows:</span></span>
   *  <span data-ttu-id="04edb-969">Во-первых, если `E` свойство или индексатор, то значение свойства или получения доступа к индексатору ([значения выражений](expressions.md#values-of-expressions)) и `E` реклассифицировать как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-969">First, if `E` is a property or indexer access, then the value of the property or indexer access is obtained ([Values of expressions](expressions.md#values-of-expressions)) and `E` is reclassified as a value.</span></span>
   *  <span data-ttu-id="04edb-970">Если `I` определяет один или несколько методов, то результатом является группа методов со связанным выражением экземпляра `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-970">If `I` identifies one or more methods, then the result is a method group with an associated instance expression of `E`.</span></span> <span data-ttu-id="04edb-971">Если указан список аргументов типа, он используется в вызове универсального метода ([вызовы методов](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-971">If a type argument list was specified, it is used in calling a generic method ([Method invocations](expressions.md#method-invocations)).</span></span>
   *  <span data-ttu-id="04edb-972">Если `I` определяет свойство экземпляра,</span><span class="sxs-lookup"><span data-stu-id="04edb-972">If `I` identifies an instance property,</span></span>
      * <span data-ttu-id="04edb-973">Если `E` — `this`, `I` определяет автоматически реализуемого свойства ([автоматически реализуемые свойства](classes.md#automatically-implemented-properties)) без метода задания и ссылка на происходит внутри конструктора для экземпляра тип класса или структуры `T`, то результатом является переменной, а именно скрытые резервное поле для автоматически свойство, заданное параметром `I` в экземпляре `T` предоставленное `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-973">If `E` is `this`, `I` identifies an automatically implemented property ([Automatically implemented properties](classes.md#automatically-implemented-properties)) without a setter, and the reference occurs within an instance constructor for a class or struct type `T`, then the result is a variable, namely the hidden backing field for the auto-property given by `I` in the instance of `T` given by `this`.</span></span>
      * <span data-ttu-id="04edb-974">В противном случае результатом является доступ к свойству со связанным выражением экземпляра `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-974">Otherwise, the result is a property access with an associated instance expression of `E`.</span></span>
   *  <span data-ttu-id="04edb-975">Если `T` — *class_type* и `I` определяет поле экземпляра, *class_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-975">If `T` is a *class_type* and `I` identifies an instance field of that *class_type*:</span></span>
      * <span data-ttu-id="04edb-976">Если значение `E` — `null`, а затем `System.NullReferenceException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-976">If the value of `E` is `null`, then a `System.NullReferenceException` is thrown.</span></span>
      * <span data-ttu-id="04edb-977">В противном случае, если поле является `readonly` и возникает за пределами конструктора экземпляра класса, в котором объявляется поле, то результатом является значение, а именно значение поля `I` в объект, упоминаемый в `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-977">Otherwise, if the field is `readonly` and the reference occurs outside an instance constructor of the class in which the field is declared, then the result is a value, namely the value of the field `I` in the object referenced by `E`.</span></span>
      * <span data-ttu-id="04edb-978">В противном случае результат является переменная, а именно поле `I` в объект, упоминаемый в `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-978">Otherwise, the result is a variable, namely the field `I` in the object referenced by `E`.</span></span>
   *  <span data-ttu-id="04edb-979">Если `T` — *struct_type* и `I` определяет поле экземпляра, *struct_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-979">If `T` is a *struct_type* and `I` identifies an instance field of that *struct_type*:</span></span>
      * <span data-ttu-id="04edb-980">Если `E` является значением, или если поле является `readonly` и возникает за пределами конструктора экземпляра структуры, в котором объявляется поле, то результатом является значение, а именно значение поля `I` в экземпляре структуры  `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-980">If `E` is a value, or if the field is `readonly` and the reference occurs outside an instance constructor of the struct in which the field is declared, then the result is a value, namely the value of the field `I` in the struct instance given by `E`.</span></span>
      * <span data-ttu-id="04edb-981">В противном случае результат является переменная, а именно поле `I` в экземпляре структуры по `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-981">Otherwise, the result is a variable, namely the field `I` in the struct instance given by `E`.</span></span>
   *  <span data-ttu-id="04edb-982">Если `I` обозначает событие экземпляра:</span><span class="sxs-lookup"><span data-stu-id="04edb-982">If `I` identifies an instance event:</span></span>
      * <span data-ttu-id="04edb-983">Если возникает внутри класса или структуры, в котором объявлено событие, и это событие было объявлено без *event_accessor_declarations* ([события](classes.md#events)), и ссылки не выполняются от имени левый операнд оператора `+=` или `-=` оператор, затем `E.I` обрабатывается точно так, как если `I` был полем экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-983">If the reference occurs within the class or struct in which the event is declared, and the event was declared without *event_accessor_declarations* ([Events](classes.md#events)), and the reference does not occur as the left-hand side of a `+=` or `-=` operator, then `E.I` is processed exactly as if `I` was an instance field.</span></span>
      * <span data-ttu-id="04edb-984">В противном случае результатом является доступ к событию со связанным выражением экземпляра `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-984">Otherwise, the result is an event access with an associated instance expression of `E`.</span></span>
*  <span data-ttu-id="04edb-985">В противном случае попытки для обработки `E.I` как вызов метода расширения ([вызовы методов расширения](expressions.md#extension-method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-985">Otherwise, an attempt is made to process `E.I` as an extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)).</span></span> <span data-ttu-id="04edb-986">В случае сбоя `E.I` является недопустимой ссылкой на член, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-986">If this fails, `E.I` is an invalid member reference, and a binding-time error occurs.</span></span>

#### <a name="identical-simple-names-and-type-names"></a><span data-ttu-id="04edb-987">Идентичные простые имена и имена типов</span><span class="sxs-lookup"><span data-stu-id="04edb-987">Identical simple names and type names</span></span>

<span data-ttu-id="04edb-988">В доступ к члену в форме `E.I`, если `E` — отдельный идентификатор и, если значение `E` как *simple_name* ([простые имена](expressions.md#simple-names)) — это константы, поля, свойства, Локальная переменная или параметр с тем же типом, что значение `E` как *type_name* ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)), то оба значения из `E` , разрешено.</span><span class="sxs-lookup"><span data-stu-id="04edb-988">In a member access of the form `E.I`, if `E` is a single identifier, and if the meaning of `E` as a *simple_name* ([Simple names](expressions.md#simple-names)) is a constant, field, property, local variable, or parameter with the same type as the meaning of `E` as a *type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)), then both possible meanings of `E` are permitted.</span></span> <span data-ttu-id="04edb-989">Два возможных значения `E.I` никогда не являются неоднозначными, так как `I` обязательно должен быть членом типа `E` в обоих случаях.</span><span class="sxs-lookup"><span data-stu-id="04edb-989">The two possible meanings of `E.I` are never ambiguous, since `I` must necessarily be a member of the type `E` in both cases.</span></span> <span data-ttu-id="04edb-990">Другими словами, правило просто разрешает доступ к статическим членам и вложенные типы `E` где во время компиляции в противном случае возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="04edb-990">In other words, the rule simply permits access to the static members and nested types of `E` where a compile-time error would otherwise have occurred.</span></span> <span data-ttu-id="04edb-991">Пример:</span><span class="sxs-lookup"><span data-stu-id="04edb-991">For example:</span></span>
```csharp
struct Color
{
    public static readonly Color White = new Color(...);
    public static readonly Color Black = new Color(...);

    public Color Complement() {...}
}

class A
{
    public Color Color;                // Field Color of type Color

    void F() {
        Color = Color.Black;           // References Color.Black static member
        Color = Color.Complement();    // Invokes Complement() on Color field
    }

    static void G() {
        Color c = Color.White;         // References Color.White static member
    }
}
```

#### <a name="grammar-ambiguities"></a><span data-ttu-id="04edb-992">Неоднозначность грамматики</span><span class="sxs-lookup"><span data-stu-id="04edb-992">Grammar ambiguities</span></span>

<span data-ttu-id="04edb-993">Порождения для *simple_name* ([простые имена](expressions.md#simple-names)) и *member_access* ([доступ к членам](expressions.md#member-access)) может привести к появлению неоднозначности в Грамматика для выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-993">The productions for *simple_name* ([Simple names](expressions.md#simple-names)) and *member_access* ([Member access](expressions.md#member-access)) can give rise to ambiguities in the grammar for expressions.</span></span> <span data-ttu-id="04edb-994">Например оператор:</span><span class="sxs-lookup"><span data-stu-id="04edb-994">For example, the statement:</span></span>
```
F(G<A,B>(7));
```
<span data-ttu-id="04edb-995">может быть интерпретирован как вызов `F` с двумя аргументами `G < A` и `B > (7)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-995">could be interpreted as a call to `F` with two arguments, `G < A` and `B > (7)`.</span></span> <span data-ttu-id="04edb-996">Кроме того, он может быть интерпретирован как вызов `F` с одним аргументом, который представляет собой вызов универсального метода `G` с двумя аргументами типа и одним обычным аргументом.</span><span class="sxs-lookup"><span data-stu-id="04edb-996">Alternatively, it could be interpreted as a call to `F` with one argument, which is a call to a generic method `G` with two type arguments and one regular argument.</span></span>

<span data-ttu-id="04edb-997">Если последовательность токенов может быть проанализировано как (в контексте) *simple_name* ([простые имена](expressions.md#simple-names)), *member_access* ([доступ к членам](expressions.md#member-access)), или *pointer_member_access* ([доступа к членам указателей](unsafe-code.md#pointer-member-access)) заканчивается *type_argument_list* ([аргументы типа](types.md#type-arguments)), токен сразу после закрывающего `>` маркер проверяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-997">If a sequence of tokens can be parsed (in context) as a *simple_name* ([Simple names](expressions.md#simple-names)), *member_access* ([Member access](expressions.md#member-access)), or *pointer_member_access* ([Pointer member access](unsafe-code.md#pointer-member-access)) ending with a *type_argument_list* ([Type arguments](types.md#type-arguments)), the token immediately following the closing `>` token is examined.</span></span> <span data-ttu-id="04edb-998">Если он является одним из</span><span class="sxs-lookup"><span data-stu-id="04edb-998">If it is one of</span></span>
```csharp
(  )  ]  }  :  ;  ,  .  ?  ==  !=  |  ^
```
<span data-ttu-id="04edb-999">затем *type_argument_list* сохраняется как часть *simple_name*, *member_access* или *pointer_member_access* , а также другой возможный разбор последовательность токенов, отбрасываются.</span><span class="sxs-lookup"><span data-stu-id="04edb-999">then the *type_argument_list* is retained as part of the *simple_name*, *member_access* or *pointer_member_access* and any other possible parse of the sequence of tokens is discarded.</span></span> <span data-ttu-id="04edb-1000">В противном случае *type_argument_list* не считается частью *simple_name*, *member_access* или *pointer_member_access*, даже если нет других возможных синтаксического анализа последовательности маркеров.</span><span class="sxs-lookup"><span data-stu-id="04edb-1000">Otherwise, the *type_argument_list* is not considered to be part of the *simple_name*, *member_access* or *pointer_member_access*, even if there is no other possible parse of the sequence of tokens.</span></span> <span data-ttu-id="04edb-1001">Обратите внимание, что эти правила не применяются при разборе *type_argument_list* в *namespace_or_type_name* ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1001">Note that these rules are not applied when parsing a *type_argument_list* in a *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)).</span></span> <span data-ttu-id="04edb-1002">Оператор</span><span class="sxs-lookup"><span data-stu-id="04edb-1002">The statement</span></span>
```csharp
F(G<A,B>(7));
```
<span data-ttu-id="04edb-1003">согласно этому правилу, интерпретируются как вызов `F` с одним аргументом, который представляет собой вызов универсального метода `G` с двумя аргументами типа и одним обычным аргументом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1003">will, according to this rule, be interpreted as a call to `F` with one argument, which is a call to a generic method `G` with two type arguments and one regular argument.</span></span> <span data-ttu-id="04edb-1004">Операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-1004">The statements</span></span>
```csharp
F(G < A, B > 7);
F(G < A, B >> 7);
```
<span data-ttu-id="04edb-1005">будет интерпретирован как вызов `F` с двумя аргументами.</span><span class="sxs-lookup"><span data-stu-id="04edb-1005">will each be interpreted as a call to `F` with two arguments.</span></span> <span data-ttu-id="04edb-1006">Оператор</span><span class="sxs-lookup"><span data-stu-id="04edb-1006">The statement</span></span>
```csharp
x = F < A > +y;
```
<span data-ttu-id="04edb-1007">будут интерпретироваться как оператор, больше, чем оператор и унарный оператор «плюс», «меньше», как если бы выражение было записано `x = (F < A) > (+y)`, а не как *simple_name* с *type_argument_list* следует оператор сложения двоичный файл.</span><span class="sxs-lookup"><span data-stu-id="04edb-1007">will be interpreted as a less than operator, greater than operator, and unary plus operator, as if the statement had been written `x = (F < A) > (+y)`, instead of as a *simple_name* with a *type_argument_list* followed by a binary plus operator.</span></span> <span data-ttu-id="04edb-1008">В инструкции</span><span class="sxs-lookup"><span data-stu-id="04edb-1008">In the statement</span></span>
```csharp
x = y is C<T> + z;
```
<span data-ttu-id="04edb-1009">токены `C<T>` интерпретируются как *namespace_or_type_name* с *type_argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1009">the tokens `C<T>` are interpreted as a *namespace_or_type_name* with a *type_argument_list*.</span></span>

### <a name="invocation-expressions"></a><span data-ttu-id="04edb-1010">Выражения вызова</span><span class="sxs-lookup"><span data-stu-id="04edb-1010">Invocation expressions</span></span>

<span data-ttu-id="04edb-1011">*Invocation_expression* используется для вызова метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-1011">An *invocation_expression* is used to invoke a method.</span></span>

```antlr
invocation_expression
    : primary_expression '(' argument_list? ')'
    ;
```

<span data-ttu-id="04edb-1012">*Invocation_expression* является динамическим ([динамической привязки](expressions.md#dynamic-binding)) Если содержит по крайней мере одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-1012">An *invocation_expression* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)) if at least one of the following holds:</span></span>

* <span data-ttu-id="04edb-1013">*Primary_expression* имеет тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1013">The *primary_expression* has compile-time type `dynamic`.</span></span>
* <span data-ttu-id="04edb-1014">По крайней мере один аргумент в необязательный *argument_list* имеет тип времени компиляции `dynamic` и *primary_expression* имеет тип делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1014">At least one argument of the optional *argument_list* has compile-time type `dynamic` and the *primary_expression* does not have a delegate type.</span></span>

<span data-ttu-id="04edb-1015">В этом случае компилятор классифицирует *invocation_expression* как значение типа `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1015">In this case the compiler classifies the *invocation_expression* as a value of type `dynamic`.</span></span> <span data-ttu-id="04edb-1016">Правила для определения значения *invocation_expression* применяются во время выполнения, используя тип времени выполнения вместо компиляции типа *primary_expression* и аргументы, которые имеют тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1016">The rules below to determine the meaning of the *invocation_expression* are then applied at run-time, using the run-time type instead of the compile-time type of those of the *primary_expression* and arguments which have the compile-time type `dynamic`.</span></span> <span data-ttu-id="04edb-1017">Если *primary_expression* не имеет типа во время компиляции `dynamic`, то вызов метода выполнена ограниченная проверка времени компиляции, как описано в разделе [Проверка динамического разрешения перегрузки во время компиляции ](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1017">If the *primary_expression* does not have compile-time type `dynamic`, then the method invocation undergoes a limited compile time check as described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="04edb-1018">*Primary_expression* из *invocation_expression* должно быть группой методов или значение *delegate_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1018">The *primary_expression* of an *invocation_expression* must be a method group or a value of a *delegate_type*.</span></span> <span data-ttu-id="04edb-1019">Если *primary_expression* является группой методов *invocation_expression* вызовом метода ([вызовы методов](expressions.md#method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1019">If the *primary_expression* is a method group, the *invocation_expression* is a method invocation ([Method invocations](expressions.md#method-invocations)).</span></span> <span data-ttu-id="04edb-1020">Если *primary_expression* представляет собой значение *delegate_type*, *invocation_expression* является вызовом делегата ([вызовыделегатов](expressions.md#delegate-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1020">If the *primary_expression* is a value of a *delegate_type*, the *invocation_expression* is a delegate invocation ([Delegate invocations](expressions.md#delegate-invocations)).</span></span> <span data-ttu-id="04edb-1021">Если *primary_expression* не является ни группу методов, ни значение *delegate_type*, возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1021">If the *primary_expression* is neither a method group nor a value of a *delegate_type*, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-1022">Необязательный *argument_list* ([списки аргументов](expressions.md#argument-lists)) предоставляет значения или ссылки на переменные для параметров метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-1022">The optional *argument_list* ([Argument lists](expressions.md#argument-lists)) provides values or variable references for the parameters of the method.</span></span>

<span data-ttu-id="04edb-1023">Результат вычисления *invocation_expression* классифицируется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1023">The result of evaluating an *invocation_expression* is classified as follows:</span></span>

*  <span data-ttu-id="04edb-1024">Если *invocation_expression* вызывает метод или делегат, который возвращает `void`, ничего не возвращается.</span><span class="sxs-lookup"><span data-stu-id="04edb-1024">If the *invocation_expression* invokes a method or delegate that returns `void`, the result is nothing.</span></span> <span data-ttu-id="04edb-1025">Выражение, которое классифицируется допускается только в контексте *statement_expression* ([операторы выражений](statements.md#expression-statements)) или в теле *lambda_expression*([Выражения анонимных функций](expressions.md#anonymous-function-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1025">An expression that is classified as nothing is permitted only in the context of a *statement_expression* ([Expression statements](statements.md#expression-statements)) or as the body of a *lambda_expression* ([Anonymous function expressions](expressions.md#anonymous-function-expressions)).</span></span> <span data-ttu-id="04edb-1026">В противном случае возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1026">Otherwise a binding-time error occurs.</span></span>
*  <span data-ttu-id="04edb-1027">В противном случае результатом является значение типа, возвращаемого методом или делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1027">Otherwise, the result is a value of the type returned by the method or delegate.</span></span>

#### <a name="method-invocations"></a><span data-ttu-id="04edb-1028">Вызовы методов</span><span class="sxs-lookup"><span data-stu-id="04edb-1028">Method invocations</span></span>

<span data-ttu-id="04edb-1029">Для вызова метода *primary_expression* из *invocation_expression* должно быть группой методов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1029">For a method invocation, the *primary_expression* of the *invocation_expression* must be a method group.</span></span> <span data-ttu-id="04edb-1030">Группа методов определяет один метод для вызова или набор перегруженных методов с возможностью выбора для вызова определенного метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-1030">The method group identifies the one method to invoke or the set of overloaded methods from which to choose a specific method to invoke.</span></span> <span data-ttu-id="04edb-1031">В последнем случае определение метода, определенного для вызова строится на основе контекста, предоставленных типов аргументов в *argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1031">In the latter case, determination of the specific method to invoke is based on the context provided by the types of the arguments in the *argument_list*.</span></span>

<span data-ttu-id="04edb-1032">Во время привязки обработка вызова метода формы `M(A)`, где `M` является группой методов (возможно, включающий *type_argument_list*), и `A` не является обязательной *argument_ список*, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1032">The binding-time processing of a method invocation of the form `M(A)`, where `M` is a method group (possibly including a *type_argument_list*), and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-1033">Создается набор методов-кандидатов для вызова метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-1033">The set of candidate methods for the method invocation is constructed.</span></span> <span data-ttu-id="04edb-1034">Для каждого метода `F` связанные с группой метод `M`:</span><span class="sxs-lookup"><span data-stu-id="04edb-1034">For each method `F` associated with the method group `M`:</span></span>
   *  <span data-ttu-id="04edb-1035">Если `F` является неуниверсальным `F` является кандидатом при:</span><span class="sxs-lookup"><span data-stu-id="04edb-1035">If `F` is non-generic, `F` is a candidate when:</span></span>
      * <span data-ttu-id="04edb-1036">`M` список аргументов типа не имеет и</span><span class="sxs-lookup"><span data-stu-id="04edb-1036">`M` has no type argument list, and</span></span>
      * <span data-ttu-id="04edb-1037">`F` применяется по отношению к `A` ([применимого члена функции](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1037">`F` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span>
   *  <span data-ttu-id="04edb-1038">Если `F` является универсальным и `M` имеет список аргументов типа не `F` является кандидатом при:</span><span class="sxs-lookup"><span data-stu-id="04edb-1038">If `F` is generic and `M` has no type argument list, `F` is a candidate when:</span></span>
      * <span data-ttu-id="04edb-1039">Определение типа ([вывод типа](expressions.md#type-inference)) завершается успешно, предоставляющий список аргументов типа для вызова, и</span><span class="sxs-lookup"><span data-stu-id="04edb-1039">Type inference ([Type inference](expressions.md#type-inference)) succeeds, inferring a list of type arguments for the call, and</span></span>
      * <span data-ttu-id="04edb-1040">После замены аргументов выведенный тип соответствующие параметры типа для метода, все сформированные типы в списке параметров F соответствуют их ограничений ([удовлетворяющий ограничениям](types.md#satisfying-constraints)) и список параметров `F` применяется по отношению к `A` ([применимого члена функции](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1040">Once the inferred type arguments are substituted for the corresponding method type parameters, all constructed types in the parameter list of F satisfy their constraints ([Satisfying constraints](types.md#satisfying-constraints)), and the parameter list of `F` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span>
   *  <span data-ttu-id="04edb-1041">Если `F` является универсальным и `M` включает список аргументов типа `F` является кандидатом при:</span><span class="sxs-lookup"><span data-stu-id="04edb-1041">If `F` is generic and `M` includes a type argument list, `F` is a candidate when:</span></span>
      * <span data-ttu-id="04edb-1042">`F` имеет тот же номер, тип параметров метода, как указано в списке аргументов типа, и</span><span class="sxs-lookup"><span data-stu-id="04edb-1042">`F` has the same number of method type parameters as were supplied in the type argument list, and</span></span>
      * <span data-ttu-id="04edb-1043">После замены аргументов типа для соответствующих параметров типа метода, все сформированные типы в списке параметров F соответствуют своим ограничениям ([удовлетворяющий ограничениям](types.md#satisfying-constraints)) и список параметров `F` применяется по отношению к `A` ([применимого члена функции](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1043">Once the type arguments are substituted for the corresponding method type parameters, all constructed types in the parameter list of F satisfy their constraints ([Satisfying constraints](types.md#satisfying-constraints)), and the parameter list of `F` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span>
*  <span data-ttu-id="04edb-1044">Набор методов-кандидатов уменьшается, чтобы содержать только методы из большинства производных типов: Для каждого метода `C.F` в наборе, где `C` — это тип, в которой метод `F` был объявлен, все методы, объявленные в базовом типе `C` удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1044">The set of candidate methods is reduced to contain only methods from the most derived types: For each method `C.F` in the set, where `C` is the type in which the method `F` is declared, all methods declared in a base type of `C` are removed from the set.</span></span> <span data-ttu-id="04edb-1045">Кроме того Если `C` не является типом класса `object`, все методы, объявленные в типе интерфейса удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1045">Furthermore, if `C` is a class type other than `object`, all methods declared in an interface type are removed from the set.</span></span> <span data-ttu-id="04edb-1046">(Последнее правило только влияет при группа методов является результатом поиск члена в параметр типа с действительного базового класса, отличного от объекта и эффективный интерфейс непустое значение.)</span><span class="sxs-lookup"><span data-stu-id="04edb-1046">(This latter rule only has affect when the method group was the result of a member lookup on a type parameter having an effective base class other than object and a non-empty effective interface set.)</span></span>
*  <span data-ttu-id="04edb-1047">Если результирующий набор методов-кандидатов пуст, оставляются дальнейшей обработки по инструкциям ниже, и вместо этого будет предпринята попытка обработать вызов в виде вызова метода расширения ([вызовы методов расширения](expressions.md#extension-method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1047">If the resulting set of candidate methods is empty, then further processing along the following steps are abandoned, and instead an attempt is made to process the invocation as an extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)).</span></span> <span data-ttu-id="04edb-1048">Если это не удается, то применимых методов не существует, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1048">If this fails, then no applicable methods exist, and a binding-time error occurs.</span></span>
*  <span data-ttu-id="04edb-1049">Лучше всего подходит набор методов-кандидатов определяется с помощью правил разрешения перегрузки [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1049">The best method of the set of candidate methods is identified using the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="04edb-1050">Если подходящий метод не может быть определен, вызов метода является неоднозначным, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1050">If a single best method cannot be identified, the method invocation is ambiguous, and a binding-time error occurs.</span></span> <span data-ttu-id="04edb-1051">При разрешении перегрузки параметров универсального метода, считаются после замены аргументов типа (предоставленных или выведенных) соответствующие параметры типа метода.</span><span class="sxs-lookup"><span data-stu-id="04edb-1051">When performing overload resolution, the parameters of a generic method are considered after substituting the type arguments (supplied or inferred) for the corresponding method type parameters.</span></span>
*  <span data-ttu-id="04edb-1052">Последняя проверка выбранного лучшего метода выполняется:</span><span class="sxs-lookup"><span data-stu-id="04edb-1052">Final validation of the chosen best method is performed:</span></span>
   * <span data-ttu-id="04edb-1053">Метод проверяется в контексте группы методов: Если лучшим способом является статическим методом, группа методов получилась из *simple_name* или *member_access* через тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1053">The method is validated in the context of the method group: If the best method is a static method, the method group must have resulted from a *simple_name* or a *member_access* through a type.</span></span> <span data-ttu-id="04edb-1054">Если лучший метод является методом экземпляра, группа методов получилась из *simple_name*, *member_access* через переменной или значения, или *base_access*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1054">If the best method is an instance method, the method group must have resulted from a *simple_name*, a *member_access* through a variable or value, or a *base_access*.</span></span> <span data-ttu-id="04edb-1055">Если ни один из этих требований имеет значение true, то возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1055">If neither of these requirements is true, a binding-time error occurs.</span></span>
   * <span data-ttu-id="04edb-1056">Если лучшим способом является универсальным методом, аргументы типа (предоставленных или выведенных) проходят проверку на соответствие ограничениям ([удовлетворяющий ограничениям](types.md#satisfying-constraints)) объявлены в универсальном методе.</span><span class="sxs-lookup"><span data-stu-id="04edb-1056">If the best method is a generic method, the type arguments (supplied or inferred) are checked against the constraints ([Satisfying constraints](types.md#satisfying-constraints)) declared on the generic method.</span></span> <span data-ttu-id="04edb-1057">Если любой аргумент типа не удовлетворяет соответствующим ограничениям для параметра типа, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1057">If any type argument does not satisfy the corresponding constraint(s) on the type parameter, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-1058">После выбора метода и проверены описанные выше действия во время привязки, фактический вызов во время выполнения обрабатывается в соответствии с правилами описано в вызове функции-члена [Проверка динамического разрешения перегрузки во время компиляции ](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1058">Once a method has been selected and validated at binding-time by the above steps, the actual run-time invocation is processed according to the rules of function member invocation described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="04edb-1059">Интуитивно понятный правила разрешения, описанные выше действует следующим образом: Чтобы найти конкретный метод, вызванный при вызове метода, начните с тип, указанный в вызове метода и перейти вверх по цепочке наследования, пока не будет найдено объявление по крайней мере один метод применимо, доступный, отличных от переопределения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1059">The intuitive effect of the resolution rules described above is as follows: To locate the particular method invoked by a method invocation, start with the type indicated by the method invocation and proceed up the inheritance chain until at least one applicable, accessible, non-override method declaration is found.</span></span> <span data-ttu-id="04edb-1060">Затем выполняется вывод типа и разрешение перегрузки для набора применимо, доступный, отличных от переопределения методов, объявленных в типе и вызвать метод выбранный таким образом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1060">Then perform type inference and overload resolution on the set of applicable, accessible, non-override methods declared in that type and invoke the method thus selected.</span></span> <span data-ttu-id="04edb-1061">Если метод не найден, предпринимается попытка обработать вызов в виде вызова метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1061">If no method was found, try instead to process the invocation as an extension method invocation.</span></span>

#### <a name="extension-method-invocations"></a><span data-ttu-id="04edb-1062">Вызовы методов расширения</span><span class="sxs-lookup"><span data-stu-id="04edb-1062">Extension method invocations</span></span>

<span data-ttu-id="04edb-1063">При вызове метода ([вызов в упакованных экземплярах](expressions.md#invocations-on-boxed-instances)) из одной из форм</span><span class="sxs-lookup"><span data-stu-id="04edb-1063">In a method invocation ([Invocations on boxed instances](expressions.md#invocations-on-boxed-instances)) of one of the forms</span></span>
```csharp
expr . identifier ( )

expr . identifier ( args )

expr . identifier < typeargs > ( )

expr . identifier < typeargs > ( args )
```
<span data-ttu-id="04edb-1064">При обычной обработке вызова применимые методы не найдены, будет предпринята попытка обработать конструкцию в виде вызова метода расширения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1064">if the normal processing of the invocation finds no applicable methods, an attempt is made to process the construct as an extension method invocation.</span></span> <span data-ttu-id="04edb-1065">Если *expr* или любой из *args* имеет тип времени компиляции `dynamic`, методы расширения не будут применяться.</span><span class="sxs-lookup"><span data-stu-id="04edb-1065">If *expr* or any of the *args* has compile-time type `dynamic`, extension methods will not apply.</span></span>

<span data-ttu-id="04edb-1066">Целью является найти наиболее *type_name* `C`, таким образом, соответствующим вызовом статического метода могут иметь место:</span><span class="sxs-lookup"><span data-stu-id="04edb-1066">The objective is to find the best *type_name* `C`, so that the corresponding static method invocation can take place:</span></span>
```csharp
C . identifier ( expr )

C . identifier ( expr , args )

C . identifier < typeargs > ( expr )

C . identifier < typeargs > ( expr , args )
```

<span data-ttu-id="04edb-1067">Метод расширения `Ci.Mj` — ***право*** если:</span><span class="sxs-lookup"><span data-stu-id="04edb-1067">An extension method `Ci.Mj` is ***eligible*** if:</span></span>

*  <span data-ttu-id="04edb-1068">`Ci` представляет собой нестандартную невложенными класс</span><span class="sxs-lookup"><span data-stu-id="04edb-1068">`Ci` is a non-generic, non-nested class</span></span>
*  <span data-ttu-id="04edb-1069">Имя `Mj` является *идентификатор*</span><span class="sxs-lookup"><span data-stu-id="04edb-1069">The name of `Mj` is *identifier*</span></span>
*  <span data-ttu-id="04edb-1070">`Mj` доступен и применим, при применении к аргументам, как статический метод, как показано выше</span><span class="sxs-lookup"><span data-stu-id="04edb-1070">`Mj` is accessible and applicable when applied to the arguments as a static method as shown above</span></span>
*  <span data-ttu-id="04edb-1071">Существует неявное идентификаторов, ссылки или упаковки-преобразования *expr* в тип первого параметра `Mj`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1071">An implicit identity, reference or boxing conversion exists from *expr* to the type of the first parameter of `Mj`.</span></span>

<span data-ttu-id="04edb-1072">Поиск `C` продолжается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1072">The search for `C` proceeds as follows:</span></span>

*  <span data-ttu-id="04edb-1073">Начиная с ближайшим включающего объявление пространства имен, продолжая каждого включающего объявления пространства имен и заканчивая содержащую единицу компиляции, последующие попытки найти набор кандидатов методов расширения:</span><span class="sxs-lookup"><span data-stu-id="04edb-1073">Starting with the closest enclosing namespace declaration, continuing with each enclosing namespace declaration, and ending with the containing compilation unit, successive attempts are made to find a candidate set of extension methods:</span></span>
   * <span data-ttu-id="04edb-1074">Если заданного пространства имен или блоке компиляции напрямую содержит объявления неуниверсального типа `Ci` с доступными методами расширения `Mj`, то набор этих методов является набор кандидатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1074">If the given namespace or compilation unit directly contains non-generic type declarations `Ci` with eligible extension methods `Mj`, then the set of those extension methods is the candidate set.</span></span>
   * <span data-ttu-id="04edb-1075">Если типы `Ci` импортировано *using_static_declarations* и непосредственно объявлены в пространствах имен, импортированных с *using_namespace_directive*s в заданного пространства имен или блоке компиляции напрямую содержит методы расширения право `Mj`, то набор этих методов является набор кандидатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1075">If types `Ci` imported by *using_static_declarations* and directly declared in namespaces imported by *using_namespace_directive*s in the given namespace or compilation unit directly contain eligible extension methods `Mj`, then the set of those extension methods is the candidate set.</span></span>
*  <span data-ttu-id="04edb-1076">Если нет набор кандидатов не найден в любой включающего пространства имен объявление или блоке компиляции, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1076">If no candidate set is found in any enclosing namespace declaration or compilation unit, a compile-time error occurs.</span></span>
*  <span data-ttu-id="04edb-1077">В противном случае разрешение перегрузки применяется к набору, как описано в разделе кандидатов ([разрешение перегрузки](expressions.md#overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1077">Otherwise, overload resolution is applied to the candidate set as described in ([Overload resolution](expressions.md#overload-resolution)).</span></span> <span data-ttu-id="04edb-1078">Если один лучший метод не найден, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1078">If no single best method is found, a compile-time error occurs.</span></span>
*  <span data-ttu-id="04edb-1079">`C` — тип, в котором лучший метод объявлен как метод расширения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1079">`C` is the type within which the best method is declared as an extension method.</span></span>

<span data-ttu-id="04edb-1080">С помощью `C` как целевой объект вызова метода затем обрабатывается как вызов статического метода ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1080">Using `C` as a target, the method call is then processed as a static method invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span>

<span data-ttu-id="04edb-1081">Указанные выше правила означают, что методы экземпляра имеют приоритет по сравнению с методами расширения, что методы расширения, доступные в объявлениях внутреннее пространство имен имеют приоритет над методы расширения, доступные в внешних объявлениях пространств имен и это расширение методы, объявленные непосредственно в пространстве имен имеют приоритет по сравнению с методами расширения, импортируются в этом же пространстве имен с помощью директивы пространства имен.</span><span class="sxs-lookup"><span data-stu-id="04edb-1081">The preceding rules mean that instance methods take precedence over extension methods, that extension methods available in inner namespace declarations take precedence over extension methods available in outer namespace declarations, and that extension methods declared directly in a namespace take precedence over extension methods imported into that same namespace with a using namespace directive.</span></span> <span data-ttu-id="04edb-1082">Пример:</span><span class="sxs-lookup"><span data-stu-id="04edb-1082">For example:</span></span>
```csharp
public static class E
{
    public static void F(this object obj, int i) { }

    public static void F(this object obj, string s) { }
}

class A { }

class B
{
    public void F(int i) { }
}

class C
{
    public void F(object obj) { }
}

class X
{
    static void Test(A a, B b, C c) {
        a.F(1);              // E.F(object, int)
        a.F("hello");        // E.F(object, string)

        b.F(1);              // B.F(int)
        b.F("hello");        // E.F(object, string)

        c.F(1);              // C.F(object)
        c.F("hello");        // C.F(object)
    }
}
```

<span data-ttu-id="04edb-1083">В примере `B`метод имеет приоритет над первый метод расширения, и `C`метод имеет приоритет над обоими методами расширения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1083">In the example, `B`'s method takes precedence over the first extension method, and `C`'s method takes precedence over both extension methods.</span></span>

```csharp
public static class C
{
    public static void F(this int i) { Console.WriteLine("C.F({0})", i); }
    public static void G(this int i) { Console.WriteLine("C.G({0})", i); }
    public static void H(this int i) { Console.WriteLine("C.H({0})", i); }
}

namespace N1
{
    public static class D
    {
        public static void F(this int i) { Console.WriteLine("D.F({0})", i); }
        public static void G(this int i) { Console.WriteLine("D.G({0})", i); }
    }
}

namespace N2
{
    using N1;

    public static class E
    {
        public static void F(this int i) { Console.WriteLine("E.F({0})", i); }
    }

    class Test
    {
        static void Main(string[] args)
        {
            1.F();
            2.G();
            3.H();
        }
    }
}
```

<span data-ttu-id="04edb-1084">Выходные данные этого примера является:</span><span class="sxs-lookup"><span data-stu-id="04edb-1084">The output of this example is:</span></span>
```
E.F(1)
D.G(2)
C.H(3)
```
<span data-ttu-id="04edb-1085">`D.G` имеет приоритет над `C.G`, и `E.F` имеет приоритет над оба `D.F` и `C.F`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1085">`D.G` takes precedence over `C.G`, and `E.F` takes precedence over both `D.F` and `C.F`.</span></span>

#### <a name="delegate-invocations"></a><span data-ttu-id="04edb-1086">Вызовы делегатов</span><span class="sxs-lookup"><span data-stu-id="04edb-1086">Delegate invocations</span></span>

<span data-ttu-id="04edb-1087">Для вызова делегата *primary_expression* из *invocation_expression* должно быть значение *delegate_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1087">For a delegate invocation, the *primary_expression* of the *invocation_expression* must be a value of a *delegate_type*.</span></span> <span data-ttu-id="04edb-1088">Кроме того, учитывая *delegate_type* быть функция-член с такой же список параметров, как *delegate_type*, *delegate_type* должно быть применимо () [Применимого члена функции](expressions.md#applicable-function-member)) по отношению к *argument_list* из *invocation_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1088">Furthermore, considering the *delegate_type* to be a function member with the same parameter list as the *delegate_type*, the *delegate_type* must be applicable ([Applicable function member](expressions.md#applicable-function-member)) with respect to the *argument_list* of the *invocation_expression*.</span></span>

<span data-ttu-id="04edb-1089">Обработка времени выполнения вызова делегата формы `D(A)`, где `D` — *primary_expression* из *delegate_type* и `A` является необязательным *argument_list*, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1089">The run-time processing of a delegate invocation of the form `D(A)`, where `D` is a *primary_expression* of a *delegate_type* and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-1090">`D` выполняется оценка.</span><span class="sxs-lookup"><span data-stu-id="04edb-1090">`D` is evaluated.</span></span> <span data-ttu-id="04edb-1091">Если эта оценка вызывает исключение, никакие дополнительные действия выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1091">If this evaluation causes an exception, no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1092">Значение `D` проверяется, чтобы быть допустимыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-1092">The value of `D` is checked to be valid.</span></span> <span data-ttu-id="04edb-1093">Если значение `D` — `null`, `System.NullReferenceException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1093">If the value of `D` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1094">В противном случае `D` является ссылкой на экземпляр делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1094">Otherwise, `D` is a reference to a delegate instance.</span></span> <span data-ttu-id="04edb-1095">Вызовы функций-членов ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) выполняются на каждом из вызываемые объекты в списке вызова делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1095">Function member invocations ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) are performed on each of the callable entities in the invocation list of the delegate.</span></span> <span data-ttu-id="04edb-1096">Для вызываемых сущностей, состоящих из экземпляра и метод экземпляра экземпляр для вызова является экземпляром, содержащимся в вызываемая сущность.</span><span class="sxs-lookup"><span data-stu-id="04edb-1096">For callable entities consisting of an instance and instance method, the instance for the invocation is the instance contained in the callable entity.</span></span>

### <a name="element-access"></a><span data-ttu-id="04edb-1097">Доступ к элементам</span><span class="sxs-lookup"><span data-stu-id="04edb-1097">Element access</span></span>

<span data-ttu-id="04edb-1098">*Element_access* состоит из *primary_no_array_creation_expression*, за которым следует "`[`" токена, за которым следует *argument_list*, за которым следует " `]`«token.</span><span class="sxs-lookup"><span data-stu-id="04edb-1098">An *element_access* consists of a *primary_no_array_creation_expression*, followed by a "`[`" token, followed by an *argument_list*, followed by a "`]`" token.</span></span> <span data-ttu-id="04edb-1099">*Argument_list* состоит из одного или нескольких *аргумент*s, разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-1099">The *argument_list* consists of one or more *argument*s, separated by commas.</span></span>

```antlr
element_access
    : primary_no_array_creation_expression '[' expression_list ']'
    ;
```

<span data-ttu-id="04edb-1100">*Argument_list* из *element_access* не может содержать `ref` или `out` аргументы.</span><span class="sxs-lookup"><span data-stu-id="04edb-1100">The *argument_list* of an *element_access* is not allowed to contain `ref` or `out` arguments.</span></span>

<span data-ttu-id="04edb-1101">*Element_access* является динамическим ([динамической привязки](expressions.md#dynamic-binding)) Если содержит по крайней мере одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-1101">An *element_access* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)) if at least one of the following holds:</span></span>

* <span data-ttu-id="04edb-1102">*Primary_no_array_creation_expression* имеет тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1102">The *primary_no_array_creation_expression* has compile-time type `dynamic`.</span></span>
* <span data-ttu-id="04edb-1103">По крайней мере одно выражение *argument_list* имеет тип времени компиляции `dynamic` и *primary_no_array_creation_expression* не поддерживает тип массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-1103">At least one expression of the *argument_list* has compile-time type `dynamic` and the *primary_no_array_creation_expression* does not have an array type.</span></span>

<span data-ttu-id="04edb-1104">В этом случае компилятор классифицирует *element_access* как значение типа `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1104">In this case the compiler classifies the *element_access* as a value of type `dynamic`.</span></span> <span data-ttu-id="04edb-1105">Правила для определения значения *element_access* применяются во время выполнения, используя тип времени выполнения вместо компиляции типа *primary_no_array_creation_expression*и *argument_list* выражения, которые имеют тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1105">The rules below to determine the meaning of the *element_access* are then applied at run-time, using the run-time type instead of the compile-time type of those of the *primary_no_array_creation_expression* and *argument_list* expressions which have the compile-time type `dynamic`.</span></span> <span data-ttu-id="04edb-1106">Если *primary_no_array_creation_expression* не имеет типа во время компиляции `dynamic`, то доступ к элементам выполнена ограниченная проверка времени компиляции, как описано в разделе [проверка динамической компиляции разрешение перегрузки](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1106">If the *primary_no_array_creation_expression* does not have compile-time type `dynamic`, then the element access undergoes a limited compile time check as described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="04edb-1107">Если *primary_no_array_creation_expression* из *element_access* представляет собой значение *array_type*, *element_access* — Массив доступа ([массива доступа](expressions.md#array-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1107">If the *primary_no_array_creation_expression* of an *element_access* is a value of an *array_type*, the *element_access* is an array access ([Array access](expressions.md#array-access)).</span></span> <span data-ttu-id="04edb-1108">В противном случае *primary_no_array_creation_expression* должно быть переменной или значения из класса, структуры или тип интерфейса, который содержит один или несколько членов индексатора, в этом случае *element_access* — доступ к индексатору ([доступа к индексатору](expressions.md#indexer-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1108">Otherwise, the *primary_no_array_creation_expression* must be a variable or value of a class, struct, or interface type that has one or more indexer members, in which case the *element_access* is an indexer access ([Indexer access](expressions.md#indexer-access)).</span></span>

#### <a name="array-access"></a><span data-ttu-id="04edb-1109">Доступ к массиву</span><span class="sxs-lookup"><span data-stu-id="04edb-1109">Array access</span></span>

<span data-ttu-id="04edb-1110">Для доступа к массиву *primary_no_array_creation_expression* из *element_access* должно быть значение *array_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1110">For an array access, the *primary_no_array_creation_expression* of the *element_access* must be a value of an *array_type*.</span></span> <span data-ttu-id="04edb-1111">Кроме того *argument_list* массива не разрешен доступ должен содержать именованные аргументы. Количество выражений в *argument_list* должен быть таким же, как ранг *array_type*, и каждое выражение должно иметь тип `int`, `uint`, `long`, `ulong`, или должен неявно преобразовываться в один или несколько из этих типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1111">Furthermore, the *argument_list* of an array access is not allowed to contain named arguments.The number of expressions in the *argument_list* must be the same as the rank of the *array_type*, and each expression must be of type `int`, `uint`, `long`, `ulong`, or must be implicitly convertible to one or more of these types.</span></span>

<span data-ttu-id="04edb-1112">Результат вычисления доступа к массиву является переменной типа элемента массива, а именно элемент массива, выбранный по значениям выражений в *argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1112">The result of evaluating an array access is a variable of the element type of the array, namely the array element selected by the value(s) of the expression(s) in the *argument_list*.</span></span>

<span data-ttu-id="04edb-1113">Обработка времени выполнения доступа к массиву формы `P[A]`, где `P` — *primary_no_array_creation_expression* из *array_type* и `A` является *argument_list*, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1113">The run-time processing of an array access of the form `P[A]`, where `P` is a *primary_no_array_creation_expression* of an *array_type* and `A` is an *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-1114">`P` выполняется оценка.</span><span class="sxs-lookup"><span data-stu-id="04edb-1114">`P` is evaluated.</span></span> <span data-ttu-id="04edb-1115">Если эта оценка вызывает исключение, никакие дополнительные действия выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1115">If this evaluation causes an exception, no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1116">Выражения индекса *argument_list* вычисляются в порядке слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-1116">The index expressions of the *argument_list* are evaluated in order, from left to right.</span></span> <span data-ttu-id="04edb-1117">После вычисления каждого выражения индекса, неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) выполняется одно из следующих типов: `int`, `uint`, `long`, `ulong`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1117">Following evaluation of each index expression, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) to one of the following types is performed: `int`, `uint`, `long`, `ulong`.</span></span> <span data-ttu-id="04edb-1118">Будет выбран первый тип, в этом списке, для которого существует неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="04edb-1118">The first type in this list for which an implicit conversion exists is chosen.</span></span> <span data-ttu-id="04edb-1119">Например если выражение индекса имеет тип `short` затем неявное преобразование в `int` выполняется, так как неявные преобразования из `short` для `int` и из `short` для `long` возможны.</span><span class="sxs-lookup"><span data-stu-id="04edb-1119">For instance, if the index expression is of type `short` then an implicit conversion to `int` is performed, since implicit conversions from `short` to `int` and from `short` to `long` are possible.</span></span> <span data-ttu-id="04edb-1120">При вычислении выражения индекса или последующих неявное преобразование возникает исключение, оцениваются следующие выражения индекса, и дальнейшие действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1120">If evaluation of an index expression or the subsequent implicit conversion causes an exception, then no further index expressions are evaluated and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1121">Значение `P` проверяется, чтобы быть допустимыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-1121">The value of `P` is checked to be valid.</span></span> <span data-ttu-id="04edb-1122">Если значение `P` — `null`, `System.NullReferenceException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1122">If the value of `P` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1123">Значение каждого выражения в *argument_list* проверяются на соответствие фактические границы каждого измерения массива экземпляра массива, `P`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1123">The value of each expression in the *argument_list* is checked against the actual bounds of each dimension of the array instance referenced by `P`.</span></span> <span data-ttu-id="04edb-1124">Если одно или несколько значений выходят за пределы диапазона, `System.IndexOutOfRangeException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1124">If one or more values are out of range, a `System.IndexOutOfRangeException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1125">Расположение элемента массива, заданного выражениями индекса является вычисляемым, и оно становится результатом доступ к массиву.</span><span class="sxs-lookup"><span data-stu-id="04edb-1125">The location of the array element given by the index expression(s) is computed, and this location becomes the result of the array access.</span></span>

#### <a name="indexer-access"></a><span data-ttu-id="04edb-1126">Доступ к индексатору</span><span class="sxs-lookup"><span data-stu-id="04edb-1126">Indexer access</span></span>

<span data-ttu-id="04edb-1127">Для доступа к индексатору *primary_no_array_creation_expression* из *element_access* должно быть переменной или значения из класса, структуры или тип интерфейса, и этот тип должен реализовывать один или несколько индексаторы, которые можно использовать по отношению к *argument_list* из *element_access*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1127">For an indexer access, the *primary_no_array_creation_expression* of the *element_access* must be a variable or value of a class, struct, or interface type, and this type must implement one or more indexers that are applicable with respect to the *argument_list* of the *element_access*.</span></span>

<span data-ttu-id="04edb-1128">Обработка времени привязки доступа к индексатору формы `P[A]`, где `P` — *primary_no_array_creation_expression* класса, структуры или тип интерфейса `T`, и `A` — *argument_list*, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1128">The binding-time processing of an indexer access of the form `P[A]`, where `P` is a *primary_no_array_creation_expression* of a class, struct, or interface type `T`, and `A` is an *argument_list*, consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-1129">Набор индексаторов, предоставляемых `T` создается.</span><span class="sxs-lookup"><span data-stu-id="04edb-1129">The set of indexers provided by `T` is constructed.</span></span> <span data-ttu-id="04edb-1130">Набор состоит из всех индексаторов, объявленных в `T` или базовый тип `T` , которые не являются `override` объявления и доступны в текущем контексте ([доступ к членам](basic-concepts.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1130">The set consists of all indexers declared in `T` or a base type of `T` that are not `override` declarations and are accessible in the current context ([Member access](basic-concepts.md#member-access)).</span></span>
*  <span data-ttu-id="04edb-1131">Набор уменьшается до индексаторов, которые применимы и не скрыты другими индексаторами.</span><span class="sxs-lookup"><span data-stu-id="04edb-1131">The set is reduced to those indexers that are applicable and not hidden by other indexers.</span></span> <span data-ttu-id="04edb-1132">Следующие правила применяются для каждого индексатора `S.I` в наборе, где `S` — это тип, в которой индексатор `I` объявляется:</span><span class="sxs-lookup"><span data-stu-id="04edb-1132">The following rules are applied to each indexer `S.I` in the set, where `S` is the type in which the indexer `I` is declared:</span></span>
   * <span data-ttu-id="04edb-1133">Если `I` не применяется по отношению к `A` ([применимого члена функции](expressions.md#applicable-function-member)), затем `I` удаляется из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1133">If `I` is not applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)), then `I` is removed from the set.</span></span>
   * <span data-ttu-id="04edb-1134">Если `I` применяется по отношению к `A` ([применимого члена функции](expressions.md#applicable-function-member)), затем всех индексаторов, объявленных в базовом типе `S` удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1134">If `I` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)), then all indexers declared in a base type of `S` are removed from the set.</span></span>
   * <span data-ttu-id="04edb-1135">Если `I` применяется по отношению к `A` ([применимого члена функции](expressions.md#applicable-function-member)) и `S` не является типом класса `object`, всех индексаторов, объявленных в интерфейсе, удаляются из набора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1135">If `I` is applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)) and `S` is a class type other than `object`, all indexers declared in an interface are removed from the set.</span></span>
*  <span data-ttu-id="04edb-1136">Если результирующий набор индексаторов-кандидатов пуст, то существовать нет применимых индексаторов, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1136">If the resulting set of candidate indexers is empty, then no applicable indexers exist, and a binding-time error occurs.</span></span>
*  <span data-ttu-id="04edb-1137">Лучший индексатор из набора индексаторов-кандидатов определяется с помощью правил разрешения перегрузки [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1137">The best indexer of the set of candidate indexers is identified using the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="04edb-1138">Если не удается определить лучший один индексатор, доступа к индексатору является неоднозначным, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1138">If a single best indexer cannot be identified, the indexer access is ambiguous, and a binding-time error occurs.</span></span>
*  <span data-ttu-id="04edb-1139">Выражения индекса *argument_list* вычисляются в порядке слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-1139">The index expressions of the *argument_list* are evaluated in order, from left to right.</span></span> <span data-ttu-id="04edb-1140">Результат обработки доступа к индексатору — это выражение, которые классифицируются как доступ к индексатору.</span><span class="sxs-lookup"><span data-stu-id="04edb-1140">The result of processing the indexer access is an expression classified as an indexer access.</span></span> <span data-ttu-id="04edb-1141">Выражения доступа к индексатору ссылается на индексатор, определенный на предыдущем шаге и имеет связанное выражение экземпляра из `P` и связанный список аргументов из `A`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1141">The indexer access expression references the indexer determined in the step above, and has an associated instance expression of `P` and an associated argument list of `A`.</span></span>

<span data-ttu-id="04edb-1142">В зависимости от контекста, в котором оно использовано, доступ к индексатору приводит вызов либо *метод доступа get* или *метода доступа set* индексатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1142">Depending on the context in which it is used, an indexer access causes invocation of either the *get accessor* or the *set accessor* of the indexer.</span></span> <span data-ttu-id="04edb-1143">Если доступ к индексатору является целевым объектом назначения, *метода доступа set* вызывается для присвоения нового значения ([простое присваивание](expressions.md#simple-assignment)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1143">If the indexer access is the target of an assignment, the *set accessor* is invoked to assign a new value ([Simple assignment](expressions.md#simple-assignment)).</span></span> <span data-ttu-id="04edb-1144">Во всех остальных случаях *метод доступа get* вызывается для получения текущего значения ([значения выражений](expressions.md#values-of-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1144">In all other cases, the *get accessor* is invoked to obtain the current value ([Values of expressions](expressions.md#values-of-expressions)).</span></span>

### <a name="this-access"></a><span data-ttu-id="04edb-1145">Такой доступ</span><span class="sxs-lookup"><span data-stu-id="04edb-1145">This access</span></span>

<span data-ttu-id="04edb-1146">Объект *this_access* состоит из ключевого слова `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1146">A *this_access* consists of the reserved word `this`.</span></span>

```antlr
this_access
    : 'this'
    ;
```

<span data-ttu-id="04edb-1147">Объект *this_access* допускается только в *блок* конструктор экземпляра, методе экземпляра или метода доступа к экземпляру.</span><span class="sxs-lookup"><span data-stu-id="04edb-1147">A *this_access* is permitted only in the *block* of an instance constructor, an instance method, or an instance accessor.</span></span> <span data-ttu-id="04edb-1148">Он имеет одно из следующих значений:</span><span class="sxs-lookup"><span data-stu-id="04edb-1148">It has one of the following meanings:</span></span>

*  <span data-ttu-id="04edb-1149">Когда `this` используется в *primary_expression* внутри конструктора экземпляра класса, он классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1149">When `this` is used in a *primary_expression* within an instance constructor of a class, it is classified as a value.</span></span> <span data-ttu-id="04edb-1150">Тип значения имеет тип экземпляра ([тип экземпляра](classes.md#the-instance-type)) класса, в котором происходит это использование, и значение является ссылкой на создаваемый объект.</span><span class="sxs-lookup"><span data-stu-id="04edb-1150">The type of the value is the instance type ([The instance type](classes.md#the-instance-type)) of the class within which the usage occurs, and the value is a reference to the object being constructed.</span></span>
*  <span data-ttu-id="04edb-1151">Когда `this` используется в *primary_expression* внутри метода экземпляра или методе доступа экземпляра класса, он классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1151">When `this` is used in a *primary_expression* within an instance method or instance accessor of a class, it is classified as a value.</span></span> <span data-ttu-id="04edb-1152">Тип значения имеет тип экземпляра ([тип экземпляра](classes.md#the-instance-type)) класса, в котором происходит это использование, и значение является ссылкой на объект, для которого был вызван метод или метод доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1152">The type of the value is the instance type ([The instance type](classes.md#the-instance-type)) of the class within which the usage occurs, and the value is a reference to the object for which the method or accessor was invoked.</span></span>
*  <span data-ttu-id="04edb-1153">Когда `this` используется в *primary_expression* внутри конструктора экземпляра структуры, он классифицируется как переменная.</span><span class="sxs-lookup"><span data-stu-id="04edb-1153">When `this` is used in a *primary_expression* within an instance constructor of a struct, it is classified as a variable.</span></span> <span data-ttu-id="04edb-1154">Тип переменной является тип экземпляра ([тип экземпляра](classes.md#the-instance-type)) в течение которого происходит это использование, а переменная представляет структуры структуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-1154">The type of the variable is the instance type ([The instance type](classes.md#the-instance-type)) of the struct within which the usage occurs, and the variable represents the struct being constructed.</span></span> <span data-ttu-id="04edb-1155">`this` Переменной конструктора экземпляра структуры ведет себя так же, как `out` параметр типа структуры — в частности, это означает, что переменной должен быть явно присвоен в каждом пути исполнения экземпляра конструктор.</span><span class="sxs-lookup"><span data-stu-id="04edb-1155">The `this` variable of an instance constructor of a struct behaves exactly the same as an `out` parameter of the struct type—in particular, this means that the variable must be definitely assigned in every execution path of the instance constructor.</span></span>
*  <span data-ttu-id="04edb-1156">Когда `this` используется в *primary_expression* внутри метода экземпляра или методе доступа экземпляра структуры, он классифицируется как переменная.</span><span class="sxs-lookup"><span data-stu-id="04edb-1156">When `this` is used in a *primary_expression* within an instance method or instance accessor of a struct, it is classified as a variable.</span></span> <span data-ttu-id="04edb-1157">Тип переменной является тип экземпляра ([тип экземпляра](classes.md#the-instance-type)) структуры, в котором осуществляется использование.</span><span class="sxs-lookup"><span data-stu-id="04edb-1157">The type of the variable is the instance type ([The instance type](classes.md#the-instance-type)) of the struct within which the usage occurs.</span></span>
   * <span data-ttu-id="04edb-1158">Если метод или метод доступа не является итератором ([итераторы](classes.md#iterators)), `this` переменная представляет структуру, для которого был вызван метод или метод доступа и ведет себя так же, как `ref` параметр типа структуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-1158">If the method or accessor is not an iterator ([Iterators](classes.md#iterators)), the `this` variable represents the struct for which the method or accessor was invoked, and behaves exactly the same as a `ref` parameter of the struct type.</span></span>
   * <span data-ttu-id="04edb-1159">Если метод или метод доступа является итератором, `this` переменная представляет копию структуры, для которого был вызван метод или метод доступа и ведет себя так же, как значение параметра типа структуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-1159">If the method or accessor is an iterator, the `this` variable represents a copy of the struct for which the method or accessor was invoked, and behaves exactly the same as a value parameter of the struct type.</span></span>

<span data-ttu-id="04edb-1160">Использование `this` в *primary_expression* в контексте, отличном от приведенных выше является ошибкой во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1160">Use of `this` in a *primary_expression* in a context other than the ones listed above is a compile-time error.</span></span> <span data-ttu-id="04edb-1161">В частности, это не можно будет ссылаться в `this` в статический метод, метод доступа статического свойства, или в *variable_initializer* объявления поля.</span><span class="sxs-lookup"><span data-stu-id="04edb-1161">In particular, it is not possible to refer to `this` in a static method, a static property accessor, or in a *variable_initializer* of a field declaration.</span></span>

### <a name="base-access"></a><span data-ttu-id="04edb-1162">Доступ к базовым членам</span><span class="sxs-lookup"><span data-stu-id="04edb-1162">Base access</span></span>

<span data-ttu-id="04edb-1163">Объект *base_access* состоит из ключевого слова `base` следуют либо "`.`" токена и идентификатор или значение *argument_list* заключенная в квадратные скобки:</span><span class="sxs-lookup"><span data-stu-id="04edb-1163">A *base_access* consists of the reserved word `base` followed by either a "`.`" token and an identifier or an *argument_list* enclosed in square brackets:</span></span>

```antlr
base_access
    : 'base' '.' identifier
    | 'base' '[' expression_list ']'
    ;
```

<span data-ttu-id="04edb-1164">Объект *base_access* используется для доступа к членам базового класса, которые скрыты с такими же именами в текущем классе или структуре.</span><span class="sxs-lookup"><span data-stu-id="04edb-1164">A *base_access* is used to access base class members that are hidden by similarly named members in the current class or struct.</span></span> <span data-ttu-id="04edb-1165">Объект *base_access* допускается только в *блок* конструктор экземпляра, методе экземпляра или метода доступа к экземпляру.</span><span class="sxs-lookup"><span data-stu-id="04edb-1165">A *base_access* is permitted only in the *block* of an instance constructor, an instance method, or an instance accessor.</span></span> <span data-ttu-id="04edb-1166">Когда `base.I` происходит в классе или структуре, `I` должно обозначать член базового класса этого класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-1166">When `base.I` occurs in a class or struct, `I` must denote a member of the base class of that class or struct.</span></span> <span data-ttu-id="04edb-1167">Аналогичным образом, если `base[E]` происходит в классе, применимый индексатор должен существовать в базовом классе.</span><span class="sxs-lookup"><span data-stu-id="04edb-1167">Likewise, when `base[E]` occurs in a class, an applicable indexer must exist in the base class.</span></span>

<span data-ttu-id="04edb-1168">Во время привязки *base_access* выражения формы `base.I` и `base[E]` вычисляются точно так же, как если бы они были написаны `((B)this).I` и `((B)this)[E]`, где `B` является базовым классом класса или структуры, в котором находится эта конструкция.</span><span class="sxs-lookup"><span data-stu-id="04edb-1168">At binding-time, *base_access* expressions of the form `base.I` and `base[E]` are evaluated exactly as if they were written `((B)this).I` and `((B)this)[E]`, where `B` is the base class of the class or struct in which the construct occurs.</span></span> <span data-ttu-id="04edb-1169">Таким образом `base.I` и `base[E]` соответствуют `this.I` и `this[E]`, за исключением `this` рассматривается как экземпляр базового класса.</span><span class="sxs-lookup"><span data-stu-id="04edb-1169">Thus, `base.I` and `base[E]` correspond to `this.I` and `this[E]`, except `this` is viewed as an instance of the base class.</span></span>

<span data-ttu-id="04edb-1170">Когда *base_access* ссылается на элемент виртуальной функции (метода, свойства или индексатора), определение которого функции-члена для вызова во время выполнения ([Проверка динамического разрешения перегрузки во время компиляции ](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) изменяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1170">When a *base_access* references a virtual function member (a method, property, or indexer), the determination of which function member to invoke at run-time ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)) is changed.</span></span> <span data-ttu-id="04edb-1171">Функцию-член, вызываемая определяется путем нахождения наиболее производной реализацией ([виртуальных методов](classes.md#virtual-methods)) члена функции по отношению к `B` (а не по отношению к тип времени выполнения `this`, как бы обычным в системе счисления с основанием доступ).</span><span class="sxs-lookup"><span data-stu-id="04edb-1171">The function member that is invoked is determined by finding the most derived implementation ([Virtual methods](classes.md#virtual-methods)) of the function member with respect to `B` (instead of with respect to the run-time type of `this`, as would be usual in a non-base access).</span></span> <span data-ttu-id="04edb-1172">Таким образом, в пределах `override` из `virtual` функции-члена *base_access* может использоваться для вызова унаследованной реализации функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-1172">Thus, within an `override` of a `virtual` function member, a *base_access* can be used to invoke the inherited implementation of the function member.</span></span> <span data-ttu-id="04edb-1173">Если функция-член, на который ссылается *base_access* является абстрактным, возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1173">If the function member referenced by a *base_access* is abstract, a binding-time error occurs.</span></span>

### <a name="postfix-increment-and-decrement-operators"></a><span data-ttu-id="04edb-1174">Постфиксных инкремента и декремента</span><span class="sxs-lookup"><span data-stu-id="04edb-1174">Postfix increment and decrement operators</span></span>

```antlr
post_increment_expression
    : primary_expression '++'
    ;

post_decrement_expression
    : primary_expression '--'
    ;
```

<span data-ttu-id="04edb-1175">Операнд постфиксного инкремента или декремента должен быть выражением, классифицируется как переменная, доступ к свойству или индексатору.</span><span class="sxs-lookup"><span data-stu-id="04edb-1175">The operand of a postfix increment or decrement operation must be an expression classified as a variable, a property access, or an indexer access.</span></span> <span data-ttu-id="04edb-1176">Результат операции является значение совпадает с типом операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1176">The result of the operation is a value of the same type as the operand.</span></span>

<span data-ttu-id="04edb-1177">Если *primary_expression* имеет тип времени компиляции `dynamic` , а затем оператор является динамическим ([динамической привязки](expressions.md#dynamic-binding)), *post_increment_expression*или *post_decrement_expression* имеет тип времени компиляции `dynamic` и следующие правила применяются во время выполнения, используя тип среды выполнения *primary_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1177">If the *primary_expression* has the compile-time type `dynamic` then the operator is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)), the *post_increment_expression* or *post_decrement_expression* has the compile-time type `dynamic` and the following rules are applied at run-time using the run-time type of the *primary_expression*.</span></span>

<span data-ttu-id="04edb-1178">Если увеличить Операнд постфиксного оператора декремента является свойство или индексатор, свойство или индексатор должны иметь `get` и `set` метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1178">If the operand of a postfix increment or decrement operation is a property or indexer access, the property or indexer must have both a `get` and a `set` accessor.</span></span> <span data-ttu-id="04edb-1179">Если это не так, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1179">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-1180">Разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1180">Unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1181">Предопределенные `++` и `--` операторов существуют для следующих типов: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` , `float`, `double`, `decimal`и любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-1181">Predefined `++` and `--` operators exist for the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, and any enum type.</span></span> <span data-ttu-id="04edb-1182">Предопределенный `++` операторы возвращают значение, полученное путем прибавления единицы к операнд и предварительно определенных `--` операторы возвращают значение, полученное путем вычитания 1 из операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1182">The predefined `++` operators return the value produced by adding 1 to the operand, and the predefined `--` operators return the value produced by subtracting 1 from the operand.</span></span> <span data-ttu-id="04edb-1183">В `checked` контекста, если результат сложения или вычитания находится вне диапазона типа результата, а тип результата — целый тип или тип перечисления, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1183">In a `checked` context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a `System.OverflowException` is thrown.</span></span>

<span data-ttu-id="04edb-1184">Во время выполнения обработки Постфиксный инкремент или операция формы декремента `x++` или `x--` состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1184">The run-time processing of a postfix increment or decrement operation of the form `x++` or `x--` consists of the following steps:</span></span>

*   <span data-ttu-id="04edb-1185">Если `x` классифицируется как переменная:</span><span class="sxs-lookup"><span data-stu-id="04edb-1185">If `x` is classified as a variable:</span></span>
    * <span data-ttu-id="04edb-1186">`x` вычисляется для создания переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-1186">`x` is evaluated to produce the variable.</span></span>
    * <span data-ttu-id="04edb-1187">Значение `x` сохраняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1187">The value of `x` is saved.</span></span>
    * <span data-ttu-id="04edb-1188">Выбранный оператор вызывается с сохраненным значением `x` аргументом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1188">The selected operator is invoked with the saved value of `x` as its argument.</span></span>
    * <span data-ttu-id="04edb-1189">Значение, возвращаемое оператором хранится в расположении, указанном при вычислении `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1189">The value returned by the operator is stored in the location given by the evaluation of `x`.</span></span>
    * <span data-ttu-id="04edb-1190">Сохраненное значение `x` становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1190">The saved value of `x` becomes the result of the operation.</span></span>
*   <span data-ttu-id="04edb-1191">Если `x` классифицируется как свойство или индексатор доступа:</span><span class="sxs-lookup"><span data-stu-id="04edb-1191">If `x` is classified as a property or indexer access:</span></span>
    * <span data-ttu-id="04edb-1192">Выражение экземпляра (если `x` не `static`) и список аргументов (если `x` имеет доступ к индексатору) связан `x` оцениваются, и полученные результаты используются в последующих `get` и `set` вызовы метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1192">The instance expression (if `x` is not `static`) and the argument list (if `x` is an indexer access) associated with `x` are evaluated, and the results are used in the subsequent `get` and `set` accessor invocations.</span></span>
    * <span data-ttu-id="04edb-1193">`get` Метод доступа `x` вызывается и возвращаемое значение сохраняется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1193">The `get` accessor of `x` is invoked and the returned value is saved.</span></span>
    * <span data-ttu-id="04edb-1194">Выбранный оператор вызывается с сохраненным значением `x` аргументом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1194">The selected operator is invoked with the saved value of `x` as its argument.</span></span>
    * <span data-ttu-id="04edb-1195">`set` Метод доступа `x` вызывается со значением, возвращенным оператором в качестве его `value` аргумент.</span><span class="sxs-lookup"><span data-stu-id="04edb-1195">The `set` accessor of `x` is invoked with the value returned by the operator as its `value` argument.</span></span>
    * <span data-ttu-id="04edb-1196">Сохраненное значение `x` становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1196">The saved value of `x` becomes the result of the operation.</span></span>

<span data-ttu-id="04edb-1197">`++` И `--` операторы также поддерживают префикса ([префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1197">The `++` and `--` operators also support prefix notation ([Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)).</span></span> <span data-ttu-id="04edb-1198">Как правило, результат `x++` или `x--` является значением `x` до операции, тогда как результат `++x` или `--x` является значением `x` после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1198">Typically, the result of `x++` or `x--` is the value of `x` before the operation, whereas the result of `++x` or `--x` is the value of `x` after the operation.</span></span> <span data-ttu-id="04edb-1199">В любом случае `x` сам имеет то же значение после выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1199">In either case, `x` itself has the same value after the operation.</span></span>

<span data-ttu-id="04edb-1200">`operator ++` Или `operator --` реализации можно вызывать в префиксной и постфиксной форме.</span><span class="sxs-lookup"><span data-stu-id="04edb-1200">An `operator ++` or `operator --` implementation can be invoked using either postfix or prefix notation.</span></span> <span data-ttu-id="04edb-1201">Это не могут существовать разные реализации операторов для обозначения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1201">It is not possible to have separate operator implementations for the two notations.</span></span>

### <a name="the-new-operator"></a><span data-ttu-id="04edb-1202">Оператор new</span><span class="sxs-lookup"><span data-stu-id="04edb-1202">The new operator</span></span>

<span data-ttu-id="04edb-1203">`new` Оператор используется для создания новых экземпляров типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1203">The `new` operator is used to create new instances of types.</span></span>

<span data-ttu-id="04edb-1204">Существует три формы `new` выражения:</span><span class="sxs-lookup"><span data-stu-id="04edb-1204">There are three forms of `new` expressions:</span></span>

*  <span data-ttu-id="04edb-1205">Выражения создания объектов используются для создания новых экземпляров типов классов и типов значений.</span><span class="sxs-lookup"><span data-stu-id="04edb-1205">Object creation expressions are used to create new instances of class types and value types.</span></span>
*  <span data-ttu-id="04edb-1206">Выражения создания массива используются для создания новых экземпляров типов массивов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1206">Array creation expressions are used to create new instances of array types.</span></span>
*  <span data-ttu-id="04edb-1207">Выражения создания делегата используются для создания новых экземпляров делегатов типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1207">Delegate creation expressions are used to create new instances of delegate types.</span></span>

<span data-ttu-id="04edb-1208">`new` Оператор подразумевает создание экземпляра типа, но не подразумевает динамическое выделение памяти.</span><span class="sxs-lookup"><span data-stu-id="04edb-1208">The `new` operator implies creation of an instance of a type, but does not necessarily imply dynamic allocation of memory.</span></span> <span data-ttu-id="04edb-1209">В частности, экземпляры типов значений не требуют дополнительной памяти за пределами переменных, в которых они находятся, и динамическое распределение не происходит при `new` используется для создания экземпляров типов значений.</span><span class="sxs-lookup"><span data-stu-id="04edb-1209">In particular, instances of value types require no additional memory beyond the variables in which they reside, and no dynamic allocations occur when `new` is used to create instances of value types.</span></span>

#### <a name="object-creation-expressions"></a><span data-ttu-id="04edb-1210">Выражения создания объектов</span><span class="sxs-lookup"><span data-stu-id="04edb-1210">Object creation expressions</span></span>

<span data-ttu-id="04edb-1211">*Object_creation_expression* используется для создания нового экземпляра *class_type* или *value_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1211">An *object_creation_expression* is used to create a new instance of a *class_type* or a *value_type*.</span></span>

```antlr
object_creation_expression
    : 'new' type '(' argument_list? ')' object_or_collection_initializer?
    | 'new' type object_or_collection_initializer
    ;

object_or_collection_initializer
    : object_initializer
    | collection_initializer
    ;
```

<span data-ttu-id="04edb-1212">*Тип* из *object_creation_expression* должно быть *class_type*, *value_type* или *параметр_типа* .</span><span class="sxs-lookup"><span data-stu-id="04edb-1212">The *type* of an *object_creation_expression* must be a *class_type*, a *value_type* or a *type_parameter*.</span></span> <span data-ttu-id="04edb-1213">*Тип* не может быть `abstract` *class_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1213">The *type* cannot be an `abstract` *class_type*.</span></span>

<span data-ttu-id="04edb-1214">Необязательный *argument_list* ([списки аргументов](expressions.md#argument-lists)) разрешается, только в том случае, если *тип* — *class_type* или *struct_ Тип*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1214">The optional *argument_list* ([Argument lists](expressions.md#argument-lists)) is permitted only if the *type* is a *class_type* or a *struct_type*.</span></span>

<span data-ttu-id="04edb-1215">Выражения создания объекта можно опустить список аргументов конструктора и скобок при условии, что он включает в себя инициализатор объекта или коллекции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1215">An object creation expression can omit the constructor argument list and enclosing parentheses provided it includes an object initializer or collection initializer.</span></span> <span data-ttu-id="04edb-1216">Пропуск список аргументов конструктора и скобок — эквивалентен предложению пустым списком аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1216">Omitting the constructor argument list and enclosing parentheses is equivalent to specifying an empty argument list.</span></span>

<span data-ttu-id="04edb-1217">Обработка выражения создания объекта, который включает в себя инициализатор объекта или коллекции включает сначала выполняется конструктор экземпляра, а затем обрабатывая инициализация члена или элемента, указанного в инициализаторе объекта ([ Инициализаторы объектов](expressions.md#object-initializers)) или коллекции ([инициализаторы](expressions.md#collection-initializers)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1217">Processing of an object creation expression that includes an object initializer or collection initializer consists of first processing the instance constructor and then processing the member or element initializations specified by the object initializer ([Object initializers](expressions.md#object-initializers)) or collection initializer ([Collection initializers](expressions.md#collection-initializers)).</span></span>

<span data-ttu-id="04edb-1218">Если любой из аргументов в необязательном *argument_list* имеет тип времени компиляции `dynamic` то *object_creation_expression* является динамическим ([динамической привязки](expressions.md#dynamic-binding)) следующие правила применяются во время выполнения с использованием типа во время выполнения эти аргументы *argument_list* , имеющих тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1218">If any of the arguments in the optional *argument_list* has the compile-time type `dynamic` then the *object_creation_expression* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)) and the following rules are applied at run-time using the run-time type of those arguments of the *argument_list* that have the compile time type `dynamic`.</span></span> <span data-ttu-id="04edb-1219">Тем не менее, для создания объекта выполняется ограниченная проверка времени компиляции, как описано в разделе [Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1219">However, the object creation undergoes a limited compile time check as described in [Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution).</span></span>

<span data-ttu-id="04edb-1220">Во время привязки обработка *object_creation_expression* формы `new T(A)`, где `T` — *class_type* или *value_type* и `A` не является обязательной *argument_list*, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1220">The binding-time processing of an *object_creation_expression* of the form `new T(A)`, where `T` is a *class_type* or a *value_type* and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*   <span data-ttu-id="04edb-1221">Если `T` — *value_type* и `A` отсутствует:</span><span class="sxs-lookup"><span data-stu-id="04edb-1221">If `T` is a *value_type* and `A` is not present:</span></span>
    * <span data-ttu-id="04edb-1222">*Object_creation_expression* является вызов конструктора по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="04edb-1222">The *object_creation_expression* is a default constructor invocation.</span></span> <span data-ttu-id="04edb-1223">Результат *object_creation_expression* является значением типа `T`, то есть значение по умолчанию для `T` как определено в [типа System.ValueType](types.md#the-systemvaluetype-type).</span><span class="sxs-lookup"><span data-stu-id="04edb-1223">The result of the *object_creation_expression* is a value of type `T`, namely the default value for `T` as defined in [The System.ValueType type](types.md#the-systemvaluetype-type).</span></span>
*   <span data-ttu-id="04edb-1224">В противном случае, если `T` — *параметр_типа* и `A` отсутствует:</span><span class="sxs-lookup"><span data-stu-id="04edb-1224">Otherwise, if `T` is a *type_parameter* and `A` is not present:</span></span>
    * <span data-ttu-id="04edb-1225">Если нет ограничение типа значения или ограничение конструктора ([ограничения параметров типа](classes.md#type-parameter-constraints)) был указан для `T`, возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1225">If no value type constraint or constructor constraint ([Type parameter constraints](classes.md#type-parameter-constraints)) has been specified for `T`, a binding-time error occurs.</span></span>
    * <span data-ttu-id="04edb-1226">Результат *object_creation_expression* является значение типа времени выполнения, привязанного параметра типа, а именно результат вызова конструктора по умолчанию этого типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1226">The result of the *object_creation_expression* is a value of the run-time type that the type parameter has been bound to, namely the result of invoking the default constructor of that type.</span></span> <span data-ttu-id="04edb-1227">Тип времени выполнения может быть ссылочным типом или типом значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1227">The run-time type may be a reference type or a value type.</span></span>
*   <span data-ttu-id="04edb-1228">В противном случае, если `T` — *class_type* или *struct_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-1228">Otherwise, if `T` is a *class_type* or a *struct_type*:</span></span>
    * <span data-ttu-id="04edb-1229">Если `T` — `abstract` *class_type*, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1229">If `T` is an `abstract` *class_type*, a compile-time error occurs.</span></span>
    * <span data-ttu-id="04edb-1230">Вызываемый конструктор экземпляра определяется с помощью правил разрешения перегрузки [разрешение перегрузки](expressions.md#overload-resolution).</span><span class="sxs-lookup"><span data-stu-id="04edb-1230">The instance constructor to invoke is determined using the overload resolution rules of [Overload resolution](expressions.md#overload-resolution).</span></span> <span data-ttu-id="04edb-1231">Набор кандидатов конструкторов экземпляров состоит из всех доступный экземпляр конструкторов, объявленных в `T` по отношению к которому применимы `A` ([применимого члена функции](expressions.md#applicable-function-member)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1231">The set of candidate instance constructors consists of all accessible instance constructors declared in `T` which are applicable with respect to `A` ([Applicable function member](expressions.md#applicable-function-member)).</span></span> <span data-ttu-id="04edb-1232">Если набор кандидатов конструкторов экземпляров пуст или не может быть определен один лучший конструктор экземпляра, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1232">If the set of candidate instance constructors is empty, or if a single best instance constructor cannot be identified, a binding-time error occurs.</span></span>
    * <span data-ttu-id="04edb-1233">Результат *object_creation_expression* является значением типа `T`, а именно: значение, создаваемое путем вызова конструктора экземпляра, определенного в предыдущем шаге.</span><span class="sxs-lookup"><span data-stu-id="04edb-1233">The result of the *object_creation_expression* is a value of type `T`, namely the value produced by invoking the instance constructor determined in the step above.</span></span>
*  <span data-ttu-id="04edb-1234">В противном случае *object_creation_expression* является недопустимым, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1234">Otherwise, the *object_creation_expression* is invalid, and a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-1235">Даже если *object_creation_expression* динамически привязаны, во время компиляции тип — по-прежнему `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1235">Even if the *object_creation_expression* is dynamically bound, the compile-time type is still `T`.</span></span>

<span data-ttu-id="04edb-1236">Во время выполнения обработки *object_creation_expression* формы `new T(A)`, где `T` — *class_type* или *struct_type* и `A` не является обязательной *argument_list*, состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1236">The run-time processing of an *object_creation_expression* of the form `new T(A)`, where `T` is *class_type* or a *struct_type* and `A` is an optional *argument_list*, consists of the following steps:</span></span>

*   <span data-ttu-id="04edb-1237">Если `T` — *class_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-1237">If `T` is a *class_type*:</span></span>
    * <span data-ttu-id="04edb-1238">Новый экземпляр класса `T` выделяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1238">A new instance of class `T` is allocated.</span></span> <span data-ttu-id="04edb-1239">Если не хватает памяти для выделения нового экземпляра, `System.OutOfMemoryException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1239">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="04edb-1240">Все поля нового экземпляра инициализируются со значениями по умолчанию ([значения по умолчанию](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1240">All fields of the new instance are initialized to their default values ([Default values](variables.md#default-values)).</span></span>
    * <span data-ttu-id="04edb-1241">Конструктор экземпляра вызывается в соответствии с правилами вызова функции-члена ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1241">The instance constructor is invoked according to the rules of function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span> <span data-ttu-id="04edb-1242">Ссылку на созданный экземпляр автоматически передается конструктору экземпляра и экземпляр может осуществляться из этого конструктора с `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1242">A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as `this`.</span></span>
*   <span data-ttu-id="04edb-1243">Если `T` — *struct_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-1243">If `T` is a *struct_type*:</span></span>
    * <span data-ttu-id="04edb-1244">Экземпляр типа `T` создается путем выделения временной локальной переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-1244">An instance of type `T` is created by allocating a temporary local variable.</span></span> <span data-ttu-id="04edb-1245">Так как конструктор экземпляра *struct_type* для явного присвоения значений для каждого поля экземпляра, необходима инициализация временной переменной не требуется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1245">Since an instance constructor of a *struct_type* is required to definitely assign a value to each field of the instance being created, no initialization of the temporary variable is necessary.</span></span>
    * <span data-ttu-id="04edb-1246">Конструктор экземпляра вызывается в соответствии с правилами вызова функции-члена ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1246">The instance constructor is invoked according to the rules of function member invocation ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)).</span></span> <span data-ttu-id="04edb-1247">Ссылку на созданный экземпляр автоматически передается конструктору экземпляра и экземпляр может осуществляться из этого конструктора с `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1247">A reference to the newly allocated instance is automatically passed to the instance constructor and the instance can be accessed from within that constructor as `this`.</span></span>

#### <a name="object-initializers"></a><span data-ttu-id="04edb-1248">Инициализаторы объектов</span><span class="sxs-lookup"><span data-stu-id="04edb-1248">Object initializers</span></span>

<span data-ttu-id="04edb-1249">***Инициализатора объекта*** указывает значения для ноль или более полей, свойств или индексированными элементами объекта.</span><span class="sxs-lookup"><span data-stu-id="04edb-1249">An ***object initializer*** specifies values for zero or more fields, properties or indexed elements of an object.</span></span>

```antlr
object_initializer
    : '{' member_initializer_list? '}'
    | '{' member_initializer_list ',' '}'
    ;

member_initializer_list
    : member_initializer (',' member_initializer)*
    ;

member_initializer
    : initializer_target '=' initializer_value
    ;

initializer_target
    : identifier
    | '[' argument_list ']'
    ;

initializer_value
    : expression
    | object_or_collection_initializer
    ;
```

<span data-ttu-id="04edb-1250">Инициализатор объекта состоит из последовательности инициализаторов членов, заключенных `{` и `}` маркеров и разделены запятыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-1250">An object initializer consists of a sequence of member initializers, enclosed by `{` and `}` tokens and separated by commas.</span></span> <span data-ttu-id="04edb-1251">Каждый *member_initializer* определяет целевой объект для инициализации.</span><span class="sxs-lookup"><span data-stu-id="04edb-1251">Each *member_initializer* designates a target for the initialization.</span></span> <span data-ttu-id="04edb-1252">*Идентификатор* необходимо присвоить имя к доступному полю или свойству объекта выполняется инициализация, тогда как *argument_list* заключены в квадратные скобки необходимо указать аргументы для индексатора доступны на инициализируемый объект.</span><span class="sxs-lookup"><span data-stu-id="04edb-1252">An *identifier* must name an accessible field or property of the object being initialized, whereas an *argument_list* enclosed in square brackets must specify arguments for an accessible indexer on the object being initialized.</span></span> <span data-ttu-id="04edb-1253">Это ошибка для инициализатора объекта для включения более чем один инициализатор элементов по одному полю или свойству.</span><span class="sxs-lookup"><span data-stu-id="04edb-1253">It is an error for an object initializer to include more than one member initializer for the same field or property.</span></span>

<span data-ttu-id="04edb-1254">Каждый *initializer_target* следуют знак равенства и выражение, инициализатора объекта или инициализатор коллекции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1254">Each *initializer_target* is followed by an equals sign and either an expression, an object initializer or a collection initializer.</span></span> <span data-ttu-id="04edb-1255">Не поддерживается для выражений внутри инициализатора объекта для ссылки на только что созданный объект, который он инициализируется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1255">It is not possible for expressions within the object initializer to refer to the newly created object it is initializing.</span></span>

<span data-ttu-id="04edb-1256">Инициализатор члена, который указывает выражение после знака равенства обрабатывается так же, как и присваивание ([простое присваивание](expressions.md#simple-assignment)) к целевому объекту.</span><span class="sxs-lookup"><span data-stu-id="04edb-1256">A member initializer that specifies an expression after the equals sign is processed in the same way as an assignment ([Simple assignment](expressions.md#simple-assignment)) to the target.</span></span>

<span data-ttu-id="04edb-1257">Инициализатор члена, который указывает инициализатора объекта, после знака равенства ***инициализатора вложенного объекта***, т. е. инициализация внедренный объект.</span><span class="sxs-lookup"><span data-stu-id="04edb-1257">A member initializer that specifies an object initializer after the equals sign is a ***nested object initializer***, i.e. an initialization of an embedded object.</span></span> <span data-ttu-id="04edb-1258">Вместо присвоения нового значения для поля или свойства, назначения в инициализаторе вложенного объекта, рассматриваются как назначения для элементов поля или свойства.</span><span class="sxs-lookup"><span data-stu-id="04edb-1258">Instead of assigning a new value to the field or property, the assignments in the nested object initializer are treated as assignments to members of the field or property.</span></span> <span data-ttu-id="04edb-1259">Инициализаторы вложенных объектов не может применяться к свойствам с типом значения или только для чтения полям с типом значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1259">Nested object initializers cannot be applied to properties with a value type, or to read-only fields with a value type.</span></span>

<span data-ttu-id="04edb-1260">Инициализатор члена, который определяет инициализатор коллекции после знака равенства, выполняет инициализацию внедренной коллекции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1260">A member initializer that specifies a collection initializer after the equals sign is an initialization of an embedded collection.</span></span> <span data-ttu-id="04edb-1261">Вместо назначения новой коллекции для целевого поля, свойства или индексатора, элементы, указанные в инициализаторе добавляются в коллекцию, ссылается на целевой объект.</span><span class="sxs-lookup"><span data-stu-id="04edb-1261">Instead of assigning a new collection to the target field, property or indexer, the elements given in the initializer are added to the collection referenced by the target.</span></span> <span data-ttu-id="04edb-1262">Целевой объект должен иметь тип коллекции, который удовлетворяет требованиям, указанным в [Инициализаторы коллекций](expressions.md#collection-initializers).</span><span class="sxs-lookup"><span data-stu-id="04edb-1262">The target must be of a collection type that satisfies the requirements specified in [Collection initializers](expressions.md#collection-initializers).</span></span>

<span data-ttu-id="04edb-1263">Аргументы для инициализатора индекса всегда вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-1263">The arguments to an index initializer will always be evaluated exactly once.</span></span> <span data-ttu-id="04edb-1264">Таким образом даже если аргументы в итоге никогда не используется начало (например, из-за пустого инициализатора вложенной), они будут вычисляться для побочного эффекта.</span><span class="sxs-lookup"><span data-stu-id="04edb-1264">Thus, even if the arguments end up never getting used (e.g. because of an empty nested initializer), they will be evaluated for their side effects.</span></span>

<span data-ttu-id="04edb-1265">Следующий класс представляет точку с помощью двух координат:</span><span class="sxs-lookup"><span data-stu-id="04edb-1265">The following class represents a point with two coordinates:</span></span>
```csharp
public class Point
{
    int x, y;

    public int X { get { return x; } set { x = value; } }
    public int Y { get { return y; } set { y = value; } }
}
```

<span data-ttu-id="04edb-1266">Экземпляр `Point` можно создавать и инициализировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1266">An instance of `Point` can be created and initialized as follows:</span></span>
```csharp
Point a = new Point { X = 0, Y = 1 };
```
<span data-ttu-id="04edb-1267">который имеет тот же эффект, что</span><span class="sxs-lookup"><span data-stu-id="04edb-1267">which has the same effect as</span></span>
```csharp
Point __a = new Point();
__a.X = 0;
__a.Y = 1; 
Point a = __a;
```
<span data-ttu-id="04edb-1268">где `__a` является невидимой и недоступной временной переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-1268">where `__a` is an otherwise invisible and inaccessible temporary variable.</span></span> <span data-ttu-id="04edb-1269">Следующий класс представляет собой прямоугольник, созданный из двух точек:</span><span class="sxs-lookup"><span data-stu-id="04edb-1269">The following class represents a rectangle created from two points:</span></span>
```csharp
public class Rectangle
{
    Point p1, p2;

    public Point P1 { get { return p1; } set { p1 = value; } }
    public Point P2 { get { return p2; } set { p2 = value; } }
}
```

<span data-ttu-id="04edb-1270">Экземпляр `Rectangle` можно создавать и инициализировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1270">An instance of `Rectangle` can be created and initialized as follows:</span></span>
```csharp
Rectangle r = new Rectangle {
    P1 = new Point { X = 0, Y = 1 },
    P2 = new Point { X = 2, Y = 3 }
};
```
<span data-ttu-id="04edb-1271">который имеет тот же эффект, что</span><span class="sxs-lookup"><span data-stu-id="04edb-1271">which has the same effect as</span></span>
```csharp
Rectangle __r = new Rectangle();
Point __p1 = new Point();
__p1.X = 0;
__p1.Y = 1;
__r.P1 = __p1;
Point __p2 = new Point();
__p2.X = 2;
__p2.Y = 3;
__r.P2 = __p2; 
Rectangle r = __r;
```
<span data-ttu-id="04edb-1272">где `__r`, `__p1` и `__p2` являются временные переменные, которые в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-1272">where `__r`, `__p1` and `__p2` are temporary variables that are otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="04edb-1273">Если `Rectangle`в конструктор выделяет два внедренных `Point` экземпляров</span><span class="sxs-lookup"><span data-stu-id="04edb-1273">If `Rectangle`'s constructor allocates the two embedded `Point` instances</span></span>
```csharp
public class Rectangle
{
    Point p1 = new Point();
    Point p2 = new Point();

    public Point P1 { get { return p1; } }
    public Point P2 { get { return p2; } }
}
```
<span data-ttu-id="04edb-1274">Следующая конструкция может использоваться для инициализации внедренный `Point` экземпляров, вместо назначения новых экземпляров:</span><span class="sxs-lookup"><span data-stu-id="04edb-1274">the following construct can be used to initialize the embedded `Point` instances instead of assigning new instances:</span></span>
```csharp
Rectangle r = new Rectangle {
    P1 = { X = 0, Y = 1 },
    P2 = { X = 2, Y = 3 }
};
```
<span data-ttu-id="04edb-1275">который имеет тот же эффект, что</span><span class="sxs-lookup"><span data-stu-id="04edb-1275">which has the same effect as</span></span>
```csharp
Rectangle __r = new Rectangle();
__r.P1.X = 0;
__r.P1.Y = 1;
__r.P2.X = 2;
__r.P2.Y = 3;
Rectangle r = __r;
```

<span data-ttu-id="04edb-1276">Если определение соответствующего языка c, в следующем примере:</span><span class="sxs-lookup"><span data-stu-id="04edb-1276">Given an appropriate definition of C, the following example:</span></span>
```csharp
var c = new C {
    x = true,
    y = { a = "Hello" },
    z = { 1, 2, 3 },
    ["x"] = 5,
    [0,0] = { "a", "b" },
    [1,2] = {}
};
```
<span data-ttu-id="04edb-1277">эквивалентно эту серию назначения:</span><span class="sxs-lookup"><span data-stu-id="04edb-1277">is equivalent to this series of assignments:</span></span>
```csharp
C __c = new C();
__c.x = true;
__c.y.a = "Hello";
__c.z.Add(1); 
__c.z.Add(2);
__c.z.Add(3);
string __i1 = "x";
__c[__i1] = 5;
int __i2 = 0, __i3 = 0;
__c[__i2,__i3].Add("a");
__c[__i2,__i3].Add("b");
int __i4 = 1, __i5 = 2;
var c = __c;
```
<span data-ttu-id="04edb-1278">где `__c`и пр., созданные переменные, которые являются и недоступными к исходному коду.</span><span class="sxs-lookup"><span data-stu-id="04edb-1278">where `__c`, etc., are generated variables that are invisible and inaccessible to the source code.</span></span> <span data-ttu-id="04edb-1279">Обратите внимание, что аргументы для `[0,0]` вычисляется только один раз и аргументы для `[1,2]` вычисляются один раз несмотря на то, что они никогда не используются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1279">Note that the arguments for `[0,0]` are evaluated only once, and the arguments for `[1,2]` are evaluated once even though they are never used.</span></span>

#### <a name="collection-initializers"></a><span data-ttu-id="04edb-1280">Инициализаторы коллекций</span><span class="sxs-lookup"><span data-stu-id="04edb-1280">Collection initializers</span></span>

<span data-ttu-id="04edb-1281">Инициализатор коллекции определяет элементы в коллекцию.</span><span class="sxs-lookup"><span data-stu-id="04edb-1281">A collection initializer specifies the elements of a collection.</span></span>

```antlr
collection_initializer
    : '{' element_initializer_list '}'
    | '{' element_initializer_list ',' '}'
    ;

element_initializer_list
    : element_initializer (',' element_initializer)*
    ;

element_initializer
    : non_assignment_expression
    | '{' expression_list '}'
    ;

expression_list
    : expression (',' expression)*
    ;
```

<span data-ttu-id="04edb-1282">Инициализатор коллекции состоит из последовательности инициализаторов элементов, заключенных `{` и `}` маркеров и разделены запятыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-1282">A collection initializer consists of a sequence of element initializers, enclosed by `{` and `}` tokens and separated by commas.</span></span> <span data-ttu-id="04edb-1283">Каждый инициализатор элемента задает элемент для добавления инициализируемый объект коллекции и состоит из списка выражений, заключенных `{` и `}` маркеров и разделены запятыми.</span><span class="sxs-lookup"><span data-stu-id="04edb-1283">Each element initializer specifies an element to be added to the collection object being initialized, and consists of a list of expressions enclosed by `{` and `}` tokens and separated by commas.</span></span>  <span data-ttu-id="04edb-1284">Инициализатор элемента с одним выражением можно записать и без фигурных скобок, но не может быть выражением присваивания, чтобы избежать неоднозначности с инициализаторы членов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1284">A single-expression element initializer can be written without braces, but cannot then be an assignment expression, to avoid ambiguity with member initializers.</span></span> <span data-ttu-id="04edb-1285">*Non_assignment_expression* рабочей определяется в [выражение](expressions.md#expression).</span><span class="sxs-lookup"><span data-stu-id="04edb-1285">The *non_assignment_expression* production is defined in [Expression](expressions.md#expression).</span></span>

<span data-ttu-id="04edb-1286">Ниже приведен пример выражения создания объекта, который включает в себя инициализатор коллекции:</span><span class="sxs-lookup"><span data-stu-id="04edb-1286">The following is an example of an object creation expression that includes a collection initializer:</span></span>
```csharp
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
```

<span data-ttu-id="04edb-1287">Объект коллекции, к которому применяется инициализатор коллекции должны иметь тип, реализующий `System.Collections.IEnumerable` или возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1287">The collection object to which a collection initializer is applied must be of a type that implements `System.Collections.IEnumerable` or a compile-time error occurs.</span></span> <span data-ttu-id="04edb-1288">Для каждого выбранного элемента в порядке, инициализатор вызывает `Add` метод для целевого объекта со списком выражения инициализатора элементов как список аргументов, применение поиске обычного элемента и разрешение для каждого вызова перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1288">For each specified element in order, the collection initializer invokes an `Add` method on the target object with the expression list of the element initializer as argument list, applying normal member lookup and overload resolution for each invocation.</span></span> <span data-ttu-id="04edb-1289">Таким образом, объект коллекции должен иметь соответствующий экземпляр или расширение метод с именем `Add` для каждого элемента инициализатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1289">Thus, the collection object must have an applicable instance or extension method with the name `Add` for each element initializer.</span></span>

<span data-ttu-id="04edb-1290">Следующий класс представляет контакт с именем и список номеров телефонов:</span><span class="sxs-lookup"><span data-stu-id="04edb-1290">The following class represents a contact with a name and a list of phone numbers:</span></span>
```csharp
public class Contact
{
    string name;
    List<string> phoneNumbers = new List<string>();

    public string Name { get { return name; } set { name = value; } }

    public List<string> PhoneNumbers { get { return phoneNumbers; } }
}
```

<span data-ttu-id="04edb-1291">Объект `List<Contact>` можно создавать и инициализировать следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1291">A `List<Contact>` can be created and initialized as follows:</span></span>
```csharp
var contacts = new List<Contact> {
    new Contact {
        Name = "Chris Smith",
        PhoneNumbers = { "206-555-0101", "425-882-8080" }
    },
    new Contact {
        Name = "Bob Harris",
        PhoneNumbers = { "650-555-0199" }
    }
};
```
<span data-ttu-id="04edb-1292">который имеет тот же эффект, что</span><span class="sxs-lookup"><span data-stu-id="04edb-1292">which has the same effect as</span></span>
```csharp
var __clist = new List<Contact>();
Contact __c1 = new Contact();
__c1.Name = "Chris Smith";
__c1.PhoneNumbers.Add("206-555-0101");
__c1.PhoneNumbers.Add("425-882-8080");
__clist.Add(__c1);
Contact __c2 = new Contact();
__c2.Name = "Bob Harris";
__c2.PhoneNumbers.Add("650-555-0199");
__clist.Add(__c2);
var contacts = __clist;
```
<span data-ttu-id="04edb-1293">где `__clist`, `__c1` и `__c2` являются временные переменные, которые в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-1293">where `__clist`, `__c1` and `__c2` are temporary variables that are otherwise invisible and inaccessible.</span></span>

#### <a name="array-creation-expressions"></a><span data-ttu-id="04edb-1294">Выражения создания массива</span><span class="sxs-lookup"><span data-stu-id="04edb-1294">Array creation expressions</span></span>

<span data-ttu-id="04edb-1295">*Array_creation_expression* используется для создания нового экземпляра *array_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1295">An *array_creation_expression* is used to create a new instance of an *array_type*.</span></span>

```antlr
array_creation_expression
    : 'new' non_array_type '[' expression_list ']' rank_specifier* array_initializer?
    | 'new' array_type array_initializer
    | 'new' rank_specifier array_initializer
    ;
```

<span data-ttu-id="04edb-1296">Выражение создания массива из первой формы выделяет экземпляр массива тип, полученный в результате удаления всех отдельных выражений из списка выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-1296">An array creation expression of the first form allocates an array instance of the type that results from deleting each of the individual expressions from the expression list.</span></span> <span data-ttu-id="04edb-1297">Например, выражение создания массива `new int[10,20]` создает экземпляр массива типа `int[,]`и выражение создания массива `new int[10][,]` создает массив объектов типа `int[][,]`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1297">For example, the array creation expression `new int[10,20]` produces an array instance of type `int[,]`, and the array creation expression `new int[10][,]` produces an array of type `int[][,]`.</span></span> <span data-ttu-id="04edb-1298">Каждое выражение в списке выражений должен иметь тип `int`, `uint`, `long`, или `ulong`, или неявно преобразуется в один или несколько из этих типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1298">Each expression in the expression list must be of type `int`, `uint`, `long`, or `ulong`, or implicitly convertible to one or more of these types.</span></span> <span data-ttu-id="04edb-1299">Значение каждого выражения определяет длину соответствующего измерения в экземпляре во вновь выделенный массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-1299">The value of each expression determines the length of the corresponding dimension in the newly allocated array instance.</span></span> <span data-ttu-id="04edb-1300">Так как длина размерности массива должны быть неотрицательными, является ошибкой во время компиляции для *constant_expression* с отрицательными значениями в списке выражений.</span><span class="sxs-lookup"><span data-stu-id="04edb-1300">Since the length of an array dimension must be nonnegative, it is a compile-time error to have a *constant_expression* with a negative value in the expression list.</span></span>

<span data-ttu-id="04edb-1301">Только в небезопасном контексте ([небезопасных контекстах](unsafe-code.md#unsafe-contexts)), макет массивов не определен.</span><span class="sxs-lookup"><span data-stu-id="04edb-1301">Except in an unsafe context ([Unsafe contexts](unsafe-code.md#unsafe-contexts)), the layout of arrays is unspecified.</span></span>

<span data-ttu-id="04edb-1302">Если выражение создания массива первого типа включает в себя инициализатор массива, каждое выражение в списке выражений должно быть константой, и ранга и размерности длины, указанные в списке выражений должны совпадать с инициализатором массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-1302">If an array creation expression of the first form includes an array initializer, each expression in the expression list must be a constant and the rank and dimension lengths specified by the expression list must match those of the array initializer.</span></span>

<span data-ttu-id="04edb-1303">В выражение создания массива в форме во втором и третьем ранг спецификатора типа "или" ранг заданного массива должна соответствовать инициализатора массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-1303">In an array creation expression of the second or third form, the rank of the specified array type or rank specifier must match that of the array initializer.</span></span> <span data-ttu-id="04edb-1304">Длины отдельных измерений выводятся из числа элементов в каждом из соответствующих уровней вложения инициализатора массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-1304">The individual dimension lengths are inferred from the number of elements in each of the corresponding nesting levels of the array initializer.</span></span> <span data-ttu-id="04edb-1305">Таким образом выражение</span><span class="sxs-lookup"><span data-stu-id="04edb-1305">Thus, the expression</span></span>
```csharp
new int[,] {{0, 1}, {2, 3}, {4, 5}}
```
<span data-ttu-id="04edb-1306">в точности соответствует</span><span class="sxs-lookup"><span data-stu-id="04edb-1306">exactly corresponds to</span></span>
```csharp
new int[3, 2] {{0, 1}, {2, 3}, {4, 5}}
```

<span data-ttu-id="04edb-1307">Выражение создания массива третьего типа называется ***неявно типизированные выражение создания массива***.</span><span class="sxs-lookup"><span data-stu-id="04edb-1307">An array creation expression of the third form is referred to as an ***implicitly typed array creation expression***.</span></span> <span data-ttu-id="04edb-1308">Это похоже на второй форме, за исключением того, что тип элемента массива не указан явно, но определяется как наиболее общий тип ([поиск это наиболее распространенный тип набора выражений](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)) из набора выражений в массиве инициализатор.</span><span class="sxs-lookup"><span data-stu-id="04edb-1308">It is similar to the second form, except that the element type of the array is not explicitly given, but determined as the best common type ([Finding the best common type of a set of expressions](expressions.md#finding-the-best-common-type-of-a-set-of-expressions)) of the set of expressions in the array initializer.</span></span> <span data-ttu-id="04edb-1309">Для многомерного массива т. е. один where *rank_specifier* содержит по крайней мере одна запятая этот набор включает в себя все *выражение*s из вложенных *array_initializer*s.</span><span class="sxs-lookup"><span data-stu-id="04edb-1309">For a multidimensional array, i.e., one where the *rank_specifier* contains at least one comma, this set comprises all *expression*s found in nested *array_initializer*s.</span></span>

<span data-ttu-id="04edb-1310">Инициализаторы массивов описаны далее в [Инициализаторы массивов](arrays.md#array-initializers).</span><span class="sxs-lookup"><span data-stu-id="04edb-1310">Array initializers are described further in [Array initializers](arrays.md#array-initializers).</span></span>

<span data-ttu-id="04edb-1311">Результат вычисления выражения создания массива классифицируется как значение, а именно: ссылка на экземпляр вновь выделенный массив.</span><span class="sxs-lookup"><span data-stu-id="04edb-1311">The result of evaluating an array creation expression is classified as a value, namely a reference to the newly allocated array instance.</span></span> <span data-ttu-id="04edb-1312">Во время выполнения обработки выражение создания массива состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1312">The run-time processing of an array creation expression consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-1313">Длина выражения измерений *список_выражений* вычисляются в порядке слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-1313">The dimension length expressions of the *expression_list* are evaluated in order, from left to right.</span></span> <span data-ttu-id="04edb-1314">После вычисления каждого выражения, неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) выполняется одно из следующих типов: `int`, `uint`, `long`, `ulong`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1314">Following evaluation of each expression, an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) to one of the following types is performed: `int`, `uint`, `long`, `ulong`.</span></span> <span data-ttu-id="04edb-1315">Будет выбран первый тип, в этом списке, для которого существует неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="04edb-1315">The first type in this list for which an implicit conversion exists is chosen.</span></span> <span data-ttu-id="04edb-1316">Если вычисление выражения или последующих неявное преобразование возникает исключение, следующие выражения оцениваются, и никакие дополнительные действия выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1316">If evaluation of an expression or the subsequent implicit conversion causes an exception, then no further expressions are evaluated and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1317">Вычисленные значения для длины по измерениям проверяются следующим образом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1317">The computed values for the dimension lengths are validated as follows.</span></span> <span data-ttu-id="04edb-1318">Если один или несколько значений меньше нуля, `System.OverflowException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1318">If one or more of the values are less than zero, a `System.OverflowException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1319">Выделяется экземпляр массива с заданной длины по измерениям.</span><span class="sxs-lookup"><span data-stu-id="04edb-1319">An array instance with the given dimension lengths is allocated.</span></span> <span data-ttu-id="04edb-1320">Если не хватает памяти для выделения нового экземпляра, `System.OutOfMemoryException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1320">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
*  <span data-ttu-id="04edb-1321">Все элементы нового экземпляра массива инициализируются значениями по умолчанию ([значения по умолчанию](variables.md#default-values)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1321">All elements of the new array instance are initialized to their default values ([Default values](variables.md#default-values)).</span></span>
*  <span data-ttu-id="04edb-1322">Если выражение создания массива содержит инициализатор массива, каждое выражение в инициализаторе массива вычисляются и присваиваются соответствующим элементом массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-1322">If the array creation expression contains an array initializer, then each expression in the array initializer is evaluated and assigned to its corresponding array element.</span></span> <span data-ttu-id="04edb-1323">Вычисления и присваивания выполняются в порядке, при написании выражения в инициализаторе массива — другими словами, элементы инициализируются в порядке по возрастанию индекса, с самого правого измерения, первым.</span><span class="sxs-lookup"><span data-stu-id="04edb-1323">The evaluations and assignments are performed in the order the expressions are written in the array initializer—in other words, elements are initialized in increasing index order, with the rightmost dimension increasing first.</span></span> <span data-ttu-id="04edb-1324">Если вычисления данного выражения или последующем присваивании в соответствующий элемент массива приводит к возникновению исключения, последующих элементов не инициализируются (и остальные элементы таким образом будут иметь значения по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="04edb-1324">If evaluation of a given expression or the subsequent assignment to the corresponding array element causes an exception, then no further elements are initialized (and the remaining elements will thus have their default values).</span></span>

<span data-ttu-id="04edb-1325">Выражение создания массива разрешает создание экземпляра массива с элементами типа массива, но элементы такого массива должны инициализироваться вручную.</span><span class="sxs-lookup"><span data-stu-id="04edb-1325">An array creation expression permits instantiation of an array with elements of an array type, but the elements of such an array must be manually initialized.</span></span> <span data-ttu-id="04edb-1326">Например инструкция</span><span class="sxs-lookup"><span data-stu-id="04edb-1326">For example, the statement</span></span>
```csharp
int[][] a = new int[100][];
```
<span data-ttu-id="04edb-1327">Создает одномерный массив с 100 элементов типа `int[]`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1327">creates a single-dimensional array with 100 elements of type `int[]`.</span></span> <span data-ttu-id="04edb-1328">Начальное значение каждого элемента является `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1328">The initial value of each element is `null`.</span></span> <span data-ttu-id="04edb-1329">Невозможно для же выражение создания массива инициализировать подмассивов и инструкции</span><span class="sxs-lookup"><span data-stu-id="04edb-1329">It is not possible for the same array creation expression to also instantiate the sub-arrays, and the statement</span></span>
```csharp
int[][] a = new int[100][5];        // Error
```
<span data-ttu-id="04edb-1330">приводит к ошибке времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1330">results in a compile-time error.</span></span> <span data-ttu-id="04edb-1331">При создании экземпляра подмассивов вместо должна выполняться вручную, как и в</span><span class="sxs-lookup"><span data-stu-id="04edb-1331">Instantiation of the sub-arrays must instead be performed manually, as in</span></span>
```csharp
int[][] a = new int[100][];
for (int i = 0; i < 100; i++) a[i] = new int[5];
```

<span data-ttu-id="04edb-1332">Массив массивов имеет форму «прямоугольная», то есть когда вложенные массивы имеют одинаковую длину, при более эффективно использовать многомерный массив.</span><span class="sxs-lookup"><span data-stu-id="04edb-1332">When an array of arrays has a "rectangular" shape, that is when the sub-arrays are all of the same length, it is more efficient to use a multi-dimensional array.</span></span> <span data-ttu-id="04edb-1333">В приведенном выше примере при инициализации массива массивов создается 101 объект — один внешний массив и 100 вложенных массивов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1333">In the example above, instantiation of the array of arrays creates 101 objects—one outer array and 100 sub-arrays.</span></span> <span data-ttu-id="04edb-1334">Напротив,</span><span class="sxs-lookup"><span data-stu-id="04edb-1334">In contrast,</span></span>
```csharp
int[,] = new int[100, 5];
```
<span data-ttu-id="04edb-1335">создает только один объект, двумерный массив и выполняет распределение в одной инструкции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1335">creates only a single object, a two-dimensional array, and accomplishes the allocation in a single statement.</span></span>

<span data-ttu-id="04edb-1336">Ниже приведены примеры выражений создание неявно типизированного массива:</span><span class="sxs-lookup"><span data-stu-id="04edb-1336">The following are examples of implicitly typed array creation expressions:</span></span>
```csharp
var a = new[] { 1, 10, 100, 1000 };                       // int[]

var b = new[] { 1, 1.5, 2, 2.5 };                         // double[]

var c = new[,] { { "hello", null }, { "world", "!" } };   // string[,]

var d = new[] { 1, "one", 2, "two" };                     // Error
```

<span data-ttu-id="04edb-1337">Последнее выражение вызывает ошибку времени компиляции, поскольку ни `int` , ни `string` может быть неявно преобразован в другой и введите там нет, наиболее часто.</span><span class="sxs-lookup"><span data-stu-id="04edb-1337">The last expression causes a compile-time error because neither `int` nor `string` is implicitly convertible to the other, and so there is no best common type.</span></span> <span data-ttu-id="04edb-1338">Выражение создания массива явным образом типизированной необходимо использовать таким образом, например указав используется тип `object[]`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1338">An explicitly typed array creation expression must be used in this case, for example specifying the type to be `object[]`.</span></span> <span data-ttu-id="04edb-1339">Кроме того один из элементов можно привести к общему базовому типу, который затем станет выведенным типом элемента.</span><span class="sxs-lookup"><span data-stu-id="04edb-1339">Alternatively, one of the elements can be cast to a common base type, which would then become the inferred element type.</span></span>

<span data-ttu-id="04edb-1340">Неявно типизированный массив создания выражения можно объединить с помощью инициализатора анонимных объектов ([выражения создания анонимных объектов](expressions.md#anonymous-object-creation-expressions)) для создания анонимно типизированных структур данных.</span><span class="sxs-lookup"><span data-stu-id="04edb-1340">Implicitly typed array creation expressions can be combined with anonymous object initializers ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) to create anonymously typed data structures.</span></span> <span data-ttu-id="04edb-1341">Пример:</span><span class="sxs-lookup"><span data-stu-id="04edb-1341">For example:</span></span>
```csharp
var contacts = new[] {
    new {
        Name = "Chris Smith",
        PhoneNumbers = new[] { "206-555-0101", "425-882-8080" }
    },
    new {
        Name = "Bob Harris",
        PhoneNumbers = new[] { "650-555-0199" }
    }
};
```

#### <a name="delegate-creation-expressions"></a><span data-ttu-id="04edb-1342">Выражения создания делегата</span><span class="sxs-lookup"><span data-stu-id="04edb-1342">Delegate creation expressions</span></span>

<span data-ttu-id="04edb-1343">Объект *delegate_creation_expression* используется для создания нового экземпляра *delegate_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1343">A *delegate_creation_expression* is used to create a new instance of a *delegate_type*.</span></span>

```antlr
delegate_creation_expression
    : 'new' delegate_type '(' expression ')'
    ;
```

<span data-ttu-id="04edb-1344">Аргумент выражения создания делегата должен быть группу методов, анонимная функция или значение типа времени компиляции `dynamic` или *delegate_type*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1344">The argument of a delegate creation expression must be a method group, an anonymous function or a value of either the compile time type `dynamic` or a *delegate_type*.</span></span> <span data-ttu-id="04edb-1345">Если аргумент представляет группу методов, он определяет метод и метод экземпляра, объект, для которого создается делегат.</span><span class="sxs-lookup"><span data-stu-id="04edb-1345">If the argument is a method group, it identifies the method and, for an instance method, the object for which to create a delegate.</span></span> <span data-ttu-id="04edb-1346">Если аргумент представляет собой анонимную функцию непосредственно определяет параметры и тело метода целевого делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1346">If the argument is an anonymous function it directly defines the parameters and method body of the delegate target.</span></span> <span data-ttu-id="04edb-1347">Если аргумент имеет значение, он определяет экземпляр делегата, для которого необходимо создать копию.</span><span class="sxs-lookup"><span data-stu-id="04edb-1347">If the argument is a value it identifies a delegate instance of which to create a copy.</span></span>

<span data-ttu-id="04edb-1348">Если *выражение* имеет тип времени компиляции `dynamic`, *delegate_creation_expression* является динамическим ([динамической привязки](expressions.md#dynamic-binding)) и правил, приведенных ниже применяются во время выполнения, используя тип среды выполнения *выражение*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1348">If the *expression* has the compile-time type `dynamic`, the *delegate_creation_expression* is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)), and the rules below are applied at run-time using the run-time type of the *expression*.</span></span> <span data-ttu-id="04edb-1349">В противном случае правила применяются во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1349">Otherwise the rules are applied at compile-time.</span></span>

<span data-ttu-id="04edb-1350">Во время привязки обработка *delegate_creation_expression* формы `new D(E)`, где `D` — *delegate_type* и `E` — *выражение* , состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1350">The binding-time processing of a *delegate_creation_expression* of the form `new D(E)`, where `D` is a *delegate_type* and `E` is an *expression*, consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-1351">Если `E` является группой методов выражения создания делегата обрабатывается так же, как преобразования группы методов ([преобразования групп методов](conversions.md#method-group-conversions)) из `E` для `D`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1351">If `E` is a method group, the delegate creation expression is processed in the same way as a method group conversion ([Method group conversions](conversions.md#method-group-conversions)) from `E` to `D`.</span></span>
*  <span data-ttu-id="04edb-1352">Если `E` является анонимной функцией, выражение создания делегата обрабатывается так же, как преобразование анонимной функции ([преобразования анонимных функций](conversions.md#anonymous-function-conversions)) из `E` для `D`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1352">If `E` is an anonymous function, the delegate creation expression is processed in the same way as an anonymous function conversion ([Anonymous function conversions](conversions.md#anonymous-function-conversions)) from `E` to `D`.</span></span>
*  <span data-ttu-id="04edb-1353">Если `E` является значением, `E` должно быть совместимо ([объявления делегатов](delegates.md#delegate-declarations)) с `D`, и результатом является ссылкой на только что созданный делегат типа `D` , ссылающийся на вызовов в списке `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1353">If `E` is a value, `E` must be compatible ([Delegate declarations](delegates.md#delegate-declarations)) with `D`, and the result is a reference to a newly created delegate of type `D` that refers to the same invocation list as `E`.</span></span> <span data-ttu-id="04edb-1354">Если `E` не совместим с `D`, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1354">If `E` is not compatible with `D`, a compile-time error occurs.</span></span>

<span data-ttu-id="04edb-1355">Во время выполнения обработки *delegate_creation_expression* формы `new D(E)`, где `D` — *delegate_type* и `E` — *выражение* , состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1355">The run-time processing of a *delegate_creation_expression* of the form `new D(E)`, where `D` is a *delegate_type* and `E` is an *expression*, consists of the following steps:</span></span>

*   <span data-ttu-id="04edb-1356">Если `E` является группой методов выражения создания делегата вычисляется как преобразования группы методов ([преобразования групп методов](conversions.md#method-group-conversions)) из `E` для `D`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1356">If `E` is a method group, the delegate creation expression is evaluated as a method group conversion ([Method group conversions](conversions.md#method-group-conversions)) from `E` to `D`.</span></span>
*   <span data-ttu-id="04edb-1357">Если `E` представляет собой анонимную функцию создания делегата обрабатывается как преобразование анонимной функции из `E` для `D` ([преобразования анонимных функций](conversions.md#anonymous-function-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1357">If `E` is an anonymous function, the delegate creation is evaluated as an anonymous function conversion from `E` to `D` ([Anonymous function conversions](conversions.md#anonymous-function-conversions)).</span></span>
*   <span data-ttu-id="04edb-1358">Если `E` представляет собой значение *delegate_type*:</span><span class="sxs-lookup"><span data-stu-id="04edb-1358">If `E` is a value of a *delegate_type*:</span></span>
    * <span data-ttu-id="04edb-1359">`E` выполняется оценка.</span><span class="sxs-lookup"><span data-stu-id="04edb-1359">`E` is evaluated.</span></span> <span data-ttu-id="04edb-1360">Если эта оценка вызывает исключение, никакие дополнительные действия выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1360">If this evaluation causes an exception, no further steps are executed.</span></span>
    * <span data-ttu-id="04edb-1361">Если значение `E` — `null`, `System.NullReferenceException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1361">If the value of `E` is `null`, a `System.NullReferenceException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="04edb-1362">Новый экземпляр типа делегата `D` выделяется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1362">A new instance of the delegate type `D` is allocated.</span></span> <span data-ttu-id="04edb-1363">Если не хватает памяти для выделения нового экземпляра, `System.OutOfMemoryException` возникает исключение и никакие дополнительные действия не выполняются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1363">If there is not enough memory available to allocate the new instance, a `System.OutOfMemoryException` is thrown and no further steps are executed.</span></span>
    * <span data-ttu-id="04edb-1364">Новый экземпляр делегата инициализируется с такой же список вызова, как экземпляр делегата, выданный `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1364">The new delegate instance is initialized with the same invocation list as the delegate instance given by `E`.</span></span>

<span data-ttu-id="04edb-1365">Список вызовов делегата определяется при создании экземпляра делегата и остается неизменным в течение всего времени существования делегата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1365">The invocation list of a delegate is determined when the delegate is instantiated and then remains constant for the entire lifetime of the delegate.</span></span> <span data-ttu-id="04edb-1366">Другими словами не сможете изменить целевые вызываемые сущности делегата после его создания.</span><span class="sxs-lookup"><span data-stu-id="04edb-1366">In other words, it is not possible to change the target callable entities of a delegate once it has been created.</span></span> <span data-ttu-id="04edb-1367">При объединении двух делегатов или удалении одного из другого ([объявления делегатов](delegates.md#delegate-declarations)), результаты новый делегат, не существующий делегат имеет его содержимое изменены.</span><span class="sxs-lookup"><span data-stu-id="04edb-1367">When two delegates are combined or one is removed from another ([Delegate declarations](delegates.md#delegate-declarations)), a new delegate results; no existing delegate has its contents changed.</span></span>

<span data-ttu-id="04edb-1368">Это не позволяет создать делегат, который ссылается на свойство, индексатор, определяемого пользователем оператора, конструктор экземпляра, деструктор или статический конструктор.</span><span class="sxs-lookup"><span data-stu-id="04edb-1368">It is not possible to create a delegate that refers to a property, indexer, user-defined operator, instance constructor, destructor, or static constructor.</span></span>

<span data-ttu-id="04edb-1369">Как описано выше, если делегат создается из группы методов, список формальных параметров и тип возвращаемого значения делегата определить, какой из перегруженных методов для выбора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1369">As described above, when a delegate is created from a method group, the formal parameter list and return type of the delegate determine which of the overloaded methods to select.</span></span> <span data-ttu-id="04edb-1370">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-1370">In the example</span></span>
```csharp
delegate double DoubleFunc(double x);

class A
{
    DoubleFunc f = new DoubleFunc(Square);

    static float Square(float x) {
        return x * x;
    }

    static double Square(double x) {
        return x * x;
    }
}
```
<span data-ttu-id="04edb-1371">`A.f` поле инициализируется с делегатом, который ссылается на второй `Square` метод, так как этот метод точно соответствует списку формальных параметров и тип возвращаемого значения `DoubleFunc`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1371">the `A.f` field is initialized with a delegate that refers to the second `Square` method because that method exactly matches the formal parameter list and return type of `DoubleFunc`.</span></span> <span data-ttu-id="04edb-1372">Второй `Square` отсутствует, во время компиляции возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="04edb-1372">Had the second `Square` method not been present, a compile-time error would have occurred.</span></span>

#### <a name="anonymous-object-creation-expressions"></a><span data-ttu-id="04edb-1373">Выражения создания анонимных объектов</span><span class="sxs-lookup"><span data-stu-id="04edb-1373">Anonymous object creation expressions</span></span>

<span data-ttu-id="04edb-1374">*Anonymous_object_creation_expression* используется для создания объекта анонимного типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1374">An *anonymous_object_creation_expression* is used to create an object of an anonymous type.</span></span>

```antlr
anonymous_object_creation_expression
    : 'new' anonymous_object_initializer
    ;

anonymous_object_initializer
    : '{' member_declarator_list? '}'
    | '{' member_declarator_list ',' '}'
    ;

member_declarator_list
    : member_declarator (',' member_declarator)*
    ;

member_declarator
    : simple_name
    | member_access
    | base_access
    | null_conditional_member_access
    | identifier '=' expression
    ;
```

<span data-ttu-id="04edb-1375">Инициализатор анонимного объекта объявляет анонимный тип и возвращает экземпляр этого типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1375">An anonymous object initializer declares an anonymous type and returns an instance of that type.</span></span> <span data-ttu-id="04edb-1376">Анонимный тип является типом безымянного класса, который напрямую наследует от `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1376">An anonymous type is a nameless class type that inherits directly from `object`.</span></span> <span data-ttu-id="04edb-1377">Члены анонимного типа представляют собой последовательность свойств только для чтения, которые получены из инициализатора анонимный объект, используемый для создания экземпляра типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1377">The members of an anonymous type are a sequence of read-only properties inferred from the anonymous object initializer used to create an instance of the type.</span></span> <span data-ttu-id="04edb-1378">В частности инициализатор анонимного объекта формы</span><span class="sxs-lookup"><span data-stu-id="04edb-1378">Specifically, an anonymous object initializer of the form</span></span>
```csharp
new { p1 = e1, p2 = e2, ..., pn = en }
```
<span data-ttu-id="04edb-1379">Объявляет анонимный тип формы</span><span class="sxs-lookup"><span data-stu-id="04edb-1379">declares an anonymous type of the form</span></span>
```csharp
class __Anonymous1
{
    private readonly T1 f1;
    private readonly T2 f2;
    ...
    private readonly Tn fn;

    public __Anonymous1(T1 a1, T2 a2, ..., Tn an) {
        f1 = a1;
        f2 = a2;
        ...
        fn = an;
    }

    public T1 p1 { get { return f1; } }
    public T2 p2 { get { return f2; } }
    ...
    public Tn pn { get { return fn; } }

    public override bool Equals(object __o) { ... }
    public override int GetHashCode() { ... }
}
```
<span data-ttu-id="04edb-1380">где каждый `Tx` — это тип соответствующее выражение `ex`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1380">where each `Tx` is the type of the corresponding expression `ex`.</span></span> <span data-ttu-id="04edb-1381">Выражение, используемое в *member_declarator* должно иметь тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1381">The expression used in a *member_declarator* must have a type.</span></span> <span data-ttu-id="04edb-1382">Таким образом, это ошибка времени компиляции для выражения в *member_declarator* быть null или анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1382">Thus, it is a compile-time error for an expression in a *member_declarator* to be null or an anonymous function.</span></span> <span data-ttu-id="04edb-1383">Это также ошибка времени компиляции иметь небезопасный тип выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1383">It is also a compile-time error for the expression to have an unsafe type.</span></span>

<span data-ttu-id="04edb-1384">Имена анонимного типа и параметра для его `Equals` метод автоматически создаются компилятором и нельзя ссылаться в тексте программы.</span><span class="sxs-lookup"><span data-stu-id="04edb-1384">The names of an anonymous type and of the parameter to its `Equals` method are automatically generated by the compiler and cannot be referenced in program text.</span></span>

<span data-ttu-id="04edb-1385">В той же программе два инициализатора анонимных объектов, указывающих последовательность свойств одинаковые имена и типы времени компиляции, в том же порядке, будут создавать экземпляры того же анонимного типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1385">Within the same program, two anonymous object initializers that specify a sequence of properties of the same names and compile-time types in the same order will produce instances of the same anonymous type.</span></span>

<span data-ttu-id="04edb-1386">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-1386">In the example</span></span>
```csharp
var p1 = new { Name = "Lawnmower", Price = 495.00 };
var p2 = new { Name = "Shovel", Price = 26.95 };
p1 = p2;
```
<span data-ttu-id="04edb-1387">Назначение в последней строке разрешен, так как `p1` и `p2` имеют одинаковый анонимный тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1387">the assignment on the last line is permitted because `p1` and `p2` are of the same anonymous type.</span></span>

<span data-ttu-id="04edb-1388">`Equals` И `GetHashcode` методы в анонимных типах переопределить эти методы, унаследованные от `object`и определяются на основе `Equals` и `GetHashcode` свойства, таким образом, чтобы два экземпляра одного анонимного типа равны Если и только в том случае, если равны их свойства.</span><span class="sxs-lookup"><span data-stu-id="04edb-1388">The `Equals` and `GetHashcode` methods on anonymous types override the methods inherited from `object`, and are defined in terms of the `Equals` and `GetHashcode` of the properties, so that two instances of the same anonymous type are equal if and only if all their properties are equal.</span></span>

<span data-ttu-id="04edb-1389">Объявление члена можно сократить до простого имени ([вывод типа](expressions.md#type-inference)), доступ к членам ([Проверка динамического разрешения перегрузки во время компиляции](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), доступ к базовым членам ([базового доступа](expressions.md#base-access)) или доступ к члену с условием null ([выражения условием Null как инициализаторы проекций](expressions.md#null-conditional-expressions-as-projection-initializers)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1389">A member declarator can be abbreviated to a simple name ([Type inference](expressions.md#type-inference)), a member access ([Compile-time checking of dynamic overload resolution](expressions.md#compile-time-checking-of-dynamic-overload-resolution)), a base access ([Base access](expressions.md#base-access)) or a null-conditional member access ([Null-conditional expressions as projection initializers](expressions.md#null-conditional-expressions-as-projection-initializers)).</span></span> <span data-ttu-id="04edb-1390">Это называется ***инициализации проекции*** и является сокращением для объявления и назначения к свойству с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="04edb-1390">This is called a ***projection initializer*** and is shorthand for a declaration of and assignment to a property with the same name.</span></span> <span data-ttu-id="04edb-1391">В частности деклараторы элементов из форм</span><span class="sxs-lookup"><span data-stu-id="04edb-1391">Specifically, member declarators of the forms</span></span>
```csharp
identifier
expr.identifier
```
<span data-ttu-id="04edb-1392">будут точными эквивалентами следующих, соответственно:</span><span class="sxs-lookup"><span data-stu-id="04edb-1392">are precisely equivalent to the following, respectively:</span></span>
```csharp
identifier = identifier
identifier = expr.identifier
```

<span data-ttu-id="04edb-1393">Таким образом, при инициализации проекции *идентификатор* выбирает как значение и поле или свойство, которому присваивается значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1393">Thus, in a projection initializer the *identifier* selects both the value and the field or property to which the value is assigned.</span></span> <span data-ttu-id="04edb-1394">Интуитивно понятным образом инициализатор проекции проектов не только значение, а также имя параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-1394">Intuitively, a projection initializer projects not just a value, but also the name of the value.</span></span>

### <a name="the-typeof-operator"></a><span data-ttu-id="04edb-1395">Оператор typeof</span><span class="sxs-lookup"><span data-stu-id="04edb-1395">The typeof operator</span></span>

<span data-ttu-id="04edb-1396">`typeof` Оператор используется для получения `System.Type` объекта для типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1396">The `typeof` operator is used to obtain the `System.Type` object for a type.</span></span>

```antlr
typeof_expression
    : 'typeof' '(' type ')'
    | 'typeof' '(' unbound_type_name ')'
    | 'typeof' '(' 'void' ')'
    ;

unbound_type_name
    : identifier generic_dimension_specifier?
    | identifier '::' identifier generic_dimension_specifier?
    | unbound_type_name '.' identifier generic_dimension_specifier?
    ;

generic_dimension_specifier
    : '<' comma* '>'
    ;

comma
    : ','
    ;
```

<span data-ttu-id="04edb-1397">В первой форме *typeof_expression* состоит из `typeof` ключевое слово и заключенные в круглые скобки *тип*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1397">The first form of *typeof_expression* consists of a `typeof` keyword followed by a parenthesized *type*.</span></span> <span data-ttu-id="04edb-1398">Результатом выражения этой формы является `System.Type` объект для определенного типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1398">The result of an expression of this form is the `System.Type` object for the indicated type.</span></span> <span data-ttu-id="04edb-1399">Имеется только один `System.Type` объекта для любого типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1399">There is only one `System.Type` object for any given type.</span></span> <span data-ttu-id="04edb-1400">Это означает, что для типа `T`, `typeof(T) == typeof(T)` всегда имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="04edb-1400">This means that for a type `T`, `typeof(T) == typeof(T)` is always true.</span></span> <span data-ttu-id="04edb-1401">*Тип* не может быть `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1401">The *type* cannot be `dynamic`.</span></span>

<span data-ttu-id="04edb-1402">Вторая форма *typeof_expression* состоит из `typeof` ключевое слово и заключенные в круглые скобки *unbound_type_name*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1402">The second form of *typeof_expression* consists of a `typeof` keyword followed by a parenthesized *unbound_type_name*.</span></span> <span data-ttu-id="04edb-1403">*Unbound_type_name* очень похожа на *type_name* ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)) за исключением того, что *unbound_type_name* содержит *generic_dimension_specifier*s где *type_name* содержит *type_argument_list*s.</span><span class="sxs-lookup"><span data-stu-id="04edb-1403">An *unbound_type_name* is very similar to a *type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) except that an *unbound_type_name* contains *generic_dimension_specifier*s where a *type_name* contains *type_argument_list*s.</span></span> <span data-ttu-id="04edb-1404">Когда операнд *typeof_expression* представляет собой последовательность токенов, удовлетворяющий грамматики обоих *unbound_type_name* и *type_name*, а именно при нем ни *generic_dimension_specifier* ни *type_argument_list*, рассматривается как последовательность токенов *type_name*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1404">When the operand of a *typeof_expression* is a sequence of tokens that satisfies the grammars of both *unbound_type_name* and *type_name*, namely when it contains neither a *generic_dimension_specifier* nor a *type_argument_list*, the sequence of tokens is considered to be a *type_name*.</span></span> <span data-ttu-id="04edb-1405">Значение *unbound_type_name* определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1405">The meaning of an *unbound_type_name* is determined as follows:</span></span>

*  <span data-ttu-id="04edb-1406">Преобразовать последовательность токенов *type_name* путем замены каждой *generic_dimension_specifier* с *type_argument_list* с таким же числом запятых и Ключевое слово `object` каждого *type_argument*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1406">Convert the sequence of tokens to a *type_name* by replacing each *generic_dimension_specifier* with a *type_argument_list* having the same number of commas and the keyword `object` as each *type_argument*.</span></span>
*  <span data-ttu-id="04edb-1407">Оцените итоговый *type_name*, игнорируя все ограничения параметра типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1407">Evaluate the resulting *type_name*, while ignoring all type parameter constraints.</span></span>
*  <span data-ttu-id="04edb-1408">*Unbound_type_name* разрешается несвязанного универсального типа, связанный с итоговый сконструированный тип ([привязан и несвязанные типы](types.md#bound-and-unbound-types)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1408">The *unbound_type_name* resolves to the unbound generic type associated with the resulting constructed type ([Bound and unbound types](types.md#bound-and-unbound-types)).</span></span>

<span data-ttu-id="04edb-1409">Результат *typeof_expression* является `System.Type` объект, полученный в результате непривязанным универсального типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1409">The result of the *typeof_expression* is the `System.Type` object for the resulting unbound generic type.</span></span>

<span data-ttu-id="04edb-1410">Третья форма из *typeof_expression* состоит из `typeof` ключевое слово и заключенные в круглые скобки `void` ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="04edb-1410">The third form of *typeof_expression* consists of a `typeof` keyword followed by a parenthesized `void` keyword.</span></span> <span data-ttu-id="04edb-1411">Результатом выражения этой формы является `System.Type` объект, представляющий отсутствие типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1411">The result of an expression of this form is the `System.Type` object that represents the absence of a type.</span></span> <span data-ttu-id="04edb-1412">Тип объекта, возвращаемого `typeof(void)` отличается от объекта типа, возвращаемого для любого типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1412">The type object returned by `typeof(void)` is distinct from the type object returned for any type.</span></span> <span data-ttu-id="04edb-1413">Этот специальный объект типа полезно в библиотеках классов, которые допускают отражение в методы на языке, где этих методов желательно иметь способ представления типа возвращаемого значения, включая void методы, с помощью экземпляра `System.Type`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1413">This special type object is useful in class libraries that allow reflection onto methods in the language, where those methods wish to have a way to represent the return type of any method, including void methods, with an instance of `System.Type`.</span></span>

<span data-ttu-id="04edb-1414">`typeof` Оператор может использоваться для параметра типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1414">The `typeof` operator can be used on a type parameter.</span></span> <span data-ttu-id="04edb-1415">В результате `System.Type` объект типа времени выполнения, который был привязан к параметру типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1415">The result is the `System.Type` object for the run-time type that was bound to the type parameter.</span></span> <span data-ttu-id="04edb-1416">`typeof` Оператор также может использоваться для сконструированного типа или несвязанного универсального типа ([привязан и несвязанные типы](types.md#bound-and-unbound-types)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1416">The `typeof` operator can also be used on a constructed type or an unbound generic type ([Bound and unbound types](types.md#bound-and-unbound-types)).</span></span> <span data-ttu-id="04edb-1417">`System.Type` Объекта для несвязанного универсального типа не является таким же, как `System.Type` объект типа экземпляра.</span><span class="sxs-lookup"><span data-stu-id="04edb-1417">The `System.Type` object for an unbound generic type is not the same as the `System.Type` object of the instance type.</span></span> <span data-ttu-id="04edb-1418">Тип экземпляра всегда является закрытым сконструированным типом во время выполнения таким образом его `System.Type` объект зависит от выполнения аргументов типа, хотя несвязанного универсального типа не имеет типа аргументов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1418">The instance type is always a closed constructed type at run-time so its `System.Type` object depends on the run-time type arguments in use, while the unbound generic type has no type arguments.</span></span>

<span data-ttu-id="04edb-1419">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-1419">The example</span></span>
```csharp
using System;

class X<T>
{
    public static void PrintTypes() {
        Type[] t = {
            typeof(int),
            typeof(System.Int32),
            typeof(string),
            typeof(double[]),
            typeof(void),
            typeof(T),
            typeof(X<T>),
            typeof(X<X<T>>),
            typeof(X<>)
        };
        for (int i = 0; i < t.Length; i++) {
            Console.WriteLine(t[i]);
        }
    }
}

class Test
{
    static void Main() {
        X<int>.PrintTypes();
    }
}
```
<span data-ttu-id="04edb-1420">получается следующий результат:</span><span class="sxs-lookup"><span data-stu-id="04edb-1420">produces the following output:</span></span>
```
System.Int32
System.Int32
System.String
System.Double[]
System.Void
System.Int32
X`1[System.Int32]
X`1[X`1[System.Int32]]
X`1[T]
```

<span data-ttu-id="04edb-1421">Обратите внимание, что `int` и `System.Int32` относятся к одному типу.</span><span class="sxs-lookup"><span data-stu-id="04edb-1421">Note that `int` and `System.Int32` are the same type.</span></span>

<span data-ttu-id="04edb-1422">Также Обратите внимание, что результат `typeof(X<>)` не зависит от аргумента типа, а результат `typeof(X<T>)` does.</span><span class="sxs-lookup"><span data-stu-id="04edb-1422">Also note that the result of `typeof(X<>)` does not depend on the type argument but the result of `typeof(X<T>)` does.</span></span>

### <a name="the-checked-and-unchecked-operators"></a><span data-ttu-id="04edb-1423">Операторы checked и unchecked</span><span class="sxs-lookup"><span data-stu-id="04edb-1423">The checked and unchecked operators</span></span>

<span data-ttu-id="04edb-1424">`checked` И `unchecked` операторы используются для управления ***контекстом проверки переполнения*** для целочисленных арифметических операций и преобразований.</span><span class="sxs-lookup"><span data-stu-id="04edb-1424">The `checked` and `unchecked` operators are used to control the ***overflow checking context*** for integral-type arithmetic operations and conversions.</span></span>

```antlr
checked_expression
    : 'checked' '(' expression ')'
    ;

unchecked_expression
    : 'unchecked' '(' expression ')'
    ;
```

<span data-ttu-id="04edb-1425">`checked` Оператор вычисляет выражение, содержащиеся в проверяемом контексте и `unchecked` оператор вычисляет содержащегося выражения в непроверенном контексте.</span><span class="sxs-lookup"><span data-stu-id="04edb-1425">The `checked` operator evaluates the contained expression in a checked context, and the `unchecked` operator evaluates the contained expression in an unchecked context.</span></span> <span data-ttu-id="04edb-1426">Объект *checked_expression* или *unchecked_expression* в точности соответствует *parenthesized_expression* ([выражения в скобках](expressions.md#parenthesized-expressions)), за исключением того, что автономной выражение вычисляется в заданной контекста проверки переполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1426">A *checked_expression* or *unchecked_expression* corresponds exactly to a *parenthesized_expression* ([Parenthesized expressions](expressions.md#parenthesized-expressions)), except that the contained expression is evaluated in the given overflow checking context.</span></span>

<span data-ttu-id="04edb-1427">Контекст проверки переполнения можно также управлять с помощью `checked` и `unchecked` инструкций ([операторы checked и unchecked](statements.md#the-checked-and-unchecked-statements)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1427">The overflow checking context can also be controlled through the `checked` and `unchecked` statements ([The checked and unchecked statements](statements.md#the-checked-and-unchecked-statements)).</span></span>

<span data-ttu-id="04edb-1428">Следующие операции зависят от контекста, опубликованный консорциумом проверки переполнения `checked` и `unchecked` операторы и операторы:</span><span class="sxs-lookup"><span data-stu-id="04edb-1428">The following operations are affected by the overflow checking context established by the `checked` and `unchecked` operators and statements:</span></span>

*  <span data-ttu-id="04edb-1429">Предопределенный `++` и `--` унарные операторы ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators) и [префиксный инкремент и декремент операторы](expressions.md#prefix-increment-and-decrement-operators)), если операнд имеет целый тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1429">The predefined `++` and `--` unary operators ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators) and [Prefix increment and decrement operators](expressions.md#prefix-increment-and-decrement-operators)), when the operand is of an integral type.</span></span>
*  <span data-ttu-id="04edb-1430">Предопределенный `-` унарный оператор ([унарный минус-оператор](expressions.md#unary-minus-operator)), если операнд является целочисленного типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1430">The predefined `-` unary operator ([Unary minus operator](expressions.md#unary-minus-operator)), when the operand is of an integral type.</span></span>
*  <span data-ttu-id="04edb-1431">Предопределенный `+`, `-`, `*`, и `/` бинарные операторы ([арифметические операторы](expressions.md#arithmetic-operators)), если оба операнда принадлежат целочисленному типу.</span><span class="sxs-lookup"><span data-stu-id="04edb-1431">The predefined `+`, `-`, `*`, and `/` binary operators ([Arithmetic operators](expressions.md#arithmetic-operators)), when both operands are of integral types.</span></span>
*  <span data-ttu-id="04edb-1432">Явных числовых преобразований ([явных числовых преобразований](conversions.md#explicit-numeric-conversions)) из одного целого типа в другой целочисленный тип или из `float` или `double` в целочисленный тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1432">Explicit numeric conversions ([Explicit numeric conversions](conversions.md#explicit-numeric-conversions)) from one integral type to another integral type, or from `float` or `double` to an integral type.</span></span>

<span data-ttu-id="04edb-1433">Когда один из указанных выше операций произвести результат, слишком велико для представления в целевом типе, контекст, в котором операция управляет результирующее поведение:</span><span class="sxs-lookup"><span data-stu-id="04edb-1433">When one of the above operations produce a result that is too large to represent in the destination type, the context in which the operation is performed controls the resulting behavior:</span></span>

*  <span data-ttu-id="04edb-1434">В `checked` контекста, если операция является константным выражением ([константные выражения](expressions.md#constant-expressions)), возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1434">In a `checked` context, if the operation is a constant expression ([Constant expressions](expressions.md#constant-expressions)), a compile-time error occurs.</span></span> <span data-ttu-id="04edb-1435">В противном случае, когда выполняется операция во время выполнения, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1435">Otherwise, when the operation is performed at run-time, a `System.OverflowException` is thrown.</span></span>
*  <span data-ttu-id="04edb-1436">В `unchecked` контекста, результат усекается путем удаления старших разрядов, которые не помещаются в целевой тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1436">In an `unchecked` context, the result is truncated by discarding any high-order bits that do not fit in the destination type.</span></span>

<span data-ttu-id="04edb-1437">Для Неконстантные выражения (выражения, которые вычисляются во время выполнения), которые не заключаются по любому `checked` или `unchecked` операторы или операторы, контекстом проверки переполнения по умолчанию является `unchecked` Если внешние факторы (например, компилятор Переключение и конфигурацией среды выполнения) вызвать для `checked` оценки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1437">For non-constant expressions (expressions that are evaluated at run-time) that are not enclosed by any `checked` or `unchecked` operators or statements, the default overflow checking context is `unchecked` unless external factors (such as compiler switches and execution environment configuration) call for `checked` evaluation.</span></span>

<span data-ttu-id="04edb-1438">Относительно константных выражений (выражения, которые можно полностью вычислить во время компиляции), всегда является контекстом проверки переполнения по умолчанию `checked`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1438">For constant expressions (expressions that can be fully evaluated at compile-time), the default overflow checking context is always `checked`.</span></span> <span data-ttu-id="04edb-1439">Если константное выражение явным образом помещается в `unchecked` контекста, переполнения, возникающие во время компиляции вычисления выражения всегда вызывать ошибки времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1439">Unless a constant expression is explicitly placed in an `unchecked` context, overflows that occur during the compile-time evaluation of the expression always cause compile-time errors.</span></span>

<span data-ttu-id="04edb-1440">Тело анонимной функции не зависит от `checked` или `unchecked` контексты, в которых происходит анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1440">The body of an anonymous function is not affected by `checked` or `unchecked` contexts in which the anonymous function occurs.</span></span>

<span data-ttu-id="04edb-1441">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-1441">In the example</span></span>
```csharp
class Test
{
    static readonly int x = 1000000;
    static readonly int y = 1000000;

    static int F() {
        return checked(x * y);      // Throws OverflowException
    }

    static int G() {
        return unchecked(x * y);    // Returns -727379968
    }

    static int H() {
        return x * y;               // Depends on default
    }
}
```
<span data-ttu-id="04edb-1442">ошибки компиляции не выводятся, поскольку ни одно из выражений может быть вычислено во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1442">no compile-time errors are reported since neither of the expressions can be evaluated at compile-time.</span></span> <span data-ttu-id="04edb-1443">Во время выполнения `F` вызывает метод `System.OverflowException`и `G` метод возвращает-727379968 (младшие 32 бита результата out of range).</span><span class="sxs-lookup"><span data-stu-id="04edb-1443">At run-time, the `F` method throws a `System.OverflowException`, and the `G` method returns -727379968 (the lower 32 bits of the out-of-range result).</span></span> <span data-ttu-id="04edb-1444">Поведение `H` метод зависит от контекста для компиляции проверки переполнения по умолчанию, но это либо совпадает `F` или так же, как `G`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1444">The behavior of the `H` method depends on the default overflow checking context for the compilation, but it is either the same as `F` or the same as `G`.</span></span>

<span data-ttu-id="04edb-1445">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-1445">In the example</span></span>
```csharp
class Test
{
    const int x = 1000000;
    const int y = 1000000;

    static int F() {
        return checked(x * y);      // Compile error, overflow
    }

    static int G() {
        return unchecked(x * y);    // Returns -727379968
    }

    static int H() {
        return x * y;               // Compile error, overflow
    }
}
```
<span data-ttu-id="04edb-1446">переполнения, возникающие при вычислении константных выражений в `F` и `H` привести к ошибкам во время компиляции, потому что выражения вычисляются в `checked` контекста.</span><span class="sxs-lookup"><span data-stu-id="04edb-1446">the overflows that occur when evaluating the constant expressions in `F` and `H` cause compile-time errors to be reported because the expressions are evaluated in a `checked` context.</span></span> <span data-ttu-id="04edb-1447">Также может произойти переполнение при вычислении константного выражения в `G`, но поскольку вычисление выполняется `unchecked` контекста, переполнение не сообщается.</span><span class="sxs-lookup"><span data-stu-id="04edb-1447">An overflow also occurs when evaluating the constant expression in `G`, but since the evaluation takes place in an `unchecked` context, the overflow is not reported.</span></span>

<span data-ttu-id="04edb-1448">`checked` И `unchecked` операторы влияют только на контекст для тех операций, содержащихся в текстовой форме проверки переполнения "`(`«и»`)`" маркеров.</span><span class="sxs-lookup"><span data-stu-id="04edb-1448">The `checked` and `unchecked` operators only affect the overflow checking context for those operations that are textually contained within the "`(`" and "`)`" tokens.</span></span> <span data-ttu-id="04edb-1449">Операторы не оказывают влияния на функции-члены, которые будут вызываться в результате вычисления выражения автономной.</span><span class="sxs-lookup"><span data-stu-id="04edb-1449">The operators have no effect on function members that are invoked as a result of evaluating the contained expression.</span></span> <span data-ttu-id="04edb-1450">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-1450">In the example</span></span>
```csharp
class Test
{
    static int Multiply(int x, int y) {
        return x * y;
    }

    static int F() {
        return checked(Multiply(1000000, 1000000));
    }
}
```
<span data-ttu-id="04edb-1451">Использование `checked` в `F` не влияет на вычисления `x * y` в `Multiply`, поэтому `x * y` вычисляется в контекст проверки переполнения по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="04edb-1451">the use of `checked` in `F` does not affect the evaluation of `x * y` in `Multiply`, so `x * y` is evaluated in the default overflow checking context.</span></span>

<span data-ttu-id="04edb-1452">`unchecked` Оператор удобно при написании константы целочисленных типов со знаком в шестнадцатеричном формате.</span><span class="sxs-lookup"><span data-stu-id="04edb-1452">The `unchecked` operator is convenient when writing constants of the signed integral types in hexadecimal notation.</span></span> <span data-ttu-id="04edb-1453">Пример:</span><span class="sxs-lookup"><span data-stu-id="04edb-1453">For example:</span></span>
```csharp
class Test
{
    public const int AllBits = unchecked((int)0xFFFFFFFF);

    public const int HighBit = unchecked((int)0x80000000);
}
```

<span data-ttu-id="04edb-1454">Оба шестнадцатеричные константы выше относятся к типу `uint`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1454">Both of the hexadecimal constants above are of type `uint`.</span></span> <span data-ttu-id="04edb-1455">Так как используются следующие константы за пределами `int` диапазон "," без `unchecked` оператор, приведения в `int` будет приводить к ошибкам компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1455">Because the constants are outside the `int` range, without the `unchecked` operator, the casts to `int` would produce compile-time errors.</span></span>

<span data-ttu-id="04edb-1456">`checked` И `unchecked` операторы и операторы позволяют программистам управлять некоторыми аспектами некоторых числовых вычислений.</span><span class="sxs-lookup"><span data-stu-id="04edb-1456">The `checked` and `unchecked` operators and statements allow programmers to control certain aspects of some numeric calculations.</span></span> <span data-ttu-id="04edb-1457">Тем не менее поведение некоторых числовых операторов зависит от типов данных их операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1457">However, the behavior of some numeric operators depends on their operands' data types.</span></span> <span data-ttu-id="04edb-1458">Например, умножение двух десятичных чисел всегда вызывает исключение в случае переполнения даже в явно `unchecked` построения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1458">For example, multiplying two decimals always results in an exception on overflow even within an explicitly `unchecked` construct.</span></span> <span data-ttu-id="04edb-1459">Аналогичным образом, умножение двух смещает никогда не результатов в исключение в случае переполнения даже в явно `checked` построения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1459">Similarly, multiplying two floats never results in an exception on overflow even within an explicitly `checked` construct.</span></span> <span data-ttu-id="04edb-1460">Кроме того, другие операторы никогда не затрагивает режимом проверки, как по умолчанию или неявным.</span><span class="sxs-lookup"><span data-stu-id="04edb-1460">In addition, other operators are never affected by the mode of checking, whether default or explicit.</span></span>

### <a name="default-value-expressions"></a><span data-ttu-id="04edb-1461">Выражения значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="04edb-1461">Default value expressions</span></span>

<span data-ttu-id="04edb-1462">Выражение значения по умолчанию используется для получения значения по умолчанию ([значения по умолчанию](variables.md#default-values)) типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1462">A default value expression is used to obtain the default value ([Default values](variables.md#default-values)) of a type.</span></span> <span data-ttu-id="04edb-1463">Обычно выражение значения по умолчанию используется для параметров типа, так как он не может быть известен, если параметр типа является типом значения или ссылочным типом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1463">Typically a default value expression is used for type parameters, since it may not be known if the type parameter is a value type or a reference type.</span></span> <span data-ttu-id="04edb-1464">(Не существует преобразования из `null` литерала к параметру типа, если не известно, параметр типа ссылочным типом.)</span><span class="sxs-lookup"><span data-stu-id="04edb-1464">(No conversion exists from the `null` literal to a type parameter unless the type parameter is known to be a reference type.)</span></span>

```antlr
default_value_expression
    : 'default' '(' type ')'
    ;
```

<span data-ttu-id="04edb-1465">Если *тип* в *default_value_expression* оценивает во время выполнения для ссылочного типа, результатом является `null` привести к этому типу.</span><span class="sxs-lookup"><span data-stu-id="04edb-1465">If the *type* in a *default_value_expression* evaluates at run-time to a reference type, the result is `null` converted to that type.</span></span> <span data-ttu-id="04edb-1466">Если *тип* в *default_value_expression* оценивает во время выполнения к типу значения, результатом является *value_type*значение по умолчанию ([по умолчанию конструкторы](types.md#default-constructors)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1466">If the *type* in a *default_value_expression* evaluates at run-time to a value type, the result is the *value_type*'s default value ([Default constructors](types.md#default-constructors)).</span></span>

<span data-ttu-id="04edb-1467">Объект *default_value_expression* является константным выражением ([константные выражения](expressions.md#constant-expressions)) Если тип является ссылочным типом или параметром типа, который известен быть ссылочным типом ([параметр типа ограничения](classes.md#type-parameter-constraints)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1467">A *default_value_expression* is a constant expression ([Constant expressions](expressions.md#constant-expressions)) if the type is a reference type or a type parameter that is known to be a reference type ([Type parameter constraints](classes.md#type-parameter-constraints)).</span></span> <span data-ttu-id="04edb-1468">Кроме того *default_value_expression* является константным выражением, в том случае, если тип является одним из следующих типов значений: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, или любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-1468">In addition, a *default_value_expression* is a constant expression if the type is one of the following value types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, or any enumeration type.</span></span>


### <a name="nameof-expressions"></a><span data-ttu-id="04edb-1469">Выражения Nameof</span><span class="sxs-lookup"><span data-stu-id="04edb-1469">Nameof expressions</span></span>

<span data-ttu-id="04edb-1470">Объект *nameof_expression* используется для получения имени сущность программы как строковую константу.</span><span class="sxs-lookup"><span data-stu-id="04edb-1470">A *nameof_expression* is used to obtain the name of a program entity as a constant string.</span></span>

```antlr
nameof_expression
    : 'nameof' '(' named_entity ')'
    ;

named_entity
    : simple_name
    | named_entity_target '.' identifier type_argument_list?
    ;

named_entity_target
    : 'this'
    | 'base'
    | named_entity 
    | predefined_type 
    | qualified_alias_member
    ;
```

<span data-ttu-id="04edb-1471">Грамматически говоря, *named_entity* операнд всегда представляет собой выражение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1471">Grammatically speaking, the *named_entity* operand is always an expression.</span></span> <span data-ttu-id="04edb-1472">Так как `nameof` не является зарезервированным ключевым словом выражения nameof всегда синтаксически неоднозначно в вызов простое имя `nameof`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1472">Because `nameof` is not a reserved keyword, a nameof expression is always syntactically ambiguous with an invocation of the simple name `nameof`.</span></span> <span data-ttu-id="04edb-1473">По причинам совместимости, если при поиске имени ([простые имена](expressions.md#simple-names)) с именем `nameof` завершается успешно, выражение рассматривается как *invocation_expression* — независимо от того, является ли вызов Юридические.</span><span class="sxs-lookup"><span data-stu-id="04edb-1473">For compatibility reasons, if a name lookup ([Simple names](expressions.md#simple-names)) of the name `nameof` succeeds, the expression is treated as an *invocation_expression* -- regardless of whether the invocation is legal.</span></span> <span data-ttu-id="04edb-1474">В противном случае это *nameof_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1474">Otherwise it is a *nameof_expression*.</span></span>

<span data-ttu-id="04edb-1475">Значение *named_entity* из *nameof_expression* означает его как выражение; то есть, либо как *simple_name*, *base_access*  или *member_access*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1475">The meaning of the *named_entity* of a *nameof_expression* is the meaning of it as an expression; that is, either as a *simple_name*, a *base_access* or a *member_access*.</span></span> <span data-ttu-id="04edb-1476">Тем не менее, где поиска описано в разделе [простые имена](expressions.md#simple-names) и [доступ к членам](expressions.md#member-access) приводит к ошибке, так как член экземпляра был найден в статическом контексте *nameof_expression*создает ошибки не.</span><span class="sxs-lookup"><span data-stu-id="04edb-1476">However, where the lookup described in [Simple names](expressions.md#simple-names) and [Member access](expressions.md#member-access) results in an error because an instance member was found in a static context, a *nameof_expression* produces no such error.</span></span>

<span data-ttu-id="04edb-1477">Произошла ошибка во время компиляции для *named_entity* обозначающий группу методов, чтобы *type_argument_list*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1477">It is a compile-time error for a *named_entity* designating a method group to have a *type_argument_list*.</span></span> <span data-ttu-id="04edb-1478">Это ошибка времени компиляции для *named_entity_target* как имеющие тип `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1478">It is a compile time error for a *named_entity_target* to have the type `dynamic`.</span></span>

<span data-ttu-id="04edb-1479">Объект *nameof_expression* — это константное выражение типа `string`, и не оказывает влияния во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1479">A *nameof_expression* is a constant expression of type `string`, and has no effect at runtime.</span></span> <span data-ttu-id="04edb-1480">В частности его *named_entity* не вычисляется и учитывается для целей анализа определенного присваивания ([общие правила для простых выражений](variables.md#general-rules-for-simple-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1480">Specifically, its *named_entity* is not evaluated, and is ignored for the purposes of definite assignment analysis ([General rules for simple expressions](variables.md#general-rules-for-simple-expressions)).</span></span> <span data-ttu-id="04edb-1481">Его значение является идентификатором последнего *named_entity* необязательно окончательной *type_argument_list*, преобразованные следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1481">Its value is the last identifier of the *named_entity* before the optional final *type_argument_list*, transformed in the following way:</span></span>

* <span data-ttu-id="04edb-1482">Префикс "`@`«, если используется, удаляется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1482">The prefix "`@`", if used, is removed.</span></span>
* <span data-ttu-id="04edb-1483">Каждый *unicode_escape_sequence* преобразуется в соответствующий символ Юникода.</span><span class="sxs-lookup"><span data-stu-id="04edb-1483">Each *unicode_escape_sequence* is transformed into its corresponding Unicode character.</span></span>
* <span data-ttu-id="04edb-1484">Любой *formatting_characters* удаляются.</span><span class="sxs-lookup"><span data-stu-id="04edb-1484">Any *formatting_characters* are removed.</span></span>

<span data-ttu-id="04edb-1485">Это те же преобразования, примененные в [идентификаторы](lexical-structure.md#identifiers) при тестировании равенства между идентификаторами.</span><span class="sxs-lookup"><span data-stu-id="04edb-1485">These are the same transformations applied in [Identifiers](lexical-structure.md#identifiers) when testing equality between identifiers.</span></span>

<span data-ttu-id="04edb-1486">TODO: примеры</span><span class="sxs-lookup"><span data-stu-id="04edb-1486">TODO: examples</span></span>

### <a name="anonymous-method-expressions"></a><span data-ttu-id="04edb-1487">Выражения анонимного метода</span><span class="sxs-lookup"><span data-stu-id="04edb-1487">Anonymous method expressions</span></span>

<span data-ttu-id="04edb-1488">*Anonymous_method_expression* является одним из двух способов определения анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1488">An *anonymous_method_expression* is one of two ways of defining an anonymous function.</span></span> <span data-ttu-id="04edb-1489">Более подробно они описаны в [выражения анонимных функций](expressions.md#anonymous-function-expressions).</span><span class="sxs-lookup"><span data-stu-id="04edb-1489">These are further described in [Anonymous function expressions](expressions.md#anonymous-function-expressions).</span></span>

## <a name="unary-operators"></a><span data-ttu-id="04edb-1490">Унарные операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-1490">Unary operators</span></span>

<span data-ttu-id="04edb-1491">`?`, `+`, `-`, `!`, `~`, `++`, `--`, Приведите, и `await` называются унарные операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-1491">The `?`, `+`, `-`, `!`, `~`, `++`, `--`, cast, and `await` operators are called the unary operators.</span></span>

```antlr
unary_expression
    : primary_expression
    | null_conditional_expression
    | '+' unary_expression
    | '-' unary_expression
    | '!' unary_expression
    | '~' unary_expression
    | pre_increment_expression
    | pre_decrement_expression
    | cast_expression
    | await_expression
    | unary_expression_unsafe
    ;
```

<span data-ttu-id="04edb-1492">Если операнд *unary_expression* имеет тип времени компиляции `dynamic`, он является динамическим ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1492">If the operand of a *unary_expression* has the compile-time type `dynamic`, it is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-1493">В этом случае тип времени компиляции *unary_expression* является `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, используя тип времени выполнения операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1493">In this case the compile-time type of the *unary_expression* is `dynamic`, and the resolution described below will take place at run-time using the run-time type of the operand.</span></span>

### <a name="null-conditional-operator"></a><span data-ttu-id="04edb-1494">Условного оператора</span><span class="sxs-lookup"><span data-stu-id="04edb-1494">Null-conditional operator</span></span>

<span data-ttu-id="04edb-1495">Условного оператора применяется список операций для своего операнда, только в том случае, если этот операнд не равно null.</span><span class="sxs-lookup"><span data-stu-id="04edb-1495">The null-conditional operator applies a list of operations to its operand only if that operand is non-null.</span></span> <span data-ttu-id="04edb-1496">В противном случае результатом применения оператора является `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1496">Otherwise the result of applying the operator is `null`.</span></span>

```antlr
null_conditional_expression
    : primary_expression null_conditional_operations
    ;

null_conditional_operations
    : null_conditional_operations? '?' '.' identifier type_argument_list?
    | null_conditional_operations? '?' '[' argument_list ']'
    | null_conditional_operations '.' identifier type_argument_list?
    | null_conditional_operations '[' argument_list ']'
    | null_conditional_operations '(' argument_list? ')'
    ;
```

<span data-ttu-id="04edb-1497">Список операций можно включить доступ к членам и операции с элементами доступа (которые могут быть условием null), а также вызова.</span><span class="sxs-lookup"><span data-stu-id="04edb-1497">The list of operations can include member access and element access operations (which may themselves be null-conditional), as well as invocation.</span></span>

<span data-ttu-id="04edb-1498">Например, выражение `a.b?[0]?.c()` — *null_conditional_expression* с *primary_expression* `a.b` и *null_conditional_operations* `?[0]` (доступ к элементам с условием null), `?.c` (доступ к членам условием null) и `()` (вызов).</span><span class="sxs-lookup"><span data-stu-id="04edb-1498">For example, the expression `a.b?[0]?.c()` is a *null_conditional_expression* with a *primary_expression* `a.b` and *null_conditional_operations* `?[0]` (null-conditional element access), `?.c` (null-conditional member access) and `()` (invocation).</span></span>

<span data-ttu-id="04edb-1499">Для *null_conditional_expression* `E` с *primary_expression* `P`, позволяют `E0` быть выражением, полученные в текстовой форме, удалив в начале `?`от каждого из *null_conditional_operations* из `E` , имеющих одно.</span><span class="sxs-lookup"><span data-stu-id="04edb-1499">For a *null_conditional_expression* `E` with a *primary_expression* `P`, let `E0` be the expression obtained by textually removing the leading `?` from each of the *null_conditional_operations* of `E` that have one.</span></span> <span data-ttu-id="04edb-1500">По существу `E0` — это выражение, которое должно быть вычислено, если ни одна из проверок значений null, представленный `?`s найти `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1500">Conceptually, `E0` is the expression that will be evaluated if none of the null checks represented by the `?`s do find a `null`.</span></span>

<span data-ttu-id="04edb-1501">Кроме того, предоставить `E1` быть выражением, полученные в текстовой форме, удалив в начале `?` из только первый из *null_conditional_operations* в `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1501">Also, let `E1` be the expression obtained by textually removing the leading `?` from just the first of the *null_conditional_operations* in `E`.</span></span> <span data-ttu-id="04edb-1502">Это может привести к *основное выражение* (если он был только что `?`) или на другой *null_conditional_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1502">This may lead to a *primary-expression* (if there was just one `?`) or to another *null_conditional_expression*.</span></span>

<span data-ttu-id="04edb-1503">Например если `E` выражение `a.b?[0]?.c()`, затем `E0` выражение `a.b[0].c()` и `E1` выражение `a.b[0]?.c()`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1503">For example, if `E` is the expression `a.b?[0]?.c()`, then `E0` is the expression `a.b[0].c()` and `E1` is the expression `a.b[0]?.c()`.</span></span>

<span data-ttu-id="04edb-1504">Если `E0` классифицируется как nothing, затем `E` классифицируется как nothing.</span><span class="sxs-lookup"><span data-stu-id="04edb-1504">If `E0` is classified as nothing, then `E` is classified as nothing.</span></span> <span data-ttu-id="04edb-1505">В противном случае E классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1505">Otherwise E is classified as a value.</span></span>

<span data-ttu-id="04edb-1506">`E0` и `E1` используются для определения значения `E`:</span><span class="sxs-lookup"><span data-stu-id="04edb-1506">`E0` and `E1` are used to determine the meaning of `E`:</span></span>

*  <span data-ttu-id="04edb-1507">Если `E` возникает как *statement_expression* значение `E` является таким же, как инструкция</span><span class="sxs-lookup"><span data-stu-id="04edb-1507">If `E` occurs as a *statement_expression* the meaning of `E` is the same as the statement</span></span>

   ```csharp
   if ((object)P != null) E1;
   ```

   <span data-ttu-id="04edb-1508">за исключением того, что P вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-1508">except that P is evaluated only once.</span></span>

*  <span data-ttu-id="04edb-1509">В противном случае, если `E0` классифицируется как ничего не происходит ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1509">Otherwise, if `E0` is classified as nothing a compile-time error occurs.</span></span>

*  <span data-ttu-id="04edb-1510">В противном случае позволить `T0` быть типом значения `E0`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1510">Otherwise, let `T0` be the type of `E0`.</span></span>

   *  <span data-ttu-id="04edb-1511">Если `T0` является параметром типа, быть ссылочным типом или типом значения, не допускающие значения NULL, возникает ошибка во время компиляции неизвестен.</span><span class="sxs-lookup"><span data-stu-id="04edb-1511">If `T0` is a type parameter that is not known to be a reference type or a non-nullable value type, a compile-time error occurs.</span></span>

   *  <span data-ttu-id="04edb-1512">Если `T0` является типом значения, не допускающие значения NULL, то тип `E` — `T0?`и значение `E` совпадает со значением</span><span class="sxs-lookup"><span data-stu-id="04edb-1512">If `T0` is a non-nullable value type, then the type of `E` is `T0?`, and the meaning of `E` is the same as</span></span>

      ```csharp
      ((object)P == null) ? (T0?)null : E1
      ```

      <span data-ttu-id="04edb-1513">за исключением того, что `P` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-1513">except that `P` is evaluated only once.</span></span>

   *  <span data-ttu-id="04edb-1514">В противном случае тип E — T0, а значение E — так же, как</span><span class="sxs-lookup"><span data-stu-id="04edb-1514">Otherwise the type of E is T0, and the meaning of E is the same as</span></span>

      ```csharp
      ((object)P == null) ? null : E1
      ```

      <span data-ttu-id="04edb-1515">за исключением того, что `P` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-1515">except that `P` is evaluated only once.</span></span>

<span data-ttu-id="04edb-1516">Если `E1` сам *null_conditional_expression*, после чего эти правила применяются опять же, вложение тесты для `null` до более нет `?`элемента, и выражение было сокращено вниз Чтобы основное выражение `E0`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1516">If `E1` is itself a *null_conditional_expression*, then these rules are applied again, nesting the tests for `null` until there are no further `?`'s, and the expression has been reduced all the way down to the primary-expression `E0`.</span></span>

<span data-ttu-id="04edb-1517">Например если выражение `a.b?[0]?.c()` возникает как оператор выражение, AS в инструкции:</span><span class="sxs-lookup"><span data-stu-id="04edb-1517">For example, if the expression `a.b?[0]?.c()` occurs as a statement-expression, as in the statement:</span></span>
```csharp
a.b?[0]?.c();
```
<span data-ttu-id="04edb-1518">его значение эквивалентно:</span><span class="sxs-lookup"><span data-stu-id="04edb-1518">its meaning is equivalent to:</span></span>
```csharp
if (a.b != null) a.b[0]?.c();
```
<span data-ttu-id="04edb-1519">что еще раз эквивалентно:</span><span class="sxs-lookup"><span data-stu-id="04edb-1519">which again is equivalent to:</span></span>
```csharp
if (a.b != null) if (a.b[0] != null) a.b[0].c();
```
<span data-ttu-id="04edb-1520">За исключением того, что `a.b` и `a.b[0]` вычисляются только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-1520">Except that `a.b` and `a.b[0]` are evaluated only once.</span></span>

<span data-ttu-id="04edb-1521">Если он находится в контексте, где его значение используется, как в:</span><span class="sxs-lookup"><span data-stu-id="04edb-1521">If it occurs in a context where its value is used, as in:</span></span>
```csharp
var x = a.b?[0]?.c();
```
<span data-ttu-id="04edb-1522">и Предположим, что тип последний вызов не является типом не поддерживающий значение NULL, его значение эквивалентно:</span><span class="sxs-lookup"><span data-stu-id="04edb-1522">and assuming that the type of the final invocation is not a non-nullable value type, its meaning is equivalent to:</span></span>
```csharp
var x = (a.b == null) ? null : (a.b[0] == null) ? null : a.b[0].c();
```
<span data-ttu-id="04edb-1523">За исключением того, что `a.b` и `a.b[0]` вычисляются только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-1523">except that `a.b` and `a.b[0]` are evaluated only once.</span></span>

#### <a name="null-conditional-expressions-as-projection-initializers"></a><span data-ttu-id="04edb-1524">Выражения с условием NULL как инициализаторы проекций</span><span class="sxs-lookup"><span data-stu-id="04edb-1524">Null-conditional expressions as projection initializers</span></span>

<span data-ttu-id="04edb-1525">Null условное выражение можно использовать только как *member_declarator* в *anonymous_object_creation_expression* ([выражения создания анонимных объектов](expressions.md#anonymous-object-creation-expressions)) Если заканчивается доступ к членам (при необходимости условием null).</span><span class="sxs-lookup"><span data-stu-id="04edb-1525">A null-conditional expression is only allowed as a *member_declarator* in an *anonymous_object_creation_expression* ([Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions)) if it ends with an (optionally null-conditional) member access.</span></span> <span data-ttu-id="04edb-1526">Грамматически это требование можно выразить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1526">Grammatically, this requirement can be expressed as:</span></span>

```antlr
null_conditional_member_access
    : primary_expression null_conditional_operations? '?' '.' identifier type_argument_list?
    | primary_expression null_conditional_operations '.' identifier type_argument_list?
    ;
```

<span data-ttu-id="04edb-1527">Это особый случай грамматики для *null_conditional_expression* выше.</span><span class="sxs-lookup"><span data-stu-id="04edb-1527">This is a special case of the grammar for *null_conditional_expression* above.</span></span> <span data-ttu-id="04edb-1528">Производство для *member_declarator* в [выражения создания анонимных объектов](expressions.md#anonymous-object-creation-expressions) затем включает в себя только *null_conditional_member_access*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1528">The production for *member_declarator* in [Anonymous object creation expressions](expressions.md#anonymous-object-creation-expressions) then includes only *null_conditional_member_access*.</span></span>

#### <a name="null-conditional-expressions-as-statement-expressions"></a><span data-ttu-id="04edb-1529">Выражения условием NULL в качестве выражения с оператором</span><span class="sxs-lookup"><span data-stu-id="04edb-1529">Null-conditional expressions as statement expressions</span></span>

<span data-ttu-id="04edb-1530">Null условное выражение можно использовать только как *statement_expression* ([операторы выражений](statements.md#expression-statements)), если оно станет вызовом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1530">A null-conditional expression is only allowed as a *statement_expression* ([Expression statements](statements.md#expression-statements)) if it ends with an invocation.</span></span> <span data-ttu-id="04edb-1531">Грамматически это требование можно выразить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1531">Grammatically, this requirement can be expressed as:</span></span>

```antlr
null_conditional_invocation_expression
    : primary_expression null_conditional_operations '(' argument_list? ')'
    ;
```

<span data-ttu-id="04edb-1532">Это особый случай грамматики для *null_conditional_expression* выше.</span><span class="sxs-lookup"><span data-stu-id="04edb-1532">This is a special case of the grammar for *null_conditional_expression* above.</span></span> <span data-ttu-id="04edb-1533">Производство для *statement_expression* в [операторы выражений](statements.md#expression-statements) затем включает в себя только *null_conditional_invocation_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1533">The production for *statement_expression* in [Expression statements](statements.md#expression-statements) then includes only *null_conditional_invocation_expression*.</span></span>


### <a name="unary-plus-operator"></a><span data-ttu-id="04edb-1534">Оператор унарного сложения</span><span class="sxs-lookup"><span data-stu-id="04edb-1534">Unary plus operator</span></span>

<span data-ttu-id="04edb-1535">Для операции в виде `+x`, разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1535">For an operation of the form `+x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1536">Операнд преобразуется в тип параметра выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1536">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="04edb-1537">Предопределенные унарные и операторы являются:</span><span class="sxs-lookup"><span data-stu-id="04edb-1537">The predefined unary plus operators are:</span></span>

```csharp
int operator +(int x);
uint operator +(uint x);
long operator +(long x);
ulong operator +(ulong x);
float operator +(float x);
double operator +(double x);
decimal operator +(decimal x);
```

<span data-ttu-id="04edb-1538">Для каждого из этих операторов результатом является просто значение операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1538">For each of these operators, the result is simply the value of the operand.</span></span>

### <a name="unary-minus-operator"></a><span data-ttu-id="04edb-1539">Унарный минус-оператор</span><span class="sxs-lookup"><span data-stu-id="04edb-1539">Unary minus operator</span></span>

<span data-ttu-id="04edb-1540">Для операции в виде `-x`, разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1540">For an operation of the form `-x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1541">Операнд преобразуется в тип параметра выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1541">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="04edb-1542">Ниже перечислены операторы предопределенные отрицания.</span><span class="sxs-lookup"><span data-stu-id="04edb-1542">The predefined negation operators are:</span></span>

*  <span data-ttu-id="04edb-1543">Отрицание целое число:</span><span class="sxs-lookup"><span data-stu-id="04edb-1543">Integer negation:</span></span>

   ```csharp
   int operator -(int x);
   long operator -(long x);
   ```

   <span data-ttu-id="04edb-1544">Результат вычисляется путем вычитания `x` с нуля.</span><span class="sxs-lookup"><span data-stu-id="04edb-1544">The result is computed by subtracting `x` from zero.</span></span> <span data-ttu-id="04edb-1545">Если значение `x` является наименьшим представимым значением для типа операнда (-2 ^ 31 для `int` или -2 ^ 63 для `long`), затем математического отрицания `x` не может быть представлен в тип операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1545">If the value of of `x` is the smallest representable value of the operand type (-2^31 for `int` or -2^63 for `long`), then the mathematical negation of `x` is not representable within the operand type.</span></span> <span data-ttu-id="04edb-1546">В этом случае в `checked` контекста, `System.OverflowException` возникает исключение; если он встречается в `unchecked` контекст, результатом является значение операнда и о переполнении не сообщается.</span><span class="sxs-lookup"><span data-stu-id="04edb-1546">If this occurs within a `checked` context, a `System.OverflowException` is thrown; if it occurs within an `unchecked` context, the result is the value of the operand and the overflow is not reported.</span></span>

   <span data-ttu-id="04edb-1547">Если оператор отрицания операнд имеет тип `uint`, он преобразуется в тип `long`, а тип результата — `long`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1547">If the operand of the negation operator is of type `uint`, it is converted to type `long`, and the type of the result is `long`.</span></span> <span data-ttu-id="04edb-1548">Исключением является правило, которое позволяет `int` значение от -2147483648 (-2 ^ 31) для записи в качестве Десятичный целочисленный литерал ([Целочисленные литералы](lexical-structure.md#integer-literals)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1548">An exception is the rule that permits the `int` value -2147483648 (-2^31) to be written as a decimal integer literal ([Integer literals](lexical-structure.md#integer-literals)).</span></span>

   <span data-ttu-id="04edb-1549">Если оператор отрицания операнд имеет тип `ulong`, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1549">If the operand of the negation operator is of type `ulong`, a compile-time error occurs.</span></span> <span data-ttu-id="04edb-1550">Исключением является правило, которое позволяет `long` значение от -9223372036854775808 (-2 ^ 63) для записи в качестве Десятичный целочисленный литерал ([Целочисленные литералы](lexical-structure.md#integer-literals)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1550">An exception is the rule that permits the `long` value -9223372036854775808 (-2^63) to be written as a decimal integer literal ([Integer literals](lexical-structure.md#integer-literals)).</span></span>

*  <span data-ttu-id="04edb-1551">С плавающей запятой отрицания:</span><span class="sxs-lookup"><span data-stu-id="04edb-1551">Floating-point negation:</span></span>

   ```csharp
   float operator -(float x);
   double operator -(double x);
   ```

   <span data-ttu-id="04edb-1552">Результатом является значение `x` с обратным знаком.</span><span class="sxs-lookup"><span data-stu-id="04edb-1552">The result is the value of `x` with its sign inverted.</span></span> <span data-ttu-id="04edb-1553">Если `x` имеет значение NaN, результат также имеет значение NaN.</span><span class="sxs-lookup"><span data-stu-id="04edb-1553">If `x` is NaN, the result is also NaN.</span></span>

*  <span data-ttu-id="04edb-1554">Decimal отрицания:</span><span class="sxs-lookup"><span data-stu-id="04edb-1554">Decimal negation:</span></span>

   ```csharp
   decimal operator -(decimal x);
   ```

   <span data-ttu-id="04edb-1555">Результат вычисляется путем вычитания `x` с нуля.</span><span class="sxs-lookup"><span data-stu-id="04edb-1555">The result is computed by subtracting `x` from zero.</span></span> <span data-ttu-id="04edb-1556">Равнозначно использованию унарный минус-оператор типа Decimal отрицания `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1556">Decimal negation is equivalent to using the unary minus operator of type `System.Decimal`.</span></span>

### <a name="logical-negation-operator"></a><span data-ttu-id="04edb-1557">Оператор логического отрицания</span><span class="sxs-lookup"><span data-stu-id="04edb-1557">Logical negation operator</span></span>

<span data-ttu-id="04edb-1558">Для операции в виде `!x`, разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1558">For an operation of the form `!x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1559">Операнд преобразуется в тип параметра выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1559">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="04edb-1560">Существует только один стандартный оператор логического отрицания:</span><span class="sxs-lookup"><span data-stu-id="04edb-1560">Only one predefined logical negation operator exists:</span></span>
```csharp
bool operator !(bool x);
```

<span data-ttu-id="04edb-1561">Этот оператор вычисляет логическое отрицание операнда: Если операнд является `true`, в результате `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1561">This operator computes the logical negation of the operand: If the operand is `true`, the result is `false`.</span></span> <span data-ttu-id="04edb-1562">Если операнд является `false`, в результате `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1562">If the operand is `false`, the result is `true`.</span></span>

### <a name="bitwise-complement-operator"></a><span data-ttu-id="04edb-1563">Оператор поразрядного дополнения</span><span class="sxs-lookup"><span data-stu-id="04edb-1563">Bitwise complement operator</span></span>

<span data-ttu-id="04edb-1564">Для операции в виде `~x`, разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1564">For an operation of the form `~x`, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1565">Операнд преобразуется в тип параметра выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1565">The operand is converted to the parameter type of the selected operator, and the type of the result is the return type of the operator.</span></span> <span data-ttu-id="04edb-1566">Ниже перечислены операторы предопределенные поразрядным дополнением значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1566">The predefined bitwise complement operators are:</span></span>
```csharp
int operator ~(int x);
uint operator ~(uint x);
long operator ~(long x);
ulong operator ~(ulong x);
```

<span data-ttu-id="04edb-1567">Для каждого из этих операторов, результатом операции является побитовым дополнением `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1567">For each of these operators, the result of the operation is the bitwise complement of `x`.</span></span>

<span data-ttu-id="04edb-1568">Каждый тип перечисления `E` неявно предоставляется следующий оператор поразрядного дополнения:</span><span class="sxs-lookup"><span data-stu-id="04edb-1568">Every enumeration type `E` implicitly provides the following bitwise complement operator:</span></span>

```csharp
E operator ~(E x);
```

<span data-ttu-id="04edb-1569">Результат вычисления `~x`, где `x` является выражением типа перечисления `E` с базовым типом `U`, именно так же, как оценка `(E)(~(U)x)`, за исключением того, что преобразование в `E` — всегда выполняется в случае, если `unchecked` контекста ([операторы checked и unchecked](expressions.md#the-checked-and-unchecked-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1569">The result of evaluating `~x`, where `x` is an expression of an enumeration type `E` with an underlying type `U`, is exactly the same as evaluating `(E)(~(U)x)`, except that the conversion to `E` is always performed as if in an `unchecked` context ([The checked and unchecked operators](expressions.md#the-checked-and-unchecked-operators)).</span></span>

### <a name="prefix-increment-and-decrement-operators"></a><span data-ttu-id="04edb-1570">Префиксный инкремент и декремент операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-1570">Prefix increment and decrement operators</span></span>

```antlr
pre_increment_expression
    : '++' unary_expression
    ;

pre_decrement_expression
    : '--' unary_expression
    ;
```

<span data-ttu-id="04edb-1571">Операнд префикс инкремента или декремента операции должно быть выражением, классифицируется как переменная, доступ к свойству или индексатору.</span><span class="sxs-lookup"><span data-stu-id="04edb-1571">The operand of a prefix increment or decrement operation must be an expression classified as a variable, a property access, or an indexer access.</span></span> <span data-ttu-id="04edb-1572">Результат операции является значение совпадает с типом операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1572">The result of the operation is a value of the same type as the operand.</span></span>

<span data-ttu-id="04edb-1573">Если увеличить операнд префикса или декремента является свойство или индексатор, свойство или индексатор должны иметь `get` и `set` метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1573">If the operand of a prefix increment or decrement operation is a property or indexer access, the property or indexer must have both a `get` and a `set` accessor.</span></span> <span data-ttu-id="04edb-1574">Если это не так, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1574">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-1575">Разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1575">Unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1576">Предопределенные `++` и `--` операторов существуют для следующих типов: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` , `float`, `double`, `decimal`и любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-1576">Predefined `++` and `--` operators exist for the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, and any enum type.</span></span> <span data-ttu-id="04edb-1577">Предопределенный `++` операторы возвращают значение, полученное путем прибавления единицы к операнд и предварительно определенных `--` операторы возвращают значение, полученное путем вычитания 1 из операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1577">The predefined `++` operators return the value produced by adding 1 to the operand, and the predefined `--` operators return the value produced by subtracting 1 from the operand.</span></span> <span data-ttu-id="04edb-1578">В `checked` контекста, если результат сложения или вычитания находится вне диапазона типа результата, а тип результата — целый тип или тип перечисления, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1578">In a `checked` context, if the result of this addition or subtraction is outside the range of the result type and the result type is an integral type or enum type, a `System.OverflowException` is thrown.</span></span>

<span data-ttu-id="04edb-1579">Во время выполнения обработки приращения префикс или операция формы декремента `++x` или `--x` состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1579">The run-time processing of a prefix increment or decrement operation of the form `++x` or `--x` consists of the following steps:</span></span>

*   <span data-ttu-id="04edb-1580">Если `x` классифицируется как переменная:</span><span class="sxs-lookup"><span data-stu-id="04edb-1580">If `x` is classified as a variable:</span></span>
    * <span data-ttu-id="04edb-1581">`x` вычисляется для создания переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-1581">`x` is evaluated to produce the variable.</span></span>
    * <span data-ttu-id="04edb-1582">Выбранный оператор вызывается со значением `x` аргументом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1582">The selected operator is invoked with the value of `x` as its argument.</span></span>
    * <span data-ttu-id="04edb-1583">Значение, возвращаемое оператором хранится в расположении, указанном при вычислении `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1583">The value returned by the operator is stored in the location given by the evaluation of `x`.</span></span>
    * <span data-ttu-id="04edb-1584">Значение, возвращаемое оператором становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1584">The value returned by the operator becomes the result of the operation.</span></span>
*   <span data-ttu-id="04edb-1585">Если `x` классифицируется как свойство или индексатор доступа:</span><span class="sxs-lookup"><span data-stu-id="04edb-1585">If `x` is classified as a property or indexer access:</span></span>
    * <span data-ttu-id="04edb-1586">Выражение экземпляра (если `x` не `static`) и список аргументов (если `x` имеет доступ к индексатору) связан `x` оцениваются, и полученные результаты используются в последующих `get` и `set` вызовы метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-1586">The instance expression (if `x` is not `static`) and the argument list (if `x` is an indexer access) associated with `x` are evaluated, and the results are used in the subsequent `get` and `set` accessor invocations.</span></span>
    * <span data-ttu-id="04edb-1587">`get` Метод доступа `x` вызывается.</span><span class="sxs-lookup"><span data-stu-id="04edb-1587">The `get` accessor of `x` is invoked.</span></span>
    * <span data-ttu-id="04edb-1588">Выбранный оператор вызывается с помощью значения, возвращенного `get` доступа в качестве аргумента.</span><span class="sxs-lookup"><span data-stu-id="04edb-1588">The selected operator is invoked with the value returned by the `get` accessor as its argument.</span></span>
    * <span data-ttu-id="04edb-1589">`set` Метод доступа `x` вызывается со значением, возвращенным оператором в качестве его `value` аргумент.</span><span class="sxs-lookup"><span data-stu-id="04edb-1589">The `set` accessor of `x` is invoked with the value returned by the operator as its `value` argument.</span></span>
    * <span data-ttu-id="04edb-1590">Значение, возвращаемое оператором становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1590">The value returned by the operator becomes the result of the operation.</span></span>

<span data-ttu-id="04edb-1591">`++` И `--` операторы также поддерживают постфиксная нотация ([постфиксных инкремента и декремента](expressions.md#postfix-increment-and-decrement-operators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1591">The `++` and `--` operators also support postfix notation ([Postfix increment and decrement operators](expressions.md#postfix-increment-and-decrement-operators)).</span></span> <span data-ttu-id="04edb-1592">Как правило, результат `x++` или `x--` является значением `x` до операции, тогда как результат `++x` или `--x` является значением `x` после завершения операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1592">Typically, the result of `x++` or `x--` is the value of `x` before the operation, whereas the result of `++x` or `--x` is the value of `x` after the operation.</span></span> <span data-ttu-id="04edb-1593">В любом случае `x` сам имеет то же значение после выполнения операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1593">In either case, `x` itself has the same value after the operation.</span></span>

<span data-ttu-id="04edb-1594">`operator++` Или `operator--` реализации можно вызывать в префиксной и постфиксной форме.</span><span class="sxs-lookup"><span data-stu-id="04edb-1594">An `operator++` or `operator--` implementation can be invoked using either postfix or prefix notation.</span></span> <span data-ttu-id="04edb-1595">Это не могут существовать разные реализации операторов для обозначения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1595">It is not possible to have separate operator implementations for the two notations.</span></span>

### <a name="cast-expressions"></a><span data-ttu-id="04edb-1596">Выражения приведения</span><span class="sxs-lookup"><span data-stu-id="04edb-1596">Cast expressions</span></span>

<span data-ttu-id="04edb-1597">Объект *cast_expression* используется для явного преобразования выражения в заданный тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1597">A *cast_expression* is used to explicitly convert an expression to a given type.</span></span>

```antlr
cast_expression
    : '(' type ')' unary_expression
    ;
```

<span data-ttu-id="04edb-1598">Объект *cast_expression* формы `(T)E`, где `T` — *тип* и `E` — *unary_expression*, выполняет явно преобразование ([явные преобразования](conversions.md#explicit-conversions)) значения `E` ввода `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1598">A *cast_expression* of the form `(T)E`, where `T` is a *type* and `E` is a *unary_expression*, performs an explicit conversion ([Explicit conversions](conversions.md#explicit-conversions)) of the value of `E` to type `T`.</span></span> <span data-ttu-id="04edb-1599">Если существует явное преобразование из `E` для `T`, возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1599">If no explicit conversion exists from `E` to `T`, a binding-time error occurs.</span></span> <span data-ttu-id="04edb-1600">В противном случае результатом является значение, произведенное явное преобразование.</span><span class="sxs-lookup"><span data-stu-id="04edb-1600">Otherwise, the result is the value produced by the explicit conversion.</span></span> <span data-ttu-id="04edb-1601">Результат всегда классифицируется как значение, даже если `E` обозначает переменную.</span><span class="sxs-lookup"><span data-stu-id="04edb-1601">The result is always classified as a value, even if `E` denotes a variable.</span></span>

<span data-ttu-id="04edb-1602">Грамматика для *cast_expression* приводит к определенным синтаксической неоднозначности.</span><span class="sxs-lookup"><span data-stu-id="04edb-1602">The grammar for a *cast_expression* leads to certain syntactic ambiguities.</span></span> <span data-ttu-id="04edb-1603">Например, выражение `(x)-y` можно интерпретировать как *cast_expression* (приведение `-y` ввода `x`) или как *additive_expression* в сочетании с *parenthesized_expression* (который вычисляет значение `x - y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1603">For example, the expression `(x)-y` could either be interpreted as a *cast_expression* (a cast of `-y` to type `x`) or as an *additive_expression* combined with a *parenthesized_expression* (which computes the value `x - y)`.</span></span>

<span data-ttu-id="04edb-1604">Чтобы устранить *cast_expression* существует неоднозначность, следующее правило: Последовательность из одного или нескольких *маркера*s ([пробелы](lexical-structure.md#white-space)) заключены в круглые скобки, считается начала *cast_expression* только в том случае, если хотя бы одно из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1604">To resolve *cast_expression* ambiguities, the following rule exists: A sequence of one or more *token*s ([White space](lexical-structure.md#white-space)) enclosed in parentheses is considered the start of a *cast_expression* only if at least one of the following are true:</span></span>

*  <span data-ttu-id="04edb-1605">Последовательность лексем имеет правильную грамматику для *тип*, но не для *выражение*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1605">The sequence of tokens is correct grammar for a *type*, but not for an *expression*.</span></span>
*  <span data-ttu-id="04edb-1606">Последовательность лексем имеет правильную грамматику для *тип*, и сразу после закрывающей круглой скобки маркер является маркером "`~`», маркер"`!`», маркер "`(`«,  *Идентификатор* ([последовательностей escape-символов Юникода](lexical-structure.md#unicode-character-escape-sequences)), *литерала* ([литералы](lexical-structure.md#literals)), или любой *ключевое слово*([Ключевые слова](lexical-structure.md#keywords)) за исключением `as` и `is`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1606">The sequence of tokens is correct grammar for a *type*, and the token immediately following the closing parentheses is the token "`~`", the token "`!`", the token "`(`", an *identifier* ([Unicode character escape sequences](lexical-structure.md#unicode-character-escape-sequences)), a *literal* ([Literals](lexical-structure.md#literals)), or any *keyword* ([Keywords](lexical-structure.md#keywords)) except `as` and `is`.</span></span>

<span data-ttu-id="04edb-1607">Термин «правильную грамматику» выше означает только то, что последовательность токенов должны соответствовать конкретного грамматических производства.</span><span class="sxs-lookup"><span data-stu-id="04edb-1607">The term "correct grammar" above means only that the sequence of tokens must conform to the particular grammatical production.</span></span> <span data-ttu-id="04edb-1608">Он специально не учитывает фактическое значение все составные идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-1608">It specifically does not consider the actual meaning of any constituent identifiers.</span></span> <span data-ttu-id="04edb-1609">Например если `x` и `y` являются идентификаторами, затем `x.y` имеет правильную грамматику для типа, даже если `x.y` фактически не указывает на тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1609">For example, if `x` and `y` are identifiers, then `x.y` is correct grammar for a type, even if `x.y` doesn't actually denote a type.</span></span>

<span data-ttu-id="04edb-1610">Из правила устранения неоднозначности следует, что если `x` и `y` являются идентификаторами, `(x)y`, `(x)(y)`, и `(x)(-y)` являются *cast_expression*s, но `(x)-y` — нет, даже если `x` определяет тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-1610">From the disambiguation rule it follows that, if `x` and `y` are identifiers, `(x)y`, `(x)(y)`, and `(x)(-y)` are *cast_expression*s, but `(x)-y` is not, even if `x` identifies a type.</span></span> <span data-ttu-id="04edb-1611">Тем не менее если `x` является ключевым словом, идентифицирующим Предопределенный тип (такие как `int`), а затем все четыре формы являются *cast_expression*s (поскольку такое ключевое слово не может быть выражением само по себе).</span><span class="sxs-lookup"><span data-stu-id="04edb-1611">However, if `x` is a keyword that identifies a predefined type (such as `int`), then all four forms are *cast_expression*s (because such a keyword could not possibly be an expression by itself).</span></span>

### <a name="await-expressions"></a><span data-ttu-id="04edb-1612">Выражения await</span><span class="sxs-lookup"><span data-stu-id="04edb-1612">Await expressions</span></span>

<span data-ttu-id="04edb-1613">Оператор await используется для приостановки вычислений, включающей функции async до завершения асинхронной операции, представленное операндом.</span><span class="sxs-lookup"><span data-stu-id="04edb-1613">The await operator is used to suspend evaluation of the enclosing async function until the asynchronous operation represented by the operand has completed.</span></span>

```antlr
await_expression
    : 'await' unary_expression
    ;
```

<span data-ttu-id="04edb-1614">*Await_expression* допускается только в теле функции async ([итераторы](classes.md#iterators)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1614">An *await_expression* is only allowed in the body of an async function ([Iterators](classes.md#iterators)).</span></span> <span data-ttu-id="04edb-1615">В ближайшем вложенном асинхронной функции *await_expression* не может указываться в этих местах:</span><span class="sxs-lookup"><span data-stu-id="04edb-1615">Within the nearest enclosing async function, an *await_expression* may not occur in these places:</span></span>

*  <span data-ttu-id="04edb-1616">Анонимные функции вложенные (синхронные)</span><span class="sxs-lookup"><span data-stu-id="04edb-1616">Inside a nested (non-async) anonymous function</span></span>
*  <span data-ttu-id="04edb-1617">Внутри блока *lock_statement*</span><span class="sxs-lookup"><span data-stu-id="04edb-1617">Inside the block of a *lock_statement*</span></span>
*  <span data-ttu-id="04edb-1618">В небезопасном контексте.</span><span class="sxs-lookup"><span data-stu-id="04edb-1618">In an unsafe context</span></span>

<span data-ttu-id="04edb-1619">Обратите внимание, что *await_expression* не может использоваться в большинстве мест в *query_expression*, так как их синтаксически преобразуются использовать синхронные лямбда-выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1619">Note that an *await_expression* cannot occur in most places within a *query_expression*, because those are syntactically transformed to use non-async lambda expressions.</span></span>

<span data-ttu-id="04edb-1620">В функцию с модификатором async `await` нельзя использовать в качестве идентификатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1620">Inside of an async function, `await` cannot be used as an identifier.</span></span> <span data-ttu-id="04edb-1621">Таким образом является не синтаксической неоднозначности между await выражения и различных выражений, содержащих идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-1621">There is therefore no syntactic ambiguity between await-expressions and various expressions involving identifiers.</span></span> <span data-ttu-id="04edb-1622">За пределами асинхронные функции `await` выступает в качестве обычного идентификатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1622">Outside of async functions, `await` acts as a normal identifier.</span></span>

<span data-ttu-id="04edb-1623">Операнд *await_expression* называется ***задачи***.</span><span class="sxs-lookup"><span data-stu-id="04edb-1623">The operand of an *await_expression* is called the ***task***.</span></span> <span data-ttu-id="04edb-1624">Он представляет асинхронную операцию, которая может быть не завершено во время *await_expression* вычисляется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1624">It represents an asynchronous operation that may or may not be complete at the time the *await_expression* is evaluated.</span></span> <span data-ttu-id="04edb-1625">Оператор await предназначена для приостановки выполнения включающей функции async, пока не будет завершена ожидаемая задача, а затем получать его результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-1625">The purpose of the await operator is to suspend execution of the enclosing async function until the awaited task is complete, and then obtain its outcome.</span></span>

#### <a name="awaitable-expressions"></a><span data-ttu-id="04edb-1626">Awaitable выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-1626">Awaitable expressions</span></span>

<span data-ttu-id="04edb-1627">Задача выражения await должен быть ***awaitable***.</span><span class="sxs-lookup"><span data-stu-id="04edb-1627">The task of an await expression is required to be ***awaitable***.</span></span> <span data-ttu-id="04edb-1628">Выражение `t` несинхронизируемый, если справедливо одно из следующих условий:</span><span class="sxs-lookup"><span data-stu-id="04edb-1628">An expression `t` is awaitable if one of the following holds:</span></span>

*  <span data-ttu-id="04edb-1629">`t` имеет тип времени компиляции `dynamic`</span><span class="sxs-lookup"><span data-stu-id="04edb-1629">`t` is of compile time type `dynamic`</span></span>
*  <span data-ttu-id="04edb-1630">`t` имеет доступный метод экземпляра или расширения вызывается `GetAwaiter` без параметров и без параметров типа и типом возвращаемого значения `A` для которого все указанные ниже хранения:</span><span class="sxs-lookup"><span data-stu-id="04edb-1630">`t` has an accessible instance or extension method called `GetAwaiter` with no parameters and no type parameters, and a return type `A` for which all of the following hold:</span></span>
   * <span data-ttu-id="04edb-1631">`A` реализует интерфейс `System.Runtime.CompilerServices.INotifyCompletion` (Далее — `INotifyCompletion` для краткости)</span><span class="sxs-lookup"><span data-stu-id="04edb-1631">`A` implements the interface `System.Runtime.CompilerServices.INotifyCompletion` (hereafter known as `INotifyCompletion` for brevity)</span></span>
   * <span data-ttu-id="04edb-1632">`A` имеет свойство доступным для чтения экземпляр `IsCompleted` типа `bool`</span><span class="sxs-lookup"><span data-stu-id="04edb-1632">`A` has an accessible, readable instance property `IsCompleted` of type `bool`</span></span>
   * <span data-ttu-id="04edb-1633">`A` имеет доступным методом экземпляра `GetResult` без параметров и без параметров типа</span><span class="sxs-lookup"><span data-stu-id="04edb-1633">`A` has an accessible instance method `GetResult` with no parameters and no type parameters</span></span>

<span data-ttu-id="04edb-1634">Цель `GetAwaiter` метод должен получать ***awaiter*** для задачи.</span><span class="sxs-lookup"><span data-stu-id="04edb-1634">The purpose of the `GetAwaiter` method is to obtain an ***awaiter*** for the task.</span></span> <span data-ttu-id="04edb-1635">Тип `A` называется ***типа awaiter*** для выражения await.</span><span class="sxs-lookup"><span data-stu-id="04edb-1635">The type `A` is called the ***awaiter type*** for the await expression.</span></span>

<span data-ttu-id="04edb-1636">Цель `IsCompleted` свойство является определение того, если задача уже завершена.</span><span class="sxs-lookup"><span data-stu-id="04edb-1636">The purpose of the `IsCompleted` property is to determine if the task is already complete.</span></span> <span data-ttu-id="04edb-1637">Если Да, нет необходимости для приостановки вычислений.</span><span class="sxs-lookup"><span data-stu-id="04edb-1637">If so, there is no need to suspend evaluation.</span></span>

<span data-ttu-id="04edb-1638">Цель `INotifyCompletion.OnCompleted` метод — зарегистрироваться «продолжение» для задачи; т. е. делегат (типа `System.Action`), будет вызываться после завершения задачи.</span><span class="sxs-lookup"><span data-stu-id="04edb-1638">The purpose of the `INotifyCompletion.OnCompleted` method is to sign up a "continuation" to the task; i.e. a delegate (of type `System.Action`) that will be invoked once the task is complete.</span></span>

<span data-ttu-id="04edb-1639">Цель `GetResult` является метод получения результата задачи, после его завершения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1639">The purpose of the `GetResult` method is to obtain the outcome of the task once it is complete.</span></span> <span data-ttu-id="04edb-1640">Этот результат может быть завершен успешно, возможно, с результирующее значение, или может быть исключение, которое вызывается `GetResult` метод.</span><span class="sxs-lookup"><span data-stu-id="04edb-1640">This outcome may be successful completion, possibly with a result value, or it may be an exception which is thrown by the `GetResult` method.</span></span>

#### <a name="classification-of-await-expressions"></a><span data-ttu-id="04edb-1641">Классификация выражениях await</span><span class="sxs-lookup"><span data-stu-id="04edb-1641">Classification of await expressions</span></span>

<span data-ttu-id="04edb-1642">Выражение `await t` классифицируется так же, как выражение `(t).GetAwaiter().GetResult()`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1642">The expression `await t` is classified the same way as the expression `(t).GetAwaiter().GetResult()`.</span></span> <span data-ttu-id="04edb-1643">Таким образом Если тип возвращаемого значения `GetResult` — `void`, *await_expression* классифицируется как nothing.</span><span class="sxs-lookup"><span data-stu-id="04edb-1643">Thus, if the return type of `GetResult` is `void`, the *await_expression* is classified as nothing.</span></span> <span data-ttu-id="04edb-1644">Если он имеет тип возврата, отличный от void `T`, *await_expression* классифицируется как значение типа `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1644">If it has a non-void return type `T`, the *await_expression* is classified as a value of type `T`.</span></span>

#### <a name="runtime-evaluation-of-await-expressions"></a><span data-ttu-id="04edb-1645">Выражения await вычисления среды выполнения</span><span class="sxs-lookup"><span data-stu-id="04edb-1645">Runtime evaluation of await expressions</span></span>

<span data-ttu-id="04edb-1646">Во время выполнения выражение `await t` вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-1646">At runtime, the expression `await t` is evaluated as follows:</span></span>

*  <span data-ttu-id="04edb-1647">Объект типа awaiter `a` получается путем вычисления выражения `(t).GetAwaiter()`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1647">An awaiter `a` is obtained by evaluating the expression `(t).GetAwaiter()`.</span></span>
*  <span data-ttu-id="04edb-1648">Объект `bool` `b` получается путем вычисления выражения `(a).IsCompleted`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1648">A `bool` `b` is obtained by evaluating the expression `(a).IsCompleted`.</span></span>
*  <span data-ttu-id="04edb-1649">Если `b` — `false` то оценки зависит от того `a` реализует интерфейс `System.Runtime.CompilerServices.ICriticalNotifyCompletion` (Далее — `ICriticalNotifyCompletion` для краткости).</span><span class="sxs-lookup"><span data-stu-id="04edb-1649">If `b` is `false` then evaluation depends on whether `a` implements the interface `System.Runtime.CompilerServices.ICriticalNotifyCompletion` (hereafter known as `ICriticalNotifyCompletion` for brevity).</span></span> <span data-ttu-id="04edb-1650">Эта проверка выполняется при привязке; т. е. во время выполнения при `a` имеет тип времени компиляции `dynamic`и во время компиляции в противном случае.</span><span class="sxs-lookup"><span data-stu-id="04edb-1650">This check is done at binding time; i.e. at runtime if `a` has the compile time type `dynamic`, and at compile time otherwise.</span></span> <span data-ttu-id="04edb-1651">Позвольте `r` обозначения возобновления делегат ([итераторы](classes.md#iterators)):</span><span class="sxs-lookup"><span data-stu-id="04edb-1651">Let `r` denote the resumption delegate ([Iterators](classes.md#iterators)):</span></span>
    * <span data-ttu-id="04edb-1652">Если `a` не реализует `ICriticalNotifyCompletion`, то результатом выражения `(a as (INotifyCompletion)).OnCompleted(r)` вычисляется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1652">If `a` does not implement `ICriticalNotifyCompletion`, then the expression `(a as (INotifyCompletion)).OnCompleted(r)` is evaluated.</span></span>
    * <span data-ttu-id="04edb-1653">Если `a` реализовать `ICriticalNotifyCompletion`, то результатом выражения `(a as (ICriticalNotifyCompletion)).UnsafeOnCompleted(r)` вычисляется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1653">If `a` does implement `ICriticalNotifyCompletion`, then the expression `(a as (ICriticalNotifyCompletion)).UnsafeOnCompleted(r)` is evaluated.</span></span>
    * <span data-ttu-id="04edb-1654">Оценки затем приостанавливается и управление возвращается вызывающему объекту текущего асинхронной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-1654">Evaluation is then suspended, and control is returned to the current caller of the async function.</span></span>
*  <span data-ttu-id="04edb-1655">Либо сразу же после (если `b` был `true`), или после последующего вызова делегата возобновления (если `b` был `false`), выражение `(a).GetResult()` вычисляется.</span><span class="sxs-lookup"><span data-stu-id="04edb-1655">Either immediately after (if `b` was `true`), or upon later invocation of the resumption delegate (if `b` was `false`), the expression `(a).GetResult()` is evaluated.</span></span> <span data-ttu-id="04edb-1656">Если он возвращает значение, это значение является результатом *await_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-1656">If it returns a value, that value is the result of the *await_expression*.</span></span> <span data-ttu-id="04edb-1657">В противном случае результатом будет ничего.</span><span class="sxs-lookup"><span data-stu-id="04edb-1657">Otherwise the result is nothing.</span></span>

<span data-ttu-id="04edb-1658">Объект типа awaiter реализации методов интерфейса `INotifyCompletion.OnCompleted` и `ICriticalNotifyCompletion.UnsafeOnCompleted` должна вызывать делегат `r` вызываемого не более одного раза.</span><span class="sxs-lookup"><span data-stu-id="04edb-1658">An awaiter's implementation of the interface methods `INotifyCompletion.OnCompleted` and `ICriticalNotifyCompletion.UnsafeOnCompleted` should cause the delegate `r` to be invoked at most once.</span></span> <span data-ttu-id="04edb-1659">В противном случае поведение включающей функции async не определено.</span><span class="sxs-lookup"><span data-stu-id="04edb-1659">Otherwise, the behavior of the enclosing async function is undefined.</span></span>

## <a name="arithmetic-operators"></a><span data-ttu-id="04edb-1660">Арифметические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-1660">Arithmetic operators</span></span>

<span data-ttu-id="04edb-1661">`*`, `/`, `%`, `+`, И `-` называются арифметические операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-1661">The `*`, `/`, `%`, `+`, and `-` operators are called the arithmetic operators.</span></span>

```antlr
multiplicative_expression
    : unary_expression
    | multiplicative_expression '*' unary_expression
    | multiplicative_expression '/' unary_expression
    | multiplicative_expression '%' unary_expression
    ;

additive_expression
    : multiplicative_expression
    | additive_expression '+' multiplicative_expression
    | additive_expression '-' multiplicative_expression
    ;
```

<span data-ttu-id="04edb-1662">Если операнд арифметический оператор имеет тип времени компиляции `dynamic`, а затем он динамически связан ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-1662">If an operand of an arithmetic operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-1663">В данном случае является типов во время компиляции выражения `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, используя тип времени выполнения операндов, имеющих указанный тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1663">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

### <a name="multiplication-operator"></a><span data-ttu-id="04edb-1664">Оператор умножения</span><span class="sxs-lookup"><span data-stu-id="04edb-1664">Multiplication operator</span></span>

<span data-ttu-id="04edb-1665">Для операции в виде `x * y`, разрешение перегрузки бинарного оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1665">For an operation of the form `x * y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1666">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1666">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-1667">Ниже перечислены стандартные операторы произведения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1667">The predefined multiplication operators are listed below.</span></span> <span data-ttu-id="04edb-1668">Все операторы вычислить произведение `x` и `y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1668">The operators all compute the product of `x` and `y`.</span></span>

*  <span data-ttu-id="04edb-1669">Произведение целых чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-1669">Integer multiplication:</span></span>

   ```csharp
   int operator *(int x, int y);
   uint operator *(uint x, uint y);
   long operator *(long x, long y);
   ulong operator *(ulong x, ulong y);
   ```

   <span data-ttu-id="04edb-1670">В `checked` контекста, если продукт за пределами диапазона типа результата, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1670">In a `checked` context, if the product is outside the range of the result type, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-1671">В `unchecked` контекст, переполнение не выводятся и удаляются любые существенные старшие разряды вне диапазона типа результата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1671">In an `unchecked` context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.</span></span>


*  <span data-ttu-id="04edb-1672">Умножения с плавающей запятой:</span><span class="sxs-lookup"><span data-stu-id="04edb-1672">Floating-point multiplication:</span></span>

   ```csharp
   float operator *(float x, float y);
   double operator *(double x, double y);
   ```

   <span data-ttu-id="04edb-1673">Произведение вычисляется в соответствии с правилами стандарта IEEE 754 арифметические.</span><span class="sxs-lookup"><span data-stu-id="04edb-1673">The product is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="04edb-1674">Ниже перечислены все возможные сочетания ненулевых значений ограниченная, нули, бесконечностей и NaN результаты.</span><span class="sxs-lookup"><span data-stu-id="04edb-1674">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="04edb-1675">В таблице `x` и `y` являются положительными значениями.</span><span class="sxs-lookup"><span data-stu-id="04edb-1675">In the table, `x` and `y` are positive finite values.</span></span> <span data-ttu-id="04edb-1676">`z` является результатом `x * y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1676">`z` is the result of `x * y`.</span></span> <span data-ttu-id="04edb-1677">Если результат слишком велик для целевого типа, `z` равно бесконечности.</span><span class="sxs-lookup"><span data-stu-id="04edb-1677">If the result is too large for the destination type, `z` is infinity.</span></span> <span data-ttu-id="04edb-1678">Если результат слишком мал для целевого типа, `z` равно нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-1678">If the result is too small for the destination type, `z` is zero.</span></span>

   |      |      |      |     |     |      |      |     |
   |:----:|-----:|:----:|:---:|:---:|:----:|:----:|:----|
   |      | <span data-ttu-id="04edb-1679">+ y</span><span class="sxs-lookup"><span data-stu-id="04edb-1679">+y</span></span>   | <span data-ttu-id="04edb-1680">-y</span><span class="sxs-lookup"><span data-stu-id="04edb-1680">-y</span></span>   | <span data-ttu-id="04edb-1681">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1681">+0</span></span>  | <span data-ttu-id="04edb-1682">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1682">-0</span></span>  | <span data-ttu-id="04edb-1683">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1683">+inf</span></span> | <span data-ttu-id="04edb-1684">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1684">-inf</span></span> | <span data-ttu-id="04edb-1685">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1685">NaN</span></span> | 
   | <span data-ttu-id="04edb-1686">+ x</span><span class="sxs-lookup"><span data-stu-id="04edb-1686">+x</span></span>   | <span data-ttu-id="04edb-1687">+ z</span><span class="sxs-lookup"><span data-stu-id="04edb-1687">+z</span></span>   | <span data-ttu-id="04edb-1688">-z</span><span class="sxs-lookup"><span data-stu-id="04edb-1688">-z</span></span>   | <span data-ttu-id="04edb-1689">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1689">+0</span></span>  | <span data-ttu-id="04edb-1690">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1690">-0</span></span>  | <span data-ttu-id="04edb-1691">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1691">+inf</span></span> | <span data-ttu-id="04edb-1692">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1692">-inf</span></span> | <span data-ttu-id="04edb-1693">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1693">NaN</span></span> | 
   | <span data-ttu-id="04edb-1694">-x</span><span class="sxs-lookup"><span data-stu-id="04edb-1694">-x</span></span>   | <span data-ttu-id="04edb-1695">-z</span><span class="sxs-lookup"><span data-stu-id="04edb-1695">-z</span></span>   | <span data-ttu-id="04edb-1696">+ z</span><span class="sxs-lookup"><span data-stu-id="04edb-1696">+z</span></span>   | <span data-ttu-id="04edb-1697">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1697">-0</span></span>  | <span data-ttu-id="04edb-1698">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1698">+0</span></span>  | <span data-ttu-id="04edb-1699">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1699">-inf</span></span> | <span data-ttu-id="04edb-1700">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1700">+inf</span></span> | <span data-ttu-id="04edb-1701">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1701">NaN</span></span> | 
   | <span data-ttu-id="04edb-1702">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1702">+0</span></span>   | <span data-ttu-id="04edb-1703">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1703">+0</span></span>   | <span data-ttu-id="04edb-1704">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1704">-0</span></span>   | <span data-ttu-id="04edb-1705">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1705">+0</span></span>  | <span data-ttu-id="04edb-1706">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1706">-0</span></span>  | <span data-ttu-id="04edb-1707">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1707">NaN</span></span>  | <span data-ttu-id="04edb-1708">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1708">NaN</span></span>  | <span data-ttu-id="04edb-1709">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1709">NaN</span></span> | 
   | <span data-ttu-id="04edb-1710">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1710">-0</span></span>   | <span data-ttu-id="04edb-1711">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1711">-0</span></span>   | <span data-ttu-id="04edb-1712">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1712">+0</span></span>   | <span data-ttu-id="04edb-1713">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1713">-0</span></span>  | <span data-ttu-id="04edb-1714">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1714">+0</span></span>  | <span data-ttu-id="04edb-1715">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1715">NaN</span></span>  | <span data-ttu-id="04edb-1716">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1716">NaN</span></span>  | <span data-ttu-id="04edb-1717">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1717">NaN</span></span> | 
   | <span data-ttu-id="04edb-1718">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1718">+inf</span></span> | <span data-ttu-id="04edb-1719">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1719">+inf</span></span> | <span data-ttu-id="04edb-1720">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1720">-inf</span></span> | <span data-ttu-id="04edb-1721">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1721">NaN</span></span> | <span data-ttu-id="04edb-1722">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1722">NaN</span></span> | <span data-ttu-id="04edb-1723">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1723">+inf</span></span> | <span data-ttu-id="04edb-1724">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1724">-inf</span></span> | <span data-ttu-id="04edb-1725">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1725">NaN</span></span> | 
   | <span data-ttu-id="04edb-1726">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1726">-inf</span></span> | <span data-ttu-id="04edb-1727">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1727">-inf</span></span> | <span data-ttu-id="04edb-1728">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1728">+inf</span></span> | <span data-ttu-id="04edb-1729">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1729">NaN</span></span> | <span data-ttu-id="04edb-1730">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1730">NaN</span></span> | <span data-ttu-id="04edb-1731">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1731">-inf</span></span> | <span data-ttu-id="04edb-1732">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1732">+inf</span></span> | <span data-ttu-id="04edb-1733">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1733">NaN</span></span> | 
   | <span data-ttu-id="04edb-1734">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1734">NaN</span></span>  | <span data-ttu-id="04edb-1735">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1735">NaN</span></span>  | <span data-ttu-id="04edb-1736">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1736">NaN</span></span>  | <span data-ttu-id="04edb-1737">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1737">NaN</span></span> | <span data-ttu-id="04edb-1738">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1738">NaN</span></span> | <span data-ttu-id="04edb-1739">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1739">NaN</span></span>  | <span data-ttu-id="04edb-1740">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1740">NaN</span></span>  | <span data-ttu-id="04edb-1741">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1741">NaN</span></span> | 

*  <span data-ttu-id="04edb-1742">Произведение десятичных чисел.</span><span class="sxs-lookup"><span data-stu-id="04edb-1742">Decimal multiplication:</span></span>

   ```csharp
   decimal operator *(decimal x, decimal y);
   ```

   <span data-ttu-id="04edb-1743">Если полученное значение слишком велико для представления в `decimal` формат, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1743">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-1744">Если результат слишком мал для представления в `decimal` формате, результат равен нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-1744">If the result value is too small to represent in the `decimal` format, the result is zero.</span></span> <span data-ttu-id="04edb-1745">Масштаб результата, до округления равно сумме шкал двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1745">The scale of the result, before any rounding, is the sum of the scales of the two operands.</span></span>

   <span data-ttu-id="04edb-1746">Равнозначно использованию оператор умножения типа Decimal умножения `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1746">Decimal multiplication is equivalent to using the multiplication operator of type `System.Decimal`.</span></span>


### <a name="division-operator"></a><span data-ttu-id="04edb-1747">Оператор деления</span><span class="sxs-lookup"><span data-stu-id="04edb-1747">Division operator</span></span>

<span data-ttu-id="04edb-1748">Для операции в виде `x / y`, разрешение перегрузки бинарного оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1748">For an operation of the form `x / y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1749">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1749">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-1750">Ниже перечислены стандартные операторы деления.</span><span class="sxs-lookup"><span data-stu-id="04edb-1750">The predefined division operators are listed below.</span></span> <span data-ttu-id="04edb-1751">Все операторы вычисляют частное `x` и `y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1751">The operators all compute the quotient of `x` and `y`.</span></span>

*  <span data-ttu-id="04edb-1752">Деление целых чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-1752">Integer division:</span></span>

   ```csharp
   int operator /(int x, int y);
   uint operator /(uint x, uint y);
   long operator /(long x, long y);
   ulong operator /(ulong x, ulong y);
   ```

   <span data-ttu-id="04edb-1753">Если значение правый операнд равен нулю, `System.DivideByZeroException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1753">If the value of the right operand is zero, a `System.DivideByZeroException` is thrown.</span></span>

   <span data-ttu-id="04edb-1754">Деление округляет результат в сторону нуля.</span><span class="sxs-lookup"><span data-stu-id="04edb-1754">The division rounds the result towards zero.</span></span> <span data-ttu-id="04edb-1755">Таким образом абсолютное значение результата является наибольшее целое число, меньше или равно абсолютному значению частного двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1755">Thus the absolute value of the result is the largest possible integer that is less than or equal to the absolute value of the quotient of the two operands.</span></span> <span data-ttu-id="04edb-1756">Результатом будет нуль или положительное число, если два операнда имеют тот же знак и ноль или отрицательное значение, если два операнда имеют противоположные знаки.</span><span class="sxs-lookup"><span data-stu-id="04edb-1756">The result is zero or positive when the two operands have the same sign and zero or negative when the two operands have opposite signs.</span></span>

   <span data-ttu-id="04edb-1757">Если левый операнд является наименьшим представимым `int` или `long` значение и правый операнд является `-1`, возникает переполнение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1757">If the left operand is the smallest representable `int` or `long` value and the right operand is `-1`, an overflow occurs.</span></span> <span data-ttu-id="04edb-1758">В `checked` контекст, в результате `System.ArithmeticException` (или его подкласс) исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1758">In a `checked` context, this causes a `System.ArithmeticException` (or a subclass thereof) to be thrown.</span></span> <span data-ttu-id="04edb-1759">В `unchecked` контекста, он определяется реализацией указатель, является ли `System.ArithmeticException` (или его подкласс) возникает исключение или недокументированных этим значением, что левого операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-1759">In an `unchecked` context, it is implementation-defined as to whether a `System.ArithmeticException` (or a subclass thereof) is thrown or the overflow goes unreported with the resulting value being that of the left operand.</span></span>

*  <span data-ttu-id="04edb-1760">Деление с плавающей запятой:</span><span class="sxs-lookup"><span data-stu-id="04edb-1760">Floating-point division:</span></span>

   ```csharp
   float operator /(float x, float y);
   double operator /(double x, double y);
   ```

   <span data-ttu-id="04edb-1761">Частное вычисляется в соответствии с правилами стандарта IEEE 754 арифметические.</span><span class="sxs-lookup"><span data-stu-id="04edb-1761">The quotient is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="04edb-1762">Ниже перечислены все возможные сочетания ненулевых значений ограниченная, нули, бесконечностей и NaN результаты.</span><span class="sxs-lookup"><span data-stu-id="04edb-1762">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="04edb-1763">В таблице `x` и `y` являются положительными значениями.</span><span class="sxs-lookup"><span data-stu-id="04edb-1763">In the table, `x` and `y` are positive finite values.</span></span> <span data-ttu-id="04edb-1764">`z` является результатом `x / y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1764">`z` is the result of `x / y`.</span></span> <span data-ttu-id="04edb-1765">Если результат слишком велик для целевого типа, `z` равно бесконечности.</span><span class="sxs-lookup"><span data-stu-id="04edb-1765">If the result is too large for the destination type, `z` is infinity.</span></span> <span data-ttu-id="04edb-1766">Если результат слишком мал для целевого типа, `z` равно нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-1766">If the result is too small for the destination type, `z` is zero.</span></span>

   |      |      |      |      |      |      |      |      |
   |:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
   |      | <span data-ttu-id="04edb-1767">+ y</span><span class="sxs-lookup"><span data-stu-id="04edb-1767">+y</span></span>   | <span data-ttu-id="04edb-1768">-y</span><span class="sxs-lookup"><span data-stu-id="04edb-1768">-y</span></span>   | <span data-ttu-id="04edb-1769">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1769">+0</span></span>   | <span data-ttu-id="04edb-1770">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1770">-0</span></span>   | <span data-ttu-id="04edb-1771">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1771">+inf</span></span> | <span data-ttu-id="04edb-1772">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1772">-inf</span></span> | <span data-ttu-id="04edb-1773">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1773">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1774">+ x</span><span class="sxs-lookup"><span data-stu-id="04edb-1774">+x</span></span>   | <span data-ttu-id="04edb-1775">+ z</span><span class="sxs-lookup"><span data-stu-id="04edb-1775">+z</span></span>   | <span data-ttu-id="04edb-1776">-z</span><span class="sxs-lookup"><span data-stu-id="04edb-1776">-z</span></span>   | <span data-ttu-id="04edb-1777">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1777">+inf</span></span> | <span data-ttu-id="04edb-1778">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1778">-inf</span></span> | <span data-ttu-id="04edb-1779">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1779">+0</span></span>   | <span data-ttu-id="04edb-1780">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1780">-0</span></span>   | <span data-ttu-id="04edb-1781">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1781">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1782">-x</span><span class="sxs-lookup"><span data-stu-id="04edb-1782">-x</span></span>   | <span data-ttu-id="04edb-1783">-z</span><span class="sxs-lookup"><span data-stu-id="04edb-1783">-z</span></span>   | <span data-ttu-id="04edb-1784">+ z</span><span class="sxs-lookup"><span data-stu-id="04edb-1784">+z</span></span>   | <span data-ttu-id="04edb-1785">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1785">-inf</span></span> | <span data-ttu-id="04edb-1786">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1786">+inf</span></span> | <span data-ttu-id="04edb-1787">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1787">-0</span></span>   | <span data-ttu-id="04edb-1788">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1788">+0</span></span>   | <span data-ttu-id="04edb-1789">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1789">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1790">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1790">+0</span></span>   | <span data-ttu-id="04edb-1791">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1791">+0</span></span>   | <span data-ttu-id="04edb-1792">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1792">-0</span></span>   | <span data-ttu-id="04edb-1793">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1793">NaN</span></span>  | <span data-ttu-id="04edb-1794">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1794">NaN</span></span>  | <span data-ttu-id="04edb-1795">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1795">+0</span></span>   | <span data-ttu-id="04edb-1796">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1796">-0</span></span>   | <span data-ttu-id="04edb-1797">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1797">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1798">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1798">-0</span></span>   | <span data-ttu-id="04edb-1799">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1799">-0</span></span>   | <span data-ttu-id="04edb-1800">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1800">+0</span></span>   | <span data-ttu-id="04edb-1801">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1801">NaN</span></span>  | <span data-ttu-id="04edb-1802">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1802">NaN</span></span>  | <span data-ttu-id="04edb-1803">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1803">-0</span></span>   | <span data-ttu-id="04edb-1804">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1804">+0</span></span>   | <span data-ttu-id="04edb-1805">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1805">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1806">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1806">+inf</span></span> | <span data-ttu-id="04edb-1807">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1807">+inf</span></span> | <span data-ttu-id="04edb-1808">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1808">-inf</span></span> | <span data-ttu-id="04edb-1809">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1809">+inf</span></span> | <span data-ttu-id="04edb-1810">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1810">-inf</span></span> | <span data-ttu-id="04edb-1811">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1811">NaN</span></span>  | <span data-ttu-id="04edb-1812">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1812">NaN</span></span>  | <span data-ttu-id="04edb-1813">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1813">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1814">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1814">-inf</span></span> | <span data-ttu-id="04edb-1815">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1815">-inf</span></span> | <span data-ttu-id="04edb-1816">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1816">+inf</span></span> | <span data-ttu-id="04edb-1817">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1817">-inf</span></span> | <span data-ttu-id="04edb-1818">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1818">+inf</span></span> | <span data-ttu-id="04edb-1819">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1819">NaN</span></span>  | <span data-ttu-id="04edb-1820">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1820">NaN</span></span>  | <span data-ttu-id="04edb-1821">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1821">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1822">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1822">NaN</span></span>  | <span data-ttu-id="04edb-1823">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1823">NaN</span></span>  | <span data-ttu-id="04edb-1824">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1824">NaN</span></span>  | <span data-ttu-id="04edb-1825">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1825">NaN</span></span>  | <span data-ttu-id="04edb-1826">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1826">NaN</span></span>  | <span data-ttu-id="04edb-1827">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1827">NaN</span></span>  | <span data-ttu-id="04edb-1828">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1828">NaN</span></span>  | <span data-ttu-id="04edb-1829">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1829">NaN</span></span>  | 

*  <span data-ttu-id="04edb-1830">Деление десятичных чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-1830">Decimal division:</span></span>

   ```csharp
   decimal operator /(decimal x, decimal y);
   ```

   <span data-ttu-id="04edb-1831">Если значение правый операнд равен нулю, `System.DivideByZeroException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1831">If the value of the right operand is zero, a `System.DivideByZeroException` is thrown.</span></span> <span data-ttu-id="04edb-1832">Если полученное значение слишком велико для представления в `decimal` формат, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1832">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-1833">Если результат слишком мал для представления в `decimal` формате, результат равен нулю.</span><span class="sxs-lookup"><span data-stu-id="04edb-1833">If the result value is too small to represent in the `decimal` format, the result is zero.</span></span> <span data-ttu-id="04edb-1834">Масштаб результата является наименьшим шкалы, сохранит результат равен ближайшему представимым десятичное значение для true математический результат.</span><span class="sxs-lookup"><span data-stu-id="04edb-1834">The scale of the result is the smallest scale that will preserve a result equal to the nearest representable decimal value to the true mathematical result.</span></span>

   <span data-ttu-id="04edb-1835">Деление десятичных чисел эквивалентно использованию оператора деления типа `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1835">Decimal division is equivalent to using the division operator of type `System.Decimal`.</span></span>


### <a name="remainder-operator"></a><span data-ttu-id="04edb-1836">Оператор остатка</span><span class="sxs-lookup"><span data-stu-id="04edb-1836">Remainder operator</span></span>

<span data-ttu-id="04edb-1837">Для операции в виде `x % y`, разрешение перегрузки бинарного оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1837">For an operation of the form `x % y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1838">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1838">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-1839">Ниже перечислены стандартные операторы остатка.</span><span class="sxs-lookup"><span data-stu-id="04edb-1839">The predefined remainder operators are listed below.</span></span> <span data-ttu-id="04edb-1840">Все операторы вычисления остатка от деления `x` и `y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1840">The operators all compute the remainder of the division between `x` and `y`.</span></span>

*  <span data-ttu-id="04edb-1841">Целочисленный остаток:</span><span class="sxs-lookup"><span data-stu-id="04edb-1841">Integer remainder:</span></span>

   ```csharp
   int operator %(int x, int y);
   uint operator %(uint x, uint y);
   long operator %(long x, long y);
   ulong operator %(ulong x, ulong y);
   ```

   <span data-ttu-id="04edb-1842">Результат `x % y` является значение, полученное путем `x - (x / y) * y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1842">The result of `x % y` is the value produced by `x - (x / y) * y`.</span></span> <span data-ttu-id="04edb-1843">Если `y` равен нулю, `System.DivideByZeroException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1843">If `y` is zero, a `System.DivideByZeroException` is thrown.</span></span>

   <span data-ttu-id="04edb-1844">Если левый операнд — наименьшей `int` или `long` значение и правый операнд является `-1`, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1844">If the left operand is the smallest `int` or `long` value and the right operand is `-1`, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-1845">В любом случае выполняет `x % y` создания исключения, где `x / y` не вызовет исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1845">In no case does `x % y` throw an exception where `x / y` would not throw an exception.</span></span>

*  <span data-ttu-id="04edb-1846">Остаток с плавающей запятой:</span><span class="sxs-lookup"><span data-stu-id="04edb-1846">Floating-point remainder:</span></span>

   ```csharp
   float operator %(float x, float y);
   double operator %(double x, double y);
   ```

   <span data-ttu-id="04edb-1847">Ниже перечислены все возможные сочетания ненулевых значений ограниченная, нули, бесконечностей и NaN результаты.</span><span class="sxs-lookup"><span data-stu-id="04edb-1847">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="04edb-1848">В таблице `x` и `y` являются положительными значениями.</span><span class="sxs-lookup"><span data-stu-id="04edb-1848">In the table, `x` and `y` are positive finite values.</span></span> <span data-ttu-id="04edb-1849">`z` является результатом `x % y` и вычисляется как `x - n * y`, где `n` наибольшее возможных целое число, которое меньше или равно `x / y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1849">`z` is the result of `x % y` and is computed as `x - n * y`, where `n` is the largest possible integer that is less than or equal to `x / y`.</span></span> <span data-ttu-id="04edb-1850">Этот метод вычисления остатка аналогично тому, который использовался для целочисленных операнда, но отличается от определения IEEE 754 (в котором `n` — целое число, ближайшее к `x / y`).</span><span class="sxs-lookup"><span data-stu-id="04edb-1850">This method of computing the remainder is analogous to that used for integer operands, but differs from the IEEE 754 definition (in which `n` is the integer closest to `x / y`).</span></span>

   |      |      |      |      |      |      |      |      |
   |:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
   |      | <span data-ttu-id="04edb-1851">+ y</span><span class="sxs-lookup"><span data-stu-id="04edb-1851">+y</span></span>   | <span data-ttu-id="04edb-1852">-y</span><span class="sxs-lookup"><span data-stu-id="04edb-1852">-y</span></span>   | <span data-ttu-id="04edb-1853">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1853">+0</span></span>   | <span data-ttu-id="04edb-1854">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1854">-0</span></span>   | <span data-ttu-id="04edb-1855">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1855">+inf</span></span> | <span data-ttu-id="04edb-1856">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1856">-inf</span></span> | <span data-ttu-id="04edb-1857">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1857">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1858">+ x</span><span class="sxs-lookup"><span data-stu-id="04edb-1858">+x</span></span>   | <span data-ttu-id="04edb-1859">+ z</span><span class="sxs-lookup"><span data-stu-id="04edb-1859">+z</span></span>   | <span data-ttu-id="04edb-1860">+ z</span><span class="sxs-lookup"><span data-stu-id="04edb-1860">+z</span></span>   | <span data-ttu-id="04edb-1861">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1861">NaN</span></span>  | <span data-ttu-id="04edb-1862">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1862">NaN</span></span>  | <span data-ttu-id="04edb-1863">x</span><span class="sxs-lookup"><span data-stu-id="04edb-1863">x</span></span>    | <span data-ttu-id="04edb-1864">x</span><span class="sxs-lookup"><span data-stu-id="04edb-1864">x</span></span>    | <span data-ttu-id="04edb-1865">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1865">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1866">-x</span><span class="sxs-lookup"><span data-stu-id="04edb-1866">-x</span></span>   | <span data-ttu-id="04edb-1867">-z</span><span class="sxs-lookup"><span data-stu-id="04edb-1867">-z</span></span>   | <span data-ttu-id="04edb-1868">-z</span><span class="sxs-lookup"><span data-stu-id="04edb-1868">-z</span></span>   | <span data-ttu-id="04edb-1869">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1869">NaN</span></span>  | <span data-ttu-id="04edb-1870">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1870">NaN</span></span>  | <span data-ttu-id="04edb-1871">-x</span><span class="sxs-lookup"><span data-stu-id="04edb-1871">-x</span></span>   | <span data-ttu-id="04edb-1872">-x</span><span class="sxs-lookup"><span data-stu-id="04edb-1872">-x</span></span>   | <span data-ttu-id="04edb-1873">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1873">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1874">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1874">+0</span></span>   | <span data-ttu-id="04edb-1875">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1875">+0</span></span>   | <span data-ttu-id="04edb-1876">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1876">+0</span></span>   | <span data-ttu-id="04edb-1877">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1877">NaN</span></span>  | <span data-ttu-id="04edb-1878">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1878">NaN</span></span>  | <span data-ttu-id="04edb-1879">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1879">+0</span></span>   | <span data-ttu-id="04edb-1880">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1880">+0</span></span>   | <span data-ttu-id="04edb-1881">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1881">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1882">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1882">-0</span></span>   | <span data-ttu-id="04edb-1883">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1883">-0</span></span>   | <span data-ttu-id="04edb-1884">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1884">-0</span></span>   | <span data-ttu-id="04edb-1885">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1885">NaN</span></span>  | <span data-ttu-id="04edb-1886">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1886">NaN</span></span>  | <span data-ttu-id="04edb-1887">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1887">-0</span></span>   | <span data-ttu-id="04edb-1888">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1888">-0</span></span>   | <span data-ttu-id="04edb-1889">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1889">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1890">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1890">+inf</span></span> | <span data-ttu-id="04edb-1891">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1891">NaN</span></span>  | <span data-ttu-id="04edb-1892">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1892">NaN</span></span>  | <span data-ttu-id="04edb-1893">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1893">NaN</span></span>  | <span data-ttu-id="04edb-1894">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1894">NaN</span></span>  | <span data-ttu-id="04edb-1895">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1895">NaN</span></span>  | <span data-ttu-id="04edb-1896">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1896">NaN</span></span>  | <span data-ttu-id="04edb-1897">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1897">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1898">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1898">-inf</span></span> | <span data-ttu-id="04edb-1899">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1899">NaN</span></span>  | <span data-ttu-id="04edb-1900">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1900">NaN</span></span>  | <span data-ttu-id="04edb-1901">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1901">NaN</span></span>  | <span data-ttu-id="04edb-1902">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1902">NaN</span></span>  | <span data-ttu-id="04edb-1903">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1903">NaN</span></span>  | <span data-ttu-id="04edb-1904">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1904">NaN</span></span>  | <span data-ttu-id="04edb-1905">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1905">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1906">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1906">NaN</span></span>  | <span data-ttu-id="04edb-1907">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1907">NaN</span></span>  | <span data-ttu-id="04edb-1908">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1908">NaN</span></span>  | <span data-ttu-id="04edb-1909">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1909">NaN</span></span>  | <span data-ttu-id="04edb-1910">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1910">NaN</span></span>  | <span data-ttu-id="04edb-1911">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1911">NaN</span></span>  | <span data-ttu-id="04edb-1912">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1912">NaN</span></span>  | <span data-ttu-id="04edb-1913">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1913">NaN</span></span>  | 

*  <span data-ttu-id="04edb-1914">Остаток для десятичных чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-1914">Decimal remainder:</span></span>

   ```csharp
   decimal operator %(decimal x, decimal y);
   ```

   <span data-ttu-id="04edb-1915">Если значение правый операнд равен нулю, `System.DivideByZeroException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1915">If the value of the right operand is zero, a `System.DivideByZeroException` is thrown.</span></span> <span data-ttu-id="04edb-1916">Масштаб результата, до округления равен большему из масштабов двух операндов, а знак результата, если ненулевое значение, является таким же, как `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1916">The scale of the result, before any rounding, is the larger of the scales of the two operands, and the sign of the result, if non-zero, is the same as that of `x`.</span></span>

   <span data-ttu-id="04edb-1917">Равнозначно использованию оператора вычисления остатка типа Decimal остаток `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1917">Decimal remainder is equivalent to using the remainder operator of type `System.Decimal`.</span></span>


### <a name="addition-operator"></a><span data-ttu-id="04edb-1918">Оператор сложения</span><span class="sxs-lookup"><span data-stu-id="04edb-1918">Addition operator</span></span>

<span data-ttu-id="04edb-1919">Для операции в виде `x + y`, разрешение перегрузки бинарного оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1919">For an operation of the form `x + y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-1920">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-1920">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-1921">Ниже перечислены стандартные операторы сложения.</span><span class="sxs-lookup"><span data-stu-id="04edb-1921">The predefined addition operators are listed below.</span></span> <span data-ttu-id="04edb-1922">Для числовые типы и типы перечисления стандартные операторы сложения вычисляет сумму двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1922">For numeric and enumeration types, the predefined addition operators compute the sum of the two operands.</span></span> <span data-ttu-id="04edb-1923">Если один или оба операнда имеют строковый тип, стандартные операторы сложения СЦЕПИТЬ строковым представлением операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1923">When one or both operands are of type string, the predefined addition operators concatenate the string representation of the operands.</span></span>

*  <span data-ttu-id="04edb-1924">Сложение целых чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-1924">Integer addition:</span></span>

   ```csharp
   int operator +(int x, int y);
   uint operator +(uint x, uint y);
   long operator +(long x, long y);
   ulong operator +(ulong x, ulong y);
   ```

   <span data-ttu-id="04edb-1925">В `checked` контекста, если сумма находится вне диапазона типа результата, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1925">In a `checked` context, if the sum is outside the range of the result type, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-1926">В `unchecked` контекст, переполнение не выводятся и удаляются любые существенные старшие разряды вне диапазона типа результата.</span><span class="sxs-lookup"><span data-stu-id="04edb-1926">In an `unchecked` context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.</span></span>

*  <span data-ttu-id="04edb-1927">Сложение чисел с плавающей запятой:</span><span class="sxs-lookup"><span data-stu-id="04edb-1927">Floating-point addition:</span></span>

   ```csharp
   float operator +(float x, float y);
   double operator +(double x, double y);
   ```

   <span data-ttu-id="04edb-1928">Сумма вычисляется в соответствии с правилами стандарта IEEE 754 арифметические.</span><span class="sxs-lookup"><span data-stu-id="04edb-1928">The sum is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="04edb-1929">Ниже перечислены все возможные сочетания ненулевых значений ограниченная, нули, бесконечностей и NaN результаты.</span><span class="sxs-lookup"><span data-stu-id="04edb-1929">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaN's.</span></span> <span data-ttu-id="04edb-1930">В таблице `x` и `y` являются ненулевыми значениями конечное, и `z` является результатом `x + y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1930">In the table, `x` and `y` are nonzero finite values, and `z` is the result of `x + y`.</span></span> <span data-ttu-id="04edb-1931">Если `x` и `y` имеют одинаковую величину, но противоположные знаки, `z` -положительный ноль.</span><span class="sxs-lookup"><span data-stu-id="04edb-1931">If `x` and `y` have the same magnitude but opposite signs, `z` is positive zero.</span></span> <span data-ttu-id="04edb-1932">Если `x + y` слишком велико для представления в целевом типе, `z` является бесконечным с тот же знак, что `x + y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1932">If `x + y` is too large to represent in the destination type, `z` is an infinity with the same sign as `x + y`.</span></span>

   |      |      |      |      |      |      |      |
   |:----:|:----:|:----:|:----:|:----:|:----:|:----:|
   |      | <span data-ttu-id="04edb-1933">y</span><span class="sxs-lookup"><span data-stu-id="04edb-1933">y</span></span>    | <span data-ttu-id="04edb-1934">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1934">+0</span></span>   | <span data-ttu-id="04edb-1935">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1935">-0</span></span>   | <span data-ttu-id="04edb-1936">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1936">+inf</span></span> | <span data-ttu-id="04edb-1937">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1937">-inf</span></span> | <span data-ttu-id="04edb-1938">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1938">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1939">x</span><span class="sxs-lookup"><span data-stu-id="04edb-1939">x</span></span>    | <span data-ttu-id="04edb-1940">з</span><span class="sxs-lookup"><span data-stu-id="04edb-1940">z</span></span>    | <span data-ttu-id="04edb-1941">x</span><span class="sxs-lookup"><span data-stu-id="04edb-1941">x</span></span>    | <span data-ttu-id="04edb-1942">x</span><span class="sxs-lookup"><span data-stu-id="04edb-1942">x</span></span>    | <span data-ttu-id="04edb-1943">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1943">+inf</span></span> | <span data-ttu-id="04edb-1944">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1944">-inf</span></span> | <span data-ttu-id="04edb-1945">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1945">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1946">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1946">+0</span></span>   | <span data-ttu-id="04edb-1947">y</span><span class="sxs-lookup"><span data-stu-id="04edb-1947">y</span></span>    | <span data-ttu-id="04edb-1948">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1948">+0</span></span>   | <span data-ttu-id="04edb-1949">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1949">+0</span></span>   | <span data-ttu-id="04edb-1950">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1950">+inf</span></span> | <span data-ttu-id="04edb-1951">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1951">-inf</span></span> | <span data-ttu-id="04edb-1952">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1952">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1953">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1953">-0</span></span>   | <span data-ttu-id="04edb-1954">y</span><span class="sxs-lookup"><span data-stu-id="04edb-1954">y</span></span>    | <span data-ttu-id="04edb-1955">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-1955">+0</span></span>   | <span data-ttu-id="04edb-1956">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-1956">-0</span></span>   | <span data-ttu-id="04edb-1957">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1957">+inf</span></span> | <span data-ttu-id="04edb-1958">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1958">-inf</span></span> | <span data-ttu-id="04edb-1959">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1959">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1960">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1960">+inf</span></span> | <span data-ttu-id="04edb-1961">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1961">+inf</span></span> | <span data-ttu-id="04edb-1962">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1962">+inf</span></span> | <span data-ttu-id="04edb-1963">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1963">+inf</span></span> | <span data-ttu-id="04edb-1964">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1964">+inf</span></span> | <span data-ttu-id="04edb-1965">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1965">NaN</span></span>  | <span data-ttu-id="04edb-1966">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1966">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1967">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1967">-inf</span></span> | <span data-ttu-id="04edb-1968">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1968">-inf</span></span> | <span data-ttu-id="04edb-1969">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1969">-inf</span></span> | <span data-ttu-id="04edb-1970">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1970">-inf</span></span> | <span data-ttu-id="04edb-1971">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1971">NaN</span></span>  | <span data-ttu-id="04edb-1972">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-1972">-inf</span></span> | <span data-ttu-id="04edb-1973">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1973">NaN</span></span>  | 
   | <span data-ttu-id="04edb-1974">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1974">NaN</span></span>  | <span data-ttu-id="04edb-1975">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1975">NaN</span></span>  | <span data-ttu-id="04edb-1976">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1976">NaN</span></span>  | <span data-ttu-id="04edb-1977">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1977">NaN</span></span>  | <span data-ttu-id="04edb-1978">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1978">NaN</span></span>  | <span data-ttu-id="04edb-1979">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1979">NaN</span></span>  | <span data-ttu-id="04edb-1980">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-1980">NaN</span></span>  | 

*  <span data-ttu-id="04edb-1981">Сложение десятичных чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-1981">Decimal addition:</span></span>

   ```csharp
   decimal operator +(decimal x, decimal y);
   ```

   <span data-ttu-id="04edb-1982">Если полученное значение слишком велико для представления в `decimal` формат, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-1982">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-1983">Масштаб результата, до округления равен большему из масштабов двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1983">The scale of the result, before any rounding, is the larger of the scales of the two operands.</span></span>

   <span data-ttu-id="04edb-1984">Decimal эквивалентно использование оператора сложения типа `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1984">Decimal addition is equivalent to using the addition operator of type `System.Decimal`.</span></span>

*  <span data-ttu-id="04edb-1985">Помимо этого перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-1985">Enumeration addition.</span></span> <span data-ttu-id="04edb-1986">Каждый тип перечисления неявно предоставляет следующие предварительно определенные операторы, где `E` является типом перечисления и `U` является базовым типом объекта `E`:</span><span class="sxs-lookup"><span data-stu-id="04edb-1986">Every enumeration type implicitly provides the following predefined operators, where `E` is the enum type, and `U` is the underlying type of `E`:</span></span>

   ```csharp
   E operator +(E x, U y);
   E operator +(U x, E y);
   ```

   <span data-ttu-id="04edb-1987">Во время выполнения эти операторы выполняются точно так, как `(E)((U)x + (U)y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1987">At run-time these operators are evaluated exactly as `(E)((U)x + (U)y)`.</span></span>

*  <span data-ttu-id="04edb-1988">Объединение строк:</span><span class="sxs-lookup"><span data-stu-id="04edb-1988">String concatenation:</span></span>

   ```csharp
   string operator +(string x, string y);
   string operator +(string x, object y);
   string operator +(object x, string y);
   ```

   <span data-ttu-id="04edb-1989">Эти перегрузки двоичного файла `+` оператор выполняют объединение строк.</span><span class="sxs-lookup"><span data-stu-id="04edb-1989">These overloads of the binary `+` operator perform string concatenation.</span></span> <span data-ttu-id="04edb-1990">Если операнд операции объединения строк `null`, подставляется пустой строкой.</span><span class="sxs-lookup"><span data-stu-id="04edb-1990">If an operand of string concatenation is `null`, an empty string is substituted.</span></span> <span data-ttu-id="04edb-1991">В противном случае любой аргумент нестроковых преобразуется в строковое представление путем вызова виртуального `ToString` метод наследуется от типа `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1991">Otherwise, any non-string argument is converted to its string representation by invoking the virtual `ToString` method inherited from type `object`.</span></span> <span data-ttu-id="04edb-1992">Если `ToString` возвращает `null`, подставляется пустой строкой.</span><span class="sxs-lookup"><span data-stu-id="04edb-1992">If `ToString` returns `null`, an empty string is substituted.</span></span>

   ```csharp
   using System;
   
   class Test
   {
       static void Main() {
           string s = null;
           Console.WriteLine("s = >" + s + "<");        // displays s = ><
           int i = 1;
           Console.WriteLine("i = " + i);               // displays i = 1
           float f = 1.2300E+15F;
           Console.WriteLine("f = " + f);               // displays f = 1.23E+15
           decimal d = 2.900m;
           Console.WriteLine("d = " + d);               // displays d = 2.900
       }
   }
   ```

   Результат оператора объединения строк является строка, состоящая из символов левого операнда следуют символы правого операнда. Оператор объединения строк никогда не возвращает `null` значение. <span data-ttu-id="04edb-1995">Объект `System.OutOfMemoryException` может быть вызвано, если не хватает памяти для выделения результирующая строка.</span><span class="sxs-lookup"><span data-stu-id="04edb-1995">A `System.OutOfMemoryException` may be thrown if there is not enough memory available to allocate the resulting string.</span></span>

*  <span data-ttu-id="04edb-1996">Объединению делегатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-1996">Delegate combination.</span></span> <span data-ttu-id="04edb-1997">Каждый тип делегата неявно предоставляется следующий стандартный оператор, где `D` является типом делегата:</span><span class="sxs-lookup"><span data-stu-id="04edb-1997">Every delegate type implicitly provides the following predefined operator, where `D` is the delegate type:</span></span>

   ```csharp
   D operator +(D x, D y);
   ```

   <span data-ttu-id="04edb-1998">Двоичный файл `+` оператор выполняет объединение делегатов, когда оба операнда имеют некоторый тип делегата `D`.</span><span class="sxs-lookup"><span data-stu-id="04edb-1998">The binary `+` operator performs delegate combination when both operands are of some delegate type `D`.</span></span> <span data-ttu-id="04edb-1999">(Если операнды имеют разные типы делегатов, происходит ошибка времени привязки.) Если первый операнд имеет `null`, результатом операции является значение второго операнда (даже если это также `null`).</span><span class="sxs-lookup"><span data-stu-id="04edb-1999">(If the operands have different delegate types, a binding-time error occurs.) If the first operand is `null`, the result of the operation is the value of the second operand (even if that is also `null`).</span></span> <span data-ttu-id="04edb-2000">В противном случае, если второй операнд является `null`, то результатом операции является значение первого операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2000">Otherwise, if the second operand is `null`, then the result of the operation is the value of the first operand.</span></span> <span data-ttu-id="04edb-2001">В противном случае результатом операции является новый экземпляр делегата, который, при вызове, вызывает первый операнд и затем вызывает второго операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2001">Otherwise, the result of the operation is a new delegate instance that, when invoked, invokes the first operand and then invokes the second operand.</span></span> <span data-ttu-id="04edb-2002">Примеры объединение делегатов, см. в разделе [оператор вычитания](expressions.md#subtraction-operator) и [вызов делегата](delegates.md#delegate-invocation).</span><span class="sxs-lookup"><span data-stu-id="04edb-2002">For examples of delegate combination, see [Subtraction operator](expressions.md#subtraction-operator) and [Delegate invocation](delegates.md#delegate-invocation).</span></span> <span data-ttu-id="04edb-2003">Так как `System.Delegate` не является типом делегата `operator`  `+` для него не определен.</span><span class="sxs-lookup"><span data-stu-id="04edb-2003">Since `System.Delegate` is not a delegate type, `operator` `+` is not defined for it.</span></span>

### <a name="subtraction-operator"></a><span data-ttu-id="04edb-2004">Оператор вычитания</span><span class="sxs-lookup"><span data-stu-id="04edb-2004">Subtraction operator</span></span>

<span data-ttu-id="04edb-2005">Для операции в виде `x - y`, разрешение перегрузки бинарного оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2005">For an operation of the form `x - y`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-2006">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2006">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-2007">Ниже перечислены стандартные операторы вычитания.</span><span class="sxs-lookup"><span data-stu-id="04edb-2007">The predefined subtraction operators are listed below.</span></span> <span data-ttu-id="04edb-2008">Операторы, все вычесть `y` из `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2008">The operators all subtract `y` from `x`.</span></span>

*  <span data-ttu-id="04edb-2009">Вычитание целых чисел:</span><span class="sxs-lookup"><span data-stu-id="04edb-2009">Integer subtraction:</span></span>

   ```csharp
   int operator -(int x, int y);
   uint operator -(uint x, uint y);
   long operator -(long x, long y);
   ulong operator -(ulong x, ulong y);
   ```

   <span data-ttu-id="04edb-2010">В `checked` контекста, если разница находится вне диапазона типа результата, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2010">In a `checked` context, if the difference is outside the range of the result type, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-2011">В `unchecked` контекст, переполнение не выводятся и удаляются любые существенные старшие разряды вне диапазона типа результата.</span><span class="sxs-lookup"><span data-stu-id="04edb-2011">In an `unchecked` context, overflows are not reported and any significant high-order bits outside the range of the result type are discarded.</span></span>

*  <span data-ttu-id="04edb-2012">Вычитания с плавающей запятой:</span><span class="sxs-lookup"><span data-stu-id="04edb-2012">Floating-point subtraction:</span></span>

   ```csharp
   float operator -(float x, float y);
   double operator -(double x, double y);
   ```

   <span data-ttu-id="04edb-2013">Разность вычисляется в соответствии с правилами стандарта IEEE 754 арифметические.</span><span class="sxs-lookup"><span data-stu-id="04edb-2013">The difference is computed according to the rules of IEEE 754 arithmetic.</span></span> <span data-ttu-id="04edb-2014">Ниже перечислены результаты всех возможных сочетаний ненулевых значений ограниченная, нули, бесконечности и значения NaN.</span><span class="sxs-lookup"><span data-stu-id="04edb-2014">The following table lists the results of all possible combinations of nonzero finite values, zeros, infinities, and NaNs.</span></span> <span data-ttu-id="04edb-2015">В таблице `x` и `y` являются ненулевыми значениями конечное, и `z` является результатом `x - y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2015">In the table, `x` and `y` are nonzero finite values, and `z` is the result of `x - y`.</span></span> <span data-ttu-id="04edb-2016">Если `x` и `y` равны, `z` -положительный ноль.</span><span class="sxs-lookup"><span data-stu-id="04edb-2016">If `x` and `y` are equal, `z` is positive zero.</span></span> <span data-ttu-id="04edb-2017">Если `x - y` слишком велико для представления в целевом типе, `z` является бесконечным с тот же знак, что `x - y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2017">If `x - y` is too large to represent in the destination type, `z` is an infinity with the same sign as `x - y`.</span></span>

   |      |      |      |      |      |      |     |
   |:----:|:----:|:----:|:----:|:----:|:----:|:---:|
   | <span data-ttu-id="04edb-2018">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2018">NaN</span></span>  | <span data-ttu-id="04edb-2019">y</span><span class="sxs-lookup"><span data-stu-id="04edb-2019">y</span></span>    | <span data-ttu-id="04edb-2020">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-2020">+0</span></span>   | <span data-ttu-id="04edb-2021">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-2021">-0</span></span>   | <span data-ttu-id="04edb-2022">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2022">+inf</span></span> | <span data-ttu-id="04edb-2023">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2023">-inf</span></span> | <span data-ttu-id="04edb-2024">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2024">NaN</span></span> | 
   | <span data-ttu-id="04edb-2025">x</span><span class="sxs-lookup"><span data-stu-id="04edb-2025">x</span></span>    | <span data-ttu-id="04edb-2026">з</span><span class="sxs-lookup"><span data-stu-id="04edb-2026">z</span></span>    | <span data-ttu-id="04edb-2027">x</span><span class="sxs-lookup"><span data-stu-id="04edb-2027">x</span></span>    | <span data-ttu-id="04edb-2028">x</span><span class="sxs-lookup"><span data-stu-id="04edb-2028">x</span></span>    | <span data-ttu-id="04edb-2029">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2029">-inf</span></span> | <span data-ttu-id="04edb-2030">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2030">+inf</span></span> | <span data-ttu-id="04edb-2031">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2031">NaN</span></span> | 
   | <span data-ttu-id="04edb-2032">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-2032">+0</span></span>   | <span data-ttu-id="04edb-2033">-y</span><span class="sxs-lookup"><span data-stu-id="04edb-2033">-y</span></span>   | <span data-ttu-id="04edb-2034">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-2034">+0</span></span>   | <span data-ttu-id="04edb-2035">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-2035">+0</span></span>   | <span data-ttu-id="04edb-2036">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2036">-inf</span></span> | <span data-ttu-id="04edb-2037">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2037">+inf</span></span> | <span data-ttu-id="04edb-2038">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2038">NaN</span></span> | 
   | <span data-ttu-id="04edb-2039">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-2039">-0</span></span>   | <span data-ttu-id="04edb-2040">-y</span><span class="sxs-lookup"><span data-stu-id="04edb-2040">-y</span></span>   | <span data-ttu-id="04edb-2041">-0</span><span class="sxs-lookup"><span data-stu-id="04edb-2041">-0</span></span>   | <span data-ttu-id="04edb-2042">+0</span><span class="sxs-lookup"><span data-stu-id="04edb-2042">+0</span></span>   | <span data-ttu-id="04edb-2043">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2043">-inf</span></span> | <span data-ttu-id="04edb-2044">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2044">+inf</span></span> | <span data-ttu-id="04edb-2045">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2045">NaN</span></span> | 
   | <span data-ttu-id="04edb-2046">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2046">+inf</span></span> | <span data-ttu-id="04edb-2047">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2047">+inf</span></span> | <span data-ttu-id="04edb-2048">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2048">+inf</span></span> | <span data-ttu-id="04edb-2049">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2049">+inf</span></span> | <span data-ttu-id="04edb-2050">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2050">NaN</span></span>  | <span data-ttu-id="04edb-2051">+inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2051">+inf</span></span> | <span data-ttu-id="04edb-2052">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2052">NaN</span></span> | 
   | <span data-ttu-id="04edb-2053">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2053">-inf</span></span> | <span data-ttu-id="04edb-2054">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2054">-inf</span></span> | <span data-ttu-id="04edb-2055">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2055">-inf</span></span> | <span data-ttu-id="04edb-2056">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2056">-inf</span></span> | <span data-ttu-id="04edb-2057">-inf</span><span class="sxs-lookup"><span data-stu-id="04edb-2057">-inf</span></span> | <span data-ttu-id="04edb-2058">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2058">NaN</span></span>  | <span data-ttu-id="04edb-2059">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2059">NaN</span></span> | 
   | <span data-ttu-id="04edb-2060">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2060">NaN</span></span>  | <span data-ttu-id="04edb-2061">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2061">NaN</span></span>  | <span data-ttu-id="04edb-2062">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2062">NaN</span></span>  | <span data-ttu-id="04edb-2063">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2063">NaN</span></span>  | <span data-ttu-id="04edb-2064">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2064">NaN</span></span>  | <span data-ttu-id="04edb-2065">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2065">NaN</span></span>  | <span data-ttu-id="04edb-2066">NaN</span><span class="sxs-lookup"><span data-stu-id="04edb-2066">NaN</span></span> | 

*  <span data-ttu-id="04edb-2067">Вычитание десятичных чисел.</span><span class="sxs-lookup"><span data-stu-id="04edb-2067">Decimal subtraction:</span></span>

   ```csharp
   decimal operator -(decimal x, decimal y);
   ```

   <span data-ttu-id="04edb-2068">Если полученное значение слишком велико для представления в `decimal` формат, `System.OverflowException` возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2068">If the resulting value is too large to represent in the `decimal` format, a `System.OverflowException` is thrown.</span></span> <span data-ttu-id="04edb-2069">Масштаб результата, до округления равен большему из масштабов двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2069">The scale of the result, before any rounding, is the larger of the scales of the two operands.</span></span>

   <span data-ttu-id="04edb-2070">Вычитание десятичных чисел эквивалентно использованию оператора вычитания типа `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2070">Decimal subtraction is equivalent to using the subtraction operator of type `System.Decimal`.</span></span>

*  <span data-ttu-id="04edb-2071">Вычитание перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-2071">Enumeration subtraction.</span></span> <span data-ttu-id="04edb-2072">Каждый тип перечисления неявно предоставляется следующий стандартный оператор, где `E` является типом перечисления и `U` является базовым типом объекта `E`:</span><span class="sxs-lookup"><span data-stu-id="04edb-2072">Every enumeration type implicitly provides the following predefined operator, where `E` is the enum type, and `U` is the underlying type of `E`:</span></span>

   ```csharp
   U operator -(E x, E y);
   ```

   <span data-ttu-id="04edb-2073">Этот оператор выполняется точно так, как `(U)((U)x - (U)y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2073">This operator is evaluated exactly as `(U)((U)x - (U)y)`.</span></span> <span data-ttu-id="04edb-2074">Другими словами, оператор вычисляет разницу между порядковыми значениями `x` и `y`, а тип результата — базовый тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-2074">In other words, the operator computes the difference between the ordinal values of `x` and `y`, and the type of the result is the underlying type of the enumeration.</span></span>

   ```csharp
   E operator -(E x, U y);
   ```

   <span data-ttu-id="04edb-2075">Этот оператор выполняется точно так, как `(E)((U)x - y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2075">This operator is evaluated exactly as `(E)((U)x - y)`.</span></span> <span data-ttu-id="04edb-2076">Другими словами оператор вычитает значение из базового типа перечисления, выдавая значение перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-2076">In other words, the operator subtracts a value from the underlying type of the enumeration, yielding a value of the enumeration.</span></span>

*  <span data-ttu-id="04edb-2077">Удаление делегатов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2077">Delegate removal.</span></span> <span data-ttu-id="04edb-2078">Каждый тип делегата неявно предоставляется следующий стандартный оператор, где `D` является типом делегата:</span><span class="sxs-lookup"><span data-stu-id="04edb-2078">Every delegate type implicitly provides the following predefined operator, where `D` is the delegate type:</span></span>

   ```csharp
   D operator -(D x, D y);
   ```

   <span data-ttu-id="04edb-2079">Двоичный файл `-` оператор выполняет удаление делегатов, когда оба операнда имеют некоторый тип делегата `D`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2079">The binary `-` operator performs delegate removal when both operands are of some delegate type `D`.</span></span> <span data-ttu-id="04edb-2080">Если операнды имеют разные типы делегатов, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2080">If the operands have different delegate types, a binding-time error occurs.</span></span> <span data-ttu-id="04edb-2081">Если первый операнд имеет `null`, результатом операции является `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2081">If the first operand is `null`, the result of the operation is `null`.</span></span> <span data-ttu-id="04edb-2082">В противном случае, если второй операнд является `null`, то результатом операции является значение первого операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2082">Otherwise, if the second operand is `null`, then the result of the operation is the value of the first operand.</span></span> <span data-ttu-id="04edb-2083">В противном случае оба операнда представляют списки вызовов ([объявления делегатов](delegates.md#delegate-declarations)) наличие одной или несколькими записями, а результат является новый список вызовов, состоящая из первого операнда со второго операнда элементов, удаленных из предоставленный список второго операнда это правильное смежных подсписок первого элемента.</span><span class="sxs-lookup"><span data-stu-id="04edb-2083">Otherwise, both operands represent invocation lists ([Delegate declarations](delegates.md#delegate-declarations)) having one or more entries, and the result is a new invocation list consisting of the first operand's list with the second operand's entries removed from it, provided the second operand's list is a proper contiguous sublist of the first's.</span></span>     <span data-ttu-id="04edb-2084">(Для определения равенства подсписка, сравнение соответствующих записей, как и для оператора равенства делегатов ([делегировать операторы равенства](expressions.md#delegate-equality-operators)).) В противном случае результатом является значение левого операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2084">(To determine sublist equality, corresponding entries are compared as for the delegate equality operator ([Delegate equality operators](expressions.md#delegate-equality-operators)).) Otherwise, the result is the value of the left operand.</span></span> <span data-ttu-id="04edb-2085">Ни один из операндов списки изменяется в процессе.</span><span class="sxs-lookup"><span data-stu-id="04edb-2085">Neither of the operands' lists is changed in the process.</span></span> <span data-ttu-id="04edb-2086">Если список второго операнда соответствует несколько подсписка последовательных записей в списке первого операнда, крайнего правого сопоставления подсписок последовательных записей удаляется.</span><span class="sxs-lookup"><span data-stu-id="04edb-2086">If the second operand's list matches multiple sublists of contiguous entries in the first operand's list, the right-most matching sublist of contiguous entries is removed.</span></span> <span data-ttu-id="04edb-2087">Если для удаления получается пустой список, возвращается `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2087">If removal results in an empty list, the result is `null`.</span></span> <span data-ttu-id="04edb-2088">Пример:</span><span class="sxs-lookup"><span data-stu-id="04edb-2088">For example:</span></span>

   ```csharp
   delegate void D(int x);
   
   class C
   {
       public static void M1(int i) { /* ... */ }
       public static void M2(int i) { /* ... */ }
   }

   class Test
   {
       static void Main() { 
           D cd1 = new D(C.M1);
           D cd2 = new D(C.M2);
           D cd3 = cd1 + cd2 + cd2 + cd1;   // M1 + M2 + M2 + M1
           cd3 -= cd1;                      // => M1 + M2 + M2
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd1 + cd2;                // => M2 + M1
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd2 + cd2;                // => M1 + M1
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd2 + cd1;                // => M1 + M2
   
           cd3 = cd1 + cd2 + cd2 + cd1;     // M1 + M2 + M2 + M1
           cd3 -= cd1 + cd1;                // => M1 + M2 + M2 + M1
       }
   }
   ```

## <a name="shift-operators"></a><span data-ttu-id="04edb-2089">Операторы сдвига</span><span class="sxs-lookup"><span data-stu-id="04edb-2089">Shift operators</span></span>

<span data-ttu-id="04edb-2090">`<<` И `>>` операторы используются для выполнения операции сдвига разрядов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2090">The `<<` and `>>` operators are used to perform bit shifting operations.</span></span>

```antlr
shift_expression
    : additive_expression
    | shift_expression '<<' additive_expression
    | shift_expression right_shift additive_expression
    ;
```

<span data-ttu-id="04edb-2091">Если операнд *shift_expression* имеет тип времени компиляции `dynamic`, а затем он динамически связан ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2091">If an operand of a *shift_expression* has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2092">В данном случае является типов во время компиляции выражения `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, используя тип времени выполнения операндов, имеющих указанный тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2092">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="04edb-2093">Для операции в виде `x << count` или `x >> count`, разрешение перегрузки бинарного оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2093">For an operation of the form `x << count` or `x >> count`, binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-2094">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2094">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-2095">При объявлении перегруженного оператора сдвига, тип первого операнда всегда должен быть класс или структура, содержащая объявление оператора, а тип второго операнда должен всегда быть `int`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2095">When declaring an overloaded shift operator, the type of the first operand must always be the class or struct containing the operator declaration, and the type of the second operand must always be `int`.</span></span>

<span data-ttu-id="04edb-2096">Предопределенные операторы перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-2096">The predefined shift operators are listed below.</span></span>

*  <span data-ttu-id="04edb-2097">Сдвиг влево:</span><span class="sxs-lookup"><span data-stu-id="04edb-2097">Shift left:</span></span>

   ```csharp
   int operator <<(int x, int count);
   uint operator <<(uint x, int count);
   long operator <<(long x, int count);
   ulong operator <<(ulong x, int count);
   ```

   <span data-ttu-id="04edb-2098">`<<` Смены оператор `x` влево на количество битов, которое вычисляется, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-2098">The `<<` operator shifts `x` left by a number of bits computed as described below.</span></span>

   <span data-ttu-id="04edb-2099">Старшие разряды вне диапазона типа результата `x` будут удалены, а оставшиеся биты сдвигаются влево и позиции битов пустые младшие присваивается нулевое значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2099">The high-order bits outside the range of the result type of `x` are discarded, the remaining bits are shifted left, and the low-order empty bit positions are set to zero.</span></span>

*  <span data-ttu-id="04edb-2100">Сдвиг вправо:</span><span class="sxs-lookup"><span data-stu-id="04edb-2100">Shift right:</span></span>

   ```csharp
   int operator >>(int x, int count);
   uint operator >>(uint x, int count);
   long operator >>(long x, int count);
   ulong operator >>(ulong x, int count);
   ```

   <span data-ttu-id="04edb-2101">`>>` Смены оператор `x` вправо на количество битов, которое вычисляется, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-2101">The `>>` operator shifts `x` right by a number of bits computed as described below.</span></span>

   <span data-ttu-id="04edb-2102">Когда `x` имеет тип `int` или `long`, младшие биты `x` , удален, а оставшиеся биты сдвигаются вправо и позиции пустой бит высокого порядка устанавливаются в нуль, если `x` неотрицательное он имеет значение, если один `x` является отрицательным.</span><span class="sxs-lookup"><span data-stu-id="04edb-2102">When `x` is of type `int` or `long`, the low-order bits of `x` are discarded, the remaining bits are shifted right, and the high-order empty bit positions are set to zero if `x` is non-negative and set to one if `x` is negative.</span></span>

   <span data-ttu-id="04edb-2103">Когда `x` имеет тип `uint` или `ulong`, младшие биты `x` будут удалены, а оставшиеся биты сдвигаются вправо, и пустой бит высокого порядка позиций присваивается нулевое значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2103">When `x` is of type `uint` or `ulong`, the low-order bits of `x` are discarded, the remaining bits are shifted right, and the high-order empty bit positions are set to zero.</span></span>

<span data-ttu-id="04edb-2104">Для стандартных операторов количество битов для сдвига вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2104">For the predefined operators, the number of bits to shift is computed as follows:</span></span>

*  <span data-ttu-id="04edb-2105">Если тип `x` — `int` или `uint`, величина сдвига определяется пятью младшими разрядами из `count`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2105">When the type of `x` is `int` or `uint`, the shift count is given by the low-order five bits of `count`.</span></span> <span data-ttu-id="04edb-2106">Другими словами, величина сдвига вычисляется на основе `count & 0x1F`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2106">In other words, the shift count is computed from `count & 0x1F`.</span></span>
*  <span data-ttu-id="04edb-2107">Если тип `x` — `long` или `ulong`, величина сдвига определяется шестью младшими разрядами из `count`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2107">When the type of `x` is `long` or `ulong`, the shift count is given by the low-order six bits of `count`.</span></span> <span data-ttu-id="04edb-2108">Другими словами, величина сдвига вычисляется на основе `count & 0x3F`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2108">In other words, the shift count is computed from `count & 0x3F`.</span></span>

<span data-ttu-id="04edb-2109">Если счетчик принял shift равно нулю, операторы сдвига просто возвращают значение `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2109">If the resulting shift count is zero, the shift operators simply return the value of `x`.</span></span>

<span data-ttu-id="04edb-2110">Операции сдвига никогда не вызывают переполнение и дают одинаковые результаты в `checked` и `unchecked` контекстов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2110">Shift operations never cause overflows and produce the same results in `checked` and `unchecked` contexts.</span></span>

<span data-ttu-id="04edb-2111">Если левый операнд `>>` оператор имеет целочисленный тип со знаком, оператор выполняет арифметический сдвиг вправо при котором значение значащий бит (бит знака) операнда распространяется на позиции пустой бит высокого порядка.</span><span class="sxs-lookup"><span data-stu-id="04edb-2111">When the left operand of the `>>` operator is of a signed integral type, the operator performs an arithmetic shift right wherein the value of the most significant bit (the sign bit) of the operand is propagated to the high-order empty bit positions.</span></span> <span data-ttu-id="04edb-2112">Если левый операнд `>>` оператор имеет целочисленный тип без знака, оператор выполняет логическим сдвигом вправо при котором позиции пустой битов высокого порядка всегда присваивается нулевое значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2112">When the left operand of the `>>` operator is of an unsigned integral type, the operator performs a logical shift right wherein high-order empty bit positions are always set to zero.</span></span> <span data-ttu-id="04edb-2113">Для выполнения обратной операции выводится из типа операнда, можно использовать явные приведения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2113">To perform the opposite operation of that inferred from the operand type, explicit casts can be used.</span></span> <span data-ttu-id="04edb-2114">Например если `x` является переменной типа `int`, операция `unchecked((int)((uint)x >> y))` выполняет логическим сдвигом справа от `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2114">For example, if `x` is a variable of type `int`, the operation `unchecked((int)((uint)x >> y))` performs a logical shift right of `x`.</span></span>

## <a name="relational-and-type-testing-operators"></a><span data-ttu-id="04edb-2115">Операторы отношения и проверки типа</span><span class="sxs-lookup"><span data-stu-id="04edb-2115">Relational and type-testing operators</span></span>

<span data-ttu-id="04edb-2116">`==`, `!=`, `<`, `>`, `<=`, `>=`, `is` И `as` называются операторами отношения и проверки типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-2116">The `==`, `!=`, `<`, `>`, `<=`, `>=`, `is` and `as` operators are called the relational and type-testing operators.</span></span>

```antlr
relational_expression
    : shift_expression
    | relational_expression '<' shift_expression
    | relational_expression '>' shift_expression
    | relational_expression '<=' shift_expression
    | relational_expression '>=' shift_expression
    | relational_expression 'is' type
    | relational_expression 'as' type
    ;

equality_expression
    : relational_expression
    | equality_expression '==' relational_expression
    | equality_expression '!=' relational_expression
    ;
```

<span data-ttu-id="04edb-2117">`is` Разделе [является оператором](expressions.md#the-is-operator) и `as` разделе [оператор As](expressions.md#the-as-operator).</span><span class="sxs-lookup"><span data-stu-id="04edb-2117">The `is` operator is described in [The is operator](expressions.md#the-is-operator) and the `as` operator is described in [The as operator](expressions.md#the-as-operator).</span></span>

<span data-ttu-id="04edb-2118">`==`, `!=`, `<`, `>`, `<=` И `>=` операторы ***операторы сравнения***.</span><span class="sxs-lookup"><span data-stu-id="04edb-2118">The `==`, `!=`, `<`, `>`, `<=` and `>=` operators are ***comparison operators***.</span></span>

<span data-ttu-id="04edb-2119">Если операнд оператора сравнения имеет тип времени компиляции `dynamic`, а затем он динамически связан ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2119">If an operand of a comparison operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2120">В данном случае является типов во время компиляции выражения `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, используя тип времени выполнения операндов, имеющих указанный тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2120">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="04edb-2121">Для операции в виде `x` *op* `y`, где *op* является оператором сравнения, разрешение перегрузки ([Разрешитьперегрузкубинарногооператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2121">For an operation of the form `x` *op* `y`, where *op* is a comparison operator, overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-2122">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2122">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-2123">Стандартные операторы сравнения описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="04edb-2123">The predefined comparison operators are described in the following sections.</span></span> <span data-ttu-id="04edb-2124">Все стандартные операторы сравнения возвращают результат типа `bool`, как описано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="04edb-2124">All predefined comparison operators return a result of type `bool`, as described in the following table.</span></span>


| <span data-ttu-id="04edb-2125">__Операция__</span><span class="sxs-lookup"><span data-stu-id="04edb-2125">__Operation__</span></span> | <span data-ttu-id="04edb-2126">__Результат__</span><span class="sxs-lookup"><span data-stu-id="04edb-2126">__Result__</span></span>                                                       |
|---------------|------------------------------------------------------------------|
| `x == y`      | <span data-ttu-id="04edb-2127">`true` Если `x` равен `y`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="04edb-2127">`true` if `x` is equal to `y`, `false` otherwise</span></span>                 | 
| `x != y`      | <span data-ttu-id="04edb-2128">`true` Если `x` не равно `y`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="04edb-2128">`true` if `x` is not equal to `y`, `false` otherwise</span></span>             | 
| `x < y`       | <span data-ttu-id="04edb-2129">`true` Если `x` — меньше, чем `y`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="04edb-2129">`true` if `x` is less than `y`, `false` otherwise</span></span>                | 
| `x > y`       | <span data-ttu-id="04edb-2130">`true` Если `x` больше, чем `y`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="04edb-2130">`true` if `x` is greater than `y`, `false` otherwise</span></span>             | 
| `x <= y`      | <span data-ttu-id="04edb-2131">`true` Если `x` меньше или равно `y`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="04edb-2131">`true` if `x` is less than or equal to `y`, `false` otherwise</span></span>    | 
| `x >= y`      | <span data-ttu-id="04edb-2132">`true` Если `x` больше или равно `y`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="04edb-2132">`true` if `x` is greater than or equal to `y`, `false` otherwise</span></span> | 

### <a name="integer-comparison-operators"></a><span data-ttu-id="04edb-2133">Операторы сравнения целое число</span><span class="sxs-lookup"><span data-stu-id="04edb-2133">Integer comparison operators</span></span>

<span data-ttu-id="04edb-2134">Ниже перечислены операторы сравнения предопределенные целочисленные.</span><span class="sxs-lookup"><span data-stu-id="04edb-2134">The predefined integer comparison operators are:</span></span>
```csharp
bool operator ==(int x, int y);
bool operator ==(uint x, uint y);
bool operator ==(long x, long y);
bool operator ==(ulong x, ulong y);

bool operator !=(int x, int y);
bool operator !=(uint x, uint y);
bool operator !=(long x, long y);
bool operator !=(ulong x, ulong y);

bool operator <(int x, int y);
bool operator <(uint x, uint y);
bool operator <(long x, long y);
bool operator <(ulong x, ulong y);

bool operator >(int x, int y);
bool operator >(uint x, uint y);
bool operator >(long x, long y);
bool operator >(ulong x, ulong y);

bool operator <=(int x, int y);
bool operator <=(uint x, uint y);
bool operator <=(long x, long y);
bool operator <=(ulong x, ulong y);

bool operator >=(int x, int y);
bool operator >=(uint x, uint y);
bool operator >=(long x, long y);
bool operator >=(ulong x, ulong y);
```

<span data-ttu-id="04edb-2135">Каждый из этих операторов сравнивает числовые значения двух целочисленных операндов и возвращает `bool` значение, указывающее, является ли соответствующее отношение `true` или `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2135">Each of these operators compares the numeric values of the two integer operands and returns a `bool` value that indicates whether the particular relation is `true` or `false`.</span></span>

### <a name="floating-point-comparison-operators"></a><span data-ttu-id="04edb-2136">Операторы сравнения с плавающей запятой</span><span class="sxs-lookup"><span data-stu-id="04edb-2136">Floating-point comparison operators</span></span>

<span data-ttu-id="04edb-2137">Ниже перечислены операторы предопределенные сравнения с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="04edb-2137">The predefined floating-point comparison operators are:</span></span>
```csharp
bool operator ==(float x, float y);
bool operator ==(double x, double y);

bool operator !=(float x, float y);
bool operator !=(double x, double y);

bool operator <(float x, float y);
bool operator <(double x, double y);

bool operator >(float x, float y);
bool operator >(double x, double y);

bool operator <=(float x, float y);
bool operator <=(double x, double y);

bool operator >=(float x, float y);
bool operator >=(double x, double y);
```

<span data-ttu-id="04edb-2138">Операторы сравнивают операнды в соответствии с правилами стандарта IEEE 754:</span><span class="sxs-lookup"><span data-stu-id="04edb-2138">The operators compare the operands according to the rules of the IEEE 754 standard:</span></span>

*  <span data-ttu-id="04edb-2139">Если один из операндов имеет значение NaN, результатом является `false` для всех операторов, за исключением `!=`, для которого получается `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2139">If either operand is NaN, the result is `false` for all operators except `!=`, for which the result is `true`.</span></span> <span data-ttu-id="04edb-2140">Для любых двух операндов `x != y` всегда дает тот же результат, как `!(x == y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2140">For any two operands, `x != y` always produces the same result as `!(x == y)`.</span></span> <span data-ttu-id="04edb-2141">Тем не менее, в том случае, когда один или оба операнда имеют значения NaN, `<`, `>`, `<=`, и `>=` операторы не производят те же результаты, что логическое отрицание оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2141">However, when one or both operands are NaN, the `<`, `>`, `<=`, and `>=` operators do not produce the same results as the logical negation of the opposite operator.</span></span> <span data-ttu-id="04edb-2142">Например, если любой из `x` и `y` имеет значение NaN, затем `x < y` — `false`, но `!(x >= y)` является `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2142">For example, if either of `x` and `y` is NaN, then `x < y` is `false`, but `!(x >= y)` is `true`.</span></span>
*  <span data-ttu-id="04edb-2143">Если ни один из операндов имеет значение NaN, операторы сравнения значений двух операндов с плавающей запятой с точки зрения упорядочение</span><span class="sxs-lookup"><span data-stu-id="04edb-2143">When neither operand is NaN, the operators compare the values of the two floating-point operands with respect to the ordering</span></span>

   ```
   -inf < -max < ... < -min < -0.0 == +0.0 < +min < ... < +max < +inf
   ```

   <span data-ttu-id="04edb-2144">где `min` и `max` являются наименьшую и наибольшую положительными значениями, которые могут быть представлены в заданном формате с плавающей запятой.</span><span class="sxs-lookup"><span data-stu-id="04edb-2144">where `min` and `max` are the smallest and largest positive finite values that can be represented in the given floating-point format.</span></span> <span data-ttu-id="04edb-2145">Ниже приведены важные последствия этот порядок.</span><span class="sxs-lookup"><span data-stu-id="04edb-2145">Notable effects of this ordering are:</span></span>
   * <span data-ttu-id="04edb-2146">Положительные и отрицательные нули, считаются равными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2146">Negative and positive zeros are considered equal.</span></span>
   * <span data-ttu-id="04edb-2147">Отрицательная бесконечность, считается меньше, чем все остальные значения, но равным другой минус бесконечности.</span><span class="sxs-lookup"><span data-stu-id="04edb-2147">A negative infinity is considered less than all other values, but equal to another negative infinity.</span></span>
   * <span data-ttu-id="04edb-2148">Положительная бесконечность считается больше, чем все остальные значения, но равным другой положительной бесконечности.</span><span class="sxs-lookup"><span data-stu-id="04edb-2148">A positive infinity is considered greater than all other values, but equal to another positive infinity.</span></span>

### <a name="decimal-comparison-operators"></a><span data-ttu-id="04edb-2149">Операторы сравнения десятичных чисел</span><span class="sxs-lookup"><span data-stu-id="04edb-2149">Decimal comparison operators</span></span>

<span data-ttu-id="04edb-2150">Ниже перечислены операторы сравнения предопределенные десятичных чисел.</span><span class="sxs-lookup"><span data-stu-id="04edb-2150">The predefined decimal comparison operators are:</span></span>
```csharp
bool operator ==(decimal x, decimal y);
bool operator !=(decimal x, decimal y);
bool operator <(decimal x, decimal y);
bool operator >(decimal x, decimal y);
bool operator <=(decimal x, decimal y);
bool operator >=(decimal x, decimal y);
```

<span data-ttu-id="04edb-2151">Каждый из этих операторов сравнивает числовые значения двух десятичных операндов и возвращает `bool` значение, указывающее, является ли соответствующее отношение `true` или `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2151">Each of these operators compares the numeric values of the two decimal operands and returns a `bool` value that indicates whether the particular relation is `true` or `false`.</span></span> <span data-ttu-id="04edb-2152">Decimal сравнение эквивалентно значению с помощью соответствующего реляционного или оператор равенства типа `System.Decimal`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2152">Each decimal comparison is equivalent to using the corresponding relational or equality operator of type `System.Decimal`.</span></span>

### <a name="boolean-equality-operators"></a><span data-ttu-id="04edb-2153">Логические операторы равенства</span><span class="sxs-lookup"><span data-stu-id="04edb-2153">Boolean equality operators</span></span>

<span data-ttu-id="04edb-2154">Ниже приведены стандартные логические операторы равенства.</span><span class="sxs-lookup"><span data-stu-id="04edb-2154">The predefined boolean equality operators are:</span></span>
```csharp
bool operator ==(bool x, bool y);
bool operator !=(bool x, bool y);
```

<span data-ttu-id="04edb-2155">Результат `==` — `true` Если оба `x` и `y` являются `true` или если оба `x` и `y` являются `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2155">The result of `==` is `true` if both `x` and `y` are `true` or if both `x` and `y` are `false`.</span></span> <span data-ttu-id="04edb-2156">В противном случае результат будет `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2156">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="04edb-2157">Результат `!=` — `false` Если оба `x` и `y` являются `true` или если оба `x` и `y` являются `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2157">The result of `!=` is `false` if both `x` and `y` are `true` or if both `x` and `y` are `false`.</span></span> <span data-ttu-id="04edb-2158">В противном случае результат будет `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2158">Otherwise, the result is `true`.</span></span> <span data-ttu-id="04edb-2159">Если операнды имеют тип `bool`, `!=` оператор дает тот же результат, как `^` оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-2159">When the operands are of type `bool`, the `!=` operator produces the same result as the `^` operator.</span></span>

### <a name="enumeration-comparison-operators"></a><span data-ttu-id="04edb-2160">Операторы сравнения перечисления</span><span class="sxs-lookup"><span data-stu-id="04edb-2160">Enumeration comparison operators</span></span>

<span data-ttu-id="04edb-2161">Каждый тип перечисления неявно предоставляет следующие стандартные операторы сравнения:</span><span class="sxs-lookup"><span data-stu-id="04edb-2161">Every enumeration type implicitly provides the following predefined comparison operators:</span></span>
```csharp
bool operator ==(E x, E y);
bool operator !=(E x, E y);
bool operator <(E x, E y);
bool operator >(E x, E y);
bool operator <=(E x, E y);
bool operator >=(E x, E y);
```

<span data-ttu-id="04edb-2162">Результат вычисления `x op y`, где `x` и `y` являются выражениями типа перечисления `E` с базовым типом `U`, и `op` является один из операторов сравнения, точно так же, как Оценка `((U)x) op ((U)y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2162">The result of evaluating `x op y`, where `x` and `y` are expressions of an enumeration type `E` with an underlying type `U`, and `op` is one of the comparison operators, is exactly the same as evaluating `((U)x) op ((U)y)`.</span></span> <span data-ttu-id="04edb-2163">Другими словами операторы сравнения для типа перечисления просто сравнивать базовые целые значения двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2163">In other words, the enumeration type comparison operators simply compare the underlying integral values of the two operands.</span></span>

### <a name="reference-type-equality-operators"></a><span data-ttu-id="04edb-2164">Операторы равенства ссылочного типа</span><span class="sxs-lookup"><span data-stu-id="04edb-2164">Reference type equality operators</span></span>

<span data-ttu-id="04edb-2165">Приведены стандартные операторы ссылочного типа проверки на равенство.</span><span class="sxs-lookup"><span data-stu-id="04edb-2165">The predefined reference type equality operators are:</span></span>
```csharp
bool operator ==(object x, object y);
bool operator !=(object x, object y);
```

<span data-ttu-id="04edb-2166">Операторы возвращают результат сравнения двух ссылок на идентичность.</span><span class="sxs-lookup"><span data-stu-id="04edb-2166">The operators return the result of comparing the two references for equality or non-equality.</span></span>

<span data-ttu-id="04edb-2167">Так как стандартные операторы ссылочного типа равенства принимает операнды типа `object`, они применяются ко всем типам, не объявляйте применимо `operator ==` и `operator !=` членов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2167">Since the predefined reference type equality operators accept operands of type `object`, they apply to all types that do not declare applicable `operator ==` and `operator !=` members.</span></span> <span data-ttu-id="04edb-2168">И наоборот любые применимые равенства, определяемые пользователем операторы скрывают стандартные операторы ссылочного типа проверки на равенство.</span><span class="sxs-lookup"><span data-stu-id="04edb-2168">Conversely, any applicable user-defined equality operators effectively hide the predefined reference type equality operators.</span></span>

<span data-ttu-id="04edb-2169">Стандартные операторы ссылочного типа равенства требуется одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-2169">The predefined reference type equality operators require one of the following:</span></span>

*  <span data-ttu-id="04edb-2170">Оба операнда имеют значение типа, известные как *reference_type* или литерала `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2170">Both operands are a value of a type known to be a *reference_type* or the literal `null`.</span></span> <span data-ttu-id="04edb-2171">Кроме того неявное преобразование ([явные преобразования ссылочных типов](conversions.md#explicit-reference-conversions)) существует тип один из операндов на тип значение второго операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2171">Furthermore, an explicit reference conversion ([Explicit reference conversions](conversions.md#explicit-reference-conversions)) exists from the type of either operand to the type of the other operand.</span></span>
*  <span data-ttu-id="04edb-2172">Один операнд является значение типа `T` где `T` — *параметр_типа* и другой операнд является литералом `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2172">One operand is a value of type `T` where `T` is a *type_parameter* and the other operand is the literal `null`.</span></span> <span data-ttu-id="04edb-2173">Кроме того `T` имеет ограничение типа значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2173">Furthermore `T` does not have the value type constraint.</span></span>

<span data-ttu-id="04edb-2174">Если одно из этих условий не true, происходит ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2174">Unless one of these conditions are true, a binding-time error occurs.</span></span> <span data-ttu-id="04edb-2175">Ниже приведены важные последствия этих правил.</span><span class="sxs-lookup"><span data-stu-id="04edb-2175">Notable implications of these rules are:</span></span>

*  <span data-ttu-id="04edb-2176">Является ошибкой времени привязки для использования стандартных операторов ссылочного типа равенства для сравнения двух ссылок, которые заведомо отличаться во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2176">It is a binding-time error to use the predefined reference type equality operators to compare two references that are known to be different at binding-time.</span></span> <span data-ttu-id="04edb-2177">Например, если во время привязки типы операндов два типа класса `A` и `B`и если ни один из `A` , ни `B` является производным от другого, то он может быть организовано два операнда для ссылки на тот же объект.</span><span class="sxs-lookup"><span data-stu-id="04edb-2177">For example, if the binding-time types of the operands are two class types `A` and `B`, and if neither `A` nor `B` derives from the other, then it would be impossible for the two operands to reference the same object.</span></span> <span data-ttu-id="04edb-2178">Таким образом операция вызовет ошибку во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2178">Thus, the operation is considered a binding-time error.</span></span>
*  <span data-ttu-id="04edb-2179">Операторы равенства предопределенные ссылочного типа не допускают значение операнды типа для сравнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2179">The predefined reference type equality operators do not permit value type operands to be compared.</span></span> <span data-ttu-id="04edb-2180">Таким образом Если тип структуры объявляет свои собственные операторы равенства, он не поддерживается для сравнения значений этого типа структуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-2180">Therefore, unless a struct type declares its own equality operators, it is not possible to compare values of that struct type.</span></span>
*  <span data-ttu-id="04edb-2181">Операторы равенства предопределенные ссылочного типа никогда не вызывают операции упаковки-преобразования, чтобы для своих операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2181">The predefined reference type equality operators never cause boxing operations to occur for their operands.</span></span> <span data-ttu-id="04edb-2182">Было бы смысла для выполнения такой операции упаковки-преобразования, так как ссылки на создаваемые упакованные экземпляры обязательно будут отличаться от всех остальных ссылок.</span><span class="sxs-lookup"><span data-stu-id="04edb-2182">It would be meaningless to perform such boxing operations, since references to the newly allocated boxed instances would necessarily differ from all other references.</span></span>
*  <span data-ttu-id="04edb-2183">Если операнд с типом параметра типа `T` сравнивается с `null`и тип времени выполнения `T` является типом значения, результатом сравнения является `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2183">If an operand of a type parameter type `T` is compared to `null`, and the run-time type of `T` is a value type, the result of the comparison is `false`.</span></span>

<span data-ttu-id="04edb-2184">В следующем примере проверяется, является ли аргумент параметра неограниченного типа `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2184">The following example checks whether an argument of an unconstrained type parameter type is `null`.</span></span>
```csharp
class C<T>
{
    void F(T x) {
        if (x == null) throw new ArgumentNullException();
        ...
    }
}
```

<span data-ttu-id="04edb-2185">`x == null` Конструкция разрешено, даже если `T` может представлять тип значения, и результат просто определяется как `false` при `T` является типом значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2185">The `x == null` construct is permitted even though `T` could represent a value type, and the result is simply defined to be `false` when `T` is a value type.</span></span>

<span data-ttu-id="04edb-2186">Для операции в виде `x == y` или `x != y`, если всем применимым `operator ==` или `operator !=` существует, разрешение перегрузки оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)), выберет правила оператор, а не стандартный оператор ссылочного типа проверки на равенство.</span><span class="sxs-lookup"><span data-stu-id="04edb-2186">For an operation of the form `x == y` or `x != y`, if any applicable `operator ==` or `operator !=` exists, the operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) rules will select that operator instead of the predefined reference type equality operator.</span></span> <span data-ttu-id="04edb-2187">Тем не менее, это всегда можно выбрать оператор равенства Предопределенная ссылка типа явным образом привести один или оба операнда к типу `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2187">However, it is always possible to select the predefined reference type equality operator by explicitly casting one or both of the operands to type `object`.</span></span> <span data-ttu-id="04edb-2188">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2188">The example</span></span>
```csharp
using System;

class Test
{
    static void Main() {
        string s = "Test";
        string t = string.Copy(s);
        Console.WriteLine(s == t);
        Console.WriteLine((object)s == t);
        Console.WriteLine(s == (object)t);
        Console.WriteLine((object)s == (object)t);
    }
}
```
<span data-ttu-id="04edb-2189">выводятся следующие выходные данные</span><span class="sxs-lookup"><span data-stu-id="04edb-2189">produces the output</span></span>
```
True
False
False
False
```

<span data-ttu-id="04edb-2190">`s` И `t` переменные ссылаются на два отдельных `string` экземпляров, содержащую те же символы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2190">The `s` and `t` variables refer to two distinct `string` instances containing the same characters.</span></span> <span data-ttu-id="04edb-2191">Выводит первое сравнение `True` так как оператор равенства заранее определенной строки ([строковые операторы равенства](expressions.md#string-equality-operators)) выбран, если оба операнда имеют тип `string`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2191">The first comparison outputs `True` because the predefined string equality operator ([String equality operators](expressions.md#string-equality-operators)) is selected when both operands are of type `string`.</span></span> <span data-ttu-id="04edb-2192">Все оставшиеся сравнения вывода `False` так как стандартный оператор ссылочного типа равенства выбрана в том случае, если один или оба операнда имеют тип `object`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2192">The remaining comparisons all output `False` because the predefined reference type equality operator is selected when one or both of the operands are of type `object`.</span></span>

<span data-ttu-id="04edb-2193">Обратите внимание на то, что указанная процедура не имеет смысла для типов значений.</span><span class="sxs-lookup"><span data-stu-id="04edb-2193">Note that the above technique is not meaningful for value types.</span></span> <span data-ttu-id="04edb-2194">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2194">The example</span></span>
```csharp
class Test
{
    static void Main() {
        int i = 123;
        int j = 123;
        System.Console.WriteLine((object)i == (object)j);
    }
}
```
<span data-ttu-id="04edb-2195">Выводит `False` из-за приведения создание ссылок на два отдельных экземпляра упакованных `int` значения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2195">outputs `False` because the casts create references to two separate instances of boxed `int` values.</span></span>

### <a name="string-equality-operators"></a><span data-ttu-id="04edb-2196">Операторы равенства строк</span><span class="sxs-lookup"><span data-stu-id="04edb-2196">String equality operators</span></span>

<span data-ttu-id="04edb-2197">Ниже перечислены операторы равенства заранее определенной строки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2197">The predefined string equality operators are:</span></span>
```csharp
bool operator ==(string x, string y);
bool operator !=(string x, string y);
```

<span data-ttu-id="04edb-2198">Два `string` значения считаются равными, если выполняется одно из следующих:</span><span class="sxs-lookup"><span data-stu-id="04edb-2198">Two `string` values are considered equal when one of the following is true:</span></span>

*  <span data-ttu-id="04edb-2199">Оба значения равны `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2199">Both values are `null`.</span></span>
*  <span data-ttu-id="04edb-2200">Оба значения являются ненулевой ссылками на экземпляры строк с одинаковой длиной и идентичные символы в каждой позиции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2200">Both values are non-null references to string instances that have identical lengths and identical characters in each character position.</span></span>

<span data-ttu-id="04edb-2201">Операторы равенства строк сравнения строковых значений, а не ссылки на строки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2201">The string equality operators compare string values rather than string references.</span></span> <span data-ttu-id="04edb-2202">Если два разных экземпляра строк содержат та же последовательность символов, значения строк равны, но ссылки отличаются.</span><span class="sxs-lookup"><span data-stu-id="04edb-2202">When two separate string instances contain the exact same sequence of characters, the values of the strings are equal, but the references are different.</span></span> <span data-ttu-id="04edb-2203">Как описано в разделе [операторы равенства ссылочного типа](expressions.md#reference-type-equality-operators), операторы равенства ссылочного типа можно использовать для сравнения ссылки на строки вместо строковых значений.</span><span class="sxs-lookup"><span data-stu-id="04edb-2203">As described in [Reference type equality operators](expressions.md#reference-type-equality-operators), the reference type equality operators can be used to compare string references instead of string values.</span></span>

### <a name="delegate-equality-operators"></a><span data-ttu-id="04edb-2204">Операторы равенства делегатов</span><span class="sxs-lookup"><span data-stu-id="04edb-2204">Delegate equality operators</span></span>

<span data-ttu-id="04edb-2205">Каждый тип делегата неявно предоставляет следующие стандартные операторы сравнения:</span><span class="sxs-lookup"><span data-stu-id="04edb-2205">Every delegate type implicitly provides the following predefined comparison operators:</span></span>

```csharp
bool operator ==(System.Delegate x, System.Delegate y);
bool operator !=(System.Delegate x, System.Delegate y);
```

<span data-ttu-id="04edb-2206">Два делегата считаются равными следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2206">Two delegate instances are considered equal as follows:</span></span>

*  <span data-ttu-id="04edb-2207">Если экземпляры делегата являются `null`, они равны, только в том случае, если выполняются оба `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2207">If either of the delegate instances is `null`, they are equal if and only if both are `null`.</span></span>
*  <span data-ttu-id="04edb-2208">Если делегаты имеют другой тип времени выполнения, они никогда не равны.</span><span class="sxs-lookup"><span data-stu-id="04edb-2208">If the delegates have different run-time type they are never equal.</span></span>
*  <span data-ttu-id="04edb-2209">Если у обоих экземпляров делегата есть список вызова ([объявления делегатов](delegates.md#delegate-declarations)), то они равны только в том случае, если их списки вызовов имеют одинаковую длину и каждая запись в список вызова равно (как определено ниже) для соответствующей записи в порядке, в списке вызова другого.</span><span class="sxs-lookup"><span data-stu-id="04edb-2209">If both of the delegate instances have an invocation list ([Delegate declarations](delegates.md#delegate-declarations)), those instances are equal if and only if their invocation lists are the same length, and each entry in one's invocation list is equal (as defined below) to the corresponding entry, in order, in the other's invocation list.</span></span>

<span data-ttu-id="04edb-2210">Следующие правила определяют равенство записей списка вызова:</span><span class="sxs-lookup"><span data-stu-id="04edb-2210">The following rules govern the equality of invocation list entries:</span></span>

*  <span data-ttu-id="04edb-2211">Если две записи списка вызова ссылается на тот же статический метод, а затем записи считаются равными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2211">If two invocation list entries both refer to the same static method then the entries are equal.</span></span>
*  <span data-ttu-id="04edb-2212">Если две записи списка вызова ссылаются на один и тот же метод статическим на тот же целевой объект (в соответствии с операторов равенства ссылок) записи считаются равными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2212">If two invocation list entries both refer to the same non-static method on the same target object (as defined by the reference equality operators) then the entries are equal.</span></span>
*  <span data-ttu-id="04edb-2213">Полученные записи списка вызова при вычислении семантически идентичных *anonymous_method_expression*s или *lambda_expression*s с тем же набором (возможно, пустой), записанный внешней переменной. экземпляры разрешены (но не требуются) должны совпадать.</span><span class="sxs-lookup"><span data-stu-id="04edb-2213">Invocation list entries produced from evaluation of semantically identical *anonymous_method_expression*s or *lambda_expression*s with the same (possibly empty) set of captured outer variable instances are permitted (but not required) to be equal.</span></span>

### <a name="equality-operators-and-null"></a><span data-ttu-id="04edb-2214">Операторы равенства и значение null</span><span class="sxs-lookup"><span data-stu-id="04edb-2214">Equality operators and null</span></span>

<span data-ttu-id="04edb-2215">`==` И `!=` операторы позволяют один операнд должен быть значение типа, допускающего значение NULL, а другой быть `null` литерал, даже если существует предопределенные или определяемые пользователем оператор не (обычного или с ликвидированный формы) для операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2215">The `==` and `!=` operators permit one operand to be a value of a nullable type and the other to be the `null` literal, even if no predefined or user-defined operator (in unlifted or lifted form) exists for the operation.</span></span>

<span data-ttu-id="04edb-2216">Для операции в одной из форм</span><span class="sxs-lookup"><span data-stu-id="04edb-2216">For an operation of one of the forms</span></span>
```csharp
x == null
null == x
x != null
null != x
```
<span data-ttu-id="04edb-2217">где `x` — это выражение типа, допускающего значение NULL, если разрешение перегрузки оператора ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) не удалось найти соответствующий оператор, результат вместо этого вычисляется на основе `HasValue` Свойство `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2217">where `x` is an expression of a nullable type, if operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) fails to find an applicable operator, the result is instead computed from the `HasValue` property of `x`.</span></span> <span data-ttu-id="04edb-2218">В частности, первые две формы преобразуются в `!x.HasValue`, и два последних преобразуются в `x.HasValue`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2218">Specifically, the first two forms are translated into `!x.HasValue`, and last two forms are translated into `x.HasValue`.</span></span>

### <a name="the-is-operator"></a><span data-ttu-id="04edb-2219">Является оператором</span><span class="sxs-lookup"><span data-stu-id="04edb-2219">The is operator</span></span>

<span data-ttu-id="04edb-2220">`is` Оператор используется для динамической проверки, совместим ли тип времени выполнения объекта с заданным типом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2220">The `is` operator is used to dynamically check if the run-time type of an object is compatible with a given type.</span></span> <span data-ttu-id="04edb-2221">Результат операции `E is T`, где `E` — это выражение и `T` — это тип, возвращается логическое значение, указывающее, ли `E` можно успешно преобразовать в тип `T` с помощью преобразования ссылок, упаковки-преобразования преобразования или распаковки-преобразования.</span><span class="sxs-lookup"><span data-stu-id="04edb-2221">The result of the operation `E is T`, where `E` is an expression and `T` is a type, is a boolean value indicating whether `E` can successfully be converted to type `T` by a reference conversion, a boxing conversion, or an unboxing conversion.</span></span> <span data-ttu-id="04edb-2222">После замены аргументов типа для всех параметров типа, операция вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2222">The operation is evaluated as follows, after type arguments have been substituted for all type parameters:</span></span>

*  <span data-ttu-id="04edb-2223">Если `E` является анонимной функцией, возникает ошибка времени компиляции</span><span class="sxs-lookup"><span data-stu-id="04edb-2223">If `E` is an anonymous function, a compile-time error occurs</span></span>
*  <span data-ttu-id="04edb-2224">Если `E` является группой методов или `null` литерал, если тип `E` — это ссылочный тип или тип, допускающий значение NULL и значение `E` имеет значение null, результат имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="04edb-2224">If `E` is a method group or the `null` literal, of if the type of `E` is a reference type or a nullable type and the value of `E` is null, the result is false.</span></span>
*  <span data-ttu-id="04edb-2225">В противном случае позволить `D` представляют динамический тип `E` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2225">Otherwise, let `D` represent the dynamic type of `E` as follows:</span></span>
   * <span data-ttu-id="04edb-2226">Если тип `E` является ссылочным типом, `D` является типом времени выполнения ссылка на экземпляр, `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2226">If the type of `E` is a reference type, `D` is the run-time type of the instance reference by `E`.</span></span>
   * <span data-ttu-id="04edb-2227">Если тип `E` является тип nullable `D` — базовый тип этого типа, допускающего значение NULL.</span><span class="sxs-lookup"><span data-stu-id="04edb-2227">If the type of `E` is a nullable type, `D` is the underlying type of that nullable type.</span></span>
   * <span data-ttu-id="04edb-2228">Если тип `E` является типом значения, не допускающие значения NULL, `D` — это тип `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2228">If the type of `E` is a non-nullable value type, `D` is the type of `E`.</span></span>
*  <span data-ttu-id="04edb-2229">Результат операции зависит от `D` и `T` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2229">The result of the operation depends on `D` and `T` as follows:</span></span>
   * <span data-ttu-id="04edb-2230">Если `T` является ссылочным типом, результат равен true, если `D` и `T` относятся к одному типу, в том случае, если `D` является ссылочным типом и и неявное ссылочное преобразование из `D` для `T` существует, или если `D` является типом значения и преобразования-упаковки из `D` для `T` существует.</span><span class="sxs-lookup"><span data-stu-id="04edb-2230">If `T` is a reference type, the result is true if `D` and `T` are the same type, if `D` is a reference type and an implicit reference conversion from `D` to `T` exists, or if `D` is a value type and a boxing conversion from `D` to `T` exists.</span></span>
   * <span data-ttu-id="04edb-2231">Если `T` является типом, допускающий значение NULL, результат равен true, если `D` является базовым типом объекта `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2231">If `T` is a nullable type, the result is true if `D` is the underlying type of `T`.</span></span>
   * <span data-ttu-id="04edb-2232">Если `T` является типом значения, не допускающие значения NULL, результат равен true, если `D` и `T` относятся к одному типу.</span><span class="sxs-lookup"><span data-stu-id="04edb-2232">If `T` is a non-nullable value type, the result is true if `D` and `T` are the same type.</span></span>
   * <span data-ttu-id="04edb-2233">В противном случае результат имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="04edb-2233">Otherwise, the result is false.</span></span>

<span data-ttu-id="04edb-2234">Обратите внимание, что пользовательские преобразования не рассматривает `is` оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-2234">Note that user defined conversions, are not considered by the `is` operator.</span></span>

### <a name="the-as-operator"></a><span data-ttu-id="04edb-2235">Оператор as</span><span class="sxs-lookup"><span data-stu-id="04edb-2235">The as operator</span></span>

<span data-ttu-id="04edb-2236">`as` Оператор используется для явного преобразования значения в указанный ссылочный тип или тип, допускающий значение NULL.</span><span class="sxs-lookup"><span data-stu-id="04edb-2236">The `as` operator is used to explicitly convert a value to a given reference type or nullable type.</span></span> <span data-ttu-id="04edb-2237">В отличие от выражения приведения ([выражения приведения](expressions.md#cast-expressions)), `as` оператор никогда не создает исключение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2237">Unlike a cast expression ([Cast expressions](expressions.md#cast-expressions)), the `as` operator never throws an exception.</span></span> <span data-ttu-id="04edb-2238">Вместо этого, если указанное преобразование невозможно, то результирующее значение равно `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2238">Instead, if the indicated conversion is not possible, the resulting value is `null`.</span></span>

<span data-ttu-id="04edb-2239">В операции формы `E as T`, `E` должно быть выражением и `T` должен быть ссылочного типа, параметром типа, быть ссылочным типом или типом, допускающий значение NULL.</span><span class="sxs-lookup"><span data-stu-id="04edb-2239">In an operation of the form `E as T`, `E` must be an expression and `T` must be a reference type, a type parameter known to be a reference type, or a nullable type.</span></span> <span data-ttu-id="04edb-2240">Кроме того по крайней мере одно из следующих должен иметь значение true, или иначе возникает ошибка времени компиляции:</span><span class="sxs-lookup"><span data-stu-id="04edb-2240">Furthermore, at least one of the following must be true, or otherwise a compile-time error occurs:</span></span>

*  <span data-ttu-id="04edb-2241">Удостоверение ([преобразование идентификации](conversions.md#identity-conversion)), неявное допускает значения NULL ([неявные преобразования обнуляемых типов](conversions.md#implicit-nullable-conversions)), неявные ссылки ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)), упаковка-преобразование ([ Осуществлять преобразования-упаковки](conversions.md#boxing-conversions)) явный допускает значения NULL ([явные преобразования обнуляемых типов](conversions.md#explicit-nullable-conversions)), явная ссылка ([преобразования явной ссылки](conversions.md#explicit-reference-conversions)), или распаковка-преобразование ([Преобразования, распаковки-преобразования](conversions.md#unboxing-conversions)) существует преобразование из `E` для `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2241">An identity ([Identity conversion](conversions.md#identity-conversion)), implicit nullable ([Implicit nullable conversions](conversions.md#implicit-nullable-conversions)), implicit reference ([Implicit reference conversions](conversions.md#implicit-reference-conversions)), boxing ([Boxing conversions](conversions.md#boxing-conversions)), explicit nullable ([Explicit nullable conversions](conversions.md#explicit-nullable-conversions)), explicit reference ([Explicit reference conversions](conversions.md#explicit-reference-conversions)), or unboxing ([Unboxing conversions](conversions.md#unboxing-conversions)) conversion exists from `E` to `T`.</span></span>
*  <span data-ttu-id="04edb-2242">Тип `E` или `T` является открытым типом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2242">The type of `E` or `T` is an open type.</span></span>
*  <span data-ttu-id="04edb-2243">`E` является `null` литерала.</span><span class="sxs-lookup"><span data-stu-id="04edb-2243">`E` is the `null` literal.</span></span>

<span data-ttu-id="04edb-2244">Если тип времени компиляции `E` не `dynamic`, операция `E as T` дает тот же результат, как</span><span class="sxs-lookup"><span data-stu-id="04edb-2244">If the compile-time type of `E` is not `dynamic`, the operation `E as T` produces the same result as</span></span>
```csharp
E is T ? (T)(E) : (T)null
```
<span data-ttu-id="04edb-2245">за исключением того, что `E` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-2245">except that `E` is only evaluated once.</span></span> <span data-ttu-id="04edb-2246">Компилятор может проводить оптимизацию `E as T` для проверки не более одного динамического типа в отличие от двух динамических проверок типа в расширении выше.</span><span class="sxs-lookup"><span data-stu-id="04edb-2246">The compiler can be expected to optimize `E as T` to perform at most one dynamic type check as opposed to the two dynamic type checks implied by the expansion above.</span></span>

<span data-ttu-id="04edb-2247">Если тип времени компиляции `E` — `dynamic`, в отличие от оператора приведения `as` оператор не имеет динамической привязки ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2247">If the compile-time type of `E` is `dynamic`, unlike the cast operator the `as` operator is not dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2248">Поэтому расширение в данном случае является:</span><span class="sxs-lookup"><span data-stu-id="04edb-2248">Therefore the expansion in this case is:</span></span>
```csharp
E is T ? (T)(object)(E) : (T)null
```

<span data-ttu-id="04edb-2249">Обратите внимание, что некоторые преобразования, например определенные пользователем, не поддерживаемых в средстве `as` оператор и следует выполнять с помощью выражения приведения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2249">Note that some conversions, such as user defined conversions, are not possible with the `as` operator and should instead be performed using cast expressions.</span></span>

<span data-ttu-id="04edb-2250">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2250">In the example</span></span>
```csharp
class X
{

    public string F(object o) {
        return o as string;        // OK, string is a reference type
    }

    public T G<T>(object o) where T: Attribute {
        return o as T;             // Ok, T has a class constraint
    }

    public U H<U>(object o) {
        return o as U;             // Error, U is unconstrained 
    }
}
```
<span data-ttu-id="04edb-2251">параметр типа `T` из `G` известно, быть ссылочным типом, так как он имеет ограничения класса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2251">the type parameter `T` of `G` is known to be a reference type, because it has the class constraint.</span></span> <span data-ttu-id="04edb-2252">Параметр типа `U` из `H` не является тем не менее, поэтому использование `as` оператор в `H` запрещено.</span><span class="sxs-lookup"><span data-stu-id="04edb-2252">The type parameter `U` of `H` is not however; hence the use of the `as` operator in `H` is disallowed.</span></span>

## <a name="logical-operators"></a><span data-ttu-id="04edb-2253">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2253">Logical operators</span></span>

<span data-ttu-id="04edb-2254">`&`, `^`, И `|` называются логическими операторами.</span><span class="sxs-lookup"><span data-stu-id="04edb-2254">The `&`, `^`, and `|` operators are called the logical operators.</span></span>

```antlr
and_expression
    : equality_expression
    | and_expression '&' equality_expression
    ;

exclusive_or_expression
    : and_expression
    | exclusive_or_expression '^' and_expression
    ;

inclusive_or_expression
    : exclusive_or_expression
    | inclusive_or_expression '|' exclusive_or_expression
    ;
```

<span data-ttu-id="04edb-2255">Если операнд логического оператора имеет тип времени компиляции `dynamic`, а затем он динамически связан ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2255">If an operand of a logical operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2256">В данном случае является типов во время компиляции выражения `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, используя тип времени выполнения операндов, имеющих указанный тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2256">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="04edb-2257">Для операции в виде `x op y`, где `op` является одним из логических операторов, разрешение перегрузки ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) применяется, чтобы выбрать конкретную реализацию оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2257">For an operation of the form `x op y`, where `op` is one of the logical operators, overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) is applied to select a specific operator implementation.</span></span> <span data-ttu-id="04edb-2258">Операнды преобразуются в типы параметров выбранного оператора и типом результата является тип возвращаемого значения оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2258">The operands are converted to the parameter types of the selected operator, and the type of the result is the return type of the operator.</span></span>

<span data-ttu-id="04edb-2259">Стандартные логические операторы описаны в следующих разделах.</span><span class="sxs-lookup"><span data-stu-id="04edb-2259">The predefined logical operators are described in the following sections.</span></span>

### <a name="integer-logical-operators"></a><span data-ttu-id="04edb-2260">Логические операторы целое число</span><span class="sxs-lookup"><span data-stu-id="04edb-2260">Integer logical operators</span></span>

<span data-ttu-id="04edb-2261">Предопределенные целочисленные перечислены логические операторы:</span><span class="sxs-lookup"><span data-stu-id="04edb-2261">The predefined integer logical operators are:</span></span>
```csharp
int operator &(int x, int y);
uint operator &(uint x, uint y);
long operator &(long x, long y);
ulong operator &(ulong x, ulong y);

int operator |(int x, int y);
uint operator |(uint x, uint y);
long operator |(long x, long y);
ulong operator |(ulong x, ulong y);

int operator ^(int x, int y);
uint operator ^(uint x, uint y);
long operator ^(long x, long y);
ulong operator ^(ulong x, ulong y);
```

<span data-ttu-id="04edb-2262">`&` Оператор выполняет побитовую операцию логического `AND` двух операндов, `|` оператор выполняет побитовую операцию логического `OR` двух операндов и `^` оператор вычисляет побитового логического исключающего `OR` двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2262">The `&` operator computes the bitwise logical `AND` of the two operands, the `|` operator computes the bitwise logical `OR` of the two operands, and the `^` operator computes the bitwise logical exclusive `OR` of the two operands.</span></span> <span data-ttu-id="04edb-2263">Не порождают переполнения из этих операций.</span><span class="sxs-lookup"><span data-stu-id="04edb-2263">No overflows are possible from these operations.</span></span>

### <a name="enumeration-logical-operators"></a><span data-ttu-id="04edb-2264">Перечисление логических операторов</span><span class="sxs-lookup"><span data-stu-id="04edb-2264">Enumeration logical operators</span></span>

<span data-ttu-id="04edb-2265">Каждый тип перечисления `E` неявно предоставляет следующие предварительно определенные логические операторы:</span><span class="sxs-lookup"><span data-stu-id="04edb-2265">Every enumeration type `E` implicitly provides the following predefined logical operators:</span></span>

```csharp
E operator &(E x, E y);
E operator |(E x, E y);
E operator ^(E x, E y);
```

<span data-ttu-id="04edb-2266">Результат вычисления `x op y`, где `x` и `y` являются выражениями типа перечисления `E` с базовым типом `U`, и `op` является одним из логических операторов, именно так же, как Оценка `(E)((U)x op (U)y)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2266">The result of evaluating `x op y`, where `x` and `y` are expressions of an enumeration type `E` with an underlying type `U`, and `op` is one of the logical operators, is exactly the same as evaluating `(E)((U)x op (U)y)`.</span></span> <span data-ttu-id="04edb-2267">Другими словами логические операторы типа перечисления просто выполняют логические операции в базовом типе двух операндов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2267">In other words, the enumeration type logical operators simply perform the logical operation on the underlying type of the two operands.</span></span>

### <a name="boolean-logical-operators"></a><span data-ttu-id="04edb-2268">Логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2268">Boolean logical operators</span></span>

<span data-ttu-id="04edb-2269">Ниже приведены стандартные логические операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2269">The predefined boolean logical operators are:</span></span>
```csharp
bool operator &(bool x, bool y);
bool operator |(bool x, bool y);
bool operator ^(bool x, bool y);
```

<span data-ttu-id="04edb-2270">Результат операции `x & y` принимает значение `true`, если оба оператора `x` и `y` имеют значение `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2270">The result of `x & y` is `true` if both `x` and `y` are `true`.</span></span> <span data-ttu-id="04edb-2271">В противном случае результат будет `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2271">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="04edb-2272">Результат `x | y` — `true` Если `x` или `y` является `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2272">The result of `x | y` is `true` if either `x` or `y` is `true`.</span></span> <span data-ttu-id="04edb-2273">В противном случае результат будет `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2273">Otherwise, the result is `false`.</span></span>

<span data-ttu-id="04edb-2274">Результат `x ^ y` — `true` Если `x` — `true` и `y` — `false`, или `x` — `false` и `y` является `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2274">The result of `x ^ y` is `true` if `x` is `true` and `y` is `false`, or `x` is `false` and `y` is `true`.</span></span> <span data-ttu-id="04edb-2275">В противном случае результат будет `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2275">Otherwise, the result is `false`.</span></span> <span data-ttu-id="04edb-2276">Если операнды имеют тип `bool`, `^` оператор вычисляет тот же результат, как `!=` оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-2276">When the operands are of type `bool`, the `^` operator computes the same result as the `!=` operator.</span></span>

### <a name="nullable-boolean-logical-operators"></a><span data-ttu-id="04edb-2277">Обнуляемые логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2277">Nullable boolean logical operators</span></span>

<span data-ttu-id="04edb-2278">Допускающий значение NULL тип данных boolean `bool?` может представлять три значения `true`, `false`, и `null`и принципиально подобен классу для трех значений типа, используемого для логических выражений в SQL.</span><span class="sxs-lookup"><span data-stu-id="04edb-2278">The nullable boolean type `bool?` can represent three values, `true`, `false`, and `null`, and is conceptually similar to the three-valued type used for boolean expressions in SQL.</span></span> <span data-ttu-id="04edb-2279">Чтобы убедиться, что результаты `&` и `|` операторов для `bool?` операндов, соответствуют SQL троичную логику, предоставляются следующие предопределенные операторы:</span><span class="sxs-lookup"><span data-stu-id="04edb-2279">To ensure that the results produced by the `&` and `|` operators for `bool?` operands are consistent with SQL's three-valued logic, the following predefined operators are provided:</span></span>

```csharp
bool? operator &(bool? x, bool? y);
bool? operator |(bool? x, bool? y);
```

<span data-ttu-id="04edb-2280">В следующей таблице перечислены результаты этих операторов для всех сочетаний значений `true`, `false`, и `null`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2280">The following table lists the results produced by these operators for all combinations of the values `true`, `false`, and `null`.</span></span>

| `x`     | `y`     | `x & y` | <code>x &#124; y</code> |
|:-------:|:-------:|:-------:|:-------:|
| `true`  | `true`  | `true`  | `true`  | 
| `true`  | `false` | `false` | `true`  | 
| `true`  | `null`  | `null`  | `true`  | 
| `false` | `true`  | `false` | `true`  | 
| `false` | `false` | `false` | `false` | 
| `false` | `null`  | `false` | `null`  | 
| `null`  | `true`  | `null`  | `true`  | 
| `null`  | `false` | `false` | `null`  | 
| `null`  | `null`  | `null`  | `null`  | 

## <a name="conditional-logical-operators"></a><span data-ttu-id="04edb-2281">Условные логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2281">Conditional logical operators</span></span>

<span data-ttu-id="04edb-2282">`&&` И `||` называются условные логические операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2282">The `&&` and `||` operators are called the conditional logical operators.</span></span> <span data-ttu-id="04edb-2283">Они также называются «Упрощенные» логические операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2283">They are also called the "short-circuiting" logical operators.</span></span>

```antlr
conditional_and_expression
    : inclusive_or_expression
    | conditional_and_expression '&&' inclusive_or_expression
    ;

conditional_or_expression
    : conditional_and_expression
    | conditional_or_expression '||' conditional_and_expression
    ;
```

<span data-ttu-id="04edb-2284">`&&` И `||` операторы представляют собой условное версии `&` и `|` операторы:</span><span class="sxs-lookup"><span data-stu-id="04edb-2284">The `&&` and `||` operators are conditional versions of the `&` and `|` operators:</span></span>

*  <span data-ttu-id="04edb-2285">Операция `x && y` соответствующей операции `x & y`, за исключением того, что `y` вычисляется только в том случае, если `x` не `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2285">The operation `x && y` corresponds to the operation `x & y`, except that `y` is evaluated only if `x` is not `false`.</span></span>
*  <span data-ttu-id="04edb-2286">Операция `x || y` соответствующей операции `x | y`, за исключением того, что `y` вычисляется только в том случае, если `x` не `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2286">The operation `x || y` corresponds to the operation `x | y`, except that `y` is evaluated only if `x` is not `true`.</span></span>

<span data-ttu-id="04edb-2287">Если операнд условного логического оператора имеет тип времени компиляции `dynamic`, а затем он динамически связан ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2287">If an operand of a conditional logical operator has the compile-time type `dynamic`, then the expression is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2288">В данном случае является типов во время компиляции выражения `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, используя тип времени выполнения операндов, имеющих указанный тип времени компиляции `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2288">In this case the compile-time type of the expression is `dynamic`, and the resolution described below will take place at run-time using the run-time type of those operands that have the compile-time type `dynamic`.</span></span>

<span data-ttu-id="04edb-2289">Операции формы `x && y` или `x || y` обрабатывается с применением разрешение перегрузки ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) как если бы операция была `x & y` или `x | y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2289">An operation of the form `x && y` or `x || y` is processed by applying overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) as if the operation was written `x & y` or `x | y`.</span></span> <span data-ttu-id="04edb-2290">Затем,</span><span class="sxs-lookup"><span data-stu-id="04edb-2290">Then,</span></span>

*  <span data-ttu-id="04edb-2291">Если разрешение перегрузки не удается найти один подходящий оператор или разрешение перегрузки выбирает одну из предопределенные целочисленные логические операторы, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2291">If overload resolution fails to find a single best operator, or if overload resolution selects one of the predefined integer logical operators, a binding-time error occurs.</span></span>
*  <span data-ttu-id="04edb-2292">В противном случае, если выбранный оператор является одним из предопределенных логических операторов ([логические операторы](expressions.md#boolean-logical-operators)) или по Обнуляемые логические операторы ([Обнуляемые логические операторы](expressions.md#nullable-boolean-logical-operators)), операция обрабатывается, как описано в разделе [условные логические операторы](expressions.md#boolean-conditional-logical-operators).</span><span class="sxs-lookup"><span data-stu-id="04edb-2292">Otherwise, if the selected operator is one of the predefined boolean logical operators ([Boolean logical operators](expressions.md#boolean-logical-operators)) or nullable boolean logical operators ([Nullable boolean logical operators](expressions.md#nullable-boolean-logical-operators)), the operation is processed as described in [Boolean conditional logical operators](expressions.md#boolean-conditional-logical-operators).</span></span>
*  <span data-ttu-id="04edb-2293">В противном случае выбранный оператор является оператором определяемые пользователем, и эта операция обрабатывается, как описано в разделе [пользовательские условные логические операторы](expressions.md#user-defined-conditional-logical-operators).</span><span class="sxs-lookup"><span data-stu-id="04edb-2293">Otherwise, the selected operator is a user-defined operator, and the operation is processed as described in [User-defined conditional logical operators](expressions.md#user-defined-conditional-logical-operators).</span></span>

<span data-ttu-id="04edb-2294">Это не позволяет непосредственно перегрузить условные логические операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2294">It is not possible to directly overload the conditional logical operators.</span></span> <span data-ttu-id="04edb-2295">Тем не менее поскольку условные логические операторы вычисляются с точки зрения регулярных логических операторов, перегрузки регулярных логических операторов с некоторыми ограничениями, считаться перегрузками условных логических операторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2295">However, because the conditional logical operators are evaluated in terms of the regular logical operators, overloads of the regular logical operators are, with certain restrictions, also considered overloads of the conditional logical operators.</span></span> <span data-ttu-id="04edb-2296">Это описано далее в [пользовательские условные логические операторы](expressions.md#user-defined-conditional-logical-operators).</span><span class="sxs-lookup"><span data-stu-id="04edb-2296">This is described further in [User-defined conditional logical operators](expressions.md#user-defined-conditional-logical-operators).</span></span>

### <a name="boolean-conditional-logical-operators"></a><span data-ttu-id="04edb-2297">Условные логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2297">Boolean conditional logical operators</span></span>

<span data-ttu-id="04edb-2298">При операндов `&&` или `||` относятся к типу `bool`, или если операнды имеют типы, которые не определяют соответствующем `operator &` или `operator |`, но определить неявные преобразования в `bool`, операция обработан следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2298">When the operands of `&&` or `||` are of type `bool`, or when the operands are of types that do not define an applicable `operator &` or `operator |`, but do define implicit conversions to `bool`, the operation is processed as follows:</span></span>

*  <span data-ttu-id="04edb-2299">Операция `x && y` вычисляется как `x ? y : false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2299">The operation `x && y` is evaluated as `x ? y : false`.</span></span> <span data-ttu-id="04edb-2300">Другими словами `x` сначала вычисляется и преобразуется в тип `bool`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2300">In other words, `x` is first evaluated and converted to type `bool`.</span></span> <span data-ttu-id="04edb-2301">Затем, если `x` — `true`, `y` вычисляется и преобразуется в тип `bool`, и это становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2301">Then, if `x` is `true`, `y` is evaluated and converted to type `bool`, and this becomes the result of the operation.</span></span> <span data-ttu-id="04edb-2302">В противном случае результатом операции является `false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2302">Otherwise, the result of the operation is `false`.</span></span>
*  <span data-ttu-id="04edb-2303">Операция `x || y` вычисляется как `x ? true : y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2303">The operation `x || y` is evaluated as `x ? true : y`.</span></span> <span data-ttu-id="04edb-2304">Другими словами `x` сначала вычисляется и преобразуется в тип `bool`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2304">In other words, `x` is first evaluated and converted to type `bool`.</span></span> <span data-ttu-id="04edb-2305">Затем, если `x` — `true`, результатом операции является `true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2305">Then, if `x` is `true`, the result of the operation is `true`.</span></span> <span data-ttu-id="04edb-2306">В противном случае `y` вычисляется и преобразуется в тип `bool`, и это становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2306">Otherwise, `y` is evaluated and converted to type `bool`, and this becomes the result of the operation.</span></span>

### <a name="user-defined-conditional-logical-operators"></a><span data-ttu-id="04edb-2307">Пользовательские условные логические операторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2307">User-defined conditional logical operators</span></span>

<span data-ttu-id="04edb-2308">Когда операндов `&&` или `||` типов, которые объявляют соответствующем определяются пользователем `operator &` или `operator |`, оба следующих должен иметь значение true, где `T` является типом, в котором объявлен выбранного оператора:</span><span class="sxs-lookup"><span data-stu-id="04edb-2308">When the operands of `&&` or `||` are of types that declare an applicable user-defined `operator &` or `operator |`, both of the following must be true, where `T` is the type in which the selected operator is declared:</span></span>

*  <span data-ttu-id="04edb-2309">Тип возвращаемого значения и тип каждого параметра, выбранного оператора должны быть `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2309">The return type and the type of each parameter of the selected operator must be `T`.</span></span> <span data-ttu-id="04edb-2310">Другими словами, следует вычислять логического оператора `AND` или логической `OR` двух операндов типа `T`и должен возвращать результат типа `T`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2310">In other words, the operator must compute the logical `AND` or the logical `OR` of two operands of type `T`, and must return a result of type `T`.</span></span>
*  <span data-ttu-id="04edb-2311">`T` должен содержать объявления `operator true` и `operator false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2311">`T` must contain declarations of `operator true` and `operator false`.</span></span>

<span data-ttu-id="04edb-2312">Ошибка времени привязки возникает, если любой из этих требований не выполнено.</span><span class="sxs-lookup"><span data-stu-id="04edb-2312">A binding-time error occurs if either of these requirements is not satisfied.</span></span> <span data-ttu-id="04edb-2313">В противном случае `&&` или `||` операция вычисляется путем объединения, определяемые пользователем `operator true` или `operator false` с выбранной определяемого пользователем оператора:</span><span class="sxs-lookup"><span data-stu-id="04edb-2313">Otherwise, the `&&` or `||` operation is evaluated by combining the user-defined `operator true` or `operator false` with the selected user-defined operator:</span></span>

*  <span data-ttu-id="04edb-2314">Операция `x && y` вычисляется как `T.false(x) ? x : T.&(x, y)`, где `T.false(x)` является вызовом `operator false` объявленные в `T`, и `T.&(x, y)` является вызовом выбранного `operator &`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2314">The operation `x && y` is evaluated as `T.false(x) ? x : T.&(x, y)`, where `T.false(x)` is an invocation of the `operator false` declared in `T`, and `T.&(x, y)` is an invocation of the selected `operator &`.</span></span> <span data-ttu-id="04edb-2315">Другими словами `x` сначала оценивается и `operator false` вызывается на результат на предмет `x` имеет значение false.</span><span class="sxs-lookup"><span data-stu-id="04edb-2315">In other words, `x` is first evaluated and `operator false` is invoked on the result to determine if `x` is definitely false.</span></span> <span data-ttu-id="04edb-2316">Затем, если `x` имеет значение false, результатом операции является значение, ранее вычисленное для `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2316">Then, if `x` is definitely false, the result of the operation is the value previously computed for `x`.</span></span> <span data-ttu-id="04edb-2317">В противном случае `y` вычисляется и выбранным `operator &` вызывается на значение, ранее вычисленное для `x` и вычисленного значения `y` для получения результата операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2317">Otherwise, `y` is evaluated, and the selected `operator &` is invoked on the value previously computed for `x` and the value computed for `y` to produce the result of the operation.</span></span>
*  <span data-ttu-id="04edb-2318">Операция `x || y` вычисляется как `T.true(x) ? x : T.|(x, y)`, где `T.true(x)` является вызовом `operator true` объявленные в `T`, и `T.|(x,y)` является вызовом выбранного `operator|`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2318">The operation `x || y` is evaluated as `T.true(x) ? x : T.|(x, y)`, where `T.true(x)` is an invocation of the `operator true` declared in `T`, and `T.|(x,y)` is an invocation of the selected `operator|`.</span></span> <span data-ttu-id="04edb-2319">Другими словами `x` сначала оценивается и `operator true` вызывается на результат на предмет `x` имеет значение true.</span><span class="sxs-lookup"><span data-stu-id="04edb-2319">In other words, `x` is first evaluated and `operator true` is invoked on the result to determine if `x` is definitely true.</span></span> <span data-ttu-id="04edb-2320">Затем, если `x` имеет значение true, результатом операции является значение, ранее вычисленное для `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2320">Then, if `x` is definitely true, the result of the operation is the value previously computed for `x`.</span></span> <span data-ttu-id="04edb-2321">В противном случае `y` вычисляется и выбранным `operator |` вызывается на значение, ранее вычисленное для `x` и вычисленного значения `y` для получения результата операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2321">Otherwise, `y` is evaluated, and the selected `operator |` is invoked on the value previously computed for `x` and the value computed for `y` to produce the result of the operation.</span></span>

<span data-ttu-id="04edb-2322">В этих операций, выражение в `x` только вычисляется один раз и выражение в `y` либо не вычисляется или вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-2322">In either of these operations, the expression given by `x` is only evaluated once, and the expression given by `y` is either not evaluated or evaluated exactly once.</span></span>

<span data-ttu-id="04edb-2323">Например, тип, реализующий `operator true` и `operator false`, см. в разделе [базы данных логического типа](structs.md#database-boolean-type).</span><span class="sxs-lookup"><span data-stu-id="04edb-2323">For an example of a type that implements `operator true` and `operator false`, see [Database boolean type](structs.md#database-boolean-type).</span></span>

## <a name="the-null-coalescing-operator"></a><span data-ttu-id="04edb-2324">Оператор объединения со значением null</span><span class="sxs-lookup"><span data-stu-id="04edb-2324">The null coalescing operator</span></span>

<span data-ttu-id="04edb-2325">`??` Оператор был вызван оператор объединения со значением null.</span><span class="sxs-lookup"><span data-stu-id="04edb-2325">The `??` operator is called the null coalescing operator.</span></span>

```antlr
null_coalescing_expression
    : conditional_or_expression
    | conditional_or_expression '??' null_coalescing_expression
    ;
```

<span data-ttu-id="04edb-2326">Null объединения со значением выражения вида `a ?? b` требует `a` как обнуляемый тип или ссылку.</span><span class="sxs-lookup"><span data-stu-id="04edb-2326">A null coalescing expression of the form `a ?? b` requires `a` to be of a nullable type or reference type.</span></span> <span data-ttu-id="04edb-2327">Если `a` отлично от NULL, результат `a ?? b` — `a`; в противном случае результатом является `b`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2327">If `a` is non-null, the result of `a ?? b` is `a`; otherwise, the result is `b`.</span></span> <span data-ttu-id="04edb-2328">Эта операция проверяет `b` только если `a` имеет значение null.</span><span class="sxs-lookup"><span data-stu-id="04edb-2328">The operation evaluates `b` only if `a` is null.</span></span>

<span data-ttu-id="04edb-2329">Оператор объединения со значением null является правоассоциативным, это означает, что операции группируются слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-2329">The null coalescing operator is right-associative, meaning that operations are grouped from right to left.</span></span> <span data-ttu-id="04edb-2330">Например, выражение в форме `a ?? b ?? c` вычисляется как `a ?? (b ?? c)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2330">For example, an expression of the form `a ?? b ?? c` is evaluated as `a ?? (b ?? c)`.</span></span> <span data-ttu-id="04edb-2331">В целом, условия выражения формы `E1 ?? E2 ?? ... ?? En` возвращаются первые операндов, отличных от null, или значение null, если все операнды имеют значение null.</span><span class="sxs-lookup"><span data-stu-id="04edb-2331">In general terms, an expression of the form `E1 ?? E2 ?? ... ?? En` returns the first of the operands that is non-null, or null if all operands are null.</span></span>

<span data-ttu-id="04edb-2332">Тип выражения `a ?? b` зависит от того, какие неявные преобразования доступны с операндами.</span><span class="sxs-lookup"><span data-stu-id="04edb-2332">The type of the expression `a ?? b` depends on which implicit conversions are available on the operands.</span></span> <span data-ttu-id="04edb-2333">В порядке предпочтения, тип `a ?? b` — `A0`, `A`, или `B`, где `A` — это тип `a` (при условии, что `a` с типом), `B` — это тип `b` () при условии, что `b` с типом), и `A0` является базовым типом объекта `A` Если `A` является типом, допускающий значение NULL, или `A` в противном случае.</span><span class="sxs-lookup"><span data-stu-id="04edb-2333">In order of preference, the type of `a ?? b` is `A0`, `A`, or `B`, where `A` is the type of `a` (provided that `a` has a type), `B` is the type of `b` (provided that `b` has a type), and `A0` is the underlying type of `A` if `A` is a nullable type, or `A` otherwise.</span></span> <span data-ttu-id="04edb-2334">В частности `a ?? b` обрабатывается следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2334">Specifically, `a ?? b` is processed as follows:</span></span>

*  <span data-ttu-id="04edb-2335">Если `A` существует и не является обнуляемым типом или ссылочным типом, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2335">If `A` exists and is not a nullable type or a reference type, a compile-time error occurs.</span></span>
*  <span data-ttu-id="04edb-2336">Если `b` является динамическим выражением, тип результата — `dynamic`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2336">If `b` is a dynamic expression, the result type is `dynamic`.</span></span> <span data-ttu-id="04edb-2337">Во время выполнения `a` сначала оценивается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2337">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="04edb-2338">Если `a` не равно null, `a` преобразуется в динамический, и это становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2338">If `a` is not null, `a` is converted to dynamic, and this becomes the result.</span></span> <span data-ttu-id="04edb-2339">В противном случае `b` вычисляется, и это становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2339">Otherwise, `b` is evaluated, and this becomes the result.</span></span>
*  <span data-ttu-id="04edb-2340">В противном случае, если `A` существует и допускает значение NULL, и существует неявное преобразование из `b` для `A0`, тип результата — `A0`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2340">Otherwise, if `A` exists and is a nullable type and an implicit conversion exists from `b` to `A0`, the result type is `A0`.</span></span> <span data-ttu-id="04edb-2341">Во время выполнения `a` сначала оценивается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2341">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="04edb-2342">Если `a` не равно null, `a` распаковывается в тип `A0`, и это становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2342">If `a` is not null, `a` is unwrapped to type `A0`, and this becomes the result.</span></span> <span data-ttu-id="04edb-2343">В противном случае `b` вычисляется и преобразуется в тип `A0`, и это становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2343">Otherwise, `b` is evaluated and converted to type `A0`, and this becomes the result.</span></span>
*  <span data-ttu-id="04edb-2344">В противном случае, если `A` существует и существует неявное преобразование из `b` для `A`, тип результата — `A`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2344">Otherwise, if `A` exists and an implicit conversion exists from `b` to `A`, the result type is `A`.</span></span> <span data-ttu-id="04edb-2345">Во время выполнения `a` сначала оценивается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2345">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="04edb-2346">Если `a` не равно null, `a` становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2346">If `a` is not null, `a` becomes the result.</span></span> <span data-ttu-id="04edb-2347">В противном случае `b` вычисляется и преобразуется в тип `A`, и это становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2347">Otherwise, `b` is evaluated and converted to type `A`, and this becomes the result.</span></span>
*  <span data-ttu-id="04edb-2348">В противном случае, если `b` с типом `B` и существует неявное преобразование из `a` для `B`, тип результата — `B`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2348">Otherwise, if `b` has a type `B` and an implicit conversion exists from `a` to `B`, the result type is `B`.</span></span> <span data-ttu-id="04edb-2349">Во время выполнения `a` сначала оценивается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2349">At run-time, `a` is first evaluated.</span></span> <span data-ttu-id="04edb-2350">Если `a` не равно null, `a` распаковывается в тип `A0` (если `A` существует и допускает значения NULL) и он преобразуется в тип `B`, и это становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2350">If `a` is not null, `a` is unwrapped to type `A0` (if `A` exists and is nullable) and converted to type `B`, and this becomes the result.</span></span> <span data-ttu-id="04edb-2351">В противном случае `b` вычисляется и становится результатом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2351">Otherwise, `b` is evaluated and becomes the result.</span></span>
*  <span data-ttu-id="04edb-2352">В противном случае `a` и `b` являются несовместимыми и ошибка времени компиляции возникает.</span><span class="sxs-lookup"><span data-stu-id="04edb-2352">Otherwise, `a` and `b` are incompatible, and a compile-time error occurs.</span></span>

## <a name="conditional-operator"></a><span data-ttu-id="04edb-2353">Условный оператор</span><span class="sxs-lookup"><span data-stu-id="04edb-2353">Conditional operator</span></span>

<span data-ttu-id="04edb-2354">`?:` Оператор был вызван условного оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2354">The `?:` operator is called the conditional operator.</span></span> <span data-ttu-id="04edb-2355">Также в некоторых случаях он называется троичный оператор.</span><span class="sxs-lookup"><span data-stu-id="04edb-2355">It is at times also called the ternary operator.</span></span>

```antlr
conditional_expression
    : null_coalescing_expression
    | null_coalescing_expression '?' expression ':' expression
    ;
```

<span data-ttu-id="04edb-2356">Условное выражение в форме `b ? x : y` сначала оценивает условие `b`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2356">A conditional expression of the form `b ? x : y` first evaluates the condition `b`.</span></span> <span data-ttu-id="04edb-2357">Затем, если `b` — `true`, `x` вычисляется и становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2357">Then, if `b` is `true`, `x` is evaluated and becomes the result of the operation.</span></span> <span data-ttu-id="04edb-2358">В противном случае `y` вычисляется и становится результатом операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2358">Otherwise, `y` is evaluated and becomes the result of the operation.</span></span> <span data-ttu-id="04edb-2359">Условное выражение вычислено, никогда не оба `x` и `y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2359">A conditional expression never evaluates both `x` and `y`.</span></span>

<span data-ttu-id="04edb-2360">Условный оператор имеет правую ассоциативность, это означает, что операции группируются слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-2360">The conditional operator is right-associative, meaning that operations are grouped from right to left.</span></span> <span data-ttu-id="04edb-2361">Например, выражение в форме `a ? b : c ? d : e` вычисляется как `a ? b : (c ? d : e)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2361">For example, an expression of the form `a ? b : c ? d : e` is evaluated as `a ? b : (c ? d : e)`.</span></span>

<span data-ttu-id="04edb-2362">Первый операнд `?:` оператор должен быть выражением, которое может быть неявно преобразован в `bool`, или выражение типа, который реализует `operator true`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2362">The first operand of the `?:` operator must be an expression that can be implicitly converted to `bool`, or an expression of a type that implements `operator true`.</span></span> <span data-ttu-id="04edb-2363">Если не выполняется ни одно из этих требований, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2363">If neither of these requirements is satisfied, a compile-time error occurs.</span></span>

<span data-ttu-id="04edb-2364">Второй и третий операнды, `x` и `y`, из `?:` оператор управления тип условного выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2364">The second and third operands, `x` and `y`, of the `?:` operator control the type of the conditional expression.</span></span>

*  <span data-ttu-id="04edb-2365">Если `x` имеет тип `X` и `y` имеет тип `Y` затем</span><span class="sxs-lookup"><span data-stu-id="04edb-2365">If `x` has type `X` and `y` has type `Y` then</span></span>
   * <span data-ttu-id="04edb-2366">Если неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) существует из `X` для `Y`, но не из `Y` для `X`, затем `Y` тип условного выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2366">If an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from `X` to `Y`, but not from `Y` to `X`, then `Y` is the type of the conditional expression.</span></span>
   * <span data-ttu-id="04edb-2367">Если неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)) существует из `Y` для `X`, но не из `X` для `Y`, затем `X` тип условного выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2367">If an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)) exists from `Y` to `X`, but not from `X` to `Y`, then `X` is the type of the conditional expression.</span></span>
   * <span data-ttu-id="04edb-2368">В противном случае можно определить тип выражения, и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2368">Otherwise, no expression type can be determined, and a compile-time error occurs.</span></span>
*  <span data-ttu-id="04edb-2369">Если только один из `x` и `y` имеет тип и оба `x` и `y`, из неявно преобразуются к этому типу, а затем этот тип условного выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2369">If only one of `x` and `y` has a type, and both `x` and `y`, of are implicitly convertible to that type, then that is the type of the conditional expression.</span></span>
*  <span data-ttu-id="04edb-2370">В противном случае можно определить тип выражения, и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2370">Otherwise, no expression type can be determined, and a compile-time error occurs.</span></span>

<span data-ttu-id="04edb-2371">Обработка времени выполнения условного выражения формы `b ? x : y` состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-2371">The run-time processing of a conditional expression of the form `b ? x : y` consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-2372">Во-первых, `b` вычисляется и `bool` значение `b` определяется:</span><span class="sxs-lookup"><span data-stu-id="04edb-2372">First, `b` is evaluated, and the `bool` value of `b` is determined:</span></span>
   * <span data-ttu-id="04edb-2373">Если неявное преобразование из типа `b` для `bool` существует, то это неявное преобразование выполняется для создания `bool` значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2373">If an implicit conversion from the type of `b` to `bool` exists, then this implicit conversion is performed to produce a `bool` value.</span></span>
   * <span data-ttu-id="04edb-2374">В противном случае `operator true` определяется тип `b` вызываемый для получения `bool` значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2374">Otherwise, the `operator true` defined by the type of `b` is invoked to produce a `bool` value.</span></span>
*  <span data-ttu-id="04edb-2375">Если `bool` является значение, созданное на предыдущем шаге `true`, затем `x` вычисляется и преобразуется в тип условного выражения, и это становится результатом условного выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2375">If the `bool` value produced by the step above is `true`, then `x` is evaluated and converted to the type of the conditional expression, and this becomes the result of the conditional expression.</span></span>
*  <span data-ttu-id="04edb-2376">В противном случае `y` вычисляется и преобразуется в тип условного выражения, и это становится результатом условного выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2376">Otherwise, `y` is evaluated and converted to the type of the conditional expression, and this becomes the result of the conditional expression.</span></span>

## <a name="anonymous-function-expressions"></a><span data-ttu-id="04edb-2377">Выражения анонимных функций</span><span class="sxs-lookup"><span data-stu-id="04edb-2377">Anonymous function expressions</span></span>

<span data-ttu-id="04edb-2378">***Анонимная функция*** выражение, которое представляет определение метода «в строке».</span><span class="sxs-lookup"><span data-stu-id="04edb-2378">An ***anonymous function*** is an expression that represents an "in-line" method definition.</span></span> <span data-ttu-id="04edb-2379">Анонимная функция не имеет значения или тип само по себе, но можно преобразовать в совместимый тип делегата или выражения дерева.</span><span class="sxs-lookup"><span data-stu-id="04edb-2379">An anonymous function does not have a value or type in and of itself, but is convertible to a compatible delegate or expression tree type.</span></span> <span data-ttu-id="04edb-2380">Вычисление преобразование анонимной функции зависит от целевой тип преобразования: Если он является типом делегата, преобразование результатом которого является значение делегата, ссылке на метод, который определяет анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2380">The evaluation of an anonymous function conversion depends on the target type of the conversion: If it is a delegate type, the conversion evaluates to a delegate value referencing the method which the anonymous function defines.</span></span> <span data-ttu-id="04edb-2381">Если это тип дерева выражения, то результатом преобразования в дерево выражения, которое представляет структуру метода в виде структуры объекта.</span><span class="sxs-lookup"><span data-stu-id="04edb-2381">If it is an expression tree type, the conversion evaluates to an expression tree which represents the structure of the method as an object structure.</span></span>

<span data-ttu-id="04edb-2382">По историческим причинам существует два синтаксический варианта анонимных функций, а именно *lambda_expression*s и *anonymous_method_expression*s.</span><span class="sxs-lookup"><span data-stu-id="04edb-2382">For historical reasons there are two syntactic flavors of anonymous functions, namely *lambda_expression*s and *anonymous_method_expression*s.</span></span> <span data-ttu-id="04edb-2383">Практически для любых целей *lambda_expression*s являются более четкими и выразительной, чем *anonymous_method_expression*s, которые остаются в язык для обеспечения обратной совместимости.</span><span class="sxs-lookup"><span data-stu-id="04edb-2383">For almost all purposes, *lambda_expression*s are more concise and expressive than *anonymous_method_expression*s, which remain in the language for backwards compatibility.</span></span>

```antlr
lambda_expression
    : anonymous_function_signature '=>' anonymous_function_body
    ;

anonymous_method_expression
    : 'delegate' explicit_anonymous_function_signature? block
    ;

anonymous_function_signature
    : explicit_anonymous_function_signature
    | implicit_anonymous_function_signature
    ;

explicit_anonymous_function_signature
    : '(' explicit_anonymous_function_parameter_list? ')'
    ;

explicit_anonymous_function_parameter_list
    : explicit_anonymous_function_parameter (',' explicit_anonymous_function_parameter)*
    ;

explicit_anonymous_function_parameter
    : anonymous_function_parameter_modifier? type identifier
    ;

anonymous_function_parameter_modifier
    : 'ref'
    | 'out'
    ;

implicit_anonymous_function_signature
    : '(' implicit_anonymous_function_parameter_list? ')'
    | implicit_anonymous_function_parameter
    ;

implicit_anonymous_function_parameter_list
    : implicit_anonymous_function_parameter (',' implicit_anonymous_function_parameter)*
    ;

implicit_anonymous_function_parameter
    : identifier
    ;

anonymous_function_body
    : expression
    | block
    ;
```

<span data-ttu-id="04edb-2384">`=>` Оператор имеет тот же приоритет, как и присваивание (`=`) и является правоассоциативным.</span><span class="sxs-lookup"><span data-stu-id="04edb-2384">The `=>` operator has the same precedence as assignment (`=`) and is right-associative.</span></span>

<span data-ttu-id="04edb-2385">Анонимная функция с `async` модификатор является асинхронной функции и следует правилам, описанным в [итераторы](classes.md#iterators).</span><span class="sxs-lookup"><span data-stu-id="04edb-2385">An anonymous function with the `async` modifier is an async function and follows the rules described in [Iterators](classes.md#iterators).</span></span>

<span data-ttu-id="04edb-2386">Параметры анонимной функции в виде *lambda_expression* может быть явно или неявно типизированы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2386">The parameters of an anonymous function in the form of a *lambda_expression* can be explicitly or implicitly typed.</span></span> <span data-ttu-id="04edb-2387">В списке параметров явным образом типизированной явно указан тип каждого параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-2387">In an explicitly typed parameter list, the type of each parameter is explicitly stated.</span></span> <span data-ttu-id="04edb-2388">В списке неявно типизированных параметров, типы параметров выводятся из контекста, в котором происходит анонимная функция — в частности, если анонимная функция преобразуется в совместимый тип делегата или тип дерева выражения, предоставляющий тип типы параметров ([преобразования анонимных функций](conversions.md#anonymous-function-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2388">In an implicitly typed parameter list, the types of the parameters are inferred from the context in which the anonymous function occurs—specifically, when the anonymous function is converted to a compatible delegate type or expression tree type, that type provides the parameter types ([Anonymous function conversions](conversions.md#anonymous-function-conversions)).</span></span>

<span data-ttu-id="04edb-2389">В анонимную функцию с параметром единый, неявно типизированные скобки можно опустить из списка параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-2389">In an anonymous function with a single, implicitly typed parameter, the parentheses may be omitted from the parameter list.</span></span> <span data-ttu-id="04edb-2390">Другими словами анонимная функция формы</span><span class="sxs-lookup"><span data-stu-id="04edb-2390">In other words, an anonymous function of the form</span></span>
```csharp
( param ) => expr
```
<span data-ttu-id="04edb-2391">можно сократить до</span><span class="sxs-lookup"><span data-stu-id="04edb-2391">can be abbreviated to</span></span>
```csharp
param => expr
```

<span data-ttu-id="04edb-2392">Список параметров анонимной функции в виде *anonymous_method_expression* является необязательным.</span><span class="sxs-lookup"><span data-stu-id="04edb-2392">The parameter list of an anonymous function in the form of an *anonymous_method_expression* is optional.</span></span> <span data-ttu-id="04edb-2393">Если он задан, параметры должны быть явно типизированы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2393">If given, the parameters must be explicitly typed.</span></span> <span data-ttu-id="04edb-2394">Если нет, можно преобразовать в делегат с помощью любого параметра анонимной функции, список, не содержащий `out` параметры.</span><span class="sxs-lookup"><span data-stu-id="04edb-2394">If not, the anonymous function is convertible to a delegate with any parameter list not containing `out` parameters.</span></span>

<span data-ttu-id="04edb-2395">Объект *блок* доступен тело анонимная функция ([конечные точки и доступность](statements.md#end-points-and-reachability)) пока не произойдет анонимной функции внутри инструкции недоступен.</span><span class="sxs-lookup"><span data-stu-id="04edb-2395">A *block* body of an anonymous function is reachable ([End points and reachability](statements.md#end-points-and-reachability)) unless the anonymous function occurs inside an unreachable statement.</span></span>

<span data-ttu-id="04edb-2396">Ниже приведены некоторые примеры анонимных функций ниже:</span><span class="sxs-lookup"><span data-stu-id="04edb-2396">Some examples of anonymous functions follow below:</span></span>

```csharp
x => x + 1                              // Implicitly typed, expression body
x => { return x + 1; }                  // Implicitly typed, statement body
(int x) => x + 1                        // Explicitly typed, expression body
(int x) => { return x + 1; }            // Explicitly typed, statement body
(x, y) => x * y                         // Multiple parameters
() => Console.WriteLine()               // No parameters
async (t1,t2) => await t1 + await t2    // Async
delegate (int x) { return x + 1; }      // Anonymous method expression
delegate { return 1 + 1; }              // Parameter list omitted
```

<span data-ttu-id="04edb-2397">Поведение *lambda_expression*s и *anonymous_method_expression*s различается только следующие моменты:</span><span class="sxs-lookup"><span data-stu-id="04edb-2397">The behavior of *lambda_expression*s and *anonymous_method_expression*s is the same except for the following points:</span></span>

*  <span data-ttu-id="04edb-2398">*anonymous_method_expression*s разрешить список параметров, чтобы опустить целиком, обеспечивая возможность делегировать типы любой список параметров значение преобразования.</span><span class="sxs-lookup"><span data-stu-id="04edb-2398">*anonymous_method_expression*s permit the parameter list to be omitted entirely, yielding convertibility to delegate types of any list of value parameters.</span></span>
*  <span data-ttu-id="04edb-2399">*lambda_expression*s разрешения типов параметр опущен и вывести, тогда как *anonymous_method_expression*s требуется явно указывать типы параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-2399">*lambda_expression*s permit parameter types to be omitted and inferred whereas *anonymous_method_expression*s require parameter types to be explicitly stated.</span></span>
*  <span data-ttu-id="04edb-2400">Тело *lambda_expression* может быть выражение или блок операторов, тогда как тело *anonymous_method_expression* должен быть блок операторов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2400">The body of a *lambda_expression* can be an expression or a statement block whereas the body of an *anonymous_method_expression* must be a statement block.</span></span>
*  <span data-ttu-id="04edb-2401">Только *lambda_expression*имеют преобразования в типы дерева выражений, совместимый ([типы дерева выражений](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2401">Only *lambda_expression*s have conversions to compatible expression tree types ([Expression tree types](types.md#expression-tree-types)).</span></span>

### <a name="anonymous-function-signatures"></a><span data-ttu-id="04edb-2402">Сигнатуры анонимных функций</span><span class="sxs-lookup"><span data-stu-id="04edb-2402">Anonymous function signatures</span></span>

<span data-ttu-id="04edb-2403">Необязательный *anonymous_function_signature* анонимной функции определяет имена и при необходимости типы формальных параметров для анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2403">The optional *anonymous_function_signature* of an anonymous function defines the names and optionally the types of the formal parameters for the anonymous function.</span></span> <span data-ttu-id="04edb-2404">Область параметров анонимной функции — *anonymous_function_body*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2404">The scope of the parameters of the anonymous function is the *anonymous_function_body*.</span></span> <span data-ttu-id="04edb-2405">([Областей](basic-concepts.md#scopes)) совместно со списком параметров (если есть) в тексте анонимного метода задает пространство объявления ([объявления](basic-concepts.md#declarations)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2405">([Scopes](basic-concepts.md#scopes)) Together with the parameter list (if given) the anonymous-method-body constitutes a declaration space ([Declarations](basic-concepts.md#declarations)).</span></span> <span data-ttu-id="04edb-2406">Таким образом является ошибкой во время компиляции для имени параметра анонимной функции в соответствии с именем локальной переменной, локальной константы или параметра, область которого входят *anonymous_method_expression* или *lambda_ выражение*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2406">It is thus a compile-time error for the name of a parameter of the anonymous function to match the name of a local variable, local constant or parameter whose scope includes the *anonymous_method_expression* or *lambda_expression*.</span></span>

<span data-ttu-id="04edb-2407">Если анонимная функция *explicit_anonymous_function_signature*, а затем набор совместимых типов делегатов и типы дерева выражений, ограничены теми, которые с такими же типами параметров и модификаторы в том же порядке.</span><span class="sxs-lookup"><span data-stu-id="04edb-2407">If an anonymous function has an *explicit_anonymous_function_signature*, then the set of compatible delegate types and expression tree types is restricted to those that have the same parameter types and modifiers in the same order.</span></span> <span data-ttu-id="04edb-2408">В отличие от преобразования групп методов ([преобразования групп методов](conversions.md#method-group-conversions)), контрвариантность типов параметра анонимная функция не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2408">In contrast to method group conversions ([Method group conversions](conversions.md#method-group-conversions)), contra-variance of anonymous function parameter types is not supported.</span></span> <span data-ttu-id="04edb-2409">Если анонимная функция не имеет *anonymous_function_signature*, а затем набор совместимых типов делегатов и типы дерева выражений, ограничены теми, которые не имеют `out` параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-2409">If an anonymous function does not have an *anonymous_function_signature*, then the set of compatible delegate types and expression tree types is restricted to those that have no `out` parameters.</span></span>

<span data-ttu-id="04edb-2410">Обратите внимание, что *anonymous_function_signature* не может включать атрибуты или массивом параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-2410">Note that an *anonymous_function_signature* cannot include attributes or a parameter array.</span></span> <span data-ttu-id="04edb-2411">Тем не менее *anonymous_function_signature* могут быть совместимы с типом делегата, список параметров которого содержит массив параметров.</span><span class="sxs-lookup"><span data-stu-id="04edb-2411">Nevertheless, an *anonymous_function_signature* may be compatible with a delegate type whose parameter list contains a parameter array.</span></span>

<span data-ttu-id="04edb-2412">Обратите внимание, что преобразование в тип дерева выражения, даже если совместимость, может привести к сбою во время компиляции ([типы дерева выражений](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2412">Note also that conversion to an expression tree type, even if compatible, may still fail at compile-time ([Expression tree types](types.md#expression-tree-types)).</span></span>

### <a name="anonymous-function-bodies"></a><span data-ttu-id="04edb-2413">Тела анонимных функций</span><span class="sxs-lookup"><span data-stu-id="04edb-2413">Anonymous function bodies</span></span>

<span data-ttu-id="04edb-2414">Текст (*выражение* или *блок*) анонимной функции, регулируется следующими правилами:</span><span class="sxs-lookup"><span data-stu-id="04edb-2414">The body (*expression* or *block*) of an anonymous function is subject to the following rules:</span></span>

*  <span data-ttu-id="04edb-2415">Если анонимная функция включает сигнатуру, параметрам, указанным в сигнатуре доступны в тексте.</span><span class="sxs-lookup"><span data-stu-id="04edb-2415">If the anonymous function includes a signature, the parameters specified in the signature are available in the body.</span></span> <span data-ttu-id="04edb-2416">Если анонимная функция не имеет подписи его можно преобразовать в тип делегата или тип выражения с параметрами ([преобразования анонимных функций](conversions.md#anonymous-function-conversions)), но параметры не в тексте.</span><span class="sxs-lookup"><span data-stu-id="04edb-2416">If the anonymous function has no signature it can be converted to a delegate type or expression type having parameters ([Anonymous function conversions](conversions.md#anonymous-function-conversions)), but the parameters cannot be accessed in the body.</span></span>
*  <span data-ttu-id="04edb-2417">За исключением `ref` или `out` параметров, указанных в сигнатуре (если таковые имеются) ближайшего внешнего анонимная функция, это ошибка времени компиляции для текста для доступа к `ref` или `out` параметра.</span><span class="sxs-lookup"><span data-stu-id="04edb-2417">Except for `ref` or `out` parameters specified in the signature (if any) of the nearest enclosing anonymous function, it is a compile-time error for the body to access a `ref` or `out` parameter.</span></span>
*  <span data-ttu-id="04edb-2418">Если тип `this` является типом структуры, это ошибка времени компиляции для текста для доступа к `this`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2418">When the type of `this` is a struct type, it is a compile-time error for the body to access `this`.</span></span> <span data-ttu-id="04edb-2419">Это верно, является ли доступ явные (как в `this.x`) или неявными (как в `x` где `x` является членом экземпляра структуры).</span><span class="sxs-lookup"><span data-stu-id="04edb-2419">This is true whether the access is explicit (as in `this.x`) or implicit (as in `x` where `x` is an instance member of the struct).</span></span> <span data-ttu-id="04edb-2420">Это правило просто запрещает такой доступ и не влияет на поиске члена является членом структуры.</span><span class="sxs-lookup"><span data-stu-id="04edb-2420">This rule simply prohibits such access and does not affect whether member lookup results in a member of the struct.</span></span>
*  <span data-ttu-id="04edb-2421">Тело имеет доступ к внешним переменным ([переменные Outer](expressions.md#outer-variables)) анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2421">The body has access to the outer variables ([Outer variables](expressions.md#outer-variables)) of the anonymous function.</span></span> <span data-ttu-id="04edb-2422">Доступ к внешней переменной будет ссылаться на экземпляр переменной, которая активна на момент *lambda_expression* или *anonymous_method_expression* вычисляется ([оценки выражения анонимных функций](expressions.md#evaluation-of-anonymous-function-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2422">Access of an outer variable will reference the instance of the variable that is active at the time the *lambda_expression* or *anonymous_method_expression* is evaluated ([Evaluation of anonymous function expressions](expressions.md#evaluation-of-anonymous-function-expressions)).</span></span>
*  <span data-ttu-id="04edb-2423">Произошла ошибка во время компиляции, для текста, который содержит `goto` инструкции `break` инструкции или `continue` инструкции, целевой объект которого находится вне тела либо в теле содержащейся анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2423">It is a compile-time error for the body to contain a `goto` statement, `break` statement, or `continue` statement whose target is outside the body or within the body of a contained anonymous function.</span></span>
*  <span data-ttu-id="04edb-2424">Объект `return` оператор в теле возвращает управление из вызова ближайшего внешнего оператора анонимной функции, не из включающей функции-члена.</span><span class="sxs-lookup"><span data-stu-id="04edb-2424">A `return` statement in the body returns control from an invocation of the nearest enclosing anonymous function, not from the enclosing function member.</span></span> <span data-ttu-id="04edb-2425">Выражения, указанного в `return` инструкция должна быть неявно преобразуемым в возвращаемый тип, тип делегата или тип дерева выражения, к которому ближайшего внешнего оператора *lambda_expression* или *anonymous_ method_expression* преобразуется ([преобразования анонимных функций](conversions.md#anonymous-function-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2425">An expression specified in a `return` statement must be implicitly convertible to the return type of the delegate type or expression tree type to which the nearest enclosing *lambda_expression* or *anonymous_method_expression* is converted ([Anonymous function conversions](conversions.md#anonymous-function-conversions)).</span></span>

<span data-ttu-id="04edb-2426">Не явно указано, есть ли способ выполнить блок анонимной функции отличный от вычисления и вызов *lambda_expression* или *anonymous_method_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2426">It is explicitly unspecified whether there is any way to execute the block of an anonymous function other than through evaluation and invocation of the *lambda_expression* or *anonymous_method_expression*.</span></span> <span data-ttu-id="04edb-2427">В частности компилятор может реализовать анонимную функцию, создав один или несколько именованных методов или типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2427">In particular, the compiler may choose to implement an anonymous function by synthesizing one or more named methods or types.</span></span> <span data-ttu-id="04edb-2428">Имена таких созданных элементов должны быть зарезервированы для внутреннего использования компиляторами формы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2428">The names of any such synthesized elements must be of a form reserved for compiler use.</span></span>

### <a name="overload-resolution-and-anonymous-functions"></a><span data-ttu-id="04edb-2429">Разрешение перегрузки и анонимных функций</span><span class="sxs-lookup"><span data-stu-id="04edb-2429">Overload resolution and anonymous functions</span></span>

<span data-ttu-id="04edb-2430">Анонимные функции в списке аргументов участвуют в выводе типа и разрешении перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2430">Anonymous functions in an argument list participate in type inference and overload resolution.</span></span> <span data-ttu-id="04edb-2431">Обратитесь к [вывод типа](expressions.md#type-inference) и [разрешение перегрузки](expressions.md#overload-resolution) конкретные правила.</span><span class="sxs-lookup"><span data-stu-id="04edb-2431">Please refer to [Type inference](expressions.md#type-inference) and [Overload resolution](expressions.md#overload-resolution) for the exact rules.</span></span>

<span data-ttu-id="04edb-2432">В следующем примере показано влияние анонимных функций на разрешение перегрузки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2432">The following example illustrates the effect of anonymous functions on overload resolution.</span></span>

```csharp
class ItemList<T>: List<T>
{
    public int Sum(Func<T,int> selector) {
        int sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }

    public double Sum(Func<T,double> selector) {
        double sum = 0;
        foreach (T item in this) sum += selector(item);
        return sum;
    }
}
```

<span data-ttu-id="04edb-2433">`ItemList<T>` Класс имеет два `Sum` методы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2433">The `ItemList<T>` class has two `Sum` methods.</span></span> <span data-ttu-id="04edb-2434">Каждое принимает `selector` аргументом, который извлекает значение для суммы на из элемента списка.</span><span class="sxs-lookup"><span data-stu-id="04edb-2434">Each takes a `selector` argument, which extracts the value to sum over from a list item.</span></span> <span data-ttu-id="04edb-2435">Извлеченное значение может быть либо `int` или `double` и Результирующая сумма равна точно так же `int` или `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2435">The extracted value can be either an `int` or a `double` and the resulting sum is likewise either an `int` or a `double`.</span></span>

<span data-ttu-id="04edb-2436">`Sum` Методы, например может использоваться для вычисления суммы из списка значений строк детализации в порядке.</span><span class="sxs-lookup"><span data-stu-id="04edb-2436">The `Sum` methods could for example be used to compute sums from a list of detail lines in an order.</span></span>

```csharp
class Detail
{
    public int UnitCount;
    public double UnitPrice;
    ...
}

void ComputeSums() {
    ItemList<Detail> orderDetails = GetOrderDetails(...);
    int totalUnits = orderDetails.Sum(d => d.UnitCount);
    double orderTotal = orderDetails.Sum(d => d.UnitPrice * d.UnitCount);
    ...
}
```

<span data-ttu-id="04edb-2437">В первом вызове `orderDetails.Sum`, оба `Sum` методы применимы так как анонимная функция `d => d. UnitCount` совместима с обоими `Func<Detail,int>` и `Func<Detail,double>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2437">In the first invocation of `orderDetails.Sum`, both `Sum` methods are applicable because the anonymous function `d => d. UnitCount` is compatible with both `Func<Detail,int>` and `Func<Detail,double>`.</span></span> <span data-ttu-id="04edb-2438">Тем не менее, разрешение перегрузки выбирает первый `Sum` метод так как преобразование в `Func<Detail,int>` лучше, чем преобразование в `Func<Detail,double>`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2438">However, overload resolution picks the first `Sum` method because the conversion to `Func<Detail,int>` is better than the conversion to `Func<Detail,double>`.</span></span>

<span data-ttu-id="04edb-2439">При втором вызове рабочих `orderDetails.Sum`, только второй `Sum` метод применим так как анонимная функция `d => d.UnitPrice * d.UnitCount` создает значение типа `double`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2439">In the second invocation of `orderDetails.Sum`, only the second `Sum` method is applicable because the anonymous function `d => d.UnitPrice * d.UnitCount` produces a value of type `double`.</span></span> <span data-ttu-id="04edb-2440">Таким образом, перегрузки при разрешении выбран второй `Sum` метод для вызова.</span><span class="sxs-lookup"><span data-stu-id="04edb-2440">Thus, overload resolution picks the second `Sum` method for that invocation.</span></span>

### <a name="anonymous-functions-and-dynamic-binding"></a><span data-ttu-id="04edb-2441">Анонимные функции и динамическая привязка</span><span class="sxs-lookup"><span data-stu-id="04edb-2441">Anonymous functions and dynamic binding</span></span>

<span data-ttu-id="04edb-2442">Анонимная функция не может быть получателем, аргументом или операнд динамически связанные операции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2442">An anonymous function cannot be a receiver, argument or operand of a dynamically bound operation.</span></span>

### <a name="outer-variables"></a><span data-ttu-id="04edb-2443">Внешние переменные</span><span class="sxs-lookup"><span data-stu-id="04edb-2443">Outer variables</span></span>

<span data-ttu-id="04edb-2444">Любой локальной переменной, значение параметра или массив параметров, область которого входят *lambda_expression* или *anonymous_method_expression* называется ***внешней переменной*** Анонимные функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2444">Any local variable, value parameter, or parameter array whose scope includes the *lambda_expression* or *anonymous_method_expression* is called an ***outer variable*** of the anonymous function.</span></span> <span data-ttu-id="04edb-2445">В экземпляр функции-члене класса `this` значение считается параметром значения и является внешней переменной любой анонимной функции, содержащиеся в функцию-член.</span><span class="sxs-lookup"><span data-stu-id="04edb-2445">In an instance function member of a class, the `this` value is considered a value parameter and is an outer variable of any anonymous function contained within the function member.</span></span>

#### <a name="captured-outer-variables"></a><span data-ttu-id="04edb-2446">Захваченные внешние переменные</span><span class="sxs-lookup"><span data-stu-id="04edb-2446">Captured outer variables</span></span>

<span data-ttu-id="04edb-2447">Если внешняя переменная ссылается анонимная функция, внешней переменной называется были ***захвата*** анонимной функцией.</span><span class="sxs-lookup"><span data-stu-id="04edb-2447">When an outer variable is referenced by an anonymous function, the outer variable is said to have been ***captured*** by the anonymous function.</span></span> <span data-ttu-id="04edb-2448">Как правило, время существования локальной переменной ограничен выполнения блока или инструкции, с которым он связан ([локальные переменные](variables.md#local-variables)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2448">Ordinarily, the lifetime of a local variable is limited to execution of the block or statement with which it is associated ([Local variables](variables.md#local-variables)).</span></span> <span data-ttu-id="04edb-2449">Тем не менее время существования захваченной внешней переменной увеличивается по крайней мере, пока делегат или дерево выражения, созданного из анонимная функция становится пригодным для сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2449">However, the lifetime of a captured outer variable is extended at least until the delegate or expression tree created from the anonymous function becomes eligible for garbage collection.</span></span>

<span data-ttu-id="04edb-2450">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2450">In the example</span></span>
```csharp
using System;

delegate int D();

class Test
{
    static D F() {
        int x = 0;
        D result = () => ++x;
        return result;
    }

    static void Main() {
        D d = F();
        Console.WriteLine(d());
        Console.WriteLine(d());
        Console.WriteLine(d());
    }
}
```
<span data-ttu-id="04edb-2451">Локальная переменная `x` захвачена анонимной функции и время существования `x` расширяется по крайней мере, пока делегат, возвращенный `F` становится пригодным для сборки мусора (что произойдет до самого конца Программа).</span><span class="sxs-lookup"><span data-stu-id="04edb-2451">the local variable `x` is captured by the anonymous function, and the lifetime of `x` is extended at least until the delegate returned from `F` becomes eligible for garbage collection (which doesn't happen until the very end of the program).</span></span> <span data-ttu-id="04edb-2452">Поскольку каждый вызов анонимная функция работает на том же экземпляре `x`, выходные данные примера:</span><span class="sxs-lookup"><span data-stu-id="04edb-2452">Since each invocation of the anonymous function operates on the same instance of `x`, the output of the example is:</span></span>
```
1
2
3
```

<span data-ttu-id="04edb-2453">При локальной переменной или параметром записанным анонимную функцию, локальную переменную или параметр больше не считается фиксированная переменная ([атрибутов неизменности и перемещаемые переменные](unsafe-code.md#fixed-and-moveable-variables)), но вместо этого считается moveable переменная.</span><span class="sxs-lookup"><span data-stu-id="04edb-2453">When a local variable or a value parameter is captured by an anonymous function, the local variable or parameter is no longer considered to be a fixed variable ([Fixed and moveable variables](unsafe-code.md#fixed-and-moveable-variables)), but is instead considered to be a moveable variable.</span></span> <span data-ttu-id="04edb-2454">Таким образом любой `unsafe` необходимо сначала использовать код, который принимает адрес захваченной внешней переменной `fixed` инструкцию, чтобы зафиксировать переменную.</span><span class="sxs-lookup"><span data-stu-id="04edb-2454">Thus any `unsafe` code that takes the address of a captured outer variable must first use the `fixed` statement to fix the variable.</span></span>

<span data-ttu-id="04edb-2455">Обратите внимание, что в отличие от переменной uncaptured, захваченной локальной переменной может быть открыт одновременно для нескольких потоков выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2455">Note that unlike an uncaptured variable, a captured local variable can be simultaneously exposed to multiple threads of execution.</span></span>

#### <a name="instantiation-of-local-variables"></a><span data-ttu-id="04edb-2456">Создание экземпляров локальных переменных</span><span class="sxs-lookup"><span data-stu-id="04edb-2456">Instantiation of local variables</span></span>

<span data-ttu-id="04edb-2457">Локальная переменная считается ***экземпляр*** при выполнения входит в область действия переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-2457">A local variable is considered to be ***instantiated*** when execution enters the scope of the variable.</span></span> <span data-ttu-id="04edb-2458">Например, при вызове следующий метод, локальной переменной `x` создается и инициализируется три раза — один раз для каждой итерации цикла.</span><span class="sxs-lookup"><span data-stu-id="04edb-2458">For example, when the following method is invoked, the local variable `x` is instantiated and initialized three times—once for each iteration of the loop.</span></span>

```csharp
static void F() {
    for (int i = 0; i < 3; i++) {
        int x = i * 2 + 1;
        ...
    }
}
```

<span data-ttu-id="04edb-2459">Тем не менее, переместив объявления `x` за пределами цикла результаты в один экземпляр `x`:</span><span class="sxs-lookup"><span data-stu-id="04edb-2459">However, moving the declaration of `x` outside the loop results in a single instantiation of `x`:</span></span>
```csharp
static void F() {
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
        ...
    }
}
```

<span data-ttu-id="04edb-2460">Когда не захвачена, не существует способа для наблюдения за точно, как часто создается локальная переменная, так как время существования экземпляров не существует вероятность для каждого экземпляра, чтобы просто использовать то же место хранения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2460">When not captured, there is no way to observe exactly how often a local variable is instantiated—because the lifetimes of the instantiations are disjoint, it is possible for each instantiation to simply use the same storage location.</span></span> <span data-ttu-id="04edb-2461">Тем не менее когда анонимная функция захватывает локальную переменную, результат создания экземпляра становятся очевидными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2461">However, when an anonymous function captures a local variable, the effects of instantiation become apparent.</span></span>

<span data-ttu-id="04edb-2462">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2462">The example</span></span>
```csharp
using System;

delegate void D();

class Test
{
    static D[] F() {
        D[] result = new D[3];
        for (int i = 0; i < 3; i++) {
            int x = i * 2 + 1;
            result[i] = () => { Console.WriteLine(x); };
        }
        return result;
    }

    static void Main() {
        foreach (D d in F()) d();
    }
}
```
<span data-ttu-id="04edb-2463">выводятся следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="04edb-2463">produces the output:</span></span>
```
1
3
5
```

<span data-ttu-id="04edb-2464">Тем не менее, если объявление `x` перемещается за пределы цикла:</span><span class="sxs-lookup"><span data-stu-id="04edb-2464">However, when the declaration of `x` is moved outside the loop:</span></span>
```csharp
static D[] F() {
    D[] result = new D[3];
    int x;
    for (int i = 0; i < 3; i++) {
        x = i * 2 + 1;
        result[i] = () => { Console.WriteLine(x); };
    }
    return result;
}
```
<span data-ttu-id="04edb-2465">Выводится следующий результат:</span><span class="sxs-lookup"><span data-stu-id="04edb-2465">the output is:</span></span>
```
5
5
5
```

<span data-ttu-id="04edb-2466">Цикл for объявляется переменная итерации, что сама переменная считается объявляться вне цикла.</span><span class="sxs-lookup"><span data-stu-id="04edb-2466">If a for-loop declares an iteration variable, that variable itself is considered to be declared outside of the loop.</span></span> <span data-ttu-id="04edb-2467">Таким образом Если изменить пример, чтобы записать и сама переменная итерации:</span><span class="sxs-lookup"><span data-stu-id="04edb-2467">Thus, if the example is changed to capture the iteration variable itself:</span></span>

```csharp
static D[] F() {
    D[] result = new D[3];
    for (int i = 0; i < 3; i++) {
        result[i] = () => { Console.WriteLine(i); };
    }
    return result;
}
```
<span data-ttu-id="04edb-2468">регистрируются только один экземпляр переменной итерации, в результате получается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2468">only one instance of the iteration variable is captured, which produces the output:</span></span>
```
3
3
3
```

<span data-ttu-id="04edb-2469">Делегаты анонимных функций могут совместно использовать некоторые захваченные переменные еще нет отдельные экземпляры других возможна.</span><span class="sxs-lookup"><span data-stu-id="04edb-2469">It is possible for anonymous function delegates to share some captured variables yet have separate instances of others.</span></span> <span data-ttu-id="04edb-2470">Например если `F` изменяется на</span><span class="sxs-lookup"><span data-stu-id="04edb-2470">For example, if `F` is changed to</span></span>
```csharp
static D[] F() {
    D[] result = new D[3];
    int x = 0;
    for (int i = 0; i < 3; i++) {
        int y = 0;
        result[i] = () => { Console.WriteLine("{0} {1}", ++x, ++y); };
    }
    return result;
}
```
<span data-ttu-id="04edb-2471">три делегаты записи тот же экземпляр `x` но отдельным экземплярам `y`, и выходные данные:</span><span class="sxs-lookup"><span data-stu-id="04edb-2471">the three delegates capture the same instance of `x` but separate instances of `y`, and the output is:</span></span>
```
1 1
2 1
3 1
```

<span data-ttu-id="04edb-2472">Отдельные анонимные функции могут захватывать один экземпляр внешней переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-2472">Separate anonymous functions can capture the same instance of an outer variable.</span></span> <span data-ttu-id="04edb-2473">В данном примере:</span><span class="sxs-lookup"><span data-stu-id="04edb-2473">In the example:</span></span>
```csharp
using System;

delegate void Setter(int value);

delegate int Getter();

class Test
{
    static void Main() {
        int x = 0;
        Setter s = (int value) => { x = value; };
        Getter g = () => { return x; };
        s(5);
        Console.WriteLine(g());
        s(10);
        Console.WriteLine(g());
    }
}
```
<span data-ttu-id="04edb-2474">две анонимные функции захватывают один экземпляр локальной переменной `x`, и таким образом «связи» через эту переменную.</span><span class="sxs-lookup"><span data-stu-id="04edb-2474">the two anonymous functions capture the same instance of the local variable `x`, and they can thus "communicate" through that variable.</span></span> <span data-ttu-id="04edb-2475">Выходные данные этого примера является:</span><span class="sxs-lookup"><span data-stu-id="04edb-2475">The output of the example is:</span></span>
```
5
10
```

### <a name="evaluation-of-anonymous-function-expressions"></a><span data-ttu-id="04edb-2476">Вычисление выражения анонимных функций</span><span class="sxs-lookup"><span data-stu-id="04edb-2476">Evaluation of anonymous function expressions</span></span>

<span data-ttu-id="04edb-2477">Анонимная функция `F` всегда должен преобразовываться в тип делегата `D` или тип дерева выражения `E`, либо непосредственно, либо с помощью выполнения выражения создания делегата `new D(F)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2477">An anonymous function `F` must always be converted to a delegate type `D` or an expression tree type `E`, either directly or through the execution of a delegate creation expression `new D(F)`.</span></span> <span data-ttu-id="04edb-2478">Это преобразование определяет результат анонимной функции, как описано в разделе [преобразования анонимных функций](conversions.md#anonymous-function-conversions).</span><span class="sxs-lookup"><span data-stu-id="04edb-2478">This conversion determines the result of the anonymous function, as described in [Anonymous function conversions](conversions.md#anonymous-function-conversions).</span></span>

## <a name="query-expressions"></a><span data-ttu-id="04edb-2479">Выражения запросов</span><span class="sxs-lookup"><span data-stu-id="04edb-2479">Query expressions</span></span>

<span data-ttu-id="04edb-2480">***Выражения запросов*** предоставляют встроенные в язык синтаксис для запросов, которые аналогичны языки реляционные и иерархические запросов, таких как SQL и XQuery.</span><span class="sxs-lookup"><span data-stu-id="04edb-2480">***Query expressions*** provide a language integrated syntax for queries that is similar to relational and hierarchical query languages such as SQL and XQuery.</span></span>

```antlr
query_expression
    : from_clause query_body
    ;

from_clause
    : 'from' type? identifier 'in' expression
    ;

query_body
    : query_body_clauses? select_or_group_clause query_continuation?
    ;

query_body_clauses
    : query_body_clause
    | query_body_clauses query_body_clause
    ;

query_body_clause
    : from_clause
    | let_clause
    | where_clause
    | join_clause
    | join_into_clause
    | orderby_clause
    ;

let_clause
    : 'let' identifier '=' expression
    ;

where_clause
    : 'where' boolean_expression
    ;

join_clause
    : 'join' type? identifier 'in' expression 'on' expression 'equals' expression
    ;

join_into_clause
    : 'join' type? identifier 'in' expression 'on' expression 'equals' expression 'into' identifier
    ;

orderby_clause
    : 'orderby' orderings
    ;

orderings
    : ordering (',' ordering)*
    ;

ordering
    : expression ordering_direction?
    ;

ordering_direction
    : 'ascending'
    | 'descending'
    ;

select_or_group_clause
    : select_clause
    | group_clause
    ;

select_clause
    : 'select' expression
    ;

group_clause
    : 'group' expression 'by' expression
    ;

query_continuation
    : 'into' identifier query_body
    ;
```

<span data-ttu-id="04edb-2481">Выражение запроса начинается с `from` предложения и заканчивается либо `select` или `group` предложение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2481">A query expression begins with a `from` clause and ends with either a `select` or `group` clause.</span></span> <span data-ttu-id="04edb-2482">Начальный `from` предложение может следовать ноль или более `from`, `let`, `where`, `join` или `orderby` предложения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2482">The initial `from` clause can be followed by zero or more `from`, `let`, `where`, `join` or `orderby` clauses.</span></span> <span data-ttu-id="04edb-2483">Каждый `from` предложение является генератором Знакомство с ***переменная диапазона*** диапазоне для элементов ***последовательности***.</span><span class="sxs-lookup"><span data-stu-id="04edb-2483">Each `from` clause is a generator introducing a ***range variable*** which ranges over the elements of a ***sequence***.</span></span> <span data-ttu-id="04edb-2484">Каждый `let` предложение вводит переменную диапазона, представляющее значение, вычисляемое с помощью предыдущих переменных диапазона.</span><span class="sxs-lookup"><span data-stu-id="04edb-2484">Each `let` clause introduces a range variable representing a value computed by means of previous range variables.</span></span> <span data-ttu-id="04edb-2485">Каждый `where` выражение является фильтром для исключения элементов из результата.</span><span class="sxs-lookup"><span data-stu-id="04edb-2485">Each `where` clause is a filter that excludes items from the result.</span></span> <span data-ttu-id="04edb-2486">Каждый `join` предложение сравнивает указанные ключи исходной последовательности с ключами другой последовательности, выдавая совпадающие пары.</span><span class="sxs-lookup"><span data-stu-id="04edb-2486">Each `join` clause compares specified keys of the source sequence with keys of another sequence, yielding matching pairs.</span></span> <span data-ttu-id="04edb-2487">Каждый `orderby` предложение изменяет порядок элементов в соответствии с указанными критериями. Конечный `select` или `group` предложение указывает форму результата с точки зрения переменных диапазона.</span><span class="sxs-lookup"><span data-stu-id="04edb-2487">Each `orderby` clause reorders items according to specified criteria.The final `select` or `group` clause specifies the shape of the result in terms of the range variables.</span></span> <span data-ttu-id="04edb-2488">Наконец `into` предложение может использоваться для «splice» запросов, рассматривая результаты одного запроса как генератор в последующем запросе.</span><span class="sxs-lookup"><span data-stu-id="04edb-2488">Finally, an `into` clause can be used to "splice" queries by treating the results of one query as a generator in a subsequent query.</span></span>

### <a name="ambiguities-in-query-expressions"></a><span data-ttu-id="04edb-2489">Неоднозначность в выражениях запросов</span><span class="sxs-lookup"><span data-stu-id="04edb-2489">Ambiguities in query expressions</span></span>

<span data-ttu-id="04edb-2490">Выражения запросов содержат «контекстными ключевыми словами», т. е. идентификаторы, которые имеют особое значение в заданном контексте.</span><span class="sxs-lookup"><span data-stu-id="04edb-2490">Query expressions contain a number of "contextual keywords", i.e., identifiers that have special meaning in a given context.</span></span> <span data-ttu-id="04edb-2491">В частности это `from`, `where`, `join`, `on`, `equals`, `into`, `let`, `orderby`, `ascending`, `descending`, `select`, `group` и `by`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2491">Specifically these are `from`, `where`, `join`, `on`, `equals`, `into`, `let`, `orderby`, `ascending`, `descending`, `select`, `group` and `by`.</span></span> <span data-ttu-id="04edb-2492">Во избежание неоднозначности в выражениях запросов, из-за смешанных эти идентификаторы используются как ключевые слова или простые имена, эти идентификаторы считаются ключевые слова, при выполнении в любом месте в выражении запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2492">In order to avoid ambiguities in query expressions caused by mixed use of these identifiers as keywords or simple names, these identifiers are considered keywords when occurring anywhere within a query expression.</span></span>

<span data-ttu-id="04edb-2493">Для этой цели, выражение запроса является любое выражение, которое начинается с "`from identifier`«следуют любому маркеру, за исключением»`;`«,»`=`«или»`,`«.</span><span class="sxs-lookup"><span data-stu-id="04edb-2493">For this purpose, a query expression is any expression that starts with "`from identifier`" followed by any token except "`;`", "`=`" or "`,`".</span></span>

<span data-ttu-id="04edb-2494">Чтобы использовать эти слова в качестве идентификаторов в выражении запроса, они могут быть с префиксом "`@`" ([идентификаторы](lexical-structure.md#identifiers)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2494">In order to use these words as identifiers within a query expression, they can be prefixed with "`@`" ([Identifiers](lexical-structure.md#identifiers)).</span></span>

### <a name="query-expression-translation"></a><span data-ttu-id="04edb-2495">Преобразования выражения запроса</span><span class="sxs-lookup"><span data-stu-id="04edb-2495">Query expression translation</span></span>

<span data-ttu-id="04edb-2496">В языке C# не указывайте семантика выполнения выражения запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2496">The C# language does not specify the execution semantics of query expressions.</span></span> <span data-ttu-id="04edb-2497">Вместо этого выражения запроса преобразуются в вызовы методов, которые соответствуют *модели выражений запросов* ([шаблон выражения запроса](expressions.md#the-query-expression-pattern)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2497">Rather, query expressions are translated into invocations of methods that adhere to the *query expression pattern* ([The query expression pattern](expressions.md#the-query-expression-pattern)).</span></span> <span data-ttu-id="04edb-2498">В частности, выражения запроса преобразуются в вызовы методов с именами `Where`, `Select`, `SelectMany`, `Join`, `GroupJoin`, `OrderBy`, `OrderByDescending`, `ThenBy`, `ThenByDescending`, `GroupBy`, и `Cast`. Эти методы должны иметь определенный подписи и типы результатов, как описано в разделе [шаблон выражения запроса](expressions.md#the-query-expression-pattern).</span><span class="sxs-lookup"><span data-stu-id="04edb-2498">Specifically, query expressions are translated into invocations of methods named `Where`, `Select`, `SelectMany`, `Join`, `GroupJoin`, `OrderBy`, `OrderByDescending`, `ThenBy`, `ThenByDescending`, `GroupBy`, and `Cast`.These methods are expected to have particular signatures and result types, as described in [The query expression pattern](expressions.md#the-query-expression-pattern).</span></span> <span data-ttu-id="04edb-2499">Эти методы могут быть методами экземпляра запрашиваемого объекта или методов расширения, которые являются внешними по отношению к объекту, и они реализуют фактическое выполнение запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2499">These methods can be instance methods of the object being queried or extension methods that are external to the object, and they implement the actual execution of the query.</span></span>

<span data-ttu-id="04edb-2500">Перевод из выражения запроса на вызовы методов — это синтаксические сопоставление, которое происходит перед любой тип привязки, или разрешение перегрузки выполнено.</span><span class="sxs-lookup"><span data-stu-id="04edb-2500">The translation from query expressions to method invocations is a syntactic mapping that occurs before any type binding or overload resolution has been performed.</span></span> <span data-ttu-id="04edb-2501">Перевод обязательно является синтаксически правильным, но не обязательно создавать семантически правильный код C#.</span><span class="sxs-lookup"><span data-stu-id="04edb-2501">The translation is guaranteed to be syntactically correct, but it is not guaranteed to produce semantically correct C# code.</span></span> <span data-ttu-id="04edb-2502">Итоговый вызовы методов, обрабатываются как вызовы методов регулярных перевод выражений запросов, и это в свою очередь позволит обнаружить ошибки, например, если методы не существуют, если аргументы имеют неправильный типы или методы являются универсальными и не удается вывести тип.</span><span class="sxs-lookup"><span data-stu-id="04edb-2502">Following translation of query expressions, the resulting method invocations are processed as regular method invocations, and this may in turn uncover errors, for example if the methods do not exist, if arguments have wrong types, or if the methods are generic and type inference fails.</span></span>

<span data-ttu-id="04edb-2503">Выражение запроса обрабатывается несколько раз, пока не удается выполнить дальнейшее сокращение возможны, применяя следующие переводы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2503">A query expression is processed by repeatedly applying the following translations until no further reductions are possible.</span></span> <span data-ttu-id="04edb-2504">Переводы, перечислены в порядке приложения: в каждом разделе предполагается, что переводы в предыдущих разделах выполнено тщательное и когда исчерпан, раздел будет не позже потребуется пересмотреть в обработке одном выражении запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2504">The translations are listed in order of application: each section assumes that the translations in the preceding sections have been performed exhaustively, and once exhausted, a section will not later be revisited in the processing of the same query expression.</span></span>

<span data-ttu-id="04edb-2505">Назначение переменных диапазона не допускается в выражениях запросов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2505">Assignment to range variables is not allowed in query expressions.</span></span> <span data-ttu-id="04edb-2506">Тем не менее реализацию на C# может не всегда выполнять это ограничение, так как это иногда не возможно с помощью синтаксического преобразования схемы, представленных здесь.</span><span class="sxs-lookup"><span data-stu-id="04edb-2506">However a C# implementation is permitted to not always enforce this restriction, since this may sometimes not be possible with the syntactic translation scheme presented here.</span></span>

<span data-ttu-id="04edb-2507">При некоторых переводах вставляются переменные диапазона с прозрачного идентификаторами, обозначенное с помощью `*`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2507">Certain translations inject range variables with transparent identifiers denoted by `*`.</span></span> <span data-ttu-id="04edb-2508">Особые свойства прозрачных идентификаторов рассматриваются в разделе [прозрачного идентификаторами](expressions.md#transparent-identifiers).</span><span class="sxs-lookup"><span data-stu-id="04edb-2508">The special properties of transparent identifiers are discussed further in [Transparent identifiers](expressions.md#transparent-identifiers).</span></span>

#### <a name="select-and-groupby-clauses-with-continuations"></a><span data-ttu-id="04edb-2509">Предложения SELECT и groupby с продолжениями</span><span class="sxs-lookup"><span data-stu-id="04edb-2509">Select and groupby clauses with continuations</span></span>

<span data-ttu-id="04edb-2510">Выражение запроса с продолжением</span><span class="sxs-lookup"><span data-stu-id="04edb-2510">A query expression with a continuation</span></span>
```csharp
from ... into x ...
```
<span data-ttu-id="04edb-2511">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2511">is translated into</span></span>
```csharp
from x in ( from ... ) ...
```

<span data-ttu-id="04edb-2512">Переводы в следующих разделах предполагается, что запросы не имеют `into` продолжений.</span><span class="sxs-lookup"><span data-stu-id="04edb-2512">The translations in the following sections assume that queries have no `into` continuations.</span></span>

<span data-ttu-id="04edb-2513">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2513">The example</span></span>
```csharp
from c in customers
group c by c.Country into g
select new { Country = g.Key, CustCount = g.Count() }
```
<span data-ttu-id="04edb-2514">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2514">is translated into</span></span>
```csharp
from g in
    from c in customers
    group c by c.Country
select new { Country = g.Key, CustCount = g.Count() }
```
<span data-ttu-id="04edb-2515">Окончательный перевод, из которых —</span><span class="sxs-lookup"><span data-stu-id="04edb-2515">the final translation of which is</span></span>
```csharp
customers.
GroupBy(c => c.Country).
Select(g => new { Country = g.Key, CustCount = g.Count() })
```

#### <a name="explicit-range-variable-types"></a><span data-ttu-id="04edb-2516">Явные типы переменных диапазона</span><span class="sxs-lookup"><span data-stu-id="04edb-2516">Explicit range variable types</span></span>

<span data-ttu-id="04edb-2517">Объект `from` предложение, которая явно задает тип переменной диапазона</span><span class="sxs-lookup"><span data-stu-id="04edb-2517">A `from` clause that explicitly specifies a range variable type</span></span>
```csharp
from T x in e
```
<span data-ttu-id="04edb-2518">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2518">is translated into</span></span>
```csharp
from x in ( e ) . Cast < T > ( )
```

<span data-ttu-id="04edb-2519">Объект `join` предложение, которая явно задает тип переменной диапазона</span><span class="sxs-lookup"><span data-stu-id="04edb-2519">A `join` clause that explicitly specifies a range variable type</span></span>
```
join T x in e on k1 equals k2
```
<span data-ttu-id="04edb-2520">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2520">is translated into</span></span>
```
join x in ( e ) . Cast < T > ( ) on k1 equals k2
```

<span data-ttu-id="04edb-2521">Переводы в следующих разделах предполагается, что запросы не явные типы переменных диапазона.</span><span class="sxs-lookup"><span data-stu-id="04edb-2521">The translations in the following sections assume that queries have no explicit range variable types.</span></span>

<span data-ttu-id="04edb-2522">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2522">The example</span></span>
```csharp
from Customer c in customers
where c.City == "London"
select c
```
<span data-ttu-id="04edb-2523">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2523">is translated into</span></span>
```csharp
from c in customers.Cast<Customer>()
where c.City == "London"
select c
```
<span data-ttu-id="04edb-2524">Окончательный перевод, из которых —</span><span class="sxs-lookup"><span data-stu-id="04edb-2524">the final translation of which is</span></span>
```csharp
customers.
Cast<Customer>().
Where(c => c.City == "London")
```

<span data-ttu-id="04edb-2525">Явные типы переменных диапазона полезны для выполнения запросов к коллекциям, которые реализуют неуниверсальный `IEnumerable` интерфейс, но не универсальный `IEnumerable<T>` интерфейс.</span><span class="sxs-lookup"><span data-stu-id="04edb-2525">Explicit range variable types are useful for querying collections that implement the non-generic `IEnumerable` interface, but not the generic `IEnumerable<T>` interface.</span></span> <span data-ttu-id="04edb-2526">В приведенном выше примере это будет том случае, если `customers` имели тип `ArrayList`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2526">In the example above, this would be the case if `customers` were of type `ArrayList`.</span></span>

#### <a name="degenerate-query-expressions"></a><span data-ttu-id="04edb-2527">Выражения вырожденных запросов</span><span class="sxs-lookup"><span data-stu-id="04edb-2527">Degenerate query expressions</span></span>

<span data-ttu-id="04edb-2528">Выражение запроса формы</span><span class="sxs-lookup"><span data-stu-id="04edb-2528">A query expression of the form</span></span>
```csharp
from x in e select x
```
<span data-ttu-id="04edb-2529">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2529">is translated into</span></span>
```csharp
( e ) . Select ( x => x )
```

<span data-ttu-id="04edb-2530">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2530">The example</span></span>
```csharp
from c in customers
select c
```
<span data-ttu-id="04edb-2531">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2531">is translated into</span></span>
```csharp
customers.Select(c => c)
```

<span data-ttu-id="04edb-2532">Выражение вырожденного запроса является просто выбирает элементы источника.</span><span class="sxs-lookup"><span data-stu-id="04edb-2532">A degenerate query expression is one that trivially selects the elements of the source.</span></span> <span data-ttu-id="04edb-2533">На более позднем этапе перевода удаляет вырожденных запросов, созданных на других этапах перевода, заменив их с их источником.</span><span class="sxs-lookup"><span data-stu-id="04edb-2533">A later phase of the translation removes degenerate queries introduced by other translation steps by replacing them with their source.</span></span> <span data-ttu-id="04edb-2534">Тем не менее важно, чтобы убедиться, что результат запроса выражение никогда не является исходный объект, как это раскроет тип и идентификатор источника для запроса клиента.</span><span class="sxs-lookup"><span data-stu-id="04edb-2534">It is important however to ensure that the result of a query expression is never the source object itself, as that would reveal the type and identity of the source to the client of the query.</span></span> <span data-ttu-id="04edb-2535">Таким образом, этот шаг защищает вырожденный запросы, написанные непосредственно в исходном коде, путем явного вызова `Select` в источнике.</span><span class="sxs-lookup"><span data-stu-id="04edb-2535">Therefore this step protects degenerate queries written directly in source code by explicitly calling `Select` on the source.</span></span> <span data-ttu-id="04edb-2536">Сами объекты, реализующие `Select` и других операторов запроса, чтобы убедиться, что эти методы возвращают никогда не самого объекта источника.</span><span class="sxs-lookup"><span data-stu-id="04edb-2536">It is then up to the implementers of `Select` and other query operators to ensure that these methods never return the source object itself.</span></span>

#### <a name="from-let-where-join-and-orderby-clauses"></a><span data-ttu-id="04edb-2537">Let, where, предложения join и orderby</span><span class="sxs-lookup"><span data-stu-id="04edb-2537">From, let, where, join and orderby clauses</span></span>

<span data-ttu-id="04edb-2538">Выражение запроса с секунды `from` предложение, за которым следует `select` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2538">A query expression with a second `from` clause followed by a `select` clause</span></span>
```csharp
from x1 in e1
from x2 in e2
select v
```
<span data-ttu-id="04edb-2539">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2539">is translated into</span></span>
```csharp
( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => v )
```

<span data-ttu-id="04edb-2540">Выражение запроса с секунды `from` предложение следуют что-то отличное от `select` предложение:</span><span class="sxs-lookup"><span data-stu-id="04edb-2540">A query expression with a second `from` clause followed by something other than a `select` clause:</span></span>

```csharp
from x1 in e1
from x2 in e2
...
```
<span data-ttu-id="04edb-2541">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2541">is translated into</span></span>
```csharp
from * in ( e1 ) . SelectMany( x1 => e2 , ( x1 , x2 ) => new { x1 , x2 } )
...
```

<span data-ttu-id="04edb-2542">Выражение запроса с `let` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2542">A query expression with a `let` clause</span></span>
```csharp
from x in e
let y = f
...
```
<span data-ttu-id="04edb-2543">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2543">is translated into</span></span>
```csharp
from * in ( e ) . Select ( x => new { x , y = f } )
...
```

<span data-ttu-id="04edb-2544">Выражение запроса с `where` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2544">A query expression with a `where` clause</span></span>
```csharp
from x in e
where f
...
```
<span data-ttu-id="04edb-2545">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2545">is translated into</span></span>
```csharp
from x in ( e ) . Where ( x => f )
...
```

<span data-ttu-id="04edb-2546">Выражение запроса с `join` предложения без `into` следуют `select` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2546">A query expression with a `join` clause without an `into` followed by a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2
select v
```
<span data-ttu-id="04edb-2547">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2547">is translated into</span></span>
```csharp
( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => v )
```

<span data-ttu-id="04edb-2548">Выражение запроса с `join` предложения без `into` следуют что-то отличное от `select` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2548">A query expression with a `join` clause without an `into` followed by something other than a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2
...
```
<span data-ttu-id="04edb-2549">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2549">is translated into</span></span>
```csharp
from * in ( e1 ) . Join( e2 , x1 => k1 , x2 => k2 , ( x1 , x2 ) => new { x1 , x2 })
...
```

<span data-ttu-id="04edb-2550">Выражение запроса с `join` предложение with `into` следуют `select` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2550">A query expression with a `join` clause with an `into` followed by a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2 into g
select v
```
<span data-ttu-id="04edb-2551">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2551">is translated into</span></span>
```csharp
( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => v )
```

<span data-ttu-id="04edb-2552">Выражение запроса с `join` предложение with `into` следуют что-то отличное от `select` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2552">A query expression with a `join` clause with an `into` followed by something other than a `select` clause</span></span>
```csharp
from x1 in e1
join x2 in e2 on k1 equals k2 into g
...
```
<span data-ttu-id="04edb-2553">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2553">is translated into</span></span>
```csharp
from * in ( e1 ) . GroupJoin( e2 , x1 => k1 , x2 => k2 , ( x1 , g ) => new { x1 , g })
...
```

<span data-ttu-id="04edb-2554">Выражение запроса с `orderby` предложение</span><span class="sxs-lookup"><span data-stu-id="04edb-2554">A query expression with an `orderby` clause</span></span>
```csharp
from x in e
orderby k1 , k2 , ..., kn
...
```
<span data-ttu-id="04edb-2555">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2555">is translated into</span></span>
```csharp
from x in ( e ) . 
OrderBy ( x => k1 ) . 
ThenBy ( x => k2 ) .
... .
ThenBy ( x => kn )
...
```

<span data-ttu-id="04edb-2556">Если упорядочение предложение задает `descending` индикатором направления, как вызов `OrderByDescending` или `ThenByDescending` вместо этого создается.</span><span class="sxs-lookup"><span data-stu-id="04edb-2556">If an ordering clause specifies a `descending` direction indicator, an invocation of `OrderByDescending` or `ThenByDescending` is produced instead.</span></span>

<span data-ttu-id="04edb-2557">Следующие переводы предполагается, что не `let`, `where`, `join` или `orderby` предложения, а не более одного начального `from` предложение в каждое выражение запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2557">The following translations assume that there are no `let`, `where`, `join` or `orderby` clauses, and no more than the one initial `from` clause in each query expression.</span></span>

<span data-ttu-id="04edb-2558">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2558">The example</span></span>
```csharp
from c in customers
from o in c.Orders
select new { c.Name, o.OrderID, o.Total }
```
<span data-ttu-id="04edb-2559">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2559">is translated into</span></span>
```csharp
customers.
SelectMany(c => c.Orders,
     (c,o) => new { c.Name, o.OrderID, o.Total }
)
```

<span data-ttu-id="04edb-2560">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2560">The example</span></span>
```csharp
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```
<span data-ttu-id="04edb-2561">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2561">is translated into</span></span>
```csharp
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.OrderID, o.Total }
```
<span data-ttu-id="04edb-2562">Окончательный перевод, из которых —</span><span class="sxs-lookup"><span data-stu-id="04edb-2562">the final translation of which is</span></span>
```csharp
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.OrderID, x.o.Total })
```
<span data-ttu-id="04edb-2563">где `x` идентификатор созданный компилятором, в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2563">where `x` is a compiler generated identifier that is otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="04edb-2564">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2564">The example</span></span>
```csharp
from o in orders
let t = o.Details.Sum(d => d.UnitPrice * d.Quantity)
where t >= 1000
select new { o.OrderID, Total = t }
```
<span data-ttu-id="04edb-2565">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2565">is translated into</span></span>
```csharp
from * in orders.
    Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) })
where t >= 1000 
select new { o.OrderID, Total = t }
```
<span data-ttu-id="04edb-2566">Окончательный перевод, из которых —</span><span class="sxs-lookup"><span data-stu-id="04edb-2566">the final translation of which is</span></span>
```csharp
orders.
Select(o => new { o, t = o.Details.Sum(d => d.UnitPrice * d.Quantity) }).
Where(x => x.t >= 1000).
Select(x => new { x.o.OrderID, Total = x.t })
```
<span data-ttu-id="04edb-2567">где `x` идентификатор созданный компилятором, в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2567">where `x` is a compiler generated identifier that is otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="04edb-2568">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2568">The example</span></span>
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
select new { c.Name, o.OrderDate, o.Total }
```
<span data-ttu-id="04edb-2569">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2569">is translated into</span></span>
```csharp
customers.Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c.Name, o.OrderDate, o.Total })
```

<span data-ttu-id="04edb-2570">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2570">The example</span></span>
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID into co
let n = co.Count()
where n >= 10
select new { c.Name, OrderCount = n }
```
<span data-ttu-id="04edb-2571">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2571">is translated into</span></span>
```csharp
from * in customers.
    GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
        (c, co) => new { c, co })
let n = co.Count()
where n >= 10 
select new { c.Name, OrderCount = n }
```
<span data-ttu-id="04edb-2572">Окончательный перевод, из которых —</span><span class="sxs-lookup"><span data-stu-id="04edb-2572">the final translation of which is</span></span>
```csharp
customers.
GroupJoin(orders, c => c.CustomerID, o => o.CustomerID,
    (c, co) => new { c, co }).
Select(x => new { x, n = x.co.Count() }).
Where(y => y.n >= 10).
Select(y => new { y.x.c.Name, OrderCount = y.n)
```
<span data-ttu-id="04edb-2573">где `x` и `y` являются идентификаторы, созданные компилятором, в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2573">where `x` and `y` are compiler generated identifiers that are otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="04edb-2574">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2574">The example</span></span>
```csharp
from o in orders
orderby o.Customer.Name, o.Total descending
select o
```
<span data-ttu-id="04edb-2575">имеет конечный перевод</span><span class="sxs-lookup"><span data-stu-id="04edb-2575">has the final translation</span></span>
```csharp
orders.
OrderBy(o => o.Customer.Name).
ThenByDescending(o => o.Total)
```

#### <a name="select-clauses"></a><span data-ttu-id="04edb-2576">Выберите предложения</span><span class="sxs-lookup"><span data-stu-id="04edb-2576">Select clauses</span></span>

<span data-ttu-id="04edb-2577">Выражение запроса формы</span><span class="sxs-lookup"><span data-stu-id="04edb-2577">A query expression of the form</span></span>
```csharp
from x in e select v
```
<span data-ttu-id="04edb-2578">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2578">is translated into</span></span>
```csharp
( e ) . Select ( x => v )
```
<span data-ttu-id="04edb-2579">Кроме случаев, когда v идентификатор x, перевод — это просто</span><span class="sxs-lookup"><span data-stu-id="04edb-2579">except when v is the identifier x, the translation is simply</span></span>
```csharp
( e )
```

<span data-ttu-id="04edb-2580">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2580">For example</span></span>
```csharp
from c in customers.Where(c => c.City == "London")
select c
```
<span data-ttu-id="04edb-2581">просто преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2581">is simply translated into</span></span>
```csharp
customers.Where(c => c.City == "London")
```

#### <a name="groupby-clauses"></a><span data-ttu-id="04edb-2582">Предложения GroupBy</span><span class="sxs-lookup"><span data-stu-id="04edb-2582">Groupby clauses</span></span>

<span data-ttu-id="04edb-2583">Выражение запроса формы</span><span class="sxs-lookup"><span data-stu-id="04edb-2583">A query expression of the form</span></span>
```csharp
from x in e group v by k
```
<span data-ttu-id="04edb-2584">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2584">is translated into</span></span>
```csharp
( e ) . GroupBy ( x => k , x => v )
```
<span data-ttu-id="04edb-2585">Кроме случаев, когда v идентификатор x, преобразование является</span><span class="sxs-lookup"><span data-stu-id="04edb-2585">except when v is the identifier x, the translation is</span></span>
```csharp
( e ) . GroupBy ( x => k )
```

<span data-ttu-id="04edb-2586">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2586">The example</span></span>
```csharp
from c in customers
group c.Name by c.Country
```
<span data-ttu-id="04edb-2587">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2587">is translated into</span></span>
```csharp
customers.
GroupBy(c => c.Country, c => c.Name)
```

#### <a name="transparent-identifiers"></a><span data-ttu-id="04edb-2588">Прозрачные идентификаторы</span><span class="sxs-lookup"><span data-stu-id="04edb-2588">Transparent identifiers</span></span>

<span data-ttu-id="04edb-2589">При некоторых переводах вставляются переменные диапазона с ***прозрачного идентификаторами*** обозначается `*`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2589">Certain translations inject range variables with ***transparent identifiers*** denoted by `*`.</span></span> <span data-ttu-id="04edb-2590">Прозрачные идентификаторы не являются компонентом языка; они существуют только в качестве промежуточного шага в процессе преобразования выражения запроса.</span><span class="sxs-lookup"><span data-stu-id="04edb-2590">Transparent identifiers are not a proper language feature; they exist only as an intermediate step in the query expression translation process.</span></span>

<span data-ttu-id="04edb-2591">При переводе запроса вставляется прозрачный идентификатор, дальнейшие этапы перевода распространяют прозрачный идентификатор в анонимные функции и инициализатора анонимных объектов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2591">When a query translation injects a transparent identifier, further translation steps propagate the transparent identifier into anonymous functions and anonymous object initializers.</span></span> <span data-ttu-id="04edb-2592">В таких контекстах прозрачные идентификаторы имеют следующие особенности:</span><span class="sxs-lookup"><span data-stu-id="04edb-2592">In those contexts, transparent identifiers have the following behavior:</span></span>

*  <span data-ttu-id="04edb-2593">Когда прозрачный идентификатор как параметр в анонимную функцию, члены связанного анонимного типа автоматически находятся в области действия в теле анонимной функции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2593">When a transparent identifier occurs as a parameter in an anonymous function, the members of the associated anonymous type are automatically in scope in the body of the anonymous function.</span></span>
*  <span data-ttu-id="04edb-2594">Когда член с прозрачным идентификатором находится в области, члены этого члена находятся в области также.</span><span class="sxs-lookup"><span data-stu-id="04edb-2594">When a member with a transparent identifier is in scope, the members of that member are in scope as well.</span></span>
*  <span data-ttu-id="04edb-2595">Когда прозрачный идентификатор роли декларатора члена в инициализаторе анонимного объекта, он создает член с прозрачным идентификатором.</span><span class="sxs-lookup"><span data-stu-id="04edb-2595">When a transparent identifier occurs as a member declarator in an anonymous object initializer, it introduces a member with a transparent identifier.</span></span>
*  <span data-ttu-id="04edb-2596">В трансляции действия, описанные выше прозрачные идентификаторы всегда вводятся вместе с анонимными типами, с целью сохранить несколько переменных диапазона в качестве членов объекта.</span><span class="sxs-lookup"><span data-stu-id="04edb-2596">In the translation steps described above, transparent identifiers are always introduced together with anonymous types, with the intent of capturing multiple range variables as members of a single object.</span></span> <span data-ttu-id="04edb-2597">Реализация C# может использовать другой механизм от анонимных типов, чтобы сгруппировать несколько переменных диапазона.</span><span class="sxs-lookup"><span data-stu-id="04edb-2597">An implementation of C# is permitted to use a different mechanism than anonymous types to group together multiple range variables.</span></span> <span data-ttu-id="04edb-2598">В следующих примерах перевода предполагается, что анонимные типы используются и Показать как прозрачные идентификаторы могут быть немедленно переведены.</span><span class="sxs-lookup"><span data-stu-id="04edb-2598">The following translation examples assume that anonymous types are used, and show how transparent identifiers can be translated away.</span></span>

<span data-ttu-id="04edb-2599">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2599">The example</span></span>
```csharp
from c in customers
from o in c.Orders
orderby o.Total descending
select new { c.Name, o.Total }
```
<span data-ttu-id="04edb-2600">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2600">is translated into</span></span>
```csharp
from * in customers.
    SelectMany(c => c.Orders, (c,o) => new { c, o })
orderby o.Total descending
select new { c.Name, o.Total }
```

<span data-ttu-id="04edb-2601">еще более преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2601">which is further translated into</span></span>
```csharp
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(* => o.Total).
Select(* => new { c.Name, o.Total })
```
<span data-ttu-id="04edb-2602">что, когда удаления прозрачных идентификаторов, эквивалентно</span><span class="sxs-lookup"><span data-stu-id="04edb-2602">which, when transparent identifiers are erased, is equivalent to</span></span>
```csharp
customers.
SelectMany(c => c.Orders, (c,o) => new { c, o }).
OrderByDescending(x => x.o.Total).
Select(x => new { x.c.Name, x.o.Total })
```
<span data-ttu-id="04edb-2603">где `x` идентификатор созданный компилятором, в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2603">where `x` is a compiler generated identifier that is otherwise invisible and inaccessible.</span></span>

<span data-ttu-id="04edb-2604">Пример</span><span class="sxs-lookup"><span data-stu-id="04edb-2604">The example</span></span>
```csharp
from c in customers
join o in orders on c.CustomerID equals o.CustomerID
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
<span data-ttu-id="04edb-2605">преобразуется в</span><span class="sxs-lookup"><span data-stu-id="04edb-2605">is translated into</span></span>
```csharp
from * in customers.
    Join(orders, c => c.CustomerID, o => o.CustomerID, 
        (c, o) => new { c, o })
join d in details on o.OrderID equals d.OrderID
join p in products on d.ProductID equals p.ProductID
select new { c.Name, o.OrderDate, p.ProductName }
```
<span data-ttu-id="04edb-2606">что дальше сокращается до</span><span class="sxs-lookup"><span data-stu-id="04edb-2606">which is further reduced to</span></span>
```csharp
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID, (c, o) => new { c, o }).
Join(details, * => o.OrderID, d => d.OrderID, (*, d) => new { *, d }).
Join(products, * => d.ProductID, p => p.ProductID, (*, p) => new { *, p }).
Select(* => new { c.Name, o.OrderDate, p.ProductName })
```
<span data-ttu-id="04edb-2607">Окончательный перевод, из которых —</span><span class="sxs-lookup"><span data-stu-id="04edb-2607">the final translation of which is</span></span>
```csharp
customers.
Join(orders, c => c.CustomerID, o => o.CustomerID,
    (c, o) => new { c, o }).
Join(details, x => x.o.OrderID, d => d.OrderID,
    (x, d) => new { x, d }).
Join(products, y => y.d.ProductID, p => p.ProductID,
    (y, p) => new { y, p }).
Select(z => new { z.y.x.c.Name, z.y.x.o.OrderDate, z.p.ProductName })
```
<span data-ttu-id="04edb-2608">где `x`, `y`, и `z` являются идентификаторы, созданные компилятором, в противном случае и недоступными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2608">where `x`, `y`, and `z` are compiler generated identifiers that are otherwise invisible and inaccessible.</span></span>

### <a name="the-query-expression-pattern"></a><span data-ttu-id="04edb-2609">Шаблон выражения запроса</span><span class="sxs-lookup"><span data-stu-id="04edb-2609">The query expression pattern</span></span>

<span data-ttu-id="04edb-2610">***Модели выражений запросов*** задает шаблон методы, реализующие типы для поддержки выражений запросов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2610">The ***Query expression pattern*** establishes a pattern of methods that types can implement to support query expressions.</span></span> <span data-ttu-id="04edb-2611">Так как выражения запроса преобразуются в вызовы методов с помощью синтаксического сопоставления, типы имеют значительную гибкость в реализации модели выражений запросов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2611">Because query expressions are translated to method invocations by means of a syntactic mapping, types have considerable flexibility in how they implement the query expression pattern.</span></span> <span data-ttu-id="04edb-2612">Например методы шаблона можно реализовать как методы экземпляра или как методы расширения, так как они имеют одинаковый синтаксис вызова, и методы могут запрашивать делегаты или в деревья выражений, поскольку анонимные функции могут быть преобразованы в обоих.</span><span class="sxs-lookup"><span data-stu-id="04edb-2612">For example, the methods of the pattern can be implemented as instance methods or as extension methods because the two have the same invocation syntax, and the methods can request delegates or expression trees because anonymous functions are convertible to both.</span></span>

<span data-ttu-id="04edb-2613">Рекомендуемый формат универсального типа `C<T>` что поддерживает шаблон выражения запроса показан ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-2613">The recommended shape of a generic type `C<T>` that supports the query expression pattern is shown below.</span></span> <span data-ttu-id="04edb-2614">Универсальный тип используется, чтобы продемонстрировать правильные отношения между типами параметров и результатов, но это можно реализовать шаблон для неуниверсальных типов, а также.</span><span class="sxs-lookup"><span data-stu-id="04edb-2614">A generic type is used in order to illustrate the proper relationships between parameter and result types, but it is possible to implement the pattern for non-generic types as well.</span></span>

```csharp
delegate R Func<T1,R>(T1 arg1);

delegate R Func<T1,T2,R>(T1 arg1, T2 arg2);

class C
{
    public C<T> Cast<T>();
}

class C<T> : C
{
    public C<T> Where(Func<T,bool> predicate);

    public C<U> Select<U>(Func<T,U> selector);

    public C<V> SelectMany<U,V>(Func<T,C<U>> selector,
        Func<T,U,V> resultSelector);

    public C<V> Join<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,U,V> resultSelector);

    public C<V> GroupJoin<U,K,V>(C<U> inner, Func<T,K> outerKeySelector,
        Func<U,K> innerKeySelector, Func<T,C<U>,V> resultSelector);

    public O<T> OrderBy<K>(Func<T,K> keySelector);

    public O<T> OrderByDescending<K>(Func<T,K> keySelector);

    public C<G<K,T>> GroupBy<K>(Func<T,K> keySelector);

    public C<G<K,E>> GroupBy<K,E>(Func<T,K> keySelector,
        Func<T,E> elementSelector);
}

class O<T> : C<T>
{
    public O<T> ThenBy<K>(Func<T,K> keySelector);

    public O<T> ThenByDescending<K>(Func<T,K> keySelector);
}

class G<K,T> : C<T>
{
    public K Key { get; }
}
```

<span data-ttu-id="04edb-2615">Выше методы используют типы универсальных делегатов `Func<T1,R>` и `Func<T1,T2,R>`, но также их можно одинаково хорошо использовать другие типы дерева делегата или выражения с тем же связи в типы параметров и результата.</span><span class="sxs-lookup"><span data-stu-id="04edb-2615">The methods above use the generic delegate types `Func<T1,R>` and `Func<T1,T2,R>`, but they could equally well have used other delegate or expression tree types with the same relationships in parameter and result types.</span></span>

<span data-ttu-id="04edb-2616">Обратите внимание на рекомендуемые соотношение `C<T>` и `O<T>` гарантирует, что `ThenBy` и `ThenByDescending` методы доступны только на результат `OrderBy` или `OrderByDescending`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2616">Notice the recommended relationship between `C<T>` and `O<T>` which ensures that the `ThenBy` and `ThenByDescending` methods are available only on the result of an `OrderBy` or `OrderByDescending`.</span></span> <span data-ttu-id="04edb-2617">Также Обратите внимание на рекомендуемый результата `GroupBy` --последовательности массивов, где каждая внутренняя последовательность имеет дополнительный `Key` свойство.</span><span class="sxs-lookup"><span data-stu-id="04edb-2617">Also notice the recommended shape of the result of `GroupBy` -- a sequence of sequences, where each inner sequence has an additional `Key` property.</span></span>

<span data-ttu-id="04edb-2618">`System.Linq` Пространство имен предоставляет реализацию шаблона запроса оператор для любого типа, реализующего `System.Collections.Generic.IEnumerable<T>` интерфейс.</span><span class="sxs-lookup"><span data-stu-id="04edb-2618">The `System.Linq` namespace provides an implementation of the query operator pattern for any type that implements the `System.Collections.Generic.IEnumerable<T>` interface.</span></span>

## <a name="assignment-operators"></a><span data-ttu-id="04edb-2619">Операторы присваивания</span><span class="sxs-lookup"><span data-stu-id="04edb-2619">Assignment operators</span></span>

<span data-ttu-id="04edb-2620">Операторы присваивания назначить новое значение переменной, свойства, события или элемента индексатора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2620">The assignment operators assign a new value to a variable, a property, an event, or an indexer element.</span></span>

```antlr
assignment
    : unary_expression assignment_operator expression
    ;

assignment_operator
    : '='
    | '+='
    | '-='
    | '*='
    | '/='
    | '%='
    | '&='
    | '|='
    | '^='
    | '<<='
    | right_shift_assignment
    ;
```

<span data-ttu-id="04edb-2621">Левый операнд присваивания должен быть выражением, классифицируется как переменная, доступ к свойству, индексатору или доступ к событию.</span><span class="sxs-lookup"><span data-stu-id="04edb-2621">The left operand of an assignment must be an expression classified as a variable, a property access, an indexer access, or an event access.</span></span>

<span data-ttu-id="04edb-2622">`=` Оператор был вызван ***оператор простого присваивания***.</span><span class="sxs-lookup"><span data-stu-id="04edb-2622">The `=` operator is called the ***simple assignment operator***.</span></span> <span data-ttu-id="04edb-2623">Значение правого операнда присваивается переменной, свойством или индексатором элемент, учитывая левым операндом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2623">It assigns the value of the right operand to the variable, property, or indexer element given by the left operand.</span></span> <span data-ttu-id="04edb-2624">Левый операнд оператора простого присваивания не может быть доступ к событию (кроме случаев, описанных в [подобные полям события](classes.md#field-like-events)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2624">The left operand of the simple assignment operator may not be an event access (except as described in [Field-like events](classes.md#field-like-events)).</span></span> <span data-ttu-id="04edb-2625">Оператор простого присваивания описан в [простое присваивание](expressions.md#simple-assignment).</span><span class="sxs-lookup"><span data-stu-id="04edb-2625">The simple assignment operator is described in [Simple assignment](expressions.md#simple-assignment).</span></span>

<span data-ttu-id="04edb-2626">Операторы присваивания, отличных от `=` оператор называются ***составные операторы присваивания***.</span><span class="sxs-lookup"><span data-stu-id="04edb-2626">The assignment operators other than the `=` operator are called the ***compound assignment operators***.</span></span> <span data-ttu-id="04edb-2627">Эти операторы выполняют указанную операцию с двумя операндами и назначьте результирующее значение переменной, свойством или индексатором элемент, учитывая левым операндом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2627">These operators perform the indicated operation on the two operands, and then assign the resulting value to the variable, property, or indexer element given by the left operand.</span></span> <span data-ttu-id="04edb-2628">Составные операторы присваивания, описаны в [Составное присваивание](expressions.md#compound-assignment).</span><span class="sxs-lookup"><span data-stu-id="04edb-2628">The compound assignment operators are described in [Compound assignment](expressions.md#compound-assignment).</span></span>

<span data-ttu-id="04edb-2629">`+=` И `-=` операторы с выражением доступа события как левый операнд называются *операторы присваивания событий*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2629">The `+=` and `-=` operators with an event access expression as the left operand are called the *event assignment operators*.</span></span> <span data-ttu-id="04edb-2630">Ни один другой оператор присваивания допустим для доступа к событию в качестве левого операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2630">No other assignment operator is valid with an event access as the left operand.</span></span> <span data-ttu-id="04edb-2631">Операторы присваивания событий описаны в [назначения события](expressions.md#event-assignment).</span><span class="sxs-lookup"><span data-stu-id="04edb-2631">The event assignment operators are described in [Event assignment](expressions.md#event-assignment).</span></span>

<span data-ttu-id="04edb-2632">Операторы присваивания имеют правую ассоциативность, это означает, что операции группируются слева направо.</span><span class="sxs-lookup"><span data-stu-id="04edb-2632">The assignment operators are right-associative, meaning that operations are grouped from right to left.</span></span> <span data-ttu-id="04edb-2633">Например, выражение в форме `a = b = c` вычисляется как `a = (b = c)`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2633">For example, an expression of the form `a = b = c` is evaluated as `a = (b = c)`.</span></span>

### <a name="simple-assignment"></a><span data-ttu-id="04edb-2634">Простое присваивание</span><span class="sxs-lookup"><span data-stu-id="04edb-2634">Simple assignment</span></span>

<span data-ttu-id="04edb-2635">`=` Оператор был вызван оператор простого присваивания.</span><span class="sxs-lookup"><span data-stu-id="04edb-2635">The `=` operator is called the simple assignment operator.</span></span>

<span data-ttu-id="04edb-2636">Если левый операнд выражения простого присваивания имеет форму `E.P` или `E[Ei]` где `E` имеет тип времени компиляции `dynamic`, а затем назначения является динамическим ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2636">If the left operand of a simple assignment is of the form `E.P` or `E[Ei]` where `E` has the compile-time type `dynamic`, then the assignment is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2637">В данном случае является типов во время компиляции выражения присваивания `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, исходя из типа времени выполнения `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2637">In this case the compile-time type of the assignment expression is `dynamic`, and the resolution described below will take place at run-time based on the run-time type of `E`.</span></span>

<span data-ttu-id="04edb-2638">При простом присваивании правый операнд должен быть выражением, который может быть неявно преобразован в тип левого операнда.</span><span class="sxs-lookup"><span data-stu-id="04edb-2638">In a simple assignment, the right operand must be an expression that is implicitly convertible to the type of the left operand.</span></span> <span data-ttu-id="04edb-2639">Операции значение правого операнда присваивается переменной, свойством или индексатором элемент, учитывая левым операндом.</span><span class="sxs-lookup"><span data-stu-id="04edb-2639">The operation assigns the value of the right operand to the variable, property, or indexer element given by the left operand.</span></span>

<span data-ttu-id="04edb-2640">Результат выражения простого присваивания имеет значение, присваиваемое левый операнд.</span><span class="sxs-lookup"><span data-stu-id="04edb-2640">The result of a simple assignment expression is the value assigned to the left operand.</span></span> <span data-ttu-id="04edb-2641">Результат имеет тот же тип, что и левый операнд и всегда классифицируется как значение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2641">The result has the same type as the left operand and is always classified as a value.</span></span>

<span data-ttu-id="04edb-2642">Если левый операнд является обращение к свойство или индексатор, свойство или индексатор должны `set` метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-2642">If the left operand is a property or indexer access, the property or indexer must have a `set` accessor.</span></span> <span data-ttu-id="04edb-2643">Если это не так, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2643">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-2644">Во время выполнения обработки простого присваивания вида `x = y` состоит из следующих действий:</span><span class="sxs-lookup"><span data-stu-id="04edb-2644">The run-time processing of a simple assignment of the form `x = y` consists of the following steps:</span></span>

*  <span data-ttu-id="04edb-2645">Если `x` классифицируется как переменная:</span><span class="sxs-lookup"><span data-stu-id="04edb-2645">If `x` is classified as a variable:</span></span>
   * <span data-ttu-id="04edb-2646">`x` вычисляется для создания переменной.</span><span class="sxs-lookup"><span data-stu-id="04edb-2646">`x` is evaluated to produce the variable.</span></span>
   * <span data-ttu-id="04edb-2647">`y` вычисляется и, при необходимости, преобразуется в тип `x` через неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2647">`y` is evaluated and, if required, converted to the type of `x` through an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>
   * <span data-ttu-id="04edb-2648">Если переменная, представленная `x` элементом массива является *reference_type*, проводится проверка во время выполнения, чтобы убедиться, что значение, вычисленное для `y` совместима с экземпляр массива, из которых `x` — элемент.</span><span class="sxs-lookup"><span data-stu-id="04edb-2648">If the variable given by `x` is an array element of a *reference_type*, a run-time check is performed to ensure that the value computed for `y` is compatible with the array instance of which `x` is an element.</span></span> <span data-ttu-id="04edb-2649">Проверка завершится успешно, если `y` — `null`, или если и неявное ссылочное преобразование ([неявные преобразования ссылочных типов](conversions.md#implicit-reference-conversions)) из фактический тип экземпляра, существует `y` к фактическим типом элемента экземпляр массива, содержащего `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2649">The check succeeds if `y` is `null`, or if an implicit reference conversion ([Implicit reference conversions](conversions.md#implicit-reference-conversions)) exists from the actual type of the instance referenced by `y` to the actual element type of the array instance containing `x`.</span></span> <span data-ttu-id="04edb-2650">В противном случае возникает исключение `System.ArrayTypeMismatchException`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2650">Otherwise, a `System.ArrayTypeMismatchException` is thrown.</span></span>
   * <span data-ttu-id="04edb-2651">Значение, являющееся результатом вычисления и преобразования `y` хранится в расположении, указанном вычисления `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2651">The value resulting from the evaluation and conversion of `y` is stored into the location given by the evaluation of `x`.</span></span>
*  <span data-ttu-id="04edb-2652">Если `x` классифицируется как свойство или индексатор доступа:</span><span class="sxs-lookup"><span data-stu-id="04edb-2652">If `x` is classified as a property or indexer access:</span></span>
   * <span data-ttu-id="04edb-2653">Выражение экземпляра (если `x` не `static`) и список аргументов (если `x` имеет доступ к индексатору) связанные с `x` оцениваются, и полученные результаты используются в последующих `set` вызов метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-2653">The instance expression (if `x` is not `static`) and the argument list (if `x` is an indexer access) associated with `x` are evaluated, and the results are used in the subsequent `set` accessor invocation.</span></span>
   * <span data-ttu-id="04edb-2654">`y` вычисляется и, при необходимости, преобразуется в тип `x` через неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2654">`y` is evaluated and, if required, converted to the type of `x` through an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>
   * <span data-ttu-id="04edb-2655">`set` Метод доступа `x` вызывается со значением, вычисленным для `y` как его `value` аргумент.</span><span class="sxs-lookup"><span data-stu-id="04edb-2655">The `set` accessor of `x` is invoked with the value computed for `y` as its `value` argument.</span></span>

<span data-ttu-id="04edb-2656">Правила совместного расхождения массива ([ковариацией](arrays.md#array-covariance)) разрешает значение типа массива `A[]` чтобы ссылаться на экземпляр типа массива `B[]`, если существует неявное преобразование ссылок из `B` для `A`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2656">The array co-variance rules ([Array covariance](arrays.md#array-covariance)) permit a value of an array type `A[]` to be a reference to an instance of an array type `B[]`, provided an implicit reference conversion exists from `B` to `A`.</span></span> <span data-ttu-id="04edb-2657">Из-за этих правил назначения на элемент массива из *reference_type* требует проверки во время выполнения, чтобы убедиться, что значения, присваиваемого совместима с экземпляром массива.</span><span class="sxs-lookup"><span data-stu-id="04edb-2657">Because of these rules, assignment to an array element of a *reference_type* requires a run-time check to ensure that the value being assigned is compatible with the array instance.</span></span> <span data-ttu-id="04edb-2658">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2658">In the example</span></span>
```csharp
string[] sa = new string[10];
object[] oa = sa;

oa[0] = null;               // Ok
oa[1] = "Hello";            // Ok
oa[2] = new ArrayList();    // ArrayTypeMismatchException
```
<span data-ttu-id="04edb-2659">Последнее присваивание вызывает `System.ArrayTypeMismatchException` исключение, так как экземпляр `ArrayList` не могут храниться в элементе `string[]`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2659">the last assignment causes a `System.ArrayTypeMismatchException` to be thrown because an instance of `ArrayList` cannot be stored in an element of a `string[]`.</span></span>

<span data-ttu-id="04edb-2660">Если свойство или индексатор, объявленный в *struct_type* является целевым объектом назначения, выражение экземпляра, связанное со свойством или доступа к индексатору должно быть классифицировано как переменную.</span><span class="sxs-lookup"><span data-stu-id="04edb-2660">When a property or indexer declared in a *struct_type* is the target of an assignment, the instance expression associated with the property or indexer access must be classified as a variable.</span></span> <span data-ttu-id="04edb-2661">Если экземпляр выражение классифицируется как значение, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2661">If the instance expression is classified as a value, a binding-time error occurs.</span></span> <span data-ttu-id="04edb-2662">Из-за [доступ к членам](expressions.md#member-access), то же правило также применяется к полям.</span><span class="sxs-lookup"><span data-stu-id="04edb-2662">Because of [Member access](expressions.md#member-access), the same rule also applies to fields.</span></span>

<span data-ttu-id="04edb-2663">В объявлениях:</span><span class="sxs-lookup"><span data-stu-id="04edb-2663">Given the declarations:</span></span>
```csharp
struct Point
{
    int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int X {
        get { return x; }
        set { x = value; }
    }

    public int Y {
        get { return y; }
        set { y = value; }
    }
}

struct Rectangle
{
    Point a, b;

    public Rectangle(Point a, Point b) {
        this.a = a;
        this.b = b;
    }

    public Point A {
        get { return a; }
        set { a = value; }
    }

    public Point B {
        get { return b; }
        set { b = value; }
    }
}
```
<span data-ttu-id="04edb-2664">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2664">in the example</span></span>
```csharp
Point p = new Point();
p.X = 100;
p.Y = 100;
Rectangle r = new Rectangle();
r.A = new Point(10, 10);
r.B = p;
```
<span data-ttu-id="04edb-2665">назначения, которые `p.X`, `p.Y`, `r.A`, и `r.B` разрешены, так как `p` и `r` являются переменными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2665">the assignments to `p.X`, `p.Y`, `r.A`, and `r.B` are permitted because `p` and `r` are variables.</span></span> <span data-ttu-id="04edb-2666">Тем не менее в примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2666">However, in the example</span></span>
```csharp
Rectangle r = new Rectangle();
r.A.X = 10;
r.A.Y = 10;
r.B.X = 100;
r.B.Y = 100;
```
<span data-ttu-id="04edb-2667">назначения будут недопустимы, так как `r.A` и `r.B` не являются переменными.</span><span class="sxs-lookup"><span data-stu-id="04edb-2667">the assignments are all invalid, since `r.A` and `r.B` are not variables.</span></span>

### <a name="compound-assignment"></a><span data-ttu-id="04edb-2668">Составное присваивание</span><span class="sxs-lookup"><span data-stu-id="04edb-2668">Compound assignment</span></span>

<span data-ttu-id="04edb-2669">Если левый операнд составного оператора присваивания имеет форму `E.P` или `E[Ei]` где `E` имеет тип времени компиляции `dynamic`, а затем назначения является динамическим ([динамической привязки](expressions.md#dynamic-binding)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2669">If the left operand of a compound assignment is of the form `E.P` or `E[Ei]` where `E` has the compile-time type `dynamic`, then the assignment is dynamically bound ([Dynamic binding](expressions.md#dynamic-binding)).</span></span> <span data-ttu-id="04edb-2670">В данном случае является типов во время компиляции выражения присваивания `dynamic`, а разрешение, приведенное ниже будет иметь место во время выполнения, исходя из типа времени выполнения `E`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2670">In this case the compile-time type of the assignment expression is `dynamic`, and the resolution described below will take place at run-time based on the run-time type of `E`.</span></span>

<span data-ttu-id="04edb-2671">Операции формы `x op= y` обрабатывается путем применения бинарного оператора перегрузках ([разрешить перегрузку бинарного оператора](expressions.md#binary-operator-overload-resolution)) как если бы операция была `x op y`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2671">An operation of the form `x op= y` is processed by applying binary operator overload resolution ([Binary operator overload resolution](expressions.md#binary-operator-overload-resolution)) as if the operation was written `x op y`.</span></span> <span data-ttu-id="04edb-2672">Затем,</span><span class="sxs-lookup"><span data-stu-id="04edb-2672">Then,</span></span>

*  <span data-ttu-id="04edb-2673">Если тип возвращаемого значения выбранного оператора неявно преобразуется в тип `x`, операция вычисляется как `x = x op y`, за исключением того, что `x` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-2673">If the return type of the selected operator is implicitly convertible to the type of `x`, the operation is evaluated as `x = x op y`, except that `x` is evaluated only once.</span></span>
*  <span data-ttu-id="04edb-2674">В противном случае, если выбранный оператор является определенного оператора, если тип возвращаемого значения выбранного оператора явно преобразуется в тип `x`и если `y` неявно преобразуется в тип `x` или оператор оператор, сдвига, то операция вычисляется как `x = (T)(x op y)`, где `T` — это тип `x`, за исключением того, что `x` вычисляется только один раз.</span><span class="sxs-lookup"><span data-stu-id="04edb-2674">Otherwise, if the selected operator is a predefined operator, if the return type of the selected operator is explicitly convertible to the type of `x`, and if `y` is implicitly convertible to the type of `x` or the operator is a shift operator, then the operation is evaluated as `x = (T)(x op y)`, where `T` is the type of `x`, except that `x` is evaluated only once.</span></span>
*  <span data-ttu-id="04edb-2675">В противном случае составного присваивания является недопустимым, и возникает ошибка во время привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2675">Otherwise, the compound assignment is invalid, and a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-2676">Термин «вычисляется только один раз» означает, что при вычислении `x op y`, результаты все составные выражения `x` временно сохраняются и повторно при выполнении назначения `x`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2676">The term "evaluated only once" means that in the evaluation of `x op y`, the results of any constituent expressions of `x` are temporarily saved and then reused when performing the assignment to `x`.</span></span> <span data-ttu-id="04edb-2677">Например, в назначении `A()[B()] += C()`, где `A` — это метод, возвращающий `int[]`, и `B` и `C` являются методами, возвращающими `int`, эти методы вызываются только один раз, в том порядке, `A`, `B`, `C`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2677">For example, in the assignment `A()[B()] += C()`, where `A` is a method returning `int[]`, and `B` and `C` are methods returning `int`, the methods are invoked only once, in the order `A`, `B`, `C`.</span></span>

<span data-ttu-id="04edb-2678">Если левый операнд составного оператора присваивания доступ к свойству или индексатору, свойство или индексатор должны иметь `get` метода доступа и `set` метода доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-2678">When the left operand of a compound assignment is a property access or indexer access, the property or indexer must have both a `get` accessor and a `set` accessor.</span></span> <span data-ttu-id="04edb-2679">Если это не так, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2679">If this is not the case, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-2680">Второе правило выше разрешает `x op= y` для оценки в качестве `x = (T)(x op y)` в определенных контекстах.</span><span class="sxs-lookup"><span data-stu-id="04edb-2680">The second rule above permits `x op= y` to be evaluated as `x = (T)(x op y)` in certain contexts.</span></span> <span data-ttu-id="04edb-2681">Правило существует, таким образом, что стандартные операторы можно использовать как составные операторы, если левый операнд имеет тип `sbyte`, `byte`, `short`, `ushort`, или `char`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2681">The rule exists such that the predefined operators can be used as compound operators when the left operand is of type `sbyte`, `byte`, `short`, `ushort`, or `char`.</span></span> <span data-ttu-id="04edb-2682">Даже если оба аргумента имеют один из таких типов, стандартные операторы дают результат типа `int`, как описано в разделе [Числовое расширение бинарных операторов](expressions.md#binary-numeric-promotions).</span><span class="sxs-lookup"><span data-stu-id="04edb-2682">Even when both arguments are of one of those types, the predefined operators produce a result of type `int`, as described in [Binary numeric promotions](expressions.md#binary-numeric-promotions).</span></span> <span data-ttu-id="04edb-2683">Таким образом без приведения не было бы невозможно присвоить результат левому операнду.</span><span class="sxs-lookup"><span data-stu-id="04edb-2683">Thus, without a cast it would not be possible to assign the result to the left operand.</span></span>

<span data-ttu-id="04edb-2684">Интуитивно понятный правила для стандартных операторов действует так просто, `x op= y` разрешается, если оба объекта `x op y` и `x = y` разрешены.</span><span class="sxs-lookup"><span data-stu-id="04edb-2684">The intuitive effect of the rule for predefined operators is simply that `x op= y` is permitted if both of `x op y` and `x = y` are permitted.</span></span> <span data-ttu-id="04edb-2685">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2685">In the example</span></span>
```csharp
byte b = 0;
char ch = '\0';
int i = 0;

b += 1;             // Ok
b += 1000;          // Error, b = 1000 not permitted
b += i;             // Error, b = i not permitted
b += (byte)i;       // Ok

ch += 1;            // Error, ch = 1 not permitted
ch += (char)1;      // Ok
```
<span data-ttu-id="04edb-2686">интуитивно понятный для каждой ошибки связано с тем что соответствующее простое присваивание также было бы ошибку.</span><span class="sxs-lookup"><span data-stu-id="04edb-2686">the intuitive reason for each error is that a corresponding simple assignment would also have been an error.</span></span>

<span data-ttu-id="04edb-2687">Это также означает, что составной операции присваивания поддерживают ликвидированный операций.</span><span class="sxs-lookup"><span data-stu-id="04edb-2687">This also means that compound assignment operations support lifted operations.</span></span> <span data-ttu-id="04edb-2688">В примере</span><span class="sxs-lookup"><span data-stu-id="04edb-2688">In the example</span></span>
```csharp
int? i = 0;
i += 1;             // Ok
```
<span data-ttu-id="04edb-2689">оператор ликвидированный `+(int?,int?)` используется.</span><span class="sxs-lookup"><span data-stu-id="04edb-2689">the lifted operator `+(int?,int?)` is used.</span></span>

### <a name="event-assignment"></a><span data-ttu-id="04edb-2690">Назначение событий</span><span class="sxs-lookup"><span data-stu-id="04edb-2690">Event assignment</span></span>

<span data-ttu-id="04edb-2691">Если левый операнд `+=` или `-=` оператор классифицируется как доступ к событию, то выражение вычисляется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="04edb-2691">If the left operand of a `+=` or `-=` operator is classified as an event access, then the expression is evaluated as follows:</span></span>

*  <span data-ttu-id="04edb-2692">Экземпляр, если таковые имеются, доступа к событию выражение.</span><span class="sxs-lookup"><span data-stu-id="04edb-2692">The instance expression, if any, of the event access is evaluated.</span></span>
*  <span data-ttu-id="04edb-2693">Правый операнд `+=` или `-=` оператор вычисляется и, при необходимости, преобразуется в тип левого операнда через неявное преобразование ([неявные преобразования](conversions.md#implicit-conversions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2693">The right operand of the `+=` or `-=` operator is evaluated, and, if required, converted to the type of the left operand through an implicit conversion ([Implicit conversions](conversions.md#implicit-conversions)).</span></span>
*  <span data-ttu-id="04edb-2694">Вызывается метод доступа события, события, со списком аргументов, состоящая из правого операнда, после оценки и, при необходимости преобразования.</span><span class="sxs-lookup"><span data-stu-id="04edb-2694">An event accessor of the event is invoked, with argument list consisting of the right operand, after evaluation and, if necessary, conversion.</span></span> <span data-ttu-id="04edb-2695">Если оператор был `+=`, `add` вызывается метод доступа; Если оператор был `-=`, `remove` вызывается метод доступа.</span><span class="sxs-lookup"><span data-stu-id="04edb-2695">If the operator was `+=`, the `add` accessor is invoked; if the operator was `-=`, the `remove` accessor is invoked.</span></span>

<span data-ttu-id="04edb-2696">Выражение присваивания события не использовать оператор yield.</span><span class="sxs-lookup"><span data-stu-id="04edb-2696">An event assignment expression does not yield a value.</span></span> <span data-ttu-id="04edb-2697">Таким образом, выражение присваивания события допустимо только в контексте *statement_expression* ([операторы выражений](statements.md#expression-statements)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2697">Thus, an event assignment expression is valid only in the context of a *statement_expression* ([Expression statements](statements.md#expression-statements)).</span></span>

## <a name="expression"></a><span data-ttu-id="04edb-2698">Выражение</span><span class="sxs-lookup"><span data-stu-id="04edb-2698">Expression</span></span>

<span data-ttu-id="04edb-2699">*Выражение* либо *non_assignment_expression* или *назначения*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2699">An *expression* is either a *non_assignment_expression* or an *assignment*.</span></span>

```antlr
expression
    : non_assignment_expression
    | assignment
    ;

non_assignment_expression
    : conditional_expression
    | lambda_expression
    | query_expression
    ;
```

## <a name="constant-expressions"></a><span data-ttu-id="04edb-2700">Константные выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-2700">Constant expressions</span></span>

<span data-ttu-id="04edb-2701">Объект *constant_expression* выражение, которое можно полностью вычислить во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2701">A *constant_expression* is an expression that can be fully evaluated at compile-time.</span></span>

```antlr
constant_expression
    : expression
    ;
```

<span data-ttu-id="04edb-2702">Константное выражение должно быть `null` литерал или значение с одним из следующих типов: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char` , `float`, `double`, `decimal`, `bool`, `object`, `string`, или любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-2702">A constant expression must be the `null` literal or a value with one of  the following types: `sbyte`, `byte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `char`, `float`, `double`, `decimal`, `bool`, `object`, `string`, or any enumeration type.</span></span> <span data-ttu-id="04edb-2703">В константных выражениях допустимы только следующие конструкции:</span><span class="sxs-lookup"><span data-stu-id="04edb-2703">Only the following constructs are permitted in constant expressions:</span></span>

*  <span data-ttu-id="04edb-2704">Литералы (включая `null` литерал).</span><span class="sxs-lookup"><span data-stu-id="04edb-2704">Literals (including the `null` literal).</span></span>
*  <span data-ttu-id="04edb-2705">Ссылки на `const` члены класса и структуры типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2705">References to `const` members of class and struct types.</span></span>
*  <span data-ttu-id="04edb-2706">Ссылки на члены типов перечисления.</span><span class="sxs-lookup"><span data-stu-id="04edb-2706">References to members of enumeration types.</span></span>
*  <span data-ttu-id="04edb-2707">Ссылки на `const` параметры или локальные переменные</span><span class="sxs-lookup"><span data-stu-id="04edb-2707">References to `const` parameters or local variables</span></span>
*  <span data-ttu-id="04edb-2708">Вложенные выражения в скобках, которые сами являются константными выражениями.</span><span class="sxs-lookup"><span data-stu-id="04edb-2708">Parenthesized sub-expressions, which are themselves constant expressions.</span></span>
*  <span data-ttu-id="04edb-2709">Выражения приведения, предоставленный тип объекта является одним из перечисленных выше типов.</span><span class="sxs-lookup"><span data-stu-id="04edb-2709">Cast expressions, provided the target type is one of the types listed above.</span></span>
*  <span data-ttu-id="04edb-2710">`checked` и `unchecked` выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-2710">`checked` and `unchecked` expressions</span></span>
*  <span data-ttu-id="04edb-2711">Выражения значения по умолчанию</span><span class="sxs-lookup"><span data-stu-id="04edb-2711">Default value expressions</span></span>
*  <span data-ttu-id="04edb-2712">Выражения Nameof</span><span class="sxs-lookup"><span data-stu-id="04edb-2712">Nameof expressions</span></span>
*  <span data-ttu-id="04edb-2713">Предопределенный `+`, `-`, `!`, и `~` унарные операторы.</span><span class="sxs-lookup"><span data-stu-id="04edb-2713">The predefined `+`, `-`, `!`, and `~` unary operators.</span></span>
*  <span data-ttu-id="04edb-2714">Предопределенный `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `&`, `|`, `^`, `&&`, `||`, `==`, `!=`, `<`, `>`, `<=`, и `>=` бинарные операторы, предоставляемые каждый операнд имеет тип, перечисленных выше.</span><span class="sxs-lookup"><span data-stu-id="04edb-2714">The predefined `+`, `-`, `*`, `/`, `%`, `<<`, `>>`, `&`, `|`, `^`, `&&`, `||`, `==`, `!=`, `<`, `>`, `<=`, and `>=` binary operators, provided each operand is of a type listed above.</span></span>
*  <span data-ttu-id="04edb-2715">`?:` Условного оператора.</span><span class="sxs-lookup"><span data-stu-id="04edb-2715">The `?:` conditional operator.</span></span>

<span data-ttu-id="04edb-2716">В константных выражениях допустимы следующие преобразования:</span><span class="sxs-lookup"><span data-stu-id="04edb-2716">The following conversions are permitted in constant expressions:</span></span>

*  <span data-ttu-id="04edb-2717">Преобразования идентификатора</span><span class="sxs-lookup"><span data-stu-id="04edb-2717">Identity conversions</span></span>
*  <span data-ttu-id="04edb-2718">Числовые преобразования</span><span class="sxs-lookup"><span data-stu-id="04edb-2718">Numeric conversions</span></span>
*  <span data-ttu-id="04edb-2719">Преобразование перечисления</span><span class="sxs-lookup"><span data-stu-id="04edb-2719">Enumeration conversions</span></span>
*  <span data-ttu-id="04edb-2720">Константное выражение преобразования</span><span class="sxs-lookup"><span data-stu-id="04edb-2720">Constant expression conversions</span></span>
*  <span data-ttu-id="04edb-2721">Явные и неявные преобразования ссылочных типов, указано, что источник преобразования является константным выражением, результатом которого является значение null.</span><span class="sxs-lookup"><span data-stu-id="04edb-2721">Implicit and explicit reference conversions, provided that the source of the conversions is a constant expression that evaluates to the null value.</span></span>

<span data-ttu-id="04edb-2722">Другие преобразования, включая упаковки-преобразования, распаковки-преобразования и неявные преобразования ссылочных типов значений, отличных от null не разрешены в константных выражениях.</span><span class="sxs-lookup"><span data-stu-id="04edb-2722">Other conversions including boxing, unboxing and implicit reference conversions of non-null values are not permitted in constant expressions.</span></span> <span data-ttu-id="04edb-2723">Пример:</span><span class="sxs-lookup"><span data-stu-id="04edb-2723">For example:</span></span>
```csharp
class C {
    const object i = 5;         // error: boxing conversion not permitted
    const object str = "hello"; // error: implicit reference conversion
}
```
<span data-ttu-id="04edb-2724">Инициализация i является ошибкой, поскольку необходима упаковка-преобразование.</span><span class="sxs-lookup"><span data-stu-id="04edb-2724">the initialization of i is an error because a boxing conversion is required.</span></span> <span data-ttu-id="04edb-2725">Инициализация str является ошибкой, так как требуется и неявное ссылочное преобразование из значения, отличное от null.</span><span class="sxs-lookup"><span data-stu-id="04edb-2725">The initialization of str is an error because an implicit reference conversion from a non-null value is required.</span></span>

<span data-ttu-id="04edb-2726">Если выражение соответствует требованиям, перечисленным выше, выражение вычисляется во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2726">Whenever an expression fulfills the requirements listed above, the expression is evaluated at compile-time.</span></span> <span data-ttu-id="04edb-2727">Это справедливо, даже если выражение вложенного выражения содержит конструкции Неконстантные выражения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2727">This is true even if the expression is a sub-expression of a larger expression that contains non-constant constructs.</span></span>

<span data-ttu-id="04edb-2728">Вычисление во время компиляции постоянных выражений использует те же правила в качестве времени выполнения вычисления Неконстантные выражения, за исключением того, что где возвращал исключение времени выполнения вычисления исключение, вычисление во время компиляции вызовет ошибку компиляции возникает.</span><span class="sxs-lookup"><span data-stu-id="04edb-2728">The compile-time evaluation of constant expressions uses the same rules as run-time evaluation of non-constant expressions, except that where run-time evaluation would have thrown an exception, compile-time evaluation causes a compile-time error to occur.</span></span>

<span data-ttu-id="04edb-2729">Если константное выражение явным образом помещается в `unchecked` контекста, переполнения, возникающие в целочисленных арифметических операций и преобразований во время компиляции вычисления выражения всегда вызывать ошибки времени компиляции ([Константные выражения](expressions.md#constant-expressions)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2729">Unless a constant expression is explicitly placed in an `unchecked` context, overflows that occur in integral-type arithmetic operations and conversions during the compile-time evaluation of the expression always cause compile-time errors ([Constant expressions](expressions.md#constant-expressions)).</span></span>

<span data-ttu-id="04edb-2730">Константные выражения находятся в контекстах, перечисленных ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-2730">Constant expressions occur in the contexts listed below.</span></span> <span data-ttu-id="04edb-2731">В таких контекстах ошибка времени компиляции возникает, если выражение не удается полностью вычислить во время компиляции.</span><span class="sxs-lookup"><span data-stu-id="04edb-2731">In these contexts, a compile-time error occurs if an expression cannot be fully evaluated at compile-time.</span></span>

*  <span data-ttu-id="04edb-2732">Объявления констант ([константы](classes.md#constants)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2732">Constant declarations ([Constants](classes.md#constants)).</span></span>
*  <span data-ttu-id="04edb-2733">Объявления членов перечисления ([члены перечисления](enums.md#enum-members)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2733">Enumeration member declarations ([Enum members](enums.md#enum-members)).</span></span>
*  <span data-ttu-id="04edb-2734">Аргументы списков формальных параметров по умолчанию ([параметры метода](classes.md#method-parameters))</span><span class="sxs-lookup"><span data-stu-id="04edb-2734">Default arguments of formal parameter lists ([Method parameters](classes.md#method-parameters))</span></span>
*  <span data-ttu-id="04edb-2735">`case` метки `switch` инструкции ([оператора switch](statements.md#the-switch-statement)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2735">`case` labels of a `switch` statement ([The switch statement](statements.md#the-switch-statement)).</span></span>
*  <span data-ttu-id="04edb-2736">`goto case` операторы ([инструкцию goto](statements.md#the-goto-statement)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2736">`goto case` statements ([The goto statement](statements.md#the-goto-statement)).</span></span>
*  <span data-ttu-id="04edb-2737">Длины измерений в выражение создания массива ([выражениях создания массива](expressions.md#array-creation-expressions)), включает в себя инициализатор.</span><span class="sxs-lookup"><span data-stu-id="04edb-2737">Dimension lengths in an array creation expression ([Array creation expressions](expressions.md#array-creation-expressions)) that includes an initializer.</span></span>
*  <span data-ttu-id="04edb-2738">Атрибуты ([атрибуты](attributes.md)).</span><span class="sxs-lookup"><span data-stu-id="04edb-2738">Attributes ([Attributes](attributes.md)).</span></span>

<span data-ttu-id="04edb-2739">Неявные преобразования выражений констант ([неявные преобразования выражений констант](conversions.md#implicit-constant-expression-conversions)) позволяет константное выражение типа `int` для преобразования в `sbyte`, `byte`, `short`, `ushort`, `uint`, или `ulong`, если значение константного выражения находится в диапазоне конечного типа.</span><span class="sxs-lookup"><span data-stu-id="04edb-2739">An implicit constant expression conversion ([Implicit constant expression conversions](conversions.md#implicit-constant-expression-conversions)) permits a constant expression of type `int` to be converted to `sbyte`, `byte`, `short`, `ushort`, `uint`, or `ulong`, provided the value of the constant expression is within the range of the destination type.</span></span>

## <a name="boolean-expressions"></a><span data-ttu-id="04edb-2740">логические выражения</span><span class="sxs-lookup"><span data-stu-id="04edb-2740">Boolean expressions</span></span>

<span data-ttu-id="04edb-2741">Объект *boolean_expression* представляет собой выражение, результатом выполнения тип `bool`; либо напрямую или путем применения `operator true` в определенных контекстах, как указано ниже.</span><span class="sxs-lookup"><span data-stu-id="04edb-2741">A *boolean_expression* is an expression that yields a result of type `bool`; either directly or through application of `operator true` in certain contexts as specified in the following.</span></span>

```antlr
boolean_expression
    : expression
    ;
```

<span data-ttu-id="04edb-2742">Управляющее выражение условного оператора *if_statement* ([if инструкции](statements.md#the-if-statement)), *while_statement* ([оператор while](statements.md#the-while-statement)), *do_statement* ([инструкции do](statements.md#the-do-statement)), или *for_statement* ([для инструкции](statements.md#the-for-statement)) является *boolean_ выражение*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2742">The controlling conditional expression of an *if_statement* ([The if statement](statements.md#the-if-statement)), *while_statement* ([The while statement](statements.md#the-while-statement)), *do_statement* ([The do statement](statements.md#the-do-statement)), or *for_statement* ([The for statement](statements.md#the-for-statement)) is a *boolean_expression*.</span></span> <span data-ttu-id="04edb-2743">Управляющее выражение условного оператора `?:` оператор ([условный оператор](expressions.md#conditional-operator)) работает так же как *boolean_expression*, но по соображениям оператора классифицируется приоритет как *conditional_or_expression*.</span><span class="sxs-lookup"><span data-stu-id="04edb-2743">The controlling conditional expression of the `?:` operator ([Conditional operator](expressions.md#conditional-operator)) follows the same rules as a *boolean_expression*, but for reasons of operator precedence is classified as a *conditional_or_expression*.</span></span>

<span data-ttu-id="04edb-2744">Объект *boolean_expression* `E` должен иметь возможность получения значения типа `bool`, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="04edb-2744">A *boolean_expression* `E` is required to be able to produce a value of type `bool`, as follows:</span></span>

*  <span data-ttu-id="04edb-2745">Если `E` неявно преобразуется к типу `bool` во время выполнения применяется это неявное преобразование.</span><span class="sxs-lookup"><span data-stu-id="04edb-2745">If `E` is implicitly convertible to `bool` then at runtime that implicit conversion is applied.</span></span>
*  <span data-ttu-id="04edb-2746">В противном случае разрешение перегрузки унарного оператора ([разрешение перегрузки унарного оператора](expressions.md#unary-operator-overload-resolution)) используется для поиска наиболее уникальную реализацию оператора `true` на `E`, и что реализация применяется во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="04edb-2746">Otherwise, unary operator overload resolution ([Unary operator overload resolution](expressions.md#unary-operator-overload-resolution)) is used to find a unique best implementation of operator `true` on `E`, and that implementation is applied at runtime.</span></span>
*  <span data-ttu-id="04edb-2747">Если оператор не найден, возникает ошибка времени привязки.</span><span class="sxs-lookup"><span data-stu-id="04edb-2747">If no such operator is found, a binding-time error occurs.</span></span>

<span data-ttu-id="04edb-2748">`DBBool` Типа структуры в [базы данных логического типа](structs.md#database-boolean-type) является примером типа, который реализует `operator true` и `operator false`.</span><span class="sxs-lookup"><span data-stu-id="04edb-2748">The `DBBool` struct type in [Database boolean type](structs.md#database-boolean-type) provides an example of a type that implements `operator true` and `operator false`.</span></span>
