---
title: 사용자 지정 ForEach 열거자 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services]
- custom foreach enumerators [Integration Services], about custom foreach enumerators
- foreach enumerators [Integration Services]
ms.assetid: bffe26e0-1b9a-47ad-bae6-6b708cb4cf4f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 3aedd7aef35555fe11bf67a11254833c52083f9d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297177"
---
# <a name="developing-a-custom-foreach-enumerator"></a>사용자 지정 ForEach 열거자 개발

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 foreach 열거자를 사용하여 컬렉션의 항목을 반복하고 각 요소에 대해 동일한 태스크를 수행합니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에는 폴더의 모든 파일, 데이터베이스의 모든 테이블 또는 패키지 변수에 저장된 목록의 모든 요소와 같이 가장 일반적으로 사용되는 컬렉션을 지원하는 다양한 foreach 열거자가 포함되어 있습니다. 제공된 foreach 열거자 및 컬렉션이 개발자의 요구 사항을 완전하게 충족시키지 못할 경우에는 사용자 지정 foreach 열거자를 만들 수 있습니다.  
  
 사용자 지정 foreach 열거자를 만들려면 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> 기본 클래스에서 상속되는 클래스를 만들고 새 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> 특성을 적용한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> 메서드를 포함하여 기본 클래스의 중요한 메서드와 속성을 재정의해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션에서는 사용자 지정 foreach 열거자와 해당 사용자 지정 사용자 인터페이스를 만들고 구성하고 코딩하는 방법을 설명합니다.  
  
 [사용자 지정 Foreach 열거자 만들기](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/creating-a-custom-foreach-enumerator.md)  
 사용자 지정 foreach 열거자 프로젝트의 클래스를 만드는 방법에 대해 설명합니다.  
  
 [사용자 지정 Foreach 열거자 코딩](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/coding-a-custom-foreach-enumerator.md)  
 기본 클래스의 메서드 및 속성을 재정의하여 사용자 지정 foreach 열거자를 구현하는 방법에 대해 설명합니다.  
  
 [사용자 지정 ForEach 열거자의 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
 사용자 지정 foreach 열거자를 구성하는 데 사용되는 사용자 인터페이스 클래스 및 폼을 구현하는 방법에 대해 설명합니다.  
  
## <a name="related-topics"></a>관련 항목  
  
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
  
 [사용자 지정 데이터 흐름 구성 요소 개발](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 사용자 지정 데이터 흐름 원본, 변환 및 대상을 프로그래밍하는 방법에 대해 설명합니다.  
 
