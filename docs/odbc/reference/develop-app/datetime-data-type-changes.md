---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6bc7e07ab65b5894c3ac2b913e5d4afcbd4f98f1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076958"
---
# <a name="datetime-data-type-changes"></a>날짜/시간 데이터 형식 변경
Odbc에서 *3.x*식별자 날짜, 시간 및 타임 스탬프 SQL 데이터 형식 SQL_TIMESTAMP SQL_DATE, SQL_TIME에서 변경 되었습니다. (인스턴스와 **#define** 9, 10 및 11의 헤더 파일에서) SQL_를 TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP (인스턴스와 **#define** 91, 92, 및 93 헤더 파일에), 각각. 해당 C 형식 식별자는 각각 SQL_C_TYPE_DATE, SQL_C_TYPE_TIME, 및 SQL_C_TYPE_TIMESTAMP를 SQL_C_DATE, SQL_C_TIME, 및 SQL_C_TIMESTAMP에서 변경 되었습니다.  
  
 열 크기 및 소수 자릿수를 ODBC SQL 날짜/시간 데이터 형식에 대 한 반환 *3.x* 는 odbc에서에 반환 되는 자릿수와 소수 자릿수와 동일 *2.x*합니다. 이러한 값 SQL_DESC_PRECISION 및 자릿수가 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. (자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).)  
  
 이러한 변경에 영향을 줍니다 **SQLDescribeCol**하십시오 **SQLDescribeParam**, 및 **SQLColAttribute**; **SQLBindCol**하십시오 **SQLBindParameter**, 및 **SQLGetData**; 및 **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**합니다 **SQLStatistics**, 및 **SQLSpecialColumns**합니다.  
  
 다음 표는 ODBC *3.x* 드라이버 관리자에서 입력 한 날짜, 시간 및 타임 스탬프 C 데이터 형식 매핑을 수행 합니다 *TargetType* 의 인수 **SQLBindCol**하 고 **SQLGetData** 또는 합니다 *ValueType* 인수의 **SQLBindParameter**합니다.  
  
|데이터 형식<br /><br /> 코드 입력|*2.x* 앱<br /><br /> *2.x* 드라이버|*2.x* 앱<br /><br /> *3.x* 드라이버|*3.x* 앱<br /><br /> *2.x* 드라이버|*3.x* 앱<br /><br /> *3.x* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_C_DATE (9)|매핑 없음|SQL_C_TYPE_DATE (91)|매핑 없음 [1]|SQL_C_TYPE_DATE (91)|  
|SQL_C_TYPE_DATE (91)|오류 (DM)에서|오류 (DM)에서|SQL_C_DATE (9)|매핑 없음 [2]|  
|SQL_C_TIME (10)|매핑 없음|SQL_C_TYPE_TIME (92)|매핑 없음 [1]|SQL_C_TYPE_TIME (92)|  
|SQL_C_TYPE_TIME (92)|오류 (DM)에서|오류 (DM)에서|SQL_C_TIME (10)|매핑 없음 [2]|  
|SQL_C_TIMESTAMP (11)|매핑 없음|SQL_C_TYPE_TIMESTAMP (93)|매핑 없음 [1]|SQL_C_TYPE_TIMESTAMP (93)|  
|SQL_C_TYPE_TIMESTAMP (93)|오류 (DM)에서|오류 (DM)에서|SQL_C_TIMESTAMP (11)|매핑 없음 [2]|  
  
 [1]의 결과로이 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *2.x* 카탈로그 함수에 의해 반환 되는 결과 집합으로 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.  
  
 [2]의 결과로이 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *3.x* 카탈로그 함수에 의해 반환 되는 결과 집합으로 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.  
  
 다음 표는 ODBC *3.x* 드라이버 관리자에서 입력 한 날짜, 시간 및 타임 스탬프 SQL 데이터 형식 매핑을 수행 합니다 *ParameterType* 인수의 **SQLBindParameter**  또는 합니다 *DataType* 인수의 **SQLGetTypeInfo**합니다.  
  
|데이터 형식<br /><br /> 코드 입력|*2.x* 앱<br /><br /> *2.x* 드라이버|*2.x* 앱<br /><br /> *3.x* 드라이버|*3.x* 앱<br /><br /> *2.x* 드라이버|*3.x* 앱<br /><br /> *3.x* 드라이버|  
|--------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|-----------------------------------|  
|SQL_DATE (9)|매핑 없음|SQL_TYPE_DATE(91)|매핑 없음 [1]|SQL_TYPE_DATE(91)|  
|SQL_TYPE_DATE(91)|오류 (DM)에서|오류 (DM)에서|SQL_DATE (9)|매핑 없음 [2]|  
|SQL_TIME (10)|매핑 없음|SQL_TYPE_TIME (92)|매핑 없음 [1]|SQL_TYPE_TIME (92)|  
|SQL_TYPE_TIME (92)|오류 (DM)에서|오류 (DM)에서|SQL_TIME (10)|매핑 없음 [2]|  
|SQL_TIMESTAMP (11)|매핑 없음|SQL_TYPE_TIMESTAMP(93)|매핑 없음 [1]|SQL_TYPE_TIMESTAMP(93)|  
|SQL_TYPE_TIMESTAMP(93)|오류 (DM)에서|오류 (DM)에서|SQL_TIMESTAMP (11)|매핑 없음 [2]|  
  
 [1]의 결과로이 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *2.x* 카탈로그 함수에 의해 반환 되는 결과 집합으로 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.  
  
 [2]의 결과로이 ODBC *3.x* ODBC를 사용 하는 응용 프로그램 *3.x* 카탈로그 함수에 의해 반환 되는 결과 집합으로 반환 된 날짜, 시간 또는 타임 스탬프 코드를 사용할 수 있습니다.
