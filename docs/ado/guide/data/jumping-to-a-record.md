---
title: "레코드 점프 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19a4275d339132db8efd4b09a313b482fc8cb666
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="jumping-to-a-record"></a>레코드로 이동
[이동](../../../ado/reference/ado-api/move-method-ado.md) 메서드를 사용 하면에서 앞 이나 뒤로 이동할 수는 **레코드 집합** 지정된 된 수의 다음 구문을 사용 하 여 레코드:  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>주의  
 **이동** 모든 메서드는 지원 **레코드 집합** 개체입니다.  
  
 경우는 *NumRecords* 인수가 0 보다 큰 레코드의 현재 위치를 앞으로 이동 (이 끝날 무렵는 **레코드 집합**). 경우 *NumRecords* 가 현재 레코드 위치 이동 합니다. 0 보다 작은 (의 시작 부분 쪽는 **레코드 집합**).  
  
 경우는 **이동** 호출 현재 레코드 위치는 첫 번째 레코드 앞에 포인터를 이동, 현재 레코드의 첫 번째 레코드 앞으로 설정 하는 ADO는 **레코드 집합** (**BOF** 은 **True**). 경우에 뒤로 이동 하려는 시도가 **BOF** 속성이 이미 **True** 오류가 발생 합니다.  
  
 경우는 **이동** 호출 지점에 마지막 레코드 뒤에 현재 레코드 위치를 이동 합니다, ADO 설정 된 위치에 있는 마지막 레코드 후의 **레코드 집합** (**EOF** 은 **True**). 경우에 앞으로 이동 하려고는 **EOF** 속성이 이미 **True** 오류가 발생 합니다.  
  
 호출 된 **이동** 메서드는 빈에서 **레코드 집합** 개체에 오류가 발생 합니다.  
  
 책갈피를 전달 하는 경우는 *시작* 인수에이 책갈피와 레코드를 기준으로 이동 가정는 **레코드 집합** 개체 책갈피를 지원 합니다. 책갈피를 사용 하 여 가져온는 [책갈피](../../../ado/reference/ado-api/bookmark-property-ado.md) 속성입니다. 지정 하지 않으면 현재 레코드를 기준으로 이동 합니다.  
  
 사용 하는 경우는 **CacheSize** 속성을 전달 공급자에서 레코드를 로컬로 캐시 한 *NumRecords* 캐시 된 레코드의 현재 그룹 외부 레코드 현재 위치를 이동 하는 인수 하면 ADO 대상 레코드부터 시작 하는 레코드의 새 그룹을 검색 합니다. **CacheSize** 새로 검색된 된 그룹의 크기를 결정 하는 속성 및 대상 레코드는 검색 된 첫 번째 레코드입니다.

