---
title: "SQL Server Data Tools에서 패키지 실행 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Integration Services 패키지, 실행"
  - "SSIS 패키지, 실행"
  - "패키지 [Integration Services], 실행"
  - "SQL Server Integration Services 패키지, 실행"
ms.assetid: 318e6beb-5540-4101-82a5-18c9d47f0570
caps.latest.revision: 58
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 58
---
# SQL Server Data Tools에서 패키지 실행
  패키지는 개발, 디버깅 및 테스팅이 이루어지는 동안 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 일반적으로 실행됩니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 실행하는 경우 패키지는 항상 즉시 실행됩니다.  
  
 패키지를 실행하는 동안 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너는 **진행률** 탭에 패키지 실행 진행률을 표시합니다. 패키지 및 패키지의 태스크 및 컨테이너의 시작 시각 및 종료 시각을 볼 수 있으며 또한 패키지 내의 실패한 모든 태스크 및 컨테이너에 대한 정보를 볼 수 있습니다. 패키지 실행이 종료되면 **실행 결과** 탭에서 런타임 정보를 확인할 수 있습니다. 자세한 내용은 [Debugging Control Flow](../../integration-services/troubleshooting/debugging-control-flow.md)항목의 "진행률 보고" 섹션을 참조하십시오.  
  
 **디자인 타임 배포**. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 패키지를 실행하면 패키지가 빌드된 다음 폴더에 배포됩니다. 패키지를 실행하기 전에 패키지가 배포되는 폴더를 지정할 수 있습니다. 폴더를 지정하지 않으면 **bin** 폴더가 기본적으로 사용됩니다. 이러한 종류의 배포를 디자인 타임 배포라고 부릅니다.  
  
### SQL Server Data Tools에서 패키지를 실행하려면  
  
1.  솔루션 탐색기에서 솔루션에 여러 프로젝트가 포함되어 있는 경우 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 폴더를 마우스 오른쪽 단추로 클릭한 다음 **시작 개체로 설정**을 클릭하여 시작 프로젝트를 설정합니다.  
  
2.  솔루션 탐색기에서 프로젝트에 여러 패키지가 포함되어 있는 경우 패키지를 마우스 오른쪽 단추로 클릭한 다음 **시작 개체로 설정**을 클릭하여 시작 패키지를 설정합니다.  
  
3.  패키지를 실행하려면 다음 절차 중 하나를 따릅니다.  
  
    -   실행하려는 패키지를 연 다음 메뉴 모음에서 **디버깅 시작** 을 클릭하거나 F5 키를 누릅니다. 패키지 실행이 완료된 다음 Shift+F5를 눌러서 디자인 모드로 돌아갑니다.  
  
    -   솔루션 탐색기에서 패키지를 마우스 오른쪽 단추로 클릭한 다음 **패키지 실행**을 클릭합니다.  
  
### 디자인 타임 배포를 위한 다른 폴더를 지정하려면  
  
1.  솔루션 탐색기에서 실행할 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트 폴더를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
2.  **\<프로젝트 이름> 속성 페이지** 대화 상자에서 **빌드**를 클릭합니다.  
  
3.  OutputPath 속성의 값을 업데이트하여 디자인 타임 배포에 사용할 폴더를 지정하고 **확인**을 클릭합니다.  
  
## 관련 항목:  
 [프로젝트 및 패키지 실행](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Integration Services(SSIS) 패키지](https://msdn.microsoft.com/library/ms141134.aspx)  
  
  