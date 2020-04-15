---
title: 식별자 인수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6831eab30daebe37baecebe3ed7053537d7de8f8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300163"
---
# <a name="identifier-arguments"></a>식별자 인수
식별자 인수의 문자열을 따옴표로 지정하면 드라이버는 선행 및 후행 공백을 제거하고 따옴표 내의 문자열을 문자 그대로 처리합니다. 문자열을 따옴표로 묶지 않으면 드라이버는 후행 공백을 제거하고 문자열을 대문자로 접습니다. 식별자 인수를 null 포인터에 설정하면 인수가 카탈로그 이름이며 카탈로그가 지원되지 않는 한 SQL_ERROR 및 SQLSTATE HY009(null 포인터의 잘못된 사용)가 반환됩니다.  
  
 이러한 인수는 SQL_ATTR_METADATA_ID 문 특성이 SQL_TRUE 설정된 경우 식별자 인수로 처리됩니다. 이 경우 밑줄(_) 및 백분율 기호(%) 검색 패턴 문자가 아닌 실제 문자로 처리됩니다. 이러한 인수는 이 특성이 SQL_FALSE 설정된 경우 인수에 따라 일반 인수 또는 패턴 인수로 처리됩니다.  
  
 특수 문자를 포함하는 식별자는 SQL 문에서 따옴표로 인용해야 하지만 카탈로그 함수에 전달된 따옴표 문자는 문자 그대로 해석되므로 카탈로그 함수 인수로 전달될 때 인용해서는 안 됩니다. 예를 들어 식별자 따옴표 문자(드라이버별 및 **SQLGetInfo를**통해 반환됨)가 이중 따옴표(")라고 가정합니다. **SQLTables에** 대한 첫 번째 호출은 미지급 금품 테이블에 대한 정보가 포함된 결과 집합을 반환하고 두 번째 호출은 의도한 것이 아닌 "미지급금" 테이블에 대한 정보를 반환합니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, "Accounts Payable", SQL_NTS, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "\"Accounts Payable\"", SQL_NTS, NULL, 0);  
```  
  
 quoted식별자는 오라클의 ROWID와 같이 동일한 이름의 의사 열과 실제 열 이름을 구분하는 데 사용됩니다. "ROWID"가 카탈로그 함수의 인수에서 전달되면 함수가 있는 경우 ROWID 의사 열과 함께 작동합니다. 의사 열이 없으면 함수는 "ROWID" 열에서 작동합니다. ROWID가 카탈로그 함수의 인수에 전달되면 이 함수는 ROWID 열에서 작동합니다.  
  
 인용된 식별자에 대한 자세한 내용은 [인용 식별자를](../../../odbc/reference/develop-app/quoted-identifiers.md)참조하십시오.
