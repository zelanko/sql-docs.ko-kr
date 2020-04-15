---
title: 시간 및 날짜 기능 (비주얼 폭스프로 ODBC 드라이버) | 마이크로 소프트 문서
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
ms.openlocfilehash: 86260f8e7245bed15122d4dbfc4649131674e17f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303064"
---
# <a name="time-and-date-functions-visual-foxpro-odbc-driver"></a>날짜 및 시간 함수(Visual FoxPro ODBC 드라이버)
다음 표에는 Visual FoxPro ODBC 드라이버에서 지원하는 ODBC 시간 및 날짜 함수가 나열되어 있습니다. 동일한 함수에 대한 Visual FoxPro 문법이 ODBC 구문과 다를 때 Visual FoxPro 와 동등한 문법이 나열됩니다.  
  
|ODBC 문법|비주얼 폭스프로 문법|  
|------------------|---------------------------|  
|커데이트 *()*|날짜 *()*|  
|(*)*|시간 *()*|  
|데이네임 *(date_exp)*|도우 *(date_exp)*|  
|데이오브월 *(date_exp)*|일 *()*|  
|시간 *(time_exp)*||  
|분 *(time_exp)*||  
|*월(time_exp)*||  
|월*명(date_exp)*|CMONTH *(date_exp)*|  
|지금 *()*|날짜 시간 *( )*|  
|세컨드 *(time_exp)*|SEC *(time_exp)*|  
|주 *(date_exp)*||  
|*연도(date_exp)*||  
  
 다음 시간 및 날짜 함수는 지원되지 않습니다.  
  
 데이오브이어 *(date_exp)*  
  
 쿼터 *(date_exp)*  
  
 *타임스탬프(간격, integer_exp, timestamp_exp)*  
  
 *타임스탬프DIFF(간격, timestamp_exp1, timestamp_exp2)*  
  
## <a name="odbc-escape-sequences"></a>ODBC 이스케이프 시퀀스  
 드라이버는 날짜 및 타임스탬프 데이터에 대한 ODBC 이스케이프 시퀀스도 지원합니다. 이스케이프 절 구문은 다음과 같습니다.  
  
```  
--(*vendor(Microsoft),product(ODBC) d 'value' *)-  
--(*vendor(Microsoft),product(ODBC) ts ''value' *)-  
```  
  
 이 구문에서 **d는** *값이* *yyyy-mm-dd* 형식의 날짜임을 나타내고 **ts는** *값이* *yyyy-mm-dd hh:mm:ss의*타임스탬프임을 나타냅니다.* f...*] 형식. 날짜 및 타임스탬프 데이터에 대한 약어 구문은 다음과 같습니다.  
  
```  
{d 'value'}  
{ts 'value'}  
```  
  
 예를 들어 다음 각 문은 지원되는 SQL UPDATE 명령에서 날짜 및 타임스탬프 단축 구문을 사용하여 ALLTYPES 테이블을 업데이트합니다.  
  
```  
UPDATE alltypes  
   SET DAT_COL={d'1968-04-28'}  
   WHERE KEY=111  
  
UPDATE alltypes  
   SET DTI_COL={ts'1968-04-28 12:00:00'}  
   WHERE KEY=111  
```  
  
## <a name="remarks"></a>설명  
 이스케이프 시퀀스에 대한 자세한 내용은 *ODBC 프로그래머 의 참조에서 ODBC의* [이스케이프 시퀀스를](../../odbc/reference/develop-app/escape-sequences-in-odbc.md) 참조하십시오.
