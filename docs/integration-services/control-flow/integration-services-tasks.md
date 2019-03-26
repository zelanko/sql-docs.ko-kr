---
title: Integration Services 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- scripts [Integration Services], tasks
- files [Integration Services], task options
- workflow tasks [Integration Services]
- Integration Services, tasks
- adding package tasks
- tasks [Integration Services], listed
- SSIS tasks
- SSIS, tasks
- control flow [Integration Services], tasks
- tasks [Integration Services]
- grouping tasks
- tasks [Integration Services], about tasks
- SQL Server Integration Services tasks
- data preparation tasks [Integration Services]
- directory operations [Integration Services]
ms.assetid: 75c8901d-6966-4af3-abe5-10af6dd9313b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 90726ed8ff3b8180e8c65c35d055dcb985001f92
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58276128"
---
# <a name="integration-services-tasks"></a>Integration Services 태스크
  태스크는 패키지 제어 흐름에서 수행되는 작업 단위를 정의하는 제어 흐름 요소입니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지는 두 개 이상의 태스크로 구성되어 있습니다. 패키지에 둘 이상의 태스크가 포함되면 이러한 태스크는 선행 제약 조건에 의해 제어 흐름으로 연결되고 순차화됩니다.  
  
 COM을 지원하는 Visual Basic 등의 프로그래밍 언어와 C#과 같은 .NET 프로그래밍 언어를 사용하여 사용자 지정 태스크를 작성할 수도 있습니다.  
  
  [!INCLUDE[ssIS](../../includes/ssis-md.md)]  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 디자이너는 패키지 제어 흐름을 만들기 위한 디자인 화면과 태스크 구성을 위한 사용자 지정 편집기를 제공합니다.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 개체 모델을 프로그래밍하여 프로그래밍 방식으로 패키지를 만들 수도 있습니다.  
  
## <a name="types-of-tasks"></a>태스크 유형  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 에는 다음 유형의 태스크가 포함되어 있습니다.  
  
 데이터 흐름 태스크  
 데이터 흐름을 실행하여 데이터를 추출하고 열 수준 변환을 적용하며 데이터를 로드하는 태스크입니다.  
  
 데이터 준비 태스크  
 파일 및 디렉터리 복사, 파일 및 데이터 다운로드, 웹 메서드 실행, XML 문서에 작업 적용 및 정리할 데이터 프로파일링 등의 프로세스를 수행하는 태스크입니다.  
  
 워크플로 태스크  
 다른 프로세스와 통신하여 패키지 실행, 프로그램 또는 배치 파일 실행, 패키지 간에 메시지 송수신, 전자 메일 메시지 보내기, WMI(Windows Management Instrumentation) 데이터 읽기, WMI 이벤트 감시 등을 수행하는 태스크입니다.  
  
 SQL Server 태스크  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체 및 데이터를 액세스, 복사, 삽입, 삭제 및 수정하는 태스크입니다.  
  
 스크립팅 태스크  
 스크립트를 사용하여 패키지 기능을 확장하는 태스크입니다.  
  
 Analysis Services 태스크  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체를 만들고 수정, 삭제 및 처리하는 태스크입니다.  
  
 유지 관리 태스크  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 백업 및 축소, 인덱스 다시 작성 및 다시 구성, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 작업 실행 등의 관리 기능을 수행하는 태스크입니다.  
  
 사용자 지정 태스크  
 COM을 지원하는 Visual Basic 등의 프로그래밍 언어와 C#과 같은 .NET 프로그래밍 언어를 사용하여 사용자 지정 태스크를 작성할 수도 있습니다. [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 사용자 지정 태스크에 액세스하려는 경우 해당 태스크의 사용자 인터페이스를 만들어 등록할 수 있습니다. 자세한 내용은 [사용자 지정 태스크 개발](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md)을 참조하세요.  
  
## <a name="configuration-of-tasks"></a>태스크 구성  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 패키지에는 패키지 실행 시 데이터베이스 테이블에서 레코드를 삭제하는 SQL 실행 태스크와 같은 단일 태스크가 포함될 수 있습니다. 그러나 패키지는 일반적으로 여러 개의 태스크를 포함하며 각 태스크는 패키지 제어 흐름의 컨텍스트에서 실행되도록 설정됩니다. 런타임 이벤트에 응답하여 실행되는 작업 흐름인 이벤트 처리기도 태스크를 가질 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하여 패키지에 태스크를 추가하는 방법에 대한 자세한 내용은 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)를 참조하세요.  
  
 프로그래밍 방식으로 패키지에 태스크를 추가하는 방법에 대한 자세한 내용은 [프로그래밍 방식으로 태스크 추가](../../integration-services/building-packages-programmatically/adding-tasks-programmatically.md)를 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 제공하는 각 태스크의 사용자 지정 대화 상자나 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]에 포함된 속성 창을 사용하여 각 태스크를 개별적으로 구성할 수 있습니다. 패키지에는 동일한 유형의 태스크(예: 6개의 SQL 실행 태스크)가 여러 개 포함될 수 있으며 각 태스크는 서로 다르게 구성될 수 있습니다. 자세한 내용은 [태스크 또는 컨테이너의 속성 설정](https://msdn.microsoft.com/library/52d47ca4-fb8c-493d-8b2b-48bb269f859b)을 참조하세요.  
  
## <a name="tasks-connections-and-groups"></a>태스크 연결 및 그룹  
 태스크에 둘 이상의 태스크가 포함되면 이러한 태스크는 선행 제약 조건에 의해 제어 흐름으로 연결되고 순차화됩니다. 자세한 내용은 [Precedence Constraints](../../integration-services/control-flow/precedence-constraints.md)을(를) 참조하세요.  
  
 태스크를 그룹화하여 단일 작업 단위로 수행하거나 루프에서 반복할 수 있습니다. 자세한 내용은 [Foreach Loop Container](../../integration-services/control-flow/foreach-loop-container.md), [For Loop Container](../../integration-services/control-flow/for-loop-container.md)및 [Sequence Container](../../integration-services/control-flow/sequence-container.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [제어 흐름에서 태스크 또는 컨테이너 추가 또는 삭제](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md)  
  
  
