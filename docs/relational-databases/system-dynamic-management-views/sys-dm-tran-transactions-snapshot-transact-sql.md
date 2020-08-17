---
description: sys.dm_tran_transactions_snapshot(Transact-SQL)
title: sys. dm_tran_transactions_snapshot (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_transactions_snapshot
- dm_tran_transactions_snapshot
- sys.dm_tran_transactions_snapshot_TSQL
- dm_tran_transactions_snapshot_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_transactions_snapshot dynamic management view
ms.assetid: 03f64883-07ad-4092-8be0-31973348c647
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f7497dbdce71e0989cc6bfa06da0acbaea118dbd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88323739"
---
# <a name="sysdm_tran_transactions_snapshot-transact-sql"></a>sys.dm_tran_transactions_snapshot(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  각 스냅숏 트랜잭션이 시작 될 때 활성 상태인 트랜잭션의 **sequence_number** 에 대 한 가상 테이블을 반환 합니다. 이 뷰에서 반환되는 정보는 다음 작업을 수행하는 데 도움이 됩니다.  
  
-   현재 활성 스냅샷 트랜잭션 수를 찾습니다.  
  
-   특정 스냅샷 트랜잭션에서 무시하는 데이터 수정 내용을 식별합니다. 스냅샷 트랜잭션이 시작될 때 활성 상태인 트랜잭션의 경우 트랜잭션이 커밋된 후에도 스냅샷 트랜잭션이 해당 트랜잭션에 의한 데이터 수정 내용을 모두 무시합니다.  
  
 예를 들어, **dm_tran_transactions_snapshot**에서 다음 출력을 고려 하십시오.  
  
```  
transaction_sequence_num snapshot_id snapshot_sequence_num  
------------------------ ----------- ---------------------  
59                       0           57  
59                       0           58  
60                       0           57  
60                       0           58  
60                       0           59  
60                       3           57  
60                       3           58  
60                       3           59  
60                       3           60  
```  
  
 `transaction_sequence_num` 열은 현재 스냅샷 트랜잭션의 XSN(트랜잭션 시퀀스 번호)을 식별합니다. 이 출력은 `59`와 `60`의 두 번호를 표시합니다. `snapshot_sequence_num` 열은 각 스냅샷 트랜잭션이 시작될 때 활성 상태인 트랜잭션의 트랜잭션 시퀀스 번호를 식별합니다.  
  
 이 출력은 두 개의 활성 트랜잭션인 XSN-57과 XSN-58이 실행되는 동안 스냅샷 트랜잭션 XSN-59가 시작됨을 보여 줍니다. XSN-57 또는 XSN-58에서 데이터를 수정할 경우 XSN-59는 이 변경 내용을 무시하고 행 버전 관리를 사용하여 트랜잭션이 일관된 데이터베이스 뷰를 유지 관리합니다.  
  
 스냅샷 트랜잭션 XSN-60은 XSN-57 및 XSN-58은 물론 XSN 59에 의한 데이터 수정 내용도 무시합니다.  
  
## <a name="table-returned"></a>반환된 테이블  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|스냅샷 트랜잭션의 XSN(트랜잭션 시퀀스 번호)입니다.|  
|**snapshot_id**|**int**|행 버전 관리를 사용하여 커밋된 읽기 스냅샷으로 시작된 각 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문의 스냅샷 ID입니다. 이 값은 행 버전 관리를 사용하여 커밋된 읽기로 실행되는 각 쿼리를 지원하는 트랜잭션이 일관된 데이터베이스 뷰를 생성하는 데 사용됩니다.|  
|**snapshot_sequence_num**|**bigint**|스냅샷 트랜잭션 시작 당시 활성화된 트랜잭션의 트랜잭션 시퀀스 번호입니다.|  
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 `VIEW SERVER STATE` 권한이 필요 합니다.   
[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]Premium 계층에서는 데이터베이스에 대 한 권한이 필요 합니다 `VIEW DATABASE STATE` . [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   
  
## <a name="remarks"></a>설명  
 스냅샷 트랜잭션이 시작될 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 해당 시점에 활성 상태인 모든 트랜잭션을 기록합니다. **dm_tran_transactions_snapshot** 현재 활성 상태인 모든 스냅숏 트랜잭션에 대해이 정보를 보고 합니다.  
  
 각 트랜잭션은 트랜잭션이 시작될 때 할당된 트랜잭션 시퀀스 번호로 식별됩니다. 트랜잭션은 BEGIN TRANSACTION 또는 BEGIN WORK 문이 실행될 때 시작됩니다. 그러나 [!INCLUDE[ssDE](../../includes/ssde-md.md)]은 BEGIN TRANSACTION 또는 BEGIN WORK 문 이후 데이터에 액세스하는 첫 번째 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행할 때 트랜잭션 시퀀스 번호를 할당합니다. 트랜잭션 시퀀스 번호는 1씩 증가합니다.  
  
## <a name="see-also"></a>참고 항목  
 [동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [트랜잭션 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  

