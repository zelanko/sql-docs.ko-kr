---
title: 기본 데이터 모델링 및 배포 속성 구성 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.deployment.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DATA_MODELING
- sql12.asvs.bidtoolset.asoptions.f1
- VS.TOOLSOPTIONSPAGES.ANALYSIS_SERVICES.DEPLOYMENT
ms.assetid: 140d0c4e-943c-4387-a8d2-6e066c7e4e75
author: minewiskan
ms.author: owend
ms.openlocfilehash: 99d1e2e6f4e4bca69b093aeb9c259db59d503083
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939864"
---
# <a name="configure-default-data-modeling-and-deployment-properties-ssas-tabular"></a>기본 데이터 모델링 및 배포 속성 구성(SSAS 테이블 형식)
  이 항목에서는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 만든 각각의 새로운 테이블 형식 모델 프로젝트에 대해 미리 정의될 수 있는 기본 호환성 수준, 배포 및 작업 영역 데이터베이스 속성 설정을 구성하는 방법에 대해 설명합니다. 새 프로젝트를 만든 후 특정 요구 사항에 따라 이러한 속성을 변경할 수 있습니다.  
  
#### <a name="to-configure-the-default-compatibility-level-property-setting-for-new-model-projects"></a>새 모델 프로젝트의 기본 호환성 수준 속성 설정을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **도구** 메뉴를 클릭한 다음 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **Analysis Services 테이블 형식 디자이너**를 확장한 다음 **호환성 수준**을 클릭합니다.  
  
3.  다음 속성 설정을 구성합니다.  
  
    |속성|기본 설정|Description|  
    |--------------|---------------------|-----------------|  
    |**새 프로젝트의 기본 호환성 수준**|SQL Server 2012 (1100)|이 설정은 새 테이블 형식 모델 프로젝트를 만들 때 사용할 기본 호환성 수준을 지정합니다. SP1이 적용되지 않은 Analysis Services 인스턴스에 배포하려는 경우 SQL Server 2012 RTM(1100)을 선택하거나 배포 인스턴스에 SP1이 적용된 경우 SQL Server 2012 SP1 또는 SQL Server 2014를 선택할 수 있습니다. 자세한 내용은 [호환성 수준 &#40;SSAS 테이블 형식 SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)을 참조 하세요.|  
    |**호환성 수준 옵션**|모든 선택됨|새 테이블 형식 모델 프로젝트의 호환성 수준 옵션 및 다른 Analysis Services 인스턴스에 배포할 시기를 지정합니다.|  
  
#### <a name="to-configure-the-default-deployment-server-property-setting-for-new-model-projects"></a>새 모델 프로젝트의 기본 배포 서버 속성 설정을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **도구** 메뉴를 클릭한 다음 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **Analysis Services 테이블 형식 디자이너**를 확장한 다음 **배포**를 클릭합니다.  
  
3.  다음 속성 설정을 구성합니다.  
  
    |속성|기본 설정|Description|  
    |--------------|---------------------|-----------------|  
    |**기본 배포 서버**|localhost|이 설정은 모델을 배포할 때 사용할 기본 서버를 지정합니다. 아래쪽 화살표를 클릭하여 사용할 수 있는 로컬 네트워크 Analysis Services 서버를 찾아보거나 원격 서버의 이름을 입력할 수 있습니다.|  
  
    > [!NOTE]  
    >  기본 배포 서버 속성 설정을 변경해도 변경 전에 만들어진 기존 프로젝트는 영향을 받지 않습니다.  
  
###  <a name="to-configure-the-default-workspace-database-property-settings-for-new-model-projects"></a><a name="bkmk_conf_default"></a> 새 모델 프로젝트의 기본 작업 영역 데이터베이스 속성 설정을 구성하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 **도구** 메뉴를 클릭한 다음 **옵션**을 클릭합니다.  
  
2.  **옵션** 대화 상자에서 **Analysis Services 테이블 형식 디자이너**를 확장한 다음 **작업 영역 데이터베이스**를 클릭합니다.  
  
3.  다음 속성 설정을 구성합니다.  
  
    |속성|기본 설정|Description|  
    |--------------|---------------------|-----------------|  
    |**기본 작업 영역 서버**|**localhost**|이 속성은 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 작성하는 동안 작업 영역 데이터베이스를 호스팅하는 데 사용할 기본 서버를 지정합니다. 로컬 컴퓨터에서 실행되는 Analysis Services의 모든 사용 가능한 인스턴스가 목록 상자에 포함됩니다.<br /><br /> 참고: 항상 로컬 Analysis Services 서버를 작업 영역 서버로 지정하는 것이 좋습니다. 원격 서버에 있는 작업 영역 데이터베이스의 경우 PowerPivot에서 데이터 가져오기가 지원되지 않고 데이터를 로컬로 백업할 수 없으며 쿼리 중에 사용자 인터페이스에서 지연이 발생할 수 있습니다.|  
    |**모델을 닫은 후 작업 영역 데이터베이스 보존**|**작업 영역 데이터베이스를 디스크에 유지하지만 메모리에서 언로드**|모델을 닫은 후 작업 영역 데이터베이스가 보존되는 방법을 지정합니다. 작업 영역 데이터베이스에는 모델 메타데이터, 모델로 가져온 데이터 및 가장 자격 증명(암호화됨)이 포함됩니다. 경우에 따라 작업 영역 데이터베이스가 매우 크고 많은 양의 메모리를 사용할 수 있습니다. 기본적으로 작업 영역 데이터베이스는 메모리에서 제거됩니다. 이 설정을 변경할 때는 모델에서 작업할 빈도뿐만 아니라 사용 가능한 메모리 리소스를 고려해야 합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **작업 영역을 메모리에 유지** - 모델을 닫은 후 메모리에 작업 영역을 유지하도록 지정합니다. 이 옵션을 사용하면 메모리 소비량이 많아지지만 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 열 때 리소스가 더 적게 사용되며 작업 영역이 더 빠르게 로드됩니다.<br /><br /> **작업 영역 데이터베이스를 디스크에 유지하지만 메모리에서 언로드** - 모델을 닫은 후 디스크에는 작업 영역 데이터베이스를 유지하지만 메모리에는 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리 소비량이 적어지지만 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 열 때 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리에 유지되는 경우보다 느리게 모델이 로드됩니다. 메모리 내 리소스가 제한되어 있거나 원격 작업 영역 데이터베이스에서 작업하는 경우 이 옵션을 사용하세요.<br /><br /> **작업 영역 삭제** - 모델을 닫은 후 메모리에서 작업 영역 데이터베이스를 삭제하고 디스크에 작업 영역 데이터베이스를 유지하지 않도록 지정합니다. 이 옵션을 사용하면 메모리 및 스토리지 공간 소비량이 적어지지만 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 모델을 열 때 리소스가 추가로 소비되며 작업 영역 데이터베이스가 메모리나 디스크에 유지되는 경우보다 느리게 모델이 로드됩니다. 가끔씩만 모델에서 작업하는 경우 이 옵션을 사용하세요.|  
    |**데이터 백업**|**디스크 데이터의 백업 보관**|모델 데이터의 백업이 백업 파일에 유지되는지 여부를 지정합니다. 이 속성 설정에는 다음과 같은 옵션이 있습니다.<br /><br /> **디스크에 데이터 백업 보관** - 모델 데이터의 백업을 디스크에 보관하도록 지정합니다. 모델을 저장하면 데이터가 백업 파일(ABF)에도 저장됩니다. 이 옵션을 선택하면 모델 저장 및 로드 시간이 길어질 수 있습니다.<br /><br /> **디스크에 데이터 백업 보관 안 함** - 모델 데이터의 백업을 디스크에 보관하지 않도록 지정합니다. 이 옵션을 사용하면 저장 및 모델 로드 시간이 최소화됩니다.|  
  
> [!NOTE]  
>  기본 모델 속성을 변경해도 변경 전에 만들어진 기존 모델의 속성은 영향을 받지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
 [프로젝트 속성 &#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)   
 [SSAS 테이블 형식&#41;&#40;모델 속성](model-properties-ssas-tabular.md)   
 [호환성 수준 &#40;SSAS 테이블 형식 SP1&#41;](compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
