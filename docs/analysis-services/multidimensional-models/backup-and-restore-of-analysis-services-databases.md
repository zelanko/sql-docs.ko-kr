---
title: Analysis Services 데이터베이스의 백업 및 복원 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e43357e843f28133f7bb2f5cd9db078ee4bace27
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024450"
---
# <a name="backup-and-restore-of-analysis-services-databases"></a>Analysis Services 데이터베이스 백업 및 복원
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에는 데이터베이스와 해당 개체를 특정 시점에서 복구할 수 있도록 백업 및 복원이 포함되어 있습니다. 백업 및 복원은 데이터베이스를 업그레이드한 서버에 마이그레이션하거나 서버 간에 데이터베이스를 이동하거나 데이터베이스를 프로덕션 서버에 배포하는 데 사용할 수 있는 기술이기도 합니다. 중요한 데이터에 대한 백업 계획이 없는 경우 데이터 복구를 위해 가능한 한 빨리 계획을 수립하고 구현해야 합니다.  
  
 백업 및 복원 명령은 배포된 Analysis Services 데이터베이스에서 수행됩니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 프로젝트 및 솔루션에 대해 원본 제어를 사용하여 특정 버전의 원본 파일을 복구한 다음 사용하고 있는 원본 제어 시스템의 리포지토리에 대한 데이터 복구 계획을 만들어야 합니다.  
  
 원본 데이터를 포함하는 전체 백업의 경우 세부 데이터가 포함된 데이터베이스를 백업해야 합니다. 특히 ROLAP 또는 DirectQuery 데이터베이스 저장소를 사용하는 경우 Analysis Services 데이터베이스와 별개의 외부 SQL Server 관계형 데이터베이스에 세부 데이터가 저장됩니다. 그렇지 않으면 모든 개체가 테이블 형식 개체 또는 다차원 개체인 경우 Analysis Services 백업에 메타데이터와 원본 데이터 모두가 포함됩니다.  
  
 백업을 자동화하면 지정한 자동 백업 빈도만큼 데이터 스냅숏이 항상 최신 상태로 유지된다는 장점이 있습니다. 자동화된 스케줄러를 사용하면 백업을 잊지 않고 수행할 수 있습니다. 또한 데이터베이스 복원을 자동화할 수 있으며 이러한 자동화 역시 데이터를 복제하는 좋은 방법이 될 수 있으나 이때 복제의 대상 위치가 되는 인스턴스의 암호화 키 파일을 반드시 백업해야 합니다. 동기화 기능은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 복제 전용이며 최신이 아닌 데이터에 대해서만 사용할 수 있습니다. 여기에 언급된 모든 기능은 XML/A 명령을 사용하거나 AMO를 통해 프로그래밍 방식으로 실행하여 사용자 인터페이스를 통해 구현할 수 있습니다. 백업 전략에 대한 자세한 내용은 [SQL Server 2005 Analysis Services를 사용한 백업 전략](http://go.microsoft.com/fwlink/?LinkId=81888)을 참조하십시오.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
-   [백업 준비](#bkmk_prep)  
  
-   [다차원 데이터베이스 또는 테이블 형식 데이터베이스 백업](#bkmk_cube)  
  
-   [Analysis Services 데이터베이스 복원](#bkmk_restore)  
  
##  <a name="bkmk_prereq"></a> 필수 구성 요소  
 Analysis Services 인스턴스에 대한 관리 권한이나 백업하려는 데이터베이스에 대한 모든 권한(관리자)을 가지고 있어야 합니다.  
  
 복원 위치는 백업이 수행된 인스턴스와 동일한 버전 또는 상위 버전인 Analysis Services 인스턴스여야 합니다. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스의 데이터베이스를 이전 버전의 Analysis Services로 복원할 수는 없지만 최신 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 인스턴스에서 SQL Server 2012와 같은 이전 버전의 데이터베이스를 복원하는 것은 일반적인 일입니다.  
  
 복원 위치는 서버 유형이 동일해야 합니다. 테이블 형식 데이터베이스는 테이블 형식 모드로 실행되는 Analysis Services로만 복원할 수 있습니다. 다차원 데이터베이스에는 다차원 모드에서 실행되는 인스턴스가 필요합니다.  
  
##  <a name="bkmk_prep"></a> 백업 준비  
 백업을 준비할 때는 다음 검사 목록을 사용합니다.  
  
-   백업 파일을 저장할 위치를 확인합니다. 원격 위치를 사용하는 경우 해당 위치를 UNC 폴더로 지정해야 합니다. UNC 경로에 액세스할 수 있는지 확인합니다.  
  
-   폴더에 대한 사용 권한을 확인하여 Analysis Services 서비스 계정에 폴더에 대한 읽기/쓰기 권한이 있는지 확인합니다.  
  
-   대상 서버에 디스크 공간이 충분히 있는지 확인합니다.  
  
-   같은 이름의 기존 파일이 있는지 확인합니다. 동일한 이름을 가진 파일이 이미 있는 경우 파일을 덮어쓰도록 옵션을 지정하지 않으면 백업이 실패합니다.  
  
##  <a name="bkmk_cube"></a> 다차원 데이터베이스 또는 테이블 형식 데이터베이스 백업  
 관리자는 데이터베이스의 크기에 관계없이 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 단일 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 백업 파일(.abf)로 백업할 수 있습니다. 단계별 지침은 [Analysis Services 데이터베이스 복원 방법(TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Backup_an_Analysis_Services_Database.html) 및 [Analysis Services 데이터베이스 백업 자동화(TechMantra)](http://www.mytechmantra.com/LearnSQLServer/Automate_Backup_of_Analysis_Services_Database.html)를 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]를 로드 하 고 쿼리에 사용 되는 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] SharePoint 환경에서 데이터 모델에는 SharePoint 콘텐츠 데이터베이스에서 해당 모델을 로드 합니다. 이러한 콘텐츠 데이터베이스는 관계형이므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 관계형 데이터베이스 엔진에서 실행됩니다. 따라서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 모델에 대해 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 백업 및 복원 전략이 없습니다. SharePoint 콘텐츠에 대한 재해 복구 계획이 있는 경우 해당 계획은 콘텐츠 데이터베이스에 저장된 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 데이터 모델을 포함합니다.  
  
 **원격 파티션**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 원격 파티션이 포함된 경우 원격 파티션도 백업해야 합니다. 원격 파티션이 있는 데이터베이스를 백업하는 경우 각 원격 서버에 있는 모든 원격 파티션이 각 해당 원격 서버의 단일 파일에 따로 백업됩니다. 그러므로 해당 호스트 컴퓨터 외부에 원격 백업을 만들려면 지정한 저장소 영역에 해당 파일을 직접 복사해야 합니다.  
  
 **백업 파일의 내용**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업하면 데이터베이스 개체에 사용되는 저장소 모드에 따라 내용이 달라지는 백업 파일이 생성됩니다. 이러한 백업 내용상의 차이는 각 저장소 모드로 인해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내에 서로 다른 정보 집합이 저장되기 때문에 발생합니다. 예를 들어 다차원 HOLAP(하이브리드 OLAP) 파티션 및 차원은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 집계 및 메타데이터를 저장하는 반면 ROLAP(관계형 OLAP) 파티션 및 차원은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 메타데이터만 저장합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 실제 내용이 각 파티션의 저장소 모드에 따라 달라지기 때문에 백업 파일의 내용도 달라집니다. 다음 표에서는 개체에 사용되는 저장소 모드에 따른 백업 파일의 내용을 보여 줍니다.  
  
|저장소 모드|백업 파일의 내용|  
|------------------|-----------------------------|  
|다차원 MOLAP 파티션 및 차원|메타데이터, 원본 데이터 및 집계|  
|다차원 HOLAP 파티션 및 차원|메타데이터 및 집계|  
|다차원 ROLAP 파티션 및 차원|메타데이터|  
|테이블 형식 메모리 내 모델|메타데이터 및 원본 데이터|  
|테이블 형식 DirectQuery 모델|메타데이터만|  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업해도 관계형 데이터베이스와 같은 기본 데이터 원본의 데이터는 백업되지 않으며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 내용만 백업됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업할 때는 다음을 선택할 수 있습니다.  
  
-   모든 데이터베이스 백업 압축 여부. 기본적으로 백업이 압축됩니다.  
  
-   백업 파일의 내용을 암호화한 다음 파일을 암호 해독 및 복원하기 전에 암호를 입력하도록 할지 여부. 기본적으로 백업된 데이터는 암호화되지 않습니다.  
  
    > [!IMPORTANT]  
    >  백업 명령을 실행하는 사용자에게는 각 백업 파일에 대해 지정한 백업 위치에 쓸 수 있는 권한이 있어야 합니다. 또한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 백업할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 백업하는 방법은 [백업 옵션](../../analysis-services/multidimensional-models/backup-options.md)을 참조하세요.  
  
##  <a name="bkmk_restore"></a> Analysis Services 데이터베이스 복원  
 관리자는 하나 이상의 백업 파일에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원할 수 있습니다.  
  
> [!NOTE]  
>  백업 파일이 암호화되어 있는 경우에는 백업을 수행하는 동안 지정한 암호를 입력해야 해당 파일을 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원할 수 있습니다.  
  
 복원을 수행하는 동안에는 다음을 수행할 수 있습니다.  
  
-   원래 데이터베이스 이름을 사용하여 데이터베이스 복원 또는 새 데이터베이스 이름 지정  
  
-   기존 데이터베이스 덮어쓰기. 데이터베이스를 덮어쓰려면 기존 데이터베이스를 덮어쓸 것이라는 점을 명시적으로 지정해야 합니다.  
  
-   기존 보안 정보를 복원할지, 아니면 보안 멤버 등록 정보를 건너뛸지 선택  
  
-   복원할 각 파티션에 대한 복원 폴더를 복원 명령으로 변경하도록 선택. 로컬 파티션은 데이터베이스 복원의 대상 위치가 되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 모든 로컬 폴더 위치에 복원될 수 있습니다. 원격 파티션은 로컬 서버를 제외한 모든 서버의 모든 폴더에 복원될 수 있습니다. 원격 파티션은 로컬이 될 수 없습니다.  
  
    > [!IMPORTANT]  
    >  복원 명령을 실행하는 사용자는 각 백업 파일에 대해 지정한 백업 위치에서 읽을 수 있는 권한을 가져야 합니다. 서버에 설치되지 않은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 복원하려면 사용자도 해당 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버여야 합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 덮어쓰려면 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 서버 역할의 멤버이거나 복원할 데이터베이스에 대한 모든 권한(관리자 권한)이 있는 데이터베이스 역할의 멤버여야 합니다.  
  
    > [!NOTE]  
    >  기존 데이터베이스를 복원한 다음에는 해당 데이터베이스를 복원한 사용자가 보유하고 있는 복원된 데이터베이스 액세스 권한이 손실될 수 있습니다. 이러한 액세스 권한 손실은 백업 수행 당시에 사용자가 서버 역할의 멤버가 아니었거나 모든 권한(관리자)이 있는 데이터베이스 역할의 멤버가 아니었던 경우 발생할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 복원 방법은 [복원 옵션](../../analysis-services/multidimensional-models/restore-options.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 백업, 복원 및 동기화&#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/backing-up-restoring-and-synchronizing-databases-xmla.md)   

  
  
