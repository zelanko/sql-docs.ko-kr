---
title: "데이터 마이닝 구조 및 모델 (Analysis Services)에 대 한 권한 부여 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.roledesignerdialog.miningmodels.f1
helpviewer_keywords:
- data mining [Analysis Services], security
- permissions [Analysis Services], mining models
- mining models [Analysis Services], security
- mining structures [Analysis Services], security
- permissions [Analysis Services], mining structures
- user access rights [Analysis Services], mining structures
- user access rights [Analysis Services], mining models
ms.assetid: a0008004-e2b7-47db-acad-5fe7e12b130f
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 12b69f08e0c56b614c2e181ca3cb62a24496e2b9
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="grant-permissions-on-data-mining-structures-and-models-analysis-services"></a>데이터 마이닝 구조 및 모델에 대한 권한 부여(Analysis Services)
  기본적으로 Analysis Services 서버 관리자만 데이터베이스의 데이터 마이닝 구조 또는 마이닝 모델을 볼 수 있습니다. 관리자가 아닌 사용자에게 권한을 부여하려면 아래 지침을 따르세요.  
  
## <a name="set-permissions-to-access-a-mining-structure"></a>마이닝 구조에 대한 액세스 권한 설정  
  
1.  SSMS에서 Analysis Services에 연결합니다. 단계에서 도움이 필요한 경우 [클라이언트 응용 프로그램에서 연결&#40;Analysis Services&#41;](../../analysis-services/instances/connect-from-client-applications-analysis-services.md)을 참조하세요.  
  
2.  **데이터베이스** 폴더를 열고 개체 탐색기에서 데이터베이스를 선택합니다.  
  
3.  **역할** 을 마우스 오른쪽 단추로 클릭하고 **새 역할**을 선택합니다.  
  
4.  일반 페이지에서 이름 및 설명(옵션)을 입력합니다. 또한 이 페이지는 모든 권한, 데이터베이스 처리, 정의 읽기 등의 몇 가지 데이터베이스 권한을 포함합니다. 데이터 마이닝 액세스에는 이러한 권한이 필요하지 않습니다. 데이터베이스 권한에 대한 자세한 내용은 [데이터베이스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md)를 참조하세요.  
  
5.  **마이닝 구조** 창에서 각 데이터 마이닝 구조에 대해 **읽기** 또는 **읽기/쓰기**를 선택합니다.  
  
6.  **멤버 자격** 창에서 이 역할을 사용하여 Analysis Services에 연결하는 Windows 사용자 및 그룹 계정을 입력합니다.  
  
7.  **확인** 을 클릭하여 역할 만들기를 마칩니다.  
  
## <a name="set-permissions-to-access-a-mining-model"></a>마이닝 모델에 대한 액세스 권한 설정  
 데이터 마이닝 모델의 경우 특정 역할에 **읽기** 또는 **읽기/쓰기** 권한뿐 아니라 기본 데이터를 보고 검색할 수 있는 **드릴스루** 및 **정의 읽기** 권한도 부여할 수 있습니다.  
  
 **참고** 마이닝 구조와 마이닝 모델 모두에서 드릴스루할 수 있으면 마이닝 모델 및 마이닝 구조에 대해 드릴스루 권한을 가지는 역할의 멤버인 사용자는 마이닝 모델에 열이 포함되지 않은 경우에도 마이닝 구조의 열을 볼 수 있습니다. 따라서 중요한 정보를 보호하려면 개인 정보를 마스킹하도록 데이터 원본 뷰를 설정하고 필요한 경우에만 마이닝 구조에 드릴스루 액세스를 허용해야 합니다.  
  
 데이터베이스 역할에 읽기 또는 읽기/쓰기 권한을 부여하려면 사용자가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 역할의 멤버이거나 모든(관리자) 권한을 가진 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 역할의 멤버여야 합니다.  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결하고 개체 탐색기에서 해당 데이터베이스에 대한 **역할** 을 확장한 다음 데이터베이스 역할을 클릭하거나 새 데이터베이스 역할을 만듭니다.  
  
2.  **마이닝 구조** 창의 **마이닝 모델** 목록에서 마이닝 모델을 찾은 다음 해당 마이닝 모델에 대해 **읽기**, **읽기/쓰기**, **드릴스루**또는 **찾아보기** 를 선택합니다.  
  
3.  **멤버 자격** 창에서 이 역할을 사용하여 Analysis Services에 연결하는 Windows 사용자 및 그룹 계정을 입력합니다.  
  
4.  **확인** 을 클릭하여 역할 만들기를 마칩니다.  
  
 DMX(Data Mining Extensions) OPENQUERY 절을 사용하는 드릴스루 쿼리에서 데이터 원본을 사용하려면 데이터베이스 역할이 해당 데이터 원본 개체에 대해 읽기/쓰기 권한도 가져야 합니다. 자세한 내용은 [데이터 원본 개체에 대한 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-permissions-on-a-data-source-object-analysis-services.md) 및 [OPENQUERY&#40;DMX&#41;](../../dmx/source-data-query-openquery.md)를 참조하세요.  
  
> [!NOTE]  
>  기본적으로 OPENROWSET을 사용하여 DMX 쿼리를 제출하는 기능이 해제되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Analysis Services 인스턴스에 서버 관리 권한 부여](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [데이터 &#40; 차원에 대 한 사용자 지정 액세스 부여 Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [셀 데이터에 대한 사용자 지정 액세스 권한 부여&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
