---
title: 파티션 (데이터베이스 복원 대화 상자) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.partitions.f1
ms.assetid: 1ad4dde5-4651-4069-875c-7ab73cd8b4f4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef5ec59980d267a8ead0f69aedb12c6eca5508dc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743479"
---
# <a name="partitions-restore-database-dialog-box-analysis-services---multidimensional-data"></a>파티션(데이터베이스 복원 대화 상자)(Analysis Services - 다차원 데이터)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] **데이터베이스 복원** 대화 상자의 **파티션** 페이지를 사용하여 로컬 파티션을 복원할 위치를 지정하고 원격 파티션 복원 여부와 원격 파티션 복원 시 사용할 원격 백업 파일을 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
 **데이터베이스 복원 대화 상자에서 파티션 페이지를 표시 하려면**  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 **인스턴스의** 데이터베이스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더 또는 **개체 탐색기**의 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **복원**을 클릭한 다음 **페이지 선택**에서 **파티션**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **스크립트**  
 대화 상자에서 선택한 옵션을 기반으로 하는 복원 스크립트를 만듭니다. 복원 스크립트는 ASSL( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripting Language)로 작성됩니다.  
  
 **스크립트** 아이콘을 클릭하면 기본적으로 복원 스크립트가 새 쿼리 창으로 전송됩니다.  
  
 **스크립트** 화살표를 클릭하면 복원 스크립트를 보낼 위치를 선택할 수 있는 메뉴가 표시됩니다.  
  
-   새 쿼리 창으로(기본값)  
  
-   파일로  
  
-   클립보드로  
  
-   작업으로  
  
 **원래 위치로 복원**  
 백업 파일에 포함된 로컬 파티션을 원래 위치로 복원하려면 선택합니다.  
  
 **다른 위치 선택**  
 로컬 파티션을 복원할 다른 위치를 지정하려면 선택합니다.  
  
> [!NOTE]  
>  큐브의 로컬 파티션에 대해 기본 위치 이외의 다른 위치를 지정한 경우에만 해당 파티션의 복원 폴더를 변경할 수 있습니다.  
  
 이 옵션을 선택하면 활성화되는 다음 표는 각 로컬 파티션에 대한 복원 폴더를 지정하는 데 사용됩니다.  
  
|Column|Description|  
|------------|-----------------|  
|**Cube**|로컬 파티션이 포함된 큐브 이름을 표시합니다.|  
|**측정값 그룹**|로컬 파티션이 포함된 측정값 그룹 이름을 표시합니다.|  
|**파티션**|로컬 파티션 이름을 표시합니다.|  
|**크기(MB)**|로컬 파티션의 크기(MB)를 표시합니다.|  
|**원본 폴더**|로컬 파티션이 저장된 원본 폴더 이름을 표시합니다.|  
|**복원 폴더**|로컬 파티션의 복원 폴더 이름을 입력하거나 줄임표 단추(**...**)를 클릭하여 **원격 폴더 찾아보기** 대화 상자를 표시하고 사용할 폴더의 경로를 선택합니다. **원격 폴더 찾아보기** 대화 상자에 대한 자세한 내용은 [원격 폴더 찾아보기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|  
  
 **원격 파티션 복원**  
 원격 백업 파일에 저장된 원격 파티션을 복원하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 원격 파티션에 대한 참조가 백업 파일에 포함된 경우에만 사용할 수 있습니다.  
  
 이 옵션을 선택하면 활성화되는 다음 표는 각 로컬 파티션에 대한 복원 폴더를 지정하는 데 사용됩니다.  
  
|Column|Description|  
|------------|-----------------|  
|**Server**|원격 파티션을 관리하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 이름을 표시합니다.|  
|**데이터 원본**|백업 파일에서 원격 파티션이 포함된 데이터베이스를 나타내는 데이터 원본 이름을 표시합니다.|  
|**백업 파일**|사용할 원격 백업 파일의 전체 경로 및 파일 이름을 입력하거나 줄임표 단추(**...**)를 클릭하여 **데이터베이스 파일 찾기** 대화 상자를 표시하고 사용할 원격 백업 파일의 경로 및 파일 이름을 선택합니다. **데이터베이스 파일 찾기** 대화 상자에 대한 자세한 내용은 [데이터베이스 파일 찾기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|  
|**...**|**원격 파티션 - 고급 설정** 대화 상자를 표시하고 데이터 원본의 연결 문자열과 같은 원격 파티션 복원에 대한 고급 옵션을 수정하려면 클릭합니다. **원격 파티션 - 고급 설정** 대화 상자에 대한 자세한 내용은 [원격 파티션 - 고급 설정 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](remote-partitions-advanced-settings-dialog-analysis-services-multidimensional-data.md)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 복원 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [일반 &#40;데이터베이스 복원 대화 상자&#41; &#40;Analysis Services-다차원 데이터&#41;](general-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services 데이터베이스 백업 및 복원](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
