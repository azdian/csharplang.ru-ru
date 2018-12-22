# <a name="documentation-comments"></a><span data-ttu-id="77e2e-101">Комментарии к документации</span><span class="sxs-lookup"><span data-stu-id="77e2e-101">Documentation comments</span></span>

<span data-ttu-id="77e2e-102">C# предоставляет механизм для программистов для документирования кода с помощью специального синтаксиса комментариев, содержащий XML-текст.</span><span class="sxs-lookup"><span data-stu-id="77e2e-102">C# provides a mechanism for programmers to document their code using a special comment syntax that contains XML text.</span></span> <span data-ttu-id="77e2e-103">В файлах исходного кода комментарии, имеющие определенный вид может использоваться для направления инструментом создания XML из этих комментариев и элементов исходного кода, которым они предшествуют.</span><span class="sxs-lookup"><span data-stu-id="77e2e-103">In source code files, comments having a certain form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede.</span></span> <span data-ttu-id="77e2e-104">Комментарии с помощью такого синтаксиса, называются ***комментарии к документации***.</span><span class="sxs-lookup"><span data-stu-id="77e2e-104">Comments using such syntax are called ***documentation comments***.</span></span> <span data-ttu-id="77e2e-105">Они должны непосредственно предшествовать определяемого пользователем типа (например, класс, делегат или интерфейс) или члена (например, поле, событие, свойство или метод).</span><span class="sxs-lookup"><span data-stu-id="77e2e-105">They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method).</span></span> <span data-ttu-id="77e2e-106">Инструмент создания XML называется ***генератор документации***.</span><span class="sxs-lookup"><span data-stu-id="77e2e-106">The XML generation tool is called the ***documentation generator***.</span></span> <span data-ttu-id="77e2e-107">(Этот генератор может быть, но не обязательно, компилятор C# сам). Выходные данные, создаваемые генератор документации вызывается ***файл документации***.</span><span class="sxs-lookup"><span data-stu-id="77e2e-107">(This generator could be, but need not be, the C# compiler itself.) The output produced by the documentation generator is called the ***documentation file***.</span></span> <span data-ttu-id="77e2e-108">Файл документации используется в качестве входных данных для ***просмотра документации***; средство для создания своего рода визуальное отображение элемента сведений о типе и соответствующая документация.</span><span class="sxs-lookup"><span data-stu-id="77e2e-108">A documentation file is used as input to a ***documentation viewer***; a tool intended to produce some sort of visual display of type information and its associated documentation.</span></span>

<span data-ttu-id="77e2e-109">Эта спецификация предлагает набор тегов для использования в комментарии к документации, но использование этих тегов не является обязательным и другие теги может использоваться при необходимости, пока соблюдаются правила корректный XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-109">This specification suggests a set of tags to be used in documentation comments, but use of these tags is not required, and other tags may be used if desired, as long the rules of well-formed XML are followed.</span></span>

## <a name="introduction"></a><span data-ttu-id="77e2e-110">Вступление</span><span class="sxs-lookup"><span data-stu-id="77e2e-110">Introduction</span></span>

<span data-ttu-id="77e2e-111">Комментарии, имеющие это особая форма может использоваться для направления инструментом создания XML из этих комментариев и элементов исходного кода, которым они предшествуют.</span><span class="sxs-lookup"><span data-stu-id="77e2e-111">Comments having a special form can be used to direct a tool to produce XML from those comments and the source code elements, which they precede.</span></span> <span data-ttu-id="77e2e-112">Такие комментарии являются однострочные комментарии, начинающиеся с трех знаков косой черты (`///`), или комментарии, которые начинаются с косой черты и двумя звездами с разделителями (`/**`).</span><span class="sxs-lookup"><span data-stu-id="77e2e-112">Such comments are single-line comments that start with three slashes (`///`), or delimited comments that start with a slash and two stars (`/**`).</span></span> <span data-ttu-id="77e2e-113">Они должны непосредственно предшествовать определяемого пользователем типа (например, класс, делегат или интерфейс) или члена (например, поле, событие, свойство или метод), к которому они относятся.</span><span class="sxs-lookup"><span data-stu-id="77e2e-113">They must immediately precede a user-defined type (such as a class, delegate, or interface) or a member (such as a field, event, property, or method) that they annotate.</span></span> <span data-ttu-id="77e2e-114">Атрибут разделы ([спецификация атрибута](attributes.md#attribute-specification)) являются частью объявления, поэтому комментарии к документации должны предшествовать атрибутов, примененных к типу или члену.</span><span class="sxs-lookup"><span data-stu-id="77e2e-114">Attribute sections ([Attribute specification](attributes.md#attribute-specification)) are considered part of declarations, so documentation comments must precede attributes applied to a type or member.</span></span>

<span data-ttu-id="77e2e-115">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-115">__Syntax:__</span></span>

```antlr
single_line_doc_comment
    : '///' input_character*
    ;

delimited_doc_comment
    : '/**' delimited_comment_section* asterisk+ '/'
    ;
```

<span data-ttu-id="77e2e-116">В *single_line_doc_comment*, если есть *пробелы* следующий `///` символов на каждом из *single_line_doc_comment*смежные s текущему *single_line_doc_comment*, затем, *пробелы* символ не включается в выходные данные XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-116">In a *single_line_doc_comment*, if there is a *whitespace* character following the `///` characters on each of the *single_line_doc_comment*s adjacent to the current *single_line_doc_comment*, then that *whitespace* character is not included in the XML output.</span></span>

<span data-ttu-id="77e2e-117">С разделителями doc-комментария Если первый отличный от пробела символ на второй строке является звездочка и та же последовательность необязательные пробелы и знак звездочки повторяется в начале каждой строки в с разделителями комментариев в документации, затем символы повторяющихся шаблона не включаются в выходные данные XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-117">In a delimited-doc-comment, if the first non-whitespace character on the second line is an asterisk and the same pattern of optional whitespace characters and an asterisk character is repeated at the beginning of each of the line within the delimited-doc-comment, then the characters of the repeated pattern are not included in the XML output.</span></span> <span data-ttu-id="77e2e-118">Шаблон может включать пробелы после, а также перед символом звездочки.</span><span class="sxs-lookup"><span data-stu-id="77e2e-118">The pattern may include whitespace characters after, as well as before, the asterisk character.</span></span>

<span data-ttu-id="77e2e-119">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-119">__Example:__</span></span>

```csharp
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>
///
public class Point 
{
    /// <summary>method <c>draw</c> renders the point.</summary>
    void draw() {...}
}
```

<span data-ttu-id="77e2e-120">Текст внутри комментариев документации должны быть сформированы в соответствии с правилами XML (http://www.w3.org/TR/REC-xml).</span><span class="sxs-lookup"><span data-stu-id="77e2e-120">The text within documentation comments must be well formed according to the rules of XML (http://www.w3.org/TR/REC-xml).</span></span> <span data-ttu-id="77e2e-121">Если XML имеет неправильную форму, сформированном, выдается предупреждение и файл документации содержит комментарий о том, что произошла ошибка.</span><span class="sxs-lookup"><span data-stu-id="77e2e-121">If the XML is ill formed, a warning is generated and the documentation file will contain a comment saying that an error was encountered.</span></span>

<span data-ttu-id="77e2e-122">Несмотря на то, что разработчики могут создавать свои собственные наборы тегов, рекомендуемый набор определяется в [Рекомендуемые теги](documentation-comments.md#recommended-tags).</span><span class="sxs-lookup"><span data-stu-id="77e2e-122">Although developers are free to create their own set of tags, a recommended set is defined in [Recommended tags](documentation-comments.md#recommended-tags).</span></span> <span data-ttu-id="77e2e-123">Некоторые рекомендуемые теги имеют особые значения.</span><span class="sxs-lookup"><span data-stu-id="77e2e-123">Some of the recommended tags have special meanings:</span></span>

*  <span data-ttu-id="77e2e-124">`<param>` Тег используется для описания параметров.</span><span class="sxs-lookup"><span data-stu-id="77e2e-124">The `<param>` tag is used to describe parameters.</span></span> <span data-ttu-id="77e2e-125">Если используется такой тег, генератор документации необходимо убедиться, что указанный параметр существует и что все параметры описаны в комментариях к документации.</span><span class="sxs-lookup"><span data-stu-id="77e2e-125">If such a tag is used, the documentation generator must verify that the specified parameter exists and that all parameters are described in documentation comments.</span></span> <span data-ttu-id="77e2e-126">Если проверка завершается ошибкой, генератор документации выдает предупреждение.</span><span class="sxs-lookup"><span data-stu-id="77e2e-126">If such verification fails, the documentation generator issues a warning.</span></span>
*  <span data-ttu-id="77e2e-127">Атрибут `cref` может быть присоединен к любому тегу для предоставления ссылки на элемент кода.</span><span class="sxs-lookup"><span data-stu-id="77e2e-127">The `cref` attribute can be attached to any tag to provide a reference to a code element.</span></span> <span data-ttu-id="77e2e-128">Генератор документации необходимо проверить наличие этого элемента кода.</span><span class="sxs-lookup"><span data-stu-id="77e2e-128">The documentation generator must verify that this code element exists.</span></span> <span data-ttu-id="77e2e-129">Если проверка будет выполнена успешно, генератор документации выдает предупреждение.</span><span class="sxs-lookup"><span data-stu-id="77e2e-129">If the verification fails, the documentation generator issues a warning.</span></span> <span data-ttu-id="77e2e-130">При поиске имени, описанная в `cref` атрибут, генератор документации должны уважать видимость пространства имен в соответствии с `using` инструкция, находящаяся сразу в исходном коде.</span><span class="sxs-lookup"><span data-stu-id="77e2e-130">When looking for a name described in a `cref` attribute, the documentation generator must respect namespace visibility according to `using` statements appearing within the source code.</span></span> <span data-ttu-id="77e2e-131">Для элементов кода, которые являются обобщенными, обычного синтаксиса универсальных шаблонов (т. е "`List<T>`«) не может использоваться, поскольку он создает недопустимый XML-код.</span><span class="sxs-lookup"><span data-stu-id="77e2e-131">For code elements that are generic, the normal generic syntax (ie "`List<T>`") cannot be used because it produces invalid XML.</span></span> <span data-ttu-id="77e2e-132">Можно использовать вместо квадратных скобок (ie "`List{T}`«), или можно использовать escape-синтаксис XML (т. е"`List&lt;T&gt;`«).</span><span class="sxs-lookup"><span data-stu-id="77e2e-132">Braces can be used instead of brackets (ie "`List{T}`"), or the XML escape syntax can be used (ie "`List&lt;T&gt;`").</span></span>
*  <span data-ttu-id="77e2e-133">`<summary>` Тег предназначен для использования средством просмотра документации для отображения дополнительных сведений о типе или член.</span><span class="sxs-lookup"><span data-stu-id="77e2e-133">The `<summary>` tag is intended to be used by a documentation viewer to display additional information about a type or member.</span></span>
*  <span data-ttu-id="77e2e-134">`<include>` Тег содержит сведения из внешнего файла XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-134">The `<include>` tag includes information from an external XML file.</span></span>

<span data-ttu-id="77e2e-135">Нужно понимать, что файл документации не предоставляет полную информацию о типе и членах (например, он не содержит никаких сведений о типе).</span><span class="sxs-lookup"><span data-stu-id="77e2e-135">Note carefully that the documentation file does not provide full information about the type and members (for example, it does not contain any type information).</span></span> <span data-ttu-id="77e2e-136">Для получения таких сведений о типе или член, необходимо использовать файл документации вместе с отражением на текущий тип или член.</span><span class="sxs-lookup"><span data-stu-id="77e2e-136">To get such information about a type or member, the documentation file must be used in conjunction with reflection on the actual type or member.</span></span>

## <a name="recommended-tags"></a><span data-ttu-id="77e2e-137">Рекомендуемые теги</span><span class="sxs-lookup"><span data-stu-id="77e2e-137">Recommended tags</span></span>

<span data-ttu-id="77e2e-138">Генератор документации должен принимать и обрабатывать любые тег, который является допустимым в соответствии с правилами XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-138">The documentation generator must accept and process any tag that is valid according to the rules of XML.</span></span> <span data-ttu-id="77e2e-139">Следующие теги предоставляют часто используемые возможности в документации для пользователей.</span><span class="sxs-lookup"><span data-stu-id="77e2e-139">The following tags provide commonly used functionality in user documentation.</span></span> <span data-ttu-id="77e2e-140">(Конечно, другие теги возможны.)</span><span class="sxs-lookup"><span data-stu-id="77e2e-140">(Of course, other tags are possible.)</span></span>


| <span data-ttu-id="77e2e-141">__Тег__</span><span class="sxs-lookup"><span data-stu-id="77e2e-141">__Tag__</span></span>          | <span data-ttu-id="77e2e-142">__Раздел__</span><span class="sxs-lookup"><span data-stu-id="77e2e-142">__Section__</span></span>                                            | <span data-ttu-id="77e2e-143">__Назначение__</span><span class="sxs-lookup"><span data-stu-id="77e2e-143">__Purpose__</span></span>                                            |
|------------------|--------------------------------------------------------|--------------------------------------------------------|
| `<c>`            | [`<c>`](documentation-comments.md#c)                   | <span data-ttu-id="77e2e-144">Задание текста шрифтом кода</span><span class="sxs-lookup"><span data-stu-id="77e2e-144">Set text in a code-like font</span></span>                           | 
| `<code>`         | [`<code>`](documentation-comments.md#code)             | <span data-ttu-id="77e2e-145">Задайте один или несколько строк исходного кода или выходных данных программы</span><span class="sxs-lookup"><span data-stu-id="77e2e-145">Set one or more lines of source code or program output</span></span> |
| `<example>`      | [`<example>`](documentation-comments.md#example)       | <span data-ttu-id="77e2e-146">Указать пример</span><span class="sxs-lookup"><span data-stu-id="77e2e-146">Indicate an example</span></span>                                    |
| `<exception>`    | [`<exception>`](documentation-comments.md#exception)   | <span data-ttu-id="77e2e-147">Определяет исключения, которые может выдавать метод</span><span class="sxs-lookup"><span data-stu-id="77e2e-147">Identifies the exceptions a method can throw</span></span>           |
| `<include>`      | [`<include>`](documentation-comments.md#include)       | <span data-ttu-id="77e2e-148">Включает в себя XML из внешнего файла</span><span class="sxs-lookup"><span data-stu-id="77e2e-148">Includes XML from an external file</span></span>                     |
| `<list>`         | [`<list>`](documentation-comments.md#list)             | <span data-ttu-id="77e2e-149">Создание списка или таблицы</span><span class="sxs-lookup"><span data-stu-id="77e2e-149">Create a list or table</span></span>                                 |
| `<para>`         | [`<para>`](documentation-comments.md#para)             | <span data-ttu-id="77e2e-150">Разрешить добавление к тексту структуры</span><span class="sxs-lookup"><span data-stu-id="77e2e-150">Permit structure to be added to text</span></span>                   |
| `<param>`        | [`<param>`](documentation-comments.md#param)           | <span data-ttu-id="77e2e-151">Описания параметра для метода или конструктора</span><span class="sxs-lookup"><span data-stu-id="77e2e-151">Describe a parameter for a method or constructor</span></span>       |
| `<paramref>`     | [`<paramref>`](documentation-comments.md#paramref)     | <span data-ttu-id="77e2e-152">Указать, что слово является именем параметра</span><span class="sxs-lookup"><span data-stu-id="77e2e-152">Identify that a word is a parameter name</span></span>               |
| `<permission>`   | [`<permission>`](documentation-comments.md#permission) | <span data-ttu-id="77e2e-153">Документ безопасности доступа к члену</span><span class="sxs-lookup"><span data-stu-id="77e2e-153">Document the security accessibility of a member</span></span>        |
| `<remark>`       | [`<remark>`](documentation-comments.md#remark)         | <span data-ttu-id="77e2e-154">Описаны дополнительные сведения о типе</span><span class="sxs-lookup"><span data-stu-id="77e2e-154">Describe additional information about a type</span></span>           |
| `<returns>`      | [`<returns>`](documentation-comments.md#returns)       | <span data-ttu-id="77e2e-155">Описания возвращаемого значения метода</span><span class="sxs-lookup"><span data-stu-id="77e2e-155">Describe the return value of a method</span></span>                  |
| `<see>`          | [`<see>`](documentation-comments.md#see)               | <span data-ttu-id="77e2e-156">Укажите ссылку</span><span class="sxs-lookup"><span data-stu-id="77e2e-156">Specify a link</span></span>                                         |
| `<seealso>`      | [`<seealso>`](documentation-comments.md#seealso)       | <span data-ttu-id="77e2e-157">Создать запись см. также</span><span class="sxs-lookup"><span data-stu-id="77e2e-157">Generate a See Also entry</span></span>                              |
| `<summary>`      | [`<summary>`](documentation-comments.md#summary)       | <span data-ttu-id="77e2e-158">Описания типа или члена типа</span><span class="sxs-lookup"><span data-stu-id="77e2e-158">Describe a type or a member of a type</span></span>                  |
| `<value>`        | [`<value>`](documentation-comments.md#value)           | <span data-ttu-id="77e2e-159">Описания свойств</span><span class="sxs-lookup"><span data-stu-id="77e2e-159">Describe a property</span></span>                                    |
| `<typeparam>`    |                                                        | <span data-ttu-id="77e2e-160">Описания параметра универсального типа</span><span class="sxs-lookup"><span data-stu-id="77e2e-160">Describe a generic type parameter</span></span>                      |
| `<typeparamref>` |                                                        | <span data-ttu-id="77e2e-161">Указать, что слово является именем параметра типа</span><span class="sxs-lookup"><span data-stu-id="77e2e-161">Identify that a word is a type parameter name</span></span>          |

### `<c>`

<span data-ttu-id="77e2e-162">Этот тег предоставляет механизм для указания, что фрагмент текст в описании следует установить особый шрифт, которые используются для блока кода.</span><span class="sxs-lookup"><span data-stu-id="77e2e-162">This tag provides a mechanism to indicate that a fragment of text within a description should be set in a special font such as that used for a block of code.</span></span> <span data-ttu-id="77e2e-163">Для строк фактический код, используйте `<code>` ([`<code>`](documentation-comments.md#code)).</span><span class="sxs-lookup"><span data-stu-id="77e2e-163">For lines of actual code, use `<code>` ([`<code>`](documentation-comments.md#code)).</span></span>

<span data-ttu-id="77e2e-164">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-164">__Syntax:__</span></span>

```xml
<c>text</c>
```

<span data-ttu-id="77e2e-165">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-165">__Example:__</span></span>

```csharp
/// <summary>Class <c>Point</c> models a point in a two-dimensional
/// plane.</summary>

public class Point 
{
    // ...
}
```

### `<code>`

<span data-ttu-id="77e2e-166">Этот тег используется для задания один или несколько строк исходного кода или программного вывода особого шрифта.</span><span class="sxs-lookup"><span data-stu-id="77e2e-166">This tag is used to set one or more lines of source code or program output in some special font.</span></span> <span data-ttu-id="77e2e-167">Для небольших фрагментов кода в комментарии, используйте `<c>` ([`<c>`](documentation-comments.md#c)).</span><span class="sxs-lookup"><span data-stu-id="77e2e-167">For small code fragments in narrative, use `<c>` ([`<c>`](documentation-comments.md#c)).</span></span>

<span data-ttu-id="77e2e-168">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-168">__Syntax:__</span></span>

```xml
<code>source code or program output</code>
```

<span data-ttu-id="77e2e-169">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-169">__Example:__</span></span>

```csharp
/// <summary>This method changes the point's location by
///    the given x- and y-offsets.
/// <example>For example:
/// <code>
///    Point p = new Point(3,5);
///    p.Translate(-1,3);
/// </code>
/// results in <c>p</c>'s having the value (2,8).
/// </example>
/// </summary>

public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}   
```

### `<example>`

<span data-ttu-id="77e2e-170">Этот тег позволяет вставить пример кода в комментарий, чтобы указать, каким образом можно использовать метод или другого элемента библиотеки.</span><span class="sxs-lookup"><span data-stu-id="77e2e-170">This tag allows example code within a comment, to specify how a method or other library member may be used.</span></span> <span data-ttu-id="77e2e-171">Как правило, это также включает в себя использование тега `<code>` ([`<code>`](documentation-comments.md#code)) также.</span><span class="sxs-lookup"><span data-stu-id="77e2e-171">Ordinarily, this would also involve use of the tag `<code>` ([`<code>`](documentation-comments.md#code)) as well.</span></span>

<span data-ttu-id="77e2e-172">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-172">__Syntax:__</span></span>

```xml
<example>description</example>
```

<span data-ttu-id="77e2e-173">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-173">__Example:__</span></span>

<span data-ttu-id="77e2e-174">См. в разделе `<code>` ([`<code>`](documentation-comments.md#code)) в качестве примера.</span><span class="sxs-lookup"><span data-stu-id="77e2e-174">See `<code>` ([`<code>`](documentation-comments.md#code)) for an example.</span></span>

### `<exception>`

<span data-ttu-id="77e2e-175">Этот тег позволяет документировать исключения, которые может выдавать метод.</span><span class="sxs-lookup"><span data-stu-id="77e2e-175">This tag provides a way to document the exceptions a method can throw.</span></span>

<span data-ttu-id="77e2e-176">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-176">__Syntax:__</span></span>

```xml
<exception cref="member">description</exception>
```

<span data-ttu-id="77e2e-177">где</span><span class="sxs-lookup"><span data-stu-id="77e2e-177">where</span></span>

* <span data-ttu-id="77e2e-178">`member` — Имя члена.</span><span class="sxs-lookup"><span data-stu-id="77e2e-178">`member` is the name of a member.</span></span> <span data-ttu-id="77e2e-179">Генератор документации проверяет, что заданный элемент существует и преобразует `member` к каноническому имени элемента в файле документации.</span><span class="sxs-lookup"><span data-stu-id="77e2e-179">The documentation generator checks that the given member exists and translates `member` to the canonical element name in the documentation file.</span></span>
* <span data-ttu-id="77e2e-180">`description` представляет собой описание обстоятельства, в которых возникает исключение.</span><span class="sxs-lookup"><span data-stu-id="77e2e-180">`description` is a description of the circumstances in which the exception is thrown.</span></span>

<span data-ttu-id="77e2e-181">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-181">__Example:__</span></span>

```csharp
public class DataBaseOperations
{
    /// <exception cref="MasterFileFormatCorruptException"></exception>
    /// <exception cref="MasterFileLockedOpenException"></exception>
    public static void ReadRecord(int flag) {
        if (flag == 1)
            throw new MasterFileFormatCorruptException();
        else if (flag == 2)
            throw new MasterFileLockedOpenException();
        // ...
    } 
}
```

### `<include>`

<span data-ttu-id="77e2e-182">Этот тег позволяет включать сведения из XML-документа, являющиеся внешними для файла исходного кода.</span><span class="sxs-lookup"><span data-stu-id="77e2e-182">This tag allows including information from an XML document that is external to the source code file.</span></span> <span data-ttu-id="77e2e-183">Внешний файл должен быть правильного формата XML-документа, и выражение XPath применяется к этому документу, чтобы указать, какие XML из этого документа, чтобы включить.</span><span class="sxs-lookup"><span data-stu-id="77e2e-183">The external file must be a well-formed XML document, and an XPath expression is applied to that document to specify what XML from that document to include.</span></span> <span data-ttu-id="77e2e-184">`<include>` Тега затем они заменяются выбранным XML из внешнего документа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-184">The `<include>` tag is then replaced with the selected XML from the external document.</span></span>

<span data-ttu-id="77e2e-185">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-185">__Syntax:__</span></span>

```
<include file="filename" path="xpath" />
```

<span data-ttu-id="77e2e-186">где</span><span class="sxs-lookup"><span data-stu-id="77e2e-186">where</span></span>

* <span data-ttu-id="77e2e-187">`filename` — Имя файла из внешнего файла XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-187">`filename` is the file name of an external XML file.</span></span> <span data-ttu-id="77e2e-188">Имя файла интерпретируется относительно файла, содержащего тег включения.</span><span class="sxs-lookup"><span data-stu-id="77e2e-188">The file name is interpreted relative to the file that contains the include tag.</span></span>
* <span data-ttu-id="77e2e-189">`xpath` Такое выражение XPath, который выбирает один из XML во внешнем файле XML.</span><span class="sxs-lookup"><span data-stu-id="77e2e-189">`xpath` is an XPath expression that selects some of the XML in the external XML file.</span></span>

<span data-ttu-id="77e2e-190">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-190">__Example:__</span></span>

<span data-ttu-id="77e2e-191">Если исходный код содержится объявление, подобное:</span><span class="sxs-lookup"><span data-stu-id="77e2e-191">If the source code contained a declaration like:</span></span>

```csharp
/// <include file="docs.xml" path='extradoc/class[@name="IntList"]/*' />
public class IntList { ... }
```

<span data-ttu-id="77e2e-192">и внешнего файла «"docs.XML есть следующее содержимое:</span><span class="sxs-lookup"><span data-stu-id="77e2e-192">and the external file "docs.xml" had the following contents:</span></span>

```xml
<?xml version="1.0"?>
<extradoc>
  <class name="IntList">
     <summary>
        Contains a list of integers.
     </summary>
  </class>
  <class name="StringList">
     <summary>
        Contains a list of integers.
     </summary>
  </class>
</extradoc>
```

<span data-ttu-id="77e2e-193">Затем эта же документация выводится как, если исходный код содержится:</span><span class="sxs-lookup"><span data-stu-id="77e2e-193">then the same documentation is output as if the source code contained:</span></span>

```csharp
/// <summary>
///    Contains a list of integers.
/// </summary>
public class IntList { ... }
```

### `<list>`

<span data-ttu-id="77e2e-194">Этот тег используется для создания списка или таблицы элементов.</span><span class="sxs-lookup"><span data-stu-id="77e2e-194">This tag is used to create a list or table of items.</span></span> <span data-ttu-id="77e2e-195">Он может содержать `<listheader>` блок для определения строки заголовка таблицы или определение списка.</span><span class="sxs-lookup"><span data-stu-id="77e2e-195">It may contain a `<listheader>` block to define the heading row of either a table or definition list.</span></span> <span data-ttu-id="77e2e-196">(При определении таблицы, только запись `term` в заголовке необходимо предоставить.)</span><span class="sxs-lookup"><span data-stu-id="77e2e-196">(When defining a table, only an entry for `term` in the heading need be supplied.)</span></span>

<span data-ttu-id="77e2e-197">Каждый элемент в списке указывается с помощью `<item>` блока.</span><span class="sxs-lookup"><span data-stu-id="77e2e-197">Each item in the list is specified with an `<item>` block.</span></span> <span data-ttu-id="77e2e-198">При создании списка определений, оба `term` и `description` должен быть указан.</span><span class="sxs-lookup"><span data-stu-id="77e2e-198">When creating a definition list, both `term` and `description` must be specified.</span></span> <span data-ttu-id="77e2e-199">Тем не менее, для таблицы, маркированного или нумерованного списка, только `description` необходимо задать.</span><span class="sxs-lookup"><span data-stu-id="77e2e-199">However, for a table, bulleted list, or numbered list, only `description` need be specified.</span></span>

<span data-ttu-id="77e2e-200">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-200">__Syntax:__</span></span>

```xml
<list type="bullet" | "number" | "table">
   <listheader>
      <term>term</term>
      <description>*description*</description>
   </listheader>
   <item>
      <term>term</term>
      <description>*description*</description>
   </item>
    ...
   <item>
      <term>term</term>
      <description>description</description>
   </item>
</list>
```

<span data-ttu-id="77e2e-201">где</span><span class="sxs-lookup"><span data-stu-id="77e2e-201">where</span></span>

* <span data-ttu-id="77e2e-202">`term` — это термин для определения, определение которого находится в `description`.</span><span class="sxs-lookup"><span data-stu-id="77e2e-202">`term` is the term to define, whose definition is in `description`.</span></span>
* <span data-ttu-id="77e2e-203">`description` — Это либо элемент маркированного или нумерованного списка, либо определение `term`.</span><span class="sxs-lookup"><span data-stu-id="77e2e-203">`description` is either an item in a bullet or numbered list, or the definition of a `term`.</span></span>

<span data-ttu-id="77e2e-204">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-204">__Example:__</span></span>

```csharp
public class MyClass
{
    /// <summary>Here is an example of a bulleted list:
    /// <list type="bullet">
    /// <item>
    /// <description>Item 1.</description>
    /// </item>
    /// <item>
    /// <description>Item 2.</description>
    /// </item>
    /// </list>
    /// </summary>
    public static void Main () {
        // ...
    }
}
```

### `<para>`

<span data-ttu-id="77e2e-205">Этот тег используется внутри других тегов, таких как `<summary>` ([`<remark>`](documentation-comments.md#remark)) или `<returns>` ([`<returns>`](documentation-comments.md#returns)) и допускает структуры для добавления текста.</span><span class="sxs-lookup"><span data-stu-id="77e2e-205">This tag is for use inside other tags, such as `<summary>` ([`<remark>`](documentation-comments.md#remark)) or `<returns>` ([`<returns>`](documentation-comments.md#returns)), and permits structure to be added to text.</span></span>

<span data-ttu-id="77e2e-206">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-206">__Syntax:__</span></span>

```xml
<para>content</para>
```

<span data-ttu-id="77e2e-207">где `content` — это текст абзаца.</span><span class="sxs-lookup"><span data-stu-id="77e2e-207">where `content` is the text of the paragraph.</span></span>

<span data-ttu-id="77e2e-208">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-208">__Example:__</span></span>

```csharp
/// <summary>This is the entry point of the Point class testing program.
/// <para>This program tests each method and operator, and
/// is intended to be run after any non-trivial maintenance has
/// been performed on the Point class.</para></summary>
public static void Main() {
    // ...
}
```

### `<param>`

<span data-ttu-id="77e2e-209">Этот тег используется для описания параметра для метода, конструктора или индексатора.</span><span class="sxs-lookup"><span data-stu-id="77e2e-209">This tag is used to describe a parameter for a method, constructor, or indexer.</span></span>

<span data-ttu-id="77e2e-210">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-210">__Syntax:__</span></span>

```xml
<param name="name">description</param>
```

<span data-ttu-id="77e2e-211">где</span><span class="sxs-lookup"><span data-stu-id="77e2e-211">where</span></span>

* <span data-ttu-id="77e2e-212">`name` — Имя параметра.</span><span class="sxs-lookup"><span data-stu-id="77e2e-212">`name` is the name of the parameter.</span></span>
* <span data-ttu-id="77e2e-213">`description` представляет собой описание параметра.</span><span class="sxs-lookup"><span data-stu-id="77e2e-213">`description` is a description of the parameter.</span></span>

<span data-ttu-id="77e2e-214">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-214">__Example:__</span></span>

```csharp
/// <summary>This method changes the point's location to
///    the given coordinates.</summary>
/// <param name="xor">the new x-coordinate.</param>
/// <param name="yor">the new y-coordinate.</param>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

### `<paramref>`

<span data-ttu-id="77e2e-215">Этот тег используется для указания, что слово является параметром.</span><span class="sxs-lookup"><span data-stu-id="77e2e-215">This tag is used to indicate that a word is a parameter.</span></span> <span data-ttu-id="77e2e-216">Чтобы этот параметр особым образом могут обрабатываться файл документации.</span><span class="sxs-lookup"><span data-stu-id="77e2e-216">The documentation file can be processed to format this parameter in some distinct way.</span></span>

<span data-ttu-id="77e2e-217">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-217">__Syntax:__</span></span>

```xml
<paramref name="name"/>
```

<span data-ttu-id="77e2e-218">где `name` — это имя параметра.</span><span class="sxs-lookup"><span data-stu-id="77e2e-218">where `name` is the name of the parameter.</span></span>

<span data-ttu-id="77e2e-219">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-219">__Example:__</span></span>

```csharp
/// <summary>This constructor initializes the new Point to
///    (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
/// <param name="xor">the new Point's x-coordinate.</param>
/// <param name="yor">the new Point's y-coordinate.</param>

public Point(int xor, int yor) {
    X = xor;
    Y = yor;
}
```

### `<permission>`

<span data-ttu-id="77e2e-220">Этот тег дает возможность безопасного доступа члена задокументировать.</span><span class="sxs-lookup"><span data-stu-id="77e2e-220">This tag allows the security accessibility of a member to be documented.</span></span>

<span data-ttu-id="77e2e-221">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-221">__Syntax:__</span></span>

```xml
<permission cref="member">description</permission>
```

<span data-ttu-id="77e2e-222">где</span><span class="sxs-lookup"><span data-stu-id="77e2e-222">where</span></span>

* <span data-ttu-id="77e2e-223">`member` — Имя члена.</span><span class="sxs-lookup"><span data-stu-id="77e2e-223">`member` is the name of a member.</span></span> <span data-ttu-id="77e2e-224">Генератор документации проверяет, что данный элемент кода существует и преобразует *член* к каноническому имени элемента в файле документации.</span><span class="sxs-lookup"><span data-stu-id="77e2e-224">The documentation generator checks that the given code element exists and translates *member* to the canonical element name in the documentation file.</span></span>
* <span data-ttu-id="77e2e-225">`description` представляет собой описание доступа к члену.</span><span class="sxs-lookup"><span data-stu-id="77e2e-225">`description` is a description of the access to the member.</span></span>

<span data-ttu-id="77e2e-226">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-226">__Example:__</span></span>

```csharp
/// <permission cref="System.Security.PermissionSet">Everyone can
/// access this method.</permission>

public static void Test() {
    // ...
}
```

### `<remark>`

<span data-ttu-id="77e2e-227">Этот тег используется для указания дополнительных сведений о типе.</span><span class="sxs-lookup"><span data-stu-id="77e2e-227">This tag is used to specify extra information about a type.</span></span> <span data-ttu-id="77e2e-228">(Используйте `<summary>` ([`<summary>`](documentation-comments.md#summary)) для описания самого типа и членов типа.)</span><span class="sxs-lookup"><span data-stu-id="77e2e-228">(Use `<summary>` ([`<summary>`](documentation-comments.md#summary)) to describe the type itself and the members of a type.)</span></span>

<span data-ttu-id="77e2e-229">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-229">__Syntax:__</span></span>

```xml
<remark>description</remark>
```

<span data-ttu-id="77e2e-230">где `description` является текст примечания.</span><span class="sxs-lookup"><span data-stu-id="77e2e-230">where `description` is the text of the remark.</span></span>

<span data-ttu-id="77e2e-231">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-231">__Example:__</span></span>

```csharp
/// <summary>Class <c>Point</c> models a point in a 
/// two-dimensional plane.</summary>
/// <remark>Uses polar coordinates</remark>
public class Point 
{
    // ...
}
```

### `<returns>`

<span data-ttu-id="77e2e-232">Этот тег используется для описания возвращаемого значения метода.</span><span class="sxs-lookup"><span data-stu-id="77e2e-232">This tag is used to describe the return value of a method.</span></span>

<span data-ttu-id="77e2e-233">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-233">__Syntax:__</span></span>

```xml
<returns>description</returns>
```

<span data-ttu-id="77e2e-234">где `description` представляет собой описание возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="77e2e-234">where `description` is a description of the return value.</span></span>

<span data-ttu-id="77e2e-235">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-235">__Example:__</span></span>

```csharp
/// <summary>Report a point's location as a string.</summary>
/// <returns>A string representing a point's location, in the form (x,y),
///    without any leading, trailing, or embedded whitespace.</returns>
public override string ToString() {
    return "(" + X + "," + Y + ")";
}
```

### `<see>`

<span data-ttu-id="77e2e-236">Этот тег дает ссылку, чтобы указать в тексте.</span><span class="sxs-lookup"><span data-stu-id="77e2e-236">This tag allows a link to be specified within text.</span></span> <span data-ttu-id="77e2e-237">Используйте `<seealso>` ([`<seealso>`](documentation-comments.md#seealso)) чтобы указать текст, отображаемый в разделе см. в разделе.</span><span class="sxs-lookup"><span data-stu-id="77e2e-237">Use `<seealso>` ([`<seealso>`](documentation-comments.md#seealso)) to indicate text that is to appear in a See Also section.</span></span>

<span data-ttu-id="77e2e-238">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-238">__Syntax:__</span></span>

```xml
<see cref="member"/>
```

<span data-ttu-id="77e2e-239">где `member` имя члена.</span><span class="sxs-lookup"><span data-stu-id="77e2e-239">where `member` is the name of a member.</span></span> <span data-ttu-id="77e2e-240">Генератор документации проверяет, что данный элемент кода существует и изменяет *член* имени элемента в файле созданную документацию.</span><span class="sxs-lookup"><span data-stu-id="77e2e-240">The documentation generator checks that the given code element exists and changes *member* to the element name in the generated documentation file.</span></span>

<span data-ttu-id="77e2e-241">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-241">__Example:__</span></span>

```csharp
/// <summary>This method changes the point's location to
///    the given coordinates.</summary>
/// <see cref="Translate"/>
public void Move(int xor, int yor) {
    X = xor;
    Y = yor;
}

/// <summary>This method changes the point's location by
///    the given x- and y-offsets.
/// </summary>
/// <see cref="Move"/>
public void Translate(int xor, int yor) {
    X += xor;
    Y += yor;
}
```

### `<seealso>`

<span data-ttu-id="77e2e-242">Этот тег позволяет запись для см.</span><span class="sxs-lookup"><span data-stu-id="77e2e-242">This tag allows an entry to be generated for the See Also section.</span></span> <span data-ttu-id="77e2e-243">Используйте `<see>` ([`<see>`](documentation-comments.md#see)) чтобы указать ссылку из текста.</span><span class="sxs-lookup"><span data-stu-id="77e2e-243">Use `<see>` ([`<see>`](documentation-comments.md#see)) to specify a link from within text.</span></span>

<span data-ttu-id="77e2e-244">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-244">__Syntax:__</span></span>

```xml
<seealso cref="member"/>
```

<span data-ttu-id="77e2e-245">где `member` имя члена.</span><span class="sxs-lookup"><span data-stu-id="77e2e-245">where `member` is the name of a member.</span></span> <span data-ttu-id="77e2e-246">Генератор документации проверяет, что данный элемент кода существует и изменяет *член* имени элемента в файле созданную документацию.</span><span class="sxs-lookup"><span data-stu-id="77e2e-246">The documentation generator checks that the given code element exists and changes *member* to the element name in the generated documentation file.</span></span>

<span data-ttu-id="77e2e-247">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-247">__Example:__</span></span>

```csharp
/// <summary>This method determines whether two Points have the same
///    location.</summary>
/// <seealso cref="operator=="/>
/// <seealso cref="operator!="/>
public override bool Equals(object o) {
    // ...
}
```

### `<summary>`

Этот тег может использоваться для описания типа или члена типа. <span data-ttu-id="77e2e-249">Используйте `<remark>` ([`<remark>`](documentation-comments.md#remark)) для описания самого типа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-249">Use `<remark>` ([`<remark>`](documentation-comments.md#remark)) to describe the type itself.</span></span>

<span data-ttu-id="77e2e-250">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-250">__Syntax:__</span></span>

```xml
<summary>description</summary>
```

<span data-ttu-id="77e2e-251">где `description` представлена сводка по типу или члену.</span><span class="sxs-lookup"><span data-stu-id="77e2e-251">where `description` is a summary of the type or member.</span></span>

<span data-ttu-id="77e2e-252">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-252">__Example:__</span></span>

```csharp
/// <summary>This constructor initializes the new Point to (0,0).</summary>
public Point() : this(0,0) {
}
```

### `<value>`

<span data-ttu-id="77e2e-253">Этот тег позволяет свойство могут существовать описания.</span><span class="sxs-lookup"><span data-stu-id="77e2e-253">This tag allows a property to be described.</span></span>

<span data-ttu-id="77e2e-254">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-254">__Syntax:__</span></span>

```xml
<value>property description</value>
```

<span data-ttu-id="77e2e-255">где `property description` представляет собой описание свойства.</span><span class="sxs-lookup"><span data-stu-id="77e2e-255">where `property description` is a description for the property.</span></span>

<span data-ttu-id="77e2e-256">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-256">__Example:__</span></span>

```csharp
/// <value>Property <c>X</c> represents the point's x-coordinate.</value>
public int X
{
    get { return x; }
    set { x = value; }
}
```

### `<typeparam>`

<span data-ttu-id="77e2e-257">Этот тег используется для описания параметра универсального типа для класса, структуры, интерфейса, делегата или метод.</span><span class="sxs-lookup"><span data-stu-id="77e2e-257">This tag is used to describe a generic type parameter for a class, struct, interface, delegate, or method.</span></span>

<span data-ttu-id="77e2e-258">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-258">__Syntax:__</span></span>

```xml
<typeparam name="name">description</typeparam>
```

<span data-ttu-id="77e2e-259">где `name` имя параметра типа и `description` является его описанием.</span><span class="sxs-lookup"><span data-stu-id="77e2e-259">where `name` is the name of the type parameter, and `description` is its description.</span></span>

<span data-ttu-id="77e2e-260">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-260">__Example:__</span></span>

```csharp
/// <summary>A generic list class.</summary>
/// <typeparam name="T">The type stored by the list.</typeparam>
public class MyList<T> {
    ...
}
```

### `<typeparamref>`

<span data-ttu-id="77e2e-261">Этот тег используется для указания, что слово является параметром типа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-261">This tag is used to indicate that a word is a type parameter.</span></span> <span data-ttu-id="77e2e-262">Файл документации могут обрабатываться для форматирования данного параметра типа определенным образом.</span><span class="sxs-lookup"><span data-stu-id="77e2e-262">The documentation file can be processed to format this type parameter in some distinct way.</span></span>

<span data-ttu-id="77e2e-263">__Синтаксис:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-263">__Syntax:__</span></span>

```xml
<typeparamref name="name"/>
```

<span data-ttu-id="77e2e-264">где `name` — это имя параметра типа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-264">where `name` is the name of the type parameter.</span></span>

<span data-ttu-id="77e2e-265">__Пример:__</span><span class="sxs-lookup"><span data-stu-id="77e2e-265">__Example:__</span></span>

```csharp
/// <summary>This method fetches data and returns a list of <typeparamref name="T"/>.</summary>
/// <param name="query">query to execute</param>
public List<T> FetchData<T>(string query) {
    ...
}
```

## <a name="processing-the-documentation-file"></a><span data-ttu-id="77e2e-266">Обработка файла документации</span><span class="sxs-lookup"><span data-stu-id="77e2e-266">Processing the documentation file</span></span>

<span data-ttu-id="77e2e-267">Генератор документации создает строку идентификатора для каждого элемента в исходном коде, помеченного комментарием документации.</span><span class="sxs-lookup"><span data-stu-id="77e2e-267">The documentation generator generates an ID string for each element in the source code that is tagged with a documentation comment.</span></span> <span data-ttu-id="77e2e-268">Строка идентификатора однозначно идентифицирует элемент источника.</span><span class="sxs-lookup"><span data-stu-id="77e2e-268">This ID string uniquely identifies a source element.</span></span> <span data-ttu-id="77e2e-269">Средство просмотра документации можно использовать строку идентификатора для идентификации соответствующего элемента метаданных или отражения, к которому применяется документации.</span><span class="sxs-lookup"><span data-stu-id="77e2e-269">A documentation viewer can use an ID string to identify the corresponding metadata/reflection item to which the documentation applies.</span></span>

<span data-ttu-id="77e2e-270">Файл документации не иерархическое представление исходного кода; Скорее это списка со строкой, сгенерированной идентификатор для каждого элемента.</span><span class="sxs-lookup"><span data-stu-id="77e2e-270">The documentation file is not a hierarchical representation of the source code; rather, it is a flat list with a generated ID string for each element.</span></span>

### <a name="id-string-format"></a><span data-ttu-id="77e2e-271">Формат строки идентификатора</span><span class="sxs-lookup"><span data-stu-id="77e2e-271">ID string format</span></span>

<span data-ttu-id="77e2e-272">Генератор документации соблюдает следующие правила при формировании строк Идентификаторов:</span><span class="sxs-lookup"><span data-stu-id="77e2e-272">The documentation generator observes the following rules when it generates the ID strings:</span></span>

*  <span data-ttu-id="77e2e-273">Пробелы в строку не вставляются.</span><span class="sxs-lookup"><span data-stu-id="77e2e-273">No white space is placed in the string.</span></span>

*  <span data-ttu-id="77e2e-274">Первая часть строки определяет тип члена задокументированы, через один символ, за которым следует двоеточие.</span><span class="sxs-lookup"><span data-stu-id="77e2e-274">The first part of the string identifies the kind of member being documented, via a single character followed by a colon.</span></span> <span data-ttu-id="77e2e-275">Определены следующие виды членов:</span><span class="sxs-lookup"><span data-stu-id="77e2e-275">The following kinds of members are defined:</span></span>

   | <span data-ttu-id="77e2e-276">__Знак__</span><span class="sxs-lookup"><span data-stu-id="77e2e-276">__Character__</span></span> | <span data-ttu-id="77e2e-277">__Описание__</span><span class="sxs-lookup"><span data-stu-id="77e2e-277">__Description__</span></span>                                             |
   |---------------|-------------------------------------------------------------|
   | <span data-ttu-id="77e2e-278">E</span><span class="sxs-lookup"><span data-stu-id="77e2e-278">E</span></span>             | <span data-ttu-id="77e2e-279">событие</span><span class="sxs-lookup"><span data-stu-id="77e2e-279">Event</span></span>                                                       |
   | <span data-ttu-id="77e2e-280">C</span><span class="sxs-lookup"><span data-stu-id="77e2e-280">F</span></span>             | <span data-ttu-id="77e2e-281">Поле</span><span class="sxs-lookup"><span data-stu-id="77e2e-281">Field</span></span>                                                       |
   | <span data-ttu-id="77e2e-282">M</span><span class="sxs-lookup"><span data-stu-id="77e2e-282">M</span></span>             | <span data-ttu-id="77e2e-283">Метод (включая конструкторы, деструкторы и операторы)</span><span class="sxs-lookup"><span data-stu-id="77e2e-283">Method (including constructors, destructors, and operators)</span></span> |
   | <span data-ttu-id="77e2e-284">в</span><span class="sxs-lookup"><span data-stu-id="77e2e-284">N</span></span>             | <span data-ttu-id="77e2e-285">Пространство имен</span><span class="sxs-lookup"><span data-stu-id="77e2e-285">Namespace</span></span>                                                   |
   | <span data-ttu-id="77e2e-286">С</span><span class="sxs-lookup"><span data-stu-id="77e2e-286">P</span></span>             | <span data-ttu-id="77e2e-287">Свойство (включая индексаторы)</span><span class="sxs-lookup"><span data-stu-id="77e2e-287">Property (including indexers)</span></span>                               |
   | <span data-ttu-id="77e2e-288">T</span><span class="sxs-lookup"><span data-stu-id="77e2e-288">T</span></span>             | <span data-ttu-id="77e2e-289">Тип (например, класс, делегат, перечисление, интерфейс и структуры)</span><span class="sxs-lookup"><span data-stu-id="77e2e-289">Type (such as class, delegate, enum, interface, and struct)</span></span> |
   | <span data-ttu-id="77e2e-290">!</span><span class="sxs-lookup"><span data-stu-id="77e2e-290">!</span></span>             | <span data-ttu-id="77e2e-291">Строка ошибки; Остальная часть строки предоставляет сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="77e2e-291">Error string; the rest of the string provides information about the error.</span></span> <span data-ttu-id="77e2e-292">Например генератор документации создает сведения об ошибках для ссылок, которые не удается разрешить.</span><span class="sxs-lookup"><span data-stu-id="77e2e-292">For example, the documentation generator generates error information for links that cannot be resolved.</span></span> |

*  <span data-ttu-id="77e2e-293">Вторая часть строки — полное имя элемента, начиная с корневого пространства имен.</span><span class="sxs-lookup"><span data-stu-id="77e2e-293">The second part of the string is the fully qualified name of the element, starting at the root of the namespace.</span></span> <span data-ttu-id="77e2e-294">Имя элемента, включающей типы и пространства имен разделяются точками.</span><span class="sxs-lookup"><span data-stu-id="77e2e-294">The name of the element, its enclosing type(s), and namespace are separated by periods.</span></span> <span data-ttu-id="77e2e-295">Если имя самого элемента есть точки, они заменяются `#(U+0023)` символов.</span><span class="sxs-lookup"><span data-stu-id="77e2e-295">If the name of the item itself has periods, they are replaced by `#(U+0023)` characters.</span></span> <span data-ttu-id="77e2e-296">(Предполагается, что элемент не имеет этот символ в имени.)</span><span class="sxs-lookup"><span data-stu-id="77e2e-296">(It is assumed that no element has this character in its name.)</span></span>
*  <span data-ttu-id="77e2e-297">Для методов и свойств с аргументами список аргументов, заключенный в круглые скобки.</span><span class="sxs-lookup"><span data-stu-id="77e2e-297">For methods and properties with arguments, the argument list follows, enclosed in parentheses.</span></span> <span data-ttu-id="77e2e-298">Для тех элементов, которые без аргументов скобки опускаются.</span><span class="sxs-lookup"><span data-stu-id="77e2e-298">For those without arguments, the parentheses are omitted.</span></span> <span data-ttu-id="77e2e-299">Аргументы разделяются запятыми.</span><span class="sxs-lookup"><span data-stu-id="77e2e-299">The arguments are separated by commas.</span></span> <span data-ttu-id="77e2e-300">Кодировка каждого аргумента выглядит так же, как сигнатура CLI следующим образом:</span><span class="sxs-lookup"><span data-stu-id="77e2e-300">The encoding of each argument is the same as a CLI signature, as follows:</span></span>
   *  <span data-ttu-id="77e2e-301">Аргументы представлены своими именами в документации, основанное на их полное имя, изменить следующим образом:</span><span class="sxs-lookup"><span data-stu-id="77e2e-301">Arguments are represented by their documentation name, which is based on their fully qualified name, modified as follows:</span></span>
      * <span data-ttu-id="77e2e-302">Аргументы, представляющие универсальные типы имеют присоединенных `` ` `` символ (обратный апостроф) за которым следует число параметров типа</span><span class="sxs-lookup"><span data-stu-id="77e2e-302">Arguments that represent generic types have an appended `` ` `` (backtick) character followed by the number of type parameters</span></span>
      * <span data-ttu-id="77e2e-303">Аргументы, в которых `out` или `ref` модификатор должен `@` за именем типа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-303">Arguments having the `out` or `ref` modifier have an `@` following their type name.</span></span> <span data-ttu-id="77e2e-304">Аргументы, передаваемые по значению или через `params` не имеют специального обозначения.</span><span class="sxs-lookup"><span data-stu-id="77e2e-304">Arguments passed by value or via `params` have no special notation.</span></span>
      * <span data-ttu-id="77e2e-305">Аргументы, которые являются массивы представляются в виде `[lowerbound:size, ... , lowerbound:size]` где число запятых равно рангу минус один, а нижние границы и размер каждого измерения, если известны, представлены в десятичном формате.</span><span class="sxs-lookup"><span data-stu-id="77e2e-305">Arguments that are arrays are represented as `[lowerbound:size, ... , lowerbound:size]` where the number of commas is the rank less one, and the lower bounds and size of each dimension, if known, are represented in decimal.</span></span> <span data-ttu-id="77e2e-306">Если нижняя граница или размер не указан, она опускается.</span><span class="sxs-lookup"><span data-stu-id="77e2e-306">If a lower bound or size is not specified, it is omitted.</span></span> <span data-ttu-id="77e2e-307">Если нижняя граница и размер для определенной размерности опущены, `:` , опускается.</span><span class="sxs-lookup"><span data-stu-id="77e2e-307">If the lower bound and size for a particular dimension are omitted, the `:` is omitted as well.</span></span> <span data-ttu-id="77e2e-308">Неравномерные массивы представляются одним `[]` на соответствующем уровне.</span><span class="sxs-lookup"><span data-stu-id="77e2e-308">Jagged arrays are represented by one `[]` per level.</span></span>
      * <span data-ttu-id="77e2e-309">Аргументы, которые имеют типы указателей, отличный от void, представлены в виде `*` после имени типа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-309">Arguments that have pointer types other than void are represented using a `*` following the type name.</span></span> <span data-ttu-id="77e2e-310">Указатель void представляется с помощью имени типа из `System.Void`.</span><span class="sxs-lookup"><span data-stu-id="77e2e-310">A void pointer is represented using a type name of `System.Void`.</span></span>
      * <span data-ttu-id="77e2e-311">Аргументы, которые ссылаются на параметры универсального типа, определенные для типов должны кодироваться с использованием `` ` `` символ (обратный апостроф) следуют отсчитываемый от нуля индекс параметра типа.</span><span class="sxs-lookup"><span data-stu-id="77e2e-311">Arguments that refer to generic type parameters defined on types are encoded using the `` ` `` (backtick) character followed by the zero-based index of the type parameter.</span></span>
      * <span data-ttu-id="77e2e-312">Аргументы, которые используют параметры универсального типа, определенные в методах использования — двойной обратный апостроф ``` `` ``` вместо `` ` `` используется для типов.</span><span class="sxs-lookup"><span data-stu-id="77e2e-312">Arguments that use generic type parameters defined in methods use a double-backtick ``` `` ``` instead of the `` ` `` used for types.</span></span>
      * <span data-ttu-id="77e2e-313">Аргументы, которые ссылаются на сконструированных универсальных типов кодируются при помощи универсального типа, за которым следует `{`следует список разделенных запятыми аргументов типа, за которыми следует `}`.</span><span class="sxs-lookup"><span data-stu-id="77e2e-313">Arguments that refer to constructed generic types are encoded using the generic type, followed by `{`, followed by a comma-separated list of type arguments, followed by `}`.</span></span>

### <a name="id-string-examples"></a><span data-ttu-id="77e2e-314">Примеры строк Идентификаторов</span><span class="sxs-lookup"><span data-stu-id="77e2e-314">ID string examples</span></span>

<span data-ttu-id="77e2e-315">Каждый в следующих примерах показано фрагмент кода C#, вместе с Идентификатором строку, полученную из каждого исходного элемента, комментария документации может:</span><span class="sxs-lookup"><span data-stu-id="77e2e-315">The following examples each show a fragment of C# code, along with the ID string produced from each source element capable of having a documentation comment:</span></span>

*  <span data-ttu-id="77e2e-316">Типы представлены их полное имя, дополненное информация общего характера:</span><span class="sxs-lookup"><span data-stu-id="77e2e-316">Types are represented using their fully qualified name, augmented with generic information:</span></span>

   ```csharp
   enum Color { Red, Blue, Green }

   namespace Acme
   {
       interface IProcess {...}

       struct ValueType {...}

       class Widget: IProcess
       {
           public class NestedClass {...}
           public interface IMenuItem {...}
           public delegate void Del(int i);
           public enum Direction { North, South, East, West }
       }

       class MyList<T>
       {
           class Helper<U,V> {...}
       }
   }

   "T:Color"
   "T:Acme.IProcess"
   "T:Acme.ValueType"
   "T:Acme.Widget"
   "T:Acme.Widget.NestedClass"
   "T:Acme.Widget.IMenuItem"
   "T:Acme.Widget.Del"
   "T:Acme.Widget.Direction"
   "T:Acme.MyList`1"
   "T:Acme.MyList`1.Helper`2"
   ```

*  <span data-ttu-id="77e2e-317">Поля представлены их полное имя:</span><span class="sxs-lookup"><span data-stu-id="77e2e-317">Fields are represented by their fully qualified name:</span></span>

   ```csharp
   namespace Acme
   {
       struct ValueType
       {
           private int total;
       }
   
       class Widget: IProcess
       {
           public class NestedClass
           {
               private int value;
           }
   
           private string message;
           private static Color defaultColor;
           private const double PI = 3.14159;
           protected readonly double monthlyAverage;
           private long[] array1;
           private Widget[,] array2;
           private unsafe int *pCount;
           private unsafe float **ppValues;
       }
   }

   "F:Acme.ValueType.total"
   "F:Acme.Widget.NestedClass.value"
   "F:Acme.Widget.message"
   "F:Acme.Widget.defaultColor"
   "F:Acme.Widget.PI"
   "F:Acme.Widget.monthlyAverage"
   "F:Acme.Widget.array1"
   "F:Acme.Widget.array2"
   "F:Acme.Widget.pCount"
   "F:Acme.Widget.ppValues"
   ```

*  <span data-ttu-id="77e2e-318">Конструкторы.</span><span class="sxs-lookup"><span data-stu-id="77e2e-318">Constructors.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           static Widget() {...}
           public Widget() {...}
           public Widget(string s) {...}
       }
   }

   "M:Acme.Widget.#cctor"
   "M:Acme.Widget.#ctor"
   "M:Acme.Widget.#ctor(System.String)"
   ```

*  <span data-ttu-id="77e2e-319">Деструкторы.</span><span class="sxs-lookup"><span data-stu-id="77e2e-319">Destructors.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           ~Widget() {...}
       }
   }
   
   "M:Acme.Widget.Finalize"
   ```

*  <span data-ttu-id="77e2e-320">Методы.</span><span class="sxs-lookup"><span data-stu-id="77e2e-320">Methods.</span></span>

   ```csharp
   namespace Acme
   {
       struct ValueType
       {
           public void M(int i) {...}
       }

       class Widget: IProcess
       {
           public class NestedClass
           {
               public void M(int i) {...}
           }

           public static void M0() {...}
           public void M1(char c, out float f, ref ValueType v) {...}
           public void M2(short[] x1, int[,] x2, long[][] x3) {...}
           public void M3(long[][] x3, Widget[][,,] x4) {...}
           public unsafe void M4(char *pc, Color **pf) {...}
           public unsafe void M5(void *pv, double *[][,] pd) {...}
           public void M6(int i, params object[] args) {...}
       }

       class MyList<T>
       {
           public void Test(T t) { }
       }

       class UseList
       {
           public void Process(MyList<int> list) { }
           public MyList<T> GetValues<T>(T inputValue) { return null; }
       }
   }

   "M:Acme.ValueType.M(System.Int32)"
   "M:Acme.Widget.NestedClass.M(System.Int32)"
   "M:Acme.Widget.M0"
   "M:Acme.Widget.M1(System.Char,System.Single@,Acme.ValueType@)"
   "M:Acme.Widget.M2(System.Int16[],System.Int32[0:,0:],System.Int64[][])"
   "M:Acme.Widget.M3(System.Int64[][],Acme.Widget[0:,0:,0:][])"
   "M:Acme.Widget.M4(System.Char*,Color**)"
   "M:Acme.Widget.M5(System.Void*,System.Double*[0:,0:][])"
   "M:Acme.Widget.M6(System.Int32,System.Object[])"
   "M:Acme.MyList`1.Test(`0)"
   "M:Acme.UseList.Process(Acme.MyList{System.Int32})"
   "M:Acme.UseList.GetValues``(``0)"
   ```

*  <span data-ttu-id="77e2e-321">Свойства и индексаторы.</span><span class="sxs-lookup"><span data-stu-id="77e2e-321">Properties and indexers.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public int Width { get {...} set {...} }
           public int this[int i] { get {...} set {...} }
           public int this[string s, int i] { get {...} set {...} }
       }
   }

   "P:Acme.Widget.Width"
   "P:Acme.Widget.Item(System.Int32)"
   "P:Acme.Widget.Item(System.String,System.Int32)"
   ```

*  <span data-ttu-id="77e2e-322">события.</span><span class="sxs-lookup"><span data-stu-id="77e2e-322">Events.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public event Del AnEvent;
       }
   }

   "E:Acme.Widget.AnEvent"
   ```

*  <span data-ttu-id="77e2e-323">Унарные операторы.</span><span class="sxs-lookup"><span data-stu-id="77e2e-323">Unary operators.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static Widget operator+(Widget x) {...}
       }
   }

   "M:Acme.Widget.op_UnaryPlus(Acme.Widget)"
   ```

   <span data-ttu-id="77e2e-324">Полный набор унарный оператор функции, используемых выглядит следующим образом: `op_UnaryPlus`, `op_UnaryNegation`, `op_LogicalNot`, `op_OnesComplement`, `op_Increment`, `op_Decrement`, `op_True`, и `op_False`.</span><span class="sxs-lookup"><span data-stu-id="77e2e-324">The complete set of unary operator function names used is as follows: `op_UnaryPlus`, `op_UnaryNegation`, `op_LogicalNot`, `op_OnesComplement`, `op_Increment`, `op_Decrement`, `op_True`, and `op_False`.</span></span>

*  <span data-ttu-id="77e2e-325">Бинарные операторы.</span><span class="sxs-lookup"><span data-stu-id="77e2e-325">Binary operators.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static Widget operator+(Widget x1, Widget x2) {...}
       }
   }

   "M:Acme.Widget.op_Addition(Acme.Widget,Acme.Widget)"
   ```

   <span data-ttu-id="77e2e-326">Полный набор имен функцию бинарного оператора, используемых выглядит следующим образом: `op_Addition`, `op_Subtraction`, `op_Multiply`, `op_Division`, `op_Modulus`, `op_BitwiseAnd`, `op_BitwiseOr`, `op_ExclusiveOr`, `op_LeftShift`, `op_RightShift`, `op_Equality`, `op_Inequality`, `op_LessThan`, `op_LessThanOrEqual`, `op_GreaterThan`, и `op_GreaterThanOrEqual`.</span><span class="sxs-lookup"><span data-stu-id="77e2e-326">The complete set of binary operator function names used is as follows: `op_Addition`, `op_Subtraction`, `op_Multiply`, `op_Division`, `op_Modulus`, `op_BitwiseAnd`, `op_BitwiseOr`, `op_ExclusiveOr`, `op_LeftShift`, `op_RightShift`, `op_Equality`, `op_Inequality`, `op_LessThan`, `op_LessThanOrEqual`, `op_GreaterThan`, and `op_GreaterThanOrEqual`.</span></span>

*  <span data-ttu-id="77e2e-327">Операторы преобразования имеют замыкающие "`~`" и типом возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="77e2e-327">Conversion operators have a trailing "`~`" followed by the return type.</span></span>

   ```csharp
   namespace Acme
   {
       class Widget: IProcess
       {
           public static explicit operator int(Widget x) {...}
           public static implicit operator long(Widget x) {...}
       }
   }

   "M:Acme.Widget.op_Explicit(Acme.Widget)~System.Int32"
   "M:Acme.Widget.op_Implicit(Acme.Widget)~System.Int64"
   ```

## <a name="an-example"></a><span data-ttu-id="77e2e-328">Пример</span><span class="sxs-lookup"><span data-stu-id="77e2e-328">An example</span></span>

### <a name="c-source-code"></a><span data-ttu-id="77e2e-329">Исходный код C#</span><span class="sxs-lookup"><span data-stu-id="77e2e-329">C# source code</span></span>

<span data-ttu-id="77e2e-330">В примере показан исходный код `Point` класса:</span><span class="sxs-lookup"><span data-stu-id="77e2e-330">The following example shows the source code of a `Point` class:</span></span>

```csharp
namespace Graphics
{

/// <summary>Class <c>Point</c> models a point in a two-dimensional plane.
/// </summary>
public class Point 
{

    /// <summary>Instance variable <c>x</c> represents the point's
    ///    x-coordinate.</summary>
    private int x;

    /// <summary>Instance variable <c>y</c> represents the point's
    ///    y-coordinate.</summary>
    private int y;

    /// <value>Property <c>X</c> represents the point's x-coordinate.</value>
    public int X
    {
        get { return x; }
        set { x = value; }
    }

    /// <value>Property <c>Y</c> represents the point's y-coordinate.</value>
    public int Y
    {
        get { return y; }
        set { y = value; }
    }

    /// <summary>This constructor initializes the new Point to
    ///    (0,0).</summary>
    public Point() : this(0,0) {}

    /// <summary>This constructor initializes the new Point to
    ///    (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
    /// <param><c>xor</c> is the new Point's x-coordinate.</param>
    /// <param><c>yor</c> is the new Point's y-coordinate.</param>
    public Point(int xor, int yor) {
        X = xor;
        Y = yor;
    }

    /// <summary>This method changes the point's location to
    ///    the given coordinates.</summary>
    /// <param><c>xor</c> is the new x-coordinate.</param>
    /// <param><c>yor</c> is the new y-coordinate.</param>
    /// <see cref="Translate"/>
    public void Move(int xor, int yor) {
        X = xor;
        Y = yor;
    }

    /// <summary>This method changes the point's location by
    ///    the given x- and y-offsets.
    /// <example>For example:
    /// <code>
    ///    Point p = new Point(3,5);
    ///    p.Translate(-1,3);
    /// </code>
    /// results in <c>p</c>'s having the value (2,8).
    /// </example>
    /// </summary>
    /// <param><c>xor</c> is the relative x-offset.</param>
    /// <param><c>yor</c> is the relative y-offset.</param>
    /// <see cref="Move"/>
    public void Translate(int xor, int yor) {
        X += xor;
        Y += yor;
    }

    /// <summary>This method determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>o</c> is the object to be compared to the current object.
    /// </param>
    /// <returns>True if the Points have the same location and they have
    ///    the exact same type; otherwise, false.</returns>
    /// <seealso cref="operator=="/>
    /// <seealso cref="operator!="/>
    public override bool Equals(object o) {
        if (o == null) {
            return false;
        }

        if (this == o) {
            return true;
        }

        if (GetType() == o.GetType()) {
            Point p = (Point)o;
            return (X == p.X) && (Y == p.Y);
        }
        return false;
    }

    /// <summary>Report a point's location as a string.</summary>
    /// <returns>A string representing a point's location, in the form (x,y),
    ///    without any leading, training, or embedded whitespace.</returns>
    public override string ToString() {
        return "(" + X + "," + Y + ")";
    }

    /// <summary>This operator determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>p1</c> is the first Point to be compared.</param>
    /// <param><c>p2</c> is the second Point to be compared.</param>
    /// <returns>True if the Points have the same location and they have
    ///    the exact same type; otherwise, false.</returns>
    /// <seealso cref="Equals"/>
    /// <seealso cref="operator!="/>
    public static bool operator==(Point p1, Point p2) {
        if ((object)p1 == null || (object)p2 == null) {
            return false;
        }

        if (p1.GetType() == p2.GetType()) {
            return (p1.X == p2.X) && (p1.Y == p2.Y);
        }

        return false;
    }

    /// <summary>This operator determines whether two Points have the same
    ///    location.</summary>
    /// <param><c>p1</c> is the first Point to be compared.</param>
    /// <param><c>p2</c> is the second Point to be compared.</param>
    /// <returns>True if the Points do not have the same location and the
    ///    exact same type; otherwise, false.</returns>
    /// <seealso cref="Equals"/>
    /// <seealso cref="operator=="/>
    public static bool operator!=(Point p1, Point p2) {
        return !(p1 == p2);
    }

    /// <summary>This is the entry point of the Point class testing
    /// program.
    /// <para>This program tests each method and operator, and
    /// is intended to be run after any non-trivial maintenance has
    /// been performed on the Point class.</para></summary>
    public static void Main() {
        // class test code goes here
    }
}
}
```

### <a name="resulting-xml"></a><span data-ttu-id="77e2e-331">Результирующий XML</span><span class="sxs-lookup"><span data-stu-id="77e2e-331">Resulting XML</span></span>

<span data-ttu-id="77e2e-332">Здесь представлен результат, созданный генератором документации для заданного исходного кода для класса `Point`, как показано выше:</span><span class="sxs-lookup"><span data-stu-id="77e2e-332">Here is the output produced by one documentation generator when given the source code for class `Point`, shown above:</span></span>

```xml
<?xml version="1.0"?>
<doc>
    <assembly>
        <name>Point</name>
    </assembly>
    <members>
        <member name="T:Graphics.Point">
            <summary>Class <c>Point</c> models a point in a two-dimensional
            plane.
            </summary>
        </member>

        <member name="F:Graphics.Point.x">
            <summary>Instance variable <c>x</c> represents the point's
            x-coordinate.</summary>
        </member>

        <member name="F:Graphics.Point.y">
            <summary>Instance variable <c>y</c> represents the point's
            y-coordinate.</summary>
        </member>

        <member name="M:Graphics.Point.#ctor">
            <summary>This constructor initializes the new Point to
        (0,0).</summary>
        </member>

        <member name="M:Graphics.Point.#ctor(System.Int32,System.Int32)">
            <summary>This constructor initializes the new Point to
            (<paramref name="xor"/>,<paramref name="yor"/>).</summary>
            <param><c>xor</c> is the new Point's x-coordinate.</param>
            <param><c>yor</c> is the new Point's y-coordinate.</param>
        </member>

        <member name="M:Graphics.Point.Move(System.Int32,System.Int32)">
            <summary>This method changes the point's location to
            the given coordinates.</summary>
            <param><c>xor</c> is the new x-coordinate.</param>
            <param><c>yor</c> is the new y-coordinate.</param>
            <see cref="M:Graphics.Point.Translate(System.Int32,System.Int32)"/>
        </member>

        <member
            name="M:Graphics.Point.Translate(System.Int32,System.Int32)">
            <summary>This method changes the point's location by
            the given x- and y-offsets.
            <example>For example:
            <code>
            Point p = new Point(3,5);
            p.Translate(-1,3);
            </code>
            results in <c>p</c>'s having the value (2,8).
            </example>
            </summary>
            <param><c>xor</c> is the relative x-offset.</param>
            <param><c>yor</c> is the relative y-offset.</param>
            <see cref="M:Graphics.Point.Move(System.Int32,System.Int32)"/>
        </member>

        <member name="M:Graphics.Point.Equals(System.Object)">
            <summary>This method determines whether two Points have the same
            location.</summary>
            <param><c>o</c> is the object to be compared to the current
            object.
            </param>
            <returns>True if the Points have the same location and they have
            the exact same type; otherwise, false.</returns>
            <seealso
      cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
            <seealso
      cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member name="M:Graphics.Point.ToString">
            <summary>Report a point's location as a string.</summary>
            <returns>A string representing a point's location, in the form
            (x,y),
            without any leading, training, or embedded whitespace.</returns>
        </member>

        <member
       name="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)">
            <summary>This operator determines whether two Points have the
            same
            location.</summary>
            <param><c>p1</c> is the first Point to be compared.</param>
            <param><c>p2</c> is the second Point to be compared.</param>
            <returns>True if the Points have the same location and they have
            the exact same type; otherwise, false.</returns>
            <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
            <seealso
     cref="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member
      name="M:Graphics.Point.op_Inequality(Graphics.Point,Graphics.Point)">
            <summary>This operator determines whether two Points have the
            same
            location.</summary>
            <param><c>p1</c> is the first Point to be compared.</param>
            <param><c>p2</c> is the second Point to be compared.</param>
            <returns>True if the Points do not have the same location and
            the
            exact same type; otherwise, false.</returns>
            <seealso cref="M:Graphics.Point.Equals(System.Object)"/>
            <seealso
      cref="M:Graphics.Point.op_Equality(Graphics.Point,Graphics.Point)"/>
        </member>

        <member name="M:Graphics.Point.Main">
            <summary>This is the entry point of the Point class testing
            program.
            <para>This program tests each method and operator, and
            is intended to be run after any non-trivial maintenance has
            been performed on the Point class.</para></summary>
        </member>

        <member name="P:Graphics.Point.X">
            <value>Property <c>X</c> represents the point's
            x-coordinate.</value>
        </member>

        <member name="P:Graphics.Point.Y">
            <value>Property <c>Y</c> represents the point's
            y-coordinate.</value>
        </member>
    </members>
</doc>
```
