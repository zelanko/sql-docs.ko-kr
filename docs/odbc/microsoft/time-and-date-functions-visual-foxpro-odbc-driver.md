---
description: 날짜 및 시간 함수(Visual FoxPro ODBC 드라이버)
title: 시간 및 날짜 함수 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d537411481a8bc6c9065e8e86c216c8c0637e565
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500076"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>날짜 및 시간 함수(Visual FoxPro ODBC 드라이버)
다음 표에서는 Visual FoxPro ODBC 드라이버에서 지 원하는 ODBC 시간 및 날짜 함수를 보여 줍니다. 동일한 함수에 대 한 Visual FoxPro 문법이 ODBC 구문과 다를 경우 Visual FoxPro와 동일한 항목이 나열 됩니다.  
  
|ODBC 문법|Visual FoxPro 문법|  
|------------------|---------------------------|  
|CURDATE *()*|DATE *()*|  
|CURTIME *()*|시간 *()*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH (*date_exp)*|일 *()*|  
|시간 *(time_exp)*||  
|분 *(time_exp)*||  
|월 *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|NOW *()*|DATETIME *()*|  
|초 *(time_exp)*|초 *(time_exp)*|  
|주 *(date_exp)*||  
|연도 *(date_exp)*||  
  
 다음 시간 및 날짜 함수는 지원 되지 않습니다.  
  
 DAYOFYEAR *(date_exp)*  
  
 사분기 *(date_exp)*  
  
 TIMESTAMPADD *(interval, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(interval, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC 이스케이프 시퀀스  
 또한 드라이버는 날짜 및 타임 스탬프 데이터에 대 한 ODBC 이스케이프 시퀀스를 지원 합니다. Escape 절 구문은 다음과 같습니다.  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 이 구문에서 **d** 는 *값* 이 *yyyy-mm-dd* 형식의 날짜이 고 **ts** 는 *값* 이 *yyyy-mm-dd hh: mm: ss*[의 타임 스탬프 임을 나타냅니다.* f ...*] 형식과. 날짜 및 타임 스탬프 데이터의 줄임 구문은 다음과 같습니다.  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 예를 들어 다음 문은 모두 지원 되는 SQL UPDATE 명령에서 date 및 timestamp 줄임 구문을 사용 하 여 ALLTYPES 테이블을 업데이트 합니다.  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>설명  
 이스케이프 시퀀스에 대 한 자세한 내용은 *Odbc 프로그래머 참조*에서 [Odbc의 이스케이프 시퀀스](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 를 참조 하세요.
