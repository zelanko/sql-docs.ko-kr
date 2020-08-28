---
description: 레코드로 이동
title: 레코드로 이동 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record jumping [ADO]
- jumping to record [ADO]
ms.assetid: 6caf6299-2eea-4d34-9b0e-b75aab07b740
author: rothja
ms.author: jroth
ms.openlocfilehash: 96987a5c51d7a888672609aa28f3fd223ccfffa1
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980404"
---
# <a name="jumping-to-a-record"></a>레코드로 이동
[Move](../../reference/ado-api/move-method-ado.md) 메서드를 사용 하면 다음 구문을 사용 하 여 레코드 **집합** 에서 지정 된 수의 레코드를 앞 이나 뒤로 이동할 수 있습니다.  
  
```  
oRs.Move NumRecords, Start  
```  
  
## <a name="remarks"></a>설명  
 **Move** 메서드는 모든 **레코드 집합** 개체에서 지원 됩니다.  
  
 *NumRecords* 인수가 0 보다 크면 현재 레코드 위치가 앞으로 이동 합니다 ( **레코드 집합**의 끝까지). *NumRecords* 가 0 보다 작은 경우에는 현재 레코드 위치가 뒤로 이동 하 여 **레코드 집합**의 시작 부분을 향해 이동 합니다.  
  
 **이동** 호출로 인해 현재 레코드 위치가 첫 번째 레코드 앞의 지점으로 이동 하는 경우 ADO는 현재 레코드를 **레코드 집합** 의 첫 번째 레코드 앞의 위치로 설정 합니다 (**BOF** 가 **True**임). **BOF** 속성이 이미 **True 이면** 뒤로 이동 하려고 하면 오류가 생성 됩니다.  
  
 **이동** 호출로 인해 현재 레코드 위치가 마지막 레코드 다음의 지점으로 이동 하는 경우 ADO는 현재 레코드를 **레코드 집합** 에서 마지막 레코드의 위치 (**EOF** 가 **True**임)로 설정 합니다. **EOF** 속성이 이미 **True** 인 경우 앞으로 이동 하려고 하면 오류가 생성 됩니다.  
  
 빈 **레코드 집합** 개체에서 **Move** 메서드를 호출 하면 오류가 발생 합니다.  
  
 *시작* 인수에 책갈피를 전달 하는 경우 레코드 **집합** 개체가 책갈피를 지원 한다고 가정 하 고이 책갈피를 사용 하는 레코드를 기준으로 이동 합니다. [책갈피 속성을](../../reference/ado-api/bookmark-property-ado.md) 사용 하 여 책갈피를 가져옵니다. 지정 하지 않으면 현재 레코드를 기준으로 이동 합니다.  
  
 **CacheSize** 속성을 사용 하 여 공급자의 레코드를 로컬로 캐시 하는 경우 현재 레코드 위치를 캐시 된 레코드의 현재 그룹 외부로 이동 하는 *NumRecords* 인수를 전달 하면 ADO에서 대상 레코드부터 시작 하 여 새 레코드 그룹을 검색 합니다. **CacheSize** 속성은 새로 검색 된 그룹의 크기를 결정 하 고, 대상 레코드는 검색 된 첫 번째 레코드입니다.