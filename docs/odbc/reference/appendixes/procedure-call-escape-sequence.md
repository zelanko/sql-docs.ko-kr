---
title: "프로시저 호출 이스케이프 시퀀스 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0ba89ae47d223ea17f02cb07976510d78ff3660e
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-call-escape-sequence"></a>프로시저 호출 이스케이프 시퀀스
ODBC는 이스케이프 시퀀스를 사용 하 여 프로시저 호출에 대 한 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 **{**[? =]**호출** *프로시저 이름*[**(**[*매개 변수*] [, [*매개 변수*]] ... **)**]**}**  
  
 BNF 표기법의 구문은 다음과 같습니다.  
  
 *ODBC 프로시저 이스케이프* :: =  
  
 &#124; *ODBC esc 시작자* [? =] 호출 *프로시저 ODBC esc 종결자*  
  
 *프로시저* :: = *프로시저 이름* &#124; *프로시저 이름* (*프로시저 매개 변수 목록을*)  
  
 *프로시저 식별자* :: = *사용자 정의 이름*  
  
 *프로시저 이름* :: = *프로시저 식별자*  
  
 &#124; *소유자 이름*. *프로시저 식별자*  
  
 &#124; *카탈로그 이름은 카탈로그 구분* *프로시저 식별자*  
  
 &#124; *카탈로그 이름은 카탈로그 구분* [*소유자 이름*]. *프로시저 식별자*  
  
 (세 번째 구문은 데이터 원본 소유자를 지원 하지 않는 경우에 유효 합니다.)  
  
 *소유자 이름을* :: = *사용자 정의 이름*  
  
 *카탈로그 이름* :: = *사용자 정의 이름*  
  
 *카탈로그 구분* :: = {*구현에서 정의 된*}  
  
 (통해 반환 되는 카탈로그 구분 **SQLGetInfo** SQL_CATALOG_NAME_SEPARATOR 정보 옵션을 사용 합니다.)  
  
 *프로시저 매개 변수 목록을* :: = *프로시저 매개 변수*  
  
 &#124; *프로시저 매개 변수*, *프로시저 매개 변수 목록*  
  
 *프로시저 매개 변수* :: = *동적 매개 변수* &#124; *리터럴* &#124; *빈 문자열*  
  
 *빈 문자열* :: =  
  
 *ODBC esc 시작자* :: = {  
  
 *ODBC esc 종결자* :: =}  
  
 (프로시저 매개 변수가 빈 문자열 하는 경우 프로시저 기본값 해당 매개 변수에 사용 합니다.)  
  
 드라이버는 ODBC 프로시저 호출 구문 지원를 데이터 소스는 프로시저를 지원 하는지 여부를 확인 하려면 응용 프로그램이 호출할 수 **SQLGetInfo** SQL_PROCEDURES 정보 유형을 사용 합니다.

