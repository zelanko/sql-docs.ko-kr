---
title: sys.dm_tran_active_snapshot_database_transactions (TRANSACT-SQL) | Microsoft Docs
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
- sys.dm_tran_active_snapshot_database_transactions_TSQL
- dm_tran_active_snapshot_database_transactions
- sys.dm_tran_active_snapshot_database_transactions
- dm_tran_active_snapshot_database_transactions_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_active_snapshot_database_transactions dynamic management view
ms.assetid: 55b83f9c-da10-4e65-9846-f4ef3c0c0f36
caps.latest.revision: 55
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7ef3ff9a4507474543a3d2049a56f7ce91f1eec2
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43068475"
---
# <a name="sysdmtranactivesnapshotdatabasetransactions-transact-sql"></a>sys.dm_tran_active_snapshot_database_transactions(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 이 동적 관리 뷰는 행 버전을 생성하거나 액세스할 수 있는 모든 활성 트랜잭션에 대한 가상 테이블을 반환합니다. 트랜잭션은 다음 중 하나 이상의 조건에서 포함됩니다.  
  
-   ALLOW_SNAPSHOT_ISOLATION 및 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션 중 하나 또는 둘 다가 ON으로 설정된 경우  
  
    -   스냅숏 격리 수준이나 행 버전 관리를 사용하는 커밋된 읽기 격리 수준에서 실행되는 각 트랜잭션에 대해 하나의 행이 있습니다.  
  
    -   현재 데이터베이스에서 행 버전이 생성되게 하는 각 트랜잭션에 대해 하나의 행이 있습니다. 예를 들어 트랜잭션은 현재 데이터베이스에서 행을 업데이트하거나 삭제하여 행 버전을 생성합니다.  
  
-   트리거가 발생하면 트리거를 실행하는 트랜잭션에 대해 하나의 행이 있습니다.  
  
-   온라인 인덱싱 프로시저가 실행되고 있으면 인덱스를 만드는 트랜잭션에 대해 하나의 행이 있습니다.  
  
-   MARS(Multiple Active Results Sets) 세션을 설정하면 행 버전에 액세스하는 각 트랜잭션에 대해 하나의 행이 있습니다.  
  
 이 동적 관리 뷰에는 시스템 트랜잭션이 포함되지 않습니다.  
  
> [!NOTE]  
>  이를 호출 하 [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 나 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], 이름을 사용 하 여 **sys.dm_pdw_nodes_tran_active_snapshot_database_transactions**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.dm_tran_active_snapshot_database_transactions  
```  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**transaction_id**|**bigint**|트랜잭션에 할당된 고유 ID입니다. 트랜잭션 ID는 주로 잠금 작업에서 트랜잭션을 식별하는 데 사용됩니다.|  
|**transaction_sequence_num**|**bigint**|트랜잭션 시퀀스 번호입니다. 트랜잭션 시작 시 해당 트랜잭션에 할당되는 고유 시퀀스 번호인 트랜잭션 시퀀스 번호입니다. 버전 레코드를 생성하지 않고 스냅숏 검색을 사용하지 않는 트랜잭션에는 트랜잭션 시퀀스 번호가 지정되지 않습니다.|  
|**commit_sequence_num**|**bigint**|트랜잭션이 완료(커밋 또는 중지)된 시기를 나타내는 시퀀스 번호입니다. 활성 트랜잭션의 경우 이 값은 NULL입니다.|  
|**is_snapshot**|**int**|0 = 스냅숏 격리 트랜잭션이 아닙니다.<br /><br /> 1 = 스냅숏 격리 트랜잭션입니다.|  
|**session_id**|**int**|트랜잭션을 시작한 세션의 ID입니다.|  
|**first_snapshot_sequence_num**|**bigint**|스냅숏을 만들 때 활성 상태인 트랜잭션의 가장 낮은 트랜잭션 시퀀스 번호입니다. 실행 시 스냅숏 트랜잭션이 해당 시점에서 활성 상태인 모든 트랜잭션의 스냅숏을 만듭니다. 스냅숏 트랜잭션이 아닌 경우 이 열에 0이 표시됩니다.|  
|**max_version_chain_traversed**|**int**|트랜잭션 측면에서 일관된 버전을 찾기 위해 이동한 버전 체인의 최대 길이입니다.|  
|**average_version_chain_traversed**|**real**|이동한 버전 체인의 평균 행 버전 수입니다.|  
|**elapsed_time_seconds**|**bigint**|트랜잭션이 트랜잭션 시퀀스 번호를 받은 이후 경과된 시간입니다.|  
|**pdw_node_id**|**int**|**적용 대상**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 이 배포에 있는 노드에 대 한 식별자입니다.|  
  
## <a name="permissions"></a>사용 권한

온 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 필요한 `VIEW SERVER STATE` 권한.   
온 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], 필요를 `VIEW DATABASE STATE` 데이터베이스의 권한.   

## <a name="remarks"></a>Remarks  
 **sys.dm_tran_active_snapshot_database_transactions** 는 XSN (트랜잭션 시퀀스 번호)에 할당 된 트랜잭션을 보고 합니다. 트랜잭션이 처음으로 버전 저장소에 액세스하면 XSN이 할당됩니다. 스냅숏 격리나 행 버전 관리를 사용하는 커밋된 읽기 격리가 설정된 데이터베이스에서 이 예는 XSN이 트랜잭션에 할당된 시기를 보여 줍니다.  
  
-   트랜잭션이 직렬화 가능 격리 수준에서 실행되는 경우 트랜잭션에서 행 버전이 생성되게 하는 UPDATE 작업 등의 문을 처음으로 실행할 때 XSN이 할당됩니다.  
  
-   트랜잭션이 스냅숏 격리에서 실행되는 경우 SELECT 작업 등의 DML(데이터 조작 언어) 문을 실행할 때 XSN이 할당됩니다.  
  
 트랜잭션 시퀀스 번호는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에서 시작된 트랜잭션마다 순차적으로 증가합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 ALLOW_SNAPSHOT_ISOLATION 및 READ_COMMITTED_SNAPSHOT 옵션이 ON으로 설정된 데이터베이스에서 각각 XSN(트랜잭션 시퀀스 번호)으로 식별되는 4개의 동시 트랜잭션이 실행되는 테스트 시나리오를 사용합니다. 다음 트랜잭션이 실행되고 있습니다.  
  
-   XSN-57은 직렬화 격리에서 실행되는 UPDATE 작업입니다.  
  
-   XSN-58은 XSN-57과 같습니다.  
  
-   XSN-59는 스냅숏 격리에서 실행되는 SELECT 작업입니다.  
  
-   XSN-60은 XSN-59와 같습니다.  
  
 다음 쿼리가 실행됩니다.  
  
```  
SELECT   
    transaction_id,  
    transaction_sequence_num,  
    commit_sequence_num,  
    is_snapshot session_id,  
    first_snapshot_sequence_num,  
    max_version_chain_traversed,  
    average_version_chain_traversed,  
    elapsed_time_seconds  
  FROM sys.dm_tran_active_snapshot_database_transactions;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_id  transaction_sequence_num  commit_sequence_num  
--------------  ------------------------  -------------------  
9295            57                        NULL  
9324            58                        NULL  
9387            59                        NULL  
9400            60                        NULL  
  
is_snapshot  session_id   first_snapshot_sequence_num  
-----------  -----------  ---------------------------  
0            54           0  
0            53           0  
1            52           57  
1            51           57  
  
max_version_chain_traversed  average_version_chain_traversed  
---------------------------  -------------------------------  
0                            0  
0                            0  
1                            1  
1                            1  
  
elapsed_time_seconds  
--------------------  
419  
397  
359  
333  
```  
  
 다음 정보를 평가 결과로 **sys.dm_tran_active_snapshot_database_transactions**:  
  
-   XSN-57:이 트랜잭션이 스냅숏 격리에서 실행 중이 아니므로 합니다 `is_snapshot` 값 및 `first_snapshot_sequence_num` 는 `0`합니다. ALLOW_SNAPSHOT_ISOLATION 또는 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션 중 하나 또는 둘 다가 ON이므로 `transaction_sequence_num`은 이 트랜잭션에 트랜잭션 시퀀스 번호가 할당되었음을 보여 줍니다.  
  
-   XSN-58:이 트랜잭션이 스냅숏 격리에서 실행 하지는 및 XSN-57에 대 한 동일한 정보를 적용 합니다.  
  
-   XSN-59:이 스냅숏 격리에서 실행 되는 첫 번째 활성 트랜잭션입니다. 이 트랜잭션은 `first_snapshot_sequence_num`에 표시된 대로 XSN-57 이전에 커밋된 데이터를 읽습니다. 또한 이 트랜잭션의 출력은 행에 대해 이동한 최대 버전 체인이 `1`이며 액세스한 각 행에 대해 평균 `1` 버전을 이동했음을 보여 줍니다. 이는 XSN-57, XSN-58 및 XSN-60 트랜잭션이 행을 수정하지 않고 커밋했음을 의미합니다.  
  
-   XSN-60:이 파일은 두 번째 트랜잭션이 스냅숏 격리에서 실행 합니다. 출력에 표시되는 정보는 XSN-59와 같습니다.  
  
## <a name="see-also"></a>관련 항목  
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  


