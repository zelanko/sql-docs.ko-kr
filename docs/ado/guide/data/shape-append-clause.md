---
description: 셰이프 APPEND 절
title: Shape APPEND 절 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: rothja
ms.author: jroth
ms.openlocfilehash: 11d2c02d24753460f90452ddd6cc6b1e1589b80b
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979624"
---
# <a name="shape-append-clause"></a>셰이프 APPEND 절
Shape command APPEND 절은 **레코드 집합**에 열을 추가 합니다. 이러한 열은 종종 자식 **레코드 집합**을 참조 하는 장 열입니다.  
  
## <a name="syntax"></a>구문  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 이 절의 부분은 다음과 같습니다.  
  
 *부모-명령*  
 0 또는 다음 중 하나입니다 ( *parent 명령을* 완전히 생략할 수 있음).  
  
-   {} **레코드 집합** 개체를 반환 하는 중괄호 ("")로 묶인 공급자 명령입니다. 명령은 기본 데이터 공급자에 대해 실행 되며 해당 구문은 해당 공급자의 요구 사항에 따라 달라 집니다. ADO에 특정 쿼리 언어가 필요 하지는 않지만 일반적으로 SQL 언어입니다.  
  
-   괄호 안에 포함 된 다른 셰이프 명령입니다.  
  
-   테이블 키워드와 데이터 공급자의 테이블 이름이 차례로 나옵니다.  
  
 *부모 별칭*  
 부모 **레코드 집합**을 참조 하는 선택적 별칭입니다.  
  
 *열 목록*  
 다음 중 하나 이상입니다.  
  
-   집계 열입니다.  
  
-   계산 된 열입니다.  
  
-   NEW 절을 사용 하 여 만든 새 열입니다.  
  
-   장 열입니다. 장 열 정의는 괄호 ("()")로 묶습니다. 다음 구문을 참조 하세요.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>설명  
 *하위 레코드 집합*  
 -   {} **레코드 집합** 개체를 반환 하는 중괄호 ("")로 묶인 공급자 명령입니다. 명령은 기본 데이터 공급자에 대해 실행 되며 해당 구문은 해당 공급자의 요구 사항에 따라 달라 집니다. ADO에 특정 쿼리 언어가 필요 하지는 않지만 일반적으로 SQL 언어입니다.  
  
-   괄호 안에 포함 된 다른 셰이프 명령입니다.  
  
-   기존 모양의 **레코드 집합**의 이름입니다.  
  
-   테이블 키워드와 데이터 공급자의 테이블 이름이 차례로 나옵니다.  
  
 *자식 별칭*  
 자식 **레코드 집합**을 참조 하는 별칭입니다.  
  
 *부모-열*  
 부모 명령에 의해 반환 되는 **레코드 집합** 의 열 *입니다.*  
  
 *자식 열*  
 *자식 명령*에서 반환 하는 **레코드 집합** 의 열입니다.  
  
 *param 번호*  
 [매개 변수가 있는 명령의 작업을](../../../ado/guide/data/operation-of-parameterized-commands.md)참조 하세요.  
  
 *장-별칭*  
 부모에 추가 된 챕터 열을 참조 하는 별칭입니다.  
  
> [!NOTE]
>  *"부모-열* 과 *자식 열"* 절은 실제로 정의 된 각 관계가 쉼표로 구분 된 목록입니다.  
  
> [!NOTE]
>  APPEND 키워드 뒤의 절은 실제로 목록으로, 각 절은 쉼표로 구분 되 고 부모에 추가할 다른 열을 정의 합니다.  
  
셰이프 명령의 일부로 사용자 입력에서 공급자 명령을 생성 하는 경우 SHAPE는 사용자 제공 공급자 명령을 불투명 문자열로 처리 하 고이를 공급자에 게 정확 하 게 전달 합니다. 예를 들어, 다음 SHAPE 명령에서  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 SHAPE는 및 (의 두 명령을 실행 `select * from t1` `select * from t2 RELATE k1 TO k2)` 합니다. 세미콜론으로 구분 된 여러 공급자 명령으로 구성 된 복합 명령을 사용자가 제공 하는 경우 SHAPE는 차이를 구분할 수 없습니다. 따라서 다음 SHAPE 명령에서  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 SHAPE는 `select * from t1; drop table t1` 및를 실행 `select * from t2 RELATE k1 TO k2),` 합니다. 즉, `drop table t1` 별도 이며이 경우에는 위험한, 공급자 명령으로 인식 되지 않습니다. 응용 프로그램은 항상 사용자 입력의 유효성을 검사 하 여 이러한 잠재적인 해커 공격이 발생 하지 않도록 해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수화되지 않은 명령 작업](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [매개 변수화된 명령 작업](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [하이브리드 명령](../../../ado/guide/data/hybrid-commands.md)  
  
-   [중간에 셰이프 COMPUTE 절](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
