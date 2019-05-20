---
title: 사용자 지정 개체를 사용한 패키지 확장 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 26616eb8-9e80-434d-b22a-ece1b00f449d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 807cefcb077fd5cf2d11d6ccae9800157395cfc1
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724609"
---
# <a name="extending-packages-with-custom-objects"></a>사용자 지정 개체를 사용한 패키지 확장

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 제공된 구성 요소가 개발자의 요구 사항을 충족시키지 못할 경우 개발자 고유의 확장을 코딩하여 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]의 기능을 확장할 수 있습니다. 두 가지 방법으로 패키지를 확장할 수 있습니다. 스크립트 태스크 및 스크립트 구성 요소에서 제공하는 강력한 래퍼 내에 코드를 작성할 수도 있고, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델에서 제공하는 기본 클래스의 파생 클래스를 만들어 사용자 지정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 확장을 처음부터 새로 만들 수도 있습니다.  
  
 이 섹션에서는 이 둘 중 보다 고급 방법인 사용자 지정 개체를 사용한 패키지 확장 방법에 대해 살펴봅니다.  
  
 사용자 지정 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 솔루션에 스크립트 태스크 및 스크립트 구성 요소가 제공하는 것 이상의 유연성이 필요한 경우 또는 여러 패키지에서 다시 사용할 수 있는 구성 요소가 필요한 경우 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델을 사용하면 관리 코드로 완벽하게 사용자 지정 작업, 데이터 흐름 구성 요소 및 기타 패키지 개체를 작성할 수 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [Integration Services용 사용자 지정 개체 개발](../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]에 대해 만들 수 있는 사용자 지정 개체를 설명하고 필수 단계 및 설정을 요약합니다.  
  
 [사용자 지정 개체 지속](../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 사용자 지정 개체의 기본 지속성과 사용자 지정 지속성의 구현 과정에 대해 설명합니다.  
  
 [사용자 지정 개체 빌드, 배포 및 디버그](../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 다양한 유형의 사용자 지정 개체를 빌드, 배포 및 테스트하는 일반적인 방법에 대해 설명합니다.  
  
 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 사용자 지정 태스크의 코딩 과정에 대해 설명합니다.  
  
 [사용자 지정 연결 관리자 개발](../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 사용자 지정 연결 관리자의 코딩 과정에 대해 설명합니다.  
  
 [사용자 지정 로그 공급자 개발](../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 사용자 지정 로그 공급자의 코딩 과정에 대해 설명합니다.  
  
 [사용자 지정 ForEach 열거자 개발](../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 사용자 지정 열거자의 코딩 과정에 대해 설명합니다.  
  
 [사용자 지정 데이터 흐름 구성 요소 개발](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 사용자 지정 데이터 흐름 원본, 변환 및 대상을 프로그래밍하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 [Integration Services 오류 및 메시지 참조](../../integration-services/integration-services-error-and-message-reference.md)  
 미리 정의된 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열합니다.  
  
## <a name="related-sections"></a>관련 섹션  
 [스크립팅을 사용한 패키지 확장](../../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
 스크립트 태스크를 사용하여 제어 흐름을 확장하는 방법이나 스크립트 구성 요소를 사용하여 데이터 흐름을 확장하는 방법에 대해 설명합니다.  
  
 [프로그래밍 방식으로 패키지 빌드](../../integration-services/building-packages-programmatically/building-packages-programmatically.md)  
 프로그래밍 방식으로 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지를 만들고 구성, 로드, 저장 및 관리하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스크립팅 솔루션과 사용자 지정 개체 비교](../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)   
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  
