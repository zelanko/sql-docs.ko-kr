---
title: 로그인 전송 태스크 편집기 (로그인 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.transferloginstask.logins.f1
helpviewer_keywords:
- Transfer Logins Task Editor
ms.assetid: bf244c24-bd45-4ece-b66b-78b488f35c5b
caps.latest.revision: 21
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 794dbafef58e466a2591b396f101e6cdb68364da
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36091314"
---
# <a name="transfer-logins-task-editor-logins-page"></a>로그인 전송 태스크 편집기(로그인 페이지)
  **로그인 전송 태스크 편집기** 대화 상자의 **로그인** 페이지를 사용하여 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 의 한 인스턴스에서 다른 인스턴스로 복사하는 속성을 지정할 수 있습니다. 이 태스크에 대한 자세한 내용은 [Transfer Logins Task](control-flow/transfer-logins-task.md)를 참조하십시오.  
  
> [!IMPORTANT]  
>  로그인 전송 태스크를 실행하면 대상 서버에 임의의 암호로 로그인이 생성되고 해당 암호는 해제됩니다. 이러한 로그인을 사용하려면 **sysadmin** 고정 서버 역할의 멤버가 해당 암호를 변경한 다음 다시 설정해야 합니다. **sa** 로그인은 전송될 수 없습니다.  
  
## <a name="options"></a>변수  
 **SourceConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 원본 서버에 대한 새 연결을 만듭니다.  
  
 **DestinationConnection**  
 목록에서 SMO 연결 관리자를 선택하거나 **\<새 연결...>** 을 클릭하여 대상 서버에 대한 새 연결을 만듭니다.  
  
 **LoginsToTransfer**  
 원본 서버에서 대상 서버로 복사할 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인을 선택합니다. 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**AllLogins**|원본 서버의 모든 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인이 대상 서버로 복사됩니다.|  
|**SelectedLogins**|**LoginsList** 로 지정된 로그인만 대상 서버로 복사됩니다.|  
|**AllLoginsFromSelectedDatabases**|**DatabasesList** 로 지정된 데이터베이스의 모든 로그인이 대상 서버로 복사됩니다.|  
  
 **LoginsList**  
 대상 서버로 복사할 원본 서버의 로그인을 선택합니다. 이 옵션은 **LoginsToTransfer** 에 대해 **SelectedLogins**를 선택한 경우에만 사용할 수 있습니다.  
  
 **DatabasesList**  
 대상 서버로 복사할 로그인을 포함하는 원본 서버의 데이터베이스를 선택합니다. 이 옵션은 **LoginsToTransfer** 에 대해 **AllLoginsFromSelectedDatabases**를 선택한 경우에만 사용할 수 있습니다.  
  
 **IfObjectExists**  
 태스크에서 대상 서버에 이미 있는 로그인과 이름이 동일한 로그인을 처리하는 방법을 선택합니다.  
  
 이 속성의 옵션은 다음 표에 나열되어 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**FailTask**|대상 서버에 이름이 동일한 로그인이 이미 있는 경우 태스크가 실패합니다.|  
|**Overwrite**|대상 서버에 이름이 동일한 로그인이 있는 경우 이를 덮어씁니다.|  
|**Skip**|대상 서버에 이름이 동일한 로그인이 있는 경우 이를 건너뜁니다.|  
  
 **CopySids**  
 로그인에 연결된 보안 식별자를 대상 서버로 복사할지 여부를 선택합니다. 로그인 전송 태스크를 데이터베이스 전송 동작과 함께 사용하는 경우에는**CopySids** 를 **True** 로 설정해야 합니다. 그렇게 하지 않으면 복사된 로그인을 전송된 데이터베이스에서 인식하지 않습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Integration Services 오류 및 메시지 참조](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Integration Services 태스크](control-flow/integration-services-tasks.md)   
 [로그인 전송 태스크 편집기 &#40;일반 페이지&#41;](general-page-of-integration-services-designers-options.md)   
 [식 페이지](expressions/expressions-page.md)   
 [SMO 연결 관리자](connection-manager/smo-connection-manager.md)   
 [강력한 암호](../relational-databases/security/strong-passwords.md)   
 [SQL Server 설치에 대한 보안 고려 사항](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
  