---
title: 업데이트 - SQL 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818811c18ed52cef5bdb1c4d97f947bb86e67422
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307644"
---
# <a name="update---sql-command"></a>UPDATE - SQL 명령
새 값으로 테이블의 레코드를 업데이트합니다.  
  
 Visual FoxPro ODBC 드라이버는 이 명령에 대한 기본 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 **드라이버 설명**을 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>인수  
 업데이트 [ *데이터베이스이름1!*] *테이블네임1*  
 레코드가 새 값으로 업데이트되는 테이블을 지정합니다.  
  
 *데이터베이스이름1!* 테이블이 포함된 데이터 원본으로 지정된 데이터베이스 이외의 데이터베이스 이름을 지정합니다. 데이터베이스가 현재 테이블이 아닌 경우 테이블을 포함하는 데이터베이스의 이름을 포함해야 합니다. 데이터베이스 이름 뒤와 테이블 이름 앞에 느낌표(!) 구분 기호를 포함합니다.  
  
 set *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 업데이트되는 열과 해당 새 값을 지정합니다. WHERE 절을 생략하면 열의 모든 행이 동일한 값으로 업데이트됩니다.  
  
 어디 *필터조건1*[및 &#124; 또는 *필터조건2*...]  
 새 값으로 업데이트된 레코드를 지정합니다.  
  
 *Filter조건은* 레코드가 새 값으로 업데이트하기 위해 충족해야 하는 조건을 지정합니다. 원하는 만큼 필터 조건을 포함하여 AND 또는 OR 연산자와 연결할 수 있습니다. NOT 연산자를 사용하여 논리 식의 값을 반대로 하거나 **EMPTY()를**사용하여 빈 필드를 확인할 수도 있습니다.  
  
## <a name="remarks"></a>설명  
 UPDATE - SQL은 단일 테이블의 레코드만 업데이트할 수 있습니다.  
  
 REPLACE와 달리 UPDATE - SQL은 공유 액세스를 위해 열린 테이블의 여러 레코드를 업데이트할 때 레코드 잠금을 사용합니다. 이렇게 하면 다중 사용자 상황에서 레코드 경합이 줄어들지만 성능은 떨어질 수 있습니다. 성능을 극대화하려면 단독으로 사용할 테이블을 열거나 **FLOCK()을**사용하여 테이블을 잠급니다.  
  
## <a name="driver-remarks"></a>운전자 발언  
 응용 프로그램이 ODBC SQL 문 UPDATE를 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 변환 없이 명령을 Visual FoxProUPDATE 명령으로 변환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [삭제 - SQL 명령](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
