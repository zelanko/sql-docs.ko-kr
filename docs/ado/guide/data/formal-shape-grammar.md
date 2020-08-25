---
description: 공식적인 셰이프 문법
title: 공식 모양 문법 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
author: rothja
ms.author: jroth
ms.openlocfilehash: 75cfedbafa7bc0c1b954f8bbdea29ec92d45c07f
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/25/2020
ms.locfileid: "88806829"
---
# <a name="formal-shape-grammar"></a>공식적인 셰이프 문법
다음은 셰이프 명령을 만들기 위한 공식 문법입니다.  
  
-   필요한 문법 조건은 꺾쇠 괄호 ("<>")로 구분 된 텍스트 문자열입니다.  
  
-   선택적 용어는 대괄호 ("[]")로 구분 됩니다.  
  
-   대안은 백슬래시 ("&#124;")로 표시 됩니다.  
  
-   반복 대안은 줄임표 ("...")로 표시 됩니다.  
  
-   *Alpha* 는 영문자의 문자열을 나타냅니다.  
  
-   *숫자는* 숫자 문자열을 나타냅니다.  
  
-   *유니코드 숫자* 는 유니코드 숫자 문자열을 나타냅니다.  
  
 다른 모든 용어는 리터럴입니다.  
  
|용어|정의|  
|----------|----------------|  
|\<shape-command>|SHAPE [ \<table-exp> [AS] \<alias> ]] [ \<shape-action> ]|  
|\<table-exp>|{ \<provider-command-text> } &#124;<br /><br /> ( \<shape-command> ) &#124;<br /><br /> 테이블 \<quoted-name> &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|\<aliased-field-list>&#124; 추가<br /><br /> COMPUTE \<aliased-field-list> [BY \<field-list> ]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias> ]|  
|\<field-exp>|( \<relation-exp> ) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias> ]<br /><br /> 관련 \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> 받는 사람 \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> 변수에 \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM ( \<qualified-field-name> ) &#124;<br /><br /> AVG ( \<qualified-field-name> ) &#124;<br /><br /> MIN ( \<qualified-field-name> ) &#124;<br /><br /> MAX ( \<qualified-field-name> ) &#124;<br /><br /> 개수 ( \<qualified-alias> &#124; \<qualified-name> ) &#124;<br /><br /> STDEV ( \<qualified-field-name> ) &#124;<br /><br /> ANY ( \<qualified-field-name> )|  
|\<calculated-exp>|CALC ( \<expression> )|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias> ]|  
|\<quoted-name>|" \<string> " &#124;<br /><br /> ' \<string> ' &#124;<br /><br /> [ \<string> ] &#124;<br /><br /> \<name>|  
|\<qualified-name>|별칭 [. alias ...]|  
|\<name>|알파 [알파 &#124; 자릿수 &#124; _ &#124; # &#124;: &#124; ...]|  
|\<number>|숫자 [digit ...]|  
|\<new-exp>|NEW \<field-type> [( \<number> [, \<number> ])]|  
|\<field-type>|OLE DB 또는 ADO 데이터 형식입니다.|  
|\<string>|유니코드 문자 [유니코드 문자 ...]|  
|\<expression>|피연산자가 같은 행에 있는 다른 비 계산 열인 Visual Basic for Applications 식입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [계층적 레코드 집합의 행 액세스](./accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](./data-shaping-overview.md)   
 [데이터 셰이핑에 필요한 공급자](./required-providers-for-data-shaping.md)   
 [Shape APPEND 절](./shape-append-clause.md)   
 [Shape 명령 일반](./shape-commands-in-general.md)   
 [셰이프 COMPUTE 절](./shape-compute-clause.md)   
 [Visual Basic for Applications 기능](./visual-basic-for-applications-functions.md)