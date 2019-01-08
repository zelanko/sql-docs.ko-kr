---
title: 프록시 서버 (SQL Server 구성 관리자)를 통해 SQL Server에 연결 | Microsoft Docs
ms.custom: ''
ms.date: 06/22/2017
ms.prod: sql-server-2014
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a621fbe124de096a5735d6e27f2913472cda6fc3
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/30/2018
ms.locfileid: "52639331"
---
# <a name="connect-to-sql-server-through-a-proxy-server-sql-server-configuration-manager"></a>프록시 서버를 통해 SQL Server에 연결(SQL Server 구성 관리자)
  이 항목에서는 SQL Server 구성 관리자를 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 프록시 서버를 통해 SQL Server에 연결하는 방법에 대해 설명합니다. 원격 WinSock(RWS)를 통해 원격으로 수신하려면 수신 노드 주소가 LAT 항목의 범위 밖에 있도록 프록시 서버에 대해 로컬 주소 테이블(LAT)을 정의하십시오.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-enable-connections-to-sql-server-through-microsoft-proxy-server"></a>Microsoft Proxy Server를 통해 SQL Server에 대한 연결을 사용하려면  
  
1.  [특정 TCP 포트로 수신하도록 서버 구성&#40;SQL Server 구성 관리자&#41;](configure-a-server-to-listen-on-a-specific-tcp-port.md)의 단계에 따라 [!INCLUDE[ssDE](../../includes/ssde-md.md)]에서 사용하는 TCP/IP 포트를 확인하거나 원하는 포트를 사용하도록 [!INCLUDE[ssDE](../../includes/ssde-md.md)]를 구성합니다.  
  
2.  사용 중인 프록시 서버에서 수신 노드 주소가 LAT(로컬 주소 테이블) 항목의 범위 밖에 있도록 프록시 서버에 LAT를 정의합니다. 자세한 내용은 프록시 서버 설명서를 참조하십시오.  
  
  
