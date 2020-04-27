---
title: TCP/IP를 사용하여 유효한 연결 문자열 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine]
- ports [SQL Server], connecting to
- TCP/IP [SQL Server], connection strings
- connection strings [Database Engine], TCP/IP
- aliases [SQL Server], TCP/IP
ms.assetid: ee5dbc2c-1fc6-42bd-bdf5-efa792557934
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6449b073adb406d15f41cfe02d477a05ad8b0b31
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63065511"
---
# <a name="creating-a-valid-connection-string-using-tcp-ip"></a>TCP/IP를 사용하여 유효한 연결 문자열 만들기
  TCP/IP를 사용하여 유효한 연결 문자열을 만들려면 다음을 수행해야 합니다.  
  
-   **별칭**을 지정합니다.  
  
-   **서버**에 **PING** 유틸리티를 사용하여 연결할 수 있는 서버 이름을 입력하거나 **PING** 유틸리티를 사용하여 연결할 수 있는 IP 주소를 입력합니다. 명명된 인스턴트에 인스턴트 이름을 추가합니다.  
  
-   **프로토콜** 로 **TCP/IP**를 지정합니다.  
  
-   필요에 따라 **포트 번호**에 포트 번호를 입력합니다. 기본값은 1433으로, 서버에 있는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 기본 인스턴스의 포트 번호입니다. 포트 1433에서 수신하지 않는 기본 인스턴스나 명명된 인스턴스에 연결하려면 해당 포트 번호를 제공하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 시작해야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 서비스를 구성하는 방법은 [SQL Server Browser 서비스](../../../2014/tools/configuration-manager/sql-server-browser-service.md)를 참조하세요.  
  
 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 구성 요소는 지정한 별칭에 대한 서버, 프로토콜 및 포트 값을 레지스트리에서 읽어온 후 `tcp:<servername>[\<instancename>],<port>` 또는 `tcp:<IPAddress>[\<instancename>],<port>`형식으로 연결 문자열을 만듭니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 방화벽에서는 포트 1433이 기본적으로 닫힙니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 포트 1433에서 통신하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 TCP/IP를 사용하여 들어오는 클라이언트 연결을 수신하도록 구성된 경우 이 포트를 다시 열어야 합니다. 방화벽 구성에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "방법: SQL Server 액세스를 허용하도록 방화벽 구성"을 참조하거나 해당 방화벽 설명서를 검토하세요.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client는 인터넷 프로토콜 버전 4(IPv4)와 인터넷 프로토콜 버전 6(IPv6)을 둘 다 지원합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자는 IP 주소로 IPv4 및 IPv6 형식을 둘 다 허용합니다. IPv6에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "IPv6을 사용하여 연결"을 참조하십시오.  
  
## <a name="connecting-to-the-local-server"></a>로컬 서버에 연결  
 클라이언트와 동일한 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결할 때는 서버 이름으로 `(local)` 을 사용할 수 있습니다. 이 방법은 모호성을 유발하므로 권장되지 않지만 클라이언트가 어떤 컴퓨터에서 실행될지 알고 있는 경우에는 유용할 수 있습니다. 예를 들어 영업 사원과 같이 네트워크에 연결되지 않은 모바일 사용자를 위해 애플리케이션을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 랩톱 컴퓨터에서 실행되고 프로젝트 데이터를 저장하는 경우 `(local)` 에 연결하는 클라이언트는 항상 랩톱에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결됩니다. `localhost` 라는 단어나 마침표( **.** )를 `(local)`대신 사용할 수 있습니다.  
  
## <a name="verifying-your-connection-protocol"></a>연결 프로토콜 확인  
 다음 쿼리는 현재 연결에 사용된 프로토콜을 반환합니다.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>예  
 서버 이름으로 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 서버 이름으로 명명된 인스턴스에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>\<instancename>  
  
```  
  
 서버 이름으로 지정한 포트에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <port>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 IP 주소로 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 IP 주소로 명명된 인스턴스에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>\<instancename>  
  
```  
  
 IP 주소로 지정한 포트에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <port number>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 `(local)`를 사용하여 로컬 컴퓨터에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             (local)  
  
```  
  
 `localhost`를 사용하여 로컬 컴퓨터에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost  
  
```  
  
 로컬 컴퓨터 `localhost`의 명명된 인스턴스에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost\<instancename>  
  
```  
  
 마침표를 사용하여 로컬 컴퓨터에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .  
  
```  
  
 마침표를 사용하여 로컬 컴퓨터의 명명된 인스턴스에 연결  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .\<instancename>  
  
```  
  
> [!NOTE]  
>  **sqlcmd** 매개 변수로 네트워크 프로토콜을 지정하는 방법은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "방법: sqlcmd.exe를 사용하여 데이터베이스 엔진에 연결"을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [공유 메모리 프로토콜을 사용하여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [명명된 파이프를 사용하여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-named-pipes.md)   
 [네트워크 프로토콜 선택](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  
