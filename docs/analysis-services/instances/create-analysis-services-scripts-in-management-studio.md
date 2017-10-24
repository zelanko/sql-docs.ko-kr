---
title: "Management Studio에서 Analysis Services 스크립트 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Analysis Services objects, scripts
- objects [Analysis Services], scripts
- scripts [Analysis Services], objects
ms.assetid: 4f1b965c-9ca6-427b-8f4d-0ce1eea7c0fe
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 24fffa56991e411dfae93321bbe238c1bbcb4db3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="create-analysis-services-scripts-in-management-studio"></a>Management Studio에서 Analysis Services 스크립트 만들기
  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에는 Analysis Services 개체 및 태스크를 스크립팅하는 데 사용할 수 있는 스크립트 생성 기능, 템플릿 및 편집기가 포함되어 있습니다.  
  
## <a name="script-analysis-services-tasks-in-management-studio"></a>Management Studio에서 Analysis Services 태스크 스크립팅  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 태스크 지향 대화 상자에서 스크립트 옵션 중 하나를 클릭하여 태스크를 스크립팅합니다. 데이터베이스 백업 또는 복원, 개체 처리, 집계 디자인과 같은 태스크를 수행하는 데 사용하는 모든 대화 상자에는 맨 위에 스크립트 옵션이 포함되어 있습니다. 이러한 옵션 중 하나를 선택하면 대화 상자의 정보 및 설정을 기반으로 XMLA 스크립트가 생성됩니다.  
  
 기본적으로 스크립트는 생성된 후 XMLA 쿼리 편집기에 배치되지만 스크립트 옵션 목록을 확장하여 스크립트를 Windows 클립보드 또는 파일로 보낼 수도 있습니다.  
  
#### <a name="to-script-an-analysis-services-task"></a>Analysis Services 태스크를 스크립팅하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결합니다.  
  
2.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **백업**을 클릭합니다. 데이터베이스 백업 대화 상자가 열립니다. 백업 파일 이름을 지정하고 이 백업에 사용할 옵션을 선택합니다.  
  
3.  대화 상자 맨 위에서 **스크립트** 를 클릭합니다. 스크립트 기능은 Management Studio에 있는 모든 태스크 기반 대화 상자의 일부입니다. 쿼리 편집기 창을 여는 **새 쿼리 창 동작 스크립팅** , XMLA 스크립트를 파일로 저장하는 **파일 동작 스크립팅** 또는 XMLA 스크립트를 클립보드로 저장하는 **클립보드 동작 스크립팅** 과 같은 옵션이 있습니다.  
  
     Management Studio에서 스크립트 옵션으로 표시되는 **작업 동작 스크립팅** 옵션은 Analysis Services 스크립트에 대해서는 지원되지 않습니다.  
  
4.  기본 옵션인 **새 쿼리 창 동작 스크립팅**을 선택하면 생성된 스크립트가 XMLA 쿼리 창에 배치됩니다.  
  
     이제 데이터베이스 백업 대화 상자를 닫고 XMLA 스크립트를 직접 편집하거나 실행할 수 있습니다.  
  
## <a name="script-analysis-services-objects-in-management-studio"></a>Management Studio에서 Analysis Services 개체 스크립팅  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 마우스 오른쪽 단추로 클릭하고 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] CREATE **,**ALTER **또는**DELETE **를 선택하여**의 개체를 스크립팅합니다. 이러한 각 옵션을 창이나 파일로 전송할 수 있지만 스크립트는 전송되는 위치에 관계없이 XMLA 래퍼의 DDL 스크립트 형태를 갖습니다. 이러한 스크립트의 가장 큰 장점은 모든 대상 서버에서 스크립트를 실행할 수 있다는 것입니다. 또한 스크립트에서 이름을 변경할 수 있고 반복적으로 실행하여 개체를 대량으로 생성, 변경 또는 삭제할 수 있습니다.  
  
 스크립팅할 수 있는 개체에는 데이터 원본, 데이터 원본 뷰, 큐브, 차원, 마이닝 구조 및 역할 등의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 요소가 포함됩니다.  
  
 사전에 XMLA(XML for Analysis)를 이해하고 있어야 합니다. 다행히 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에는 큐브 등의 개체를 만드는 데 필요한 XMLA 스크립트를 자동으로 만드는 기능이 있습니다. 이 자동화 기능을 이용하면 XMLA를 배우는 데 드는 시간과 노력을 줄일 수 있습니다. XMLA를 사용하는 방법에 대한 자세한 내용은 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)을 참조하세요. XMLA를 사용하는 방법에 대한 자세한 내용은 [Analysis Services에서 XMLA를 사용하여 개발](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  역할 개체를 스크립팅할 때 보안 권한은 연관된 보안 역할이 아니라 해당 권한이 보안을 설정하는 개체에 포함되어 있다는 사실에 유의해야 합니다.  
  
#### <a name="to-script-analysis-services-objects"></a>Analysis Services 개체를 스크립팅하려면  
  
1.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]인스턴스에 연결합니다.  
  
2.  개체 작성, 변경 또는 삭제 스크립트를 만들 개체를 찾습니다.  
  
3.  개체를 마우스 오른쪽 단추로 클릭하고 **큐브 스크립팅**, **CREATE**, **ALTER**또는 **DELETE**를 차례로 가리킨 후 다음 옵션 중 하나를 클릭합니다. 쿼리 편집기 창을 열려면 **새 쿼리 편집기 창** , XMLA 스크립트를 파일에 저장하려면 **파일** , XMLA 스크립트를 클립보드에 저장하려면 **클립보드** 를 클릭합니다.  
  
    > [!NOTE]  
    >  일반적으로 버전이 다른 파일을 여러 개 만들려면 **파일** 을 선택합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [XMLA 쿼리 편집기 &#40; Analysis Services-다차원 데이터 &#41;](http://msdn.microsoft.com/library/14623019-7839-4038-9d12-2f8953d2ec04)  
  
  

