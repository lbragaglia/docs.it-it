---
title: Interfaccia ICorProfilerInfo
ms.date: 03/30/2017
api_name:
- ICorProfilerInfo
api_location:
- mscorwks.dll
api_type:
- COM
f1_keywords:
- ICorProfilerInfo
helpviewer_keywords:
- ICorProfilerInfo interface [.NET Framework profiling]
ms.assetid: eb4e4ce0-06e7-4469-bbc4-edc2eb5da4b1
topic_type:
- apiref
author: mairaw
ms.author: mairaw
ms.openlocfilehash: 3b82d9ac610cb393696ef94fb797a48b737b0231
ms.sourcegitcommit: 68653db98c5ea7744fd438710248935f70020dfb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/22/2019
ms.locfileid: "69965743"
---
# <a name="icorprofilerinfo-interface"></a>Interfaccia ICorProfilerInfo
Fornisce metodi per l'uso da parte dei profiler del codice per comunicare con il Common Language Runtime (CLR) per controllare il monitoraggio degli eventi e le informazioni sulla richiesta.  
  
> [!NOTE]
> Ogni metodo nell' `ICorProfilerInfo` interfaccia restituisce un valore HRESULT per indicare l'esito positivo o negativo. Per un elenco dei codici restituiti possibili, vedere CorError. h.  
  
## <a name="methods"></a>Metodi  
  
|Metodo|Descrizione|  
|------------|-----------------|  
|[Metodo BeginInprocDebugging](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-begininprocdebugging-method.md)|Inizializza il supporto per il debug in-process. Questo metodo è obsoleto nella versione .NET Framework 2,0.|  
|[Metodo EndInprocDebugging](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-endinprocdebugging-method.md)|Arresta una sessione di debug in-process. Questo metodo è obsoleto nella versione .NET Framework 2,0.|  
|[Metodo ForceGC](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-forcegc-method.md)|Impone che Garbage Collection venga eseguita all'interno del runtime.|  
|[Metodo GetAppDomainInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getappdomaininfo-method.md)|Ottiene informazioni sul dominio applicazione specificato.|  
|[Metodo GetAssemblyInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getassemblyinfo-method.md)|Ottiene informazioni sull'assembly specificato.|  
|[Metodo GetClassFromObject](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromobject-method.md)|Ottiene l' `ClassID` oggetto di un oggetto.<br /><br /> , dato il relativo `ObjectID`oggetto.|  
|[Metodo GetClassFromToken](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassfromtoken-method.md)|Ottiene l'ID della classe, dato il token di metadati. Questo metodo è obsoleto nella versione .NET Framework 2,0. Usare invece il metodo [ICorProfilerInfo2:: GetClassFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getclassfromtokenandtypeargs-method.md) .|  
|[Metodo GetClassIDInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getclassidinfo-method.md)|Ottiene il modulo padre e il token di metadati per la classe specificata.|  
|[Metodo GetCodeInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcodeinfo-method.md)|Ottiene l'ambito del codice nativo associato all'ID funzione specificato. Questo metodo è obsoleto. Usare invece il metodo [ICorProfilerInfo2:: GetCodeInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getcodeinfo2-method.md) .|  
|[Metodo GetCurrentThreadID](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getcurrentthreadid-method.md)|Ottiene l'ID del thread corrente, se è un thread gestito.|  
|[Metodo GetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-geteventmask-method.md)|Ottiene le categorie di eventi correnti per le quali il profiler vuole ricevere notifiche di eventi da CLR.|  
|[Metodo GetFunctionFromIP](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromip-method.md)|Esegue il mapping di un puntatore all'istruzione `FunctionID`di codice gestito a.|  
|[Metodo GetFunctionFromToken](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctionfromtoken-method.md)|Ottiene l'ID di una funzione. Questo metodo è obsoleto nella versione .NET Framework 2,0. Usare invece il metodo [ICorProfilerInfo2:: GetFunctionFromTokenAndTypeArgs](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-getfunctionfromtokenandtypeargs-method.md) .|  
|[Metodo GetFunctionInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getfunctioninfo-method.md)|Ottiene la classe padre e il token di metadati per la funzione specificata.|  
|[Metodo GetHandleFromThread](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gethandlefromthread-method.md)|Esegue il mapping dell'ID di un thread a un handle di thread Win32.|  
|[Metodo GetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbody-method.md)|Ottiene un puntatore al corpo di un metodo nel codice MSIL (Microsoft Intermediate Language), a partire dalla relativa intestazione.|  
|[Metodo GetILFunctionBodyAllocator](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getilfunctionbodyallocator-method.md)|Ottiene un'interfaccia che fornisce un metodo per allocare la memoria da utilizzare per lo swapping del corpo di un metodo nel codice MSIL.|  
|[Metodo GetILToNativeMapping](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getiltonativemapping-method.md)|Ottiene una mappa dagli offset MSIL agli offset nativi per il codice contenuto nella funzione specificata.|  
|[Metodo GetInprocInspectionInterface](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectioninterface-method.md)|Ottiene un oggetto su cui è possibile eseguire una query per un'interfaccia ICorDebugProcess. Questo metodo è obsoleto nella versione .NET Framework 2,0.|  
|[Metodo GetInprocInspectionIThisThread](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getinprocinspectionithisthread-method.md)|Ottiene un oggetto su cui è possibile eseguire query per l'interfaccia ICorDebugThread. Questo metodo è obsoleto nella versione .NET Framework 2,0.|  
|[Metodo GetModuleInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmoduleinfo-method.md)|Dato un ID modulo, restituisce il nome file del modulo e l'ID dell'assembly padre del modulo.|  
|[Metodo GetModuleMetaData](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getmodulemetadata-method.md)|Ottiene un'istanza dell'interfaccia di metadati mappata al modulo specificato.|  
|[Metodo GetObjectSize](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getobjectsize-method.md)|Ottiene le dimensioni di un oggetto specificato.|  
|[Metodo GetThreadContext](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadcontext-method.md)|Ottiene l'identità del contesto attualmente associata al thread specificato.|  
|[Metodo GetThreadInfo](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-getthreadinfo-method.md)|Ottiene l'identità corrente del thread Win32 per il thread specificato.|  
|[Metodo GetTokenAndMetadataFromFunction](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-gettokenandmetadatafromfunction-method.md)|Ottiene il token di metadati e un'istanza dell'interfaccia di metadati che può essere utilizzata per il token per la funzione specificata.|  
|[Metodo IsArrayClass](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-isarrayclass-method.md)|Determina se la classe specificata è una classe di matrici.|  
|[Metodo SetEnterLeaveFunctionHooks](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setenterleavefunctionhooks-method.md)|Specifica le funzioni implementate dal profiler da chiamare sugli hook "Enter", "Leave" e "tailcall" delle funzioni gestite.|  
|[Metodo SetEventMask](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-seteventmask-method.md)|Imposta un valore che specifica i tipi di eventi per i quali il profiler vuole ricevere notifiche da CLR.|  
|[Metodo SetFunctionIDMapper](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionidmapper-method.md)|Specifica la funzione implementata dal profiler che verrà chiamata per trasformare i valori `FunctionID` in valori alternativi, che vengono passati agli hook di ingresso/uscita delle funzioni del profiler.|  
|[Metodo SetFunctionReJIT](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setfunctionrejit-method.md)|Non implementato. Non usare.|  
|[Metodo SetILFunctionBody](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilfunctionbody-method.md)|Sostituisce il corpo della funzione specificata nel modulo specificato.|  
|[Metodo SetILInstrumentedCodeMap](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo-setilinstrumentedcodemap-method.md)|Specifica il modo in cui gli offset del codice MSIL originale di una funzione specificata vengono mappati ai nuovi offset del codice MSIL modificato dal profiler della funzione.|  
  
## <a name="remarks"></a>Note  
 Un profiler chiama un metodo `ICorProfilerInfo` nell'interfaccia per comunicare con CLR per controllare il monitoraggio degli eventi e le informazioni sulla richiesta.  
  
 I metodi dell' `ICorProfilerInfo` interfaccia sono implementati da CLR usando il modello a thread libero. Ogni metodo restituisce un valore HRESULT per indicare esito positivo o negativo. Per un elenco dei codici restituiti possibili, vedere CorError. h.  
  
 CLR passa, tramite l'implementazione del profiler di [ICorProfilerCallback:: Initialize](../../../../docs/framework/unmanaged-api/profiling/icorprofilercallback-initialize-method.md), `ICorProfilerInfo` un'interfaccia a ogni Code Profiler durante l'inizializzazione. Un code profiler può quindi chiamare i `ICorProfilerInfo` metodi dell'interfaccia per ottenere informazioni sul codice gestito eseguito sotto il controllo di CLR.  
  
## <a name="requirements"></a>Requisiti  
 **Piattaforme** Vedere [Requisiti di sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Intestazione:** CorProf. idl, CorProf. h  
  
 **Libreria** CorGuids.lib  
  
 **Versioni di .NET Framework:** [!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Vedere anche

- [Interfacce di profilatura](../../../../docs/framework/unmanaged-api/profiling/profiling-interfaces.md)
- [Interfaccia ICorProfilerInfo2](../../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo2-interface.md)
