---
description: 따옴표 붙은 식별자
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cd317e5d92618d8b458d6d28fa870c6945e136fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465683"
---
# <a name="quoted-identifiers"></a>따옴표 붙은 식별자
SQL 문에서 특수 문자 또는 match 키워드를 포함 하는 식별자는 *식별자 따옴표 문자로*묶어야 합니다. 이러한 문자로 묶인 식별자를 *따옴표 붙은 식별자* (SQL-92에서는 *구분 식별자* 라고도 함) 라고 합니다. 예를 들어 외상 매입금 식별자는 다음 **SELECT** 문에서 따옴표로 묶여 있습니다.  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 식별자를 따옴표로 묶는 이유는 문을 구문 분석할 하는 것입니다. 예를 들어 외상 매입금 계정이 이전 문에서 따옴표로 묶여 있지 않은 경우 파서는 외상 and 매입금 라는 두 개의 테이블이 있다고 가정 하 고 쉼표로 구분 되지 않는 구문 오류를 반환 합니다. 식별자 따옴표 문자는 드라이버에 한정 되며 **SQLGetInfo**의 SQL_IDENTIFIER_QUOTE_CHAR 옵션을 사용 하 여 검색 됩니다. 특수 문자 및 키워드의 목록은 **SQLGetInfo**의 SQL_SPECIAL_CHARACTERS 및 SQL_KEYWORDS 옵션을 사용 하 여 검색 됩니다.  
  
 안전 하 게 보호 하기 위해 상호 운용 가능한 응용 프로그램은 종종 Oracle의 ROWID 열과 같은 의사 (pseudo) 열에 대 한 식별자를 제외한 모든 식별자를 따옴표로 묶습니다. **SQLSpecialColumns** 는 의사 (pseudo) 열 목록을 반환 합니다. 또한 개체 이름에 특수 문자가 나타날 수 있는 위치에 대 한 응용 프로그램별 제한이 있는 경우 해당 위치에서 특수 문자를 사용 하지 않는 상호 운용 가능한 응용 프로그램에 가장 적합 합니다.
