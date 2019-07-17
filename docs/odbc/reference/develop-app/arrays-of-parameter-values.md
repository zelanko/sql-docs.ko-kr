---
title: 매개 변수 값의 배열 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e65928cd078a3f05032f4e4fb400e3e2eb1f27a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68077068"
---
# <a name="arrays-of-parameter-values"></a>매개 변수 값 배열
응용 프로그램 매개 변수 배열을 전달 하는 것이 유용 합니다. 예를 들어, 매개 변수 및 매개 변수가 있는 배열을 사용 하 여 **삽입** 문을 응용 프로그램은 행 개수를 한 번에 삽입할 수 있습니다. 배열을 사용 하면 여러 이점이 있습니다. 먼저 (데이터 원본에 매개 변수 배열 고유 하 게 지 원하는) 경우 많은 문에 대 한 데이터를 단일 패킷으로 전송 되기 때문에 네트워크 트래픽이 감소 됩니다. 둘째, 일부 데이터 원본은 동일한 수의 별도 SQL 문 실행할 때 보다 더 빠르게 배열을 사용 하 여 SQL 문을 실행할 수 있습니다. 마지막으로 데이터를 저장할 경우 배열에 있는 경우가 화면 데이터용으로, 응용 프로그램을에서 바인딩할 수의 모든 행에 대 한 단일 호출을 사용 하 여 특정 열 **SQLBindParameter** 단일 문을 실행 하 여 업데이트 합니다.  
  
 아쉽게도 많지 데이터 원본 매개 변수 배열을 지원 합니다. 그러나 드라이버는 매개 변수 값 집합 각각에 대해 한 번 SQL 문을 실행 하 여 매개 변수 배열을 에뮬레이트할 수 있습니다. 이 드라이버 문을 각 매개 변수 집합에 대 한 두 번 실행 계획을 준비해 수 때문에 속도가 증가 될 수 있습니다. 간단한 응용 프로그램 코드에는 발생할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
