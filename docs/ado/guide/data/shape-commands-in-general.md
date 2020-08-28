---
description: 일반적인 셰이핑 명령
title: Shape 명령 일반 Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], shape commands
ms.assetid: 1fac7831-a187-4b15-9b43-aad380c5556c
author: rothja
ms.author: jroth
ms.openlocfilehash: a982f08323a9e852f555732b290d598412d3a802
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979614"
---
# <a name="shape-commands-in-general"></a>일반적인 셰이핑 명령
데이터 셰이핑은 셰이프 **레코드 집합**의 열, 열이 나타내는 엔터티 간의 관계 및 **레코드 집합이** 데이터로 채워지는 방식을 정의 합니다.  
  
 도형 **레코드 집합** 은 다음과 같은 유형의 열로 구성 될 수 있습니다.  
  
|열 유형|설명|  
|-----------------|-----------------|  
|데이터|쿼리 명령에 의해 반환 되는 **레코드 집합** 의 필드를 데이터 공급자, 테이블 또는 이전에 만든 **레코드 집합**에 반환 합니다.|  
|마치면|*장*이라는 다른 **레코드 집합**에 대 한 참조입니다. 장 열 *에서 부모* -자식 관계를 정의할 수 있습니다. 부모 *-자식* 관계는 chapter 열을 포함 하는 **레코드 집합이** 고 *자식은* 챕터가 나타내는 **레코드 집합** 입니다.|  
|aggregate|열 값은 모든 행 또는 자식 **레코드 집합**의 모든 행에 있는 열에 대해 *집계 함수* 를 실행 하 여 파생 됩니다. 집계 함수, [CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)항목의 집계 함수를 참조 하세요.|  
|계산 식|열의 값은 **레코드 집합**의 같은 행에 있는 열에서 Visual Basic for Applications 식을 계산 하 여 파생 됩니다. 식은 CALC 함수에 대 한 인수입니다. [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md) 와 [Visual Basic for Applications 함수](../../../ado/guide/data/visual-basic-for-applications-functions.md)에서 계산 된 식을 참조 하세요.|  
|new|나중에 데이터로 채워질 수 있는 비어 있고 미리 구성한 필드입니다. 열은 NEW 키워드를 사용 하 여 정의 됩니다. [집계 함수, CALC 함수 및 New 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)항목의 new 키워드를 참조 하세요.|  
  
 셰이프 명령에는 **레코드 집합** 개체를 반환 하는 기본 데이터 공급자에 대 한 쿼리 명령을 지정 하는 절이 포함 될 수 있습니다. 쿼리의 구문은 기본 데이터 공급자의 요구 사항에 따라 달라 집니다. 이는 ADO에서 특정 쿼리 언어를 사용할 필요가 없더라도 일반적으로 SQL입니다.  
  
 셰이프 명령은 **레코드 집합** 개체에서 실행 하거나 [명령](../../../ado/reference/ado-api/command-object-ado.md) 개체의 [CommandText](../../../ado/reference/ado-api/commandtext-property-ado.md) 속성을 설정한 다음 Execute 메서드를 호출 하 여 [실행할](../../../ado/reference/ado-api/execute-method-ado-command.md) 수 있습니다.  
  
 SQL JOIN 절을 사용 하 여 두 테이블을 연결할 수 있습니다. 그러나 계층적 **레코드 집합** 은 정보를 보다 효율적으로 나타낼 수 있습니다. 조인에 의해 생성 된 **레코드 집합** 의 각 행은 테이블 중 하나에서 중복 된 정보를 반복 합니다. 계층적 **레코드 집합** 에는 여러 자식 **레코드 집합** 개체에 대해 하나의 부모 **레코드** 집합만 있습니다.  
  
 셰이프 명령은 중첩 될 수 있습니다. 즉, *부모* 명령 또는 *자식 명령은* 다른 셰이프 명령 일 수 있습니다.  
  
 사용자가 **Aduseserver**의 커서 위치를 지정 하는 경우에도 셰이프 공급자는 항상 클라이언트 커서를 반환 합니다.  
  
 프로그래밍 방식으로 또는 적절 한 시각적 컨트롤을 통해 모양을 지정 하는 **레코드** **집합의 구성 요소** 에 액세스할 수 있습니다.  
  
 Microsoft는 shape 명령을 생성 하는 시각적 도구를 제공 합니다 (Visual Basic 6 설명서의 [데이터 환경 디자이너](https://go.microsoft.com/fwlink/?LinkId=5689) 참조). 그리고 계층적 커서를 표시 하는 다른 도구를 제공 합니다 (Visual Basic 6 설명서의 "Microsoft 계층적 Flexgrid 컨트롤 사용" 참조).  
  
 계층적 **레코드 집합**을 탐색 하는 방법에 대 한 자세한 내용은 [계층적 레코드 집합의 행에 액세스](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)를 참조 하세요.  
  
 구문상 올바른 shape 명령에 대 한 정확한 정보는 [공식 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)을 참조 하세요.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [집계 함수, CALC 함수 및 NEW 키워드](../../../ado/guide/data/aggregate-functions-the-calc-function-and-the-new-keyword.md)  
  
-   [기본 데이터 공급자에 명령 발급](../../../ado/guide/data/issuing-commands-to-the-underlying-data-provider.md)
