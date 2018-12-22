# <a name="lexical-structure"></a><span data-ttu-id="9e751-101">Лексическая структура</span><span class="sxs-lookup"><span data-stu-id="9e751-101">Lexical structure</span></span>

## <a name="programs"></a><span data-ttu-id="9e751-102">Programs</span><span class="sxs-lookup"><span data-stu-id="9e751-102">Programs</span></span>

<span data-ttu-id="9e751-103">C# ***программы*** состоит из одного или нескольких ***исходные файлы***, которая называется формально ***блоков компиляции*** ([блоков компиляции](namespaces.md#compilation-units)).</span><span class="sxs-lookup"><span data-stu-id="9e751-103">A C# ***program*** consists of one or more ***source files***, known formally as ***compilation units*** ([Compilation units](namespaces.md#compilation-units)).</span></span> <span data-ttu-id="9e751-104">Исходный файл — это упорядоченная последовательность символов Юникода.</span><span class="sxs-lookup"><span data-stu-id="9e751-104">A source file is an ordered sequence of Unicode characters.</span></span> <span data-ttu-id="9e751-105">Исходные файлы обычно имеют однозначное соответствие с файлами в файловой системе, но это соответствие не является обязательным.</span><span class="sxs-lookup"><span data-stu-id="9e751-105">Source files typically have a one-to-one correspondence with files in a file system, but this correspondence is not required.</span></span> <span data-ttu-id="9e751-106">Для максимальной переносимости рекомендуется, что файлы в файловой системе быть закодирован с использованием UTF-8 кодирования.</span><span class="sxs-lookup"><span data-stu-id="9e751-106">For maximal portability, it is recommended that files in a file system be encoded with the UTF-8 encoding.</span></span>

<span data-ttu-id="9e751-107">С концептуальной точки зрения программа компилируется в три этапа:</span><span class="sxs-lookup"><span data-stu-id="9e751-107">Conceptually speaking, a program is compiled using three steps:</span></span>

1. <span data-ttu-id="9e751-108">Преобразование, которое преобразует файл из конкретного набора символов и схемы кодировки в последовательность символов Юникода.</span><span class="sxs-lookup"><span data-stu-id="9e751-108">Transformation, which converts a file from a particular character repertoire and encoding scheme into a sequence of Unicode characters.</span></span>
2. <span data-ttu-id="9e751-109">Лексический анализ преобразует поток входных символов Юникода в поток токенов.</span><span class="sxs-lookup"><span data-stu-id="9e751-109">Lexical analysis, which translates a stream of Unicode input characters into a stream of tokens.</span></span>
3. <span data-ttu-id="9e751-110">Синтаксический анализ преобразует поток лексем в исполняемый код.</span><span class="sxs-lookup"><span data-stu-id="9e751-110">Syntactic analysis, which translates the stream of tokens into executable code.</span></span>

## <a name="grammars"></a><span data-ttu-id="9e751-111">Грамматики</span><span class="sxs-lookup"><span data-stu-id="9e751-111">Grammars</span></span>

<span data-ttu-id="9e751-112">Эта спецификация представлен синтаксис языка программирования C# с помощью двух грамматики.</span><span class="sxs-lookup"><span data-stu-id="9e751-112">This specification presents the syntax of the C# programming language using two grammars.</span></span> <span data-ttu-id="9e751-113">***Лексическая грамматика*** ([лексическая грамматика](lexical-structure.md#lexical-grammar)) определяет, как символы Юникода объединяются для формы признаки конца строки, пробелы, комментарии, токены и директивы предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="9e751-113">The ***lexical grammar*** ([Lexical grammar](lexical-structure.md#lexical-grammar)) defines how Unicode characters are combined to form line terminators, white space, comments, tokens, and pre-processing directives.</span></span> <span data-ttu-id="9e751-114">***Синтаксическая грамматика*** ([Синтаксическая грамматика](lexical-structure.md#syntactic-grammar)) определяет, как маркеры, полученные в результате лексическая грамматика объединяются для формирования C# программ.</span><span class="sxs-lookup"><span data-stu-id="9e751-114">The ***syntactic grammar*** ([Syntactic grammar](lexical-structure.md#syntactic-grammar)) defines how the tokens resulting from the lexical grammar are combined to form C# programs.</span></span>

### <a name="grammar-notation"></a><span data-ttu-id="9e751-115">Грамматическая нотация</span><span class="sxs-lookup"><span data-stu-id="9e751-115">Grammar notation</span></span>

<span data-ttu-id="9e751-116">Грамматики лексическую и синтаксическую представлены в форме Бэкуса-Наура, с помощью нотации средство ANTLR грамматики.</span><span class="sxs-lookup"><span data-stu-id="9e751-116">The lexical and syntactic grammars are presented in Backus-Naur form using the notation of the ANTLR grammar tool.</span></span>

### <a name="lexical-grammar"></a><span data-ttu-id="9e751-117">Лексическая грамматика</span><span class="sxs-lookup"><span data-stu-id="9e751-117">Lexical grammar</span></span>

<span data-ttu-id="9e751-118">Лексическая грамматика C# представлены в [Лексический анализ](lexical-structure.md#lexical-analysis), [маркеры](lexical-structure.md#tokens), и [директивы предварительной обработки](lexical-structure.md#pre-processing-directives).</span><span class="sxs-lookup"><span data-stu-id="9e751-118">The lexical grammar of C# is presented in [Lexical analysis](lexical-structure.md#lexical-analysis), [Tokens](lexical-structure.md#tokens), and [Pre-processing directives](lexical-structure.md#pre-processing-directives).</span></span> <span data-ttu-id="9e751-119">Терминалов символы лексическая грамматика символов кодировки Юникод, и лексическая грамматика определяет, как символы объединяются для формирования лексем ([маркеры](lexical-structure.md#tokens)), пробел ([пустое пространство](lexical-structure.md#white-space)), комментарии ([комментарии](lexical-structure.md#comments)) и директивы предварительной обработки ([директивы предварительной обработки](lexical-structure.md#pre-processing-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-119">The terminal symbols of the lexical grammar are the characters of the Unicode character set, and the lexical grammar specifies how characters are combined to form tokens ([Tokens](lexical-structure.md#tokens)), white space ([White space](lexical-structure.md#white-space)), comments ([Comments](lexical-structure.md#comments)), and pre-processing directives ([Pre-processing directives](lexical-structure.md#pre-processing-directives)).</span></span>

<span data-ttu-id="9e751-120">Каждый исходный файл программы на C# должны соответствовать *входной* производства лексическая грамматика ([Лексический анализ](lexical-structure.md#lexical-analysis)).</span><span class="sxs-lookup"><span data-stu-id="9e751-120">Every source file in a C# program must conform to the *input* production of the lexical grammar ([Lexical analysis](lexical-structure.md#lexical-analysis)).</span></span>

### <a name="syntactic-grammar"></a><span data-ttu-id="9e751-121">Синтаксическая грамматика</span><span class="sxs-lookup"><span data-stu-id="9e751-121">Syntactic grammar</span></span>

<span data-ttu-id="9e751-122">Синтаксическая грамматика C# представлены в главах и приложениях, выполните указания в этой главе.</span><span class="sxs-lookup"><span data-stu-id="9e751-122">The syntactic grammar of C# is presented in the chapters and appendices that follow this chapter.</span></span> <span data-ttu-id="9e751-123">Используются токены, определяется лексическая грамматика терминалов символы синтаксической грамматики и Синтаксическая грамматика определяет, как маркеры объединяются для программ на C# формы.</span><span class="sxs-lookup"><span data-stu-id="9e751-123">The terminal symbols of the syntactic grammar are the tokens defined by the lexical grammar, and the syntactic grammar specifies how tokens are combined to form C# programs.</span></span>

<span data-ttu-id="9e751-124">Каждый исходный файл C# программы должны соответствовать *compilation_unit* производства Синтаксическая грамматика ([блоков компиляции](namespaces.md#compilation-units)).</span><span class="sxs-lookup"><span data-stu-id="9e751-124">Every source file in a C# program must conform to the *compilation_unit* production of the syntactic grammar ([Compilation units](namespaces.md#compilation-units)).</span></span>

## <a name="lexical-analysis"></a><span data-ttu-id="9e751-125">Лексический анализ</span><span class="sxs-lookup"><span data-stu-id="9e751-125">Lexical analysis</span></span>

<span data-ttu-id="9e751-126">*Входной* рабочей определяет Лексическая структура исходного файла C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-126">The *input* production defines the lexical structure of a C# source file.</span></span> <span data-ttu-id="9e751-127">В рабочей среде этот лексическая грамматика должен соответствовать каждый исходный файл в программе на C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-127">Each source file in a C# program must conform to this lexical grammar production.</span></span>

```antlr
input
    : input_section?
    ;

input_section
    : input_section_part+
    ;

input_section_part
    : input_element* new_line
    | pp_directive
    ;

input_element
    : whitespace
    | comment
    | token
    ;
```

<span data-ttu-id="9e751-128">Пять основных элементов, составляющих Лексическая структура C# исходный файл: Признаки конца строки ([символов признака конца строки](lexical-structure.md#line-terminators)), пробел ([пробелы](lexical-structure.md#white-space)), комментарии ([комментарии](lexical-structure.md#comments)), маркеры ([маркеры](lexical-structure.md#tokens)), и директивы предварительной обработки ([директивы предварительной обработки](lexical-structure.md#pre-processing-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-128">Five basic elements make up the lexical structure of a C# source file: Line terminators ([Line terminators](lexical-structure.md#line-terminators)), white space ([White space](lexical-structure.md#white-space)), comments ([Comments](lexical-structure.md#comments)), tokens ([Tokens](lexical-structure.md#tokens)), and pre-processing directives ([Pre-processing directives](lexical-structure.md#pre-processing-directives)).</span></span> <span data-ttu-id="9e751-129">Из этих основных элементов учитываются только токены в синтаксис программы на C# ([Синтаксическая грамматика](lexical-structure.md#syntactic-grammar)).</span><span class="sxs-lookup"><span data-stu-id="9e751-129">Of these basic elements, only tokens are significant in the syntactic grammar of a C# program ([Syntactic grammar](lexical-structure.md#syntactic-grammar)).</span></span>

<span data-ttu-id="9e751-130">Лексическая обработка исходным файлом C# состоит из файла в последовательность токенов, который становятся входными данными для синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="9e751-130">The lexical processing of a C# source file consists of reducing the file into a sequence of tokens which becomes the input to the syntactic analysis.</span></span> <span data-ttu-id="9e751-131">Признаки конца строки, пробелы и комментарии можно использовать для разделения лексем, директивы предварительной обработки может привести к части исходного файла, которые нужно пропустить, а в противном случае эти лексические элементы не оказывают влияния на синтаксической структуры программы на C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-131">Line terminators, white space, and comments can serve to separate tokens, and pre-processing directives can cause sections of the source file to be skipped, but otherwise these lexical elements have no impact on the syntactic structure of a C# program.</span></span>

<span data-ttu-id="9e751-132">В случае интерполированные строковые литералы ([интерполированные строковые литералы](lexical-structure.md#interpolated-string-literals)) один токен, изначально созданные лексического анализа, но разбивается на несколько входных элементов, которые многократно подвергались Лексический анализ пока все интерполированные строковые литералы, были устранены.</span><span class="sxs-lookup"><span data-stu-id="9e751-132">In the case of interpolated string literals ([Interpolated string literals](lexical-structure.md#interpolated-string-literals)) a single token is initially produced by lexical analysis, but is broken up into several input elements which are repeatedly subjected to lexical analysis until all interpolated string literals have been resolved.</span></span> <span data-ttu-id="9e751-133">Полученных маркеров выступать в качестве входных данных для синтаксического анализа.</span><span class="sxs-lookup"><span data-stu-id="9e751-133">The resulting tokens then serve as input to the syntactic analysis.</span></span>

<span data-ttu-id="9e751-134">Когда несколько производств лексическая грамматика соответствует последовательности символов в исходном файле, Лексическая обработка всегда создает длинный возможный лексический элемент.</span><span class="sxs-lookup"><span data-stu-id="9e751-134">When several lexical grammar productions match a sequence of characters in a source file, the lexical processing always forms the longest possible lexical element.</span></span> <span data-ttu-id="9e751-135">Например, последовательность знаков `//` обрабатывается как начало однострочного комментария, так как этот лексический элемент длиннее, чем один `/` токена.</span><span class="sxs-lookup"><span data-stu-id="9e751-135">For example, the character sequence `//` is processed as the beginning of a single-line comment because that lexical element is longer than a single `/` token.</span></span>

### <a name="line-terminators"></a><span data-ttu-id="9e751-136">Признаки конца строки</span><span class="sxs-lookup"><span data-stu-id="9e751-136">Line terminators</span></span>

<span data-ttu-id="9e751-137">Признаки конца строки символов исходного файла C# разбивается на строки.</span><span class="sxs-lookup"><span data-stu-id="9e751-137">Line terminators divide the characters of a C# source file into lines.</span></span>

```antlr
new_line
    : '<Carriage return character (U+000D)>'
    | '<Line feed character (U+000A)>'
    | '<Carriage return character (U+000D) followed by line feed character (U+000A)>'
    | '<Next line character (U+0085)>'
    | '<Line separator character (U+2028)>'
    | '<Paragraph separator character (U+2029)>'
    ;
```

<span data-ttu-id="9e751-138">Для совместимости с исходного кода средства редактирования, которые добавляют маркеры конец файла, и включить источник файл, чтобы просмотреть в виде последовательности правильно завершенных строк, применяются следующие преобразования, в порядке, каждый файл исходного кода в программе на C#:</span><span class="sxs-lookup"><span data-stu-id="9e751-138">For compatibility with source code editing tools that add end-of-file markers, and to enable a source file to be viewed as a sequence of properly terminated lines, the following transformations are applied, in order, to every source file in a C# program:</span></span>

*  <span data-ttu-id="9e751-139">Если последний символ исходного файла является символ CTRL + Z (`U+001A`), этот символ будет удален.</span><span class="sxs-lookup"><span data-stu-id="9e751-139">If the last character of the source file is a Control-Z character (`U+001A`), this character is deleted.</span></span>
*  <span data-ttu-id="9e751-140">Символ возврата каретки (`U+000D`) добавляется в конец исходного файла, если этот исходный файл не является пустым и последним символом исходного файла не является символ возврата каретки (`U+000D`), перевода строки (`U+000A`), разделитель (`U+2028`), или разделителем абзацев (`U+2029`).</span><span class="sxs-lookup"><span data-stu-id="9e751-140">A carriage-return character (`U+000D`) is added to the end of the source file if that source file is non-empty and if the last character of the source file is not a carriage return (`U+000D`), a line feed (`U+000A`), a line separator (`U+2028`), or a paragraph separator (`U+2029`).</span></span>

### <a name="comments"></a><span data-ttu-id="9e751-141">Комментарии</span><span class="sxs-lookup"><span data-stu-id="9e751-141">Comments</span></span>

<span data-ttu-id="9e751-142">Поддерживаются два вида примечаний: однострочные комментарии и комментарии с разделителями.</span><span class="sxs-lookup"><span data-stu-id="9e751-142">Two forms of comments are supported: single-line comments and delimited comments.</span></span> <span data-ttu-id="9e751-143">***Однострочные комментарии*** начинаются с символов `//` и расширить его в конец исходной строки.</span><span class="sxs-lookup"><span data-stu-id="9e751-143">***Single-line comments*** start with the characters `//` and extend to the end of the source line.</span></span> <span data-ttu-id="9e751-144">***Комментарии с разделителями*** начинаются с символов `/*` и заканчиваются символами `*/`.</span><span class="sxs-lookup"><span data-stu-id="9e751-144">***Delimited comments*** start with the characters `/*` and end with the characters `*/`.</span></span> <span data-ttu-id="9e751-145">С разделителями комментарии могут занимать несколько строк.</span><span class="sxs-lookup"><span data-stu-id="9e751-145">Delimited comments may span multiple lines.</span></span>

```antlr
comment
    : single_line_comment
    | delimited_comment
    ;

single_line_comment
    : '//' input_character*
    ;

input_character
    : '<Any Unicode character except a new_line_character>'
    ;

new_line_character
    : '<Carriage return character (U+000D)>'
    | '<Line feed character (U+000A)>'
    | '<Next line character (U+0085)>'
    | '<Line separator character (U+2028)>'
    | '<Paragraph separator character (U+2029)>'
    ;

delimited_comment
    : '/*' delimited_comment_section* asterisk* '/'
    ;

delimited_comment_section
    : '/'
    | asterisk* not_slash_or_asterisk
    ;

asterisk
    : '*'
    ;

not_slash_or_asterisk
    : '<Any Unicode character except / or *>'
    ;
```

<span data-ttu-id="9e751-146">Комментарии не могут быть вложенными.</span><span class="sxs-lookup"><span data-stu-id="9e751-146">Comments do not nest.</span></span> <span data-ttu-id="9e751-147">Последовательности символов `/*` и `*/` не имеют особого значения в пределах `//` комментарий и последовательности символов `//` и `/*` не имеют особого значения с разделителями комментария.</span><span class="sxs-lookup"><span data-stu-id="9e751-147">The character sequences `/*` and `*/` have no special meaning within a `//` comment, and the character sequences `//` and `/*` have no special meaning within a delimited comment.</span></span>

<span data-ttu-id="9e751-148">Комментарии, не обрабатываются в символьные и строковые литералы.</span><span class="sxs-lookup"><span data-stu-id="9e751-148">Comments are not processed within character and string literals.</span></span>

<span data-ttu-id="9e751-149">Пример</span><span class="sxs-lookup"><span data-stu-id="9e751-149">The example</span></span>
```csharp
/* Hello, world program
   This program writes "hello, world" to the console
*/
class Hello
{
    static void Main() {
        System.Console.WriteLine("hello, world");
    }
}
```
<span data-ttu-id="9e751-150">содержит комментарий с разделителями.</span><span class="sxs-lookup"><span data-stu-id="9e751-150">includes a delimited comment.</span></span>

<span data-ttu-id="9e751-151">Пример</span><span class="sxs-lookup"><span data-stu-id="9e751-151">The example</span></span>
```csharp
// Hello, world program
// This program writes "hello, world" to the console
//
class Hello // any name will do for this class
{
    static void Main() { // this method must be named "Main"
        System.Console.WriteLine("hello, world");
    }
}
```
<span data-ttu-id="9e751-152">показано несколько однострочных комментариев.</span><span class="sxs-lookup"><span data-stu-id="9e751-152">shows several single-line comments.</span></span>

### <a name="white-space"></a><span data-ttu-id="9e751-153">Пробел</span><span class="sxs-lookup"><span data-stu-id="9e751-153">White space</span></span>

<span data-ttu-id="9e751-154">Пустое пространство определяется как символ перевода любой символ Юникода класса Zs (который включает символ пробела), а также символ горизонтальной табуляции, символ вертикальной табуляции и формы.</span><span class="sxs-lookup"><span data-stu-id="9e751-154">White space is defined as any character with Unicode class Zs (which includes the space character) as well as the horizontal tab character, the vertical tab character, and the form feed character.</span></span>

```antlr
whitespace
    : '<Any character with Unicode class Zs>'
    | '<Horizontal tab character (U+0009)>'
    | '<Vertical tab character (U+000B)>'
    | '<Form feed character (U+000C)>'
    ;
```

## <a name="tokens"></a><span data-ttu-id="9e751-155">лексемы</span><span class="sxs-lookup"><span data-stu-id="9e751-155">Tokens</span></span>

<span data-ttu-id="9e751-156">Существует несколько типов токенов: идентификаторы, ключевые слова, литералы, операторы и символы пунктуации.</span><span class="sxs-lookup"><span data-stu-id="9e751-156">There are several kinds of tokens: identifiers, keywords, literals, operators, and punctuators.</span></span> <span data-ttu-id="9e751-157">Пробелы и комментарии не являются лексемами, хотя действуют как разделители для маркеров.</span><span class="sxs-lookup"><span data-stu-id="9e751-157">White space and comments are not tokens, though they act as separators for tokens.</span></span>

```antlr
token
    : identifier
    | keyword
    | integer_literal
    | real_literal
    | character_literal
    | string_literal
    | interpolated_string_literal
    | operator_or_punctuator
    ;
```

### <a name="unicode-character-escape-sequences"></a><span data-ttu-id="9e751-158">Escape-последовательности символов Юникода</span><span class="sxs-lookup"><span data-stu-id="9e751-158">Unicode character escape sequences</span></span>

<span data-ttu-id="9e751-159">Управляющая последовательность символов Юникода представляет символ Юникода.</span><span class="sxs-lookup"><span data-stu-id="9e751-159">A Unicode character escape sequence represents a Unicode character.</span></span> <span data-ttu-id="9e751-160">Escape-последовательности символов Юникода обрабатываются в идентификаторах ([идентификаторы](lexical-structure.md#identifiers)), символьные литералы ([символьные литералы](lexical-structure.md#character-literals)) и строковые литералы regular ([строковые литералы](lexical-structure.md#string-literals)).</span><span class="sxs-lookup"><span data-stu-id="9e751-160">Unicode character escape sequences are processed in identifiers ([Identifiers](lexical-structure.md#identifiers)), character literals ([Character literals](lexical-structure.md#character-literals)), and regular string literals ([String literals](lexical-structure.md#string-literals)).</span></span> <span data-ttu-id="9e751-161">Escape-символ Юникода не обрабатывается в любом другом месте (например, для формирования оператор символ пунктуации и ключевое слово).</span><span class="sxs-lookup"><span data-stu-id="9e751-161">A Unicode character escape is not processed in any other location (for example, to form an operator, punctuator, or keyword).</span></span>

```antlr
unicode_escape_sequence
    : '\\u' hex_digit hex_digit hex_digit hex_digit
    | '\\U' hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit
    ;
```

<span data-ttu-id="9e751-162">Escape-последовательность Юникода представляет один знак Юникода, образованное шестнадцатеричный номер после "`\u`«или»`\U`" символов.</span><span class="sxs-lookup"><span data-stu-id="9e751-162">A Unicode escape sequence represents the single Unicode character formed by the hexadecimal number following the "`\u`" or "`\U`" characters.</span></span> <span data-ttu-id="9e751-163">Так как в C# используется 16-разрядная кодировка кодовых позиций Юникода в символы и строковые значения, символ Юникода в диапазоне от U + 10000 до U + 10FFFF не допускается в символьных литералов и представляется с помощью суррогатной пары Юникода в строковом литерале.</span><span class="sxs-lookup"><span data-stu-id="9e751-163">Since C# uses a 16-bit encoding of Unicode code points in characters and string values, a Unicode character in the range U+10000 to U+10FFFF is not permitted in a character literal and is represented using a Unicode surrogate pair in a string literal.</span></span> <span data-ttu-id="9e751-164">Символы Юникода с элементами кода выше 0x10FFFF не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="9e751-164">Unicode characters with code points above 0x10FFFF are not supported.</span></span>

<span data-ttu-id="9e751-165">Несколько переводов не выполняются.</span><span class="sxs-lookup"><span data-stu-id="9e751-165">Multiple translations are not performed.</span></span> <span data-ttu-id="9e751-166">Например, строковый литерал "`\u005Cu005C`«эквивалентно»`\u005C`«вместо»`\`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-166">For instance, the string literal "`\u005Cu005C`" is equivalent to "`\u005C`" rather than "`\`".</span></span> <span data-ttu-id="9e751-167">Значение в кодировке Юникод `\u005C` — это символ, "`\`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-167">The Unicode value `\u005C` is the character "`\`".</span></span>

<span data-ttu-id="9e751-168">Пример</span><span class="sxs-lookup"><span data-stu-id="9e751-168">The example</span></span>
```csharp
class Class1
{
    static void Test(bool \u0066) {
        char c = '\u0066';
        if (\u0066)
            System.Console.WriteLine(c.ToString());
    }        
}
```
<span data-ttu-id="9e751-169">показаны несколько способов применения `\u0066`, который является escape-последовательность для письма "`f`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-169">shows several uses of `\u0066`, which is the escape sequence for the letter "`f`".</span></span> <span data-ttu-id="9e751-170">Программа эквивалентно</span><span class="sxs-lookup"><span data-stu-id="9e751-170">The program is equivalent to</span></span>
```csharp
class Class1
{
    static void Test(bool f) {
        char c = 'f';
        if (f)
            System.Console.WriteLine(c.ToString());
    }        
}
```

### <a name="identifiers"></a><span data-ttu-id="9e751-171">Идентификаторы</span><span class="sxs-lookup"><span data-stu-id="9e751-171">Identifiers</span></span>

<span data-ttu-id="9e751-172">Правилам для идентификаторов, приведенный в этом разделе точно соответствуют рекомендованным Unicode Standard Annex 31, за исключением того, что символ подчеркивания допустим в качестве исходного символа (как в традиционных на языке программирования C), являются последовательностей escape-символов Юникода допускается в идентификаторах и "`@`" символ разрешено как префикс включать ключевые слова для использования в качестве идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="9e751-172">The rules for identifiers given in this section correspond exactly to those recommended by the Unicode Standard Annex 31, except that underscore is allowed as an initial character (as is traditional in the C programming language), Unicode escape sequences are permitted in identifiers, and the "`@`" character is allowed as a prefix to enable keywords to be used as identifiers.</span></span>

```antlr
identifier
    : available_identifier
    | '@' identifier_or_keyword
    ;

available_identifier
    : '<An identifier_or_keyword that is not a keyword>'
    ;

identifier_or_keyword
    : identifier_start_character identifier_part_character*
    ;

identifier_start_character
    : letter_character
    | '_'
    ;

identifier_part_character
    : letter_character
    | decimal_digit_character
    | connecting_character
    | combining_character
    | formatting_character
    ;

letter_character
    : '<A Unicode character of classes Lu, Ll, Lt, Lm, Lo, or Nl>'
    | '<A unicode_escape_sequence representing a character of classes Lu, Ll, Lt, Lm, Lo, or Nl>'
    ;

combining_character
    : '<A Unicode character of classes Mn or Mc>'
    | '<A unicode_escape_sequence representing a character of classes Mn or Mc>'
    ;

decimal_digit_character
    : '<A Unicode character of the class Nd>'
    | '<A unicode_escape_sequence representing a character of the class Nd>'
    ;

connecting_character
    : '<A Unicode character of the class Pc>'
    | '<A unicode_escape_sequence representing a character of the class Pc>'
    ;

formatting_character
    : '<A Unicode character of the class Cf>'
    | '<A unicode_escape_sequence representing a character of the class Cf>'
    ;
```

<span data-ttu-id="9e751-173">Сведения о классах символов Юникода, упомянутых выше см. в разделе Стандарт Юникода версии 3.0, раздел 4.5.</span><span class="sxs-lookup"><span data-stu-id="9e751-173">For information on the Unicode character classes mentioned above, see The Unicode Standard, Version 3.0, section 4.5.</span></span>

<span data-ttu-id="9e751-174">Примеры допустимых идентификаторов "`identifier1`«,»`_identifier2`«, и"`@if`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-174">Examples of valid identifiers include "`identifier1`", "`_identifier2`", and "`@if`".</span></span>

<span data-ttu-id="9e751-175">Идентификатор в соответствующей программе должен быть в канонический формат, определяемый формой нормализации Юникода C, в соответствии с определением Unicode Standard Annex 15.</span><span class="sxs-lookup"><span data-stu-id="9e751-175">An identifier in a conforming program must be in the canonical format defined by Unicode Normalization Form C, as defined by Unicode Standard Annex 15.</span></span> <span data-ttu-id="9e751-176">Поведение при обнаружении идентификатора не в форму нормализации C определяется реализацией; Тем не менее Диагностика не требуется.</span><span class="sxs-lookup"><span data-stu-id="9e751-176">The behavior when encountering an identifier not in Normalization Form C is implementation-defined; however, a diagnostic is not required.</span></span>

<span data-ttu-id="9e751-177">Префикс "`@`" позволяет использовать ключевые слова как идентификаторы, что полезно при взаимодействии с другими языками программирования.</span><span class="sxs-lookup"><span data-stu-id="9e751-177">The prefix "`@`" enables the use of keywords as identifiers, which is useful when interfacing with other programming languages.</span></span> <span data-ttu-id="9e751-178">Символ `@` не фактически входит идентификатора, поэтому идентификатор можно рассматривать в других языках в качестве обычного идентификатора, без префикса.</span><span class="sxs-lookup"><span data-stu-id="9e751-178">The character `@` is not actually part of the identifier, so the identifier might be seen in other languages as a normal identifier, without the prefix.</span></span> <span data-ttu-id="9e751-179">Идентификатор с `@` префикс называется ***буквальным идентификатором***.</span><span class="sxs-lookup"><span data-stu-id="9e751-179">An identifier with an `@` prefix is called a ***verbatim identifier***.</span></span> <span data-ttu-id="9e751-180">Использование `@` префикс для идентификаторов, которые не являются ключевые слова, разрешено, но настоятельно не рекомендуется в рамках стиля.</span><span class="sxs-lookup"><span data-stu-id="9e751-180">Use of the `@` prefix for identifiers that are not keywords is permitted, but strongly discouraged as a matter of style.</span></span>

<span data-ttu-id="9e751-181">Пример:</span><span class="sxs-lookup"><span data-stu-id="9e751-181">The example:</span></span>
```csharp
class @class
{
    public static void @static(bool @bool) {
        if (@bool)
            System.Console.WriteLine("true");
        else
            System.Console.WriteLine("false");
    }    
}

class Class1
{
    static void M() {
        cl\u0061ss.st\u0061tic(true);
    }
}
```
<span data-ttu-id="9e751-182">Определяет класс с именем "`class`«со статическим методом с именем»`static`«, принимающий параметр с именем»`bool`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-182">defines a class named "`class`" with a static method named "`static`" that takes a parameter named "`bool`".</span></span> <span data-ttu-id="9e751-183">Обратите внимание, что поскольку escape-последовательности Юникода не разрешены в ключевых слов, токен "`cl\u0061ss`«— это идентификатор, и тем же идентификатором, как»`@class`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-183">Note that since Unicode escapes are not permitted in keywords, the token "`cl\u0061ss`" is an identifier, and is the same identifier as "`@class`".</span></span>

<span data-ttu-id="9e751-184">Два идентификатора считаются одинаковыми, если они были идентичны после следующие преобразования применяются в порядке:</span><span class="sxs-lookup"><span data-stu-id="9e751-184">Two identifiers are considered the same if they are identical after the following transformations are applied, in order:</span></span>

*  <span data-ttu-id="9e751-185">Префикс "`@`«, если используется, удаляется.</span><span class="sxs-lookup"><span data-stu-id="9e751-185">The prefix "`@`", if used, is removed.</span></span>
*  <span data-ttu-id="9e751-186">Каждый *unicode_escape_sequence* преобразуется в соответствующий символ Юникода.</span><span class="sxs-lookup"><span data-stu-id="9e751-186">Each *unicode_escape_sequence* is transformed into its corresponding Unicode character.</span></span>
*  <span data-ttu-id="9e751-187">Любой *formatting_character*s удаляются.</span><span class="sxs-lookup"><span data-stu-id="9e751-187">Any *formatting_character*s are removed.</span></span>

<span data-ttu-id="9e751-188">Идентификаторы, содержащие двух последовательных символы подчеркивания (`U+005F`) зарезервированы для использования в реализации.</span><span class="sxs-lookup"><span data-stu-id="9e751-188">Identifiers containing two consecutive underscore characters (`U+005F`) are reserved for use by the implementation.</span></span> <span data-ttu-id="9e751-189">Например реализация может предоставлять расширенные ключевые слова, которые начинаются с двух символов подчеркивания.</span><span class="sxs-lookup"><span data-stu-id="9e751-189">For example, an implementation might provide extended keywords that begin with two underscores.</span></span>

### <a name="keywords"></a><span data-ttu-id="9e751-190">Ключевые слова</span><span class="sxs-lookup"><span data-stu-id="9e751-190">Keywords</span></span>

<span data-ttu-id="9e751-191">Объект ***ключевое слово*** — это последовательность символов, зарезервирован и не может использоваться как идентификатор зарезервированная `@` символ.</span><span class="sxs-lookup"><span data-stu-id="9e751-191">A ***keyword*** is an identifier-like sequence of characters that is reserved, and cannot be used as an identifier except when prefaced by the `@` character.</span></span>

```antlr
keyword
    : 'abstract' | 'as'       | 'base'       | 'bool'      | 'break'
    | 'byte'     | 'case'     | 'catch'      | 'char'      | 'checked'
    | 'class'    | 'const'    | 'continue'   | 'decimal'   | 'default'
    | 'delegate' | 'do'       | 'double'     | 'else'      | 'enum'
    | 'event'    | 'explicit' | 'extern'     | 'false'     | 'finally'
    | 'fixed'    | 'float'    | 'for'        | 'foreach'   | 'goto'
    | 'if'       | 'implicit' | 'in'         | 'int'       | 'interface'
    | 'internal' | 'is'       | 'lock'       | 'long'      | 'namespace'
    | 'new'      | 'null'     | 'object'     | 'operator'  | 'out'
    | 'override' | 'params'   | 'private'    | 'protected' | 'public'
    | 'readonly' | 'ref'      | 'return'     | 'sbyte'     | 'sealed'
    | 'short'    | 'sizeof'   | 'stackalloc' | 'static'    | 'string'
    | 'struct'   | 'switch'   | 'this'       | 'throw'     | 'true'
    | 'try'      | 'typeof'   | 'uint'       | 'ulong'     | 'unchecked'
    | 'unsafe'   | 'ushort'   | 'using'      | 'virtual'   | 'void'
    | 'volatile' | 'while'
    ;
```

<span data-ttu-id="9e751-192">В некоторых областях грамматики определенных идентификаторов имеют специальное значение, но не являются ключевыми словами.</span><span class="sxs-lookup"><span data-stu-id="9e751-192">In some places in the grammar, specific identifiers have special meaning, but are not keywords.</span></span> <span data-ttu-id="9e751-193">Такие идентификаторы иногда называются «контекстными ключевыми словами».</span><span class="sxs-lookup"><span data-stu-id="9e751-193">Such identifiers are sometimes referred to as "contextual keywords".</span></span> <span data-ttu-id="9e751-194">Например, в объявлении свойства "`get`«и»`set`" идентификаторы имеют особое значение ([методы доступа](classes.md#accessors)).</span><span class="sxs-lookup"><span data-stu-id="9e751-194">For example, within a property declaration, the "`get`" and "`set`" identifiers have special meaning ([Accessors](classes.md#accessors)).</span></span> <span data-ttu-id="9e751-195">Идентификатор, отличных от `get` или `set` , никогда не разрешается в этих расположениях, поэтому такое использование не конфликтует с использования эти слова в качестве идентификаторов.</span><span class="sxs-lookup"><span data-stu-id="9e751-195">An identifier other than `get` or `set` is never permitted in these locations, so this use does not conflict with a use of these words as identifiers.</span></span> <span data-ttu-id="9e751-196">В других случаях, таких как и в случае с идентификатором "`var`" в объявлениях неявно типизированной локальной переменной ([объявления локальных переменных](statements.md#local-variable-declarations)), контекстное ключевое слово может конфликтовать с объявленных имен.</span><span class="sxs-lookup"><span data-stu-id="9e751-196">In other cases, such as with the identifier "`var`" in implicitly typed local variable declarations ([Local variable declarations](statements.md#local-variable-declarations)), a contextual keyword can conflict with declared names.</span></span> <span data-ttu-id="9e751-197">В таком случае объявленное имя имеет приоритет над использование идентификатора в качестве контекстно-зависимое ключевое слово.</span><span class="sxs-lookup"><span data-stu-id="9e751-197">In such cases, the declared name takes precedence over the use of the identifier as a contextual keyword.</span></span>

### <a name="literals"></a><span data-ttu-id="9e751-198">Литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-198">Literals</span></span>

<span data-ttu-id="9e751-199">Объект ***литерала*** является представлением кода исходного значения.</span><span class="sxs-lookup"><span data-stu-id="9e751-199">A ***literal*** is a source code representation of a value.</span></span>

```antlr
literal
    : boolean_literal
    | integer_literal
    | real_literal
    | character_literal
    | string_literal
    | null_literal
    ;
```

#### <a name="boolean-literals"></a><span data-ttu-id="9e751-200">Логические литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-200">Boolean literals</span></span>

<span data-ttu-id="9e751-201">Существуют два значения логического литерала: `true` и `false`.</span><span class="sxs-lookup"><span data-stu-id="9e751-201">There are two boolean literal values: `true` and `false`.</span></span>

```antlr
boolean_literal
    : 'true'
    | 'false'
    ;
```

<span data-ttu-id="9e751-202">Тип *boolean_literal* является `bool`.</span><span class="sxs-lookup"><span data-stu-id="9e751-202">The type of a *boolean_literal* is `bool`.</span></span>

#### <a name="integer-literals"></a><span data-ttu-id="9e751-203">Целочисленные литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-203">Integer literals</span></span>

<span data-ttu-id="9e751-204">Целочисленные литералы используются для записи значения типов `int`, `uint`, `long`, и `ulong`.</span><span class="sxs-lookup"><span data-stu-id="9e751-204">Integer literals are used to write values of types `int`, `uint`, `long`, and `ulong`.</span></span> <span data-ttu-id="9e751-205">Целочисленные литералы имеют две возможных формы: десятичные и шестнадцатеричные.</span><span class="sxs-lookup"><span data-stu-id="9e751-205">Integer literals have two possible forms: decimal and hexadecimal.</span></span>

```antlr
integer_literal
    : decimal_integer_literal
    | hexadecimal_integer_literal
    ;

decimal_integer_literal
    : decimal_digit+ integer_type_suffix?
    ;

decimal_digit
    : '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
    ;

integer_type_suffix
    : 'U' | 'u' | 'L' | 'l' | 'UL' | 'Ul' | 'uL' | 'ul' | 'LU' | 'Lu' | 'lU' | 'lu'
    ;

hexadecimal_integer_literal
    : '0x' hex_digit+ integer_type_suffix?
    | '0X' hex_digit+ integer_type_suffix?
    ;

hex_digit
    : '0' | '1' | '2' | '3' | '4' | '5' | '6' | '7' | '8' | '9'
    | 'A' | 'B' | 'C' | 'D' | 'E' | 'F' | 'a' | 'b' | 'c' | 'd' | 'e' | 'f';
```

<span data-ttu-id="9e751-206">Тип целочисленного литерала определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e751-206">The type of an integer literal is determined as follows:</span></span>

*  <span data-ttu-id="9e751-207">Если литерал не имеет суффикса, его тип — первый из этих типов, в которых может быть представлено его значение: `int`, `uint`, `long`, `ulong`.</span><span class="sxs-lookup"><span data-stu-id="9e751-207">If the literal has no suffix, it has the first of these types in which its value can be represented: `int`, `uint`, `long`, `ulong`.</span></span>
*  <span data-ttu-id="9e751-208">Если литерал с суффиксом `U` или `u`, его тип — первый из этих типов, в которых может быть представлено его значение: `uint`, `ulong`.</span><span class="sxs-lookup"><span data-stu-id="9e751-208">If the literal is suffixed by `U` or `u`, it has the first of these types in which its value can be represented: `uint`, `ulong`.</span></span>
*  <span data-ttu-id="9e751-209">Если литерал с суффиксом `L` или `l`, его тип — первый из этих типов, в которых может быть представлено его значение: `long`, `ulong`.</span><span class="sxs-lookup"><span data-stu-id="9e751-209">If the literal is suffixed by `L` or `l`, it has the first of these types in which its value can be represented: `long`, `ulong`.</span></span>
*  <span data-ttu-id="9e751-210">Если литерал с суффиксом `UL`, `Ul`, `uL`, `ul`, `LU`, `Lu`, `lU`, или `lu`, он имеет тип `ulong`.</span><span class="sxs-lookup"><span data-stu-id="9e751-210">If the literal is suffixed by `UL`, `Ul`, `uL`, `ul`, `LU`, `Lu`, `lU`, or `lu`, it is of type `ulong`.</span></span>

<span data-ttu-id="9e751-211">Если значение, представленное целочисленным литералом находится вне диапазона `ulong` типа, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-211">If the value represented by an integer literal is outside the range of the `ulong` type, a compile-time error occurs.</span></span>

<span data-ttu-id="9e751-212">Как со стилем, рекомендуется, "`L`«использовано вместо свойства»`l`» при записи литералов типа `long`, так как это легко перепутать буква"`l`«с цифрой»`1`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-212">As a matter of style, it is suggested that "`L`" be used instead of "`l`" when writing literals of type `long`, since it is easy to confuse the letter "`l`" with the digit "`1`".</span></span>

<span data-ttu-id="9e751-213">Чтобы разрешить наименьшим из возможных `int` и `long` значения в виде литералов десятичное целое число, существует два правила:</span><span class="sxs-lookup"><span data-stu-id="9e751-213">To permit the smallest possible `int` and `long` values to be written as decimal integer literals, the following two rules exist:</span></span>

* <span data-ttu-id="9e751-214">Когда *decimal_integer_literal* со значением 2147483648 (2 ^ 31) и не *integer_type_suffix* доступен в качестве маркера, который сразу после "унарный минус" лексема оператора (["унарный минус" оператор](expressions.md#unary-minus-operator)), результатом является константа типа `int` со значением от -2147483648 (-2 ^ 31).</span><span class="sxs-lookup"><span data-stu-id="9e751-214">When a *decimal_integer_literal* with the value 2147483648 (2^31) and no *integer_type_suffix* appears as the token immediately following a unary minus operator token ([Unary minus operator](expressions.md#unary-minus-operator)), the result is a constant of type `int` with the value -2147483648 (-2^31).</span></span> <span data-ttu-id="9e751-215">В других случаях такие *decimal_integer_literal* имеет тип `uint`.</span><span class="sxs-lookup"><span data-stu-id="9e751-215">In all other situations, such a *decimal_integer_literal* is of type `uint`.</span></span>
* <span data-ttu-id="9e751-216">Когда *decimal_integer_literal* со значением 9223372036854775808 (2 ^ 63) и не *integer_type_suffix* или *integer_type_suffix* `L` или `l` доступен в качестве маркера, который сразу после "унарный минус" лексема оператора ([унарный минус-оператор](expressions.md#unary-minus-operator)), результатом является константа типа `long` со значением -9223372036854775808 (-2 ^ 63).</span><span class="sxs-lookup"><span data-stu-id="9e751-216">When a *decimal_integer_literal* with the value 9223372036854775808 (2^63) and no *integer_type_suffix* or the *integer_type_suffix* `L` or `l` appears as the token immediately following a unary minus operator token ([Unary minus operator](expressions.md#unary-minus-operator)), the result is a constant of type `long` with the value -9223372036854775808 (-2^63).</span></span> <span data-ttu-id="9e751-217">В других случаях такие *decimal_integer_literal* имеет тип `ulong`.</span><span class="sxs-lookup"><span data-stu-id="9e751-217">In all other situations, such a *decimal_integer_literal* is of type `ulong`.</span></span>

#### <a name="real-literals"></a><span data-ttu-id="9e751-218">Реальные литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-218">Real literals</span></span>

<span data-ttu-id="9e751-219">Для записи значения типов используются реальные литералы `float`, `double`, и `decimal`.</span><span class="sxs-lookup"><span data-stu-id="9e751-219">Real literals are used to write values of types `float`, `double`, and `decimal`.</span></span>

```antlr
real_literal
    : decimal_digit+ '.' decimal_digit+ exponent_part? real_type_suffix?
    | '.' decimal_digit+ exponent_part? real_type_suffix?
    | decimal_digit+ exponent_part real_type_suffix?
    | decimal_digit+ real_type_suffix
    ;

exponent_part
    : 'e' sign? decimal_digit+
    | 'E' sign? decimal_digit+
    ;

sign
    : '+'
    | '-'
    ;

real_type_suffix
    : 'F' | 'f' | 'D' | 'd' | 'M' | 'm'
    ;
```

<span data-ttu-id="9e751-220">Если не *real_type_suffix* указан, имеет тип действительный литерал `double`.</span><span class="sxs-lookup"><span data-stu-id="9e751-220">If no *real_type_suffix* is specified, the type of the real literal is `double`.</span></span> <span data-ttu-id="9e751-221">В противном случае суффикс действительного типа определяет тип действительный литерал, следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9e751-221">Otherwise, the real type suffix determines the type of the real literal, as follows:</span></span>

*  <span data-ttu-id="9e751-222">Действительный литерал с суффиксом `F` или `f` имеет тип `float`.</span><span class="sxs-lookup"><span data-stu-id="9e751-222">A real literal suffixed by `F` or `f` is of type `float`.</span></span> <span data-ttu-id="9e751-223">Например, литералы `1f`, `1.5f`, `1e10f`, и `123.456F` типа `float`.</span><span class="sxs-lookup"><span data-stu-id="9e751-223">For example, the literals `1f`, `1.5f`, `1e10f`, and `123.456F` are all of type `float`.</span></span>
*  <span data-ttu-id="9e751-224">Действительный литерал с суффиксом `D` или `d` имеет тип `double`.</span><span class="sxs-lookup"><span data-stu-id="9e751-224">A real literal suffixed by `D` or `d` is of type `double`.</span></span> <span data-ttu-id="9e751-225">Например, литералы `1d`, `1.5d`, `1e10d`, и `123.456D` типа `double`.</span><span class="sxs-lookup"><span data-stu-id="9e751-225">For example, the literals `1d`, `1.5d`, `1e10d`, and `123.456D` are all of type `double`.</span></span>
*  <span data-ttu-id="9e751-226">Действительный литерал с суффиксом `M` или `m` имеет тип `decimal`.</span><span class="sxs-lookup"><span data-stu-id="9e751-226">A real literal suffixed by `M` or `m` is of type `decimal`.</span></span> <span data-ttu-id="9e751-227">Например, литералы `1m`, `1.5m`, `1e10m`, и `123.456M` типа `decimal`.</span><span class="sxs-lookup"><span data-stu-id="9e751-227">For example, the literals `1m`, `1.5m`, `1e10m`, and `123.456M` are all of type `decimal`.</span></span> <span data-ttu-id="9e751-228">Этот литерал преобразуется в `decimal` значение точное значение, и, при необходимости округления до ближайшего представимое значение с помощью банковское округление ([десятичного типа](types.md#the-decimal-type)).</span><span class="sxs-lookup"><span data-stu-id="9e751-228">This literal is converted to a `decimal` value by taking the exact value, and, if necessary, rounding to the nearest representable value using banker's rounding ([The decimal type](types.md#the-decimal-type)).</span></span> <span data-ttu-id="9e751-229">Любого масштаба, видимый в литерале сохраняется в том случае, если значение округляется, или значение равно нулю (в этом последнем случае знак и масштаб будет 0).</span><span class="sxs-lookup"><span data-stu-id="9e751-229">Any scale apparent in the literal is preserved unless the value is rounded or the value is zero (in which latter case the sign and scale will be 0).</span></span> <span data-ttu-id="9e751-230">Таким образом литерал `2.900m` будут анализироваться десятичное значение со знаком `0`, коэффициент `2900`и масштаб `3`.</span><span class="sxs-lookup"><span data-stu-id="9e751-230">Hence, the literal `2.900m` will be parsed to form the decimal with sign `0`, coefficient `2900`, and scale `3`.</span></span>

<span data-ttu-id="9e751-231">Если указанный литерал невозможно представить в указанный тип, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-231">If the specified literal cannot be represented in the indicated type, a compile-time error occurs.</span></span>

<span data-ttu-id="9e751-232">Значение действительный литерал типа `float` или `double` определяется с помощью IEEE «округления до ближайшего целого» режим.</span><span class="sxs-lookup"><span data-stu-id="9e751-232">The value of a real literal of type `float` or `double` is determined by using the IEEE "round to nearest" mode.</span></span>

<span data-ttu-id="9e751-233">Обратите внимание, что в действительный литерал, всегда требуется десятичных цифр после десятичной запятой.</span><span class="sxs-lookup"><span data-stu-id="9e751-233">Note that in a real literal, decimal digits are always required after the decimal point.</span></span> <span data-ttu-id="9e751-234">Например `1.3F` — это реальный литерал но `1.F` не является.</span><span class="sxs-lookup"><span data-stu-id="9e751-234">For example, `1.3F` is a real literal but `1.F` is not.</span></span>

#### <a name="character-literals"></a><span data-ttu-id="9e751-235">Символьные литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-235">Character literals</span></span>

<span data-ttu-id="9e751-236">Символьный литерал представляет один символ и обычно состоит из символа в кавычках, как показано на `'a'`.</span><span class="sxs-lookup"><span data-stu-id="9e751-236">A character literal represents a single character, and usually consists of a character in quotes, as in `'a'`.</span></span>

<span data-ttu-id="9e751-237">Примечание. Грамматическая нотация ANTLR делает путаницу!</span><span class="sxs-lookup"><span data-stu-id="9e751-237">Note: The ANTLR grammar notation makes the following confusing!</span></span> <span data-ttu-id="9e751-238">В ANTLR, при написании `\'` это сокращение от одинарная кавычка `'`.</span><span class="sxs-lookup"><span data-stu-id="9e751-238">In ANTLR, when you write `\'` it stands for a single quote `'`.</span></span> <span data-ttu-id="9e751-239">И при написании `\\` это сокращение от одной обратной косой черты `\`.</span><span class="sxs-lookup"><span data-stu-id="9e751-239">And when you write `\\` it stands for a single backslash `\`.</span></span> <span data-ttu-id="9e751-240">Поэтому первое правило для символьного литерала означает, что он начинается с одинарной кавычки, символ, а затем одинарная кавычка.</span><span class="sxs-lookup"><span data-stu-id="9e751-240">Therefore the first rule for a character literal means it starts with a single quote, then a character, then a single quote.</span></span> <span data-ttu-id="9e751-241">И одиннадцать возможных простые escape-последовательности `\'`, `\"`, `\\`, `\0`, `\a`, `\b`, `\f`, `\n`, `\r`, `\t`, `\v`.</span><span class="sxs-lookup"><span data-stu-id="9e751-241">And the eleven possible simple escape sequences are `\'`, `\"`, `\\`, `\0`, `\a`, `\b`, `\f`, `\n`, `\r`, `\t`, `\v`.</span></span>

```antlr
character_literal
    : '\'' character '\''
    ;

character
    : single_character
    | simple_escape_sequence
    | hexadecimal_escape_sequence
    | unicode_escape_sequence
    ;

single_character
    : '<Any character except \' (U+0027), \\ (U+005C), and new_line_character>'
    ;

simple_escape_sequence
    : '\\\'' | '\\"' | '\\\\' | '\\0' | '\\a' | '\\b' | '\\f' | '\\n' | '\\r' | '\\t' | '\\v'
    ;

hexadecimal_escape_sequence
    : '\\x' hex_digit hex_digit? hex_digit? hex_digit?;
```

<span data-ttu-id="9e751-242">Символ, следующий за символом обратной косой черты (`\`) в *символ* должен быть одним из следующих символов: `'`, `"`, `\`, `0`, `a`, `b` , `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span><span class="sxs-lookup"><span data-stu-id="9e751-242">A character that follows a backslash character (`\`) in a *character* must be one of the following characters: `'`, `"`, `\`, `0`, `a`, `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span></span> <span data-ttu-id="9e751-243">В противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-243">Otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="9e751-244">Шестнадцатеричная escape-последовательность представляет один знак Юникода, со значением, образованное шестнадцатеричный номер после "`\x`«.</span><span class="sxs-lookup"><span data-stu-id="9e751-244">A hexadecimal escape sequence represents a single Unicode character, with the value formed by the hexadecimal number following "`\x`".</span></span>

<span data-ttu-id="9e751-245">Если значение, представленное символьный литерал больше, чем `U+FFFF`, возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-245">If the value represented by a character literal is greater than `U+FFFF`, a compile-time error occurs.</span></span>

<span data-ttu-id="9e751-246">Управляющая последовательность символов Юникода ([последовательностей escape-символов Юникода](lexical-structure.md#unicode-character-escape-sequences)) в строковом литерале должно быть в диапазоне `U+0000` для `U+FFFF`.</span><span class="sxs-lookup"><span data-stu-id="9e751-246">A Unicode character escape sequence ([Unicode character escape sequences](lexical-structure.md#unicode-character-escape-sequences)) in a character literal must be in the range `U+0000` to `U+FFFF`.</span></span>

<span data-ttu-id="9e751-247">Простая управляющая последовательность представляет кодировку символов Юникода, как описано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="9e751-247">A simple escape sequence represents a Unicode character encoding, as described in the table below.</span></span>


| <span data-ttu-id="9e751-248">__Escape-последовательность__</span><span class="sxs-lookup"><span data-stu-id="9e751-248">__Escape sequence__</span></span> | <span data-ttu-id="9e751-249">__Имя символа__</span><span class="sxs-lookup"><span data-stu-id="9e751-249">__Character name__</span></span> | <span data-ttu-id="9e751-250">__Кодировка Юникод__</span><span class="sxs-lookup"><span data-stu-id="9e751-250">__Unicode encoding__</span></span> |
|---------------------|--------------------|----------------------|
| `\'`                | <span data-ttu-id="9e751-251">Одинарная кавычка</span><span class="sxs-lookup"><span data-stu-id="9e751-251">Single quote</span></span>       | `0x0027`             | 
| `\"`                | <span data-ttu-id="9e751-252">Двойная кавычка</span><span class="sxs-lookup"><span data-stu-id="9e751-252">Double quote</span></span>       | `0x0022`             | 
| `\\`                | <span data-ttu-id="9e751-253">Обратная косая черта</span><span class="sxs-lookup"><span data-stu-id="9e751-253">Backslash</span></span>          | `0x005C`             | 
| `\0`                | <span data-ttu-id="9e751-254">Null</span><span class="sxs-lookup"><span data-stu-id="9e751-254">Null</span></span>               | `0x0000`             | 
| `\a`                | <span data-ttu-id="9e751-255">Предупреждение</span><span class="sxs-lookup"><span data-stu-id="9e751-255">Alert</span></span>              | `0x0007`             | 
| `\b`                | <span data-ttu-id="9e751-256">Backspace</span><span class="sxs-lookup"><span data-stu-id="9e751-256">Backspace</span></span>          | `0x0008`             | 
| `\f`                | <span data-ttu-id="9e751-257">Перевод страницы</span><span class="sxs-lookup"><span data-stu-id="9e751-257">Form feed</span></span>          | `0x000C`             | 
| `\n`                | <span data-ttu-id="9e751-258">Новая строка</span><span class="sxs-lookup"><span data-stu-id="9e751-258">New line</span></span>           | `0x000A`             | 
| `\r`                | <span data-ttu-id="9e751-259">Возврат каретки</span><span class="sxs-lookup"><span data-stu-id="9e751-259">Carriage return</span></span>    | `0x000D`             | 
| `\t`                | <span data-ttu-id="9e751-260">Горизонтальная табуляция</span><span class="sxs-lookup"><span data-stu-id="9e751-260">Horizontal tab</span></span>     | `0x0009`             | 
| `\v`                | <span data-ttu-id="9e751-261">Вертикальная табуляция</span><span class="sxs-lookup"><span data-stu-id="9e751-261">Vertical tab</span></span>       | `0x000B`             | 

<span data-ttu-id="9e751-262">Тип *character_literal* является `char`.</span><span class="sxs-lookup"><span data-stu-id="9e751-262">The type of a *character_literal* is `char`.</span></span>

#### <a name="string-literals"></a><span data-ttu-id="9e751-263">Строковые литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-263">String literals</span></span>

<span data-ttu-id="9e751-264">C# поддерживает два вида строковых литералов: ***строковые литералы regular*** и ***строковые литералы verbatim***.</span><span class="sxs-lookup"><span data-stu-id="9e751-264">C# supports two forms of string literals: ***regular string literals*** and ***verbatim string literals***.</span></span>

<span data-ttu-id="9e751-265">Обычный строковый литерал состоит из нуля или более символов, заключенные в двойные кавычки, как показано на `"hello"`и могут содержаться оба простые escape-последовательности (например `\t` символа табуляции) и в шестнадцатеричном формате, так и в escape-последовательности Юникода.</span><span class="sxs-lookup"><span data-stu-id="9e751-265">A regular string literal consists of zero or more characters enclosed in double quotes, as in `"hello"`, and may include both simple escape sequences (such as `\t` for the tab character), and hexadecimal and Unicode escape sequences.</span></span>

<span data-ttu-id="9e751-266">Буквальный строковый литерал состоит из `@` символ за которым следует символ двойной кавычки, ноль или более символов и закрывающего символа двойной кавычки.</span><span class="sxs-lookup"><span data-stu-id="9e751-266">A verbatim string literal consists of an `@` character followed by a double-quote character, zero or more characters, and a closing double-quote character.</span></span> <span data-ttu-id="9e751-267">Ниже приведен простой пример `@"hello"`.</span><span class="sxs-lookup"><span data-stu-id="9e751-267">A simple example is `@"hello"`.</span></span> <span data-ttu-id="9e751-268">В буквального строкового литерала, символы между разделителями интерпретируются буквально, единственное исключение, *quote_escape_sequence*.</span><span class="sxs-lookup"><span data-stu-id="9e751-268">In a verbatim string literal, the characters between the delimiters are interpreted verbatim, the only exception being a *quote_escape_sequence*.</span></span> <span data-ttu-id="9e751-269">В частности простые escape-последовательности и шестнадцатеричном формате и escape-последовательности Юникода, не обрабатываются в строковые литералы verbatim.</span><span class="sxs-lookup"><span data-stu-id="9e751-269">In particular, simple escape sequences, and hexadecimal and Unicode escape sequences are not processed in verbatim string literals.</span></span> <span data-ttu-id="9e751-270">Буквальный строковый литерал может занимать несколько строк.</span><span class="sxs-lookup"><span data-stu-id="9e751-270">A verbatim string literal may span multiple lines.</span></span>

```antlr
string_literal
    : regular_string_literal
    | verbatim_string_literal
    ;

regular_string_literal
    : '"' regular_string_literal_character* '"'
    ;

regular_string_literal_character
    : single_regular_string_literal_character
    | simple_escape_sequence
    | hexadecimal_escape_sequence
    | unicode_escape_sequence
    ;

single_regular_string_literal_character
    : '<Any character except " (U+0022), \\ (U+005C), and new_line_character>'
    ;

verbatim_string_literal
    : '@"' verbatim_string_literal_character* '"'
    ;

verbatim_string_literal_character
    : single_verbatim_string_literal_character
    | quote_escape_sequence
    ;

single_verbatim_string_literal_character
    : '<any character except ">'
    ;

quote_escape_sequence
    : '""'
    ;
```

<span data-ttu-id="9e751-271">Символ, следующий за символом обратной косой черты (`\`) в *regular_string_literal_character* должен быть одним из следующих символов: `'`, `"`, `\`, `0`, `a` , `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span><span class="sxs-lookup"><span data-stu-id="9e751-271">A character that follows a backslash character (`\`) in a *regular_string_literal_character* must be one of the following characters: `'`, `"`, `\`, `0`, `a`, `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`.</span></span> <span data-ttu-id="9e751-272">В противном случае возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-272">Otherwise, a compile-time error occurs.</span></span>

<span data-ttu-id="9e751-273">Пример</span><span class="sxs-lookup"><span data-stu-id="9e751-273">The example</span></span>
```csharp
string a = "hello, world";                   // hello, world
string b = @"hello, world";                  // hello, world

string c = "hello \t world";                 // hello      world
string d = @"hello \t world";                // hello \t world

string e = "Joe said \"Hello\" to me";       // Joe said "Hello" to me
string f = @"Joe said ""Hello"" to me";      // Joe said "Hello" to me

string g = "\\\\server\\share\\file.txt";    // \\server\share\file.txt
string h = @"\\server\share\file.txt";       // \\server\share\file.txt

string i = "one\r\ntwo\r\nthree";
string j = @"one
two
three";
```
<span data-ttu-id="9e751-274">содержит различные строковые литералы.</span><span class="sxs-lookup"><span data-stu-id="9e751-274">shows a variety of string literals.</span></span> <span data-ttu-id="9e751-275">Последний строковый литерал, `j`, является буквального строкового литерала, занимает несколько строк.</span><span class="sxs-lookup"><span data-stu-id="9e751-275">The last string literal, `j`, is a verbatim string literal that spans multiple lines.</span></span> <span data-ttu-id="9e751-276">Символы в кавычках, включая пробелы, например символы новой строки, сохраняются буквально.</span><span class="sxs-lookup"><span data-stu-id="9e751-276">The characters between the quotation marks, including white space such as new line characters, are preserved verbatim.</span></span>

<span data-ttu-id="9e751-277">Поскольку Шестнадцатеричная escape-последовательность может иметь переменное число шестнадцатеричных цифр, строковый литерал `"\x123"` содержит один символ с шестнадцатеричным значением 123.</span><span class="sxs-lookup"><span data-stu-id="9e751-277">Since a hexadecimal escape sequence can have a variable number of hex digits, the string literal `"\x123"` contains a single character with hex value 123.</span></span> <span data-ttu-id="9e751-278">Чтобы создать строку, содержащую символ с шестнадцатеричным значением 12, за которым следует символ 3, можно написать `"\x00123"` или `"\x12" + "3"` вместо этого.</span><span class="sxs-lookup"><span data-stu-id="9e751-278">To create a string containing the character with hex value 12 followed by the character 3, one could write `"\x00123"` or `"\x12" + "3"` instead.</span></span>

<span data-ttu-id="9e751-279">Тип *string_literal* является `string`.</span><span class="sxs-lookup"><span data-stu-id="9e751-279">The type of a *string_literal* is `string`.</span></span>

<span data-ttu-id="9e751-280">Каждый строковый литерал не обязательно приводит в новом экземпляре строки.</span><span class="sxs-lookup"><span data-stu-id="9e751-280">Each string literal does not necessarily result in a new string instance.</span></span> <span data-ttu-id="9e751-281">Когда два или несколько строковых литералов, которые эквивалентны в соответствии с оператор равенства строк ([строковые операторы равенства](expressions.md#string-equality-operators)) отображаются в той же программе, см. такие строковые литералы к тому же экземпляру строки.</span><span class="sxs-lookup"><span data-stu-id="9e751-281">When two or more string literals that are equivalent according to the string equality operator ([String equality operators](expressions.md#string-equality-operators)) appear in the same program, these string literals refer to the same string instance.</span></span> <span data-ttu-id="9e751-282">Например выходные данные</span><span class="sxs-lookup"><span data-stu-id="9e751-282">For instance, the output produced by</span></span>
```csharp
class Test
{
    static void Main() {
        object a = "hello";
        object b = "hello";
        System.Console.WriteLine(a == b);
    }
}
```
<span data-ttu-id="9e751-283">является `True` поскольку два литерала ссылаются на один и тот же экземпляр строки.</span><span class="sxs-lookup"><span data-stu-id="9e751-283">is `True` because the two literals refer to the same string instance.</span></span>

#### <a name="interpolated-string-literals"></a><span data-ttu-id="9e751-284">Интерполированные строковые литералы</span><span class="sxs-lookup"><span data-stu-id="9e751-284">Interpolated string literals</span></span>

<span data-ttu-id="9e751-285">Интерполированные строковые литералы похожи на строковые литералы, но содержит пропуски, разделенных `{` и `}`, при котором может возникнуть выражения.</span><span class="sxs-lookup"><span data-stu-id="9e751-285">Interpolated string literals are similar to string literals, but contain holes delimited by `{` and `}`, wherein expressions can occur.</span></span> <span data-ttu-id="9e751-286">Во время выполнения выражения вычисляются с целью с текстовые формы подстановки в строку в месте, где встречается эта брешь в системе.</span><span class="sxs-lookup"><span data-stu-id="9e751-286">At runtime, the expressions are evaluated with the purpose of having their textual forms substituted into the string at the place where the hole occurs.</span></span> <span data-ttu-id="9e751-287">Синтаксис и семантику интерполяция описаны в разделе ([интерполированные строки](expressions.md#interpolated-strings)).</span><span class="sxs-lookup"><span data-stu-id="9e751-287">The syntax and semantics of string interpolation are described in section ([Interpolated strings](expressions.md#interpolated-strings)).</span></span>

<span data-ttu-id="9e751-288">Как и строковые литералы интерполированные строковые литералы может быть обычный или дословно.</span><span class="sxs-lookup"><span data-stu-id="9e751-288">Like string literals, interpolated string literals can be either regular or verbatim.</span></span> <span data-ttu-id="9e751-289">Интерполированные строковые литералы regular разделены с помощью `$"` и `"`, и интерполированные строковые литералы verbatim разделены `$@"` и `"`.</span><span class="sxs-lookup"><span data-stu-id="9e751-289">Interpolated regular string literals are delimited by `$"` and `"`, and interpolated verbatim string literals are delimited by `$@"` and `"`.</span></span>

<span data-ttu-id="9e751-290">Как и другие литералы Лексический анализ интерполированной строки литерала изначально приводит один маркер, согласно ниже грамматики.</span><span class="sxs-lookup"><span data-stu-id="9e751-290">Like other literals, lexical analysis of an interpolated string literal initially results in a single token, as per the grammar below.</span></span> <span data-ttu-id="9e751-291">Тем не менее перед синтаксический анализ один токен интерполированной строки литерала разбивается на несколько токенов для частей строки, включающий слабые места и входных элементов, выполняемых в «дыр» являются лексически анализируются еще раз.</span><span class="sxs-lookup"><span data-stu-id="9e751-291">However, before syntactic analysis, the single token of an interpolated string literal is broken into several tokens for the parts of the string enclosing the holes, and the input elements occurring in the holes are lexically analysed again.</span></span> <span data-ttu-id="9e751-292">Это в свою очередь может привести к более интерполированные строковые литералы для обработки, но, если лексически исправить, в конечном итоге приведет к последовательность токенов для синтаксического анализа для обработки.</span><span class="sxs-lookup"><span data-stu-id="9e751-292">This may in turn produce more interpolated string literals to be processed, but, if lexically correct, will eventually lead to a sequence of tokens for syntactic analysis to process.</span></span>

```antlr
interpolated_string_literal
    : '$' interpolated_regular_string_literal
    | '$' interpolated_verbatim_string_literal
    ;

interpolated_regular_string_literal
    : interpolated_regular_string_whole
    | interpolated_regular_string_start  interpolated_regular_string_literal_body interpolated_regular_string_end
    ;

interpolated_regular_string_literal_body
    : regular_balanced_text
    | interpolated_regular_string_literal_body interpolated_regular_string_mid regular_balanced_text
    ;

interpolated_regular_string_whole
    : '"' interpolated_regular_string_character* '"'
    ;

interpolated_regular_string_start
    : '"' interpolated_regular_string_character* '{'
    ;

interpolated_regular_string_mid
    : interpolation_format? '}' interpolated_regular_string_characters_after_brace? '{'
    ;

interpolated_regular_string_end
    : interpolation_format? '}' interpolated_regular_string_characters_after_brace? '"'
    ;

interpolated_regular_string_characters_after_brace
    : interpolated_regular_string_character_no_brace
    | interpolated_regular_string_characters_after_brace interpolated_regular_string_character
    ;

interpolated_regular_string_character
    : single_interpolated_regular_string_character
    | simple_escape_sequence
    | hexadecimal_escape_sequence
    | unicode_escape_sequence
    | open_brace_escape_sequence
    | close_brace_escape_sequence
    ;

interpolated_regular_string_character_no_brace
    : '<Any interpolated_regular_string_character except close_brace_escape_sequence and any hexadecimal_escape_sequence or unicode_escape_sequence designating } (U+007D)>'
    ;

single_interpolated_regular_string_character
    : '<Any character except \" (U+0022), \\ (U+005C), { (U+007B), } (U+007D), and new_line_character>'
    ;

open_brace_escape_sequence
    : '{{'
    ;

    close_brace_escape_sequence
    : '}}'
    ;
    
regular_balanced_text
    : regular_balanced_text_part+
    ;

regular_balanced_text_part
    : single_regular_balanced_text_character
    | delimited_comment
    | '@' identifier_or_keyword
    | string_literal
    | interpolated_string_literal
    | '(' regular_balanced_text ')'
    | '[' regular_balanced_text ']'
    | '{' regular_balanced_text '}'
    ;
    
single_regular_balanced_text_character
    : '<Any character except / (U+002F), @ (U+0040), \" (U+0022), $ (U+0024), ( (U+0028), ) (U+0029), [ (U+005B), ] (U+005D), { (U+007B), } (U+007D) and new_line_character>'
    | '</ (U+002F), if not directly followed by / (U+002F) or * (U+002A)>'
    ;
    
interpolation_format
    : interpolation_format_character+
    ;
    
interpolation_format_character
    : '<Any character except \" (U+0022), : (U+003A), { (U+007B) and } (U+007D)>'
    ;
    
interpolated_verbatim_string_literal
    : interpolated_verbatim_string_whole
    | interpolated_verbatim_string_start interpolated_verbatim_string_literal_body interpolated_verbatim_string_end
    ;

interpolated_verbatim_string_literal_body
    : verbatim_balanced_text
    | interpolated_verbatim_string_literal_body interpolated_verbatim_string_mid verbatim_balanced_text
    ;
    
interpolated_verbatim_string_whole
    : '@"' interpolated_verbatim_string_character* '"'
    ;
    
interpolated_verbatim_string_start
    : '@"' interpolated_verbatim_string_character* '{'
    ;
    
interpolated_verbatim_string_mid
    : interpolation_format? '}' interpolated_verbatim_string_characters_after_brace? '{'
    ;
    
interpolated_verbatim_string_end
    : interpolation_format? '}' interpolated_verbatim_string_characters_after_brace? '"'
    ;
    
interpolated_verbatim_string_characters_after_brace
    : interpolated_verbatim_string_character_no_brace
    | interpolated_verbatim_string_characters_after_brace interpolated_verbatim_string_character
    ;
    
interpolated_verbatim_string_character
    : single_interpolated_verbatim_string_character
    | quote_escape_sequence
    | open_brace_escape_sequence
    | close_brace_escape_sequence
    ;
    
interpolated_verbatim_string_character_no_brace
    : '<Any interpolated_verbatim_string_character except close_brace_escape_sequence>'
    ;
    
single_interpolated_verbatim_string_character
    : '<Any character except \" (U+0022), { (U+007B) and } (U+007D)>'
    ;
    
verbatim_balanced_text
    : verbatim_balanced_text_part+
    ;

verbatim_balanced_text_part
    : single_verbatim_balanced_text_character
    | comment
    | '@' identifier_or_keyword
    | string_literal
    | interpolated_string_literal
    | '(' verbatim_balanced_text ')'
    | '[' verbatim_balanced_text ']'
    | '{' verbatim_balanced_text '}'
    ;
    
single_verbatim_balanced_text_character
    : '<Any character except / (U+002F), @ (U+0040), \" (U+0022), $ (U+0024), ( (U+0028), ) (U+0029), [ (U+005B), ] (U+005D), { (U+007B) and } (U+007D)>'
    | '</ (U+002F), if not directly followed by / (U+002F) or * (U+002A)>'
    ;
```

<span data-ttu-id="9e751-293">*Interpolated_string_literal* маркер будет интерпретировать как несколько маркеров и других входных элементов как описано ниже, в порядке появления в *interpolated_string_literal*:</span><span class="sxs-lookup"><span data-stu-id="9e751-293">An *interpolated_string_literal* token is reinterpreted as multiple tokens and other input elements as follows, in order of occurrence in the *interpolated_string_literal*:</span></span>

* <span data-ttu-id="9e751-294">Вхождений следующих являются интерпретировать как отдельные отдельных токенов: начальные `$` входа, *interpolated_regular_string_whole*, *interpolated_regular_string_start*, *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_whole*,  *interpolated_verbatim_string_start*, *interpolated_verbatim_string_mid* и *interpolated_verbatim_string_end*.</span><span class="sxs-lookup"><span data-stu-id="9e751-294">Occurrences of the following are reinterpreted as separate individual tokens: the leading `$` sign, *interpolated_regular_string_whole*, *interpolated_regular_string_start*, *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_whole*, *interpolated_verbatim_string_start*, *interpolated_verbatim_string_mid* and *interpolated_verbatim_string_end*.</span></span>
* <span data-ttu-id="9e751-295">Вхождения *regular_balanced_text* и *verbatim_balanced_text* между этими обрабатываются как *input_section* ([Лексический анализ ](lexical-structure.md#lexical-analysis)) и являются интерпретировать как результирующей последовательности элементов ввода.</span><span class="sxs-lookup"><span data-stu-id="9e751-295">Occurrences of *regular_balanced_text* and *verbatim_balanced_text* between these are reprocessed as an *input_section* ([Lexical analysis](lexical-structure.md#lexical-analysis)) and are reinterpreted as the resulting sequence of input elements.</span></span> <span data-ttu-id="9e751-296">В свою очередь, они могут включать интерполированной строки литерала маркеры позволяют интерпретировать.</span><span class="sxs-lookup"><span data-stu-id="9e751-296">These may in turn include interpolated string literal tokens to be reinterpreted.</span></span>

<span data-ttu-id="9e751-297">Синтаксический анализ будет перекомпоновать маркеры в *interpolated_string_expression* ([интерполированные строки](expressions.md#interpolated-strings)).</span><span class="sxs-lookup"><span data-stu-id="9e751-297">Syntactic analysis will recombine the tokens into an *interpolated_string_expression* ([Interpolated strings](expressions.md#interpolated-strings)).</span></span>

<span data-ttu-id="9e751-298">Примеры TODO</span><span class="sxs-lookup"><span data-stu-id="9e751-298">Examples TODO</span></span>


#### <a name="the-null-literal"></a><span data-ttu-id="9e751-299">Литерал null</span><span class="sxs-lookup"><span data-stu-id="9e751-299">The null literal</span></span>

```antlr
null_literal
    : 'null'
    ;
```

<span data-ttu-id="9e751-300">*Null_literal* может быть неявно преобразован в ссылочный тип или тип, допускающий значение NULL.</span><span class="sxs-lookup"><span data-stu-id="9e751-300">The  *null_literal* can be implicitly converted to a reference type or nullable type.</span></span>

### <a name="operators-and-punctuators"></a><span data-ttu-id="9e751-301">Операторы и символы пунктуации</span><span class="sxs-lookup"><span data-stu-id="9e751-301">Operators and punctuators</span></span>

<span data-ttu-id="9e751-302">Существует несколько типов операторов и символы пунктуации.</span><span class="sxs-lookup"><span data-stu-id="9e751-302">There are several kinds of operators and punctuators.</span></span> <span data-ttu-id="9e751-303">Операторы используются в выражениях для описания операций, связанных с одним или несколькими операндами.</span><span class="sxs-lookup"><span data-stu-id="9e751-303">Operators are used in expressions to describe operations involving one or more operands.</span></span> <span data-ttu-id="9e751-304">Например, выражение `a + b` использует `+` оператор, чтобы добавить два операнда `a` и `b`.</span><span class="sxs-lookup"><span data-stu-id="9e751-304">For example, the expression `a + b` uses the `+` operator to add the two operands `a` and `b`.</span></span> <span data-ttu-id="9e751-305">Знаки пунктуации служат для группирования и разделения.</span><span class="sxs-lookup"><span data-stu-id="9e751-305">Punctuators are for grouping and separating.</span></span>

```antlr
operator_or_punctuator
    : '{'  | '}'  | '['  | ']'  | '('   | ')'  | '.'  | ','  | ':'  | ';'
    | '+'  | '-'  | '*'  | '/'  | '%'   | '&'  | '|'  | '^'  | '!'  | '~'
    | '='  | '<'  | '>'  | '?'  | '??'  | '::' | '++' | '--' | '&&' | '||'
    | '->' | '==' | '!=' | '<=' | '>='  | '+=' | '-=' | '*=' | '/=' | '%='
    | '&=' | '|=' | '^=' | '<<' | '<<=' | '=>'
    ;

right_shift
    : '>>'
    ;

right_shift_assignment
    : '>>='
    ;
```

<span data-ttu-id="9e751-306">Вертикальная черта в *right_shift* и *right_shift_assignment* производства используются для указания того, что, в отличие от других производства в Синтаксическая грамматика, никакие символы не любого типа (даже не пробелы) разрешены между маркерами.</span><span class="sxs-lookup"><span data-stu-id="9e751-306">The vertical bar in the *right_shift* and *right_shift_assignment* productions are used to indicate that, unlike other productions in the syntactic grammar, no characters of any kind (not even whitespace) are allowed between the tokens.</span></span> <span data-ttu-id="9e751-307">Эти порождения обрабатываются особым образом, чтобы обеспечить правильную обработку *type_parameter_list*s ([параметры типа](classes.md#type-parameters)).</span><span class="sxs-lookup"><span data-stu-id="9e751-307">These productions are treated specially in order to enable the correct  handling of *type_parameter_list*s ([Type parameters](classes.md#type-parameters)).</span></span>

## <a name="pre-processing-directives"></a><span data-ttu-id="9e751-308">Директивы предварительной обработки</span><span class="sxs-lookup"><span data-stu-id="9e751-308">Pre-processing directives</span></span>

<span data-ttu-id="9e751-309">Директивы предварительной обработки дают возможность условно пропускать разделы исходных файлов, чтобы отчет условиях ошибок и предупреждений и устанавливать отдельные области исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9e751-309">The pre-processing directives provide the ability to conditionally skip sections of source files, to report error and warning conditions, and to delineate distinct regions of source code.</span></span> <span data-ttu-id="9e751-310">Термин «директивы препроцессора» используется только для обеспечения согласованности с языками программирования C и C++.</span><span class="sxs-lookup"><span data-stu-id="9e751-310">The term "pre-processing directives" is used only for consistency with the C and C++ programming languages.</span></span> <span data-ttu-id="9e751-311">В C# есть нет отдельного шага предварительной обработки; директивы предварительной обработки, обрабатываются как часть этапа лексического анализа.</span><span class="sxs-lookup"><span data-stu-id="9e751-311">In C#, there is no separate pre-processing step; pre-processing directives are processed as part of the lexical analysis phase.</span></span>

```antlr
pp_directive
    : pp_declaration
    | pp_conditional
    | pp_line
    | pp_diagnostic
    | pp_region
    | pp_pragma
    ;
```

<span data-ttu-id="9e751-312">Доступны следующие директивы предварительной обработки:</span><span class="sxs-lookup"><span data-stu-id="9e751-312">The following pre-processing directives are available:</span></span>

*  <span data-ttu-id="9e751-313">`#define` и `#undef`, которые используются для определения и отмены определения, соответственно, символы условной компиляции ([директивы объявления](lexical-structure.md#declaration-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-313">`#define` and `#undef`, which are used to define and undefine, respectively, conditional compilation symbols ([Declaration directives](lexical-structure.md#declaration-directives)).</span></span>
*  <span data-ttu-id="9e751-314">`#if`, `#elif`, `#else`, и `#endif`, которые используются для условно пропускать части исходного кода ([директивы условной компиляции](lexical-structure.md#conditional-compilation-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-314">`#if`, `#elif`, `#else`, and `#endif`, which are used to conditionally skip sections of source code ([Conditional compilation directives](lexical-structure.md#conditional-compilation-directives)).</span></span>
*  <span data-ttu-id="9e751-315">`#line`, который используется для управления номера строк, генерируется для ошибок и предупреждений ([строки директивы](lexical-structure.md#line-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-315">`#line`, which is used to control line numbers emitted for errors and warnings ([Line directives](lexical-structure.md#line-directives)).</span></span>
*  <span data-ttu-id="9e751-316">`#error` и `#warning`, которые используются для выдачи ошибок и предупреждений, соответственно ([диагностики директивы](lexical-structure.md#diagnostic-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-316">`#error` and `#warning`, which are used to issue errors and warnings, respectively ([Diagnostic directives](lexical-structure.md#diagnostic-directives)).</span></span>
*  <span data-ttu-id="9e751-317">`#region` и `#endregion`, которые используются для явной пометки части исходного кода ([директивы области](lexical-structure.md#region-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-317">`#region` and `#endregion`, which are used to explicitly mark sections of source code ([Region directives](lexical-structure.md#region-directives)).</span></span>
*  <span data-ttu-id="9e751-318">`#pragma`, который используется для указания компилятору необязательных сведений о контексте ([директивы Pragma](lexical-structure.md#pragma-directives)).</span><span class="sxs-lookup"><span data-stu-id="9e751-318">`#pragma`, which is used to specify optional contextual information to the compiler ([Pragma directives](lexical-structure.md#pragma-directives)).</span></span>

<span data-ttu-id="9e751-319">Директивы предварительной обработки, всегда занимает отдельную строку исходного кода и всегда начинается с `#` символ и имя директивы предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="9e751-319">A pre-processing directive always occupies a separate line of source code and always begins with a `#` character and a pre-processing directive name.</span></span> <span data-ttu-id="9e751-320">Пустое пространство может предшествовать `#` символ и между `#` символ и имя директивы.</span><span class="sxs-lookup"><span data-stu-id="9e751-320">White space may occur before the `#` character and between the `#` character and the directive name.</span></span>

<span data-ttu-id="9e751-321">Исходной строке, которая содержит `#define`, `#undef`, `#if`, `#elif`, `#else`, `#endif`, `#line`, или `#endregion` директива может заканчиваться однострочный комментарий.</span><span class="sxs-lookup"><span data-stu-id="9e751-321">A source line containing a `#define`, `#undef`, `#if`, `#elif`, `#else`, `#endif`, `#line`, or `#endregion` directive may end with a single-line comment.</span></span> <span data-ttu-id="9e751-322">Комментарии с разделителями ( `/* */` стиль комментариев) не разрешены для строк исходного кода, содержащий директивы предварительной обработки.</span><span class="sxs-lookup"><span data-stu-id="9e751-322">Delimited comments (the `/* */` style of comments) are not permitted on source lines containing pre-processing directives.</span></span>

<span data-ttu-id="9e751-323">Директивы предварительной обработки не токенов и не являются частью Синтаксическая грамматика C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-323">Pre-processing directives are not tokens and are not part of the syntactic grammar of C#.</span></span> <span data-ttu-id="9e751-324">Тем не менее директивы предварительной обработки можно использовать для включения или исключения последовательностей маркеров и можно таким образом влиять на значение программы на C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-324">However, pre-processing directives can be used to include or exclude sequences of tokens and can in that way affect the meaning of a C# program.</span></span> <span data-ttu-id="9e751-325">Например, при компиляции программы:</span><span class="sxs-lookup"><span data-stu-id="9e751-325">For example, when compiled, the program:</span></span>
```csharp
#define A
#undef B

class C
{
#if A
    void F() {}
#else
    void G() {}
#endif

#if B
    void H() {}
#else
    void I() {}
#endif
}
```
<span data-ttu-id="9e751-326">результаты в ту же последовательность токенов, программа:</span><span class="sxs-lookup"><span data-stu-id="9e751-326">results in the exact same sequence of tokens as the program:</span></span>
```csharp
class C
{
    void F() {}
    void I() {}
}
```

<span data-ttu-id="9e751-327">Таким образом тогда как лексически, две программы являются довольно большие различия, синтаксически, они идентичны.</span><span class="sxs-lookup"><span data-stu-id="9e751-327">Thus, whereas lexically, the two programs are quite different, syntactically, they are identical.</span></span>

### <a name="conditional-compilation-symbols"></a><span data-ttu-id="9e751-328">Символы условной компиляции</span><span class="sxs-lookup"><span data-stu-id="9e751-328">Conditional compilation symbols</span></span>

<span data-ttu-id="9e751-329">Условная компиляция, предоставляемую `#if`, `#elif`, `#else`, и `#endif` директивы осуществляется с помощью предварительной обработки выражения ([предварительной обработки выражения](lexical-structure.md#pre-processing-expressions)) и символы условной компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-329">The conditional compilation functionality provided by the `#if`, `#elif`, `#else`, and `#endif` directives is controlled through pre-processing expressions ([Pre-processing expressions](lexical-structure.md#pre-processing-expressions)) and conditional compilation symbols.</span></span>

```antlr
conditional_symbol
    : '<Any identifier_or_keyword except true or false>'
    ;
```

<span data-ttu-id="9e751-330">Символ условной компиляции имеет два возможных состояния: ***определенные*** или ***неопределенный***.</span><span class="sxs-lookup"><span data-stu-id="9e751-330">A conditional compilation symbol has two possible states: ***defined*** or ***undefined***.</span></span> <span data-ttu-id="9e751-331">В начале лексические обработки исходного файла, символ условной компиляции не определено, если оно явно определено с помощью внешнего механизма (например, параметр командной строки компилятора).</span><span class="sxs-lookup"><span data-stu-id="9e751-331">At the beginning of the lexical processing of a source file, a conditional compilation symbol is undefined unless it has been explicitly defined by an external mechanism (such as a command-line compiler option).</span></span> <span data-ttu-id="9e751-332">Когда `#define` обработке директивы, символ условной компиляции, упомянутый в этой директиве становится определенным в этом исходном файле.</span><span class="sxs-lookup"><span data-stu-id="9e751-332">When a `#define` directive is processed, the conditional compilation symbol named in that directive becomes defined in that source file.</span></span> <span data-ttu-id="9e751-333">Этот символ остается определенным до `#undef` директив для обработки того же самого символа, или пока не будет достигнут конец исходного файла.</span><span class="sxs-lookup"><span data-stu-id="9e751-333">The symbol remains defined until an `#undef` directive for that same symbol is processed, or until the end of the source file is reached.</span></span> <span data-ttu-id="9e751-334">Следствием этого является то, что `#define` и `#undef` директивы в одном исходном файле не оказывают влияния на другие исходные файлы в одной программе.</span><span class="sxs-lookup"><span data-stu-id="9e751-334">An implication of this is that `#define` and `#undef` directives in one source file have no effect on other source files in the same program.</span></span>

<span data-ttu-id="9e751-335">При обращении в выражении предварительной обработки, определенный символ условной компиляции имеет логическое значение `true`, и это неопределенный символ имеет логическое значение `false`.</span><span class="sxs-lookup"><span data-stu-id="9e751-335">When referenced in a pre-processing expression, a defined conditional compilation symbol has the boolean value `true`, and an undefined conditional compilation symbol has the boolean value `false`.</span></span> <span data-ttu-id="9e751-336">Нет необходимости что символы условной компиляции должны быть явно объявлены, прежде чем они указаны в предварительной обработки выражения.</span><span class="sxs-lookup"><span data-stu-id="9e751-336">There is no requirement that conditional compilation symbols be explicitly declared before they are referenced in pre-processing expressions.</span></span> <span data-ttu-id="9e751-337">Вместо этого просто являются неопределенными Необъявленные символы и имеют значение `false`.</span><span class="sxs-lookup"><span data-stu-id="9e751-337">Instead, undeclared symbols are simply undefined and thus have the value `false`.</span></span>

<span data-ttu-id="9e751-338">Пространство имен для символы условной компиляции, отделен от других именованных сущностей в программе на C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-338">The name space for conditional compilation symbols is distinct and separate from all other named entities in a C# program.</span></span> <span data-ttu-id="9e751-339">Символы условной компиляции можно ссылаться только `#define` и `#undef` директивы и в предварительной обработки выражения.</span><span class="sxs-lookup"><span data-stu-id="9e751-339">Conditional compilation symbols can only be referenced in `#define` and `#undef` directives and in pre-processing expressions.</span></span>

### <a name="pre-processing-expressions"></a><span data-ttu-id="9e751-340">Предварительная обработка выражения</span><span class="sxs-lookup"><span data-stu-id="9e751-340">Pre-processing expressions</span></span>

<span data-ttu-id="9e751-341">Предварительная обработка выражений могут возникать в `#if` и `#elif` директивы.</span><span class="sxs-lookup"><span data-stu-id="9e751-341">Pre-processing expressions can occur in `#if` and `#elif` directives.</span></span> <span data-ttu-id="9e751-342">Операторы `!`, `==`, `!=`, `&&` и `||` разрешены в предварительной обработки выражения, и можно использовать скобки для группирования.</span><span class="sxs-lookup"><span data-stu-id="9e751-342">The operators `!`, `==`, `!=`, `&&` and `||` are permitted in pre-processing expressions, and parentheses may be used for grouping.</span></span>

```antlr
pp_expression
    : whitespace? pp_or_expression whitespace?
    ;

pp_or_expression
    : pp_and_expression
    | pp_or_expression whitespace? '||' whitespace? pp_and_expression
    ;

pp_and_expression
    : pp_equality_expression
    | pp_and_expression whitespace? '&&' whitespace? pp_equality_expression
    ;

pp_equality_expression
    : pp_unary_expression
    | pp_equality_expression whitespace? '==' whitespace? pp_unary_expression
    | pp_equality_expression whitespace? '!=' whitespace? pp_unary_expression
    ;

pp_unary_expression
    : pp_primary_expression
    | '!' whitespace? pp_unary_expression
    ;

pp_primary_expression
    : 'true'
    | 'false'
    | conditional_symbol
    | '(' whitespace? pp_expression whitespace? ')'
    ;
```

<span data-ttu-id="9e751-343">При обращении в выражении предварительной обработки, определенный символ условной компиляции имеет логическое значение `true`, и это неопределенный символ имеет логическое значение `false`.</span><span class="sxs-lookup"><span data-stu-id="9e751-343">When referenced in a pre-processing expression, a defined conditional compilation symbol has the boolean value `true`, and an undefined conditional compilation symbol has the boolean value `false`.</span></span>

<span data-ttu-id="9e751-344">Вычисление предварительной обработки выражения всегда дает логическое значение.</span><span class="sxs-lookup"><span data-stu-id="9e751-344">Evaluation of a pre-processing expression always yields a boolean value.</span></span> <span data-ttu-id="9e751-345">Правила вычисления для предварительной обработки выражения являются такие же, как для константного выражения ([константные выражения](expressions.md#constant-expressions)), за исключением того, что только определяемых пользователем сущностей, которые можно указывать символы условной компиляции .</span><span class="sxs-lookup"><span data-stu-id="9e751-345">The rules of evaluation for a pre-processing expression are the same as those for a constant expression ([Constant expressions](expressions.md#constant-expressions)), except that the only user-defined entities that can be referenced are conditional compilation symbols.</span></span>

### <a name="declaration-directives"></a><span data-ttu-id="9e751-346">Объявление директивы</span><span class="sxs-lookup"><span data-stu-id="9e751-346">Declaration directives</span></span>

<span data-ttu-id="9e751-347">Директивы объявления используются для определения или отмены определения символы условной компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-347">The declaration directives are used to define or undefine conditional compilation symbols.</span></span>

```antlr
pp_declaration
    : whitespace? '#' whitespace? 'define' whitespace conditional_symbol pp_new_line
    | whitespace? '#' whitespace? 'undef' whitespace conditional_symbol pp_new_line
    ;

pp_new_line
    : whitespace? single_line_comment? new_line
    ;
```

<span data-ttu-id="9e751-348">Обработка `#define` директива вызывает данный символ условной компиляции определенным, начиная с исходной строки, следующей за директивой.</span><span class="sxs-lookup"><span data-stu-id="9e751-348">The processing of a `#define` directive causes the given conditional compilation symbol to become defined, starting with the source line that follows the directive.</span></span> <span data-ttu-id="9e751-349">Аналогично, обработку `#undef` директива приводит данный символ условной компиляции неопределенным, начиная с исходной строки, следующей за директивой.</span><span class="sxs-lookup"><span data-stu-id="9e751-349">Likewise, the processing of an `#undef` directive causes the given conditional compilation symbol to become undefined, starting with the source line that follows the directive.</span></span>

<span data-ttu-id="9e751-350">Любой `#define` и `#undef` директивы в файле исходного кода должно находиться перед первым *маркера* ([маркеры](lexical-structure.md#tokens)) в исходном файле; иначе во время компиляции возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="9e751-350">Any `#define` and `#undef` directives in a source file must occur before the first *token* ([Tokens](lexical-structure.md#tokens)) in the source file; otherwise a compile-time error occurs.</span></span> <span data-ttu-id="9e751-351">Интуитивно понятно `#define` и `#undef` директивы должно предшествовать любой «реальный код» в исходном файле.</span><span class="sxs-lookup"><span data-stu-id="9e751-351">In intuitive terms, `#define` and `#undef` directives must precede any "real code" in the source file.</span></span>

<span data-ttu-id="9e751-352">Пример:</span><span class="sxs-lookup"><span data-stu-id="9e751-352">The example:</span></span>
```csharp
#define Enterprise

#if Professional || Enterprise
    #define Advanced
#endif

namespace Megacorp.Data
{
    #if Advanced
    class PivotTable {...}
    #endif
}
```
<span data-ttu-id="9e751-353">является допустимым поскольку `#define` директивы перед первым токеном ( `namespace` ключевое слово) в исходном файле.</span><span class="sxs-lookup"><span data-stu-id="9e751-353">is valid because the `#define` directives precede the first token (the `namespace` keyword) in the source file.</span></span>

<span data-ttu-id="9e751-354">Следующий пример приводит к ошибке времени компиляции, так как `#define` следует за фактическим кодом:</span><span class="sxs-lookup"><span data-stu-id="9e751-354">The following example results in a compile-time error because a `#define` follows real code:</span></span>
```csharp
#define A
namespace N
{
    #define B
    #if B
    class Class1 {}
    #endif
}
```

<span data-ttu-id="9e751-355">Объект `#define` можно определить символ условной компиляции, которое уже определено, без, что все промежуточные `#undef` данного символа.</span><span class="sxs-lookup"><span data-stu-id="9e751-355">A `#define` may define a conditional compilation symbol that is already defined, without there being any intervening `#undef` for that symbol.</span></span> <span data-ttu-id="9e751-356">В приведенном ниже примере определяет символ условной компиляции `A` и определяющий его снова.</span><span class="sxs-lookup"><span data-stu-id="9e751-356">The example below defines a conditional compilation symbol `A` and then defines it again.</span></span>
```csharp
#define A
#define A
```

<span data-ttu-id="9e751-357">Объект `#undef` может «отменить» символ условной компиляции, который не определен.</span><span class="sxs-lookup"><span data-stu-id="9e751-357">A `#undef` may "undefine" a conditional compilation symbol that is not defined.</span></span> <span data-ttu-id="9e751-358">В приведенном ниже примере определяет символ условной компиляции `A` и затем отменяет определение его дважды; хотя второй `#undef` не оказывает влияния, он по-прежнему допустим.</span><span class="sxs-lookup"><span data-stu-id="9e751-358">The example below defines a conditional compilation symbol `A` and then undefines it twice; although the second `#undef` has no effect, it is still valid.</span></span>
```csharp
#define A
#undef A
#undef A
```

### <a name="conditional-compilation-directives"></a><span data-ttu-id="9e751-359">Директивы условной компиляции</span><span class="sxs-lookup"><span data-stu-id="9e751-359">Conditional compilation directives</span></span>

<span data-ttu-id="9e751-360">Директивы условной компиляции используются для условного включения или исключения частей исходного файла.</span><span class="sxs-lookup"><span data-stu-id="9e751-360">The conditional compilation directives are used to conditionally include or exclude portions of a source file.</span></span>

```antlr
pp_conditional
    : pp_if_section pp_elif_section* pp_else_section? pp_endif
    ;

pp_if_section
    : whitespace? '#' whitespace? 'if' whitespace pp_expression pp_new_line conditional_section?
    ;

pp_elif_section
    : whitespace? '#' whitespace? 'elif' whitespace pp_expression pp_new_line conditional_section?
    ;

pp_else_section:
    | whitespace? '#' whitespace? 'else' pp_new_line conditional_section?
    ;

pp_endif
    : whitespace? '#' whitespace? 'endif' pp_new_line
    ;

conditional_section
    : input_section
    | skipped_section
    ;

skipped_section
    : skipped_section_part+
    ;

skipped_section_part
    : skipped_characters? new_line
    | pp_directive
    ;

skipped_characters
    : whitespace? not_number_sign input_character*
    ;

not_number_sign
    : '<Any input_character except #>'
    ;
```

<span data-ttu-id="9e751-361">Как указано в синтаксисе директив условной компиляции должно быть записано как наборами, состоящими из, в порядке, `#if` директивы, ноль или более `#elif` директивы, нуль или один `#else` директивы и `#endif` директива.</span><span class="sxs-lookup"><span data-stu-id="9e751-361">As indicated by the syntax, conditional compilation directives must be written as sets consisting of, in order, an `#if` directive, zero or more `#elif` directives, zero or one `#else` directive, and an `#endif` directive.</span></span> <span data-ttu-id="9e751-362">Между этими директивами находятся условные разделы исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9e751-362">Between the directives are conditional sections of source code.</span></span> <span data-ttu-id="9e751-363">Каждый раздел управляется немедленно предшествующей директиве.</span><span class="sxs-lookup"><span data-stu-id="9e751-363">Each section is controlled by the immediately preceding directive.</span></span> <span data-ttu-id="9e751-364">Условный раздел может содержать вложенные директивы условной компиляции условии они образуют полные наборы.</span><span class="sxs-lookup"><span data-stu-id="9e751-364">A conditional section may itself contain nested conditional compilation directives provided these directives form complete sets.</span></span>

<span data-ttu-id="9e751-365">Объект *pp_conditional* выбирает максимум одну из вложенных *conditional_section*s для обычной лексические обработки:</span><span class="sxs-lookup"><span data-stu-id="9e751-365">A *pp_conditional* selects at most one of the contained *conditional_section*s for normal lexical processing:</span></span>

*  <span data-ttu-id="9e751-366">*Pp_expression*s из `#if` и `#elif` директивы вычисляются в порядке, пока не дает одно `true`.</span><span class="sxs-lookup"><span data-stu-id="9e751-366">The *pp_expression*s of the `#if` and `#elif` directives are evaluated in order until one yields `true`.</span></span> <span data-ttu-id="9e751-367">Если выражение выдает `true`, *conditional_section* соответствующей директивы выбран.</span><span class="sxs-lookup"><span data-stu-id="9e751-367">If an expression yields `true`, the *conditional_section* of the corresponding directive is selected.</span></span>
*  <span data-ttu-id="9e751-368">Если все *pp_expression*s yield `false`и если `#else` присутствует директива *conditional_section* из `#else` директива выбран.</span><span class="sxs-lookup"><span data-stu-id="9e751-368">If all *pp_expression*s yield `false`, and if an `#else` directive is present, the *conditional_section* of the `#else` directive is selected.</span></span>
*  <span data-ttu-id="9e751-369">В противном случае — нет *conditional_section* выбран.</span><span class="sxs-lookup"><span data-stu-id="9e751-369">Otherwise, no *conditional_section* is selected.</span></span>

<span data-ttu-id="9e751-370">Выбранный *conditional_section*, если есть, обрабатывается как обычный *input_section*: исходного кода, содержащегося в разделе необходимо следовать лексическая грамматика: токены создаются из источника код в разделе; и директивы предварительной обработки в разделе предписанных эффектами.</span><span class="sxs-lookup"><span data-stu-id="9e751-370">The selected *conditional_section*, if any, is processed as a normal *input_section*: the source code contained in the section must adhere to the lexical grammar; tokens are generated from the source code in the section; and pre-processing directives in the section have the prescribed effects.</span></span>

<span data-ttu-id="9e751-371">Оставшиеся *conditional_section*s, если таковое имеется, обрабатываются как *skipped_section*s: за исключением директивы предварительной обработки исходного кода в разделе не обязан соблюдать лексическая грамматика; нет токены создаются из исходного кода в разделе; и директивы предварительной обработки в разделе, должны быть лексически правильным, но, в противном случае не обрабатываются.</span><span class="sxs-lookup"><span data-stu-id="9e751-371">The remaining *conditional_section*s, if any, are processed as *skipped_section*s: except for pre-processing directives, the source code in the section need not adhere to the lexical grammar; no tokens are generated from the source code in the section; and pre-processing directives in the section must be lexically correct but are not otherwise processed.</span></span> <span data-ttu-id="9e751-372">В рамках *conditional_section* , обрабатывается как *skipped_section*, все вложенные *conditional_section*s (содержится в вложенные `#if`... `#endif` и `#region`... `#endregion` конструкции) также обрабатываются как *skipped_section*s.</span><span class="sxs-lookup"><span data-stu-id="9e751-372">Within a *conditional_section* that is being processed as a *skipped_section*, any nested *conditional_section*s (contained in nested `#if`...`#endif` and `#region`...`#endregion` constructs) are also processed as *skipped_section*s.</span></span>

<span data-ttu-id="9e751-373">В следующем примере показано, как условной компиляции, можно создавать вложенные директивы:</span><span class="sxs-lookup"><span data-stu-id="9e751-373">The following example illustrates how conditional compilation directives can nest:</span></span>
```csharp
#define Debug       // Debugging on
#undef Trace        // Tracing off

class PurchaseTransaction
{
    void Commit() {
        #if Debug
            CheckConsistency();
            #if Trace
                WriteToLog(this.ToString());
            #endif
        #endif
        CommitHelper();
    }
}
```

<span data-ttu-id="9e751-374">За исключением директивы предварительной обработки пропущенных исходный код не подлежащий лексическому анализу.</span><span class="sxs-lookup"><span data-stu-id="9e751-374">Except for pre-processing directives, skipped source code is not subject to lexical analysis.</span></span> <span data-ttu-id="9e751-375">Например, допустим следующий несмотря на комментарий без признака завершения в `#else` разделе:</span><span class="sxs-lookup"><span data-stu-id="9e751-375">For example, the following is valid despite the unterminated comment in the `#else` section:</span></span>
```csharp
#define Debug        // Debugging on

class PurchaseTransaction
{
    void Commit() {
        #if Debug
            CheckConsistency();
        #else
            /* Do something else
        #endif
    }
}
```

<span data-ttu-id="9e751-376">Обратите внимание, что директивы предварительной обработки должны быть лексически правильными даже в пропущенных разделах исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9e751-376">Note, however, that pre-processing directives are required to be lexically correct even in skipped sections of source code.</span></span>

<span data-ttu-id="9e751-377">Директивы предварительной обработки, не обрабатываются, когда они присутствуют внутри многострочного входных элементов.</span><span class="sxs-lookup"><span data-stu-id="9e751-377">Pre-processing directives are not processed when they appear inside multi-line input elements.</span></span> <span data-ttu-id="9e751-378">Например, программа:</span><span class="sxs-lookup"><span data-stu-id="9e751-378">For example, the program:</span></span>
```csharp
class Hello
{
    static void Main() {
        System.Console.WriteLine(@"hello, 
#if Debug
        world
#else
        Nebraska
#endif
        ");
    }
}
```
<span data-ttu-id="9e751-379">результаты в выходных данных:</span><span class="sxs-lookup"><span data-stu-id="9e751-379">results in the output:</span></span>
```
hello,
#if Debug
        world
#else
        Nebraska
#endif
```

<span data-ttu-id="9e751-380">В особенных случаях набор директивы предварительной обработки, который обрабатывается могут зависеть от оценки *pp_expression*.</span><span class="sxs-lookup"><span data-stu-id="9e751-380">In peculiar cases, the set of pre-processing directives that is processed might depend on the evaluation of the *pp_expression*.</span></span> <span data-ttu-id="9e751-381">Пример:</span><span class="sxs-lookup"><span data-stu-id="9e751-381">The example:</span></span>
```csharp
#if X
    /*
#else
    /* */ class Q { }
#endif
```
<span data-ttu-id="9e751-382">всегда создает же поток лексем (`class` `Q` `{` `}`), независимо от того, нужно ли `X` определен.</span><span class="sxs-lookup"><span data-stu-id="9e751-382">always produces the same token stream (`class` `Q` `{` `}`), regardless of whether or not `X` is defined.</span></span> <span data-ttu-id="9e751-383">Если `X` будет определен, являются обрабатываются только директивы `#if` и `#endif`из- за многострочного комментария.</span><span class="sxs-lookup"><span data-stu-id="9e751-383">If `X` is defined, the only processed directives are `#if` and `#endif`, due to the multi-line comment.</span></span> <span data-ttu-id="9e751-384">Если `X` является неопределенным, затем три директивы (`#if`, `#else`, `#endif`) являются частью набора директив.</span><span class="sxs-lookup"><span data-stu-id="9e751-384">If `X` is undefined, then three directives (`#if`, `#else`, `#endif`) are part of the directive set.</span></span>

### <a name="diagnostic-directives"></a><span data-ttu-id="9e751-385">Директивы диагностики</span><span class="sxs-lookup"><span data-stu-id="9e751-385">Diagnostic directives</span></span>

<span data-ttu-id="9e751-386">Директивы диагностики позволяют явно создавать ошибки и предупреждения, отображаемые в так же, как другие ошибки времени компиляции и предупреждения.</span><span class="sxs-lookup"><span data-stu-id="9e751-386">The diagnostic directives are used to explicitly generate error and warning messages that are reported in the same way as other compile-time errors and warnings.</span></span>

```antlr
pp_diagnostic
    : whitespace? '#' whitespace? 'error' pp_message
    | whitespace? '#' whitespace? 'warning' pp_message
    ;

pp_message
    : new_line
    | whitespace input_character* new_line
    ;
```

<span data-ttu-id="9e751-387">Пример:</span><span class="sxs-lookup"><span data-stu-id="9e751-387">The example:</span></span>
```csharp
#warning Code review needed before check-in

#if Debug && Retail
    #error A build can't be both debug and retail
#endif

class Test {...}
```
<span data-ttu-id="9e751-388">всегда выдает предупреждение («проверка кода до возврата требуется») и вызывает ошибку времени компиляции («сборки не может быть как для отладки, так и для розничной торговли») Если условных символов `Debug` и `Retail` определены.</span><span class="sxs-lookup"><span data-stu-id="9e751-388">always produces a warning ("Code review needed before check-in"), and produces a compile-time error ("A build can't be both debug and retail") if the conditional symbols `Debug` and `Retail` are both defined.</span></span> <span data-ttu-id="9e751-389">Обратите внимание, что *pp_message* могут содержать произвольный текст; в частности, оно не должно содержать правильный формат маркеров, как показано в одинарные кавычки в слове `can't`.</span><span class="sxs-lookup"><span data-stu-id="9e751-389">Note that a *pp_message* can contain arbitrary text; specifically, it need not contain well-formed tokens, as shown by the single quote in the word `can't`.</span></span>

### <a name="region-directives"></a><span data-ttu-id="9e751-390">Директивы региона</span><span class="sxs-lookup"><span data-stu-id="9e751-390">Region directives</span></span>

<span data-ttu-id="9e751-391">Директивы области позволяют явным образом пометить области исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9e751-391">The region directives are used to explicitly mark regions of source code.</span></span>

```antlr
pp_region
    : pp_start_region conditional_section? pp_end_region
    ;

pp_start_region
    : whitespace? '#' whitespace? 'region' pp_message
    ;

pp_end_region
    : whitespace? '#' whitespace? 'endregion' pp_message
    ;
```

<span data-ttu-id="9e751-392">Нет семантического значения присоединяется к области; регионы предназначены для использования в программу самим разработчиком и автоматические средства для пометки части исходного кода.</span><span class="sxs-lookup"><span data-stu-id="9e751-392">No semantic meaning is attached to a region; regions are intended for use by the programmer or by automated tools to mark a section of source code.</span></span> <span data-ttu-id="9e751-393">Сообщения, заданного в `#region` или `#endregion` директива точно так же не имеет семантического значения; он просто служит для определения области.</span><span class="sxs-lookup"><span data-stu-id="9e751-393">The message specified in a `#region` or `#endregion` directive likewise has no semantic meaning; it merely serves to identify the region.</span></span> <span data-ttu-id="9e751-394">Сопоставление `#region` и `#endregion` директивы может иметь другие *pp_message*s.</span><span class="sxs-lookup"><span data-stu-id="9e751-394">Matching `#region` and `#endregion` directives may have different *pp_message*s.</span></span>

<span data-ttu-id="9e751-395">Обработка лексической области:</span><span class="sxs-lookup"><span data-stu-id="9e751-395">The lexical processing of a region:</span></span>
```csharp
#region
...
#endregion
```
<span data-ttu-id="9e751-396">точно соответствует Лексическая обработка директивы условной компиляции в формате:</span><span class="sxs-lookup"><span data-stu-id="9e751-396">corresponds exactly to the lexical processing of a conditional compilation directive of the form:</span></span>
```csharp
#if true
...
#endif
```

### <a name="line-directives"></a><span data-ttu-id="9e751-397">Директивы строк</span><span class="sxs-lookup"><span data-stu-id="9e751-397">Line directives</span></span>

<span data-ttu-id="9e751-398">Директивы строк может использоваться для изменения номера строк и имен исходных файлов, выводятся компилятором в выходных данных, такие как предупреждения и ошибки, и, которые используются в информационные атрибуты вызывающего объекта ([информационные атрибуты вызывающего объекта](attributes.md#caller-info-attributes)).</span><span class="sxs-lookup"><span data-stu-id="9e751-398">Line directives may be used to alter the line numbers and source file names that are reported by the compiler in output such as warnings and errors, and that are used by caller info attributes ([Caller info attributes](attributes.md#caller-info-attributes)).</span></span>

<span data-ttu-id="9e751-399">Директивы строк чаще всего используются в средствах метапрограммирования, Создание исходного кода C# из другого текстового ввода.</span><span class="sxs-lookup"><span data-stu-id="9e751-399">Line directives are most commonly used in meta-programming tools that generate C# source code from some other text input.</span></span>

```antlr
pp_line
    : whitespace? '#' whitespace? 'line' whitespace line_indicator pp_new_line
    ;

line_indicator
    : decimal_digit+ whitespace file_name
    | decimal_digit+
    | 'default'
    | 'hidden'
    ;

file_name
    : '"' file_name_character+ '"'
    ;

file_name_character
    : '<Any input_character except ">'
    ;
```

<span data-ttu-id="9e751-400">Если аргумент `#line` директив, компилятор сообщает настоящие номера строк и имен исходных файлов в своих выходных данных.</span><span class="sxs-lookup"><span data-stu-id="9e751-400">When no `#line` directives are present, the compiler reports true line numbers and source file names in its output.</span></span> <span data-ttu-id="9e751-401">При обработке `#line` директива, которая включает в себя *line_indicator* , не `default`, компилятор обрабатывает строки после директивы как имеющий указанный номер строки (и имя файла, если указано).</span><span class="sxs-lookup"><span data-stu-id="9e751-401">When processing a `#line` directive that includes a *line_indicator* that is not `default`, the compiler treats the line after the directive as having the given line number (and file name, if specified).</span></span>

<span data-ttu-id="9e751-402">Объект `#line default` директива отменяет эффект всех предшествующих директив #line.</span><span class="sxs-lookup"><span data-stu-id="9e751-402">A `#line default` directive reverses the effect of all preceding #line directives.</span></span> <span data-ttu-id="9e751-403">Компилятор сообщает сведения о строке значение true, для последующих строк, как если нет `#line` директивы будут обработаны.</span><span class="sxs-lookup"><span data-stu-id="9e751-403">The compiler reports true line information for subsequent lines, precisely as if no `#line` directives had been processed.</span></span>

<span data-ttu-id="9e751-404">Объект `#line hidden` директива не действует для файла и номера строки, полученные по ошибке сообщения, но влияет на отладку на исходном уровне.</span><span class="sxs-lookup"><span data-stu-id="9e751-404">A `#line hidden` directive has no effect on the file and line numbers reported in error messages, but does affect source level debugging.</span></span> <span data-ttu-id="9e751-405">При отладке, все строки между `#line hidden` директивы и последующих `#line` директива (это не `#line hidden`) имеют нет информация о номере строки.</span><span class="sxs-lookup"><span data-stu-id="9e751-405">When debugging, all lines between a `#line hidden` directive and the subsequent `#line` directive (that is not `#line hidden`) have no line number information.</span></span> <span data-ttu-id="9e751-406">При пошаговом выполнении кода в отладчике, эти строки будут пропущены полностью.</span><span class="sxs-lookup"><span data-stu-id="9e751-406">When stepping through code in the debugger, these lines will be skipped entirely.</span></span>

<span data-ttu-id="9e751-407">Обратите внимание, что *имя_файла* отличается от обычного строкового литерала, что escape-символы, не обрабатываются; "`\`" символ просто означает символ обычные обратной косой черты в *имя_файла*.</span><span class="sxs-lookup"><span data-stu-id="9e751-407">Note that a *file_name* differs from a regular string literal in that escape characters are not processed; the "`\`" character simply designates an ordinary backslash character within a *file_name*.</span></span>

### <a name="pragma-directives"></a><span data-ttu-id="9e751-408">Директивы pragma</span><span class="sxs-lookup"><span data-stu-id="9e751-408">Pragma directives</span></span>

<span data-ttu-id="9e751-409">`#pragma` Директивы предварительной обработки используется для указания компилятору необязательных сведений о контексте.</span><span class="sxs-lookup"><span data-stu-id="9e751-409">The `#pragma` preprocessing directive is used to specify optional contextual information to the compiler.</span></span> <span data-ttu-id="9e751-410">Сведения, указанные в `#pragma` директива будет никогда не изменяют семантику программы.</span><span class="sxs-lookup"><span data-stu-id="9e751-410">The information supplied in a `#pragma` directive will never change program semantics.</span></span>

```antlr
pp_pragma
    : whitespace? '#' whitespace? 'pragma' whitespace pragma_body pp_new_line
    ;

pragma_body
    : pragma_warning_body
    ;
```

<span data-ttu-id="9e751-411">C# предоставляет `#pragma` директивы для управления предупреждениями компилятора.</span><span class="sxs-lookup"><span data-stu-id="9e751-411">C# provides `#pragma` directives to control compiler warnings.</span></span> <span data-ttu-id="9e751-412">Будущие версии языка могут включать дополнительные `#pragma` директивы.</span><span class="sxs-lookup"><span data-stu-id="9e751-412">Future versions of the language may include additional `#pragma` directives.</span></span> <span data-ttu-id="9e751-413">Чтобы обеспечить взаимодействие с другими компиляторами C#, компилятор Microsoft C# выдает ошибки компиляции для неизвестных `#pragma` директивы; такие директивы не формировать предупреждения, тем не менее.</span><span class="sxs-lookup"><span data-stu-id="9e751-413">To ensure interoperability with other C# compilers, the Microsoft C# compiler does not issue compilation errors for unknown `#pragma` directives; such directives do however generate warnings.</span></span>

#### <a name="pragma-warning"></a><span data-ttu-id="9e751-414">В директиве pragma warning</span><span class="sxs-lookup"><span data-stu-id="9e751-414">Pragma warning</span></span>

<span data-ttu-id="9e751-415">`#pragma warning` Директива используется для отключения или восстановления всех или определенный набор предупреждение сообщений во время компиляции последующего текста программы.</span><span class="sxs-lookup"><span data-stu-id="9e751-415">The `#pragma warning` directive is used to disable or restore all or a particular set of warning messages during compilation of the subsequent program text.</span></span>

```antlr
pragma_warning_body
    : 'warning' whitespace warning_action
    | 'warning' whitespace warning_action whitespace warning_list
    ;

warning_action
    : 'disable'
    | 'restore'
    ;

warning_list
    : decimal_digit+ (whitespace? ',' whitespace? decimal_digit+)*
    ;
```

<span data-ttu-id="9e751-416">Объект `#pragma warning` директива, исключающую список предупреждений, влияет на все предупреждения.</span><span class="sxs-lookup"><span data-stu-id="9e751-416">A `#pragma warning` directive that omits the warning list affects all warnings.</span></span> <span data-ttu-id="9e751-417">Объект `#pragma warning` директива включает в себя список предупреждений влияет только на предупреждения, которые указаны в списке.</span><span class="sxs-lookup"><span data-stu-id="9e751-417">A `#pragma warning` directive the includes a warning list affects only those warnings that are specified in the list.</span></span>

<span data-ttu-id="9e751-418">Объект `#pragma warning disable` директив отключает все или заданный набор предупреждений.</span><span class="sxs-lookup"><span data-stu-id="9e751-418">A `#pragma warning disable` directive disables all or the given set of warnings.</span></span>

<span data-ttu-id="9e751-419">Объект `#pragma warning restore` директив восстанавливает все или заданный набор предупреждений с состоянием, в действительности применялся в начале блока компиляции.</span><span class="sxs-lookup"><span data-stu-id="9e751-419">A `#pragma warning restore` directive restores all or the given set of warnings to the state that was in effect at the beginning of the compilation unit.</span></span> <span data-ttu-id="9e751-420">Обратите внимание, что если конкретного предупреждения было отключено извне, `#pragma warning restore` (для всех или для конкретного предупреждения) не включит это предупреждение.</span><span class="sxs-lookup"><span data-stu-id="9e751-420">Note that if a particular warning was disabled externally, a `#pragma warning restore` (whether for all or the specific warning) will not re-enable that warning.</span></span>

<span data-ttu-id="9e751-421">В следующем примере показано использование `#pragma warning` для временного отключения этого предупреждения, переданные при устаревшим ссылкой на члены, используя номер предупреждения компилятора Microsoft C#.</span><span class="sxs-lookup"><span data-stu-id="9e751-421">The following example shows use of `#pragma warning` to temporarily disable the warning reported when obsoleted members are referenced, using the warning number from the Microsoft C# compiler.</span></span>
```csharp
using System;

class Program
{
    [Obsolete]
    static void Foo() {}

    static void Main() {
#pragma warning disable 612
    Foo();
#pragma warning restore 612
    }
}
```
