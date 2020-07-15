---
title: SQL Server에 로그인 | Microsoft Docs
description: SQL Server 인스턴스에 로그인하는 다양한 방법을 알아봅니다. 다양한 환경에서 서버 이름에 사용하는 형식에 대해 알아봅니다.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, logging in
- services [SQL Server], logging in
- TCP connection string
- connecting to the Database Engine
- logins [SQL Server], about logging in
- named pipe connection string
- log ins [SQL Server]
- shared memory connection string
- logging in [SQL Server]
- logins [SQL Server]
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ec03d8cd7b6e29bf3241b1646ec7c2e92c41b39a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85789803"
---
# <a name="logging-in-to-sql-server"></a>SQL Server로 로그인
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  그래픽 관리 도구를 사용하거나 명령 프롬프트에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 로그인할 수 있습니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 같은 그래픽 관리 도구를 사용하여 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 인스턴스에 로그인할 때 필요에 따라 서버 이름, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 및 암호를 제공하라는 메시지가 표시됩니다. Windows 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 로그인하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 액세스할 때마다 SQL Server 로그인을 제공할 필요가 없습니다. 대신 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 사용자의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정을 사용하여 자동으로 로그인합니다. 혼합 모드 인증([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 Windows 인증 모드)에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 실행 중인 상태에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 로그인하도록 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인과 암호를 제공해야 합니다. 가능하면 Windows 인증을 사용하세요.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치할 때 대/소문자를 구분하는 데이터 정렬을 선택한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인도 대/소문자를 구분합니다.  
  
## <a name="format-for-specifying-the-name-of-sql-server"></a>SQL Server의 이름을 지정하는 형식  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스의 이름을 지정해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 기본 인스턴스(명명되지 않은 인스턴스)인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 컴퓨터의 이름 또는 컴퓨터의 IP 주소를 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 명명된 인스턴스(예: SQLEXPRESS)인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 설치된 컴퓨터의 이름 또는 컴퓨터의 IP 주소를 지정하고 슬래시와 인스턴스 이름을 추가합니다.  
  
 다음 예에서는 APPHOST라는 컴퓨터에서 실행하는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 명명된 인스턴스를 지정하는 경우 이 예에서는 SQLEXPRESS라는 인스턴스 이름을 사용합니다.  
  
 **예:**  
  
|인스턴스 유형|서버 이름 항목|  
|----------------------|-------------------------------|  
|기본 프로토콜을 사용하여 기본 인스턴스에 연결합니다.|APPHOST|  
|기본 프로토콜을 사용하여 명명된 인스턴스에 연결합니다. |APPHOST\SQLEXPRESS|  
|인스턴스가 로컬 컴퓨터에서 실행하고 있음을 표시하기 위해 마침표를 사용하여 동일한 컴퓨터의 기본 인스턴스에 연결합니다.|.|  
|인스턴스가 로컬 컴퓨터에서 실행하고 있음을 표시하기 위해 마침표를 사용하여 동일한 컴퓨터의 명명된 인스턴스에 연결합니다.|.\SQLEXPRESS|  
|인스턴스가 로컬 컴퓨터에서 실행하고 있음을 표시하기 위해 localhost를 사용하여 동일한 컴퓨터의 기본 인스턴스에 연결합니다.|localhost|  
|인스턴스가 로컬 컴퓨터에서 실행하고 있음을 표시하기 위해 localhost를 사용하여 동일한 컴퓨터의 명명된 인스턴스에 연결합니다.|localhost\SQLEXPRESS|  
|인스턴스가 로컬 컴퓨터에서 실행하고 있음을 표시하기 위해 (local)을 사용하여 동일한 컴퓨터의 기본 인스턴스에 연결합니다.|(local)|  
|인스턴스가 로컬 컴퓨터에서 실행하고 있음을 표시하기 위해 (local)을 사용하여 동일한 컴퓨터의 명명된 인스턴스에 연결합니다.|(local)\SQLEXPRESS|  
|공유 메모리 연결을 강제 적용하여 동일한 컴퓨터의 기본 인스턴스에 연결합니다.|lpc:APPHOST|  
|공유 메모리 연결을 강제 적용하여 동일한 컴퓨터의 명명된 인스턴스에 연결합니다.|lpc:APPHOST\SQLEXPRESS|  
|IP 주소를 사용하여 TCP 주소 192.168.17.28에서 수신 대기하는 기본 인스턴스에 연결합니다.|192.168.17.28|  
|IP 주소를 사용하여 TCP 주소 192.168.17.28에서 수신 대기하는 명명된 인스턴스에 연결합니다.|192.168.17.28\SQLEXPRESS|  
|사용 중인 포트(이 경우 2828)를 지정하여 기본 TCP 포트에서 수신 대기하지 않는 기본 인스턴스에 연결합니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)]가 기본 포트(1433)에서 수신 대기하는 경우 포트 번호를 지정하는 작업은 필요하지 않습니다.|APPHOST,2828|  
|지정된 TCP 포트(이 경우 2828)에서 명명된 인스턴스에 연결합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스가 호스트 컴퓨터에서 실행되지 않는 경우 대개 포트 번호를 지정하는 작업은 필요합니다.|APPHOST,2828|  
|IP 주소와 사용 중인 포트(이 경우 2828)를 지정하여 기본 TCP 포트에서 수신 대기하지 않는 기본 인스턴스에 연결합니다.|192.168.17.28,2828|  
|IP 주소와 사용 중인 포트(이 경우 2828)를 지정하여 명명된 인스턴스에 연결합니다.|192.168.17.28\SQLEXPRESS,2828|  
|TCP 연결을 강제 적용하여 이름별로 기본 인스턴스에 연결합니다.|tcp:APPHOST|  
|TCP 연결을 강제 적용하여 이름별로 명명된 인스턴스에 연결합니다.|tcp:APPHOST\SQLEXPRESS|  
|명명된 파이프 연결을 지정하여 기본 인스턴스에 연결합니다.|\\\APPHOST\pipe\SQL\query|  
|명명된 파이프 연결을 지정하여 기본 인스턴스에 연결합니다.|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|명명된 파이프 연결을 강제 적용하여 이름별로 기본 인스턴스에 연결합니다.|np:APPHOST|  
|명명된 파이프 연결을 강제 적용하여 이름별로 명명된 인스턴스에 연결합니다.|np:APPHOST\SQLEXPRESS|  
  
## <a name="verifying-your-connection-protocol"></a>연결 프로토콜 확인  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에 연결된 경우 다음 쿼리는 인증 방법(NTLM 또는 Kerberos)과 함께 현재 연결에 사용되는 프로토콜을 반환하며 연결이 암호화되는지 여부를 표시합니다.  
  
```sql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## <a name="related-tasks"></a>관련 작업  
 [SQL Server 인스턴스에 로그인&#40;명령 프롬프트&#41;](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 다음 리소스는 연결 문제를 해결하는 데 도움이 될 수 있습니다.  
  
-   [SQL Server 데이터베이스 엔진에 대한 연결 문제를 해결하는 방법](https://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [SQL 연결 문제를 해결하는 단계](https://docs.microsoft.com/archive/blogs/sql_protocols/steps-to-troubleshoot-sql-connectivity-issues)  
  
## <a name="related-content"></a>관련 내용  
 [인증 모드 선택](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [sqlcmd 유틸리티 사용](../../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
 [로그인 만들기](../../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
