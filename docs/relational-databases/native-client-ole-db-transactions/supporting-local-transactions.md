---
title: 로컬 트랜잭션 지원 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- SQL Server Native Client OLE DB provider, transactions
- local transactions [OLE DB]
ms.assetid: 78f2e5fc-b6fb-4eda-9f71-991a4d6c4902
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 399951305556626b634eeb8e7ef2a2344dd080d6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37409375"
---
# <a name="supporting-local-transactions"></a>로컬 트랜잭션 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  세션의 트랜잭션 범위를 구분을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 로컬 트랜잭션의 합니다. 소비자의 방향에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 인스턴스에 연결된 하는 요청을 제출 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 요청에 대 한 작업 단위가 구성는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. 로컬 트랜잭션을 항상 단일 작업의 하나 이상의 단위를 래핑할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션입니다.  
  
 기본값을 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 자동 커밋 모드는 단일 작업 단위 로컬 트랜잭션 범위로 처리 됩니다. 하나의 단위만 로컬 트랜잭션에 참여합니다. 세션이 만들어지면는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션의 트랜잭션을 시작 합니다. 작업 단위가 성공적으로 완료되면 해당 작업이 커밋됩니다. 실패하면 시작된 모든 작업이 롤백되며 소비자에게 오류가 반환됩니다. 두 경우 모두는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 트랜잭션 내에서 수행 하는 모든 작업 세션에 대 한 새 로컬 트랜잭션을 시작 합니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자를 사용 하 여 로컬 트랜잭션 범위에 대해 보다 정확한 제어를 전달할 수 있습니다 합니다 **ITransactionLocal** 인터페이스입니다. 모든 세션 작업 단위 트랜잭션 간의 시작 지점과 최종 소비자 세션이 트랜잭션을 시작 하는 경우 **커밋** 하거나 **중단** 메서드 호출을 원자 단위로 처리 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자가 이렇게 하려면 지시 하는 경우 트랜잭션을 암시적으로 시작 합니다. 소비자가 보존을 요청하지 않으면 세션은 일반적으로 자동 커밋 모드인 부모 트랜잭션 수준 동작으로 돌아갑니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 지원 **itransactionlocal:: Starttransaction** 다음과 같은 매개 변수입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*isoLevel*[in]|이 트랜잭션에 사용할 격리 수준입니다. 로컬 트랜잭션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음을 지원 합니다.<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE로**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 참고: 부터는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], isolationlevel_snapshot을 합니다 *isoLevel* 인수는 데이터베이스에 대 한 버전 관리가 활성화 여부입니다. 그러나 버전 관리가 설정되어 있지 않거나 데이터베이스가 읽기 전용이 아닌 상태에서 사용자가 문을 실행하려고 하면 오류가 발생합니다. XACT_E_ISOLATIONLEVEL 오류가 또한 ISOLATIONLEVEL_SNAPSHOT로 지정 된 경우 발생 합니다 *isoLevel* 의 버전에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]합니다.|  
|*isoFlags*[in]|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 0이 아닌 모든 값에 대 한 오류를 반환 합니다.|  
|*pOtherOptions*[in]|NULL이 아닌 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 인터페이스에서 옵션 개체를 요청 합니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 경우 XACT_E_NOTIMEOUT을 반환 옵션 개체의 *ulTimeout* 멤버가 0이 아닙니다. 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 값을 무시 합니다 *szDescription* 멤버입니다.|  
|*pulTransactionLevel*[out]|NULL이 아닌 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 트랜잭션의 중첩된 수준을 반환 합니다.|  
  
 로컬 트랜잭션의 경우 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 구현 **itransaction:: Abort** 다음과 같은 매개 변수입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*pboidReason*[in]|설정된 경우 무시됩니다. NULL이어도 안전합니다.|  
|*fRetaining*[in]|TRUE인 경우 해당 세션을 위한 새 트랜잭션이 암시적으로 시작됩니다. 이 트랜잭션은 소비자가 커밋 또는 종료해야 합니다. FALSE 인 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션에 대 한 자동 커밋 모드로 되돌아갑니다.|  
|*fAsync*[in]|비동기 중단에서 지원 되지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 값 FALSE 이면 XACT_E_NOTSUPPORTED를 반환 합니다.|  
  
 로컬 트랜잭션의 경우 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 구현 **itransaction::** 다음과 같은 매개 변수입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*fRetaining*[in]|TRUE인 경우 해당 세션을 위한 새 트랜잭션이 암시적으로 시작됩니다. 이 트랜잭션은 소비자가 커밋 또는 종료해야 합니다. FALSE 인 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 세션에 대 한 자동 커밋 모드로 되돌아갑니다.|  
|*grfTC*[in]|비동기 및 1 단계 반환 하 여 지원 되지 않습니다는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 xacttc_sync 값 XACT_E_NOTSUPPORTED를 반환 합니다.|  
|*grfRM*[in]|0이어야 합니다.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 집합 세션에서 로컬 커밋 시 유지 됩니다 또는 행 집합 속성 DBPROP_ABORTPRESERVE 및 DBPROP_COMMITPRESERVE 값을 기반으로 하는 작업을 중단 합니다. 기본적으로 이러한 속성은 모두 VARIANT_FALSE 및, 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 행 집합에서 세션 중단 또는 커밋 작업 손실 됩니다.  
  
 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 구현 하지 않는 합니다 **ITransactionObject** 인터페이스입니다. 소비자가 인터페이스에 대한 참조를 얻으려고 하면 E_NOINTERFACE가 반환됩니다.  
  
 이 예제에서는 **ITransactionLocal**합니다.  
  
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
  
## <a name="see-also"></a>관련 항목  
 [트랜잭션](../../relational-databases/native-client-ole-db-transactions/transactions.md)   
 [스냅숏 격리 작업](../../relational-databases/native-client/features/working-with-snapshot-isolation.md)  
  
  
