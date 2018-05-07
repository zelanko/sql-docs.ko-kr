---
title: sp_wait_for_database_copy_sync (Azure SQL 데이터베이스) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6658ab7b1b68637978ca76ea709c4c0a23414d07
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>활성 지리적 복제-sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  이 프로시저는 기본 및 보조 간 [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] 관계로 한정됩니다. 호출 된 **sp_wait_for_database_copy_sync** 응용 프로그램에 커밋된 모든 트랜잭션이 복제 되 고 활성 보조 데이터베이스에서 승인할 때까지 기다립니다. 실행 **sp_wait_for_database_copy_sync** 에 주 데이터베이스에만 합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>구문  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>인수  
 [ @target_server =] 'server_name'  
 활성 보조 데이터베이스를 호스트하는 SQL Database 서버의 이름입니다. server_name은 sysname이며 기본값은 없습니다.  
  
 [ @target_database =] 's e _'  
 활성 보조 데이터베이스의 이름입니다. database_name은 sysname이며 기본값은 없습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 성공하면 0을 반환하고 실패하면 오류 번호를 반환합니다.  
  
 가장 가능성이 높은 오류 조건은 다음과 같습니다.  
  
-   서버 이름 또는 데이터베이스 이름이 없는 경우  
  
-   지정된 서버 이름 또는 데이터베이스에 대한 링크를 찾을 수 없는 경우  
  
-   상호 링크 연결이 손실된 경우. **sp_wait_for_database_copy_sync** 연결 시간 초과 후 반환 합니다.  
  
## <a name="permissions"></a>Permissions  
 주 데이터베이스의 모든 사용자가 이 시스템 저장 프로시저를 호출할 수 있습니다. 로그인은 기본 및 활성 보조 데이터베이스 둘 다에 있는 사용자여야 합니다.  
  
## <a name="remarks"></a>주의  
 전에 커밋된 모든 트랜잭션이 **sp_wait_for_database_copy_sync** 호출 활성 보조 데이터베이스에 전송 됩니다.  
  
## <a name="examples"></a>예  
 다음 예제에서는 호출 **sp_wait_for_database_copy_sync** db0 주 데이터베이스로 커밋된 모든 트랜잭션이 인지 확인 하는 대상 서버 ubfyu5ssyt의 활성 보조 데이터베이스를 전송 합니다.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.dm_continuous_copy_status &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [지리적 복제 동적 관리 뷰 및 함수 &#40;Azure SQL 데이터베이스&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
