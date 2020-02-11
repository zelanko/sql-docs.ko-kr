---
title: DELETE-SQL 명령 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 79a9c9a86e290f568f205a7e7678122f9089a7e2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68096327"
---
# <a name="delete---sql-command"></a>DELETE - SQL 명령
레코드 삭제를 표시 합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원 합니다. 드라이버 관련 정보는 설명 부분을 참조 하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>인수  
 FROM [ *DatabaseName!*] *TableName*  
 레코드가 삭제 되도록 표시 되는 테이블을 지정 합니다.  
  
 *DatabaseName!* 포함 하는 데이터베이스가 데이터 원본에 지정 된 데이터베이스가 아닌 경우 테이블이 포함 된 데이터베이스의 이름을 지정 합니다. 데이터베이스가 데이터 원본에 지정 된 데이터베이스가 아닌 경우 테이블이 포함 된 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름과 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 WHERE *FilterCondition1*[AND &#124; OR *FilterCondition2*...]  
 Visual FoxPro에서 특정 레코드만 삭제 하도록 지정 합니다.  
  
 *Filtercondition* 은 레코드가 삭제 되도록 표시 하기 위해 충족 해야 하는 조건을 지정 합니다. 원하는 수 만큼 필터 조건을 포함 하 여 AND 또는 OR 연산자를 사용 하 여 연결할 수 있습니다. NOT 연산자를 사용 하 여 논리 식의 값을 반대로 하거나 **empty**()를 사용 하 여 빈 필드를 확인할 수도 있습니다.  
  
## <a name="remarks"></a>설명  
 SET DELETED가 ON으로 설정 된 경우에는 삭제 하도록 표시 된 레코드가 범위를 포함 하는 모든 명령에서 무시 됩니다.  
  
 삭제-SQL은 공유 액세스를 위해 열린 테이블에서 삭제를 위해 여러 레코드를 표시할 때 레코드 잠금을 사용 합니다. 이렇게 하면 다중 사용자 상황에서 레코드 경합이 줄어들지만 성능이 저하 될 수 있습니다. 성능을 최대화 하려면 단독 사용을 위해 테이블을 엽니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램에서 ODBC SQL 문 삭제를 데이터 원본으로 보낼 때 Visual FoxPro ODBC 드라이버는 변환을 수행 하지 않고 명령을 Visual FoxPro DELETE 명령으로 변환 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SET DELETED 명령](../../odbc/microsoft/set-deleted-command.md)
