---
title: 매개 변수 값의 배열 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb9389c769e3a7bb0c39959a559531e8051a7bec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298804"
---
# <a name="arrays-of-parameter-values"></a>매개 변수 값 배열
응용 프로그램에서 매개 변수 배열을 전달하는 것이 유용한 경우가 많습니다. 예를 들어 매개 변수 배열과 매개 변수화된 **INSERT** 문을 사용하여 응용 프로그램은 한 번에 여러 행을 삽입할 수 있습니다. 배열을 사용하면 몇 가지 이점이 있습니다. 첫째, 많은 문에 대한 데이터가 단일 패킷으로 전송되므로 네트워크 트래픽이 줄어듭니다(데이터 원본이 기본적으로 매개 변수 배열을 지원하는 경우). 둘째, 일부 데이터 원본은 동일한 수의 별도의 SQL 문을 실행하는 것보다 더 빠르게 배열을 사용하여 SQL 문을 실행할 수 있습니다. 마지막으로, 데이터가 배열에 저장되는 경우, 종종 화면 데이터의 경우와 마찬가지로 응용 프로그램은 **SQLBindParameter에** 대한 단일 호출로 특정 열의 모든 행을 바인딩하고 단일 문을 실행하여 업데이트 할 수 있습니다.  
  
 안타깝게도 매개 변수 배열을 지원하는 데이터 원본은 많지 않습니다. 그러나 드라이버는 각 매개 변수 값 집합에 대해 SQL 문을 한 번 실행하여 매개 변수 배열을 에뮬레이트할 수 있습니다. 이로 인해 드라이버가 각 매개 변수 집합에 대해 한 번 실행하려는 문을 준비할 수 있으므로 속도가 빨라지날 수 있습니다. 또한 더 간단한 응용 프로그램 코드로 이어질 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
