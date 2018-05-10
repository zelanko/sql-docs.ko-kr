---
title: Analysis Services 인스턴스에 서버 관리 권한 부여 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ''
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 080e12b4c6c4939ff97cef4a521ef6c073b3c632
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="grant-server-admin-rights-to-an--analysis-services-instance"></a>Analysis Services 인스턴스에 서버 관리 권한 부여
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스 내에서 서버 관리자 역할의 멤버는 해당 인스턴스의 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체와 데이터에 무제한으로 액세스할 수 있습니다. 데이터베이스 작성 또는 처리, 서버 속성 수정, 추적 시작(이벤트 처리용 제외) 등의 서버 차원의 태스크를 수행하려면 사용자가 서버 관리자 역할의 멤버여야 합니다.  
  
 역할 멤버 자격은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 이 설치될 때 설정됩니다. 설치 프로그램을 실행하는 사용자는 본인을 역할에 추가하거나 다른 사용자를 추가할 수 있습니다. 관리자를 한 명 이상 지정해야 설치를 계속할 수 있습니다.  
  
 기본적으로 로컬 관리자 그룹의 멤버는 Analysis Server에서 관리 권한도 부여 받습니다. 로컬 그룹은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 관리자 역할의 멤버 자격을 명시적으로 부여 받지는 않지만 로컬 관리자는 데이터베이스를 만들고 사용자 및 사용 권한을 추가하고 시스템 관리자에게 허용된 기타 모든 작업을 수행할 수 있습니다. 관리자 권한의 암시적 부여는 구성이 가능하고, **BuiltinAdminsAreServerAdmins** 서버 속성에 의해 결정되며 기본적으로 **true** 로 설정되어 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 이 속성을 변경할 수 있습니다. 자세한 내용은 [Security Properties](../../analysis-services/server-properties/security-properties.md)을 참조하세요.  
  
 설치 후에는 역할 멤버 자격을 수정하여 서비스에 대한 모든 권한이 필요한 사용자를 더 추가할 수 있습니다. AMO(Analysis Management Objects)를 사용하여 서버 역할을 관리할 수도 있습니다. 자세한 내용은 [AMO&#40;Analysis Management Objects&#41;를 사용하여 개발](../../analysis-services/multidimensional-models/analysis-management-objects/developing-with-analysis-management-objects-amo.md)을 참조하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 상세 역할로 점차적으로 이동 하는 처리 및 서버, 데이터베이스 및 개체 수준에서 쿼리를 제공 합니다. 이러한 역할을 사용하는 방법에 대한 자세한 내용은 [역할 및 권한&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)을 참조하세요.  
  
## <a name="modify-server-role-membership"></a>서버 역할 멤버 자격 수정  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 인스턴스 이름을 마우스 오른쪽 단추로 클릭한 후 **속성**을 클릭합니다.  
  
2.  **페이지 선택** 창에서 **보안** 을 클릭하고 페이지 맨 아래쪽에서 **추가** 를 클릭하여 서버 역할에 Windows 사용자나 그룹을 하나 이상 추가합니다.  
  
     ![Management studio에서 추가 사용자가 대화 상자](../../analysis-services/instances/media/ssas-serveradminadd.png "management studio에서 추가 사용자가 대화 상자")  
  
### <a name="add-computer-accounts"></a>컴퓨터 계정 추가  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 컴퓨터 계정을 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자 그룹의 멤버로 지정할 수도 있습니다.  
  
1.  **사용자 또는 그룹 선택** 대화 상자에서 **위치**를 클릭합니다.  
  
2.  추가하려는 컴퓨터가 멤버로 속해 있는 도메인을 선택하거나 **전체 디렉터리** 를 선택하고 **확인**을 클릭합니다.  
  
3.  **개체 유형**을 클릭합니다.  
  
4.  **컴퓨터** 를 선택하고 **확인**을 클릭합니다.  
  
     ![ssas 관리자로 컴퓨터 계정 추가](../../analysis-services/instances/media/ssas-in-ssms-computerobjects.png "ssas 관리자로 컴퓨터 계정 추가")  
  
5.  **선택할 개체 이름을 입력하세요.** 텍스트 상자에 컴퓨터의 이름을 입력하고 **이름 확인** 을 클릭하여 컴퓨터 계정을 현재 위치에서 찾을 수 있는지 확인합니다. 컴퓨터 계정을 찾을 수 없으면 컴퓨터 이름과 컴퓨터가 멤버로 속한 현재 도메인을 확인합니다.  
  
## <a name="nt-servicessastelemetry-account"></a>NT Service\SSASTelemetry 계정  
 설치 중에 생성되는 권한이 낮은 컴퓨터 계정인**NT Service/SSASTelemetry** 는 CEIP(사용자 환경 개선 프로그램) 서비스의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 구현 실행 전용으로 사용됩니다. 이 서비스에는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 관리 권한(다양한 검색 명령 실행용)이 필요합니다. 자세한 내용은 [Customer Experience Improvement Program for SQL Server Data Tools](../../sql-server/customer-experience-improvement-program-for-sql-server-data-tools.md) 및 [Microsoft SQL Server Privacy Statement](http://msdn.microsoft.com/library/57769f4a-5689-49a1-8298-e3c0db5106f8) 를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [개체 및 작업에 대한 액세스 승인&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [보안 역할&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
  
