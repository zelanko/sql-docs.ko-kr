---
title: sp_clean_db_file_free_space (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_clean_db_file_free_space
- sp_clean_db_file_free_space_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ghost records
- sp_clean_db_file_free_space
ms.assetid: 3eb53a67-969d-4cb8-9681-b1c8e6fd55b6
caps.latest.revision: 11
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 41c242e65df878a0a97d6fce221d3bcf3dcde9e8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spcleandbfilefreespace-transact-sql"></a>sp_clean_db_file_free_space(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 데이터 수정 루틴 때문에 데이터베이스 페이지에 남겨진 정보를 제거합니다. sp_clean_db_file_free_space는 데이터베이스의 파일 하나에서만 모든 페이지를 정리합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_clean_db_file_free_space   
[ @dbname ] = 'database_name'   
, @fileid = 'file_number'   
 [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>인수  
 [ @dbname=] '*database_name*'  
 정리할 데이터베이스의 이름입니다. *dbname* 은 **sysname** NULL 일 수 없습니다.  
  
 [ @fileid=] '*file_number*'  
 정리할 데이터 파일 ID입니다. *file_number* 은 **int** NULL 일 수 없습니다.  
  
 [ @cleaning_delay=] '*delay_in_seconds*'  
 페이지 정리를 멈추고 대기할 시간 간격을 지정합니다. 이 간격을 지정하면 I/O 시스템에 미치는 영향을 줄이는 데 도움이 됩니다. *delay_in_seconds* 은 **int** 기본값은 0입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 테이블에서 삭제 작업을 수행하거나 업데이트 작업으로 행을 이동하면 행에 대한 참조를 제거하여 페이지에서 공간을 즉시 확보할 수 있습니다. 그러나 상황에 따라서는 행이 데이터 페이지에 물리적으로 남아 있어 삭제해야 할 레코드가 될 수 있습니다. 삭제할 레코드는 백그라운드 프로세스를 통해 정기적으로 제거됩니다. 이 잔여 데이터를 반환 하지 않습니다는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리에 대 한 응답입니다. 그러나 데이터나 백업 파일의 물리적 보안이 중요한 환경에서는 sp_clean_db_file_free_space를 사용하여 이와 같이 삭제할 레코드를 강제로 정리할 수 있습니다.  
  
 sp_clean_db_file_free_space를 실행하는 데 필요한 시간은 파일의 크기, 사용 가능한 여유 공간, 디스크의 용량에 따라 달라집니다. sp_clean_db_file_free_space를 실행하면 I/O 작업 속도가 크게 저하될 수 있으므로 이 프로시저는 평상 업무 시간이 아닐 때 실행하는 것이 좋습니다.  
  
 sp_clean_db_file_free_space를 실행하기 전에 전체 데이터베이스 백업을 만드는 것이 좋습니다.  
  
 관련 [sp_clean_db_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md) 저장된 프로시저는 데이터베이스의에서 모든 파일을 정리 합니다.  
  
## <a name="permissions"></a>Permissions  
 db_owner 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스의 주 데이터 파일에서 잔여 정보를 모두 정리하는 방법을 보여 줍니다.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_file_free_space   
@dbname = N'AdventureWorks2012', @fileid = 1 ;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 엔진 저장 프로시저 &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
