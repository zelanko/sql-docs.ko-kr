---
title: 데이터베이스 대화 상자 (Analysis Services-다차원 데이터) 백업 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.Backup.f1
ms.assetid: 7811ce7d-6c37-4189-bfa6-ef36fb4932db
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 741f3b761e4c6645cee7c43c3e8f593dbad13219
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62650467"
---
# <a name="backup-database-dialog-box-analysis-services---multidimensional-data"></a>데이터베이스 백업 대화 상자(Analysis Services - 다차원 데이터)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 **데이터베이스 백업** 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 백업 파일(.abf) 형식을 사용하는 백업 파일에 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 백업할 수 있습니다.  
  
> [!IMPORTANT]  
>  백업 명령을 실행하는 사용자에게는 각 백업 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
 **데이터베이스 백업 대화 상자를 표시 하려면**  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 **인스턴스의** 데이터베이스 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 폴더 또는 **개체 탐색기**의 데이터베이스를 마우스 오른쪽 단추로 클릭한 다음 **백업**을 클릭합니다.  
  
## <a name="options"></a>변수  
 **스크립트**  
 대화 상자에서 선택한 옵션을 기반으로 하는 백업 스크립트를 만듭니다. 복원 스크립트는 ASSL( [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Scripting Language)로 작성됩니다.  
  
 **스크립트** 아이콘을 클릭하면 기본적으로 백업 스크립트가 새 쿼리 창으로 전송됩니다.  
  
 **스크립트** 화살표를 클릭하면 백업 스크립트를 보낼 위치를 선택할 수 있는 메뉴가 표시됩니다.  
  
-   새 쿼리 창으로(기본값)  
  
-   파일로  
  
-   클립보드로  
  
-   작업으로  
  
 **데이터베이스 백업**  
 현재 선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스의 이름을 표시합니다.  
  
 **백업 파일**  
 사용할 백업 파일의 전체 경로 및 파일 이름을 입력합니다.  
  
 **찾아보기**  
 **다른 이름으로 파일 저장** 대화 상자를 표시하고 사용할 백업 파일의 경로 및 파일 이름을 선택하려면 클릭합니다. **다른 이름으로 파일 저장** 대화 상자에 대한 자세한 내용은 [다른 이름으로 파일 저장 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.  
  
 **파일 덮어쓰기 허용**  
 기존 백업 파일 또는 원격 백업 파일이 있는 경우 덮어쓰려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션을 선택하지 않은 경우 **백업 파일** 에서 지정한 백업 파일 또는 **원격 백업 파일** 에서 지정한 원격 백업 파일이 존재하면 오류가 발생합니다.  
  
 **압축 적용**  
 백업 파일 및 원격 백업 파일(지정한 경우)의 내용을 압축하려면 선택합니다.  
  
 **백업 파일 암호화**  
 **암호**에 입력한 암호를 사용하여 백업 파일을 암호화하려면 선택합니다.  
  
 **암호**  
 백업 파일 및 원격 백업 파일(지정한 경우)을 암호화하는 데 사용할 암호를 입력합니다.  
  
> [!NOTE]  
>  이 옵션은 **백업 파일 암호화** 를 선택한 경우에만 사용할 수 있습니다.  
  
 **암호 확인**  
 백업 파일 및 원격 백업 파일(지정된 경우)의 암호를 확인하려면 **암호** 에 입력한 암호를 입력합니다.  
  
> [!NOTE]  
>  이 옵션은 **백업 파일 암호화** 를 선택한 경우에만 사용할 수 있습니다.  
  
 **원격 파티션 백업**  
 백업 파일에 원격 파티션에 대한 위치 정보 및 데이터를 포함하려면 선택합니다.  
  
> [!NOTE]  
>  이 옵션은 현재 선택한 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스가 원격 파티션을 사용하는 경우에만 사용할 수 있습니다.  
  
 **원격 파티션 백업 위치**  
 원격 파티션에 대한 데이터 및 메타데이터를 백업하는 데 사용된 원격 백업 파일을 비롯하여 선택한 데이터베이스와 연결된 원격 파티션의 위치를 표시합니다. 사용할 수 있는 열은 다음과 같습니다.  
  
|Column|Description|  
|------------|-----------------|  
|**Server**|원격 파티션을 관리하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 표시합니다.|  
|**데이터베이스 백업**|원격 파티션을 포함하는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 데이터베이스를 표시합니다.|  
|**파티션 목록**|**데이터베이스**에 표시된 데이터베이스가 포함하는 원격 파티션의 목록을 표시합니다.|  
|**원격 백업 파일**|사용할 원격 백업 파일의 전체 경로 및 파일 이름을 입력하거나 줄임표 단추(**...**)를 클릭하여 **다른 이름으로 파일 저장** 대화 상자를 표시하고 사용할 원격 백업 파일의 경로 및 파일 이름을 선택합니다. **다른 이름으로 파일 저장** 대화 상자에 대한 자세한 내용은 [다른 이름으로 파일 저장 대화 상자&#40;Analysis Services - 다차원 데이터&#41;](save-file-as-dialog-box-analysis-services-multidimensional-data.md)를 참조하세요.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Designers and Dialog Boxes &#40;다차원 데이터&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Analysis Services 데이터베이스 백업 및 복원](multidimensional-models/backup-and-restore-of-analysis-services-databases.md)  
  
  
