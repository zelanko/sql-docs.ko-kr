---
title: "식별자 인수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- identifier arguments [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], identifier
ms.assetid: b9de003f-cb49-4dec-b528-14a5b8ff12bd
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1a81844609833db4953102f72d2eb6d0939cfc78
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="identifier-arguments"></a>식별자 인수
식별자 인수에 문자열에 따옴표를 드라이버 선행 및 후행 공백을 제거 하 고 따옴표 안에 문자열 리터럴로 처리 합니다. 문자열에 따옴표가 사용 되지 드라이버 제거 후행 공백 및 접기 문자열을 대문자로 합니다. SQL_ERROR 및 SQLSTATE HY009 반환 식별자 인수는 null 포인터를 설정 (잘못 된 null 포인터)를 사용 하는 경우가 아니면 인수가 카탈로그 이름을 카탈로그는 지원 되지 않습니다.  
  
 이 인수는 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE로 설정 된 경우 식별자 인수로 처리 됩니다. 이 경우 밑줄 (_) 및 백분율 기호 (%) 검색 패턴 문자 아니라 실제 문자로 처리 됩니다. 이 인수는이 특성은 SQL_FALSE로 설정 하는 경우에 일반 인수 또는 인수에 따라 패턴 인수를으로 처리 됩니다.  
  
 SQL 문에서 특수 문자를 포함 하는 식별자에 포함 되어야 하지만 하지 묶어야 카탈로그 함수 인수로 전달 될 때 카탈로그 함수에 전달 된 인용 문자는 문자 그대로 해석 되기 때문에 있습니다. 예를 들어 식별자 역따옴표 문자 (드라이버 관련 되며를 통해 반환 된 **SQLGetInfo**)는 큰따옴표 ("). 첫 번째 호출 **SQLTables** 두 번째 호출에서 의도 하지 않이 되는 "Accounts Payable" 테이블에 대 한 정보를 반환 하는 동안 Accounts Payable 테이블에 대 한 정보를 포함 한 결과 집합을 반환 합니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 따옴표 붙은 식별자는 동일한 이름의 Oracle에서 ROWID 같은 의사 열에서 true 열 이름을 구분 하는 데 사용 됩니다. "ROWID" 카탈로그 함수의 인수에 전달 되 면이 특성이 있으면 함수는 ROWID 의사 열과 작동 합니다. 의사 열이 없는 경우 함수는 "ROWID" 열과 작동 합니다. ROWID 카탈로그 함수의 인수에 전달 되 면 함수 행 ID 열과 사용 합니다.  
  
 따옴표 붙은 식별자에 대 한 자세한 내용은 참조 [따옴표 붙은 식별자](../../../odbc/reference/develop-app/quoted-identifiers.md)합니다.
