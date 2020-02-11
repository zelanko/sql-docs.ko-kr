---
title: 'C에서 SQL로: 연도-월 간격 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3db8d61bacefa8588db4c0081c6be591d7ffdacf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019279"
---
# <a name="c-to-sql-year-month-intervals"></a>C에서 SQL로: 연-월 간격
년-월 간격 ODBC C 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 다음 표에서는 연도-월 간격 C 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|열 바이트 길이 >= 문자 바이트 길이<br /><br /> 열 바이트 길이 < 문자 바이트 길이 [a]<br /><br /> 데이터 값이 올바른 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|열 문자 길이 >= 데이터의 문자 길이<br /><br /> 열 문자 길이 < 데이터의 문자 길이 [a]<br /><br /> 데이터 값이 올바른 간격 리터럴이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL [b]|단일 필드 간격을 변환 하지 못해 전체 자릿수가 잘렸습니다.<br /><br /> 변환 결과로 전체 자릿수가 잘렸습니다.|해당 없음<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|필드 잘림 없이 데이터 값이 변환 되었습니다.<br /><br /> 변환 하는 동안 하나 이상의 데이터 값 필드가 잘렸습니다.|해당 없음<br /><br /> 22015|  
  
 [a] 모든 C interval 데이터 형식을 문자 데이터 형식으로 변환할 수 있습니다.  
  
 [b] interval 구조의 type 필드가 간격이 단일 필드 (SQL_YEAR 또는 SQL_MONTH) 인 경우 간격 C 유형을 정확한 숫자 (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL 또는 SQL_NUMERIC)로 변환할 수 있습니다.  
  
 간격 C 형식의 기본 변환은 해당 연도-월 간격 SQL 형식입니다.  
  
 이 드라이버는 interval C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 간격 C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
