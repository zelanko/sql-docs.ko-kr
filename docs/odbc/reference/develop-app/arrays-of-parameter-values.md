---
description: 매개 변수 값 배열
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 230f15f1c9cae0509ba7d616ab61ed5d8d7a370b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483116"
---
# <a name="arrays-of-parameter-values"></a>매개 변수 값 배열
응용 프로그램에서 매개 변수 배열을 전달 하는 것이 유용한 경우가 많습니다. 예를 들어 매개 변수 배열과 매개 변수가 있는 **INSERT** 문을 사용 하는 경우 응용 프로그램은 한 번에 여러 행을 삽입할 수 있습니다. 배열을 사용 하는 경우 몇 가지 이점이 있습니다. 첫째, 대부분의 문에 대 한 데이터가 단일 패킷으로 전송 되기 때문에 (데이터 원본이 기본적으로 매개 변수 배열을 지 원하는 경우) 네트워크 트래픽이 줄어듭니다. 둘째, 일부 데이터 소스는 동일한 수의 개별 SQL 문을 실행 하는 것 보다 빠르게 배열을 사용 하 여 SQL 문을 실행할 수 있습니다. 마지막으로 데이터가 배열에 저장 될 때 화면 데이터의 경우 처럼 응용 프로그램은 **SQLBindParameter** 에 대 한 단일 호출로 특정 열의 모든 행을 바인딩하고 단일 문을 실행 하 여 업데이트할 수 있습니다.  
  
 아쉽게도 많은 데이터 원본이 매개 변수 배열을 지원 하지는 않습니다. 그러나 드라이버는 각 매개 변수 값 집합에 대해 SQL 문을 한 번 실행 하 여 매개 변수 배열을 에뮬레이트할 수 있습니다. 이렇게 하면 드라이버는 각 매개 변수 집합에 대해 한 번씩 실행 하려는 문을 준비할 수 있으므로 속도가 향상 될 수 있습니다. 또한 응용 프로그램 코드를 더 간단 하 게 만들 수 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [매개 변수 배열 바인딩](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [매개 변수 배열 사용](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
