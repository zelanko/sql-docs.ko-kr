---
title: 연결 된 측정값 그룹 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- linked measure groups [Analysis Services]
- referencing measure groups
- Linked Measure Group Wizard
- measure groups [Analysis Services], linked
- linked dimensions [Analysis Services]
ms.assetid: 7f838452-8669-4194-8e15-7afdc7f15251
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7695f971504744d42056d0067217e102ef3d990
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53368461"
---
# <a name="linked-measure-groups"></a>연결된 측정값 그룹
  연결된 측정값 그룹은 동일한 데이터베이스 또는 다른 Analysis Services 데이터베이스 내에 있는 다른 큐브의 또 다른 측정값 그룹을 기반으로 합니다. 측정값 집합을 다시 사용하려는 경우 여러 큐브에서 연결된 측정값 그룹과 해당 데이터 값을 사용할 수 있습니다.  
  
 원본 측정값 그룹과 연결된 측정값 그룹은 동일한 서버에서 실행되는 솔루션에 상주하는 것이 좋습니다. 향후 릴리스에서 사용 중단 예정 된 원격 서버의 측정값 그룹에 연결 (참조 [SQL Server 2014에서 Analysis Services 기능의 사용 되지 않는](../deprecated-analysis-services-features-in-sql-server-2014.md)).  
  
> [!IMPORTANT]  
>  연결된 측정값 그룹은 읽기 전용입니다. 최근 변경 사항을 선택하려면 모든 연결된 측정값을 삭제하고 수정된 원본 개체를 기반으로 다시 만들어야 합니다. 따라서 이후에 측정값 그룹 수정이 필요할 경우에는 프로젝트 사이에 측정값 그룹을 복사하고 붙여넣는 방식을 고려해야 할 수 있습니다.  
  
## <a name="usage-limitations"></a>사용 제한 사항  
 앞에서 설명한 대로 연결된 측정값을 사용하는 데 있어서 중요한 제한 사항은 연결된 측정값을 직접 사용자 지정할 수 없다는 점입니다. 데이터 형식, 형식, 데이터 바인딩 및 표시 유형뿐만 아니라 측정값 그룹 자체에 있는 항목의 멤버 자격에 대한 수정 사항은 모두 원래 측정값 그룹에서 변경해야 합니다.  
  
 작업 측면에서 연결된 측정값 그룹은 클라이언트 애플리케이션에서 액세스하면 다른 측정값 그룹과 동일하므로 다른 측정값 그룹과 동일한 방식으로 쿼리됩니다.  
  
 연결된 측정값 그룹을 포함하는 큐브를 쿼리하는 경우 대상 큐브에 대한 첫 번째 계산 패스 동안 연결이 설정되고 확인됩니다. 이러한 동작으로 인해 쿼리가 평가되기 전에는 연결된 측정값 그룹에 저장되는 어떠한 계산도 확인할 수 없습니다. 즉, 계산 측정값과 계산 셀은 원본 큐브에서 상속받지 말고 대상 큐브에서 다시 만들어야 합니다.  
  
 사용 제한 사항은 다음과 같습니다.  
  
-   연결된 다른 측정값 그룹에서는 연결된 측정값 그룹을 만들 수 없습니다.  
  
-   연결된 측정값 그룹에서 측정값을 추가하거나 제거할 수 없습니다. 멤버 자격은 원래 측정값 그룹에서만 정의됩니다.  
  
-   연결된 측정값 그룹에서는 쓰기 저장(writeback)이 지원되지 않습니다.  
  
-   연결된 측정값 그룹은 여러 다 대 다 관계에서 사용할 수 없으며 특히 해당 관계가 서로 다른 큐브에 있는 경우에 사용할 수 없습니다. 사용하면 모호한 집계가 발생할 수 있습니다. 자세한 내용은 [다 대 다 관계가 포함된 큐브의 연결된 측정값에 대한 잘못된 집계](https://social.technet.microsoft.com/wiki/contents/articles/22911.incorrect-amounts-for-linked-measures-in-cubes-containing-many-to-many-relationships-ssas-troubleshooting.aspx)를 참조하세요.  
  
 연결된 측정값 그룹에 포함된 측정값은 동일한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에서 검색한 연결된 차원과만 직접 구성이 가능합니다. 그러나 계산 멤버를 사용하면 연결된 측정값 그룹의 정보를 큐브 내의 연결되지 않은 다른 차원과 연결할 수 있습니다. 또한 참조 또는 다 대 다 관계 등의 간접 관계를 사용하여 연결되지 않은 차원을 연결된 측정값 그룹에 연결할 수 있습니다.  
  
## <a name="create-or-modify-a-linked-measure"></a>연결된 측정값 만들기 또는 수정  
 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 를 사용하여 연결된 측정값 그룹을 만들 수 있습니다.  
  
1.  이제 원본 큐브에서 원래 측정값 그룹에 대한 수정을 모두 완료합니다. 이에 따라 나중에 이후 큐브에서 연결된 측정값 그룹을 다시 만들 필요가 없습니다. 연결된 개체의 이름을 바꿀 수 있지만 다른 속성을 변경할 수는 없습니다.  
  
2.  솔루션 탐색기에서 연결된 측정값 그룹을 추가할 큐브를 두 번 클릭합니다. 이 단계에서는 큐브 디자이너에서 큐브를 엽니다.  
  
3.  큐브 디자이너에서 측정값 창이나 차원 창을 마우스 오른쪽 단추로 클릭한 다음 **새 연결된 개체**를 선택합니다. 연결된 개체 마법사가 시작됩니다.  
  
4.  첫 번째 페이지에서 데이터 원본을 지정합니다. 이 단계에서는 원본 측정값 그룹의 위치를 설정합니다. 기본값은 현재 데이터베이스의 현재 큐브이지만 다른 Analysis Services 데이터베이스를 선택할 수도 있습니다.  
  
5.  다음 페이지에서 연결할 측정값 그룹 또는 차원을 선택합니다. 측정값 그룹 등의 큐브 개체 및 차원이 별도로 나열됩니다. 현재 큐브에 없는 개체만 사용할 수 있습니다.  
  
6.  **마침** 을 클릭하여 연결된 개체를 만듭니다. 연결된 개체가 측정값 및 차원 창에서 링크 아이콘으로 표시되어 나타납니다.  
  
## <a name="secure-a-linked-measure"></a>연결된 측정값 보안  
 연결이 정의된 다음에는 연결된 측정값 그룹의 측정값에 대한 액세스가 다른 측정값 그룹에 대한 액세스와 동일한 방법으로 관리됩니다. 연결된 개체가 역할 디자이너에서 연결되지 않은 해당 항목과 함께 나타납니다. 측정값 그룹의 보안 관리에 대한 자세한 내용은 [큐브 또는 모델 권한 부여&#40;Analysis Services&#41;](grant-cube-or-model-permissions-analysis-services.md)를 참조하세요.  
  
 연결된 측정값 그룹을 정의하거나 사용하려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 Windows 서비스 계정이 원본 큐브 및 측정값 그룹에 대해 원본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 `ReadDefinition` 및 `Read` 액세스 권한이 있는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 역할에 속하거나 원본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 대한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리자 역할에 속해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [연결된 차원 정의](define-linked-dimensions.md)  
  
  
