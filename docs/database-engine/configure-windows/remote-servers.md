---
title: 원격 서버 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- server management [SQL Server], remote servers
- remote servers [SQL Server], configuring
- remote servers [SQL Server]
- servers [SQL Server], remote
- remote access option
ms.assetid: abf0fa24-f199-4273-9a1a-e8787ac9bee1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 6a18484c470c3485fca750e1f6986702a9c37ff7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47612462"
---
# <a name="remote-servers"></a>원격 서버
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 이전 버전과의 호환성을 위해서만 원격 서버를 지원합니다. 새 응용 프로그램은 그 대신 연결된 서버를 사용해야 합니다. 자세한 내용은 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)를 참조하세요.  
  
 원격 서버를 구성하면 별도의 연결을 설정하지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스에 연결된 클라이언트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 다른 인스턴스에서 저장 프로시저를 실행할 수 있습니다. 대신 클라이언트가 연결된 서버는 클라이언트 요청을 수락하고 해당 클라이언트를 대신해서 원격 서버에 요청을 전송합니다. 원격 서버는 요청을 처리하고 원래 서버에 결과를 보냅니다. 원래 서버는 클라이언트에 다시 결과를 전송합니다. 원격 서버 구성을 설정할 때는 보안을 설정하는 방법도 고려해야 합니다.  
  
 다른 서버에서 저장 프로시저를 실행하기 위해 서버 구성을 설정할 때 기존의 원격 서버 구성이 없는 경우 원격 서버 대신에 연결된 서버를 사용합니다. 저장 프로시저와 분산 쿼리는 둘 다 연결된 서버에 대해 허용되지만 원격 서버에 대해서는 저장 프로시저만이 허용됩니다.  
  
## <a name="remote-server-details"></a>원격 서버 정보  
 원격 서버는 쌍으로 설정합니다. 한 쌍의 원격 서버를 설정하려면 양쪽 서버가 서로를 원격 서버로 인식하도록 구성해야 합니다.  
  
 대개 원격 서버에 대한 구성 옵션은 설정할 필요가 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Set은 로컬 및 원격 컴퓨터 모두에 기본값을 설정하여 원격 서버 연결을 허용합니다.  
  
 원격 서버에 액세스하려면 **remote access** 구성 옵션을 로컬 컴퓨터와 원격 컴퓨터에서 1로 설정해야 합니다. 이것은 기본 설정입니다.  **원격 액세스** 는 원격 서버로부터의 로그인을 제어합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] **sp_configure** 저장 프로시저 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 이 구성 옵션을 다시 설정할 수 있습니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 옵션을 설정하려면 **서버 속성 연결** 페이지에서 **이 서버에 대한 원격 연결 허용**을 사용합니다. **서버 속성 연결** 페이지에 접근하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭한 다음 **속성**을 클릭합니다. **서버 속성** 페이지에서 **연결** 페이지를 클릭합니다.  
  
 로컬 서버에서 원격 서버 구성을 해제하여 쌍을 이루는 원격 서버의 사용자가 해당 로컬 서버에 액세스하는 것을 차단할 수 있습니다.  
  
## <a name="security-for-remote-servers"></a>원격 서버의 보안  
 원격 서버에 대한 RPC(원격 프로시저 호출)를 설정하려면 해당 원격 서버 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스가 실행되는 로컬 서버에서 로그인 매핑을 설정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 RPC는 기본적으로 해제되어 있습니다. 이 구성은 공격 받을 수 있는 노출 영역을 줄여 서버의 보안을 향상시킵니다. RPC를 사용하기 전에 이 기능을 설정해야 합니다. 자세한 내용은 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)를 참조하세요.  
  
### <a name="setting-up-the-remote-server"></a>원격 서버 설정  
 원격 서버에서 원격 로그인 매핑을 설정해야 합니다. 원격 서버에서는 이 매핑을 사용하여 지정된 서버와의 RPC 연결에 대한 수신 로그인을 로컬 로그인으로 매핑합니다. 원격 로그인 매핑은 원격 서버에서 **sp_addremotelogin** 저장 프로시저를 사용하여 설정할 수 있습니다.  
  
> [!NOTE]  
>  **에서는** sp_remoteoption  **의** trusted [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]옵션이 지원되지 않습니다.  
  
### <a name="setting-up-the-local-server"></a>로컬 서버 설정  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로컬 로그인에 대해서는 로컬 서버에 로그인 매핑을 설정할 필요가 없습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 원격 서버 연결에 로컬 로그인과 암호를 사용합니다. Windows 인증 로그인에 대해서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스가 원격 서버에 RPC 연결을 할 때 사용할 로그인과 암호를 정의하는 로컬 로그인 매핑을 로컬 서버에 설정합니다.  
  
 Windows 인증에서 만든 로그인의 경우 사용자는 **sp_addlinkedservlogin** 저장 프로시저를 사용하여 로그인 이름 및 암호에 대한 매핑을 만들어야 합니다. 이 로그인 이름과 암호는 원격 서버에서 예상하는 **sp_addremotelogin**이 만든 수신 로그인 및 암호와 일치해야 합니다.  
  
> [!NOTE]  
>  가능하면 Windows 인증을 사용하세요.  
  
### <a name="remote-server-security-example"></a>원격 서버 보안 예  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serverSend **및** serverReceive **와 같은**설치를 고려합니다. **serverReceive** 는 **serverSend**로부터의 **Sales_Mary**라는 수신 로그인을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] serverReceive **의**Alice **라는**인증 로그인에 매핑하도록 구성되어 있습니다. **serverSend**로부터의 **Joe**라는 또 다른 수신 로그인은 **serverReceive**** 에서 **Joe**라는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 로그인에 매핑됩니다.  
  
 다음 Transact-SQL 코드 예제는 `serverSend` 에 대해 RPC를 수행하도록 `serverReceive`를 구성합니다.  
  
```  
--Create remote server entry for RPCs   
--from serverSend in serverReceive.  
EXEC sp_addserver 'serverSend';  
GO  
  
--Create remote login mapping for login 'Sales_Mary' from serverSend  
--to Alice.  
EXEC sp_addremotelogin 'serverSend', 'Alice', 'Sales_Mary';  
GO  
--Create remote login mapping for login Joe from serverReceive   
--to same login.  
--Assumes same password for Joe in both servers.  
EXEC sp_addremotelogin 'serverSend', 'Joe', 'Joe';  
GO  
```  
  
 `serverSend`에서 Windows 인증 로그인 `Sales\Mary` 에 대해 로그인 `Sales_Mary`으로의 로컬 로그인 매핑이 만들어집니다. 동일한 로그인 이름과 암호를 사용하는 것이 기본값이고 `Joe`가 `serverReceive` 에 대한 매핑을 가지고 있으므로 `Joe`에게는 로컬 매핑이 필요하지 않습니다.  
  
```  
--Create a remote server entry for RPCs from serverReceive.  
EXEC sp_addserver 'serverReceive';  
GO  
--Create a local login mapping for the Windows authenticated login.  
--Sales\Mary to Sales_Mary. The password should match the  
--password for the login Sales_Mary in serverReceive.  
EXEC sp_addlinkedsrvlogin 'serverReceive', false, 'Sales\Mary',  
   'Sales_Mary', '430[fj%dk';  
GO  
```  
  
## <a name="viewing-local-or-remote-server-properties"></a>로컬 서버 또는 원격 서버 속성 보기  
 **xp_msver** 확장 저장 프로시저를 사용하여 로컬 서버 또는 원격 서버의 특성을 검토할 수 있습니다. 이러한 특성에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전 번호, 컴퓨터의 프로세서 유형과 개수 및 운영 체제 버전이 포함됩니다. 로컬 서버에서는 원격 서버의 데이터베이스, 파일, 로그인 및 도구를 볼 수 있습니다. 자세한 내용은 [xp_msver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/xp-msver-transact-sql.md)을 참조하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 [연결된 서버&#40;데이터베이스 엔진&#41;](../../relational-databases/linked-servers/linked-servers-database-engine.md)  
  
## <a name="related-content"></a>관련 내용  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 [remote access 서버 구성 옵션 구성](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md)  
  
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
  
  
