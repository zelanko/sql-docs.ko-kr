---
title: "사용 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 11/28/2016
ms.prod: sql-non-specified
ms.prod_service: pdw, sql-database
ms.service: 
ms.component: t-sql|language-elements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USE_TSQL
- USE
dev_langs: TSQL
helpviewer_keywords:
- USE statement
- database context [SQL Server]
- context changes [SQL Server]
- modifying database context
ms.assetid: c05acac8-c063-4770-8e36-d7f71d500b10
caps.latest.revision: "40"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Active
ms.openlocfilehash: 1de8ddd8d109e7ba2b83dd6c940487c6aa3fd155
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="use-transact-sql"></a>USE(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 컨텍스트를 지정된 데이터베이스나 데이터베이스 스냅숏으로 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
USE { database_name }   
[;]  
```  
  
## <a name="arguments"></a>인수  
 *database_name*  
 사용자 컨텍스트가 전환되는 데이터베이스 또는 데이터베이스 스냅숏의 이름입니다. 에 대 한 규칙을 사용 하 여 데이터베이스 및 데이터베이스 스냅숏 이름은 따라야 [식별자](../../relational-databases/databases/database-identifiers.md)합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 데이터베이스 매개 변수는 현재 데이터베이스만 참조할 수 있습니다. 경우 현재 데이터베이스가 아닌 데이터베이스에 제공 되는, `USE` 문은 데이터베이스 간에 전환 되지 않습니다 및 40508 오류 코드가 반환 됩니다. 데이터베이스를 변경하려면 데이터베이스에 직접 연결해야 합니다. USE 문을 있을 수 있으므로이 페이지의 위쪽에 SQL 데이터베이스에 적용할 수 없는로 표시 된 `USE` 문을 일괄 처리를 수행 하지 않습니다.
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때 자동으로 기본 데이터베이스에 연결되며 데이터베이스 사용자의 보안 컨텍스트를 획득합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 데이터베이스 사용자가 생성되지 않은 경우 해당 로그인은 게스트로서 연결합니다. 데이터베이스 사용자에게 데이터베이스에 대한 CONNECT 권한이 없으면 USE 문은 실패합니다. 로그인에 기본 데이터베이스를 할당하지 않은 경우 기본 데이터베이스는 master로 설정됩니다.  
  
 USE는 컴파일과 실행 시간에 모두 실행되고 효력이 즉시 나타납니다. 따라서 USE 문 다음에 일괄적으로 나타나는 문은 지정된 데이터베이스에서 실행됩니다.  
  
## <a name="permissions"></a>Permissions  
 대상 데이터베이스에 대한 CONNECT 권한이 필요합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `AdventureWorks2012` 데이터베이스로 데이터베이스 컨텍스트를 변경합니다.  
  
```  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
  


