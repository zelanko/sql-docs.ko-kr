---
title: "Master 저장 프로시저 전송 태스크 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.transfermasterspstask.f1"
helpviewer_keywords: 
  - "Master 저장 프로시저 전송 태스크 [Integration Services]"
ms.assetid: 81702560-48a3-46d1-a469-e41304c7af8e
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Master 저장 프로시저 전송 태스크
  master 저장 프로시저 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 **master** 데이터베이스 간에 하나 이상의 사용자 정의 저장 프로시저를 전송합니다. **master** 데이터베이스에서 저장 프로시저를 전송하려면 프로시저 소유자가 dbo여야 합니다.  
  
 모든 저장 프로시저를 전송하거나 지정된 저장 프로시저만을 전송하도록 Master 저장 프로시저 전송 태스크를 구성할 수 있습니다. 이 태스크는 시스템 저장 프로시저를 복사하지 않습니다.  
  
 전송될 Master 저장 프로시저가 대상에 이미 존재할 수 있습니다. 다음 방식으로 기존의 저장 프로시저를 처리하도록 Master 저장 프로시저 전송 태스크를 구성할 수 있습니다.  
  
-   기존의 저장 프로시저를 덮어씁니다.  
  
-   중복 저장 프로시저가 있는 경우 태스크가 실패합니다.  
  
-   중복 저장 프로시저를 건너뜁니다.  
  
 Master 저장 프로시저 전송 태스크는 런타임에 두 개의 SMO 연결 관리자를 사용해 원본 서버와 대상 서버로 연결합니다. SMO 연결 관리자는 Master 저장 프로시저 전송 태스크와 별도로 구성되며 Master 저장 프로시저 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../../integration-services/connection-manager/smo-connection-manager.md)을 참조하세요.  
  
## SQL Server 인스턴스 간 저장 프로시저 전송  
 Master 저장 프로시저 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 및 대상을 지원합니다.  
  
## 이벤트  
 Master 저장 프로시저 전송 태스크는 전송된 저장 프로시저의 수를 보고하는 정보 이벤트 및 저장 프로시저를 덮어쓰는 경우 경고 이벤트를 발생시킵니다.  
  
 Master 저장 프로시저 전송 태스크는 로그인 전송의 진행 상황은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## 실행 값  
 태스크의 **ExecutionValue** 속성에 정의된 실행 값은 전송된 저장 프로시저의 수를 반환합니다. master 저장 프로시저 전송 태스크의 **ExecValueVariable** 속성에 사용자 정의 변수를 할당하면 패키지 내의 다른 개체에서 저장 프로시저 전송에 대한 정보를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../../integration-services/integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../Topic/Use%20Variables%20in%20Packages.md)을 참조하세요.  
  
## 로그 항목  
 Master 저장 프로시저 전송 태스크는 다음 사용자 지정 로그 항목을 포함합니다.  
  
-   TransferStoredProceduresTaskStartTransferringObjects  이 로그 항목은 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferSStoredProceduresTaskFinishedTransferringObjects  이 로그 항목은 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 또한 **OnInformation** 이벤트 로그 항목은 전송된 저장 프로시저의 수를 보고하며 대상의 저장 프로시저를 덮어쓸 때마다 **OnWarning** 이벤트 로그 항목이 기록됩니다.  
  
## 보안 및 사용 권한  
 사용자는 원본에서 **master** 데이터베이스의 저장 프로시저 목록을 볼 수 있는 권한이 있어야 하며 sysadmin 서버 역할의 멤버이거나 대상 서버의 **master** 데이터베이스에서 저장 프로시저를 만들 수 있는 권한이 있어야 합니다.  
  
## Master 저장 프로시저 전송 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [master 저장 프로시저 전송 태스크 편집기&#40;일반 페이지&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-general-page.md)  
  
-   [master 저장 프로시저 전송 태스크 편집기&#40저장 프로시저 페이지&#41;](../../integration-services/control-flow/transfer-master-stored-procedures-task-editor-stored-procedures-page.md)  
  
-   [식 페이지](../../integration-services/expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferStoredProceduresTask.TransferStoredProceduresTask>  
  
### 태스크 프로그래밍 방식으로 Master 저장 프로시저 전송 구성  
  
## 관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../Topic/Set%20the%20Properties%20of%20a%20Task%20or%20Container.md)  
  
## 관련 항목:  
 [SQL Server 개체 전송 태스크](../../integration-services/control-flow/transfer-sql-server-objects-task.md)   
 [Integration Services 태스크](../../integration-services/control-flow/integration-services-tasks.md)   
 [제어 흐름](../../integration-services/control-flow/control-flow.md)  
  
  