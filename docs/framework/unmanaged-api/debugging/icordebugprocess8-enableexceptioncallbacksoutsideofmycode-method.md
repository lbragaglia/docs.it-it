---
title: Metodo ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode
ms.date: 03/30/2017
dev_langs:
- cpp
ms.assetid: b3af44ec-7d41-425b-aed9-0c4379e5cbe9
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 52a58f75ca7abd1bd1f871bcf4637bfd7eb7bdcd
ms.sourcegitcommit: 621a5f6df00152006160987395b93b5b55f7ffcd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/29/2019
ms.locfileid: "66300548"
---
# <a name="icordebugprocess8enableexceptioncallbacksoutsideofmycode-method"></a>Metodo ICorDebugProcess8::EnableExceptionCallbacksOutsideOfMyCode
[Supportato in .NET Framework 4.6 e versioni successive]  
  
 Abilita o disabilita alcuni tipi di [ICorDebugManagedCallback2](../../../../docs/framework/unmanaged-api/debugging/icordebugmanagedcallback2-interface.md) callback di eccezione.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
HRESULT EnableExceptionCallbacksOutsideOfMyCode(  
   [in] BOOL enableExceptionsOutsideOfJMC  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `enableExceptionsOutsideOfJMC`  
 [in]  
  
## <a name="remarks"></a>Note  
 Se il valore di `enableExceptionsOutsideOfJMC` è `false`:  
  
- Un'eccezione DEBUG_EXCEPTION_FIRST_CHANCE non comporterà un callback al debugger.  
  
- Un'eccezione DEBUG_EXCEPTION_CATCH_HANDLER_FOUND non comporterà un callback al debugger se l'eccezione non ignora mai nel codice utente (vale a dire, il percorso dall'origine di un gestore di eccezioni non ha metodi contrassegnati JustMyCode o JMC).  
  
 Il valore predefinito di `enableExceptionsOutsideOfJMC` è `true`.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme:** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug.idl, CorDebug.h  
  
 **Libreria:** CorGuids.lib  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v46plus](../../../../includes/net-current-v46plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfaccia ICorDebugProcess8](../../../../docs/framework/unmanaged-api/debugging/icordebugprocess8-interface.md)
- [Interfacce di debug](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)
