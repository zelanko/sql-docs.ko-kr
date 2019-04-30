---
title: 'SQL에서 C로: 이진 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 16112ca3b66e0218efd54d3bf385e04cb654e3e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270956"
---
# <a name="sql-to-c-binary"></a>SQL에서 C로: 이진
이진 ODBC SQL 데이터 형식에 대 한 식별자 다음과 같습니다.  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 다음 표에서 ODBC C 데이터 형식에는 이진 SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [SQL에서 C 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)입니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(데이터의 바이트 길이) \* 2 < *BufferLength*<br /><br /> (데이터의 바이트 길이) \* 2 > = *BufferLength*|data<br /><br /> 잘린된 데이터|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|(데이터의 문자 길이) \* 2 < *BufferLength*<br /><br /> (데이터의 문자 길이) \* 2 > = *BufferLength*|data<br /><br /> 잘린된 데이터|문자에서 데이터의 길이<br /><br /> 문자에서 데이터의 길이|n/a<br /><br /> 01004|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|data<br /><br /> 잘린된 데이터|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이|n/a<br /><br /> 01004|  
  
 이진 SQL 데이터 C 문자 데이터를 변환할 때 원본 데이터의 각 바이트 (8 비트)를 두 개의 ASCII 문자로 표시 됩니다. 이러한 문자는 ASCII 문자 표시의 해당 16 진수입니다. 예를 들어 이진 00000001 "01"로 변환 됩니다 및 이진 11111111 "FF"로 변환 됩니다.  
  
 드라이버는 항상 개별 바이트 16 진수 숫자의 쌍을 변환 하 고 null 바이트를 사용 하 여 문자열을 종료 합니다. 이 인해 경우 *BufferLength* 도 이며의 마지막 바이트가 변환 된 데이터의 길이 보다 작으면는 **TargetValuePtr* 버퍼가 사용 되지 않습니다. (변환 된 데이터 바이트 수는 짝수 필요 다음 마지막 바이트를 null 바이트 이며 마지막 바이트를 사용할 수 없습니다.)  
  
> [!NOTE]  
>  응용 프로그램 개발자는 문자 C 데이터 형식으로 이진 SQL 데이터 바인딩 것이 좋습니다. 이 변환은 비효율적 이며 느린는 일반적으로 합니다.
