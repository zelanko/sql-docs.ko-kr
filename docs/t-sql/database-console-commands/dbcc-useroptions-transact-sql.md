---
title: DBCC USEROPTIONS (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC USEROPTIONS
- DBCC_USEROPTIONS_TSQL
- USEROPTIONS_TSQL
- USEROPTIONS
dev_langs:
- TSQL
helpviewer_keywords:
- DBCC USEROPTIONS statement
- active SET options
- SET statement, active SET options
ms.assetid: 565ab112-7af1-4c18-a579-07cdb332f539
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f3bf507ff174822e5133326555e8a9d2ab25f6e5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/25/2018
---
# <a name="dbcc-useroptions-transact-sql"></a>DBCC USEROPTIONS(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

현재 연결에 설정된 SET 옵션을 반환합니다.
  
![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>구문  
  
```sql
DBCC USEROPTIONS  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>인수  
NO_INFOMSGS  
심각도가 0에서 10 사이인 모든 정보 메시지를 표시하지 않습니다.
  
## <a name="result-sets"></a>결과 집합  
DBCC USEROPTIONS는 SET 옵션의 이름이 포함된 열과 옵션 값이 포함된 열을 반환합니다. 값과 항목은 다음과 다를 수 있습니다.

```sql

Set Option                   Value`  
---------------------------- ---------------------------`  
textsize                     64512 
language                     us_english 
dateformat                   mdy  
datefirst                    7 
lock_timeout                 -1 
quoted_identifier            SET 
arithabort                   SET 
ansi_null_dflt_on            SET 
ansi_warnings                SET 
ansi_padding                 SET 
ansi_nulls                   SET 
concat_null_yields_null      SET 
isolation level              read committed  
(13 row(s) affected) 
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```  
  
## <a name="remarks"></a>주의  
데이터베이스 옵션 READ_COMMITTED_SNAPSHOT을 ON으로 설정하고 트랜잭션 격리 수준을 '커밋된 읽기'로 설정하면 DBCC USEROPTIONS가 커밋된 읽기 스냅숏의 격리 수준을 보고합니다. 그러나 실제 격리 수준은 커밋된 읽기입니다.
  
## <a name="permissions"></a>Permissions  
**public** 역할의 멤버 자격이 필요합니다.
  
## <a name="examples"></a>예  
다음 예에서는 현재 연결에 설정된 SET 옵션을 반환합니다.
  
```sql  
DBCC USEROPTIONS;  
```  
  
## <a name="see-also"></a>관련 항목:  
[DBCC&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[SET 문&#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
[SET TRANSACTION ISOLATION LEVEL&#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)
  
  
