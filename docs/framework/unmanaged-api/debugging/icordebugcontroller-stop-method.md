---
title: Metodo ICorDebugController::Stop
ms.date: 03/30/2017
api_name:
- ICorDebugController.Stop
api_location:
- mscordbi.dll
api_type:
- COM
f1_keywords:
- ICorDebugController::Stop
helpviewer_keywords:
- Stop method, ICorDebugController interface [.NET Framework debugging]
- ICorDebugController::Stop method [.NET Framework debugging]
ms.assetid: c34e79be-a7fb-479e-8dec-d126a4c330e5
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 363d8f7d8cf960fb23210225c4545f73d597d663
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69912836"
---
# <a name="icordebugcontrollerstop-method"></a>Metodo ICorDebugController::Stop
Esegue un arresto cooperativo su tutti i thread che eseguono codice gestito nel processo.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
HRESULT Stop (  
    [in] DWORD dwTimeoutIgnored  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `dwTimeoutIgnored`  
 Non usato.  
  
## <a name="remarks"></a>Note  
 `Stop`esegue un arresto cooperativo su tutti i thread che eseguono codice gestito nel processo. Durante una sessione di debug solo gestita, i thread non gestiti possono continuare a essere eseguiti (ma verranno bloccati quando si tenta di chiamare il codice gestito). Durante una sessione di debug di interoperabilità, verranno arrestati anche i thread non gestiti. Il `dwTimeoutIgnored` valore è attualmente ignorato e considerato infinito (-1). Se l'arresto cooperativo non riesce a causa di un deadlock, tutti i thread vengono sospesi e viene restituito E_TIMEOUT.  
  
> [!NOTE]
> `Stop`è l'unico metodo sincrono nell'API di debug. Quando `Stop` restituisce S_OK, il processo viene arrestato. Non viene specificato alcun callback per notificare ai listener l'arresto. Il debugger deve chiamare [ICorDebugController:: continue](../../../../docs/framework/unmanaged-api/debugging/icordebugcontroller-continue-method.md) per consentire la ripresa del processo.  
  
 Il debugger mantiene un contatore di interruzioni. Quando il contatore va a zero, il controller viene ripreso. Ogni chiamata a `Stop` o a ogni callback inviato incrementa il contatore. Ogni chiamata a `ICorDebugController::Continue` decrementa il contatore.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** CorDebug. idl, CorDebug. h  
  
 **Libreria** CorGuids.lib  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche
