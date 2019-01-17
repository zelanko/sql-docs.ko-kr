---
title: MDSModelDeploy를 사용하여 모델 배포 패키지 배포 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: fb2a4df4-5e0d-4b34-818f-383dbde1b15c
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 99e11038cbc7315ff485177f9270e6f0fba74142
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52823697"
---
# <a name="deploy-a-model-deployment-package-by-using-mdsmodeldeploy"></a>MDSModelDeploy를 사용하여 모델 배포 패키지 배포

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 MDSModelDeploy 도구를 사용하여 다음 중 하나를 포함하는 패키지를 배포합니다.  
  
-   모델 개체만  
  
-   모델 개체 및 데이터  
  
 모델 개체만 포함하는 패키지를 배포하려면 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션에서 모델 배포 마법사를 대신 사용할 수 있습니다. 자세한 내용은 [Deploy a Model Deployment Package by Using the Wizard](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  패키지는 해당 패키지를 만드는 데 사용한 버전의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에만 배포할 수 있습니다. 따라서 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] 에서 만든 패키지는 [!INCLUDE[ssSQL14](../includes/sssql14-md.md)] 이상에 배포할 수 없습니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
 이 절차를 수행하려면  
  
-   대상 **환경의** 시스템 관리 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] 기능 영역에 액세스할 수 있는 권한이 있어야 합니다.  
  
-   모델 배포 패키지가 있어야 합니다. 자세한 내용은  [Create a Model Deployment Package by Using MDSModelDeploy](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)를 참조하세요.  
  
-   모델을 배포하는 환경에서 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)에 액세스하지 않고 그룹에서 사용자를 추가하고 제거할 수 있습니다.  
  
-   데이터로 모델을 업데이트하려는 경우 배포하려는 버전을 **잠금** 또는 **커밋됨** 상태로 만들 수 없습니다.  
  
### <a name="to-deploy-a-model-deployment-package"></a>모델 배포 패키지를 배포하려면  
  
1.  새 모델 또는 모델 복제를 배포할지 이전에 복제된 모델을 업데이트할지 여부를 결정합니다. 자세한 내용은 [모델 배포 옵션&#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md)을 참조하세요.  
  
2.  관리자 열기: 명령 프롬프트를 열고 MDSModelDeploy.exe로 이동합니다.  
  
    -   MDS를 기본 위치에 설치하는 경우 도구는 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration에서 사용할 수 있습니다.  
  
    -   MDS를 기본 위치에 설치하지 않은 경우 로컬 컴퓨터에서 MDSModelDeploy.exe를 검색하십시오.  
  
3.  (선택 사항) 보기 옵션 및 도움말입니다.  
  
    -   모든 사용 가능한 옵션을 표시하려면 `MDSModelDeploy` 를 입력하고 Enter 키를 누릅니다.  
  
    -   옵션에 대한 도움말을 표시하려면 *과 같이 입력합니다. 여기서* OptionName `MDSModelDeploy help OptionName`은 옵션의 이름입니다.  
  
4.  (선택 사항) 여러 웹 애플리케이션이 있는 경우 이 명령을 입력하고 Enter 키를 눌러 배포할 서비스의 이름을 결정합니다.  
  
    ```  
    MDSModelDeploy listservices  
    ```  
  
     값의 목록(예: `MDS1, Default Web Site, MDS`)이 반환됩니다. 이 목록의 첫 번째 값(이 경우 `MDS1`)은 모델을 배포하는 데 필요합니다.  
  
5.  모델을 만들지, 복제할지 또는 업데이트할지에 따라 명령 프롬프트에 다음과 같이 입력하고 Enter 키를 누릅니다.  
  
    -   새 모델을 만들려면  
  
        ```  
        MDSModelDeploy deploynew -package PackageName -model ModelName -service ServiceName  
        ```  
  
    -   모델 복제를 만들려면  
  
        ```  
        MDSModelDeploy deployclone -package PackageName  
        ```  
  
    -   기존 모델과 해당 데이터를 업데이트하려면  
  
        ```  
        MDSModelDeploy deployupdate -package PackageName -version VersionName  
        ```  
  
    > [!IMPORTANT]  
    >  MDSModelDeploy 도구를 사용하여 기존 모델 및 해당 데이터를 업데이트하고 패키지에 엔터티, 특성 또는 대상 모델에 있는 멤버를 포함하지 않는 경우 MDSModelDeploy는 모델에서 해당 엔터티, 특성 또는 멤버를 삭제하지 않습니다.  
  
     여기서 *PackageName* 은 패키지 파일(.pkg)의 이름이고, *ModelName* 은 새 모델의 이름이고, *VersionName* 은 버전 이름이고, *ServiceName* 은 이전 단계에서 반환된 서비스의 이름입니다. 모델 및 버전 이름이 대/소문자가 구분되는 이름과 정확하게 일치하는지 확인합니다.  
  
6.  패키지가 성공적으로 배포되면 "MDSModelDeploy 작업이 성공적으로 완료되었습니다."라는 메시지가 표시됩니다.  
  
 **참고:**  
  
-   패키지의 구독 보기가 기존 모델의 구독 보기 이름과 동일한 경우 다음 경고가 표시됩니다. **배포자 구독 보기의 이름이 바뀌고** 보기가 *modelname.subscriptionviewname*으로 생성됩니다. 이 이름이 이미 사용 중이면 구독 뷰가 만들어지지 않습니다.  
  
-   배포 프로세스는 다음과 같은 4단계로 진행됩니다.  
  
    1.  모델 개체가 만들어집니다.  
  
    2.  비즈니스 규칙이 만들어집니다.  
  
    3.  구독 뷰가 만들어집니다.  
  
    4.  마스터 데이터가 채워집니다.  
  
-   새 모델 또는 복제된 모델을 만들 때 단계 실행 중 프로세스가 실패하면 모델이 삭제됩니다.  
  
     모델을 업데이트할 때 처음 3단계 동안 프로세스가 실패하면 진행되지 않습니다. 그러나 이미 수행한 변경 내용은 롤백되지 않습니다. 4단계에서 프로세스가 실패하면 업데이트 가능한 멤버가 업데이트됩니다.  
  
## <a name="next-steps"></a>Next Steps  
 파일 특성, 사용자 및 그룹 권한은 모델 배포 패키지에 포함되지 않습니다. 모델을 배포한 후에 이러한 항목을 수동으로 업데이트해야 합니다. 참조 항목:  
  
-   [모델 개체 사용 권한 할당&#40;Master Data Services&#41;](../master-data-services/assign-model-object-permissions-master-data-services.md)  
  
## <a name="see-also"></a>참고 항목  
 [모델 배포&#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md)  
  
  
