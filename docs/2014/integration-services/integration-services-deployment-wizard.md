---
title: Integration Services 배포 마법사 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.deploymentwizard.f1
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2039968976df2e22a16c47abbcc3f51ba25bbeb2
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85424810"
---
# <a name="integration-services-deployment-wizard"></a>Integration Services 배포 마법사
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 배포 마법사는 프로젝트 배포 모델을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 SSISDB 카탈로그에 프로젝트를 배포합니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 열려 있는 프로젝트에서 배포 마법사를 시작 하려면 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] **프로젝트** 메뉴에서 **배포** 를 선택 합니다. 에서 마법사를 시작 하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 개체 탐색기에서 **Integration Services 카탈로그**  >  **SSISDB** 노드를 확장 하 고 **프로젝트** 폴더를 마우스 오른쪽 단추로 클릭 한 다음 **프로젝트 배포**를 클릭 합니다.  
  
 마법사에서 다음 네 단계가 진행됩니다. 다음 **을 클릭 하** 여 다음 단계로 이동 하거나 이전 단계로 돌아가려면 **이전** 을 클릭 합니다.  
  
1.  **원본 선택** -배포 하려는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 선택 합니다.  
  
2.  **대상 선택** -프로젝트 대상을 선택 합니다.  
  
3.  **검토** -선택 항목을 표시 합니다.  
  
4.  **배포/결과** -프로젝트를 배포 하 고 결과를 표시 합니다.  
  
## <a name="select-source"></a>원본 선택  
 만든 프로젝트 배포 파일을 배포 하려면 **프로젝트 배포 파일** 을 선택 하 고 .ispac 파일의 경로를 입력 하거나 **찾아보기** 를 클릭 하 여 프로젝트 폴더에서 찾습니다. [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 후 서버 이름과 카탈로그에 있는 프로젝트 경로를 입력합니다.  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에서 마법사를 시작하면 기본적으로 마법사에서 열린 프로젝트가 원본으로 선택되고 이 단계를 건너뜁니다. 이 단계로 돌아가서 다른 원본을 선택 하려면 **이전** 을 클릭 하거나 왼쪽 창에서 **원본 선택** 을 클릭 합니다.  
  
## <a name="select-destination"></a>대상 선택  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그에서 프로젝트에 대한 대상 폴더를 선택하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 입력하거나 서버 목록에서 **찾아보기** 를 클릭하여 선택합니다. SSISDB에 프로젝트 경로를 입력하거나 **찾아보기** 를 클릭하여 선택합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 마법사를 시작하면 기본적으로 마법사에서 연결된 서버 인스턴스를 선택하고 선택한 프로젝트에 대한 경로를 입력합니다. 다른 위치에 프로젝트를 배포할 경우 이러한 값을 변경할 수 있습니다.  
  
## <a name="review"></a>검토  
 이 마법사에서는 프로젝트를 배포하기 전에 사용자가 선택한 설정을 검토할 수 있습니다. **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다.  
  
## <a name="deployresults"></a>배포/결과  
 **검토** 페이지에서 **배포** 를 클릭 하면 프로젝트가 배포 되 고 **결과** 페이지에 각 동작의 성공 또는 실패 여부가 표시 됩니다. 작업이 실패하면 **결과** 열에서 **실패** 를 클릭하여 해당 오류에 대한 설명을 표시합니다. **보고서 저장** ...을 클릭 하 여 결과를 XML 파일에 저장 합니다.  
  
 **닫기**를 클릭하여 마법사를 종료합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 서버에 프로젝트 배포](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [프로젝트 및 패키지 배포](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
