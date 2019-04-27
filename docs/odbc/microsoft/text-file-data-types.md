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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23416cb067507d821701e57255fdc6f81ee607c4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633008"
---
# <a name="text-file-data-types"></a>텍스트 파일 데이터 형식
다음 표에서 텍스트 데이터 형식을 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 줍니다. 일부 ODBC SQL 데이터 형식이 텍스트 ODBC 드라이버에서 지원 하는지 참고 합니다.  
  
|Text 데이터 형식|ODBC 데이터 형식|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC 데이터 형식을 반환 합니다. 부록 D의 모든 변환 합니다 *ODBC 프로그래머 참조* 이전 표에 나열 된 SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 텍스트 데이터 형식의 제한 사항 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|CHAR|0 CHAR 열을 만들 지정 되지 않은 길이 실제로 255 bit 열을 반환 합니다.<br /><br /> 구분 기호로 분리 된 파일에 CHAR 열 수도 있고 있습니다 처음과 끝; 큰따옴표 구분 기호 고정 길이 파일에서 큰따옴표를 구분 기호로 사용 되지 않습니다.|  
|DATETIME|MM-DD-YY (예: 92-01-17)<br /><br /> MMM DD YY (예를 들어 1 월 1 일-17-92)<br /><br /> DD-MMM-YY (예를 들어 17-월-92)<br /><br /> YYYY-월-일 (예: 1992-01-17)<br /><br /> YYYY-MMM-일 (예: 1992-월-17)<br /><br /> 혼합된 날짜 구분 기호 테이블 내에서 허용 되지 않습니다.<br /><br /> 텍스트 ISAM Windows 제어판의 국가별 설정에 따라 미국 또는 유럽 형식으로 DATETIME 필드에 서식을 지정 합니다.|  
|FLOAT|최대 너비는 기호와 소수점을 포함합니다. Schema.ini, 너비를 다음과 같이 표시 됩니다.<br /><br /> 14.083은 너비가 6 FLOAT<br /><br /> -14.083은 고정 너비 7<br /><br /> +14.083은 고정 너비 7<br /><br /> 14083는 FLOAT 너비가 6<br /><br /> ODBC는 항상 FLOAT 열에 대 한 8을 반환합니다.<br /><br /> 예를 들어 과학적 표기법에 FLOAT 열 있을 수도 있습니다.<br /><br /> -3.04E + 2는 너비 8 Float<br /><br /> 25E4은 고정 너비 4<br /><br /> **참고** 열에 10 진수 및 과학 표기법을 혼합할 수 없습니다.<br /><br /> NULL 값 고정 길이 파일에서 채워진 빈 문자열로 표시 되 고 구분 기호로 분리 된 파일에서 생략 됩니다.<br /><br /> Float 데이터 앞에 공백을 사용 하 여 채워질 수 있습니다.|  
|INTEGER|정수 열에 대 한 유효한 값은-32766을 32767 사이입니다.<br /><br /> Schema.ini, 너비를 다음과 같이 표시 됩니다.<br /><br /> 14083은 정수 너비 5<br /><br /> 0은 정수 너비 1<br /><br /> ODBC는 항상 정수 열에 대 한 4를 반환합니다.<br /><br /> 최대 너비는 기호를 포함합니다. 정수 열 최대 너비는 너비를 고정 형식 테이블에서 허용 되는 공백으로 인해 클 수 있지만 11입니다.|  
|LONGCHAR|이론적 제한에서 LONGCHAR 열의 너비를 고정 길이 또는 구분 기호로 분리 된 테이블 65500 K입니다. 텍스트 ISAM 최대 32k에 대 한 신뢰할 수 있는 지원을 제공 하기 위해 가능성이 더 높습니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 찾을 수 있습니다 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)합니다.
