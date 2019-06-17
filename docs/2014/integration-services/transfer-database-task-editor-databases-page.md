---
title: 데이터베이스 전송 태스크 편집기 (데이터베이스 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.transferdatabasetask.database.f1
helpviewer_keywords:
- Transfer Database Task Editor
ms.assetid: ccdb74d0-4bea-420c-a726-2e0eb8957e0a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8d93d2e95f6a18174a6d9b2f05e434a5443701ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66055105"
---
# <a name="transfer-database-task-editor-databases-page"></a>데이터베이스 전송 태스크 편집기(데이터베이스 페이지)
  **데이터베이스 전송 태스크 편집기** 대화 상자의 **데이터베이스** 페이지를 사용하여 데이터베이스 전송 태스크와 관련된 원본 및 대상 데이터베이스의 속성을 지정할 수 있습니다. 데이터베이스 전송 태스크에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스를 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]의 두 인스턴스 간에 복사 또는 이동합니다. 동일한 서버 내에서 데이터베이스를 복사하는 데도 전송 태스크를 사용할 수 있습니다. 이 태스크에 대한 자세한 내용은 [데이터베이스 전송 태스크](control-flow/transfer-database-task.md)를 참조하세요.  
  
## <a name="options"></a>변수  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationDatabaseName**  
 대상 서버에 있는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 데이터베이스의 이름을 지정합니다.  
  
 이 필드를 원본 데이터베이스 이름으로 자동으로 채우려면 먼저 **SourceConnection** 및 **SourceDatabaseName** 을 지정합니다.  
  
 대상 서버에 있는 데이터베이스의 이름을 바꾸려면 이 필드에 새 이름을 입력합니다.  
  
 **DestinationDatabaseFiles**  
 대상 서버에 있는 데이터베이스 파일의 이름 및 위치를 지정합니다.  
  
 이 필드를 원본 데이터베이스 파일 이름 및 위치로 자동으로 채우려면 먼저 **SourceConnection**, **SourceDatabaseName**및 **SourceDatabaseFiles** 를 지정합니다.  
  
 데이터베이스 파일의 이름을 바꾸거나 대상 서버에 새 위치를 지정하려면 이 필드를 원본 데이터베이스 정보로 채운 다음 찾아보기 단추를 클릭합니다. **대상 데이터베이스 파일** 대화 상자에서 **대상 파일**, **대상 폴더**또는 **네트워크 파일 공유**를 편집합니다.  
  
> [!NOTE]  
>  찾아보기 단추를 사용하여 데이터베이스 파일을 찾으면 해당 파일 위치가 로컬 드라이브 표기법을 사용하여 입력됩니다(예: c:\\). 이는 컴퓨터 이름 및 공유 이름과 함께 네트워크 공유 표기법으로 바꾸어야 합니다. 기본 관리 공유를 사용하는 경우 $ 표기법을 사용하고 공유에 대한 관리 액세스가 있어야 합니다.  
  
 **DestinationOverwrite**  
 대상 서버에 있는 데이터베이스를 덮어쓸지 여부를 지정합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**True**|대상 서버 데이터베이스를 덮어씁니다.|  
|**False**|대상 서버 데이터베이스를 덮어쓰지 않습니다.|  
  
> [!CAUTION]  
>  **DestinationOverwrite** 에 대해 **True**를 지정하면 대상 서버 데이터베이스의 데이터를 덮어쓰며 이로 인해 데이터가 손실될 수 있습니다. 이를 방지하려면 데이터베이스 전송 태스크를 실행하기 전에 대상 서버 데이터베이스를 다른 위치에 백업합니다.  
  
 **동작**  
 데이터베이스를 대상 서버로 복사하려면 **Copy** , 이동하려면 **Move** 를 지정합니다.  
  
 **메서드**  
 원본 서버의 데이터베이스가 온라인 모드에 있을 때 태스크를 실행할지, 아니면 오프라인 모드에 있을 때 실행할지를 지정합니다.  
  
 오프라인 모드를 사용하여 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 **sysadmin** 고정 서버 역할의 멤버여야 합니다.  
  
 온라인 모드를 사용하여 데이터베이스를 전송하려면 패키지를 실행하는 사용자가 **sysadmin** 고정 서버 역할의 멤버이거나 선택한 데이터베이스의 데이터베이스 소유자(**dbo**)여야 합니다.  
  
 **SourceDatabaseName**  
 복사 또는 이동할 데이터베이스의 이름을 선택합니다.  
  
 **SourceDatabaseFiles**  
 데이터베이스 파일을 선택하려면 찾아보기 단추를 클릭합니다.  
  
 **ReattachSourceDatabase**  
 오류 발생 시 원본 데이터베이스를 다시 연결할지 여부를 지정합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**True**|원본 데이터베이스를 다시 연결합니다.|  
|**False**|원본 데이터베이스를 다시 연결하지 않습니다.|  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [데이터베이스 전송 태스크 편집기&#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [식 페이지](expressions/expressions-page.md)   
 [SMO 연결 관리자](connection-manager/smo-connection-manager.md)  
  
  
