---
title: NULL 및 UNKNOWN(Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, pdw, sql-database
ms.service: ''
ms.component: t-sql|language-elements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ff35786ca071881f25922ed955301fc8e38af2bf
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="null-and-unknown-transact-sql"></a>NULL 및 UNKNOWN(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL은 값을 알 수 없다는 의미입니다. Null은 빈 값이나 0과는 다르며 2개의 Null 값이 서로 같다고 할 수는 없습니다. 2개의 Null 값을 비교하거나 Null 값과 다른 값을 비교하면 각각의 NULL 값을 알 수 없으므로 unknown이 반환됩니다.  
  
 Null 값은 대개 데이터를 알 수 없거나 해당 사항이 없거나 나중에 추가됨을 나타냅니다. 예를 들어 고객이 주문할 당시 고객의 중간 이름을 알 수 없는 경우도 있습니다.  
  
 Null 값에 관해 다음 사항을 참고하세요.  
  
-   쿼리에서 Null 값을 검사하려면 WHERE 절에서 IS NULL이나 IS NOT NULL을 사용합니다.  
  
-   null 값은 INSERT 또는 UPDATE 문에서 NULL을 명시적으로 입력하거나 INSERT 문에서 해당 열을 제외시켜 열에 입력됩니다.  
  
-   널 (Null) 값은 기본 키와 같이 테이블의 행을 다른 행과 구별하는 데 필요한 정보로, 또는 분산 키와 같이 행을 분산하는 데 사용되는 정보로 사용할 수 없습니다.  
  
 데이터, 논리 연산자, 비교 연산자에 Null 값이 포함되어 있으면 TRUE 또는 FALSE 대신 UNKNOWN이라는 결과가 반환될 수 있습니다. 이와 같이 세 가지 결과를 가져오는 논리는 대부분 응용 프로그램에서 오류의 원인이 됩니다. UNKNOWN을 포함하는 부울 식의 논리 연산자는 연산자의 결과가 UNKNOWN 식에 의존하지 않는 한 UNKNOWN을 반환합니다. 이러한 표에서 이 동작의 예가 제공됩니다.  
  
 다음 표는 하나의 식에서 UNKNOWN이 반환되는 2개의 부울 피연산자에 AND 연산자를 적용한 결과를 보여 줍니다.  
  
|Expression 1|Expression 2|결과|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|UNKNOWN|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|FALSE|  
  
 다음 표는 하나의 식에서 UNKNOWN이 반환되는 2개의 부울 피연산자에 OR 연산자를 적용한 결과를 보여 줍니다.  
  
|Expression 1|Expression 2|결과|  
|---------------|---------------|------------|  
|TRUE|UNKNOWN|TRUE|  
|UNKNOWN|UNKNOWN|UNKNOWN|  
|FALSE|UNKNOWN|UNKNOWN|  
  
## <a name="see-also"></a>참고 항목  
 [AND&#40;Transact-SQL&#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [OR&#40;Transact-SQL&#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [NOT&#40;Transact-SQL&#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [IS NULL&#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
