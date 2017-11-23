---
title: "분산된 트랜잭션 지원 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-transactions
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- SQL Server Native Client OLE DB provider, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
ms.assetid: d250b43b-9260-4ea4-90cc-57d9a2f67ea7
caps.latest.revision: "28"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2085ae56343197b7ddb71c094f356d229baf8ed6
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="supporting-distributed-transactions"></a>분산 트랜잭션 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 소비자가 사용할 수는 **itransactionjoin:: Jointransaction** Microsoft Distributed Transaction Coordinator (MS DTC)에 의해 메서드는 분산된 트랜잭션에 참여할를 조정 합니다.  
  
 MS DTC는 클라이언트가 여러 데이터 저장소에 대한 둘 이상의 연결에서 통합 트랜잭션을 시작하거나 통합 트랜잭션에 참가하는 데 사용할 수 있는 COM 개체를 제공합니다. 트랜잭션을 초기화 하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 MS DTC를 사용 하 여 **ITransactionDispenser** 인터페이스입니다. **BeginTransaction** 소속 **ITransactionDispenser** 분산된 트랜잭션 개체에 대 한 참조를 반환 합니다. 이 참조가 전달 되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자를 사용 하 여 **JoinTransaction**합니다.  
  
 MS DTC는 분산 트랜잭션에 대해 비동기 커밋 및 중단을 지원합니다. 소비자에 대 한 알림을 비동기 트랜잭션 상태를 구현는 **ITransactionOutcomeEvents** 인터페이스 및 인터페이스는 MS DTC 트랜잭션 개체에 연결 합니다.  
  
 분산 트랜잭션에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자가 구현 하 **itransactionjoin:: Jointransaction** 다음과 같이 매개 변수입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*punkTransactionCoord*|MS DTC 트랜잭션 개체에 대한 포인터입니다.|  
|*IsoLevel*|무시 된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자입니다. MS DTC 통합 트랜잭션의 격리 수준은 소비자가 MS DTC로부터 트랜잭션 개체를 가져올 때 결정됩니다.|  
|*IsoFlags*|0이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 소비자가 다른 값을 지정 하는 Native Client OLE DB 공급자가 XACT_E_NOISORETAIN을 반환 합니다.|  
|*POtherOptions*|NULL이 아닌 경우는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 인터페이스에서 옵션 개체를 요청 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 경우 XACT_E_NOTIMEOUT을 반환 옵션 개체의 *ulTimeout* 멤버가 0이 아닌 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자의 값을 무시 된 *szDescription* 멤버입니다.|  
  
 이 예에서는 MS DTC를 사용하여 트랜잭션을 관리합니다.  
  
```  
// Interfaces used in the example.  
IDBCreateSession*       pIDBCreateSession   = NULL;  
ITransactionJoin*       pITransactionJoin   = NULL;  
IDBCreateCommand*       pIDBCreateCommand   = NULL;  
IRowset*                pIRowset            = NULL;  
  
// Transaction dispenser and transaction from MS DTC.  
ITransactionDispenser*  pITransactionDispenser = NULL;  
ITransaction*           pITransaction       = NULL;  
  
    HRESULT             hr;  
  
// Get the command creation interface for the session.  
if (FAILED(hr = pIDBCreateSession->CreateSession(NULL,  
     IID_IDBCreateCommand, (IUnknown**) &pIDBCreateCommand)))  
    {  
    // Process error from session creation. Release any references and  
    // return.  
    }  
  
// Get a transaction dispenser object from MS DTC and  
// start a transaction.  
if (FAILED(hr = DtcGetTransactionManager(NULL, NULL,  
    IID_ITransactionDispenser, 0, 0, NULL,  
    (void**) &pITransactionDispenser)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
if (FAILED(hr = pITransactionDispenser->BeginTransaction(  
    NULL, ISOLATIONLEVEL_READCOMMITTED, ISOFLAG_RETAIN_DONTCARE,  
    NULL, &pITransaction)))  
    {  
    // Process error message from MS DTC, release any references,  
    // and then return.  
    }  
  
// Join the transaction.  
if (FAILED(pIDBCreateCommand->QueryInterface(IID_ITransactionJoin,  
    (void**) &pITransactionJoin)))  
    {  
    // Process failure to get an interface, release any references, and  
    // then return.  
    }  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) pITransaction, 0, 0, NULL)))  
    {  
    // Process join failure, release any references, and then return.  
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
    // Get error from update, then abort.  
    pITransaction->Abort(NULL, FALSE, FALSE);  
    }  
else  
    {  
    if (FAILED(hr = pITransaction->Commit(FALSE, 0, 0)))  
        {  
        // Get error from failed commit.  
        //  
        // If a distributed commit fails, application logic could  
        // analyze failure and retry. In this example, terminate. The   
        // consumer must resolve this somehow.  
        pITransaction->Abort(NULL, FALSE, FALSE);  
        }  
    }  
  
if (FAILED(hr))  
    {  
    // Update of data or commit failed. Release any references and  
    // return.  
    }  
  
// Un-enlist from the distributed transaction by setting   
// the transaction object pointer to NULL.  
if (FAILED(pITransactionJoin->JoinTransaction(  
    (IUnknown*) NULL, 0, 0, NULL)))  
    {  
    // Process failure, and then return.  
    }  
  
// Release any references and continue.  
```  
  
## <a name="see-also"></a>관련 항목:  
 [의](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
