---
title: 프록시 서버를 통해 SQL Server에 연결(SQL Server 구성 관리자) | Microsoft Docs
description: SQL Server 구성 관리자를 사용하여 프록시 서버를 통해 SQL Server에 연결하는 방법을 알아봅니다. 원격 WinSock(RWS)을 사용하여 원격으로 수신 대기하는 방법을 확인합니다.
ms.custom: ''
ms.date: 12/15/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Remote WinSock
- RWS
- LATs
- proxy servers [SQL Server]
- connections [SQL Server], proxy server
- Microsoft Proxy Server [SQL Server]
- local address tables [SQL Server]
ms.assetid: 39714de0-2a1f-4179-9091-5c3fa4612545
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0b8e6c54a7f496f06067bb0393f83899f8df4253
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670279"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>프록시 서버를 통해 SQL Server에 연결(SQL Server 구성 관리자)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 프록시 서버를 통해 SQL Server에 연결하는 방법에 대해 설명합니다. 원격 WinSock(RWS)를 통해 원격으로 수신하려면 수신 노드 주소가 LAT 항목의 범위 밖에 있도록 프록시 서버에 대해 로컬 주소 테이블(LAT)을 정의하십시오.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Microsoft Proxy Server를 통해 SQL Server에 대한 연결을 사용하려면  
  
1.  [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)의 단계에 따라 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용하는 TCP/IP 포트를 확인하거나 원하는 포트를 사용하도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 구성합니다.  
  
2.  사용 중인 프록시 서버에서 수신 노드 주소가 LAT(로컬 주소 테이블) 항목의 범위 밖에 있도록 프록시 서버에 LAT를 정의합니다. 자세한 내용은 프록시 서버 설명서를 참조하십시오.  
  
> [!NOTE]
>  이 항목은 온-프레미스 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]에 적용됩니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]와 관련된 연결 문제의 경우 [Azure SQL Database에 대한 연결 문제 해결](/azure/sql-database/sql-database-troubleshoot-common-connection-issues)을 참조하세요.