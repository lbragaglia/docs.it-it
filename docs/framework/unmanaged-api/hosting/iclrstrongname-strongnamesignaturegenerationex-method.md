---
title: Metodo ICLRStrongName::StrongNameSignatureGenerationEx
ms.date: 03/30/2017
api_name:
- ICLRStrongName.StrongNameSignatureGenerationEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRStrongName::StrongNameSignatureGenerationEx
helpviewer_keywords:
- ICLRStrongName::StrongNameSignatureGenerationEx method [.NET Framework hosting]
- StrongNameSignatureGenerationEx method, ICLRStrongName interface [.NET Framework hosting]
ms.assetid: c3f34584-c6e2-41fd-bb44-e44da8546309
topic_type:
- apiref
author: rpetrusha
ms.author: ronpet
ms.openlocfilehash: b411a51a5640a924d3eeae5d52102a842966d3fa
ms.sourcegitcommit: 205b9a204742e9c77256d43ac9d94c3f82909808
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/10/2019
ms.locfileid: "70855506"
---
# <a name="iclrstrongnamestrongnamesignaturegenerationex-method"></a>Metodo ICLRStrongName::StrongNameSignatureGenerationEx
Genera una firma con nome sicuro per l'assembly specificato, in base ai flag specificati.  
  
## <a name="syntax"></a>Sintassi  
  
```cpp
HRESULT StrongNameSignatureGenerationEx (  
    [in]  LPCWSTR   wszFilePath,  
    [in]  LPCWSTR   wszKeyContainer,  
    [in]  BYTE      *pbKeyBlob,  
    [in]  ULONG     cbKeyBlob,  
    [out] BYTE      **ppbSignatureBlob,  
    [out] ULONG     *pcbSignatureBlob,  
    [in]  DWORD     dwFlags  
);  
```  
  
## <a name="parameters"></a>Parametri  
 `wszFilePath`  
 in Percorso del file contenente il manifesto dell'assembly per il quale verrà generata la firma con nome sicuro.  
  
 `wszKeyContainer`  
 in Nome del contenitore di chiavi che contiene la coppia di chiavi pubblica/privata.  
  
 Se `pbKeyBlob` è null, `wszKeyContainer` è necessario specificare un contenitore valido all'interno del provider del servizio di crittografia (CSP). In questo caso, la coppia di chiavi archiviata nel contenitore viene usata per firmare il file.  
  
 Se `pbKeyBlob` non è null, si presuppone che la coppia di chiavi sia contenuta nel BLOB (Binary Large Object) della chiave.  
  
 `pbKeyBlob`  
 in Puntatore alla coppia di chiavi pubblica/privata. Questa coppia è nel formato creato dalla funzione Win32 `CryptExportKey` . Se `pbKeyBlob` è null, si presuppone che il contenitore `wszKeyContainer` di chiavi specificato da contenga la coppia di chiavi.  
  
 `cbKeyBlob`  
 in Dimensione, in byte, di `pbKeyBlob`.  
  
 `ppbSignatureBlob`  
 out Puntatore alla posizione in cui il Common Language Runtime restituisce la firma. Se `ppbSignatureBlob` è null, il runtime archivia la firma nel file specificato da `wszFilePath`.  
  
 Se `ppbSignatureBlob` non è null, il Common Language Runtime alloca spazio per la restituzione della firma. Il chiamante deve liberare questo spazio usando il metodo [ICLRStrongName:: StrongNameFreeBuffer](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamefreebuffer-method.md) .  
  
 `pcbSignatureBlob`  
 out Dimensione, in byte, della firma restituita.  
  
 `dwFlags`  
 in Uno o più dei valori seguenti:  
  
- `SN_SIGN_ALL_FILES`(0x00000001): Ricalcola tutti gli hash per i moduli collegati.  
  
- `SN_TEST_SIGN`(0x00000002)-test-firma l'assembly.  
  
## <a name="return-value"></a>Valore restituito  
 `S_OK`Se il metodo è stato completato correttamente; in caso contrario, valore HRESULT che indica l'esito negativo (vedere [valori HRESULT comuni](https://go.microsoft.com/fwlink/?LinkId=213878) per un elenco).  
  
## <a name="remarks"></a>Note  
 Specificare null per `wszFilePath` per calcolare le dimensioni della firma senza creare la firma.  
  
 La firma può essere archiviata direttamente nel file o restituita al chiamante.  
  
 Se `SN_SIGN_ALL_FILES` viene specificato, ma non è inclusa una chiave pubblica ( `pbKeyBlob` sia `wszFilePath` che sono null), gli hash per i moduli collegati vengono ricalcolati, ma l'assembly non viene firmato nuovamente.  
  
 Se `SN_TEST_SIGN` si specifica, l'intestazione Common Language Runtime non viene modificata per indicare che l'assembly è firmato con un nome sicuro.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** Metahost. h  
  
 **Libreria** Incluso come risorsa in MSCorEE. dll  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Metodo StrongNameSignatureGeneration](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-strongnamesignaturegeneration-method.md)
- [Interfaccia ICLRStrongName](../../../../docs/framework/unmanaged-api/hosting/iclrstrongname-interface.md)
