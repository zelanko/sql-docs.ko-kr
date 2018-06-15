---
title: SQL Server Data Tools에서 작업 영역 데이터베이스 | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 817c3b821fef5fe1c8dcfb539e93b9bf275ee5d9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34045177"
---
# <a name="workspace-database"></a>작업 영역 데이터베이스 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  모델을 제작하는 동안 사용되는 테이블 형식 모델 작업 영역 데이터베이스는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 새 테이블 형식 모델 프로젝트를 만들 때 만들어집니다.
  
## <a name="specifying-a-workspace-instance"></a>작업 영역 인스턴스 지정  
  SSDT에서 새 테이블 형식 모델 프로젝트를 만들 때 프로젝트를 제작하는 동안 사용할 Analysis Services 인스턴스를 지정할 수 있습니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 2016년 9월 릴리스(14.0.60918.0)부터 새 테이블 형식 모델 프로젝트를 만들 때 작업 영역 인스턴스를 지정하기 위한 두 가지 모드가 도입됩니다. 

**통합 작업 영역** - SSDT의 자체 내부 Analysis Services 인스턴스를 활용합니다.

**작업 영역 서버** - 작업 영역 데이터베이스가 Analysis Services 인스턴스에 생성됩니다. 대부분의 경우 SSDT와 동일한 컴퓨터나 동일한 네트워크의 다른 컴퓨터에 생성됩니다.
  
### <a name="integrated-workspace"></a>통합 작업 영역
통합 작업 영역에서는 작업 데이터베이스가 SSDT 자체 암시적 Analysis Services 인스턴스를 사용하여 메모리에 만들어집니다. 통합 작업 영역 모드에서는 따로 SQL Server Analysis Services를 명시적으로 설치할 필요가 없으므로 SSDT에서 테이블 형식 프로젝트 제작할 때의 복잡성을 크게 줄입니다.

통합 작업 영역 모드를 사용하면 SSDT 테이블 형식에서 자체의 내부 SSAS 인스턴스를 백그라운드에서 동적으로 시작하고 데이터베이스를 로드합니다. 모델 디자이너에서 뷰 테이블, 열 및 데이터를 추가할 수 있습니다. 테이블, 열, 관계 등을 추가하는 경우 작업 영역 데이터베이스가 수정됩니다. 통합 작업 영역 모드에서는 SSDT 테이블 형식이 작업 영역 서버 및 데이터베이스에서 작동하는 방식은 변경하지 않습니다. SSDT 테이블 형식이 작업 영역 데이터베이스를 호스트하는 위치만 변경합니다.

SSDT에서 새 테이블 형식 모델 프로젝트를 만드는 경우 통합 작업 영역 모드를 선택할 수 있습니다.

![SSAS 통합 작업 영역 모드](../../analysis-services/tabular-models/media/ssas-integrated-workspace-mode.png)

model.bim의 작업 영역 데이터베이스 및 작업 영역 서버 속성을 사용하여 SSDT 테이블 형식이 데이터베이스를 호스트하는 내부 SSAS 인스턴스의 TCP 포트와 임시 데이터베이스의 이름을 검색할 수 있습니다. SSDT 테이블 형식에 로드된 데이터베이스가 있는 경우 SSMS를 사용하여 작업 영역 데이터베이스에 연결할 수 있습니다. 작업 영역 보존 설정은 모델 프로젝트를 닫은 후 SSDT 테이블 형식에서 디스크에는 작업 영역 데이터베이스를 유지하지만 메모리에는 유지하지 않도록 지정합니다. 이렇게 하면 모델을 메모리에 항상 유지하는 경우보다 메모리를 덜 사용하게 됩니다. 이러한 설정을 제어하려면 통합 작업 영역 모드 속성을 False로 설정하고 명시적 작업 영역 서버를 제공합니다. 모델로 가져오는 데이터가 SSDT 워크스테이션의 메모리 용량을 초과하는 경우에도 명시적 작업 영역 서버가 적합합니다.

> [!NOTE]  
>  통합된 작업 모드를 사용 하는 경우 로컬 Analysis Services 인스턴스에 SSDT는 Visual Studio의 32 비트 환경에서 실행 되는 동안 64 비트입니다. 특수 데이터 원본에 연결하는 경우 워크스테이션에 해당 데이터 공급자의 32비트 버전과 64비트 버전을 모두 설치해야 합니다. 64 비트 공급자가 64 비트 Analysis Services 인스턴스에 대 한 필요 되며 32 비트 버전의 SSDT에서는 테이블 가져오기 마법사에 대 한 필요 합니다.

###  <a name="bkmk_overview"></a> 작업 영역 서버  
 작업 영역 데이터베이스는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 테이블 형식 모델 프로젝트 템플릿 중 하나를 사용하여 새 비즈니스 인텔리전스 프로젝트를 만들 때 작업 영역 서버 속성에서 지정한 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]인스턴스에 만들어집니다. 각 테이블 형식 모델 프로젝트에는 고유의 작업 영역 데이터베이스가 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 작업 영역 데이터베이스를 볼 수 있습니다. 작업 영역 데이터베이스 이름에는 프로젝트 이름이 포함되고 뒤에 밑줄, 사용자 이름, 밑줄, GUID가 차례로 옵니다.  
  
 작업 영역 데이터베이스는 테이블 형식 모델 프로젝트가 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에 열려 있는 동안 메모리 내에 상주합니다. 프로젝트를 닫으면 작업 영역 데이터베이스는 작업 영역 보존 속성을 통해 정의된 옵션에 따라 메모리 내에 유지되거나, 디스크에 저장되고 메모리에서 제거되거나(기본값), 메모리에서 제거되고 디스크에 저장되지 않습니다. 작업 영역 보존 속성에 대한 자세한 내용은 이 항목 뒷부분에 있는 [작업 영역 데이터베이스 속성](#bkmk_ws_prop) 을 참조하십시오.  
  
 테이블 가져오기 마법사를 사용하거나 복사/붙여넣기를 사용하여 데이터를 모델 프로젝트에 추가한 후 모델 디자이너에서 테이블, 열 및 데이터를 보면 작업 영역 데이터베이스가 보입니다. 추가 테이블, 열, 관계 등을 추가하는 경우 작업 영역 데이터베이스를 변경하는 것입니다.  
  
 테이블 형식 모델 프로젝트를 배포하면 본질적으로 작업 영역 데이터베이스의 복사본인 배포된 model 데이터베이스는 배포 서버 속성에서 지정한 Analysis Services 서버 인스턴스에서 만들어집니다. 배포 서버 속성에 대 한 자세한 내용은 참조 [프로젝트 속성](../../analysis-services/tabular-models/project-properties-ssas-tabular.md)합니다.  
  
 모델 작업 영역 데이터베이스는 일반적으로 localhost 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버의 명명된 로컬 인스턴스에 상주합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 원격 인스턴스를 사용하여 작업 영역 데이터베이스를 호스팅할 수 있지만, 데이터 쿼리 중 대기 시간 및 기타 제한 사항 때문에 이 구성은 권장되지 않습니다. 최적의 경우 작업 영역 데이터베이스를 호스팅할 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 인스턴스는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]와 동일한 컴퓨터에 있습니다. 작업 영역 데이터베이스를 호스팅하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 동일한 컴퓨터에서 모델 프로젝트를 제작하면 성능을 향상할 수 있습니다.  
  
 원격 작업 영역 데이터베이스에는 다음과 같은 제한 사항이 있습니다.  
  
-   쿼리 중 잠재적인 대기 시간입니다.  
  
-   데이터 백업 속성을 **디스크에 백업**으로 설정할 수 없습니다.  
  
-   [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서 가져오기 프로젝트 템플릿을 사용하여 새로운 테이블 형식 모델 프로젝트를 만들 때 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 통합 문서에서 데이터를 가져올 수 없습니다.  
  
  > [!IMPORTANT]  
>  모델의 호환성 수준 및 작업 영역 서버는 일치해야 합니다.
  
> [!NOTE]  
>  모델에 많은 행이 포함된 테이블이 있는 경우에는 모델 제작 중에 데이터의 하위 집합만 가져오는 것이 좋습니다. 데이터의 하위 집합을 가져오면 처리 시간 및 작업 영역 데이터베이스 서버 리소스 사용량을 줄일 수 있습니다.  
  
> [!NOTE]  
>  테이블 가져오기 마법사의 테이블 및 뷰 선택 페이지에 있는 미리 보기 창, 테이블 속성 편집 대화 상자, 파티션 관리자 대화 상자에는 데이터 원본에 테이블, 열 및 행이 표시되며 작업 영역 데이터베이스와 동일한 테이블, 열 및 행이 표시되지 않을 수 있습니다.  
  
  
##  <a name="bkmk_ws_prop"></a> 작업 영역 데이터베이스 속성  
 작업 영역 데이터베이스 속성은 모델 속성에 포함됩니다. 모델 속성을 보려면 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 **솔루션 탐색기**에서 **Model.bim** 파일을 클릭합니다. **속성** 창을 사용하여 모델 속성을 구성할 수 있습니다. 작업 영역 데이터베이스에 특정한 속성은 다음과 같습니다.  
  
> [!NOTE]  
>  **통합 작업 영역 모드**, **작업 영역 서버**, **작업 영역 보존** 및 **데이터 백업** 속성에는 새 모델 프로젝트를 만들 때 적용되는 기본 설정이 있습니다. 도구\옵션 대화 상자의 **Analysis Server** 설정에서 **데이터 모델링** 페이지를 사용하여 새 모델 프로젝트의 기본 설정을 변경할 수 있습니다. **속성** 창에서 각 모델 프로젝트에 대해 이러한 속성 및 기타 속성을 설정할 수도 있습니다. 이미 만들어진 모델 프로젝트에는 기본 설정 변경이 적용되지 않습니다. 자세한 내용은 참조 [기본 데이터 모델링 및 배포 속성 구성](../../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)합니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**통합 작업 영역 모드**|True, False|프로젝트를 만들 때 작업 영역 데이터베이스에 대해 통합 작업 영역 모드를 선택하는 경우 이 속성은 True가 됩니다. 프로젝트를 만들 때 **작업 영역 서버** 모드를 선택하는 경우 이 속성은 False가 됩니다. | 
|**작업 영역 데이터베이스**|이름|작업 영역 데이터베이스의 이름입니다. **통합 작업 영역 모드****True**인 경우 이 속성을 편집할 수 없습니다.|  
|**작업 영역 보존**|메모리에서 언로드|모델 프로젝트를 닫은 후 작업 영역 데이터베이스가 보존되는 방법을 지정합니다. 작업 영역 데이터베이스에는 모델 메타데이터와 가져온 데이터가 포함됩니다. 경우에 따라 작업 영역 데이터베이스가 매우 크고 많은 양의 메모리를 사용할 수 있습니다. 기본적으로 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 닫을 때 작업 영역 데이터베이스는 메모리에서 언로드됩니다. 이 설정을 변경할 때는 모델 프로젝트에서 작업할 빈도뿐만 아니라 사용 가능한 메모리 리소스를 고려해야 합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **메모리에 유지** - 모델 프로젝트를 닫은 후 메모리에 작업 영역 데이터베이스를 유지하도록 지정합니다. 이 옵션을 사용하면 메모리 소비량이 많아지지만 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 열 때 리소스가 더 적게 사용되며 작업 영역 데이터베이스가 더 빠르게 로드됩니다.<br /><br /> **메모리에서 언로드** - 모델 프로젝트를 닫은 후 디스크에는 작업 영역 데이터베이스를 유지하지만 메모리에는 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리가 더 적게 소비되지만, [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 열 때 작업 영역 데이터베이스를 다시 연결해야 하고 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리에 유지되는 경우보다 느리게 모델 프로젝트가 로드됩니다. 메모리 내 리소스가 제한되어 있거나 원격 작업 영역 데이터베이스에서 작업하는 경우 이 옵션을 사용하세요.<br /><br /> **작업 영역 삭제** - 모델 프로젝트를 닫은 후 메모리에서 작업 영역 데이터베이스를 삭제하고 디스크에 작업 영역 데이터베이스를 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리 및 저장소 공간 소비량이 줄어들지만 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 열 때 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리나 디스크에 유지되는 경우보다 느리게 모델 프로젝트가 로드됩니다. 가끔씩만 모델 프로젝트에서 작업하는 경우 이 옵션을 사용하십시오.<br /><br /> 도구\옵션 대화 상자의 **Analysis Server** 설정에서 **데이터 모델링** 페이지를 사용하여 이 속성의 기본 설정을 변경할 수 있습니다. **통합 작업 영역 모드****True**인 경우 이 속성을 편집할 수 없습니다.|  
|**작업 영역 서버**|localhost|이 속성은 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 모델 프로젝트를 제작하는 동안 작업 영역 데이터베이스를 호스팅하는 데 사용할 기본 서버를 지정합니다. 로컬 컴퓨터에서 실행되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 의 모든 사용 가능한 인스턴스가 목록 상자에 포함됩니다.<br /><br /> 다른 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버(테이블 형식 모드에서 실행)를 지정하려면 서버 이름을 입력합니다. 로그온한 사용자는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에서 관리자여야 합니다.<br /><br /> 로컬 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버를 작업 영역 서버로 지정하는 것이 좋습니다. 원격 서버에 있는 작업 영역 데이터베이스의 경우 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] 에서 가져오기가 지원되지 않고 데이터를 로컬로 백업할 수 없으며 쿼리 중에 사용자 인터페이스에서 지연이 발생할 수 있습니다.<br /><br /> 도구\옵션 대화 상자의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 설정에서 데이터 모델링 페이지를 사용하여 이 속성의 기본 설정을 변경할 수 있습니다. **통합 작업 영역 모드****True**인 경우 이 속성을 편집할 수 없습니다.|  
  
##  <a name="bkmk_use_ssms"></a> SSMS를 사용하여 작업 영역 데이터베이스 관리  
 SSMS(SQL Server Management Studio)를 사용하여 작업 영역 데이터베이스를 호스트하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 연결할 수 있습니다. 일반적으로 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 수행해야 하는 작업 영역 데이터베이스 분리 또는 삭제 작업을 제외하면 작업 영역 데이터베이스의 관리는 필요하지 않습니다. 모델 디자이너에 프로젝트가 열려 있는 동안 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 를 사용하여 작업 영역 데이터베이스를 관리하지 마십시오. 이렇게 하면 데이터가 손실될 수 있습니다.
   
## <a name="see-also"></a>참고 항목  
[모델 속성](../../analysis-services/tabular-models/model-properties-ssas-tabular.md) 
  
  
