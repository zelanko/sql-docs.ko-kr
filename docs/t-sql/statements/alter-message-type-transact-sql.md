---
title: ALTER MESSAGE TYPE(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_MESSAGE_TYPE_TSQL
- ALTER MESSAGE TYPE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER MESSAGE TYPE statement
- modifying message types
- message types [Service Broker], modifying
ms.assetid: 98c94176-2bdf-4725-b4bc-d33b6b14817d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: e0e9e6a6d8e0f4b976775271532fc61b03b199fa
ms.sourcegitcommit: b2ab989264dd9d23c184f43fff2ec8966793a727
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/14/2020
ms.locfileid: "86381177"
---
# <a name="alter-message-type-transact-sql"></a>ALTER MESSAGE TYPE(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  메시지 유형의 속성을 변경합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```syntaxsql
  
ALTER MESSAGE TYPE message_type_name  
   VALIDATION =  
    {  NONE   
     | EMPTY   
     | WELL_FORMED_XML   
     | VALID_XML WITH SCHEMA COLLECTION schema_collection_name }  
[ ; ]  
```  
  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>인수
 *message_type_name*  
 변경할 메시지 유형의 이름입니다. 서버, 데이터베이스 및 스키마 이름은 지정될 수 없습니다.  
  
 VALIDATION  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)]에서 이 유형의 메시지 본문 유효성을 검사하는 방법을 지정합니다.  
  
 없음  
 유효성 검사가 수행되지 않습니다. 메시지 본문이 데이터를 포함할 수도 있고 NULL일 수도 있습니다.  
  
 EMPTY  
 메시지 본문이 NULL이어야 합니다.  
  
 WELL_FORMED_XML  
 메시지 본문에 올바른 형식의 XML이 있어야 합니다.  
  
 VALID_XML_WITH_SCHEMA = *schema_collection_name*  
 메시지 본문에는 지정된 스키마 컬렉션의 스키마를 준수하는 XML이 포함되어야 합니다. *schema_collection_name*은 기존 XML 스키마 컬렉션의 이름이어야 합니다.  
  
## <a name="remarks"></a>설명  
 메시지 유형의 유효성 검사를 변경해도 이미 큐에 배달된 메시지에는 영향을 주지 않습니다.  
  
 메시지 유형에 대한 AUTHORIZATION을 변경하려면 ALTER AUTHORIZATION 문을 사용합니다.  
  
## <a name="permissions"></a>사용 권한  
 메시지 유형 변경 권한은 기본적으로 메시지 유형의 소유자, **db_ddladmin** 또는 **db_owner** 고정 데이터베이스 역할의 멤버 및 **sysadmin** 고정 서버 역할의 멤버로 설정됩니다.  
  
 ALTER MESSAGE TYPE 문에서 스키마 컬렉션을 지정하면 이 문을 실행하는 사용자는 지정된 스키마 컬렉션에 대해 REFERENCES 권한이 있어야 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 메시지 본문에 올바른 형식의 XML 문서가 포함되도록 `//Adventure-Works.com/Expenses/SubmitExpense` 메시지 유형을 변경합니다.  
  
```  
ALTER MESSAGE TYPE  
    [//Adventure-Works.com/Expenses/SubmitExpense]  
    VALIDATION = WELL_FORMED_XML ;  
```  
  
## <a name="see-also"></a>참고 항목  
 [ALTER AUTHORIZATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [CREATE MESSAGE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/create-message-type-transact-sql.md)   
 [DROP MESSAGE TYPE&#40;Transact-SQL&#41;](../../t-sql/statements/drop-message-type-transact-sql.md)   
 [EVENTDATA&#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
