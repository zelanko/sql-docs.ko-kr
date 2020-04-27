---
title: Analysis Services 프로젝트 빌드 (SSDT) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- projects [Analysis Services], building
- Business Intelligence Development Studio, project building [Analysis Services]
ms.assetid: caac03cb-b2b4-4652-8913-3dd39c4b0127
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 97e32b80d19675b3763101d1c226529a48e23e68
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66076769"
---
# <a name="build-analysis-services-projects-ssdt"></a>Analysis Services 프로젝트 빌드(SSDT)
  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에서는 Visual Studio에서 프로그래밍 개체를 빌드하는 것과 유사한 방식으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 빌드할 수 있습니다. 프로젝트를 빌드하면 출력 디렉터리에 XML 파일 집합이 생성됩니다. 이러한 XML 파일은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 비롯한 클라이언트 애플리케이션에서 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 만들거나 수정하기 위해 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스와 통신하는 데 사용하는 XML 언어인 ASSL(Analysis Services Scripting Language)을 사용합니다. XML 파일은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 정의를 지정한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 배포하는 데 사용됩니다.  
  
## <a name="building-a-project"></a>프로젝트 빌드  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 빌드하면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 프로젝트의 모든 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스 개체를 작성하는 데 필요한 모든 ASSL 명령을 비롯한 전체 XML 파일 집합을 출력 폴더에 작성합니다. 프로젝트가 이전에 빌드되었으며 활성 구성에 증분 배포가 지정되어 있으면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 배포된 개체에 대한 증분 업데이트를 수행하는 ASSL 명령이 포함된 XML 파일도 작성합니다. 이 XML 파일은 프로젝트의 ..\obj\\<활성 구성\> 폴더에 기록됩니다. 증분 빌드를 사용하면 대규모 프로젝트나 데이터베이스를 배포 및 처리할 때 시간을 절약할 수 있습니다.  
  
> [!NOTE]  
>  모두 다시 빌드 명령을 사용하여 증분 배포 설정을 무시할 수 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 빌드하면 프로젝트에 있는 개체 정의의 유효성이 검사됩니다. 유효성 검사에는 참조된 어셈블리도 모두 포함됩니다. 빌드 오류는 AMO(Analysis Management Objects) 오류 텍스트와 함께 태스크 목록 창에 표시됩니다. 오류를 클릭하면 오류 수정에 필요한 디자이너를 열 수 있습니다.  
  
 유효성 검사에 성공했다고 해서 반드시 배포 중에 개체가 대상 서버에서 생성되거나 배포 후에 성공적으로 처리될 수 있는 것은 아닙니다. 다음과 같은 문제로 인해 배포나 배포 후의 처리에 성공하지 못할 수 있습니다.  
  
-   서버에 대한 보안 검사가 수행되지 않아 잠금이 발생하여 배포할 수 없습니다.  
  
-   서버에서 물리적 위치의 유효성이 검사되지 않았습니다.  
  
-   데이터 원본 뷰의 세부 정보가 대상 서버의 실제 데이터 원본에 대해 확인되지 않았습니다.  
  
 유효성 검사에 성공하면 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 에서 XML 파일을 생성합니다. 빌드 후에 출력 폴더에는 다음 표에 설명된 파일이 포함됩니다.  
  
|파일(bin 폴더)|설명|  
|-----------------------------|-----------------|  
|*Projectname*.asdatabase|배포 스크립트 파일에 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트의 개체에 대한 메타데이터를 정의하는 ASSL 요소를 포함합니다. 배포 엔진은 이 파일을 사용하여 해당 개체를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 배포합니다.|  
|*Projectname*.configsettings|배포 중에 사용되며 직접 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 수정할 수 있는 구성 설정을 포함합니다(예: 데이터 원본에 대한 연결 문자열).|  
|*Projectname*.deploymenttargets|배포 중에 사용되며 직접 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 수정할 수 있는 대상 설정을 포함합니다(예: 서버 및 데이터베이스 이름).|  
|*Projectname*.deploymentoptions|배포 중에 사용되며 직접 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 마법사에서 수정할 수 있는 다양한 옵션 설정을 포함합니다(예: 스토리지 위치).|  
|*Assemblyname*/*dllname.* gdiplus.dll|참조된 각 어셈블리에 대한 개별 폴더입니다. 각 폴더에는 어셈블리에 대한 DLL, 참조된 모든 어셈블리 및 출력 디버그 정보를 위한 연결된 모든 .pdb 파일이 들어 있습니다.|  
  
|파일(obj 폴더)|설명|  
|-----------------------------|-----------------|  
|\<구성 이름> \LastBuilt.xml|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트가 마지막으로 빌드된 시간을 식별하는 타임스탬프 및 해시 코드를 포함합니다.|  
  
 이러한 XML 파일에는 배포 \<중에 생성 \<되는 Create> 및 Alter> 태그가 포함 되지 않습니다.  
  
 참조된 어셈블리(표준 시스템 및 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 어셈블리 제외)도 출력 디렉터리로 복사됩니다. 솔루션의 다른 프로젝트를 참조하는 경우 적절한 프로젝트 구성과 프로젝트 참조에 의해 설정된 빌드 종속성을 사용하여 해당 프로젝트가 먼저 빌드된 다음 프로젝트 출력 폴더로 복사됩니다.  
  
## <a name="see-also"></a>참고 항목  
 [Analysis Services 스크립팅 언어 &#40;,&#41; 참조](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla)   
 [Analysis Services 프로젝트 배포&#40;SSDT&#41;](deploy-analysis-services-projects-ssdt.md)  
  
  
