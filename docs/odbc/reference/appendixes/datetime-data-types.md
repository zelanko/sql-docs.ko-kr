---
title: 날짜/시간 데이터 형식 | Microsoft Docs
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
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 730d72fecb5b452949d7336a59586f877cb09b40
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="datetime-data-types"></a>날짜/시간 데이터 형식
ODBC 3에서 *.x*, 날짜에 대 한 식별자, SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP에서 time 및 timestamp SQL 데이터 형식 변경 (의 인스턴스와 **#define** 9, 10 및 11의 헤더 파일에서) SQL_를 TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP (의 인스턴스와 **#define** 91이 고, 92, 및 93 헤더 파일에), 각각. 인스턴스 식별자에서 변경 SQL_C_DATE, SQL_C_TIME, 및 SQL_C_TIMESTAMP SQL_C_TYPE_DATE, SQL_C_TYPE_TIME, 및 SQL_C_TYPE_TIMESTAMP를 각각 해당 C 형식 및 인스턴스 **#define** 변경 적절 하 게 합니다.  
  
 ODBC 3에서 SQL 날짜/시간 데이터 형식에 반환 된 열 크기 및 소수 자릿수 *.x* 는 ODBC 2에서에 반환 되는 자릿수와 소수 자릿수와 동일 합니다. *x*합니다. 이러한 값은 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. (자세한 내용은 참조 [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.)  
  
 이러한 변경에 영향을 **SQLDescribeCol**, **SQLDescribeParam**, 및 **SQLColAttributes**; **SQLBindCol**, **SQLBindParameter**, 및 **SQLGetData**; 및 **SQLColumns**, **SQLGetTypeInfo** , **SQLProcedureColumns**, **SQLStatistics**, 및 **SQLSpecialColumns**합니다.  
  
 ODBC 3 *.x* 드라이버 SQL_ATTR_ODBC_VERSION 환경 특성의 설정에 따라 이전 단락에 나열 된 함수 호출을 처리 합니다. 에 대 한 **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**, 및 **SQLStatistics** sql_attr_odbc_version으로로 설정 되어 있으면 SQL_OV_ODBC3, 함수 반환 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP DATA_TYPE 필드에, 합니다. COLUMN_SIZE 열의 (반환한 결과 집합에서 **SQLColumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, 및 **SQLSpecialColumns**) 근사 숫자 형식에 대 한 이진 정밀도 포함합니다. NUM_PREC_RADIX 열 (반환한 결과 집합에서 **SQLColumns**, **SQLGetTypeInfo**, 및 **SQLProcedureColumns**) 2의 값을 포함 합니다. COLUMN_SIZE 열의 근사치 숫자 형식 및 NUM_PREC_RADIX 열에 대 한 소수점 정밀도 포함 sql_attr_odbc_version으로 설정 되어 있으면 SQL_OV_ODBC2, 다음 함수 반환 SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP DATA_TYPE 필드에, 10의 값을 포함합니다.  
  
 모든 데이터 형식에 대 한 호출에서 요청 된 경우 **SQLGetTypeInfo**, ODBC 3에 정의 된 함수에서 반환 된 결과 집합 통해 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP를 포함 됩니다 *.x*, 및의 경우 SQL_DATE, SQL_TIME, 및 SQL_TIMESTAMP ODBC 2에 정의 된 대로 합니다. *x*합니다.  
  
 방식 때문에 ODBC 3 *.x* 드라이버 관리자가 수행 하는 날짜, 시간 및 타임 스탬프 데이터 형식 매핑, ODBC 3 *.x* 드라이버 인식 필요 **#defines** 91의 92, 및 에 입력 된 날짜, 시간 및 타임 스탬프 C 데이터 형식에 대 한 93는 *TargetType* 의 인수 **SQLBindCol** 및 **SQLGetData** 또는  *ValueType* 의 인수 **SQLBindParameter**, 인식 필요 하 고 **#defines** 91의 92, 및 93 날짜, 시간, 및는 에입력된타임스탬프SQL데이터형식을*ParameterType* 의 인수 **SQLBindParameter** 또는 *DataType* 의 인수 **SQLGetTypeInfo**합니다. 자세한 내용은 참조 [Datetime 데이터 형식 변경 내용은](../../../odbc/reference/develop-app/datetime-data-type-changes.md)합니다.
