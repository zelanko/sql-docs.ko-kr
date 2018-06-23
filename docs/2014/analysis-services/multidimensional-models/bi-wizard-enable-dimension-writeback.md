---
title: 차원 쓰기 저장을 사용 하도록 설정 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- modifying dimensions
- writeback [Analysis Services], setting up
- dimensions [Analysis Services], Business Intelligence enhancements
- Business Intelligence enhancements [Analysis Services], writeback
- dimensions [Analysis Services], writeback
- writeback [Analysis Services]
- dimensions [Analysis Services], modifying
- manual dimension structure modifications
ms.assetid: a4b5eb5a-366d-4fc8-ad0d-5bdb8e7b4163
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a05010b2f102170b64df13e4eb079dde8fbe325
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185519"
---
# <a name="enable-dimension-writeback"></a>차원 쓰기 저장(writeback) 설정
  큐브나 차원에 차원 쓰기 저장 기능을 추가하면 수동으로 차원 구조와 멤버를 수정할 수 있습니다. 쓰기 가능 차원에 대한 업데이트는 차원 테이블에 직접 기록됩니다. 이 기능은 차원의 `WriteEnabled` 속성 설정을 변경합니다.  
  
 차원에 쓰기 저장 기능을 추가하려면 비즈니스 인텔리전스 마법사의 **기능 선택** 페이지에서 **차원 쓰기 저장(writeback) 설정** 옵션을 선택합니다. 그런 다음 마법사의 안내를 따라 차원 쓰기 저장을 적용할 차원을 선택하고 선택한 차원에 대해 이 옵션을 설정합니다.  
  
> [!NOTE]  
>  쓰기 저장은 SQL Server 관계형 데이터베이스 및 데이터 마트에 대해서만 지원됩니다.  
  
## <a name="selecting-a-dimension"></a>차원 선택  
 마법사의 첫 번째 **차원 쓰기 저장(writeback) 설정** 페이지에서 차원 쓰기 저장을 적용할 차원을 지정합니다. 선택한 차원에 차원 쓰기 저장 기능을 추가하면 차원이 변경됩니다. 이러한 변경 내용은 선택된 차원을 포함하는 모든 큐브에 상속됩니다.  
  
## <a name="setting-dimension-writeback-capability"></a>차원 쓰기 저장(Writeback) 기능 설정  
 마법사의 두 번째 **차원 쓰기 저장(writeback) 설정** 페이지에서 실제로 **차원에 쓰기 저장(writeback) 설정** 옵션을 설정합니다. 이 옵션을 선택 하면 자동으로 설정 하는 `WriteEnabled` 차원의 속성 `True`합니다. 이 옵션을 자동으로 취소 속성을 설정 `False`합니다.  
  
## <a name="remarks"></a>Remarks  
 새 멤버를 만들 때 차원에 모든 특성을 포함해야 합니다. 차원의 키 특성 값을 지정하지 않고 멤버를 삽입할 수 없습니다. 따라서 멤버를 만들 때는 차원 테이블에 정의된 모든 제약 조건(예: Null이 아닌 키 값)이 적용됩니다. 지정 된 열과 같은 차원 속성에 의해 선택적으로 지정 된 고려해 야는 `CustomRollupColumn`, `CustomRollupPropertiesColumn` 또는 `UnaryOperatorColumn` 차원 속성입니다.  
  
> [!WARNING]  
>  SQL Azure를 데이터 원본으로 사용하여 Analysis Services에 쓰기 저장(writeback)을 수행할 경우 작업이 실패합니다. MARS(Multiple Active Result Set)를 활성화하는 공급자 옵션이 기본적으로 설정되어 있지 않기 때문에 이 작업이 실패하는 것입니다.  
>   
>  이 문제를 해결하려면 연결 문자열에 MARS를 지원하고 쓰기 저장(writeback)을 활성화하는 다음 설정을 추가합니다.  
>   
>  `"MultipleActiveResultSets=True"`  
>   
>  자세한 내용은 [MARS&#40;Multiple Active Result Sets&#41; 사용](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [쓰기 가능 차원](../multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md)  
  
  