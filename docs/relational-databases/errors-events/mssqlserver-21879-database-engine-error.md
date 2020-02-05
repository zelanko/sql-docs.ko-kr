---
title: MSSQLSERVER_21879 | Microsoft 문서
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21879 (Database Engine error)
ms.assetid: fcfab735-05ca-423a-89f1-fdee7e2ed8c0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 7068229bcfcf63bb08fe46272cf308cee60be022
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056713"
---
# <a name="mssqlserver_21879"></a>MSSQLSERVER_21879
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>세부 정보  
  
|||  
|-|-|  
|제품 이름|SQL Server|  
|이벤트 ID|21879|  
|이벤트 원본|MSSQLSERVER|  
|구성 요소|SQLEngine|  
|심볼 이름|SQLErrorNum21879|  
|메시지 텍스트|%d 오류로 인해 원래 게시자 '%s' 및 게시자 데이터베이스 '%s'의 리디렉션된 서버 '%s'을(를) 쿼리하여 원격 서버 이름을 확인할 수 없습니다(오류 메시지 '%s').|  
  
## <a name="explanation"></a>설명  
**sp_validate_redirected_publisher**는 원격 서버의 이름을 검색하기 위해 자체적으로 만든 임시 연결된 서버를 사용하여 리디렉션된 게시자에 연결합니다. 오류 21879는 연결된 서버 쿼리에 실패한 경우에 반환됩니다. 원격 서버 이름 요청을 위한 호출은 일반적으로 임시 연결된 서버를 처음 사용할 때 이루어지므로 연결 문제가 있을 경우 가장 먼저 이 호출에서 연결 문제가 나타날 가능성이 높습니다. 이 원격 호출은 원격 서버에서 **@@servername** 을 선택하여 실행합니다.  
  
리디렉션된 게시자를 쿼리하는 데 사용된 연결된 서버는 원래 게시자에 대해 **sp_adddistpublisher**가 호출될 때 제공된 보안 모드, 로그인 및 암호를 사용합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증(보안 모드 0)이 사용된 경우에는 지정된 로그인 및 암호를 사용하여 원격 서버에 연결합니다.  
  
-   Windows 인증(보안 모드 1)이 사용된 경우에는 트러스트된 연결을 사용하여 연결합니다.  
  
    -   사용자가 **sp_validate_redirected_publisher**를 명시적으로 호출한 경우에는 사용자가 실행되고 있는 Windows 로그인을 사용하여 연결합니다.  
  
    -   **sp_validate_redirected_** publisher를 **sp_get_redirected_publisher**의 복제 에이전트에서 호출한 경우에는 해당 에이전트와 연관된 Windows 로그인이 사용됩니다.  
  
오류 21879는 리디렉션된 대상 게시자에 알려지지 않은 로그인을 사용하여 **sp_validate_redirected_publisher**가 호출되었음을 나타낼 수 있습니다.  
  
## <a name="user-action"></a>사용자 동작  
모든 가용성 그룹 복제본에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인 또는 Windows 인증 로그인이 올바른지 및 인증 로그인이 게시자 데이터베이스에 있는 구독 메타데이터 테이블(syssubscriptions 및 sysmergesubscriptions)에 액세스할 수 있는 권한을 가지고 있는지 확인하십시오.  
  
구독자에서 실행되는 병합 에이전트 같이 배포자와는 다른 노드에서 실행되는 복제 에이전트에서 시작한 **sp_get_redirected_publisher** 호출에서 오류 21879가 반환될 경우 특별히 고려해야 할 사항이 있습니다. Windows 인증을 사용하여 리디렉션된 게시자에 연결하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 Kerberos 인증이 구성되어 있어야만 성공적으로 연결할 수 있습니다. Windows 인증을 사용하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 Kerberos 인증이 구성되어 있지 않을 경우 구독자에서 실행되는 병합 에이전트는 'NT AUTHORITY\ANONYMOUS LOGON' 로그인이 실패했음을 나타내는 오류 18456을 수신합니다. 다음 세 가지 방법으로 이 문제를 해결할 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 Kerberos 인증을 구성합니다. **온라인 설명서의**Kerberos 인증 및 SQL Server[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 참조하세요.  
  
-   **sp_changedistpublisher**를 사용하여 MSdistpublishers에 있는 원래 게시자와 연관된 보안 모드를 변경하고 연결에 사용할 로그인 및 암호를 지정합니다.  
  
-   배포자에서 *sp_get_redirected_publisher*가 호출될 때 유효성 검사를 무시하도록 병합 에이전트 명령줄에서 명령줄 매개 변수 **BypassPublisherValidation**을 지정합니다.  
  
