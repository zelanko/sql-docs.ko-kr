---
title: NUMA 노드에 TCP IP 포트 매핑(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- NUMA
- memory [SQL Server], NUMA
- affinity NUMA
- ports [SQL Server], working with NUMA
- CPU [SQL Server], NUMA support
- NUMA, How to map a port to a NUMA node
- NUMA affinity
- TCP/IP [SQL Server], NUMA support
- non-uniform memory access
ms.assetid: 07727642-0266-4cbc-8c55-3c367e4458ca
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 48c645bd85034f226650cf5e98ddd18a6b8efa9e
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "67997980"
---
# <a name="map-tcp-ip-ports-to-numa-nodes-sql-server"></a>NUMA 노드에 TCP IP 포트 매핑(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자를 사용하여 TCP/IP 포트를 NUMA(Non-Uniform Memory Access) 노드로 매핑하는 방법에 대해 설명합니다. 시작할 때 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 오류 로그에 노드 정보를 씁니다.  
  
 사용할 노드의 번호를 확인하려면 오류 로그나 **sys.dm_os_schedulers** 뷰의 노드 정보를 확인하세요. 한 개 또는 여러 개의 노드에 TCP/IP 주소와 포트를 설정하려면 포트 번호 뒤에서 괄호 안에 노드 확인 비트맵(선호도 마스크)을 추가합니다. 십진수나 16진수 형식으로 노드를 지정할 수 있습니다. 비트맵을 만들려면 먼저 76543210처럼 0부터 시작하여 오른쪽에서 왼쪽으로 노드 번호를 매깁니다. 사용할 노드에 1을 지정하고 사용하지 않을 노드에 0을 지정하여 노드 목록의 이진 표현을 만드세요. 예를 들어 NUMA 노드 0, 2, 5를 사용하려면 00100101을 지정합니다.  
  
|||  
|-|-|  
|NUMA 노드 번호|76543210|  
|오른쪽에서부터 0, 2, 5 숫자에 마스크 설정|00100101|  
  
 이진 표현(00100101)을 십진수 `[37]`또는 16진수 `[0x25]`로 변환합니다. 모든 노드에서 수신하려면 노드 식별자를 제공하지 마세요.  
  
 포트가 둘 이상의 NUMA 노드에 매핑되어 있으면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 노드에서 로드 균형을 조정하지 않고 라운드 로빈 방식으로 노드에 연결을 할당합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 각 IP 주소에 대해 여러 TCP 포트에서 수신할 수 있게 하려면 [여러 TCP 포트에서 수신하도록 데이터베이스 엔진 구성](../../database-engine/configure-windows/configure-the-database-engine-to-listen-on-multiple-tcp-ports.md)을 참조하세요.  
  
##  <a name="SSMSProcedure"></a> SQL Server 구성 관리자 사용  
  
#### <a name="to-map-a-tcpip-port-to-a-numa-node"></a>NUMA 노드에 TCP/IP 포트를 매핑하려면  
  
1.  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자에서 **SQL Server 네트워크 구성**을 확장한 다음 ‘\<인스턴스 이름>’**에 대한 프로토콜**을 클릭합니다.   
  
2.  세부 정보 창에서 **TCP/IP**를 두 번 클릭합니다.  
  
3.  **IP 주소** 탭을 선택하여 구성할 IP 주소에 해당하는 섹션의 **TCP 포트** 입력란에서 포트 번호 뒤에 NUMA 노드 식별자를 대괄호 안에 추가합니다. 예를 들어 TCP 포트 1500과 노드 0, 2, 5의 경우 **1500[37]** 또는 **1500[0x25]** 를 사용합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Soft-NUMA&#40;SQL Server&#41;](../../database-engine/configure-windows/soft-numa-sql-server.md)  
  
  
