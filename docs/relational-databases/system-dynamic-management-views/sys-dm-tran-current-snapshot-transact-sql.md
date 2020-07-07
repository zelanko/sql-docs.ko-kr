---
title: sys. dm_tran_current_snapshot (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_current_snapshot_TSQL
- dm_tran_current_snapshot
- dm_tran_current_snapshot_TSQL
- sys.dm_tran_current_snapshot
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_current_snapshot dynamic management view
ms.assetid: 7509d595-c0e1-4237-a5ac-b41ad934544c
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5e35f7cc69508c9d0a98f78eb2a6ee9940098f86
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005555"
---
# <a name="sysdm_tran_current_snapshot-transact-sql"></a>sys.dm_tran_current_snapshot(Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  현재 스냅샷 트랜잭션이 시작될 때의 모든 활성 트랜잭션을 표시하는 가상 테이블을 반환합니다. 현재 트랜잭션이 스냅샷 트랜잭션이 아니면 이 함수는 행을 반환하지 않습니다. **dm_tran_current_snapshot** 은 sys. **dm_tran_transactions_snapshot**와 유사 합니다. 단, **dm_tran_current_snapshot** 는 현재 스냅숏 트랜잭션에 대 한 활성 트랜잭션만 반환 합니다.  
  
> [!NOTE]  
>  또는에서이를 호출 하려면 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 이름 **sys. dm_pdw_nodes_tran_current_snapshot**을 사용 합니다.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sys.dm_tran_current_snapshot  
```  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|활성 트랜잭션의 트랜잭션 시퀀스 번호입니다.|  
|pdw_node_id|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] ,[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포가 설정 된 노드의 식별자입니다.|  
  
## <a name="permissions"></a>권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="examples"></a>예  
 다음 예에서는 ALLOW_SNAPSHOT_ISOLATION 및 READ_COMMITTED_SNAPSHOT 옵션이 ON으로 설정된 데이터베이스에서 각각 XSN(트랜잭션 시퀀스 번호)으로 식별되는 4개의 동시 트랜잭션이 실행되는 테스트 시나리오를 사용합니다. 다음 트랜잭션이 실행되고 있습니다.  
  
-   XSN-57은 직렬화 격리에서 실행되는 UPDATE 작업입니다.  
  
-   XSN-58은 XSN-57과 같습니다.  
  
-   XSN-59는 스냅샷 격리에서 실행되는 SELECT 작업입니다.  
  
-   XSN-60은 XSN-59와 같습니다.  
  
 다음 쿼리는 XSN-59 범위 내에서 실행됩니다.  
  
```  
SELECT   
    transaction_sequence_num  
  FROM sys.dm_tran_current_snapshot;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num  
------------------------  
57  
58  
```  
  
 결과는 스냅샷 트랜잭션 XSN-59가 시작될 때 XSN-57과 XSN-58이 활성 상태였음을 보여 줍니다. XSN-57과 XSN-58이 커밋되거나 롤백된 후에도 스냅샷 트랜잭션이 완료될 때까지 동일한 결과가 지속됩니다.  
  
 XSN-60 범위 내에서 동일한 쿼리를 실행합니다.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num  
------------------------  
57  
58  
59  
```  
  
 XSN-60의 출력에는 XSN-59에 대해 표시되는 것과 같은 트랜잭션은 물론 XSN-60이 시작될 때 활성 상태였던 XSN-59도 포함됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;동적 관리 뷰 및 함수](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


