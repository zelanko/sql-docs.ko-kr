---
title: "S Q l 92 CAST 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8389ff0812c91ca5a35007a21d70a2a1ca0baee8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="sql-92-cast-function"></a>S Q l 92 CAST 함수
**캐스트** s Q l-92에 정의 된 함수는 동일는 **변환** ODBC에 정의 된 함수입니다. 해당 하는 함수의 구문은 다음과 같습니다.  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL 92 **캐스트** 함수는 다른 데이터 형식으로 변환할 수 있는 데이터 형식을 보내도록 규정 합니다. (자세한 내용은 SQL 92 사양을 참조). **캐스트** 함수는 FIPS 전환 수준에서 지원 됩니다.  
  
 응용 프로그램에 대 한 지원을 확인할 수는 **캐스트** 다음과 같이 작동 합니다.  
  
1.  호출 **SQLGetInfo** SQL_SQL_CONFORMANCE 정보 유형을 사용 합니다. 정보 유형에 대 한 반환 값은 SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE, 또는 SQL_SC_SQL92_FULL, 하는 경우는 **캐스트** 함수는 지원 합니다.  
  
2.  SQL_SQL_CONFORMANCE 정보 형식의 반환 값 SQL_SC_ENTRY_LEVEL 또는 0 이면 호출 **SQLGetInfo** SQL_SQL92_VALUE_EXPRESSIONS 정보 유형을 사용 합니다. SQL_SVE_CAST 비트가 설정 되 고 **캐스트** 함수는 지원 합니다.
