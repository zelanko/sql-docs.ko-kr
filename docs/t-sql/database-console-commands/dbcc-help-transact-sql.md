---
description: DBCC HELP(Transact-SQL)
title: DBCC HELP(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/16/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC HELP
- DBCC_HELP_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC statement syntax information
- DBCC HELP statement
ms.assetid: 306092c6-4354-4e47-928b-606124fbdc6e
author: pmasl
ms.author: umajay
ms.openlocfilehash: 3440683db3fb0b72987e26913a43ed4ba2a852ec
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88311169"
---
# <a name="dbcc-help-transact-sql"></a>DBCC HELP(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

지정한 DBCC 명령의 구문 정보를 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC HELP ( 'dbcc_statement' | @dbcc_statement_var | '?' )  
[ WITH NO_INFOMSGS ]  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *dbcc_statement* |  *\@dbcc_statement_var*  
 구문 정보를 받을 DBCC 명령의 이름입니다. DBCC 뒤에 오는 DBCC 명령 부분만 지정하십시오(예: DBCC CHECKDB 대신 CHECKDB).  
  
 ?  
 도움말을 볼 수 있는 DBCC 명령을 모두 반환합니다.  
  
 WITH NO_INFOMSGS  
 심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.  
  
## <a name="result-sets"></a>결과 집합  
DBCC HELP는 지정한 DBCC 명령의 구문을 보여 주는 결과 집합을 반환합니다.
  
## <a name="permissions"></a>사용 권한  
**sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.
  
## <a name="examples"></a>예  
### <a name="a-using-dbcc-help-with-a-variable"></a>A. DBCC HELP에 변수를 지정  
다음 예에서는 DBCC `CHECKDB`의 구문 정보를 반환합니다.
  
```sql  
DECLARE @dbcc_stmt sysname;  
SET @dbcc_stmt = 'CHECKDB';  
DBCC HELP (@dbcc_stmt);  
GO  
```  
  
### <a name="b-using-dbcc-help-with-the--option"></a>B. DBCC HELP에 옵션 ?를 옵션  
다음 예에서는 도움말을 볼 수 있는 모든 DBCC 문을 반환합니다.
  
```sql  
DBCC HELP ('?');  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)
  
  
