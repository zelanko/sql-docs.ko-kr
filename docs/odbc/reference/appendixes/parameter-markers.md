---
title: 매개 변수 표식을 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: df895c9e9956c1fde178824d1e14030246710946
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="parameter-markers"></a>매개 변수 표식
Sql-92 사양에 따라 응용 프로그램은 다음 위치에 매개 변수 표식에 배치할 수 없습니다. 보다 포괄적인 목록에 대 한 SQL 92 사양을 참조 하십시오.  
  
-   에 **선택** 목록  
  
-   두 가지 모두 *식* 에 *비교 조건자*  
  
-   이항 연산자의 피연산자가 모두로  
  
-   첫 번째 및 두 번째 피연산자가 모두로 **BETWEEN** 작업  
  
-   첫 번째 및 세 번째 피연산자로 **BETWEEN** 작업  
  
-   식 및의 첫 번째 값으로는 **IN** 작업  
  
-   단항 피연산자로 + 또는-작업  
  
-   인수로 *집합 함수 참조*  
  
 매개 변수 표식에 대 한 자세한 내용은 SQL 92 사양을 참조 하십시오. 매개 변수에 대 한 자세한 내용은 참조 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)합니다.
