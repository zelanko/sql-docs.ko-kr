---
title: Banyan VINES SPP Sequenced Packet Protocol (), 멀티 프로토콜, AppleTalk 또는 NWLink IPX SPX 네트워크 프로토콜을 사용 하는 연결을 수정 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- network protocols [SQL Server], modifying connections
- SPP [SQL Server]
- NWLink IPX/SPX [SQL Server]
- connections [SQL Server]
- AppleTalk [SQL Server]
- Sequenced Packet Protocol [SQL Server]
- Multiprotocol Net-Library [SQL Server]
- Banyan VINES Sequenced Package Protocol [SQL Server]
- IPX/SPX [SQL Server]
- protocols [SQL Server], modifying connections
- RPC [SQL Server]
ms.assetid: 5c5ae453-cc5b-4898-95c7-ad34157b1f60
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cdbcaa39e3d9630bd4ea50919f31cdbb15a36d14
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66093894"
---
# <a name="modify-connections-that-use-banyan-vines-sequenced-packet-protocol-spp-multiprotocol-appletalk-or-nwlink-ipx-spx-network-protocols"></a>Banyan VINES SPP(Sequenced Packet Protocol), 멀티프로토콜, AppleTalk 또는 NWLink IPX/SPX 네트워크 프로토콜을 사용하는 연결을 수정합니다.
  업그레이드 관리자가 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되지 않는 클라이언트 서버 연결 프로토콜을 검색했습니다. Banyan VINES SPP(Sequenced Packet Protocol), 멀티프로토콜(RPC), AppleTalk 또는 NWLink IPX/SPX 네트워크 프로토콜을 사용하는 클라이언트 응용 프로그램은 지원되는 프로토콜을 사용하여 연결해야 합니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 Banyan VINES SPP(Sequenced Packet Protocol), 멀티프로토콜, AppleTalk 또는 NWLink IPX/SPX 네트워크 프로토콜을 지원하지 않습니다. 이전에 이러한 프로토콜을 사용하여 연결된 클라이언트는 다른 프로토콜을 선택해야 합니다.  
  
## <a name="corrective-action"></a>수정 동작  
 서버에 연결할 때 지원되는 프로토콜을 사용하도록 클라이언트 응용 프로그램을 변경합니다. 지원되지 않는 프로토콜 중 하나를 사용하는 별칭이 설정된 경우 지원되는 프로토콜 중 하나를 사용하도록 해당 별칭을 수정해야 합니다.  
  
 응용 프로그램 연결 문자열 로드 중 프로토콜을 지정 하거나 네트워크에서 = DBMSRPCN RPC, 네트워크에 대 한 = DBMSADSN Appletalk 또는 NETWORK = DBMSVINN Banyan VINES 속성에 대 한 또는 같은 명시적 접두사를 사용 하 여 "spx: *서버 \ 인스턴스*"spx," bv:*서버*"Banyan에 대 한 VINES," adsp:*server*"appletalk를 또는" rpc:*server*" 멀티 프로토콜을 수정 해야 지원 되는 프로토콜 중 하나를 사용 하도록 응용 프로그램입니다.  
  
 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 온라인 설명서에서 "네트워크 프로토콜 선택"을 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 엔진 업그레이드 문제](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 업그레이드 관리자 &#91;새로 만들기&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
