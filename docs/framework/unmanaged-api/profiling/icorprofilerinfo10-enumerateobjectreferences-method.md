---
title: ICorProfilerInfo10::EnumerateObjectReferences
ms.date: 08/06/2019
dev_langs:
- cpp
api_name:
- ICorProfilerInfo10.EnumerateObjectReferences
api_location:
- mscorwks.dll
api_type:
- COM
author: davmason
ms.author: davmason
ms.openlocfilehash: ac193b6b78434245b8f11a4f627b4e1992feb8a7
ms.sourcegitcommit: cdf67135a98a5a51913dacddb58e004a3c867802
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/21/2019
ms.locfileid: "69661280"
---
# <a name="icorprofilerinfo10enumerateobjectreferences-method"></a>Metodo ICorProfilerInfo10:: EnumerateObjectReferences

Dato un ObjectID, callback e clientData, enumera ogni riferimento a un oggetto (se presente).

## <a name="syntax"></a>Sintassi

```cpp
HRESULT EnumerateObjectReferences( [in] ObjectID objectId,
                                   [in] ObjectReferenceCallback callback,
                                   [in] void* clientData);
```

#### <a name="parameters"></a>Parametri

`objectId` \
in Oggetto su cui enumerare i riferimenti.

`callback` \
in Funzione che verrà chiamata con i riferimenti per l'oggetto.

`clientData` \
in Dati forniti dal `callback` Profiler da passare alla funzione.

## <a name="remarks"></a>Note

Il `EnumerateObjectReferences` metodo è simile a [ObjectReferences](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-objectreferences-method.md), ad eccezione del fatto che scorre i riferimenti su richiesta per il profiler anziché pre-allocare una matrice per archiviare i riferimenti.

## <a name="requirements"></a>Requisiti

**Piattaforme** Vedere [sistemi operativi supportati da .NET Core](../../../core/windows-prerequisites.md#net-core-supported-operating-systems).

**Intestazione:** CorProf. idl, CorProf. h

**Libreria** CorGuids.lib

**Versioni di .NET:** [!INCLUDE[net_core_22](../../../../includes/net-core-30-md.md)]

## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorProfilerInfo10](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo10-interface.md)
