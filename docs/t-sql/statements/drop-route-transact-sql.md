---
title: DROP ROUTE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP ROUTE
- DROP_ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping routes
- DROP ROUTE statement
- deleting routes
- routes [Service Broker], removing
- removing routes
ms.assetid: d8fab0bc-d54a-46ca-9437-552db7477d40
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 85afe80062fafb0da1a9a2a4aaae21302cbc1891
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86485500"
---
# <a name="drop-route-transact-sql"></a>DROP ROUTE(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  현재 데이터베이스의 라우팅 테이블에서 경로에 대한 정보를 삭제하여 경로를 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
DROP ROUTE route_name  
[ ; ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *route_name*  
 삭제할 경로의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
## <a name="remarks"></a>설명  
 경로를 저장하는 라우팅 테이블은 카탈로그 뷰 **sys.routes**를 통해 읽을 수 있는 메타데이터 테이블입니다. 라우팅 테이블은 CREATE ROUTE, ALTER ROUTE 및 DROP ROUTE 문으로만 업데이트할 수 있습니다.  
  
 대화에서 해당 경로를 사용하는지 여부에 상관없이 경로를 삭제할 수 있습니다. 그러나 원격 서비스에 대한 다른 경로가 없을 경우 원격 서비스의 경로가 생성되거나 대화 제한 시간을 초과할 때까지 해당 대화에 대한 메시지는 전송 큐에 유지됩니다.  
  
## <a name="permissions"></a>사용 권한  
 경로 삭제 권한은 기본적으로 경로 소유자, db_ddladmin 또는 db_owner 고정 데이터베이스 역할의 멤버 및 sysadmin 고정 서버 역할의 멤버로 설정됩니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `ExpenseRoute`라는 경로를 삭제합니다.  
  
```  
DROP ROUTE ExpenseRoute ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [CREATE ROUTE&#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.routes&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)  
  
  
