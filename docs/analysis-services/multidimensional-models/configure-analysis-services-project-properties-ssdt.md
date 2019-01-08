---
title: Analysis Services 프로젝트 속성 구성 (SSDT) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 90fd3a238d7b4ab3e573c4ecef76bdbdd3bde7f1
ms.sourcegitcommit: 3f19c843b38d3835d07921612f0143620eb9a0e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53709806"
---
# <a name="configure-analysis-services-project-properties-ssdt"></a>Analysis Services 프로젝트 속성 구성(SSDT)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 작성 및 배포에 영향을 미치는 몇 가지 기본 속성과 함께 정의됩니다.  
  
 프로젝트 속성을 변경하려면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 개체를 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. 또는 프로젝트 메뉴에서 **속성** 을 클릭해도 됩니다.  
  
## <a name="property-description"></a>속성 설명  
 다음 표에서는 각 프로젝트 속성에 대해 설명하고 기본값을 나열하며 값 변경에 대한 정보를 제공합니다.  
  
|속성|기본 설정|Description|  
|--------------|---------------------|-----------------|  
|빌드 / 배포 서버 버전|프로젝트 개발에 사용되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전|프로젝트가 최종적으로 배포될 서버의 버전을 지정합니다. 여러 개발자가 한 프로젝트에서 작업하는 경우 개발자가 서버 버전을 이해해야만 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트에 통합될 기능을 알 수 있습니다.|  
|빌드 / 배포 서버 버전|프로젝트 개발에 사용되는 버전|프로젝트가 최종적으로 배포될 서버의 버전을 지정합니다.|  
|빌드 / 출력|/bin|프로젝트 빌드 프로세스 출력의 상대 경로입니다.|  
|빌드 / 암호 제거|True|빌드 프로세스 중에 출력 디렉터리에 기록되는 연결 문자열에서 알려진 암호를 제거할지 여부를 지정합니다. 암호는 보안을 향상시키기 위해 제거됩니다. 암호를 제거하면 배포된 프로젝트를 처리할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 원본 데이터에 액세스할 수 있도록 암호를 제공해야 합니다.|  
|디버깅 / 시작 개체|\<현재 활성 개체 >|디버깅을 시작할 때 시작될 개체를 결정합니다.|  
|배포 / 배포 모드|변경 내용만 배포|프로젝트 외부에서 직접 개체를 변경하지 않은 경우 기본적으로 프로젝트 개체의 변경 내용만 배포됩니다. 각 개체의 변경 내용 배포 중에 모든 프로젝트 개체를 배포하도록 선택할 수도 있습니다. 최상의 성능을 얻으려면 변경 내용만 배포를 사용합니다.|  
|배포 / 처리 옵션|Default|기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 개체 변경 내용을 배포할 때 필요한 처리 유형을 결정합니다. 일반적으로 이 경우의 배포 시간이 가장 빠릅니다. 그러나 각 개체의 변경 내용 배포 시 전체 처리를 수행하거나 처리를 수행하지 않도록 선택할 수도 있습니다.|  
|배포 / 트랜잭션 배포|False|기본적으로 변경된 개체나 모든 개체의 배포는 배포된 개체의 처리를 포함하는 트랜잭션이 아닙니다. 처리가 실패해도 배포는 성공하고 유지될 수 있습니다. 이 기본값을 변경하여 배포 및 처리를 단일 트랜잭션에 통합할 수 있습니다.|  
|배포/대상 서버|localhost|기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 내의 데이터베이스 개체는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 사용되는 로컬 컴퓨터에 있는 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 의 기본 인스턴스에 배포됩니다. 이 기본값을 변경하여 로컬 컴퓨터의 명명된 인스턴스나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 만들 권한이 있는 원격 컴퓨터의 임의 인스턴스를 지정할 수 있습니다.|  
|배포 / 데이터베이스|\<프로젝트 이름 >|기본적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 개체가 배포 시 인스턴스화되는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 이름은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 정의할 때 지정한 이름입니다. 이 속성을 변경하여 서버 속성에 지정된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스의 데이터베이스 이름을 변경할 수 있습니다.|  
  
## <a name="property-configurations"></a>속성 구성  
 속성은 구성 단위로 정의됩니다. 프로젝트 구성을 사용하면 개발자가 기본 XML 프로젝트 파일을 직접 편집하지 않고도 다른 빌드, 디버깅 및 배포 설정으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 사용할 수 있습니다.  
  
 처음에 프로젝트는 Development라는 하나의 구성으로 생성됩니다. 구성 관리자를 사용하여 추가 구성을 만들고 구성 간에 전환할 수 있습니다.  
  
 추가 구성을 만들 때까지는 모든 개발자가 이 일반 구성을 사용합니다. 그러나 다양 한 단계 중 초기 개발 하는 동안 같은 개발 프로젝트와 다른 데이터 원본을 사용 및 다양 한 용도로 여러 서버에 프로젝트를 배포할 수 있습니다-다른 개발자가 프로젝트의 테스트 합니다. 구성을 사용하면 이러한 각각의 설정을 서로 다른 구성 파일에 유지할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 프로젝트 빌드&#40;SSDT&#41;](../../analysis-services/multidimensional-models/build-analysis-services-projects-ssdt.md)   
 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](../../analysis-services/multidimensional-models/deploy-analysis-services-projects-ssdt.md)  
  
  
