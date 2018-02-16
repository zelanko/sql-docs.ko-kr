---
title: "개체 및 작업 (Analysis Services)에 대 한 액세스 권한을 부여 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.general.f1
- sql13.asvs.roledesignerdialog.membership.f1
helpviewer_keywords:
- access rights [Analysis Services], users
- permissions [Analysis Services], users
- security [Analysis Services], user access
- user access rights [Analysis Services]
- granting permissions [Analysis Services], users
ms.assetid: af28524e-5eca-4dce-a050-da4f406ee1c7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 956638a01fc1280d16bb6fd7a7ddade1978ceb2f
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/15/2018
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>개체 및 작업에 대한 액세스 승인(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 내의 큐브, 차원 및 마이닝 모델에 대한 비관리자 사용자 액세스는 하나 이상의 데이터베이스 역할의 구성원 자격을 통해 부여됩니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자는 이러한 데이터베이스 역할을 만들고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체에 대한 읽기 또는 읽기/쓰기 권한을 부여한 다음 각 역할에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자 및 그룹을 추가합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 사용자나 그룹이 속한 각 데이터베이스 역할과 연관된 사용 권한을 결합하여 특정 Windows 사용자나 그룹에 대한 유효 사용 권한을 결정합니다. 따라서 한 데이터베이스 역할은 사용자나 그룹에 차원, 측정값 또는 특성을 볼 수 있는 사용 권한을 부여하지 않지만 다른 데이터베이스 역할이 이 사용자나 그룹에 사용 권한을 부여하는 경우 해당 사용자나 그룹은 개체를 볼 수 있게 됩니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 관리자 역할의 멤버와 모든 권한(관리자)한을 가진 데이터베이스 역할의 멤버는 데이터베이스의 모든 데이터와 메타데이터에 액세스할 수 있으며 추가 사용 권한 없이 특정 개체를 볼 수 있습니다. 또한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 역할의 멤버는 데이터베이스의 모든 개체에 제한 없이 액세스할 수 있고 데이터베이스 내에서 모든 권한(관리자)을 가진 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 역할의 멤버는 해당 데이터베이스의 모든 개체에 제한 없이 액세스할 수 있습니다. 처리처럼 특별한 관리 작업은 낮은 수준의 권한을 가진 별도의 역할을 통해 승인될 수 있습니다. 자세한 내용은 [처리 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)를 참조하세요.  
  
## <a name="list-roles-defined-for-your-database"></a>데이터베이스에 대해 정의된 역할 나열  
 관리자는 SQL Server Management Studio에서 간단한 DMV 쿼리를 실행하여 서버에 정의된 모든 역할의 목록을 가져올 수 있습니다.  
  
1.  SSMS에서 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **새 쿼리** | **MDX**를 선택합니다.  
  
2.  다음 쿼리를 입력하고 F5 키를 눌러 실행합니다.  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     결과에는 데이터베이스 이름, 설명, 역할 이름 및 마지막으로 수정한 날짜가 포함됩니다. 이 정보를 바탕으로 개별 데이터베이스를 진행하여 특정 역할의 구성원 자격과 권한을 확인할 수 있습니다.  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>Analysis Services 권한에 대한 하향식 개요  
 이 섹션에서는 권한 구성에 대한 기본적인 워크플로를 설명합니다.  
  
 **1단계: 서버 관리**  
  
 첫 번째 단계로, 서버 수준에서 관리자 권한을 가질 사람을 결정합니다. 설치 중 SQL Server를 설치하는 로컬 관리자는 하나 이상의 Windows 계정을 Analysis Services 서버 관리자로 지정해야 합니다. 서버 관리자는 서버의 개체 보기, 수정, 삭제 권한 또는 연결된 데이터 보기 권한을 포함하여 서버에 대해 가능한 모든 권한을 가집니다. 설치가 완료된 후 서버 관리자는 계정을 추가하거나 제거하여 이 역할에 대한 구성원 자격을 변경할 수 있습니다. 이 권한 수준에 대한 자세한 내용은 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 를 참조하세요.  
  
 **2단계: 데이터베이스 관리**  
  
 다음으로, 테이블 형식 또는 다차원 솔루션이 생성된 후 서버에 데이터베이스로 배포됩니다. 서버 관리자는 해당 데이터베이스에 대해 모든 권한을 지닌 역할을 정의하여 데이터베이스 관리 작업을 위임할 수 있습니다. 이 역할의 구성원은 데이터베이스의 개체를 처리하거나 쿼리할 뿐만 아니라 데이터베이스 자체 내의 큐브, 차원 및 기타 개체에 대해 추가 역할을 만들 수 있습니다. 자세한 내용은 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)를 참조하세요.  
  
 **3단계: 쿼리 및 작업 처리에 대해 큐브 또는 모델 액세스 활성화**  
  
 기본적으로 서버 및 데이터베이스 관리자만 큐브 또는 테이블 형식의 모델에 액세스할 수 있습니다. 조직 내 다른 사람들도 이러한 데이터 구조를 사용할 수 있도록 하려면 **Read** 권한을 지정하는 권한과 함께 Windows 사용자 및 그룹 계정을 큐브 또는 모델에 매핑하는 추가 역할 할당이 필요합니다. 자세한 내용은 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)를 참조하세요.  
  
 처리 태스크는 다른 관리 기능과 격리되어 서버 및 데이터베이스 관리자가 이 태스크를 다른 사람에게 위임하거나 예약 소프트웨어를 실행하는 서비스 계정을 지정하여 무인 처리를 구성할 수 있습니다. 자세한 내용은 [처리 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md)를 참조하세요.  
  
> [!NOTE]  
>  사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 데이터를 로드하는 기본 관계형 데이터베이스에 있는 관계형 테이블에 대해 사용 권한이 필요하지 않으며 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스가 실행되고 있는 컴퓨터에서 파일 수준의 사용 권한도 필요로 하지 않습니다.  
  
 **4단계: 내부 큐브 개체에 대한 액세스를 허용하거나 거부합니다.**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 데이터 모델 내의 차원 구성원 및 셀을 포함하여 각 개체에 대한 권한을 설정하는 보안 설정을 제공합니다. 자세한 내용은 [차원 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) 및 [셀 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)를 참조하세요.  
  
 사용자 ID에 따라 권한을 다르게 설정할 수도 있습니다. 이를 종종 동적 보안이라고 하며, [UserName&#40;MDX&#41;](../../mdx/username-mdx.md) 함수를 사용하여 구현됩니다.  
  
## <a name="best-practices"></a>최선의 구현 방법  
 권한을 잘 관리하기 위해 다음과 유사한 방법을 제안합니다.  
  
1.  역할을 관리하는 사람은 누구라도 역할에서 허용하는 것을 알 수 있도록 기능별 역할(예: dbadmin, cubedeveloper, processadmin)을 만듭니다. 다른 곳에서 설명한 것처럼, 모델 정의에 역할을 정의하여 이러한 역할을 이후 솔루션 배포에 대해서 유지할 수 있습니다.  
  
2.  Active Directory에 해당 Windows 보안 그룹을 만든 다음 Active Directory의 보안 그룹이 적절한 개별 계정을 포함하도록 관리합니다. 그러면 조직에서 계정 관리에 사용하는 도구 및 프로세스에 이미 익숙한 보안 전문가에게 보안 그룹 구성원 자격의 책임을 맡기게 됩니다.  
  
3.  모델이 원본 파일에서 서버로 재배포될 때마다 역할 할당을 빠르게 복제할 수 있도록 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에 스크립트를 생성합니다. 스크립트를 빠르게 생성하는 방법에 대한 자세한 내용은 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)를 참조하세요.  
  
4.  역할의 범위와 구성원 자격을 반영하는 명명 규칙을 적용합니다. 역할 이름은 디자인 및 관리 도구에만 표시되므로 큐브 보안 전문가에게 맞는 명명 규칙을 사용하세요. 예를 들어 **processadmin-windowsgroup1** 은 각 Windows 사용자 계정이 **windowsgroup1** 보안 그룹의 멤버인 조직의 사람들에 대한 처리 권한과 함께 읽기 권한을 나타냅니다.  
  
     계정 정보를 포함하면 여러 역할에서 어느 계정이 사용되는지 추적하는 데 도움이 될 수 있습니다. 역할은 가산적이기 때문에, **windowsgroup1** 과 연결되어 있는 결합된 역할은 해당 보안 그룹에 속하는 사람들에 대해 유효한 권한 집합을 구성합니다.  
  
5.  큐브 개발자는 개발 중인 모델 및 데이터베이스에 대해 모든 권한이 필요하지만, 데이터베이스를 프로덕션 서버에 전달하고 나면 읽기 권한만 필요합니다. 개발, 테스트 및 프로덕션 배포를 포함하여 모든 시나리오에 대해 역할 정의 및 할당을 개발하세요.  
  
 이와 같은 방법을 사용하여 모델에서 역할 정의 및 역할 구성원 자격에 대한 변동을 최소화하고 큐브 권한을 더 쉽게 실행하고 관리하는 역할 할당을 파악합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [역할 및 권한&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Analysis Services에서 지 원하는 인증 방법](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  
