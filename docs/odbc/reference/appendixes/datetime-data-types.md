---
title: 날짜/시간 데이터 형식 | Microsoft Docs
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
- data types [ODBC], date
- backward compatibility [ODBC], datetime data types
- timestamp data type [ODBC]
- data types [ODBC], timestamp
- data types [ODBC], backward compatibility
- compatibility [ODBC], datetime data types
- data types [ODBC], time
ms.assetid: 6b9363c9-04bf-4492-a210-7aa15dea4af8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1cb92afa9467717b8a589ddbcaee4ab8a5a529f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130086"
---
# <a name="datetime-data-types"></a>날짜/시간 데이터 형식
Odbc에서 *3.x*식별자 날짜, 시간 및 타임 스탬프 SQL 데이터 형식 SQL_TIMESTAMP SQL_DATE, SQL_TIME에서 변경 되었습니다. (인스턴스와 **#define** 9, 10 및 11의 헤더 파일에서) SQL_를 TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP (인스턴스와 **#define** 91, 92, 및 93 헤더 파일에), 각각. 식별자에서 변경 SQL_C_DATE, SQL_C_TIME, 및 SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME, 및 SQL_C_TYPE_TIMESTAMP를 각각 해당 C 형식 및 인스턴스 **#define** 변경 적절 하 게 합니다.  
  
 열 크기 및 소수 자릿수를 ODBC SQL 날짜/시간 데이터 형식에 대 한 반환 *3.x* 는 odbc에서에 반환 되는 자릿수와 소수 자릿수와 동일 *2.x*합니다. 이러한 값 SQL_DESC_PRECISION 및 자릿수가 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. (자세한 내용은 [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식입니다.)  
  
 이러한 변경에 영향을 줍니다 **SQLDescribeCol**하십시오 **SQLDescribeParam**, 및 **SQLColAttributes**; **SQLBindCol**하십시오 **SQLBindParameter**, 및 **SQLGetData**; 및 **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**합니다 **SQLStatistics**, 및 **SQLSpecialColumns**합니다.  
  
 ODBC *3.x* 드라이버 SQL_ATTR_ODBC_VERSION 환경 특성의 설정에 따라 이전 단락에 나열 된 함수 호출을 처리 합니다. 에 대 한 **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**하십시오 **SQLSpecialColumns**, 및 **SQLStatistics** SQL_ATTR_ODBC_VERSION로 설정 된 경우 함수 반환을 SQL_OV_ODBC3 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP DATA_TYPE 필드에, 합니다. COLUMN_SIZE 열의 (반환한 결과 집합의 **SQLColumns**를 **SQLGetTypeInfo**합니다 **SQLProcedureColumns**, 및 **SQLSpecialColumns**) 대략적인 숫자 형식에 대 한 이진 정밀도 포함합니다. NUM_PREC_RADIX 열 (반환한 결과 집합의 **SQLColumns**를 **SQLGetTypeInfo**, 및 **SQLProcedureColumns**) 2의 값을 포함 합니다. COLUMN_SIZE 열의 대략적인 숫자 형식 및 NUM_PREC_RADIX 열에 대 한 소수점 전체 자릿수를 SQL_ATTR_ODBC_VERSION으로 설정 된 SQL_OV_ODBC2, 다음 함수 반환 SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP DATA_TYPE 필드에 하는 경우 포함 10의 값을 포함합니다.  
  
 모든 데이터 형식에 대 한 호출에서 요청 하는 경우 **SQLGetTypeInfo**, ODBC에 정의 된 대로 함수에서 반환한 결과 집합에는 모두 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP에 포함 됩니다 *3.x*, SQL_DATE, SQL_TIME, 및 ODBC에 정의 된 대로 SQL_TIMESTAMP *2.x*합니다.  
  
 방식 때문에 ODBC *3.x* 드라이버 관리자는 date, time 및 timestamp 데이터 형식, ODBC의 매핑을 수행 *3.x* 드라이버 인식 해야 **#defines** 의 91, 92, 및 에 입력 한 날짜, 시간 및 타임 스탬프 C 데이터 형식에 대 한 93 합니다 *TargetType* 인수 **SQLBindCol** 하 고 **SQLGetData** 또는  *ValueType* 인수의 **SQLBindParameter**에 인식 해야 **#defines** 91의 92, 및 93 날짜, 시간, 타임 스탬프 SQL 데이터 형식에에서을 입력 합니다 *ParameterType* 인수의 **SQLBindParameter** 나 *DataType* 인수의 **SQLGetTypeInfo**합니다. 자세한 내용은 [날짜/시간 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)합니다.
