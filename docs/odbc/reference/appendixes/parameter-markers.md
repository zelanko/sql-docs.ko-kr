---
title: 매개 변수 표식 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.openlocfilehash: acb8d5f9687798bc0efa514ee8646b16140fcd36
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100577"
---
# <a name="parameter-markers"></a>매개 변수 표식
SQL-92 사양에 따라 응용 프로그램은 다음 위치에 매개 변수 표식을 추가할 수 없습니다. 보다 포괄적인 목록은 SQL-92 사양을 참조 하십시오.  
  
-   **SELECT** 목록에서  
  
-   *비교 조건자* 의 두 *식* 으로  
  
-   이항 연산자의 두 피연산자로  
  
-   **BETWEEN** 작업의 첫 번째 피연산자와 두 번째 피연산자 모두로  
  
-   **BETWEEN** 작업의 첫 번째 피연산자와 세 번째 피연산자 모두로  
  
-   식과 **IN** 작업의 첫 번째 값 모두로  
  
-   단항 + 또는-연산의 피연산자로  
  
-   *집합 함수 참조* 의 인수로  
  
 매개 변수 표식에 대 한 자세한 내용은 SQL-92 사양을 참조 하십시오. 매개 변수에 대 한 자세한 내용은 [문 매개 변수](../../../odbc/reference/develop-app/statement-parameters.md)를 참조 하세요.
