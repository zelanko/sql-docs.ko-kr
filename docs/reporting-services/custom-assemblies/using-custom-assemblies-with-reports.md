---
title: 보고서에서 사용자 지정 어셈블리 사용 | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-assemblies
ms.topic: reference
helpviewer_keywords:
- custom assemblies [Reporting Services]
- assemblies [Reporting Services], custom
- custom assemblies [Reporting Services], about custom assemblies
ms.assetid: 53d141d0-2185-466a-84dc-7b90d284da3d
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 94fdcbb6219aefb0cf38f0d77c0c3437ccf19915
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194100"
---
# <a name="using-custom-assemblies-with-reports"></a>보고서에서 사용자 지정 어셈블리 사용
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]에서 보고서 항목 값, 스타일 및 서식 지정을 위한 사용자 지정 코드를 작성할 수 있습니다. 예를 들어, 사용자 지정 코드를 사용하여 로캘에 따른 통화 형식을 지정하거나 특정 값을 특수한 서식으로 플래그 지정하거나 회사에서 사용되는 다른 비즈니스 규칙을 적용할 수 있습니다. 보고서에 이 코드를 포함시키는 방법은 보고서 정의 파일 내에서 참조할 수 있는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]를 사용하여 사용자 지정 코드 어셈블리를 만드는 것입니다. 보고서가 실행되면 서버는 사용자 어셈블리에서 함수를 호출합니다. 사용자 지정 어셈블리는 보고서에서 사용하고자 하는 특수화된 함수를 검색하는 데 사용할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [RDL 파일에서 어셈블리 참조](../../reporting-services/custom-assemblies/referencing-assemblies-in-an-rdl-file.md)  
 보고서 정의 언어 파일에서 사용자 지정 어셈블리를 참조하는 방법을 설명합니다.  
  
 [사용자 지정 어셈블리 배포](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
 사용자 지정 어셈블리를 보고서 디자이너 및 보고서 서버에 배포하는 방법을 설명합니다.  
  
 [강력한 이름의 사용자 지정 어셈블리 사용](../../reporting-services/custom-assemblies/using-strong-named-custom-assemblies.md)  
 강력한 이름을 가진 사용자 지정 어셈블리를 사용하는 방법을 설명합니다.  
  
 [사용자 지정 어셈블리에서 사용 권한 어설션](../../reporting-services/custom-assemblies/asserting-permissions-in-custom-assemblies.md)  
 제한된 권한 및 특정 권한으로 사용자 지정 어셈블리를 배포하는 방법과 이러한 권한을 코드에서 어설션하는 방법을 설명합니다.  
  
 [식을 통해 사용자 지정 어셈블리 액세스](../../reporting-services/custom-assemblies/accessing-custom-assemblies-through-expressions.md)  
 사용자 지정 어셈블리 메서드를 보고서 정의에서 보고서 식의 형태로 호출하는 방법을 설명합니다.  
  
 [사용자 지정 어셈블리 개체 초기화](../../reporting-services/custom-assemblies/initializing-custom-assembly-objects.md)  
 보고서에서 호출된 사용자 지정 어셈블리 개체에 대한 값을 초기화하는 방법을 설명합니다.  
  
 [방법: 사용자 지정 어셈블리 디버깅](../../reporting-services/custom-assemblies/how-to-debug-custom-assemblies.md)  
 사용자 지정 어셈블리 코드를 디버깅하는 방법을 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [RDL(Report Definition Language)&#40;SSRS&#41;](../../reporting-services/reports/report-definition-language-ssrs.md)  
  
  
