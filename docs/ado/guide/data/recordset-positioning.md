---
title: "레코드 집합 위치 지정 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe94f3a39a42bedd5bd3d1569e5210320b1e7c4f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="recordset-positioning"></a>레코드 집합 위치 지정
사용 하 여는 **AbsolutePosition** 레코드로 이동 하는 속성의 서 수 위치에 따라는 **레코드 집합** 개체 또는 현재 레코드의 서 수 위치를 결정 합니다. 공급자는이 속성을 사용할 수에 대 한 적절 한 기능을 지원 해야 합니다.  
  
 **AbsolutePosition** 는 1부터 시작 하 고 현재 레코드의 첫 번째 레코드는 경우는 **레코드 집합**합니다. 앞에서 설명한 대로 있는 레코드의 총 수를 가져올 수 있습니다는 **레코드 집합** 에서 개체는 **RecordCount** 속성입니다.  
  
 설정 하는 경우는 **AbsolutePosition** 속성, 현재 캐시에서 레코드를가 하는 경우에 ADO 캐시를 다시 로드와 지정한 레코드부터 시작 하는 레코드의 새로운 그룹입니다. **CacheSize** 속성이이 그룹의 크기를 결정 합니다.  
  
> [!NOTE]
>  사용 하지 않아야는 **AbsolutePosition** 속성으로 서로게이트 레코드 번호입니다. 지정된 된 레코드의 위치는 이전 레코드를 삭제 하는 경우 변경 됩니다. 또한 없는 확신할 수 같은 특정된 레코드 가질 수 없습니다 **AbsolutePosition** 경우는 **레코드 집합** 개체가 쿼리가 다시 실행 또는 다시 열입니다. 책갈피는 유지 하 고 지정된 된 위치를 반환 하는 권장된 방법 및 모든 종류의에서 위치를 지정 하는 유일한 방법은 **레코드 집합** 개체입니다.
