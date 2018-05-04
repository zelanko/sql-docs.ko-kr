---
title: 매개 변수 값의 배열 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38dc5fb0ed2286b3077e6198bc978808063b5d2f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="arrays-of-parameter-values"></a>매개 변수 값의 배열
종종 응용 프로그램의 매개 변수 배열을 전달 하는 것이 유용 합니다. 예를 들어, 매개 변수 및 매개 변수가 있는 배열을 사용 하 여 **삽입** 문, 응용 프로그램은 행 수를 한 번에 삽입할 수 있습니다. 배열을 사용 하 여 여러 가지 장점이 있습니다. 첫째, (데이터 원본에서는 기본적으로 매개 변수 배열 지원) 하는 경우 단일 패킷을 많은 문에 대 한 데이터 전송 되므로 네트워크 트래픽이 줄어듭니다. 둘째, 일부 데이터 원본에는 동일한 수의 별도 SQL 문 실행할 때 보다 더 빠르게 배열을 사용 하 여 SQL 문을 실행할 수 있습니다. 마지막으로 사용할 경우는 경우 화면 데이터에 대 한 데이터를 배열에 저장 됩니다, 응용 프로그램 바인딩할 수의 모든 행을 단일 호출 하 여 특정 열에 **SQLBindParameter** 단일 문을 실행 하 여 서버를 업데이트 하 고 있습니다.  
  
 아쉽게도 많지 데이터 원본에는 매개 변수 배열 지원. 그러나, 드라이버는 매개 변수 값 집합 각각에 대해 한 번 SQL 문을 실행 하 여 매개 변수 배열을 에뮬레이트할 수 있습니다. 이 값은 드라이버 각 매개 변수 집합에 대 한 두 번 실행할 계획 하는 문을 준비한 다음 수 때문에 속도의 증가를 발생할 수 있습니다. 또한 응용 프로그램 코드가 단순해 집니다 발생할 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
