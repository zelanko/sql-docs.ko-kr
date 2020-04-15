---
title: 마이크로소프트 액세스 데이터 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fb65b6fdc81ae0a8e007d1cee150c6a35b91c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307732"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 데이터 형식
다음 표에서는 Microsoft Access 데이터 형식, 테이블을 만드는 데 사용되는 데이터 형식 및 ODBC SQL 데이터 형식을 보여 주며 있습니다.  
  
|마이크로소프트 액세스 데이터 형식|데이터 유형(CREATETABLE)|ODBC SQL 데이터 유형|  
|--------------------------------|-------------------------------|------------------------|  
|빅바이너리[1]|롱 바이너리|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|카운터|카운터|SQL_INTEGER|  
|Currency|Currency|SQL_NUMERIC|  
|날짜/시간|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|긴 바이너리|롱 바이너리|SQL_LONGVARBINARY|  
|긴 텍스트|긴 텍스트|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|메모|긴 텍스트|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|번호(필드크기= 단일)|단일|SQL_REAL|  
|번호(필드크기= 두 배)|DOUBLE|SQL_DOUBLE|  
|번호(필드크기= 바이트)|서명되지 않은 바이트|SQL_TINYINT|  
|번호(필드크기= 정수)|SHORT|SQL_SMALLINT|  
|번호(필드크기= 긴 정수)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|롱 바이너리|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 액세스 4.0 응용 프로그램만. 최대 길이 4,000바이트. LONGBINARY와 유사한 동작입니다.  
  
 [2] ANSI 응용 프로그램만.  
  
 [3] 유니코드 및 액세스 4.0 응용 프로그램만.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC 데이터 형식을 반환합니다. 두 개 이상의 Microsoft 액세스 형식이 동일한 ODBC SQL 데이터 형식에 매핑된 경우 모든 Microsoft Access 데이터 형식을 반환하지 는 않습니다. *ODBC 프로그래머* 참조부록 D의 모든 변환은 이전 표에 나열된 SQL 데이터 형식에 대해 지원됩니다.  
  
 다음 표에서는 Microsoft Access 데이터 형식에 대한 제한 사항이 보여 있습니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|바이너리, 바바이너리, 바르차|0 또는 지정되지 않은 길이의 이진, VARBINARY 또는 VARCHAR 열을 만들면 실제로 510바이트 열이 반환됩니다.|  
|BYTE|BYTE와 동일한 FieldSize가 있는 Microsoft 액세스 번호 필드는 서명되지 않았지만 Microsoft Access 드라이버를 사용할 때 필드에 음수를 삽입할 수 있습니다.|  
|차, 롱바르차, 바르차르|문자 문자열 리터럴은 ANSI 문자(소수점 1-255)를 포함할 수 있습니다. 두 개의 연속된 단일 따옴표('')를 사용하여 하나의 따옴표(')를 나타냅니다.<br /><br /> 프로시저는 문자 데이터 형식 열에서 특수 문자를 사용할 때 문자 데이터를 전달하는 데 사용해야 합니다.|  
|DATE|날짜 값은 ODBC 표준 날짜 형식에 따라 구분되거나 날짜 시간 구분 기호("#")에 의해 구분되어야 합니다. 그렇지 않으면 Microsoft Access는 값을 산술 식으로 처리하고 경고 또는 오류를 발생시키지 않습니다.<br /><br /> 예를 들어 날짜 "1996년 3월 5일"은 {d '1996-03-05'} 또는 #03/05/1996#로 표시되어야 합니다. 그렇지 않으면 1993년 03/05만 제출하면 Microsoft Access에서 이를 3을 5로 1996으로 나눈 값으로 평가합니다. 이 값은 정수 0으로 반올림되며 0일 맵이 1899-12-31로 매핑되므로 이 값이 사용된 날짜입니다.<br /><br /> 파이프 문자(&#124;)는 백 따옴표로 둘러싸인 경우에도 날짜 값으로 사용할 수 없습니다.|  
|GUID|데이터 형식은 Microsoft 액세스 4.0으로 제한됩니다.|  
|NUMERIC|데이터 형식은 Microsoft 액세스 4.0으로 제한됩니다.|  
  
 데이터 형식에 대한 더 많은 제한 사항은 [데이터 형식 제한에서](../../odbc/microsoft/data-type-limitations.md)찾을 수 있습니다.
