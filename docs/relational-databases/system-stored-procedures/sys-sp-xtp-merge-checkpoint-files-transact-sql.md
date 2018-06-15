---
title: sys.sp_xtp_merge_checkpoint_files (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
caps.latest.revision: 15
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1bc2c91d93ad24147fa288ffb8164823f4f8a84c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33259693"
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **sys.sp_xtp_merge_checkpoint_files** 지정 된 트랜잭션 범위에서 모든 데이터 및 델타 파일을 병합 합니다.  
  
 자세한 내용은 참조 [저장소 만들기 및 관리 메모리 액세스에 최적화 개체에 대 한](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**참고**:이 저장된 프로시저에서 사용 되지 않는 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다. 더 이상 필요 하 고 사용할 수 없습니다, 시작 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]합니다.|  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 병합을 호출할 데이터베이스의 이름입니다. 데이터베이스에 메모리 테이블이 없는 경우 이 프로시저는 사용자 오류를 반환합니다. 데이터베이스가 오프라인인 경우 오류를 반환합니다.  
  
 *lower_bound_Tid*  
 에 표시 된 대로 데이터 파일에 대 한 트랜잭션 (bigint) 하 한 [sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) 병합 시작 검사점 파일에 해당 합니다. 트랜잭션 ID 값이 잘못된 경우 오류가 생성됩니다.  
  
 *upper_bound_Tid*  
 에 표시 된 대로 데이터 파일에 대 한 트랜잭션 (bigint) 상한 [sys.dm_db_xtp_checkpoint_files &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)합니다. 트랜잭션 ID 값이 잘못된 경우 오류가 생성됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 InclusionThresholdSetting  
  
## <a name="cursors-returned"></a>반환되는 커서  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>Permissions  
 sysadmin 고정 서버 역할 및 db_owner 고정 데이터베이스 역할이 필요합니다.  
  
## <a name="remarks"></a>주의  
 단일 데이터 및 델타 파일을 생성하려면 유효한 범위에 있는 모든 데이터 및 델타 파일을 병합합니다. 이 프로시저는 병합 정책을 준수하지 않습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
