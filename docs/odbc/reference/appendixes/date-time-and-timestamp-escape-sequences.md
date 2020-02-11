---
title: 날짜, 시간 및 타임 스탬프 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC]
- escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC], about escape sequences
- ODBC escape sequences [ODBC]
ms.assetid: 67b7dee0-e5b1-4469-a626-0c7767852b80
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a6d7a35d0697d1dcbda8f9f64b7ac5a32307d5c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68051144"
---
# <a name="date-time-and-timestamp-escape-sequences"></a>날짜, 시간 및 타임스탬프 이스케이프 시퀀스
ODBC는 날짜, 시간 및 타임 스탬프 리터럴에 대 한 이스케이프 시퀀스를 정의 합니다. 이러한 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
```  
  
{d 'value'}  
{t 'value'}  
{ts 'value'}  
```  
  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
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
  
## <a name="remarks"></a>설명  
 날짜, 시간 및 타임 스탬프 리터럴 이스케이프 시퀀스는 데이터 원본에서 날짜, 시간 및 타임 스탬프 데이터 형식이 지원 되는 경우에만 지원 됩니다. 응용 프로그램은 **SQLGetTypeInfo** 를 호출 하 여 이러한 데이터 형식이 지원 되는지 여부를 확인 해야 합니다.
