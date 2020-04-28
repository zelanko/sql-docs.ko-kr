---
title: 텍스트 파일 데이터 형식 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81302661"
---
# <a name="text-file-data-types"></a>텍스트 파일 데이터 형식
다음 표에서는 텍스트 데이터 형식이 ODBC SQL 데이터 형식으로 매핑되는 방법을 보여 줍니다. Odbc 텍스트 드라이버에서 모든 ODBC SQL 데이터 형식이 지원 되는 것은 아닙니다.  
  
|Text 데이터 형식|ODBC 데이터 형식|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|이상 문자|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC 데이터 형식을 반환 합니다. *ODBC 프로그래머 참조* 의 부록 D에 있는 모든 변환은 이전 표에 나와 있는 SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서는 텍스트 데이터 형식에 대 한 제한 사항을 보여 줍니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|CHAR|0 또는 지정 되지 않은 길이의 CHAR 열을 만드는 것은 실제로 255 비트 열을 반환 합니다.<br /><br /> 구분 된 파일에서는 CHAR 열이 시작 부분과 끝 부분에 큰따옴표 구분 기호를 포함할 수도 있고 그렇지 않을 수도 있습니다. 고정 길이 파일에서는 큰따옴표를 구분 기호로 사용 하지 않습니다.|  
|DATETIME|MM-DD-YY (예: 01-17-92)<br /><br /> MMM-DD-YY (예: 1 월-17-92)<br /><br /> DD-음-YY (예: 17-Jan-92)<br /><br /> YYYY-MM-DD (예: 1992-01-17)<br /><br /> YYYY-MM-DD (예: 1992-1 월-17)<br /><br /> 테이블 내에서는 혼합 날짜 구분 기호를 사용할 수 없습니다.<br /><br /> 텍스트 ISAM은 Windows 제어판의 국가별 설정에 따라 미국 또는 유럽 형식으로 날짜/시간 필드의 서식을 지정 합니다.|  
|FLOAT|최대 너비는 부호와 소수점을 포함 합니다. Schema.ini에서 너비는 다음과 같이 표시 됩니다.<br /><br /> 14.083은 FLOAT 너비 6입니다.<br /><br /> -14.083은 FLOAT 너비 7입니다.<br /><br /> + 14.083은 FLOAT 너비 7입니다.<br /><br /> 14083. FLOAT 너비는 6입니다.<br /><br /> ODBC는 항상 FLOAT 열에 대해 8을 반환 합니다.<br /><br /> FLOAT 열은 과학적 표기법으로도 사용할 수 있습니다. 예를 들면 다음과 같습니다.<br /><br /> -3.04 e + 2는 Float 너비 8입니다.<br /><br /> 25E4는 Float 너비 4입니다.<br /><br /> **참고** Decimal 및 과학적 표기법은 열에서 혼합할 수 없습니다.<br /><br /> NULL 값은 고정 길이 파일에서 빈 패딩 문자열로 표시 되며 구분 된 파일에서는 생략 됩니다.<br /><br /> Float 데이터는 선행 공백으로 채워질 수 있습니다.|  
|INTEGER|정수 열에 유효한 값은 32767 ~ 32766입니다.<br /><br /> Schema.ini에서 너비는 다음과 같이 표시 됩니다.<br /><br /> 14083은 정수 너비 5입니다.<br /><br /> 0은 정수 너비 1입니다.<br /><br /> ODBC는 항상 정수 열에 대해 4를 반환 합니다.<br /><br /> 최대 너비는 부호를 포함 합니다. 정수 열의 최대 너비는 11 이지만 고정 형식 테이블에서 허용 되는 공백으로 인해 너비가 더 클 수 있습니다.|  
|이상 문자|고정 길이 또는 구분 기호로 분리 된 테이블에서가 나 문자 열의 너비에 대 한 이론적 제한은 65500K입니다. 텍스트 ISAM은 최대 32K까지 신뢰할 수 있는 지원을 제공할 가능성이 높습니다.|  
  
 데이터 형식에 대 한 더 많은 제한은 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)에서 찾을 수 있습니다.
