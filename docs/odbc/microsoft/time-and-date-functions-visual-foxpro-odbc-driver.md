---
title: "시간 및 날짜 함수 (Visual FoxPro ODBC 드라이버) | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC date functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], time and date functions
- FoxPro ODBC driver [ODBC], time and date functions
- time and date functions [ODBC]
- ODBC time and date functions [ODBC]
- date functions [ODBC]
ms.assetid: c1fb63b7-af50-45d6-8dec-ae6ea7119527
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 95545399054e35ee9377f2be5ad2569205c64e8b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>시간 및 날짜 함수 (Visual FoxPro ODBC 드라이버)
다음 표에서; Visual FoxPro ODBC 드라이버에서 지 원하는 ODBC 날짜 및 시간 함수를 보여 줍니다. Visual FoxPro 문법 동일한 기능에 대 한 ODBC 구문을 다를 경우 해당 Visual FoxPro 나열 됩니다.  
  
|ODBC 문법|Visual FoxPro 문법|  
|------------------|---------------------------|  
|CURDATE*)*|날짜*)*|  
|CURTIME*)*|시간*)*|  
|DAYNAME*(date_exp)*|CDOW*(date_exp)*|  
|DAYOFMONTH (*date_exp)*|DAY*)*|  
|시간*(time_exp)*||  
|분*(time_exp)*||  
|월*(time_exp)*||  
|MONTHNAME*(date_exp)*|CMONTH*(date_exp)*|  
|지금은*)*|날짜/시간*)*|  
|두 번째*(time_exp)*|SEC*(time_exp)*|  
|주*(date_exp)*||  
|연도*(date_exp)*||  
  
 다음 날짜 및 시간 함수는 지원 되지 않습니다.  
  
 DAYOFYEAR *(date_exp)*  
  
 분기 *(date_exp)*  
  
 TIMESTAMPADD *(간격, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(간격, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC 이스케이프 시퀀스  
 또한 드라이버는 날짜 및 타임 스탬프 데이터에 대 한 ODBC 이스케이프 시퀀스를 지원합니다. Escape 절 구문은 다음과 같습니다.  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)—  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)—  
```  
  
 이 구문에서 **d** 나타냅니다 *값* 갖는 날짜는 *yyyy-월-일* 형식 및 **ts** 나타냅니다 *값*  은에 타임 스탬프는 *h:mm: ss yyyy-월-일*[. *f...* ] 형식입니다. 날짜 및 타임 스탬프 데이터에 대 한 축약형 구문을 다음과 같습니다.  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 예를 들어, 다음 문 중 각 지원 되는 SQL 업데이트 명령에서 날짜 및 타임 스탬프 축약형 구문을 사용 하 여 ALLTYPES 테이블 업데이트:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>주의  
 이스케이프 시퀀스에 대 한 자세한 내용은 참조 [odbc에서 이스케이프 시퀀스](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 에 *ODBC Programmer's Reference*합니다.
