---
title: sp_databases (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_databases_TSQL
- sp_databases
dev_langs: TSQL
helpviewer_keywords: sp_databases
ms.assetid: 2a83b92a-9ecc-43c4-8ff4-e91e3a940b5a
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3eaf930a86171226ccb3a32e746b9a79f229910d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spdatabases-transact-sql"></a>sp_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 있거나 데이터베이스 게이트웨이를 통해 액세스할 수 있는 데이터베이스를 나열합니다.  
  
||  
|-|  
|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
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
|**A S E _**|**sysname**|데이터베이스의 이름입니다. 에 [!INCLUDE[ssDE](../../includes/ssde-md.md)],이 열에 저장 되어 있는 데이터베이스 이름을 나타내는 **sys.databases** 카탈로그 뷰.|  
|**DATABASE_SIZE**|**int**|데이터베이스 크기(KB)입니다.|  
|**설명**|**varchar(254)**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]의 경우 이 필드는 항상 NULL을 반환합니다.|  
  
## <a name="remarks"></a>주의  
 반환된 데이터베이스 이름은 현재 데이터베이스 컨텍스트를 변경하기 위해 USE 문에서 매개 변수로 사용할 수 있습니다.  
  
 **sp_databases** 해당 키 없음에서 ODBC Open Database Connectivity ()가 있습니다.  
  
## <a name="permissions"></a>Permissions  
 CREATE DATABASE, ALTER ANY DATABASE 또는 VIEW ANY DEFINITION 권한이 필요하며 데이터베이스에 대한 액세스 권한이 있어야 합니다. VIEW ANY DEFINITION 권한은 거부될 수 없습니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sp_databases`를 실행하는 방법을 보여 줍니다.  
  
```tsql  
USE master;  
GO  
EXEC sp_databases;  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [HAS_DBACCESS &#40; Transact SQL &#41;](../../t-sql/functions/has-dbaccess-transact-sql.md)  
  
  
