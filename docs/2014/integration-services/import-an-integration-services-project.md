---
title: Integration Services 프로젝트 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 3301c328-b0f5-4517-915c-93713413e453
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8fb6b68cbb30e9bbf19f854cf1dd1e7e0dd19d25
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58394441"
---
# <a name="import-an-integration-services-project"></a>Integration Services 프로젝트 가져오기
  기존 배포 파일(.ispac) 또는 Integration Services 카탈로그에 배포된 프로젝트에서 프로젝트를 만들려면 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] **프로젝트 가져오기 마법사**를 사용합니다. 이 기능은 프로젝트의 원본이 없지만 .ispac 파일 또는 SSISDB 카탈로그에서 프로젝트를 만들려는 경우에 특히 유용합니다.  
  
### <a name="to-import-a-project"></a>프로젝트를 가져오려면  
  
1.  [!INCLUDE[vsprvs](../includes/vsprvs-md.md)]의 **파일** > **메뉴에서** 새로 만들기 **프로젝트** 를 클릭합니다.  
  
2.  **새 프로젝트** 창의 **설치되어 있는 템플릿** 영역에서 **비즈니스 인텔리전스**를 확장하고 **Integration Services**를 클릭합니다.  
  
3.  프로젝트 형식 목록에서 **Integration Services 프로젝트 가져오기 마법사** 를 선택합니다.  
  
4.  **이름** 입력란에 만들 새 프로젝트의 이름을 입력합니다.  
  
5.  **위치** 입력란에 프로젝트의 경로 또는 위치를 입력하거나 **찾아보기** 를 클릭하여 위치를 선택합니다.  
  
6.  **솔루션 이름** 입력란에 솔루션의 이름을 입력합니다.  
  
7.  **확인** 을 클릭하여 **Integration Services 프로젝트 가져오기 마법사** 대화 상자를 시작합니다.  
  
8.  **다음** 을 클릭하여 **원본 선택** 페이지로 전환합니다.  
  
9. **.ispac** 파일에서 가져오는 경우 **경로** 입력란에 파일 이름을 포함한 경로를 입력합니다. **찾아보기** 를 클릭하여 솔루션을 저장할 폴더로 이동하고 **파일 이름** 입력란에 파일 이름을 입력한 다음 **열기**를 클릭합니다.  
  
     **Integration Services 카탈로그**에서 가져오는 경우 **서버 이름** 입력란에 데이터베이스 인스턴스 이름을 입력하거나 **찾아보기** 를 클릭하고 카탈로그가 들어 있는 데이터베이스 인스턴스를 선택합니다.  
  
     **경로** 입력란 옆의 **찾아보기** 를 클릭하고 카탈로그에서 폴더를 확장한 다음 가져올 프로젝트를 선택하고 **확인**을 클릭합니다.  
  
     **다음** 을 클릭하여 **검토** 페이지로 전환합니다.  
  
10. 정보를 검토하고 **가져오기** 를 클릭하여 선택한 기존 프로젝트를 기반으로 프로젝트를 만듭니다.  
  
11. 선택 사항: **보고서 저장** 을 클릭하여 결과를 파일에 저장합니다.  
  
12. **닫기** 를 클릭하여 **Integration Services 프로젝트 가져오기 마법사** 대화 상자를 닫습니다.  
  
  
