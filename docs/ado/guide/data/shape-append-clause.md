---
title: "APPEND 절 셰이프 | Microsoft Docs"
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
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 52c9495e221ba7a4b71ba91d276eefd576f6715d
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="shape-append-clause"></a>셰이프 APPEND 절
열 또는 열을 추가 하는 셰이프 명령 APPEND 절은 **레코드 집합**합니다. 대부분의 경우 이러한 열은 장 열을 참조 하는 자식 **레코드 집합**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 이 절의 일부는 다음과 같습니다.  
  
 *부모 명령*  
 다음 중 하나 또는 0 (생략할 수 있습니다는 *부모 명령이* 완전히):  
  
-   반환 하는 공급자 명령 중괄호 ("{")는 **레코드 집합** 개체입니다. 기본 데이터 공급자에는 명령이 실행 될 하 고 해당 공급자의 요구 사항에 해당 구문에 따라 달라 집니다. ADO 특별 한 쿼리 언어 필요 하지 않지만 SQL 언어 같아야 합니다.  
  
-   다른 도형 명령 괄호에 포함 합니다.  
  
-   데이터 공급자에 있는 테이블의 이름이 차례로 나옵니다 테이블 키워드입니다.  
  
 *부모 별칭*  
 부모를 참조 하는 선택적 별칭 **레코드 집합**합니다.  
  
 *열 목록*  
 하나 이상의 다음:  
  
-   집계 열입니다.  
  
-   계산 된 열입니다.  
  
-   새 절을 사용 하 여 만든 새 열입니다.  
  
-   장 열입니다. 장 열 정의 ("()") 괄호로 묶여 있습니다. 다음 구문을 참조 하십시오.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>주의  
 *자식 레코드 집합*  
 -   반환 하는 공급자 명령 중괄호 ("{")는 **레코드 집합** 개체입니다. 기본 데이터 공급자에는 명령이 실행 될 하 고 해당 공급자의 요구 사항에 해당 구문에 따라 달라 집니다. ADO 특별 한 쿼리 언어 필요 하지 않지만 SQL 언어 같아야 합니다.  
  
-   다른 도형 명령 괄호에 포함 합니다.  
  
-   기존 모양 이름 **레코드 집합**합니다.  
  
-   데이터 공급자에 있는 테이블의 이름이 차례로 나옵니다 테이블 키워드입니다.  
  
 *자식 별칭*  
 자식 참조 하는 별칭 **레코드 집합**합니다.  
  
 *부모 열*  
 열에는 **레코드 집합** 에서 반환 되는 *부모 명령입니다.*  
  
 *자식 열*  
 열에는 **레코드 집합** 에서 반환 되는 *자식 명령*합니다.  
  
 *매개 변수 번호*  
 참조 [작업 매개 변수가 있는 명령의](../../../ado/guide/data/operation-of-parameterized-commands.md)합니다.  
  
 *장 별칭*  
 부모에 추가 된 장 열을 참조 하는 별칭입니다.  
  
> [!NOTE]
>  *"부모 열* TO *자식 열"* 절은 실제로 목록에 정의 된 각 관계는 쉼표로 구분 하 여  
  
> [!NOTE]
>  APPEND 키워드 다음 절은 실제로 목록, 여기서 각 절은 쉼표로 구분 하 고 부모에 추가할 다른 열을 정의 합니다.  
  
## <a name="remarks"></a>주의  
 SHAPE 명령의 일환으로 사용자 입력 으로부터 공급자 명령을 생성할 때 셰이프는 사용자가 제공한 공급자 명령을 불투명 문자열로 처리 하며 공급자에 정확 하 게 전달 합니다. 예를 들어 다음 SHAPE 명령에서  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 셰이프 두 명령을 실행 합니다: `select * from t1` 및 (`select * from t2 RELATE k1 TO k2)`합니다. 사용자가 세미콜론으로 구분 된 여러 공급자 명령으로 구성 된 복합 명령을 제공 하는 경우 셰이프 차이 구분할 수지 않습니다. 계산 되는 다음 SHAPE 명령을  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 셰이프 실행 `select * from t1; drop table t1` 및 (`select * from t2 RELATE k1 TO k2),` 를 인식 하지 `drop table t1` 는 별도와이 case, 위험, 공급자 명령입니다. 응용 프로그램 사용자를 차단할 잠재적인 해커의 공격을 방지 하기 위해 입력에 항상 유효성을 검사 해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수화되지 않은 명령 작업](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [매개 변수화된 명령 작업](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [하이브리드 명령](../../../ado/guide/data/hybrid-commands.md)  
  
-   [중간에 셰이프 COMPUTE 절](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
