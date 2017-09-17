---
title: "C에서 SQL로: 비트 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8e7232773b97a66fc0b1b047e3fb8cc4212754f0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-bit"></a>C에서 SQL로: 비트
다음은 비트 ODBC C 데이터 형식에 대 한 식별자가입니다.  
  
 SQL_C_BIT  
  
 다음 표에서 ODBC SQL 데이터 형식에 비트 C 데이터를 변환 될 수 있습니다를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHAR SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|없음|n/a|  
|SQL_DECIMAL SQL_NUMERIC<br /><br /> SQL_TINYINT SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT<br /><br /> SQL_REAL SQL_FLOAT<br /><br /> SQL_DOUBLE|없음|n/a|  
|SQL_BIT|없음|n/a|  
  
 드라이버 비트 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기는 C bit 데이터 형식 크기 있다고 가정 합니다. 에 길이/표시기 값이 전달 되는 *StrLen_or_Ind* 인수 **SQLPutData** 및 지정 된 버퍼는 *StrLen_or_IndPtr* 인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼는 *DataPtr* 인수에 **SQLPutData** 및 *ParameterValuePtr* 인수에 **SQLBindParameter**.
