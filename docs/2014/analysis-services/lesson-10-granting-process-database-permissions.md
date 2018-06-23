---
title: 데이터베이스 처리 권한 부여 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 69ba952e-09ae-49a9-9297-00e32e8e89a8
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: c309ca3781bea3594c6d7e8d1b912730371635e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36185096"
---
# <a name="granting-process-database-permissions"></a>데이터베이스 처리 권한 부여
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 설치하면 해당 인스턴스에 있는 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 서버 관리자 역할의 모든 멤버가 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스 내에서 모든 태스크를 수행할 수 있는 서버 차원의 사용 권한을 갖습니다. 기본적으로 어떠한 사용자에게도 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]인스턴스의 개체를 관리하거나 볼 수 있는 권한이 없습니다.  
  
 서버 관리자 역할의 멤버는 사용자를 역할 멤버로 만들어 사용자에게 서버 차원에서 관리자 액세스 권한을 부여할 수 있습니다. 서버 관리자 역할의 멤버는 데이터베이스 수준에서 사용자에게 제한되거나 완전한 관리 또는 액세스 권한을 부여하여 더욱 제한적인 방식으로 액세스 권한을 부여할 수도 있습니다. 제한된 관리자 권한에는 데이터베이스, 큐브 또는 차원 수준의 정의 처리 또는 읽기 권한이 포함됩니다.  
  
 이 항목의 태스크에서는 역할의 멤버에게 모든 데이터베이스 개체를 처리할 권한은 부여하지만 데이터베이스 내 데이터를 볼 수 있는 권한은 부여하지 않는 데이터베이스 개체 처리 보안 역할을 정의합니다.  
  
## <a name="defining-a-process-database-objects-security-role"></a>데이터베이스 개체 처리 보안 역할 정의  
  
1.  솔루션 탐색기에서 **역할** 을 마우스 오른쪽 단추로 클릭한 다음 **새 역할** 을 클릭하여 역할 디자이너를 엽니다.  
  
2.  **데이터베이스 처리** 확인란을 클릭합니다.  
  
3.  속성 창에서 변경 된 **이름** 이 새 역할에 대해 속성 `Process Database Objects Role`합니다.  
  
     ![역할 디자이너](../../2014/tutorials/media/l10-security-1.png "역할 디자이너")  
  
4.  역할 디자이너의 **멤버 자격** 탭으로 전환하고 **추가**를 클릭합니다.  
  
5.  이 역할의 멤버가 될 Windows 도메인 사용자 또는 그룹의 계정을 입력합니다. **이름 확인** 을 클릭하여 계정 정보를 확인한 다음 **확인**을 클릭합니다.  
  
6.  역할 디자이너의 **큐브** 탭으로 전환합니다.  
  
     이 역할의 멤버에게는 이 데이터베이스를 처리할 권한이 있지만 다음 그림에 표시된 것처럼 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 큐브의 데이터에 액세스할 수 있는 권한과 로컬 큐브/드릴스루 액세스는 없습니다.  
  
     ![역할 디자이너의 큐브 탭](../../2014/tutorials/media/l10-security-2.png "역할 디자이너의 큐브 탭")  
  
7.  역할 디자이너의 **차원** 탭으로 전환합니다.  
  
     이 역할의 멤버에게는 이 데이터베이스의 모든 차원 개체를 처리할 수 있는 권한이 있으며 기본적으로 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Tutorial 데이터베이스의 각 차원 개체에 액세스하기 위한 읽기 권한이 있습니다.  
  
8.  **빌드** 메뉴에서 **Analysis Services Tutorial 배포**를 클릭합니다.  
  
     이제 데이터베이스 개체 처리 보안 역할을 성공적으로 정의하여 배포했습니다. 큐브가 프로덕션 환경으로 배포된 후에 배포된 큐브의 관리자는 필요에 따라 이 역할에 사용자를 추가하여 특정 사용자에게 처리 권한을 위임할 수 있습니다.  
  
> [!NOTE]  
>  10단원의 완료된 프로젝트는 예제를 다운로드 및 설치하여 사용할 수 있습니다. 자세한 내용은 [Analysis Services 다차원 모델링 자습서에 사용할 예제 데이터 및 프로젝트 설치](install-sample-data-and-projects.md)을(를) 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [역할 및 사용 권한 &#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  