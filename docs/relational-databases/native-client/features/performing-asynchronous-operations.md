---
title: 비동기 작업 수행 | Microsoft Docs
description: 응용 프로그램이 SQL Server Native Client 이전 DB 공급자를 사용 하 여 비동기 데이터베이스 작업을 수행 하도록 허용 합니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9ccf1741e211c2d465359162a5deb73636a40af7
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97418623"
---
# <a name="performing-asynchronous-operations-in-sql-server-native-client"></a>SQL Server Native Client에서 비동기 작업 수행
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]을 사용하면 애플리케이션에서 비동기 데이터베이스 작업을 수행할 수 있습니다. 비동기 처리는 호출 스레드를 차단하지 않고 메서드를 즉시 반환할 수 있도록 합니다. 이를 통해 개발자는 명시적으로 스레드를 만들거나 동기화를 처리하지 않고도 보다 강력하고 유연한 다중 스레딩을 구현할 수 있습니다. 데이터베이스 연결을 초기화하거나 명령의 실행 결과를 초기화할 때 애플리케이션에서는 비동기 처리를 요청합니다.  
  
## <a name="opening-and-closing-a-database-connection"></a>데이터베이스 연결 열기 및 닫기  
 Native Client OLE DB 공급자를 사용 하는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터 소스 개체를 비동기적으로 초기화 하도록 디자인 된 응용 프로그램은 **IDBInitialize:: initialize** 를 호출 하기 전에 DBPROP_INIT_ASYNCH 속성에서 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정할 수 있습니다. 이 속성이 설정된 경우 공급자는 **Initialize** 호출 시 S_OK 또는 DB_S_ASYNCHRONOUS와 함께 즉시 반환됩니다. S_OK는 초기화 작업이 즉시 완료된 경우 반환되고 DB_S_ASYNCHRONOUS는 초기화 작업이 비동기식으로 계속되는 경우 반환됩니다. 응용 프로그램은 데이터 원본 개체에서 **IdISSAsynchStatus** 인터페이스에 [](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)대해 쿼리 한 다음 **Idw Chstatus:: GetStatus** 또는 [ISSAsynchStatus:: WaitForAsynchCompletion](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-waitforasynchcompletion-ole-db.md) 을 호출 하 여 초기화 상태를 가져올 수 있습니다.  
  
 또한 SSPROP_ISSAsynchStatus 속성이 DBPROPSET_SQLSERVERROWSET 속성 집합에 추가되었습니다. **ISSAsynchStatus** 인터페이스를 지원하는 공급자는 VARIANT_TRUE 값을 사용하여 이 속성을 구현해야 합니다.  
  
 **IDBAsynchStatus::Abort** 또는 [ISSAsynchStatus::Abort](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-abort-ole-db.md)를 호출하여 비동기 **Initialize** 호출을 취소할 수 있습니다. 소비자는 비동기 데이터 원본 초기화를 명시적으로 요청해야 합니다. 그렇지 않으면 데이터 원본 개체가 완전히 초기화될 때까지 **IDBInitialize::Initialize** 가 반환되지 않습니다.  
  
> [!NOTE]  
>  연결 풀링을 사용 하는 데이터 원본 개체는  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자에서 ISSAsynchStatus 인터페이스를 호출할 수 없습니다. **ISSAsynchStatus** 인터페이스는 풀에 있는 데이터 원본 개체에 대해 표시되지 않습니다.  
>   
>  애플리케이션에서 명시적으로 커서 엔진을 사용하도록 설정한 경우 **IOpenRowset::OpenRowset** 및 **IMultipleResults::GetResult** 는 비동기 처리를 지원하지 않습니다.  
>   
>  또한 원격 프록시/스텁 dll (MDAC 2.8)은 Native Client에서 **ISSAsynchStatus** 인터페이스를 호출할 수 없습니다 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . **ISSAsynchStatus** 인터페이스는 원격을 통해 표시되지 않습니다.  
>   
>  Service Components는 **ISSAsynchStatus** 를 지원하지 않습니다.  
  
## <a name="execution-and-rowset-initialization"></a>실행 및 행 집합 초기화  
 명령의 실행 결과를 비동기식으로 열도록 설계된 애플리케이션에서는 DBPROP_ROWSET_ASYNCH 속성의 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정할 수 있습니다. **IDBInitialize::Initialize**, **ICommand::Execute**, **IOpenRowset::OpenRowset** 또는 **IMultipleResults::GetResult** 를 호출하기 전에 이 비트를 설정할 경우 *riid* 인수를 IID_IDBAsynchStatus, IID_ISSAsynchStatus 또는 IID_IUnknown으로 설정해야 합니다.  
  
 메서드는 행 집합 초기화가 즉시 완료되면 S_OK와 함께 즉시 반환되고 행 집합 초기화가 행 집합의 요청된 인터페이스로 설정된 *ppRowset* 을 사용하여 비동기식으로 계속되면 DB_S_ASYNCHRONOUS와 함께 즉시 반환됩니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자의 경우이 인터페이스는 **IdwISSAsynchStatus chstatus** 또는 일 수 있습니다. 행 집합이 완전히 초기화될 때까지 이 인터페이스는 일시 중단 상태에 있는 것처럼 동작하며 인터페이스에 대해 **IID_IDBAsynchStatus** 또는 **IID_ISSAsynchStatus** 가 아닌 **QueryInterface** 를 호출하면 E_NOINTERFACE가 반환될 수 있습니다. 소비자가 비동기 처리를 명시적으로 요청하지 않을 경우 행 집합은 동기식으로 초기화됩니다. 동기화 작업이 완료되었다는 메시지와 함께 **IDBAsynchStaus::GetStatus** 또는 **ISSAsynchStatus::WaitForAsynchCompletion** 이 반환되면 요청된 모든 인터페이스를 사용할 수 있습니다. 이는 행 집합이 모두 채워지지는 않았지만 초기화가 완료되어 모든 기능이 올바로 작동함을 의미합니다.  
  
 실행한 명령이 행 집합을 반환하지 않을 경우 이 명령은 계속 **IDBAsynchStatus** 를 지원하는 개체와 함께 즉시 반환됩니다.  
  
 비동기 명령의 실행 결과를 여러 개 가져와야 하는 경우 다음을 수행해야 합니다.  
  
-   명령을 실행하기 전에 DBPROP_ROWSET_ASYNCH 속성의 DBPROPVAL_ASYNCH_INITIALIZE 비트를 설정합니다.  
  
-   **ICommand::Execute** 를 호출하고 **IMultipleResults** 를 요청합니다.  
  
 그러면 **QueryInterface** 를 통해 여러 결과 인터페이스를 쿼리하여 **IDBAsynchStatus** 및 **ISSAsynchStatus** 인터페이스를 가져올 수 있습니다.  
  
 명령의 실행이 완료되면 **IMultipleResults** 를 정상적으로 사용할 수 있습니다. 그러나 예외적으로 동기 작업을 수행할 경우 DB_S_ASYNCHRONOUS가 반환될 수도 있습니다. 이 경우 **IDBAsynchStatus** 또는 **ISSAsynchStatus** 를 사용하여 작업이 완료된 시점을 확인할 수 있습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 애플리케이션에서 비블로킹 메서드를 호출하고 몇 가지 다른 처리를 수행한 다음 다시 호출 결과를 처리합니다. **ISSAsynchStatus::WaitForAsynchCompletion** 은 비동기식으로 실행된 작업이 완료되거나 *dwMilisecTimeOut* 으로 지정한 시간이 경과될 때까지 내부 이벤트 개체를 기다립니다.  
  
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
  
 **ISSAsynchStatus::WaitForAsynchCompletion** 은 비동기식으로 실행된 작업이 완료되거나 *dwMilisecTimeOut* 값이 전달될 때까지 내부 이벤트 개체를 기다립니다.  
  
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
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Native Client 기능](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [행 집합 속성 및 동작](../../../relational-databases/native-client-ole-db-rowsets/rowset-properties-and-behaviors.md)   
 [ISSAsynchStatus &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/issasynchstatus-ole-db.md)  
  
  
