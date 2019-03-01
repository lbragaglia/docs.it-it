---
title: Personalizzazione del marshalling delle strutture - .NET
description: Informazioni su come personalizzare il modo in cui .NET effettua il marshalling delle strutture in una rappresentazione nativa.
author: jkoritzinsky
ms.author: jekoritz
ms.date: 01/18/2019
dev_langs:
- csharp
- cpp
ms.openlocfilehash: c4d2d84a59aebedda2d1e6380caeef170051c0a3
ms.sourcegitcommit: b56d59ad42140d277f2acbd003b74d655fdbc9f1
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/19/2019
ms.locfileid: "56411441"
---
# <a name="customizing-structure-marshalling"></a><span data-ttu-id="63509-103">Personalizzazione del marshalling delle strutture</span><span class="sxs-lookup"><span data-stu-id="63509-103">Customizing structure marshalling</span></span>

<span data-ttu-id="63509-104">In alcuni casi le regole di marshalling predefinite per le strutture non sono esattamente quelle necessarie.</span><span class="sxs-lookup"><span data-stu-id="63509-104">Sometimes the default marshalling rules for structures aren't exactly what you need.</span></span> <span data-ttu-id="63509-105">I runtime .NET offrono alcuni punti di estensione per poter personalizzare il layout della struttura e la modalità di marshalling dei campi.</span><span class="sxs-lookup"><span data-stu-id="63509-105">The .NET runtimes provide a few extension points for you to customize your structure's layout and how fields are marshaled.</span></span>

## <a name="customizing-structure-layout"></a><span data-ttu-id="63509-106">Personalizzazione del layout della struttura</span><span class="sxs-lookup"><span data-stu-id="63509-106">Customizing structure layout</span></span>

<span data-ttu-id="63509-107">.NET offre l'attributo <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> e l'enumerazione <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=nameWithType> per consentire di personalizzare il modo in cui i campi vengono inseriti nella memoria.</span><span class="sxs-lookup"><span data-stu-id="63509-107">.NET provides the <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType> attribute and the <xref:System.Runtime.InteropServices.LayoutKind?displayProperty=nameWithType> enumeration to allow you to customize how fields are placed in memory.</span></span> <span data-ttu-id="63509-108">Le linee guida seguenti saranno utili per evitare problemi comuni.</span><span class="sxs-lookup"><span data-stu-id="63509-108">The following guidance will help you avoid common issues.</span></span>

<span data-ttu-id="63509-109">**✔️ PRENDERE IN CONSIDERAZIONE** l'uso di `LayoutKind.Sequential` laddove possibile.</span><span class="sxs-lookup"><span data-stu-id="63509-109">**✔️ CONSIDER** using `LayoutKind.Sequential` whenever possible.</span></span>

<span data-ttu-id="63509-110">**✔️ USARE** solo `LayoutKind.Explicit` nel marshalling quando lo struct nativo ha anche un layout esplicito, ad esempio un'unione.</span><span class="sxs-lookup"><span data-stu-id="63509-110">**✔️ DO** only use `LayoutKind.Explicit` in marshalling when your native struct is also has an explicit layout, such as a union.</span></span>

<span data-ttu-id="63509-111">**❌ EVITARE** di usare `LayoutKind.Explicit` per il marshalling delle strutture in piattaforme non Windows.</span><span class="sxs-lookup"><span data-stu-id="63509-111">**❌ AVOID** using `LayoutKind.Explicit` when marshalling structures on non-Windows platforms.</span></span> <span data-ttu-id="63509-112">Il runtime di .NET Core non supporta il passaggio di strutture esplicite per valore a funzioni native in sistemi non Windows Intel o AMD a 64 bit.</span><span class="sxs-lookup"><span data-stu-id="63509-112">The .NET Core runtime doesn't support passing explicit structures by value to native functions on Intel or AMD 64-bit non-Windows systems.</span></span> <span data-ttu-id="63509-113">Tuttavia, il runtime supporta il passaggio di strutture esplicite per riferimento in tutte le piattaforme.</span><span class="sxs-lookup"><span data-stu-id="63509-113">However, the runtime supports passing explicit structures by reference on all platforms.</span></span>

## <a name="customizing-boolean-field-marshalling"></a><span data-ttu-id="63509-114">Personalizzazione del marshalling di campi booleani</span><span class="sxs-lookup"><span data-stu-id="63509-114">Customizing boolean field marshalling</span></span>

<span data-ttu-id="63509-115">Il codice nativo include molte rappresentazioni booleane diverse.</span><span class="sxs-lookup"><span data-stu-id="63509-115">Native code has many different boolean representations.</span></span> <span data-ttu-id="63509-116">Solo in Windows esistono tre modi per rappresentare valori booleani.</span><span class="sxs-lookup"><span data-stu-id="63509-116">On Windows alone, there are three ways to represent boolean values.</span></span> <span data-ttu-id="63509-117">Il runtime non conosce la definizione nativa della struttura, quindi può al massimo fare supposizioni su come effettuare il marshalling dei valori booleani.</span><span class="sxs-lookup"><span data-stu-id="63509-117">The runtime doesn't know the native definition of your structure, so the best it can do is make a guess on how to marshal your boolean values.</span></span> <span data-ttu-id="63509-118">Il runtime .NET offre un modo per indicare come effettuare il marshalling del campo booleano.</span><span class="sxs-lookup"><span data-stu-id="63509-118">The .NET runtime provides a way to indicate how to marshal your boolean field.</span></span> <span data-ttu-id="63509-119">Gli esempi seguenti illustrano come eseguire il marshalling del tipo `bool` .NET in diversi tipi booleani nativi.</span><span class="sxs-lookup"><span data-stu-id="63509-119">The following examples show how to marshal .NET `bool` to different native boolean types.</span></span>

<span data-ttu-id="63509-120">Per impostazione predefinita, il marshalling dei valori booleani viene effettuato come valore [`BOOL`](/windows/desktop/winprog/windows-data-types#BOOL) Win32 a 4 byte nativo, come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="63509-120">Boolean values default to marshalling as a native 4-byte Win32 [`BOOL`](/windows/desktop/winprog/windows-data-types#BOOL) value as shown in the following example:</span></span>

```csharp
public struct WinBool
{
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

<span data-ttu-id="63509-121">Se si vuole essere espliciti, è possibile usare il valore <xref:System.Runtime.InteropServices.UnmanagedType.Bool?displayProperty=nameWithType> per ottenere lo stesso comportamento illustrato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="63509-121">If you want to be explicit, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.Bool?displayProperty=nameWithType> value to get the same behavior as above:</span></span>

```csharp
public struct WinBool
{
    [MarshalAs(UnmanagedType.Bool)]
    public bool b;
}
```

```cpp
struct WinBool
{
    public BOOL b;
};
```

<span data-ttu-id="63509-122">Usando i valori `UmanagedType.U1` o `UnmanagedType.I1` di seguito, è possibile indicare al runtime di effettuare il marshalling del campo `b` come tipo `bool` nativo a 1 byte.</span><span class="sxs-lookup"><span data-stu-id="63509-122">Using the `UmanagedType.U1` or `UnmanagedType.I1` values below, you can tell the runtime to marshal the `b` field as a 1-byte native `bool` type.</span></span>

```csharp
public struct CBool
{
    [MarshalAs(UnmanagedType.U1)]
    public bool b;
}
```

```cpp
struct CBool
{
    public bool b;
};
```

<span data-ttu-id="63509-123">In Windows, è possibile usare il valore <xref:System.Runtime.InteropServices.UnmanagedType.VariantBool?displayProperty=nameWithType> per indicare al runtime di effettuare il marshalling del valore booleano in un valore `VARIANT_BOOL` a 2 byte:</span><span class="sxs-lookup"><span data-stu-id="63509-123">On Windows, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.VariantBool?displayProperty=nameWithType> value to tell the runtime to marshal your boolean value to a 2-byte `VARIANT_BOOL` value:</span></span>

```csharp
public struct VariantBool
{
    [MarshalAs(UnmanagedType.VariantBool)]
    public bool b;
}
```

```cpp
struct VariantBool
{
    public VARIANT_BOOL b;
};
```

> [!NOTE]
> <span data-ttu-id="63509-124">`VARIANT_BOOL` è diverso dalla maggior parte dei tipi bool in quanto `VARIANT_TRUE = -1` e `VARIANT_FALSE = 0`.</span><span class="sxs-lookup"><span data-stu-id="63509-124">`VARIANT_BOOL` is different than most bool types in that `VARIANT_TRUE = -1` and `VARIANT_FALSE = 0`.</span></span> <span data-ttu-id="63509-125">Inoltre, tutti i valori che non sono uguali a `VARIANT_TRUE` sono considerati false.</span><span class="sxs-lookup"><span data-stu-id="63509-125">Additionally, all values that aren't equal to `VARIANT_TRUE` are considered false.</span></span>

## <a name="customizing-array-field-marshalling"></a><span data-ttu-id="63509-126">Personalizzazione del marshalling delle matrici</span><span class="sxs-lookup"><span data-stu-id="63509-126">Customizing array field marshalling</span></span>

<span data-ttu-id="63509-127">.NET include anche alcuni modi per personalizzare il marshalling delle matrici.</span><span class="sxs-lookup"><span data-stu-id="63509-127">.NET also includes a few ways to customize array marshalling.</span></span>

<span data-ttu-id="63509-128">Per impostazione predefinita, .NET effettua il marshalling delle matrici come puntatore a un elenco di elementi contigui:</span><span class="sxs-lookup"><span data-stu-id="63509-128">By default, .NET marshals arrays as a pointer to a contiguous list of the elements:</span></span>

```csharp
public struct DefaultArray
{
    public int[] values;
}
```

```cpp
struct DefaultArray
{
    int* values;
};
```

<span data-ttu-id="63509-129">Per interfacciarsi con le API COM, potrebbe essere necessario effettuare il marshalling delle matrici come oggetti `SAFEARRAY*`.</span><span class="sxs-lookup"><span data-stu-id="63509-129">If you're interfacing with COM APIs, you may have to marshal arrays as `SAFEARRAY*` objects.</span></span> <span data-ttu-id="63509-130">È possibile usare <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> e il valore <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> per indicare al runtime di effettuare il marshalling di una matrice come `SAFEARRAY*`:</span><span class="sxs-lookup"><span data-stu-id="63509-130">You can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> and the <xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=nameWithType> value to tell the runtime to marshal an array as a `SAFEARRAY*`:</span></span>

```csharp
public struct SafeArrayExample
{
    [MarshalAs(UnmanagedType.SafeArray)]
    public int[] values;
}
```

```cpp
struct SafeArrayExample
{
    SAFEARRAY* values;
};
```

<span data-ttu-id="63509-131">Se è necessario personalizzare il tipo di elemento presente in `SAFEARRAY`, è possibile usare i campi <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> e <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> per personalizzare il tipo di elemento esatto di `SAFEARRAY`.</span><span class="sxs-lookup"><span data-stu-id="63509-131">If you need to customize what type of element is in the `SAFEARRAY`, then you can use the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArraySubType?displayProperty=nameWithType> and <xref:System.Runtime.InteropServices.MarshalAsAttribute.SafeArrayUserDefinedSubType?displayProperty=nameWithType> fields to customize the exact element type of the `SAFEARRAY`.</span></span>

<span data-ttu-id="63509-132">Se è necessario effettuare il marshalling della matrice sul posto, è possibile usare il valore <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> per indicare al gestore di marshalling di effettuare il marshalling della matrice sul posto.</span><span class="sxs-lookup"><span data-stu-id="63509-132">If you need to marshal the array in-place, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=nameWithType> value to tell the marshaler to marshal the array in-place.</span></span> <span data-ttu-id="63509-133">Quando si usa questo tipo di marshalling, è anche necessario fornire un valore al campo <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> per il numero di elementi nella matrice, in modo che il runtime possa allocare correttamente spazio per la struttura.</span><span class="sxs-lookup"><span data-stu-id="63509-133">When you're using this marshalling, you also must supply a value to the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> field  for the number of elements in the array so the runtime can correctly allocate space for the structure.</span></span>

```csharp
public struct InPlaceArray
{
    [MarshalAs(UnmanagedType.ByValArray, SizeConst = 4)]
    public int[] values;
}
```

```cpp
struct InPlaceArray
{
    int values[4];
};
```

> [!NOTE]
> <span data-ttu-id="63509-134">.NET non supporta il marshalling di un campo di matrice di lunghezza variabile come membro di matrice flessibile C99.</span><span class="sxs-lookup"><span data-stu-id="63509-134">.NET doesn't support marshalling a variable length array field as a C99 Flexible Array Member.</span></span>

## <a name="customizing-string-field-marshalling"></a><span data-ttu-id="63509-135">Personalizzazione del marshalling dei campi stringa</span><span class="sxs-lookup"><span data-stu-id="63509-135">Customizing string field marshalling</span></span>

<span data-ttu-id="63509-136">.NET offre anche un'ampia gamma di personalizzazioni per il marshalling dei campi stringa.</span><span class="sxs-lookup"><span data-stu-id="63509-136">.NET also provides a wide variety of customizations for marshalling string fields.</span></span>

<span data-ttu-id="63509-137">Per impostazione predefinita, .NET effettua il marshalling di una stringa come un puntatore a una stringa con terminazione Null.</span><span class="sxs-lookup"><span data-stu-id="63509-137">By default, .NET marshals a string as a pointer to a null-terminated string.</span></span> <span data-ttu-id="63509-138">La codifica dipende dal valore del campo <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> in <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="63509-138">The encoding depends on the value of the <xref:System.Runtime.InteropServices.StructLayoutAttribute.CharSet?displayProperty=nameWithType> field in the <xref:System.Runtime.InteropServices.StructLayoutAttribute?displayProperty=nameWithType>.</span></span> <span data-ttu-id="63509-139">Se non viene specificato alcun attributo, viene usata la codifica predefinita ANSI.</span><span class="sxs-lookup"><span data-stu-id="63509-139">If no attribute is specified, the encoding defaults to an ANSI encoding.</span></span>

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char* str;
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

<span data-ttu-id="63509-140">Se è necessario usare codifiche differenti per campi diversi oppure semplicemente si preferisce essere più espliciti nella definizione dello struct, è possibile usare i valori <xref:System.Runtime.InteropServices.UnmanagedType.LPStr?displayProperty=nameWithType> o <xref:System.Runtime.InteropServices.UnmanagedType.LPWStr?displayProperty=nameWithType> per un attributo <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="63509-140">If you need to use different encodings for different fields or just prefer to be more explicit in your struct definition, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.LPStr?displayProperty=nameWithType> or <xref:System.Runtime.InteropServices.UnmanagedType.LPWStr?displayProperty=nameWithType> values on a <xref:System.Runtime.InteropServices.MarshalAsAttribute?displayProperty=nameWithType> attribute.</span></span>

```csharp
public struct AnsiString
{
    [MarshalAs(UnmanagedType.LPStr)]
    public string str;
}
```

```cpp
struct AnsiString
{
    char* str;
};
```

```csharp
public struct UnicodeString
{
    [MarshalAs(UnmanagedType.LPWStr)]
    public string str;
}
```

```cpp
struct UnicodeString
{
    char16_t* str; // Could also be wchar_t* on Windows.
};
```

<span data-ttu-id="63509-141">Se si vuole effettuare il marshalling delle stringhe con la codifica UTF-8, è possibile usare il valore <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> in <xref:System.Runtime.InteropServices.MarshalAsAttribute>.</span><span class="sxs-lookup"><span data-stu-id="63509-141">If you want to marshal your strings using the UTF-8 encoding, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> value in your <xref:System.Runtime.InteropServices.MarshalAsAttribute>.</span></span>


```csharp
public struct UTF8String
{
    [MarshalAs(UnmanagedType.LPUTF8Str)]
    public string str;
}
```

```cpp
struct UTF8String
{
    char* str;
};
```

> [!NOTE]
> <span data-ttu-id="63509-142">L'uso di <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> richiede .NET Framework 4.7 (o versioni successive) o .NET Core 1.1 (o versioni successive).</span><span class="sxs-lookup"><span data-stu-id="63509-142">Using <xref:System.Runtime.InteropServices.UnmanagedType.LPUTF8Str?displayProperty=nameWithType> requires either .NET Framework 4.7 (or later versions) or .NET Core 1.1 (or later versions).</span></span> <span data-ttu-id="63509-143">Non è disponibile in .NET Standard 2.0.</span><span class="sxs-lookup"><span data-stu-id="63509-143">It isn't available in .NET Standard 2.0.</span></span>

<span data-ttu-id="63509-144">Se si utilizzano API COM, potrebbe essere necessario effettuare il marshalling di una stringa come `BSTR`.</span><span class="sxs-lookup"><span data-stu-id="63509-144">If you're working with COM APIs, you may need to marshal a string as a `BSTR`.</span></span> <span data-ttu-id="63509-145">Usando il valore <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> è possibile effettuare il marshalling di una stringa come `BSTR`.</span><span class="sxs-lookup"><span data-stu-id="63509-145">Using the <xref:System.Runtime.InteropServices.UnmanagedType.BStr?displayProperty=nameWithType> value, you can marshal a string as a `BSTR`.</span></span>

```csharp
public struct BString
{
    [MarshalAs(UnmanagedType.BStr)]
    public string str;
}
```

```cpp
struct BString
{
    BSTR str;
};
```

<span data-ttu-id="63509-146">Quando si usa un'API basata su WinRT, potrebbe essere necessario effettuare il marshalling di una stringa come `HSTRING`.</span><span class="sxs-lookup"><span data-stu-id="63509-146">When using a WinRT-based API, you may need to marshal a string as an `HSTRING`.</span></span>  <span data-ttu-id="63509-147">Usando il valore <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> è possibile effettuare il marshalling di una stringa come `HSTRING`.</span><span class="sxs-lookup"><span data-stu-id="63509-147">Using the <xref:System.Runtime.InteropServices.UnmanagedType.HString?displayProperty=nameWithType> value, you can marshal a string as a `HSTRING`.</span></span>

```csharp
public struct HString
{
    [MarshalAs(UnmanagedType.HString)]
    public string str;
}
```

```cpp
struct BString
{
    HSTRING str;
};
```

<span data-ttu-id="63509-148">Se l'API richiede di passare la stringa sul posto nella struttura, è possibile usare il valore <xref:System.Runtime.InteropServices.UnmanagedType.ByValTStr?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="63509-148">If your API requires you to pass the string in-place in the structure, you can use the <xref:System.Runtime.InteropServices.UnmanagedType.ByValTStr?displayProperty=nameWithType> value.</span></span> <span data-ttu-id="63509-149">Si noti che la codifica per una stringa sottoposta a marshalling con `ByValTStr` è determinata dall'attributo `CharSet`.</span><span class="sxs-lookup"><span data-stu-id="63509-149">Do note that the encoding for a string marshalled by `ByValTStr` is determined from the `CharSet` attribute.</span></span> <span data-ttu-id="63509-150">È inoltre richiesto il passaggio della lunghezza della stringa con il campo <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="63509-150">Additionally, it requires that a string length is passed by the <xref:System.Runtime.InteropServices.MarshalAsAttribute.SizeConst?displayProperty=nameWithType> field.</span></span>

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Ansi)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char str[4];
};
```

```csharp
[StructLayout(LayoutKind.Sequential, CharSet = CharSet.Unicode)]
public struct DefaultString
{
    [MarshalAs(UnmanagedType.ByValTStr, SizeConst = 4)]
    public string str;
}
```

```cpp
struct DefaultString
{
    char16_t str[4]; // Could also be wchar_t[4] on Windows.
};
```

## <a name="customizing-decimal-field-marshalling"></a><span data-ttu-id="63509-151">Personalizzazione del marshalling dei campi decimali</span><span class="sxs-lookup"><span data-stu-id="63509-151">Customizing decimal field marshalling</span></span>

<span data-ttu-id="63509-152">In Windows è possibile riscontrare alcune API che usano la struttura [`CY` o `CURRENCY`](/windows/desktop/api/wtypes/ns-wtypes-tagcy) nativa.</span><span class="sxs-lookup"><span data-stu-id="63509-152">If you're working on Windows, you might encounter some APIs that use the native [`CY` or `CURRENCY`](/windows/desktop/api/wtypes/ns-wtypes-tagcy) structure.</span></span> <span data-ttu-id="63509-153">Per impostazione predefinita, il tipo .NET `decimal` effettua il marshalling nella struttura [`DECIMAL`](/windows/desktop/api/wtypes/ns-wtypes-tagdec) nativa.</span><span class="sxs-lookup"><span data-stu-id="63509-153">By default, the .NET `decimal` type marshals to the native [`DECIMAL`](/windows/desktop/api/wtypes/ns-wtypes-tagdec) structure.</span></span> <span data-ttu-id="63509-154">Tuttavia, è possibile usare un <xref:System.Runtime.InteropServices.MarshalAsAttribute> con il valore <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=nameWithType> per indicare al gestore di marshalling di convertire un valore `decimal` in un valore `CY` nativo.</span><span class="sxs-lookup"><span data-stu-id="63509-154">However, you can use a <xref:System.Runtime.InteropServices.MarshalAsAttribute> with the <xref:System.Runtime.InteropServices.UnmanagedType.Currency?displayProperty=nameWithType> value to instruct the marshaler to convert a `decimal` value to a native `CY` value.</span></span>

```csharp
public struct Currency
{
    [MarshalAs(UnmanagedType.Currency)]
    public decimal dec;
}
```

```cpp
struct Currency
{
    CY dec;
};
```

## <a name="marshalling-systemobjects"></a><span data-ttu-id="63509-155">Marshalling di `System.Object`</span><span class="sxs-lookup"><span data-stu-id="63509-155">Marshalling `System.Object`s</span></span>

<span data-ttu-id="63509-156">In Windows è possibile effettuare il marshalling di campi di tipo `object` in codice nativo.</span><span class="sxs-lookup"><span data-stu-id="63509-156">On Windows, you can marshal `object`-typed fields to native code.</span></span> <span data-ttu-id="63509-157">È possibile effettuare il marshalling di questi campi in uno di tre tipi:</span><span class="sxs-lookup"><span data-stu-id="63509-157">You can marshal these fields to one of three types:</span></span>
- [`VARIANT`](/windows/desktop/api/oaidl/ns-oaidl-tagvariant)
- [`IUnknown*`](/windows/desktop/api/unknwn/nn-unknwn-iunknown)
- <span data-ttu-id="63509-158">[`IDispatch*`](/windows/desktop/api/oaidl/nn-oaidl-idispatch).</span><span class="sxs-lookup"><span data-stu-id="63509-158">[`IDispatch*`](/windows/desktop/api/oaidl/nn-oaidl-idispatch).</span></span> 

<span data-ttu-id="63509-159">Per impostazione predefinita, un campo di tipo `object` verrà sottoposto a marshalling come `IUnknown*` che esegue il wrapping dell'oggetto.</span><span class="sxs-lookup"><span data-stu-id="63509-159">By default, an `object`-typed field will be marshalled to an `IUnknown*` that wraps the object.</span></span>

```csharp
public struct ObjectDefault
{
    public object obj;
}
```

```cpp
struct ObjectDefault
{
    IUnknown* obj;
};
```

<span data-ttu-id="63509-160">Se si vuole effettuare il marshalling di un campo oggetto come `IDispatch*`, aggiungere un <xref:System.Runtime.InteropServices.MarshalAsAttribute> con il valore <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="63509-160">If you want to marshal an object field to an `IDispatch*`, add a <xref:System.Runtime.InteropServices.MarshalAsAttribute> with the <xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=nameWithType> value.</span></span>

```csharp
public struct ObjectDispatch
{
    [MarshalAs(UnmanagedType.IDispatch)]
    public object obj;
}
```

```cpp
struct ObjectDispatch
{
    IDispatch* obj;
};
```

<span data-ttu-id="63509-161">Se si vuole effettuare il marshalling come `VARIANT`, aggiungere un <xref:System.Runtime.InteropServices.MarshalAsAttribute> con il valore <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType>.</span><span class="sxs-lookup"><span data-stu-id="63509-161">If you want to marshal it as a `VARIANT`, add a <xref:System.Runtime.InteropServices.MarshalAsAttribute> with the <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=nameWithType> value.</span></span>

```csharp
public struct ObjectVariant
{
    [MarshalAs(UnmanagedType.Struct)]
    public object obj;
}
```

```cpp
struct ObjectVariant
{
    VARIANT obj;
};
```

<span data-ttu-id="63509-162">La tabella seguente descrive i mapping tra i diversi tipi di runtime del campo `obj` e i vari tipi archiviati in un `VARIANT`:</span><span class="sxs-lookup"><span data-stu-id="63509-162">The following table describes how different runtime types of the `obj` field map to the various types stored in a `VARIANT`:</span></span>

| <span data-ttu-id="63509-163">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="63509-163">.NET Type</span></span> | <span data-ttu-id="63509-164">Tipo VARIANT</span><span class="sxs-lookup"><span data-stu-id="63509-164">VARIANT Type</span></span> | | <span data-ttu-id="63509-165">Tipo .NET</span><span class="sxs-lookup"><span data-stu-id="63509-165">.NET Type</span></span> | <span data-ttu-id="63509-166">Tipo VARIANT</span><span class="sxs-lookup"><span data-stu-id="63509-166">VARIANT Type</span></span> |
|------------|--------------|-|----------|--------------|
|  `byte`  | `VT_UI1` |     | `System.Runtime.InteropServices.BStrWrapper` | `VT_BSTR` |
| `sbyte`  | `VT_I1`  |     | `object`  | `VT_DISPATCH` |
| `short`  | `VT_I2`  |     | `System.Runtime.InteropServices.UnknownWrapper` | `VT_UNKNOWN` |
| `ushort` | `VT_UI2` |     | `System.Runtime.InteropServices.DispatchWrapper` | `VT_DISPATCH` |
| `int`    | `VT_I4`  |     | `System.Reflection.Missing` | `VT_ERROR` |
| `uint`   | `VT_UI4` |     | `(object)null` | `VT_EMPTY` |
| `long`   | `VT_I8`  |     | `bool` | `VT_BOOL` |
| `ulong`  | `VT_UI8` |     | `System.DateTime` | `VT_DATE` |
| `float`  | `VT_R4`  |     | `decimal` | `VT_DECIMAL` |
| `double` | `VT_R8`  |     | `System.Runtime.InteropServices.CurrencyWrapper` | `VT_CURRENCY` |
| `char`   | `VT_UI2` |     | `System.DBNull` | `VT_NULL` |
| `string` | `VT_BSTR`|