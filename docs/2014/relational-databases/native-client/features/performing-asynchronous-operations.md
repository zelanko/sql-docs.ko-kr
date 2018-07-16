---
title: 비동기 작업을 수행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- initialization [SQL Server Native Client]
- database connections [SQL Server Native Client]
- data access [SQL Server Native Client], asynchronous operations
- connections [SQL Server Native Client]
- asynchronous operations [SQL Server Native Client]
- rowsets [SQL Server], initializing
- SQLNCLI, asynchronous operations
- SQL Server Native Client, asynchronous operations
ms.assetid: 8fbd84b4-69cb-4708-9f0f-bbdf69029bcc
caps.latest.revision: 45
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84d46265f1d057c805c4ad4dcb9463dc319c12a2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37407773"
---
# <a name="performing-asynchronous-operations"></a>비동기 작업 수행
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 사용하면 응용 프로그램에서 비동기 데이터베이스 작업을 수행할 수 있습니다. 비동기 처리는 호출 스레드를 차단하지 않고 메서드를 즉시 반환할 수 있도록 합니다. 이를 통해 개발자는 명시적으로 스레드를 만들거나 동기화를 처리하지 않고도 보다 강력하고 유연한 다중 스레딩을 구현할 수 있습니다. 데이터베이스 연결을 초기화하거나 명령의 실행 결과를 초기화할 때 응용 프로그램에서는 비동기 처리를 요청합니다.  
  
## <a name="opening-and-closing-a-database-connection"></a>데이터베이스 연결 열기 및 닫기  
 사용 하는 경우는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 데이터 원본 개체를 비동기적으로 초기화 하도록 설계 된 응용 프로그램에 호출 하기 전에 DBPROP_INIT_ASYNCH 속성의 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정할 수 있습니다  **Idbinitialize:: Initialize**합니다. 공급자를 호출 하 여 즉시 반환 하는이 속성을 설정 하는 경우 **초기화** 작업이 즉시 완료 된 경우 S_OK 또는 DB_S_ASYNCHRONOUS, 초기화를 비동기적으로 계속 됩니다. 응용 프로그램에 대 한 쿼리 수를 **IDBAsynchStatus** 또는 [ISSAsynchStatus](../../native-client-ole-db-interfaces/issasynchstatus-ole-db.md)데이터 원본 개체에 대해 인터페이스 및 다음 호출 **idbasynchstatus:: Getstatus** 또는[ Issasynchstatus:: Waitforasynchcompletion](../../native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) 초기화의 상태를 가져옵니다.  
  
 또한 SSPROP_ISSAsynchStatus 속성이 DBPROPSET_SQLSERVERROWSET 속성 집합에 추가되었습니다. 지 원하는 공급자는 **ISSAsynchStatus** 인터페이스는 VARIANT_TRUE 값을 사용 하 여이 속성을 구현 해야 합니다.  
  
 **Idbasynchstatus:: Abort** 나 [issasynchstatus:: Abort](../../native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md) 비동기 취소를 호출할 수 있습니다 **초기화** 호출 합니다. 소비자는 비동기 데이터 원본 초기화를 명시적으로 요청해야 합니다. 그렇지 않으면 **idbinitialize:: Initialize** 데이터 원본 개체가 완전히 초기화 될 때까지 반환 하지 않습니다.  
  
> [!NOTE]  
>  연결 풀링이 사용 되는 데이터 원본 개체를 호출할 수 없습니다는 **ISSAsynchStatus** 인터페이스는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. 합니다 **ISSAsynchStatus** 풀링된 데이터 원본 개체에 대 한 인터페이스 노출 되지 않습니다.  
>   
>  응용 프로그램에는 명시적으로 커서 엔진을 사용 하 여 강제로 **iopenrowset:: Openrowset** 하 고 **imultipleresults:: Getresult** 비동기 처리를 지원 하지 것입니다.  
>   
>  또한 원격 프록시/스텁 dll (MDAC 2.8)에서 호출할 수 없습니다는 **ISSAsynchStatus** 인터페이스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client입니다. 합니다 **ISSAsynchStatus** 인터페이스 원격 서비스를 통해 노출 되지 않습니다.  
>   
>  서비스 구성 요소를 지원 하지 않습니다 **ISSAsynchStatus**합니다.  
  
## <a name="execution-and-rowset-initialization"></a>실행 및 행 집합 초기화  
 명령의 실행 결과를 비동기식으로 열도록 설계된 응용 프로그램에서는 DBPROP_ROWSET_ASYNCH 속성의 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정할 수 있습니다. 호출 하기 전에이 비트를 설정 하는 경우 **idbinitialize:: Initialize**를 **icommand:: Execute**하십시오 **iopenrowset:: Openrowset** 또는 **IMultipleResults:: GetResult**서 *riid* 인수를 IID_IDBAsynchStatus, IID_ISSAsynchStatus 또는 IID_IUnknown으로 설정 되어 있어야 합니다.  
  
 메서드가 즉시 반환 하면 S_OK와 함께 행 집합을 비동기식으로 계속 되 면 즉시 또는 DB_S_ASYNCHRONOUS를 사용 하 여 행 집합 초기화를 완료 하는 경우 사용 하 여 *ppRowset* 설정 요청된 된 인터페이스에는 행 집합입니다. 에 대 한 합니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를이 인터페이스만 될 수 있습니다 **IDBAsynchStatus** 하거나 **ISSAsynchStatus**합니다. 이 인터페이스는 일시 중단 된 상태 및 호출 처럼 동작 하는 행 집합이 완전히 초기화 될 때까지 **QueryInterface** 이외의 인터페이스에 대 한 **IID_IDBAsynchStatus** 또는 **IID_ ISSAsynchStatus** 하면 e_nointerface가 반환 될 수 있습니다. 소비자가 비동기 처리를 명시적으로 요청하지 않을 경우 행 집합은 동기식으로 초기화됩니다. 인터페이스는 사용할 수 있는 요청 된 모든 **idbasynchstaus:: Getstatus** 하거나 **issasynchstatus:: Waitforasynchcompletion** 비동기 작업이 완료 되었음을 표시를 사용 하 여 반환 합니다. 이는 행 집합이 모두 채워지지는 않았지만 초기화가 완료되어 모든 기능이 올바로 작동함을 의미합니다.  
  
 실행된 된 명령 행 집합을 반환 하지 않는 경우 여전히 즉시 반환을 지 원하는 개체를 사용 하 여 **IDBAsynchStatus**합니다.  
  
 비동기 명령의 실행 결과를 여러 개 가져와야 하는 경우 다음을 수행해야 합니다.  
  
-   명령을 실행하기 전에 DBPROP_ROWSET_ASYNCH 속성의 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정합니다.  
  
-   호출 **icommand:: Execute**, 및 요청 **IMultipleResults**합니다.  
  
 합니다 **IDBAsynchStatus** 하 고 **ISSAsynchStatus** 인터페이스를 통해 여러 결과 인터페이스를 쿼리하여 가져올 수 있습니다 **QueryInterface**합니다.  
  
 명령 실행을 마치면 **IMultipleResults** 동기 사례에서 한 가지 예외를 사용 하 여 정상적으로 사용할 수 있습니다: DB_S_ASYNCHRONOUS을 반환할 수 있으며 이때 **IDBAsynchStatus** 또는 **ISSAsynchStatus** 작업이 완료 되 면 확인 하기 위해 사용할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 응용 프로그램에서 비블로킹 메서드를 호출하고 몇 가지 다른 처리를 수행한 다음 다시 호출 결과를 처리합니다. **Issasynchstatus:: Waitforasynchcompletion** 비동기적으로 실행 중인 작업이 완료 될 때까지 내부 이벤트 개체에 의해 지정 된 기간 대기 *dwMilisecTimeOut* 전달 됩니다.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
  
DBPROPSET CmdPropset[1];  
DBPROP CmdProperties[1];  
  
CmdPropset[0].rgProperties = CmdProperties;  
CmdPropset[0].cProperties = 1;  
CmdPropset[0].guidPropertySet = DBPROPSET_ROWSET;  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
CmdProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
  
hr = pICommandProps->SetProperties(1, CmdPropset);  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if ( hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 **Issasynchstatus:: Waitforasynchcompletion** 비동기적으로 실행 중인 작업이 완료 될 때까지 내부 이벤트 개체에 대기 또는 *dwMilisecTimeOut* 값이 전달 됩니다.  
  
 다음 예에서는 다중 결과 집합의 비동기 처리를 보여 줍니다.  
  
```  
DBPROP CmdProperties[1];  
  
// Set asynch mode for command.  
CmdProperties[0].dwPropertyID = DBPROP_ROWSET_ASYNCH;  
CmdProperties[0].vValue.vt = VT_I4;  
CmdProperties[0].vValue.lVal = DBPROPVAL_ASYNCH_INITIALIZE;  
  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_IMultipleResults,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pIMultipleResults);  
  
// Use GetResults for ISSAsynchStatus.  
hr = pIMultipleResults->GetResult(IID_ISSAsynchStatus, (void **) &pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work here...  
  
   hr = pISSAsynchStatus->WaitForAsynchCompletion(dwMilisecTimeOut);  
   if (hr == S_OK)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
      pISSAsynchStatus->Release();  
   }  
}  
```  
  
 다음 예에서는 차단 문제를 방지하기 위해 클라이언트에서 실행 중인 비동기 작업의 상태를 확인하는 방법을 보여 줍니다.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);   
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   do{  
      // Do some work...  
      hr = pISSAsynchStatus->GetStatus(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN, NULL, NULL, &ulAsynchPhase, NULL);  
   }while (DBASYNCHPHASE_COMPLETE != ulAsynchPhase)  
   if SUCCEEDED(hr)  
   {  
      hr = pISSAsynchStatus->QueryInterface(IID_IRowset, (void**)&pRowset);  
   }  
   pIDBAsynchStatus->Release();  
}  
```  
  
 다음 예에서는 현재 실행 중인 비동기 작업을 취소하는 방법을 보여 줍니다.  
  
```  
// Set the DBPROPVAL_ASYNCH_INITIALIZE bit in the   
// DBPROP_ROWSET_ASYNCH property before calling Execute().  
hr = pICommand->Execute(  
   pUnkOuter,  
   IID_ISSAsynchStatus,  
   pParams,  
   pcRowsAffected,  
   (IUnknown**)&pISSAsynchStatus);  
  
if (hr == DB_S_ASYNCHRONOUS)  
{  
   // Do some work...  
   hr = pISSAsynchStatus->Abort(DB_NULL_HCHAPTER, DBASYNCHOP_OPEN);  
}  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Native Client 기능](sql-server-native-client-features.md)   
 [행 집합 속성 및 동작](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
