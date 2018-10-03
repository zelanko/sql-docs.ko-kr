---
title: Microsoft Access 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 11f45698a5ad8b7fd05052cbb2d23520790c425a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692981"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 데이터 형식
다음 표에서 Microsoft Access 데이터 형식, 테이블을 만드는 데 사용 되는 데이터 형식 및 ODBC SQL 데이터 형식을 보여 줍니다.  
  
|Microsoft Access 데이터 형식|데이터 형식 (CREATETABLE)|ODBC SQL 데이터 형식|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|카운터|카운터|SQL_INTEGER|  
|Currency|Currency|SQL_NUMERIC|  
|날짜/시간|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|긴 이진|LONGBINARY|SQL_LONGVARBINARY|  
|긴 텍스트|LONGTEXT|[2] SQL_LONGVARCHAR SQL_WLONGVARCHAR [3]|  
|메모|LONGTEXT|[2] SQL_LONGVARCHAR SQL_WLONGVARCHAR [3]|  
|수 (FieldSize = 미혼)|단일|SQL_REAL|  
|수 (FieldSize DOUBLE =)|DOUBLE|SQL_DOUBLE|  
|수 (FieldSize 바이트 =)|부호 없는 바이트|SQL_TINYINT|  
|수 (FieldSize = 정수)|짧은|SQL_SMALLINT|  
|수 (FieldSize 정수 (LONG) =)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|[1] SQL_VARCHAR SQL_WVARCHAR [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 4.0 응용 프로그램에 액세스 합니다. 최대 길이 4000 바이트입니다. LONGBINARY 비슷하게 사용 되는 동작입니다.  
  
 [2] ANSI 응용 프로그램만 사용 합니다.  
  
 [3] 유니코드 액세스 4.0 응용 프로그램 에서만입니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC 데이터 형식을 반환 합니다. 둘 이상의 Microsoft Access 형식이 동일한 ODBC SQL 데이터 형식에 매핑되는 모든 Microsoft Access 데이터 형식을 반환 하지 않습니다. 부록 D의 모든 변환 합니다 *ODBC 프로그래머 참조* 이전 표에 나열 된 SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 Microsoft Access 데이터 형식에 대해 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY 및 VARCHAR|0 BINARY, VARBINARY 또는 VARCHAR 열을 만들 지정 되지 않은 길이 실제로 510-바이트 열을 반환 합니다.|  
|BYTE|Microsoft 액세스 번호 필드는 FieldSize 바이트 같음를 사용 하 여 서명 되지 않은 경우에 Microsoft Access 드라이버를 사용 하는 경우 음수 필드에 삽입할 수 있습니다.|  
|CHAR, LONGVARCHAR, 및 VARCHAR|리터럴 문자열을 ANSI 문자 (1-255 10 진수)를 포함할 수 있습니다. 두 개의 연속 된 작은따옴표가 (")를 사용 하 여 하나의 작은따옴표 (')를 나타냅니다.<br /><br /> 프로시저 모든 특수 문자를 사용 하 여 문자 데이터 형식 열의 경우 문자 데이터를 전달 하는 것 같습니다.|  
|DATE|날짜 값은 ODBC 정식 날짜 형식에 따라 구분 되거나 ("#") 날짜/시간 구분 기호로 구분 해야 합니다. 이 고, 그렇지 Microsoft Access 산술 식으로 값은 처리 및 경고 또는 오류를 발생 하지 않습니다.<br /><br /> 예를 들어, "1996 년 3 월 5,"으로 나타나야 합니다 날짜 {d ' 1996-03-05'을 (를) 또는 # #03/05/1996; 이 고, 그렇지 03/05/1993 제출 될 경우 Microsoft Access에서는 평가이 1996로 나눈 값 5로 나누면 3으로 합니다. 이 값이 0으로 정수 반올림 및 제로 데가는 1899-12-31에 맵,이 되므로 사용 되는 날짜입니다.<br /><br /> 파이프 문자 (&#124;) 뒤에 따옴표를 포함 하는 경우에 날짜 값에 사용할 수 없습니다.|  
|GUID|Microsoft Access 4.0으로 제한 하는 데이터 형식입니다.|  
|NUMERIC|Microsoft Access 4.0으로 제한 하는 데이터 형식입니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 찾을 수 있습니다 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)합니다.
