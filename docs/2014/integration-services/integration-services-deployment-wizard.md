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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 721953c31a44a2ea02f480c9830e6347adfd4eb3
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66058004"
---
# <a name="integration-services-deployment-wizard"></a>Integration Services 배포 마법사
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 배포 마법사는 프로젝트 배포 모델을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에서 SSISDB 카탈로그에 프로젝트를 배포합니다.  
  
 시작 하는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 열려 있는 프로젝트에서 배포 마법사 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]를 선택 **배포** 에서 **프로젝트** 메뉴. 마법사를 시작 하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]를 확장 합니다 **Integration Services 카탈로그** > **SSISDB** , 개체 탐색기 노드를에서 마우스 오른쪽 단추로 클릭 합니다 **프로젝트** 폴더를 마우스 클릭 **프로젝트 배포**합니다.  
  
 마법사에서 다음 네 단계가 진행됩니다. 클릭 **다음** 하 여 다음 단계로 이동할 또는 **이전** 이전 단계로 돌아갑니다.  
  
1.  **원본 선택** -선택 된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 배포 하려는 프로젝트.  
  
2.  **대상 선택** -프로젝트 대상을 선택 합니다.  
  
3.  **검토** -선택 항목을 표시 합니다.  
  
4.  **배포/결과** -프로젝트를 배포 하 고 결과 표시 합니다.  
  
## <a name="select-source"></a>원본 선택  
 사용자가 만든 프로젝트 배포 파일을 배포 하려면를 선택 **프로젝트 배포 파일** .ispac 파일에 경로 입력 하거나 클릭 하 고 **찾아보기** 에서 찾을 수는 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] 프로젝트 폴더입니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 후 서버 이름과 카탈로그에 있는 프로젝트 경로를 입력합니다.  
  
 [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]에서 마법사를 시작하면 기본적으로 마법사에서 열린 프로젝트가 원본으로 선택되고 이 단계를 건너뜁니다. 이 단계로 돌아가서 다른 원본을 선택, 클릭 **이전** 누르거나 **원본 선택** 왼쪽된 창에서.  
  
## <a name="select-destination"></a>대상 선택  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그에서 프로젝트에 대한 대상 폴더를 선택하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스를 입력하거나 서버 목록에서 **찾아보기** 를 클릭하여 선택합니다. SSISDB에 프로젝트 경로를 입력하거나 **찾아보기** 를 클릭하여 선택합니다.  
  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 마법사를 시작하면 기본적으로 마법사에서 연결된 서버 인스턴스를 선택하고 선택한 프로젝트에 대한 경로를 입력합니다. 다른 위치에 프로젝트를 배포할 경우 이러한 값을 변경할 수 있습니다.  
  
## <a name="review"></a>검토  
 이 마법사에서는 프로젝트를 배포하기 전에 사용자가 선택한 설정을 검토할 수 있습니다. **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다.  
  
## <a name="deployresults"></a>배포/결과  
 클릭 하면 **배포** 에서 **검토** 페이지에서 프로젝트 배포 및 **결과** 페이지 각 동작의 성공 여부를 표시 합니다. 작업이 실패하면 **결과** 열에서 **실패** 를 클릭하여 해당 오류에 대한 설명을 표시합니다. 클릭 **보고서를 저장 하는 중...**  XML 파일에 결과 저장할 수 있습니다.  
  
 **닫기**를 클릭하여 마법사를 종료합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 서버에 프로젝트 배포](../../2014/integration-services/deploy-projects-to-integration-services-server.md)   
 [프로젝트 및 패키지 배포](packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
