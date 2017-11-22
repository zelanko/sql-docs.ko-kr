---
title: "모델 배포 패키지 편집 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: master-data-services
ms.reviewer: 
ms.suite: sql
ms.technology: master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6b0fdb7d-83dd-4392-9011-4ae642c471f1
caps.latest.revision: "7"
author: smartysanthosh
ms.author: nagavo
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cd4abcfde3f017de3bff746a596f031025dd214e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="edit-a-model-deployment-package"></a>모델 배포 패키지 편집
  이 항목에서는 MDS에서 전체 모델 대신 모델의 선택한 부분을 배포하는 방법에 대해 설명합니다. 이렇게 하려면 모델 패키지 편집기를 사용하여 MDS 모델 패키지를 편집하면 됩니다.  
  
 모델 패키지 편집기 마법사에서는 MDS 패키지에 포함할 모델의 특정 엔터티, 파생 계층, 구독 뷰 및 비즈니스 규칙을 선택한 다음 나중에 배포할 수 있습니다. 모델에서 배포하지 않으려는 부분은 그대로 남겨 둘 수 있습니다. 엔터티를 선택하면 해당 엔터티의 모든 종속 개체도 자동으로 선택됩니다.  
  
 모델 패키지 편집기를 사용하여 MDSModelDeploy 도구(개체 및 데이터가 포함된 패키지 파일을 만드는 도구) 또는 모델 배포 마법사(모델 구조만 포함된 파일을 만드는 도구)를 사용하여 만든 패키지 파일에서 모델의 일부분을 선택할 수 있습니다. 패키지의 모델을 편집한 후에는 MDSModelDeploy 도구를 사용하여 개체 및 데이터를 배포하거나 모델 배포 마법사를 사용하여 모델 구조만 배포할 수 있습니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 이 절차를 수행하려면  
  
-   모델 관리자여야 합니다. 자세한 내용은 [관리자&#40;Master Data Services&#41;](../master-data-services/administrators-master-data-services.md)를 참조하세요.  
  
-   편집할 모델 패키지가 있어야 합니다. 자세한 내용은 [모델 배포&#40;Master Data Services&#41;](../master-data-services/deploying-models-master-data-services.md) 및 [마법사를 사용하여 모델 배포 패키지 만들기](../master-data-services/create-a-model-deployment-package-by-using-the-wizard.md) 또는 [MDSModelDeploy를 사용하여 모델 배포 패키지 만들기](../master-data-services/create-a-model-deployment-package-by-using-mdsmodeldeploy.md)를 참조하세요.  
  
### <a name="to-edit-a-model-deployment-package"></a>모델 배포 패키지를 편집하려면  
  
1.  MDS 서버의 Windows 탐색기에서 *드라이브*:\Program Files\Microsoft SQL Server\130\Master Data Services\Configuration으로 이동합니다.  
  
2.  Modelpackageeditor.exe를 실행합니다.  
  
3.  모델 패키지 편집기 마법사에서 **찾아보기**를 클릭하여 패키지가 포함된 폴더로 이동한 다음 패키지를 선택하고 **열기**를 클릭합니다. **다음**을 클릭합니다.  
  
4.  배포할 엔터티, 파생 계층, 구독 뷰 또는 비즈니스 규칙을 선택합니다. 배포하지 않을 엔터티, 파생 계층, 구독 뷰 또는 비즈니스 규칙의 선택을 취소합니다. **다음**을 클릭합니다.  
  
5.  배포할 선택 항목의 목록을 확인합니다. 변경하려면 **뒤로** 를 클릭한 다음 4단계를 반복합니다.  
  
6.  **찾아보기**를 클릭하여 부분 패키지를 저장할 폴더로 이동한 다음 부분 패키지의 파일 이름(확장명은 .pkg)을 입력합니다. **저장**을 클릭합니다.  
  
7.  **마침**을 클릭합니다.  
  
## <a name="next-steps"></a>다음 단계  
  
-   [마법사를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-the-wizard.md)  
  
-   [MDSModelDeploy를 사용하여 모델 배포 패키지 배포](../master-data-services/deploy-a-model-deployment-package-by-using-mdsmodeldeploy.md)  
  
  
