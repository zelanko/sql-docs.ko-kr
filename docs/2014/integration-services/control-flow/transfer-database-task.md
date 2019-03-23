---
title: 데이터베이스 전송 태스크 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.f1
helpviewer_keywords:
- Transfer Database task [Integration Services]
ms.assetid: b9a2e460-cdbc-458f-8df8-06b8b2de3d67
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f7ddf838269932c19b0614d5a5219a7f03daed17
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58377036"
---
# <a name="transfer-database-task"></a>데이터베이스 전송 태스크
  데이터베이스 전송 태스크는 두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 간에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스를 전송합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 복사하여 전송하는 다른 태스크와 달리 데이터베이스 전송 태스크는 데이터베이스를 복사 또는 이동할 수 있습니다. 동일한 서버 내에서 데이터베이스를 복사하는 데도 전송 태스크를 사용할 수 있습니다.  
  
## <a name="offline-and-online-modes"></a>오프라인 및 온라인 모드  
 온라인 또는 오프라인 모드에서 데이터베이스를 전송할 수 있습니다. 온라인 모드를 사용하는 경우 데이터베이스는 연결된 상태를 유지하며 데이터베이스 개체를 복사하는 SMO(SQL Management Object)를 통해 전송됩니다. 오프라인 모드를 사용하는 경우 데이터베이스가 분리된 상태로 데이터베이스 파일을 복사 또는 이동하며 성공적으로 전송을 완료한 다음 대상에 데이터베이스를 연결합니다. 데이터베이스를 복사하면 복사가 완료될 때 자동으로 원본에 다시 연결됩니다. 오프라인 모드에서는 좀 더 빠르게 데이터베이스를 복사할 수 있지만 전송하는 동안 데이터베이스를 사용할 수 없습니다.  
  
 오프라인 모드를 사용하려면 데이터베이스 파일을 가진 대상 서버 및 원본 서버에 네트워크 파일 공유를 지정해야 합니다. 폴더를 공유하여 사용자가 액세스할 수 있는 경우 \\\computername\Program Files\myfolder\\구문을 사용하여 네트워크 공유를 참조할 수 있습니다. 그렇지 않으면 \\\computername\c$\Program Files\myfolder\\구문을 사용해야 합니다. 두 번째 구문을 사용하려면 원본 및 대상 네트워크 공유에 대한 쓰기 액세스가 필요합니다.  
  
## <a name="transfer-of-databases-between-versions-of-sql-server"></a>SQL Server 버전 간 데이터베이스 전송  
 데이터베이스 전송 태스크는 여러 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전의 인스턴스 간에 데이터베이스를 전송할 수 있습니다.  
  
## <a name="events"></a>이벤트  
 데이터베이스 전송 태스크는 오류 메시지 전송의 진행 상황은 보고하지 않으며 0% 및 100% 완료만 보고합니다.  
  
## <a name="execution-value"></a>실행 값  
 다른 전송 태스크와 달리 데이터베이스 전송 태스크는 한 개의 데이터베이스만 전송할 수 있으므로 태스크의 `ExecutionValue` 속성에 정의된 실행 값은 1을 반환합니다.  
  
 데이터베이스 전송 태스크의 `ExecValueVariable` 속성에 사용자 정의 변수를 할당하면 패키지 내의 다른 개체에서 오류 메시지 전송에 대한 정보를 사용할 수 있습니다. 자세한 내용은 [Integration Services&#40;SSIS&#41; 변수](../integration-services-ssis-variables.md) 및 [패키지에서 변수 사용](../use-variables-in-packages.md)을 참조하세요.  
  
## <a name="log-entries"></a>로그 항목  
 데이터베이스 전송 태스크는 다음 사용자 지정 로그 항목을 포함합니다.  
  
-   SourceSQLServer    이 로그 항목은 원본 서버의 이름을 나열합니다.  
  
-   DestSQLServer    이 로그 항목은 대상 서버의 이름을 나열합니다.  
  
-   SourceDB    이 로그 항목은 전송된 데이터베이스의 이름을 나열합니다.  
  
 또한 대상 데이터베이스를 덮어쓰는 경우 `OnInformation` 이벤트에 대한 로그 항목이 기록됩니다.  
  
## <a name="security-and-permissions"></a>보안 및 사용 권한  
 오프라인 모드를 사용해 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 sysadmin 서버 역할의 멤버여야 합니다.  
  
 온라인 모드를 사용해 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 sysadmin 서버 역할의 멤버이거나 선택한 데이터베이스의 데이터베이스 소유자(dbo)여야 합니다.  
  
## <a name="configuration-of-the-transfer-database-task"></a>데이터베이스 전송 태스크 구성  
 데이터베이스 전송이 실패하는 경우 태스크가 원본 데이터베이스에 다시 연결할지 여부를 지정할 수 있습니다.  
  
 동일한 이름의 대상 데이터베이스를 덮어쓰고 대상 데이터베이스를 대체할 수 있도록 데이터베이스 전송 태스크를 구성할 수 있습니다.  
  
 전송 과정의 일부로 원본 데이터베이스의 이름을 바꿀 수 있습니다. 대상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 이미 같은 이름의 데이터베이스가 있는 경우 원본 데이터베이스의 이름을 변경하여 데이터베이스를 전송할 수 있습니다. 그러나 같은 이름의 데이터베이스 파일이 대상에 있는 경우에는 태스크가 실패하므로 데이터베이스 파일의 이름은 반드시 달라야 합니다.  
  
 데이터베이스를 복사할 경우 데이터베이스는 대상 서버에 있는 **model** 데이터베이스의 크기보다 작을 수 없습니다. 복사할 데이터베이스의 크기를 늘리거나 **model**의 크기를 줄일 수 있습니다.  
  
 데이터베이스 전송 태스크는 런타임에 한 개 또는 두 개의 SMO 연결 관리자를 사용해 원본 서버 및 대상 서버에 연결합니다. 동일한 서버에 데이터베이스 복사본을 만드는 경우 하나의 SMO 연결 관리자만 필요합니다. SMO 연결 관리자는 데이터베이스 전송 태스크와 별도로 구성된 후 데이터베이스 전송 태스크에서 참조됩니다. SMO 연결 관리자는 태스크가 서버에 액세스할 때 사용할 서버 및 인증 모드를 지정합니다. 자세한 내용은 [SMO Connection Manager](../connection-manager/smo-connection-manager.md)을 참조하세요.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너를 사용하거나 프로그래밍 방식으로 속성을 설정할 수 있습니다.  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 설정할 수 있는 속성에 대한 자세한 내용을 보려면 다음 항목 중 하나를 클릭하십시오.  
  
-   [데이터베이스 전송 태스크 편집기&#40;일반 페이지&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [데이터베이스 전송 태스크 편집기&#40;데이터베이스 페이지&#41;](../transfer-database-task-editor-databases-page.md)  
  
-   [식 페이지](../expressions/expressions-page.md)  
  
 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 디자이너에서 이러한 속성을 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   [태스크 또는 컨테이너의 속성 설정](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-transfer-database-task"></a>데이터베이스 전송 태스크의 프로그래밍 방식 구성  
 이러한 속성을 프로그래밍 방식으로 설정하는 방법을 보려면 다음 항목을 클릭하십시오.  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.TransferDatabaseTask.TransferDatabaseTask>  
  
  
