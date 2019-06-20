---
title: 마법사를 사용하여 모델 배포 패키지 배포 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], deploying
- models [Master Data Services], deploying a package
ms.assetid: 4f65dc60-0ff8-46e6-9988-5bc5b9603ad0
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8cc48c9015edf14ebdf67d767ca7bb6c928a7d2f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65477351"
---
# <a name="deploy-a-model-deployment-package-by-using-the-wizard"></a>마법사를 사용하여 모델 배포 패키지 배포

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 모델 배포 마법사를 사용하여 모델 개체만 포함된 패키지를 배포할 수 있습니다. 데이터가 포함된 패키지를 배포해야 하는 경우 [MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  패키지는 해당 패키지를 만드는 데 사용한 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에만 배포할 수 있습니다. 따라서 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에서 만든 패키지는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]에 배포할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   대상 **환경의** 시스템 관리 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 배포 패키지가 있어야 합니다. 자세한 내용은 [마법사를 사용하여 모델 배포 패키지 만들기](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)를 참조하세요.  
  
-   모델을 배포하는 환경에서 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
### <a name="to-deploy-a-model-deployment-package-of-model-objects-only"></a>모델 개체의 모델 배포 패키지만 배포하려면  
  
1.  [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]에서 **시스템 관리**를 클릭합니다.  
  
2.  **모델 뷰** 페이지의 메뉴 모음에서 **시스템** 을 가리키고 **배포**를 클릭합니다.  
  
3.  **모델 배포 마법사**에서 **배포**를 클릭합니다.  
  
4.  **찾아보기**를 클릭합니다.  
  
5.  배포 패키지(.pkg 파일)를 찾은 다음 **열기**를 클릭합니다.  
  
6.  **다음**을 클릭합니다.  
  
7.  패키지가 로드되면 **다음**을 클릭합니다.  
  
8.  모델이 이미 있는 경우 **기존 모델 업데이트**를 선택하여 해당 모델을 업데이트할 수 있습니다. 새 모델을 만들려는 경우 **새 모델 만들기** 를 선택하고 **다음** 을 클릭하면 새 모델의 이름을 입력할 수 있습니다.  
  
9. **마침** 을 클릭하여 마법사를 끝냅니다.  
  
 **참고:**  
  
-   패키지의 구독 보기가 기존 모델의 구독 보기 이름과 동일한 경우 다음 경고가 표시됩니다. **배포자 구독 보기의 이름이 바뀌었습니다**. 또한 *modelname.subscriptionviewname*(으)로 뷰가 만들어집니다. 이 이름이 이미 사용 중이면 구독 뷰가 만들어지지 않습니다.  
  
-   배포 프로세스는 다음과 같은 4단계로 진행됩니다.  
  
    1.  모델 개체가 만들어집니다.  
  
    2.  구독 뷰가 만들어집니다.  
  
    3.  비즈니스 규칙이 만들어집니다.  
  
-   새 모델 또는 복제된 모델을 만들 때 단계 실행 중 프로세스가 실패하면 모델이 삭제됩니다.  
  
     모델을 업데이트할 때 처음 3단계 동안 프로세스가 실패하면 해당 단계 다음으로 진행되지 않습니다. 그러나 이미 수행한 변경 내용은 롤백되지 않습니다.  
  
## <a name="next-steps"></a>다음 단계  
 파일 특성, 사용자 및 그룹 권한은 모델 배포 패키지에 포함되지 않습니다. 모델을 배포한 후에 이러한 항목을 수동으로 업데이트해야 합니다. 참조 항목:  
  
-   [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>관련 항목  
 [모델 배포&#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
