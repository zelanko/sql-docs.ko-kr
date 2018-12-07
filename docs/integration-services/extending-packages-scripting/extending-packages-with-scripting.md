---
title: 스크립팅을 사용한 패키지 확장 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SQL Server Integration Services, scripting
- SSIS, scripting
- scripts [Integration Services], about scripting
ms.assetid: 67fe18ef-f3aa-41d4-9b9d-5defd4618c4b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5928217d9ca44cf03fda79009da42a52e7f0614a
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52517256"
---
# <a name="extending-packages-with-scripting"></a>스크립팅을 사용한 패키지 확장
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 기본 제공 구성 요소가 개발자의 요구 사항을 충족시키지 못할 경우 개발자 고유의 확장을 코딩하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 기능을 확장할 수 있습니다. 두 가지 방법으로 패키지를 확장할 수 있습니다. 스크립트 태스크 및 스크립트 구성 요소에서 제공하는 강력한 래퍼 내에 코드를 작성할 수도 있고, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 제공하는 기본 클래스의 파생 클래스를 만들어 사용자 지정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 확장을 처음부터 새로 만들 수도 있습니다.  
  
 이 섹션에서는 두 옵션 중 보다 단순한 옵션인 스크립팅을 사용하여 패키지를 확장하는 방법에 대해 설명합니다.  
  
 스크립트 태스크 및 스크립트 구성 요소를 사용하면 매우 적은 코딩만으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지의 제어 흐름 및 데이터 흐름을 둘 다 확장할 수 있습니다. 두 개체 모두 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] VSTA(Tools for Applications) 개발 환경과 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# 프로그래밍 언어를 사용하며 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 클래스 라이브러리뿐만 아니라 사용자 지정 어셈블리에서 제공하는 모든 기능을 활용할 수 있습니다. 스크립트 태스크와 스크립트 구성 요소를 사용하면 개발자가 사용자 지정 태스크 또는 사용자 지정 데이터 흐름 구성 요소를 개발할 때 일반적으로 필요한 모든 인프라 코드를 작성하지 않고도 사용자 지정 기능을 만들 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [스크립트 태스크와 스크립트 구성 요소 비교](../../integration-services/extending-packages-scripting/comparing-the-script-task-and-the-script-component.md)  
 스크립트 태스크와 스크립트 구성 요소의 유사점 및 차이점에 대해 설명합니다.  
  
 [스크립팅 솔루션과 사용자 지정 개체 비교](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
 스크립팅 솔루션과 사용자 지정 개체 개발 중에서 선택하는 데 사용되는 기준에 대해 설명합니다.  
  
 [스크립팅 솔루션에서 다른 어셈블리 참조](../../integration-services/extending-packages-scripting/referencing-other-assemblies-in-scripting-solutions.md)  
 스크립팅 프로젝트에서 외부 어셈블리와 네임스페이스를 참조 및 사용하는 데 필요한 단계에 대해 설명합니다.  
  
 [스크립트 태스크를 사용하여 패키지 확장](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)  
 스크립트 태스크를 사용하여 사용자 지정 태스크를 만드는 방법에 대해 설명합니다. 태스크는 일반적으로 패키지를 실행할 때마다 한 번씩 호출되거나, 패키지에서 여는 각 데이터 원본에 대해 한 번씩 호출됩니다.  
  
 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
 스크립트 태스크를 사용하여 사용자 지정 데이터 흐름, 변환 및 대상을 만드는 방법에 대해 설명합니다. 데이터 흐름 구성 요소는 일반적으로 처리되는 각 데이터 행에 대해 한 번씩 호출됩니다.  
  
## <a name="reference"></a>참조  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)  
 미리 정의된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열합니다.  
  
## <a name="related-sections"></a>관련 섹션  
 [사용자 지정 개체를 사용한 패키지 확장](../../integration-services/extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 여러 패키지에서 사용할 프로그램 사용자 지정 태스크, 데이터 흐름 구성 요소 및 기타 패키지 개체를 만드는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 빌드](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만들고 구성, 로드, 저장 및 관리하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
