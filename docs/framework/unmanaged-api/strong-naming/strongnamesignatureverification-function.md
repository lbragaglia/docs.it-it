---
title: Funzione StrongNameSignatureVerification
ms.date: 03/30/2017
api_name:
- StrongNameSignatureVerification
api_location:
- mscoree.dll
api_type:
- DLLExport
f1_keywords:
- StrongNameSignatureVerification
helpviewer_keywords:
- StrongNameSignatureVerification function [.NET Framework strong naming]
ms.assetid: 933758dd-231e-4382-8819-242c0a13a4b7
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: 8943df861b1bff2b28c68d0233fc336d1b5d4579
ms.sourcegitcommit: d2e1dfa7ef2d4e9ffae3d431cf6a4ffd9c8d378f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/07/2019
ms.locfileid: "70798939"
---
# <a name="strongnamesignatureverification-function"></a>Funzione StrongNameSignatureVerification
Ottiene un valore che indica se il manifesto dell'assembly nel percorso specificato contiene una firma con nome sicuro, che viene verificata in base ai flag specificati.  
  
 Questa funzione è stata deprecata. Usare invece il metodo [ICLRStrongName:: StrongNameSignatureVerification](../hosting/iclrstrongname-strongnamesignatureverification-method.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```cpp  
BOOLEAN StrongNameSignatureVerification (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  DWORD     dwInFlags,  
    [out] DWORD     *pdwOutFlags  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `wszFilePath`  
 in Percorso del file eseguibile (con estensione dll o exe) portatile per l'assembly da verificare.  
  
 `dwInFlags`  
 in Flag per modificare il comportamento di verifica. Sono supportati i valori seguenti:  
  
- `SN_INFLAG_FORCE_VER`(0x00000001): impone la verifica anche se è necessario eseguire l'override delle impostazioni del registro di sistema.  
  
- `SN_INFLAG_INSTALL`(0x00000002): specifica che questa è la prima volta che il manifesto viene verificato.  
  
- `SN_INFLAG_ADMIN_ACCESS`(0x00000004): specifica che la cache consentirà l'accesso solo agli utenti che dispongono di privilegi amministrativi.  
  
- `SN_INFLAG_USER_ACCESS`(0x00000008): specifica che l'assembly sarà accessibile solo all'utente corrente.  
  
- `SN_INFLAG_ALL_ACCESS`(0x00000010): specifica che la cache non fornirà alcuna garanzia di restrizione di accesso.  
  
- `SN_INFLAG_RUNTIME`(0x80000000)-riservato per il debug interno.  
  
 `pdwOutFlags`  
 out Flag che indicano se la firma del nome sicuro è stata verificata. È supportato il valore seguente:  
  
- `SN_OUTFLAG_WAS_VERIFIED`(0x00000001): questo valore è impostato su `false` per specificare che la verifica ha avuto esito positivo a causa delle impostazioni del registro di sistema.  
  
## <a name="return-value"></a>Valore restituito  
 `true`Se la verifica ha avuto esito positivo; in caso `false`contrario,.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme** Vedere [Requisiti di sistema](../../get-started/system-requirements.md).  
  
 **Intestazione:** StrongName. h  
  
 **Libreria** Incluso come risorsa in MsCorEE. dll  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Metodo StrongNameSignatureVerification](../hosting/iclrstrongname-strongnamesignatureverification-method.md)
- [Metodo StrongNameSignatureVerificationEx](../hosting/iclrstrongname-strongnamesignatureverificationex-method.md)
- [Interfaccia ICLRStrongName](../hosting/iclrstrongname-interface.md)
