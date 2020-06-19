---
title: 프로젝트 속성 (SSAS 테이블 형식) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.depservconfig.f1
- sql12.asvs.bidtoolset.semmodelprojprop.f1
ms.assetid: 333c1fc0-361c-415a-bd68-4e057f67bcb7
author: minewiskan
ms.author: owend
ms.openlocfilehash: a89a37f328bd8109002393107e400969b7699903
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938718"
---
# <a name="project-properties-ssas-tabular"></a>프로젝트 속성(SSAS 테이블 형식)
  이 항목에서는 모델 프로젝트 속성에 대해 설명합니다. 각 테이블 형식 모델 프로젝트에는 배포 옵션 및 배포 서버 속성이 제공되어 프로젝트 및 모델의 배포 방식을 지정할 수 있습니다. 예를 들어 모델이 배포될 서버와 배포될 모델 데이터베이스 이름을 지정할 수 있습니다. 이러한 설정은 모델 작업 영역 데이터베이스에 영향을 주는 모델 속성과 다릅니다. 여기에서 설명하는 프로젝트 속성은 모달 속성 대화 상자에 있습니다. 이 대화 상자는 다른 유형의 속성을 표시하는 데 사용되는 속성 창과 다릅니다. 모달 프로젝트 속성을 표시하려면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다.  
  
 이 항목의 섹션:  
  
-   [프로젝트 속성](#bkmk_proj_properties)  
  
-   [배포 옵션 및 배포 서버 속성 설정을 구성하려면](#bkmk_conf_proj_settings)  
  
##  <a name="project-properties"></a><a name="bkmk_proj_properties"></a>프로젝트 속성  
 **배포 옵션**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**처리 옵션**|**기본값**|기본적으로 Analysis Services에서 개체 변경 내용을 배포할 때 필요한 처리 유형을 결정합니다. 일반적으로 이 경우의 배포 시간이 가장 빠릅니다. 그러나 각 개체의 변경 내용 배포 시 전체 처리를 수행하거나 처리를 수행하지 않도록 선택할 수도 있습니다.|  
|**트랜잭션 배포**|**False**|모델의 배포가 트랜잭션인지 여부를 지정합니다. 기본적으로 모든 개체 또는 변경된 개체의 배포는 배포되는 개체의 처리에 있어서 트랜잭션이 아닙니다. 처리가 실패해도 배포는 성공하고 유지될 수 있습니다. 이를 변경하여 배포와 처리를 단일 트랜잭션에 통합할 수 있습니다.|  
|**쿼리 모드**|**메모리 내**|쿼리 결과가 반환될 원본을 지정합니다. 자세한 내용은 [DirectQuery 모드&#40;SSAS 테이블 형식&#41;](directquery-mode-ssas-tabular.md)를 참조하세요.|  
  
 **배포 서버**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**Server**|**localhost**|Analysis Services 인스턴스를 지정합니다. 기본적으로 모델은 로컬 컴퓨터에 있는 기본 Analysis Services 인스턴스로 배포됩니다. 이 설정을 변경하여 로컬 컴퓨터의 명명된 인스턴스 또는 Analysis Services 개체를 만들 권한이 있는 원격 컴퓨터의 인스턴스를 지정할 수 있습니다. 일반적으로 관리자 권한을 사용합니다.<br /><br /> 이 속성의 기본 설정은 도구\옵션 대화 상자에서 Analysis Server 설정의 배포 페이지에 있는 기본 배포 서버 속성을 사용하여 변경할 수 있습니다. 자세한 내용은 [기본 데이터 모델링 및 배포 속성 구성&#40;SSAS 테이블 형식&#41;](properties-ssas-tabular.md)을 참조하세요.|  
|**버전**|**개발자**|모델이 배포될 Analysis Services 서버의 버전을 지정합니다. 서버 버전은 프로젝트에 통합할 수 있는 다양한 기능을 정의합니다.|  
|**Database**|**모델**|배포 시 모델 개체가 인스턴스화될 Analysis Services 데이터베이스의 이름을 지정합니다. 이 이름은 데이터 연결 또는 .rsds 데이터 연결 파일에서 지정됩니다. 이름은 모델을 사용하여 수행할 분석 유형을 나타내는 것이 좋습니다(예: AdventureWorksSalesModel).<br /><br /> ** \* \* 중요 \* 배포 \* ** 된 모델의 이름이 중복 되지 않도록 하려면 모델의 용도를 반영 하도록 **데이터베이스** 속성 이름 설정을 변경 해야 합니다. 사용자가 데이터 원본으로 사용할 모델에 연결할 때 이 이름이 표시됩니다.|  
|**큐브 이름**|**모델**|보고 클라이언트 데이터 연결에 표시된 것과 같이 데이터베이스 큐브의 이름을 지정합니다.|  
|**버전**|**11.0**|프로젝트를 배포할 Analysis Services 인스턴스의 버전입니다.|  
  
 **DirectQuery 옵션**  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|**가장 설정**|**기본값**|DirectQuery 모드로 실행되는 모델의 데이터 원본에 연결하는 데 사용되는 자격 증명을 지정합니다. 이 자격 증명은 기본 메모리 내 모드에서 사용되는 가장 자격 증명과 다릅니다. 자세한 내용은 [가장&#40;SSAS 테이블 형식&#41;](impersonation-ssas-tabular.md)을 참조하세요.|  
  
###  <a name="to-configure-deployment-options-and-deployment-server-property-settings"></a><a name="bkmk_conf_proj_settings"></a>배포 옵션 및 배포 서버 속성 설정을 구성 하려면  
  
1.  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]의 **솔루션 탐색기**에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **속성**을 클릭합니다.  
  
2.  **속성** 창에서 속성을 클릭한 다음 값을 입력하거나 아래쪽 화살표를 클릭하여 설정 옵션을 선택합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SSAS 테이블 형식&#41;&#40;기본 데이터 모델링 및 배포 속성 구성](properties-ssas-tabular.md)   
 [SSAS 테이블 형식&#41;&#40;모델 속성](model-properties-ssas-tabular.md)   
 [테이블 형식 모델 솔루션 배포&#40;SSAS 테이블 형식&#41;](tabular-model-solution-deployment-ssas-tabular.md)  
  
  
