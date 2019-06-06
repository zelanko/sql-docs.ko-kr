---
title: 커서 (ADO) 유형의 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- cursors [ADO], types
ms.assetid: 7cc01544-e814-403b-bbfe-a2750bf921bd
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 717229c9645384477b89e67b569c15179e9f3bc5
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2019
ms.locfileid: "66704911"
---
# <a name="types-of-cursors-ado"></a>커서 형식(ADO)
일반적으로 응용 프로그램에서는 필요한 데이터 액세스를 제공 하는 가장 간단한 커서를 사용 해야 합니다. 향상 된 기능 (정방향 전용, 읽기 전용, 정적, 스크롤, 버퍼링 되지 않은) 각 추가 커서 특징을 가격-클라이언트 메모리, 네트워크 부하 또는 성능을 있습니다. 대부분의 경우 기본 커서 옵션 응용 프로그램에 실제로 필요한 것 보다 더 복잡 한 커서를 생성 합니다.  
  
 커서 유형 선택에 따라 달라 집니다 응용 프로그램에서 결과 집합을 사용 하는 방법 또한 결과 집합 사용 될 데이터의 비율, 데이터 변경 및 응용 프로그램 성능에 대 한 민감도의 크기를 비롯 한 여러 디자인 고려 사항, 요구 사항입니다.  
  
 기본적으로, 커서 선택 변경 하거나 단순히 데이터를 확인 해야 하는지 여부에 따라 달라 집니다.  
  
-   결과 하지만 하지 변경 데이터의 집합을 통해 스크롤할 하기만 하는 경우 사용 하 여는 [정방향](../../../ado/guide/data/forward-only-cursors.md) 또는 [정적](../../../ado/guide/data/static-cursors.md) 커서입니다.  
  
-   사용 하 여 큰 결과 집합을 행 몇 개만 선택 해야 하는 경우는 [keyset](../../../ado/guide/data/keyset-cursors.md) 커서입니다.  
  
-   동기화 하려는 경우 결과 집합을 최신 추가, 변경 및 모든 동시 사용자가 삭제 된 [동적](../../../ado/guide/data/dynamic-cursors.md) 커서입니다.  
  
 각 커서 유형을 구분 되어야 하는 것 처럼 보이지만, 이러한 커서 유형에 훨씬 다양 한 종류 겹치는 특성 및 옵션의 결과를 염두에서에 둡니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [고정 커서](../../../ado/guide/data/static-cursors.md)  
  
-   [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)  
  
-   [동적 커서](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>관련 항목  
 [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)   
 [동적 커서](../../../ado/guide/data/dynamic-cursors.md)
