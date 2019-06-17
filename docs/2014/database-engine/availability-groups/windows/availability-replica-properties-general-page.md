---
title: 가용성 복제본 속성(일반 페이지) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.availabilityreplicaproperties.general.f1
ms.assetid: 8318fefb-e045-4fab-8507-e1951fc7cec6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07652cec7b3b7a17c4b994eb68afd939e15244a3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791907"
---
# <a name="availability-replica-properties-general-page"></a>가용성 복제본 속성(일반 페이지)
  이 대화 상자를 사용하여 가용성 복제본의 속성을 확인할 수 있습니다.  
  
## <a name="task-list"></a>작업 목록  
 **가용성 복제본 속성을 보려면**  
  
-   [가용성 복제본 속성 보기&#40;SQL Server&#41;](view-availability-replica-properties-sql-server.md)  
  
-   [AlwaysOn 대시보드 사용&#40;SQL Server Management Studio&#41;](use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>UIElement 목록  
 **가용성 그룹 이름**  
 가용성 그룹의 이름으로, WSFC(Windows Server 장애 조치(failover) 클러스터) 내에서 고유해야 하는 사용자 지정 이름입니다.  
  
 **서버 인스턴스**  
 이 복제본을 호스팅하는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 인스턴스의 서버 이름(기본 인스턴스가 아닌 경우에는 인스턴스 이름)입니다.  
  
 **역할**  
 **주**  
 현재 주 복제본입니다.  
  
 **보조**  
 현재 보조 복제본입니다.  
  
 **확인**  
 현재 복제본 역할이 주 역할 또는 보조 역할로 확인 중입니다.  
  
 **가용성 모드**  
 복제본의 가용성 모드로,  다음 중 하나입니다.  
  
 **비동기 커밋**  
 주 복제본은 보조 복제본이 로그를 디스크에 쓸 때까지 기다리지 않고 트랜잭션을 커밋할 수 있습니다.  
  
 **동기 커밋**  
 주 복제본은 보조 복제본이 트랜잭션을 디스크에 쓸 때까지 기다렸다가 지정된 트랜잭션을 커밋합니다.  
  
 자세한 내용은 [가용성 모드 (AlwaysOn 가용성 그룹)](availability-modes-always-on-availability-groups.md)합니다.  
  
 **Failover mode**  
 복제본의 장애 조치(failover) 모드로, 다음 중 하나입니다.  
  
 **자동**  
 자동 장애 조치(failover). 복제본이 자동 장애 조치(failover)의 대상입니다. 이 옵션은 가용성 모드가 동기 커밋으로 설정된 경우에만 지원됩니다.  
  
 **수동**  
 수동 장애 조치(failover). 데이터베이스 관리자가 복제본을 수동으로만 장애 조치할 수 있습니다.  
  
 **주 역할의 연결 모드**  
 복제본이 주 역할을 소유한 경우에 지원되는 클라이언트 연결 유형입니다.  
  
 **모든 연결 허용**  
 주 복제본의 데이터베이스에 대한 모든 연결이 허용됩니다. 이 값은 기본 설정입니다.  
  
 **읽기/쓰기 연결 허용**  
 애플리케이션 의도 연결 속성이 **ReadOnly** 로 설정된 연결은 허용되지 않습니다. 애플리케이션 의도 속성이 **ReadWrite** 로 설정되었거나 애플리케이션 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다.  
  
 **읽기용 보조**  
 보조 역할을 수행하는 가용성 복제본,  즉 보조 복제본이 클라이언트로부터의 연결을 허용할 수 있는지 여부를 나타내며,  다음 중 하나입니다.  
  
 **아니요**  
 이 복제본의 보조 데이터베이스에 대한 직접 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 이 값은 기본 설정입니다.  
  
 **읽기 전용만**  
 이 복제본의 보조 데이터베이스에 대한 직접 읽기 전용 연결만 허용됩니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
 **예**  
 이 복제본의 보조 데이터베이스에 대한 모든 연결이 허용되지만 읽기 액세스만 가능합니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
 자세한 내용은 [활성 보조 복제본: 읽기 가능한 보조 복제본 (AlwaysOn 가용성 그룹)](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)합니다.  
  
 **세션 제한 시간(초)**  
 제한 시간(초)입니다. 제한 시간은 복제본이 주 복제본과 보조 복제본 간의 연결이 실패한 것으로 간주하기 전에 복제본에서 다른 복제본의 메시지를 받기 위해 기다리는 최대 시간입니다. 세션 제한 시간은 보조 복제본이 주 복제본에 연결되어 있는지 여부를 검색합니다. 실패한 보조 복제본 연결을 검색한 경우 주 복제본은 보조 복제본을 NOT_SYNCHRONIZED로 간주합니다. 주 복제본과의 실패한 연결을 검색할 경우 보조 복제본에서는 단순히 다시 연결을 시도합니다.  
  
> [!NOTE]  
>  세션 제한 시간은 자동 장애 조치(failover)를 발생시키지 않습니다.  
  
 **엔드포인트 URL**  
 데이터 동기화를 위해 주 복제본과 보조 복제본 간의 연결에 사용되는 사용자 지정 데이터베이스 미러링 엔드포인트의 문자열 표현입니다. 엔드포인트 URL의 구문에 대한 자세한 내용은 [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&amp;#40;SQL Server&amp;#41;](specify-endpoint-url-adding-or-modifying-availability-replica.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [AlwaysOn 가용성 그룹 개요 &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)  
  
  
