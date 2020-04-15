---
title: 'C에서 SQL로: 바이너리 | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 818de0086ce3996cc1f6194311d2a2bb80c9f564
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292119"
---
# <a name="c-to-sql-binary"></a>C에서 SQL로: 이진
이진 ODBC C 데이터 형식의 식별자는 다음과 입니다.  
  
 SQL_C_BINARY  
  
 다음 표에서는 이진 C 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주며 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|데이터 <바이트 길이 = 열 바이트 길이<br /><br /> 데이터 > 열 바이트 길이의 바이트 길이|해당 없음<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|데이터의 문자 길이 <= 열 문자 길이<br /><br /> 데이터의 문자 길이 > 열 문자 길이|해당 없음<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|바이트 데이터 길이 = SQL 데이터 길이<br /><br /> SQL 데이터 길이를 <> 데이터 바이트 길이|해당 없음<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|데이터 <길이 = 열 길이<br /><br /> 데이터 > 열 길이|해당 없음<br /><br /> 22001|
