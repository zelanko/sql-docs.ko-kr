---
title: 작업 영역 데이터베이스 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 662daf08-a514-44a7-8675-44644aa454a2
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5a52eb01f176eddd8e69dcdc14609c3776bd54a1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090737"
---
# <a name="workspace-database-ssas-tabular"></a>작업 영역 데이터베이스(SSAS 테이블 형식)
  모델을 제작하는 동안 사용되는 테이블 형식 모델 작업 영역 데이터베이스는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 새 테이블 형식 모델 프로젝트를 만들 때 만들어집니다. 작업 영역 데이터베이스는 일반적으로 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]와 동일한 컴퓨터에서 테이블 형식 모드로 실행하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에서 메모리 내에 상주합니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
-   [작업 영역 데이터베이스 개요](#bkmk_overview)  
  
-   [작업 영역 데이터베이스 속성](#bkmk_ws_prop)  
  
-   [SSMS를 사용 하 여 작업 영역 데이터베이스를 관리 하려면](#bkmk_use_ssms)  
  
-   [관련 작업](#bkmk_related_tasks)  
  
##  <a name="bkmk_overview"></a> 작업 영역 데이터베이스 개요  
 작업 영역 데이터베이스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 테이블 형식 모델 프로젝트 템플릿 중 하나를 사용하여 새 비즈니스 인텔리전스 프로젝트를 만들 때 작업 영역 서버 속성에서 지정한 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]인스턴스에 만들어집니다. 각 테이블 형식 모델 프로젝트에는 고유의 작업 영역 데이터베이스가 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 작업 영역 데이터베이스를 볼 수 있습니다. 작업 영역 데이터베이스 이름에는 프로젝트 이름이 포함되고 뒤에 밑줄, 사용자 이름, 밑줄, GUID가 차례로 옵니다.  
  
 작업 영역 데이터베이스는 테이블 형식 모델 프로젝트가 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에 열려 있는 동안 메모리 내에 상주합니다. 프로젝트를 닫으면 작업 영역 데이터베이스는 작업 영역 보존 속성을 통해 정의된 옵션에 따라 메모리 내에 유지되거나, 디스크에 저장되고 메모리에서 제거되거나(기본값), 메모리에서 제거되고 디스크에 저장되지 않습니다. 작업 영역 보존 속성에 대한 자세한 내용은 이 항목 뒷부분에 있는 [작업 영역 데이터베이스 속성](#bkmk_ws_prop) 을 참조하십시오.  
  
 테이블 가져오기 마법사를 사용하거나 복사/붙여넣기를 사용하여 데이터를 모델 프로젝트에 추가한 후 모델 디자이너에서 테이블, 열 및 데이터를 보면 작업 영역 데이터베이스가 보입니다. 추가 테이블, 열, 관계 등을 추가하는 경우 작업 영역 데이터베이스를 변경하는 것입니다.  
  
> [!IMPORTANT]  
>  모델에 많은 행이 포함된 테이블이 있는 경우에는 모델 제작 중에 데이터의 하위 집합만 가져오는 것이 좋습니다. 데이터의 하위 집합을 가져오면 처리 시간 및 작업 영역 데이터베이스 서버 리소스 사용량을 줄일 수 있습니다.  
  
> [!NOTE]  
>  테이블 가져오기 마법사의 테이블 및 뷰 선택 페이지에 있는 미리 보기 창, 테이블 속성 편집 대화 상자, 파티션 관리자 대화 상자에는 데이터 원본에 테이블, 열 및 행이 표시되며 작업 영역 데이터베이스와 동일한 테이블, 열 및 행이 표시되지 않을 수 있습니다.  
  
 테이블 형식 모델 프로젝트를 배포하면 본질적으로 작업 영역 데이터베이스의 복사본인 배포된 model 데이터베이스는 배포 서버 속성에서 지정한 Analysis Services 서버 인스턴스에서 만들어집니다. 배포 서버 속성에 대한 자세한 내용은 [프로젝트 속성&#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)을 참조하세요.  
  
 모델 작업 영역 데이터베이스는 일반적으로 localhost 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버의 명명된 로컬 인스턴스에 상주합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 원격 인스턴스를 사용하여 작업 영역 데이터베이스를 호스팅할 수 있지만, 데이터 쿼리 중 대기 시간 및 기타 제한 사항 때문에 이 구성은 권장되지 않습니다. 최적의 경우 작업 영역 데이터베이스를 호스팅할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]와 동일한 컴퓨터에 있습니다. 작업 영역 데이터베이스를 호스팅하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 동일한 컴퓨터에서 모델 프로젝트를 제작하면 성능을 향상할 수 있습니다.  
  
 원격 작업 영역 데이터베이스에는 다음과 같은 제한 사항이 있습니다.  
  
-   쿼리 중 잠재적인 대기 시간입니다.  
  
-   데이터 백업 속성을 **디스크에 백업**으로 설정할 수 없습니다.  
  
-   PowerPivot에서 가져오기 프로젝트 템플릿을 사용하여 새로운 테이블 형식 모델 프로젝트를 만들 때 PowerPivot 통합 문서에서 데이터를 가져올 수 없습니다.  
  
##  <a name="bkmk_ws_prop"></a> 작업 영역 데이터베이스 속성  
 작업 영역 데이터베이스 속성은 모델 속성에 포함됩니다. 모델 속성을 보려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **솔루션 탐색기**에서 **Model.bim** 파일을 클릭합니다. **속성** 창을 사용하여 모델 속성을 구성할 수 있습니다. 작업 영역 데이터베이스에 특정한 속성은 다음과 같습니다.  
  
> [!NOTE]  
>  **작업 영역 서버**, **작업 영역 보존**및 **데이터 백업** 속성은 새 모델 프로젝트를 만들 때 적용되는 기본 설정을 가지고 있습니다. 도구\옵션 대화 상자의 **Analysis Server** 설정에서 **데이터 모델링** 페이지를 사용하여 새 모델 프로젝트의 기본 설정을 변경할 수 있습니다. **속성** 창에서 각 모델 프로젝트에 대해 이러한 속성 및 기타 속성을 설정할 수도 있습니다. 이미 만들어진 모델 프로젝트에는 기본 설정 변경이 적용되지 않습니다. 자세한 내용은 [기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)을 참조하세요.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**작업 영역 데이터베이스**|프로젝트 이름, 밑줄, 사용자 이름, 밑줄, GUID가 차례로 포함됩니다.|메모리 내 모델 프로젝트를 저장하고 편집하는 데 사용되는 작업 영역 데이터베이스의 이름입니다. 테이블 형식 모델 프로젝트가 만들어진 후 이 데이터베이스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 작업 영역 서버 **속성에서 지정한** 인스턴스에 나타납니다. 이 속성은 속성 창에서 설정할 수 없습니다.|  
|**작업 영역 보존**|메모리에서 언로드|모델 프로젝트를 닫은 후 작업 영역 데이터베이스가 보존되는 방법을 지정합니다. 작업 영역 데이터베이스에는 모델 메타데이터와 가져온 데이터가 포함됩니다. 경우에 따라 작업 영역 데이터베이스가 매우 크고 많은 양의 메모리를 사용할 수 있습니다. 기본적으로 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 닫을 때 작업 영역 데이터베이스는 메모리에서 언로드됩니다. 이 설정을 변경할 때는 모델 프로젝트에서 작업할 빈도뿐만 아니라 사용 가능한 메모리 리소스를 고려해야 합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **메모리에 유지** - 모델 프로젝트를 닫은 후 메모리에 작업 영역 데이터베이스를 유지하도록 지정합니다. 이 옵션을 사용하면 메모리 소비량이 많아지지만 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 열 때 리소스가 더 적게 사용되며 작업 영역 데이터베이스가 더 빠르게 로드됩니다.<br /><br /> **메모리에서 언로드** - 모델 프로젝트를 닫은 후 디스크에는 작업 영역 데이터베이스를 유지하지만 메모리에는 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리가 더 적게 소비되지만, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 열 때 작업 영역 데이터베이스를 다시 연결해야 하고 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리에 유지되는 경우보다 느리게 모델 프로젝트가 로드됩니다. 메모리 내 리소스가 제한되어 있거나 원격 작업 영역 데이터베이스에서 작업하는 경우 이 옵션을 사용하세요.<br /><br /> **작업 영역 삭제** - 모델 프로젝트를 닫은 후 메모리에서 작업 영역 데이터베이스를 삭제하고 디스크에 작업 영역 데이터베이스를 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리 및 저장소 공간 소비량이 줄어들지만 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 열 때 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리나 디스크에 유지되는 경우보다 느리게 모델 프로젝트가 로드됩니다. 가끔씩만 모델 프로젝트에서 작업하는 경우 이 옵션을 사용하십시오.<br /><br /> <br /><br /> 도구\옵션 대화 상자의 **Analysis Server** 설정에서 **데이터 모델링** 페이지를 사용하여 이 속성의 기본 설정을 변경할 수 있습니다.|  
|**Workspace Server**|localhost|이 속성은 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 제작하는 동안 작업 영역 데이터베이스를 호스팅하는 데 사용할 기본 서버를 지정합니다. 로컬 컴퓨터에서 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 모든 사용 가능한 인스턴스가 목록 상자에 포함됩니다.<br /><br /> 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버(테이블 형식 모드에서 실행)를 지정하려면 서버 이름을 입력합니다. 로그온한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 관리자여야 합니다.<br /><br /> 것이 좋습니다 로컬 지정 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버 작업 영역 서버로 합니다. 원격 서버에 있는 작업 영역 데이터베이스의 경우 PowerPivot에서 가져오기가 지원되지 않고 데이터를 로컬로 백업할 수 없으며 쿼리 중에 사용자 인터페이스에서 대기 시간이 발생할 수 있습니다.<br /><br /> 또한이 속성에 대 한 기본 설정에서 데이터 모델링 페이지에서 변경할 수 있습니다에 유의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 도구 \ 옵션 대화 상자에서 설정 합니다.|  
  
##  <a name="bkmk_use_ssms"></a> SSMS를 사용하여 작업 영역 데이터베이스 관리  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)](SSMS)를 사용하여 작업 영역 데이터베이스를 호스팅하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 연결할 수 있습니다. 일반적으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 수행해야 하는 작업 영역 데이터베이스 분리 또는 삭제 작업을 제외하면 작업 영역 데이터베이스의 관리는 필요하지 않습니다.  
  
> [!WARNING]  
>  모델 디자이너에 프로젝트가 열려 있는 동안 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 작업 영역 데이터베이스를 관리하지 마십시오. 이렇게 하면 데이터가 손실될 수 있습니다.  
  
##  <a name="bkmk_related_tasks"></a> 관련 태스크  
  
|항목|Description|  
|-----------|-----------------|  
|[모델 속성 &#40;SSAS 테이블 형식&#41;](model-properties-ssas-tabular.md)|모델의 작업 영역 데이터베이스 속성에 대한 설명 및 구성 단계를 제공합니다.|  
  
## <a name="see-also"></a>관련 항목  
 [기본 데이터 모델링 및 배포 속성 구성 &#40;SSAS 테이블 형식&#41;](configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [프로젝트 속성 &#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)  
  
  