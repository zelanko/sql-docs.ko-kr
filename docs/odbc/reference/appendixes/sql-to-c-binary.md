---
title: 'C: 이진 SQL | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf0036043bf25186a89ed3c8cbc5ef7d062f25c6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sql-to-c-binary"></a>C: 이진 SQL
이진 ODBC SQL 데이터 형식에 대 한 식별자는.  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 다음 표에서 ODBC C 데이터 형식에 이진 SQL 데이터를 변환 될 수 있습니다를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [SQL에서 C 데이터 형식 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)합니다.  
  
|C 형식 식별자|테스트|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(데이터의 바이트 길이) \* 2 < *BufferLength*<br /><br /> (데이터의 바이트 길이) \* 2 > = *BufferLength*|Data<br /><br /> 잘린된 데이터|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이|n/a<br /><br /> 01004|  
|SQL_C_WCHAR|(문자 데이터의 길이) \* 2 < *BufferLength*<br /><br /> (문자 데이터의 길이) \* 2 > = *BufferLength*|Data<br /><br /> 잘린된 데이터|문자에서 데이터의 길이<br /><br /> 문자에서 데이터의 길이|n/a<br /><br /> 01004|  
|SQL_C_BINARY|데이터의 바이트 길이 < = *BufferLength*<br /><br /> 데이터의 바이트 길이 > *BufferLength*|Data<br /><br /> 잘린된 데이터|데이터의 바이트 길이<br /><br /> 데이터의 바이트 길이|n/a<br /><br /> 01004|  
  
 이진 SQL 데이터를 C 문자 데이터로 변환 되 면 원본 데이터의 각 바이트 (8 비트)는 두 개의 ASCII 문자로 표시 됩니다. 이러한 문자는 16 진수 형식으로 숫자의 ASCII 문자 표현 합니다. 예를 들어 "01" 이진 00000001은 변환 하 고 이진 11111111 "FF"로 변환 됩니다.  
  
 드라이버는 항상 개별 바이트 16 진수 숫자의 쌍으로 변환 하 고 null 바이트 문자열을 종료 합니다. 이 인해 경우 *BufferLength* 짝수 하 고 변환된 된 데이터의 마지막 바이트의 길이 보다 작으면는 **TargetValuePtr* 버퍼가 사용 되지 않습니다. (변환된 된 데이터 바이트 수는 짝수, 마지막에서 두 번째 바이트를 null 바이트를 걸리며 마지막 바이트를 사용할 수 없습니다.)  
  
> [!NOTE]  
>  응용 프로그램 개발자가 문자 C 데이터 형식으로 이진 SQL 데이터 바인딩 해서는 안 됩니다. 이 변환은 일반적으로 비효율적인 및 느립니다.
