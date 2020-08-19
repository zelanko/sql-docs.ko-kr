---
description: 커서 형식(ADO)
title: 커서 유형 (ADO) | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: ea996827565f0cc6d593078e7772c336699260bf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88452715"
---
# <a name="types-of-cursors-ado"></a>커서 형식(ADO)
일반적으로 응용 프로그램은 필요한 데이터 액세스를 제공 하는 가장 간단한 커서를 사용 해야 합니다. 앞 으로만 이동 가능한 읽기 전용, 정적, 스크롤, 버퍼링 되지 않음 등의 추가 커서 특성에는 가격 책정 클라이언트 메모리, 네트워크 로드 또는 성능이 있습니다. 대부분의 경우 기본 커서 옵션은 응용 프로그램에 실제로 필요한 것 보다 더 복잡 한 커서를 생성 합니다.  
  
 커서 유형 선택은 응용 프로그램에서 결과 집합을 사용 하는 방법 및 결과 집합의 크기, 사용 될 수 있는 데이터의 백분율, 데이터 변경 내용에 대 한 민감도 및 응용 프로그램 성능 요구 사항 등의 몇 가지 디자인 고려 사항에 따라 달라 집니다.  
  
 가장 기본적인 커서 선택은 데이터를 변경 하거나 보기만 해야 하는지 여부에 따라 달라 집니다.  
  
-   결과 집합을 변경 하는 것이 아니라 데이터를 변경 해야 하는 경우 [앞 으로만 이동](../../../ado/guide/data/forward-only-cursors.md) 하거나 [정적](../../../ado/guide/data/static-cursors.md) 커서를 사용 합니다.  
  
-   결과 집합이 크고 몇 개의 행만 선택 해야 하는 경우에는 [키 집합](../../../ado/guide/data/keyset-cursors.md) 커서를 사용 합니다.  
  
-   모든 동시 사용자가 결과 집합을 최근 추가, 변경 및 삭제와 동기화 하려면 [동적](../../../ado/guide/data/dynamic-cursors.md) 커서를 사용 합니다.  
  
 각 커서 유형이 서로 다릅니다. 이러한 커서 유형은 단순히 특성 및 옵션을 겹치게 하는 것과는 다른 종류의 차이가 없다는 점을 명심 해야 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [정방향 전용 커서](../../../ado/guide/data/forward-only-cursors.md)  
  
-   [정적 커서](../../../ado/guide/data/static-cursors.md)  
  
-   [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)  
  
-   [동적 커서](../../../ado/guide/data/dynamic-cursors.md)  
  
## <a name="see-also"></a>참고 항목  
 [앞 으로만 이동 가능한 커서](../../../ado/guide/data/forward-only-cursors.md)   
 [정적 커서](../../../ado/guide/data/static-cursors.md)   
 [키 집합 커서](../../../ado/guide/data/keyset-cursors.md)   
 [동적 커서](../../../ado/guide/data/dynamic-cursors.md)
