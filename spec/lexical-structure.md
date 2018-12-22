# <a name="lexical-structure"></a>Лексическая структура

## <a name="programs"></a>Programs

C# ***программы*** состоит из одного или нескольких ***исходные файлы***, которая называется формально ***блоков компиляции*** ([блоков компиляции](namespaces.md#compilation-units)). Исходный файл — это упорядоченная последовательность символов Юникода. Исходные файлы обычно имеют однозначное соответствие с файлами в файловой системе, но это соответствие не является обязательным. Для максимальной переносимости рекомендуется, что файлы в файловой системе быть закодирован с использованием UTF-8 кодирования.

С концептуальной точки зрения программа компилируется в три этапа:

1. Преобразование, которое преобразует файл из конкретного набора символов и схемы кодировки в последовательность символов Юникода.
2. Лексический анализ преобразует поток входных символов Юникода в поток токенов.
3. Синтаксический анализ преобразует поток лексем в исполняемый код.

## <a name="grammars"></a>Грамматики

Эта спецификация представлен синтаксис языка программирования C# с помощью двух грамматики. ***Лексическая грамматика*** ([лексическая грамматика](lexical-structure.md#lexical-grammar)) определяет, как символы Юникода объединяются для формы признаки конца строки, пробелы, комментарии, токены и директивы предварительной обработки. ***Синтаксическая грамматика*** ([Синтаксическая грамматика](lexical-structure.md#syntactic-grammar)) определяет, как маркеры, полученные в результате лексическая грамматика объединяются для формирования C# программ.

### <a name="grammar-notation"></a>Грамматическая нотация

Грамматики лексическую и синтаксическую представлены в форме Бэкуса-Наура, с помощью нотации средство ANTLR грамматики.

### <a name="lexical-grammar"></a>Лексическая грамматика

Лексическая грамматика C# представлены в [Лексический анализ](lexical-structure.md#lexical-analysis), [маркеры](lexical-structure.md#tokens), и [директивы предварительной обработки](lexical-structure.md#pre-processing-directives). Терминалов символы лексическая грамматика символов кодировки Юникод, и лексическая грамматика определяет, как символы объединяются для формирования лексем ([маркеры](lexical-structure.md#tokens)), пробел ([пустое пространство](lexical-structure.md#white-space)), комментарии ([комментарии](lexical-structure.md#comments)) и директивы предварительной обработки ([директивы предварительной обработки](lexical-structure.md#pre-processing-directives)).

Каждый исходный файл программы на C# должны соответствовать *входной* производства лексическая грамматика ([Лексический анализ](lexical-structure.md#lexical-analysis)).

### <a name="syntactic-grammar"></a>Синтаксическая грамматика

Синтаксическая грамматика C# представлены в главах и приложениях, выполните указания в этой главе. Используются токены, определяется лексическая грамматика терминалов символы синтаксической грамматики и Синтаксическая грамматика определяет, как маркеры объединяются для программ на C# формы.

Каждый исходный файл C# программы должны соответствовать *compilation_unit* производства Синтаксическая грамматика ([блоков компиляции](namespaces.md#compilation-units)).

## <a name="lexical-analysis"></a>Лексический анализ

*Входной* рабочей определяет Лексическая структура исходного файла C#. В рабочей среде этот лексическая грамматика должен соответствовать каждый исходный файл в программе на C#.

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

Пять основных элементов, составляющих Лексическая структура C# исходный файл: Признаки конца строки ([символов признака конца строки](lexical-structure.md#line-terminators)), пробел ([пробелы](lexical-structure.md#white-space)), комментарии ([комментарии](lexical-structure.md#comments)), маркеры ([маркеры](lexical-structure.md#tokens)), и директивы предварительной обработки ([директивы предварительной обработки](lexical-structure.md#pre-processing-directives)). Из этих основных элементов учитываются только токены в синтаксис программы на C# ([Синтаксическая грамматика](lexical-structure.md#syntactic-grammar)).

Лексическая обработка исходным файлом C# состоит из файла в последовательность токенов, который становятся входными данными для синтаксического анализа. Признаки конца строки, пробелы и комментарии можно использовать для разделения лексем, директивы предварительной обработки может привести к части исходного файла, которые нужно пропустить, а в противном случае эти лексические элементы не оказывают влияния на синтаксической структуры программы на C#.

В случае интерполированные строковые литералы ([интерполированные строковые литералы](lexical-structure.md#interpolated-string-literals)) один токен, изначально созданные лексического анализа, но разбивается на несколько входных элементов, которые многократно подвергались Лексический анализ пока все интерполированные строковые литералы, были устранены. Полученных маркеров выступать в качестве входных данных для синтаксического анализа.

Когда несколько производств лексическая грамматика соответствует последовательности символов в исходном файле, Лексическая обработка всегда создает длинный возможный лексический элемент. Например, последовательность знаков `//` обрабатывается как начало однострочного комментария, так как этот лексический элемент длиннее, чем один `/` токена.

### <a name="line-terminators"></a>Признаки конца строки

Признаки конца строки символов исходного файла C# разбивается на строки.

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

Для совместимости с исходного кода средства редактирования, которые добавляют маркеры конец файла, и включить источник файл, чтобы просмотреть в виде последовательности правильно завершенных строк, применяются следующие преобразования, в порядке, каждый файл исходного кода в программе на C#:

*  Если последний символ исходного файла является символ CTRL + Z (`U+001A`), этот символ будет удален.
*  Символ возврата каретки (`U+000D`) добавляется в конец исходного файла, если этот исходный файл не является пустым и последним символом исходного файла не является символ возврата каретки (`U+000D`), перевода строки (`U+000A`), разделитель (`U+2028`), или разделителем абзацев (`U+2029`).

### <a name="comments"></a>Комментарии

Поддерживаются два вида примечаний: однострочные комментарии и комментарии с разделителями. ***Однострочные комментарии*** начинаются с символов `//` и расширить его в конец исходной строки. ***Комментарии с разделителями*** начинаются с символов `/*` и заканчиваются символами `*/`. С разделителями комментарии могут занимать несколько строк.

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

Комментарии не могут быть вложенными. Последовательности символов `/*` и `*/` не имеют особого значения в пределах `//` комментарий и последовательности символов `//` и `/*` не имеют особого значения с разделителями комментария.

Комментарии, не обрабатываются в символьные и строковые литералы.

Пример
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
содержит комментарий с разделителями.

Пример
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
показано несколько однострочных комментариев.

### <a name="white-space"></a>Пробел

Пустое пространство определяется как символ перевода любой символ Юникода класса Zs (который включает символ пробела), а также символ горизонтальной табуляции, символ вертикальной табуляции и формы.

```antlr
whitespace
    : '<Any character with Unicode class Zs>'
    | '<Horizontal tab character (U+0009)>'
    | '<Vertical tab character (U+000B)>'
    | '<Form feed character (U+000C)>'
    ;
```

## <a name="tokens"></a>лексемы

Существует несколько типов токенов: идентификаторы, ключевые слова, литералы, операторы и символы пунктуации. Пробелы и комментарии не являются лексемами, хотя действуют как разделители для маркеров.

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

### <a name="unicode-character-escape-sequences"></a>Escape-последовательности символов Юникода

Управляющая последовательность символов Юникода представляет символ Юникода. Escape-последовательности символов Юникода обрабатываются в идентификаторах ([идентификаторы](lexical-structure.md#identifiers)), символьные литералы ([символьные литералы](lexical-structure.md#character-literals)) и строковые литералы regular ([строковые литералы](lexical-structure.md#string-literals)). Escape-символ Юникода не обрабатывается в любом другом месте (например, для формирования оператор символ пунктуации и ключевое слово).

```antlr
unicode_escape_sequence
    : '\\u' hex_digit hex_digit hex_digit hex_digit
    | '\\U' hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit
    ;
```

Escape-последовательность Юникода представляет один знак Юникода, образованное шестнадцатеричный номер после "`\u`«или»`\U`" символов. Так как в C# используется 16-разрядная кодировка кодовых позиций Юникода в символы и строковые значения, символ Юникода в диапазоне от U + 10000 до U + 10FFFF не допускается в символьных литералов и представляется с помощью суррогатной пары Юникода в строковом литерале. Символы Юникода с элементами кода выше 0x10FFFF не поддерживаются.

Несколько переводов не выполняются. Например, строковый литерал "`\u005Cu005C`«эквивалентно»`\u005C`«вместо»`\`«. Значение в кодировке Юникод `\u005C` — это символ, "`\`«.

Пример
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
показаны несколько способов применения `\u0066`, который является escape-последовательность для письма "`f`«. Программа эквивалентно
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

### <a name="identifiers"></a>Идентификаторы

Правилам для идентификаторов, приведенный в этом разделе точно соответствуют рекомендованным Unicode Standard Annex 31, за исключением того, что символ подчеркивания допустим в качестве исходного символа (как в традиционных на языке программирования C), являются последовательностей escape-символов Юникода допускается в идентификаторах и "`@`" символ разрешено как префикс включать ключевые слова для использования в качестве идентификаторов.

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

Сведения о классах символов Юникода, упомянутых выше см. в разделе Стандарт Юникода версии 3.0, раздел 4.5.

Примеры допустимых идентификаторов "`identifier1`«,»`_identifier2`«, и"`@if`«.

Идентификатор в соответствующей программе должен быть в канонический формат, определяемый формой нормализации Юникода C, в соответствии с определением Unicode Standard Annex 15. Поведение при обнаружении идентификатора не в форму нормализации C определяется реализацией; Тем не менее Диагностика не требуется.

Префикс "`@`" позволяет использовать ключевые слова как идентификаторы, что полезно при взаимодействии с другими языками программирования. Символ `@` не фактически входит идентификатора, поэтому идентификатор можно рассматривать в других языках в качестве обычного идентификатора, без префикса. Идентификатор с `@` префикс называется ***буквальным идентификатором***. Использование `@` префикс для идентификаторов, которые не являются ключевые слова, разрешено, но настоятельно не рекомендуется в рамках стиля.

Пример:
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
Определяет класс с именем "`class`«со статическим методом с именем»`static`«, принимающий параметр с именем»`bool`«. Обратите внимание, что поскольку escape-последовательности Юникода не разрешены в ключевых слов, токен "`cl\u0061ss`«— это идентификатор, и тем же идентификатором, как»`@class`«.

Два идентификатора считаются одинаковыми, если они были идентичны после следующие преобразования применяются в порядке:

*  Префикс "`@`«, если используется, удаляется.
*  Каждый *unicode_escape_sequence* преобразуется в соответствующий символ Юникода.
*  Любой *formatting_character*s удаляются.

Идентификаторы, содержащие двух последовательных символы подчеркивания (`U+005F`) зарезервированы для использования в реализации. Например реализация может предоставлять расширенные ключевые слова, которые начинаются с двух символов подчеркивания.

### <a name="keywords"></a>Ключевые слова

Объект ***ключевое слово*** — это последовательность символов, зарезервирован и не может использоваться как идентификатор зарезервированная `@` символ.

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

В некоторых областях грамматики определенных идентификаторов имеют специальное значение, но не являются ключевыми словами. Такие идентификаторы иногда называются «контекстными ключевыми словами». Например, в объявлении свойства "`get`«и»`set`" идентификаторы имеют особое значение ([методы доступа](classes.md#accessors)). Идентификатор, отличных от `get` или `set` , никогда не разрешается в этих расположениях, поэтому такое использование не конфликтует с использования эти слова в качестве идентификаторов. В других случаях, таких как и в случае с идентификатором "`var`" в объявлениях неявно типизированной локальной переменной ([объявления локальных переменных](statements.md#local-variable-declarations)), контекстное ключевое слово может конфликтовать с объявленных имен. В таком случае объявленное имя имеет приоритет над использование идентификатора в качестве контекстно-зависимое ключевое слово.

### <a name="literals"></a>Литералы

Объект ***литерала*** является представлением кода исходного значения.

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

#### <a name="boolean-literals"></a>Логические литералы

Существуют два значения логического литерала: `true` и `false`.

```antlr
boolean_literal
    : 'true'
    | 'false'
    ;
```

Тип *boolean_literal* является `bool`.

#### <a name="integer-literals"></a>Целочисленные литералы

Целочисленные литералы используются для записи значения типов `int`, `uint`, `long`, и `ulong`. Целочисленные литералы имеют две возможных формы: десятичные и шестнадцатеричные.

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

Тип целочисленного литерала определяется следующим образом:

*  Если литерал не имеет суффикса, его тип — первый из этих типов, в которых может быть представлено его значение: `int`, `uint`, `long`, `ulong`.
*  Если литерал с суффиксом `U` или `u`, его тип — первый из этих типов, в которых может быть представлено его значение: `uint`, `ulong`.
*  Если литерал с суффиксом `L` или `l`, его тип — первый из этих типов, в которых может быть представлено его значение: `long`, `ulong`.
*  Если литерал с суффиксом `UL`, `Ul`, `uL`, `ul`, `LU`, `Lu`, `lU`, или `lu`, он имеет тип `ulong`.

Если значение, представленное целочисленным литералом находится вне диапазона `ulong` типа, возникает ошибка времени компиляции.

Как со стилем, рекомендуется, "`L`«использовано вместо свойства»`l`» при записи литералов типа `long`, так как это легко перепутать буква"`l`«с цифрой»`1`«.

Чтобы разрешить наименьшим из возможных `int` и `long` значения в виде литералов десятичное целое число, существует два правила:

* Когда *decimal_integer_literal* со значением 2147483648 (2 ^ 31) и не *integer_type_suffix* доступен в качестве маркера, который сразу после "унарный минус" лексема оператора (["унарный минус" оператор](expressions.md#unary-minus-operator)), результатом является константа типа `int` со значением от -2147483648 (-2 ^ 31). В других случаях такие *decimal_integer_literal* имеет тип `uint`.
* Когда *decimal_integer_literal* со значением 9223372036854775808 (2 ^ 63) и не *integer_type_suffix* или *integer_type_suffix* `L` или `l` доступен в качестве маркера, который сразу после "унарный минус" лексема оператора ([унарный минус-оператор](expressions.md#unary-minus-operator)), результатом является константа типа `long` со значением -9223372036854775808 (-2 ^ 63). В других случаях такие *decimal_integer_literal* имеет тип `ulong`.

#### <a name="real-literals"></a>Реальные литералы

Для записи значения типов используются реальные литералы `float`, `double`, и `decimal`.

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

Если не *real_type_suffix* указан, имеет тип действительный литерал `double`. В противном случае суффикс действительного типа определяет тип действительный литерал, следующим образом:

*  Действительный литерал с суффиксом `F` или `f` имеет тип `float`. Например, литералы `1f`, `1.5f`, `1e10f`, и `123.456F` типа `float`.
*  Действительный литерал с суффиксом `D` или `d` имеет тип `double`. Например, литералы `1d`, `1.5d`, `1e10d`, и `123.456D` типа `double`.
*  Действительный литерал с суффиксом `M` или `m` имеет тип `decimal`. Например, литералы `1m`, `1.5m`, `1e10m`, и `123.456M` типа `decimal`. Этот литерал преобразуется в `decimal` значение точное значение, и, при необходимости округления до ближайшего представимое значение с помощью банковское округление ([десятичного типа](types.md#the-decimal-type)). Любого масштаба, видимый в литерале сохраняется в том случае, если значение округляется, или значение равно нулю (в этом последнем случае знак и масштаб будет 0). Таким образом литерал `2.900m` будут анализироваться десятичное значение со знаком `0`, коэффициент `2900`и масштаб `3`.

Если указанный литерал невозможно представить в указанный тип, возникает ошибка времени компиляции.

Значение действительный литерал типа `float` или `double` определяется с помощью IEEE «округления до ближайшего целого» режим.

Обратите внимание, что в действительный литерал, всегда требуется десятичных цифр после десятичной запятой. Например `1.3F` — это реальный литерал но `1.F` не является.

#### <a name="character-literals"></a>Символьные литералы

Символьный литерал представляет один символ и обычно состоит из символа в кавычках, как показано на `'a'`.

Примечание. Грамматическая нотация ANTLR делает путаницу! В ANTLR, при написании `\'` это сокращение от одинарная кавычка `'`. И при написании `\\` это сокращение от одной обратной косой черты `\`. Поэтому первое правило для символьного литерала означает, что он начинается с одинарной кавычки, символ, а затем одинарная кавычка. И одиннадцать возможных простые escape-последовательности `\'`, `\"`, `\\`, `\0`, `\a`, `\b`, `\f`, `\n`, `\r`, `\t`, `\v`.

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

Символ, следующий за символом обратной косой черты (`\`) в *символ* должен быть одним из следующих символов: `'`, `"`, `\`, `0`, `a`, `b` , `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`. В противном случае возникает ошибка времени компиляции.

Шестнадцатеричная escape-последовательность представляет один знак Юникода, со значением, образованное шестнадцатеричный номер после "`\x`«.

Если значение, представленное символьный литерал больше, чем `U+FFFF`, возникает ошибка времени компиляции.

Управляющая последовательность символов Юникода ([последовательностей escape-символов Юникода](lexical-structure.md#unicode-character-escape-sequences)) в строковом литерале должно быть в диапазоне `U+0000` для `U+FFFF`.

Простая управляющая последовательность представляет кодировку символов Юникода, как описано в следующей таблице.


| __Escape-последовательность__ | __Имя символа__ | __Кодировка Юникод__ |
|---------------------|--------------------|----------------------|
| `\'`                | Одинарная кавычка       | `0x0027`             | 
| `\"`                | Двойная кавычка       | `0x0022`             | 
| `\\`                | Обратная косая черта          | `0x005C`             | 
| `\0`                | Null               | `0x0000`             | 
| `\a`                | Предупреждение              | `0x0007`             | 
| `\b`                | Backspace          | `0x0008`             | 
| `\f`                | Перевод страницы          | `0x000C`             | 
| `\n`                | Новая строка           | `0x000A`             | 
| `\r`                | Возврат каретки    | `0x000D`             | 
| `\t`                | Горизонтальная табуляция     | `0x0009`             | 
| `\v`                | Вертикальная табуляция       | `0x000B`             | 

Тип *character_literal* является `char`.

#### <a name="string-literals"></a>Строковые литералы

C# поддерживает два вида строковых литералов: ***строковые литералы regular*** и ***строковые литералы verbatim***.

Обычный строковый литерал состоит из нуля или более символов, заключенные в двойные кавычки, как показано на `"hello"`и могут содержаться оба простые escape-последовательности (например `\t` символа табуляции) и в шестнадцатеричном формате, так и в escape-последовательности Юникода.

Буквальный строковый литерал состоит из `@` символ за которым следует символ двойной кавычки, ноль или более символов и закрывающего символа двойной кавычки. Ниже приведен простой пример `@"hello"`. В буквального строкового литерала, символы между разделителями интерпретируются буквально, единственное исключение, *quote_escape_sequence*. В частности простые escape-последовательности и шестнадцатеричном формате и escape-последовательности Юникода, не обрабатываются в строковые литералы verbatim. Буквальный строковый литерал может занимать несколько строк.

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

Символ, следующий за символом обратной косой черты (`\`) в *regular_string_literal_character* должен быть одним из следующих символов: `'`, `"`, `\`, `0`, `a` , `b`, `f`, `n`, `r`, `t`, `u`, `U`, `x`, `v`. В противном случае возникает ошибка времени компиляции.

Пример
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
содержит различные строковые литералы. Последний строковый литерал, `j`, является буквального строкового литерала, занимает несколько строк. Символы в кавычках, включая пробелы, например символы новой строки, сохраняются буквально.

Поскольку Шестнадцатеричная escape-последовательность может иметь переменное число шестнадцатеричных цифр, строковый литерал `"\x123"` содержит один символ с шестнадцатеричным значением 123. Чтобы создать строку, содержащую символ с шестнадцатеричным значением 12, за которым следует символ 3, можно написать `"\x00123"` или `"\x12" + "3"` вместо этого.

Тип *string_literal* является `string`.

Каждый строковый литерал не обязательно приводит в новом экземпляре строки. Когда два или несколько строковых литералов, которые эквивалентны в соответствии с оператор равенства строк ([строковые операторы равенства](expressions.md#string-equality-operators)) отображаются в той же программе, см. такие строковые литералы к тому же экземпляру строки. Например выходные данные
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
является `True` поскольку два литерала ссылаются на один и тот же экземпляр строки.

#### <a name="interpolated-string-literals"></a>Интерполированные строковые литералы

Интерполированные строковые литералы похожи на строковые литералы, но содержит пропуски, разделенных `{` и `}`, при котором может возникнуть выражения. Во время выполнения выражения вычисляются с целью с текстовые формы подстановки в строку в месте, где встречается эта брешь в системе. Синтаксис и семантику интерполяция описаны в разделе ([интерполированные строки](expressions.md#interpolated-strings)).

Как и строковые литералы интерполированные строковые литералы может быть обычный или дословно. Интерполированные строковые литералы regular разделены с помощью `$"` и `"`, и интерполированные строковые литералы verbatim разделены `$@"` и `"`.

Как и другие литералы Лексический анализ интерполированной строки литерала изначально приводит один маркер, согласно ниже грамматики. Тем не менее перед синтаксический анализ один токен интерполированной строки литерала разбивается на несколько токенов для частей строки, включающий слабые места и входных элементов, выполняемых в «дыр» являются лексически анализируются еще раз. Это в свою очередь может привести к более интерполированные строковые литералы для обработки, но, если лексически исправить, в конечном итоге приведет к последовательность токенов для синтаксического анализа для обработки.

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

*Interpolated_string_literal* маркер будет интерпретировать как несколько маркеров и других входных элементов как описано ниже, в порядке появления в *interpolated_string_literal*:

* Вхождений следующих являются интерпретировать как отдельные отдельных токенов: начальные `$` входа, *interpolated_regular_string_whole*, *interpolated_regular_string_start*, *interpolated_regular_string_mid*, *interpolated_regular_string_end*, *interpolated_verbatim_string_whole*,  *interpolated_verbatim_string_start*, *interpolated_verbatim_string_mid* и *interpolated_verbatim_string_end*.
* Вхождения *regular_balanced_text* и *verbatim_balanced_text* между этими обрабатываются как *input_section* ([Лексический анализ ](lexical-structure.md#lexical-analysis)) и являются интерпретировать как результирующей последовательности элементов ввода. В свою очередь, они могут включать интерполированной строки литерала маркеры позволяют интерпретировать.

Синтаксический анализ будет перекомпоновать маркеры в *interpolated_string_expression* ([интерполированные строки](expressions.md#interpolated-strings)).

Примеры TODO


#### <a name="the-null-literal"></a>Литерал null

```antlr
null_literal
    : 'null'
    ;
```

*Null_literal* может быть неявно преобразован в ссылочный тип или тип, допускающий значение NULL.

### <a name="operators-and-punctuators"></a>Операторы и символы пунктуации

Существует несколько типов операторов и символы пунктуации. Операторы используются в выражениях для описания операций, связанных с одним или несколькими операндами. Например, выражение `a + b` использует `+` оператор, чтобы добавить два операнда `a` и `b`. Знаки пунктуации служат для группирования и разделения.

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

Вертикальная черта в *right_shift* и *right_shift_assignment* производства используются для указания того, что, в отличие от других производства в Синтаксическая грамматика, никакие символы не любого типа (даже не пробелы) разрешены между маркерами. Эти порождения обрабатываются особым образом, чтобы обеспечить правильную обработку *type_parameter_list*s ([параметры типа](classes.md#type-parameters)).

## <a name="pre-processing-directives"></a>Директивы предварительной обработки

Директивы предварительной обработки дают возможность условно пропускать разделы исходных файлов, чтобы отчет условиях ошибок и предупреждений и устанавливать отдельные области исходного кода. Термин «директивы препроцессора» используется только для обеспечения согласованности с языками программирования C и C++. В C# есть нет отдельного шага предварительной обработки; директивы предварительной обработки, обрабатываются как часть этапа лексического анализа.

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

Доступны следующие директивы предварительной обработки:

*  `#define` и `#undef`, которые используются для определения и отмены определения, соответственно, символы условной компиляции ([директивы объявления](lexical-structure.md#declaration-directives)).
*  `#if`, `#elif`, `#else`, и `#endif`, которые используются для условно пропускать части исходного кода ([директивы условной компиляции](lexical-structure.md#conditional-compilation-directives)).
*  `#line`, который используется для управления номера строк, генерируется для ошибок и предупреждений ([строки директивы](lexical-structure.md#line-directives)).
*  `#error` и `#warning`, которые используются для выдачи ошибок и предупреждений, соответственно ([диагностики директивы](lexical-structure.md#diagnostic-directives)).
*  `#region` и `#endregion`, которые используются для явной пометки части исходного кода ([директивы области](lexical-structure.md#region-directives)).
*  `#pragma`, который используется для указания компилятору необязательных сведений о контексте ([директивы Pragma](lexical-structure.md#pragma-directives)).

Директивы предварительной обработки, всегда занимает отдельную строку исходного кода и всегда начинается с `#` символ и имя директивы предварительной обработки. Пустое пространство может предшествовать `#` символ и между `#` символ и имя директивы.

Исходной строке, которая содержит `#define`, `#undef`, `#if`, `#elif`, `#else`, `#endif`, `#line`, или `#endregion` директива может заканчиваться однострочный комментарий. Комментарии с разделителями ( `/* */` стиль комментариев) не разрешены для строк исходного кода, содержащий директивы предварительной обработки.

Директивы предварительной обработки не токенов и не являются частью Синтаксическая грамматика C#. Тем не менее директивы предварительной обработки можно использовать для включения или исключения последовательностей маркеров и можно таким образом влиять на значение программы на C#. Например, при компиляции программы:
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
результаты в ту же последовательность токенов, программа:
```csharp
class C
{
    void F() {}
    void I() {}
}
```

Таким образом тогда как лексически, две программы являются довольно большие различия, синтаксически, они идентичны.

### <a name="conditional-compilation-symbols"></a>Символы условной компиляции

Условная компиляция, предоставляемую `#if`, `#elif`, `#else`, и `#endif` директивы осуществляется с помощью предварительной обработки выражения ([предварительной обработки выражения](lexical-structure.md#pre-processing-expressions)) и символы условной компиляции.

```antlr
conditional_symbol
    : '<Any identifier_or_keyword except true or false>'
    ;
```

Символ условной компиляции имеет два возможных состояния: ***определенные*** или ***неопределенный***. В начале лексические обработки исходного файла, символ условной компиляции не определено, если оно явно определено с помощью внешнего механизма (например, параметр командной строки компилятора). Когда `#define` обработке директивы, символ условной компиляции, упомянутый в этой директиве становится определенным в этом исходном файле. Этот символ остается определенным до `#undef` директив для обработки того же самого символа, или пока не будет достигнут конец исходного файла. Следствием этого является то, что `#define` и `#undef` директивы в одном исходном файле не оказывают влияния на другие исходные файлы в одной программе.

При обращении в выражении предварительной обработки, определенный символ условной компиляции имеет логическое значение `true`, и это неопределенный символ имеет логическое значение `false`. Нет необходимости что символы условной компиляции должны быть явно объявлены, прежде чем они указаны в предварительной обработки выражения. Вместо этого просто являются неопределенными Необъявленные символы и имеют значение `false`.

Пространство имен для символы условной компиляции, отделен от других именованных сущностей в программе на C#. Символы условной компиляции можно ссылаться только `#define` и `#undef` директивы и в предварительной обработки выражения.

### <a name="pre-processing-expressions"></a>Предварительная обработка выражения

Предварительная обработка выражений могут возникать в `#if` и `#elif` директивы. Операторы `!`, `==`, `!=`, `&&` и `||` разрешены в предварительной обработки выражения, и можно использовать скобки для группирования.

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

При обращении в выражении предварительной обработки, определенный символ условной компиляции имеет логическое значение `true`, и это неопределенный символ имеет логическое значение `false`.

Вычисление предварительной обработки выражения всегда дает логическое значение. Правила вычисления для предварительной обработки выражения являются такие же, как для константного выражения ([константные выражения](expressions.md#constant-expressions)), за исключением того, что только определяемых пользователем сущностей, которые можно указывать символы условной компиляции .

### <a name="declaration-directives"></a>Объявление директивы

Директивы объявления используются для определения или отмены определения символы условной компиляции.

```antlr
pp_declaration
    : whitespace? '#' whitespace? 'define' whitespace conditional_symbol pp_new_line
    | whitespace? '#' whitespace? 'undef' whitespace conditional_symbol pp_new_line
    ;

pp_new_line
    : whitespace? single_line_comment? new_line
    ;
```

Обработка `#define` директива вызывает данный символ условной компиляции определенным, начиная с исходной строки, следующей за директивой. Аналогично, обработку `#undef` директива приводит данный символ условной компиляции неопределенным, начиная с исходной строки, следующей за директивой.

Любой `#define` и `#undef` директивы в файле исходного кода должно находиться перед первым *маркера* ([маркеры](lexical-structure.md#tokens)) в исходном файле; иначе во время компиляции возникает ошибка. Интуитивно понятно `#define` и `#undef` директивы должно предшествовать любой «реальный код» в исходном файле.

Пример:
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
является допустимым поскольку `#define` директивы перед первым токеном ( `namespace` ключевое слово) в исходном файле.

Следующий пример приводит к ошибке времени компиляции, так как `#define` следует за фактическим кодом:
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

Объект `#define` можно определить символ условной компиляции, которое уже определено, без, что все промежуточные `#undef` данного символа. В приведенном ниже примере определяет символ условной компиляции `A` и определяющий его снова.
```csharp
#define A
#define A
```

Объект `#undef` может «отменить» символ условной компиляции, который не определен. В приведенном ниже примере определяет символ условной компиляции `A` и затем отменяет определение его дважды; хотя второй `#undef` не оказывает влияния, он по-прежнему допустим.
```csharp
#define A
#undef A
#undef A
```

### <a name="conditional-compilation-directives"></a>Директивы условной компиляции

Директивы условной компиляции используются для условного включения или исключения частей исходного файла.

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

Как указано в синтаксисе директив условной компиляции должно быть записано как наборами, состоящими из, в порядке, `#if` директивы, ноль или более `#elif` директивы, нуль или один `#else` директивы и `#endif` директива. Между этими директивами находятся условные разделы исходного кода. Каждый раздел управляется немедленно предшествующей директиве. Условный раздел может содержать вложенные директивы условной компиляции условии они образуют полные наборы.

Объект *pp_conditional* выбирает максимум одну из вложенных *conditional_section*s для обычной лексические обработки:

*  *Pp_expression*s из `#if` и `#elif` директивы вычисляются в порядке, пока не дает одно `true`. Если выражение выдает `true`, *conditional_section* соответствующей директивы выбран.
*  Если все *pp_expression*s yield `false`и если `#else` присутствует директива *conditional_section* из `#else` директива выбран.
*  В противном случае — нет *conditional_section* выбран.

Выбранный *conditional_section*, если есть, обрабатывается как обычный *input_section*: исходного кода, содержащегося в разделе необходимо следовать лексическая грамматика: токены создаются из источника код в разделе; и директивы предварительной обработки в разделе предписанных эффектами.

Оставшиеся *conditional_section*s, если таковое имеется, обрабатываются как *skipped_section*s: за исключением директивы предварительной обработки исходного кода в разделе не обязан соблюдать лексическая грамматика; нет токены создаются из исходного кода в разделе; и директивы предварительной обработки в разделе, должны быть лексически правильным, но, в противном случае не обрабатываются. В рамках *conditional_section* , обрабатывается как *skipped_section*, все вложенные *conditional_section*s (содержится в вложенные `#if`... `#endif` и `#region`... `#endregion` конструкции) также обрабатываются как *skipped_section*s.

В следующем примере показано, как условной компиляции, можно создавать вложенные директивы:
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

За исключением директивы предварительной обработки пропущенных исходный код не подлежащий лексическому анализу. Например, допустим следующий несмотря на комментарий без признака завершения в `#else` разделе:
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

Обратите внимание, что директивы предварительной обработки должны быть лексически правильными даже в пропущенных разделах исходного кода.

Директивы предварительной обработки, не обрабатываются, когда они присутствуют внутри многострочного входных элементов. Например, программа:
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
результаты в выходных данных:
```
hello,
#if Debug
        world
#else
        Nebraska
#endif
```

В особенных случаях набор директивы предварительной обработки, который обрабатывается могут зависеть от оценки *pp_expression*. Пример:
```csharp
#if X
    /*
#else
    /* */ class Q { }
#endif
```
всегда создает же поток лексем (`class` `Q` `{` `}`), независимо от того, нужно ли `X` определен. Если `X` будет определен, являются обрабатываются только директивы `#if` и `#endif`из- за многострочного комментария. Если `X` является неопределенным, затем три директивы (`#if`, `#else`, `#endif`) являются частью набора директив.

### <a name="diagnostic-directives"></a>Директивы диагностики

Директивы диагностики позволяют явно создавать ошибки и предупреждения, отображаемые в так же, как другие ошибки времени компиляции и предупреждения.

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

Пример:
```csharp
#warning Code review needed before check-in

#if Debug && Retail
    #error A build can't be both debug and retail
#endif

class Test {...}
```
всегда выдает предупреждение («проверка кода до возврата требуется») и вызывает ошибку времени компиляции («сборки не может быть как для отладки, так и для розничной торговли») Если условных символов `Debug` и `Retail` определены. Обратите внимание, что *pp_message* могут содержать произвольный текст; в частности, оно не должно содержать правильный формат маркеров, как показано в одинарные кавычки в слове `can't`.

### <a name="region-directives"></a>Директивы региона

Директивы области позволяют явным образом пометить области исходного кода.

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

Нет семантического значения присоединяется к области; регионы предназначены для использования в программу самим разработчиком и автоматические средства для пометки части исходного кода. Сообщения, заданного в `#region` или `#endregion` директива точно так же не имеет семантического значения; он просто служит для определения области. Сопоставление `#region` и `#endregion` директивы может иметь другие *pp_message*s.

Обработка лексической области:
```csharp
#region
...
#endregion
```
точно соответствует Лексическая обработка директивы условной компиляции в формате:
```csharp
#if true
...
#endif
```

### <a name="line-directives"></a>Директивы строк

Директивы строк может использоваться для изменения номера строк и имен исходных файлов, выводятся компилятором в выходных данных, такие как предупреждения и ошибки, и, которые используются в информационные атрибуты вызывающего объекта ([информационные атрибуты вызывающего объекта](attributes.md#caller-info-attributes)).

Директивы строк чаще всего используются в средствах метапрограммирования, Создание исходного кода C# из другого текстового ввода.

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

Если аргумент `#line` директив, компилятор сообщает настоящие номера строк и имен исходных файлов в своих выходных данных. При обработке `#line` директива, которая включает в себя *line_indicator* , не `default`, компилятор обрабатывает строки после директивы как имеющий указанный номер строки (и имя файла, если указано).

Объект `#line default` директива отменяет эффект всех предшествующих директив #line. Компилятор сообщает сведения о строке значение true, для последующих строк, как если нет `#line` директивы будут обработаны.

Объект `#line hidden` директива не действует для файла и номера строки, полученные по ошибке сообщения, но влияет на отладку на исходном уровне. При отладке, все строки между `#line hidden` директивы и последующих `#line` директива (это не `#line hidden`) имеют нет информация о номере строки. При пошаговом выполнении кода в отладчике, эти строки будут пропущены полностью.

Обратите внимание, что *имя_файла* отличается от обычного строкового литерала, что escape-символы, не обрабатываются; "`\`" символ просто означает символ обычные обратной косой черты в *имя_файла*.

### <a name="pragma-directives"></a>Директивы pragma

`#pragma` Директивы предварительной обработки используется для указания компилятору необязательных сведений о контексте. Сведения, указанные в `#pragma` директива будет никогда не изменяют семантику программы.

```antlr
pp_pragma
    : whitespace? '#' whitespace? 'pragma' whitespace pragma_body pp_new_line
    ;

pragma_body
    : pragma_warning_body
    ;
```

C# предоставляет `#pragma` директивы для управления предупреждениями компилятора. Будущие версии языка могут включать дополнительные `#pragma` директивы. Чтобы обеспечить взаимодействие с другими компиляторами C#, компилятор Microsoft C# выдает ошибки компиляции для неизвестных `#pragma` директивы; такие директивы не формировать предупреждения, тем не менее.

#### <a name="pragma-warning"></a>В директиве pragma warning

`#pragma warning` Директива используется для отключения или восстановления всех или определенный набор предупреждение сообщений во время компиляции последующего текста программы.

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

Объект `#pragma warning` директива, исключающую список предупреждений, влияет на все предупреждения. Объект `#pragma warning` директива включает в себя список предупреждений влияет только на предупреждения, которые указаны в списке.

Объект `#pragma warning disable` директив отключает все или заданный набор предупреждений.

Объект `#pragma warning restore` директив восстанавливает все или заданный набор предупреждений с состоянием, в действительности применялся в начале блока компиляции. Обратите внимание, что если конкретного предупреждения было отключено извне, `#pragma warning restore` (для всех или для конкретного предупреждения) не включит это предупреждение.

В следующем примере показано использование `#pragma warning` для временного отключения этого предупреждения, переданные при устаревшим ссылкой на члены, используя номер предупреждения компилятора Microsoft C#.
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
