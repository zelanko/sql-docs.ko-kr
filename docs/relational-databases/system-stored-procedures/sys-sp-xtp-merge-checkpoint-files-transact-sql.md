---
description: sys.sp_xtp_merge_checkpoint_files(Transact-SQL)
title: sys. sp_xtp_merge_checkpoint_files (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9bd9412dd63c8fa167fde614992b255508eea6b3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88473386"
---
# <a name="syssp_xtp_merge_checkpoint_files-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files(Transact-SQL)
[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

  **sp_xtp_merge_checkpoint_files** 지정 된 트랜잭션 범위에 있는 모든 데이터 및 델타 파일을 병합 합니다.  
  
 자세한 내용은 [메모리 액세스에 최적화 된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)를 참조 하세요.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**참고**:이 저장 프로시저는에서 더 이상 사용 되지 않습니다 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] . 더 이상 필요 하지 않으므로를 사용 하 여 시작할 수 없습니다 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] .|  
  
## <a name="syntax"></a>구문  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 병합을 호출할 데이터베이스의 이름입니다. 데이터베이스에 메모리 테이블이 없는 경우 이 프로시저는 사용자 오류를 반환합니다. 데이터베이스가 오프라인인 경우 오류를 반환합니다.  
  
 *lower_bound_Tid*  
 Dm_db_xtp_checkpoint_files에 표시 된 것 처럼 데이터 파일에 대 한 트랜잭션 (bigint)의 하한값은 병합 시작 검사점 파일에 해당 하는 [transact-sql&#41;&#40;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) . 트랜잭션 ID 값이 잘못된 경우 오류가 생성됩니다.  
  
 *upper_bound_Tid*  
 [Dm_db_xtp_checkpoint_files &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)에 표시 되는 데이터 파일의 트랜잭션 (bigint) 상한입니다. 트랜잭션 ID 값이 잘못된 경우 오류가 생성됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 None  
  
## <a name="cursors-returned"></a>반환되는 커서  
 None  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할 및 db_owner 고정 데이터베이스 역할이 필요합니다.  
  
## <a name="remarks"></a>설명  
 단일 데이터 및 델타 파일을 생성하려면 유효한 범위에 있는 모든 데이터 및 델타 파일을 병합합니다. 이 프로시저는 병합 정책을 준수하지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;시스템 저장 프로시저 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
