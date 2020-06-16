---
title: 모델 배포
description: 모델 패키지를 배포 하 여 한 MDS(Master Data Services) 환경에서 다른 환경으로 모델 복사본을 이동 하거나 사용자 환경에 새 모델을 만듭니다.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: mds
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- deployment packages [Master Data Services], about deployment packages
- deployment packages [Master Data Services]
ms.assetid: 30085c08-034f-4efe-80fe-408f9091ff5c
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: ef909fd817da4835e9f3d0903a4e8a7f8f1a4658
ms.sourcegitcommit: 7d6eb09588ff3477cf39a8fd507d537a603bc60d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/16/2020
ms.locfileid: "84796374"
---
# <a name="deploying-models-master-data-services"></a>모델 배포(Master Data Services)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]에서 패키지는 배포 가능한 모델 구조와 모델의 데이터(옵션)를 포함하는 XML 파일입니다. 모델 패키지를 사용하여 MDS 환경 간에 모델의 복사본을 이동하거나 기존 MDS 환경에 새로운 모델을 만듭니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]**MDSModelDeploy 도구** 는 이상에서 만든 패키지와 이전 버전과 호환 됩니다 [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] .  
  
## <a name="tools-for-deploying-models"></a>모델 배포 도구  
 모델 패키지를 사용하려면 필요에 따라 다음 세 도구 중 하나를 사용합니다.  
  
-   **MDSModelDeploy 도구**: 모델 개체와 데이터를 만들고 배포하려면 MDSModelDeploy.exe 도구를 사용합니다. MDS 설치 시 기본 경로를 선택한 경우 이 도구는 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration에 있습니다.  
  
-   **모델 배포 마법사**: 모델 구조만의 패키지를 만들고 배포하려면 [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] 웹 애플리케이션의 마법사를 사용합니다. 이 마법사를 사용하여 데이터를 배포할 수는 없습니다.  
  
-   **모델 패키지 편집기**: 모델 패키지를 편집하려면 모델 패키지 편집기 마법사를 실행하는 ModelPackageEditor.exe를 사용합니다. 이 마법사를 사용하여 MDSModelDeploy 도구 또는 모델 배포 마법사로 만든 패키지를 편집합니다. MDS 설치 시 기본 경로를 선택한 경우 이 도구는 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration에 있습니다.  
  
> [!IMPORTANT]  
>  MDSModelDeploy 도구를 사용하여 새 모델을 만들거나 모델의 복제본을 만들거나 기존 모델 및 해당 데이터를 업데이트할 수 있습니다. MDSModelDeploy 도구를 사용하여 기존 모델 및 해당 데이터를 업데이트하고 패키지에 엔터티, 특성 또는 대상 모델에 있는 멤버를 포함하지 않는 경우 MDSModelDeploy는 모델에서 해당 엔터티, 특성 또는 멤버를 삭제하지 않습니다.  
  
## <a name="what-packages-contain"></a>패키지에 포함된 내용  
 모델 패키지는 .pkg 확장명으로 저장되는 XML 파일입니다. 배포 패키지를 만드는 경우 데이터 포함 여부를 결정할 수 있습니다. 데이터를 포함하려면 포함할 데이터의 버전을 선택해야 합니다.  
  
 모든 모델 개체가 패키지에 포함됩니다. 모델 개체는 다음과 같습니다.  
  
-   엔터티  
  
-   특성  
  
-   특성 그룹  
  
-   계층 구조  
  
-   컬렉션  
  
-   비즈니스 규칙  
  
-   버전 플래그  
  
-   구독 뷰  
  
 파일 특성, 사용자 및 그룹 권한은 포함되지 않습니다. 모델을 배포한 후에 이러한 항목을 수동으로 업데이트해야 합니다.  
  
## <a name="sample-packages"></a>예제 패키지  
 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치하면 예제 패키지 파일이 포함됩니다. 이러한 패키지 파일은 [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]를 설치한 Master Data Services\Samples\Packages 디렉터리에 있습니다. MDSModelDeploy 도구를 사용하여 이러한 예제 패키지를 배포하면 예제 모델이 생성되어 데이터로 채워집니다.  
  
## <a name="related-tasks"></a>관련 작업  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|MDSModelDeploy 도구를 사용하여 모델 개체 및/또는 데이터의 새 배포 패키지를 만듭니다.|[MDSModelDeploy를 사용하여 모델 배포 패키지 만들기](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|마법사를 사용하여 모델 개체만의 새 배포 패키지를 만듭니다.|[마법사를 사용하여 모델 배포 패키지 만들기](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md)|  
|MDSModelDeploy 도구를 사용하여 모델 개체 및/또는 데이터의 패키지를 배포합니다.|[MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)|  
|마법사를 사용하여 모델 개체만의 패키지를 배포합니다.|[마법사를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)|  
|모델 배포 패키지를 편집하여 전체 모델이 아닌 모델의 일부 선택한 부분만 배포합니다.|[모델 배포 패키지 편집](../master-data-services/edit-a-model-deployment-package.md)|  
  
## <a name="related-content"></a>관련 내용  
  
-   [모델 배포 옵션&#40;Master Data Services&#41;](../master-data-services/model-deployment-options-master-data-services.md)  
  
  
