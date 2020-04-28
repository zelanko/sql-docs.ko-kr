---
title: 'C에서 SQL로: Bit | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a96982573d83cf01947f82dc2014ee2c470931e3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81292046"
---
# <a name="c-to-sql-bit"></a>C에서 SQL로: 비트
ODBC C 데이터 형식의 비트 식별자는 다음과 같습니다.  
  
 SQL_C_BIT  
  
 다음 표에서는 비트 C 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR<br /><br /> SQL_WCHAR SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|없음|해당 없음|  
|SQL_DECIMAL SQL_NUMERIC<br /><br /> SQL_TINYINT SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT<br /><br /> SQL_REAL SQL_FLOAT<br /><br /> SQL_DOUBLE|없음|해당 없음|  
|SQL_BIT|없음|해당 없음|  
  
 비트 C 데이터 형식에서 데이터를 변환할 때 드라이버는 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 비트 C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
