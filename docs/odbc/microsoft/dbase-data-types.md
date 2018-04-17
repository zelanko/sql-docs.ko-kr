---
title: 데이터 형식 dBASE | Microsoft Docs
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
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2793b2aea4b783f2fa27fc8248866b18e44a945e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="dbase-data-types"></a>dBASE 데이터 형식
다음 표에서 dBASE 데이터 형식을 ODBC SQL 데이터 형식에 매핑되는 방법을 보여 줍니다. Note 일부 ODBC SQL 데이터 형식이 지원 됩니다.  
  
|dBASE 데이터 형식|ODBC 데이터 형식|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT [1]|SQL_DOUBLE|  
|논리|SQL_BIT|  
|메모|SQL_LONGVARCHAR|  
|숫자 BCD)|SQL_DOUBLE|  
|OLEOBJECT [1]|SQL_LONGBINARY|  
  
 DBASE 버전 5에 대 한 유효 기간 [1]입니다. *x*  
  
 DBASE에 전체 자릿수를 III 허용를 가진 숫자를 포함 하는 숫자 dBASE IV 및 두 자리 지 수를 최대 3 자리 지수가 합니다. 숫자는 텍스트로 저장 되므로, 숫자로 변환 됩니다. 변환할 숫자가 포함 되지 않는 경우 필드에 설명할 수 없는 결과가 발생할 수 있습니다.  
  
 DBASE는 정밀도 배율이 숫자 데이터 형식으로 지정을 허용 하는 동안 dBASE ODBC 드라이버에서 지원 되지 않습니다. DBASE ODBC 드라이버는 항상 15의 전체 자릿수 및 소수 자릿수가 0 숫자 데이터 형식에 대 한 반환합니다.  
  
 ODBC SQL_DOUBLE 데이터 형식으로 ODBC dBASE 드라이버 지도 사용 하 여 숫자 데이터 형식을 사용 하 여 만든 열입니다. 따라서이 열에 데이터 반올림 될 수 있습니다. 이 동작은 Binary Coded Decimal (BCD)은 dBASE (N 형식)에 입력 하는 숫자 데이터의 동일 않습니다.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** ODBC SQL 데이터 형식을 반환 합니다. 부록 d의 모든 변환이 *ODBC Programmer's Reference* 이 항목의 앞부분에 나열 된 ODBC SQL 데이터 형식에 대해 지원 됩니다.  
  
 다음 표에서 데이터 형식으로 하 dBASE에 한계를 보여 줍니다.  
  
|데이터 형식|Description|  
|---------------|-----------------|  
|CHAR|0 CHAR 열을 만들 하거나 지정 되지 않은 길이 254 바이트 열을 실제로 반환 합니다.|  
|암호화된 데이터|DBASE 드라이버는 암호화 된 dBASE 테이블을 지원 하지 않습니다.|  
|논리|DBASE 드라이버 논리 열에 인덱스를 만들 수 없습니다.|  
|메모|메모 열의 최대 길이 65, 500 바이트입니다.|  
  
 데이터 형식에 대 한 자세한 제한에서 확인할 수 있습니다 [데이터 형식 제한](../../odbc/microsoft/data-type-limitations.md)합니다.
