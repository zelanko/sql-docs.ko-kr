---
title: 설정 또는 DirectQuery에 대 한 기본 연결 방법 변경 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: f10d5678-d678-4251-8cce-4e30cfe15751
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f5c4e2c19fb768849c3418874b4f1a831fae858c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48186693"
---
# <a name="set-or-change-the-preferred-connection-method-for-directquery"></a>DirectQuery의 기본 연결 방법 설정 또는 변경
  DirectQuery 모드에서 사용할 모델을 만들 때는 먼저 디자인 환경에서 DirectQuery 사용을 지원하도록 구성해야 합니다. 이렇게 하려면 참조 [DirectQuery 디자인 모드를 사용 하도록 설정 &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)합니다.  
  
 모델을 배포할 준비가 되면 사용자가 DirectQuery 모드 중 하나를 사용하여 모델에 액세스할 수 있도록 다음과 같이 몇 가지 추가 속성을 설정해야 합니다.  
  
-   모델에 대한 쿼리에서 캐시된 데이터를 사용할지 아니면 관계형 데이터 원본을 사용할지를 나타내야 합니다. 혼합 모드 또는 DirectQuery 전용을 사용할 수 있습니다.  
  
-   파티션을 사용하는 경우 DirectQuery 데이터 원본으로 사용할 파티션을 나타내야 합니다.  
  
-   SQL Server 데이터 원본에 액세스할 사용자를 위한 가장 옵션을 설정해야 합니다.  
  
 이 절차에서는 디자이너에서 DirectQuery 모델의 기본 연결 방법을 설정하는 방법을 설명합니다. 또한 모델을 배포한 후 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 이 속성을 변경하는 방법도 설명합니다.  
  
### <a name="to-set-the-preferred-connection-method-for-a-directquery-model"></a>DirectQuery 모델의 기본 연결 방법을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], DirectQuery 모델에 대 한 솔루션 파일을 엽니다.  
  
2.  Visual Studio의 **프로젝트** 메뉴에서 **속성**을 선택합니다.  
  
3.  **속성** 창에서 **DirectQueryMode**속성을 다음과 같이 DirectQuery 사용을 지원하는 값 중 하나로 변경합니다.  
  
    -   **InMemory with DirectQuery**: 이 옵션을 사용하면 모델이 배포되지만 모델에 대해 쿼리를 실행하기 전에 캐시를 처리해야 합니다.  
  
    -   **DirectQuery with InMemory**: 이 옵션을 사용하면 캐시가 이미 처리된 경우 클라이언트에서 캐시를 사용할 수 있습니다. 이 설정으로 모델을 배포하고 캐시를 처리하지 않으면 일부 클라이언트에서 모델에 연결하려고 할 때 오류가 발생합니다.  
  
    -   **DirectQuery only**: 이 옵션을 사용하면 메타데이터가 배포되지만 모델에는 데이터가 포함되지 않습니다. 클라이언트에서 InMemory 모드를 사용하여 연결하려고 하면 모델이 없거나 처리되지 않았다는 오류가 발생합니다.  
  
4.  오류가 발생하면 Visual Studio에서 **오류 목록** 을 열고 DirectQuery 모드에서 모델을 배포할 수 없도록 하는 문제를 해결합니다.  
  
### <a name="to-verify-or-change-the-preferred-connection-method-for-a-directquery-model"></a>DirectQuery 모델의 기본 연결 방법을 확인하거나 변경하려면  
  
1.  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 DirectQuery 모델을 배포한 인스턴스에 연결합니다.  
  
2.  model 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다.  
  
3.  **속성** 창에서 **DirectQueryMode**속성을 다음 값 중 하나로 변경합니다.  
  
    -   **DirectQuery 전용**  
  
    -   **InMemory with DirectQuery**  
  
    -   **DirectQuery with InMemory**  
  
 이러한 속성은 Visual Studio에서 배포 전에 프로젝트에 대해 설정한 속성과 동일합니다. DirectQuery 사용을 지원하도록 모델을 구성한 경우 언제든지 DirectQuery 모드의 기본 연결 모드를 변경할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [DirectQuery 디자인 모드를 사용 하도록 설정 &#40;&AMP;#40;SSAS 테이블 형식&#41;](tabular-models/enable-directquery-mode-in-ssdt.md)  
  
  
