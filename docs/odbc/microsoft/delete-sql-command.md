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
manager: craigg
ms.openlocfilehash: dac94d8bfb0e2bc0ab91f6a18e6f18606481b112
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53202032"
---
# <a name="delete---sql-command"></a>DELETE - SQL 명령
삭제에 대 한 레코드를 표시합니다.  
  
 Visual FoxPro ODBC 드라이버는이 명령에 대 한 네이티브 Visual FoxPro 언어 구문을 지원합니다. 드라이버 관련 정보에 대 한 설명을 참조 하세요.  
  
## <a name="syntax"></a>구문  
  
```  
  
DELETE FROM [DatabaseName!]TableName  
   [WHERE FilterCondition1 [AND | OR FilterCondition2 ...]]  
```  
  
## <a name="arguments"></a>인수  
 [ *DatabaseName!*] *TableName*  
 삭제 하도록 표시 된 레코드가 있는 테이블을 지정 합니다.  
  
 *DatabaseName!* 포함 된 데이터베이스 데이터 소스를 사용 하 여 지정 된 데이터베이스가 없는 경우 테이블을 포함 하는 데이터베이스의 이름을 지정 합니다. 데이터베이스 데이터 소스를 사용 하 여 지정 된 데이터베이스가 없는 경우 테이블을 포함 하는 데이터베이스의 이름을 포함 해야 합니다. 데이터베이스 이름 뒤에 오는 및 테이블 이름 앞에 느낌표 (!) 구분 기호를 포함 합니다.  
  
 여기서 *FilterCondition1*[AND &#124; 하거나 *FilterCondition2*...]  
 Visual FoxPro 삭제에 대 한 특정 레코드에만 표시를 지정 합니다.  
  
 *FilterCondition* 레코드 삭제 되도록 표시 하려면 충족 해야 하는 조건을 지정 합니다. AND를 사용 하 여 연결을 원하는 개수 만큼 필터 조건을 포함할 수 있습니다 또는 OR 연산자입니다. 논리 식의 값을 반전 하려면 NOT 연산자를 사용할 수도 있습니다 하거나 사용할 수 있습니다 **빈**빈 필드에 대 한 확인 ().  
  
## <a name="remarks"></a>Remarks  
 설정 삭제가 ON으로 설정 된 경우 범위를 포함 하는 모든 명령에서 삭제 표시 된 레코드가 무시 됩니다.  
  
 DELETE-공유 액세스에 대 한 SQL에서는 열 테이블에서 삭제에 대 한 여러 레코드를 표시 하는 경우 레코드 잠금. 다중 사용자 환경에서 레코드 경합 줄어들지만 성능이 저하 될 수 있습니다. 최상의 성능을 위해 배타적으로 사용에 대 한 테이블을 엽니다.  
  
## <a name="driver-remarks"></a>드라이버 설명  
 응용 프로그램의 데이터 원본에는 ODBC SQL 문을 삭제 보내면 Visual FoxPro ODBC 드라이버 명령을 변환 하지 않아도 Visual FoxPro 삭제 명령으로 변환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SET DELETED 명령](../../odbc/microsoft/set-deleted-command.md)
