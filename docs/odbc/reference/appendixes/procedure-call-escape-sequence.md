---
title: 프로시저 호출 이스케이프 시퀀스 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1194efe6a21c456a722ccd4352661c998f0316d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298223"
---
# <a name="procedure-call-escape-sequence"></a>프로시저 호출 이스케이프 시퀀스
ODBC는 프로시저 호출에 이스케이프 시퀀스를 사용합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 **{**[?=]**호출** *프로시저 이름*[**[**[ 매개*변수*][[[[[[매개*변수]]...* **)**]**}**  
  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC 프로시저-이스케이프::=*  
  
 &#124; *ODBC-esc-이니시에이터* [?=] 호출 *절차 ODBC-esc-종료기*  
  
 *프로시저* ::= *프로시저 이름* &#124; *프로시저* 이름(프로시저*매개 변수 목록)*  
  
 *프로시저 식별자* ::= *사용자 정의 이름*  
  
 *프로시저 이름* ::= *프로시저 식별자*  
  
 &#124; *소유자 이름*. *프로시저 식별자*  
  
 &#124; *카탈로그 이름 카탈로그 구분자* *프로시저 식별자*  
  
 &#124; *카탈로그-카탈로그 구분기호* *[소유자 이름].* *프로시저 식별자*  
  
 세 번째 구문은 데이터 원본이 소유자를 지원하지 않는 경우에만 유효합니다.  
  
 *소유자 이름* ::= *사용자 정의 이름*  
  
 *카탈로그 이름* ::= *사용자 정의 이름*  
  
 *카탈로그 구분 기호* ::= {*구현 정의*}  
  
 카탈로그 구분 기호는 SQL_CATALOG_NAME_SEPARATOR 정보 옵션을 통해 **SQLGetInfo를** 통해 반환됩니다.  
  
 *프로시저 매개 변수 목록* ::= *프로시저 매개 변수*  
  
 &#124; *프로시저 매개 변수,* *프로시저 매개 변수 목록*  
  
 *프로시저 매개 변수* ::= *동적 매개 변수* &#124; *리터럴* &#124; *빈 문자열*  
  
 *빈 문자열* ::=  
  
 *ODBC-esc-이니시에이터* ::= {  
  
 *ODBC-esc-종결자* ::= }  
  
 프로시저 매개 변수가 빈 문자열인 경우 프로시저는 해당 매개 변수에 대한 기본값을 사용합니다.  
  
 데이터 원본이 프로시저를 지원하고 드라이버가 ODBC 프로시저 호출 구문을 지원하는지 여부를 확인하기 위해 응용 프로그램은 SQL_PROCEDURES 정보 형식을 사용하여 **SQLGetInfo를** 호출할 수 있습니다.
