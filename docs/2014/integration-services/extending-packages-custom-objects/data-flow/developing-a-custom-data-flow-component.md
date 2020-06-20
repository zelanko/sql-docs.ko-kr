---
title: 사용자 지정 데이터 흐름 구성 요소 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- data flow task [Integration Services], extending
- data flow [Integration Services], extending
- extending data flow task [Integration Services]
- components [Integration Services], data flow
ms.assetid: be126913-2a9a-41c9-9bf5-a7b0a0aea2f8
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2e1a6af8407813a2a712b0c43c0b06097477f00f
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966521"
---
# <a name="developing-a-custom-data-flow-component"></a>사용자 지정 데이터 흐름 구성 요소 개발
  데이터 흐름 태스크는 다양한 데이터 원본에 연결한 다음 해당 데이터를 빠른 속도로 변환하고 라우팅하는 여러 구성 요소로 구성됩니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 개발자가 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]와 배포된 패키지에서 사용할 수 있는 사용자 지정 원본, 변환 및 대상을 만들 수 있게 해주는 확장 가능한 개체 모델을 제공합니다. 이 섹션에는 사용자 지정 데이터 흐름 구성 요소의 개발 과정을 설명하는 항목이 포함되어 있습니다.

## <a name="in-this-section"></a>섹션 내용
 [사용자 지정 데이터 흐름 구성 요소 만들기](creating-a-custom-data-flow-component.md) 사용자 지정 데이터 흐름 구성 요소를 만드는 초기 단계에 대해 설명 합니다.

 [데이터 흐름 구성 요소의 디자인 타임 메서드](design-time-methods-of-a-data-flow-component.md) 사용자 지정 데이터 흐름 구성 요소에서 구현할 디자인 타임 메서드를 설명 합니다.

 [데이터 흐름 구성 요소의 런타임 메서드](run-time-methods-of-a-data-flow-component.md) 사용자 지정 데이터 흐름 구성 요소에서 구현 하는 런타임 메서드에 대해 설명 합니다.

 [실행 계획 및 버퍼 할당](execution-plan-and-buffer-allocation.md) 데이터 흐름 실행 계획 및 데이터 버퍼 할당에 대해 설명 합니다.

 [데이터 흐름의 데이터 형식 작업](working-with-data-types-in-the-data-flow.md) 데이터 흐름이 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 데이터 형식을 .NET Framework 관리 되는 데이터 형식에 매핑하는 방법을 설명 합니다.

 [데이터 흐름 구성 요소의 유효성 검사](validating-a-data-flow-component.md) 구성 요소 구성을 확인 하 고 구성 요소 메타 데이터를 다시 구성 하는 데 사용 되는 메서드를 설명 합니다

 [외부 메타 데이터 구현](implementing-external-metadata.md) 외부 메타 데이터 열을 사용 하 여 데이터 유효성 검사를 수행 하는 방법을 설명 합니다.

 [데이터 흐름 구성 요소에서 이벤트 발생 및 정의](raising-and-defining-events-in-a-data-flow-component.md) 미리 정의 된 이벤트 및 사용자 지정 이벤트를 발생 시키는 방법에 대해 설명 합니다.

 [데이터 흐름 구성 요소에서 로그 항목 로깅 및 정의](logging-and-defining-log-entries-in-a-data-flow-component.md) 사용자 지정 로그 항목을 만들고 작성 하는 방법에 대해 설명 합니다.

 [데이터 흐름 구성 요소에서 오류 출력 사용](using-error-outputs-in-a-data-flow-component.md) 오류 행을 대체 출력으로 리디렉션하는 방법에 대해 설명 합니다.

 [데이터 흐름 구성 요소의 버전 업그레이드](upgrading-the-version-of-a-data-flow-component.md) 구성 요소의 새 버전을 처음 사용할 때 저장 된 구성 요소 메타 데이터를 업데이트 하는 방법을 설명 합니다.

 [데이터 흐름 구성 요소에 대 한 사용자 인터페이스 개발](developing-a-user-interface-for-a-data-flow-component.md) 구성 요소에 대 한 사용자 지정 편집기를 구현 하는 방법을 설명 합니다.

 [특정 유형의 데이터 흐름 구성 요소 개발](../../extending-packages-custom-objects-data-flow-types/developing-specific-types-of-data-flow-components.md) 세 가지 유형의 데이터 흐름 구성 요소인 원본, 변환 및 대상을 개발 하는 방법에 대 한 정보를 포함 합니다.

## <a name="reference"></a>참조
 <xref:Microsoft.SqlServer.Dts.Pipeline>사용자 지정 데이터 흐름 구성 요소를 만드는 데 사용 되는 클래스 및 인터페이스를 포함 합니다.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper>데이터 흐름 태스크 개체 모델을 구성 하 고 사용자 지정 데이터 흐름 구성 요소를 만들거나 데이터 흐름 태스크를 작성 하는 데 사용 되는 클래스 및 인터페이스를 포함 합니다.

 <xref:Microsoft.SqlServer.Dts.Pipeline.Design>데이터 흐름 구성 요소에 대 한 사용자 인터페이스를 만드는 데 사용 되는 클래스 및 인터페이스를 포함 합니다.

 [Integration Services 오류 및 메시지 참조](../../integration-services-error-and-message-reference.md) 미리 정의 된 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 오류 코드와 해당 심볼 이름 및 설명을 나열 합니다.

## <a name="related-sections"></a>관련 단원

### <a name="information-common-to-all-custom-objects"></a>모든 사용자 지정 개체에 대한 일반적인 정보
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 모든 사용자 지정 개체 유형에 공통적인 내용은 다음 항목을 참조하십시오.

 [Integration Services에 대 한 사용자 지정 개체 개발](../../extending-packages-custom-objects/developing-custom-objects-for-integration-services.md) 에 대 한 모든 형식의 사용자 지정 개체를 구현 하는 기본 단계를 설명 합니다 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .

 [사용자 지정 개체 유지](../../extending-packages-custom-objects/persisting-custom-objects.md) 사용자 지정 지 속성에 대해 설명 하 고 필요한 경우에 대해 설명 합니다.

 [사용자 지정 개체 빌드, 배포 및 디버깅](../../extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md) 사용자 지정 개체를 빌드, 서명, 배포 및 디버깅 하는 기술에 대해 설명 합니다.

### <a name="information-about-other-custom-objects"></a>기타 사용자 지정 개체에 대한 정보
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 기타 사용자 지정 개체 유형에 대한 내용은 다음 항목을 참조하십시오.

 [사용자 지정 작업 개발](../../extending-packages-custom-objects/task/developing-a-custom-task.md) 사용자 지정 태스크를 프로그래밍 하는 방법을 설명 합니다.

 [사용자 지정 연결 관리자 개발](../../extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md) 사용자 지정 연결 관리자를 프로그래밍 하는 방법을 설명 합니다.

 [사용자 지정 로그 공급자 개발](../../extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md) 사용자 지정 로그 공급자를 프로그래밍 하는 방법을 설명 합니다.

 [사용자 지정 ForEach 열거자 개발](../../extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md) 사용자 지정 열거자를 프로그래밍 하는 방법을 설명 합니다.

![Integration Services 아이콘 (작은 아이콘)](../../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지를 방문하세요.](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하세요.

## <a name="see-also"></a>참고 항목
 [스크립트 구성 요소를 사용 하 여 데이터 흐름 확장] (.. /.. /extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md [스크립팅 솔루션과 사용자 지정 개체 비교](../../extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)


