---
title: 따옴표 붙은 식별자 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0a81237eddd4836394cc9797a79690ba4b49a35
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861648"
---
# <a name="quoted-identifiers"></a>따옴표 붙은 식별자
SQL 문에서 특수 문자나 일치 키워드를 포함 하는 식별자 묶어야 *식별자 따옴표*;와 같은 문자 묶인 식별자 라고 *따옴표 붙은 식별자*(라고도 *구분 식별자* SQL-92에). 예를 들어, Accounts Payable 식별자 다음에 나와 **선택** 문:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 따옴표 식별자에 대 한 원인은 문을 구문 분석할 되도록 합니다. 예를 들어, Accounts Payable 따옴표가 붙지 않았습니다 이전 문에서 경우 파서는 있었습니다 계정과 Payable, 두 테이블을 가정 되 고 쉼표로 구분 된 올바르지 않은 구문 오류를 반환 합니다. 인용 문자는 식별자는 드라이버 및 SQL_IDENTIFIER_QUOTE_CHAR 옵션을 사용 하 여 검색 **SQLGetInfo**합니다. 키워드 및 특수 문자의 목록을 SQL_SPECIAL_CHARACTERS 및 SQL_KEYWORDS 옵션을 사용 하 여 검색 됩니다 **SQLGetInfo**합니다.  
  
 안전 하 게 하려면 상호 운용 가능한 응용 프로그램은 Oracle ROWID 열과 같이 의사 (pseudo) 열을 제외한 모든 식별자를 자주 측정 합니다. **SQLSpecialColumns** 의사 (pseudo) 열 목록을 반환 합니다. 또한 개체 이름에 특수 한 문자가 나타나는 수에 대 한 응용 프로그램별 제한의 경우 것이 좋습니다 상호 운용 가능한 응용 프로그램의 해당 위치에 특수 문자는 사용할 수 없습니다.
