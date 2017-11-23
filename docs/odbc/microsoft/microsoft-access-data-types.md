---
title: "Microsoft Access 데이터 형식 | Microsoft Docs"
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
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 48f7a518f02cd37d1f41a539fc70750c834a3a57
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
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
|숫자 (FieldSize = 미혼)|단일|SQL_REAL|  
|숫자 (FieldSize DOUBLE =)|DOUBLE|SQL_DOUBLE|  
|숫자 (FieldSize 바이트 =)|부호 없는 바이트|SQL_TINYINT|  
|숫자 (FieldSize 정수 =)|짧은|SQL_SMALLINT|  
|숫자 (FieldSize 정수 (LONG) =)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|[1] SQL_VARCHAR SQL_WVARCHAR [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 4.0 응용 프로그램에 액세스 합니다. 최대 길이 4000 바이트입니다. LONGBINARY와 유사한 동작입니다.  
  
 [2] ANSI 응용 프로그램만 해당 합니다.  
  
 [3] 유니코드 4.0 및 액세스 응용 프로그램 자동 전용입니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC 데이터 형식을 반환 합니다. 둘 이상의 Microsoft Access 형식을 동일한 ODBC SQL 데이터 형식에 매핑하는 모든 Microsoft Access 데이터 형식을 반환 하지 않습니다. 부록 d의 모든 변환이 *ODBC Programmer's Reference* 앞의 표에 나열 된 SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 Microsoft Access 데이터 형식에 대해 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY 및 VARCHAR|0 BINARY, VARBINARY 또는 VARCHAR 열을 만들 하거나 지정 되지 않은 길이 실제로 510 바이트 열을 반환 합니다.|  
|BYTE|Microsoft Access 번호 필드는 FieldSize 같은 바이트를 서명 되지 않은 경우에 Microsoft Access 드라이버를 사용 하는 경우 음수 필드에 삽입할 수 있습니다.|  
|CHAR, LONGVARCHAR, 및 VARCHAR|문자열 리터럴을 ANSI 문자 (1-255 10 진수)를 포함할 수 있습니다. 하나의 작은따옴표 (')을 나타내기 위해 두 개의 연속 된 작은따옴표가 (")를 사용 합니다.<br /><br /> 프로시저에 문자 데이터 형식 열에서 모든 특수 문자를 사용할 때 문자 데이터를 전달 하는 것 같습니다.|  
|DATE|날짜 값은 ODBC 정식 날짜 형식에 따라 구분 또는 날짜/시간 구분 기호 ("#")으로 구분 해야 합니다. 아니면 Microsoft Access 산술 식으로 값을 처리 하 고 경고 또는 오류 발생 시 키 지 않습니다.<br /><br /> 예를 들어 "1996 년 3 월 5,"으로 표시 해야 하는 날짜 {d ' 1996-03-05'을 (를) 또는 # #03/05/1996; 그렇지 않으면만 03/05/1993 전송 되 면 Microsoft Access가 평가이 1996 나눈 5로 나누면 3으로 합니다. 이 값에서 정수 0으로 반올림 하 고이 사용 되는 날짜는 1899-12-31에 맵 0 일 이후입니다.<br /><br /> 파이프 문자 (&#124;) 뒤에 따옴표를 포함 하는 경우에 날짜 값에 사용할 수 없습니다.|  
|GUID|Microsoft Access 4.0으로 제한 된 데이터 형식입니다.|  
|NUMERIC|Microsoft Access 4.0으로 제한 된 데이터 형식입니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 확인할 수 있습니다 [데이터 형식 제한](../../odbc/microsoft/data-type-limitations.md)합니다.
