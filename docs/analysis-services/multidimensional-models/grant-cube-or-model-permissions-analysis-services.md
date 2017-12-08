---
title: "큐브 또는 모델 권한 부여 (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.roledesignerdialog.cubes.f1
helpviewer_keywords:
- user access rights [Analysis Services], cubes
- cubes [Analysis Services], security
- read/write permissions
- permissions [Analysis Services], cubes
ms.assetid: 55b1456e-2f6b-4101-b316-c926f40304e3
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: b57c8f78162dbfcfe414ed8bc4fcdcedd04c85d0
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="grant-cube-or-model-permissions-analysis-services"></a>큐브 또는 모델 권한 부여(Analysis Services)
  큐브 또는 테이블 형식 모델은 Analysis Services 데이터 모델의 기본 쿼리 개체입니다. 임시 데이터 탐색을 위해 Excel에서 다차원 또는 테이블 형식 데이터에 연결할 경우 일반적으로 가장 먼저 피벗 보고서 개체를 지원하는 데이터 구조로 특정 큐브 또는 테이블 형식 모델을 선택합니다. 이 항목에서는 큐브 또는 테이블 형식 데이터 액세스에 필요한 사용 권한을 부여하는 방법에 대해 설명합니다.  
  
 기본적으로 서버 관리자 또는 데이터베이스 관리자에게 데이터베이스의 큐브를 쿼리할 수 있는 권한이 없다고 생각하는 사람은 없습니다. 관리자가 아닌 사용자가 큐브에 액세스하려면 큐브를 포함한 데이터베이스에 대해 만든 역할의 멤버 자격이 필요합니다. 멤버 자격은 Windows 사용자 또는 그룹 계정에서 지원하며, Active Directory 또는 로컬 컴퓨터에서 정의됩니다. 시작하기에 앞서 생성하려는 역할의 멤버 자격을 할당할 계정을 확인합니다.  
  
 큐브에 대한 **Read** 권한이 있는 경우 차원, 측정값 그룹 및 큐브 뷰에 대한 사용 권한도 갖게 됩니다. 대부분의 관리자는 큐브 수준에서 읽기 권한을 부여한 후 특정 개체 또는 연결된 데이터에 대한 사용 권한을 제한하거나 사용자 ID별로 사용 권한을 제한합니다.  
  
 연속적인 솔루션 배포 중에 역할 정의를 유지하려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서 모델의 필수적인 부분으로 역할을 정의한 다음, 데이터베이스를 게시한 후 데이터베이스 관리자가 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 역할 멤버 자격을 할당하는 것이 가장 좋습니다. 그러나 두 작업 모두에 어느 도구든 사용할 수 있습니다. 연습을 단순화하려면 역할 정의와 멤버 자격 둘 다에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용합니다.  
  
> [!NOTE]  
>  모든 권한을 보유한 서버 관리자 또는 데이터베이스 관리자만 원본 파일에서 서버로 큐브를 배포하거나 역할을 만들고 구성원을 할당할 수 있습니다. 이러한 권한 수준에 대한 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 및 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)를 참조하세요.  
  
#### <a name="step-1-create-the-role"></a>1단계: 역할 만들기  
  
1.  SSMS에서 Analysis Services에 연결합니다. 이 단계에서 도움이 필요한 경우 [클라이언트 응용 프로그램에서 연결&#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)을 참조하세요.  
  
2.  개체 탐색기에서 **데이터베이스** 폴더를 열고 데이터베이스를 선택합니다.  
  
3.  **역할** 을 마우스 오른쪽 단추로 클릭하고 **새 역할**을 선택합니다. 역할이 데이터베이스 수준에서 생성되고 해당 데이터베이스 내 개체에 적용됩니다. 데이터베이스 간에 역할을 공유할 수 없습니다.  
  
4.  **일반** 창에서 이름 및 설명(옵션)을 입력합니다. 이 창에는 모든 권한, 데이터베이스 처리 및 정의 읽기와 같은 몇 가지 데이터베이스 사용 권한도 포함되어 있습니다. 이러한 사용 권한은 큐브 또는 테이블 형식 모델을 쿼리하는 데 필요하지 않습니다. 이러한 권한에 대한 자세한 내용은 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)를 참조하세요.  
  
5.  이름 및 설명(옵션)을 입력한 후 다음 단계를 계속 진행합니다.  
  
#### <a name="step-2-assign-membership"></a>2단계: 멤버 자격 할당  
  
1.  **멤버 자격** 창에서 **추가** 를 클릭하여 이 역할을 사용하는 큐브에 액세스할 Windows 사용자 또는 그룹 계정을 입력합니다. Analysis Services만 Windows 보안 ID를 지원합니다. 이 단계에서는 데이터베이스 로그인을 만들지 않습니다. Analysis Services에서 사용자는 Windows 계정을 통해 연결합니다.  
  
2.  다음 단계인 큐브 사용 권한 설정을 계속 진행합니다.  
  
     데이터 소스 창은 건너뜁니다. 대부분 Analysis Services 데이터에의 일반 소비자에게는 데이터 소스 개체에 대한 사용 권한이 필요하지 않습니다. 이러한 권한 수준에 대한 자세한 내용은 [데이터 원본 개체에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) 를 참조하세요.  
  
#### <a name="step-3-set-cube-permissions"></a>3단계: 큐브 사용 권한 설정  
  
1.  **큐브** 창에서 큐브를 선택한 후 **읽기** 또는 **읽기/쓰기** 권한을 클릭합니다.  
  
     대부분의 작업에는**읽기** 권한이면 충분합니다. **읽기/쓰기** 권한은 쓰기 저장에만 사용되며 처리에는 사용되지 않습니다. 이 기능에 대한 자세한 내용은 [Set Partition Writeback](../../analysis-services/multidimensional-models/set-partition-writeback.md) 을 참조하세요.  
  
     여러 큐브는 물론 역할 만들기 대화 상자에서 만들 수 있는 다른 개체도 선택할 수 있습니다. 큐브에 대한 사용 권한을 부여하면 해당 큐브와 연결된 차원 및 큐브 뷰에 대한 액세스 권한도 부여됩니다. 이미 큐브에 있는 개체를 수동으로 추가할 필요는 없습니다.  
  
     개체 또는 사용자별로 권한을 다르게 부여해야 하는 경우 예를 들어 특정 측정값을 사용할 수 없도록 설정하려는 경우 셀을 비롯하여 특정 개체에 대한 액세스를 허용하거나 거부할 수 있습니다. 자세한 내용은 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 및 [셀 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)를 참조하세요.  
  
2.  여기서 **확인**을 클릭하면 이 역할의 모든 구성원은 지정한 사용 권한 수준으로 큐브에 액세스할 수 있습니다.  
  
     **큐브** 창에서 **드릴스루 및 로컬 큐브**를 통해 또는 드릴스루만 허용된 경우 **드릴스루** 권한을 통해 서버 큐브에서 로컬 큐브를 만들 수 있는 권한을 사용자에게 부여할 수 있습니다.  
  
     마지막으로, 이 창을 통해 큐브에 대한 **데이터베이스 처리** 권한을 부여하여 이 역할의 모든 구성원에게 이 큐브의 데이터를 처리할 권한을 제공할 수 있습니다. 일반적으로 처리는 제한된 작업이므로 해당 작업을 관리자에게만 부여하거나 해당 작업에 대해 구체적으로 별도의 역할을 정의하는 것이 좋습니다. 처리 권한의 모범 사례에 대한 자세한 내용은 [처리 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)를 참조하세요.  
  
#### <a name="step-4-test"></a>4단계: 테스트  
  
1.  Excel을 사용하여 큐브 액세스 권한을 테스트합니다. 또한 아래에서 설명한 것과 동일한 기법(관리자가 아닌 사용자로 응용 프로그램 실행)에 따라 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용할 수 있습니다.  
  
    > [!NOTE]  
    >  Analysis Services 관리자인 경우 사용 권한이 더 적은 역할과 관리자 권한이 결합되므로 격리된 상태에서 역할 권한을 테스트하는 것이 어려워집니다. 테스트를 단순화하려면 테스트 중인 역할에 할당된 계정을 사용하는 SSMS의 두 번째 인스턴스를 여는 것이 좋습니다.  
  
2.  Shift 키를 누른 상태에서 **Excel** 바로 가기를 마우스 오른쪽 단추로 클릭하여 **다른 사용자로 실행** 옵션에 액세스합니다. 이 역할의 멤버 자격을 보유한 Windows 사용자 또는 그룹 계정 중 하나를 입력합니다.  
  
3.  Excel이 열리면 데이터 탭을 사용하여 Analysis Services에 연결합니다. 다른 Windows 사용자로 Excel을 실행하고 있기 때문에 **Windows 인증 사용** 옵션이 역할을 테스트할 때 사용하기에 적합한 자격 증명 유형입니다. 이 단계에서 도움이 필요한 경우 [클라이언트 응용 프로그램에서 연결&#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)을 참조하세요.  
  
     연결에 오류가 발생한 경우 Analysis Services의 포트 구성을 점검하고 서버에서 원격 연결을 수락했는지 확인합니다. 포트 구성에 대해서는 [Analysis Services 액세스를 허용하도록 Windows 방화벽 구성](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md) 을 참조하세요.  
  
#### <a name="step-5-script-role-definition-and-assignments"></a>5단계: 역할 정의 스크립팅 및 할당  
  
1.  마지막 단계로 방금 만든 역할 정의를 캡처하는 스크립트를 생성해야 합니다.  
  
     [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 에서 프로젝트를 재배포하면 프로젝트 내부에서 정의되지 않은 역할 또는 역할 멤버 자격을 덮어씁니다. 재배포 이후 역할 및 역할 멤버 자격을 다시 빌드하는 가장 빠른 방법은 스크립트를 이용하는 것입니다.  
  
2.  SSMS에서 **역할** 폴더로 이동한 후 기존 역할을 마우스 오른쪽 단추로 클릭합니다.  
  
3.  **역할 스크립팅** | **CREATE TO** | **파일**을 선택합니다.  
  
4.  파일을 .xmla 파일 확장명으로 저장합니다. 스크립트를 테스트하려면 현재 역할을 삭제하고 SSMS에서 파일을 열고 F5 키를 눌러 스크립트를 실행합니다.  
  
## <a name="next-step"></a>다음 단계  
 큐브 권한을 구체화하여 셀 또는 차원 데이터에 대한 액세스를 제한할 수 있습니다. 자세한 내용은 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 및 [셀 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services에서 지원하는 인증 방법](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [데이터 마이닝 구조 및 모델 &#40;에 대 한 권한 부여 Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-permissions-on-data-mining-structures-and-models-analysis-services.md)   
 [데이터 원본 개체에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md)  
  
  
