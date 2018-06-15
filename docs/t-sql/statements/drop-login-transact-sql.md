---
title: DROP LOGIN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/11/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DROP LOGIN
- DROP_LOGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- deleting login accounts
- logins [SQL Server], removing
- DROP LOGIN statement
- removing login accounts
- dropping login accounts
ms.assetid: acb5c3dc-7aa2-49f6-9330-573227ba9b1a
caps.latest.revision: 36
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: cebe57a15a02e755fe25041bacfa22643f39aa7b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33066600"
---
# <a name="drop-login-transact-sql"></a>DROP LOGIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>인수  
 *login_name*  
 삭제할 로그인의 이름을 지정합니다.  
  
## <a name="remarks"></a>Remarks  
 로그인한 상태의 로그인은 삭제할 수 없습니다. 보안 개체, 서버 수준 개체 또는 SQL Server 에이전트 작업을 소유한 로그인은 삭제할 수 없습니다.  
  
 데이터베이스 사용자가 매핑된 로그인을 삭제할 수는 있지만 이 경우 사용자는 분리됩니다. 자세한 내용은 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)을 실행합니다.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]에서 연결을 인증하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 강제 실행하고 데이터베이스에 최신 버전의 로그인 테이블이 있는지 확인하려면 [DBCC FLUSHAUTHCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)를 실행합니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-login"></a>1. 로그인 매핑  
 다음 예에서는 `WilliJo` 로그인을 삭제합니다.  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>참고 항목  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  

