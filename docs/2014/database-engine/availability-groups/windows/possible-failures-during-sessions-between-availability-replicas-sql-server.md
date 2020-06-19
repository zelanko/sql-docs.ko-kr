---
title: 가용성 복제본 간의 세션 동안 발생 가능한 오류(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting [SQL Server, HADR]
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], troubleshooting
ms.assetid: cd613898-82d9-482f-a255-0230a6c7d6fe
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4cfacb7f7c75875d4f5d0b0b435d282b3f537cc7
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936654"
---
# <a name="possible-failures-during-sessions-between-availability-replicas-sql-server"></a>가용성 복제본 간의 세션 동안 발생 가능한 오류(SQL Server)
  물리적 문제, 운영 체제 문제 또는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 문제로 인해 두 가용성 복제본 사이의 세션에서 오류가 발생할 수 있습니다. 가용성 복제본은 Sqlservr.exe에서 사용하는 구성 요소를 정기적으로 검사하여 구성 요소가 올바르게 작동하는지 아니면 실패했는지 확인하지 않습니다. 하지만 일부 오류 유형의 경우 영향을 받는 구성 요소가 Sqlservr.exe에 오류를 보고합니다. 다른 구성 요소에서 보고된 오류를 *하드 오류*라고 합니다. 확인되지 않는 다른 오류를 감지하기 위해 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 자체적으로 세션 제한 시간 메커니즘을 구현합니다. 세션 제한 시간(초)을 지정합니다. 이 제한 시간은 서버 인스턴스가 다른 인스턴스로부터 PING 메시지를 받기까지 기다리는 최대 시간으로, 이 시간이 경과하면 해당 인스턴스의 연결이 끊어진 것으로 간주됩니다. 두 가용성 복제본 사이에서 세션 제한 시간이 발생하면 가용성 복제본은 오류가 발생했다고 가정하고 *소프트 오류*를 선언합니다.  
  
> [!IMPORTANT]  
>  주 데이터베이스가 아닌 다른 데이터베이스의 오류는 감지되지 않습니다. 또한 데이터베이스가 데이터 디스크 오류로 인해 다시 시작되지 않는 한 데이터 디스크 오류도 감지되지 않습니다.  
  
 오류 감지 속도 그리고 이에 따른 오류 반응 속도는 오류가 하드 오류인지 소프트 오류인지에 따라 달라집니다. 네트워크 오류와 같은 일부 하드 오류는 즉시 보고되지만 경우에 따라 구성 요소별 제한 시간으로 인해 일부 하드 오류 보고가 지연될 수 있습니다. 소프트 오류의 경우 세션 제한 시간의 길이가 오류 검색 속도를 결정합니다. 기본적으로 이 시간은 10초( 최소 권장 값)입니다.  
  
## <a name="failures-due-to-hard-errors"></a>하드 오류로 인한 실패  
 하드 오류를 일으킬 수 있는 원인 중에는 다음 조건이 있습니다.  
  
-   연결 또는 전선의 끊어짐  
  
-   잘못된 네트워크 카드  
  
-   라우터 변경  
  
-   방화벽 내의 변경 사항  
  
-   엔드포인트 다시 구성  
  
-   트랜잭션 로그가 있는 드라이브 손실  
  
-   운영 체제 또는 프로세스 오류  
  
 예를 들어 주 데이터베이스의 로그 드라이브가 응답하지 않거나 실패하면 운영 체제에서 Sqlservr.exe에 심각한 오류 발생 사실을 알립니다.  
  
 네트워크 구성 요소 및 일부 IO 하위 시스템과 같은 구성 요소에는 자체적으로 오류를 확인하기 위한 제한 시간이 있습니다. 이러한 제한 시간은 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]에 독립적이므로 데이터베이스 미러링에 대해 알지 못하며 데이터베이스 미러링 동작을 전혀 파악할 수 없습니다. 이러한 경우 제한 시간이 지연되어 오류가 발생한 다음 가용성 복제본이 결과 하드 오류를 수신할 때까지의 시간이 늘어납니다.  
  
> [!NOTE]  
>  가용성 복제본에 대한 활성 오류 검사는 소프트웨어 오류의 경우에만 수행됩니다. 자세한 내용은 이 항목의 뒷부분에 나오는 "소프트 오류로 인한 오류"를 참조하십시오.  
  
 네트워크에서 발생하는 오류 상황을 해석하는 데 도움이 되도록 네트워크 엔지니어에게 TCP 연결에서 다음 이벤트가 발생할 경우 어떤 오류 메시지가 포트로 전송되는지 문의하십시오.  
  
-   DNS가 작동하지 않는 경우  
  
-   케이블이 연결되어 있지 않은 경우  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows에 특정 포트를 차단하는 방화벽이 있는 경우  
  
-   포트를 모니터링하는 애플리케이션에서 오류가 발생한 경우  
  
-   Windows 기반 서버 이름이 바뀐 경우  
  
-   Windows 기반 서버가 다시 부팅된 경우  
  
> [!NOTE]  
>  [!INCLUDE[ssHADRc](../../../includes/sshadrc-md.md)]은 서버에 액세스하는 클라이언트 관련 문제에 대해 보호하지 않습니다. 예를 들어 프라이빗 네트워크 인터페이스 카드가 가용성 그룹 복제본을 호스팅 중인 서버 인스턴스 간의 트래픽을 처리하는 동안 퍼블릭 네트워크 어댑터가 주 복제본에 대한 클라이언트 연결을 처리하는 경우 이 경우 공용 네트워크 어댑터의 오류로 인해 클라이언트가 데이터베이스에 액세스하지 못합니다.  
  
## <a name="failures-due-to-soft-errors"></a>소프트 오류로 인한 오류  
 세션 제한 시간 초과가 발생할 수 있는 상황은 다음(여기에 한정되지 않음)과 같습니다.  
  
-   TCP 연결 제한 시간 초과, 삭제되거나 손상된 패킷, 잘못된 순서의 패킷 등의 네트워크 오류  
  
-   응답하지 않는 운영 체제, 서버 또는 데이터베이스  
  
-   Windows 서버 제한 시간 초과  
  
-   CPU 또는 디스크 오버로드, 꽉 찬 트랜잭션 로그 또는 시스템의 메모리나 스레드 부족과 같은 컴퓨팅 리소스 부족. 이런 경우에는 제한 시간을 늘이거나, 작업을 줄이거나, 작업을 처리할 수 있도록 하드웨어를 변경해야 합니다.  
  
### <a name="the-session-timeout-mechanism"></a>세션 제한 시간 메커니즘  
 소프트 오류는 서버 인스턴스에서 직접 감지되지 않으므로 소프트 오류 발생 시 가용성 복제본이 세션 내 다른 가용성 복제본의 응답을 무기한 대기할 수 있습니다. 이를 방지하기 위해 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 은 연결된 가용성 복제본을 기반으로 열려 있는 각 연결에서 일정한 간격으로 ping을 보내는 제한 시간 메커니즘을 구현합니다. 제한 시간 내에 ping을 받은 경우 연결이 열려 있으며 서버 인스턴스가 해당 연결을 통해 통신하고 있음을 나타냅니다. ping을 받으면 복제본은 해당 연결의 제한 시간 카운터를 다시 설정합니다. 가용성 모드와 세션 시간 초과의 관계에 대 한 자세한 내용은 [가용성 모드 (AlwaysOn 가용성 그룹)](availability-modes-always-on-availability-groups.md)를 참조 하세요.  
  
 주 복제본과 보조 복제본은 서로에 대해 ping을 수행하여 자신이 아직 활성 상태임을 나타내며 세션 제한 시간은 이들 복제본이 상대 복제본의 ping을 무기한 수신 대기하지 않도록 합니다. 세션 제한 시간은 사용자가 구성 가능한 복제본 속성이며 기본값은 0초입니다. 제한 시간 내에 ping을 받은 경우 연결이 열려 있으며 서버 인스턴스가 해당 연결을 통해 통신하고 있음을 나타냅니다. ping을 받으면 가용성 복제본은 해당 연결의 제한 시간 카운터를 다시 설정 합니다.  
  
 세션 제한 시간 내에 다른 복제본 으로부터 ping을 받지 못하면 연결 시간이 초과 됩니다. 연결이 닫히고 시간 초과 된 복제본이 연결이 끊어진 상태로 전환 됩니다. 연결이 끊어진 복제본이 동기 커밋 모드로 구성되어 있더라도 트랜잭션에서는 해당 복제본이 다시 연결되어 다시 동기화될 때까지 대기하지 않습니다.  
  
## <a name="responding-to-an-error"></a>오류에 대한 응답  
 오류 유형에 관계없이 오류를 감지하는 서버 인스턴스는 인스턴스의 역할, 세션의 가용성 모드 및 세션 내 다른 연결의 상태를 기반으로 적절하게 오류에 응답합니다. 파트너가 손실 될 때 발생 하는 상황에 대 한 자세한 내용은 [가용성 모드 (AlwaysOn 가용성 그룹)](availability-modes-always-on-availability-groups.md)를 참조 하세요.  
  
## <a name="related-tasks"></a>관련 작업  
 **제한 시간 값을 변경하려면(동기 커밋 가용성 모드 전용)**  
  
-   [가용성 복제본에 대한 세션 제한 시간 변경&#40;SQL Server&#41;](change-the-session-timeout-period-for-an-availability-replica-sql-server.md)  
  
 **현재 제한 시간 값을 보려면**  
  
-   [sys.availability_replicas&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)에서 **session_timeout**을 쿼리합니다.  
  
## <a name="see-also"></a>참고 항목  
 [AlwaysOn 가용성 그룹 &#40;SQL Server 개요&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
