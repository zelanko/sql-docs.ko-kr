---
title: 'C에서 SQL로: GUID | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: af0ed8307652ccf45e7fbfffb6c00355c8a8b004
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63159357"
---
# <a name="c-to-sql-guid"></a>C에서 SQL로: GUID
GUID ODBC C 데이터 형식에 대 한 식별자가 있습니다.  
  
 SQL_C_GUID  
  
 다음 표에서 ODBC SQL 데이터 형식에는 GUID C 데이터를 변환 될 수 있습니다를 보여 줍니다. 열과 테이블의 용어 설명은 참조 하세요 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)입니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|열의 바이트 길이 > = 36|n/a|  
|SQL_VARCHAR|열 길이 < 36 바이트|22001|  
|SQL_LONGVARCHAR|데이터 값이 유효한 GUID|22018|  
|SQL_WCHAR|열의 문자 길이 > = 36|n/a|  
|SQL_WVARCHAR|열 길이 < 36 문자|22001|  
|SQL_WLONGVARCHAR|데이터 값이 유효한 GUID|22018|  
|SQL_GUID|[A] 없음|n/a|  
  
 [a] 모든 16 진수 값을 GUID로 유효 합니다.  
  
 드라이버는 GUID C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 GUID C 데이터 형식의 크기를 가정 합니다. 길이/표시기 값이 전달 합니다 *StrLen_or_Ind* 인수에 **SQLPutData** 에 지정 된 버퍼는 *StrLen_or_IndPtr* 에서인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼를 *DataPtr* 에서 인수 **SQLPutData** 및 *ParameterValuePtr* 인수에서 **SQLBindParameter**.
