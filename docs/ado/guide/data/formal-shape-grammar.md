---
title: "정식 문법을 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO], shape grammar
- data shaping [ADO], shape grammar
ms.assetid: ea691475-0f03-4abe-a785-b77e77712d1d
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ae47b751e9e62d84188927186f186c6c9d344ce0
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

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
|\<shape 명령 >|셰이프 [\<테이블 exp > [[AS] \<별칭 >]] [\<셰이프 작업 >]|  
|\<exp 테이블 >|{\<공급자 명령 텍스트 >} &#124;<br /><br /> (\<shape 명령 >) &#124;<br /><br /> 테이블 \<따옴표 붙은 이름 > &#124;<br /><br /> \<따옴표 붙은 이름 >|  
|\<셰이프 작업 >|APPEND \<별칭이 지정 된 필드 목록 > &#124;<br /><br /> 계산 \<별칭이 지정 된 필드 목록 > [BY \<필드 목록 >]|  
|\<별칭이 지정 된 필드 목록 >|\<별칭이 지정 된 필드 > [, \<별칭이 지정 된 필드... >]|  
|\<필드 별칭 >|\<필드 exp > [[AS] \<별칭 >]|  
|\<필드 exp >|(\<관계 exp >) &#124;<br /><br /> \<계산 exp > &#124;<br /><br /> \<집계 exp > &#124;<br /><br /> \<새 exp >|  
|< relation_exp >|\<테이블 exp > [[AS] \<별칭 >]<br /><br /> 관계 \<관계 조건 목록 >|  
|\<관계 조건 목록 >|\<관계 조건 > [, \<관계 조건 >...]|  
|\<관계 조건 >|\<필드 이름 > TO \<자식 ref >|  
|\<자식 ref >|\<필드 이름 > &#124;<br /><br /> 매개 변수 \<param ref >|  
|\<ref 매개 변수 >|\<숫자 >|  
|\<필드 목록 >|\<필드 이름 > [, \<필드 이름 >]|  
|\<집계 exp >|SUM (\<정규화 된 필드-이름 >) &#124;<br /><br /> AVG (\<정규화 된 필드-이름 >) &#124;<br /><br /> MIN (\<정규화 된 필드-이름 >) &#124;<br /><br /> MAX (\<정규화 된 필드-이름 >) &#124;<br /><br /> COUNT (\<한정 별칭 > &#124; \<정규화 된 이름 >) &#124;<br /><br /> STDEV (\<정규화 된 필드-이름 >) &#124;<br /><br /> 모든 (\<정규화 된 필드-이름 >)|  
|\<계산 exp >|계산 (\<식 >)|  
|\<정규화 된 필드-이름 >|\<별칭 > 합니다. [\<별칭 >...] \<필드 이름 >|  
|\<별칭 >|\<따옴표 붙은 이름 >|  
|\<필드 이름 >|\<따옴표 붙은 이름 > [[AS] \<별칭 >]|  
|\<따옴표 붙은 이름 >|"\<문자열 >" &#124;<br /><br /> '\<문자열 >' &#124;<br /><br /> [\<문자열 >] &#124;<br /><br /> \<이름 >|  
|\<정규화 된 이름 >|별칭 [.alias...]|  
|\<이름 >|알파 [알파 &#124; 자리 &#124; _ &#124; # &#124;: &#124;...]|  
|\<숫자 >|숫자 [자리...]|  
|\<새 exp >|새 \<필드 유형 > [(\<번호 > [, \<번호 >])]|  
|\<필드 형식 >|OLE DB 또는 ADO 데이터 형식입니다.|  
|\<문자열 >|유니코드 char [유니코드 char...]|  
|\<식 >|응용 프로그램 식 인 피연산자가 같은 행에 있는 다른 아닌 계산 열에 대 한 Visual Basic입니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [데이터 셰이핑 개요](../../../ado/guide/data/data-shaping-overview.md)   
 [데이터 모양 지정에 필요한 공급자](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [셰이프 APPEND 절](../../../ado/guide/data/shape-append-clause.md)   
 [일반적으로 shape 명령](../../../ado/guide/data/shape-commands-in-general.md)   
 [셰이프 COMPUTE 절](../../../ado/guide/data/shape-compute-clause.md)   
 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md)

