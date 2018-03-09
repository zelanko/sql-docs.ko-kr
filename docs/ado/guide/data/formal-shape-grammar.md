---
title: "정식 문법을 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f9eb99feba381701f7e590add3906cd0285b2720
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
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
|\<shape-command>|SHAPE [\<table-exp> [[AS] \<alias>]][\<shape-action>]|  
|\<table-exp>|{\<공급자 명령 텍스트 >} &#124;<br /><br /> (\<shape-command>) &#124;<br /><br /> 테이블 \<따옴표 붙은 이름 > &#124;<br /><br /> \<quoted-name>|  
|\<shape-action>|APPEND \<별칭이 지정 된 필드 목록 > &#124;<br /><br /> COMPUTE \<aliased-field-list> [BY \<field-list>]|  
|\<aliased-field-list>|\<aliased-field> [, \<aliased-field...>]|  
|\<aliased-field>|\<field-exp> [[AS] \<alias>]|  
|\<field-exp>|(\<relation-exp>) &#124;<br /><br /> \<calculated-exp> &#124;<br /><br /> \<aggregate-exp> &#124;<br /><br /> \<new-exp>|  
|<relation_exp>|\<table-exp> [[AS] \<alias>]<br /><br /> RELATE \<relation-cond-list>|  
|\<relation-cond-list>|\<relation-cond> [, \<relation-cond>...]|  
|\<relation-cond>|\<field-name> TO \<child-ref>|  
|\<child-ref>|\<field-name> &#124;<br /><br /> PARAMETER \<param-ref>|  
|\<param-ref>|\<number>|  
|\<field-list>|\<field-name> [, \<field-name>]|  
|\<aggregate-exp>|SUM(\<qualified-field-name>) &#124;<br /><br /> AVG(\<qualified-field-name>) &#124;<br /><br /> MIN(\<qualified-field-name>) &#124;<br /><br /> MAX(\<qualified-field-name>) &#124;<br /><br /> COUNT(\<qualified-alias> &#124; \<qualified-name>) &#124;<br /><br /> STDEV(\<qualified-field-name>) &#124;<br /><br /> ANY(\<qualified-field-name>)|  
|\<calculated-exp>|CALC(\<expression>)|  
|\<qualified-field-name>|\<alias>.[\<alias>...]\<field-name>|  
|\<alias>|\<quoted-name>|  
|\<field-name>|\<quoted-name> [[AS] \<alias>]|  
|\<quoted-name>|"\<string>" &#124;<br /><br /> '\<string>' &#124;<br /><br /> [\<string>] &#124;<br /><br /> \<name>|  
|\<qualified-name>|alias[.alias...]|  
|\<name>|알파 [알파 &#124; 자리 &#124; _ &#124; # &#124;: &#124;...]|  
|\<number>|digit [digit...]|  
|\<new-exp>|NEW \<field-type> [(\<number> [, \<number>])]|  
|\<field-type>|OLE DB 또는 ADO 데이터 형식입니다.|  
|\<string>|유니코드 char [유니코드 char...]|  
|\<expression>|응용 프로그램 식 인 피연산자가 같은 행에 있는 다른 아닌 계산 열에 대 한 Visual Basic입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [데이터 모양 지정에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적으로 shape 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [셰이프 COMPUTE 절](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)
