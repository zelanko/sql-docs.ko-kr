---
description: USE(Transact-SQL)
title: USE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/28/2016
ms.prod: sql
ms.prod_service: pdw, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- USE_TSQL
- USE
dev_langs:
- TSQL
helpviewer_keywords:
- USE statement
- database context [SQL Server]
- context changes [SQL Server]
- modifying database context
ms.assetid: c05acac8-c063-4770-8e36-d7f71d500b10
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 27e6f62e7b867fcae8d97a080ead87daf5536b7f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464204"
---
# <a name="use-transact-sql"></a>USE(Transact-SQL)
[!INCLUDE [sql-asdbmi-pdw](../../includes/applies-to-version/sql-asdbmi-pdw.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 데이터베이스 컨텍스트를 지정된 데이터베이스나 데이터베이스 스냅샷으로 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
USE { database_name }   
[;]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *database_name*  
 사용자 컨텍스트가 전환되는 데이터베이스 또는 데이터베이스 스냅샷의 이름입니다. 데이터베이스와 데이터베이스 스냅샷 이름은 [식별자](../../relational-databases/databases/database-identifiers.md)에 대한 규칙을 따라야 합니다.  
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]에서 데이터베이스 매개 변수는 현재 데이터베이스만 참조할 수 있습니다. 현재 데이터베이스가 아닌 데이터베이스를 제공할 경우 `USE` 문은 데이터베이스 사이를 전환하지 않으며 오류 코드 40508이 반환됩니다. 데이터베이스를 변경하려면 데이터베이스에 직접 연결해야 합니다. USE 문은 이 페이지 맨 위에 SQL Database에 해당하지 않는다고 표기되어 있습니다. 일괄 처리에 `USE` 문이 포함될 수는 있지만 아무 것도 수행되지 않습니다.
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때 자동으로 기본 데이터베이스에 연결되며 데이터베이스 사용자의 보안 컨텍스트를 획득합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인에 대해 데이터베이스 사용자가 생성되지 않은 경우 해당 로그인은 게스트로서 연결합니다. 데이터베이스 사용자에게 데이터베이스에 대한 CONNECT 권한이 없으면 USE 문은 실패합니다. 로그인에 기본 데이터베이스를 할당하지 않은 경우 기본 데이터베이스는 master로 설정됩니다.  
  
 USE는 컴파일과 실행 시간에 모두 실행되고 효력이 즉시 나타납니다. 따라서 USE 문 다음에 일괄적으로 나타나는 문은 지정된 데이터베이스에서 실행됩니다.  
  
## <a name="permissions"></a>사용 권한  
 대상 데이터베이스에 대한 CONNECT 권한이 필요합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `AdventureWorks2012` 데이터베이스로 데이터베이스 컨텍스트를 변경합니다.  
  
```sql  
USE AdventureWorks2012;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER&#40;Transact-SQL&#41;](../../t-sql/statements/create-user-transact-sql.md)   
 [보안 주체&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../statements/create-database-transact-sql.md)   
 [DROP DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-database-transact-sql.md)   
 [EXECUTE&#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md)  
  
