---
title: "패키지 보호 수준 설정 또는 변경 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "암호 [Integration Services]"
  - "패키지 [Integration Services], 보안"
  - "보안 [Integration Services], 보호 수준"
  - "패키지 보호 수준 [Integration Services]"
ms.assetid: 904a5580-82ba-4a26-b0c5-d1c989975f61
caps.latest.revision: 10
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 10
---
# 패키지 보호 수준 설정 또는 변경
  패키지 내용과 패키지에 포함된 중요한 값(예: 암호)에 대한 액세스를 제어하려면 **ProtectionLevel** 속성의 값을 설정합니다. 프로젝트에 포함된 패키지는 프로젝트 생성을 위해 프로젝트와 보호 수준이 동일해야 합니다. 프로젝트에서 **ProtectionLevel** 속성을 변경한 경우 패키지에 대한 프록시 설정을 수동으로 업데이트해야 합니다.  
  
 패키지 수명 주기의 여러 단계에서 사용 중인 패키지에 적합한 **ProtectionLevel** 설정을 결정하는 방법은 [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)을 참조하십시오. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 보안 기능에 대한 개요는 [보안 개요&#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md)를 참조하세요.  
  
 이 항목의 절차에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 또는 dtutil 명령 프롬프트 유틸리티를 사용하여 **ProtectionLevel** 속성의 값을 설정합니다.  
  
> [!NOTE]  
>  이 항목의 절차 외에도 일반적으로 패키지를 가져오거나 내보낼 때 패키지의 **ProtectionLevel** 속성을 설정하거나 변경할 수 있습니다. 또한 **ProtectionLevel** 가져오기 및 내보내기 마법사를 사용하여 패키지를 저장할 때도 패키지의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 속성을 변경할 수 있습니다.  
  
### SQL Server Data Tools에서 패키지 보호 수준을 설정하거나 변경하려면  
  
1.  **패키지 보호 수준 설정** 항목에서 [ProtectionLevel](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)속성에 사용할 수 있는 값을 검토하고 사용 중인 패키지에 적합한 값을 결정합니다.  
  
2.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 패키지가 들어 있는 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 프로젝트를 엽니다.  
  
3.  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 패키지를 엽니다.  
  
4.  속성 창에 패키지 속성이 표시되지 않으면 디자인 화면을 클릭합니다.  
  
5.  속성 창의 **보안** 그룹에서 **ProtectionLevel** 속성에 적합한 값을 선택합니다.  
  
     암호가 필요한 보호 수준을 선택한 경우 암호를 **PackagePassword** 속성의 값으로 입력합니다.  
  
6.  **파일** 메뉴에서 **선택한 항목 저장** 을 선택하여 수정한 패키지를 저장합니다.  
  
### 명령 프롬프트에서 패키지 보호 수준을 설정하거나 변경하려면  
  
1.  **패키지 보호 수준 설정** 항목에서 [ProtectionLevel](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md)속성에 사용할 수 있는 값을 검토하고 사용 중인 패키지에 적합한 값을 결정합니다.  
  
2.  **dtutil Utility** 항목에서 [Encrypt](../../integration-services/dtutil-utility.md)옵션에 대한 매핑을 검토하고 선택한 **ProtectionLevel** 속성의 값으로 사용하기에 적합한 정수를 결정합니다.  
  
3.  명령 프롬프트 창을 엽니다.  
  
4.  명령 프롬프트에서 **ProtectionLevel** 속성을 설정할 패키지가 들어 있는 폴더로 이동합니다.  
  
     다음 단계에 나오는 구문 예에서는 이 폴더가 현재 폴더라고 가정합니다.  
  
5.  다음 예 중 하나와 비슷한 명령을 사용하여 패키지 보호 수준을 설정하거나 변경합니다.  
  
    -   다음 명령은 파일 시스템에 있는 개별 패키지의 **ProtectionLevel** 속성을 수준 2, "암호로 중요한 데이터 암호화"로 설정하고 암호로 "strongpassword"를 사용합니다.  
  
         `dtutil.exe /file "C:\Package.dtsx" /encrypt file;"C:\Package.dtsx";2;strongpassword`  
  
    -   다음 명령은 파일 시스템의 특정 폴더에 있는 모든 패키지의 **ProtectionLevel** 속성을 수준 2, "암호로 중요한 데이터 암호화"로 설정하고 암호로 "strongpassword"를 사용합니다.  
  
         `for %f in (*.dtsx) do dtutil.exe /file %f /encrypt file;%f;2;strongpassword`  
  
         배치 파일에서 비슷한 명령을 사용할 경우 배치 파일에 파일 자리 표시자로 "%f" 대신 "%%f"를 입력합니다.  
  
## 관련 항목:  
 [dtutil 유틸리티](../../integration-services/dtutil-utility.md)  
  
  