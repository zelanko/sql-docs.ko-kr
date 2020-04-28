---
title: sys. sp_xtp_unbind_db_resource_pool (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_unbind_db_resource_pool_TSQL
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool_TSQL
- sys.sp_xtp_unbind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
author: stevestein
ms.author: sstein
ms.openlocfilehash: be0f8e7b410abb2e9027ce0b773d1a1ad5a14465
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68041004"
---
# <a name="syssp_xtp_unbind_db_resource_pool-transact-sql"></a>sys.sp_xtp_unbind_db_resource_pool(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  이 시스템 프로시저는 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 메모리 사용량 추적을 위해 데이터베이스와 풀 리소스 간의 기존 바인딩을 제거합니다.  지정된 데이터베이스에 현재 바인딩된 풀이 없으면 성공이 반환됩니다. 데이터베이스가 바인딩 해제되면 메모리 최적화 개체에 대해 이전에 할당된 메모리가 이전 리소스 풀에 할당된 상태로 유지됩니다. 할당된 메모리를 해제하려면 데이터베이스를 다시 시작해야 합니다. 데이터베이스가 리소스 풀에서 바인딩 해제되면 DEFAULT 리소스 풀에 바인딩됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## <a name="arguments"></a>인수  
 database_name  
 기존 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 사용 데이터베이스의 이름입니다.  
  
#### <a name="parameters"></a>매개 변수  
  
## <a name="messages"></a>메시지  
 데이터베이스가 명명된 리소스 풀에 바인딩된 경우 프로시저가 성공적으로 반환합니다. 그러나 데이터베이스를 다시 시작해야 바인딩 해제가 적용됩니다.  
 지정된 데이터베이스에 대한 기존 바인딩이 없는 경우 `sp_xtp_unbind_db_resource_pool`은 성공을 반환하지만 정보 메시지를 제공합니다.  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## <a name="example"></a>예제  
 다음 코드에서는 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 리소스 풀에서 Hekaton_DB를 바인딩 해제합니다.  Hekaton_DB가 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 리소스 풀에 바인딩되어 있지 않은 경우 메시지가 제공됩니다. 데이터베이스를 다시 시작해야 바인딩 해제가 적용됩니다.  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## <a name="requirements"></a>요구 사항  
  
-   `database_name`에서 지정하는 데이터베이스에 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 리소스 풀에 대한 바인딩이 있어야 합니다.  
  
-   CONTROL SERVER 권한이 필요합니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 액세스에 최적화 된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
