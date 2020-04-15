---
title: 삭제 - SQL 명령 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DELETE [ODBC]
ms.assetid: 0d5bd477-626f-4f22-a05a-f531d9f8c5e7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9757fd57d999815964266c035963de1129eaf5e8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303554"
---
# <a name="delete---sql-command"></a>DELETE - SQL 명령
삭제레코드를 표시합니다.  
  
 Visual FoxPro ODBC 드라이버는 이 명령에 대한 기본 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보는 비고를 참조하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>인수  
 FROM [ *데이터베이스 이름!*] *테이블 이름*  
 레코드가 삭제로 표시된 테이블을 지정합니다.  
  
 *Databasename!* 포함된 데이터베이스가 데이터 원본으로 지정된 데이터베이스가 아닌 경우 테이블을 포함하는 데이터베이스의 이름을 지정합니다. 데이터베이스가 데이터 원본으로 지정된 데이터베이스가 아닌 경우 테이블을 포함하는 데이터베이스의 이름을 포함해야 합니다. 데이터베이스 이름 뒤와 테이블 이름 앞에 느낌표(!) 구분 기호를 포함합니다.  
  
 어디 *필터조건1*[및 &#124; 또는 *필터조건2*...]  
 Visual FoxPro가 삭제를 위해 특정 레코드만 표시되도록 지정합니다.  
  
 *FilterCondition는* 레코드가 삭제를 위해 표시되도록 충족해야 하는 조건을 지정합니다. 원하는 만큼 필터 조건을 포함하여 AND 또는 OR 연산자와 연결할 수 있습니다. NOT 연산자를 사용하여 논리 식의 값을 반대로 하거나 **EMPTY()를**사용하여 빈 필드를 확인할 수도 있습니다.  
  
## <a name="remarks"></a>설명  
 SET DELETED가 ON으로 설정된 경우 삭제로 표시된 레코드는 범위를 포함하는 모든 명령에서 무시됩니다.  
  
 DELETE - SQL은 공유 액세스를 위해 열린 테이블에서 삭제를 위해 여러 레코드를 표시할 때 레코드 잠금을 사용합니다. 이렇게 하면 다중 사용자 상황에서 레코드 경합이 줄어들지만 성능은 떨어질 수 있습니다. 성능을 극대화하기 위해 테이블을 열어 단독으로 사용하십시오.  
  
## <a name="driver-remarks"></a>운전자 발언  
 응용 프로그램이 ODBC SQL 문 DELETE를 데이터 원본으로 보내면 Visual FoxPro ODBC 드라이버는 변환 없이 명령을 Visual FoxPro DELETE 명령으로 변환합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SET DELETED 명령](../../odbc/microsoft/set-deleted-command.md)
