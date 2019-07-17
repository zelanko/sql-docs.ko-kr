---
title: ALTER CUBE 문 (MDX) | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 750f8ae7a1b9275bdab734a15134d255916e7d44
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098521"
---
# <a name="mdx-data-definition---alter-cube"></a>MDX 데이터 정의 - ALTER CUBE


  일반적으로 차원 쓰기 저장을 지원하는 데 사용되는 지정한 큐브의 구조를 변경합니다. 응용 프로그램에서 쓰기 저장을 사용 하는 방법에 대 한 자세한 내용은이 블로그 게시물을 참조 하세요. [Analysis Services (블로그)를 사용 하 여 쓰기 저장 응용 프로그램 빌드](https://go.microsoft.com/fwlink/?LinkId=394977)  
  
 동시 차원 쓰기 저장으로 교착 상태가 발생할 수 있습니다. 두 번째 쓰기 저장이 보유한 공유 잠금으로 인해 커밋에서 첫 번째 쓰기 저장이 차단됩니다. 이 상황에서 발생되는 오류는 없지만 아무 작업도 진행할 수 없습니다. 결국 제한 시간 및 변경 내용이 롤백됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
ALTER CUBE  
      Cube_Name | CURRENTCUBE  
      <alter clause>   
            [ < alter clause> ...n]  
  
< alter clause> ::=   
   <create dimension member clause>   
  | <remove dimension member clause>  
  | <move dimension member clause>   
    | <update clause>   
    | <create cell calculation clause>  
  
<create dimension member clause> ::=  
CREATE DIMENSION MEMBER [ParentName.]MemberName  
    , [[KEY = Key_Value]   
    | [Property_Name = Property_Value[, ...n]]  
  
<dropping clause>::=  
DROP   
      DIMENSION MEMBER Member_Name   
            Member_Name ...n ]   
      [WITH DESCENDANTS]  
      | [ SESSION ] [ CALCULATED ] MEMBER Member_Name   
                  [ ,Member_Name,...n ]   
    | SET Set_Name  
                  [ ,Set_Name,...n ]   
    | [ SESSION ] CELL CALCULATION CellCalc_Name  
                  [ ,CellCalc_Name,...n ]   
    | ACTION Action_Name  
  
<move dimension member clause> ::=  
MOVE DIMENSION MEMBER MemberName  
        [, SKIPPED_LEVELS = Unsigned_Integer]   
      [WITH DESCENDANTS]  
    UNDER ParentName      
  
<update clause> ::=  
UPDATE   
    CUSTOM ROLLUP FOR MEMBER MemberName  
      [,MemberName, ...n] AS MDX_Expression  
   | DIMENSION Dimension_Name | Hierarchy_Name  
      , DEFAULT_MEMBER = MDX_Expression  
   | DIMENSION MEMBER MemberName AS  
   [MDX_Expression]  
   [Property_Name = Property_Value[, ...n]]  
  
<create cell calculation clause>::=  
CELL CALCULATION Calculation_Name   
   FOR Set_Expression AS MDX_Expression   
            [ [ CONDITION = 'Logical_Expression' ]   
    | [ DISABLED = { TRUE | FALSE } ]   
    | [ DESCRIPTION =String ]   
    | [ CALCULATION_PASS_NUMBER = Integer]   
    | [ CALCULATION_PASS_DEPTH = Integer]   
    | [ SOLVE_ORDER = Integer]   
    | [ Calculation_Name= Scalar_Expression ], ...n]  
```  
  
## <a name="creating-a-dimension-member"></a>차원 멤버 만들기  
 기본 차원 테이블에 새 행을 추가합니다.  
  
### <a name="arguments"></a>인수  
 *ParentName*  
 새 차원 멤버를 루트에 만들지 않을 경우 새 차원 멤버의 부모 이름을 지정하는 유효한 문자열 식입니다.  
  
 *MemberName*  
 멤버 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Key_Value*  
 새 차원 멤버의 키 값을 정의하는 유효한 스칼라 식입니다.  
  
 *Property_Name*  
 멤버 속성을 나타내는 유효한 MDX 식별자입니다.  
  
 *Property_Value*  
 계산 멤버 속성의 값을 정의하는 유효한 MDX 스칼라 식입니다.  
  
## <a name="dropping-a-dimension-member"></a>차원 멤버 삭제  
 쓰기 가능한 차원에서 차원 멤버를 삭제하면 해당 멤버와 기본 차원 테이블의 해당 행이 삭제됩니다.  
  
### <a name="arguments"></a>인수  
 *Cube_Name*  
 큐브 이름을 지정하는 유효한 문자열 식입니다.  
  
 *Member_Name*  
 멤버 이름이나 멤버 키를 지정하는 유효한 문자열 식입니다.  
  
### <a name="remarks"></a>설명  
 WITH DESCENDANTS 절을 사용하지 않을 경우 삭제된 멤버의 자식은 삭제된 멤버의 부모의 자식이 됩니다. WITH DESCENDANTS 절을 사용하면 모든 하위 항목과 차원 테이블의 해당 행도 삭제됩니다.  
  
> [!NOTE]  
>  계산된 멤버, 명명 된 집합, 동작 및 셀 계산 삭제에 대 한 정보를 참조 하세요. [DROP MEMBER 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-member.md)하십시오 [SET 문을 삭제 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-set.md), [DROP ACTION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-action.md), 및 [DROP CELL CALCULATION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md).  
  
## <a name="updating-the-default-dimension-member"></a>기본 차원 멤버 업데이트  
 이 절은 큐브의 기본 멤버를 업데이트하며, MDX 계산 스크립트에서 기본 멤버를 정의하는 데 사용됩니다. 기본 멤버는 데이터베이스 차원, 큐브 차원 또는 사용자 로그인에 대해 지정할 수 있습니다. 또한 기본 멤버는 세션 동안 변경될 수 있습니다.  
  
### <a name="arguments"></a>인수  
 *Dimension_Name*  
 차원의 이름을 지정하는 유효한 문자열입니다.  
  
 *MDX_Expression*  
 단일 멤버를 반환하는 유효한 MDX 식입니다.  
  
### <a name="remarks"></a>설명  
 지정된 MDX 식은 정적이거나 동적일 수 있습니다.  
  
## <a name="moving-a-dimension-member"></a>차원 멤버 이동  
 기본 차원 테이블에서 행을 수정합니다.  
  
### <a name="arguments"></a>인수  
 *ParentName*  
 이동할 차원 멤버의 새 부모 이름을 지정하는 유효한 문자열 식입니다.  
  
 *MemberName*  
 멤버 이름을 지정하는 유효한 문자열 식입니다.  
  
 Unsigned_*정수*  
 건너뛸 수준 수를 지정하는 유효한 숫자입니다.  
  
 WITH DESCENDANTS 절이 지정된 경우 트리 전체가 이동됩니다. WITH DESCENDANTS 절이 지정되지 않은 경우 이동된 부모의 자식은 이동된 멤버의 부모의 자식이 됩니다. 차원 멤버를 이동하면 단순히 기본 차원 테이블에 있는 부모 키 열의 값이 업데이트됩니다.  
  
## <a name="updating-a-dimension-member"></a>차원 멤버 업데이트  
 UPDATE DIMENSION MEMBER 절을 사용하면 멤버의 속성뿐 아니라 멤버와 관련된 사용자 지정 멤버 수식도 수정할 수 있습니다.  
  
### <a name="arguments"></a>인수  
 *MemberName*  
 멤버 이름을 지정하는 유효한 문자열 식입니다.  
  
 *MDX_Expression*  
 단일 멤버를 반환하는 유효한 MDX 식입니다.  
  
 *Property_Value*  
 계산 멤버 속성의 값을 정의하는 유효한 MDX 스칼라 식입니다.  
  
## <a name="creating-a-cell-calculation"></a>셀 계산 만들기  
 ALTER CUBE 문을 사용 하 여 셀 계산을 만드는 방법에 대 한 자세한 내용은 참조 하세요. [DROP CELL CALCULATION 문 &#40;MDX&#41;](../mdx/mdx-data-definition-drop-cell-calculation.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MDX 데이터 정의 문 &#40;MDX&#41;](../mdx/mdx-data-definition-statements-mdx.md)  
  
  
