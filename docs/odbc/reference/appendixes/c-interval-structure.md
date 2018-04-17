---
title: C 간격 구조 | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 359facef0aecb21eabfd931970d41b3ea3f5d9c9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="c-interval-structure"></a>C 간격 구조
에 나열 된 각 C 간격 데이터 형식의 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 섹션은 동일한 구조를 사용 하 여 간격 데이터를 포함 시키십시오. 때 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLGetData** 은, 드라이버 SQL_INTERVAL_STRUCT 구조에 데이터를 반환 합니다.를 호출 하 여 지정 된 값을 사용 하 여는 C 데이터 형식에 대 한 응용 프로그램 (에 대 한 호출에서 **SQLBindCol**, **SQLGetData**, 또는 **SQLBindParameter**) SQL_INTERVAL_STRUCT의 내용을 해석 하려면 정보를 표시 하 고는 *interval_type* 구조의 필드는 *enum* C 형식에 해당 하는 값입니다. 드라이버 읽지 않는 *interval_type* 간격의 유형을 결정 하도록 필드; SQL_DESC_CONCISE_TYPE 설명자 필드의 값을 검색 합니다. 매개 변수 데이터 구조를 사용 하면 드라이버를 사용 하 여 APD의 SQL_DESC_CONCISE_TYPE 필드에서 응용 프로그램에 의해 지정 된 값, SQL_INTERVAL_STRUCT의 내용을 해석 응용 프로그램의 값을 설정 하는 경우에는  *interval_type* 필드 값을 다른 값입니다.  
  
 이 구조는 다음과 같이 정의 됩니다.  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 *interval_type* 필드는 SQL_INTERVAL_STRUCT의 응용 프로그램에 구조 공용 구조체에 유지 되 나타내고 구조체의 멤버에 관련 된도 합니다. *interval_sign* 필드에 SQL_FALSE 값 필드를 유도 하는 간격 서명 되지 않은 경우에 SQL_TRUE 인 경우 선행 필드 음수입니다. 선행 필드 자체의 값은 항상 값에 상관 없이 서명 된 *interval_sign*합니다. *interval_sign* 필드를 부호 비트로 역할입니다.
