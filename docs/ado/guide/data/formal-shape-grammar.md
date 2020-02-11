---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 91bdf0cfbfe87075d2c9484bca7edd835a950ee6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67925344"
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
|\<셰이프-명령>|SHAPE [\<테이블-exp> [[AS] \<alias>]] [\<셰이프 동작>]|  
|\<테이블-exp>|{\<provider-명령 텍스트>} &#124;<br /><br /> (\<shape 명령>) &#124;<br /><br /> 테이블 \<따옴표 붙은-이름> &#124;<br /><br /> \<따옴표 붙은-이름>|  
|\<셰이프-동작>|추가 \<별칭 지정-필드 목록> &#124;<br /><br /> 계산 \<별칭-필드 목록> [ \<필드별 목록>]|  
|\<별칭 필드 목록>|\<별칭인-field> [, \<별칭인-field ... >]|  
|\<별칭 필드>|\<필드-exp> [[AS] \<별칭>]|  
|\<필드-exp>|(\<관계-exp>) &#124;<br /><br /> \<계산 된 exp> &#124;<br /><br /> \<집계-exp> &#124;<br /><br /> \<새-exp>|  
|<relation_exp>|\<테이블-exp> [[AS] \<별칭>]<br /><br /> \<관계-조건-목록>|  
|\<관계-조건-목록>|\<관계-조건> [, \<관계-조건> ...]|  
|\<관계-조건>|\<필드-이름> \<자식-참조>|  
|\<자식-참조>|\<필드 이름> &#124;<br /><br /> 매개 \<변수-참조>|  
|\<param-참조>|\<숫자>|  
|\<필드 목록>|\<필드 이름> [, \<필드 이름>]|  
|\<집계-exp>|합계 (\<정규화 된 필드 이름>) &#124;<br /><br /> AVG (\<정규화 된 필드 이름>) &#124;<br /><br /> MIN (\<정규화 된 필드 이름>) &#124;<br /><br /> MAX (\<정규화 된 필드 이름>) &#124;<br /><br /> COUNT (\<정규화 된 별칭> &#124; \<정규화 된 이름>) &#124;<br /><br /> STDEV (\<정규화 된 필드-이름>) &#124;<br /><br /> ANY (\<정규화 된 필드 이름>)|  
|\<계산 된 exp>|CALC (\<식>)|  
|\<정규화 된 필드 이름>|\<별칭>입니다. [\<별칭> ...] \<필드 이름>|  
|\<별칭>|\<따옴표 붙은-이름>|  
|\<필드 이름>|\<따옴표 붙은-이름> [[AS \<] 별칭>]|  
|\<따옴표 붙은-이름>|"\<string>" &#124;<br /><br /> '\<string> ' &#124;<br /><br /> [\<문자열>] &#124;<br /><br /> \<이름>|  
|\<정규화 된 이름>|별칭 [. alias ...]|  
|\<이름>|알파 [알파 &#124; 자릿수 &#124; _ &#124; # &#124;: &#124; ...]|  
|\<숫자>|숫자 [digit ...]|  
|\<새-exp>|새 \<필드 형식> [(\<number> [, \<number>])]|  
|\<필드 형식>|OLE DB 또는 ADO 데이터 형식입니다.|  
|\<문자열>|유니코드 문자 [유니코드 문자 ...]|  
|\<식>|피연산자가 같은 행에 있는 다른 비 계산 열인 Visual Basic for Applications 식입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [계층적 레코드 집합의 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [데이터 셰이핑에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [Shape 명령 일반](../../../ado/guide/data/shape-commands-in-general.md)   
 [셰이프 COMPUTE 절](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)
