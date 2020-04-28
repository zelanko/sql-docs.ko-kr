---
title: Microsoft Excel 데이터 형식 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81283773"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 데이터 형식
다음 표에서는 Microsoft Excel 드라이버 데이터 형식을 ODBC SQL 데이터 형식에 매핑하는 방법을 보여 줍니다. Microsoft Excel 드라이버는 열의 데이터를 기반으로 Microsoft Excel 테이블의 열에 이러한 데이터 형식을 할당 합니다.  
  
|Microsoft Excel 데이터 형식|ODBC 데이터 형식|  
|-------------------------------|--------------------|  
|Currency|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|논리곱|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC SQL 데이터 형식을 반환 합니다. *Odbc 프로그래머 참조* 의 부록 D에 있는 모든 변환은이 항목의 앞부분에 나열 된 odbc SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서는 Microsoft Excel 데이터 형식에 대 한 제한 사항을 보여 줍니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|암호화된 데이터|Microsoft Excel driver에서 암호화 된 데이터를 읽을 수 없습니다.|  
|오류 문자열|Microsoft Excel 드라이버는 Microsoft Excel 오류 값 (#N/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME? 및 #NULL!)에 대 한 문자열을 반환할 수 없지만 대신 NULL을 반환 합니다.|  
|논리곱|논리적 열의 값은 0 또는 1로 SQL_C_CHAR 버퍼에서 반환 됩니다.|  
|NUMBER|정수 열을 만들 경우 정수 데이터 형식에 대해 너무 큰 숫자를 입력할 수 있으며, 정수가 아닌 값을 포함 하는 데이터를 삽입할 수 있으며, 그 결과 열이 SQL_DOUBLE으로 변환 될 수 있습니다.|  
|TEXT|열의 행에 두 개 이상의 Microsoft Excel 데이터 형식이 포함 된 경우 ODBC Microsoft Excel driver는 열에 SQL_VARCHAR 데이터 형식을 할당 합니다. 이에 대 한 한 가지 예외가 있습니다. 열에 datetime 데이터 형식 (DATE, TIME 및 DATETIME)이 2 ~ 3 개만 있는 경우 ODBC Microsoft Excel driver는 열에 SQL_TIMESTAMP 데이터 형식을 할당 합니다.<br /><br /> 0 또는 지정 되지 않은 길이의 텍스트 열을 만들면 실제로 255 바이트 열이 반환 됩니다.<br /><br /> 문자열 리터럴은 ANSI 문자 (1-255 10 진수)를 포함할 수 있습니다. 작은따옴표 두 개 (")를 사용 하 여 작은따옴표 하나 (')를 나타냅니다.<br /><br /> SQL_VARCHAR 아닌 데이터 형식의 열에 NULL을 삽입 하면 열의 데이터 형식이 SQL_VARCHAR으로 변경 됩니다.|  
  
 데이터 형식에 대 한 더 많은 제한은 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)에서 찾을 수 있습니다.
