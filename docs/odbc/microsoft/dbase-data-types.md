---
title: dBASE 데이터 형식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17b96ad0b6674a2d120ef46d9bfa221e8df6d140
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307694"
---
# <a name="dbase-data-types"></a>dBASE 데이터 형식
다음 표에서는 dBASE 데이터 형식이 ODBC SQL 데이터 형식으로 매핑되는 방법을 보여 줍니다. 모든 ODBC SQL 데이터 형식이 지원 되는 것은 아닙니다.  
  
|dBASE 데이터 형식|ODBC 데이터 형식|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|논리곱|SQL_BIT|  
|MEMO|SQL_LONGVARCHAR|  
|NUMERIC (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] dBASE 버전 5에 대해서만 유효 합니다. *x*  
  
 DBASE III의 전체 자릿수는 최대 3 자리 지수가 있는 dBASE IV 숫자와 최대 두 자리 지 수를 포함 하는 숫자를 허용 합니다. 숫자는 텍스트로 저장 되므로 숫자로 변환 됩니다. 변환할 숫자가 필드에 맞지 않는 경우 설명할 수 없는 결과가 발생할 수 있습니다.  
  
 DBASE는 전체 자릿수와 소수 자릿수를 숫자 데이터 형식으로 지정할 수 있지만 ODBC dBASE 드라이버에서는 지원 되지 않습니다. ODBC dBASE 드라이버는 숫자 데이터 형식에 대해 항상 정밀도 15와 소수 자릿수 0을 반환 합니다.  
  
 ODBC dBASE 드라이버를 사용 하 여 숫자 데이터 형식을 사용 하 여 만든 열은 SQL_DOUBLE ODBC 데이터 형식에 매핑됩니다. 따라서이 열의 데이터는 반올림 될 수 있습니다. 이 동작은 blob (Binary 코딩 된 10 진수) 인 dBASE (type N)의 숫자 데이터 형식과 다릅니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** 는 ODBC SQL 데이터 형식을 반환 합니다. *Odbc 프로그래머 참조* 의 부록 D에 있는 모든 변환은이 항목의 앞부분에 나열 된 odbc SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서는 dBASE 데이터 형식에 대 한 제한 사항을 보여 줍니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|CHAR|0 또는 지정 되지 않은 길이의 CHAR 열을 만들면 실제로 254 바이트 열이 반환 됩니다.|  
|암호화된 데이터|DBASE 드라이버는 암호화 된 dBASE 테이블을 지원 하지 않습니다.|  
|논리곱|DBASE 드라이버는 논리적 열에 인덱스를 만들 수 없습니다.|  
|MEMO|메모 열의 최대 길이는 65500 바이트입니다.|  
  
 데이터 형식에 대 한 더 많은 제한은 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)에서 찾을 수 있습니다.
