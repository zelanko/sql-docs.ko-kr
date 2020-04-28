---
title: UPDATE-SQL 명령 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307644"
---
# <a name="update---sql-command"></a>UPDATE - SQL 명령
테이블의 레코드를 새 값으로 업데이트 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다. 드라이버 관련 정보는 **드라이버 설명**을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>인수  
 업데이트 [ *DatabaseName1!*] *TableName1*  
 새 값으로 레코드를 업데이트 하는 테이블을 지정 합니다.  
  
 *DatabaseName1!* 테이블을 포함 하는 데이터 원본에 지정 된 데이터베이스가 아닌 데이터베이스의 이름을 지정 합니다. 데이터베이스가 현재 데이터베이스가 아닌 경우 테이블이 포함 된 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름과 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 업데이트 되는 열과 새 값을 지정 합니다. WHERE 절을 생략 하면 열의 모든 행이 동일한 값으로 업데이트 됩니다.  
  
 WHERE *FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 새 값으로 업데이트 되는 레코드를 지정 합니다.  
  
 *Filtercondition* 은 레코드가 새 값으로 업데이트 되려면 충족 해야 하는 조건을 지정 합니다. AND 또는 OR 연산자를 사용 하 여 원하는 수 만큼 필터 조건을 포함 하 여 연결할 수 있습니다. NOT 연산자를 사용 하 여 논리 식의 값을 반대로 하거나 **empty**()를 사용 하 여 빈 필드를 확인할 수도 있습니다.  
  
## <a name="remarks"></a>설명  
 업데이트-SQL은 단일 테이블의 레코드만 업데이트할 수 있습니다.  
  
 REPLACE와 달리 UPDATE SQL은 공유 액세스용으로 열린 테이블에서 여러 레코드를 업데이트할 때 레코드 잠금을 사용 합니다. 이렇게 하면 다중 사용자 상황에서 레코드 경합이 줄어들지만 성능이 저하 될 수 있습니다. 성능을 최대화 하려면 단독 사용을 위해 테이블을 열거나 **FLOCK**()를 사용 하 여 테이블을 잠급니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문 업데이트를 데이터 원본으로 보내는 경우 Visual FoxPro ODBC 드라이버는 변환 하지 않고 명령을 Visual FoxProUPDATE 명령으로 변환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [삭제 SQL 명령](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
