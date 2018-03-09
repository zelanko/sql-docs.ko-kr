---
title: "업데이트-SQL 명령 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: update [ODBC]
ms.assetid: ff1e0331-c060-4304-b280-039725b45f63
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6fb2e4d3e3010eaba53b36de383c3365d82db289
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="update---sql-command"></a>업데이트-SQL 명령
새 값이 포함 된 테이블에서 레코드를 업데이트합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보를 참조 하십시오. **드라이버 주의**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
UPDATE [DatabaseName1!]TableName1  
SET Column_Name1 = eExpression1  
   [, Column_Name2 = eExpression2 ...]  
   WHERE FilterCondition1 [AND | OR FilterCondition2 ...]  
```  
  
## <a name="arguments"></a>인수  
 업데이트 [ *DatabaseName1!*] *TableName1*  
 새 값으로 업데이트 되는 레코드 테이블을 지정 합니다.  
  
 *DatabaseName1!* 테이블을 포함 하는 데이터 원본으로 지정 된 데이터베이스가 아닌 데이터베이스의 이름을 지정 합니다. 데이터베이스가 현재 경우 테이블을 포함 하는 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름 뒤에 오는 및 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 설정 *Column_Name1*= *eExpression1*[, *Column_Name2*= *eExpression2*  
 업데이트 되는 열과 새 값을 지정 합니다. WHERE 절을 생략 하면 모든 행의 열에 동일한 값으로 업데이트 됩니다.  
  
 여기서 *FilterCondition1*[AND &#124; 또는 *FilterCondition2*...]  
 새 값으로 업데이트 하는 레코드를 지정 합니다.  
  
 *FilterCondition* 레코드가 새 값으로 업데이트 하려면 충족 해야 하는 조건을 지정 합니다. AND를 원하는 만큼 필터 조건을 포함할 수 있습니다 또는 OR 연산자입니다. 논리 식의 값을 반전 하려면 NOT 연산자를 사용할 수도 있습니다 사용할 수 있습니다 또는 **빈**빈 필드를 확인 하려면 ().  
  
## <a name="remarks"></a>주의  
 업데이트-SQL 레코드만 단일 테이블에서 업데이트할 수 있습니다.  
  
 바꾸기를 달리 업데이트-SQL 레코드 잠금 공유 액세스에 대 한 열 테이블의 여러 레코드를 업데이트할 때 사용 합니다. 다중 사용자 환경에서 레코드 경합 줄어들지만 성능이 저하 될 수 있습니다. 최상의 성능을 위해 테이블을 열고 배타적 사용 하거나 사용 **떼**테이블을 잠그려면 ().  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램의 데이터 원본에는 ODBC SQL 문을 업데이트 보내면 Visual FoxPro ODBC 드라이버는 명령을 변환 하지 않아도 Visual FoxProUPDATE 명령으로 변환 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [DELETE-SQL 명령](../../odbc/microsoft/delete-sql-command.md)   
 [INSERT - SQL 명령](../../odbc/microsoft/insert-sql-command.md)
