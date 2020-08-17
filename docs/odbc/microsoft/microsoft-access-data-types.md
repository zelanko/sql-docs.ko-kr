---
description: Microsoft Access 데이터 형식
title: Microsoft Access 데이터 형식 | Microsoft Docs
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
ms.openlocfilehash: 24428c436e9e60c8ca5e42288b217f2c576cbd0d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88340769"
---
# <a name="microsoft-access-data-types"></a>Microsoft Access 데이터 형식
다음 표에서는 Microsoft Access 데이터 형식, 테이블을 만드는 데 사용 되는 데이터 형식 및 ODBC SQL 데이터 형식을 보여 줍니다.  
  
|Microsoft Access 데이터 형식|데이터 형식 (CREATETABLE)|ODBC SQL 데이터 형식|  
|--------------------------------|-------------------------------|------------------------|  
|이상 이진 [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|COUNTER|COUNTER|SQL_INTEGER|  
|CURRENCY|통화|SQL_NUMERIC|  
|날짜/시간|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|긴 이진|LONGBINARY|SQL_LONGVARBINARY|  
|긴 텍스트|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|MEMO|LONGTEXT|SQL_LONGVARCHAR [2] SQL_WLONGVARCHAR [3]|  
|숫자 (FieldSize = SINGLE)|단|SQL_REAL|  
|NUMBER (FieldSize = DOUBLE)|DOUBLE|SQL_DOUBLE|  
|NUMBER (FieldSize = BYTE)|부호 없는 바이트|SQL_TINYINT|  
|NUMBER (FieldSize = INTEGER)|SHORT|SQL_SMALLINT|  
|NUMBER (FieldSize = LONG 정수)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR [1] SQL_WVARCHAR [2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] 4.0 응용 프로그램에만 액세스 합니다. 최대 길이는 4000 바이트입니다. LONGBINARY와 유사한 동작입니다.  
  
 [2] ANSI 응용 프로그램에만 해당 합니다.  
  
 [3] 유니코드 및 액세스 4.0 응용 프로그램에만 해당 합니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC 데이터 형식을 반환 합니다. 두 개 이상의 Microsoft Access 형식이 동일한 ODBC SQL 데이터 형식에 매핑되는 경우에는 모든 Microsoft Access 데이터 형식이 반환 되지 않습니다. *ODBC 프로그래머 참조* 의 부록 D에 있는 모든 변환은 이전 표에 나와 있는 SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서는 Microsoft Access 데이터 형식에 대 한 제한 사항을 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY 및 VARCHAR|0 또는 지정 되지 않은 길이의 BINARY, VARBINARY 또는 VARCHAR 열을 만들면 실제로 510 바이트 열이 반환 됩니다.|  
|BYTE|FieldSize가 BYTE 인 Microsoft Access NUMBER 필드에는 부호가 없지만 Microsoft Access driver를 사용할 때 필드에 음수를 삽입할 수 있습니다.|  
|CHAR,가 나 VARCHAR 및 VARCHAR|문자열 리터럴은 ANSI 문자 (1-255 10 진수)를 포함할 수 있습니다. 작은따옴표 두 개 (' ')를 사용 하 여 하나의 작은따옴표 (')를 나타냅니다.<br /><br /> 문자 데이터 형식 열에서 특수 문자를 사용 하는 경우에는 문자 데이터를 전달 하는 데 프로시저를 사용 해야 합니다.|  
|DATE|날짜 값은 ODBC 정식 날짜 형식에 따라 구분 되거나 datetime 구분 기호 ("#")로 구분 되어야 합니다. 그렇지 않으면 Microsoft Access에서 값을 산술 식으로 처리 하 고 경고 또는 오류를 발생 시 키 지 않습니다.<br /><br /> 예를 들어 "3 월 5 일 1996" 날짜는 {d ' 1996-03-05 '} 또는 #03/05/1996 #;으로 표시 되어야 합니다. 그렇지 않으면 03/05/1993만 제출 되는 경우 Microsoft Access는이를 3으로 5로 나눈 값을 1996으로 계산 합니다. 이 값은 정수 0으로 반올림 되 고 0 일은 1899-12-31에 매핑되므로 사용 된 날짜입니다.<br /><br /> 파이프 문자 (&#124;)는 따옴표로 묶여 있는 경우에도 날짜 값에 사용할 수 없습니다.|  
|GUID|Microsoft Access 4.0로 제한 된 데이터 형식입니다.|  
|NUMERIC|Microsoft Access 4.0로 제한 된 데이터 형식입니다.|  
  
 데이터 형식에 대 한 더 많은 제한은 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)에서 찾을 수 있습니다.
