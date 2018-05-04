---
title: 따옴표 붙은 식별자 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3af402bd63bf1892b1906da34114d5515e6dfa30
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="quoted-identifiers"></a>따옴표 붙은 식별자
SQL 문 특수 문자 또는 일치 키워드를 포함 하는 식별자에 포함 되어야 합니다 *식별자 인용 문자*; 이러한 문자로 묶인 식별자 라고 *따옴표 붙은 식별자*(라고도 *구분 식별자* s Q l-92에). Accounts Payable 식별자 다음에 인용 된 예를 들어 **선택** 문:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 따옴표 식별자에 대 한 이유는 문을 구문 분석할 확인 하기 위해서입니다. 예를 들어 위의 문에서 Accounts Payable 따옴표가 붙지 않았습니다, 파서가 경우 두 개의 테이블, 계정 및 과장, 되었습니다 가정을 쉼표로 구분 된 없었기 구문 오류를 반환 합니다. 인용 문자가 식별자는 드라이버 다르며 SQL_IDENTIFIER_QUOTE_CHAR 옵션에서 검색 됩니다 **SQLGetInfo**합니다. 키워드 및 특수 문자의 목록 SQL_SPECIAL_CHARACTERS 및 SQL_KEYWORDS 옵션에서 검색 됩니다 **SQLGetInfo**합니다.  
  
 안전한 상호 운용 가능한 응용 프로그램 자주 Oracle에서 행 ID 열 등의 의사 (pseudo) 열에 대 한 것을 제외한 모든 식별자를 측정 합니다. **SQLSpecialColumns** 의사 열 목록을 반환 합니다. 또한 개체 이름에 사용할 수 있는 특수 문자에 대 한 응용 프로그램별 제한 인 것이 좋습니다를 해당 위치에 특수 문자를 사용 하지 않는 상호 운용 가능한 응용 프로그램.
