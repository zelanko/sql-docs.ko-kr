---
title: 식별자 인수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 156dfaf5c6a6a4ec06a0c96b5f726383cba32ba6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447552"
---
# <a name="identifier-arguments"></a>식별자 인수
식별자 인수에서는 문자열은 따옴표로 묶을 경우 드라이버는 선행 및 후행 공백을 제거 하 고 따옴표 안의 문자열 리터럴로 처리. 문자열에 따옴표가 사용 되지 경우 드라이버 제거 후행 공백 및 접기 문자열을 대문자로 합니다. SQL_ERROR 및 SQLSTATE HY009 반환 식별자 인수를 null 포인터로 설정 (잘못 된 null 포인터)를 사용 하는 경우가 아니면 인수 카탈로그 이름은 카탈로그는 지원 되지 않습니다.  
  
 이러한 인수는 SQL_ATTR_METADATA_ID 문 특성 SQL_TRUE로 설정 된 경우 식별자 인수로 처리 됩니다. 이 경우 밑줄 (_) 및 백분율 기호 (%) 검색 패턴 문자가 아니라 실제 문자로 처리 됩니다. 이 특성이 SQL_FALSE로 설정 된 경우 이러한 인수가 일반 인수 또는 인수에 따라 패턴 인수를 처리 됩니다.  
  
 특수 문자를 포함 하는 식별자 SQL 문에서 따옴표로 묶어야 합니다 하지만 하지 묶어야 카탈로그 함수 인수로 전달 될 때 카탈로그 함수에 전달 된 인용 문자는 문자 그대로 해석 되기 때문에 합니다. 예를 들어 식별자 인용 문자 (드라이버별 및 통해 반환 된 **SQLGetInfo**)는 큰따옴표 ("). 첫 번째 호출은 **SQLTables** 의도 되지 않을 수 있습니다는 "Accounts Payable" 테이블에 대 한 정보를 반환 하는 두 번째 호출 하는 동안 Accounts Payable 테이블에 대 한 정보를 포함 하는 집합 결과 반환 합니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 따옴표 붙은 식별자는 의사 (pseudo) Oracle에서 ROWID 같은 이름 열에서 true 열 이름을 구분 하는 데 사용 됩니다. "ROWID" 카탈로그 함수의 인수로 전달 되 면 있으면 ROWID 의사 (pseudo) 열을 사용 하 여 함수가 작동 합니다. 의사 (pseudo) 열이 없으면 함수는 "ROWID" 열을 사용 하 여 작동 합니다. ROWID 카탈로그 함수의 인수에 전달 되 면 함수 행 ID 열을 사용 하 여 작동 합니다.  
  
 따옴표 붙은 식별자에 대 한 자세한 내용은 참조 하세요. [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)합니다.
