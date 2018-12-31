# <a name="namespaces"></a><span data-ttu-id="08cc1-101">Пространства имен</span><span class="sxs-lookup"><span data-stu-id="08cc1-101">Namespaces</span></span>

<span data-ttu-id="08cc1-102">C#, структуре программ использование пространств имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-102">C# programs are organized using namespaces.</span></span> <span data-ttu-id="08cc1-103">Пространства имен используются как в качестве системы для программы «internal» организации, так и в качестве системы «external» организации — способа представления элементы программы, которые предоставляются другим программам.</span><span class="sxs-lookup"><span data-stu-id="08cc1-103">Namespaces are used both as an "internal" organization system for a program, and as an "external" organization system—a way of presenting program elements that are exposed to other programs.</span></span>

<span data-ttu-id="08cc1-104">Директивы using ([директив Using](namespaces.md#using-directives)) предоставляются для упрощения использования пространств имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-104">Using directives ([Using directives](namespaces.md#using-directives)) are provided to facilitate the use of namespaces.</span></span>

## <a name="compilation-units"></a><span data-ttu-id="08cc1-105">Единицы компиляции</span><span class="sxs-lookup"><span data-stu-id="08cc1-105">Compilation units</span></span>

<span data-ttu-id="08cc1-106">Объект *compilation_unit* определяет общую структуру исходного файла.</span><span class="sxs-lookup"><span data-stu-id="08cc1-106">A *compilation_unit* defines the overall structure of a source file.</span></span> <span data-ttu-id="08cc1-107">Единица компиляции состоит из нуля или более *using_directive*следуют ноль или более *global_attributes* следуют ноль или более *namespace_member_declaration*s .</span><span class="sxs-lookup"><span data-stu-id="08cc1-107">A compilation unit consists of zero or more *using_directive*s followed by zero or more *global_attributes* followed by zero or more *namespace_member_declaration*s.</span></span>

```antlr
compilation_unit
    : extern_alias_directive* using_directive* global_attributes? namespace_member_declaration*
    ;
```

<span data-ttu-id="08cc1-108">Программы на C# состоит из одного или несколько блоков компиляции, каждый из которых размещается в отдельном исходном файле.</span><span class="sxs-lookup"><span data-stu-id="08cc1-108">A C# program consists of one or more compilation units, each contained in a separate source file.</span></span> <span data-ttu-id="08cc1-109">При компиляции программы на C# все единицы компиляции обрабатываются вместе.</span><span class="sxs-lookup"><span data-stu-id="08cc1-109">When a C# program is compiled, all of the compilation units are processed together.</span></span> <span data-ttu-id="08cc1-110">Таким образом единицы компиляции может зависеть друг от друга, возможно по кругу.</span><span class="sxs-lookup"><span data-stu-id="08cc1-110">Thus, compilation units can depend on each other, possibly in a circular fashion.</span></span>

<span data-ttu-id="08cc1-111">*Using_directive*s единицы компиляции эффект будет иметь *global_attributes* и *namespace_member_declaration*s этой единицы компиляции, но не оказывают влияния на другие единицы компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-111">The *using_directive*s of a compilation unit affect the *global_attributes* and *namespace_member_declaration*s of that compilation unit, but have no effect on other compilation units.</span></span>

<span data-ttu-id="08cc1-112">*Global_attributes* ([атрибуты](attributes.md)) единицы компиляции разрешают спецификацию атрибуты для целевой сборки и модуля.</span><span class="sxs-lookup"><span data-stu-id="08cc1-112">The *global_attributes* ([Attributes](attributes.md)) of a compilation unit permit the specification of attributes for the target assembly and module.</span></span> <span data-ttu-id="08cc1-113">Сборки и модули действуют как физические контейнеры для типов.</span><span class="sxs-lookup"><span data-stu-id="08cc1-113">Assemblies and modules act as physical containers for types.</span></span> <span data-ttu-id="08cc1-114">Сборка может состоять из нескольких физически отдельных модулей.</span><span class="sxs-lookup"><span data-stu-id="08cc1-114">An assembly may consist of several physically separate modules.</span></span>

<span data-ttu-id="08cc1-115">*Namespace_member_declaration*s каждой единицы компиляции программы размещают члены пространства одно объявление, называемого глобальное пространство имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-115">The *namespace_member_declaration*s of each compilation unit of a program contribute members to a single declaration space called the global namespace.</span></span> <span data-ttu-id="08cc1-116">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-116">For example:</span></span>

<span data-ttu-id="08cc1-117">Файл `A.cs`:</span><span class="sxs-lookup"><span data-stu-id="08cc1-117">File `A.cs`:</span></span>
```csharp
class A {}
```

<span data-ttu-id="08cc1-118">Файл `B.cs`:</span><span class="sxs-lookup"><span data-stu-id="08cc1-118">File `B.cs`:</span></span>
```csharp
class B {}
```

<span data-ttu-id="08cc1-119">Две единицы компиляции размещаются в одном глобальное пространство имен, в данном случае объявление двух классов с помощью полных имен `A` и `B`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-119">The two compilation units contribute to the single global namespace, in this case declaring two classes with the fully qualified names `A` and `B`.</span></span> <span data-ttu-id="08cc1-120">Поскольку эти две единицы компиляции размещаются в одном пространстве объявлений, было бы ошибку, если каждый содержащийся объявление члена с таким именем.</span><span class="sxs-lookup"><span data-stu-id="08cc1-120">Because the two compilation units contribute to the same declaration space, it would have been an error if each contained a declaration of a member with the same name.</span></span>

## <a name="namespace-declarations"></a><span data-ttu-id="08cc1-121">Декларации пространств имен</span><span class="sxs-lookup"><span data-stu-id="08cc1-121">Namespace declarations</span></span>

<span data-ttu-id="08cc1-122">Объект *namespace_declaration* состоит из ключевого слова `namespace`, за которым следует имя пространства имен и текста, при необходимости и точку с запятой.</span><span class="sxs-lookup"><span data-stu-id="08cc1-122">A *namespace_declaration* consists of the keyword `namespace`, followed by a namespace name and body, optionally followed by a semicolon.</span></span>

```antlr
namespace_declaration
    : 'namespace' qualified_identifier namespace_body ';'?
    ;

qualified_identifier
    : identifier ('.' identifier)*
    ;

namespace_body
    : '{' extern_alias_directive* using_directive* namespace_member_declaration* '}'
    ;
```

<span data-ttu-id="08cc1-123">Объект *namespace_declaration* наблюдается объявлением верхнего уровня в *compilation_unit* или объявлением члена внутри другого *namespace_declaration*.</span><span class="sxs-lookup"><span data-stu-id="08cc1-123">A *namespace_declaration* may occur as a top-level declaration in a *compilation_unit* or as a member declaration within another *namespace_declaration*.</span></span> <span data-ttu-id="08cc1-124">Когда *namespace_declaration* происходит объявлением верхнего уровня в *compilation_unit*, пространство имен становится членом глобального пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-124">When a *namespace_declaration* occurs as a top-level declaration in a *compilation_unit*, the namespace becomes a member of the global namespace.</span></span> <span data-ttu-id="08cc1-125">Когда *namespace_declaration* происходит внутри другого *namespace_declaration*, внутреннее пространство имен становится членом внешнего пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-125">When a *namespace_declaration* occurs within another *namespace_declaration*, the inner namespace becomes a member of the outer namespace.</span></span> <span data-ttu-id="08cc1-126">В любом случае имя пространства имен должно быть уникальным в пределах содержащего пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-126">In either case, the name of a namespace must be unique within the containing namespace.</span></span>

<span data-ttu-id="08cc1-127">Пространства имен являются неявно `public` и объявление пространства имен не может включать модификаторы доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-127">Namespaces are implicitly `public` and the declaration of a namespace cannot include any access modifiers.</span></span>

<span data-ttu-id="08cc1-128">В рамках *namespace_body*, необязательный *using_directive*s импортировать имена других пространств имен, типов и членов, позволяющих ссылаться напрямую вместо того через полные имена.</span><span class="sxs-lookup"><span data-stu-id="08cc1-128">Within a *namespace_body*, the optional *using_directive*s import the names of other namespaces, types and members, allowing them to be referenced directly instead of through qualified names.</span></span> <span data-ttu-id="08cc1-129">Необязательный *namespace_member_declaration*s размещают члены в области объявления пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-129">The optional *namespace_member_declaration*s contribute members to the declaration space of the namespace.</span></span> <span data-ttu-id="08cc1-130">Обратите внимание, что все *using_directive*s должны располагаться перед любыми объявлениями членов.</span><span class="sxs-lookup"><span data-stu-id="08cc1-130">Note that all *using_directive*s must appear before any member declarations.</span></span>

<span data-ttu-id="08cc1-131">*Qualified_identifier* из *namespace_declaration* может быть один идентификатор или последовательность идентификаторов, разделенных "`.`" маркеров.</span><span class="sxs-lookup"><span data-stu-id="08cc1-131">The *qualified_identifier* of a *namespace_declaration* may be a single identifier or a sequence of identifiers separated by "`.`" tokens.</span></span> <span data-ttu-id="08cc1-132">Последняя форма позволяет программе определить вложенное пространство имен без лексически вложение несколько объявлений пространств имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-132">The latter form permits a program to define a nested namespace without lexically nesting several namespace declarations.</span></span> <span data-ttu-id="08cc1-133">Например, примененная к объекту директива</span><span class="sxs-lookup"><span data-stu-id="08cc1-133">For example,</span></span>

```csharp
namespace N1.N2
{
    class A {}

    class B {}
}
```
<span data-ttu-id="08cc1-134">семантически эквивалентен</span><span class="sxs-lookup"><span data-stu-id="08cc1-134">is semantically equivalent to</span></span>
```csharp
namespace N1
{
    namespace N2
    {
        class A {}

        class B {}
    }
}
```

<span data-ttu-id="08cc1-135">Пространства имен являются открытыми, и два объявления пространств имен с тем же полным именем размещаются в одном пространстве объявлений ([объявления](basic-concepts.md#declarations)).</span><span class="sxs-lookup"><span data-stu-id="08cc1-135">Namespaces are open-ended, and two namespace declarations with the same fully qualified name contribute to the same declaration space ([Declarations](basic-concepts.md#declarations)).</span></span> <span data-ttu-id="08cc1-136">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-136">In the example</span></span>
```csharp
namespace N1.N2
{
    class A {}
}

namespace N1.N2
{
    class B {}
}
```
<span data-ttu-id="08cc1-137">Два объявления пространства имен выше, размещаются в одной области объявления, в этом случае объявляются два класса с полными доменными именами `N1.N2.A` и `N1.N2.B`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-137">the two namespace declarations above contribute to the same declaration space, in this case declaring two classes with the fully qualified names `N1.N2.A` and `N1.N2.B`.</span></span> <span data-ttu-id="08cc1-138">Поскольку два объявления размещаются в одном пространстве объявлений, было бы что ошибку, если каждый содержится объявление члена с таким именем.</span><span class="sxs-lookup"><span data-stu-id="08cc1-138">Because the two declarations contribute to the same declaration space, it would have been an error if each contained a declaration of a member with the same name.</span></span>

## <a name="extern-aliases"></a><span data-ttu-id="08cc1-139">Внешние псевдонимы</span><span class="sxs-lookup"><span data-stu-id="08cc1-139">Extern aliases</span></span>

<span data-ttu-id="08cc1-140">*Extern_alias_directive* представляет идентификатор, служащий в качестве псевдонима для пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-140">An *extern_alias_directive* introduces an identifier that serves as an alias for a namespace.</span></span> <span data-ttu-id="08cc1-141">Спецификации пространства имен с псевдонимом является внешним по отношению к исходному коду программы, а также распространяется на вложенные пространства имен пространства имен с псевдонимом.</span><span class="sxs-lookup"><span data-stu-id="08cc1-141">The specification of the aliased namespace is external to the source code of the program and applies also to nested namespaces of the aliased namespace.</span></span>

```antlr
extern_alias_directive
    : 'extern' 'alias' identifier ';'
    ;
```

<span data-ttu-id="08cc1-142">Область *extern_alias_directive* распространяется *using_directive*s, *global_attributes* и *namespace_member_declaration*s его непосредственно вмещающего компиляции единицы или пространства имен текста.</span><span class="sxs-lookup"><span data-stu-id="08cc1-142">The scope of an *extern_alias_directive* extends over the *using_directive*s, *global_attributes* and *namespace_member_declaration*s of its immediately containing compilation unit or namespace body.</span></span>

<span data-ttu-id="08cc1-143">В теле компиляции единицы или пространства имен, содержащий *extern_alias_directive*, идентификатор, представленный *extern_alias_directive* может использоваться для ссылки на пространство имен с псевдонимом.</span><span class="sxs-lookup"><span data-stu-id="08cc1-143">Within a compilation unit or namespace body that contains an *extern_alias_directive*, the identifier introduced by the *extern_alias_directive* can be used to reference the aliased namespace.</span></span> <span data-ttu-id="08cc1-144">Произошла ошибка во время компиляции для *идентификатор* слово `global`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-144">It is a compile-time error for the *identifier* to be the word `global`.</span></span>

<span data-ttu-id="08cc1-145">*Extern_alias_directive* делает псевдоним доступным в теле конкретной компиляции единицы или пространства имен, но не размещает новые члены в основной области объявления.</span><span class="sxs-lookup"><span data-stu-id="08cc1-145">An *extern_alias_directive* makes an alias available within a particular compilation unit or namespace body, but it does not contribute any new members to the underlying declaration space.</span></span> <span data-ttu-id="08cc1-146">Другими словами *extern_alias_directive* не является транзитивным, но, скорее, влияет только на компиляцию единицы или пространства имен тело в которой оно встречается.</span><span class="sxs-lookup"><span data-stu-id="08cc1-146">In other words, an *extern_alias_directive* is not transitive, but, rather, affects only the compilation unit or namespace body in which it occurs.</span></span>

<span data-ttu-id="08cc1-147">Следующая программа объявляет и использует два псевдонима extern `X` и `Y`, каждый из который представляет корень иерархии отдельное пространство имен:</span><span class="sxs-lookup"><span data-stu-id="08cc1-147">The following program declares and uses two extern aliases, `X` and `Y`, each of which represent the root of a distinct namespace hierarchy:</span></span>
```csharp
extern alias X;
extern alias Y;

class Test
{
    X::N.A a;
    X::N.B b1;
    Y::N.B b2;
    Y::N.C c;
}
```

<span data-ttu-id="08cc1-148">Программа объявляет существование extern псевдонимы `X` и `Y`, но фактические определения псевдонимов являются внешними по отношению к программе.</span><span class="sxs-lookup"><span data-stu-id="08cc1-148">The program declares the existence of the extern aliases `X` and `Y`, but the actual definitions of the aliases are external to the program.</span></span> <span data-ttu-id="08cc1-149">Таким же именем `N.B` классов теперь можно ссылаться как на `X.N.B` и `Y.N.B`, либо с помощью квалификатор псевдонима пространства имен, `X::N.B` и `Y::N.B`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-149">The identically named `N.B` classes can now be referenced as `X.N.B` and `Y.N.B`, or, using the namespace alias qualifier, `X::N.B` and `Y::N.B`.</span></span> <span data-ttu-id="08cc1-150">Ошибка возникает, если программа объявляющем внешний псевдоним для которой предоставляются не внешнее определение.</span><span class="sxs-lookup"><span data-stu-id="08cc1-150">An error occurs if a program declares an extern alias for which no external definition is provided.</span></span>

## <a name="using-directives"></a><span data-ttu-id="08cc1-151">директивы using</span><span class="sxs-lookup"><span data-stu-id="08cc1-151">Using directives</span></span>

<span data-ttu-id="08cc1-152">***С помощью директивы*** облегчают использование пространств имен и типов, определенных в других пространствах имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-152">***Using directives*** facilitate the use of namespaces and types defined in other namespaces.</span></span> <span data-ttu-id="08cc1-153">Процесс разрешения с помощью директивы влияние *namespace_or_type_name*s ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)) и *simple_name*s ([простые имена ](expressions.md#simple-names)), но в отличие от объявлений, с использованием директивы не включаются новые члены в базовых пробелы объявление единицы компиляции или пространства имен, в котором они используются.</span><span class="sxs-lookup"><span data-stu-id="08cc1-153">Using directives impact the name resolution process of *namespace_or_type_name*s ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) and *simple_name*s ([Simple names](expressions.md#simple-names)), but unlike declarations, using directives do not contribute new members to the underlying declaration spaces of the compilation units or namespaces within which they are used.</span></span>

```antlr
using_directive
    : using_alias_directive
    | using_namespace_directive
    | using_static_directive
    ;
```

<span data-ttu-id="08cc1-154">Объект *using_alias_directive* ([директивы псевдонима Using](namespaces.md#using-alias-directives)) появился псевдоним для пространства имен или типа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-154">A *using_alias_directive* ([Using alias directives](namespaces.md#using-alias-directives)) introduces an alias for a namespace or type.</span></span>

<span data-ttu-id="08cc1-155">Объект *using_namespace_directive* ([с помощью директивы пространства имен](namespaces.md#using-namespace-directives)) импортирует элементы типа пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-155">A *using_namespace_directive* ([Using namespace directives](namespaces.md#using-namespace-directives)) imports the type members of a namespace.</span></span>

<span data-ttu-id="08cc1-156">Объект *using_static_directive* ([директивами Using static](namespaces.md#using-static-directives)) импортирует вложенные типы и статические члены типа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-156">A *using_static_directive* ([Using static directives](namespaces.md#using-static-directives)) imports the nested types and static members of a type.</span></span>

<span data-ttu-id="08cc1-157">Область *using_directive* распространяется *namespace_member_declaration*s его непосредственно вмещающего компиляции единицы или пространства имен текста.</span><span class="sxs-lookup"><span data-stu-id="08cc1-157">The scope of a *using_directive* extends over the *namespace_member_declaration*s of its immediately containing compilation unit or namespace body.</span></span> <span data-ttu-id="08cc1-158">Область *using_directive* специально не содержит его коллеге *using_directive*s.</span><span class="sxs-lookup"><span data-stu-id="08cc1-158">The scope of a *using_directive* specifically does not include its peer *using_directive*s.</span></span> <span data-ttu-id="08cc1-159">Таким образом, одноранговые *using_directive*s не влияют друг на друга, и порядок, в котором они записаны не играет роли.</span><span class="sxs-lookup"><span data-stu-id="08cc1-159">Thus, peer *using_directive*s do not affect each other, and the order in which they are written is insignificant.</span></span>

### <a name="using-alias-directives"></a><span data-ttu-id="08cc1-160">Директивы псевдонима using</span><span class="sxs-lookup"><span data-stu-id="08cc1-160">Using alias directives</span></span>

<span data-ttu-id="08cc1-161">Объект *using_alias_directive* представляет идентификатор, служащий в качестве псевдонима для пространства имен или тип в теле немедленно включающего компиляции единицы или пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-161">A *using_alias_directive* introduces an identifier that serves as an alias for a namespace or type within the immediately enclosing compilation unit or namespace body.</span></span>

```antlr
using_alias_directive
    : 'using' identifier '=' namespace_or_type_name ';'
    ;
```

<span data-ttu-id="08cc1-162">В объявлениях членов в единицу компиляции или пространстве имен тело, содержащий *using_alias_directive*, идентификатор, представленный *using_alias_directive* можно использовать ссылку на заданный пространство имен или тип.</span><span class="sxs-lookup"><span data-stu-id="08cc1-162">Within member declarations in a compilation unit or namespace body that contains a *using_alias_directive*, the identifier introduced by the *using_alias_directive* can be used to reference the given namespace or type.</span></span> <span data-ttu-id="08cc1-163">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-163">For example:</span></span>
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using A = N1.N2.A;

    class B: A {}
}
```

<span data-ttu-id="08cc1-164">Выше, в объявлениях членов в `N3` пространства имен, `A` является псевдонимом для `N1.N2.A`и поэтому класс `N3.B` является производным от класса `N1.N2.A`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-164">Above, within member declarations in the `N3` namespace, `A` is an alias for `N1.N2.A`, and thus class `N3.B` derives from class `N1.N2.A`.</span></span> <span data-ttu-id="08cc1-165">Тот же эффект достигается путем создания псевдонима `R` для `N1.N2` и указав `R.A`:</span><span class="sxs-lookup"><span data-stu-id="08cc1-165">The same effect can be obtained by creating an alias `R` for `N1.N2` and then referencing `R.A`:</span></span>
```csharp
namespace N3
{
    using R = N1.N2;

    class B: R.A {}
}
```

<span data-ttu-id="08cc1-166">*Идентификатор* из *using_alias_directive* должно быть уникальным в области объявления блока компиляции или пространство имен, содержащее немедленно *using_alias_directive* .</span><span class="sxs-lookup"><span data-stu-id="08cc1-166">The *identifier* of a *using_alias_directive* must be unique within the declaration space of the compilation unit or namespace that immediately contains the *using_alias_directive*.</span></span> <span data-ttu-id="08cc1-167">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-167">For example:</span></span>
```csharp
namespace N3
{
    class A {}
}

namespace N3
{
    using A = N1.N2.A;        // Error, A already exists
}
```

<span data-ttu-id="08cc1-168">Выше, `N3` уже содержит элемент `A`, так что это ошибка времени компиляции для *using_alias_directive* использование этого идентификатора.</span><span class="sxs-lookup"><span data-stu-id="08cc1-168">Above, `N3` already contains a member `A`, so it is a compile-time error for a *using_alias_directive* to use that identifier.</span></span> <span data-ttu-id="08cc1-169">Аналогичным образом, это ошибка времени компиляции в двух или более *using_alias_directive*s в одной единице компиляции или пространство имен теле объявлять псевдонимы с тем же именем.</span><span class="sxs-lookup"><span data-stu-id="08cc1-169">Likewise, it is a compile-time error for two or more *using_alias_directive*s in the same compilation unit or namespace body to declare aliases by the same name.</span></span>

<span data-ttu-id="08cc1-170">Объект *using_alias_directive* делает псевдоним доступным в теле конкретной компиляции единицы или пространства имен, но не размещает новые члены в основной области объявления.</span><span class="sxs-lookup"><span data-stu-id="08cc1-170">A *using_alias_directive* makes an alias available within a particular compilation unit or namespace body, but it does not contribute any new members to the underlying declaration space.</span></span> <span data-ttu-id="08cc1-171">Другими словами *using_alias_directive* не является транзитивным, а скорее влияет только единицы компиляции или пространстве имен тела в которой оно встречается.</span><span class="sxs-lookup"><span data-stu-id="08cc1-171">In other words, a *using_alias_directive* is not transitive but rather affects only the compilation unit or namespace body in which it occurs.</span></span> <span data-ttu-id="08cc1-172">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-172">In the example</span></span>
```csharp
namespace N3
{
    using R = N1.N2;
}

namespace N3
{
    class B: R.A {}            // Error, R unknown
}
```
<span data-ttu-id="08cc1-173">область *using_alias_directive* , в которой вводятся `R` распространяется только на объявления членов в теле пространства имен, в котором она содержится, поэтому `R` неизвестно во втором объявлении пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-173">the scope of the *using_alias_directive* that introduces `R` only extends to member declarations in the namespace body in which it is contained, so `R` is unknown in the second namespace declaration.</span></span> <span data-ttu-id="08cc1-174">Тем не менее, поместив *using_alias_directive* в содержащем компиляции единицы, то этот псевдоним, станут доступны в обоих объявления пространств имен:</span><span class="sxs-lookup"><span data-stu-id="08cc1-174">However, placing the *using_alias_directive* in the containing compilation unit causes the alias to become available within both namespace declarations:</span></span>
```csharp
using R = N1.N2;

namespace N3
{
    class B: R.A {}
}

namespace N3
{
    class C: R.A {}
}
```

<span data-ttu-id="08cc1-175">Так же как обычные элементы, представленные имена *using_alias_directive*s скрыты с помощью членов с таким же именем в вложенных областей.</span><span class="sxs-lookup"><span data-stu-id="08cc1-175">Just like regular members, names introduced by *using_alias_directive*s are hidden by similarly named members in nested scopes.</span></span> <span data-ttu-id="08cc1-176">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-176">In the example</span></span>
```csharp
using R = N1.N2;

namespace N3
{
    class R {}

    class B: R.A {}        // Error, R has no member A
}
```
<span data-ttu-id="08cc1-177">ссылка на `R.A` в объявлении `B` приводит к ошибке времени компиляции, так как `R` ссылается на `N3.R`, а не `N1.N2`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-177">the reference to `R.A` in the declaration of `B` causes a compile-time error because `R` refers to `N3.R`, not `N1.N2`.</span></span>

<span data-ttu-id="08cc1-178">Порядок, в котором *using_alias_directive*s записываются не значимости, а также разрешение *namespace_or_type_name* ссылается *using_alias_directive*не зависит от *using_alias_directive* сам или другими *using_directive*s в непосредственно содержащей единицы компиляции или пространстве имен тела.</span><span class="sxs-lookup"><span data-stu-id="08cc1-178">The order in which *using_alias_directive*s are written has no significance, and resolution of the *namespace_or_type_name* referenced by a *using_alias_directive* is not affected by the *using_alias_directive* itself or by other *using_directive*s in the immediately containing compilation unit or namespace body.</span></span> <span data-ttu-id="08cc1-179">Другими словами *namespace_or_type_name* из *using_alias_directive* разрешается, если непосредственно вмещающего единицы компиляции или пространстве имен тела бы нет *using_directive*s.</span><span class="sxs-lookup"><span data-stu-id="08cc1-179">In other words, the *namespace_or_type_name* of a *using_alias_directive* is resolved as if the immediately containing compilation unit or namespace body had no *using_directive*s.</span></span> <span data-ttu-id="08cc1-180">Объект *using_alias_directive* тем не менее могут быть подвержены *extern_alias_directive*s в непосредственно содержащей единицы компиляции или пространстве имен тела.</span><span class="sxs-lookup"><span data-stu-id="08cc1-180">A *using_alias_directive* may however be affected by *extern_alias_directive*s in the immediately containing compilation unit or namespace body.</span></span> <span data-ttu-id="08cc1-181">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-181">In the example</span></span>
```csharp
namespace N1.N2 {}

namespace N3
{
    extern alias E;

    using R1 = E.N;        // OK

    using R2 = N1;         // OK

    using R3 = N1.N2;      // OK

    using R4 = R2.N2;      // Error, R2 unknown
}
```
<span data-ttu-id="08cc1-182">последний *using_alias_directive* приводит к ошибке времени компиляции, так как он не влияет первый *using_alias_directive*.</span><span class="sxs-lookup"><span data-stu-id="08cc1-182">the last *using_alias_directive* results in a compile-time error because it is not affected by the first *using_alias_directive*.</span></span> <span data-ttu-id="08cc1-183">Первый *using_alias_directive* не приведет к ошибке с момента рамки внешний псевдоним `E` включает в себя *using_alias_directive*.</span><span class="sxs-lookup"><span data-stu-id="08cc1-183">The first *using_alias_directive* does not result in an error since the scope of the extern alias `E` includes the *using_alias_directive*.</span></span>

<span data-ttu-id="08cc1-184">Объект *using_alias_directive* можно создать псевдоним для любого пространства имен или типа, включая пространство имен, в котором он отображается, и любое пространство имен или тип, вложенные в это пространство имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-184">A *using_alias_directive* can create an alias for any namespace or type, including the namespace within which it appears and any namespace or type nested within that namespace.</span></span>

<span data-ttu-id="08cc1-185">Доступ к пространство имен или тип через псевдоним дает точно такой же результат, как доступ к этому пространству имен или тип по ее объявленному имени.</span><span class="sxs-lookup"><span data-stu-id="08cc1-185">Accessing a namespace or type through an alias yields exactly the same result as accessing that namespace or type through its declared name.</span></span> <span data-ttu-id="08cc1-186">Например если</span><span class="sxs-lookup"><span data-stu-id="08cc1-186">For example, given</span></span>
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using R1 = N1;
    using R2 = N1.N2;

    class B
    {
        N1.N2.A a;            // refers to N1.N2.A
        R1.N2.A b;            // refers to N1.N2.A
        R2.A c;               // refers to N1.N2.A
    }
}
```
<span data-ttu-id="08cc1-187">имена `N1.N2.A`, `R1.N2.A`, и `R2.A` являются эквивалентом и все ссылки на класс является полное имя которого `N1.N2.A`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-187">the names `N1.N2.A`, `R1.N2.A`, and `R2.A` are equivalent and all refer to the class whose fully qualified name is `N1.N2.A`.</span></span>

<span data-ttu-id="08cc1-188">С помощью псевдонимов можно имя закрытого сконструированного типа, но не имя является объявлением несвязанного универсального типа без указания аргументов типа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-188">Using aliases can name a closed constructed type, but cannot name an unbound generic type declaration without supplying type arguments.</span></span> <span data-ttu-id="08cc1-189">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-189">For example:</span></span>
```csharp
namespace N1
{
    class A<T>
    {
        class B {}
    }
}

namespace N2
{
    using W = N1.A;          // Error, cannot name unbound generic type

    using X = N1.A.B;        // Error, cannot name unbound generic type

    using Y = N1.A<int>;     // Ok, can name closed constructed type

    using Z<T> = N1.A<T>;    // Error, using alias cannot have type parameters
}
```

### <a name="using-namespace-directives"></a><span data-ttu-id="08cc1-190">С помощью директивы пространства имен</span><span class="sxs-lookup"><span data-stu-id="08cc1-190">Using namespace directives</span></span>

<span data-ttu-id="08cc1-191">Объект *using_namespace_directive* импортирует типы, содержащиеся в пространстве имен в немедленно включающего единицы компиляции или пространстве имен тела, включение идентификатор каждый тип, который будет использоваться без уточнения.</span><span class="sxs-lookup"><span data-stu-id="08cc1-191">A *using_namespace_directive* imports the types contained in a namespace into the immediately enclosing compilation unit or namespace body, enabling the identifier of each type to be used without qualification.</span></span>

```antlr
using_namespace_directive
    : 'using' namespace_name ';'
    ;
```

<span data-ttu-id="08cc1-192">В объявлениях членов в единицу компиляции или пространстве имен тело, содержащий *using_namespace_directive*, можно непосредственно ссылаться на типы, содержащиеся в данном пространстве имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-192">Within member declarations in a compilation unit or namespace body that contains a *using_namespace_directive*, the types contained in the given namespace can be referenced directly.</span></span> <span data-ttu-id="08cc1-193">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-193">For example:</span></span>
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1.N2;

    class B: A {}
}
```

<span data-ttu-id="08cc1-194">Выше, в объявлениях членов в `N3` пространства имен, члены типа `N1.N2` доступны непосредственно и поэтому класс `N3.B` является производным от класса `N1.N2.A`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-194">Above, within member declarations in the `N3` namespace, the type members of `N1.N2` are directly available, and thus class `N3.B` derives from class `N1.N2.A`.</span></span>

<span data-ttu-id="08cc1-195">Объект *using_namespace_directive* импортирует типы, содержащиеся в данном пространстве имен, но не импортирует вложенные пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-195">A *using_namespace_directive* imports the types contained in the given namespace, but specifically does not import nested namespaces.</span></span> <span data-ttu-id="08cc1-196">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-196">In the example</span></span>
```csharp
namespace N1.N2
{
    class A {}
}

namespace N3
{
    using N1;

    class B: N2.A {}        // Error, N2 unknown
}
```
<span data-ttu-id="08cc1-197">*using_namespace_directive* импортирует типы, содержащиеся в `N1`, но не пространства имен, вложенные в `N1`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-197">the *using_namespace_directive* imports the types contained in `N1`, but not the namespaces nested in `N1`.</span></span> <span data-ttu-id="08cc1-198">Таким образом, ссылку на `N2.A` в объявлении `B` приводит к ошибке времени компиляции, так как нет членов с именем `N2` находятся в области действия.</span><span class="sxs-lookup"><span data-stu-id="08cc1-198">Thus, the reference to `N2.A` in the declaration of `B` results in a compile-time error because no members named `N2` are in scope.</span></span>

<span data-ttu-id="08cc1-199">В отличие от *using_alias_directive*, *using_namespace_directive* может импортировать типы, идентификаторы которых уже определены в теле включающего компиляции единицы или пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-199">Unlike a *using_alias_directive*, a *using_namespace_directive* may import types whose identifiers are already defined within the enclosing compilation unit or namespace body.</span></span> <span data-ttu-id="08cc1-200">По сути, имена импортируемых *using_namespace_directive* скрыты с помощью членов с таким же именем в включающего единицы компиляции или пространстве имен тела.</span><span class="sxs-lookup"><span data-stu-id="08cc1-200">In effect, names imported by a *using_namespace_directive* are hidden by similarly named members in the enclosing compilation unit or namespace body.</span></span> <span data-ttu-id="08cc1-201">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-201">For example:</span></span>
```csharp
namespace N1.N2
{
    class A {}

    class B {}
}

namespace N3
{
    using N1.N2;

    class A {}
}
```

<span data-ttu-id="08cc1-202">Здесь в объявления членов в `N3` пространства имен, `A` ссылается на `N3.A` вместо `N1.N2.A`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-202">Here, within member declarations in the `N3` namespace, `A` refers to `N3.A` rather than `N1.N2.A`.</span></span>

<span data-ttu-id="08cc1-203">При импорте более одного пространства имен или типа *using_namespace_directive*s или *using_static_directive*s внутри же компиляции единицы или пространства имен содержат типы, с тем же именем, ссылки на Это имя как *type_name* неоднозначны.</span><span class="sxs-lookup"><span data-stu-id="08cc1-203">When more than one namespace or type imported by *using_namespace_directive*s or *using_static_directive*s in the same compilation unit or namespace body contain types by the same name, references to that name as a *type_name* are considered ambiguous.</span></span> <span data-ttu-id="08cc1-204">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-204">In the example</span></span>
```csharp
namespace N1
{
    class A {}
}

namespace N2
{
    class A {}
}

namespace N3
{
    using N1;

    using N2;

    class B: A {}                // Error, A is ambiguous
}
```
<span data-ttu-id="08cc1-205">оба `N1` и `N2` содержат член `A`и поскольку `N3` импортирует оба, ссылающиеся на `A` в `N3` ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-205">both `N1` and `N2` contain a member `A`, and because `N3` imports both, referencing `A` in `N3` is a compile-time error.</span></span> <span data-ttu-id="08cc1-206">В этом случае конфликт разрешается или через уточнения ссылок на `A`, либо введя *using_alias_directive* , использует `A`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-206">In this situation, the conflict can be resolved either through qualification of references to `A`, or by introducing a *using_alias_directive* that picks a particular `A`.</span></span> <span data-ttu-id="08cc1-207">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-207">For example:</span></span>
```csharp
namespace N3
{
    using N1;

    using N2;

    using A = N1.A;

    class B: A {}                // A means N1.A
}
```

<span data-ttu-id="08cc1-208">Кроме того, когда более одного пространства имен или типа импортировано *using_namespace_directive*s или *using_static_directive*внутри же компиляции единицы или пространства имен содержат типы или члены по таким же именем, ссылается на это имя как *simple_name* неоднозначны.</span><span class="sxs-lookup"><span data-stu-id="08cc1-208">Furthermore, when more than one namespace or type imported by *using_namespace_directive*s or *using_static_directive*s in the same compilation unit or namespace body contain types or members by the same name, references to that name as a *simple_name* are considered ambiguous.</span></span> <span data-ttu-id="08cc1-209">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-209">In the example</span></span>
```csharp
namespace N1
{
    class A {}
}

class C
{
    public static int A;
}

namespace N2
{
    using N1;
    using static C;

    class B
    {
        void M() 
        { 
            A a = new A();   // Ok, A is unambiguous as a type-name
            A.Equals(2);     // Error, A is ambiguous as a simple-name
        }
    }
}
```
<span data-ttu-id="08cc1-210">`N1` содержит член типа `A`, и `C` содержит статический метод `A`и поскольку `N2` импортирует оба, ссылающиеся на `A` как *simple_name* является неоднозначным, а во время компиляции Ошибка.</span><span class="sxs-lookup"><span data-stu-id="08cc1-210">`N1` contains a type member `A`, and `C` contains a static method `A`, and because `N2` imports both, referencing `A` as a *simple_name* is ambiguous and a compile-time error.</span></span> 

<span data-ttu-id="08cc1-211">Как и *using_alias_directive*, *using_namespace_directive* не размещает новые члены в базовой области объявления блока компиляции или пространства имен, а влияет только тело компиляции единицы или пространства имен, в котором он находится.</span><span class="sxs-lookup"><span data-stu-id="08cc1-211">Like a *using_alias_directive*, a *using_namespace_directive* does not contribute any new members to the underlying declaration space of the compilation unit or namespace, but rather affects only the compilation unit or namespace body in which it appears.</span></span>

<span data-ttu-id="08cc1-212">*Namespace_name* ссылается *using_namespace_directive* разрешается в так же, как *namespace_or_type_name* ссылается  *using_alias_directive*.</span><span class="sxs-lookup"><span data-stu-id="08cc1-212">The *namespace_name* referenced by a *using_namespace_directive* is resolved in the same way as the *namespace_or_type_name* referenced by a *using_alias_directive*.</span></span> <span data-ttu-id="08cc1-213">Таким образом *using_namespace_directive*s, в том же теле единицы или пространства имен компиляции не влияют друг на друга и могут быть записаны в любом порядке.</span><span class="sxs-lookup"><span data-stu-id="08cc1-213">Thus, *using_namespace_directive*s in the same compilation unit or namespace body do not affect each other and can be written in any order.</span></span>

### <a name="using-static-directives"></a><span data-ttu-id="08cc1-214">Директивами using static</span><span class="sxs-lookup"><span data-stu-id="08cc1-214">Using static directives</span></span>

<span data-ttu-id="08cc1-215">Объект *using_static_directive* импортирует вложенные типы и статические члены, содержащимися непосредственно в объявлении типа в немедленно включающего единицы компиляции или пространстве имен тела, включение идентификатор каждый член и тип быть использовать без уточнения.</span><span class="sxs-lookup"><span data-stu-id="08cc1-215">A *using_static_directive* imports the nested types and static members contained directly in a type declaration into the immediately enclosing compilation unit or namespace body, enabling the identifier of each member and type to be used without qualification.</span></span>

```antlr
using_static_directive
    : 'using' 'static' type_name ';'
    ;
```

<span data-ttu-id="08cc1-216">В объявлениях членов в единицу компиляции или пространстве имен тело, содержащий *using_static_directive*, доступный вложенные типы и члены статических (за исключением методов расширения) содержатся непосредственно в объявлении Данный тип можно ссылаться непосредственно.</span><span class="sxs-lookup"><span data-stu-id="08cc1-216">Within member declarations in a compilation unit or namespace body that contains a *using_static_directive*, the accessible nested types and static members (except extension methods) contained directly in the declaration of the given type can be referenced directly.</span></span> <span data-ttu-id="08cc1-217">Пример:</span><span class="sxs-lookup"><span data-stu-id="08cc1-217">For example:</span></span>

```csharp
namespace N1
{
    class A 
    {
        public class B{}
        public static B M(){ return new B(); }
    }
}

namespace N2
{
    using static N1.A;
    class C
    {
        void N() { B b = M(); }
    }
}
```

<span data-ttu-id="08cc1-218">Выше, в объявлениях членов в `N2` пространства имен, статические члены и вложенные типы `N1.A` доступны непосредственно и, следовательно, метод `N` может ссылаться на оба `B` и `M` членами `N1.A`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-218">Above, within member declarations in the `N2` namespace, the static members and nested types of `N1.A` are directly available, and thus the method `N` is able to reference both the `B` and `M` members of `N1.A`.</span></span>

<span data-ttu-id="08cc1-219">Объект *using_static_directive* специально не импортирует методы расширения непосредственно как статические методы, но делает их доступными для вызова метода расширения ([вызовы методов расширения](expressions.md#extension-method-invocations)).</span><span class="sxs-lookup"><span data-stu-id="08cc1-219">A *using_static_directive* specifically does not import extension methods directly as static methods, but makes them available for extension method invocation ([Extension method invocations](expressions.md#extension-method-invocations)).</span></span> <span data-ttu-id="08cc1-220">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-220">In the example</span></span>

```csharp
namespace N1 
{
    static class A 
    {
        public static void M(this string s){}
    }
}

namespace N2
{
    using static N1.A;

    class B
    {
        void N() 
        {
            M("A");      // Error, M unknown
            "B".M();     // Ok, M known as extension method
            N1.A.M("C"); // Ok, fully qualified
        }
    }
}
```
<span data-ttu-id="08cc1-221">*using_static_directive* импортирует метод расширения `M` содержащихся в `N1.A`, но только в качестве метода расширения.</span><span class="sxs-lookup"><span data-stu-id="08cc1-221">the *using_static_directive* imports the extension method `M` contained in `N1.A`, but only as an extension method.</span></span> <span data-ttu-id="08cc1-222">Таким образом, первым обращением к `M` в теле `B.N` приводит к ошибке времени компиляции, так как нет членов с именем `M` находятся в области действия.</span><span class="sxs-lookup"><span data-stu-id="08cc1-222">Thus, the first reference to `M` in the body of `B.N` results in a compile-time error because no members named `M` are in scope.</span></span>

<span data-ttu-id="08cc1-223">Объект *using_static_directive* импортирует только элементы и типы, объявленные непосредственно в указанный тип, не членов и типов, объявленных в базовых классах.</span><span class="sxs-lookup"><span data-stu-id="08cc1-223">A *using_static_directive* only imports members and types declared directly in the given type, not members and types declared in base classes.</span></span>

<span data-ttu-id="08cc1-224">TODO: Пример</span><span class="sxs-lookup"><span data-stu-id="08cc1-224">TODO: Example</span></span>

<span data-ttu-id="08cc1-225">Неоднозначность между несколькими *using_namespace_directives* и *using_static_directives* рассматриваются в [с помощью директивы пространства имен](namespaces.md#using-namespace-directives).</span><span class="sxs-lookup"><span data-stu-id="08cc1-225">Ambiguities between multiple *using_namespace_directives* and *using_static_directives* are discussed in [Using namespace directives](namespaces.md#using-namespace-directives).</span></span>

## <a name="namespace-members"></a><span data-ttu-id="08cc1-226">Члены пространства имен</span><span class="sxs-lookup"><span data-stu-id="08cc1-226">Namespace members</span></span>

<span data-ttu-id="08cc1-227">Объект *namespace_member_declaration* либо *namespace_declaration* ([объявления пространств имен](namespaces.md#namespace-declarations)) или *type_declaration* () [Объявления типов](namespaces.md#type-declarations)).</span><span class="sxs-lookup"><span data-stu-id="08cc1-227">A *namespace_member_declaration* is either a *namespace_declaration* ([Namespace declarations](namespaces.md#namespace-declarations)) or a *type_declaration* ([Type declarations](namespaces.md#type-declarations)).</span></span>

```antlr
namespace_member_declaration
    : namespace_declaration
    | type_declaration
    ;
```

<span data-ttu-id="08cc1-228">Блок компиляции или тело пространства имен может содержать *namespace_member_declaration*s и такие объявления добавляют новые члены в базовой области объявления, содержащего текста компиляции единицы или пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-228">A compilation unit or a namespace body can contain *namespace_member_declaration*s, and such declarations contribute new members to the underlying declaration space of the containing compilation unit or namespace body.</span></span>

## <a name="type-declarations"></a><span data-ttu-id="08cc1-229">Объявления типов</span><span class="sxs-lookup"><span data-stu-id="08cc1-229">Type declarations</span></span>

<span data-ttu-id="08cc1-230">Объект *type_declaration* — *class_declaration* ([объявлений классов](classes.md#class-declarations)), *struct_declaration* ([структуры объявления](structs.md#struct-declarations)), *interface_declaration* ([объявления интерфейсов](interfaces.md#interface-declarations)), *enum_declaration* ([Enum объявления](enums.md#enum-declarations)), или *delegate_declaration* ([объявления делегатов](delegates.md#delegate-declarations)).</span><span class="sxs-lookup"><span data-stu-id="08cc1-230">A *type_declaration* is a *class_declaration* ([Class declarations](classes.md#class-declarations)), a *struct_declaration* ([Struct declarations](structs.md#struct-declarations)), an *interface_declaration* ([Interface declarations](interfaces.md#interface-declarations)), an *enum_declaration* ([Enum declarations](enums.md#enum-declarations)), or a *delegate_declaration* ([Delegate declarations](delegates.md#delegate-declarations)).</span></span>

```antlr
type_declaration
    : class_declaration
    | struct_declaration
    | interface_declaration
    | enum_declaration
    | delegate_declaration
    ;
```

<span data-ttu-id="08cc1-231">Объект *type_declaration* может возникнуть объявлением верхнего уровня в единице компиляции или объявлением члена внутри пространства имен, класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="08cc1-231">A *type_declaration* can occur as a top-level declaration in a compilation unit or as a member declaration within a namespace, class, or struct.</span></span>

<span data-ttu-id="08cc1-232">Если объявление типа для типа `T` происходит объявлением верхнего уровня в единице компиляции, полное имя вновь объявленного типа является просто `T`.</span><span class="sxs-lookup"><span data-stu-id="08cc1-232">When a type declaration for a type `T` occurs as a top-level declaration in a compilation unit, the fully qualified name of the newly declared type is simply `T`.</span></span> <span data-ttu-id="08cc1-233">Если объявление типа для типа `T` содержится в пространстве имен, класса или структуры, полное имя типа вновь объявленное `N.T`, где `N` полное имя вмещающего пространства имен, класса или структуры.</span><span class="sxs-lookup"><span data-stu-id="08cc1-233">When a type declaration for a type `T` occurs within a namespace, class, or struct, the fully qualified name of the newly declared type is `N.T`, where `N` is the fully qualified name of the containing namespace, class, or struct.</span></span>

<span data-ttu-id="08cc1-234">Тип, объявленный в пределах класса или структуры, называется вложенным типом ([вложенные типы](classes.md#nested-types)).</span><span class="sxs-lookup"><span data-stu-id="08cc1-234">A type declared within a class or struct is called a nested type ([Nested types](classes.md#nested-types)).</span></span>

<span data-ttu-id="08cc1-235">Разрешенные модификаторы доступа и доступ по умолчанию для объявления типа зависит от контекста, в котором происходит объявление ([объявленную доступность](basic-concepts.md#declared-accessibility)):</span><span class="sxs-lookup"><span data-stu-id="08cc1-235">The permitted access modifiers and the default access for a type declaration depend on the context in which the declaration takes place ([Declared accessibility](basic-concepts.md#declared-accessibility)):</span></span>

*  <span data-ttu-id="08cc1-236">Типы, объявленные в единицах компиляции или пространства имен могут иметь `public` или `internal` доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-236">Types declared in compilation units or namespaces can have `public` or `internal` access.</span></span> <span data-ttu-id="08cc1-237">По умолчанию используется `internal` доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-237">The default is `internal` access.</span></span>
*  <span data-ttu-id="08cc1-238">Типы, объявленные в классах могут иметь `public`, `protected internal`, `protected`, `internal`, или `private` доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-238">Types declared in classes can have `public`, `protected internal`, `protected`, `internal`, or `private` access.</span></span> <span data-ttu-id="08cc1-239">По умолчанию используется `private` доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-239">The default is `private` access.</span></span>
*  <span data-ttu-id="08cc1-240">Типы, объявленные в структурах может иметь `public`, `internal`, или `private` доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-240">Types declared in structs can have `public`, `internal`, or `private` access.</span></span> <span data-ttu-id="08cc1-241">По умолчанию используется `private` доступа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-241">The default is `private` access.</span></span>

## <a name="namespace-alias-qualifiers"></a><span data-ttu-id="08cc1-242">Квалификаторы псевдонима пространства имен</span><span class="sxs-lookup"><span data-stu-id="08cc1-242">Namespace alias qualifiers</span></span>

<span data-ttu-id="08cc1-243">***Квалификатор псевдонима пространства имен*** `::` делает возможным гарантирует, что поиск имени типа не влияет на общие сведения о новых типов и членов.</span><span class="sxs-lookup"><span data-stu-id="08cc1-243">The ***namespace alias qualifier*** `::` makes it possible to guarantee that type name lookups are unaffected by the introduction of new types and members.</span></span> <span data-ttu-id="08cc1-244">Квалификатор псевдонима пространства имен всегда появляется между двумя идентификаторами, которые называют идентификаторы левую и правую.</span><span class="sxs-lookup"><span data-stu-id="08cc1-244">The namespace alias qualifier always appears between two identifiers referred to as the left-hand and right-hand identifiers.</span></span> <span data-ttu-id="08cc1-245">В отличие от обычного `.` квалификатор, слева идентификатор `::` квалификатор осуществляется только как extern или с помощью псевдонима.</span><span class="sxs-lookup"><span data-stu-id="08cc1-245">Unlike the regular `.` qualifier, the left-hand identifier of the `::` qualifier is looked up only as an extern or using alias.</span></span>

<span data-ttu-id="08cc1-246">Объект *qualified_alias_member* определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="08cc1-246">A *qualified_alias_member* is defined as follows:</span></span>

```antlr
qualified_alias_member
    : identifier '::' identifier type_argument_list?
    ;
```

<span data-ttu-id="08cc1-247">Объект *qualified_alias_member* можно использовать в качестве *namespace_or_type_name* ([пространства имен и тип](basic-concepts.md#namespace-and-type-names)) или как левый операнд в *member_access* ([Доступ к членам](expressions.md#member-access)).</span><span class="sxs-lookup"><span data-stu-id="08cc1-247">A *qualified_alias_member* can be used as a *namespace_or_type_name* ([Namespace and type names](basic-concepts.md#namespace-and-type-names)) or as the left operand in a *member_access* ([Member access](expressions.md#member-access)).</span></span>

<span data-ttu-id="08cc1-248">Объект *qualified_alias_member* имеет одну из двух форм:</span><span class="sxs-lookup"><span data-stu-id="08cc1-248">A *qualified_alias_member* has one of two forms:</span></span>

*  <span data-ttu-id="08cc1-249">`N::I<A1, ..., Ak>`, где `N` и `I` представляют идентификаторы, и `<A1, ..., Ak>` — список аргументов типа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-249">`N::I<A1, ..., Ak>`, where `N` and `I` represent identifiers, and `<A1, ..., Ak>` is a type argument list.</span></span> <span data-ttu-id="08cc1-250">(`K` всегда имеет по крайней мере одно.)</span><span class="sxs-lookup"><span data-stu-id="08cc1-250">(`K` is always at least one.)</span></span>
*  <span data-ttu-id="08cc1-251">`N::I`, где `N` и `I` представляют идентификаторы.</span><span class="sxs-lookup"><span data-stu-id="08cc1-251">`N::I`, where `N` and `I` represent identifiers.</span></span> <span data-ttu-id="08cc1-252">(В этом случае `K` считается равным 0.)</span><span class="sxs-lookup"><span data-stu-id="08cc1-252">(In this case, `K` is considered to be zero.)</span></span>

<span data-ttu-id="08cc1-253">При использовании этой нотации значение *qualified_alias_member* определяется следующим образом:</span><span class="sxs-lookup"><span data-stu-id="08cc1-253">Using this notation, the meaning of a *qualified_alias_member* is determined as follows:</span></span>

*  <span data-ttu-id="08cc1-254">Если `N` идентификатор `global`, а затем выполняется поиск глобальное пространство имен `I`:</span><span class="sxs-lookup"><span data-stu-id="08cc1-254">If `N` is the identifier `global`, then the global namespace is searched for `I`:</span></span>
   * <span data-ttu-id="08cc1-255">Если глобальное пространство имен содержит пространство имен с именем `I` и `K` равен нулю, то *qualified_alias_member* ссылается на это пространство имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-255">If the global namespace contains a namespace named `I` and `K` is zero, then the *qualified_alias_member* refers to that namespace.</span></span>
   * <span data-ttu-id="08cc1-256">В противном случае, если глобальное пространство имен содержит не универсальный тип с именем `I` и `K` равен нулю, то *qualified_alias_member* ссылается на этот тип.</span><span class="sxs-lookup"><span data-stu-id="08cc1-256">Otherwise, if the global namespace contains a non-generic type named `I` and `K` is zero, then the *qualified_alias_member* refers to that type.</span></span>
   * <span data-ttu-id="08cc1-257">В противном случае, если глобальное пространство имен содержит тип с именем `I` с `K`  параметры типа, а затем *qualified_alias_member* ссылается на этот тип, сформированный с заданными аргументами типа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-257">Otherwise, if the global namespace contains a type named `I` that has `K` type parameters, then the *qualified_alias_member* refers to that type constructed with the given type arguments.</span></span>
   * <span data-ttu-id="08cc1-258">В противном случае *qualified_alias_member* — не определено и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-258">Otherwise, the *qualified_alias_member* is undefined and a compile-time error occurs.</span></span>

*  <span data-ttu-id="08cc1-259">В противном случае — начиная с объявление пространства имен ([объявления пространств имен](namespaces.md#namespace-declarations)), непосредственно содержащего *qualified_alias_member* (если таковые имеются), продолжение с каждого включающего объявления пространства имен (если таковые имеются) и заканчивая единицей компиляции, содержащей *qualified_alias_member*, оцениваются следующие действия, пока не будет обнаружена сущность:</span><span class="sxs-lookup"><span data-stu-id="08cc1-259">Otherwise, starting with the namespace declaration ([Namespace declarations](namespaces.md#namespace-declarations)) immediately containing the *qualified_alias_member* (if any), continuing with each enclosing namespace declaration (if any), and ending with the compilation unit containing the *qualified_alias_member*, the following steps are evaluated until an entity is located:</span></span>

   * <span data-ttu-id="08cc1-260">Если пространство имен объявление или блоке компиляции содержит *using_alias_directive* , связывающая `N` с типом, а затем *qualified_alias_member* не определен и во время компиляции возникает ошибка.</span><span class="sxs-lookup"><span data-stu-id="08cc1-260">If the namespace declaration or compilation unit contains a *using_alias_directive* that associates `N` with a type, then the *qualified_alias_member* is undefined and a compile-time error occurs.</span></span>
   * <span data-ttu-id="08cc1-261">В противном случае, если единица объявления или компиляции пространство имен содержит *extern_alias_directive* или *using_alias_directive* , связывающая `N` с пространством имен, затем:</span><span class="sxs-lookup"><span data-stu-id="08cc1-261">Otherwise, if the namespace declaration or compilation unit contains an *extern_alias_directive* or *using_alias_directive* that associates `N` with a namespace, then:</span></span>
     * <span data-ttu-id="08cc1-262">Если пространство имен, связанное с `N` содержит пространство имен с именем `I` и `K` равен нулю, то *qualified_alias_member* ссылается на это пространство имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-262">If the namespace associated with `N` contains a namespace named `I` and `K` is zero, then the *qualified_alias_member* refers to that namespace.</span></span>
     * <span data-ttu-id="08cc1-263">В противном случае, если пространство имен, связанное с `N` содержит не универсальный тип с именем `I` и `K` равен нулю, то *qualified_alias_member* ссылается на этот тип.</span><span class="sxs-lookup"><span data-stu-id="08cc1-263">Otherwise, if the namespace associated with `N` contains a non-generic type named `I` and `K` is zero, then the *qualified_alias_member* refers to that type.</span></span>
     * <span data-ttu-id="08cc1-264">В противном случае, если пространство имен, связанное с `N` содержит тип с именем `I` с `K`  параметры типа, а затем *qualified_alias_member* ссылается на тип, сформированный с аргументы данного типа.</span><span class="sxs-lookup"><span data-stu-id="08cc1-264">Otherwise, if the namespace associated with `N` contains a type named `I` that has `K` type parameters, then the *qualified_alias_member* refers to that type constructed with the given type arguments.</span></span>
     * <span data-ttu-id="08cc1-265">В противном случае *qualified_alias_member* — не определено и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-265">Otherwise, the *qualified_alias_member* is undefined and a compile-time error occurs.</span></span>
*  <span data-ttu-id="08cc1-266">В противном случае *qualified_alias_member* — не определено и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-266">Otherwise, the *qualified_alias_member* is undefined and a compile-time error occurs.</span></span>

<span data-ttu-id="08cc1-267">Обратите внимание на то, что с помощью квалификатор псевдонима пространства имен с псевдонимом, ссылающимся на тип приводит к ошибке времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-267">Note that using the namespace alias qualifier with an alias that references a type causes a compile-time error.</span></span> <span data-ttu-id="08cc1-268">Также Обратите внимание, что если идентификатор `N` — `global`, а затем выполняется поиск в глобальном пространстве имен, даже если существует псевдоним using, связывающий `global` с типа или пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-268">Also note that if the identifier `N` is `global`, then lookup is performed in the global namespace, even if there is a using alias associating `global` with a type or namespace.</span></span>

### <a name="uniqueness-of-aliases"></a><span data-ttu-id="08cc1-269">Уникальность псевдонимов</span><span class="sxs-lookup"><span data-stu-id="08cc1-269">Uniqueness of aliases</span></span>

<span data-ttu-id="08cc1-270">Каждой компиляции модульных и пространство имен текст имеет отдельную область объявления для псевдонимов extern и использования псевдонимов.</span><span class="sxs-lookup"><span data-stu-id="08cc1-270">Each compilation unit and namespace body has a separate declaration space for extern aliases and using aliases.</span></span> <span data-ttu-id="08cc1-271">Таким образом, хотя имя псевдонима extern или с помощью псевдонима должно быть уникальным в пределах набора внешние псевдонимы и псевдонимы using объявленных в непосредственно содержащей единицы компиляции или пространстве имен тела, псевдоним может иметь имя, совпадающее с именем типа или пространства имен, при условии, я t используется только с `::` квалификатор.</span><span class="sxs-lookup"><span data-stu-id="08cc1-271">Thus, while the name of an extern alias or using alias must be unique within the set of extern aliases and using aliases declared in the immediately containing compilation unit or namespace body, an alias is permitted to have the same name as a type or namespace as long as it is used only with the `::` qualifier.</span></span>

<span data-ttu-id="08cc1-272">В примере</span><span class="sxs-lookup"><span data-stu-id="08cc1-272">In the example</span></span>
```csharp
namespace N
{
    public class A {}

    public class B {}
}

namespace N
{
    using A = System.IO;

    class X
    {
        A.Stream s1;            // Error, A is ambiguous

        A::Stream s2;           // Ok
    }
}
```
<span data-ttu-id="08cc1-273">имя `A` имеет два значения в тексте второго пространства имен, так как оба класса `A` и с помощью псевдонима `A` находятся в области действия.</span><span class="sxs-lookup"><span data-stu-id="08cc1-273">the name `A` has two possible meanings in the second namespace body because both the class `A` and the using alias `A` are in scope.</span></span> <span data-ttu-id="08cc1-274">По этой причине использование `A` в полном имени `A.Stream` является неоднозначным и возникает ошибка времени компиляции.</span><span class="sxs-lookup"><span data-stu-id="08cc1-274">For this reason, use of `A` in the qualified name `A.Stream` is ambiguous and causes a compile-time error to occur.</span></span> <span data-ttu-id="08cc1-275">Однако использование `A` с `::` квалификатора не является ошибкой, поскольку `A` выполняется поиск только в качестве псевдонима пространства имен.</span><span class="sxs-lookup"><span data-stu-id="08cc1-275">However, use of `A` with the `::` qualifier is not an error because `A` is looked up only as a namespace alias.</span></span>
