---
title: 병합 복제에 대한 웹 동기화 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- merge replication synchronization [SQL Server replication]
- Internet [SQL Server replication], synchronization
- synchronization [SQL Server replication], Web Synchronization
- Web publishing [SQL Server replication], synchronization
- Web synchronization, about
- Web synchronization
ms.assetid: 84785aba-b2c1-4821-9e9d-a363c73dcb37
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8cf6a58c50922b412b76576ee2a7fd44cdf9e32a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176704"
---
# <a name="web-synchronization-for-merge-replication"></a>병합 복제에 대한 웹 동기화
  병합 복제에 대한 웹 동기화를 사용하면 HTTPS 프로토콜을 사용하여 데이터를 복제할 수 있으며 다음 시나리오에서도 유용합니다.

-   인터넷을 통해 모바일 사용자로부터 데이터 동기화

-   회사 방화벽을 통해 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 간 데이터 동기화

 예를 들어 출장 중인 영업 담당자가 웹 동기화를 사용할 수 있습니다. [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]라는 회사의 영업 담당자는 전역에 있는 매장과 공급업체로 출장을 갑니다. 장기 출장인 경우 담당자는 호텔에 머무르면서 매일 업무가 끝날 때마다 판매 데이터를 업로드하고 제품 업데이트를 다운로드할 수 있는 편리한 방법이 필요합니다.

 [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] IT 부서에서는 각 휴대용 컴퓨터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 구성하고 웹 동기화를 사용할 수 있도록 병합 복제를 설정했습니다. 각 휴대용 컴퓨터의 병합 에이전트에는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS)를 실행하는 컴퓨터에 설치된 복제 구성 요소를 가리키는 인터넷 URL이 있습니다. 이러한 구성 요소는 구독자와 게시자를 동기화합니다. 각 담당자는 이제 원격 전화 접속 연결을 사용하지 않고도 사용 가능한 임의의 인터넷 연결을 통해 연결을 설정하여 해당 데이터를 업로드 및 다운로드할 수 있습니다. 인터넷 연결은 SSL(Secure Sockets Layer)을 사용하므로 VPN(가상 프라이빗 네트워크)이 필요하지 않습니다.

 웹 동기화에 필요한 구성 요소를 구성하는 방법은 [웹 동기화 구성](configure-web-synchronization.md), [웹 동기화를 위한 IIS 구성](configure-iis-for-web-synchronization.md) 및 [웹 동기화를 위한 IIS 7 구성](configure-iis-7-for-web-synchronization.md)을 참조하세요.

> [!NOTE]
>  웹 동기화는 데이터를 휴대용 컴퓨터, 핸드헬드 디바이스 및 기타 클라이언트와 동기화하기 위해 디자인되었으며 고용량 서버 간 애플리케이션을 위해 디자인되지 않았습니다.

## <a name="overview-of-how-web-synchronization-works"></a>웹 동기화 작동 방식 개요
 웹 동기화를 사용하면 구독자의 업데이트가 패키지되어 IIS를 실행하는 컴퓨터에 HTTPS 프로토콜을 통해 XML 메시지로 전송됩니다. 그러면 IIS를 실행하는 컴퓨터에서 명령을 이진 형식으로 게시자에 보냅니다. 이때 일반적으로 TCP/IP를 사용합니다. 게시자의 업데이트 내용은 IIS를 실행하는 컴퓨터로 전송된 다음 구독자에 배달할 수 있도록 XML 메시지로 패키지됩니다.

 아래 그림에서는 병합 복제에 대한 웹 동기화에 관련된 구성 요소 중 일부를 보여 줍니다.

 ![웹 동기화 구성 요소 및 데이터 흐름](media/web-sync01.gif "웹 동기화 구성 요소 및 데이터 흐름")

 웹 동기화는 끌어오기 구독 전용 옵션이므로 병합 에이전트가 항상 구독자에서 실행됩니다. 이 병합 에이전트는 표준 병합 에이전트, 병합 에이전트 ActiveX 컨트롤 또는 RMO(복제 관리 개체)를 통해 동기화를 제공하는 애플리케이션일 수 있습니다. IIS를 실행 하는 컴퓨터의 위치를 지정 하려면 병합 에이전트에 **-interneturl** 매개 변수를 사용 합니다.

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기(replisapi.dll)는 IIS를 실행하는 컴퓨터에 구성되어 있으며 게시자와 구독자에서 서버로 전송된 메시지를 처리합니다. 토폴로지에 있는 각 노드는 병합 복제 조정자(Replrec.dll)를 사용하여 XML 데이터 스트림을 처리합니다.

 웹 동기화에 참여하는 모든 컴퓨터에[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상이 필요합니다.

### <a name="synchronization-process"></a>동기화 프로세스
 다음은 동기화를 수행하는 동안 발생하는 단계입니다.

1.  구독자에서 병합 에이전트가 시작됩니다. 이 에이전트는 다음을 수행합니다.

    1.  구독 데이터베이스에 대해 SQL 연결을 설정합니다.

    2.  데이터베이스에서 변경 내용을 추출합니다.

    3.  IIS를 실행하는 컴퓨터에 HTTPS 요청을 보냅니다.

    4.  데이터 변경 내용을 XML 메시지로 업로드합니다.

2.  IIS를 실행하는 컴퓨터에 호스팅되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 수신기 및 병합 복제 조정자는 다음을 수행합니다.

    1.  HTTPS 요청에 응답합니다.

    2.  게시 데이터베이스에 대해 SQL 연결을 설정합니다.

    3.  업로드한 변경 내용을 게시 데이터베이스에 적용합니다.

    4.  다운로드한 구독자 변경 내용을 추출합니다.

    5.  병합 에이전트에 HTTPS 응답을 보냅니다.

3.  그러면 구독자의 병합 에이전트가 이 HTTPS 응답을 수락하고 다운로드한 변경 내용을 구독 데이터베이스에 적용합니다.

## <a name="see-also"></a>참고 항목
 웹 [동기화를 위한](topologies-for-web-synchronization.md) [웹 동기화 토폴로지 구성](configure-web-synchronization.md)


