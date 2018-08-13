---
title: sys.dm_tran_current_transaction (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_current_transaction
- sys.dm_tran_current_transaction_TSQL
- dm_tran_current_transaction_TSQL
- dm_tran_current_transaction
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_current_transaction dynamic management view
ms.assetid: 75d5697d-b390-4963-99b8-fa0b4244a40c
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: a6ad21884497725d9aadd07f1b681eaef76355c0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39533003"
---
# <a name="sysdmtrancurrenttransaction-transact-sql"></a>sys.dm_tran_current_transaction(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  현재 세션에 있는 트랜잭션의 상태 정보를 표시하는 단일 행을 반환합니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_tran_current_transaction**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_tran_current_transaction  
```  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|현재 스냅숏의 트랜잭션 ID입니다.|  
|**transaction_sequence_num**|**bigint**|레코드 버전을 생성하는 트랜잭션 시퀀스 번호입니다.|  
|**transaction_is_snapshot**|**bit**|스냅숏 격리 상태입니다. 트랜잭션이 스냅숏 격리 상태에서 시작된 경우 이 값은 1입니다. 그렇지 않으면 값이 0입니다.|  
|**first_snapshot_sequence_num**|**bigint**|스냅숏을 만들 때 활성 상태인 트랜잭션의 가장 낮은 트랜잭션 시퀀스 번호입니다. 실행 시 스냅숏 트랜잭션이 해당 시점에서 활성 상태인 모든 트랜잭션의 스냅숏을 만듭니다. 스냅숏 트랜잭션이 아닌 경우 이 열에 0이 표시됩니다.|  
|**last_transaction_sequence_num**|**bigint**|전역 시퀀스 번호입니다. 이 값은 시스템에서 생성된 마지막 트랜잭션 시퀀스 번호를 나타냅니다.|  
|**first_useful_sequence_num**|**bigint**|전역 시퀀스 번호입니다. 이 값은 버전 저장소에 보관해야 하는 행 버전이 있는 트랜잭션의 가장 오래된 트랜잭션 시퀀스 번호를 나타냅니다. 이전 트랜잭션에서 만든 행 버전을 제거할 수 있습니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   
  
## <a name="examples"></a>예  
 다음 예에서는 ALLOW_SNAPSHOT_ISOLATION 및 READ_COMMITTED_SNAPSHOT 옵션이 ON으로 설정된 데이터베이스에서 각각 XSN(트랜잭션 시퀀스 번호)으로 식별되는 4개의 동시 트랜잭션이 실행되는 테스트 시나리오를 사용합니다. 다음 트랜잭션이 실행되고 있습니다.  
  
-   XSN-57은 직렬화 격리에서 실행되는 UPDATE 작업입니다.  
  
-   XSN-58은 XSN-57과 같습니다.  
  
-   XSN-59는 스냅숏 격리에서 실행되는 SELECT 작업입니다.  
  
-   XSN-60은 XSN-59와 같습니다.  
  
 다음 쿼리는 각 트랜잭션 범위 내에서 실행됩니다.  
  
```  
SELECT   
    transaction_id  
   ,transaction_sequence_num  
   ,transaction_is_snapshot  
   ,first_snapshot_sequence_num  
   ,last_transaction_sequence_num  
   ,first_useful_sequence_num  
  FROM sys.dm_tran_current_transaction;  
```  
  
 XSN-59의 결과는 다음과 같습니다.  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9387                 59                       1                         
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
57                               61                        
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 출력은 XSN-59가 XSN-59 시작 시 활성 상태였던 XSN-57을 첫 번째 트랜잭션으로 사용하는 스냅숏 트랜잭션임을 보여 줍니다. 즉, XSN-59는 XSN-57보다 낮은 트랜잭션 시퀀스 번호를 가진 트랜잭션이 커밋한 데이터를 읽습니다.  
  
 XSN-57의 결과는 다음과 같습니다.  
  
```  
transaction_id       transaction_sequence_num transaction_is_snapshot  
-------------------- ------------------------ -----------------------  
9295                 57                       0  
  
first_snapshot_sequence_num last_transaction_sequence_num  
--------------------------- -----------------------------  
NULL                        61  
  
first_useful_sequence_num  
-------------------------  
57  
```  
  
 XSN-57은 스냅숏 트랜잭션이 아니므로 `first_snapshot_sequence_num`은 `NULL`입니다.  
  
## <a name="see-also"></a>관련 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


