---
title: '가용성 그룹 속성: 새 가용성 그룹(일반 페이지) | Microsoft Docs'
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.availabilitygroupproperties.general.f1
ms.assetid: 9af5379f-91b8-4729-9f75-4a80242a30e9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 098bc8bf6746acdec41aecc9533b21bc0b49e095
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47690001"
---
# <a name="availability-group-properties-new-availability-group-general-page"></a>가용성 그룹 속성: 새 가용성 그룹(일반 페이지)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목은 **새 가용성 그룹** 대화 상자 및 **가용성 그룹 속성** 대화 상자의 **일반** 탭에 적용됩니다.  **를 사용하지 않고** 새 가용성 그룹 [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)]대화 상자를 사용하여 새 가용성 그룹을 만들 수 있으며, **가용성 그룹 속성** 대화 상자를 사용하여 기존 가용성 그룹의 구성을 확인하고 변경할 수 있습니다.  
  
 **가용성 그룹 속성을 보려면**  
  
-   [가용성 그룹 속성 보기&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-properties-sql-server.md)  
  
-   [Always On 대시보드 사용&#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
## <a name="uielement-list"></a>UIElement 목록  
 **가용성 그룹 이름**  
 가용성 그룹의 이름으로, WSFC(Windows Server 장애 조치(failover) 클러스터) 내에서 고유해야 하는 사용자 지정 이름입니다.  
  
## <a name="availability-databases"></a>가용성 데이터베이스  
 **Database Name**  
 가용성 그룹에 추가된 데이터베이스의 이름입니다.  
  
 **추가**  
 가용성 그룹에 데이터베이스를 추가하려면 클릭합니다.  
  
 **제거**  
 가용성 그룹에서 선택된 데이터베이스를 제거하려면 클릭합니다.  
  
## <a name="availability-replicas"></a>가용성 복제본  
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
  
 자세한 내용은 [가용성 모드&#40;Always On 가용성 그룹&#41;](../../../database-engine/availability-groups/windows/availability-modes-always-on-availability-groups.md)라는 프로세스에서 서로 바꿀 수 있습니다.  
  
 **장애 조치(Failover) 모드**  
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
 애플리케이션 의도 연결 속성이 **ReadOnly** 로 설정된 연결은 허용되지 않습니다. 애플리케이션 의도 속성이 **ReadWrite** 로 설정되었거나 애플리케이션 의도 연결 속성이 설정되지 않은 경우에는 연결이 허용됩니다. 애플리케이션 의도 연결 속성에 대한 자세한 내용은 [Using Connection String Keywords with SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)을 참조하십시오.  
  
 **읽기용 보조**  
 보조 역할을 수행하는 가용성 복제본,  즉 보조 복제본이 클라이언트로부터의 연결을 허용할 수 있는지 여부를 나타내며,  다음 중 하나입니다.  
  
 **아니요**  
 이 복제본의 보조 데이터베이스에 대한 직접 연결이 허용되지 않습니다. 즉, 읽기 액세스가 가능하지 않습니다. 이 값은 기본 설정입니다.  
  
 **읽기 전용만**  
 이 복제본의 보조 데이터베이스에 대한 직접 읽기 전용 연결만 허용됩니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
 **예**  
 이 복제본의 보조 데이터베이스에 대한 모든 연결이 허용되지만 읽기 액세스만 가능합니다. 즉, 모든 보조 데이터베이스에 대한 읽기 액세스가 가능합니다.  
  
 **세션 제한 시간(초)**  
 이 복제본에 대한 세션 제한 시간(초)입니다.  
  
 **엔드포인트 URL**  
 엔드포인트의 URL입니다. 이러한 URL 형식에 대한 자세한 내용은 [가용성 복제본 추가 또는 수정 시 엔드포인트 URL 지정&amp;#40;SQL Server&amp;#41;](../../../database-engine/availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)을 참조하세요.  
  
 **추가**  
 가용성 그룹에 보조 복제본을 추가하려면 클릭합니다.  
  
 **제거**  
 보조 복제본을 가용성 그룹에서 제거하려면 클릭합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)  
  
  
