---
title: 'C에서 SQL로: GUID | 마이크로 소프트 문서'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3b559499273e885e23da10d9093a0ce9ff92393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306624"
---
# <a name="c-to-sql-guid"></a>C에서 SQL로: GUID
GUID ODBC C 데이터 형식의 식별자는 다음과 입니다.  
  
 SQL_C_GUID  
  
 다음 표에서는 GUID C 데이터를 변환할 수 있는 ODBC SQL 데이터 형식을 보여 주실 수 있습니다. 표의 열 및 용어에 대한 설명은 [C에서 SQL 데이터 유형으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조하십시오.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|열 바이트 길이 >= 36|해당 없음|  
|SQL_VARCHAR|열 바이트 길이 < 36|22001|  
|SQL_LONGVARCHAR|데이터 값이 유효한 GUID가 아닙니다.|22018|  
|SQL_WCHAR|열 문자 길이 >= 36|해당 없음|  
|SQL_WVARCHAR|열 문자 길이 < 36|22001|  
|SQL_WLONGVARCHAR|데이터 값이 유효한 GUID가 아닙니다.|22018|  
|SQL_GUID|없음[a]|해당 없음|  
  
 [a] 모든 고유값은 GUID로 유효합니다.  
  
 드라이버는 GUID C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시하고 데이터 버퍼의 크기가 GUID C 데이터 형식의 크기라고 가정합니다. 길이/표시기 값은 **SQLPutData의** *StrLen_or_Ind* 인수와 **SQLBindParameter**에서 *StrLen_or_IndPtr* 인수로 지정된 버퍼에서 전달됩니다. 데이터 버퍼는 **SQLPutData의** *DataPtr* 인수와 **SQLBind매개**변수 매개 변수의 *매개 변수 값 Ptr* 인수로 지정됩니다.
