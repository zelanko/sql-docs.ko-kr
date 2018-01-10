---
title: "사용자 지정 데이터 흐름 구성 요소 개발 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: extending-packages-custom-objects
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
caps.latest.revision: "57"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 60c5b673e22aabcd0ed3f6064e1a5d8c94a73f97
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="developing-a-custom-data-flow-component"></a>사용자 지정 데이터 흐름 구성 요소 개발
  데이터 흐름 태스크는 다양한 데이터 원본에 연결한 다음 해당 데이터를 빠른 속도로 변환하고 라우팅하는 여러 구성 요소로 구성됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 개발자가 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]와 배포된 패키지에서 사용할 수 있는 사용자 지정 원본, 변환 및 대상을 만들 수 있게 해주는 확장 가능한 개체 모델을 제공합니다. 이 섹션에는 사용자 지정 데이터 흐름 구성 요소의 개발 과정을 설명하는 항목이 포함되어 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 [사용자 지정 데이터 흐름 구성 요소 만들기](../../../integration-services/extending-packages-custom-objects/data-flow/creating-a-custom-data-flow-component.md)  
 사용자 지정 데이터 흐름 구성 요소를 만드는 초기 단계에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소의 디자인 타임 메서드](../../../integration-services/extending-packages-custom-objects/data-flow/design-time-methods-of-a-data-flow-component.md)  
 사용자 지정 데이터 흐름 구성 요소를 구현하는 디자인 타임 메서드에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소의 런타임 메서드](../../../integration-services/extending-packages-custom-objects/data-flow/run-time-methods-of-a-data-flow-component.md)  
 사용자 지정 데이터 흐름 구성 요소를 구현하는 런타임 메서드에 대해 설명합니다.  
  
 [실행 계획 및 버퍼 할당](../../../integration-services/extending-packages-custom-objects/data-flow/execution-plan-and-buffer-allocation.md)  
 데이터 흐름 실행 계획과 데이터 버퍼의 할당에 대해 설명합니다.  
  
 [데이터 흐름의 데이터 형식 작업](../../../integration-services/extending-packages-custom-objects/data-flow/working-with-data-types-in-the-data-flow.md)  
 데이터 흐름에서 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 .NET Framework의 관리되는 데이터 형식에 매핑하는 방식에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소의 유효성 검사](../../../integration-services/extending-packages-custom-objects/data-flow/validating-a-data-flow-component.md)  
 구성 요소의 구성 유효성을 검사하고 구성 요소 메타데이터를 다시 구성하는 데 사용하는 메서드에 대해 설명합니다.  
  
 [외부 메타데이터 구현](../../../integration-services/extending-packages-custom-objects/data-flow/implementing-external-metadata.md)  
 데이터 유효성 검사에 외부 메타데이터 열을 사용하는 방법에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소에서 이벤트 발생 및 정의](../../../integration-services/extending-packages-custom-objects/data-flow/raising-and-defining-events-in-a-data-flow-component.md)  
 미리 정의된 사용자 지정 이벤트를 발생시키는 방법에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소에서 로그 항목 로깅 및 정의](../../../integration-services/extending-packages-custom-objects/data-flow/logging-and-defining-log-entries-in-a-data-flow-component.md)  
 사용자 지정 로그 항목을 만들고 기록하는 방법에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소에서 오류 출력 사용](../../../integration-services/extending-packages-custom-objects/data-flow/using-error-outputs-in-a-data-flow-component.md)  
 오류 행을 대체 출력으로 리디렉션하는 방법에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소의 버전 업그레이드](../../../integration-services/extending-packages-custom-objects/data-flow/upgrading-the-version-of-a-data-flow-component.md)  
 새 버전의 구성 요소가 처음 사용될 때 저장된 구성 요소 메타데이터를 업데이트하는 방법에 대해 설명합니다.  
  
 [데이터 흐름 구성 요소의 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-user-interface-for-a-data-flow-component.md)  
 구성 요소의 사용자 지정 편집기를 구현하는 방법에 대해 설명합니다.  
  
 [특정 유형의 데이터 흐름 구성 요소 개발](../../../integration-services/extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md)  
 세 가지 유형의 데이터 흐름 구성 요소인 원본, 변환 및 대상을 개발하는 방법에 대해 설명합니다.  
  
## <a name="reference"></a>참조  
 <xref:Microsoft.SqlServer.Dts.Pipeline>  
 사용자 지정 데이터 흐름 구성 요소를 만드는 데 사용되는 클래스와 인터페이스에 대해 설명합니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>  
 데이터 흐름 태스크 개체 모델을 구성하며 사용자 지정 데이터 흐름 구성 요소를 만들거나 데이터 흐름 태스크를 빌드하는 데 사용되는 클래스와 인터페이스가 들어 있습니다.  
  
 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>  
 데이터 흐름 구성 요소의 사용자 인터페이스를 만드는 데 사용되는 클래스와 인터페이스가 들어 있습니다.  
  
 [Integration Services 오류 및 메시지 참조](../../../integration-services/integration-services-error-and-message-reference.md)  
 미리 정의된 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열합니다.  
  
## <a name="related-sections"></a>관련 섹션  
  
### <a name="information-common-to-all-custom-objects"></a>모든 사용자 지정 개체에 대한 일반적인 정보  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 모든 사용자 지정 개체 유형에 공통적인 내용은 다음 항목을 참조하십시오.  
  
 [Integration Services용 사용자 지정 개체 개발](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]의 모든 사용자 지정 개체 유형을 구현하는 기본 단계에 대해 설명합니다.  
  
 [사용자 지정 개체 지속](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 사용자 지정 지속성 및 해당 지속성이 필요한 경우에 대해 설명합니다.  
  
 [사용자 지정 개체 빌드, 배포 및 디버그](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 사용자 지정 개체를 작성, 서명, 배포 및 디버깅하는 방법에 대해 설명합니다.  
  
### <a name="information-about-other-custom-objects"></a>기타 사용자 지정 개체에 대한 정보  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 기타 사용자 지정 개체 유형에 대한 내용은 다음 항목을 참조하십시오.  
  
 [사용자 지정 태스크 개발](../../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)  
 사용자 지정 태스크를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 연결 관리자 개발](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 사용자 지정 연결 관리자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 로그 공급자 개발](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 사용자 지정 로그 공급자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 ForEach 열거자 개발](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 사용자 지정 열거자를 프로그래밍하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 구성 요소를 사용하여 데이터 흐름 확장](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
 [스크립팅 솔루션과 사용자 지정 개체 비교](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
