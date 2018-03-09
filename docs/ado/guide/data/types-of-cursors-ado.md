---
title: "종류의 커서 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3ec8ccca017236a8f6aa784d92e8304a98452f02
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="types-of-cursors-ado"></a>(ADO) 커서 유형
일반적으로 응용 프로그램에서는 필요한 데이터 액세스를 제공 하는 가장 간단한 커서를 사용 해야 합니다. 각 추가 커서 특징 (정방향 전용, 읽기 전용, 정적, 스크롤, 버퍼링) 기본적인 사항 보다 않음과 같은-클라이언트 메모리, 네트워크 부하 또는 성능입니다. 대부분의 경우 기본 커서 옵션에는 응용 프로그램에 실제로 필요한 것 보다 더 복잡 한 커서를 생성 합니다.  
  
 응용 프로그램은 결과 집합을 사용 하는 방법 뿐만 아니라 결과 집합, 사용 되는 데이터의 비율, 데이터 변경 및 응용 프로그램 성능에 대 한 민감도의 크기를 비롯 한 몇 가지 디자인 고려 사항, 달라 커서 유형 선택에 따라 달라 집니다. 요구 사항입니다.  
  
 가장 기본적으로 커서 선택 변경 하거나 데이터를 확인할 해야 하는지 여부에 따라 달라 집니다.  
  
-   사용 하 여 결과 얻으려면 되는데 이때 데이터는 변경 하지는 집합을 통해 스크롤하여 하기만 하는 경우는 [앞 으로만 이동 가능한](../../../ado/guide/data/forward-only-cursors.md) 또는 [정적](../../../ado/guide/data/static-cursors.md) 커서입니다.  
  
-   사용 하 여 큰 결과 집합 및 몇 개의 행을 선택 해야 하는 경우는 [키 집합](../../../ado/guide/data/keyset-cursors.md) 커서입니다.  
  
-   사용 하 여 동기화 하려는 경우 결과 집합을 최근 추가, 변경 및 삭제 모든 동시 사용자가을 [동적](../../../ado/guide/data/dynamic-cursors.md) 커서입니다.  
  
 각 커서 유형을 구분 되어야 하는 것 처럼 보이지만, 이러한 커서 유형에 없는지 다른 종류 훨씬 겹치는 특성 및 옵션의 결과를 염두에서에 둬야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [고정 커서](../../../ado/guide/data/static-cursors.md)  
  
-   [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)  
  
-   [동적 커서](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>관련 항목:  
 [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)   
 [동적 커서](../../../ado/guide/data/dynamic-cursors.md)
