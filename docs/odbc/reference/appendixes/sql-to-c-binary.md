---
title: 'SQL에서 C까지: 바이너리 | 마이크로 소프트 문서'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b0ce72f650e61b83ec99b0727752612d18da52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298829"
---
# <a name="sql-to-c-binary"></a>SQL에서 C로: 이진
이진 ODBC SQL 데이터 형식의 식별자는 다음과 같습니다.  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 다음 표에서는 이진 SQL 데이터를 변환할 수 있는 ODBC C 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [SQL에서 C 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)을 참조하십시오.  
  
|C 유형 식별자|테스트|**대상 밸류프트*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(데이터 바이트 길이) \* 2 < *버퍼길이*<br /><br /> (데이터 바이트 길이) \* 2 >= *버퍼길이*|데이터<br /><br /> 잘린 데이터|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이|해당 없음<br /><br /> 01004|  
|SQL_C_WCHAR|(데이터의 문자 길이) \* 2 < *버퍼길이*<br /><br /> (데이터의 문자 길이) \* 2 >= *버퍼길이*|데이터<br /><br /> 잘린 데이터|문자로 된 데이터 길이<br /><br /> 문자로 된 데이터 길이|해당 없음<br /><br /> 01004|  
|SQL_C_BINARY|데이터 <바이트 길이 = *버퍼길이*<br /><br /> *버퍼길이>* 데이터의 바이트 길이|데이터<br /><br /> 잘린 데이터|바이트 내 데이터 길이<br /><br /> 바이트 내 데이터 길이|해당 없음<br /><br /> 01004|  
  
 이진 SQL 데이터가 문자 C 데이터로 변환되면 원본 데이터의 각 바이트(8비트)가 두 개의 ASCII 문자로 표시됩니다. 이러한 문자는 육각형 형식의 숫자의 ASCII 문자 표현입니다. 예를 들어 이진 00000001은 "01"으로 변환되고 이진 111111111은 "FF"로 변환됩니다.  
  
 드라이버는 항상 개별 바이트를 헥사데피말 자릿수 쌍으로 변환하고 null 바이트로 문자 문자열을 종료합니다. 따라서 *BufferLength가* 짝수이고 변환된 데이터의 길이보다 적으면 **TargetValuePtr* 버퍼의 마지막 바이트가 사용되지 않습니다. 변환된 데이터에는 짝수 바이트가 필요하고, 다음-마지막 바이트는 null 바이트이고 마지막 바이트는 사용할 수 없습니다.  
  
> [!NOTE]  
>  응용 프로그램 개발자는 이진 SQL 데이터를 문자 C 데이터 형식에 바인딩하지 않는 것이 좋습니다. 이 변환은 일반적으로 비효율적이고 느립니다.
