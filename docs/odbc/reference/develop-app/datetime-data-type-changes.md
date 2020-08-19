---
description: 날짜/시간 데이터 형식 변경
title: Datetime 데이터 형식 변경 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- time data type [ODBC]
- datetime data types [ODBC]
- date data type [ODBC]
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- compatibility [ODBC], datetime data types
ms.assetid: c38c79f9-8bb0-4633-ac86-542366c09a95
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a36339f275ff03584a3682f9f57eeeb8445faf3b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424755"
---
# <a name="datetime-data-type-changes"></a>날짜/시간 데이터 형식 변경
*ODBC 3.x에서는 date*, time 및 timestamp SQL 데이터 형식에 대 한 식별자가 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP (헤더 파일의 **#define** 인스턴스를 사용 하 여 9, 10 및 11)에서 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP (91, 92 및 93의 헤더 파일의 **#define** 인스턴스 사용)로 변경 되었습니다. 해당 C 형식 식별자는 SQL_C_DATE, SQL_C_TIME 및 SQL_C_TIMESTAMP에서 각각 SQL_C_TYPE_DATE, SQL_C_TYPE_TIME 및 SQL_C_TYPE_TIMESTAMP로 변경 되었습니다.  
  
 ODBC 3.x의 SQL datetime 데이터 형식에 대해 *반환 되는* 열 크기와 소수 자릿수 *는 odbc 2.x*에서 반환 된 전체 자릿수 및 소수 자릿수와 동일 합니다. 이러한 값은 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)를 참조 하십시오.  
  
 이러한 변경 내용은 **SQLDescribeCol**, **SQLDescribeParam**및 **sqlcolattribute**에 영향을 줍니다. **SQLBindCol**, **SQLBindParameter**및 **SQLGetData**; 및 **Sqlcolumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLStatistics**및 **SQLSpecialColumns**입니다.  
  
 다음 표에서는 ODBC *3.X 드라이버 관리자* 가 **SQLBindCol** 및 **SQLGetData** 의 *TargetType* 인수에 입력 된 날짜, 시간 및 타임 스탬프 C 데이터 형식을 **SQLBindParameter**의 *ValueType* 인수에 매핑하는 방법을 보여 줍니다.  
  
|데이터 형식<br /><br /> 코드 입력 됨|2.x *앱을*<br /><br /> *2.x* 2.x 드라이버|2.x *앱을*<br /><br /> *3(sp3)* 드라이버|*3. x* 앱<br /><br /> *2.x* 2.x 드라이버|*3. x* 앱<br /><br /> *3(sp3)* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|매핑 없음|SQL_C_TYPE_DATE (91)|매핑 없음 [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|오류 (DM)|오류 (DM)|SQL_C_DATE (9)|매핑 없음 [2]|  
|SQL_C_TIME (10)|매핑 없음|SQL_C_TYPE_TIME (92)|매핑 없음 [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|오류 (DM)|오류 (DM)|SQL_C_TIME (10)|매핑 없음 [2]|  
|SQL_C_TIMESTAMP (11)|매핑 없음|SQL_C_TYPE_TIMESTAMP (93)|매핑 없음 [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|오류 (DM)|오류 (DM)|SQL_C_TIMESTAMP (11)|매핑 없음 [2]|  
  
 [1]이로 인해 ODBC 2.x 드라이버를 사용 하 여 작업 하는 ODBC *2.x 응용 프로그램* 은 카탈로그 함수에서 반환 된 결과 집합에 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 *있습니다.*  
  
 [2]이로 인해 ODBC 3.x 드라이버를 사용 하는 ODBC *2.x 응용 프로그램* 은 카탈로그 함수에서 반환 된 결과 집합에 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 *있습니다.*  
  
 다음 표에서 *는 ODBC 3.X* 드라이버 관리자가 **SQLBindParameter** 의 *ParameterType* 인수 또는 **SQLGetTypeInfo**의 *DataType* 인수에 입력 된 날짜, 시간 및 타임 스탬프 SQL 데이터 형식을 매핑하는 방법을 보여 줍니다.  
  
|데이터 형식<br /><br /> 코드 입력 됨|2.x *앱을*<br /><br /> *2.x* 2.x 드라이버|2.x *앱을*<br /><br /> *3(sp3)* 드라이버|*3. x* 앱<br /><br /> *2.x* 2.x 드라이버|*3. x* 앱<br /><br /> *3(sp3)* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|매핑 없음|SQL_TYPE_DATE(91)|매핑 없음 [1]|SQL_TYPE_DATE(91)|  
|SQL_TYPE_DATE(91)|오류 (DM)|오류 (DM)|SQL_DATE (9)|매핑 없음 [2]|  
|SQL_TIME (10)|매핑 없음|SQL_TYPE_TIME (92)|매핑 없음 [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|오류 (DM)|오류 (DM)|SQL_TIME (10)|매핑 없음 [2]|  
|SQL_TIMESTAMP (11)|매핑 없음|SQL_TYPE_TIMESTAMP(93)|매핑 없음 [1]|SQL_TYPE_TIMESTAMP(93)|  
|SQL_TYPE_TIMESTAMP(93)|오류 (DM)|오류 (DM)|SQL_TIMESTAMP (11)|매핑 없음 [2]|  
  
 [1]이로 인해 ODBC 2.x 드라이버를 사용 하 여 작업 하는 ODBC *2.x 응용 프로그램* 은 카탈로그 함수에서 반환 된 결과 집합에 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 *있습니다.*  
  
 [2]이로 인해 ODBC 3.x 드라이버를 사용 하는 ODBC *2.x 응용 프로그램* 은 카탈로그 함수에서 반환 된 결과 집합에 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 *있습니다.*
