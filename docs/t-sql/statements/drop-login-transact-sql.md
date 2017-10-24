---
title: DROP LOGIN (TRANSACT-SQL) | Microsoft Docs
ms.custom: 
ms.date: 05/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8c13d7800893b860b1bcaf3f631f01f190a2715
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="drop-login-transact-sql"></a>DROP LOGIN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 계정을 제거합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
DROP LOGIN login_name  
```  
  
## <a name="arguments"></a>인수  
 *login_name*  
 삭제할 로그인의 이름을 지정합니다.  
  
## <a name="remarks"></a>주의  
 로그인한 상태의 로그인은 삭제할 수 없습니다. 보안 개체, 서버 수준 개체 또는 SQL Server 에이전트 작업을 소유한 로그인은 삭제할 수 없습니다.  
  
 데이터베이스 사용자가 매핑된 로그인을 삭제할 수는 있지만 이 경우 사용자는 분리됩니다. 자세한 내용은 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)을 참조하세요.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)], 한 연결을 인증 하는 데 필요한 로그인 데이터 및 서버 수준 방화벽 규칙은 각 데이터베이스에 일시적으로 캐시 됩니다. 이 캐시는 주기적으로 새로 고쳐집니다. 인증 캐시 새로 고침을 데이터베이스에 최신 버전의 로그인 테이블에 있는지 확인 하려면 실행할 [DBCC FLUSHAUTHCACHE &#40; Transact SQL &#41; ](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-dropping-a-login"></a>1. 로그인을 삭제 하는 중  
 다음 예에서는 `WilliJo` 로그인을 삭제합니다.  
  
```  
DROP LOGIN WilliJo;  
GO 
```  
 
  
## <a name="see-also"></a>관련 항목:  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  


