---
title: C 간격 구조 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bbd920b77fd44eaf4765f0983d7d16feb31a4d91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026588"
---
# <a name="c-interval-structure"></a>C 간격 구조
에 나열 된 각 C 간격 데이터 형식 합니다 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션 간격 데이터를 포함 하도록 동일한 구조를 사용 합니다. 때 **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLGetData** 는, 드라이버 SQL_INTERVAL_STRUCT 구조로 데이터를 반환 합니다.를 호출 하 여 지정 된 값을 사용 합니다 C 데이터 형식에 대 한 응용 프로그램 (에 대 한 호출에서 **SQLBindCol**를 **SQLGetData**, 또는 **SQLBindParameter**) SQL_INTERVAL_STRUCT의 내용을 해석 하려면 을 채웁니다 합니다 *interval_type* 구조체의 필드를 *열거형* C 형식에 해당 하는 값입니다. 드라이버 읽지 않는지 확인 합니다 *interval_type* 간격의 형식을 확인 하려면 필드; SQL_DESC_CONCISE_TYPE 설명자 필드의 값을 검색 합니다. 매개 변수 데이터 구조를 사용 하면 드라이버를 사용 하 여 APD의 SQL_DESC_CONCISE_TYPE 필드에서 응용 프로그램에서 지정 된 값, SQL_INTERVAL_STRUCT의 내용을 해석 응용 프로그램의 값을 설정 하는 경우에는  *interval_type* 필드 값을 다른 값입니다.  
  
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
  
 합니다 *interval_type* 필드는 SQL_INTERVAL_STRUCT의 응용 프로그램 구조는 공용 구조체에 저장 된 나타내며 구조체의 멤버는 관련도 합니다. 합니다 *interval_sign* 필드는 필드를 유도 하는 간격 서명 되어 있지 않으면 SQL_FALSE 값에는 SQL_TRUE 인 경우 선행 필드 음수입니다. 선행 필드 자체의 값은 항상 값에 관계 없이 서명 *interval_sign*합니다. 합니다 *interval_sign* 를 부호 비트로 필드는 역할입니다.
