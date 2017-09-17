---
title: "Microsoft Excel 데이터 형식을 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], Excel driver
- Excel data types [ODBC]
- Jet-based ODBC drivers [ODBC], Excel driver
- desktop database drivers [ODBC], Excel driver
- ODBC desktop database drivers [ODBC], Excel driver
- Excel driver [ODBC], data types
ms.assetid: 7b44c8e5-0bc3-4912-8a5d-56f4d5562fe6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eeb2bc72ce34141eb3dbdca3f952dca0c476c2dd
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 데이터 형식
다음 표에서 Microsoft Excel 드라이버 데이터 형식을 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 줍니다. Microsoft Excel 드라이버는 이러한 데이터 형식을 열에 데이터를 기반으로 하는 Microsoft Excel 테이블의 열에 할당 합니다.  
  
|Microsoft Excel 데이터 형식|ODBC 데이터 형식|  
|-------------------------------|--------------------|  
|Currency|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|논리|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환 합니다. 부록 d의 모든 변환이 *ODBC Programmer's Reference* 이 항목의 앞부분에 나열 된 ODBC SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 Microsoft Excel 데이터 형식에 대해 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|암호화된 데이터|Microsoft Excel 드라이버는 암호화 된 데이터를 읽을 수 없습니다.|  
|오류 문자열|Microsoft Excel 드라이버는 Microsoft Excel 오류 값에 대 한 문자열을 반환할 수 없습니다 (# n/A!, #VALUE!, #REF!, #DIV/0!, #NUM!, #NAME?, 및 #NULL!), 하지만 대신 NULL을 반환 합니다.|  
|논리|논리 열에 있는 값은 0 또는 1으로 SQL_C_CHAR 버퍼에 반환 됩니다.|  
|NUMBER|정수 열이 만들어지면 정수 데이터 형식에 대해 너무 큰 숫자를 입력할 수 있습니다 및 정수가 아닌 값이 포함 된 데이터 삽입할 수 있지만, 결과 열 SQL_DOUBLE 변환 될 수 있습니다.|  
|TEXT|둘 이상의 Microsoft Excel 데이터 형식이 포함 되는 열의 행, Microsoft Excel ODBC 드라이버는 열에 SQL_VARCHAR 데이터 형식을 할당 합니다. 이 한 가지 예외가: 열 2, 날짜/시간 데이터 형식 (날짜, 시간 및 날짜/시간)의 3 개만 있으면 ODBC Microsoft Excel 드라이버 SQL_TIMESTAMP 데이터 형식 열을 지정 합니다.<br /><br /> 0의 텍스트 열 만들기 또는 실제로 지정 되지 않은 길이 255 바이트 열을 반환 합니다.<br /><br /> 문자열 리터럴을 ANSI 문자 (1-255 10 진수)를 포함할 수 있습니다. 하나의 작은따옴표 (')을 나타내기 위해 두 개의 연속 된 작은따옴표가 (")를 사용 합니다.<br /><br /> 이외의 SQL_VARCHAR 데이터 형식의 열에 NULL을 삽입 SQL_VARCHAR로 변경 하려면 열의 데이터 형식을 발생 합니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 확인할 수 있습니다 [데이터 형식 제한](../../odbc/microsoft/data-type-limitations.md)합니다.
