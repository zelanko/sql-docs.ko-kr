---
title: 마이크로소프트 엑셀 데이터 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8574985e10e5aaa3ae5431af7ee1245643e20b60
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283773"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 데이터 형식
다음 표에서는 Microsoft Excel 드라이버 데이터 형식이 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 주며 있습니다. Microsoft Excel 드라이버는 열의 데이터를 기반으로 Microsoft Excel 테이블의 열에 이러한 데이터 형식을 할당합니다.  
  
|마이크로 소프트 엑셀 데이터 유형|ODBC 데이터 형식|  
|-------------------------------|--------------------|  
|Currency|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|논리|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환합니다. *ODBC 프로그래머* 참조부록 D의 모든 변환은 이 항목의 앞에 나열된 ODBC SQL 데이터 형식에 대해 지원됩니다.  
  
 다음 표에서는 Microsoft Excel 데이터 형식에 대한 제한 사항이 보여 있습니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|암호화된 데이터|Microsoft Excel 드라이버는 암호화된 데이터를 읽을 수 없습니다.|  
|오류 문자열|Microsoft Excel 드라이버는 Microsoft Excel 오류 값(#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME?, #NULL!)에 대한 문자 문자열을 반환할 수 없지만 NULL을 반환합니다.|  
|논리|논리 열의 값은 SQL_C_CHAR 버퍼에서 0 또는 1로 반환됩니다.|  
|NUMBER|정수 열을 만들면 정수 데이터 형식에 대해 너무 큰 숫자를 입력할 수 있으며 정수 가 아닌 값을 포함하는 데이터를 삽입할 수 있으며 그 결과 열이 SQL_DOUBLE 변환될 수 있습니다.|  
|TEXT|열의 행에 두 개 이상의 Microsoft Excel 데이터 형식이 포함된 경우 ODBC Microsoft Excel 드라이버는 SQL_VARCHAR 데이터 형식을 열에 할당합니다. 한 가지 예외가 있습니다: 열에 날짜 시간 데이터 형식(날짜, 시간 및 DATETIME)이 두개 또는 세 개만 포함된 경우 ODBC Microsoft Excel 드라이버는 SQL_TIMESTAMP 데이터 형식을 열에 할당합니다.<br /><br /> 0 또는 지정되지 않은 길이의 TEXT 열을 만들면 실제로 255바이트 열이 반환됩니다.<br /><br /> 문자 문자열 리터럴은 ANSI 문자(소수점 1-255)를 포함할 수 있습니다. 두 개의 연속된 단일 따옴표(")를 사용하여 하나의 따옴표(')를 나타냅니다.<br /><br /> SQL_VARCHAR 이외의 데이터 형식이 있는 열에 NULL을 삽입하면 열의 데이터 형식이 SQL_VARCHAR 변경됩니다.|  
  
 데이터 형식에 대한 더 많은 제한 사항은 [데이터 형식 제한에서](../../odbc/microsoft/data-type-limitations.md)찾을 수 있습니다.
