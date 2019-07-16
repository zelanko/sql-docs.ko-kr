---
title: 셰이프 일반적 명령 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 09fec8bd07d036fd6a93b8f6bcb54a51a68150fa
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924173"
---
# <a name="shape-commands-in-general"></a>일반적인 셰이핑 명령
모양의 열의 정의 데이터 셰이핑 **Recordset**, 열 및는 방식을 나타내는 엔터티 간의 관계를 **레코드 집합** 데이터로 채워집니다.  
  
 모양의 **레코드 집합** 열에는 다음과 같은 유형의 구성 될 수 있습니다.  
  
|열 유형|설명|  
|-----------------|-----------------|  
|data|필드를 **레코드 집합** 테이블을 데이터 공급자는 쿼리 명령에서 반환 된, 또는 이전에 모양 **레코드 집합**합니다.|  
|장|다른에 대 한 참조가 **레코드 집합**라는 *장*합니다. 장 열 수 있도록 정의 *부모-자식* 관계 위치를 *부모* 은 합니다 **레코드 집합** 장 열을 포함 하는 는*자식* 은 합니다 **레코드 집합** 장 나타내는입니다.|  
|집계(aggregate)|실행 하 여 파생 된 열의 값을 *집계 함수* 모든 행 또는 자식의 모든 행의 열에 **레코드 집합**합니다. (다음 항목에서는 집계 함수를 참조 하세요 [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
|계산된 식|응용 프로그램의 같은 행의 열에는 식에 대 한 Visual Basic을 계산 하 여 열 값 파생 된 **레코드 집합**합니다. 식에는 계산 함수에 인수입니다. (다음 항목에서는 식 계산을 참조 하세요 [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) 고 [Visual Basic for Applications 기능](../../../ado/guide/data/visual-basic-for-applications-functions.md).)|  
|new|빈, 작성 된 필드를 나중에 데이터를 사용 하 여 채울 수 있습니다. NEW 키워드를 사용 하 여 열이 정의 됩니다. (다음 항목에서는 새 키워드를 참조 하세요 [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md).)|  
  
 Shape 명령을 반환 하는 기본 데이터 공급자에는 쿼리 명령을 지정 하는 절을 포함할 수 있습니다는 **레코드 집합** 개체입니다. 쿼리의 구문을 기본 데이터 공급자 요구 사항에 따라 달라 집니다. ADO에서는 모든 특정 쿼리 언어를 사용 하지 않지만 SQL, 일반적으로 됩니다.  
  
 도형 명령에서 발급할 수 있습니다 **레코드 집합** 개체 또는 설정 하 여를 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성을 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체와 호출는 [실행 ](../../../ado/reference/ado-api/execute-method-ado-command.md) 메서드.  
  
 SQL JOIN 절을 사용 하 여 두 테이블에 연결할 수 없습니다. 그러나 계층적 **레코드 집합** 정보를 보다 효율적으로 나타낼 수 있습니다. 각 행을 **레코드 집합** 테이블 중 하나에서 중복 해 서 조인 반복 정보로 생성 합니다. 계층적 **레코드 집합** 하나만 부모가 **레코드 집합** 마다 여러 자식 **레코드 집합** 개체입니다.  
  
 도형 명령을 중첩할 수 있습니다. 즉, 합니다 *부모 명령이* 또는 *자식* 다른 셰이프 명령 자체가 될 수 있습니다.  
  
 사용자의 커서 위치를 지정 하는 경우에 항상 셰이프 공급자 클라이언트 커서를 반환 **가 adUseServer**합니다.  
  
 액세스할 수 있습니다는 **레코드 집합** 구성 요소는 모양의 **레코드 집합** 프로그래밍 방식으로 또는 적절 한 시각적 컨트롤을 통해.  
  
 Microsoft 셰이프 명령을 생성 하는 비주얼 도구를 제공 합니다. (참조를 [데이터 환경 디자이너](https://go.microsoft.com/fwlink/?LinkId=5689) Visual Basic 6 설명서에서) (참조 "를 사용 하 여 the Microsoft 계층적 계층적 커서를 표시 하 고 다른 Flexgrid 컨트롤 "Visual Basic 6 문서의)입니다.  
  
 계층적 탐색에 대 한 자세한 **레코드 집합**를 참조 하세요 [계층적 레코드 집합에서 행 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)합니다.  
  
 구문이 올바른 모양 명령에 대 한 정확한 내용은 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [기본 데이터 공급자에 명령 발급](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
