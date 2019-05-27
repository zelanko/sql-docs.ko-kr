---
title: 일반 (데이터베이스 복원 대화 상자) (Analysis Services-다차원 데이터) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.restoredbdialog.f1
ms.assetid: 319e7ef5-c9c7-4e50-8690-02a90aed006f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2ebc1bc72a15545412adcc71d10feb08f3f05b16
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080951"
---
# <a name="general-restore-database-dialog-box-analysis-services---multidimensional-data"></a>일반(데이터베이스 복원 대화 상자)(Analysis Services - 다차원 데이터)
  **에서** 데이터베이스 복원 **대화 상자의** 일반 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 페이지를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 복원할 때 사용할 백업 파일 및 일반 설정을 지정할 수 있습니다.  
  
> [!IMPORTANT]  
>  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
> [!NOTE]  
>  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
 **데이터베이스 복원 대화 상자에서 일반 페이지를 표시 하려면**  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 **인스턴스의** 데이터베이스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더 또는 **개체 탐색기**의 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **복원**을 클릭한 다음 **페이지 선택**에서 **일반**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **스크립트**  
 대화 상자에서 선택한 옵션을 기반으로 하는 복원 스크립트를 만듭니다. 복원 스크립트는 ASSL( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripting Language)로 작성됩니다.  
  
 **스크립트** 아이콘을 클릭하면 기본적으로 복원 스크립트가 새 쿼리 창으로 전송됩니다.  
  
 **스크립트** 화살표를 클릭하면 복원 스크립트를 보낼 위치를 선택할 수 있는 메뉴가 표시됩니다.  
  
-   새 쿼리 창으로(기본값)  
  
-   파일로  
  
-   클립보드로  
  
-   작업으로  
  
 **데이터베이스 복원**  
 복원할 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 선택합니다.  
  
 **백업 파일에서**  
 선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 복원할 백업 파일을 선택합니다.  
  
 **찾아보기**  
 **데이터베이스 파일 찾기** 대화 상자를 표시하고 사용할 백업 파일의 경로 및 파일 이름을 선택하려면 클릭합니다. **데이터베이스 파일 찾기** 대화 상자에 대한 자세한 내용은 [데이터베이스 파일 찾기 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](locate-database-files-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **데이터베이스 덮어쓰기 허용**  
 선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 모든 기존 개체에 대해 선택한 백업 파일의 내용을 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 에서 복원할 수 있게 하려면 선택합니다.  
  
 **보안 정보 포함**  
 백업 파일에 저장된 보안 정보를 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스로 복사하려면 선택합니다.  
  
 이 옵션을 선택하면 사용 가능한 드롭다운 목록에서 보안 정보의 양을 선택할 수 있습니다. 사용할 수 있는 옵션은 다음과 같습니다.  
  
|옵션|Description|  
|------------|-----------------|  
|**모두 복사**|백업 파일에 포함된 데이터베이스 역할 및 해당 역할과 연결된 사용자 계정을 복원합니다.|  
|**멤버 등록 생략**|백업 파일에 포함된 데이터베이스 역할만 복원하고 해당 역할과 연결된 사용자 계정은 복원하지 않습니다.|  
  
 **암호**  
 백업 파일이 암호화된 경우 백업 파일을 암호화하는 데 사용한 암호를 입력합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 복원 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [파티션 &#40;데이터베이스 복원 대화 상자&#41; &#40;Analysis Services-다차원 데이터&#41;](partitions-restore-database-dialog-box-analysis-services-multidimensional-data.md)   
 [Analysis Services 데이터베이스 백업 및 복원](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
