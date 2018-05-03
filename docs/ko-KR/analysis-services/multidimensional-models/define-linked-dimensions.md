---
title: 연결 된 차원 정의 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f779e994f38565f7c793c9b2a419d2c80b307f8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="define-linked-dimensions"></a>연결된 차원 정의
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  연결된 차원은 동일한 버전 및 호환성 수준의 다른 Analysis Services 데이터베이스에서 만들어지고 저장된 차원을 기반으로 합니다. 연결된 차원을 통해 하나의 데이터베이스에 차원을 만들고 저장하고 유지 관리할 수 있으며 이와 동시에 여러 데이터베이스의 사용자가 이 차원을 사용하도록 할 수 있습니다. 연결된 차원은 사용자에게 다른 차원과 동일하게 나타납니다.  
  
 연결된 차원은 읽기 전용입니다. 차원을 수정하거나 새로운 관계를 만들려는 경우 원본 차원을 변경한 다음 연결된 차원 및 해당 관계를 삭제하고 다시 만들어야 합니다. 연결된 차원을 새로 고쳐서 원본 개체의 변경 내용을 적용할 수 없습니다.  
  
 관련된 모든 측정값 그룹 및 차원은 같은 원본 데이터베이스를 기반으로 해야 합니다. 로컬 측정값 그룹과 큐브를 추가할 연결된 차원 간에는 새로운 관계를 만들 수 없습니다. 연결된 차원과 측정값 그룹을 현재 큐브에 추가한 후에는 해당 관계를 원본 데이터베이스에서 유지 관리해야 합니다.  
  
> [!NOTE]  
>  새로 고침을 사용할 수 없기 때문에 대부분의 Analysis Services 개발자는 차원을 연결하는 대신 복사합니다. 동일한 솔루션 내에서 프로젝트 간에 차원을 복사할 수 있습니다. 자세한 내용은 [SSAS에서 연결된 차원의 새로 고침](http://sqlblog.com/blogs/marco_russo/archive/2006/09/12/refresh-of-a-linked-dimension-in-ssas.aspx)을 참조하십시오.  
  
## <a name="prerequisites"></a>필수 구성 요소  
 차원을 제공하는 원본 데이터베이스와 차원을 사용하는 현재 데이터베이스는 버전 및 호환성 수준이 같아야 합니다. 자세한 내용은 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)을 참조하십시오.  
  
 원본 데이터베이스가 배포되고 온라인 상태여야 합니다. 연결된 개체를 게시하거나 사용하는 서버가 작업을 허용하도록 구성되어야 합니다(아래 참조).  
  
 사용할 차원은 자체적으로 연결된 차원이 될 수 없습니다.  
  
## <a name="configure-server-to-allow-linked-objects"></a>연결된 개체를 허용하도록 서버 구성  
  
1.  SQL Server Management Studio에서 Analysis Services 서버에 연결합니다. 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **패싯**을 선택합니다.  
  
2.  **LinkedObjectsLinksFromOtherInstancesEnabled** 를 **True** 로 설정하여 서버에서 다른 인스턴스에서 실행 중인 데이터베이스에 있는 연결된 개체에 대한 요청을 실행할 수 있도록 합니다.  
  
3.  **LinkedObjectsLinksToOtherInstances** 를 **True** 로 설정하여 서버에서 다른 인스턴스에서 실행 중인 데이터베이스에 있는 연결된 개체에 대한 데이터를 요청할 수 있도록 합니다.  
  
## <a name="create-a-linked-dimension-in-sql-server-data-tools"></a>SQL Server Data Tools에서 연결된 차원 만들기  
  
1.  마법사를 시작합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **데이터베이스 또는 프로젝트의** 차원 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 폴더를 마우스 오른쪽 단추로 클릭한 다음 **새 연결된 차원**을 클릭합니다.  
  
2.  차원을 제공하는 Analysis Services 데이터베이스에 연결합니다. 연결된 개체 마법사의 **데이터 원본 선택** 페이지에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터 원본을 선택하거나 새로 만듭니다.  
  
3.  마법사의 **개체 선택** 페이지에서 원격 데이터베이스에 있는 연결할 차원을 선택합니다.  
  
4.  **마법사 완료** 페이지에서 연결된 개체를 미리 볼 수 있습니다. 이미 있는 것과 이름이 같은 차원을 연결하면 이름에 서수 번호(중복된 첫 번째 이름의 경우 '1'로 시작)가 추가됩니다. 마법사를 완료하면 **차원** 폴더에 차원이 추가됩니다.  
  
##  <a name="bkmk_CreateNew"></a> Analysis Services 데이터베이스에 대한 새 데이터 원본 연결 만들기  
 새 데이터 원본 마법사를 사용하여 차원을 제공하는 Analysis Services 데이터베이스에 대한 프로젝트 연결 정보를 추가할 수 있습니다. 연결된 개체 마법사의 데이터 원본 선택 페이지에서 **새 데이터 원본** 을 클릭하여 마법사를 시작할 수 있습니다.  
  
1.  데이터 원본 마법사 시작의 연결 정의 방법 선택 페이지에서 **새로 만들기**를 클릭합니다.  
  
2.  연결 관리자에서 공급자가 **Native OLE DB\Microsoft OLE DB Provider for Analysis Services 11.0**으로 설정되어 있는지 확인합니다.  
  
3.  서버 이름을 입력(명명된 인스턴스의 경우 *servername*\\*instancename* 사용)하거나 **localhost** 를 입력하여 같은 컴퓨터에서 실행 중인 Analysis Services 서버에 연결합니다.  
  
4.  연결을 위해 Windows 인증을 사용합니다.  
  
5.  **초기 카탈로그**에서 아래쪽 화살표를 클릭하여 이 서버의 데이터베이스를 선택합니다.  
  
6.  데이터 원본 마법사에서 **다음** 을 클릭하여 계속합니다.  
  
7.  가장 정보 페이지에서 **서비스 계정 사용**을 클릭합니다. **다음**을 클릭한 다음 마법사를 끝냅니다. 방금 정의한 연결이 연결된 개체 마법사에서 선택됩니다.  
  
## <a name="next-steps"></a>다음 단계  
 연결된 차원의 구조는 변경할 수 없으므로 차원 디자이너의 **차원 구조** 탭에서 볼 수 없습니다. 연결된 차원을 처리한 후에는 **브라우저** 탭에서 볼 수 있습니다. 이름을 변경하고 이름에 대한 번역을 만들 수도 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 데이터베이스의 호환성 수준&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [연결 된 측정값 그룹](../../analysis-services/multidimensional-models/linked-measure-groups.md)   
 [차원 관계](../../analysis-services/multidimensional-models-olap-logical-cube-objects/dimension-relationships.md)  
  
  
