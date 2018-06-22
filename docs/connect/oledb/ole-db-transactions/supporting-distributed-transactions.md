---
title: 분산된 트랜잭션 지원 | Microsoft Docs
description: SQL Server 용 OLE DB 드라이버에서 분산된 트랜잭션
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-transactions
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 469f72b416e1e262d2a775b1b49e14723a44b171
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35690306"
---
# <a name="supporting-distributed-transactions"></a>분산 트랜잭션 지원
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 소비자가 사용할 수는 **itransactionjoin:: Jointransaction** Microsoft Distributed Transaction Coordinator (MS DTC)에 의해 메서드는 분산된 트랜잭션에 참여할를 조정 합니다.  
  
 MS DTC는 클라이언트가 여러 데이터 저장소에 대한 둘 이상의 연결에서 통합 트랜잭션을 시작하거나 통합 트랜잭션에 참가하는 데 사용할 수 있는 COM 개체를 제공합니다. 트랜잭션을 시작, OLE DB 드라이버에서 SQL Server 소비자 사용 하 여 MS DTC **ITransactionDispenser** 인터페이스입니다. **BeginTransaction** 소속 **ITransactionDispenser** 분산된 트랜잭션 개체에 대 한 참조를 반환 합니다. 이 참조가 사용 하 여 SQL Server에 대 한 OLE DB 드라이버에 전달 되 **JoinTransaction**합니다.  
  
 MS DTC는 분산 트랜잭션에 대해 비동기 커밋 및 중단을 지원합니다. 소비자에 대 한 알림을 비동기 트랜잭션 상태를 구현는 **ITransactionOutcomeEvents** 인터페이스 및 인터페이스는 MS DTC 트랜잭션 개체에 연결 합니다.  
  
 OLE DB Driver for SQL Server 분산된 트랜잭션에 대 한 구현 **itransactionjoin:: Jointransaction** 다음과 같이 매개 변수입니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*punkTransactionCoord*|MS DTC 트랜잭션 개체에 대한 포인터입니다.|  
|*IsoLevel*|SQL Server 용 OLE DB 드라이버에서 무시 됩니다. MS DTC 통합 트랜잭션의 격리 수준은 소비자가 MS DTC로부터 트랜잭션 개체를 가져올 때 결정됩니다.|  
|*IsoFlags*|0이어야 합니다. OLE DB Driver for SQL Server 소비자가 다른 값을 지정 하는 XACT_E_NOISORETAIN을 반환 합니다.|  
|*POtherOptions*|그렇지 않은 경우 null 인 경우에 OLE DB Driver for SQL Server 인터페이스에서 옵션 개체를 요청 합니다. 경우 XACT_E_NOTIMEOUT을 반환 하는 OLE DB Driver for SQL Server 옵션 개체의 *ulTimeout* 멤버가 0이 아닌 합니다. 값을 무시 하는 OLE DB Driver for SQL Server는 *szDescription* 멤버입니다.|  
  
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
  
## <a name="see-also"></a>관련 항목  
 [의](../../oledb/ole-db-transactions/transactions.md)  
  
  
