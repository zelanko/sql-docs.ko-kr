---
title: 'C에서 SQL로: 비트 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], bit
- bit data type [ODBC]
- data conversions from C to SQL types [ODBC], bit
ms.assetid: 267c9fa9-599e-4ee6-b51b-0cae43f09183
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9eeeaeaa3bb4af7a244697e992e79e8c66c2a660
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47709711"
---
# <a name="c-to-sql-bit"></a>C에서 SQL로: 비트
비트 ODBC C 데이터 형식에 대 한 식별자가 있습니다.  
  
 SQL_C_BIT  
  
 다음 표에서 ODBC SQL 데이터 형식 bit C 데이터 변환 될 수 있습니다는 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)입니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHAR SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|없음|n/a|  
|SQL_DECIMAL SQL_NUMERIC<br /><br /> SQL_TINYINT SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT<br /><br /> SQL_REAL SQL_FLOAT<br /><br /> SQL_DOUBLE|없음|n/a|  
|SQL_BIT|없음|n/a|  
  
 드라이버 비트 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기를 비트 C 데이터 형식의 크기 있다고 가정 합니다. 길이/표시기 값이 전달 합니다 *StrLen_or_Ind* 인수에 **SQLPutData** 에 지정 된 버퍼는 *StrLen_or_IndPtr* 에서인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼를 *DataPtr* 에서 인수 **SQLPutData** 및 *ParameterValuePtr* 인수에서 **SQLBindParameter**.
