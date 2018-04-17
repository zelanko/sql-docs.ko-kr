---
title: 'C에서 SQL로: 이진 | Microsoft Docs'
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
ms.topic: article
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 564e23b1ac629d16698640692b32636cdd5aa8e3
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-binary"></a>C에서 SQL로: 이진
다음은 이진 ODBC C 데이터 형식에 대 한 식별자가입니다.  
  
 SQL_C_BINARY  
  
 다음 표에서 ODBC SQL 데이터 형식이 이진 C 데이터 변환할 수를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|데이터의 바이트 길이 < = 바이트 길이 열<br /><br /> 데이터의 바이트 길이 > 열의 바이트 길이|n/a<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|문자 데이터의 길이 < = 열 문자 길이<br /><br /> 문자 데이터의 길이 > 열 문자 길이|n/a<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|데이터의 바이트 길이 = SQL 데이터 길이<br /><br /> <> SQL 데이터 길이 데이터의 바이트 길이|n/a<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|데이터의 길이 < = 열 길이<br /><br /> 데이터의 길이 > 열 길이|n/a<br /><br /> 22001|
