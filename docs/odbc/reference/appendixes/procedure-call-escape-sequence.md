---
description: 프로시저 호출 이스케이프 시퀀스
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ba88f3d78edeaa1ce4f4884977656cd8a4a16062
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483226"
---
# <a name="procedure-call-escape-sequence"></a>프로시저 호출 이스케이프 시퀀스
ODBC는 프로시저 호출에 이스케이프 시퀀스를 사용 합니다. 이 이스케이프 시퀀스의 구문은 다음과 같습니다.  
  
 **{**[? =]**call** *프로시저-name*[**(**[*parameter*] [, [*parameter*]] ... **)**]**}**  
  
 BNF 표기법에서 구문은 다음과 같습니다.  
  
 *ODBC-프로시저-이스케이프* :: =  
  
 &#124; *odbc-esc-시작자* [? =] CALL *프로시저 odbc-esc-종결자*  
  
 *프로시저* :: = *프로시저 이름* &#124; *프로시저* 이름 (*프로시저 매개 변수 목록*)  
  
 *프로시저-identifier* :: = *사용자 정의 이름*  
  
 *프로시저-name* :: = *procedure-identifier*  
  
 *소유자 이름*&#124; 합니다. *프로시저-식별자*  
  
 &#124; *카탈로그-이름 카탈로그-구분* *프로시저-식별자*  
  
 *카탈로그-이름 카탈로그-구분 기호* [*소유자-이름*]을 &#124; 합니다. *프로시저-식별자*  
  
 세 번째 구문은 데이터 소스가 소유자를 지원 하지 않는 경우에만 유효 합니다.  
  
 *소유자 이름* :: = *사용자 정의 이름*  
  
 *catalog-name* :: = *사용자 정의-이름*  
  
 *카탈로그 구분 기호* :: = {*구현 정의*}  
  
 카탈로그 구분 기호는 SQL_CATALOG_NAME_SEPARATOR 정보 옵션과 함께 **SQLGetInfo** 를 통해 반환 됩니다.  
  
 *프로시저 매개 변수 목록* :: = *프로시저-매개 변수*  
  
 &#124; *프로시저-매개 변수*, *프로시저 매개 변수 목록*  
  
 *프로시저-parameter* :: = *동적-parameter* &#124; *literal* &#124; *empty 문자열*  
  
 *빈 문자열* :: =  
  
 *ODBC-esc-시작자* :: = {  
  
 *ODBC-esc-종결자* :: =}  
  
 프로시저 매개 변수가 빈 문자열인 경우 프로시저는 해당 매개 변수에 대 한 기본값을 사용 합니다.  
  
 데이터 원본이 프로시저를 지원 하 고 드라이버에서 ODBC 프로시저 호출 구문을 지원 하는지 확인 하기 위해 응용 프로그램은 SQL_PROCEDURES 된 정보 형식으로 **SQLGetInfo** 를 호출할 수 있습니다.
