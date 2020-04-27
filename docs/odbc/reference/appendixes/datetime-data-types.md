---
title: Datetime 데이터 형식 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 10626c4f0bf2e33c70322a0eb49af6c3e01e4303
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307064"
---
# <a name="datetime-data-types"></a>날짜/시간 데이터 형식
*ODBC 3.x에서는 date*, time 및 timestamp SQL 데이터 형식에 대 한 식별자가 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP (헤더 파일의 **#define** 인스턴스를 사용 하 여 9, 10 및 11)에서 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP (91, 92 및 93의 헤더 파일의 **#define** 인스턴스 사용)로 변경 되었습니다. 해당 C 형식 식별자가 SQL_C_DATE, SQL_C_TIME 및 SQL_C_TIMESTAMP에서 각각 SQL_C_TYPE_DATE, SQL_C_TYPE_TIME 및 SQL_C_TYPE_TIMESTAMP으로 변경 되었으며 그에 따라 **#define** 인스턴스가 변경 되었습니다.  
  
 ODBC 3.x의 SQL datetime 데이터 형식에 대해 *반환 되는* 열 크기와 소수 자릿수 *는 odbc 2.x*에서 반환 된 전체 자릿수 및 소수 자릿수와 동일 합니다. 이러한 값은 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.  
  
 이러한 변경 내용은 **SQLDescribeCol**, **SQLDescribeParam**및 **sqlcolattributes**에 영향을 줍니다. **SQLBindCol**, **SQLBindParameter**및 **SQLGetData**; 및 **Sqlcolumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLStatistics**및 **SQLSpecialColumns**입니다.  
  
 ODBC 3.x 드라이버는 SQL_ATTR_ODBC_VERSION 환경 특성의 설정에 따라 이전 단락에 나열 된 함수 호출을 처리 *합니다.* **Sqlcolumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**, **SQLSpecialColumns**및 **SQLStatistics**의 경우 SQL_ATTR_ODBC_VERSION이 SQL_OV_ODBC3으로 설정 된 경우 함수는 SQL_TYPE_TIMESTAMP 필드에서 SQL_TYPE_DATE, SQL_TYPE_TIME 및 DATA_TYPE를 반환 합니다. **Sqlcolumns**, **SQLGetTypeInfo**, **SQLProcedureColumns**및 **SQLSpecialColumns**에서 반환 하는 결과 집합의 COLUMN_SIZE 열에는 근사 숫자 형식에 대 한 이진 전체 자릿수가 포함 됩니다. **Sqlcolumns**, **SQLGetTypeInfo**및 **SQLProcedureColumns**에서 반환 된 결과 집합의 NUM_PREC_RADIX 열에는 값 2가 포함 됩니다. SQL_ATTR_ODBC_VERSION이 SQL_OV_ODBC2으로 설정 된 경우 함수는 SQL_TIMESTAMP 필드에서 SQL_DATE, SQL_TIME 및 DATA_TYPE을 반환 하 고, COLUMN_SIZE 열에는 근사 숫자 형식에 대 한 소수 자릿수가 포함 되며, NUM_PREC_RADIX 열에는 값 10이 포함 됩니다.  
  
 **SQLGetTypeInfo**에 대 한 호출에서 모든 데이터 형식이 요청 될 때 함수에서 반환 되는 결과 집합에 *는 odbc 2.x*에 정의 된 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP *와 odbc 2.x*에 정의 된 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP가 모두 포함 됩니다.  
  
 ODBC *3.X 드라이버 관리자* 가 날짜, 시간 및 타임 스탬프 데이터 형식의 매핑을 수행 하는 방법 때문에 odbc *3. x* 드라이버는 **SQLBindCol** 및 **SQLGetData** 의 *TargetType* *인수에* 입력 된 날짜, 시간 및 타임 스탬프 C 데이터 형식에 대해 91, 92 및 93의, 및만 **인식** **하면 됩니다** **. SQLBindParameter** **의** ParameterType *인수* 에 입력 된 **날짜** , 시간 및 타임 스탬프 SQL 데이터 형식에 *대해서는 #defines* 91, 92 및 93만 인식 해야 합니다. #defines 자세한 내용은 [Datetime 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)을 참조 하세요.
