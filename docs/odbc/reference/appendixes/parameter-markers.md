---
title: 매개 변수 마커 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: 132473de586094f79dd34c999d44f6dd59aefaef
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303574"
---
# <a name="parameter-markers"></a>매개 변수 표식
SQL-92 사양에 따라 응용 프로그램은 다음 위치에 매개 변수 마커를 배치할 수 없습니다. 보다 포괄적인 목록은 SQL-92 사양을 참조하십시오.  
  
-   **SELECT** 목록에서  
  
-   *비교 조건자에서* 두 *식으로*  
  
-   바이너리 연산자의 두 가지 로서  
  
-   **사이** 작업의 첫 번째 및 두 번째 히연으로  
  
-   **사이** 작업의 첫 번째 및 세 번째 시연으로  
  
-   **IN** 연산의 식과 첫 번째 값 모두  
  
-   unary + 또는 - 작업의 진연으로  
  
-   *세트 함수 참조의* 인수로  
  
 매개 변수 마커에 대한 자세한 내용은 SQL-92 사양을 참조하십시오. 매개 변수에 대한 자세한 내용은 [문 매개 변수 를](../../../odbc/reference/develop-app/statement-parameters.md)참조하십시오.
