---
title: MSSQLSERVER_916 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 916 (Database Engine error)
ms.assetid: 73eb6581-99fe-49a5-9b42-e239d7ffe27f
caps.latest.revision: 8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 856f2801cb5e1de811773e24997d5550ac1df56b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver916"></a>MSSQLSERVER_916
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|916|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|NOTUSER|  
|메시지 텍스트|현재 보안 컨텍스트로는 서버 보안 주체 "%.*ls"이(가) 데이터베이스 "%.\*ls"에 액세스할 수 없습니다.|  
  
## <a name="explanation"></a>설명  
해당 로그인에는 명명된 데이터베이스에 연결할 수 있는 권한이 없습니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 수 있지만 데이터베이스의 특정 권한이 없는 로그인은 게스트 사용자 권한을 받습니다. 이는 한 데이터베이스의 사용자가 사용 권한이 없는 다른 데이터베이스에 연결하지 못하도록 방지하는 보안 수단입니다. 게스트 사용자에게 명명된 데이터베이스에 대한 CONNECT 권한이 없고 trustworthy 속성이 설정되지 않은 경우 이 오류 메시지가 발생할 수 있습니다. 게스트 사용자에게 명명된 데이터베이스에 대한 CONNECT 권한이 없으면 이 오류 메시지가 발생할 수 있습니다.  
  
msdb 데이터베이스에 대한 CONNECT 권한이 거부되거나 취소되면 개체 탐색기에서 각 데이터베이스의 정책 기반 관리 상태를 표시하려고 할 때 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 이러한 오류를 받을 수 있습니다. 개체 탐색기가 현재 로그인의 권한을 사용하여 msdb 데이터베이스에서 해당 정보를 쿼리하면 오류가 발생합니다. 다음과 같은 오류 메시지도 나타납니다.  
  
이 요청에 대한 데이터를 검색하지 못했습니다. (Microsoft.SqlServer.Management.Sdk.Sfc)  
  
## <a name="user-action"></a>사용자 동작  
  
> [!WARNING]  
> 이 보안 수단을 무시하기 전에 사용자가 다양한 데이터베이스에서 인증된다는 것을 분명히 이해해야 합니다. 다음 방법을 사용하면 한 데이터베이스의 사용 권한을 가진 사용자가 다른 데이터베이스에 연결할 수 있어 악의적 사용자에게 데이터가 노출될 수 있습니다. 포함된 데이터베이스를 사용하도록 설정하면 다음 단계에서는 한 데이터베이스의 데이터베이스 소유자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 다른 데이터베이스에 대한 액세스 권한을 부여하도록 허용할 수 있습니다.  
  
다음 방법 중 하나로 데이터베이스에 연결할 수 있습니다.  
  
-   명명된 데이터베이스에 대한 특정 로그인 액세스 권한을 부여합니다. 다음 예에서는 `Adventure-Works\Larry` 데이터베이스에 대한 로그인 `msdb` 액세스 권한을 부여합니다.  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO [Adventure-Works\Larry] ;  
  
-   게스트 사용자에 대해 오류 메시지에 명명된 데이터베이스에 대한 CONNECT 권한을 부여합니다. 다음 예에서는 사용자 `CONNECT`에 대해 `msdb` 데이터베이스에 대한 `guest` 권한을 부여합니다.  
  
    USE msdb ;  
  
    GO  
  
    GRANT CONNECT TO guest ;  
  
-   사용자를 인증한 데이터베이스에 TRUSTWORTHY 속성을 사용하도록 설정합니다.  
  
    `ALTER DATABASE AdventureWorks SET TRUSTWORTHY ON;`  
  
