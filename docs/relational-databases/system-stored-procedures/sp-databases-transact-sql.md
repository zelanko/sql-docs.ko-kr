---
title: sp_databases (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs:
- TSQL
helpviewer_keywords:
- sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1be4fbfb6ce30443a979fb500954e7aa8fa9779a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62507408"
---
# <a name="spdatabases-transact-sql"></a>sp_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있거나 데이터베이스 게이트웨이를 통해 액세스할 수 있는 데이터베이스를 나열합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_databases  
```  
  
## <a name="return-code-values"></a>반환 코드 값  
 없음  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DATABASE_NAME**|**sysname**|데이터베이스의 이름입니다. 에 [!INCLUDE[ssDE](../../includes/ssde-md.md)],이 열에 저장 된 데이터베이스 이름을 나타냅니다는 **sys.databases** 카탈로그 뷰.|  
|**DATABASE_SIZE**|**int**|데이터베이스 크기(KB)입니다.|  
|**REMARKS**|**varchar(254)**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]의 경우 이 필드는 항상 NULL을 반환합니다.|  
  
## <a name="remarks"></a>Remarks  
 반환된 데이터베이스 이름은 현재 데이터베이스 컨텍스트를 변경하기 위해 USE 문에서 매개 변수로 사용할 수 있습니다.  
  
 **sp_databases** 에 해당 요소가에서 열린 데이터베이스 연결 (ODBC).  
  
## <a name="permissions"></a>사용 권한  
 CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION 권한이 필요하며 데이터베이스에 대한 액세스 권한이 있어야 합니다. VIEW ANY DEFINITION 권한은 거부될 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sp_databases`를 실행하는 방법을 보여 줍니다.  
  
```sql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>관련 항목  
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40;TRANSACT-SQL&#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
