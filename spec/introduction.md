# <a name="introduction"></a><span data-ttu-id="2685c-101">Вступление</span><span class="sxs-lookup"><span data-stu-id="2685c-101">Introduction</span></span>

<span data-ttu-id="2685c-102">C# (произносится как "си шарп") — простой, современный объектно-ориентированный и типобезопасный язык программирования.</span><span class="sxs-lookup"><span data-stu-id="2685c-102">C# (pronounced "See Sharp") is a simple, modern, object-oriented, and type-safe programming language.</span></span> <span data-ttu-id="2685c-103">C# относится к широко известному семейству языков C и будет немедленно знакомые программистам C, C++ и Java.</span><span class="sxs-lookup"><span data-stu-id="2685c-103">C# has its roots in the C family of languages and will be immediately familiar to C, C++, and Java programmers.</span></span> <span data-ttu-id="2685c-104">C# Стандартизован ECMA International в качестве ***ECMA-334*** standard и ISO/IEC как ***ISO/IEC 23270*** standard.</span><span class="sxs-lookup"><span data-stu-id="2685c-104">C# is standardized by ECMA International as the ***ECMA-334*** standard and by ISO/IEC as the ***ISO/IEC 23270*** standard.</span></span> <span data-ttu-id="2685c-105">Компилятор с C# корпорации Майкрософт для .NET Framework является соответствующая реализация обоих этих стандартов.</span><span class="sxs-lookup"><span data-stu-id="2685c-105">Microsoft's C# compiler for the .NET Framework is a conforming implementation of both of these standards.</span></span>

<span data-ttu-id="2685c-106">C# является объектно-ориентированным языком, но поддерживает также и ***компонентно-ориентированное*** программирование.</span><span class="sxs-lookup"><span data-stu-id="2685c-106">C# is an object-oriented language, but C# further includes support for ***component-oriented*** programming.</span></span> <span data-ttu-id="2685c-107">Разработка современных приложений все больше тяготеет к созданию программных компонентов в форме автономных и самоописательных пакетов, реализующих отдельные функциональные возможности.</span><span class="sxs-lookup"><span data-stu-id="2685c-107">Contemporary software design increasingly relies on software components in the form of self-contained and self-describing packages of functionality.</span></span> <span data-ttu-id="2685c-108">Важная особенность таких компонентов — это модель программирования на основе свойств, методов и событий. Каждый компонент имеет атрибуты, предоставляющие декларативные сведения о компоненте, а также встроенные элементы документации.</span><span class="sxs-lookup"><span data-stu-id="2685c-108">Key to such components is that they present a programming model with properties, methods, and events; they have attributes that provide declarative information about the component; and they incorporate their own documentation.</span></span> <span data-ttu-id="2685c-109">C# предоставляет языковые конструкции, непосредственно поддерживающие такую концепцию работы благодаря этому C# очень естественного языка, в котором для создания и применения программных компонентов.</span><span class="sxs-lookup"><span data-stu-id="2685c-109">C# provides language constructs to directly support these concepts, making C# a very natural language in which to create and use software components.</span></span>

<span data-ttu-id="2685c-110">Несколько C# функции помощь в создании надежных и устойчивых приложений: ***Сборка мусора*** автоматически освобождает память, занятую неиспользуемые объекты; ***обработки исключений*** предоставляет структурированный и расширяемый способ определения ошибки и восстановления; и ***типобезопасный*** языка делает невозможной для чтения из неинициализированных переменных приведения типов массивов за пределы их границы или выполнить unchecked для индексирования.</span><span class="sxs-lookup"><span data-stu-id="2685c-110">Several C# features aid in the construction of robust and durable applications: ***Garbage collection*** automatically reclaims memory occupied by unused objects; ***exception handling*** provides a structured and extensible approach to error detection and recovery; and the ***type-safe*** design of the language makes it impossible to read from uninitialized variables, to index arrays beyond their bounds, or to perform unchecked type casts.</span></span>

<span data-ttu-id="2685c-111">В C# существует ***единая система типов***.</span><span class="sxs-lookup"><span data-stu-id="2685c-111">C# has a ***unified type system***.</span></span> <span data-ttu-id="2685c-112">Все типы C#, включая типы-примитивы, такие как `int` и `double`, наследуют от одного корневого типа `object`.</span><span class="sxs-lookup"><span data-stu-id="2685c-112">All C# types, including primitive types such as `int` and `double`, inherit from a single root `object` type.</span></span> <span data-ttu-id="2685c-113">Таким образом, все типы используют общий набор операций, и значения любого типа можно хранить, передавать и обрабатывать схожим образом.</span><span class="sxs-lookup"><span data-stu-id="2685c-113">Thus, all types share a set of common operations, and values of any type can be stored, transported, and operated upon in a consistent manner.</span></span> <span data-ttu-id="2685c-114">Кроме того, C# поддерживает пользовательские ссылочные типы и типы значений, позволяя как динамически выделять память для объектов, так и хранить упрощенные структуры в стеке.</span><span class="sxs-lookup"><span data-stu-id="2685c-114">Furthermore, C# supports both user-defined reference types and value types, allowing dynamic allocation of objects as well as in-line storage of lightweight structures.</span></span>

<span data-ttu-id="2685c-115">Чтобы убедиться, что программы на C# и библиотеки со временем могут развиваться совместимость, много внимания было уделено ***управление версиями*** в разработке C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-115">To ensure that C# programs and libraries can evolve over time in a compatible manner, much emphasis has been placed on ***versioning*** in C#'s design.</span></span> <span data-ttu-id="2685c-116">Многие языки программирования обходят вниманием этот вопрос, и в результате программы на этих языках ломаются чаще, чем хотелось бы, при выходе новых версий зависимых библиотек.</span><span class="sxs-lookup"><span data-stu-id="2685c-116">Many programming languages pay little attention to this issue, and, as a result, programs written in those languages break more often than necessary when newer versions of dependent libraries are introduced.</span></span> <span data-ttu-id="2685c-117">Аспекты разработки C#, на которые повлияли вопросы управления версиями раздельные `virtual` и `override` модификаторы, правила разрешения перегрузки методов и поддержка явного объявления членов интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2685c-117">Aspects of C#'s design that were directly influenced by versioning considerations include the separate `virtual` and `override` modifiers, the rules for method overload resolution, and support for explicit interface member declarations.</span></span>

<span data-ttu-id="2685c-118">В оставшейся части этой главе описываются основные возможности языка C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-118">The rest of this chapter describes the essential features of the C# language.</span></span> <span data-ttu-id="2685c-119">Несмотря на то, что в последующих главах описывают правила и исключения подробно ориентированные и иногда математические, для ясности и краткости за счет полноты стремится в этой главе.</span><span class="sxs-lookup"><span data-stu-id="2685c-119">Although later chapters describe rules and exceptions in a detail-oriented and sometimes mathematical manner, this chapter strives for clarity and brevity at the expense of completeness.</span></span> <span data-ttu-id="2685c-120">Целью является предоставить общие сведения о языке, которая будет полезна при написании простых программ и считывание в последующих главах.</span><span class="sxs-lookup"><span data-stu-id="2685c-120">The intent is to provide the reader with an introduction to the language that will facilitate the writing of early programs and the reading of later chapters.</span></span>

## <a name="hello-world"></a><span data-ttu-id="2685c-121">Здравствуй, мир</span><span class="sxs-lookup"><span data-stu-id="2685c-121">Hello world</span></span>

<span data-ttu-id="2685c-122">Для первого знакомства с языком программирования традиционно используется программа "Hello, World".</span><span class="sxs-lookup"><span data-stu-id="2685c-122">The "Hello, World" program is traditionally used to introduce a programming language.</span></span> <span data-ttu-id="2685c-123">Вот ее пример на C#:</span><span class="sxs-lookup"><span data-stu-id="2685c-123">Here it is in C#:</span></span>

```csharp
using System;

class Hello
{
    static void Main() {
        Console.WriteLine("Hello, World");
    }
}
```

<span data-ttu-id="2685c-124">Файлы исходного кода C# обычно имеют расширение `.cs`.</span><span class="sxs-lookup"><span data-stu-id="2685c-124">C# source files typically have the file extension `.cs`.</span></span> <span data-ttu-id="2685c-125">Предположим, что программа «Hello, World» хранится в файле `hello.cs`, программу можно скомпилировать с помощью командной строки компилятора Microsoft C#</span><span class="sxs-lookup"><span data-stu-id="2685c-125">Assuming that the "Hello, World" program is stored in the file `hello.cs`, the program can be compiled with the Microsoft C# compiler using the command line</span></span>
```
csc hello.cs
```
<span data-ttu-id="2685c-126">что порождает исполняемую сборку с именем `hello.exe`.</span><span class="sxs-lookup"><span data-stu-id="2685c-126">which produces an executable assembly named `hello.exe`.</span></span> <span data-ttu-id="2685c-127">— Выходные данные этого приложения при его выполнении</span><span class="sxs-lookup"><span data-stu-id="2685c-127">The output produced by this application when it is run is</span></span>
```
Hello, World
```

<span data-ttu-id="2685c-128">Программа "Hello, World" начинается с директивы `using`, которая ссылается на пространство имен `System`.</span><span class="sxs-lookup"><span data-stu-id="2685c-128">The "Hello, World" program starts with a `using` directive that references the `System` namespace.</span></span> <span data-ttu-id="2685c-129">Пространства имен позволяют иерархически упорядочивать программы и библиотеки C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-129">Namespaces provide a hierarchical means of organizing C# programs and libraries.</span></span> <span data-ttu-id="2685c-130">Пространства имен содержат типы и другие пространства имен. Например, пространство имен `System` содержит несколько типов (в том числе используемый в нашей программе класс `Console`) и несколько других пространств имен, таких как `IO` и `Collections`.</span><span class="sxs-lookup"><span data-stu-id="2685c-130">Namespaces contain types and other namespaces—for example, the `System` namespace contains a number of types, such as the `Console` class referenced in the program, and a number of other namespaces, such as `IO` and `Collections`.</span></span> <span data-ttu-id="2685c-131">Директива `using`, которая ссылается на пространство имен, позволяет использовать типы из этого пространства имен без указания полного имени.</span><span class="sxs-lookup"><span data-stu-id="2685c-131">A `using` directive that references a given namespace enables unqualified use of the types that are members of that namespace.</span></span> <span data-ttu-id="2685c-132">Благодаря директиве `using` в коде программы можно использовать сокращенное имя `Console.WriteLine` вместо полного варианта `System.Console.WriteLine`.</span><span class="sxs-lookup"><span data-stu-id="2685c-132">Because of the `using` directive, the program can use `Console.WriteLine` as shorthand for `System.Console.WriteLine`.</span></span>

<span data-ttu-id="2685c-133">Класс `Hello`, объявленный в программе "Hello, World", имеет только один член — это метод с именем `Main`.</span><span class="sxs-lookup"><span data-stu-id="2685c-133">The `Hello` class declared by the "Hello, World" program has a single member, the method named `Main`.</span></span> <span data-ttu-id="2685c-134">`Main` Метод объявлен с `static` модификатор.</span><span class="sxs-lookup"><span data-stu-id="2685c-134">The `Main` method is declared with the `static` modifier.</span></span> <span data-ttu-id="2685c-135">Методы экземпляра могут ссылаться на конкретный экземпляр объекта, используя ключевое слово `this`, а статические методы работают без ссылки на конкретный объект.</span><span class="sxs-lookup"><span data-stu-id="2685c-135">While instance methods can reference a particular enclosing object instance using the keyword `this`, static methods operate without reference to a particular object.</span></span> <span data-ttu-id="2685c-136">По стандартному соглашению точкой входа программы является статический метод с именем `Main`.</span><span class="sxs-lookup"><span data-stu-id="2685c-136">By convention, a static method named `Main` serves as the entry point of a program.</span></span>

<span data-ttu-id="2685c-137">Выходные данные программы создаются в методе `WriteLine` класса `Console` из пространства имен `System`.</span><span class="sxs-lookup"><span data-stu-id="2685c-137">The output of the program is produced by the `WriteLine` method of the `Console` class in the `System` namespace.</span></span> <span data-ttu-id="2685c-138">Этот класс предоставляется в библиотеках классов .NET Framework, которые по умолчанию автоматически ссылается компилятор Microsoft C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-138">This class is provided by the .NET Framework class libraries, which, by default, are automatically referenced by the Microsoft C# compiler.</span></span> <span data-ttu-id="2685c-139">Обратите внимание, что C# сам собственная библиотека времени выполнения.</span><span class="sxs-lookup"><span data-stu-id="2685c-139">Note that C# itself does not have a separate runtime library.</span></span> <span data-ttu-id="2685c-140">Вместо этого .NET Framework — это библиотека среды выполнения C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-140">Instead, the .NET Framework is the runtime library of C#.</span></span>

## <a name="program-structure"></a><span data-ttu-id="2685c-141">Структура программы</span><span class="sxs-lookup"><span data-stu-id="2685c-141">Program structure</span></span>

<span data-ttu-id="2685c-142">В C# основными понятиями организационной структуры являются ***программы***, ***пространства имен***, ***типы***, ***члены*** и ***сборки***.</span><span class="sxs-lookup"><span data-stu-id="2685c-142">The key organizational concepts in C# are ***programs***, ***namespaces***, ***types***, ***members***, and ***assemblies***.</span></span> <span data-ttu-id="2685c-143">Программа на языке C# состоит из одного или нескольких файлов.</span><span class="sxs-lookup"><span data-stu-id="2685c-143">C# programs consist of one or more source files.</span></span> <span data-ttu-id="2685c-144">В программе объявляются типы, которые содержат члены. Эти типы можно организовать в пространства имен.</span><span class="sxs-lookup"><span data-stu-id="2685c-144">Programs declare types, which contain members and can be organized into namespaces.</span></span> <span data-ttu-id="2685c-145">Примерами типов являются классы и интерфейсы.</span><span class="sxs-lookup"><span data-stu-id="2685c-145">Classes and interfaces are examples of types.</span></span> <span data-ttu-id="2685c-146">К членам относятся поля, методы, свойства и события.</span><span class="sxs-lookup"><span data-stu-id="2685c-146">Fields, methods, properties, and events are examples of members.</span></span> <span data-ttu-id="2685c-147">При компиляции программы на C# упаковываются в сборки.</span><span class="sxs-lookup"><span data-stu-id="2685c-147">When C# programs are compiled, they are physically packaged into assemblies.</span></span> <span data-ttu-id="2685c-148">Сборки, обычно имеют расширение файла `.exe` или `.dll`, в зависимости от ли они реализуют ***приложений*** или ***библиотеки***.</span><span class="sxs-lookup"><span data-stu-id="2685c-148">Assemblies typically have the file extension `.exe` or `.dll`, depending on whether they implement ***applications*** or ***libraries***.</span></span>

<span data-ttu-id="2685c-149">Пример</span><span class="sxs-lookup"><span data-stu-id="2685c-149">The example</span></span>

```csharp
using System;

namespace Acme.Collections
{
    public class Stack
    {
        Entry top;

        public void Push(object data) {
            top = new Entry(top, data);
        }

        public object Pop() {
            if (top == null) throw new InvalidOperationException();
            object result = top.data;
            top = top.next;
            return result;
        }

        class Entry
        {
            public Entry next;
            public object data;
    
            public Entry(Entry next, object data) {
                this.next = next;
                this.data = data;
            }
        }
    }
}
```
<span data-ttu-id="2685c-150">объявляет класс с именем `Stack` в пространство имен с именем `Acme.Collections`.</span><span class="sxs-lookup"><span data-stu-id="2685c-150">declares a class named `Stack` in a namespace called `Acme.Collections`.</span></span> <span data-ttu-id="2685c-151">Полное имя этого класса: `Acme.Collections.Stack`.</span><span class="sxs-lookup"><span data-stu-id="2685c-151">The fully qualified name of this class is `Acme.Collections.Stack`.</span></span> <span data-ttu-id="2685c-152">Этот класс содержит несколько членов: поле с именем `top`, два метода с именами `Push` и `Pop`, а также вложенный класс с именем `Entry`.</span><span class="sxs-lookup"><span data-stu-id="2685c-152">The class contains several members: a field named `top`, two methods named `Push` and `Pop`, and a nested class named `Entry`.</span></span> <span data-ttu-id="2685c-153">Класс `Entry`, в свою очередь, содержит три члена: поле с именем `next`, поле с именем `data` и конструктор.</span><span class="sxs-lookup"><span data-stu-id="2685c-153">The `Entry` class further contains three members: a field named `next`, a field named `data`, and a constructor.</span></span> <span data-ttu-id="2685c-154">Если мы сохраним исходный код этого примера в файле `acme.cs`, то для его компиляции нужно выполнить такую командную строку:</span><span class="sxs-lookup"><span data-stu-id="2685c-154">Assuming that the source code of the example is stored in the file `acme.cs`, the command line</span></span>

```
csc /t:library acme.cs
```
<span data-ttu-id="2685c-155">Результатом компиляции будет библиотека (код без точки входа `Main`), сохраненная в сборке с именем `acme.dll`.</span><span class="sxs-lookup"><span data-stu-id="2685c-155">compiles the example as a library (code without a `Main` entry point) and produces an assembly named `acme.dll`.</span></span>

<span data-ttu-id="2685c-156">Сборки содержат исполняемый код в виде ***промежуточный язык*** инструкции (IL) и символьную информацию в виде ***метаданных***.</span><span class="sxs-lookup"><span data-stu-id="2685c-156">Assemblies contain executable code in the form of ***Intermediate Language*** (IL) instructions, and symbolic information in the form of ***metadata***.</span></span> <span data-ttu-id="2685c-157">Перед выполнением сборки ее код на языке IL автоматически преобразуется в код для конкретного процессора. Эту задачу выполняет JIT-компилятор среды .NET CLR (Common Language Runtime).</span><span class="sxs-lookup"><span data-stu-id="2685c-157">Before it is executed, the IL code in an assembly is automatically converted to processor-specific code by the Just-In-Time (JIT) compiler of .NET Common Language Runtime.</span></span>

<span data-ttu-id="2685c-158">Cборка полностью описывает сама себя и содержит весь код и метаданные, поэтому в C# не используются директивы `#include` и файлы заголовков.</span><span class="sxs-lookup"><span data-stu-id="2685c-158">Because an assembly is a self-describing unit of functionality containing both code and metadata, there is no need for `#include` directives and header files in C#.</span></span> <span data-ttu-id="2685c-159">Чтобы использовать в программе C# открытые типы и члены, содержащиеся в определенной сборке, вам достаточно указать ссылку на эту сборку при компиляции программы.</span><span class="sxs-lookup"><span data-stu-id="2685c-159">The public types and members contained in a particular assembly are made available in a C# program simply by referencing that assembly when compiling the program.</span></span> <span data-ttu-id="2685c-160">Например, эта программа использует класс `Acme.Collections.Stack` из сборки `acme.dll`:</span><span class="sxs-lookup"><span data-stu-id="2685c-160">For example, this program uses the `Acme.Collections.Stack` class from the `acme.dll` assembly:</span></span>

```csharp
using System;
using Acme.Collections;

class Test
{
    static void Main() {
        Stack s = new Stack();
        s.Push(1);
        s.Push(10);
        s.Push(100);
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
        Console.WriteLine(s.Pop());
    }
}
```
<span data-ttu-id="2685c-161">Если программа хранится в файле `test.cs`, когда `test.cs` компилируется, `acme.dll` сборки можно ссылаться с помощью компилятора `/r` параметр:</span><span class="sxs-lookup"><span data-stu-id="2685c-161">If the program is stored in the file `test.cs`, when `test.cs` is compiled, the `acme.dll` assembly can be referenced using the compiler's `/r` option:</span></span>

```
csc /r:acme.dll test.cs
```
<span data-ttu-id="2685c-162">Эта команда создает исполняемую сборку с именем `test.exe`, которая при запуске возвращает такие данные:</span><span class="sxs-lookup"><span data-stu-id="2685c-162">This creates an executable assembly named `test.exe`, which, when run, produces the output:</span></span>

```
100
10
1
```
<span data-ttu-id="2685c-163">В C# исходный текст программы можно хранить в нескольких исходных файлах.</span><span class="sxs-lookup"><span data-stu-id="2685c-163">C# permits the source text of a program to be stored in several source files.</span></span> <span data-ttu-id="2685c-164">При компиляции многофайловой программы на C# все исходные файлы обрабатываются вместе, и все они могут свободно ссылаться друг на друга. По сути обработка выполняется так, как если бы все исходные файлы были объединены в один большой файл.</span><span class="sxs-lookup"><span data-stu-id="2685c-164">When a multi-file C# program is compiled, all of the source files are processed together, and the source files can freely reference each other—conceptually, it is as if all the source files were concatenated into one large file before being processed.</span></span> <span data-ttu-id="2685c-165">В C# никогда не используются опережающие объявления, поскольку порядок объявления, за редким исключением, не играет никакой роли.</span><span class="sxs-lookup"><span data-stu-id="2685c-165">Forward declarations are never needed in C# because, with very few exceptions, declaration order is insignificant.</span></span> <span data-ttu-id="2685c-166">В C# нет требований объявлять только один открытый тип в одном исходном файле, а также имя исходного файла не обязано совпадать с типом, объявляемом в этом файле.</span><span class="sxs-lookup"><span data-stu-id="2685c-166">C# does not limit a source file to declaring only one public type nor does it require the name of the source file to match a type declared in the source file.</span></span>

## <a name="types-and-variables"></a><span data-ttu-id="2685c-167">Типы и переменные</span><span class="sxs-lookup"><span data-stu-id="2685c-167">Types and variables</span></span>

<span data-ttu-id="2685c-168">В C# существуют две разновидности типов: ***ссылочные типы*** и ***типы значений***.</span><span class="sxs-lookup"><span data-stu-id="2685c-168">There are two kinds of types in C#: ***value types*** and ***reference types***.</span></span> <span data-ttu-id="2685c-169">Переменные типа значений содержат непосредственно данные, а в переменных ссылочных типов хранятся ссылки на нужные данные, которые именуются объектами.</span><span class="sxs-lookup"><span data-stu-id="2685c-169">Variables of value types directly contain their data whereas variables of reference types store references to their data, the latter being known as objects.</span></span> <span data-ttu-id="2685c-170">Две переменные ссылочного типа могут ссылаться на один и тот же объект, поэтому может случиться так, что операции над одной переменной затронут объект, на который ссылается другая переменная.</span><span class="sxs-lookup"><span data-stu-id="2685c-170">With reference types, it is possible for two variables to reference the same object and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="2685c-171">Каждая переменная типа значения имеет собственную копию данных, и операции над одной переменной не могут затрагивать другую (за исключением переменных параметров `ref` и `out`).</span><span class="sxs-lookup"><span data-stu-id="2685c-171">With value types, the variables each have their own copy of the data, and it is not possible for operations on one to affect the other (except in the case of `ref` and `out` parameter variables).</span></span>

<span data-ttu-id="2685c-172">Типы значений C# подразделяются ***простых типов***, ***типы перечисления***, ***типы структур***, и ***обнуляемые типы***и справочник по C# типы подразделяются ***типы классов***, ***типы интерфейсов***, ***типы массивов***, и ***типы делегатов***.</span><span class="sxs-lookup"><span data-stu-id="2685c-172">C#'s value types are further divided into ***simple types***, ***enum types***, ***struct types***, and ***nullable types***, and C#'s reference types are further divided into ***class types***, ***interface types***, ***array types***, and ***delegate types***.</span></span>

<span data-ttu-id="2685c-173">Ниже приведены общие сведения о системе типов C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-173">The following table provides an overview of C#'s type system.</span></span>

| <span data-ttu-id="2685c-174">__Категория__</span><span class="sxs-lookup"><span data-stu-id="2685c-174">__Category__</span></span>    |                 | <span data-ttu-id="2685c-175">__Описание__</span><span class="sxs-lookup"><span data-stu-id="2685c-175">__Description__</span></span> |
|-----------------|-----------------|-----------------|
| <span data-ttu-id="2685c-176">Типы значений</span><span class="sxs-lookup"><span data-stu-id="2685c-176">Value types</span></span>     | <span data-ttu-id="2685c-177">Простые типы</span><span class="sxs-lookup"><span data-stu-id="2685c-177">Simple types</span></span>    | <span data-ttu-id="2685c-178">Целочисленный со знаком: `sbyte`, `short`, `int`,`long`</span><span class="sxs-lookup"><span data-stu-id="2685c-178">Signed integral: `sbyte`, `short`, `int`, `long`</span></span> |
|                 |                 | <span data-ttu-id="2685c-179">Целочисленный без знака: `byte`, `ushort`, `uint`,`ulong`</span><span class="sxs-lookup"><span data-stu-id="2685c-179">Unsigned integral: `byte`, `ushort`, `uint`, `ulong`</span></span> |
|                 |                 | <span data-ttu-id="2685c-180">Символы Юникода: `char`</span><span class="sxs-lookup"><span data-stu-id="2685c-180">Unicode characters: `char`</span></span> |
|                 |                 | <span data-ttu-id="2685c-181">IEEE-представление с плавающей запятой: `float`, `double`</span><span class="sxs-lookup"><span data-stu-id="2685c-181">IEEE floating point: `float`, `double`</span></span> |
|                 |                 | <span data-ttu-id="2685c-182">Десятичный с повышенной точностью: `decimal`</span><span class="sxs-lookup"><span data-stu-id="2685c-182">High-precision decimal: `decimal`</span></span> |
|                 |                 | <span data-ttu-id="2685c-183">Логическое значение: `bool`</span><span class="sxs-lookup"><span data-stu-id="2685c-183">Boolean: `bool`</span></span> |
|                 | <span data-ttu-id="2685c-184">Типы перечисления</span><span class="sxs-lookup"><span data-stu-id="2685c-184">Enum types</span></span>      | <span data-ttu-id="2685c-185">Пользовательские типы в формате `enum E {...}`</span><span class="sxs-lookup"><span data-stu-id="2685c-185">User-defined types of the form `enum E {...}`</span></span> |
|                 | <span data-ttu-id="2685c-186">Типы структур</span><span class="sxs-lookup"><span data-stu-id="2685c-186">Struct types</span></span>    | <span data-ttu-id="2685c-187">Пользовательские типы в формате `struct S {...}`</span><span class="sxs-lookup"><span data-stu-id="2685c-187">User-defined types of the form `struct S {...}`</span></span> |
|                 | <span data-ttu-id="2685c-188">Типы, допускающие значения NULL</span><span class="sxs-lookup"><span data-stu-id="2685c-188">Nullable types</span></span>  | <span data-ttu-id="2685c-189">Расширения других типов значений, допускающие значение `null`</span><span class="sxs-lookup"><span data-stu-id="2685c-189">Extensions of all other value types with a `null` value</span></span> |
| <span data-ttu-id="2685c-190">Ссылочные типы</span><span class="sxs-lookup"><span data-stu-id="2685c-190">Reference types</span></span> | <span data-ttu-id="2685c-191">Типы классов</span><span class="sxs-lookup"><span data-stu-id="2685c-191">Class types</span></span>     | <span data-ttu-id="2685c-192">Исходный базовым классом для всех типов: `object`</span><span class="sxs-lookup"><span data-stu-id="2685c-192">Ultimate base class of all other types: `object`</span></span> |
|                 |                 | <span data-ttu-id="2685c-193">Строки Юникода: `string`</span><span class="sxs-lookup"><span data-stu-id="2685c-193">Unicode strings: `string`</span></span> |
|                 |                 | <span data-ttu-id="2685c-194">Пользовательские типы в формате `class C {...}`</span><span class="sxs-lookup"><span data-stu-id="2685c-194">User-defined types of the form `class C {...}`</span></span> |
|                 | <span data-ttu-id="2685c-195">Типы интерфейса</span><span class="sxs-lookup"><span data-stu-id="2685c-195">Interface types</span></span> | <span data-ttu-id="2685c-196">Пользовательские типы в формате `interface I {...}`</span><span class="sxs-lookup"><span data-stu-id="2685c-196">User-defined types of the form `interface I {...}`</span></span> |
|                 | <span data-ttu-id="2685c-197">Типы массивов</span><span class="sxs-lookup"><span data-stu-id="2685c-197">Array types</span></span>     | <span data-ttu-id="2685c-198">Одно- и многомерные, например, `int[]` и `int[,]`</span><span class="sxs-lookup"><span data-stu-id="2685c-198">Single- and multi-dimensional, for example, `int[]` and `int[,]`</span></span> |
|                 | <span data-ttu-id="2685c-199">Тип делегатов</span><span class="sxs-lookup"><span data-stu-id="2685c-199">Delegate types</span></span>  | <span data-ttu-id="2685c-200">Определяемые пользователем типы формы например `delegate int  D(...)`</span><span class="sxs-lookup"><span data-stu-id="2685c-200">User-defined types of the form e.g. `delegate int  D(...)`</span></span> |

<span data-ttu-id="2685c-201">Восемь целочисленных типов обеспечивают поддержку 8-разрядных, 16-разрядных, 32-разрядных и 64-разрядных значений со знаком или без знака.</span><span class="sxs-lookup"><span data-stu-id="2685c-201">The eight integral types provide support for 8-bit, 16-bit, 32-bit, and 64-bit values in signed or unsigned form.</span></span>

<span data-ttu-id="2685c-202">Два с плавающей запятой укажите типы, `float` и `double`, представлены с помощью 32-разрядный одиночной точности и 64-разрядных двойной точности IEEE 754 форматов.</span><span class="sxs-lookup"><span data-stu-id="2685c-202">The two floating point types, `float` and `double`, are represented using the 32-bit single-precision and 64-bit double-precision IEEE 754 formats.</span></span>

<span data-ttu-id="2685c-203">Тип `decimal` — это 128-разрядный тип данных для финансовых и денежных расчетов.</span><span class="sxs-lookup"><span data-stu-id="2685c-203">The `decimal` type is a 128-bit data type suitable for financial and monetary calculations.</span></span>

<span data-ttu-id="2685c-204">C# `bool` тип используется для представления логических значений, которые могут иметь `true` или `false`.</span><span class="sxs-lookup"><span data-stu-id="2685c-204">C#'s `bool` type is used to represent boolean values—values that are either `true` or `false`.</span></span>

<span data-ttu-id="2685c-205">Обработка знаков и строк в C# выполняется в кодировке Юникода.</span><span class="sxs-lookup"><span data-stu-id="2685c-205">Character and string processing in C# uses Unicode encoding.</span></span> <span data-ttu-id="2685c-206">Тип `char` представляет элемент в кодировке UTF-16, а тип `string` представляет последовательность элементов в кодировке UTF-16.</span><span class="sxs-lookup"><span data-stu-id="2685c-206">The `char` type represents a UTF-16 code unit, and the `string` type represents a sequence of UTF-16 code units.</span></span>

<span data-ttu-id="2685c-207">В следующей таблице перечислены числовых типов C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-207">The following table summarizes C#'s numeric types.</span></span>


| <span data-ttu-id="2685c-208">__Категория__</span><span class="sxs-lookup"><span data-stu-id="2685c-208">__Category__</span></span>      | <span data-ttu-id="2685c-209">__BITS__</span><span class="sxs-lookup"><span data-stu-id="2685c-209">__Bits__</span></span> | <span data-ttu-id="2685c-210">__Type__</span><span class="sxs-lookup"><span data-stu-id="2685c-210">__Type__</span></span>  | <span data-ttu-id="2685c-211">__Диапазон и точность__</span><span class="sxs-lookup"><span data-stu-id="2685c-211">__Range/Precision__</span></span> |
|-------------------|----------|-----------|---------------------|
| <span data-ttu-id="2685c-212">Целочисленный со знаком</span><span class="sxs-lookup"><span data-stu-id="2685c-212">Signed integral</span></span>   | <span data-ttu-id="2685c-213">8</span><span class="sxs-lookup"><span data-stu-id="2685c-213">8</span></span>        | `sbyte`   | <span data-ttu-id="2685c-214">– 128... 127</span><span class="sxs-lookup"><span data-stu-id="2685c-214">-128...127</span></span> |
|                   | <span data-ttu-id="2685c-215">16</span><span class="sxs-lookup"><span data-stu-id="2685c-215">16</span></span>       | `short`   | <span data-ttu-id="2685c-216">-32, 768... 32, 767</span><span class="sxs-lookup"><span data-stu-id="2685c-216">-32,768...32,767</span></span> |
|                   | <span data-ttu-id="2685c-217">32</span><span class="sxs-lookup"><span data-stu-id="2685c-217">32</span></span>       | `int`     | <span data-ttu-id="2685c-218">-2,147,483, 648... 2 147, 483, 647</span><span class="sxs-lookup"><span data-stu-id="2685c-218">-2,147,483,648...2,147,483,647</span></span> |
|                   | <span data-ttu-id="2685c-219">64</span><span class="sxs-lookup"><span data-stu-id="2685c-219">64</span></span>       | `long`    | <span data-ttu-id="2685c-220">-9,223,372,036,854,775, 808... 9 223, 372, 036, 854, 775, 807</span><span class="sxs-lookup"><span data-stu-id="2685c-220">-9,223,372,036,854,775,808...9,223,372,036,854,775,807</span></span> |
| <span data-ttu-id="2685c-221">Целочисленный без знака</span><span class="sxs-lookup"><span data-stu-id="2685c-221">Unsigned integral</span></span> | <span data-ttu-id="2685c-222">8</span><span class="sxs-lookup"><span data-stu-id="2685c-222">8</span></span>        | `byte`    | <span data-ttu-id="2685c-223">0... 255</span><span class="sxs-lookup"><span data-stu-id="2685c-223">0...255</span></span> |
|                   | <span data-ttu-id="2685c-224">16</span><span class="sxs-lookup"><span data-stu-id="2685c-224">16</span></span>       | `ushort`  | <span data-ttu-id="2685c-225">0... 65 535</span><span class="sxs-lookup"><span data-stu-id="2685c-225">0...65,535</span></span> |
|                   | <span data-ttu-id="2685c-226">32</span><span class="sxs-lookup"><span data-stu-id="2685c-226">32</span></span>       | `uint`    | <span data-ttu-id="2685c-227">0... 4 294 967 295</span><span class="sxs-lookup"><span data-stu-id="2685c-227">0...4,294,967,295</span></span> |
|                   | <span data-ttu-id="2685c-228">64</span><span class="sxs-lookup"><span data-stu-id="2685c-228">64</span></span>       | `ulong`   | <span data-ttu-id="2685c-229">0... 18446744073709551615</span><span class="sxs-lookup"><span data-stu-id="2685c-229">0...18,446,744,073,709,551,615</span></span> |
| <span data-ttu-id="2685c-230">С плавающей запятой</span><span class="sxs-lookup"><span data-stu-id="2685c-230">Floating point</span></span>    | <span data-ttu-id="2685c-231">32</span><span class="sxs-lookup"><span data-stu-id="2685c-231">32</span></span>       | `float`   | <span data-ttu-id="2685c-232">1,5 × 10 ^ 45 до 3,4 × 10 ^ 38, 7-значной точностью</span><span class="sxs-lookup"><span data-stu-id="2685c-232">1.5 × 10^−45 to 3.4 × 10^38, 7-digit precision</span></span> |
|                   | <span data-ttu-id="2685c-233">64</span><span class="sxs-lookup"><span data-stu-id="2685c-233">64</span></span>       | `double`  | <span data-ttu-id="2685c-234">5,0 × 10 ^ – 324 до 1,7 × 10 ^ 308, 15 цифр точности</span><span class="sxs-lookup"><span data-stu-id="2685c-234">5.0 × 10^−324 to 1.7 × 10^308, 15-digit precision</span></span> |
| <span data-ttu-id="2685c-235">Десятичное число</span><span class="sxs-lookup"><span data-stu-id="2685c-235">Decimal</span></span>           | <span data-ttu-id="2685c-236">128</span><span class="sxs-lookup"><span data-stu-id="2685c-236">128</span></span>      | `decimal` | <span data-ttu-id="2685c-237">1.0 × 10 ^ −28 до 7,9 × 10 ^ 28, 28 разрядами</span><span class="sxs-lookup"><span data-stu-id="2685c-237">1.0 × 10^−28 to 7.9 × 10^28, 28-digit precision</span></span> |

<span data-ttu-id="2685c-238">Программы C# используют ***объявления типов*** для создания новых типов.</span><span class="sxs-lookup"><span data-stu-id="2685c-238">C# programs use ***type declarations*** to create new types.</span></span> <span data-ttu-id="2685c-239">В объявлении типа указываются имя и члены нового типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-239">A type declaration specifies the name and the members of the new type.</span></span> <span data-ttu-id="2685c-240">Пять из C# категории типов определяются пользователем: класс типы, типы структур, типы интерфейсов, типы перечисления и типы делегатов.</span><span class="sxs-lookup"><span data-stu-id="2685c-240">Five of C#'s categories of types are user-definable: class types, struct types, interface types, enum types, and delegate types.</span></span>

<span data-ttu-id="2685c-241">Тип класса определяет структуру данных, содержащую данные-члены (поля) и функции-члены (методы, свойства и другие).</span><span class="sxs-lookup"><span data-stu-id="2685c-241">A class type defines a data structure that contains data members (fields) and function members (methods, properties, and others).</span></span> <span data-ttu-id="2685c-242">Классы поддерживают механизмы одиночного наследования и полиморфизма, которые позволяют создавать производные классы, расширяющие и уточняющие определения базовых классов.</span><span class="sxs-lookup"><span data-stu-id="2685c-242">Class types support single inheritance and polymorphism, mechanisms whereby derived classes can extend and specialize base classes.</span></span>

<span data-ttu-id="2685c-243">Типом структуры похож на тип класса, в том, что он представляет структуру, используя данные-члены и функции-члены.</span><span class="sxs-lookup"><span data-stu-id="2685c-243">A struct type is similar to a class type in that it represents a structure with data members and function members.</span></span> <span data-ttu-id="2685c-244">Тем не менее в отличие от классов, структуры являются типами значений и не требуется выделение кучи.</span><span class="sxs-lookup"><span data-stu-id="2685c-244">However, unlike classes, structs are value types and do not require heap allocation.</span></span> <span data-ttu-id="2685c-245">Типы структуры не поддерживают определяемое пользователем наследование, и все типы структуры неявно наследуют от типа `object`.</span><span class="sxs-lookup"><span data-stu-id="2685c-245">Struct types do not support user-specified inheritance, and all struct types implicitly inherit from type `object`.</span></span>

<span data-ttu-id="2685c-246">Тип интерфейса определяет контракт в виде именованного набора открытых функций-членов.</span><span class="sxs-lookup"><span data-stu-id="2685c-246">An interface type defines a contract as a named set of public function members.</span></span> <span data-ttu-id="2685c-247">Класс или структура, реализующие интерфейс должен содержать реализации функции-члены этого интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2685c-247">A class or struct that implements an interface must provide implementations of the interface's function members.</span></span> <span data-ttu-id="2685c-248">Интерфейс может наследовать от нескольких базовых интерфейсах и класс или структура может реализовывать несколько интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="2685c-248">An interface may inherit from multiple base interfaces, and a class or struct may implement multiple interfaces.</span></span>

<span data-ttu-id="2685c-249">Тип делегата представляет ссылки на методы с конкретным списком параметров и типом возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="2685c-249">A delegate type represents references to methods with a particular parameter list and return type.</span></span> <span data-ttu-id="2685c-250">Делегаты позволяют использовать методы как сущности, сохраняя их в переменные и передавая в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-250">Delegates make it possible to treat methods as entities that can be assigned to variables and passed as parameters.</span></span> <span data-ttu-id="2685c-251">Принцип работы делегатов близок к указателям функций из некоторых языков, но в отличие от указателей функций делегаты являются объектно-ориентированными и строго типизированными.</span><span class="sxs-lookup"><span data-stu-id="2685c-251">Delegates are similar to the concept of function pointers found in some other languages, but unlike function pointers, delegates are object-oriented and type-safe.</span></span>

<span data-ttu-id="2685c-252">Типы поддерживают универсальные шаблоны, они позволяют передавать с другими типами, класса, структуры, интерфейса и делегата.</span><span class="sxs-lookup"><span data-stu-id="2685c-252">Class, struct, interface and delegate types all support generics, whereby they can be parameterized with other types.</span></span>

<span data-ttu-id="2685c-253">Тип перечисления является отдельным типом со списком именованных констант.</span><span class="sxs-lookup"><span data-stu-id="2685c-253">An enum type is a distinct type with named constants.</span></span> <span data-ttu-id="2685c-254">Каждый тип перечисления имеет базовый тип, который должен быть одним из восьми целочисленных типов.</span><span class="sxs-lookup"><span data-stu-id="2685c-254">Every enum type has an underlying type, which must be one of the eight integral types.</span></span> <span data-ttu-id="2685c-255">Набор значений типа перечисления является таким же, как набор значений базового типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-255">The set of values of an enum type is the same as the set of values of the underlying type.</span></span>

<span data-ttu-id="2685c-256">C# поддерживает одно- и многомерные массивы любого типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-256">C# supports single- and multi-dimensional arrays of any type.</span></span> <span data-ttu-id="2685c-257">В отличие от перечисленных выше типов, типы массивов не требуется объявлять перед использованием.</span><span class="sxs-lookup"><span data-stu-id="2685c-257">Unlike the types listed above, array types do not have to be declared before they can be used.</span></span> <span data-ttu-id="2685c-258">Типы массивов можно сформировать, просто введя квадратные скобки после имени типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-258">Instead, array types are constructed by following a type name with square brackets.</span></span> <span data-ttu-id="2685c-259">Например `int[]` представляет собой одномерный массив `int`, `int[,]` является двумерным массивом значений типа `int`, и `int[][]` представляет собой одномерный массив одномерных массивов `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-259">For example, `int[]` is a single-dimensional array of `int`, `int[,]` is a two-dimensional array of `int`, and `int[][]` is a single-dimensional array of single-dimensional arrays of `int`.</span></span>

<span data-ttu-id="2685c-260">Обнуляемые типы, кроме того, нет необходимости объявить, прежде чем они могут использоваться.</span><span class="sxs-lookup"><span data-stu-id="2685c-260">Nullable types also do not have to be declared before they can be used.</span></span> <span data-ttu-id="2685c-261">Для каждого типа не допускающим значения `T` имеется соответствующий обнуляемый тип `T?`, который может содержать дополнительное значение `null`.</span><span class="sxs-lookup"><span data-stu-id="2685c-261">For each non-nullable value type `T` there is a corresponding nullable type `T?`, which can hold an additional value `null`.</span></span> <span data-ttu-id="2685c-262">Например `int?` — это тип, который может содержать любое 32-разрядное целое число или значение `null`.</span><span class="sxs-lookup"><span data-stu-id="2685c-262">For instance, `int?` is a type that can hold any 32 bit integer or the value `null`.</span></span>

<span data-ttu-id="2685c-263">Система типов C# унифицирована таким образом, что значение любого типа можно рассматривать как объект.</span><span class="sxs-lookup"><span data-stu-id="2685c-263">C#'s type system is unified such that a value of any type can be treated as an object.</span></span> <span data-ttu-id="2685c-264">Каждый тип в C# является прямо или косвенно производным от типа класса `object`, и этот тип `object` является исходным базовым классом для всех типов.</span><span class="sxs-lookup"><span data-stu-id="2685c-264">Every type in C# directly or indirectly derives from the `object` class type, and `object` is the ultimate base class of all types.</span></span> <span data-ttu-id="2685c-265">Чтобы значения ссылочного типа обрабатывались как объекты, им просто присваивается тип `object`.</span><span class="sxs-lookup"><span data-stu-id="2685c-265">Values of reference types are treated as objects simply by viewing the values as type `object`.</span></span> <span data-ttu-id="2685c-266">Значения типов значений, рассматриваются как объекты, выполняя ***упаковки-преобразования*** и ***распаковки*** операций.</span><span class="sxs-lookup"><span data-stu-id="2685c-266">Values of value types are treated as objects by performing ***boxing*** and ***unboxing*** operations.</span></span> <span data-ttu-id="2685c-267">В следующем примере значение `int` преобразуется в `object`, а затем обратно в `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-267">In the following example, an `int` value is converted to `object` and back again to `int`.</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        int i = 123;
        object o = i;          // Boxing
        int j = (int)o;        // Unboxing
    }
}
```
<span data-ttu-id="2685c-268">Если значение типа значения преобразуется в тип `object`, для хранения значения выделяется экземпляр объекта, также называемый «упаковка», и значение копируется в эту упаковку.</span><span class="sxs-lookup"><span data-stu-id="2685c-268">When a value of a value type is converted to type `object`, an object instance, also called a "box," is allocated to hold the value, and the value is copied into that box.</span></span> <span data-ttu-id="2685c-269">И наоборот, если `object` ссылка приводится к типу значения, то выполняется проверка, указанный объект является правильного типа и, если проверка завершится успешно, копируется значение в поле.</span><span class="sxs-lookup"><span data-stu-id="2685c-269">Conversely, when an `object` reference is cast to a value type, a check is made that the referenced object is a box of the correct value type, and, if the check succeeds, the value in the box is copied out.</span></span>

<span data-ttu-id="2685c-270">Системы с единым типом C#, фактически означает, что типы значений могут преобразовываться в объекты «по требованию».</span><span class="sxs-lookup"><span data-stu-id="2685c-270">C#'s unified type system effectively means that value types can become objects "on demand."</span></span> <span data-ttu-id="2685c-271">Такая унификация позволяет применять универсальные библиотеки, использующие тип `object`, как со ссылочными типами, так и с типами значений.</span><span class="sxs-lookup"><span data-stu-id="2685c-271">Because of the unification, general-purpose libraries that use type `object` can be used with both reference types and value types.</span></span>

<span data-ttu-id="2685c-272">В C# существует несколько типов ***переменных***, в том числе поля, элементы массива, локальные переменные и параметры.</span><span class="sxs-lookup"><span data-stu-id="2685c-272">There are several kinds of ***variables*** in C#, including fields, array elements, local variables, and parameters.</span></span> <span data-ttu-id="2685c-273">Переменные представляют места хранения, и каждая переменная имеет тип, который определяет значения, которые могут быть сохранены в переменной, как показано в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="2685c-273">Variables represent storage locations, and every variable has a type that determines what values can be stored in the variable, as shown by the following table.</span></span>


| <span data-ttu-id="2685c-274">__Тип переменной__</span><span class="sxs-lookup"><span data-stu-id="2685c-274">__Type of Variable__</span></span>    | <span data-ttu-id="2685c-275">__Возможное содержимое__</span><span class="sxs-lookup"><span data-stu-id="2685c-275">__Possible Contents__</span></span> |
|-------------------------|-----------------------|
| <span data-ttu-id="2685c-276">Тип значения, не допускающий значения Null</span><span class="sxs-lookup"><span data-stu-id="2685c-276">Non-nullable value type</span></span> | <span data-ttu-id="2685c-277">Значение такого типа</span><span class="sxs-lookup"><span data-stu-id="2685c-277">A value of that exact type</span></span> |
| <span data-ttu-id="2685c-278">Тип значения, допускающий значение Null</span><span class="sxs-lookup"><span data-stu-id="2685c-278">Nullable value type</span></span>     | <span data-ttu-id="2685c-279">Значение null или значение такого типа</span><span class="sxs-lookup"><span data-stu-id="2685c-279">A null value or a value of that exact type</span></span> |
| `object`                | <span data-ttu-id="2685c-280">Пустая ссылка, ссылку на объект любого ссылочного типа или ссылка на упакованное значение любого типа значения</span><span class="sxs-lookup"><span data-stu-id="2685c-280">A null reference, a reference to an object of any reference type, or a reference to a boxed value of any value type</span></span> |
| <span data-ttu-id="2685c-281">Тип класса</span><span class="sxs-lookup"><span data-stu-id="2685c-281">Class type</span></span>              | <span data-ttu-id="2685c-282">Пустая ссылка, ссылку на экземпляр этого типа класса или ссылку на экземпляр класса, производным от типа класса</span><span class="sxs-lookup"><span data-stu-id="2685c-282">A null reference, a reference to an instance of that class type, or a reference to an instance of a class derived from that class type</span></span> |
| <span data-ttu-id="2685c-283">Тип интерфейса</span><span class="sxs-lookup"><span data-stu-id="2685c-283">Interface type</span></span>          | <span data-ttu-id="2685c-284">Пустая ссылка, ссылку на экземпляр типа класса, который реализует такой тип интерфейса или ссылка на упакованное значение типа значения, который реализует такой тип интерфейса</span><span class="sxs-lookup"><span data-stu-id="2685c-284">A null reference, a reference to an instance of a class type that implements that interface type, or a reference to a boxed value of a value type that implements that interface type</span></span> |
| <span data-ttu-id="2685c-285">Тип массива</span><span class="sxs-lookup"><span data-stu-id="2685c-285">Array type</span></span>              | <span data-ttu-id="2685c-286">Пустая ссылка, ссылку на экземпляр такого типа массива или ссылку на экземпляр совместимого типа массива</span><span class="sxs-lookup"><span data-stu-id="2685c-286">A null reference, a reference to an instance of that array type, or a reference to an instance of a compatible array type</span></span> |
| <span data-ttu-id="2685c-287">Тип делегата</span><span class="sxs-lookup"><span data-stu-id="2685c-287">Delegate type</span></span>           | <span data-ttu-id="2685c-288">Пустая ссылка или ссылка на экземпляр этого типа делегата</span><span class="sxs-lookup"><span data-stu-id="2685c-288">A null reference or a reference to an instance of that delegate type</span></span> |

## <a name="expressions"></a><span data-ttu-id="2685c-289">Выражения</span><span class="sxs-lookup"><span data-stu-id="2685c-289">Expressions</span></span>

<span data-ttu-id="2685c-290">***Выражения*** создаются из ***операндов*** и ***операторов***.</span><span class="sxs-lookup"><span data-stu-id="2685c-290">***Expressions*** are constructed from ***operands*** and ***operators***.</span></span> <span data-ttu-id="2685c-291">Операторы в выражении указывают, какие действия нужно применить к операндам.</span><span class="sxs-lookup"><span data-stu-id="2685c-291">The operators of an expression indicate which operations to apply to the operands.</span></span> <span data-ttu-id="2685c-292">Примеры операторов: `+`, `-`, `*`, `/` и `new`.</span><span class="sxs-lookup"><span data-stu-id="2685c-292">Examples of operators include `+`, `-`, `*`, `/`, and `new`.</span></span> <span data-ttu-id="2685c-293">Операндами могут являться литералы, поля, локальные переменные, выражения и т. п.</span><span class="sxs-lookup"><span data-stu-id="2685c-293">Examples of operands include literals, fields, local variables, and expressions.</span></span>

<span data-ttu-id="2685c-294">Если выражение содержит несколько операторов, порядок вычисления этих операторов определяется их ***приоритетом***.</span><span class="sxs-lookup"><span data-stu-id="2685c-294">When an expression contains multiple operators, the ***precedence*** of the operators controls the order in which the individual operators are evaluated.</span></span> <span data-ttu-id="2685c-295">Например, выражение `x + y * z` вычисляется как `x + (y * z)`, поскольку оператор `*` имеет более высокий приоритет, чем оператор `+`.</span><span class="sxs-lookup"><span data-stu-id="2685c-295">For example, the expression `x + y * z` is evaluated as `x + (y * z)` because the `*` operator has higher precedence than the `+` operator.</span></span>

<span data-ttu-id="2685c-296">Большинство операторов допускают ***перегрузку***.</span><span class="sxs-lookup"><span data-stu-id="2685c-296">Most operators can be ***overloaded***.</span></span> <span data-ttu-id="2685c-297">Перегрузка операторов позволяет создать пользовательскую реализацию оператора для таких операций, в которых один или оба операнда имеют определяемый пользователем тип класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="2685c-297">Operator overloading permits user-defined operator implementations to be specified for operations where one or both of the operands are of a user-defined class or struct type.</span></span>

<span data-ttu-id="2685c-298">В следующей таблице перечислены операторы C#, категории операторов в порядке от самого высокого до самого низкого.</span><span class="sxs-lookup"><span data-stu-id="2685c-298">The following table summarizes C#'s operators, listing the operator categories in order of precedence from highest to lowest.</span></span> <span data-ttu-id="2685c-299">Операторы в одной категории имеют одинаковый приоритет.</span><span class="sxs-lookup"><span data-stu-id="2685c-299">Operators in the same category have equal precedence.</span></span>


| <span data-ttu-id="2685c-300">__Категория__</span><span class="sxs-lookup"><span data-stu-id="2685c-300">__Category__</span></span>                     | <span data-ttu-id="2685c-301">__Выражение__</span><span class="sxs-lookup"><span data-stu-id="2685c-301">__Expression__</span></span>    | <span data-ttu-id="2685c-302">__Описание__</span><span class="sxs-lookup"><span data-stu-id="2685c-302">__Description__</span></span> |
|----------------------------------|-------------------|-----------------|
| <span data-ttu-id="2685c-303">Первичный</span><span class="sxs-lookup"><span data-stu-id="2685c-303">Primary</span></span>                          | `x.m`             | <span data-ttu-id="2685c-304">Доступ к членам</span><span class="sxs-lookup"><span data-stu-id="2685c-304">Member access</span></span> |
|                                  | `x(...)`          | <span data-ttu-id="2685c-305">Вызов метода и делегата</span><span class="sxs-lookup"><span data-stu-id="2685c-305">Method and delegate invocation</span></span> |
|                                  | `x[...]`          | <span data-ttu-id="2685c-306">Доступ к массиву и индексатору</span><span class="sxs-lookup"><span data-stu-id="2685c-306">Array and indexer access</span></span> |
|                                  | `x++`             | <span data-ttu-id="2685c-307">Постфиксный инкремент</span><span class="sxs-lookup"><span data-stu-id="2685c-307">Post-increment</span></span> |
|                                  | `x--`             | <span data-ttu-id="2685c-308">Постфиксный декремент</span><span class="sxs-lookup"><span data-stu-id="2685c-308">Post-decrement</span></span> |
|                                  | `new T(...)`      | <span data-ttu-id="2685c-309">Создание объекта и делегата</span><span class="sxs-lookup"><span data-stu-id="2685c-309">Object and delegate creation</span></span> |
|                                  | `new T(...){...}` | <span data-ttu-id="2685c-310">Создание объекта с инициализатором</span><span class="sxs-lookup"><span data-stu-id="2685c-310">Object creation with initializer</span></span> |
|                                  | `new {...}`       | <span data-ttu-id="2685c-311">Анонимный инициализатор объекта</span><span class="sxs-lookup"><span data-stu-id="2685c-311">Anonymous object initializer</span></span> |
|                                  | `new T[...]`      | <span data-ttu-id="2685c-312">Создание массива</span><span class="sxs-lookup"><span data-stu-id="2685c-312">Array creation</span></span> |
|                                  | `typeof(T)`       | <span data-ttu-id="2685c-313">Получить `System.Type` для объекта `T`</span><span class="sxs-lookup"><span data-stu-id="2685c-313">Obtain `System.Type` object for `T`</span></span> |
|                                  | `checked(x)`      | <span data-ttu-id="2685c-314">Вычисление выражения в проверенном контексте</span><span class="sxs-lookup"><span data-stu-id="2685c-314">Evaluate expression in checked context</span></span> |
|                                  | `unchecked(x)`    | <span data-ttu-id="2685c-315">Вычисление выражения в непроверенном контексте</span><span class="sxs-lookup"><span data-stu-id="2685c-315">Evaluate expression in unchecked context</span></span> |
|                                  | `default(T)`      | <span data-ttu-id="2685c-316">Получение значения по умолчанию для типа `T`</span><span class="sxs-lookup"><span data-stu-id="2685c-316">Obtain default value of type `T`</span></span> |
|                                  | `delegate {...}`  | <span data-ttu-id="2685c-317">Анонимная функция (анонимный метод)</span><span class="sxs-lookup"><span data-stu-id="2685c-317">Anonymous function (anonymous method)</span></span> |
| <span data-ttu-id="2685c-318">Унарный</span><span class="sxs-lookup"><span data-stu-id="2685c-318">Unary</span></span>                            | `+x`              | <span data-ttu-id="2685c-319">идентификации</span><span class="sxs-lookup"><span data-stu-id="2685c-319">Identity</span></span> |
|                                  | `-x`              | <span data-ttu-id="2685c-320">Отрицание</span><span class="sxs-lookup"><span data-stu-id="2685c-320">Negation</span></span> |
|                                  | `!x`              | <span data-ttu-id="2685c-321">Логическое отрицание</span><span class="sxs-lookup"><span data-stu-id="2685c-321">Logical negation</span></span> |
|                                  | `~x`              | <span data-ttu-id="2685c-322">Поразрядное отрицание</span><span class="sxs-lookup"><span data-stu-id="2685c-322">Bitwise negation</span></span> |
|                                  | `++x`             | <span data-ttu-id="2685c-323">Префиксный инкремент</span><span class="sxs-lookup"><span data-stu-id="2685c-323">Pre-increment</span></span> |
|                                  | `--x`             | <span data-ttu-id="2685c-324">Префиксный декремент</span><span class="sxs-lookup"><span data-stu-id="2685c-324">Pre-decrement</span></span> |
|                                  | `(T)x`            | <span data-ttu-id="2685c-325">Явным образом преобразовать `x` ввода `T`</span><span class="sxs-lookup"><span data-stu-id="2685c-325">Explicitly convert `x` to type `T`</span></span> |
|                                  | `await x`         | <span data-ttu-id="2685c-326">Асинхронное Ожидание `x` для завершения</span><span class="sxs-lookup"><span data-stu-id="2685c-326">Asynchronously wait for `x` to complete</span></span> |
| <span data-ttu-id="2685c-327">Мультипликативный</span><span class="sxs-lookup"><span data-stu-id="2685c-327">Multiplicative</span></span>                   | `x * y`           | <span data-ttu-id="2685c-328">Умножение</span><span class="sxs-lookup"><span data-stu-id="2685c-328">Multiplication</span></span> |
|                                  | `x / y`           | <span data-ttu-id="2685c-329">Деление</span><span class="sxs-lookup"><span data-stu-id="2685c-329">Division</span></span> |
|                                  | `x % y`           | <span data-ttu-id="2685c-330">Остаток</span><span class="sxs-lookup"><span data-stu-id="2685c-330">Remainder</span></span> |
| <span data-ttu-id="2685c-331">Аддитивный</span><span class="sxs-lookup"><span data-stu-id="2685c-331">Additive</span></span>                         | `x + y`           | <span data-ttu-id="2685c-332">Сложение, объединение строк, объединение делегатов</span><span class="sxs-lookup"><span data-stu-id="2685c-332">Addition, string concatenation, delegate combination</span></span> |
|                                  | `x - y`           | <span data-ttu-id="2685c-333">Вычитание, удаление делегатов</span><span class="sxs-lookup"><span data-stu-id="2685c-333">Subtraction, delegate removal</span></span> |
| <span data-ttu-id="2685c-334">Сдвиг</span><span class="sxs-lookup"><span data-stu-id="2685c-334">Shift</span></span>                            | `x << y`          | <span data-ttu-id="2685c-335">Сдвиг влево</span><span class="sxs-lookup"><span data-stu-id="2685c-335">Shift left</span></span> |
|                                  | `x >> y`          | <span data-ttu-id="2685c-336">Сдвиг вправо</span><span class="sxs-lookup"><span data-stu-id="2685c-336">Shift right</span></span> |
| <span data-ttu-id="2685c-337">Тестирования типа и относительные</span><span class="sxs-lookup"><span data-stu-id="2685c-337">Relational and type testing</span></span>      | `x < y`           | <span data-ttu-id="2685c-338">Меньше</span><span class="sxs-lookup"><span data-stu-id="2685c-338">Less than</span></span> |
|                                  | `x > y`           | <span data-ttu-id="2685c-339">Больше</span><span class="sxs-lookup"><span data-stu-id="2685c-339">Greater than</span></span> |
|                                  | `x <= y`          | <span data-ttu-id="2685c-340">Меньше или равно</span><span class="sxs-lookup"><span data-stu-id="2685c-340">Less than or equal</span></span> |
|                                  | `x >= y`          | <span data-ttu-id="2685c-341">Больше или равно</span><span class="sxs-lookup"><span data-stu-id="2685c-341">Greater than or equal</span></span> |
|                                  | `x is T`          | <span data-ttu-id="2685c-342">Вернуть `true` Если `x` — `T`, `false` в противном случае</span><span class="sxs-lookup"><span data-stu-id="2685c-342">Return `true` if `x` is a `T`, `false` otherwise</span></span> |
|                                  | `x as T`          | <span data-ttu-id="2685c-343">Вернуть `x` типизируется как `T`, или `null` Если `x` не `T`</span><span class="sxs-lookup"><span data-stu-id="2685c-343">Return `x` typed as `T`, or `null` if `x` is not a `T`</span></span> |
| <span data-ttu-id="2685c-344">Равенство</span><span class="sxs-lookup"><span data-stu-id="2685c-344">Equality</span></span>                         | `x == y`          | <span data-ttu-id="2685c-345">Равно</span><span class="sxs-lookup"><span data-stu-id="2685c-345">Equal</span></span>      |
|                                  | `x != y`          | <span data-ttu-id="2685c-346">Не равно</span><span class="sxs-lookup"><span data-stu-id="2685c-346">Not equal</span></span> |
| <span data-ttu-id="2685c-347">Логическое И</span><span class="sxs-lookup"><span data-stu-id="2685c-347">Logical AND</span></span>                      | `x & y`           | <span data-ttu-id="2685c-348">Целочисленного побитовое и, логическое и</span><span class="sxs-lookup"><span data-stu-id="2685c-348">Integer bitwise AND, boolean logical AND</span></span> |
| <span data-ttu-id="2685c-349">Логическое исключающее ИЛИ</span><span class="sxs-lookup"><span data-stu-id="2685c-349">Logical XOR</span></span>                      | `x ^ y`           | <span data-ttu-id="2685c-350">Поразрядное исключающее ИЛИ для операндов целочисленного типа, логическое исключающее ИЛИ для операндов логического типа</span><span class="sxs-lookup"><span data-stu-id="2685c-350">Integer bitwise XOR, boolean logical XOR</span></span> |
| <span data-ttu-id="2685c-351">Логическое ИЛИ</span><span class="sxs-lookup"><span data-stu-id="2685c-351">Logical OR</span></span>                       | <code>x &#124; y</code> | <span data-ttu-id="2685c-352">Поразрядное ИЛИ для операндов целочисленного типа, логическое ИЛИ для операндов логического типа</span><span class="sxs-lookup"><span data-stu-id="2685c-352">Integer bitwise OR, boolean logical OR</span></span> |
| <span data-ttu-id="2685c-353">Условное И</span><span class="sxs-lookup"><span data-stu-id="2685c-353">Conditional AND</span></span>                  | `x && y`          | <span data-ttu-id="2685c-354">Результатом является `y` только если `x` — `true`</span><span class="sxs-lookup"><span data-stu-id="2685c-354">Evaluates `y` only if `x` is `true`</span></span> |
| <span data-ttu-id="2685c-355">Условное ИЛИ</span><span class="sxs-lookup"><span data-stu-id="2685c-355">Conditional OR</span></span>                   | <code>x &#124;&#124; y</code> | <span data-ttu-id="2685c-356">Результатом является `y` только если `x` — `false`</span><span class="sxs-lookup"><span data-stu-id="2685c-356">Evaluates `y` only if `x` is `false`</span></span> |
| <span data-ttu-id="2685c-357">Объединение со значением NULL</span><span class="sxs-lookup"><span data-stu-id="2685c-357">Null coalescing</span></span>                  | `X ?? y`          | <span data-ttu-id="2685c-358">Принимает значение `y` Если `x` — `null`, `x` в противном случае</span><span class="sxs-lookup"><span data-stu-id="2685c-358">Evaluates to `y` if `x` is `null`, to `x` otherwise</span></span> |
| <span data-ttu-id="2685c-359">Условие</span><span class="sxs-lookup"><span data-stu-id="2685c-359">Conditional</span></span>                      | `x ? y : z`       | <span data-ttu-id="2685c-360">Результатом является `y` Если `x` — `true`, `z` Если `x` — `false`</span><span class="sxs-lookup"><span data-stu-id="2685c-360">Evaluates `y` if `x` is `true`, `z` if `x` is `false`</span></span> |
| <span data-ttu-id="2685c-361">Присваивание или анонимная функция</span><span class="sxs-lookup"><span data-stu-id="2685c-361">Assignment or anonymous function</span></span> | `x = y`           | <span data-ttu-id="2685c-362">Назначение</span><span class="sxs-lookup"><span data-stu-id="2685c-362">Assignment</span></span> |
|                                  | `x op= y`         | <span data-ttu-id="2685c-363">Составное присваивание; Ниже перечислены поддерживаемые операторы `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `&=` `^=` <code>&#124;=</code></span><span class="sxs-lookup"><span data-stu-id="2685c-363">Compound assignment; supported operators are `*=` `/=` `%=` `+=` `-=` `<<=` `>>=` `&=` `^=` <code>&#124;=</code></span></span> |
|                                  | `(T x) => y`      | <span data-ttu-id="2685c-364">Анонимная функция (лямбда-выражение)</span><span class="sxs-lookup"><span data-stu-id="2685c-364">Anonymous function (lambda expression)</span></span> |

## <a name="statements"></a><span data-ttu-id="2685c-365">Операторы</span><span class="sxs-lookup"><span data-stu-id="2685c-365">Statements</span></span>

<span data-ttu-id="2685c-366">Действия программы выражаются с помощью ***операторов***.</span><span class="sxs-lookup"><span data-stu-id="2685c-366">The actions of a program are expressed using ***statements***.</span></span> <span data-ttu-id="2685c-367">C# поддерживает несколько типов операторов, некоторые из которых определяются как внедренные операторы.</span><span class="sxs-lookup"><span data-stu-id="2685c-367">C# supports several different kinds of statements, a number of which are defined in terms of embedded statements.</span></span>

<span data-ttu-id="2685c-368">С помощью ***блоков*** можно использовать несколько операторов в таких контекстах, где ожидается только один оператор.</span><span class="sxs-lookup"><span data-stu-id="2685c-368">A ***block*** permits multiple statements to be written in contexts where a single statement is allowed.</span></span> <span data-ttu-id="2685c-369">Блок состоит из списка инструкций, заключенных между разделителями `{` и `}`.</span><span class="sxs-lookup"><span data-stu-id="2685c-369">A block consists of a list of statements written between the delimiters `{` and `}`.</span></span>

<span data-ttu-id="2685c-370">***Операторы объявления*** используются для объявления локальных переменных и констант.</span><span class="sxs-lookup"><span data-stu-id="2685c-370">***Declaration statements*** are used to declare local variables and constants.</span></span>

<span data-ttu-id="2685c-371">***Операторы выражений*** позволяют вычислять выражения.</span><span class="sxs-lookup"><span data-stu-id="2685c-371">***Expression statements*** are used to evaluate expressions.</span></span> <span data-ttu-id="2685c-372">Выражения, которые могут использоваться как операторы включают в себя вызовов методов, выделение объектов с помощью `new` оператор, при сбое с помощью `=` и составные операторы присваивания, операции увеличения и уменьшения, с помощью `++`и `--` операторы и выражения await.</span><span class="sxs-lookup"><span data-stu-id="2685c-372">Expressions that can be used as statements include method invocations, object allocations using the `new` operator, assignments using `=` and the compound assignment operators, increment and decrement operations using the `++` and `--` operators and await expressions.</span></span>

<span data-ttu-id="2685c-373">***Операторы выбора*** используются для выбора одного оператора из нескольких возможных вариантов в зависимости от значения какого-либо выражения.</span><span class="sxs-lookup"><span data-stu-id="2685c-373">***Selection statements*** are used to select one of a number of possible statements for execution based on the value of some expression.</span></span> <span data-ttu-id="2685c-374">К этой группе относятся операторы `if` и `switch`.</span><span class="sxs-lookup"><span data-stu-id="2685c-374">In this group are the `if` and `switch` statements.</span></span>

<span data-ttu-id="2685c-375">***Операторы итерации*** используются для многократного выполнения внедренного оператора.</span><span class="sxs-lookup"><span data-stu-id="2685c-375">***Iteration statements*** are used to repeatedly execute an embedded statement.</span></span> <span data-ttu-id="2685c-376">К этой группе относятся операторы `while`, `do`, `for` и `foreach`.</span><span class="sxs-lookup"><span data-stu-id="2685c-376">In this group are the `while`, `do`, `for`, and `foreach` statements.</span></span>

<span data-ttu-id="2685c-377">***Операторы перехода*** используются для передачи управления.</span><span class="sxs-lookup"><span data-stu-id="2685c-377">***Jump statements*** are used to transfer control.</span></span> <span data-ttu-id="2685c-378">К этой группе относятся операторы `break`, `continue`, `goto`, `throw`, `return` и `yield`.</span><span class="sxs-lookup"><span data-stu-id="2685c-378">In this group are the `break`, `continue`, `goto`, `throw`, `return`, and `yield` statements.</span></span>

<span data-ttu-id="2685c-379">Операторы `try`...`catch` позволяют перехватывать исключения, создаваемые при выполнении блока кода, а оператор `try`...`finally` используется для указания кода завершения, который выполняется всегда, независимо от появления исключений.</span><span class="sxs-lookup"><span data-stu-id="2685c-379">The `try`...`catch` statement is used to catch exceptions that occur during execution of a block, and the `try`...`finally` statement is used to specify finalization code that is always executed, whether an exception occurred or not.</span></span>

<span data-ttu-id="2685c-380">`checked` И `unchecked` инструкции используются для управления контекстом для целочисленных арифметических операций и преобразований проверки переполнения.</span><span class="sxs-lookup"><span data-stu-id="2685c-380">The `checked` and `unchecked` statements are used to control the overflow checking context for integral-type arithmetic operations and conversions.</span></span>

<span data-ttu-id="2685c-381">Оператор `lock` позволяет создать взаимоисключающую блокировку заданного объекта перед выполнением определенных операторов, а затем снять блокировку.</span><span class="sxs-lookup"><span data-stu-id="2685c-381">The `lock` statement is used to obtain the mutual-exclusion lock for a given object, execute a statement, and then release the lock.</span></span>

<span data-ttu-id="2685c-382">Оператор `using` используется для получения ресурса перед определенным оператором, и для удаления ресурса после его завершения.</span><span class="sxs-lookup"><span data-stu-id="2685c-382">The `using` statement is used to obtain a resource, execute a statement, and then dispose of that resource.</span></span>

<span data-ttu-id="2685c-383">Ниже приведены примеры каждого типа инструкции</span><span class="sxs-lookup"><span data-stu-id="2685c-383">Below are examples of each kind of statement</span></span>

<span data-ttu-id="2685c-384">__Объявления локальных переменных__</span><span class="sxs-lookup"><span data-stu-id="2685c-384">__Local variable declarations__</span></span>

```csharp
static void Main() {
   int a;
   int b = 2, c = 3;
   a = 1;
   Console.WriteLine(a + b + c);
}
```


<span data-ttu-id="2685c-385">__В объявлении локальной константы__</span><span class="sxs-lookup"><span data-stu-id="2685c-385">__Local constant declaration__</span></span>

```csharp
static void Main() {
    const float pi = 3.1415927f;
    const int r = 25;
    Console.WriteLine(pi * r * r);
}
```


<span data-ttu-id="2685c-386">__Оператор выражений__</span><span class="sxs-lookup"><span data-stu-id="2685c-386">__Expression statement__</span></span>

```csharp
static void Main() {
    int i;
    i = 123;                // Expression statement
    Console.WriteLine(i);   // Expression statement
    i++;                    // Expression statement
    Console.WriteLine(i);   // Expression statement
}
```

<span data-ttu-id="2685c-387">__`if` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-387">__`if` statement__</span></span>

```csharp
static void Main(string[] args) {
    if (args.Length == 0) {
        Console.WriteLine("No arguments");
    }
    else {
        Console.WriteLine("One or more arguments");
    }
}
```


<span data-ttu-id="2685c-388">__`switch` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-388">__`switch` statement__</span></span>

```csharp
static void Main(string[] args) {
    int n = args.Length;
    switch (n) {
        case 0:
            Console.WriteLine("No arguments");
            break;
        case 1:
            Console.WriteLine("One argument");
            break;
        default:
            Console.WriteLine("{0} arguments", n);
            break;
    }
}
```

<span data-ttu-id="2685c-389">__`while` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-389">__`while` statement__</span></span>

```csharp
static void Main(string[] args) {
    int i = 0;
    while (i < args.Length) {
        Console.WriteLine(args[i]);
        i++;
    }
}
```


<span data-ttu-id="2685c-390">__`do` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-390">__`do` statement__</span></span>

```csharp
static void Main() {
    string s;
    do {
        s = Console.ReadLine();
        if (s != null) Console.WriteLine(s);
    } while (s != null);
}
```

<span data-ttu-id="2685c-391">__`for` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-391">__`for` statement__</span></span>

```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        Console.WriteLine(args[i]);
    }
}
```

<span data-ttu-id="2685c-392">__`foreach` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-392">__`foreach` statement__</span></span>

```csharp
static void Main(string[] args) {
    foreach (string s in args) {
        Console.WriteLine(s);
    }
}
```

<span data-ttu-id="2685c-393">__`break` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-393">__`break` statement__</span></span>

```csharp
static void Main() {
    while (true) {
        string s = Console.ReadLine();
        if (s == null) break;
        Console.WriteLine(s);
    }
}
```

<span data-ttu-id="2685c-394">__`continue` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-394">__`continue` statement__</span></span>

```csharp
static void Main(string[] args) {
    for (int i = 0; i < args.Length; i++) {
        if (args[i].StartsWith("/")) continue;
        Console.WriteLine(args[i]);
    }
}
```

<span data-ttu-id="2685c-395">__`goto` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-395">__`goto` statement__</span></span>

```csharp
static void Main(string[] args) {
    int i = 0;
    goto check;
    loop:
    Console.WriteLine(args[i++]);
    check:
    if (i < args.Length) goto loop;
}
```

<span data-ttu-id="2685c-396">__`return` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-396">__`return` statement__</span></span>

```csharp
static int Add(int a, int b) {
    return a + b;
}

static void Main() {
    Console.WriteLine(Add(1, 2));
    return;
}
```

<span data-ttu-id="2685c-397">__`yield` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-397">__`yield` statement__</span></span>

```csharp
static IEnumerable<int> Range(int from, int to) {
    for (int i = from; i < to; i++) {
        yield return i;
    }
    yield break;
}

static void Main() {
    foreach (int x in Range(-10,10)) {
        Console.WriteLine(x);
    }
}
```

<span data-ttu-id="2685c-398">__`throw` и `try` инструкций__</span><span class="sxs-lookup"><span data-stu-id="2685c-398">__`throw` and `try` statements__</span></span>

```csharp
static double Divide(double x, double y) {
    if (y == 0) throw new DivideByZeroException();
    return x / y;
}

static void Main(string[] args) {
    try {
        if (args.Length != 2) {
            throw new Exception("Two numbers required");
        }
        double x = double.Parse(args[0]);
        double y = double.Parse(args[1]);
        Console.WriteLine(Divide(x, y));
    }
    catch (Exception e) {
        Console.WriteLine(e.Message);
    }
    finally {
        Console.WriteLine("Good bye!");
    }
}
```

<span data-ttu-id="2685c-399">__`checked` и `unchecked` инструкций__</span><span class="sxs-lookup"><span data-stu-id="2685c-399">__`checked` and `unchecked` statements__</span></span>

```csharp
static void Main() {
    int i = int.MaxValue;
    checked {
        Console.WriteLine(i + 1);        // Exception
    }
    unchecked {
        Console.WriteLine(i + 1);        // Overflow
    }
}
```

<span data-ttu-id="2685c-400">__`lock` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-400">__`lock` statement__</span></span>

```csharp
class Account
{
    decimal balance;
    public void Withdraw(decimal amount) {
        lock (this) {
            if (amount > balance) {
                throw new Exception("Insufficient funds");
            }
            balance -= amount;
        }
    }
}
```

<span data-ttu-id="2685c-401">__`using` Инструкции__</span><span class="sxs-lookup"><span data-stu-id="2685c-401">__`using` statement__</span></span>

```csharp
static void Main() {
    using (TextWriter w = File.CreateText("test.txt")) {
        w.WriteLine("Line one");
        w.WriteLine("Line two");
        w.WriteLine("Line three");
    }
}
```

## <a name="classes-and-objects"></a><span data-ttu-id="2685c-402">Классы и объекты</span><span class="sxs-lookup"><span data-stu-id="2685c-402">Classes and objects</span></span>

<span data-ttu-id="2685c-403">***Классы*** являются самым важным типом в языке C#.</span><span class="sxs-lookup"><span data-stu-id="2685c-403">***Classes*** are the most fundamental of C#'s types.</span></span> <span data-ttu-id="2685c-404">Класс представляет собой структуру данных, которая объединяет в себе значения (поля) и действия (методы и другие функции-члены).</span><span class="sxs-lookup"><span data-stu-id="2685c-404">A class is a data structure that combines state (fields) and actions (methods and other function members) in a single unit.</span></span> <span data-ttu-id="2685c-405">Класс предоставляет определение для динамически создаваемых ***экземпляров*** класса, которые также именуются ***объектами***.</span><span class="sxs-lookup"><span data-stu-id="2685c-405">A class provides a definition for dynamically created ***instances*** of the class, also known as ***objects***.</span></span> <span data-ttu-id="2685c-406">Классы поддерживают механизмы ***наследования*** и ***полиморфизма***, которые позволяют создавать ***производные классы***, расширяющие и уточняющие определения ***базовых классов***.</span><span class="sxs-lookup"><span data-stu-id="2685c-406">Classes support ***inheritance*** and ***polymorphism***, mechanisms whereby ***derived classes*** can extend and specialize ***base classes***.</span></span>

<span data-ttu-id="2685c-407">Новые классы создаются с помощью объявлений классов.</span><span class="sxs-lookup"><span data-stu-id="2685c-407">New classes are created using class declarations.</span></span> <span data-ttu-id="2685c-408">Объявление класса начинается с заголовка, в котором указаны атрибуты и модификаторы класса, имя класса, базовый класс (если есть) и интерфейсы, реализуемые этим классом.</span><span class="sxs-lookup"><span data-stu-id="2685c-408">A class declaration starts with a header that specifies the attributes and modifiers of the class, the name of the class, the base class (if given), and the interfaces implemented by the class.</span></span> <span data-ttu-id="2685c-409">За заголовком между разделителями `{` и `}` следует тело класса, в котором последовательно объявляются все члены класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-409">The header is followed by the class body, which consists of a list of member declarations written between the delimiters `{` and `}`.</span></span>

<span data-ttu-id="2685c-410">Вот простой пример объявления класса с именем `Point`:</span><span class="sxs-lookup"><span data-stu-id="2685c-410">The following is a declaration of a simple class named `Point`:</span></span>

```csharp
public class Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
<span data-ttu-id="2685c-411">Экземпляры классов создаются с помощью оператора `new`, который выделяет память для нового экземпляра, вызывает конструктор для инициализации этого экземпляра и возвращает ссылку на экземпляр.</span><span class="sxs-lookup"><span data-stu-id="2685c-411">Instances of classes are created using the `new` operator, which allocates memory for a new instance, invokes a constructor to initialize the instance, and returns a reference to the instance.</span></span> <span data-ttu-id="2685c-412">Следующие инструкции создают два `Point` объектов и сохранения ссылок на эти объекты в двух переменных:</span><span class="sxs-lookup"><span data-stu-id="2685c-412">The following statements create two `Point` objects and store references to those objects in two variables:</span></span>

```
Point p1 = new Point(0, 0);
Point p2 = new Point(10, 20);
```
<span data-ttu-id="2685c-413">Занимаемая объектом память автоматически освобождается, когда объект больше не используется.</span><span class="sxs-lookup"><span data-stu-id="2685c-413">The memory occupied by an object is automatically reclaimed when the object is no longer in use.</span></span> <span data-ttu-id="2685c-414">В C# нет ни необходимости, ни возможности освобождать память объектов явным образом.</span><span class="sxs-lookup"><span data-stu-id="2685c-414">It is neither necessary nor possible to explicitly deallocate objects in C#.</span></span>

### <a name="members"></a><span data-ttu-id="2685c-415">Участники</span><span class="sxs-lookup"><span data-stu-id="2685c-415">Members</span></span>

<span data-ttu-id="2685c-416">Члены класса являются либо ***статические члены*** или ***члены экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="2685c-416">The members of a class are either ***static members*** or ***instance members***.</span></span> <span data-ttu-id="2685c-417">Статические члены принадлежат классу в целом, а члены экземпляра принадлежат конкретным объектам (экземплярам классов).</span><span class="sxs-lookup"><span data-stu-id="2685c-417">Static members belong to classes, and instance members belong to objects (instances of classes).</span></span>

<span data-ttu-id="2685c-418">Ниже приведены общие сведения о виды членов, которые могут содержаться в классе.</span><span class="sxs-lookup"><span data-stu-id="2685c-418">The following table provides an overview of the kinds of members a class can contain.</span></span>


| <span data-ttu-id="2685c-419">__Член__</span><span class="sxs-lookup"><span data-stu-id="2685c-419">__Member__</span></span>   | <span data-ttu-id="2685c-420">__Описание__</span><span class="sxs-lookup"><span data-stu-id="2685c-420">__Description__</span></span> |
|------------  |-----------------|
| <span data-ttu-id="2685c-421">Константы</span><span class="sxs-lookup"><span data-stu-id="2685c-421">Constants</span></span>    | <span data-ttu-id="2685c-422">Константные значения, связанные с классом.</span><span class="sxs-lookup"><span data-stu-id="2685c-422">Constant values associated with the class</span></span> |
| <span data-ttu-id="2685c-423">Поля</span><span class="sxs-lookup"><span data-stu-id="2685c-423">Fields</span></span>       | <span data-ttu-id="2685c-424">Переменные класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-424">Variables of the class</span></span> |
| <span data-ttu-id="2685c-425">Методы</span><span class="sxs-lookup"><span data-stu-id="2685c-425">Methods</span></span>      | <span data-ttu-id="2685c-426">Вычисления и действия, которые может выполнять класс.</span><span class="sxs-lookup"><span data-stu-id="2685c-426">Computations and actions that can be performed by the class</span></span> |
| <span data-ttu-id="2685c-427">Свойства</span><span class="sxs-lookup"><span data-stu-id="2685c-427">Properties</span></span>   | <span data-ttu-id="2685c-428">Действия, связанные с чтением и записью именованных свойств класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-428">Actions associated with reading and writing named properties of the class</span></span> |
| <span data-ttu-id="2685c-429">Индексаторы</span><span class="sxs-lookup"><span data-stu-id="2685c-429">Indexers</span></span>     | <span data-ttu-id="2685c-430">Действия, реализующие индексирование экземпляров класса, чтобы обращаться к ним как к массиву.</span><span class="sxs-lookup"><span data-stu-id="2685c-430">Actions associated with indexing instances of the class like an array</span></span> |
| <span data-ttu-id="2685c-431">События</span><span class="sxs-lookup"><span data-stu-id="2685c-431">Events</span></span>       | <span data-ttu-id="2685c-432">Уведомления, которые могут быть созданы этим классом.</span><span class="sxs-lookup"><span data-stu-id="2685c-432">Notifications that can be generated by the class</span></span> |
| <span data-ttu-id="2685c-433">Операторы</span><span class="sxs-lookup"><span data-stu-id="2685c-433">Operators</span></span>    | <span data-ttu-id="2685c-434">Поддерживаемые классом операторы преобразования и выражения.</span><span class="sxs-lookup"><span data-stu-id="2685c-434">Conversions and expression operators supported by the class</span></span> |
| <span data-ttu-id="2685c-435">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="2685c-435">Constructors</span></span> | <span data-ttu-id="2685c-436">Действия, необходимые для инициализации экземпляров класса или класса в целом.</span><span class="sxs-lookup"><span data-stu-id="2685c-436">Actions required to initialize instances of the class or the class itself</span></span> |
| <span data-ttu-id="2685c-437">Деструкторы</span><span class="sxs-lookup"><span data-stu-id="2685c-437">Destructors</span></span>  | <span data-ttu-id="2685c-438">Действия, выполняемые перед окончательным удалением экземпляров класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-438">Actions to perform before instances of the class are permanently discarded</span></span> |
| <span data-ttu-id="2685c-439">Типы</span><span class="sxs-lookup"><span data-stu-id="2685c-439">Types</span></span>        | <span data-ttu-id="2685c-440">Вложенные типы, объявленные в классе.</span><span class="sxs-lookup"><span data-stu-id="2685c-440">Nested types declared by the class</span></span> |

### <a name="accessibility"></a><span data-ttu-id="2685c-441">Специальные возможности</span><span class="sxs-lookup"><span data-stu-id="2685c-441">Accessibility</span></span>

<span data-ttu-id="2685c-442">Каждый член класса имеет определенный уровень доступности. Он определяет, из какой области программы можно обращаться к этому члену.</span><span class="sxs-lookup"><span data-stu-id="2685c-442">Each member of a class has an associated accessibility, which controls the regions of program text that are able to access the member.</span></span> <span data-ttu-id="2685c-443">Существует пять уровней доступности.</span><span class="sxs-lookup"><span data-stu-id="2685c-443">There are five possible forms of accessibility.</span></span> <span data-ttu-id="2685c-444">Эти отчеты представлены в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="2685c-444">These are summarized in the following table.</span></span>


| <span data-ttu-id="2685c-445">__Специальные возможности__</span><span class="sxs-lookup"><span data-stu-id="2685c-445">__Accessibility__</span></span>    | <span data-ttu-id="2685c-446">__Значение__</span><span class="sxs-lookup"><span data-stu-id="2685c-446">__Meaning__</span></span> |
|----------------------|-----------------|
| `public`             | <span data-ttu-id="2685c-447">Доступ не ограничен.</span><span class="sxs-lookup"><span data-stu-id="2685c-447">Access not limited</span></span> |
| `protected`          | <span data-ttu-id="2685c-448">Доступ возможен из этого класса и из классов, унаследованных от него.</span><span class="sxs-lookup"><span data-stu-id="2685c-448">Access limited to this class or classes derived from this class</span></span> |
| `internal`           | <span data-ttu-id="2685c-449">Доступ возможен только из текущей программы.</span><span class="sxs-lookup"><span data-stu-id="2685c-449">Access limited to this program</span></span> |
| `protected internal` | <span data-ttu-id="2685c-450">Доступ возможен только из текущей программы и из классов, унаследованных от этого класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-450">Access limited to this program or classes derived from this class</span></span> |
| `private`            | <span data-ttu-id="2685c-451">Доступ возможен только из этого класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-451">Access limited to this class</span></span> |

### <a name="type-parameters"></a><span data-ttu-id="2685c-452">Параметры типа</span><span class="sxs-lookup"><span data-stu-id="2685c-452">Type parameters</span></span>

<span data-ttu-id="2685c-453">Определение класса может задать набор параметров типа. Список имен параметров типа указывается в угловых скобках после имени класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-453">A class definition may specify a set of type parameters by following the class name with angle brackets enclosing a list of type parameter names.</span></span> <span data-ttu-id="2685c-454">Параметры типа могут использоваться в теле объявления класса для определения членов класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-454">The type parameters can the be used in the body of the class declarations to define the members of the class.</span></span> <span data-ttu-id="2685c-455">В следующем примере для класса `Pair` заданы параметры типа `TFirst` и `TSecond`:</span><span class="sxs-lookup"><span data-stu-id="2685c-455">In the following example, the type parameters of `Pair` are `TFirst` and `TSecond`:</span></span>

```csharp
public class Pair<TFirst,TSecond>
{
    public TFirst First;
    public TSecond Second;
}
```
<span data-ttu-id="2685c-456">Типом класса, объявленного параметры типа, называется типом универсального класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-456">A class type that is declared to take type parameters is called a generic class type.</span></span> <span data-ttu-id="2685c-457">Типы структуры, интерфейса и делегата также могут быть универсальными.</span><span class="sxs-lookup"><span data-stu-id="2685c-457">Struct, interface and delegate types can also be generic.</span></span>

<span data-ttu-id="2685c-458">Если вы используете универсальный класс, необходимо указать аргумент типа для каждого параметра типа, вот так:</span><span class="sxs-lookup"><span data-stu-id="2685c-458">When the generic class is used, type arguments must be provided for each of the type parameters:</span></span>

```csharp
Pair<int,string> pair = new Pair<int,string> { First = 1, Second = "two" };
int i = pair.First;     // TFirst is int
string s = pair.Second; // TSecond is string
```
<span data-ttu-id="2685c-459">Универсальный тип с предоставленными аргументами типа, например `Pair<int,string>
    ` , называется сконструированного типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-459">A generic type with type arguments provided, like `Pair<int,string>
    ` above, is called a constructed type.</span></span>

### <a name="base-classes"></a><span data-ttu-id="2685c-460">базовых классов;</span><span class="sxs-lookup"><span data-stu-id="2685c-460">Base classes</span></span>

<span data-ttu-id="2685c-461">В объявлении класса можно указать базовый класс, включив имя базового класса после имени класса и параметров типа, и отделив его двоеточием.</span><span class="sxs-lookup"><span data-stu-id="2685c-461">A class declaration may specify a base class by following the class name and type parameters with a colon and the name of the base class.</span></span> <span data-ttu-id="2685c-462">Если спецификация базового класса не указана, класс наследуется от типа `object`.</span><span class="sxs-lookup"><span data-stu-id="2685c-462">Omitting a base class specification is the same as deriving from type `object`.</span></span> <span data-ttu-id="2685c-463">В следующем примере `Point3D` имеет базовый класс `Point`, а `Point` — базовый класс `object`:</span><span class="sxs-lookup"><span data-stu-id="2685c-463">In the following example, the base class of `Point3D` is `Point`, and the base class of `Point` is `object`:</span></span>

```csharp
public class Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

public class Point3D: Point
{
    public int z;

    public Point3D(int x, int y, int z): base(x, y) {
        this.z = z;
    }
}
```
<span data-ttu-id="2685c-464">Класс наследует члены базового класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-464">A class inherits the members of its base class.</span></span> <span data-ttu-id="2685c-465">Наследование означает, что класс неявно содержит все члены базового класса, за исключением экземпляра и статические конструкторы и деструкторы базового класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-465">Inheritance means that a class implicitly contains all members of its base class, except for the instance and static constructors, and the destructors of the base class.</span></span> <span data-ttu-id="2685c-466">Производный класс может дополнить наследуемые элементы новыми элементами, но он не может удалить определение для наследуемого члена.</span><span class="sxs-lookup"><span data-stu-id="2685c-466">A derived class can add new members to those it inherits, but it cannot remove the definition of an inherited member.</span></span> <span data-ttu-id="2685c-467">В предыдущем примере `Point3D` наследует поля `x` и `y` из `Point`, и каждый экземпляр `Point3D` содержит три поля: `x`, `y` и `z`.</span><span class="sxs-lookup"><span data-stu-id="2685c-467">In the previous example, `Point3D` inherits the `x` and `y` fields from `Point`, and every `Point3D` instance contains three fields, `x`, `y`, and `z`.</span></span>

<span data-ttu-id="2685c-468">Используется неявное преобразование из типа класса к любому из типов соответствующего базового класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-468">An implicit conversion exists from a class type to any of its base class types.</span></span> <span data-ttu-id="2685c-469">Это означает, что переменная типа класса может ссылаться как на экземпляр этого класса, так и на экземпляры любого производного класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-469">Therefore, a variable of a class type can reference an instance of that class or an instance of any derived class.</span></span> <span data-ttu-id="2685c-470">Например, если мы используем описанные выше объявления классов, то переменная типа `Point` может ссылаться на `Point` или `Point3D`:</span><span class="sxs-lookup"><span data-stu-id="2685c-470">For example, given the previous class declarations, a variable of type `Point` can reference either a `Point` or a `Point3D`:</span></span>

```csharp
Point a = new Point(10, 20);
Point b = new Point3D(10, 20, 30);
```

### <a name="fields"></a><span data-ttu-id="2685c-471">Поля</span><span class="sxs-lookup"><span data-stu-id="2685c-471">Fields</span></span>

<span data-ttu-id="2685c-472">Поле — это переменная, который связан с классом или экземпляром класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-472">A field is a variable that is associated with a class or with an instance of a class.</span></span>

<span data-ttu-id="2685c-473">Поле объявлено с `static` модификатор определяет ***статическое поле***.</span><span class="sxs-lookup"><span data-stu-id="2685c-473">A field declared with the `static` modifier defines a ***static field***.</span></span> <span data-ttu-id="2685c-474">Статическое поле определяет строго одно место хранения.</span><span class="sxs-lookup"><span data-stu-id="2685c-474">A static field identifies exactly one storage location.</span></span> <span data-ttu-id="2685c-475">Независимо от того, сколько будет создано экземпляров этого класса, существует только одна копия статического поля.</span><span class="sxs-lookup"><span data-stu-id="2685c-475">No matter how many instances of a class are created, there is only ever one copy of a static field.</span></span>

<span data-ttu-id="2685c-476">Поле объявлено без `static` модификатор определяет ***поле экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="2685c-476">A field declared without the `static` modifier defines an ***instance field***.</span></span> <span data-ttu-id="2685c-477">Каждый экземпляр класса содержит отдельные копии всех полей экземпляра, определенных для этого класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-477">Every instance of a class contains a separate copy of all the instance fields of that class.</span></span>

<span data-ttu-id="2685c-478">В следующем примере каждый экземпляр класса `Color` содержит отдельную копию полей экземпляра `r`, `g` и `b`, но для каждого из статических полей `Black`, `White`, `Red`, `Green` и `Blue` существует только одна копия:</span><span class="sxs-lookup"><span data-stu-id="2685c-478">In the following example, each instance of the `Color` class has a separate copy of the `r`, `g`, and `b` instance fields, but there is only one copy of the `Black`, `White`, `Red`, `Green`, and `Blue` static fields:</span></span>

```csharp
public class Color
{
    public static readonly Color Black = new Color(0, 0, 0);
    public static readonly Color White = new Color(255, 255, 255);
    public static readonly Color Red = new Color(255, 0, 0);
    public static readonly Color Green = new Color(0, 255, 0);
    public static readonly Color Blue = new Color(0, 0, 255);
    private byte r, g, b;

    public Color(byte r, byte g, byte b) {
        this.r = r;
        this.g = g;
        this.b = b;
    }
}
```
<span data-ttu-id="2685c-479">Как показано в предыдущем примере, можно объявить ***поля только для чтения***, используя модификатор `readonly`.</span><span class="sxs-lookup"><span data-stu-id="2685c-479">As shown in the previous example, ***read-only fields*** may be declared with a `readonly` modifier.</span></span> <span data-ttu-id="2685c-480">Назначение `readonly` поля может происходить только как часть объявления поля или в конструкторе в том же классе.</span><span class="sxs-lookup"><span data-stu-id="2685c-480">Assignment to a `readonly` field can only occur as part of the field's declaration or in a constructor in the same class.</span></span>

### <a name="methods"></a><span data-ttu-id="2685c-481">Методы</span><span class="sxs-lookup"><span data-stu-id="2685c-481">Methods</span></span>

<span data-ttu-id="2685c-482">***Метод*** — это член, реализующий вычисление или действие, которое может выполнять объект или класс.</span><span class="sxs-lookup"><span data-stu-id="2685c-482">A ***method*** is a member that implements a computation or action that can be performed by an object or class.</span></span> <span data-ttu-id="2685c-483">Доступ к ***статическим методам*** осуществляется через класс.</span><span class="sxs-lookup"><span data-stu-id="2685c-483">***Static methods*** are accessed through the class.</span></span> <span data-ttu-id="2685c-484">Доступ к ***методам экземпляра*** осуществляется через экземпляр класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-484">***Instance methods*** are accessed through instances of the class.</span></span>

<span data-ttu-id="2685c-485">Методы имеют (возможно, пустой) список ***параметры***, которые представляют значения или ссылки на переменные, передаваемые методу и ***тип возвращаемого значения***, который указывает тип значения, вычисляемого и возвращаемого по метод.</span><span class="sxs-lookup"><span data-stu-id="2685c-485">Methods have a (possibly empty) list of ***parameters***, which represent values or variable references passed to the method, and a ***return type***, which specifies the type of the value computed and returned by the method.</span></span> <span data-ttu-id="2685c-486">Тип возвращаемого значения метода `void` если он не возвращает значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-486">A method's return type is `void` if it does not return a value.</span></span>

<span data-ttu-id="2685c-487">Как и типы, методы могут иметь набор параметров типа, для которых при вызове метода необходимо указывать аргументы типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-487">Like types, methods may also have a set of type parameters, for which type arguments must be specified when the method is called.</span></span> <span data-ttu-id="2685c-488">В отличие от типов, аргументы типа зачастую могут выводиться из аргументов вызова метода, и тогда их не обязательно задавать явным образом.</span><span class="sxs-lookup"><span data-stu-id="2685c-488">Unlike types, the type arguments can often be inferred from the arguments of a method call and need not be explicitly given.</span></span>

<span data-ttu-id="2685c-489">***Сигнатура*** метода должна быть уникальной в пределах класса, в котором объявлен этот метод.</span><span class="sxs-lookup"><span data-stu-id="2685c-489">The ***signature*** of a method must be unique in the class in which the method is declared.</span></span> <span data-ttu-id="2685c-490">Сигнатура метода включает имя метода, количество параметров типа, а также количество, модификаторы и типы параметров метода.</span><span class="sxs-lookup"><span data-stu-id="2685c-490">The signature of a method consists of the name of the method, the number of type parameters and the number, modifiers, and types of its parameters.</span></span> <span data-ttu-id="2685c-491">Сигнатура метода не включает возвращаемый тип.</span><span class="sxs-lookup"><span data-stu-id="2685c-491">The signature of a method does not include the return type.</span></span>

#### <a name="parameters"></a><span data-ttu-id="2685c-492">Параметры</span><span class="sxs-lookup"><span data-stu-id="2685c-492">Parameters</span></span>

<span data-ttu-id="2685c-493">Параметры позволяют передать в метод значения или ссылки на переменные.</span><span class="sxs-lookup"><span data-stu-id="2685c-493">Parameters are used to pass values or variable references to methods.</span></span> <span data-ttu-id="2685c-494">Фактические значения параметрам метода присваиваются на основе ***аргументов***, заданных при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="2685c-494">The parameters of a method get their actual values from the ***arguments*** that are specified when the method is invoked.</span></span> <span data-ttu-id="2685c-495">Существует четыре типа параметров: параметры значения, ссылочные параметры, параметры вывода и массивы параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-495">There are four kinds of parameters: value parameters, reference parameters, output parameters, and parameter arrays.</span></span>

<span data-ttu-id="2685c-496">***Параметр значения*** передает один входной параметр.</span><span class="sxs-lookup"><span data-stu-id="2685c-496">A ***value parameter*** is used for input parameter passing.</span></span> <span data-ttu-id="2685c-497">Параметр значения сопоставляется с локальной переменной, которая получит начальное значение из значения аргумента, переданного в этом параметре.</span><span class="sxs-lookup"><span data-stu-id="2685c-497">A value parameter corresponds to a local variable that gets its initial value from the argument that was passed for the parameter.</span></span> <span data-ttu-id="2685c-498">Изменения параметра значения не влияют на аргумент, переданный для этого параметра.</span><span class="sxs-lookup"><span data-stu-id="2685c-498">Modifications to a value parameter do not affect the argument that was passed for the parameter.</span></span>

<span data-ttu-id="2685c-499">Параметры значения можно сделать необязательными, указав для них значения по умолчанию. Тогда соответствующие аргументы можно не указывать.</span><span class="sxs-lookup"><span data-stu-id="2685c-499">Value parameters can be optional, by specifying a default value so that corresponding arguments can be omitted.</span></span>

<span data-ttu-id="2685c-500">***Ссылочный параметр*** используется как для входных, так и для выходных параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-500">A ***reference parameter*** is used for both input and output parameter passing.</span></span> <span data-ttu-id="2685c-501">Аргумент, передаваемый ссылочному параметру, должен являться переменной. При выполнении метода ссылочный параметр указывает на то же место хранения, где размещена переменная аргумента.</span><span class="sxs-lookup"><span data-stu-id="2685c-501">The argument passed for a reference parameter must be a variable, and during execution of the method, the reference parameter represents the same storage location as the argument variable.</span></span> <span data-ttu-id="2685c-502">Чтобы объявить ссылочный параметр, используйте модификатор `ref`.</span><span class="sxs-lookup"><span data-stu-id="2685c-502">A reference parameter is declared with the `ref` modifier.</span></span> <span data-ttu-id="2685c-503">Следующий пример кода демонстрирует использование параметров `ref`.</span><span class="sxs-lookup"><span data-stu-id="2685c-503">The following example shows the use of `ref` parameters.</span></span>

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
        Console.WriteLine("{0} {1}", i, j);            // Outputs "2 1"
    }
}
```
<span data-ttu-id="2685c-504">***Параметр вывода*** передает один выходной параметр.</span><span class="sxs-lookup"><span data-stu-id="2685c-504">An ***output parameter*** is used for output parameter passing.</span></span> <span data-ttu-id="2685c-505">Параметр вывода действует так же, как и ссылочный параметр, но для него не используется исходное значение аргумента, предоставленного при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="2685c-505">An output parameter is similar to a reference parameter except that the initial value of the caller-provided argument is unimportant.</span></span> <span data-ttu-id="2685c-506">Чтобы объявить параметр вывода, используйте модификатор `out`.</span><span class="sxs-lookup"><span data-stu-id="2685c-506">An output parameter is declared with the `out` modifier.</span></span> <span data-ttu-id="2685c-507">Следующий пример кода демонстрирует использование параметров `out`.</span><span class="sxs-lookup"><span data-stu-id="2685c-507">The following example shows the use of `out` parameters.</span></span>

```csharp
using System;

class Test
{
    static void Divide(int x, int y, out int result, out int remainder) {
        result = x / y;
        remainder = x % y;
    }

    static void Main() {
        int res, rem;
        Divide(10, 3, out res, out rem);
        Console.WriteLine("{0} {1}", res, rem);    // Outputs "3 1"
    }
}
```
<span data-ttu-id="2685c-508">***Массив параметров*** позволяет передавать в метод переменное число аргументов.</span><span class="sxs-lookup"><span data-stu-id="2685c-508">A ***parameter array*** permits a variable number of arguments to be passed to a method.</span></span> <span data-ttu-id="2685c-509">Чтобы объявить массив параметров, используйте модификатор `params`.</span><span class="sxs-lookup"><span data-stu-id="2685c-509">A parameter array is declared with the `params` modifier.</span></span> <span data-ttu-id="2685c-510">Массив параметров может быть только последним параметром в методе. Для него можно использовать только тип одномерного массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-510">Only the last parameter of a method can be a parameter array, and the type of a parameter array must be a single-dimensional array type.</span></span> <span data-ttu-id="2685c-511">`Write` И `WriteLine` методы `System.Console` класс — это хорошие примеры использования массива параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-511">The `Write` and `WriteLine` methods of the `System.Console` class are good examples of parameter array usage.</span></span> <span data-ttu-id="2685c-512">Ниже представлены объявления этих методов.</span><span class="sxs-lookup"><span data-stu-id="2685c-512">They are declared as follows.</span></span>

```csharp
public class Console
{
    public static void Write(string fmt, params object[] args) {...}
    public static void WriteLine(string fmt, params object[] args) {...}
    ...
}
```
<span data-ttu-id="2685c-513">Внутри метода массив параметров полностью идентичен обычному параметру типа массив.</span><span class="sxs-lookup"><span data-stu-id="2685c-513">Within a method that uses a parameter array, the parameter array behaves exactly like a regular parameter of an array type.</span></span> <span data-ttu-id="2685c-514">Но зато при вызове метода, использующего массив параметров, ему можно передать либо один аргумент типа массив, либо любое количество аргументов типа элемент для массива параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-514">However, in an invocation of a method with a parameter array, it is possible to pass either a single argument of the parameter array type or any number of arguments of the element type of the parameter array.</span></span> <span data-ttu-id="2685c-515">В последнем случае экземпляр массива автоматически создается и инициализируется с заданными аргументами.</span><span class="sxs-lookup"><span data-stu-id="2685c-515">In the latter case, an array instance is automatically created and initialized with the given arguments.</span></span> <span data-ttu-id="2685c-516">Код из этого примера...</span><span class="sxs-lookup"><span data-stu-id="2685c-516">This example</span></span>

```csharp
Console.WriteLine("x={0} y={1} z={2}", x, y, z);
```
<span data-ttu-id="2685c-517">...эквивалентен следующей конструкции:</span><span class="sxs-lookup"><span data-stu-id="2685c-517">is equivalent to writing the following.</span></span>

```csharp
string s = "x={0} y={1} z={2}";
object[] args = new object[3];
args[0] = x;
args[1] = y;
args[2] = z;
Console.WriteLine(s, args);
```

#### <a name="method-body-and-local-variables"></a><span data-ttu-id="2685c-518">Тело метода и локальные переменные</span><span class="sxs-lookup"><span data-stu-id="2685c-518">Method body and local variables</span></span>

<span data-ttu-id="2685c-519">В теле метода задает операторы, выполняемые при вызове метода.</span><span class="sxs-lookup"><span data-stu-id="2685c-519">A method's body specifies the statements to execute when the method is invoked.</span></span>

<span data-ttu-id="2685c-520">В теле метода можно объявлять переменные, относящиеся к выполнению этого метода.</span><span class="sxs-lookup"><span data-stu-id="2685c-520">A method body can declare variables that are specific to the invocation of the method.</span></span> <span data-ttu-id="2685c-521">Такие переменные называются ***локальными переменными***.</span><span class="sxs-lookup"><span data-stu-id="2685c-521">Such variables are called ***local variables***.</span></span> <span data-ttu-id="2685c-522">В объявлении локальной переменной нужно указать имя типа и имя переменной. Также можно задать ее начальное значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-522">A local variable declaration specifies a type name, a variable name, and possibly an initial value.</span></span> <span data-ttu-id="2685c-523">Следующий пример кода объявляет локальную переменную `i` с нулевым начальным значением, и еще одну локальную переменную `j` без начального значения.</span><span class="sxs-lookup"><span data-stu-id="2685c-523">The following example declares a local variable `i` with an initial value of zero and a local variable `j` with no initial value.</span></span>

```csharp
using System;

class Squares
{
    static void Main() {
        int i = 0;
        int j;
        while (i < 10) {
            j = i * i;
            Console.WriteLine("{0} x {0} = {1}", i, j);
            i = i + 1;
        }
    }
}
```
<span data-ttu-id="2685c-524">C# требует, чтобы локальной переменной было ***явно присвоено значение***, прежде чем можно будет получить это значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-524">C# requires a local variable to be ***definitely assigned*** before its value can be obtained.</span></span> <span data-ttu-id="2685c-525">Например, если в предложенное выше объявление `i` не включить начальное значение, компилятор сообщит об ошибке при последующем использовании `i`, поскольку для `i` нет явно присвоенного значения.</span><span class="sxs-lookup"><span data-stu-id="2685c-525">For example, if the declaration of the previous `i` did not include an initial value, the compiler would report an error for the subsequent usages of `i` because `i` would not be definitely assigned at those points in the program.</span></span>

<span data-ttu-id="2685c-526">Метод может использовать инструкцию `return`, чтобы вернуть управление вызывающему объекту.</span><span class="sxs-lookup"><span data-stu-id="2685c-526">A method can use `return` statements to return control to its caller.</span></span> <span data-ttu-id="2685c-527">Если метод возвращает `void`, в нем нельзя использовать инструкцию `return` с выражением.</span><span class="sxs-lookup"><span data-stu-id="2685c-527">In a method returning `void`, `return` statements cannot specify an expression.</span></span> <span data-ttu-id="2685c-528">Метод возвращает не -`void`, `return` инструкции должны содержать выражение, которое вычисляет возвращаемое значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-528">In a method returning non-`void`, `return` statements must include an expression that computes the return value.</span></span>

#### <a name="static-and-instance-methods"></a><span data-ttu-id="2685c-529">Статические методы и методы экземпляра</span><span class="sxs-lookup"><span data-stu-id="2685c-529">Static and instance methods</span></span>

<span data-ttu-id="2685c-530">Метод, объявленный с `static` модификатор ***статический метод***.</span><span class="sxs-lookup"><span data-stu-id="2685c-530">A method declared with a `static` modifier is a ***static method***.</span></span> <span data-ttu-id="2685c-531">Статический метод не работает с конкретным экземпляром и может напрямую обращаться только к статическим членам.</span><span class="sxs-lookup"><span data-stu-id="2685c-531">A static method does not operate on a specific instance and can only directly access static members.</span></span>

<span data-ttu-id="2685c-532">Метод, объявленный без `static` модификатор ***метод экземпляра***.</span><span class="sxs-lookup"><span data-stu-id="2685c-532">A method declared without a `static` modifier is an ***instance method***.</span></span> <span data-ttu-id="2685c-533">Метод экземпляра работает в определенном экземпляре и может обращаться как к статическим методам, так и к методам этого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2685c-533">An instance method operates on a specific instance and can access both static and instance members.</span></span> <span data-ttu-id="2685c-534">В методе можно напрямую обратиться к экземпляру, для которого этот метод был вызван, используя дескриптор `this`.</span><span class="sxs-lookup"><span data-stu-id="2685c-534">The instance on which an instance method was invoked can be explicitly accessed as `this`.</span></span> <span data-ttu-id="2685c-535">Использование `this` в статическом методе приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="2685c-535">It is an error to refer to `this` in a static method.</span></span>

<span data-ttu-id="2685c-536">Следующий класс `Entity` содержит статические члены и члены экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2685c-536">The following `Entity` class has both static and instance members.</span></span>

```csharp
class Entity
{
    static int nextSerialNo;
    int serialNo;

    public Entity() {
        serialNo = nextSerialNo++;
    }

    public int GetSerialNo() {
        return serialNo;
    }

    public static int GetNextSerialNo() {
        return nextSerialNo;
    }

    public static void SetNextSerialNo(int value) {
        nextSerialNo = value;
    }
}
```
<span data-ttu-id="2685c-537">Каждый экземпляр `Entity` содержит серийный номер (и может содержать другие данные, которые здесь не показаны).</span><span class="sxs-lookup"><span data-stu-id="2685c-537">Each `Entity` instance contains a serial number (and presumably some other information that is not shown here).</span></span> <span data-ttu-id="2685c-538">Конструктор объекта `Entity` (который рассматривается как метод экземпляра) задает для нового экземпляра следующий доступный серийный номер.</span><span class="sxs-lookup"><span data-stu-id="2685c-538">The `Entity` constructor (which is like an instance method) initializes the new instance with the next available serial number.</span></span> <span data-ttu-id="2685c-539">Поскольку конструктор является членом экземпляра, он может обращаться как к полю экземпляра `serialNo`, так и к статическому полю `nextSerialNo`.</span><span class="sxs-lookup"><span data-stu-id="2685c-539">Because the constructor is an instance member, it is permitted to access both the `serialNo` instance field and the `nextSerialNo` static field.</span></span>

<span data-ttu-id="2685c-540">Статические методы `GetNextSerialNo` и `SetNextSerialNo` могут обращаться к статическому полю `nextSerialNo`, но прямое обращение из них к полю экземпляра `serialNo` приводит к ошибке.</span><span class="sxs-lookup"><span data-stu-id="2685c-540">The `GetNextSerialNo` and `SetNextSerialNo` static methods can access the `nextSerialNo` static field, but it would be an error for them to directly access the `serialNo` instance field.</span></span>

<span data-ttu-id="2685c-541">В следующем примере показано использование `Entity` класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-541">The following example shows the use of the `Entity` class.</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        Entity.SetNextSerialNo(1000);
        Entity e1 = new Entity();
        Entity e2 = new Entity();
        Console.WriteLine(e1.GetSerialNo());           // Outputs "1000"
        Console.WriteLine(e2.GetSerialNo());           // Outputs "1001"
        Console.WriteLine(Entity.GetNextSerialNo());   // Outputs "1002"
    }
}
```
<span data-ttu-id="2685c-542">Обратите внимание, что статические методы `SetNextSerialNo` и `GetNextSerialNo` вызываются для класса, а метод экземпляра `GetSerialNo` вызывается для экземпляров класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-542">Note that the `SetNextSerialNo` and `GetNextSerialNo` static methods are invoked on the class whereas the `GetSerialNo` instance method is invoked on instances of the class.</span></span>

#### <a name="virtual-override-and-abstract-methods"></a><span data-ttu-id="2685c-543">Виртуальные, переопределяющие и абстрактные методы</span><span class="sxs-lookup"><span data-stu-id="2685c-543">Virtual, override, and abstract methods</span></span>

<span data-ttu-id="2685c-544">Если объявление метода экземпляра включает модификатор `virtual`, такой метод называется ***виртуальным методом***.</span><span class="sxs-lookup"><span data-stu-id="2685c-544">When an instance method declaration includes a `virtual` modifier, the method is said to be a ***virtual method***.</span></span> <span data-ttu-id="2685c-545">Если аргумент `virtual` модификатора, метод считается ***невиртуальный метод***.</span><span class="sxs-lookup"><span data-stu-id="2685c-545">When no `virtual` modifier is present, the method is said to be a ***non-virtual method***.</span></span>

<span data-ttu-id="2685c-546">При вызове виртуального метода могут быть вызваны разные его реализации в зависимости от того, какой ***тип среды выполнения*** имеет экземпляр, для которого вызван этот метод.</span><span class="sxs-lookup"><span data-stu-id="2685c-546">When a virtual method is invoked, the ***run-time type*** of the instance for which that invocation takes place determines the actual method implementation to invoke.</span></span> <span data-ttu-id="2685c-547">При вызове невиртуального метода решающим фактором является ***тип во время компиляции*** для этого экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2685c-547">In a nonvirtual method invocation, the ***compile-time type*** of the instance is the determining factor.</span></span>

<span data-ttu-id="2685c-548">Виртуальный метод можно ***переопределить*** в производном классе.</span><span class="sxs-lookup"><span data-stu-id="2685c-548">A virtual method can be ***overridden*** in a derived class.</span></span> <span data-ttu-id="2685c-549">Если объявление метода экземпляра включает `override` модификатор, метод переопределяет унаследованный виртуальный метод с такой же сигнатурой.</span><span class="sxs-lookup"><span data-stu-id="2685c-549">When an instance method declaration includes an `override` modifier, the method overrides an inherited virtual method with the same signature.</span></span> <span data-ttu-id="2685c-550">Изначальное объявление виртуального метода создает новый метод, а переопределение этого метода создает специализированный виртуальный метод с новой реализацией взамен унаследованного виртуального метода.</span><span class="sxs-lookup"><span data-stu-id="2685c-550">Whereas a virtual method declaration introduces a new method, an override method declaration specializes an existing inherited virtual method by providing a new implementation of that method.</span></span>

<span data-ttu-id="2685c-551">***Абстрактный*** метод является виртуальным методом без реализации.</span><span class="sxs-lookup"><span data-stu-id="2685c-551">An ***abstract*** method is a virtual method with no implementation.</span></span> <span data-ttu-id="2685c-552">Абстрактный метод объявляется с `abstract` модификатор и допускается только в классе, объявленном как `abstract`.</span><span class="sxs-lookup"><span data-stu-id="2685c-552">An abstract method is declared with the `abstract` modifier and is permitted only in a class that is also declared `abstract`.</span></span> <span data-ttu-id="2685c-553">Абстрактный метод должен обязательно переопределяться в каждом производном классе, не являющемся абстрактным.</span><span class="sxs-lookup"><span data-stu-id="2685c-553">An abstract method must be overridden in every non-abstract derived class.</span></span>

<span data-ttu-id="2685c-554">Следующий пример кода объявляет абстрактный класс `Expression`, который представляет узел дерева выражений, а также три производных класса: `Constant`, `VariableReference` и `Operation`, которые реализуют узлы дерева выражений для констант, ссылок на переменные и арифметических операций.</span><span class="sxs-lookup"><span data-stu-id="2685c-554">The following example declares an abstract class, `Expression`, which represents an expression tree node, and three derived classes, `Constant`, `VariableReference`, and `Operation`, which implement expression tree nodes for constants, variable references, and arithmetic operations.</span></span> <span data-ttu-id="2685c-555">(Это похоже на, но не следует путать с типы дерева выражений, представленные в [типы дерева выражений](types.md#expression-tree-types)).</span><span class="sxs-lookup"><span data-stu-id="2685c-555">(This is similar to, but not to be confused with the expression tree types introduced in [Expression tree types](types.md#expression-tree-types)).</span></span>

```csharp
using System;
using System.Collections;

public abstract class Expression
{
    public abstract double Evaluate(Hashtable vars);
}

public class Constant: Expression
{
    double value;

    public Constant(double value) {
        this.value = value;
    }

    public override double Evaluate(Hashtable vars) {
        return value;
    }
}

public class VariableReference: Expression
{
    string name;

    public VariableReference(string name) {
        this.name = name;
    }

    public override double Evaluate(Hashtable vars) {
        object value = vars[name];
        if (value == null) {
            throw new Exception("Unknown variable: " + name);
        }
        return Convert.ToDouble(value);
    }
}

public class Operation: Expression
{
    Expression left;
    char op;
    Expression right;

    public Operation(Expression left, char op, Expression right) {
        this.left = left;
        this.op = op;
        this.right = right;
    }

    public override double Evaluate(Hashtable vars) {
        double x = left.Evaluate(vars);
        double y = right.Evaluate(vars);
        switch (op) {
            case '+': return x + y;
            case '-': return x - y;
            case '*': return x * y;
            case '/': return x / y;
        }
        throw new Exception("Unknown operator");
    }
}
```
<span data-ttu-id="2685c-556">Четыре приведенных выше класса можно использовать для моделирования арифметических выражений.</span><span class="sxs-lookup"><span data-stu-id="2685c-556">The previous four classes can be used to model arithmetic expressions.</span></span> <span data-ttu-id="2685c-557">Например, с помощью экземпляров этих классов выражение `x + 3` можно представить следующим образом.</span><span class="sxs-lookup"><span data-stu-id="2685c-557">For example, using instances of these classes, the expression `x + 3` can be represented as follows.</span></span>

```csharp
Expression e = new Operation(
    new VariableReference("x"),
    '+',
    new Constant(3));
```
<span data-ttu-id="2685c-558">Метод `Evaluate` экземпляра `Expression` вызывается для вычисления данного выражения и создает значение `double`.</span><span class="sxs-lookup"><span data-stu-id="2685c-558">The `Evaluate` method of an `Expression` instance is invoked to evaluate the given expression and produce a `double` value.</span></span> <span data-ttu-id="2685c-559">Этот метод принимает в качестве аргумента `Hashtable` , содержащий имена переменных (в качестве ключей записей) и значения (в качестве значений записей).</span><span class="sxs-lookup"><span data-stu-id="2685c-559">The method takes as an argument a `Hashtable` that contains variable names (as keys of the entries) and values (as values of the entries).</span></span> <span data-ttu-id="2685c-560">`Evaluate` Метод является виртуальным методом абстрактный, это означает, что неабстрактные производные классы должны переопределить его, чтобы предоставить фактическую реализацию.</span><span class="sxs-lookup"><span data-stu-id="2685c-560">The `Evaluate` method is a virtual abstract method, meaning that non-abstract derived classes must override it to provide an actual implementation.</span></span>

<span data-ttu-id="2685c-561">В `Constant` реализация метода `Evaluate` просто возвращает хранимую константу.</span><span class="sxs-lookup"><span data-stu-id="2685c-561">A `Constant`'s implementation of `Evaluate` simply returns the stored constant.</span></span> <span data-ttu-id="2685c-562">Объект `VariableReference`реализация этого метода выполняет поиск имени переменной в хэш-таблицу и возвращает результирующее значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-562">A `VariableReference`'s implementation looks up the variable name in the hashtable and returns the resulting value.</span></span> <span data-ttu-id="2685c-563">В `Operation` реализация этого метода сначала вычисляет левый и правый операнды (рекурсивно вызывая их методы `Evaluate`), а затем выполняет предоставленную арифметическую операцию.</span><span class="sxs-lookup"><span data-stu-id="2685c-563">An `Operation`'s implementation first evaluates the left and right operands (by recursively invoking their `Evaluate` methods) and then performs the given arithmetic operation.</span></span>

<span data-ttu-id="2685c-564">В следующей программе классы `Expression` используются для вычисления выражения `x * (y + 2)` с различными значениями `x` и `y`.</span><span class="sxs-lookup"><span data-stu-id="2685c-564">The following program uses the `Expression` classes to evaluate the expression `x * (y + 2)` for different values of `x` and `y`.</span></span>

```csharp
using System;
using System.Collections;

class Test
{
    static void Main() {
        Expression e = new Operation(
            new VariableReference("x"),
            '*',
            new Operation(
                new VariableReference("y"),
                '+',
                new Constant(2)
            )
        );
        Hashtable vars = new Hashtable();
        vars["x"] = 3;
        vars["y"] = 5;
        Console.WriteLine(e.Evaluate(vars));        // Outputs "21"
        vars["x"] = 1.5;
        vars["y"] = 9;
        Console.WriteLine(e.Evaluate(vars));        // Outputs "16.5"
    }
}
```

#### <a name="method-overloading"></a><span data-ttu-id="2685c-565">Перегрузка методов</span><span class="sxs-lookup"><span data-stu-id="2685c-565">Method overloading</span></span>

<span data-ttu-id="2685c-566">***Перегрузка*** метода позволяет использовать в одном классе несколько методов с одинаковыми именами, если они имеют уникальные сигнатуры.</span><span class="sxs-lookup"><span data-stu-id="2685c-566">Method ***overloading*** permits multiple methods in the same class to have the same name as long as they have unique signatures.</span></span> <span data-ttu-id="2685c-567">Когда при компиляции встречается вызов перегруженного метода, компилятор использует принцип ***разрешения перегрузки***, чтобы определить, какой из методов следует вызвать.</span><span class="sxs-lookup"><span data-stu-id="2685c-567">When compiling an invocation of an overloaded method, the compiler uses ***overload resolution*** to determine the specific method to invoke.</span></span> <span data-ttu-id="2685c-568">Разрешение перегрузки выбирает из методов тот, который лучше всего соответствует предоставленным аргументам, или возвращает ошибку, если не удается выбрать конкретный подходящий метод.</span><span class="sxs-lookup"><span data-stu-id="2685c-568">Overload resolution finds the one method that best matches the arguments or reports an error if no single best match can be found.</span></span> <span data-ttu-id="2685c-569">В следующем примере показано, как работает разрешение перегрузки.</span><span class="sxs-lookup"><span data-stu-id="2685c-569">The following example shows overload resolution in effect.</span></span> <span data-ttu-id="2685c-570">Комментарий к каждому вызову метода `Main` подсказывает, какой из методов будет вызван для этой строки.</span><span class="sxs-lookup"><span data-stu-id="2685c-570">The comment for each invocation in the `Main` method shows which method is actually invoked.</span></span>

```csharp
class Test
{
    static void F() {
        Console.WriteLine("F()");
    }

    static void F(object x) {
        Console.WriteLine("F(object)");
    }

    static void F(int x) {
        Console.WriteLine("F(int)");
    }

    static void F(double x) {
        Console.WriteLine("F(double)");
    }

    static void F<T>(T x) {
        Console.WriteLine("F<T>(T)");
    }

    static void F(double x, double y) {
        Console.WriteLine("F(double, double)");
    }

    static void Main() {
        F();                 // Invokes F()
        F(1);                // Invokes F(int)
        F(1.0);              // Invokes F(double)
        F("abc");            // Invokes F(object)
        F((double)1);        // Invokes F(double)
        F((object)1);        // Invokes F(object)
        F<int>(1);           // Invokes F<T>(T)
        F(1, 1);             // Invokes F(double, double)
    }
}
```
<span data-ttu-id="2685c-571">Как видно из этого примера, вы всегда можете выбрать конкретный метод, явным образом приведя типы аргументов к соответствующим типам параметров, и (или) явно предоставив аргументы нужного типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-571">As shown by the example, a particular method can always be selected by explicitly casting the arguments to the exact parameter types and/or explicitly supplying type arguments.</span></span>

### <a name="other-function-members"></a><span data-ttu-id="2685c-572">Другие функции-члены</span><span class="sxs-lookup"><span data-stu-id="2685c-572">Other function members</span></span>

<span data-ttu-id="2685c-573">Все члены класса, содержащие исполняемый код, совокупно называются ***функции-члены***.</span><span class="sxs-lookup"><span data-stu-id="2685c-573">Members that contain executable code are collectively known as the ***function members*** of a class.</span></span> <span data-ttu-id="2685c-574">В предыдущем разделе мы рассмотрели основные варианты методов, используемых как функции-члены.</span><span class="sxs-lookup"><span data-stu-id="2685c-574">The preceding section describes methods, which are the primary kind of function members.</span></span> <span data-ttu-id="2685c-575">В этом разделе описываются другие типы функций-членов, поддерживающиеся C#: конструкторы, свойства, индексаторы, события, операторы и деструкторы.</span><span class="sxs-lookup"><span data-stu-id="2685c-575">This section describes the other kinds of function members supported by C#: constructors, properties, indexers, events, operators, and destructors.</span></span>

<span data-ttu-id="2685c-576">В следующем коде показано универсальный класс с именем `List<T>`, который реализует расширяемый список объектов.</span><span class="sxs-lookup"><span data-stu-id="2685c-576">The following code shows a generic class called `List<T>`, which implements a growable list of objects.</span></span> <span data-ttu-id="2685c-577">Этот класс содержит несколько наиболее распространенных типов функций-членов.</span><span class="sxs-lookup"><span data-stu-id="2685c-577">The class contains several examples of the most common kinds of function members.</span></span>


```csharp
public class List<T> {
    // Constant...
    const int defaultCapacity = 4;

    // Fields...
    T[] items;
    int count;

    // Constructors...
    public List(int capacity = defaultCapacity) {
        items = new T[capacity];
    }

    // Properties...
    public int Count {
        get { return count; }
    }
    public int Capacity {
        get {
            return items.Length;
        }
        set {
            if (value < count) value = count;
            if (value != items.Length) {
                T[] newItems = new T[value];
                Array.Copy(items, 0, newItems, 0, count);
                items = newItems;
            }
        }
    }

    // Indexer...
    public T this[int index] {
        get {
            return items[index];
        }
        set {
            items[index] = value;
            OnChanged();
        }
    }

    // Methods...
    public void Add(T item) {
        if (count == Capacity) Capacity = count * 2;
        items[count] = item;
        count++;
        OnChanged();
    }
    protected virtual void OnChanged() {
        if (Changed != null) Changed(this, EventArgs.Empty);
    }
    public override bool Equals(object other) {
        return Equals(this, other as List<T>);
    }
    static bool Equals(List<T> a, List<T> b) {
        if (a == null) return b == null;
        if (b == null || a.count != b.count) return false;
        for (int i = 0; i < a.count; i++) {
            if (!object.Equals(a.items[i], b.items[i])) {
                return false;
            }
        }
        return true;
    }

    // Event...
    public event EventHandler Changed;

    // Operators...
    public static bool operator ==(List<T> a, List<T> b) {
        return Equals(a, b);
    }
    public static bool operator !=(List<T> a, List<T> b) {
        return !Equals(a, b);
    }
}
```

#### <a name="constructors"></a><span data-ttu-id="2685c-578">Конструкторы</span><span class="sxs-lookup"><span data-stu-id="2685c-578">Constructors</span></span>

<span data-ttu-id="2685c-579">C# поддерживает конструкторы экземпляров и статические конструкторы.</span><span class="sxs-lookup"><span data-stu-id="2685c-579">C# supports both instance and static constructors.</span></span> <span data-ttu-id="2685c-580">***Конструктор экземпляра*** является членом, который реализует действия для инициализации нового экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-580">An ***instance constructor*** is a member that implements the actions required to initialize an instance of a class.</span></span> <span data-ttu-id="2685c-581">***Статический конструктор*** является членом, который реализует действия для инициализации самого класса при первоначальной его загрузке.</span><span class="sxs-lookup"><span data-stu-id="2685c-581">A ***static constructor*** is a member that implements the actions required to initialize a class itself when it is first loaded.</span></span>

<span data-ttu-id="2685c-582">Конструктор объявляется в виде метода без возвращаемого типа, имя которого совпадает с именем класса, в котором он определен.</span><span class="sxs-lookup"><span data-stu-id="2685c-582">A constructor is declared like a method with no return type and the same name as the containing class.</span></span> <span data-ttu-id="2685c-583">Если объявление конструктора содержит `static` модификатор, он объявляет статический конструктор.</span><span class="sxs-lookup"><span data-stu-id="2685c-583">If a constructor declaration includes a `static` modifier, it declares a static constructor.</span></span> <span data-ttu-id="2685c-584">В противном случае это объявление считается конструктором экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2685c-584">Otherwise, it declares an instance constructor.</span></span>

<span data-ttu-id="2685c-585">Конструкторы экземпляров могут быть перегружены.</span><span class="sxs-lookup"><span data-stu-id="2685c-585">Instance constructors can be overloaded.</span></span> <span data-ttu-id="2685c-586">Например, класс `List<T>
` объявляет два конструктора экземпляра: один без параметров и один с параметром `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-586">For example, the `List<T>
` class declares two instance constructors, one with no parameters and one that takes an `int` parameter.</span></span> <span data-ttu-id="2685c-587">Конструкторы экземпляров вызываются с помощью оператора `new`.</span><span class="sxs-lookup"><span data-stu-id="2685c-587">Instance constructors are invoked using the `new` operator.</span></span> <span data-ttu-id="2685c-588">Следующий пример кода выделяет два `List<string>
` экземпляров с помощью каждого из конструкторов `List` класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-588">The following statements allocate two `List<string>
` instances using each of the constructors of the `List` class.</span></span>

```csharp
List<string> list1 = new List<string>();
List<string> list2 = new List<string>(10);
```
<span data-ttu-id="2685c-589">В отличие от других членов конструкторы экземпляров не наследуются, и класс не имеет конструкторов экземпляров, кроме объявленных в самом этом классе.</span><span class="sxs-lookup"><span data-stu-id="2685c-589">Unlike other members, instance constructors are not inherited, and a class has no instance constructors other than those actually declared in the class.</span></span> <span data-ttu-id="2685c-590">Если в классе не объявлен конструктор экземпляра, для него автоматически создается пустой конструктор без параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-590">If no instance constructor is supplied for a class, then an empty one with no parameters is automatically provided.</span></span>

#### <a name="properties"></a><span data-ttu-id="2685c-591">Свойства</span><span class="sxs-lookup"><span data-stu-id="2685c-591">Properties</span></span>

<span data-ttu-id="2685c-592">***Свойства*** естественным образом дополняют поля.</span><span class="sxs-lookup"><span data-stu-id="2685c-592">***Properties*** are a natural extension of fields.</span></span> <span data-ttu-id="2685c-593">И те, и другие являются именованными членами со связанными типами, и для доступа к ним используется одинаковый синтаксис.</span><span class="sxs-lookup"><span data-stu-id="2685c-593">Both are named members with associated types, and the syntax for accessing fields and properties is the same.</span></span> <span data-ttu-id="2685c-594">Однако свойства, в отличие от полей, не указывают места хранения.</span><span class="sxs-lookup"><span data-stu-id="2685c-594">However, unlike fields, properties do not denote storage locations.</span></span> <span data-ttu-id="2685c-595">Вместо этого свойства содержат ***методы доступа***, в которых описаны инструкции для выполнения при чтении или записи значений.</span><span class="sxs-lookup"><span data-stu-id="2685c-595">Instead, properties have ***accessors*** that specify the statements to be executed when their values are read or written.</span></span>

<span data-ttu-id="2685c-596">Свойство объявлено как поле, за исключением того, что объявление заканчивается `get` метода доступа и/или `set` метод доступа, записанных между разделителями `{` и `}` вместо заканчиваются точкой с запятой.</span><span class="sxs-lookup"><span data-stu-id="2685c-596">A property is declared like a field, except that the declaration ends with a `get` accessor and/or a `set` accessor written between the delimiters `{` and `}` instead of ending in a semicolon.</span></span> <span data-ttu-id="2685c-597">Свойство, имеющее оба `get` метода доступа и `set` метод доступа является ***чтения и записи свойство***, свойство, имеющее только `get` метод доступа является ***свойство только для чтения***и свойство, имеющее только `set` метод доступа является ***свойство, доступное только для записи***.</span><span class="sxs-lookup"><span data-stu-id="2685c-597">A property that has both a `get` accessor and a `set` accessor is a ***read-write property***, a property that has only a `get` accessor is a ***read-only property***, and a property that has only a `set` accessor is a ***write-only property***.</span></span>

<span data-ttu-id="2685c-598">Объект `get` метод доступа соответствует оформляется как метод с возвращаемым значением типа свойства.</span><span class="sxs-lookup"><span data-stu-id="2685c-598">A `get` accessor corresponds to a parameterless method with a return value of the property type.</span></span> <span data-ttu-id="2685c-599">За исключением случаев, целевым объектом назначения, при ссылке на свойство в выражении, `get` для вычисления значения свойства вызывается метод доступа свойства.</span><span class="sxs-lookup"><span data-stu-id="2685c-599">Except as the target of an assignment, when a property is referenced in an expression, the `get` accessor of the property is invoked to compute the value of the property.</span></span>

<span data-ttu-id="2685c-600">Объект `set` доступа соответствует методу с одним параметром с именем `value` и без возвращаемого типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-600">A `set` accessor corresponds to a method with a single parameter named `value` and no return type.</span></span> <span data-ttu-id="2685c-601">Если ссылка на свойство как целевым объектом назначения или как операнд `++` или `--`, `set` вызывается метод доступа с аргументом, содержащим новое значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-601">When a property is referenced as the target of an assignment or as the operand of `++` or `--`, the `set` accessor is invoked with an argument that provides the new value.</span></span>

<span data-ttu-id="2685c-602">`List<T>
` Класс объявляет два свойства `Count` и `Capacity`, которые являются только для чтения и чтения и записи, соответственно.</span><span class="sxs-lookup"><span data-stu-id="2685c-602">The `List<T>
` class declares two properties, `Count` and `Capacity`, which are read-only and read-write, respectively.</span></span> <span data-ttu-id="2685c-603">Образец использования этих свойств приведен ниже.</span><span class="sxs-lookup"><span data-stu-id="2685c-603">The following is an example of use of these properties.</span></span>

```csharp
List<string> names = new List<string>();
names.Capacity = 100;            // Invokes set accessor
int i = names.Count;             // Invokes get accessor
int j = names.Capacity;          // Invokes get accessor
```
<span data-ttu-id="2685c-604">Как и в отношении полей и методов, C# поддерживает свойства экземпляра и статические свойства.</span><span class="sxs-lookup"><span data-stu-id="2685c-604">Similar to fields and methods, C# supports both instance properties and static properties.</span></span> <span data-ttu-id="2685c-605">Статические свойства объявляются с `static` модификатор, а свойства экземпляра объявлены без него.</span><span class="sxs-lookup"><span data-stu-id="2685c-605">Static properties are declared with the `static` modifier, and instance properties are declared without it.</span></span>

<span data-ttu-id="2685c-606">Акцессоры свойства могут быть виртуальными.</span><span class="sxs-lookup"><span data-stu-id="2685c-606">The accessor(s) of a property can be virtual.</span></span> <span data-ttu-id="2685c-607">Если объявление свойства содержит модификатор `virtual`, `abstract` или `override`, этот модификатор применяется к акцессорам свойства.</span><span class="sxs-lookup"><span data-stu-id="2685c-607">When a property declaration includes a `virtual`, `abstract`, or `override` modifier, it applies to the accessor(s) of the property.</span></span>

#### <a name="indexers"></a><span data-ttu-id="2685c-608">Индексаторы</span><span class="sxs-lookup"><span data-stu-id="2685c-608">Indexers</span></span>

<span data-ttu-id="2685c-609">***Индексатор*** является членом, позволяющим индексировать объекты так, как будто они включены в массив.</span><span class="sxs-lookup"><span data-stu-id="2685c-609">An ***indexer*** is a member that enables objects to be indexed in the same way as an array.</span></span> <span data-ttu-id="2685c-610">Индексатор объявляется как свойство, за исключением того, что имя члена — `this` следуют список параметров, записанных между разделителями `[` и `]`.</span><span class="sxs-lookup"><span data-stu-id="2685c-610">An indexer is declared like a property except that the name of the member is `this` followed by a parameter list written between the delimiters `[` and `]`.</span></span> <span data-ttu-id="2685c-611">Эти параметры доступны в акцессорах индексатора.</span><span class="sxs-lookup"><span data-stu-id="2685c-611">The parameters are available in the accessor(s) of the indexer.</span></span> <span data-ttu-id="2685c-612">Как и свойства, можно объявить индексаторы для чтения и записи, только для чтения или только для записи. Кроме того, поддерживаются виртуальные акцессоры индексатора.</span><span class="sxs-lookup"><span data-stu-id="2685c-612">Similar to properties, indexers can be read-write, read-only, and write-only, and the accessor(s) of an indexer can be virtual.</span></span>

<span data-ttu-id="2685c-613">Класс `List` объявляет один индексатор для чтения и записи, который принимает параметр `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-613">The `List` class declares a single read-write indexer that takes an `int` parameter.</span></span> <span data-ttu-id="2685c-614">Индексатор позволяет индексировать экземпляры `List` значениями с типом `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-614">The indexer makes it possible to index `List` instances with `int` values.</span></span> <span data-ttu-id="2685c-615">Пример</span><span class="sxs-lookup"><span data-stu-id="2685c-615">For example</span></span>

```csharp
List<string> names = new List<string>();
names.Add("Liz");
names.Add("Martha");
names.Add("Beth");
for (int i = 0; i < names.Count; i++) {
    string s = names[i];
    names[i] = s.ToUpper();
}
```
<span data-ttu-id="2685c-616">Индексаторы можно перегружать, то есть в одном классе можно объявить несколько индексаторов, если у них различаются количество или типы параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-616">Indexers can be overloaded, meaning that a class can declare multiple indexers as long as the number or types of their parameters differ.</span></span>

#### <a name="events"></a><span data-ttu-id="2685c-617">События</span><span class="sxs-lookup"><span data-stu-id="2685c-617">Events</span></span>

<span data-ttu-id="2685c-618">***Событие*** — это член, с помощью которого класс или объект предоставляют уведомления.</span><span class="sxs-lookup"><span data-stu-id="2685c-618">An ***event*** is a member that enables a class or object to provide notifications.</span></span> <span data-ttu-id="2685c-619">Событие объявляется как поле, за исключением того, что объявление включает `event` ключевое слово и тип должен быть типом делегата.</span><span class="sxs-lookup"><span data-stu-id="2685c-619">An event is declared like a field except that the declaration includes an `event` keyword and the type must be a delegate type.</span></span>

<span data-ttu-id="2685c-620">В классе, который объявляет член события, это событие действует, как обычное поле с типом делегата (если это событие не является абстрактным и не объявляет акцессоры).</span><span class="sxs-lookup"><span data-stu-id="2685c-620">Within a class that declares an event member, the event behaves just like a field of a delegate type (provided the event is not abstract and does not declare accessors).</span></span> <span data-ttu-id="2685c-621">Это поле хранит ссылку на делегат, который представляет добавленные к событию обработчики событий.</span><span class="sxs-lookup"><span data-stu-id="2685c-621">The field stores a reference to a delegate that represents the event handlers that have been added to the event.</span></span> <span data-ttu-id="2685c-622">Если обработчики событий отсутствуют, то поле выравнивается `null`.</span><span class="sxs-lookup"><span data-stu-id="2685c-622">If no event handles are present, the field is `null`.</span></span>

<span data-ttu-id="2685c-623">Класс `List<T>
` объявляет один член события с именем `Changed`, который обрабатывает добавление нового элемента.</span><span class="sxs-lookup"><span data-stu-id="2685c-623">The `List<T>
` class declares a single event member called `Changed`, which indicates that a new item has been added to the list.</span></span> <span data-ttu-id="2685c-624">`Changed` Событие `OnChanged` виртуальный метод, который сначала проверяет, является ли событие `null` (это означает, что обработчики не присутствуют).</span><span class="sxs-lookup"><span data-stu-id="2685c-624">The `Changed` event is raised by the `OnChanged` virtual method, which first checks whether the event is `null` (meaning that no handlers are present).</span></span> <span data-ttu-id="2685c-625">Концепция создания события в точности соответствует вызову делегата, представленного этим событием. Это позволяет обойтись без особой языковой конструкции для создания событий.</span><span class="sxs-lookup"><span data-stu-id="2685c-625">The notion of raising an event is precisely equivalent to invoking the delegate represented by the event—thus, there are no special language constructs for raising events.</span></span>

<span data-ttu-id="2685c-626">Клиенты реагируют на события посредством ***обработчиков событий***.</span><span class="sxs-lookup"><span data-stu-id="2685c-626">Clients react to events through ***event handlers***.</span></span> <span data-ttu-id="2685c-627">Обработчики событий можно подключать с помощью оператора `+=` и удалять с помощью оператора `-=`.</span><span class="sxs-lookup"><span data-stu-id="2685c-627">Event handlers are attached using the `+=` operator and removed using the `-=` operator.</span></span> <span data-ttu-id="2685c-628">Следующий пример кода подключает обработчик события `Changed` к событию `List<string>
`.</span><span class="sxs-lookup"><span data-stu-id="2685c-628">The following example attaches an event handler to the `Changed` event of a `List<string>
`.</span></span>

```csharp
using System;

class Test
{
    static int changeCount;

    static void ListChanged(object sender, EventArgs e) {
        changeCount++;
    }

    static void Main() {
        List<string> names = new List<string>();
        names.Changed += new EventHandler(ListChanged);
        names.Add("Liz");
        names.Add("Martha");
        names.Add("Beth");
        Console.WriteLine(changeCount);        // Outputs "3"
    }
}
```
<span data-ttu-id="2685c-629">Для более сложных сценариев, требующих контроля над базовым хранилищем события, в объявлении события можно явным образом предоставить акцессоры `add` и `remove`. Они будут действовать примерно так же, как акцессор `set` для свойства.</span><span class="sxs-lookup"><span data-stu-id="2685c-629">For advanced scenarios where control of the underlying storage of an event is desired, an event declaration can explicitly provide `add` and `remove` accessors, which are somewhat similar to the `set` accessor of a property.</span></span>

#### <a name="operators"></a><span data-ttu-id="2685c-630">Операторы</span><span class="sxs-lookup"><span data-stu-id="2685c-630">Operators</span></span>

<span data-ttu-id="2685c-631">***Оператор*** является членом, который определяет правила применения определенного выражения к экземплярам класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-631">An ***operator*** is a member that defines the meaning of applying a particular expression operator to instances of a class.</span></span> <span data-ttu-id="2685c-632">Вы можете определить операторы трех типов: унарные операторы, двоичные операторы и операторы преобразования.</span><span class="sxs-lookup"><span data-stu-id="2685c-632">Three kinds of operators can be defined: unary operators, binary operators, and conversion operators.</span></span> <span data-ttu-id="2685c-633">Все операторы объявляются с модификаторами `public` и `static`.</span><span class="sxs-lookup"><span data-stu-id="2685c-633">All operators must be declared as `public` and `static`.</span></span>

<span data-ttu-id="2685c-634">Класс `List<T>
` объявляет два оператора: `operator==` и `operator!=`. Это позволяет определить новое значение для выражений, которые применяют эти операторы к экземплярам `List`.</span><span class="sxs-lookup"><span data-stu-id="2685c-634">The `List<T>
` class declares two operators, `operator==` and `operator!=`, and thus gives new meaning to expressions that apply those operators to `List` instances.</span></span> <span data-ttu-id="2685c-635">В частности, эти операторы определяют равенство двух `List<T>
` экземпляров проверяется путем сравнения всех содержащихся в них объектов с помощью их `Equals` методы.</span><span class="sxs-lookup"><span data-stu-id="2685c-635">Specifically, the operators define equality of two `List<T>
` instances as comparing each of the contained objects using their `Equals` methods.</span></span> <span data-ttu-id="2685c-636">Следующий пример кода использует оператор `==` для сравнения двух экземпляров `List<int>
`.</span><span class="sxs-lookup"><span data-stu-id="2685c-636">The following example uses the `==` operator to compare two `List<int>
` instances.</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        List<int> a = new List<int>();
        a.Add(1);
        a.Add(2);
        List<int> b = new List<int>();
        b.Add(1);
        b.Add(2);
        Console.WriteLine(a == b);        // Outputs "True"
        b.Add(3);
        Console.WriteLine(a == b);        // Outputs "False"
    }
}
```

<span data-ttu-id="2685c-637">Первый `Console.WriteLine` выводит `True`, поскольку два списка содержат одинаковое число объектов с одинаковыми значениями в том же порядке.</span><span class="sxs-lookup"><span data-stu-id="2685c-637">The first `Console.WriteLine` outputs `True` because the two lists contain the same number of objects with the same values in the same order.</span></span> <span data-ttu-id="2685c-638">Если бы в `List<T>
` не было определения `operator==`, первый `Console.WriteLine` возвращал бы `False`, поскольку `a` и `b` указывают на различные экземпляры `List<int>
`.</span><span class="sxs-lookup"><span data-stu-id="2685c-638">Had `List<T>
` not defined `operator==`, the first `Console.WriteLine` would have output `False` because `a` and `b` reference different `List<int>
` instances.</span></span>

#### <a name="destructors"></a><span data-ttu-id="2685c-639">Деструкторы</span><span class="sxs-lookup"><span data-stu-id="2685c-639">Destructors</span></span>

<span data-ttu-id="2685c-640">Объект ***деструктор*** является членом, который реализует действия для уничтожения экземпляра класса.</span><span class="sxs-lookup"><span data-stu-id="2685c-640">A ***destructor*** is a member that implements the actions required to destruct an instance of a class.</span></span> <span data-ttu-id="2685c-641">Деструкторы не могут иметь параметры, они не могут иметь модификаторы доступа и их нельзя вызвать явным образом.</span><span class="sxs-lookup"><span data-stu-id="2685c-641">Destructors cannot have parameters, they cannot have accessibility modifiers, and they cannot be invoked explicitly.</span></span> <span data-ttu-id="2685c-642">Деструктор для экземпляра вызывается автоматически во время сборки мусора.</span><span class="sxs-lookup"><span data-stu-id="2685c-642">The destructor for an instance is invoked automatically during garbage collection.</span></span>

<span data-ttu-id="2685c-643">Сборщик мусора может широкую степень свободы в выборе времени уничтожения объектов и вызова деструкторов.</span><span class="sxs-lookup"><span data-stu-id="2685c-643">The garbage collector is allowed wide latitude in deciding when to collect objects and run destructors.</span></span> <span data-ttu-id="2685c-644">В частности о времени для вызова деструктора не является детерминированным и деструкторы могут выполняться в любом потоке.</span><span class="sxs-lookup"><span data-stu-id="2685c-644">Specifically, the timing of destructor invocations is not deterministic, and destructors may be executed on any thread.</span></span> <span data-ttu-id="2685c-645">Для этих и других причин классы должны реализовывать деструкторы только в том случае, когда невозможны другие решения нет.</span><span class="sxs-lookup"><span data-stu-id="2685c-645">For these and other reasons, classes should implement destructors only when no other solutions are feasible.</span></span>

<span data-ttu-id="2685c-646">Уничтожение объектов лучше контролировать с помощью инструкции `using`.</span><span class="sxs-lookup"><span data-stu-id="2685c-646">The `using` statement provides a better approach to object destruction.</span></span>

## <a name="structs"></a><span data-ttu-id="2685c-647">Структуры</span><span class="sxs-lookup"><span data-stu-id="2685c-647">Structs</span></span>

<span data-ttu-id="2685c-648">Как и классы, ***структуры*** — это сущности для хранения данных, которые могут содержать данные-члены и функции-члены. Но в отличие от классов, структуры являются типами значений и для них не выделяется память из кучи.</span><span class="sxs-lookup"><span data-stu-id="2685c-648">Like classes, ***structs*** are data structures that can contain data members and function members, but unlike classes, structs are value types and do not require heap allocation.</span></span> <span data-ttu-id="2685c-649">Переменная типа структура напрямую хранит все свои данные, а переменная типа класс хранит ссылку на динамически выделяемый объект.</span><span class="sxs-lookup"><span data-stu-id="2685c-649">A variable of a struct type directly stores the data of the struct, whereas a variable of a class type stores a reference to a dynamically allocated object.</span></span> <span data-ttu-id="2685c-650">Типы структуры не поддерживают определяемое пользователем наследование, и все типы структуры неявно наследуют от типа `object`.</span><span class="sxs-lookup"><span data-stu-id="2685c-650">Struct types do not support user-specified inheritance, and all struct types implicitly inherit from type `object`.</span></span>

<span data-ttu-id="2685c-651">Структуры особенно удобны для небольших структур данных, имеющих семантику значений.</span><span class="sxs-lookup"><span data-stu-id="2685c-651">Structs are particularly useful for small data structures that have value semantics.</span></span> <span data-ttu-id="2685c-652">Хорошими примерами структур можно считать комплексные числа, точки в системе координат или словари с парами ключ-значение.</span><span class="sxs-lookup"><span data-stu-id="2685c-652">Complex numbers, points in a coordinate system, or key-value pairs in a dictionary are all good examples of structs.</span></span> <span data-ttu-id="2685c-653">Если использовать структуры вместо классов для небольших структур данных, можно существенно снизить количество операций по выделению памяти в приложении.</span><span class="sxs-lookup"><span data-stu-id="2685c-653">The use of structs rather than classes for small data structures can make a large difference in the number of memory allocations an application performs.</span></span> <span data-ttu-id="2685c-654">Например, следующая программа создает и инициализирует массив из 100 точек.</span><span class="sxs-lookup"><span data-stu-id="2685c-654">For example, the following program creates and initializes an array of 100 points.</span></span> <span data-ttu-id="2685c-655">Если реализовать `Point` как класс, создаются экземпляры для 101 отдельных объектов — один для массива и еще 100 для его элементов.</span><span class="sxs-lookup"><span data-stu-id="2685c-655">With `Point` implemented as a class, 101 separate objects are instantiated—one for the array and one each for the 100 elements.</span></span>

```csharp
class Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}

class Test
{
    static void Main() {
        Point[] points = new Point[100];
        for (int i = 0; i < 100; i++) points[i] = new Point(i, i);
    }
}
```
<span data-ttu-id="2685c-656">Другой вариант — реализовать `Point` структуры.</span><span class="sxs-lookup"><span data-stu-id="2685c-656">An alternative is to make `Point` a struct.</span></span>

```csharp
struct Point
{
    public int x, y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```
<span data-ttu-id="2685c-657">Теперь создается всего один объект (для массива), а экземпляры `Point` хранятся в стеке массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-657">Now, only one object is instantiated—the one for the array—and the `Point` instances are stored in-line in the array.</span></span>

<span data-ttu-id="2685c-658">Конструктор структур вызывается оператором `new`, но это не приводит к выделению дополнительной памяти.</span><span class="sxs-lookup"><span data-stu-id="2685c-658">Struct constructors are invoked with the `new` operator, but that does not imply that memory is being allocated.</span></span> <span data-ttu-id="2685c-659">Вместо того, чтобы динамически выделять объект и возвращать ссылку на него, конструктор структуры возвращает само значение структуры (обычно сохраняя его во временном расположении в стеке), и затем это значение копируется туда, где оно нужно.</span><span class="sxs-lookup"><span data-stu-id="2685c-659">Instead of dynamically allocating an object and returning a reference to it, a struct constructor simply returns the struct value itself (typically in a temporary location on the stack), and this value is then copied as necessary.</span></span>

<span data-ttu-id="2685c-660">При использовании классов две переменные могут ссылаться на один и тот же объект, поэтому может случиться так, что операции над одной переменной затронут объект, на который ссылается другая переменная.</span><span class="sxs-lookup"><span data-stu-id="2685c-660">With classes, it is possible for two variables to reference the same object and thus possible for operations on one variable to affect the object referenced by the other variable.</span></span> <span data-ttu-id="2685c-661">При использовании структур каждая переменная имеет собственную копию данных, и операции над одной переменной не могут затрагивать другую.</span><span class="sxs-lookup"><span data-stu-id="2685c-661">With structs, the variables each have their own copy of the data, and it is not possible for operations on one to affect the other.</span></span> <span data-ttu-id="2685c-662">Например, выходные данные в следующем фрагменте кода зависит от того `Point` это класс или структура.</span><span class="sxs-lookup"><span data-stu-id="2685c-662">For example, the output produced by the following code fragment depends on whether `Point` is a class or a struct.</span></span>

```csharp
Point a = new Point(10, 10);
Point b = a;
a.x = 20;
Console.WriteLine(b.x);
```
<span data-ttu-id="2685c-663">Если `Point` — это класс, выводится `20` поскольку `a` и `b` ссылаются на один объект.</span><span class="sxs-lookup"><span data-stu-id="2685c-663">If `Point` is a class, the output is `20` because `a` and `b` reference the same object.</span></span> <span data-ttu-id="2685c-664">Если `Point` является структурой, возвращается значение `10` так как назначение `a` для `b` создает копию значения, и это значение не изменяется при последующем присваивании в `a.x`.</span><span class="sxs-lookup"><span data-stu-id="2685c-664">If `Point` is a struct, the output is `10` because the assignment of `a` to `b` creates a copy of the value, and this copy is unaffected by the subsequent assignment to `a.x`.</span></span>

<span data-ttu-id="2685c-665">Предыдущий пример демонстрирует два ограничения, действующие для структур.</span><span class="sxs-lookup"><span data-stu-id="2685c-665">The previous example highlights two of the limitations of structs.</span></span> <span data-ttu-id="2685c-666">Во-первых, копирование структуры целиком обычно менее эффективно, чем копирование ссылки на объект, поэтому присваивание и передача в качестве параметра потребует больше затрат для структур, чем для ссылочных типов.</span><span class="sxs-lookup"><span data-stu-id="2685c-666">First, copying an entire struct is typically less efficient than copying an object reference, so assignment and value parameter passing can be more expensive with structs than with reference types.</span></span> <span data-ttu-id="2685c-667">Во-вторых, вы не можете создавать ссылки на структуры (за исключением параметров `ref` и `out`), что в некоторых ситуациях мешает их применять.</span><span class="sxs-lookup"><span data-stu-id="2685c-667">Second, except for `ref` and `out` parameters, it is not possible to create references to structs, which rules out their usage in a number of situations.</span></span>

## <a name="arrays"></a><span data-ttu-id="2685c-668">Массивы</span><span class="sxs-lookup"><span data-stu-id="2685c-668">Arrays</span></span>

<span data-ttu-id="2685c-669">***Массив*** — это структура данных, содержащая несколько переменных, доступ к которым осуществляется по вычисляемым индексам.</span><span class="sxs-lookup"><span data-stu-id="2685c-669">An ***array*** is a data structure that contains a number of variables that are accessed through computed indices.</span></span> <span data-ttu-id="2685c-670">Содержащиеся в массиве переменные именуются ***элементами*** этого массива. Все они имеют одинаковый тип, который называется ***типом элементов*** массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-670">The variables contained in an array, also called the ***elements*** of the array, are all of the same type, and this type is called the ***element type*** of the array.</span></span>

<span data-ttu-id="2685c-671">Сами массивы имеют ссылочный тип, и объявление переменной массива только выделяет память для ссылки на экземпляр массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-671">Array types are reference types, and the declaration of an array variable simply sets aside space for a reference to an array instance.</span></span> <span data-ttu-id="2685c-672">Фактические экземпляры массива создаются динамически во время выполнения с помощью `new` оператор.</span><span class="sxs-lookup"><span data-stu-id="2685c-672">Actual array instances are created dynamically at run-time using the `new` operator.</span></span> <span data-ttu-id="2685c-673">`new` Операции указывает ***длина*** нового экземпляра массива, которая остается неизменной в течение времени существования экземпляра.</span><span class="sxs-lookup"><span data-stu-id="2685c-673">The `new` operation specifies the ***length*** of the new array instance, which is then fixed for the lifetime of the instance.</span></span> <span data-ttu-id="2685c-674">Элементы массива имеют индексы в диапазоне от `0` до `Length - 1`.</span><span class="sxs-lookup"><span data-stu-id="2685c-674">The indices of the elements of an array range from `0` to `Length - 1`.</span></span> <span data-ttu-id="2685c-675">Оператор `new` автоматически инициализирует все элементы массива значением по умолчанию. Например, для всех числовых типов устанавливается нулевое значение, а для всех ссылочных типов — значение `null`.</span><span class="sxs-lookup"><span data-stu-id="2685c-675">The `new` operator automatically initializes the elements of an array to their default value, which, for example, is zero for all numeric types and `null` for all reference types.</span></span>

<span data-ttu-id="2685c-676">Следующий пример кода создает массив из `int` элементов, затем инициализирует этот массив и выводит содержимое массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-676">The following example creates an array of `int` elements, initializes the array, and prints out the contents of the array.</span></span>

```csharp
using System;

class Test
{
    static void Main() {
        int[] a = new int[10];
        for (int i = 0; i < a.Length; i++) {
            a[i] = i * i;
        }
        for (int i = 0; i < a.Length; i++) {
            Console.WriteLine("a[{0}] = {1}", i, a[i]);
        }
    }
}
```
<span data-ttu-id="2685c-677">Этот пример создает и использует ***одномерный массив***.</span><span class="sxs-lookup"><span data-stu-id="2685c-677">This example creates and operates on a ***single-dimensional array***.</span></span> <span data-ttu-id="2685c-678">Кроме этого, C# поддерживает ***многомерные массивы***.</span><span class="sxs-lookup"><span data-stu-id="2685c-678">C# also supports ***multi-dimensional arrays***.</span></span> <span data-ttu-id="2685c-679">Число измерений массива, которое именуется ***рангом*** для типа массива, всегда на единицу больше числа запятых, включенных в квадратные скобки типа массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-679">The number of dimensions of an array type, also known as the ***rank*** of the array type, is one plus the number of commas written between the square brackets of the array type.</span></span> <span data-ttu-id="2685c-680">Следующий пример создает одномерный, двухмерный и трехмерный массив.</span><span class="sxs-lookup"><span data-stu-id="2685c-680">The following example allocates a one-dimensional, a two-dimensional, and a three-dimensional array.</span></span>

```csharp
int[] a1 = new int[10];
int[,] a2 = new int[10, 5];
int[,,] a3 = new int[10, 5, 2];
```
<span data-ttu-id="2685c-681">Массив `a1` содержит 10 элементов, массив `a2` — 50 элементов (10 × 5), и наконец `a3` содержит 100 элементов (10 × 5 × 2).</span><span class="sxs-lookup"><span data-stu-id="2685c-681">The `a1` array contains 10 elements, the `a2` array contains 50 (10 × 5) elements, and the `a3` array contains 100 (10 × 5 × 2) elements.</span></span>

<span data-ttu-id="2685c-682">Элементы массива могут иметь любой тип, в том числе тип массива.</span><span class="sxs-lookup"><span data-stu-id="2685c-682">The element type of an array can be any type, including an array type.</span></span> <span data-ttu-id="2685c-683">Массив с элементами типа массива иногда называют ***ступенчатым массивом***, поскольку элементы такого массива не обязаны иметь одинаковую длину.</span><span class="sxs-lookup"><span data-stu-id="2685c-683">An array with elements of an array type is sometimes called a ***jagged array*** because the lengths of the element arrays do not all have to be the same.</span></span> <span data-ttu-id="2685c-684">Следующий пример создает массив массивов `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-684">The following example allocates an array of arrays of `int`:</span></span>

```csharp
int[][] a = new int[3][];
a[0] = new int[10];
a[1] = new int[5];
a[2] = new int[20];
```
<span data-ttu-id="2685c-685">В первой строке создается массив с тремя элементами, каждый из которых имеет тип `int[]` и начальное значение `null`.</span><span class="sxs-lookup"><span data-stu-id="2685c-685">The first line creates an array with three elements, each of type `int[]` and each with an initial value of `null`.</span></span> <span data-ttu-id="2685c-686">В последующих строках эти три элемента инициализируются ссылками на отдельные экземпляры массивов различной длины.</span><span class="sxs-lookup"><span data-stu-id="2685c-686">The subsequent lines then initialize the three elements with references to individual array instances of varying lengths.</span></span>

<span data-ttu-id="2685c-687">`new` Оператор позволяет задать начальные значения элементов массива с помощью ***инициализатор массива***, который является список выражений, записанных между разделителями `{` и `}`.</span><span class="sxs-lookup"><span data-stu-id="2685c-687">The `new` operator permits the initial values of the array elements to be specified using an ***array initializer***, which is a list of expressions written between the delimiters `{` and `}`.</span></span> <span data-ttu-id="2685c-688">Следующий пример создает и инициализирует массив `int[]` с тремя элементами.</span><span class="sxs-lookup"><span data-stu-id="2685c-688">The following example allocates and initializes an `int[]` with three elements.</span></span>

```csharp
int[] a = new int[] {1, 2, 3};
```
<span data-ttu-id="2685c-689">Обратите внимание, что длина массива определяется количество выражений между `{` и `}`.</span><span class="sxs-lookup"><span data-stu-id="2685c-689">Note that the length of the array is inferred from the number of expressions between `{` and `}`.</span></span> <span data-ttu-id="2685c-690">Локальные объявления переменных и полей можно сократить, поскольку тип массива не обязательно объявлять повторно.</span><span class="sxs-lookup"><span data-stu-id="2685c-690">Local variable and field declarations can be shortened further such that the array type does not have to be restated.</span></span>

```csharp
int[] a = {1, 2, 3};
```
<span data-ttu-id="2685c-691">Оба указанных выше примера дают результат, эквивалентный такому объявлению.</span><span class="sxs-lookup"><span data-stu-id="2685c-691">Both of the previous examples are equivalent to the following:</span></span>

```csharp
int[] t = new int[3];
t[0] = 1;
t[1] = 2;
t[2] = 3;
int[] a = t;
```
## <a name="interfaces"></a><span data-ttu-id="2685c-692">интерфейсов,</span><span class="sxs-lookup"><span data-stu-id="2685c-692">Interfaces</span></span>

<span data-ttu-id="2685c-693">***Интерфейс*** определяет контракт, который может быть реализован классами и структурами.</span><span class="sxs-lookup"><span data-stu-id="2685c-693">An ***interface*** defines a contract that can be implemented by classes and structs.</span></span> <span data-ttu-id="2685c-694">Интерфейс может содержать методы, свойства, события и индексаторы.</span><span class="sxs-lookup"><span data-stu-id="2685c-694">An interface can contain methods, properties, events, and indexers.</span></span> <span data-ttu-id="2685c-695">Интерфейс не предоставляет реализацию членов, которые в нем определены. Он лишь перечисляет члены, которые должны быть определены в классах или структурах, реализующих этот интерфейс.</span><span class="sxs-lookup"><span data-stu-id="2685c-695">An interface does not provide implementations of the members it defines—it merely specifies the members that must be supplied by classes or structs that implement the interface.</span></span>

<span data-ttu-id="2685c-696">Интерфейсы могут применять ***множественное наследование***.</span><span class="sxs-lookup"><span data-stu-id="2685c-696">Interfaces may employ ***multiple inheritance***.</span></span> <span data-ttu-id="2685c-697">В следующем примере интерфейс `IComboBox` наследует одновременно от `ITextBox` и `IListBox`.</span><span class="sxs-lookup"><span data-stu-id="2685c-697">In the following example, the interface `IComboBox` inherits from both `ITextBox` and `IListBox`.</span></span>

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
<span data-ttu-id="2685c-698">Классы и структуры могут реализовывать несколько интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="2685c-698">Classes and structs can implement multiple interfaces.</span></span> <span data-ttu-id="2685c-699">В следующем примере класс `EditBox` реализует одновременно `IControl` и `IDataBound`.</span><span class="sxs-lookup"><span data-stu-id="2685c-699">In the following example, the class `EditBox` implements both `IControl` and `IDataBound`.</span></span>

```csharp
interface IDataBound
{
    void Bind(Binder b);
}

public class EditBox: IControl, IDataBound
{
    public void Paint() {...}
    public void Bind(Binder b) {...}
}
```
<span data-ttu-id="2685c-700">Если класс или структура реализует конкретный интерфейс, любой экземпляр этого класса или структуры можно неявно преобразовать в такой тип интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2685c-700">When a class or struct implements a particular interface, instances of that class or struct can be implicitly converted to that interface type.</span></span> <span data-ttu-id="2685c-701">Пример</span><span class="sxs-lookup"><span data-stu-id="2685c-701">For example</span></span>

```csharp
EditBox editBox = new EditBox();
IControl control = editBox;
IDataBound dataBound = editBox;
```
<span data-ttu-id="2685c-702">Если в статическом контексте невозможно достоверно знать, что экземпляр реализует определенный интерфейс, можно использовать динамическое приведение типов.</span><span class="sxs-lookup"><span data-stu-id="2685c-702">In cases where an instance is not statically known to implement a particular interface, dynamic type casts can be used.</span></span> <span data-ttu-id="2685c-703">Например, следующие операторы используют динамическое приведение типов для получения объекта `IControl` и `IDataBound` реализации интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="2685c-703">For example, the following statements use dynamic type casts to obtain an object's `IControl` and `IDataBound` interface implementations.</span></span> <span data-ttu-id="2685c-704">Так как фактический тип объекта является `EditBox`, приведения выполняются успешно.</span><span class="sxs-lookup"><span data-stu-id="2685c-704">Because the actual type of the object is `EditBox`, the casts succeed.</span></span>

```csharp
object obj = new EditBox();
IControl control = (IControl)obj;
IDataBound dataBound = (IDataBound)obj;
```
<span data-ttu-id="2685c-705">В предыдущем `EditBox` класс, `Paint` метода из `IControl` интерфейс и `Bind` метода из `IDataBound` интерфейса реализуются с помощью `public` членов.</span><span class="sxs-lookup"><span data-stu-id="2685c-705">In the previous `EditBox` class, the `Paint` method from the `IControl` interface and the `Bind` method from the `IDataBound` interface are implemented using `public` members.</span></span> <span data-ttu-id="2685c-706">C# также поддерживает ***явные реализации члена интерфейса***, с помощью которого класса или структуры можно избежать создания членов `public`.</span><span class="sxs-lookup"><span data-stu-id="2685c-706">C# also supports ***explicit interface member implementations***, using which the class or struct can avoid making the members `public`.</span></span> <span data-ttu-id="2685c-707">Явная реализация члена интерфейса записывается с использованием полного имени члена интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2685c-707">An explicit interface member implementation is written using the fully qualified interface member name.</span></span> <span data-ttu-id="2685c-708">Например, класс `EditBox` может реализовывать методы `IControl.Paint` и `IDataBound.Bind` с использованием явной реализации членов интерфейса, как показано в следующем примере.</span><span class="sxs-lookup"><span data-stu-id="2685c-708">For example, the `EditBox` class could implement the `IControl.Paint` and `IDataBound.Bind` methods using explicit interface member implementations as follows.</span></span>

```csharp
public class EditBox: IControl, IDataBound
{
    void IControl.Paint() {...}
    void IDataBound.Bind(Binder b) {...}
}
```
<span data-ttu-id="2685c-709">Обращение к явным членам интерфейса можно осуществлять только через тип интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2685c-709">Explicit interface members can only be accessed via the interface type.</span></span> <span data-ttu-id="2685c-710">Например, реализация `IControl.Paint` предоставляемые предыдущего `EditBox` класс может вызываться только сначала следует преобразовать `EditBox` ссылка `IControl` тип интерфейса.</span><span class="sxs-lookup"><span data-stu-id="2685c-710">For example, the implementation of `IControl.Paint` provided by the previous `EditBox` class can only be invoked by first converting the `EditBox` reference to the `IControl` interface type.</span></span>

```csharp
EditBox editBox = new EditBox();
editBox.Paint();                        // Error, no such method
IControl control = editBox;
control.Paint();                        // Ok
```

## <a name="enums"></a><span data-ttu-id="2685c-711">перечислениям;</span><span class="sxs-lookup"><span data-stu-id="2685c-711">Enums</span></span>

<span data-ttu-id="2685c-712">***Тип enum*** представляет собой тип значения с набором именованных констант.</span><span class="sxs-lookup"><span data-stu-id="2685c-712">An ***enum type*** is a distinct value type with a set of named constants.</span></span> <span data-ttu-id="2685c-713">В следующем примере, объявляет и использует тип перечисления с именем `Color` с три константы: `Red`, `Green`, и `Blue`.</span><span class="sxs-lookup"><span data-stu-id="2685c-713">The following example declares and uses an enum type named `Color` with three constant values, `Red`, `Green`, and `Blue`.</span></span>

```csharp
using System;

enum Color
{
    Red,
    Green,
    Blue
}

class Test
{
    static void PrintColor(Color color) {
        switch (color) {
            case Color.Red:
                Console.WriteLine("Red");
                break;
            case Color.Green:
                Console.WriteLine("Green");
                break;
            case Color.Blue:
                Console.WriteLine("Blue");
                break;
            default:
                Console.WriteLine("Unknown color");
                break;
        }
    }

    static void Main() {
        Color c = Color.Red;
        PrintColor(c);
        PrintColor(Color.Blue);
    }
}
```
<span data-ttu-id="2685c-714">Каждый тип перечисления имеет соответствующий целочисленных типов, который ***базовый тип*** типа перечисления.</span><span class="sxs-lookup"><span data-stu-id="2685c-714">Each enum type has a corresponding integral type called the ***underlying type*** of the enum type.</span></span> <span data-ttu-id="2685c-715">Базовый тип явно не объявлен тип перечисления имеет базовый тип из `int`.</span><span class="sxs-lookup"><span data-stu-id="2685c-715">An enum type that does not explicitly declare an underlying type has an underlying type of `int`.</span></span> <span data-ttu-id="2685c-716">Формат хранения и диапазон возможных значений типа перечисления определяются его базовым типом.</span><span class="sxs-lookup"><span data-stu-id="2685c-716">An enum type's storage format and range of possible values are determined by its underlying type.</span></span> <span data-ttu-id="2685c-717">Набор значений, которые может принимать тип перечисления не ограничивается его членами перечисления.</span><span class="sxs-lookup"><span data-stu-id="2685c-717">The set of values that an enum type can take on is not limited by its enum members.</span></span> <span data-ttu-id="2685c-718">В частности любое значение базового типа перечисления может быть приведен к типу перечисления и являться допустимым дискретным значением этого типа перечисления.</span><span class="sxs-lookup"><span data-stu-id="2685c-718">In particular, any value of the underlying type of an enum can be cast to the enum type and is a distinct valid value of that enum type.</span></span>

<span data-ttu-id="2685c-719">В следующем примере объявляется тип перечисления с именем `Alignment` с базовым типом `sbyte`.</span><span class="sxs-lookup"><span data-stu-id="2685c-719">The following example declares an enum type named `Alignment` with an underlying type of `sbyte`.</span></span>

```csharp
enum Alignment: sbyte
{
    Left = -1,
    Center = 0,
    Right = 1
}
```
<span data-ttu-id="2685c-720">Как показано в предыдущем примере, объявление члена перечисления может включать константное выражение, задающее значение члена.</span><span class="sxs-lookup"><span data-stu-id="2685c-720">As shown by the previous example, an enum member declaration can include a constant expression that specifies the value of the member.</span></span> <span data-ttu-id="2685c-721">Постоянное значение для каждого члена перечисления должен быть в диапазоне базового типа перечисления.</span><span class="sxs-lookup"><span data-stu-id="2685c-721">The constant value for each enum member must be in the range of the underlying type of the enum.</span></span> <span data-ttu-id="2685c-722">При объявлении члена перечисления значение не указано явным образом, члену присваивается нулевое (если это первый элемент в тип перечисления) значение или значения объявленного члена перечисления, а также один.</span><span class="sxs-lookup"><span data-stu-id="2685c-722">When an enum member declaration does not explicitly specify a value, the member is given the value zero (if it is the first member in the enum type) or the value of the textually preceding enum member plus one.</span></span>

<span data-ttu-id="2685c-723">Значения перечислений можно преобразовать к целочисленным значениям и наоборот с помощью приведения типов.</span><span class="sxs-lookup"><span data-stu-id="2685c-723">Enum values can be converted to integral values and vice versa using type casts.</span></span> <span data-ttu-id="2685c-724">Пример</span><span class="sxs-lookup"><span data-stu-id="2685c-724">For example</span></span>

```csharp
int i = (int)Color.Blue;        // int i = 2;
Color c = (Color)2;             // Color c = Color.Blue;
```
<span data-ttu-id="2685c-725">Значение по умолчанию любого типа перечисления — целочисленное значение ноль преобразуется в тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="2685c-725">The default value of any enum type is the integral value zero converted to the enum type.</span></span> <span data-ttu-id="2685c-726">В случаях, когда переменная автоматически инициализируются значением по умолчанию это значение, присваиваемое переменным перечисляемого типа.</span><span class="sxs-lookup"><span data-stu-id="2685c-726">In cases where variables are automatically initialized to a default value, this is the value given to variables of enum types.</span></span> <span data-ttu-id="2685c-727">В порядке для значения по умолчанию для типа перечисления было легко доступно литерала `0` неявно преобразует в любой тип перечисления.</span><span class="sxs-lookup"><span data-stu-id="2685c-727">In order for the default value of an enum type to be easily available, the literal `0` implicitly converts to any enum type.</span></span> <span data-ttu-id="2685c-728">Таким образом, допустимо следующее выражение.</span><span class="sxs-lookup"><span data-stu-id="2685c-728">Thus, the following is permitted.</span></span>

```csharp
Color c = 0;
```

## <a name="delegates"></a><span data-ttu-id="2685c-729">Делегаты</span><span class="sxs-lookup"><span data-stu-id="2685c-729">Delegates</span></span>

<span data-ttu-id="2685c-730">***Тип delegate*** представляет ссылки на методы с конкретным списком параметров и типом возвращаемого значения.</span><span class="sxs-lookup"><span data-stu-id="2685c-730">A ***delegate type*** represents references to methods with a particular parameter list and return type.</span></span> <span data-ttu-id="2685c-731">Делегаты позволяют использовать методы как сущности, сохраняя их в переменные и передавая в качестве параметров.</span><span class="sxs-lookup"><span data-stu-id="2685c-731">Delegates make it possible to treat methods as entities that can be assigned to variables and passed as parameters.</span></span> <span data-ttu-id="2685c-732">Принцип работы делегатов близок к указателям функций из некоторых языков, но в отличие от указателей функций делегаты являются объектно-ориентированными и строго типизированными.</span><span class="sxs-lookup"><span data-stu-id="2685c-732">Delegates are similar to the concept of function pointers found in some other languages, but unlike function pointers, delegates are object-oriented and type-safe.</span></span>

<span data-ttu-id="2685c-733">Следующий пример кода объявляет и использует тип делегата с именем `Function`.</span><span class="sxs-lookup"><span data-stu-id="2685c-733">The following example declares and uses a delegate type named `Function`.</span></span>

```csharp
using System;

delegate double Function(double x);

class Multiplier
{
    double factor;

    public Multiplier(double factor) {
        this.factor = factor;
    }

    public double Multiply(double x) {
        return x * factor;
    }
}

class Test
{
    static double Square(double x) {
        return x * x;
    }

    static double[] Apply(double[] a, Function f) {
        double[] result = new double[a.Length];
        for (int i = 0; i < a.Length; i++) result[i] = f(a[i]);
        return result;
    }

    static void Main() {
        double[] a = {0.0, 0.5, 1.0};
        double[] squares = Apply(a, Square);
        double[] sines = Apply(a, Math.Sin);
        Multiplier m = new Multiplier(2.0);
        double[] doubles =  Apply(a, m.Multiply);
    }
}
```
<span data-ttu-id="2685c-734">Экземпляр `Function` с типом делегата может ссылаться на любой метод, который принимает аргумент `double` и возвращает значение `double`.</span><span class="sxs-lookup"><span data-stu-id="2685c-734">An instance of the `Function` delegate type can reference any method that takes a `double` argument and returns a `double` value.</span></span> <span data-ttu-id="2685c-735">`Apply` Метод применим данный `Function` к элементам `double[]`, возвращение `double[]` с результатами.</span><span class="sxs-lookup"><span data-stu-id="2685c-735">The `Apply` method applies a given `Function` to the elements of a `double[]`, returning a `double[]` with the results.</span></span> <span data-ttu-id="2685c-736">В методе `Main` используется `Apply` для применения трех различных функций к `double[]`.</span><span class="sxs-lookup"><span data-stu-id="2685c-736">In the `Main` method, `Apply` is used to apply three different functions to a `double[]`.</span></span>

<span data-ttu-id="2685c-737">Делегат может ссылаться на статический метод (например, `Square` или `Math.Sin` в предыдущем примере) или метод экземпляра (например, `m.Multiply` в предыдущем примере).</span><span class="sxs-lookup"><span data-stu-id="2685c-737">A delegate can reference either a static method (such as `Square` or `Math.Sin` in the previous example) or an instance method (such as `m.Multiply` in the previous example).</span></span> <span data-ttu-id="2685c-738">Делегат, который ссылается на метод экземпляра, также содержит ссылку на конкретный объект. Когда метод экземпляра вызывается через делегат, этот объект превращается в `this` в вызове.</span><span class="sxs-lookup"><span data-stu-id="2685c-738">A delegate that references an instance method also references a particular object, and when the instance method is invoked through the delegate, that object becomes `this` in the invocation.</span></span>

<span data-ttu-id="2685c-739">Делегаты могут также создаваться с использованием анонимных функций, то есть создаваемых на ходу "встроенных методов".</span><span class="sxs-lookup"><span data-stu-id="2685c-739">Delegates can also be created using anonymous functions, which are "inline methods" that are created on the fly.</span></span> <span data-ttu-id="2685c-740">Анонимные функции могут использовать локальные переменные соседних методов.</span><span class="sxs-lookup"><span data-stu-id="2685c-740">Anonymous functions can see the local variables of the surrounding methods.</span></span> <span data-ttu-id="2685c-741">Таким образом, приведенный выше пример умножения можно записать проще и без использования `Multiplier` класса:</span><span class="sxs-lookup"><span data-stu-id="2685c-741">Thus, the multiplier example above can be written more easily without using a `Multiplier` class:</span></span>

```csharp
double[] doubles =  Apply(a, (double x) => x * 2.0);
```
<span data-ttu-id="2685c-742">Также стоит упомянуть о такой интересной и полезной особенности делегата, что он не имеет информации или ограничений в отношении того, к какому классу относится указанный в нем метод. Достаточно лишь, чтобы указанный метод имел такие же типы параметров и возвращаемого значения, которые назначены для делегата.</span><span class="sxs-lookup"><span data-stu-id="2685c-742">An interesting and useful property of a delegate is that it does not know or care about the class of the method it references; all that matters is that the referenced method has the same parameters and return type as the delegate.</span></span>

## <a name="attributes"></a><span data-ttu-id="2685c-743">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="2685c-743">Attributes</span></span>

<span data-ttu-id="2685c-744">Типы, члены и другие сущности в программе C# поддерживают модификаторы, которые управляют некоторыми аспектами их поведения.</span><span class="sxs-lookup"><span data-stu-id="2685c-744">Types, members, and other entities in a C# program support modifiers that control certain aspects of their behavior.</span></span> <span data-ttu-id="2685c-745">Например, доступность метода определяется с помощью модификаторов `public`, `protected`, `internal` и `private`.</span><span class="sxs-lookup"><span data-stu-id="2685c-745">For example, the accessibility of a method is controlled using the `public`, `protected`, `internal`, and `private` modifiers.</span></span> <span data-ttu-id="2685c-746">C# обобщает эту возможность, позволяя пользователям определять собственные типы декларативных сведений, назначать их для сущностей программы и извлекать во время выполнения.</span><span class="sxs-lookup"><span data-stu-id="2685c-746">C# generalizes this capability such that user-defined types of declarative information can be attached to program entities and retrieved at run-time.</span></span> <span data-ttu-id="2685c-747">В программах эти дополнительные декларативные сведения определяются и используются посредством ***атрибутов***.</span><span class="sxs-lookup"><span data-stu-id="2685c-747">Programs specify this additional declarative information by defining and using ***attributes***.</span></span>

<span data-ttu-id="2685c-748">Следующий пример кода объявляет атрибут `HelpAttribute`, который можно поместить в сущности программы для указания связей с соответствующей документацией.</span><span class="sxs-lookup"><span data-stu-id="2685c-748">The following example declares a `HelpAttribute` attribute that can be placed on program entities to provide links to their associated documentation.</span></span>

```csharp
using System;

public class HelpAttribute: Attribute
{
    string url;
    string topic;

    public HelpAttribute(string url) {
        this.url = url;
    }

    public string Url {
        get { return url; }
    }

    public string Topic {
        get { return topic; }
        set { topic = value; }
    }
}
```
<span data-ttu-id="2685c-749">Все классы атрибутов являются производными от `System.Attribute` базового класса, предоставляемые платформой .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="2685c-749">All attribute classes derive from the `System.Attribute` base class provided by the .NET Framework.</span></span> <span data-ttu-id="2685c-750">Чтобы задать атрибут, его имя и возможные аргументы указываются в квадратных скобках непосредственно перед объявлением соответствующей сущности.</span><span class="sxs-lookup"><span data-stu-id="2685c-750">Attributes can be applied by giving their name, along with any arguments, inside square brackets just before the associated declaration.</span></span> <span data-ttu-id="2685c-751">Если имя атрибута заканчивается на `Attribute`, можно опустить, часть имени, при ссылке на атрибут.</span><span class="sxs-lookup"><span data-stu-id="2685c-751">If an attribute's name ends in `Attribute`, that part of the name can be omitted when the attribute is referenced.</span></span> <span data-ttu-id="2685c-752">Например, атрибут с именем `HelpAttribute` можно использовать так:</span><span class="sxs-lookup"><span data-stu-id="2685c-752">For example, the `HelpAttribute` attribute can be used as follows.</span></span>

```csharp
[Help("http://msdn.microsoft.com/.../MyClass.htm")]
public class Widget
{
    [Help("http://msdn.microsoft.com/.../MyClass.htm", Topic = "Display")]
    public void Display(string text) {}
}
```
<span data-ttu-id="2685c-753">В этом примере подключается `HelpAttribute` для `Widget` класса, а другой `HelpAttribute` для `Display` метода в классе.</span><span class="sxs-lookup"><span data-stu-id="2685c-753">This example attaches a `HelpAttribute` to the `Widget` class and another `HelpAttribute` to the `Display` method in the class.</span></span> <span data-ttu-id="2685c-754">Открытые конструкторы класса атрибута указывают, какие сведения необходимо указать при назначении атрибута некоторой сущности программы.</span><span class="sxs-lookup"><span data-stu-id="2685c-754">The public constructors of an attribute class control the information that must be provided when the attribute is attached to a program entity.</span></span> <span data-ttu-id="2685c-755">Дополнительные сведения можно предоставить через обращения к открытым свойствам класса атрибута, доступным для чтения и записи (например, как указанная выше ссылка на свойство `Topic`).</span><span class="sxs-lookup"><span data-stu-id="2685c-755">Additional information can be provided by referencing public read-write properties of the attribute class (such as the reference to the `Topic` property previously).</span></span>

<span data-ttu-id="2685c-756">В следующем примере показано, как можно получить сведения об атрибутах для заданной сущности программы во время выполнения с помощью отражения.</span><span class="sxs-lookup"><span data-stu-id="2685c-756">The following example shows how attribute information for a given program entity can be retrieved at run-time using reflection.</span></span>

```csharp
using System;
using System.Reflection;

class Test
{
    static void ShowHelp(MemberInfo member) {
        HelpAttribute a = Attribute.GetCustomAttribute(member,
            typeof(HelpAttribute)) as HelpAttribute;
        if (a == null) {
            Console.WriteLine("No help for {0}", member);
        }
        else {
            Console.WriteLine("Help for {0}:", member);
            Console.WriteLine("  Url={0}, Topic={1}", a.Url, a.Topic);
        }
    }

    static void Main() {
        ShowHelp(typeof(Widget));
        ShowHelp(typeof(Widget).GetMethod("Display"));
    }
}
```
<span data-ttu-id="2685c-757">Когда выполняется запрос конкретного атрибута через отражение, вызывается конструктор для класса атрибута с указанием сведений, представленных в исходном коде программы, а затем возвращается созданный экземпляр атрибута.</span><span class="sxs-lookup"><span data-stu-id="2685c-757">When a particular attribute is requested through reflection, the constructor for the attribute class is invoked with the information provided in the program source, and the resulting attribute instance is returned.</span></span> <span data-ttu-id="2685c-758">Если дополнительные сведения предоставляются через свойства, перед возвращением экземпляра атрибута этим свойствам присваиваются указанные значения.</span><span class="sxs-lookup"><span data-stu-id="2685c-758">If additional information was provided through properties, those properties are set to the given values before the attribute instance is returned.</span></span>
