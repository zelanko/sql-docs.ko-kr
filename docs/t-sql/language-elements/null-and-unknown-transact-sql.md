---
title: "NULL 및 알 수 없음 (Transact SQL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 9d491846-4730-4740-a680-77c69fae4a58
caps.latest.revision: 5
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: bdac1899707b3caa4f4c515324511a47830f2722
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="null-and-unknown-transact-sql"></a>NULL 및 알 수 없음 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-pdw_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-pdw-md.md)]

  NULL 값이 알려진 나타냅니다. Null 값은 빈 또는 0 값과 다릅니다. 2개의 Null 값이 서로 같다고 할 수는 없습니다. 각각의 NULL 값 알 수 없기 때문에 2 개의 null 값 또는 null 값과 다른 값 간의 비교는 알 수 없는 반환 합니다.  
  
 Null 값에는 일반적으로 데이터를 알 수 없는, 해당 없음 나타냅니다 또는 나중에 추가할 수 있습니다. 예를 들어 고객이 주문할 당시 고객의 중간 이름을 알 수 없는 경우도 있습니다.  
  
 Null 값에 대해 다음 note:  
  
-   쿼리에서 Null 값을 검사하려면 WHERE 절에서 IS NULL이나 IS NOT NULL을 사용합니다.  
  
-   INSERT 또는 UPDATE 문에서 NULL을 명시적으로 지정 하 여 또는 INSERT 문에 열을 그대로 유지 되므로 열에 null 값을 삽입할 수 있습니다.  
  
-   기본 키와 같이 또는 배포 키와 같은 행에 배포 하는 데 사용 되는 정보에 대 한 테이블의 다른 행에서 테이블의 한 행을 구별 하는 데 필요한 정보로 null 값을 사용할 수 없습니다.  
  
 데이터, 논리 연산자, 비교 연산자에 Null 값이 포함되어 있으면 TRUE 또는 FALSE 대신 UNKNOWN이라는 결과가 반환될 수 있습니다. 이와 같이 세 가지 결과를 가져오는 논리는 대부분 응용 프로그램에서 오류의 원인이 됩니다. 다음은 Null 값을 비교 연산한 결과를 정리한 표입니다.  
  
 다음 표에서 하나의 피연산자에 NULL을 반환 하는 위치를 두 개의 부울 피연산자에 AND 연산자를 적용 한 결과 보여 줍니다.  
  
|Operand 1|Operand 2|결과|  
|---------------|---------------|------------|  
|TRUE|NULL|FALSE|  
|NULL|NULL|FALSE|  
|FALSE|NULL|FALSE|  
  
 다음 표에서 하나의 피연산자에 NULL을 반환 하는 위치를 두 개의 부울 피연산자에 OR 연산자를 적용 한 결과 보여 줍니다.  
  
|Operand 1|Operand 2|결과|  
|---------------|---------------|------------|  
|TRUE|NULL|TRUE|  
|NULL|NULL|UNKNOWN|  
|FALSE|NULL|UNKNOWN|  
  
## <a name="see-also"></a>관련 항목:  
 [및 &#40; Transact SQL &#41;](../../t-sql/language-elements/and-transact-sql.md)   
 [또는 &#40; Transact SQL &#41;](../../t-sql/language-elements/or-transact-sql.md)   
 [하지 &#40; Transact SQL &#41;](../../t-sql/language-elements/not-transact-sql.md)   
 [NULL &#40; Transact SQL &#41;](../../t-sql/queries/is-null-transact-sql.md)  
  
  
