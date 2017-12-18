---
title: "1단계: 배포 유틸리티 작성 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
ms.assetid: 1ff4dcff-89b3-4b99-a725-5f7963e98abf
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f2d1ad6752ce23a04d3c9989d0f35660c05e904e
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-2-1---building-the-deployment-utility"></a>2-1단원 - 배포 유틸리티 작성
이 태스크에서는 Deployment Tutorial 프로젝트를 위한 배포 유틸리티를 구성 및 작성합니다.  
  
배포 유틸리티를 작성할 수 있으려면 Deployment Tutorial 프로젝트의 속성을 수정해야 합니다. **Deployment Tutorial 속성 페이지** 대화 상자를 사용하여 이러한 속성을 구성합니다. 이 대화 상자에서 배포 중에 구성을 업데이트하는 기능을 설정하고 빌드 프로세스에서 배포 유틸리티를 생성하도록 지정해야 합니다. 속성을 설정한 후에 프로젝트를 작성합니다.  
  
[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 에서는 패키지를 디버그하는 데 사용할 수 있는 일련의 창이 제공됩니다. 오류, 경고 및 정보 메시지를 확인하고 런타임에 패키지 상태를 추적하며 빌드 프로세스의 진행률과 결과를 볼 수 있습니다. 이 단원에서는 출력 창을 사용하여 배포 유틸리티 작성의 진행률과 결과를 확인합니다.  
  
### <a name="to-set-the-deployment-utility-properties"></a>배포 유틸리티 속성을 설정하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 를 아직 열지 않은 경우 **시작**을 클릭하고 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **Business Intelligence Development Studio**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **열기**, **프로젝트/솔루션**, **Deployment Tutorial** 폴더, **열기**를 차례로 클릭한 다음 **Deployment Tutorial.sln**을 두 번 클릭합니다.  
  
3.  솔루션 탐색기에서 Deployment Tutorial을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
4.  **Deployment Tutorial 속성 페이지** 대화 상자에서 구성 속성을 확장하고 배포 유틸리티를 클릭합니다.  
  
5.  **Deployment Tutorial 속성 페이지** 대화 상자의 오른쪽 창에서 **AllowConfigurationChanges** 가 **true**로 설정되어 있는지 확인하고 **CreateDeploymentUtility** 를 **true**로 설정한 다음 필요에 따라 **DeploymentOutputPath**의 기본값을 업데이트합니다.  
  
6.  **확인**을 클릭합니다.  
  
### <a name="to-build-the-deployment-utility"></a>배포 유틸리티를 작성하려면  
  
1.  솔루션 탐색기에서 **Deployment Tutorial**을 클릭합니다.  
  
2.  **보기** 메뉴에서 **출력**을 클릭합니다. 기본적으로 출력 창은 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]의 왼쪽 하단 모퉁이에 있습니다.  
  
3.  **빌드** 메뉴에서 **Deployment Tutorial 빌드**를 클릭합니다.  
  
4.  출력 창에서 다음 정보를 확인합니다.  
  
    빌드 시작: SQL Integration Services 프로젝트: 증분...  
  
    배포 유틸리티를 만드는 중...  
  
    배포 유틸리티가 생성되었습니다.  
  
    빌드 완료 -- 0개 오류, 0개 경고  
  
    ========== 빌드: 성공 0, 실패 0, 최신 1, 생략 0 ==========  
  
5.  **파일** 메뉴에서 **끝내기**를 클릭합니다. Deployment Tutorial 항목의 변경 내용을 저장할 것인지 묻는 메시지가 표시되면 **예**를 클릭합니다.  
  
## <a name="next-task-in-lesson"></a>단원의 다음 태스크  
[2단계: 배포 번들 확인](../integration-services/lesson-2-2-verifying-the-deployment-bundle.md)  
  
## <a name="see-also"></a>참고 항목  
[배포 유틸리티 만들기](../integration-services/packages/create-a-deployment-utility.md)  
  
  
  
