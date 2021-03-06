---
title: Metodo ICorDebugEval::CallFunction
ms.date: 03/30/2017
api_name:
- ICorDebugEval.CallFunction
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugEval::CallFunction
helpviewer_keywords:
- ICorDebugEval::CallFunction method [.NET Framework debugging]
- CallFunction method [.NET Framework debugging]
ms.assetid: 7f470c5c-e1c0-4d8d-aad8-830f113ae751
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 65225281fe3abaa20e69e96f4cd4d2a4b03a87ce
ms.sourcegitcommit: 8699383914c24a0df033393f55db3369db728a7b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/15/2019
ms.locfileid: "65629946"
---
# <a name="icordebugevalcallfunction-method"></a>Metodo ICorDebugEval::CallFunction

Imposta una chiamata alla funzione specificata.

Questo metodo è obsoleto in .NET Framework versione 2.0. Uso [ICorDebugEval2::CallParameterizedFunction](icordebugeval2-callparameterizedfunction-method.md) invece.

## <a name="syntax"></a>Sintassi

```cpp
HRESULT CallFunction (
    [in] ICorDebugFunction  *pFunction,
    [in] ULONG32            nArgs,
    [in, size_is(nArgs)] ICorDebugValue *ppArgs[]
);
```

## <a name="parameters"></a>Parametri

`pFunction`\
[in] Puntatore a un oggetto ICorDebugFunction che specifica la funzione da chiamare.

`nArgs`\
[in] Il numero di argomenti per la funzione.

`ppArgs`\
[in] Una matrice di puntatori, ognuno dei quali punta a un oggetto ICorDebugValue che specifica un argomento deve essere passato alla funzione.

## <a name="remarks"></a>Note

Se la funzione è virtuale, `CallFunction` eseguirà chiamate virtuali. Se la funzione è in un altro dominio applicazione, si verificherà una transizione, purché tutti gli argomenti sono presenti anche in tale dominio dell'applicazione.

## <a name="requirements"></a>Requisiti

**Piattaforme:** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).

**Intestazione:** CorDebug.idl, CorDebug.h

**Libreria:** CorGuids.lib

**Versioni di .NET framework:** 1.1, 1.0

## <a name="see-also"></a>Vedere anche

- [Metodo CallParameterizedFunction](icordebugeval2-callparameterizedfunction-method.md)
