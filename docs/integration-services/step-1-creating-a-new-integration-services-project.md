---
title: "1단계: 새 Integration Services 프로젝트 만들기 | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
---
# 1단계: 새 Integration Services 프로젝트 만들기
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 에서 패키지를 만드는 첫 번째 단계는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만드는 것입니다. 이 프로젝트는 데이터 변환 솔루션에서 사용하는 데이터 원본, 데이터 원본 뷰, 패키지 등의 개체에 대한 템플릿을 포함합니다.  
  
이 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 자습서에서 만들 패키지는 로캘 구분 데이터의 값을 해석합니다. 컴퓨터가 영어(미국) 국가별 옵션을 사용하도록 구성되어 있지 않은 경우 패키지에 추가 속성을 설정해야 합니다. 2-5단원에서 사용하는 패키지는 1단원에서 만든 패키지에서 복사한 것이므로 복사된 패키지의 로캘 구분 속성을 업데이트할 필요가 없습니다.  
  
> [!NOTE]  
> 이 자습서를 사용하려면 Microsoft SQL Server Data Tools가 필요합니다.  
>   
> SQL Server Data Tools 설치 방법에 대한 자세한 내용은 [SQL Server Data Tools 다운로드](http://msdn.microsoft.com/en-us/data/hh297027)를 참조하세요.  
  
### 새 Integration Services 프로젝트를 만들려면  
  
1.  **시작** 메뉴에서 **모든 프로그램**, **Microsoft SQL Server**를 차례로 가리킨 다음 **SQL Server Data Tools**를 클릭합니다.  
  
2.  **파일** 메뉴에서 **새로 만들기**를 가리킨 다음 **프로젝트** 를 클릭하여 새 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트를 만듭니다.  
  
3.  **새 프로젝트** 대화 상자의 **설치된 템플릿** 아래에서 **비즈니스 인텔리전스**를 확장하고 **템플릿** 창에서 **통합 서비스 프로젝트** 를 선택합니다.  
  
4.  **이름** 상자에서 기본 이름을 **SSIS Tutorial**로 변경합니다. 필요에 따라 **솔루션용 디렉터리 만들기** 확인란의 선택을 취소합니다.  
  
5.  기본 위치를 적용하거나 **찾아보기** 를 클릭하여 사용할 폴더를 찾아 이동합니다. **프로젝트 위치** 대화 상자에서 해당 폴더를 클릭한 다음 **폴더 선택**을 클릭합니다.  
  
6.  **확인**을 클릭합니다.  
  
    기본적으로 **Package.dtsx**라는 빈 패키지가 만들어지고 SSIS 패키지 아래 프로젝트에 추가됩니다.  
  
7.  **솔루션 탐색기** 도구 모음에서 **Package.dtsx**를 마우스 오른쪽 단추로 클릭하고 **이름 바꾸기**를 클릭한 다음 기본 패키지의 이름을 **Lesson 1.dtsx**로 바꿉니다.  
  
## 단원의 다음 태스크  
[2단계: 플랫 파일 연결 관리자 추가 및 구성](../integration-services/step-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
