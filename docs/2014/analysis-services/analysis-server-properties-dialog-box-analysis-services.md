---
title: Analysis Server 속성 대화 상자 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- SQL12.ASVS.SSMSIMBI.SERVERPROPERTIES.F1
- SQL12.ASVS.SQLSERVERSTUDIO.SERVERPROPERTIES.F1
helpviewer_keywords:
- Analysis Server Properties dialog box
ms.assetid: b01ec658-c191-49c9-a6cb-549b21a368ab
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e9bcb19e10417c24b30b5ee6346d6d6a19d4bbcb
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/26/2018
ms.locfileid: "50145098"
---
# <a name="analysis-server-properties-dialog-box-analysis-services"></a>분석 서버 속성 대화 상자(Analysis Services)
  [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 **Analysis Server 속성** 대화 상자를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 일반, 언어/데이터 정렬 및 보안 설정을 지정할 수 있습니다. **개체 탐색기**에서 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스를 마우스 오른쪽 단추로 클릭하고 상황에 맞는 메뉴에서 **속성**을 선택하여 **Analysis Server 속성** 대화 상자를 표시할 수 있습니다. **Analysis Server 속성** 대화 상자에는 다음 속성이 있습니다.  
  
## <a name="information-properties"></a>정보 속성  
 이 페이지를 사용하여 서버 모드, 버전 및 호환성 수준을 봅니다. 각 인스턴스는 테이블 형식 또는 다차원 모델을 로드할 수 있는 기능과 함께 테이블 형식 또는 다차원 서버 모드에 설치됩니다. 두 모드를 모두 지원하려면 두 인스턴스를 설치해야 합니다.  
  
 **지원 되는 호환성 수준** 해당 하는 `DefaultCompatibilityLevel` AMO의 속성입니다. 설치 시 지정한 서버 배포 모드를 기반으로 읽기 전용입니다. 서버에서는 테이블 형식 서버 인스턴스에 테이블 형식 데이터베이스 백업을 복원하는 등 서버 모드 또는 버전에 따라 달라지는 작업을 수행할 때 이 속성을 확인합니다. 비슷한 이름 및 값을 가진 테이블 형식 또는 다차원 모델의 데이터베이스 호환성 모드와 혼동하지 마십시오. 이 서버 속성에 대한 유효한 값에는 다음이 포함됩니다.  
  
-   **1100** 은 다차원 및 데이터 마이닝 모드의 경우 배포 모드 0에 대한 기본 호환성 수준입니다.  
  
-   **1103** 은 테이블 형식 모드 또는 [!INCLUDE[ssGeminiShort](../includes/ssgeminishort-md.md)]를 지원하는 설치의 경우 배포 모드 1 또는 2에 대한 기본 호환성 수준입니다.  
  
 서버에서는 네임스페이스를 지원하는 클라이언트가 DISCOVER_XML_METADATA를 요청할 때 이 값을 반환합니다. 자세한 내용은 [DISCOVER_XML_METADATA 행 집합](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset)을 참조하세요.  
  
## <a name="general-properties"></a>일반 속성  
 이 페이지를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스에 대한 폴더 위치 및 네트워크 설정과 같은 기본 및 고급 일반 속성을 설정할 수 있습니다.  
  
 서버 속성 페이지에는 특정 구성에 대한 서버를 튜닝하는 데 사용되는 메모리 및 스레드 풀 속성과 같이 관리자가 변경하기 쉬운 속성만 표시됩니다. 다음 목록에서는 주 속성 그룹에 대한 링크를 제공합니다.  
  
-   [일반 속성](server-properties/general-properties.md)  
  
-   [데이터 마이닝 속성](server-properties/data-mining-properties.md)  
  
-   [기능 속성](server-properties/feature-properties.md)  
  
-   [Filestore 속성](server-properties/filestore-properties.md)  
  
-   [잠금 관리자 속성](server-properties/lock-manager-properties.md)  
  
-   [로그 속성](server-properties/log-properties.md)  
  
-   [메모리 속성](server-properties/memory-properties.md)  
  
-   [네트워크 속성](server-properties/network-properties.md)  
  
-   [OLAP 속성](server-properties/olap-properties.md)  
  
-   [보안 속성](server-properties/security-properties.md)  
  
-   [스레드 풀 속성](server-properties/thread-pool-properties.md)  
  
## <a name="language-collation-properties"></a>언어/데이터 정렬 속성  
 이 페이지를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]의 기본 언어 및 데이터 정렬 옵션을 설정할 수 있습니다. 다음 목록에는 각 옵션에 대한 간략한 설명이 포함됩니다. 자세한 설명은 [언어 및 데이터 정렬&#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)을 참조하세요.  
  
-   **이진** 은 각 문자에 대해 정의된 비트 패턴을 기준으로 데이터를 정렬 및 비교하는 데 사용됩니다. 이진 정렬 순서는 대/소문자(소문자가 대문자 앞에 와야 함) 및 악센트를 구분합니다. 이것은 가장 빠른 정렬 순서입니다.  
  
     이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 관련된 언어 또는 알파벳에 대해 사전에 정의된 정렬 및 비교 규칙을 따릅니다.  
  
    > [!NOTE]  
    >  이 옵션을 선택하면 **대/소문자 구분**, **악센트 구분**, **일본어 가나 구분**및 **전자/반자 구분** 옵션을 사용할 수 없습니다.  
  
-   **이진 2** 는 각 문자에 대해 정의된 비트 패턴을 기준으로 유니코드 데이터를 정렬 및 비교하는 데 사용됩니다. 이진 정렬 순서는 대/소문자(소문자가 대문자 앞에 와야 함) 및 악센트를 구분합니다. 이것은 가장 빠른 정렬 순서입니다.  
  
-   **대/소문자 구분** 은 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 대문자와 소문자를 구분하는 데 사용됩니다.  
  
     이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 대문자와 소문자가 동일한 것으로 간주합니다. [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 여부를 소문자의 정렬 순서 문자와 관련 된 대문자 시기를 정의 하지 않습니다 **대/소문자 구분** 선택 하지 않으면.  
  
-   **악센트 구분** 은 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 악센트가 있는 문자와 악센트가 없는 문자를 구분하는 데 사용됩니다. 예를 들어 'a'와 'á'는 같지 않습니다.  
  
     이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 악센트가 있는 문자와 악센트가 없는 문자가 동일한 것으로 간주합니다.  
  
-   **일본어 가나 구분** 은 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 히라가나와 가타카나 등 두 가지 유형의 일본어 가나 문자를 구분하는 데 사용됩니다.  
  
     이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 는 히라가나 문자와 가타카나 문자가 동일한 것으로 간주합니다.  
  
-   **전자/반자 구분** 은 관련된 언어 또는 알파벳에 대해 제공된 사전 규칙을 기준으로 데이터를 정렬 및 비교하고 단일 바이트 문자(반자)와 더블바이트 문자로 표시될 때의 동일한 문자(전자)를 구분하는 데 사용됩니다.  
  
     이 옵션을 선택하지 않으면 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]는 싱글바이트와 더블바이트로 표시된 같은 문자를 동일한 것으로 간주합니다.  
  
## <a name="security-properties"></a>보안 속성  
 이 페이지를 사용하여 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 인스턴스의 서버 관리자 역할에 속하는 Windows 사용자 및 그룹 계정을 지정할 수 있습니다. 이 역할의 멤버 자격에 대한 권한이 있으면 데이터베이스를 만들거나 처리하고 서버 속성을 수정하고 이 역할의 다른 멤버를 추가 또는 제거하거나 추적을 시작하는 등 서버 차원 태스크를 수행할 수 있습니다. 참조 [서버 관리자 권한 부여 &#40;Analysis Services&#41; ](instances/grant-server-admin-rights-to-an-analysis-services-instance.md) 세부 정보에 대 한 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 인스턴스의 서버 모드 확인](instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Analysis Services의 서버 속성 구성](server-properties/server-properties-in-analysis-services.md)   
 [Analysis Services에서 지원하는 인증 방법](instances/authentication-methodologies-supported-by-analysis-services.md)   
 [역할 및 권한&#40;Analysis Services&#41;](multidimensional-models/roles-and-permissions-analysis-services.md)   
 [언어 및 데이터 정렬&#40;Analysis Services&#41;](languages-and-collations-analysis-services.md)  
  
  
