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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 10695dd9bf044e270bb1ce1d26de78e53a1dd85a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63026782"
---
# <a name="microsoft-excel-data-types"></a>Microsoft Excel 데이터 형식
다음 표에서 Microsoft Excel 드라이버 데이터 형식을 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 줍니다. Microsoft Excel 드라이버는 이러한 데이터 형식 열에 데이터를 기반으로 하는 Microsoft Excel 테이블의 열에 할당 합니다.  
  
|Microsoft Excel 데이터 형식|ODBC 데이터 형식|  
|-------------------------------|--------------------|  
|Currency|SQL_NUMERIC|  
|DATETIME|SQL_TIMESTAMP|  
|논리|SQL_BIT|  
|NUMBER|SQL_DOUBLE|  
|TEXT|SQL_VARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환 합니다. 부록 D의 모든 변환 합니다 *ODBC 프로그래머 참조* 이 항목의 앞부분에 나열 된 ODBC SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 Microsoft Excel 데이터 형식에 대해 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|암호화된 데이터|Microsoft Excel 드라이버는 암호화 된 데이터를 읽을 수 없습니다.|  
|오류 문자열|Microsoft Excel 드라이버는 Microsoft Excel 오류 값에 대 한 문자열을 반환할 수 없습니다 (# n/A!, #VALUE!, #REF!, #DIV 0!, #NUM!, #NAME?, 및 #NULL!), 하지만 대신 NULL을 반환 합니다.|  
|논리|논리적 열 값은 0 또는 1로 SQL_C_CHAR 버퍼에 반환 됩니다.|  
|NUMBER|정수 열이 만들어지면 정수 데이터 형식에 대해 너무 큰 숫자를 입력 하 고 열 SQL_DOUBLE 변환 될 수 있다는 결과 사용 하 여 정수가 아닌 값이 포함 된 데이터에 삽입할를 수 있습니다.|  
|TEXT|열의 행에 둘 이상의 Microsoft Excel 데이터 형식을 포함 하는 경우 ODBC Microsoft Excel 드라이버 SQL_VARCHAR 데이터 형식 열에 할당 합니다. 이 한 가지 예외가: 열의 날짜/시간 데이터 형식 (날짜, 시간 및 날짜/시간)의 세 가지 또는 두 개만 있으면 ODBC Microsoft Excel 드라이버 SQL_TIMESTAMP 데이터 형식 열을 지정 합니다.<br /><br /> 0 텍스트 열을 만들 지정 되지 않은 길이 255 바이트 열을 실제로 반환 합니다.<br /><br /> 리터럴 문자열을 ANSI 문자 (1-255 10 진수)를 포함할 수 있습니다. 두 개의 연속 된 작은따옴표가 (")를 사용 하 여 하나의 작은따옴표 (')를 나타냅니다.<br /><br /> SQL_VARCHAR 이외의 데이터 형식을 가진 열에 NULL을 삽입 하면 SQL_VARCHAR를 변경 하려면 열의 데이터 형식입니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 찾을 수 있습니다 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)합니다.
