---
title: WMI e contatori delle prestazioni (riferimenti alle API non gestite)
description: Contiene informazioni sull'API non gestita .NET Framework per WMI e i contatori delle prestazioni.
author: rpetrusha
ms.author: ronpet
ms.date: 11/06/2017
ms.openlocfilehash: bbf22496098f848cc7c55652198d792c6f631c15
ms.sourcegitcommit: 9b552addadfb57fab0b9e7852ed4f1f1b8a42f8e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62049310"
---
# <a name="windows-management-instrumentation-wmi-and-performance-counters-unmanaged-api-reference"></a>Strumentazione gestione Windows (WMI) e contatori delle prestazioni (riferimenti alle API non gestite)

L'API non gestita .NET Framework per WMI e i contatori delle prestazioni è costituita da un set di funzioni che eseguono il wrapping delle chiamate all'[API di Strumentazione gestione Windows nativa](/windows/desktop/WmiSdk/com-api-for-wmi). Consente lo sviluppo di strumenti e librerie che gestiscono e monitorano i computer remoti.

[!INCLUDE[internalonly-unmanaged](../../../../includes/internalonly-unmanaged.md)]

L'API include le funzioni seguenti:

| Funzione | Description |
|---------|---------|
| [BeginEnumeration](beginenumeration.md) | Reimposta l'enumeratore all'inizio di un'enumerazione di proprietà di oggetti WMI. |
| [BeginMethodEnumeration](beginmethodenumeration.md) |  Inizia l'enumerazione dei metodi disponibili per un oggetto. |
| [BlessIWbemServices](blessiwbemservices.md) | Indica se le credenziali utente consentono l'accesso a una classe IWbemServices specificata. |
| [BlessIWbemServicesObject](blessiwbemservicesobject.md) | Indica se le credenziali utente consentono l'accesso a un oggetto del servizio IWbem specificato. |
| [Clone](clone.md) | Restituisce un nuovo oggetto che è un clone completo dell'oggetto corrente. |
| [CloneEnumWbemClassObject](cloneenumwbemclassobject.md) | Crea una copia logica di un enumeratore mantenendone la posizione corrente in un'enumerazione. |
| [CompareTo](compareto.md) | Confronta un oggetto con un altro oggetto di Gestione Windows. |
| [Funzione ConnectServerWmi](connectserverwmi.md) | Crea una connessione tramite DCOM a uno spazio dei nomi WMI in un computer specifico. |
| [Funzione CreateClassEnumWmi](createclassenumwmi.md) | Restituisce un enumeratore per tutte le classi che soddisfano i criteri di selezione specificati. |
| [Funzione CreateInstanceEnumWmi](createinstanceenumwmi.md) | Restituisce un enumeratore che restituisce le istanze di una classe specificata che soddisfa i criteri di selezione specificati. |
| [Delete](delete.md) | Elimina una proprietà specificata dalla definizione di una classe e tutti i relativi qualificatori. |
| [DeleteMethod](deletemethod.md) | Elimina un metodo specificato dalla definizione di una classe CIM. |
| [EndEnumeration](endenumeration.md) | Termina una sequenza di enumerazione. |
| [EndMethodEnumeration](endmethodenumeration.md) | Termina una sequenza di enumerazione avviata chiamando la [funzione BeginMethodEnumeration](beginmethodenumeration.md). |
| [ExecNotificationQueryWmi](execnotificationquerywmi.md) | Esegue una query per la ricezione di eventi. |
| [ExecQueryWmi](execquerywmi.md) | Esegue una query per il recupero di oggetti. |
| [FormatFromRawValue](formatfromrawvalue.md) | Converte un valore di dati sulle prestazioni non elaborati nel formato specificato o due valori di dati sulle prestazioni non elaborati se la conversione del formato è basata sul tempo. |
| [Get](get.md) | Recupera un valore di proprietà specificato, se esistente. |
| [Funzione GetCurrentApartmentType](getcurrentapartmenttype.md) | Recupera il tipo di apartment in cui il chiamante è in esecuzione. |
| [Funzione GetDemultiplexedStub](getdemultiplexedstub.md) | Crea un sink di inoltro oggetti per consentire a un client di ricevere chiamate asincrone da Gestione Windows. |
| [Funzione GetErrorInfo](geterrorinfo.md) | Recupera le informazioni di errore dalla chiamata di funzione precedente. |
| [GetMethod](getmethod.md) | Recupera le informazioni relative al metodo specificato. |
| [GetMethodOrigin](getmethodorigin.md) | Determina la classe in cui viene dichiarato un metodo. |
| [GetMethodQualifierSet](getmethodqualifierset.md) | Recupera il qualificatore impostato per un particolare metodo. |
| [GetNames](getnames.md) | Recupera un subset o tutti i nomi delle proprietà di un oggetto. |
| [GetObjectText](getobjecttext.md) | Restituisce un rendering testuale di un oggetto nella sintassi MOF. |
| [GetPropertyHandle](getpropertyhandle.md) | Restituisce un handle univoco che identifica una proprietà. |
| [GetPropertyOrigin](getpropertyorigin.md) | Determina la classe in cui viene dichiarata una proprietà. |
| [Funzione GetPropertyQualifierSet](getpropertyqualifierset.md) | Recupera il qualificatore impostato per una particolare proprietà.  |
| [Funzione GetQualifierSet](getqualifierset.md) | Recupera il qualificatore impostato per l'istanza di una classe o la definizione di una classe. |
| [Funzione InheritsFrom](inheritsfrom.md) | Determina se la classe o l'istanza corrente deriva da una classe padre specificata. |
| [Funzione Initialize](initialize.md) | Esegue l'inizializzazione di WMI. |
| [Funzione Next](next.md) | Recupera la proprietà successiva in un'enumerazione. |
| [Funzione NextMethod](nextmethod.md) | Recupera il metodo successivo in un'enumerazione. |
| [Put](put.md) | Imposta una proprietà denominata su un nuovo valore. |
| [Funzione PutClassWmi](putclasswmi.md) | Crea una nuova classe o ne aggiorna una esistente. |
| [Funzione PutInstanceWmi](putinstancewmi.md) | Crea o aggiorna un'istanza di una classe esistente. L'istanza viene scritta nel repository WMI. |
| [Funzione PutMethod](putmethod.md) | Crea un metodo. |
| [Funzione QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md) | Reimposta un enumeratore dei qualificatori di un oggetto all'inizio dell'enumerazione. |
| [Funzione QualifierSet_Delete](qualifierset-delete.md) | Elimina un qualificatore specificato in base al nome.  |
| [Funzione QualifierSet_EndEnumeration](qualifierset-endenumeration.md) | Termina l'enumerazione iniziata con una chiamata alla funzione `QualifierSet_BeginEnumeration`. |
| [Funzione QualifierSet_Get](qualifierset-get.md) | Ottiene il qualificatore denominato specificato.  |
| [Funzione QualifierSet_GetNames](qualifierset-getnames.md) | Recupera i nomi di tutti i qualificatori o di qualificatori specificati disponibili dall'oggetto o dalla proprietà corrente. |
| [Funzione QualifierSet_Next](qualifierset-next.md) | Recupera il qualificatore successivo in un'enumerazione avviata con una chiamata alla funzione [QualifierSet_BeginEnumeration](qualifierset-beginenumeration.md). |
| [Funzione QualifierSet_Put](qualifierset-put.md) | Scrive il qualificatore e il valore denominati. |
| [Funzione ResetSecurity](resetsecurity.md) | Assegna il token di rappresentazione fornito al thread corrente. |
| [Funzione SetSecurity](setsecurity.md) | Recupera il token di rappresentazione associato al thread corrente. |
| [Funzione SpawnDerivedClass](spawnderivedclass.md) | Crea un nuovo oggetto di classe derivata da un oggetto specificato. |
| [Funzione SpawnInstance](spawninstance.md) | Crea una nuova istanza di una classe. |
| [Funzione VerifyClient](verifyclientkey.md) | Verifica che la chiave client includa la sicurezza corretta. |
| [Funzione WritePropertyValue](writepropertyvalue.md) | Scrive un numero specificato di byte in una proprietà identificata da un handle di proprietà. |

## <a name="see-also"></a>Vedere anche

- [Riferimenti alle API non gestite](../index.md)
