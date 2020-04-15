---
title: 인용식별자 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0c03fa8bbc059566288997b29c899056f26de252
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282006"
---
# <a name="quoted-identifiers"></a>따옴표 붙은 식별자
SQL 문에서 특수 문자 또는 일치 키워드를 포함하는 식별자는 *식별자 따옴표 문자로*동봉되어야 합니다. 이러한 문자로 둘러싸인 식별자를 인용 식별자(SQL-92의 *구분식별자라고도* 함)라고 합니다. *quoted identifiers* 예를 들어, 지급액 식별자는 다음 **SELECT** 명세서에 인용됩니다.  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 식별자를 인용하는 이유는 문을 구문 분석할 수 있도록 하기 위해서입니다. 예를 들어, 이전 문에서 지불 할 수 없는 계정 으로 인용 되지 않은 경우 파서는 두 개의 테이블, 계정 및 지불, 쉼표에 의해 구분 되지 않은 구문 오류를 반환 합니다. 식별자 따옴표 문자는 드라이버에 따라 다르며 **SQLGetInfo**에서 SQL_IDENTIFIER_QUOTE_CHAR 옵션으로 검색됩니다. 특수 문자 및 키워드 목록은 **SQLGetInfo**에서 SQL_SPECIAL_CHARACTERS 및 SQL_KEYWORDS 옵션으로 검색됩니다.  
  
 안전을 위해 상호 운용 가능한 응용 프로그램은 오라클의 ROWID 열과 같은 의사 열에 대한 식별자를 제외한 모든 식별자를 인용하는 경우가 많습니다. **SQLSpecial열은** 의사 열 목록을 반환합니다. 또한 특수 문자가 개체 이름에 나타날 수 있는 위치에 대한 응용 프로그램별 제한이 있는 경우 상호 운용 가능한 응용 프로그램에서 해당 위치에 특수 문자를 사용하지 않는 것이 가장 좋습니다.
