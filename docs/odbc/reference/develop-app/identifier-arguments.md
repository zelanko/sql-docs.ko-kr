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
ms.openlocfilehash: 93cf744cf105762fb90a92049d6698e67a19d58c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68139003"
---
# <a name="identifier-arguments"></a>식별자 인수
식별자 인수의 문자열이 따옴표 붙은 경우 드라이버는 선행 및 후행 공백을 제거 하 고 문자열을 따옴표 안에 그대로 처리 합니다. 문자열이 따옴표로 묶여 있지 않으면 드라이버는 후행 공백을 제거 하 고 문자열을 대문자로 정리 합니다. 인수가 카탈로그 이름이 고 카탈로그가 지원 되지 않는 경우 식별자 인수를 null 포인터로 설정 하면 SQL_ERROR 및 SQLSTATE HY009 (null 포인터 사용이 잘못 되었습니다)가 반환 됩니다.  
  
 이러한 인수는 SQL_ATTR_METADATA_ID statement 특성이 SQL_TRUE으로 설정 된 경우 식별자 인수로 처리 됩니다. 이 경우 밑줄 (_)과 백분율 기호 (%)가 는 검색 패턴 문자가 아닌 실제 문자로 처리 됩니다. 이러한 인수는 인수에 따라 일반 인수 또는 패턴 인수로 처리 됩니다 (이 특성이 SQL_FALSE로 설정 된 경우).  
  
 특수 문자를 포함 하는 식별자는 SQL 문에서 따옴표로 묶어야 하지만 카탈로그 함수에 전달 된 따옴표 문자는 문자 그대로 해석 되기 때문에 카탈로그 함수 인수로 전달 될 때 따옴표로 묶지 않아야 합니다. 예를 들어 식별자 따옴표 문자 (드라이버별 및 **SQLGetInfo**를 통해 반환 됨)는 큰따옴표 (")로 가정 합니다. **Sqltables** 에 대 한 첫 번째 호출에서는 외상 매입금 테이블에 대 한 정보가 포함 된 결과 집합을 반환 하는 반면 두 번째 호출은 "외상 매입금" 테이블에 대 한 정보를 반환 합니다 .이는 의도 한 것이 아닙니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 따옴표 붙은 식별자는 Oracle의 ROWID와 같이 동일한 이름의 의사 (pseudo) 열과 true 열 이름을 구분 하는 데 사용 됩니다. "ROWID"가 카탈로그 함수의 인수에 전달 되는 경우 함수는 ROWID 의사 (pseudo) 열 (있는 경우)과 함께 작동 합니다. 의사 (pseudo) 열이 없으면 함수는 "ROWID" 열과 함께 작동 합니다. ROWID가 카탈로그 함수의 인수에 전달 되 면이 함수는 ROWID 열에서 작동 합니다.  
  
 따옴표 붙은 식별자에 대 한 자세한 내용은 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)를 참조 하세요.
