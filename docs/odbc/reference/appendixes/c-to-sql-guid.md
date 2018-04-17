---
title: 'C에서 SQL로: GUID | Microsoft Docs'
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
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb1bea9153a8468358d926c3a357a948d2dca302
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-guid"></a>C에서 SQL로: GUID
다음은 GUID ODBC C 데이터 형식에 대 한 식별자가입니다.  
  
 SQL_C_GUID  
  
 다음 표에서 ODBC SQL 데이터 형식을 GUID C 데이터 변환할 수를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|열의 바이트 길이 > = 36|n/a|  
|SQL_VARCHAR|열의 바이트 길이 < 36|22001|  
|SQL_LONGVARCHAR|데이터 값이 올바른 GUID|22018|  
|SQL_WCHAR|열의 문자 길이 > = 36|n/a|  
|SQL_WVARCHAR|열 길이 < 36 문자|22001|  
|SQL_WLONGVARCHAR|데이터 값이 올바른 GUID|22018|  
|SQL_GUID|[A] 없음|n/a|  
  
 [a] 모든 16 진수 값을 GUID로 유효 합니다.  
  
 드라이버는 GUID C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기 GUID C 데이터 형식 크기 있다고 가정 합니다. 에 길이/표시기 값이 전달 되는 *StrLen_or_Ind* 인수 **SQLPutData** 및 지정 된 버퍼는 *StrLen_or_IndPtr* 인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼는 *DataPtr* 인수에 **SQLPutData** 및 *ParameterValuePtr* 인수에 **SQLBindParameter**.
