---
title: 로그인 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferloginstask.f1
helpviewer_keywords:
- Transfer Logins task [Integration Services]
ms.assetid: 1df60fd6-c019-405d-8155-c330dbac2cc1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d22dc265eda8e090d00674e198be2616514b857b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48143905"
---
# <a name="transfer-logins-task"></a>로그인 전송 태스크
  로그인 전송 태스크는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스 사이에서 하나 이상의 로그인을 전송합니다.  
  
## <a name="transfer-logins-between-instances-of-sql-server"></a>SQL Server 인스턴스 간 로그인 전송  
 로그인 전송 태스크의 원본 및 대상으로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 사용할 수 있습니다.  
  
## <a name="events"></a>이벤트  
 로그인 전송 태스크는 전송된 로그인 수를 보고하는 정보 이벤트와 로그인을 덮어씀을 알리는 경고 이벤트를 생성합니다.  
  
 태스크는 로그인 전송의 진행률을 보고하지 않으며 0% 및 100 %(완료)만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 태스크의 `ExecutionValue` 속성에 정의된 실행 값은 전송된 로그인 수를 반환합니다. 사용자 정의 변수를 로그인 전송 태스크의 `ExecValueVariable` 속성에 할당하여 로그인 전송에 대한 정보를 패키지에 있는 다른 개체에서 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 로그인 전송 태스크는 다음과 같은 사용자 지정 로그 항목을 포함합니다.  
  
-   TransferLoginsTaskStarTransferringObjects - 이 로그 항목은 전송이 시작되었음을 보고합니다. 로그 항목에 시작 시간이 포함됩니다.  
  
-   TransferLoginsTaskFinishedTransferringObjects - 이 로그 항목은 전송이 완료되었음을 보고합니다. 로그 항목에 종료 시간이 포함됩니다.  
  
 이외에 `OnInformation` 이벤트의 로그 항목은 전송된 로그인 수를 보고하며 `OnWarning` 이벤트의 로그 항목은 덮어쓴 각 대상 로그인에 대해 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 원본 서버에서 로그인을 찾고 대상 서버에서 로그인을 만들려면 사용자는 두 서버 모두에서 sysadmin 서버 역할의 멤버여야 합니다.  
  
## <a name="configuration-of-the-transfer-logins-task"></a>로그인 전송 태스크 구성  
 로그인 전송 태스크를 모든 로그인을 전송하거나, 지정된 로그인만 전송하거나, 지정된 데이터베이스에 액세스할 수 있는 모든 로그인만을 전송하도록 구성할 수 있습니다. sa 로그인은 전송할 수 없습니다. sa 로그인의 이름을 바꿀 수 있지만 이름을 바꾼 sa 로그인도 전송할 수 없습니다.  
  
 또한 이 태스크가 로그인과 연결된 SID(보안 ID)를 복사할지 여부도 지정할 수 있습니다. 로그인 전송 태스크를 데이터베이스 전송 태스크와 연결하여 사용하는 경우 SID를 대상에 복사해야 합니다. 그렇지 않으면 전송된 로그인은 대상 데이터베이스에서 인식되지 않습니다.  
  
 대상으로 전송된 로그인은 비활성화되고 임의의 암호가 할당됩니다. 대상 서버에 있는 sysadmin 역할의 멤버가 암호를 변경하고 로그인을 활성화해야 로그인을 사용할 수 있습니다.  
  
 전송할 로그인이 이미 대상에 있을 수 있습니다. 기존 로그인이 있을 경우 다음과 같이 처리하도록 로그인 전송 태스크를 구성할 수 있습니다.  
  
-   기존 로그인을 덮어씁니다.  
  
-   중복 로그인이 있으면 전송이 실패하도록 합니다.  
  
-   중복 로그인을 건너뜁니다.  
  
 로그인 전송 태스크는 실행 시 하나 또는 두 개의 SMO 연결 관리자를 사용하여 원본과 대상을 연결합니다. SMO 연결 관리자는 로그인 전송 태스크와 별도로 구성된 후 로그인 전송 태스크에서 참조됩니다. SMO 연결 관리자는 액세스할 서버 및 사용할 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [로그인 전송 태스크 편집기 &#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [로그인 전송 태스크 편집기 &#40;로그인 페이지&#41;](../transfer-logins-task-editor-logins-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-logins-task"></a>로그인 전송 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferLoginsTask.TransferLoginsTask>  
  
  
