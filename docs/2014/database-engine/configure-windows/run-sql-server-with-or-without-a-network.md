---
title: 네트워크 유무에 관계없이 SQL Server 실행 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- verifying Server service has been started
- net start [SQL Server]
- command prompt [SQL Server], connections
- SQL Server services, networks
- status information [SQL Server], Server service
- running SQL Server
- networking [SQL Server], SQL Server with or without
- services [SQL Server], networks
- starting Server service
- SQL Server, running
ms.assetid: 54eac961-5c7a-4481-982d-f93a64b5c2f4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b52c8939aff1bb0d5802e49f22f613ffe641f622
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083453"
---
# <a name="run-sql-server-with-or-without-a-network"></a>네트워크에서 또는 네트워크 없이 SQL Server 실행
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 네트워크에서 또는 네트워크 없이 작동할 수 있습니다.  
  
## <a name="running-sql-server-on-a-network"></a>네트워크에서 SQL Server 실행  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 네트워크에서 통신하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행 중이어야 합니다. 기본적으로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows는 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 자동으로 시작합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스의 시작 여부를 확인하려면 명령 프롬프트에서 다음을 입력합니다.  
  
 **net start**  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 연결된 서비스가 시작되었으면 **net start** 출력 시 다음 서비스가 표시됩니다.  
  
-   Analysis Services (MSSQLSERVER)  
  
-   SQL Server(MSSQLSERVER)  
  
-   SQL Server Agent(MSSQLSERVER)  
  
## <a name="running-sql-server-without-a-network"></a>네트워크 없이 SQL Server 실행  
 네트워크 없이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 인스턴스를 실행하면 기본 제공 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스를 시작하지 않아도 됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], SQL Server 구성 관리자, **net start** 및 **net stop** 명령은 네트워크 없이도 작동하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 시작 및 중지 절차는 네트워크나 독립 실행형 작업의 경우에 동일합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sqlcmd **와 같은 로컬 클라이언트에서 독립 실행형**인스턴스에 연결할 때는 네트워크를 사용하지 않고 로컬 파이프를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 직접 연결합니다. 로컬 파이프와 네트워크 파이프 간의 차이는 네트워크의 사용 여부에 있습니다. 달리 지정하지 않는 한, 표준 파이프( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .\pipe\sql\query)를 사용하여 로컬 파이프와 네트워크 파이프에서\\\\인스턴스에 연결합니다.  
  
 서버 이름을 지정하지 않고 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하면 로컬 파이프를 사용하게 됩니다. 로컬 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결하고 서버 이름을 정확하게 지정하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 구성하여 다중 네트워크를 사용했을 경우 IPX/SPX와 같이 다른 네트워크 IPC 메커니즘이나 네트워크 파이프를 사용하게 됩니다. 독립 실행형 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]은 네트워크 파이프를 지원하지 않으므로 클라이언트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 때는 불필요한 **/***<Server_name>* 인수를 제외해야 합니다. 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] osql **에서 독립 실행형**인스턴스에 연결하려면 다음을 입력합니다.  
  
 **osql /Usa /P** *\<saPassword>*  
  
  
