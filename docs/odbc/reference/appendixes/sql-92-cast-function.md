---
title: S Q l 92 CAST 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7d7d3d00128d4ddbb79c43f53c0d439e6974ddb6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910938"
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
