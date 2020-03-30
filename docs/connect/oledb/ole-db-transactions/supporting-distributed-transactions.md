---
title: 분산 트랜잭션 지원 | Microsoft Docs
description: OLE DB Driver for SQL Server의 분산 트랜잭션
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, transactions
- distributed transactions [OLE DB]
- MS DTC
- transactions [OLE DB]
- OLE DB Driver for SQL Server, transactions
- ITransactionJoin interface
- MS DTC, about distributed transaction support
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 22527cdfa08907dfdf120ef32c918ecb9eaf86bb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "67993981"
---
# <a name="supporting-distributed-transactions"></a>분산 트랜잭션 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server용 OLE DB 드라이버 소비자는 **ITransactionJoin::JoinTransaction** 메서드를 사용하여 MS DTC(Microsoft Distributed Transaction Coordinator)가 관리하는 분산 트랜잭션에 참가할 수 있습니다.  
  
 MS DTC는 클라이언트가 여러 데이터 저장소에 대한 둘 이상의 연결에서 통합 트랜잭션을 시작하거나 통합 트랜잭션에 참가하는 데 사용할 수 있는 COM 개체를 제공합니다. OLE DB Driver for SQL Server 소비자는 MS DTC **ITransactionDispenser** 인터페이스를 사용하여 트랜잭션을 시작합니다. **ITransactionDispenser**의 **BeginTransaction** 멤버는 분산 트랜잭션 개체에 대한 참조를 반환합니다. 이 참조는 **JoinTransaction**을 사용하여 OLE DB Driver for SQL Server에 전달됩니다.  
  
 MS DTC는 분산 트랜잭션에 대해 비동기 커밋 및 중단을 지원합니다. 비동기 트랜잭션 상태에 대한 알림을 제공하려면 소비자는 **ITransactionOutcomeEvents** 인터페이스를 구현하고 이 인터페이스를 MS DTC 트랜잭션 개체에 연결합니다.  
  
 분산 트랜잭션의 경우 SQL Server용 OLE DB 드라이버는 다음과 같이 **ITransactionJoin::JoinTransaction** 매개 변수를 구현합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*punkTransactionCoord*|MS DTC 트랜잭션 개체에 대한 포인터입니다.|  
|*IsoLevel*|OLE DB Driver for SQL Server에서 무시합니다. MS DTC 통합 트랜잭션의 격리 수준은 소비자가 MS DTC로부터 트랜잭션 개체를 가져올 때 결정됩니다.|  
|*IsoFlags*|0이어야 합니다. 소비자가 다른 값을 지정하면 OLE DB Driver for SQL Server는 XACT_E_NOISORETAIN을 반환합니다.|  
|*POtherOptions*|NULL이 아니면 OLE DB Driver for SQL Server는 인터페이스에서 옵션 개체를 요청합니다. 옵션 개체의 *ulTimeout* 멤버가 0이 아닌 경우 OLE DB Driver for SQL Server는 XACT_E_NOTIMEOUT을 반환합니다. OLE DB Driver for SQL Server는 *szDescription* 멤버의 값을 무시합니다.|  
  
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
  
## <a name="see-also"></a>참고 항목  
 [트랜잭션](../../oledb/ole-db-transactions/transactions.md)  
  
  
