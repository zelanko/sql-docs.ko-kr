---
title: 일시적 데이터 유형 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307064"
---
# <a name="datetime-data-types"></a>날짜/시간 데이터 형식
ODBC *3.x에서*날짜, 시간 및 타임스탬프 SQL 데이터 형식에 대한 식별자는 각각 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP(9, 10 및 11의 헤더 파일에 **#define** 인스턴스)에서 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP(헤더 파일의 **#define** 인스턴스 포함)으로 각각 변경되었습니다. 해당 C 유형 식별자가 SQL_C_DATE, SQL_C_TIME 및 SQL_C_TIMESTAMP 각각 SQL_C_TYPE_DATE, SQL_C_TYPE_TIME 및 SQL_C_TYPE_TIMESTAMP 변경되었으며 **#define** 인스턴스가 그에 따라 변경되었습니다.  
  
 ODBC *3.x의* SQL datetime 데이터 형식에 대해 반환되는 열 크기와 소수 자릿수는 ODBC *2.x에서*반환되는 정밀도 및 배율과 동일합니다. 이러한 값은 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 설명자 필드의 값과 다릅니다. 자세한 내용은 열 [크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.  
  
 이러한 변경 사항은 **SQLDescribeCol,** **SQLDescribeParam**및 **SQLColAttributes에**영향을 미칩니다. **SQLBindCol**, **SQLBind매개 변수**및 **SQLGetData**; 및 **SQLColumns,** **SQLGetTypeInfo,** **SQLProcedure열,** **SQLStatistics**및 **SQLSpecialColumns**.  
  
 ODBC *3.x* 드라이버는 SQL_ATTR_ODBC_VERSION 환경 특성설정에 따라 이전 단락에 나열된 함수 호출을 처리합니다. **SQLColumns의**경우 **SQLGetTypeInfo,** **SQL절차열,** **SQL특수열**및 **SQLStatistics는**SQL_ATTR_ODBC_VERSION SQL_OV_ODBC3 설정되면 함수가 DATA_TYPE 필드에서 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP 반환합니다. COLUMN_SIZE **열(SQLColumns에서**반환된 결과 집합, **SQLGetTypeInfo,** **SQLProcedureColumns**및 **SQLSpecialColumns)에는**대략적인 숫자 형식에 대한 이진 정밀도가 포함되어 있습니다. NUM_PREC_RADIX **열(SQLColumns에서**반환되는 결과 집합, **SQLGetTypeInfo**및 **SQLProcedureColumns)에는**2의 값이 포함됩니다. SQL_ATTR_ODBC_VERSION SQL_OV_ODBC2 설정되면 함수는 DATA_TYPE 필드의 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP 반환하며 COLUMN_SIZE 열에는 대략적인 숫자 형식에 대한 소수점 정밀도가 포함되고 NUM_PREC_RADIX 열에는 값이 10입니다.  
  
 **SQLGetTypeInfo**를 호출하는 모든 데이터 형식을 요청하면 함수에서 반환되는 결과 집합에는 ODBC *3.x에*정의된 대로 SQL_TYPE_DATE, SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP, ODBC *2.x에*정의된 SQL_DATE, SQL_TIME 및 SQL_TIMESTAMP 모두 포함됩니다.  
  
 ODBC *3.x* 드라이버 관리자가 날짜, 시간 및 타임스탬프 데이터 형식의 매핑을 수행하는 방법 때문에 ODBC *3.x* 드라이버는 SQLBindCol 및 **SQLGetTypeInfo** **SQLGetData** *DataType* 또는 **SQLBindParameter의** *ValueType* 인수의 *TargetType* 인수에 입력된 날짜, 시간 및 타임스탬프 C 데이터 형식에 대해 91, 92 및 93의 **#defines** 인식하기만 하면 *되며,* **SQLBindType** 의 데이터 형식에 입력된 날짜, 시간 및 타임스탬프 데이터 형식에 대해 91, 92 및 93의 값인 파일만 **#defines** 인식하면 됩니다. **SQLBindParameter** 자세한 내용은 [날짜 시간 데이터 형식 변경](../../../odbc/reference/develop-app/datetime-data-type-changes.md)을 참조하십시오.
