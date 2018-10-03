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
manager: craigg
ms.openlocfilehash: 9131e5fa8f16a137461bde5ecea3fd793b2cf9be
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47792711"
---
# <a name="date-time-and-timestamp-escape-sequences"></a>날짜, 시간 및 타임스탬프 이스케이프 시퀀스
ODBC 날짜, 시간 및 타임 스탬프 리터럴에 대 한 이스케이프 시퀀스를 정의합니다. 이러한 이스케이프 시퀀스 구문은 다음과 같습니다.  
  
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
  
## <a name="remarks"></a>Remarks  
 날짜, 시간 및 타임 스탬프 리터럴 이스케이프 시퀀스는 데이터 원본에서 날짜, 시간 및 타임 스탬프 데이터 형식을 지 원하는 경우 지원 됩니다. 응용 프로그램에서 호출 해야 **SQLGetTypeInfo** 이러한 데이터 형식이 지원 되는지 여부를 확인 하려면.
