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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fbd5ec98791d782fe7ad1fdb1e1884b646dcf9f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632560"
---
# <a name="update---sql-command"></a>UPDATE - SQL 명령
새 값을 사용 하 여 테이블의 레코드를 업데이트합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보를 참조 하세요 **드라이버 주의**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>인수  
 UPDATE [ *DatabaseName1!*] *TableName1*  
 새 값으로 업데이트 되는 레코드 테이블을 지정 합니다.  
  
 *DatabaseName1!* 테이블이 포함 된 데이터 소스를 사용 하 여 지정 된 데이터베이스가 아닌 데이터베이스의 이름을 지정 합니다. 데이터베이스가 현재 없는 경우 테이블을 포함 하는 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름 뒤에 오는 및 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 SET *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 업데이트 되는 열과 새 값을 지정 합니다. WHERE 절을 생략 하면 동일한 값을 가진 열의 모든 행이 업데이트 됩니다.  
  
 WHERE *FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 새 값으로 업데이트 된 레코드를 지정 합니다.  
  
 *FilterCondition* 레코드가 새 값으로 업데이트 하려면 충족 해야 하는 조건을 지정 합니다. AND를 사용 하 여 연결을 원하는 개수 만큼 필터 조건을 포함할 수 있습니다 또는 OR 연산자입니다. 논리 식의 값을 반전 하려면 NOT 연산자를 사용할 수도 있습니다 하거나 사용할 수 있습니다 **빈**빈 필드에 대 한 확인 ().  
  
## <a name="remarks"></a>Remarks  
 업데이트-SQL 단일 테이블의 레코드에만 업데이트할 수 있습니다.  
  
 바꾸기 달리 업데이트-SQL 레코드 잠금을 공유 액세스용으로 연 테이블에 여러 레코드를 업데이트 하는 경우 사용 합니다. 다중 사용자 환경에서 레코드 경합 줄어들지만 성능이 느려질 수 있습니다. 최상의 성능을 위해 테이블을 엽니다 배타적 사용 또는 사용 하 여 **떼**()를 테이블을 잠글 수 있습니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램의 데이터 원본에는 ODBC SQL 문을 업데이트 보내면 Visual FoxPro ODBC 드라이버 명령을 변환 하지 않아도 Visual FoxProUPDATE 명령으로 변환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [DELETE-SQL 명령](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
