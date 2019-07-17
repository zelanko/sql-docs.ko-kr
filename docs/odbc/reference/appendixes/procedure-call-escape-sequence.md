---
title: 프로시저 호출 이스케이프 시퀀스 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aa936eb9f8ef3328945d4ece63fb36432a5fd618
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100587"
---
# <a name="procedure-call-escape-sequence"></a>프로시저 호출 이스케이프 시퀀스
ODBC는 이스케이프 시퀀스를 사용 하 여 프로시저 호출에 대 한 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 **{** [? =]**호출** *프로시저 이름*[ **(** [*매개 변수*] [, [*매개 변수*]]... **)** ] **}**  
  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC-procedure-escape* ::=  
  
 &#124;*ODBC esc 시작자* [? =] 호출 *프로시저 ODBC esc 종결자*  
  
 *프로시저* :: = *프로시저 이름* &#124; *프로시저 이름* (*프로시저 매개 변수 목록을*)  
  
 *프로시저 식별자* :: = *사용자 정의 이름*  
  
 *프로시저 이름을* :: = *프로시저 식별자*  
  
 &#124;*소유자 이름*. *절차-식별자*  
  
 &#124;*카탈로그 이름을 카탈로그 구분 기호* *프로시저 식별자*  
  
 &#124;*카탈로그 이름을 카탈로그 구분 기호* [*소유자 이름*]. *절차-식별자*  
  
 (세 번째 구문은 데이터 원본 소유자를 지원 하지 않는 경우에 유효 합니다.)  
  
 *소유자 이름을* :: = *사용자 정의 이름*  
  
 *카탈로그 이름이* :: = *사용자 정의 이름*  
  
 *카탈로그 구분 기호* :: = {*구현에서 정의 된*}  
  
 (통해 반환 되는 카탈로그 구분 **SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 정보 옵션을 사용 하 여.)  
  
 *프로시저 매개 변수 목록을* :: = *프로시저 매개 변수*  
  
 &#124;*프로시저 매개 변수가*, *프로시저 매개 변수 목록*  
  
 *프로시저 매개 변수가* :: = *동적 매개 변수* &#124; *리터럴* &#124; *빈 문자열*  
  
 *empty-string* ::=  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 (프로시저 매개 변수는 빈 문자열인 경우 프로시저는 기본 값을 해당 매개 변수에 대 한 합니다.)  
  
 드라이버는 ODBC 프로시저 호출 구문 지원를 데이터 소스는 프로시저를 지원 하는지 여부를 확인 하려면 응용 프로그램이 호출할 수 있습니다 **SQLGetInfo** SQL_PROCEDURES 정보 형식을 사용 하 여 합니다.
