---
title: '1단계: 새 Integration Services 프로젝트 만들기 | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0b5fd6b088b9affb4986b67deffb50b134e08d5c
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143233"
---
# <a name="lesson-1-1-create-a-new-integration-services-project"></a>1-1단원: 새 Integration Services 프로젝트 만들기

[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 패키지를 만드는 첫 번째 단계는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만드는 것입니다. 이 프로젝트 예시에는 데이터 변환 솔루션을 구성하는 데이터 원본, 데이터 원본 뷰, 패키지의 템플릿이 포함됩니다.  
  
이 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 자습서에서 만드는 패키지는 로캘 구분 데이터의 값을 해석합니다. 컴퓨터가 **영어(미국)** 국가별 옵션을 사용하도록 구성되어 있지 않은 경우 패키지에 추가 속성을 설정해야 합니다. 

2~6단원에서 사용하는 패키지는 이 단원에서 만든 패키지에서 복사됩니다.  
  
> [!NOTE]  
> 아직 준비가 되지 않았다면 [1단원 필수 구성 요소](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites)를 참조하세요.

## <a name="create-a-new-integration-services-project"></a>새 Integration Services 프로젝트 만들기  
  
1.  Windows의 **시작** 메뉴에서 **Visual Studio(SSDT)** 를 검색하여 선택합니다.  
  
2.  Visual Studio에서 **파일** > **새로 만들기** > **프로젝트**를 선택하여 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만듭니다.  
  
3.  **새 프로젝트** 대화 상자의 **설치됨**에서 **비즈니스 인텔리전스**를 확장하고 **템플릿** 창에서 **통합 서비스 프로젝트** 를 선택합니다.  
  
4.  **이름** 상자에서 기본 이름을 **SSIS Tutorial**로 변경합니다. 이미 존재하는 폴더를 사용하려면 **솔루션용 디렉터리 만들기** 확인란의 선택을 취소합니다.  
  
5.  기본 위치를 적용하거나 **찾아보기**를 선택하여 사용할 폴더를 찾아 이동합니다. **프로젝트 위치** 대화 상자에서 해당 폴더를 선택한 다음 **폴더 선택**을 선택합니다.  
  
6.  **확인**을 선택합니다.  
  
    기본적으로 **Package.dtsx**라는 빈 패키지가 만들어지고 **SSIS 패키지**의 프로젝트에 추가됩니다.  
  
7.  **솔루션 탐색기**에서 **Package.dtsx**를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 선택한 다음 기본 패키지의 이름을 **Lesson 1.dtsx**로 바꿉니다.  
  
## <a name="go-to-next-task"></a>다음 작업으로 이동
[2단계: 플랫 파일 연결 관리자 추가 및 구성](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
