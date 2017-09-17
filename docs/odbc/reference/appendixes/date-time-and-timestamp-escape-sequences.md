---
title: "날짜, 시간 및 타임 스탬프 이스케이프 시퀀스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC]
- escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC]
ms.assetid: 67b7dee0-e5b1-4469-a626-0c7767852b80
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0476415619db3591fd9c26d22bc615b6d90f6c2e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="date-time-and-timestamp-escape-sequences"></a>날짜, 시간 및 타임 스탬프 이스케이프 시퀀스
ODBC 날짜, 시간 및 타임 스탬프 리터럴에 대 한 이스케이프 시퀀스를 정의 합니다. 이러한 이스케이프 시퀀스 구문은 다음과 같습니다.  
  
```  
  
{d 'value'}  
{t 'value'}  
{ts 'value'}  
```  
  
 BNF 표기법의 구문은 다음과 같습니다.  
  
```  
  
      ODBC-date-time-escape ::=  
     ODBC-date-escape  
     | ODBC-time-escape  
     | ODBC-timestamp-escapeODBC-date-escape ::=  
     ODBC-esc-initiator d 'date-value' ODBC-esc-terminatorODBC-time-escape ::=  
     ODBC-esc-initiator t 'time-value' ODBC-esc-terminatorODBC-timestamp-escape ::=  
     ODBC-esc-initiator ts 'timestamp-value' ODBC-esc-terminatorODBC-esc-initiator ::= {  
ODBC-esc-terminator ::= }  
date-value ::=   
     years-value date-separator months-value date-separator days-valuetime-value ::=   
     hours-value time-separator minutes-value time-separatorseconds-valuetimestamp-value ::= date-value timestamp-separator time-valuedate-separator ::= -  
time-separator ::= :  
timestamp-separator ::=  
     (The blank character)years-value ::= digit digit digit digitmonths-value ::= digit digitdays-value ::= digit digithours-value ::= digit digitminutes-value ::= digit digitseconds-value ::= digit digit[.digit...]  
```  
  
## <a name="remarks"></a>주의  
 Date, time 및 timestamp 리터럴 이스케이프 시퀀스는 데이터 소스에서 날짜, 시간 및 타임 스탬프 데이터 형식을 지 원하는 경우 지원 됩니다. 응용 프로그램 호출 해야 **SQLGetTypeInfo** 를 이러한 데이터 형식이 지원 되는지 확인 합니다.
