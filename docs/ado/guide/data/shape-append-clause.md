---
title: 셰이프 APPEND 절 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7b51e2cbfb298493e7001937f7b0f274044478a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47801592"
---
# <a name="shape-append-clause"></a>셰이프 APPEND 절
열 또는 열을 추가 하는 셰이프 명령은 APPEND 절을 **레코드 집합**합니다. 이러한 열은 자식 참조 하는 장 열을 자주 **레코드 집합**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 이 절의 일부는 다음과 같습니다.  
  
 *parent-command*  
 다음의 영 또는 일 (생략할 수 있습니다 합니다 *부모 명령이* 완전히):  
  
-   중괄호로 묶인 공급자 명령을 ("{}")을 반환 하는 **레코드 집합** 개체. 기본 데이터 공급자에 게 명령을 실행 하 고 해당 구문은 해당 공급자의 요구 사항에 따라 달라 집니다. ADO 특별 한 쿼리 언어 필요 하지 않지만 SQL 언어에서 일반적으로 됩니다.  
  
-   다른 셰이프 명령을 괄호 안에 포함 합니다.  
  
-   데이터 공급자에서 테이블의 이름 뒤에 테이블 키워드입니다.  
  
 *parent-alias*  
 부모를 가리키는 선택적인 별칭 **레코드 집합**합니다.  
  
 *column-list*  
 하나 이상의 중:  
  
-   집계 열입니다.  
  
-   계산된 열입니다.  
  
-   새 절을 사용 하 여 만든 새 열입니다.  
  
-   장 열입니다. 장 열 정의 ("()") 괄호로 묶입니다. 다음 구문을 참조 하세요.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>Remarks  
 *child-recordset*  
 -   중괄호로 묶인 공급자 명령을 ("{}")을 반환 하는 **레코드 집합** 개체. 기본 데이터 공급자에 게 명령을 실행 하 고 해당 구문은 해당 공급자의 요구 사항에 따라 달라 집니다. ADO 특별 한 쿼리 언어 필요 하지 않지만 SQL 언어에서 일반적으로 됩니다.  
  
-   다른 셰이프 명령을 괄호 안에 포함 합니다.  
  
-   기존 모양의 이름을 **레코드 집합**합니다.  
  
-   데이터 공급자에서 테이블의 이름 뒤에 테이블 키워드입니다.  
  
 *child-alias*  
 자식으로 참조 하는 별칭 **레코드 집합**합니다.  
  
 *parent-column*  
 열에는 **레코드 집합** 반환한는 *상위 명령입니다.*  
  
 *child-column*  
 열에는 **레코드 집합** 반환한 합니다 *자식*합니다.  
  
 *param-number*  
 참조 [작업 매개 변수가 있는 명령의](../../../ado/guide/data/operation-of-parameterized-commands.md)합니다.  
  
 *chapter-alias*  
 부모에 추가 장 열을 참조 하는 별칭입니다.  
  
> [!NOTE]
>  합니다 *"부모 열* TO *자식 열"* 절이 여기서 정의 된 각 관계는 쉼표로 구분 하 여 실제로 목록  
  
> [!NOTE]
>  추가 키워드 뒤에 절을 실제로 목록, 각 절 쉼표로 구분 됩니다 하 고 부모에 추가할 다른 열을 정의 하는 위치입니다.  
  
## <a name="remarks"></a>Remarks  
 셰이프 명령의 일부로 공급자 명령에서 사용자 입력을 생성 하는 경우 셰이프를 사용자가 제공한 공급자 명령으로 처리 하는 불투명 문자열 공급자를 정확 하 게 전달 합니다. 예를 들어, 다음 셰이프의 명령에서  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 셰이프는 두 명령을 실행 합니다. `select * from t1` 하 고 (`select * from t2 RELATE k1 TO k2)`합니다. 사용자가 세미콜론으로 구분 된 여러 공급자 명령으로 구성 된 복합 명령을 제공 하는 경우 셰이프 차이 구분할 수 아닙니다. 하자면 다음 셰이프 명령  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 셰이프 실행 `select * from t1; drop table t1` 및 (`select * from t2 RELATE k1 TO k2),` 인식 하지는 `drop table t1` 은 별도 및이 여기서는 위험한 공급자 명령입니다. 응용 프로그램 사용자를 잠재적인 해커의 공격을 방지 하려면 입력에 항상 유효성을 검사 해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수화되지 않은 명령 작업](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [매개 변수화된 명령 작업](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [하이브리드 명령](../../../ado/guide/data/hybrid-commands.md)  
  
-   [중간에 셰이프 COMPUTE 절](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
