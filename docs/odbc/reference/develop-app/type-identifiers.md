---
title: "형식 식별자 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], identifiers
- type identifiers [ODBC]
- identifiers [ODBC], type
- type identifiers [ODBC], about type identifiers
ms.assetid: 1d9fdfa2-e378-44fe-ac66-9743d9bbdd5a
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: da01de66ee5b20d873b3b50ea24c72549174e90b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="type-identifiers"></a>유형 식별자
ODBC SQL 및 C 데이터 형식을 설명 하기 위해 두 개의 집합이 이미 정의 되어 *형식 식별자*합니다. 형식 식별자에는 SQL 열 또는 C 버퍼의 형식을 설명합니다. 한 **#define** 값 이며 일반적으로 함수 인수로 전달 하거나 메타 데이터의 반환 합니다.  
  
 다음을 호출 하는 예를 들어 **SQLBindParameter** SQL_DATE_STRUCT 형식의 변수는 SQL 문의 날짜 매개 변수를 바인딩합니다. C 형식 식별자 SQL_C_TYPE_DATE의 유형을 지정는 *날짜* 변수와 SQL 유형 식별자 SQL_TYPE_DATE 동적 매개 변수 유형을 지정 합니다.  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER  DateInd = 0;  
SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 0, 0,  
                  &Date, 0, &DateInd);  
```

