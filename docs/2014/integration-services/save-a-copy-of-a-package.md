---
title: 패키지 복사본 저장 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, saving
- packages [Integration Services], saving
- saving packages
- SSIS packages, saving
- SQL Server Integration Services packages, saving
ms.assetid: 21482a20-e420-4452-b7eb-8f9fa1929f31
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9d68eac95885b6c40d607237eeb51050a9c6130f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85422540"
---
# <a name="save-a-copy-of-a-package"></a>패키지의 복사본 저장
  이 절차에서는 파일 시스템, 패키지 저장소 또는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 **msdb** 데이터베이스에 패키지 복사본을 저장하는 방법을 설명합니다. 패키지 복사본의 저장 위치를 지정할 때 패키지 이름을 업데이트할 수도 있습니다.  
  
 패키지 저장소에는 **msdb** 데이터베이스와 파일 시스템의 폴더가 모두 포함될 수도 있고, **msdb**또는 파일 시스템의 폴더 중 하나만 포함될 수도 있습니다. **msdb**에서 패키지는 **sysssispackages** 테이블에 저장됩니다. 이 테이블에는 패키지가 속한 논리적 폴더를 식별하는 **folderid** 열이 있습니다. 논리적 폴더를 사용하면 파일 시스템의 폴더를 통해 파일 시스템에 저장된 패키지를 그룹화할 수 있는 것과 동일한 방식으로 **msdb** 에 저장된 패키지를 그룹화할 수 있습니다. **msdb** 의 **sysssispackagefolders** 테이블에 있는 행은 폴더를 정의합니다.  
  
 **msdb** 가 패키지 저장소의 일부로 정의되어 있지 않은 경우 **패키지 경로** 옵션에서 SQL Server를 선택할 때 패키지를 기존 논리적 폴더와 계속 연결할 수 있습니다.  
  
> [!NOTE]  
>  패키지 복사본을 저장하려면 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너에서 패키지를 열어야 합니다.  
  
### <a name="to-save-a-copy-of-a-package"></a>패키지 복사본을 저장하려면  
  
1.  솔루션 탐색기에서 복사본을 저장하려는 패키지를 두 번 클릭합니다.  
  
2.  **파일** 메뉴에서 ** \<package file> 다른 이름으로 복사본 저장**을 클릭 합니다.  
  
3.  **패키지 복사본 저장** 대화 상자의 **패키지 위치** 목록에서 패키지 위치를 선택합니다.  
  
4.  위치가 **SQL Server** 또는 **SSIS 패키지 저장소**인 경우 서버 이름을 제공합니다.  
  
5.  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로 저장하는 경우에는 인증 유형을 지정하고 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하는 경우에는 사용자 이름과 암호를 제공합니다.  
  
6.  패키지 경로를 지정하려면 해당 경로를 직접 입력하거나, 찾아보기 단추 **(…)** 를 클릭하고 패키지 위치를 지정합니다. 패키지의 기본 이름은 Package입니다. 필요에 맞게 패키지 이름을 업데이트할 수도 있습니다.  
  
     **패키지 경로** 옵션으로 **SQL Server** 를 선택하면 패키지 경로는 **msdb** 의 논리적 폴더와 패키지 이름으로 구성됩니다. 예를 들어 DownloadMonthlyData 패키지가 MSDB 폴더( **msdb**에 있는 논리적 루트 폴더의 기본 이름) 내의 Finance 폴더와 연결되어 있으면 DownloadMonthlyData 패키지의 패키지 경로는 MSDB/Finance/DownloadMonthlyData가 됩니다.  
  
     **패키지 경로** 옵션으로 **SSIS 패키지 저장소** 를 선택하면 패키지 경로는 Integration Services 서비스에서 관리하는 폴더로 구성됩니다. 예를 들어 UpdateDeductions 패키지가 Integration Services 서비스에서 관리하는 파일 시스템 폴더 내의 HumanResources 폴더에 있으면 해당 패키지 경로는 /File System/HumanResources/UpdateDeductions가 됩니다. 마찬가지로 PostResumes 패키지가 MSDB 폴더 내의 HumanResources 폴더와 연결되어 있으면 해당 패키지 경로는 MSDB/HumanResources/PostResumes가 됩니다.  
  
     **패키지 경로** 옵션으로 **파일 시스템** 을 선택하면 패키지 경로는 파일 시스템에서의 위치와 파일 이름으로 구성됩니다. 예를 들어 패키지 이름이 UpdateDemographics이면 패키지 경로는 C:\HumanResources\Quarterly\UpdateDemographics.dtsx와 같이 됩니다.  
  
7.  패키지 보호 수준을 검토합니다.  
  
8.  선택적으로 **보호 수준** 상자 옆에 있는 찾아보기 단추 **(…)** 를 클릭하여 보호 수준을 바꿉니다.  
  
    -   **패키지 보호 수준** 대화 상자에서 다른 보호 수준을 선택합니다.  
  
    -   **확인**을 클릭합니다.  
  
9. **확인**을 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSIS&#41; 패키지 Integration Services &#40;](../../2014/integration-services/integration-services-ssis-packages.md)   
 [Integration Services 서비스 구성&#40;SSIS 서비스&#41;](service/integration-services-service-ssis-service.md)  
  
  
