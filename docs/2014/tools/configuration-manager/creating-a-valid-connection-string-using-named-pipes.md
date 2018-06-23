---
title: 명명 된 파이프를 사용 하 여 유효한 연결 문자열 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 264c615e38baf39676f1310d6465bfaac2a92785
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36088749"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>명명된 파이프를 사용하여 유효한 연결 문자열 만들기
  사용자가 변경 하지 않은 경우의 기본 인스턴스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명명된 된 파이프 프로토콜에서 수신 대기를 사용 하 여 `\\.\pipe\sql\query` 파이프 이름으로 합니다. 마침표는 컴퓨터가 로컬 컴퓨터임을 나타내고 `pipe` 는 연결이 명명된 파이프임을 나타내며 `sql\query` 는 파이프의 이름입니다. 기본 파이프에 연결하려면 별칭의 파이프 이름으로 `\\<computer_name>\pipe\sql\query` 를 지정해야 합니다. 다른 파이프에서 수신하도록 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 구성한 경우 파이프 이름으로 해당 파이프를 사용해야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 `\\.\pipe\unit\app`를 파이프로 사용하는 경우 별칭의 파이프 이름은 `\\<computer_name>\pipe\unit\app`여야 합니다.  
  
 올바른 파이프 이름을 만들려면 다음을 수행해야 합니다.  
  
-   **별칭**을 지정합니다.  
  
-   **명명된 파이프** 를 **프로토콜**로 선택합니다.  
  
-   **파이프 이름**을 입력합니다. 둘 수 있습니다 **파이프 이름** 빈 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 지정 하면 구성 관리자는 적절 한 파이프 이름을 완성 합니다는 **프로토콜** 및 **서버**  
  
-   **서버**를 지정합니다. 명명된 인스턴스의 경우 서버 이름과 인스턴스 이름을 제공할 수 있습니다.  
  
 연결의 시간에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 구성 요소 읽는 서버, 프로토콜 및 파이프 이름 값는 지정한 별칭에 대 한 레지스트리에서 형식에서으로 파이프 이름을 만듭니다 `np:\\<computer_name>\pipe\<pipename>` 또는 `np:\\<IPAddress>\pipe\<pipename>`합니다. 명명 된 인스턴스의 경우 기본 파이프 이름은 `\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query`합니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 방화벽이 기본적으로 포트 445를 닫습니다. 때문에 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 통신 포트 445 통해 포트 경우 열어야 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 명명 된 파이프를 사용 하 여 들어오는 클라이언트 연결을 수신 하도록 구성 됩니다. 방화벽 구성에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서의 "방법: SQL Server 액세스를 허용하도록 방화벽 구성"을 참조하거나 해당 방화벽 설명서를 검토하세요.  
  
## <a name="connecting-to-the-local-server"></a>로컬 서버에 연결  
 클라이언트와 동일한 컴퓨터에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결할 때는 서버 이름으로 `(local)`을 사용할 수 있습니다. `(local)` 을 사용하면 모호해질 수 있으므로 권장되지는 않지만 클라이언트가 어떤 컴퓨터에서 실행될지 알고 있는 경우에는 유용할 수 있습니다. 예를 들어 영업 사원과 같이 네트워크에 연결되지 않은 모바일 사용자를 위해 응용 프로그램을 만들 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 랩톱 컴퓨터에서 실행되고 프로젝트 데이터를 저장하는 경우 (local)에 연결하는 클라이언트는 항상 랩톱에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결됩니다. `localhost`라는 단어나 마침표(.)를 `(local)` 대신 사용할 수 있습니다.  
  
## <a name="verifying-your-connection-protocol"></a>연결 프로토콜 확인  
 다음 쿼리는 현재 연결에 사용된 프로토콜을 반환합니다.  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>예  
 서버 이름으로 기본 파이프에 연결  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 IP 주소로 기본 파이프에 연결  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 서버 이름으로 기본이 아닌 파이프에 연결  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 서버 이름으로 명명된 인스턴스에 연결  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 `localhost`를 사용하여 로컬 컴퓨터에 연결  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 마침표를 사용하여 로컬 컴퓨터에 연결  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  변수로 네트워크 프로토콜을 지정 하는 **sqlcmd** 매개 변수를 참조 하십시오 "하는 방법: 사용 하 여 데이터베이스 엔진 sqlcmd.exe에 연결"에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서.  
  
## <a name="see-also"></a>관련 항목  
 [공유 메모리 프로토콜을 사용 하 여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [TCP/IP를 사용하여 유효한 연결 문자열 만들기](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [네트워크 프로토콜 선택](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  