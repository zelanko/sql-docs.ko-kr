---
title: 사용자 지정 연결 관리자 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- packages [Integration Services], connections
- custom connection managers [Integration Services], about custom connection managers
- connection managers [Integration Services], custom
- Integration Services packages, connection managers
- SSIS packages, connection managers
- SQL Server Integration Services packages, connection managers
- custom connection managers [Integration Services]
ms.assetid: bda0b29e-57f5-4879-b04d-1396dc56daa8
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 7e8810b9f6aa5b167ff45607821d304af81123c2
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "71287744"
---
# <a name="developing-a-custom-connection-manager"></a>사용자 지정 연결 관리자 개발

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 연결 관리자를 사용하여 외부 데이터 원본에 연결하는 데 필요한 정보를 캡슐화합니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에는 엔터프라이즈 데이터베이스에서 텍스트 파일 및 Excel 워크시트에 이르기까지 가장 일반적으로 사용되는 데이터 원본에 대한 연결을 지원하는 다양한 연결 관리자가 포함되어 있습니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 지원하는 연결 관리자와 외부 데이터 원본이 개발자의 요구 사항을 완전히 충족시키지 못할 경우에는 사용자 지정 연결 관리자를 만들 수 있습니다.  
  
 사용자 지정 연결 관리자를 만들려면 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase> 기본 클래스에서 상속되는 클래스를 만들고 새 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsConnectionAttribute> 특성을 적용한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.ConnectionString%2A> 속성과 <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManagerBase.AcquireConnection%2A> 메서드를 포함하여 기본 클래스의 중요한 메서드와 속성을 재정의해야 합니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에 기본 제공된 대부분의 태스크, 원본 및 대상은 특정 유형의 기본 제공 연결 관리자와만 사용할 수 있습니다. 기본 제공 태스크 및 구성 요소에 사용할 사용자 지정 연결 관리자를 개발하려면 먼저 해당 구성 요소에서 특정 유형의 연결 관리자만 사용할 수 있도록 제한하는지 여부를 확인해야 합니다. 솔루션에 사용자 지정 연결 관리자가 필요한 경우에는 연결 관리자와 함께 사용할 사용자 지정 태스크나 사용자 지정 원본 또는 대상을 개발해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션에서는 사용자 지정 연결 관리자와 선택 사항인 연결 관리자의 사용자 지정 사용자 인터페이스를 만들고 구성하고 코딩하는 방법을 설명합니다. 이 섹션에 표시된 코드 조각은 SQL Server 사용자 지정 연결 관리자 예제에서 가져온 것입니다.  
  
 [사용자 지정 연결 관리자 만들기](../../../integration-services/extending-packages-custom-objects/connection-manager/creating-a-custom-connection-manager.md)  
 사용자 지정 연결 관리자 프로젝트의 클래스를 만드는 방법에 대해 설명합니다.  
  
 [사용자 지정 연결 관리자 코딩](../../../integration-services/extending-packages-custom-objects/connection-manager/coding-a-custom-connection-manager.md)  
 기본 클래스의 메서드 및 속성을 재정의하여 사용자 지정 연결 관리자를 구현하는 방법에 대해 설명합니다.  
  
 [사용자 지정 연결 관리자의 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-user-interface-for-a-custom-connection-manager.md)  
 사용자 지정 연결 관리자를 구성하는 데 사용되는 사용자 인터페이스 클래스 및 폼을 구현하는 방법에 대해 설명합니다.  
  
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
  
 [사용자 지정 로그 공급자 개발](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 사용자 지정 로그 공급자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 ForEach 열거자 개발](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 사용자 지정 열거자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 데이터 흐름 구성 요소 개발](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 사용자 지정 데이터 흐름 원본, 변환 및 대상을 프로그래밍하는 방법에 대해 설명합니다.  
  
