---
title: "텍스트 파일 데이터 형식 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- text file driver [ODBC], data types
- ODBC desktop database drivers [ODBC], text file driver
- desktop database drivers [ODBC], text file driver
- text file data types [ODBC]
- Jet-based ODBC drivers [ODBC], text file driver
ms.assetid: e113112e-ae42-469e-8e4b-a365a10d9071
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d3ac713de27efa4ddc41ec52285231dde7518402
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="text-file-data-types"></a>텍스트 파일 데이터 형식
다음 표에서 텍스트 데이터 형식은 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 줍니다. 참고 일부 ODBC SQL 데이터 형식이 텍스트 ODBC 드라이버에서 지원 됩니다.  
  
|Text 데이터 형식|ODBC 데이터 형식|  
|--------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATETIME|SQL_TIMESTAMP|  
|FLOAT|SQL_DOUBLE|  
|INTEGER|SQL_INTEGER|  
|LONGCHAR|SQL_LONGVARCHAR|  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC 데이터 형식을 반환 합니다. 부록 d의 모든 변환이 *ODBC Programmer's Reference* 앞의 표에 나열 된 SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 텍스트 데이터 형식에 대해 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|CHAR|0의 CHAR 열 만들기 또는 지정 되지 않은 길이 실제로 255 bit 열을 반환 합니다.<br /><br /> 구분 기호로 분리 된 파일에서 CHAR 열 수 있습니다 또는 시작 및 끝; 큰따옴표 구분 기호를 사용할 수 없습니다. 고정 길이 파일에서 큰따옴표 구분 기호로 사용 되지 않습니다.|  
|DATETIME|MM-일-년 (예: 01-17-92)<br /><br /> MMM DD YY (예를 들어 1 월-17-92)<br /><br /> DD MMM-확인 (예를 들어 17-월-92)<br /><br /> YYYY-월-일 (예: 1992-01-17)<br /><br /> YYYY-MMM-일 (예: 1992-월-17)<br /><br /> 혼합된 날짜 구분 기호 테이블 내에서 허용 되지 않습니다.<br /><br /> 텍스트 ISAM Windows 제어판의 국가별 설정에 따라 미국 또는 유럽 형식으로 날짜/시간 필드 형식을 지정 합니다.|  
|FLOAT|최대 너비는 부호와 소수점을 포함합니다. Schema.ini, 너비 다음과 같이 표시 됩니다.<br /><br /> 14.083은 너비가 6 FLOAT<br /><br /> -14.083은 FLOAT 너비 7<br /><br /> +14.083은 FLOAT 너비 7<br /><br /> 14083. FLOAT 너비가 6은<br /><br /> ODBC는 항상 FLOAT 열에 대 한 8을 반환합니다.<br /><br /> 예를 들어 과학적 표기법으로 FLOAT 열 실행할 수도 있습니다.<br /><br /> -3.04E + 2는 너비 8 Float<br /><br /> 25E4은 Float 너비 4<br /><br /> **참고** 열에 10 진수 및 과학 표기법을 혼합할 수 없습니다.<br /><br /> NULL 값은 고정 길이 파일에 빈 채워진된 문자열으로 나타내고 구분 기호로 분리 된 파일에서 생략 됩니다.<br /><br /> 부동 소수점 수 데이터 앞에 공백을 채워집니다 될 수 있습니다.|  
|INTEGER|정수 열에 유효한 값은-32766 32767까지 범위의 합니다.<br /><br /> Schema.ini, 너비 다음과 같이 표시 됩니다.<br /><br /> 14083은 정수 너비 5<br /><br /> 0은 정수 너비 1<br /><br /> ODBC는 항상 정수 열에 대해 4를 반환합니다.<br /><br /> 최대 너비는 로그인이 포함 됩니다. 너비는 고정 형식 테이블에서 허용 하는 공백을 인해 클 수 있지만의 정수 열 최대 너비는 11입니다.|  
|LONGCHAR|이론상 제한 중 하나에 있는 LONGCHAR 열의 너비에 고정 길이 또는 구분 기호로 분리 된 테이블은 65500 K. 텍스트 ISAM는 32k 약까지 신뢰할 수 있는 지원을 제공 하기 위해 가능성이 높습니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 확인할 수 있습니다 [데이터 형식 제한](../../odbc/microsoft/data-type-limitations.md)합니다.
