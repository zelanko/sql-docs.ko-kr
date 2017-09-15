---
title: "셰이프 일반적 명령 | Microsoft Docs"
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
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 245f842883ec0be1ac92ad58ea75b4cdef7d9cb3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="shape-commands-in-general"></a>일반적으로 shape 명령
모양의의 열을 정의 데이터 셰이핑 **레코드 집합**, 열 및는 방식을 나타내는 엔터티 사이의 관계는 **레코드 집합** 데이터로 채워집니다.  
  
 모양의 **레코드 집합** 다음 유형의 열으로 구성 될 수 있습니다.  
  
|열 유형|Description|  
|-----------------|-----------------|  
|data|필드는 **레코드 집합** 테이블을 쿼리하거나 모양 이전에 데이터 공급자에 대 한 쿼리 명령을 반환한 **레코드 집합**합니다.|  
|장|에 대 한 참조를 다른 **레코드 집합**라고 하는 *장*합니다. 장 열 수 있도록 정의 하는 *부모-자식* 관계 여기서는 *부모* 는 **레코드 집합** 장 열을 포함 하는 있는*자식* 는 **레코드 집합** 여 합니다.|  
|집계(aggregate)|실행 하 여 열 값 파생는 *집계 함수* 모든 행 또는 자식의 모든 행의 열에 **레코드 집합**합니다. (다음 항목에서는 집계 함수를 참조 하십시오. [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|계산 된 식|예를 들어 응용 프로그램의 같은 행의 열에는 식 계산 하 여 파생 된 열의 값은 **레코드 집합**합니다. 식은 계산 함수에 대 한 인수입니다. (다음 항목에서 계산 된 식 참조 [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) 및 [응용 프로그램 기능에 대 한 Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|new|빈, 맞추어진 있는 필드는 나중에 데이터로 채울 수 있습니다. 열은 새 키워드와 함께 정의 됩니다. (NEW 키워드는 다음 항목에서 참조 [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Shape 명령에서 반환 되는 기본 데이터 공급자에는 쿼리 명령을 지정 하는 절을 포함할 수 있습니다는 **레코드 집합** 개체입니다. 쿼리의 구문은 기본 데이터 공급자의 요구 사항에 따라 달라 집니다. ADO에서는 모든 특정 쿼리 언어를 사용 하지 않지만 SQL, 일반적으로 됩니다.  
  
 Shape 명령에서 발급 될 수 **레코드 집합** 개체 또는 설정 하는 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성은 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체 하 고 호출할는 [Execute ](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드.  
  
 두 개의 테이블; SQL JOIN 절을 사용할 수 있습니다. 그러나 계층적 **레코드 집합** 정보를 보다 효율적으로 나타낼 수 있습니다. 각 행에는 **레코드 집합** 테이블 중 하나에서 중복 해 서 조인 반복이 정보에 의해 발생 합니다. 계층적 **레코드 집합** 에 하나의 부모 **레코드 집합** 각 여러 명의 자식에 대 한 **레코드 집합** 개체입니다.  
  
 Shape 명령 중첩 될 수 있습니다. 즉,는 *부모 명령이* 또는 *자식 명령* 다른 셰이프 명령 자체가 될 수 있습니다.  
  
 사용자의 커서 위치를 지정 하는 경우에 항상 클라이언트 커서를 반환 셰이프 공급자 **가 adUseServer**합니다.  
  
 에 액세스할 수 있습니다는 **레코드 집합** 모양을의 구성 요소 **레코드 집합** 프로그래밍 방식으로 또는 적절 한 시각적 컨트롤을 통해.  
  
 Microsoft는 셰이프 명령을 생성 하는 비주얼 도구를 제공 (참조는 [데이터 환경 디자이너](http://go.microsoft.com/fwlink/?LinkId=5689) Visual Basic 6 설명서에서) (참조 "를 사용 하 여 the Microsoft 계층적 계층적 커서를 표시 하는 쿼리와 Flexgrid 컨트롤 "Visual Basic 6 설명서에서)입니다.  
  
 계층적 구조를 탐색 하는 방법에 대 한 내용은 **레코드 집합**, 참조 [계층적 레코드 집합에서 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)합니다.  
  
 구문상 올바른 모양 명령에 대 한 정확한 정보를 참조 하십시오. [형식 문법을](../../../ado/guide/data/formal-shape-grammar.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [기본 데이터 공급자에 명령 발급](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
