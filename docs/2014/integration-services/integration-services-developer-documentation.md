---
title: 개발자&#39;가이드 (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Integration Services, programming
- SSIS, programming
- SQL Server Integration Services, programming
- packages [Integration Services], programming
ms.assetid: 60fe148b-a7c4-4289-ae3e-2e949fc1886c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3fc7c93f8e499fb063e0d01c9132606f3ddfa3f7
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384461"
---
# <a name="developer39s-guide-integration-services"></a>개발자&#39;가이드 (Integration Services)
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에는 완전히 다시 작성된 개체 모델이 포함되어 있으며 이러한 개체 모델은 패키지 확장 및 프로그래밍을 보다 쉽고 유연하고 강력하게 해 주는 다양한 기능을 갖도록 향상되었습니다. 개발자는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지의 거의 모든 측면을 확장하고 프로그래밍할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개발자가 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로그래밍에 사용할 수 있는 기본적인 방법은 다음 두 가지가 있습니다.  
  
-   패키지에 사용자 지정 기능을 제공하기 위해 [!INCLUDE[ssIS](../includes/ssis-md.md)] 디자이너 내에서 사용할 수 있게 되는 구성 요소를 작성하여 패키지를 확장할 수 있습니다.  
  
-   개발자 고유의 응용 프로그램에서 프로그래밍 방식으로 패키지를 만들고 구성하고 실행할 수 있습니다.  
  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 기본 제공 구성 요소가 개발자의 요구 사항을 충족시키지 못할 경우 개발자 고유의 확장을 코딩하여 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]의 기능을 확장할 수 있습니다. 이 경우 다음 중 하나를 선택할 수 있습니다.  
  
-   단일 패키지에서 임시로 사용하려는 경우 스크립트 태스크에 코드를 작성하여 사용자 지정 태스크를 만들거나, 스크립트 구성 요소에 코드를 작성하여 사용자 지정 데이터 흐름 구성 요소를 만들 수 있습니다. 스크립트 구성 요소는 원본, 변환 또는 대상으로 구성할 수 있습니다. 이러한 강력한 래퍼는 인프라 코드를 자동으로 작성하므로 개발자가 사용자 지정 기능을 개발하는 데만 집중할 수 있게 해 주지만 다른 항목에서 쉽게 재사용할 수는 없습니다.  
  
-   여러 패키지에서 사용하려는 경우 연결 관리자, 태스크, 열거자, 로그 공급자 및 데이터 흐름 구성 요소와 같은 사용자 지정 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 확장을 만들 수 있습니다. 관리되는 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개체 모델에는 사용자 지정 확장을 개발하기 위한 시작 지점을 제공하며 이 작업을 이전보다 쉽게 해 주는 기본 클래스가 포함되어 있습니다.  
  
 패키지를 동적으로 만들거나 개발 환경 외부에서 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 관리 및 실행하려는 경우 패키지를 프로그래밍 방식으로 조작할 수 있습니다. 기존 패키지를 로드한 다음 수정하여 실행할 수도 있고 프로그래밍 방식으로 완전히 새로운 패키지를 만들어 실행할 수도 있습니다. 이 경우 다음 중 하나를 선택할 수 있습니다.  
  
-   기존 패키지를 로드하고 수정하지 않은 채로 실행합니다.  
  
-   기존 패키지를 로드하고 다시 구성(예를 들어 다른 데이터 원본을 지정)한 다음 실행합니다.  
  
-   새 패키지를 만들고, 개체별 및 속성별로 변경 작업을 수행하여 구성 요소를 추가 및 구성하고, 새 패키지를 저장한 다음 실행합니다.  
  
 이 섹션에서는 이러한 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 프로그래밍 방법에 대해 설명하고 예를 보여 줍니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Integration Services 프로그래밍 개요](integration-services-programming-overview.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 개발 과정에서 제어 흐름과 데이터 흐름이 하는 역할을 설명합니다.  
  
 [동기 및 비동기 변환 이해](understanding-synchronous-and-asynchronous-transformations.md)  
 동기 출력과 비동기 출력 간의 중요한 차이를 설명하고 데이터 흐름에서 이러한 출력을 사용하는 구성 요소에 대해 설명합니다.  
  
 [프로그래밍 방식으로 연결 관리자 사용](working-with-connection-managers-programmatically.md)  
 관리 코드에서 사용할 수 있는 연결 관리자 및 코드에서 `AcquireConnection` 메서드를 호출할 때 연결 관리자에서 반환하는 값을 나열합니다.  
  
 [스크립팅을 사용한 패키지 확장](extending-packages-scripting/extending-packages-with-scripting.md)  
 스크립트 태스크를 사용하여 제어 흐름을 확장하는 방법이나 스크립트 구성 요소를 사용하여 데이터 흐름을 확장하는 방법에 대해 설명합니다.  
  
 [사용자 지정 개체를 사용한 패키지 확장](extending-packages-custom-objects/extending-packages-with-custom-objects.md)  
 여러 패키지에서 사용할 사용자 지정 태스크, 데이터 흐름 구성 요소 및 기타 패키지 개체를 만들고 프로그래밍하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 빌드](building-packages-programmatically/building-packages-programmatically.md)  
 프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 만들고 구성 및 저장하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 실행 및 관리](run-manage-packages-programmatically/running-and-managing-packages-programmatically.md)  
 프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 패키지를 열거, 실행 및 관리하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 [Integration Services 오류 및 메시지 참조](integration-services-error-and-message-reference.md)  
 미리 정의된 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열합니다.  
  
## <a name="related-sections"></a>관련 섹션  
 [패키지 배포 문제 해결 도구](troubleshooting/troubleshooting-tools-for-package-development.md)  
 [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]에서 개발 과정의 패키지 문제 해결을 위해 제공하는 기능 및 도구에 대해 설명합니다.  
  
## <a name="external-resources"></a>외부 리소스  
  
-   www.codeplex.com/MSFTISProdSamples의 CodePlex 예제 - [Integration Services 제품 예제](https://go.microsoft.com/fwlink/?LinkID=131204)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server Integration Services](sql-server-integration-services.md)  
  
  
