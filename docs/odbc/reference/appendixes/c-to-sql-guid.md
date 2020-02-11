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
ms.openlocfilehash: 5863935ddf595409d48be79dc646c0994ddeb0b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019317"
---
# <a name="c-to-sql-guid"></a>C에서 SQL로: GUID
GUID ODBC C 데이터 형식에 대 한 식별자는 다음과 같습니다.  
  
 SQL_C_GUID  
  
 다음 표에서는 GUID C 데이터가 변환 될 수 있는 ODBC SQL 데이터 형식을 보여 줍니다. 테이블의 열 및 용어에 대 한 설명은 [C에서 SQL 데이터 형식으로 데이터 변환](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)을 참조 하세요.  
  
|SQL 유형 식별자|테스트|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|열 바이트 길이 >= 36|해당 없음|  
|SQL_VARCHAR|열 바이트 길이 < 36|22001|  
|SQL_LONGVARCHAR|데이터 값이 올바른 GUID가 아닙니다.|22018|  
|SQL_WCHAR|열 문자 길이 >= 36|해당 없음|  
|SQL_WVARCHAR|열 문자 길이 < 36|22001|  
|SQL_WLONGVARCHAR|데이터 값이 올바른 GUID가 아닙니다.|22018|  
|SQL_GUID|없음 [a]|해당 없음|  
  
 [a] 모든 16 진수 값은 GUID로 유효 합니다.  
  
 GUID C 데이터 형식에서 데이터를 변환할 때 드라이버는 길이/표시기 값을 무시 하 고 데이터 버퍼의 크기가 GUID C 데이터 형식의 크기인 것으로 가정 합니다. 길이/표시기 값은 **Sqlputdata** 의 *StrLen_or_Ind* 인수와 **SQLBindParameter**의 *StrLen_or_IndPtr* 인수를 사용 하 여 지정 된 버퍼에 전달 됩니다. 데이터 버퍼는 **Sqlputdata** 의 *Dataptr* 인수와 **SQLBindParameter**의 *parametervalueptr* 인수를 사용 하 여 지정 됩니다.
