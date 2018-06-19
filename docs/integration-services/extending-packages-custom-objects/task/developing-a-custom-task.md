---
title: 사용자 지정 태스크 개발 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- custom tasks [Integration Services], about custom tasks
- Task class
- custom tasks [Integration Services]
- SSIS custom tasks
- SSIS custom tasks, about custom tasks
- IDtsTaskUI interface
- DtsTaskAttribute attribute
- tasks [Integration Services], custom
- TaskHost object
ms.assetid: dcbd8615-fa6d-4ddb-b8a5-0b19dddd6239
caps.latest.revision: 67
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a45e0f439c27b5f822df7d017444947761380275
ms.sourcegitcommit: de5e726db2f287bb32b7910831a0c4649ccf3c4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35330117"
---
# <a name="developing-a-custom-task"></a>사용자 지정 태스크 개발
  [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서는 태스크를 사용하여 데이터의 추출, 변환 및 로드를 지원하는 작업 단위를 수행합니다. [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에는 SQL 문 실행부터 FTP 사이트의 파일 다운로드에 이르기까지 가장 자주 사용되는 동작을 수행하는 다양한 태스크가 포함되어 있습니다. 포함된 태스크와 지원되는 동작이 요구 사항을 완전히 충족시키지 못할 경우에는 사용자 지정 태스크를 만들 수 있습니다.  
  
 사용자 지정 태스크를 만들려면 <xref:Microsoft.SqlServer.Dts.Runtime.Task> 기본 클래스에서 상속되는 클래스를 만들고 새 클래스에 <xref:Microsoft.SqlServer.Dts.Runtime.DtsTaskAttribute> 특성을 적용한 다음 <xref:Microsoft.SqlServer.Dts.Runtime.Task.Execute%2A> 메서드를 포함하여 기본 클래스의 중요한 메서드와 속성을 재정의해야 합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 이 섹션에서는 사용자 지정 태스크와 선택 사항인 태스크의 사용자 지정 사용자 인터페이스를 만들고 구성하고 코딩하는 방법을 설명합니다.  
  
 [사용자 지정 태스크 만들기](../../../integration-services/extending-packages-custom-objects/task/creating-a-custom-task.md)  
 사용자 지정 태스크를 만드는 첫 번째 단계를 설명합니다.  
  
 [사용자 지정 태스크 코딩](../../../integration-services/extending-packages-custom-objects/task/coding-a-custom-task.md)  
 사용자 지정 태스크의 주요 메서드를 코딩하는 방법에 대해 설명합니다.  
  
 [사용자 지정 태스크에서 데이터 원본에 연결](../../../integration-services/extending-packages-custom-objects/task/connecting-to-data-sources-in-a-custom-task.md)  
 사용자 지정 태스크를 데이터 원본에 연결하는 방법에 대해 설명합니다.  
  
 [사용자 지정 태스크에서 이벤트 발생 및 정의](../../../integration-services/extending-packages-custom-objects/task/raising-and-defining-events-in-a-custom-task.md)  
 사용자 지정 태스크에서 이벤트를 발생시키고 사용자 지정 이벤트를 정의하는 방법에 대해 설명합니다.  
  
 [사용자 지정 태스크에 디버깅 지원 추가](../../../integration-services/extending-packages-custom-objects/task/adding-support-for-debugging-in-a-custom-task.md)  
 사용자 지정 태스크에 중단점 대상을 만드는 방법에 대해 설명합니다.  
  
 [사용자 지정 태스크의 사용자 인터페이스 개발](../../../integration-services/extending-packages-custom-objects/task/developing-a-user-interface-for-a-custom-task.md)  
 [!INCLUDE[ssIS](../../../includes/ssis-md.md)] 디자이너에 표시되는 사용자 인터페이스를 만들어 사용자 지정 태스크의 속성을 구성하는 방법에 대해 설명합니다.  
  
## <a name="related-sections"></a>관련 섹션  
  
### <a name="information-common-to-all-custom-objects"></a>모든 사용자 지정 개체에 대한 일반적인 정보  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 모든 사용자 지정 개체 유형에 공통적인 내용은 다음 항목을 참조하십시오.  
  
 [Integration Services용 사용자 지정 개체 개발](../../../integration-services/extending-packages-custom-objects/developing-custom-objects-for-integration-services.md)  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]의 모든 종류의 사용자 지정 개체를 구현하는 기본 단계에 대해 설명합니다.  
  
 [사용자 지정 개체 지속](../../../integration-services/extending-packages-custom-objects/persisting-custom-objects.md)  
 사용자 지정 지속성 및 해당 지속성이 필요한 경우에 대해 설명합니다.  
  
 [사용자 지정 개체 빌드, 배포 및 디버그](../../../integration-services/extending-packages-custom-objects/building-deploying-and-debugging-custom-objects.md)  
 사용자 지정 개체를 작성, 서명, 배포 및 디버깅하는 방법에 대해 설명합니다.  
  
### <a name="information-about-other-custom-objects"></a>기타 사용자 지정 개체에 대한 정보  
 [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)]에서 만들 수 있는 기타 사용자 지정 개체 유형에 대한 내용은 다음 항목을 참조하십시오.  
  
 [사용자 지정 연결 관리자 개발](../../../integration-services/extending-packages-custom-objects/connection-manager/developing-a-custom-connection-manager.md)  
 사용자 지정 연결 관리자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 로그 공급자 개발](../../../integration-services/extending-packages-custom-objects/log-provider/developing-a-custom-log-provider.md)  
 사용자 지정 로그 공급자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 ForEach 열거자 개발](../../../integration-services/extending-packages-custom-objects/foreach-enumerator/developing-a-custom-foreach-enumerator.md)  
 사용자 지정 열거자를 프로그래밍하는 방법에 대해 설명합니다.  
  
 [사용자 지정 데이터 흐름 구성 요소 개발](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md)  
 사용자 지정 데이터 흐름 원본, 변환 및 대상을 프로그래밍하는 방법에 대해 설명합니다.  
  
## <a name="see-also"></a>참고 항목  
 [스크립트 태스크를 사용하여 패키지 확장](../../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [스크립팅 솔루션과 사용자 지정 개체 비교](../../../integration-services/extending-packages-scripting/comparing-scripting-solutions-and-custom-objects.md)  
  
  
