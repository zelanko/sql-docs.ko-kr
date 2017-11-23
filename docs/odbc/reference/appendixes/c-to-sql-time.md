---
title: "C에서 SQL로: 시간 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b2bdc4c764afc7574fe5898bdf9e356b25d2954b
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="c-to-sql-time"></a>C에서 SQL로: 시간
다음은 시간 ODBC C 데이터 형식에 대 한 식별자가입니다.  
  
 SQL_C_TYPE_TIME  
  
 다음 표에서 ODBC SQL 데이터 형식 시간 C 데이터 변환할 수를 보여 줍니다. 참조에 대 한 열과 테이블의 용어 설명은 [C에서 SQL 데이터 형식으로 변환 데이터](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)합니다.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열의 바이트 길이 > = 8<br /><br /> 열 길이 < 8 바이트<br /><br /> 데이터 값이 유효한 시간|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열의 문자 길이 > = 8<br /><br /> 열 길이 < 8 문자<br /><br /> 데이터 값이 유효한 시간|n/a<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|데이터 값이 유효한 시간<br /><br /> 데이터 값이 유효한 시간|n/a<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|데이터 값은 올바른 시간이 [a]<br /><br /> 데이터 값이 유효한 시간|n/a<br /><br /> 22007|  
  
 [a] 날짜 타임 스탬프에 현재 날짜 및 소수 자릿수 초가 0으로 설정 되어 타임 스탬프의 부분으로 설정 됩니다.  
  
 SQL_C_TYPE_TIME 구조에서 유효한 값에 대 한 정보를 참조 하십시오. [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md)이 부록 앞부분에 나오는 합니다.  
  
 결과 문자 데이터에는 C 시간 데이터를 문자 SQL 변환 되 면는 "*hh*:*mm*:*ss*" 형식입니다.  
  
 드라이버에서 C 데이터 형식과 데이터 버퍼의 크기는 C 시간 데이터 형식의 크기 있다고 가정 하는 시간 데이터를 변환할 때 길이/표시기 값을 무시 합니다. 에 길이/표시기 값이 전달 되는 *StrLen_or_Ind* 인수 **SQLPutData** 및 지정 된 버퍼는 *StrLen_or_IndPtr* 인수**SQLBindParameter**합니다. 지정 된 데이터 버퍼는 *DataPtr* 인수에 **SQLPutData** 및 *ParameterValuePtr* 인수에 **SQLBindParameter**.
