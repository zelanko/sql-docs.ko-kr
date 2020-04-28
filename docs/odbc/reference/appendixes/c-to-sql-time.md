---
title: 'C에서 SQL로: 시간 | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 264ce7751072b79163923f0c141542680f7b02bb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304766"
---
# <a name="c-to-sql-time"></a>C에서 SQL로: 시간
ODBC C 데이터 형식의 시간에 대 한 식별자는 다음과 같습니다.  
  
 SQL_C_TYPE_TIME  
  
 다음 표에서는 C 데이터를 변환 하는 데 사용할 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|열 바이트 길이 >= 8<br /><br /> 열 바이트 길이 < 8<br /><br /> 데이터 값이 올바른 시간이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|열 문자 길이 >= 8<br /><br /> 열 문자 길이 < 8<br /><br /> 데이터 값이 올바른 시간이 아닙니다.|해당 없음<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|데이터 값이 유효한 시간입니다.<br /><br /> 데이터 값이 올바른 시간이 아닙니다.|해당 없음<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|데이터 값이 유효한 시간 [a]입니다.<br /><br /> 데이터 값이 올바른 시간이 아닙니다.|해당 없음<br /><br /> 22007|  
  
 [a] 타임 스탬프의 날짜 부분이 현재 날짜로 설정 되 고 타임 스탬프의 초 소수 부분이 0으로 설정 됩니다.  
  
 SQL_C_TYPE_TIME 구조에서 유효한 값에 대 한 자세한 내용은이 부록 앞부분의 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md)을 참조 하세요.  
  
 시간 C 데이터가 문자 SQL 데이터로 변환 되는 경우 결과 문자 데이터는 "*hh*:*mm*:*ss*" 형식입니다.  
  
 이 드라이버는 시간 C 데이터 형식에서 데이터를 변환할 때 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 시간 C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
