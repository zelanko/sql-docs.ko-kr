---
title: '2단계: 배포 번들 확인 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 6c13f5c9-c75e-4e52-94dc-2d2db2c578fe
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 163df99c54ed323d1039d50c69e812cb4c1d2286
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368785"
---
# <a name="step-2-verifying-the-deployment-bundle"></a>2단계: 배포 번들 확인
  1단원에서는 Deployment Tutorial 프로젝트를 만들고 패키지와 보조 파일을 프로젝트에 추가했습니다. 이전 태스크에서는 프로젝트를 위한 배포 유틸리티를 작성했습니다.  
  
 이 태스크에서는 배포 번들의 내용을 확인합니다. 배포 번들은 대상 컴퓨터에 복사하고 패키지를 설치하는 데 사용하는 폴더입니다. 배포 유틸리티의 위치로 기본값인 bin\Deployment를 사용한 경우 배포 번들은 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로젝트의 Deployment Tutorial 폴더 내에 있는 Bin\Deployment 폴더입니다.  
  
### <a name="to-verify-the-content-of-deployment-bundle"></a>배포 번들의 내용을 확인하려면  
  
1.  컴퓨터에서 bin\Deployment 폴더를 찾습니다.  
  
2.  다음 파일이 있는지 확인합니다.  
  
    -   DataTransfer.dtsx  
  
    -   datatransferconfig.dtsconfig  
  
    -   Deployment Tutorial.SSISDeploymentManifest  
  
    -   LoadXMLData.dtsx  
  
    -   loadxmldataconfig.dtsconfig  
  
    -   NewCustomers.txt  
  
    -   orders.xml  
  
    -   orders.xsd  
  
    -   Readme.txt  
  
3.  Deployment Tutorial.SSISDeploymentManifest를 마우스 오른쪽 단추로 클릭하고 **연결 프로그램**을 가리킨 다음 **Internet Explorer**를 클릭합니다. 또한 메모장과 같은 텍스트 편집기에서 파일을 열 수도 있습니다. 파일의 XML 코드는 다음과 같아야 합니다.  
  
     `<?xml version="1.0"?><DTSDeploymentManifest GeneratedBy="Domain\UserName" GeneratedFromProjectName="Deployment Tutorial" GeneratedDate="2006-02-24T13:29:02.6537669-08:00" AllowConfigurationChanges="true"><Package>DataTransfer.dtsx</Package><Package>LoadXMLData.dtsx</Package><ConfigurationFile>datatransferconfig.dtsconfig</ConfigurationFile><ConfigurationFile>loadxmldataconfig.dtsconfig</ConfigurationFile><MiscellaneousFile>Readme.txt</MiscellaneousFile><MiscellaneousFile>orders.xml</MiscellaneousFile><MiscellaneousFile>NewCustomers.txt</MiscellaneousFile><MiscellaneousFile>orders.xsd</MiscellaneousFile></DTSDeploymentManifest>`  
  
4.  되어 있는지 확인 값을 `AllowConfigurationChanges` 특성은 **true** XML에 포함 되어는 `Package` 고 두 패키지 각각에 대 한 요소를 `MiscellaneousFile` 는 4 개의 패키지가 아닌 파일의 각 요소 및 `ConfigurationFile` 두 XML 구성 파일의 각 요소입니다.  
  
5.  Internet Explorer 또는 텍스트 편집기를 종료합니다.  
  
## <a name="next-lesson"></a>다음 단원  
 [3 단원: 패키지 설치](../integration-services/lesson-3-install-ssis-package.md)  
  
![Integration Services 아이콘 (작은)](media/dts-16.gif "Integration Services 아이콘 (작은)")**Integration Services를 사용 하 여 날짜를 알림 설정**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.  
  
  
