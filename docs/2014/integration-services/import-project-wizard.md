---
title: 프로젝트 가져오기 마법사 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.importprojectwizard.f1
ms.assetid: 9247ad6c-4bd1-43ab-b347-583181cb9917
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 33e6400c9076d96cbe9999cc4110b0e3bd5f0902
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58391201"
---
# <a name="import-project-wizard"></a>프로젝트 가져오기 마법사
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트 가져오기 마법사를 사용하여 기존 항목에 따라 새 Integration Services 프로젝트를 만듭니다. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 카탈로그에 이미 배포된 프로젝트를 가져오거나 프로젝트 배포 파일(확장명 .ispac)에서 프로젝트를 가져옵니다.  
  
### <a name="to-create-a-project-based-on-a-project-in-ispac-file-or-in-catalog"></a>.ispac 파일 또는 카탈로그의 프로젝트를 기반으로 프로젝트를 만들려면  
  
1.  **파일**을 클릭하고 **새로 만들기**를 가리킨 후 프로젝트를 클릭합니다.  
  
2.  **비즈니스 인텔리전스**를 확장하고 **Integration Services**를 클릭합니다.  
  
3.  가운데 창에서 **Integration Services 가져오기 마법사** 를 선택하고 솔루션, 프로젝트에 대한 **이름** 을 입력하고 프로젝트에 대한 **폴더** 를 지정한 후 **확인**을 클릭합니다.  
  
     **Integration Services 프로젝트 가져오기 마법사**가 표시됩니다. 이 마법사는 기존 항목에 따라 새 Integration Services 프로젝트를 만듭니다.  
  
4.  **소개** 페이지에서 **다음** 을 클릭하여 **원본 선택** 페이지를 표시합니다.  
  
5.  .ispac 파일 또는 카탈로그에서 프로젝트를 가져올지를 지정합니다.  
  
    -   **프로젝트 배포 파일** 옵션을 선택한 경우 .ispac 파일에 대한 경로를 지정합니다.  
  
    -   **Integration Services 카탈로그** 옵션을 선택한 경우 카탈로그가 있는 데이터베이스 서버 인스턴스의 이름을 지정하고 카탈로그에서 프로젝트에 대한 경로를 지정합니다.  
  
6.  **원본 선택** 페이지에서 **다음** 을 클릭하여 **검토** 페이지를 표시합니다. 페이지에 표시된 마법사가 수행하려는 가져오기 작업에 대한 정보를 검토합니다.  
  
7.  **가져오기** 를 클릭하여 사용자가 선택한 항목에 따라 새 Integration Services 프로젝트를 만듭니다.  
  
8.  **결과** 페이지에 마법사가 수행한 가져오기 작업의 결과가 표시됩니다. **보고서 저장** 을 클릭하여 보고서를 XML 파일로 저장합니다.  
  
9. **닫기** 를 클릭하여 마법사를 닫습니다.  
  
  
