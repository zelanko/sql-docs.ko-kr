---
title: 텍스트 파일 데이터 형식 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7864dc81eaa3dd37f3d0053b2329c8842e445c8d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302661"
---
# <a name="text-file-data-types"></a>텍스트 파일 데이터 형식
다음 표에서는 텍스트 데이터 형식이 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 주며 있습니다. 모든 ODBC SQL 데이터 형식이 ODBC 텍스트 드라이버에서 지원되는 것은 아닙니다.  
  
|텍스트 데이터 형식|ODBC 데이터 형식|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|롱차르 (주)|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC 데이터 형식을 반환합니다. *ODBC 프로그래머* 참조부록 D의 모든 변환은 이전 표에 나열된 SQL 데이터 형식에 대해 지원됩니다.  
  
 다음 표에서는 텍스트 데이터 형식에 대한 제한 사항이 보여 있습니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|CHAR|0 또는 지정되지 않은 길이의 CHAR 열을 만들면 실제로 255비트 열이 반환됩니다.<br /><br /> 구분된 파일에서 CHAR 열은 시작과 끝에 이중 따옴표 구분기호를 가질 수도 있고 없을 수도 있습니다. 고정 길이 파일에서는 이중 따옴표가 구분 기호로 사용되지 않습니다.|  
|DATETIME|MM-DD-YY(예: 01-17-92)<br /><br /> MMM-DD-YY(예: 1월 17-92일)<br /><br /> DD-MMM-YY(예: 1월 17일-92일)<br /><br /> YYY-MM-DD (예: 1992-01-17)<br /><br /> YYYY-MMM-DD (예: 1992-1월-17)<br /><br /> 혼합 날짜 구분 기호는 테이블 내에서 허용되지 않습니다.<br /><br /> 텍스트 ISAM은 Windows 제어판의 국제 설정에 따라 미국 또는 유럽 형식의 DATETIME 필드의 서식을 지정합니다.|  
|FLOAT|최대 너비에는 부호와 소수점이 포함됩니다. Schema.ini에서 너비는 다음과 같이 표시됩니다.<br /><br /> 14.083은 FLOAT 너비 6입니다.<br /><br /> -14.083은 FLOAT 폭 7입니다.<br /><br /> +14.083은 FLOAT 너비 7입니다.<br /><br /> 14083. FLOAT 너비 6<br /><br /> ODBC는 FLOAT 열에 대해 항상 8을 반환합니다.<br /><br /> FLOAT 열은 과학적 표기표현에 있을 수도 있습니다.<br /><br /> -3.04E+2는 부동 폭 8입니다.<br /><br /> 25E4는 부동 폭 4입니다.<br /><br /> **참고 사항** 십진수와 과학적 표기는 열에 혼합할 수 없습니다.<br /><br /> NULL 값은 고정 길이 파일의 빈 패딩 문자열로 표시되며 구분된 파일에서는 생략됩니다.<br /><br /> 플로트 데이터는 선행 공백으로 패딩할 수 있습니다.|  
|INTEGER|정수 열에 대한 유효한 값은 32767 ~ -32766입니다.<br /><br /> Schema.ini에서 너비는 다음과 같이 표시됩니다.<br /><br /> 14083은 정수 너비 5입니다.<br /><br /> 0은 정수 너비 1입니다.<br /><br /> ODBC는 항상 정수 열에 대해 4를 반환합니다.<br /><br /> 최대 너비에는 기호가 포함됩니다. 고정 형식 테이블에서 허용되는 공백으로 인해 너비가 커질 수 있지만 INTEGER 열의 최대 너비는 11입니다.|  
|롱차르 (주)|고정 길이 또는 구분된 테이블의 LONGCHAR 열 너비에 대한 이론적 제한은 65500K입니다. 텍스트 ISAM은 최대 약 32K의 안정적인 지원을 제공할 가능성이 높습니다.|  
  
 데이터 형식에 대한 더 많은 제한 사항은 [데이터 형식 제한에서](../../odbc/microsoft/data-type-limitations.md)찾을 수 있습니다.
