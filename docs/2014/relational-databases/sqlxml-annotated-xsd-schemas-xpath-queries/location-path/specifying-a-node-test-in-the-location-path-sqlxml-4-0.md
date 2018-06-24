---
title: 위치 경로 (SQLXML 4.0)에서 노드 테스트 지정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- XPath queries [SQLXML], location paths
- principal node types [SQLXML]
- node tests [SQLXML]
- location path for XPath query
ms.assetid: f46c30bf-1e24-4435-9ac2-f8ba43a8ff94
caps.latest.revision: 20
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ca3eff7a8d915588d632dc12ff94e42d946d8aad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079477"
---
# <a name="specifying-a-node-test-in-the-location-path-sqlxml-40"></a>위치 경로에 노드 테스트 지정(SQLXML 4.0)
  노드 테스트는 위치 단계에서 선택되는 노드 유형을 지정합니다. 모든 축(`child`, `parent`, `attribute` 또는 `self`)에는 주 노드 유형이 있습니다. 에 대 한는 `attribute` 축의 주 노드 유형은입니다  **\<특성 >** 합니다. 에 대 한는 `parent`, `child`, 및 `self` 축의 주 노드 유형은입니다  **\<요소 >** 합니다.  
  
> [!NOTE]  
>  와일드카드 노드 테스트 *(예: `child::*`)는 지원되지 않습니다.  
  
## <a name="node-test-example-1"></a>노드 테스트: 예 1  
 위치 경로 `child::Customer` 선택  **\<고객 >** 컨텍스트 노드의 요소 자식이 있습니다.  
  
 이 예에서는 `child`가 축이고 `Customer`가 노드 테스트입니다. 에 대 한 주 노드 종류는 `child` 축은  **\<요소 >** 합니다. 따라서 노드 테스트 이면 TRUE는  **\<고객 >** 노드는  **\<요소 >** 노드. 컨텍스트 노드에서 없는 경우  **\<고객 >** 자녀는 빈 노드 집합이 반환 됩니다.  
  
## <a name="node-test-example-2"></a>노드 테스트: 예제 2  
 위치 경로 `attribute::CustomerID` 선택은 **CustomerID** 컨텍스트 노드의 특성입니다.  
  
 이 예에서는 `attribute`가 축이고 `CustomerID`가 노드 테스트입니다. 주 노드 종류는 `attribute` 축은  **\<특성 >** 합니다. 따라서 노드 테스트 이면 TRUE **CustomerID** 는  **\<특성 >** 노드. 컨텍스트 노드에서 없는 경우 **CustomerID**, 빈 노드 집합이 반환 됩니다.  
  
> [!NOTE]  
>  이 XPath 구현에서는 위치 단계에서 참조 하는 경우에  **\<요소 >** 또는  **\<특성 >** 오류가 생성 되는 스키마에서 선언 되지 않은 형식입니다. 이 동작은 빈 노드 집합을 반환하는 MSXML에서의 XPath 구현과는 다릅니다.  
  
## <a name="abbreviated-syntax-for-the-axes"></a>축의 축약형 구문  
 위치 경로에 대한 다음 축약형 구문이 지원됩니다.  
  
-   `attribute::`는 `@` 기호로 축약할 수 있습니다.  
  
     위치 경로 `Customer[@CustomerID="ALFKI"]`는 `child::Customer[attribute::CustomerID="ALFKI"]`와 같습니다.  
  
-   `child::`는 위치 단계에서 생략할 수 있습니다.  
  
     따라서 기본 축은 `child`이고, 위치 경로 `Customer/Order`는 `child::Customer/child::Order`와 같습니다.  
  
-   `self::node()`는 한 개의 마침표(.)로 축약할 수 있으며, `parent::node()`는 두 개의 마침표(..)로 축약할 수 있습니다.  
  
  