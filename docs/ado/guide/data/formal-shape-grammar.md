---
title: 정식 문법을 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9bb375b0b580bec75b1994a549a1a5815f4e34ec
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/11/2018
ms.locfileid: "35270372"
---
# <a name="formal-shape-grammar"></a>형식 모양 문법
다음은 shape 명령을 만드는 정식 문법입니다.  
  
-   필수 문법 용어는 꺾쇠 괄호 ("<>")로 구분 된 텍스트 문자열입니다.  
  
-   선택적 용어는 대괄호 ("")으로 구분 됩니다.  
  
-   대안 분할선 표시 됩니다 ("&#124;").  
  
-   반복 대안 줄임표 ("…")로 표시 됩니다.  
  
-   *알파* 알파벳 문자와 문자열을 나타냅니다.  
  
-   *자리* 숫자의 문자열을 나타냅니다.  
  
-   *유니코드 자리* 유니코드 숫자의 문자열을 나타냅니다.  
  
 다른 모든 용어는 리터럴입니다.  
  
|용어|정의|  
|----------|----------------|  
|\<shape-command>|셰이프 [\<테이블 exp > [[AS] \<별칭 >]] [\<셰이프 작업 >]|  
|\<table-exp>|{\<공급자 명령 텍스트 >}&#124;<br /><br /> (\<shape-command>) &#124;<br /><br /> 테이블 \<따옴표 붙은 이름 >&#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|APPEND \<별칭이 지정 된 필드 목록 >&#124;<br /><br /> 계산 \<별칭이 지정 된 필드 목록 > [BY \<필드 목록 >]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<필드 exp > [[AS] \<별칭 >]|  
|\<field-exp>|(\<relation-exp>) &#124;<br /><br /> \<계산 exp >&#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<테이블 exp > [[AS] \<별칭 >]<br /><br /> RELATE \<relation-cond-list>|  
|\<relation-cond-list>|\<관계 조건 > [, \<관계 조건 >...]|  
|\<relation-cond>|\<field-name> TO \<child-ref>|  
|\<child-ref>|\<필드 이름 >&#124;<br /><br /> 매개 변수 \<param ref >|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM(\<qualified-field-name>) &#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|계산 (\<식 >)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<따옴표 붙은 이름 > [[AS] \<별칭 >]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|별칭 [.alias...]|  
|\<name>|알파 [알파 &#124; 자리 &#124; _ &#124; # &#124; : &#124; ...]|  
|\<number>|digit [digit...]|  
|\<new-exp>|NEW \<field-type> [(\<number> [, \<number>])]|  
|\<field-type>|OLE DB 또는 ADO 데이터 형식입니다.|  
|\<string>|유니코드 char [유니코드 char...]|  
|\<expression>|응용 프로그램 식 인 피연산자가 같은 행에 있는 다른 아닌 계산 열에 대 한 Visual Basic입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [데이터 모양 지정에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적으로 shape 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [셰이프 COMPUTE 절](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)
