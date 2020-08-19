---
description: SQL Server Native Client에서 분산 트랜잭션 지원
title: 분산 트랜잭션 지원 (Native Client OLE DB 공급자)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4512cea869bae06bde3343db1487e060a35928b7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88498983"
---
# <a name="supporting-distributed-transactions-in-sql-server-native-client"></a>SQL Server Native Client에서 분산 트랜잭션 지원
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자 소비자는 **ITransactionJoin:: JoinTransaction** 메서드를 사용 하 여 MS DTC (Microsoft DTC(Distributed Transaction Coordinator))에서 조정 하는 분산 트랜잭션에 참여할 수 있습니다.  
  
 MS DTC는 클라이언트가 여러 데이터 저장소에 대한 둘 이상의 연결에서 통합 트랜잭션을 시작하거나 통합 트랜잭션에 참가하는 데 사용할 수 있는 COM 개체를 제공합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자 소비자는 트랜잭션을 시작 하기 위해 MS DTC **ITransactionDispenser** 인터페이스를 사용 합니다. **ITransactionDispenser**의 **BeginTransaction** 멤버는 분산 트랜잭션 개체에 대한 참조를 반환합니다. 이 참조는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **JoinTransaction**을 사용 하 여 Native Client OLE DB 공급자로 전달 됩니다.  
  
 MS DTC는 분산 트랜잭션에 대해 비동기 커밋 및 중단을 지원합니다. 비동기 트랜잭션 상태에 대한 알림을 제공하려면 소비자는 **ITransactionOutcomeEvents** 인터페이스를 구현하고 이 인터페이스를 MS DTC 트랜잭션 개체에 연결합니다.  
  
 분산 트랜잭션의 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 다음과 같이 **ITransactionJoin:: JoinTransaction** 매개 변수를 구현 합니다.  
  
|매개 변수|Description|  
|---------------|-----------------|  
|*punkTransactionCoord*|MS DTC 트랜잭션 개체에 대한 포인터입니다.|  
|*IsoLevel*|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자가 무시 합니다. MS DTC 통합 트랜잭션의 격리 수준은 소비자가 MS DTC로부터 트랜잭션 개체를 가져올 때 결정됩니다.|  
|*IsoFlags*|0이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]소비자가 다른 값을 지정 하는 경우 Native Client OLE DB 공급자는 XACT_E_NOISORETAIN를 반환 합니다.|  
|*POtherOptions*|NULL이 아닌 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB 공급자는 인터페이스에서 options 개체를 요청 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]옵션 개체의 *ultimeout* 멤버가 0이 아니면 Native Client OLE DB 공급자가 XACT_E_NOTIMEOUT을 반환 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client OLE DB 공급자는 *szdescription* 멤버의 값을 무시 합니다.|  
  
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
 [트랜잭션](../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
  
