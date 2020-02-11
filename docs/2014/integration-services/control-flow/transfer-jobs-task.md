---
title: 작업 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferjobstask.f1
helpviewer_keywords:
- Transfer Jobs task [Integration Services]
ms.assetid: 1bf33885-9c5b-47e4-a549-f5920b66a1de
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 03913242246fcdaf11e9272e827cd8e06951a108
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62829899"
---
# <a name="transfer-jobs-task"></a>작업 전송 태스크
  작업 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 사이에서 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 작업을 전송합니다.  
  
 작업 전송 태스크는 모든 작업 또는 지정된 작업만 전송하도록 구성할 수 있습니다. 또한 전송된 작업을 대상에서 활성화할지 여부를 나타낼 수 있습니다.  
  
 전송할 작업이 대상에 이미 있을 수 있습니다. 기존 태스크가 있을 경우 처리할 수 있는 방식은 다음과 같습니다.  
  
-   기존 작업을 덮어씁니다.  
  
-   중복 작업이 있으면 전송이 실패하도록 합니다.  
  
-   중복 작업을 건너뜁니다.  
  
 작업 전송 태스크는 실행 시 하나 또는 두 개의 SMO 연결 관리자를 사용하여 원본과 대상을 연결합니다. SMO 연결 관리자는 작업 전송 태스크와 별도로 구성된 후 작업 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 서버 액세스 시 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)을 참조하세요.  
  
## <a name="transferring-jobs-between-instances-of-sql-server"></a>SQL Server 인스턴스 간 작업 전송  
 작업 전송 태스크의 원본 및 대상으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용할 수 있습니다. 원본 또는 대상으로 사용하는 버전에 대한 제한은 없습니다.  
  
## <a name="events"></a>이벤트  
 작업 전송 태스크는 전송된 작업 수를 보고하는 정보 이벤트와 작업을 덮어씀을 알리는 경고 이벤트를 생성합니다. 태스크는 작업 전송의 진행률을 보고하지 않으며 0% 및 100%(완료)만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 태스크의 `ExecutionValue` 속성에 정의된 실행 값은 전송된 작업 수를 반환합니다. 사용자 정의 변수를 작업 전송 태스크의 `ExecValueVariable` 속성에 할당하여 작업 전송에 대한 정보를 패키지에 있는 다른 개체에서 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 작업 전송 태스크는 다음과 같은 사용자 지정 로그 항목을 포함합니다.  
  
-   TransferJobsTaskStarTransferringObjects - 이 로그 항목은 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferJobsTaskFinishedTransferringObjects - 이 로그 항목은 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 이외에 `OnInformation` 이벤트의 로그 항목은 전송된 작업 수를 보고하며 `OnWarning` 이벤트의 로그 항목은 덮어쓴 각 대상 작업에 대해 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 작업을 전송하려면 사용자는 sysadmin 고정 서버 역할의 멤버이거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 원본 및 대상 인스턴스 모두에 있는 msdb 데이터베이스의 고정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에이전트 고정 데이터베이스 역할의 멤버여야 합니다.  
  
## <a name="configuration-of-the-transfer-jobs-task"></a>작업 전송 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 
  [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [작업 전송 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [작업 전송 태스크 편집기 &#40;작업 페이지&#41;](../transfer-jobs-task-editor-jobs-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법은 다음 항목을 참조하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferJobsTask.TransferJobsTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>참고 항목  
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
