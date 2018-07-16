---
title: DirectQuery 디자인 모드 (SSAS 테이블 형식)를 사용 하도록 설정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 93b95dc39c0efb088003af9d5fb8b68cfce11ce9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37310413"
---
# <a name="enable-directquery-design-mode-ssas-tabular"></a>DirectQuery 디자인 모드를 사용하도록 설정(SSAS 테이블 형식)
  DirectQuery 모드에서 모델을 만들려면 먼저 DirectQuery 모드 사용자를 지원하도록 디자인 타임 환경을 변경해야 합니다. 이렇게 하면 디자이너에서 다음과 같은 작업이 수행됩니다.  
  
-   DirectQuery 배포 속성을 사용하도록 설정합니다.  
  
-   작업 영역 데이터베이스를 디자인에 캐시를 사용하는 혼합 모드에서 실행되도록 변경합니다. 실제로 모델을 배포할 때는 모드가 프로젝트 배포 속성에 지정한 값으로 다시 변경됩니다.  
  
-   DirectQuery 모드와 호환되지 않는 디자인 기능을 사용하지 않도록 설정합니다.  
  
-   기존 모델의 유효성을 검사합니다.  
  
 이 절차에서는 디자이너에서 DirectQuery 모드를 사용하도록 설정하는 방법에 대해 설명합니다.  
  
### <a name="to-enable-use-of-directquery-in-a-model"></a>모델에서 DirectQuery를 사용하도록 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 솔루션 파일을 엽니다.  
  
2.  개체 탐색기에서 Model.bim 파일을 두 번 클릭합니다.  
  
3.  **속성** 창에서 **DirectQueryMode**속성을 **On**으로 변경합니다.  
  
4.  오류가 발생하면 Visual Studio에서 **오류 목록** 을 열고 모델을 DirectQuery 모드로 전환할 수 없도록 하는 문제를 해결합니다.  
  
## <a name="see-also"></a>관련 항목  
 [DirectQuery 모드 &#40;&AMP;#40;SSAS 테이블 형식&#41;](directquery-mode-ssas-tabular.md)  
  
  
