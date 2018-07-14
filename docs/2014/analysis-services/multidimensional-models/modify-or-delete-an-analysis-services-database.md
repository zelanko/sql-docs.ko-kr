---
title: Analysis Services 데이터베이스 수정 또는 삭제 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- databases [Analysis Services], modifying
- removing databases
- deleting databases
- dropping databases
- databases [Analysis Services], deleting
- modifying databases
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 949767979720880225431bb2e0c928623822ee23
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37206293"
---
# <a name="modify-or-delete-an-analysis-services-database"></a>Analysis Services 데이터베이스 수정 또는 삭제
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에 배포하기 전에 그리고 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에 배포한 후에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]데이터베이스의 이름과 설명을 변경할 수 있습니다. 또한 환경에 따라 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 추가 설정을 조정할 수 있습니다.  
  
> [!NOTE]  
>  온라인 모드에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 데이터베이스 속성을 변경할 수는 없습니다.  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>SQL Server Management Studio를 사용하여 데이터베이스 수정  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 배포한 후에는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 데이터베이스에 포함된 데이터 원본에 연결할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용하는 가장 모드를 변경할 수 있습니다. 가장 모드를 사용하면 처리, 검색 또는 드릴스루를 위해 데이터 원본에 연결을 시도할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 사용하는 보안 컨텍스트를 지정할 수 있습니다.  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>SQL Server Data Tools를 사용하여 데이터베이스 수정  
 프로젝트 모드에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 사용하여 데이터베이스 정의에 사용되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 캡션 및 설명에 대한 번역을 수정할 수 있습니다. 번역 사용 방법은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 참조 하십시오 [Analysis Services 다차원에 대 한 전역화 시나리오](../globalization-scenarios-for-analysis-services-multiidimensional.md)합니다.  
  
 또한 데이터베이스에 포함된 차원의 계정 특성에서 사용하는 계정 유형과 연결된 별칭 및 집계 함수를 설정할 수 있습니다. 별칭을 사용하면 계정 차트의 계정 유형에 대해 조직에서 사용하는 비즈니스 관련 용어를 선택할 수 있습니다. 계정 유형은 데이터베이스에 포함된 각 계정 유형에 대해 지정된 집계 함수를 사용하여 각 멤버에 대해 측정값을 집계하는 방법을 나타내기 위해 계정 특성의 멤버에서 사용합니다. 계정 특성에 대한 자세한 내용은 [특성 및 특성 계층](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)을 참조하세요.  
  
## <a name="deleting-databases"></a>데이터베이스 삭제  
 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스를 삭제하면 데이터베이스 및 해당 데이터베이스에 있는 모든 큐브, 차원 및 마이닝 모델도 삭제됩니다. 기존 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서만 삭제할 수 있습니다.  
  
#### <a name="to-delete-an-analysis-services-database"></a>Analysis Services 데이터베이스를 삭제하려면  
  
1.  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 연결합니다.  
  
2.  **개체 탐색기**에서 연결된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 노드를 확장한 다음 삭제할 개체가 표시되어 있는지 확인합니다.  
  
3.  삭제할 개체를 마우스 오른쪽 단추로 클릭한 다음 **삭제**를 선택합니다.  
  
4.  **개체 삭제** 대화 상자에서 **확인**을 클릭합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 데이터베이스 문서화 및 스크립트](document-and-script-an-analysis-services-database.md)  
  
  
