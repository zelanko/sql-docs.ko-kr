---
title: 로컬 트랜잭션 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8533747bbe5ccb79a06b10a754c4af45ab241843
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280300"
---
# <a name="supporting-local-transactions"></a>로컬 트랜잭션 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  세션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 로컬 트랜잭션에 대 한 트랜잭션 범위를 구분 합니다. 소비자의 방향으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB 공급자가 연결 된 인스턴스에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]요청을 전송 하는 경우 요청은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client OLE DB 공급자에 대 한 작업 단위를 구성 합니다. 로컬 트랜잭션은 항상 단일 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션에서 하나 이상의 작업 단위를 래핑합니다.  
  
 기본 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 자동 커밋 모드를 사용 하는 경우 단일 작업 단위가 로컬 트랜잭션의 범위로 처리 됩니다. 하나의 단위만 로컬 트랜잭션에 참여합니다. 세션이 만들어질 때 Native Client OLE DB 공급자 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 세션에 대 한 트랜잭션을 시작 합니다. 작업 단위가 성공적으로 완료되면 해당 작업이 커밋됩니다. 실패하면 시작된 모든 작업이 롤백되며 소비자에게 오류가 반환됩니다. 두 경우 모두 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자는 세션에 대 한 새 로컬 트랜잭션을 시작 하 여 트랜잭션 내에서 모든 작업이 수행 되도록 합니다.  
  
 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자 소비자는 **ITransactionLocal** 인터페이스를 사용 하 여 로컬 트랜잭션 범위를 보다 정확 하 게 제어할 수 있습니다. 소비자 세션이 트랜잭션을 시작하면 트랜잭션 시작점과 결과 **Commit** 또는 **Abort** 메서드 호출 시점 사이에 있는 모든 세션 작업 단위는 원자 단위로 처리됩니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 소비자에 게 전달 될 때 암시적으로 트랜잭션을 시작 합니다. 소비자가 보존을 요청하지 않으면 세션은 일반적으로 자동 커밋 모드인 부모 트랜잭션 수준 동작으로 돌아갑니다.  
  
 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 다음과 같이 **ITransactionLocal:: starttransaction** 매개 변수를 지원 합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*isoLevel*[in]|이 트랜잭션에 사용할 격리 수준입니다. 로컬 트랜잭션에서 Native Client OLE DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자는 다음을 지원 합니다.<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 참고: [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]부터는 데이터베이스에 버전 관리가 설정되어 있는지 여부에 관계없이 *isoLevel* 인수에 대해 ISOLATIONLEVEL_SNAPSHOT이 유효합니다. 그러나 버전 관리가 설정되어 있지 않거나 데이터베이스가 읽기 전용이 아닌 상태에서 사용자가 문을 실행하려고 하면 오류가 발생합니다. 또한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 버전에 연결할 때 ISOLATIONLEVEL_SNAPSHOT을 *isoLevel*로 지정하면 XACT_E_ISOLATIONLEVEL 오류가 발생합니다.|  
|*isoFlags*[in]|Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 0 이외의 값에 대해 오류를 반환 합니다.|  
|*pOtherOptions*[in]|NULL이 아닌 경우 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 인터페이스에서 options 개체를 요청 합니다. 옵션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 *ultimeout* 멤버가 0이 아니면 Native Client OLE DB 공급자가 XACT_E_NOTIMEOUT을 반환 합니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 *szdescription* 멤버의 값을 무시 합니다.|  
|*pulTransactionLevel*[out]|NULL이 아닌 경우 Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 트랜잭션 중첩 수준을 반환 합니다.|  
  
 로컬 트랜잭션의 경우 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자는 다음과 같이 **ITransaction:: Abort** 매개 변수를 구현 합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*pboidReason*[in]|설정된 경우 무시됩니다. NULL이어도 안전합니다.|  
|*fRetaining*[in]|TRUE인 경우 해당 세션을 위한 새 트랜잭션이 암시적으로 시작됩니다. 이 트랜잭션은 소비자가 커밋 또는 종료해야 합니다. FALSE 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 세션에 대해 자동 커밋 모드로 되돌립니다.|  
|*fAsync*[in]|Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비동기 중단을 지원 하지 않습니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 값이 FALSE가 아닌 경우 XACT_E_NOTSUPPORTED을 반환 합니다.|  
  
 로컬 트랜잭션의 경우 Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB 공급자는 다음과 같이 **ITransaction:: Commit** 매개 변수를 구현 합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*fRetaining*[in]|TRUE인 경우 해당 세션을 위한 새 트랜잭션이 암시적으로 시작됩니다. 이 트랜잭션은 소비자가 커밋 또는 종료해야 합니다. FALSE 이면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 세션에 대해 자동 커밋 모드로 되돌립니다.|  
|*grfTC*[in]|Native Client OLE DB 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 비동기 및 1 단계 반환을 지원 하지 않습니다. Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client OLE DB 공급자는 XACTTC_SYNC 이외의 값에 대해 XACT_E_NOTSUPPORTED을 반환 합니다.|  
|*grfRM*[in]|0이어야 합니다.|  
  
 세션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 Native Client OLE DB 공급자 행 집합은 행 집합 속성 DBPROP_ABORTPRESERVE 및 DBPROP_COMMITPRESERVE의 값에 따라 로컬 커밋 또는 중단 작업에서 유지 됩니다. 기본적으로 이러한 속성은 모두 VARIANT_FALSE 이며 세션의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 모든 Native Client OLE DB 공급자 행 집합은 중단 또는 커밋 작업 후에 손실 됩니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 **ITransactionObject** 인터페이스를 구현 하지 않습니다. 소비자가 인터페이스에 대한 참조를 얻으려고 하면 E_NOINTERFACE가 반환됩니다.  
  
 이 예에서는 **ITransactionLocal**을 사용합니다.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*   pIDBCreateSession   = NULL;  
ITransaction*       pITransaction       = NULL;  
IDBCreateCommand*   pIDBCreateCommand   = NULL;  
IRowset*            pIRowset            = NULL;  
  
HRESULT             hr;  
  
// Get the command creation and local transaction interfaces for the  
// session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
if (FAILED(hr = pIDBCreateCommand->QueryInterface(IID_ITransactionLocal,  
    (void**) &pITransaction)))  
    {  
    // Process error. Release any references and return.  
    }  
  
// Start the local transaction.  
if (FAILED(hr = ((ITransactionLocal*) pITransaction)->StartTransaction(  
    ISOLATIONLEVEL_REPEATABLEREAD, 0, NULL, NULL)))  
    {  
    // Process error from StartTransaction. Release any references and  
    // return.  
    }  
  
// Get data into a rowset, then update the data. Functions are not  
// illustrated in this example.  
if (FAILED(hr = ExecuteCommand(pIDBCreateCommand, &pIRowset)))  
    {  
    // Release any references and return.  
    }  
  
// If rowset data update fails, then terminate the transaction, else  
// commit. The example doesn't retain the rowset.  
if (FAILED(hr = UpdateDataInRowset(pIRowset, bDelayedUpdate)))  
    {  
    // Get error from update, then terminate.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, XACTTC_SYNC, 0)))  
        {  
        // Get error from failed commit.  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션을](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [스냅샷 격리 작업](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
