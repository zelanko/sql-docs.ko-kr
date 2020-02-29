---
title: 사용자 지정 로그 공급자 개발 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- SSIS packages, log providers
- custom log providers [Integration Services]
- SQL Server Integration Services packages, log providers
- log providers [Integration Services]
- packages [Integration Services], logs
- Integration Services packages, log providers
ms.assetid: 3f715b95-7074-4f5c-8ae2-246998052e78
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af3478e254f01f7cf53d5a09b6febab3b1e85e8b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78176306"
---
# <a name="developing-a-custom-log-provider"></a>사용자 지정 로그 공급자 개발
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에는 패키지 실행 중 발생하는 이벤트를 캡처할 수 있게 해 주는 광범위한 로깅 기능이 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에는 XML, 텍스트, 데이터베이스, Windows 이벤트 로그 등의 형식으로 로그를 만들고 저장하는 데 사용할 수 있는 다양한 로그 공급자가 포함되어 있습니다. 제공된 로그 공급자 및 출력 형식이 개발자의 요구 사항을 완전하게 충족시키지 못할 경우 사용자 지정 로그 공급자를 만들 수 있습니다.

 사용자 지정 로그 공급자를 만들려면 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase> 기본 클래스에서 상속되는 클래스를 만들고 새 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsLogProviderAttribute> 특성을 적용한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.ConfigString%2A> 속성 및 <xref:Microsoft.SqlServer.Dts.Runtime.LogProviderBase.Log%2A> 메서드를 포함하여 기본 클래스의 중요한 메서드와 속성을 재정의해야 합니다.

## <a name="in-this-section"></a>섹션 내용
 이 섹션에서는 사용자 지정 로그 공급자를 만들고 구성하고 코딩하는 방법에 대해 설명합니다.

 [사용자 지정 로그 공급자 만들기](creating-a-custom-log-provider.md) 사용자 지정 로그 공급자 프로젝트에 대 한 클래스를 만드는 방법을 설명 합니다.

 [사용자 지정 로그 공급자 코딩](coding-a-custom-log-provider.md) 기본 클래스의 메서드 및 속성을 재정의 하 여 사용자 지정 로그 공급자를 구현 하는 방법을 설명 합니다.

 [사용자 지정 로그 공급자의 사용자 인터페이스 개발](developing-a-user-interface-for-a-custom-log-provider.md) 사용자 지정 로그 공급자에 대 한 사용자 지정 사용자 인터페이스 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]는에서 지원 되지 않습니다.

## <a name="related-topics"></a>관련 항목

### <a name="information-common-to-all-custom-objects"></a>모든 사용자 지정 개체에 대한 일반적인 정보
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 모든 사용자 지정 개체 유형에 공통적인 내용은 다음 항목을 참조하십시오.

 [Integration Services에 대 한 사용자 지정 개체 개발](../developing-custom-objects-for-integration-services.md) 에 대 한 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]모든 형식의 사용자 지정 개체를 구현 하는 기본 단계를 설명 합니다.

 [사용자 지정 개체 유지](../persisting-custom-objects.md) 사용자 지정 지 속성에 대해 설명 하 고 필요한 경우에 대해 설명 합니다.

 [사용자 지정 개체 빌드, 배포 및 디버깅](../building-deploying-and-debugging-custom-objects.md) 사용자 지정 개체를 빌드, 서명, 배포 및 디버깅 하는 기술에 대해 설명 합니다.

### <a name="information-about-other-custom-objects"></a>기타 사용자 지정 개체에 대한 정보
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 기타 사용자 지정 개체 유형에 대한 내용은 다음 항목을 참조하십시오.

 [사용자 지정 작업 개발](../task/developing-a-custom-task.md) 사용자 지정 태스크를 프로그래밍 하는 방법을 설명 합니다.

 [사용자 지정 연결 관리자 개발](../connection-manager/developing-a-custom-connection-manager.md) 사용자 지정 연결 관리자를 프로그래밍 하는 방법을 설명 합니다.

 [사용자 지정 ForEach 열거자 개발](../foreach-enumerator/developing-a-custom-foreach-enumerator.md) 사용자 지정 열거자를 프로그래밍 하는 방법을 설명 합니다.

 [사용자 지정 데이터 흐름 구성 요소 개발](../data-flow/developing-a-custom-data-flow-component.md) 사용자 지정 데이터 흐름 원본, 변환 및 대상을 프로그래밍 하는 방법에 대해 설명 합니다.

![Integration Services 아이콘 (작은 아이콘)](../../media/dts-16.gif "Integration Services 아이콘(작은 아이콘)")  **은 최신 상태로 유지 Integration Services**<br /> Microsoft의 최신 다운로드, 문서, 예제 및 비디오와 커뮤니티에서 선택된 솔루션을 보려면 MSDN의 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] 페이지를 방문하세요.<br /><br /> [MSDN의 Integration Services 페이지 방문](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> 이러한 업데이트에 대한 자동 알림을 받으려면 해당 페이지에서 제공하는 RSS 피드를 구독하십시오.


