---
title: 오류 메시지 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transfererrormessagestask.f1
helpviewer_keywords:
- Transfer Error Messages task [Integration Services]
ms.assetid: da702289-035a-4d14-bd74-04461fbfee1b
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b5f1089c48d4a3ebc844bf01644407b138ce265
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48098413"
---
# <a name="transfer-error-messages-task"></a>오류 메시지 전송 태스크
  오류 메시지 전송 태스크에서는 하나 이상의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 사용자 정의 오류 메시지를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 간에 전송합니다. 사용자 정의 메시지는 50000보다 크거나 같은 식별자를 가진 메시지입니다. 50000보다 작은 식별자를 가진 메시지는 시스템 오류 메시지이며 오류 메시지 전송 태스크를 사용하여 전송할 수 없습니다.  
  
 모든 오류 메시지를 전송하거나 지정한 오류 메시지만 전송하도록 오류 메시지 전송 태스크를 구성할 수 있습니다. 사용자 정의 오류 메시지는 여러 다른 언어로 제공될 수 있으며 지정된 언어로만 메시지를 전송하도록 태스크를 구성할 수 있습니다. 다른 언어 버전의 메시지를 대상 서버로 전송하려면 해당 서버에 1033 코드 페이지를 사용하는 us_english 버전의 메시지가 있어야 합니다.  
  
 master 데이터베이스의 sysmessages 테이블에는 시스템 및 사용자 정의 오류 메시지를 포함하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용하는 모든 오류 메시지가 들어 있습니다.  
  
 전송할 사용자 정의 메시지가 이미 대상에 있을 수 있습니다. 식별자 및 언어가 동일한 경우 오류 메시지는 중복 오류 메시지로 정의됩니다. 다음 방식으로 기존 오류 메시지를 처리하도록 오류 메시지 전송 태스크를 구성할 수 있습니다.  
  
-   기존 오류 메시지를 덮어씁니다.  
  
-   중복 메시지가 있는 경우 태스크가 실패합니다.  
  
-   중복 오류 메시지를 건너뜁니다.  
  
 오류 메시지 전송 태스크는 런타임에 한 개 또는 두 개의 SMO 연결 관리자를 사용하여 원본 및 대상 서버에 연결합니다. SMO 연결 관리자는 오류 메시지 전송 태스크와 별도로 구성된 후 오류 메시지 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 서버 액세스 시 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)을 참조하세요.  
  
 오류 메시지 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 원본 및 대상을 지원합니다. 원본 또는 대상으로 사용하는 버전에 대한 제한은 없습니다.  
  
## <a name="events"></a>이벤트  
 이 태스크는 전송된 오류 메시지의 수를 보고하는 정보 이벤트를 발생시킵니다.  
  
 오류 메시지 전송 태스크는 오류 메시지를 전송하는 진행 과정은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 전송된 오류 메시지의 개수는 태스크의 `ExecutionValue` 속성에 정의된 실행 값으로 반환됩니다. 사용자 정의 변수를 할당 하 여는 `ExecValueVariable` 오류 메시지 전송에 대 한 정보 오류 메시지 전송 태스크의 속성 수 다른 개체에 사용할 수 있는 패키지에 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 오류 메시지 전송 태스크에는 다음 사용자 지정 로그 항목이 포함됩니다.  
  
-   TransferErrorMessagesTaskStartTransferringObjects    이 로그 항목에서는 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferErrorMessagesTaskFinishedTransferringObjects   이 로그 항목에서는 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 또한 로그 항목을 `OnInformation` 전송 된 오류 메시지 및 로그 항목의 수를 보고 하는 이벤트를 `OnWarning event` 은 덮어쓴 대상에 각 오류 메시지에 대해 기록 됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 새 오류 메시지를 만들려면 패키지를 실행하는 사용자가 대상 서버의 sysadmin 또는 serveradmin 서버 역할의 멤버여야 합니다.  
  
## <a name="configuration-of-the-transfer-error-messages-task"></a>오류 메시지 전송 태스크 구성  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [오류 메시지 전송 태스크 편집기 &#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [오류 메시지 전송 태스크 편집기 &#40;페이지를 메시지&#41;](../transfer-error-messages-task-editor-messages-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferErrorMessagesTask.TransferErrorMessagesTask>  
  
## <a name="related-tasks"></a>관련 작업  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 태스크](integration-services-tasks.md)   
 [제어 흐름](control-flow.md)  
  
  
