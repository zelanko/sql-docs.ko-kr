---
title: 로컬 트랜잭션 지원 | Microsoft Docs
description: SQL Server에 대 한 OLE DB 드라이버에서 로컬 트랜잭션
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- autocommit mode
- transactions [OLE DB]
- ITransactionLocal interface
- OLE DB Driver for SQL Server, transactions
- local transactions [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: de00c4aac3125209bb56a1867f07b1f395804cc8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="supporting-local-transactions"></a>로컬 트랜잭션 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  세션의 트랜잭션 범위는 OLE DB Driver for SQL Server 로컬 트랜잭션을를 구분합니다. 시기, 전문가 지도 소비자는 OLE DB Driver for SQL Server에 요청을 제출의 연결 된 인스턴스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], SQL Server 용 OLE DB Driver에 대 한 작업 단위를 구성 합니다. 로컬 트랜잭션은 항상 SQL Server 세션에 대 한 단일 OLE DB 드라이버에서 하나 이상의 작업 단위를 래핑합니다.  
  
 기본 OLE DB 드라이버를 사용 하 여 SQL Server 자동 커밋 모드에 대 한, 단일 작업 단위 로컬 트랜잭션 범위로 처리 됩니다. 하나의 단위만 로컬 트랜잭션에 참여합니다. 세션이 생성 되는 OLE DB Driver for SQL Server 세션에 대 한 트랜잭션을 시작 합니다. 작업 단위가 성공적으로 완료되면 해당 작업이 커밋됩니다. 실패하면 시작된 모든 작업이 롤백되며 소비자에게 오류가 반환됩니다. 두 경우 모두에 OLE DB Driver for SQL Server 트랜잭션 내에서 수행 하는 모든 작업을 세션에 대 한 새로운 로컬 트랜잭션을 시작 합니다.  
  
 OLE DB 드라이버에서 SQL Server 소비자를 사용 하 여 로컬 트랜잭션 범위에 대해 보다 세부적으로 제어를 전달할 수는 **ITransactionLocal** 인터페이스입니다. 소비자 세션이 트랜잭션을 시작, 모든 세션 작업 단위 트랜잭션 간의 시작 지점과 최종 **커밋** 또는 **중단** 메서드 호출은 원자 단위로 처리 됩니다. OLE DB Driver for SQL Server는 이렇게 하려면 소비자가 지시 하는 경우 트랜잭션을 암시적으로 시작 합니다. 소비자가 보존을 요청하지 않으면 세션은 일반적으로 자동 커밋 모드인 부모 트랜잭션 수준 동작으로 돌아갑니다.  
  
 OLE DB driver for SQL Server **itransactionlocal:: Starttransaction** 다음과 같이 매개 변수입니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*isoLevel*[in]|이 트랜잭션에 사용할 격리 수준입니다. 로컬 트랜잭션의 경우에 OLE DB Driver for SQL Server 다음을 지원합니다.<br /><br /> **ISOLATIONLEVEL_UNSPECIFIED**<br /><br /> **ISOLATIONLEVEL_CHAOS**<br /><br /> **ISOLATIONLEVEL_READUNCOMMITTED**<br /><br /> **ISOLATIONLEVEL_READCOMMITTED**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_CURSORSTABILITY**<br /><br /> **ISOLATIONLEVEL_REPEATABLEREAD**<br /><br /> **ISOLATIONLEVEL_SERIALIZABLE**<br /><br /> **ISOLATIONLEVEL_ISOLATED**<br /><br /> **ISOLATIONLEVEL_SNAPSHOT**<br /><br /> <br /><br /> 참고: 부터는 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], ISOLATIONLEVEL_SNAPSHOT를 사용할 수는 *isoLevel* 인수는 데이터베이스에 대 한 버전 관리가 활성화 여부입니다. 그러나 버전 관리가 설정되어 있지 않거나 데이터베이스가 읽기 전용이 아닌 상태에서 사용자가 문을 실행하려고 하면 오류가 발생합니다. 또한 하면 XACT_E_ISOLATIONLEVEL 오류가 ISOLATIONLEVEL_SNAPSHOT로 지정 된 경우 발생 됩니다는 *isoLevel* 의 버전에 연결 된 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이전의 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]합니다.|  
|*isoFlags*[in]|OLE DB Driver for SQL Server는 0이 아닌 모든 값에 대 한 오류를 반환합니다.|  
|*pOtherOptions*[in]|그렇지 않은 경우 null 인 경우에 OLE DB Driver for SQL Server 인터페이스에서 옵션 개체를 요청 합니다. 경우 XACT_E_NOTIMEOUT을 반환 하는 OLE DB Driver for SQL Server 옵션 개체의 *ulTimeout* 멤버가 0이 아닌 합니다. 값을 무시 하는 OLE DB Driver for SQL Server는 *szDescription* 멤버입니다.|  
|*pulTransactionLevel*[out]|아니면 null 인 경우에 OLE DB Driver for SQL Server에는 트랜잭션의 중첩된 수준을 반환 합니다.|  
  
 OLE DB Driver for SQL Server 로컬 트랜잭션에 대 한 구현 **itransaction:: Abort** 다음과 같이 매개 변수입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*pboidReason*[in]|설정된 경우 무시됩니다. NULL이어도 안전합니다.|  
|*fRetaining*[in]|TRUE인 경우 해당 세션을 위한 새 트랜잭션이 암시적으로 시작됩니다. 이 트랜잭션은 소비자가 커밋 또는 종료해야 합니다. FALSE 인 경우에 OLE DB Driver for SQL Server는 세션에 대 한 자동 커밋 모드로 되돌립니다.|  
|*fAsync*[in]|비동기 중단 SQL Server 용 OLE DB 드라이버에서 지원 되지 않습니다. 값이 FALSE 하는 경우는 OLE DB Driver for SQL Server는 XACT_E_NOTSUPPORTED를 반환 합니다.|  
  
 OLE DB Driver for SQL Server 로컬 트랜잭션에 대 한 구현 **itransaction:: Commit** 다음과 같이 매개 변수입니다.  
  
|매개 변수|설명|  
|---------------|-----------------|  
|*fRetaining*[in]|TRUE인 경우 해당 세션을 위한 새 트랜잭션이 암시적으로 시작됩니다. 이 트랜잭션은 소비자가 커밋 또는 종료해야 합니다. FALSE 인 경우에 OLE DB Driver for SQL Server는 세션에 대 한 자동 커밋 모드로 되돌립니다.|  
|*grfTC*[in]|비동기 및 1 단계 반환 SQL Server 용 OLE DB 드라이버에서 지원 되지 않습니다. OLE DB Driver for SQL Server xacttc_sync 외의 다른 모든 값에 대 한 XACT_E_NOTSUPPORTED를 반환합니다.|  
|*grfRM*[in]|0이어야 합니다.|  
  
 OLE DB Driver for SQL Server 세션에서 행 집합 로컬 커밋에 유지 하거나 작업을 중단 DBPROP_ABORTPRESERVE 및 DBPROP_COMMITPRESERVE 행 집합 속성의 값에 기반 합니다. 기본적으로 이러한 속성은 모두 VARIANT_FALSE 및 모든 OLE DB Driver for SQL Server 세션에서 행 집합에 있도록 중단 손실 커밋하거나 작업입니다.  
  
 OLE DB Driver for SQL Server를 구현 하지 않습니다는 **ITransactionObject** 인터페이스입니다. 소비자가 인터페이스에 대한 참조를 얻으려고 하면 E_NOINTERFACE가 반환됩니다.  
  
 이 예에서는 **ITransactionLocal**합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [트랜잭션](../../oledb/ole-db-transactions/transactions.md)   
 [스냅숏 격리 작업](../../oledb/features/working-with-snapshot-isolation.md)  
  
  
