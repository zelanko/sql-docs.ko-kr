---
title: "Integration Services 배포 마법사 | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.deploymentwizard.f1"
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Integration Services 배포 마법사
  **Integration Services 배포 마법사**는 아래의 두 가지 배포 모델을 지원합니다.
   - 프로젝트 배포 모델
   - 패키지 배포 모델 
   
 **프로젝트 배포 모델**을 사용하면 SSIS(SQL Server Integration Services) 프로젝트를 를 하나의 단위로 SSIS 카탈로그에 배포할 수 있습니다.
 
 **패키지 배포 모델**을 사용하면 전체 프로젝트를 배포할 필요 없이 SSIS 카탈로그로 업데이트한 패키지를 배포할 수 있습니다. 
 
 > **참고:** Integration Services 배포 마법사의 기본 배포는 프로젝트 배포 모델입니다.  
  
## 마법사 시작
다음과 같이 마법사를 시작합니다.

 - Windows Search에서 **"SQL Server 배포 마법사"**를 입력합니다. 

**OR**

 - SQL Server 설치 폴더에서 실행 파일 **ISDeploymentWizard.exe**를 검색합니다(예: C:\Program Files (x86)\Microsoft SQL Server\130\DTS\Binn). 
 
 > **참고:** **소개** 페이지에서 **다음**을 클릭하여 **원본 선택** 페이지로 전환합니다. 
 
 이 페이지의 설정은 각 배포 모델에서 서로 다릅니다. 이 페이지에서 선택한 모델에 따라 [Project Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#ProjectModel) 섹션의 단계 또는 [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) 섹션의 단계를 따릅니다.  
  
##  <a name="ProjectModel"></a> 프로젝트 배포 모델  
  
### 원본 선택  
 만든 프로젝트 배포 파일을 배포하려면 **프로젝트 배포 파일** 을 선택하고 .ispac 파일에 대한 경로를 입력합니다. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에 있는 프로젝트를 배포하려면 **Integration Services 카탈로그**를 선택한 후 서버 이름과 카탈로그에 있는 프로젝트 경로를 입력합니다. **다음** 을 클릭하여 **대상 선택** 페이지를 표시합니다.  
  
### 대상 선택  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 카탈로그에서 프로젝트에 대한 대상 폴더를 선택하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 입력하거나 서버 목록에서 **찾아보기** 를 클릭하여 선택합니다. SSISDB에 프로젝트 경로를 입력하거나 **찾아보기** 를 클릭하여 선택합니다. **다음** 을 클릭하여 **검토** 페이지를 표시합니다.  
  
### 검토(및 배포)  
 이 페이지를 사용하면 선택한 설정을 검토할 수 있습니다. **이전**을 클릭하거나 왼쪽 창의 단계 중 하나를 클릭하여 선택 항목을 변경할 수 있습니다. **배포** 를 클릭해 배포 프로세스를 시작합니다.  
  
### 결과  
 배포 프로세스가 완료되면 **결과** 페이지가 표시되어야 합니다. 이 페이지는 각 동작의 성공 또는 실패 여부를 표시합니다. 작업이 실패하면 **결과** 열에서 **실패** 를 클릭하여 해당 오류에 대한 설명을 표시합니다. 결과를 XML 파일로 저장하려면 **보고서 저장...** 을 클릭하거나 **닫기** 를 클릭해 마법사를 종료합니다.  
  
##  <a name="PackageModel"></a> 패키지 배포 모델  
  
### 원본 선택  
 **Integration Services 배포 마법사** 의 **원본 선택** 페이지는 **배포 모델** 에서 **패키지 배포**옵션을 선택할 때 패키지 배포 모델별 설정을 보여줍니다.  
  
 원본 패키지를 선택하려면 **찾아보기...** 단추를 클릭해 패키지가 포함된 **폴더** that contains the packages or type the 폴더 path in the **Packages 폴더 path** 텍스트 상자에 폴더 경로를 입력하고 페이지 아래쪽에 있는 **새로 고침** 단추를 클릭합니다. 이제 목록 상자의 지정된 폴더에 모든 패키지가 표시됩니다. 기본적으로 모든 패키지가 선택되어 있습니다. 첫 번째 열에 있는 **확인란** 을 클릭해 서버로 배포할 패키지를 선택합니다.  
  
 **상태** 및 **메시지** 열을 참조하여 패키지 상태를 확인합니다. 상태가 **준비** 또는 **경고**로 설정된 경우 배포 마법사는 배포 프로세스를 차단하지 않습니다. 반면, 상태가 **오류**로 설정된 경우 마법사는 선택한 패키지의 배포를 더 이상 진행하지 않습니다. 자세한 경고/오류 메시지를 보려면 **메시지** 열에 있는 링크를 클릭합니다.  
  
 중요한 데이터 또는 패키지 데이터가 암호로 암호화된 경우 **암호** 열에 암호를 입력한 후 **새로 고침** 단추를 클릭해 암호가 맞는지 확인합니다. 암호가 맞는 경우 상태가 **준비** 로 변경되고 경고 메시지가 사라집니다. 여러 패키지의 암호가 동일한 경우 동일한 암호화 암호가 있는 패키지들을 선택한 후 **암호** 텍스트 상자에 암호를 입력한 후 **적용** 단추를 클릭합니다. 암호는 선택한 패키지에 적용됩니다.  
  
 선택한 일부 패키지가 **오류**로 설정되지 않은 경우 **다음** 단추가 활성화되어 패키지 배포 프로세스를 계속 진행할 수 있습니다.  
  
### 대상 선택  
 패키지 소스를 선택한 후 **다음** 단추를 클릭해 **대상 선택** 페이지로 전환합니다. 패키지는 SSIS 카탈로그(SSISDB)에 프로젝트로 배포되어야 합니다. 따라서 대상 프로젝트가 SSIS 카탈로그에 이미 있는지 확인한 후 패키지를 배포하십시오. 그렇지 않으면 빈 프로젝트를 만듭니다. **대상 선택** 페이지에서 **서버 선택** 텍스트 상자에 서버 이름을 입력하거나 **찾아보기...** 단추를 클릭해 서버 인스턴스를 선택합니다. 그런 다음 **찾아보기...** 옆에 있는 **찾아보기...** 단추를 클릭해 대상 프로젝트를 지정합니다. 프로젝트가 존재하지 않는 경우 **새 프로젝트...** 를 클릭해 대상 프로젝트로 빈 프로젝트를 만듭니다. 프로젝트는 **반드시** 폴더 아래에 생성되어야 합니다.  
  
### 검토 및 배포  
 **대상 선택** 페이지에서 **다음** 을 클릭해 **Integration Services 배포 마법사** 의 **검토**페이지로 전환합니다. 검토 페이지에서 배포 작업에 대한 요약 보고서를 검토합니다. 검토한 후, **배포** 단추를 클릭해 배포 작업을 수행합니다.  
  
### 결과  
 배포가 완료되면 **결과** 페이지가 표시되어야 합니다. **결과** 페이지에서 배포 프로세스의 각 단계 결과를 검토합니다. **결과** 페이지에서 **보고서 저장** 을 클릭해 배포 보고서를 저장하거나 **닫기** 를 클릭해 마법사를 종료합니다.  
  
## 관련 항목:  
 [Integration Services 서버에 프로젝트 배포](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [프로젝트 및 패키지 배포](https://msdn.microsoft.com/library/hh213290.aspx)  
  
  