---
title: 날짜 및 시간 함수 (Visual FoxPro ODBC 드라이버) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf8e7552faf9567dab25ee3dc5b7b293034faef0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632773"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>날짜 및 시간 함수(Visual FoxPro ODBC 드라이버)
다음 표에서 Visual FoxPro ODBC 드라이버;에서 지원 되는 ODBC 날짜 및 시간 함수 동일한 함수에 대 한 Visual FoxPro 문법 ODBC 구문을 다를 경우에 해당 Visual FoxPro 나열 됩니다.  
  
|ODBC 문법|Visual FoxPro 문법|  
|------------------|---------------------------|  
|CURDATE *( )*|DATE *( )*|  
|CURTIME *( )*|TIME *( )*|  
|DAYNAME *(date_exp)*|CDOW *(date_exp)*|  
|DAYOFMONTH(*date_exp)*|DAY *( )*|  
|HOUR *(time_exp)*||  
|MINUTE *(time_exp)*||  
|MONTH *(time_exp)*||  
|MONTHNAME *(date_exp)*|CMONTH *(date_exp)*|  
|NOW *( )*|DATETIME *( )*|  
|SECOND *(time_exp)*|SEC *(time_exp)*|  
|WEEK *(date_exp)*||  
|YEAR *(date_exp)*||  
  
 다음 날짜 및 시간 함수는 지원 되지 않습니다.  
  
 DAYOFYEAR *(date_exp)*  
  
 분기 *(date_exp)*  
  
 TIMESTAMPADD *(interval, integer_exp, timestamp_exp)*  
  
 TIMESTAMPDIFF *(interval, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC 이스케이프 시퀀스  
 또한 드라이버는 날짜 및 타임 스탬프 데이터에 대 한 ODBC 이스케이프 시퀀스를 지원합니다. Escape 절 구문 아래와 같습니다.  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 이 구문에서 **d** 나타냅니다 *값* 갖는 날짜를 *yyyy-월-일* 형식 및 **ts** 나타내는 *값*  은 타임 스탬프에는 *h:mm: ss yyyy-월-일*[.*f...*] 형식입니다. 날짜 및 타임 스탬프 데이터에 대 한 약식 구문을 아래와 같습니다.  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 예를 들어, 다음 문 중 각 지원 되는 SQL UPDATE 명령을에서 날짜 및 타임 스탬프 축약형 구문을 사용 하 여 ALLTYPES 테이블 업데이트:  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>Remarks  
 이스케이프 시퀀스에 대 한 자세한 내용은 참조 하세요. [ODBC의 이스케이프 시퀀스](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 에 *ODBC 프로그래머 참조*합니다.
