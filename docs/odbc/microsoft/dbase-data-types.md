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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc4b4c7a5c1074a62bf0e84d265840109f65ea55
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63126316"
---
# <a name="dbase-data-types"></a>dBASE 데이터 형식
다음 표에서 dBASE 데이터 형식을 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 줍니다. Note 일부 ODBC SQL 데이터 형식이 지원 됩니다.  
  
|dBASE 데이터 형식|ODBC 데이터 형식|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT[1]|SQL_DOUBLE|  
|논리|SQL_BIT|  
|메모|SQL_LONGVARCHAR|  
|숫자 (BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 DBASE 버전 5에만 유효 [1]입니다. *x*  
  
 DBASE에 전체 자릿수를 III에서는 숫자를 두 자리 지 수를 사용 하 여 dBASE IV 숫자에서 최대 3 자리 지수가 합니다. 숫자는 텍스트로 저장 되므로, 숫자로 변환 됩니다. 변환할 숫자 필드에 맞지 않으면를 설명할 수 없는 결과가 발생할 수 있습니다.  
  
 DBASE 정밀도 및 배율을 숫자 데이터 형식으로 지정을 허용 하는 동안 ODBC dBASE 드라이버에서 지원 되지 않습니다. ODBC dBASE 드라이버에는 항상 15 자릿수, 소수 자릿수 숫자 데이터 형식에 대 한 0 반환합니다.  
  
 ODBC SQL_DOUBLE 데이터 형식을 ODBC dBASE 드라이버 맵을 사용 하 여 숫자 데이터 형식으로 만들어진 열입니다. 따라서이 열의 데이터를에서 반올림 될 수 있습니다. 이 동작은 숫자 데이터의 형식로 dBASE (N 형식), Binary Coded Decimal (BCD)는 동일한 아닙니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환 합니다. 부록 D의 모든 변환 합니다 *ODBC 프로그래머 참조* 이 항목의 앞부분에 나열 된 ODBC SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 데이터 형식으로 하 dBASE에 한계를 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|CHAR|0 CHAR 열을 만들 지정 되지 않은 길이 254 바이트 열을 실제로 반환 합니다.|  
|암호화된 데이터|DBASE 드라이버는 암호화 된 dBASE 테이블을 지원 하지 않습니다.|  
|논리|DBASE 드라이버 논리 열에 인덱스를 만들 수 없습니다.|  
|메모|메모 열의 최대 길이 65,500 바이트입니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 찾을 수 있습니다 [데이터 형식 제한 사항](../../odbc/microsoft/data-type-limitations.md)합니다.
