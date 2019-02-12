---
title: 동기화 범위 설정(보고서 작성기 및 SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 6f4a11e6-6151-47be-a43f-e3dbf6c0e737
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 87aa869269b11ce6e3d3c54296ed08861e0406bb
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034764"
---
# <a name="set-synchronization-scope-report-builder-and-ssrs"></a>동기화 범위 설정(보고서 작성기 및 SSRS)
  표시기는 지정된 범위 내에서 전체 표시기 데이터 값 범위를 동기화하여 데이터 값을 나타냅니다. 이 범위는 기본적으로 표시기가 포함된 테이블, 행렬 등 표시기의 상위 컨테이너입니다. 보고서 레이아웃에 따라 표시기 동기화를 변경할 수 있습니다. 예를 들어 테이블 같은 데이터 영역에 행 그룹이 있는 경우 이 그룹을 표시기 범위로 지정할 수 있습니다. 표시기의 동기화를 생략할 수도 있습니다.  
  
 식을 사용하여 단위 등의 옵션을 설정할 수 있습니다. 자세한 내용은 [식&#40;보고서 작성기 및 SSRS&#41;](expressions-report-builder-and-ssrs.md)을 참조하세요.  
  
 보고서 내의 범위를 이해하고 설정하는 방법에 대한 일반적인 내용은 [합계, 집계 및 기본 제공 컬렉션의 식 범위&#40;보고서 작성기 및 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-synchronization-scope-of-an-indicator"></a>표시기의 동기화 범위를 변경하려면  
  
1.  변경할 표시기를 마우스 오른쪽 단추로 클릭하고 **표시기 속성**을 클릭합니다.  
  
2.  왼쪽 창에서 **값 및 상태** 를 클릭합니다.  
  
3.  **동기화 범위** 목록에서 적용할 범위를 클릭합니다.  
  
     **(없음)** 옵션(표시기에서 동기화 범위 제거)은 항상 사용할 수 있고 다른 옵션은 보고서 레이아웃에 따라 달라집니다.  
  
     원하는 경우 **식** 단추(*fx*)를 클릭하여 범위를 설정하는 식을 편집합니다.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>관련 항목  
 [표시기&#40;보고서 작성기 및 SSRS&#41;](indicators-report-builder-and-ssrs.md)  
  
  
