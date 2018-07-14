---
title: 모델 속성 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.fileprop.f1
- sql12.asvs.bidtoolset.wspacedbconfig.f1
ms.assetid: 8ab04656-75a5-485c-9687-7b1ca49f7f80
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dd7defb693d6dbce28382a95e45b478293d2aadc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37202213"
---
# <a name="model-properties-ssas-tabular"></a>모델 속성(SSAS 테이블 형식)
  이 항목에서는 테이블 형식 모델 속성에 대해 설명합니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 테이블 형식 모델 프로젝트 각각에는 제작하는 모델의 빌드 방식, 백업 방식 및 작업 영역 데이터베이스의 저장 방식에 영향을 주는 모델 속성이 있습니다. 여기서 설명하는 모델 속성은 이미 배포된 모델에는 적용되지 않습니다.  
  
 이 항목의 섹션:  
  
-   [모델 속성](#bkmk_model_properties)  
  
-   [모델 속성 설정을 구성 하려면](#bkmk_conf)  
  
##  <a name="bkmk_model_properties"></a> 모델 속성  
 **고급**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**빌드 동작**|컴파일|이 속성은 파일이 빌드 및 배포 프로세스에 관련되는 방식을 지정합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **컴파일** - 정상적인 빌드 동작이 수행됩니다. 모델 개체에 대한 정의는 .asdatabase 파일에 기록됩니다.<br /><br /> **없음** - .asdatabase 파일에 대한 출력이 비어 있게 됩니다.|  
|**출력 디렉터리로 복사**|복사 안 함|이 속성은 출력 디렉터리에 복사될 원본 파일을 지정합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **복사 안 함** - 출력 디렉터리에 복사본이 만들어지지 않습니다.<br /><br /> **항상 복사** - 출력 디렉터리에 복사본이 항상 만들어집니다.<br /><br /> **변경된 내용만 복사** - model.bim 파일에 변경 내용이 있을 경우에만 출력 디렉터리에 복사본이 만들어집니다.|  
  
 **기타**  
  
> [!NOTE]  
>  일부 속성은 모델을 만들 때 자동으로 설정되며 변경할 수 없습니다.  
  
> [!NOTE]  
>  작업 영역 서버, 작업 영역 보존 및 데이터 백업 속성은 새 모델 프로젝트를 만들 때 적용되는 기본 설정을 가지고 있습니다. 도구\옵션 대화 상자의 Analysis Server 설정에서 데이터 모델링 페이지를 사용하여 새 모델의 기본 설정을 변경할 수 있습니다. 속성 창에서 각 모델에 대해 이러한 속성 및 기타 속성을 설정할 수도 있습니다. 자세한 내용은 [기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)을 참조하세요.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**데이터 정렬**|Visual Studio가 설치된 컴퓨터의 기본 데이터 정렬입니다.|모델에 대한 데이터 정렬 지정자입니다.|  
|**호환성 수준**|기본 수준 또는 프로젝트를 만들 때 선택한 다른 수준입니다.|SQL Server 2012 Analysis Services SP1 이상에 적용됩니다. 이 모델에 사용할 수 있는 기능과 설정을 지정합니다. 자세한 내용은 [호환성 &#40;SSAS 테이블 형식 SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)합니다.|  
|**데이터 백업**|디스크에 백업 안 함|모델 데이터의 백업이 백업 파일에 유지되는지 여부를 지정합니다. 도구 \ 옵션 대화 상자의 분석 서버 설정에서 데이터 모델링 페이지에서이 속성에 대 한 기본 설정은 변경할 수 있습니다 note 합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **디스크에 백업** - 모델 데이터의 백업을 디스크에 유지하도록 지정합니다. 모델을 저장하면 데이터가 백업 파일(ABF)에도 저장됩니다. 이 옵션을 선택하면 모델 저장 및 로드 시간이 길어질 수 있습니다.<br /><br /> **디스크에 백업 안 함** - 모델 데이터의 백업을 디스크에 유지하지 않도록 지정합니다. 이 옵션을 사용하면 저장 및 모델 로드 시간이 최소화됩니다.|  
|**DirectQuery 모드**|Off|이 모델이 DirectQuery 모드에서 작동하는지 여부를 지정합니다. 자세한 내용은 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](directquery-mode-ssas-tabular.md)를 참조하세요.|  
|**파일 이름**|Model.bim|.bim 파일의 이름을 지정합니다. 파일 이름은 변경할 수 없습니다.|  
|**전체 경로**|프로젝트를 만들 때 지정한 경로입니다.|model.bim 파일 위치입니다. 이 속성은 속성 창에서 설정할 수 없습니다.|  
|**언어**|영어|모델의 기본 언어입니다. Visual Studio 언어에 따라 결정되는 기본 언어입니다. 이 속성은 속성 창에서 설정할 수 없습니다.|  
|**작업 영역 데이터베이스**|프로젝트 이름 뒤에 밑줄이 오고 그 뒤에 GUID가 옵니다.|선택한 model.bim 파일의 메모리 내 모델을 저장하고 편집하는 데 사용되는 작업 영역 데이터베이스의 이름입니다. 이 데이터베이스는 작업 영역 서버 속성에 지정된 Analysis Services 인스턴스에 나타납니다. 이 속성은 속성 창에서 설정할 수 없습니다. 자세한 내용은 [작업 영역 데이터베이스&#40;SSAS 테이블 형식&#41;](workspace-database-ssas-tabular.md)를 참조하세요.|  
|**작업 영역 보존**|메모리에서 언로드|모델을 닫은 후 작업 영역 데이터베이스가 보존되는 방법을 지정합니다. 작업 영역 데이터베이스에는 모델 메타데이터, 모델로 가져온 데이터 및 가장 자격 증명(암호화됨)이 포함됩니다. 경우에 따라 작업 영역 데이터베이스가 매우 크고 많은 양의 메모리를 사용할 수 있습니다. 기본적으로 작업 영역 데이터베이스는 메모리에서 언로드됩니다. 이 설정을 변경할 때는 모델에서 작업할 빈도뿐만 아니라 사용 가능한 메모리 리소스를 고려해야 합니다. 도구 \ 옵션 대화 상자의 분석 서버 설정에서 데이터 모델링 페이지에서이 속성에 대 한 기본 설정은 변경할 수 있습니다 note 합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **메모리에 유지** - 모델을 닫은 후 메모리에 작업 영역 데이터베이스를 유지하도록 지정합니다. 이 옵션을 사용 하면 메모리; 그러나에서 모델을 열 때 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]더 적은 리소스가 사용 되 고 작업 영역 데이터베이스가 더 빠르게 로드 됩니다.<br /><br /> **메모리에서 언로드** - 모델을 닫은 후 디스크에는 작업 영역 데이터베이스를 유지하지만 메모리에는 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리 소비량이 적어지지만 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 열 때 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리에 유지되는 경우보다 느리게 모델이 로드됩니다. 메모리 내 리소스가 제한되어 있거나 원격 작업 영역 데이터베이스에서 작업하는 경우 이 옵션을 사용하십시오.<br /><br /> **작업 영역 삭제** - 모델을 닫은 후 메모리에서 작업 영역 데이터베이스를 삭제하고 디스크에 작업 영역 데이터베이스를 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리 및 저장소 공간 소비량이 적어지지만 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 열 때 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리나 디스크에 유지되는 경우보다 느리게 모델이 로드됩니다. 가끔씩만 모델에서 작업하는 경우 이 옵션을 사용하세요.|  
|**작업 영역 서버**|localhost|이 속성은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 작성하는 동안 작업 영역 데이터베이스를 호스팅하는 데 사용할 기본 서버를 지정합니다. 로컬 컴퓨터에서 실행되는 Analysis Services의 모든 사용 가능한 인스턴스가 목록 상자에 포함됩니다.<br /><br /> 참고: 항상 로컬 Analysis Services 서버를 작업 영역 서버로 지정하는 것이 좋습니다. 원격 서버에 있는 작업 영역 데이터베이스의 경우 PowerPivot에서 가져오기가 지원되지 않고 데이터를 로컬로 백업할 수 없으며 쿼리 중에 사용자 인터페이스에서 지연이 발생할 수 있습니다.<br /><br /> 도구\옵션 대화 상자의 Analysis Server 설정에서 데이터 모델링 페이지를 사용하여 이 속성의 기본 설정을 변경할 수 있습니다.|  
  
##  <a name="bkmk_conf_model_prop"></a>   
###  <a name="bkmk_conf"></a> 모델 속성 설정을 구성 하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**를 클릭 합니다 **Model.bim** 파일입니다.  
  
2.  **속성** 창에서 속성을 클릭한 다음 값을 입력하거나 아래쪽 화살표를 클릭하여 설정 옵션을 선택합니다.  
  
## <a name="see-also"></a>관련 항목  
 [기본 데이터 모델링 및 배포 속성 구성 &#40;&AMP;#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)   
 [프로젝트 속성 &#40;&AMP;#40;SSAS 테이블 형식&#41;](project-properties-ssas-tabular.md)  
  
  
