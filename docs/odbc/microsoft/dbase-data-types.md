---
title: dBASE 데이터 유형 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307694"
---
# <a name="dbase-data-types"></a>dBASE 데이터 형식
다음 표에서는 dBASE 데이터 형식이 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 주며 있습니다. 모든 ODBC SQL 데이터 형식이 지원되는 것은 아닙니다.  
  
|dBASE 데이터 형식|ODBC 데이터 형식|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|플로트[1]|SQL_DOUBLE|  
|논리|SQL_BIT|  
|메모|SQL_LONGVARCHAR|  
|숫자 (BCD)|SQL_DOUBLE|  
|올레오브젝트[1]|SQL_LONGBINARY|  
  
 [1] dBASE 버전 5에만 유효합니다. *x*  
  
 dBASE III의 정밀도는 최대 두 자리 지수의 숫자와 최대 3자리 지수의 dBASE IV 숫자를 허용합니다. 숫자는 텍스트로 저장되므로 숫자로 변환됩니다. 변환할 수가 필드에 맞지 않으면 설명할 수 없는 결과가 발생할 수 있습니다.  
  
 dBASE를 사용하면 NUMERIC 데이터 유형으로 정밀도와 배율을 지정할 수 있지만 ODBC dBASE 드라이버에서는 지원되지 않습니다. ODBC dBASE 드라이버는 항상 숫자 데이터 형식에 대해 15의 정밀도와 0의 배율을 반환합니다.  
  
 ODBC dBASE 드라이버를 사용하여 숫자 데이터 유형으로 만든 열은 SQL_DOUBLE ODBC 데이터 형식에 매핑됩니다. 따라서 이 열의 데이터는 반올림될 수 있습니다. 이 동작은 이진 코딩 된 소수점 (BCD)인 dBASE (유형 N)의 NUMERIC 데이터 형식과 동일하지 않습니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환합니다. *ODBC 프로그래머* 참조부록 D의 모든 변환은 이 항목의 앞에 나열된 ODBC SQL 데이터 형식에 대해 지원됩니다.  
  
 다음 표에서는 dBASE 데이터 형식에 대한 제한 사항이 보여 있습니다.  
  
|데이터 형식|설명|  
|---------------|-----------------|  
|CHAR|0 또는 지정되지 않은 길이의 CHAR 열을 만들면 실제로 254바이트 열이 반환됩니다.|  
|암호화된 데이터|dBASE 드라이버는 암호화된 dBASE 테이블을 지원하지 않습니다.|  
|논리|dBASE 드라이버는 논리 열에 인덱스를 만들 수 없습니다.|  
|메모|MEMO 열의 최대 길이는 65,500바이트입니다.|  
  
 데이터 형식에 대한 더 많은 제한 사항은 [데이터 형식 제한에서](../../odbc/microsoft/data-type-limitations.md)찾을 수 있습니다.
