---
title: "Always On 가용성 그룹이 있는 데이터베이스 스냅숏(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- database snapshots [SQL Server], AlwaysOn Availability Groups
- Availability Groups [SQL Server], interoperability
ms.assetid: 7432da1c-ce2f-4cd9-af41-54c97744166b
caps.latest.revision: 7
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a490cf9ff2ed4b847525056411cc58923e03e97f
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="database-snapshots-with-always-on-availability-groups-sql-server"></a>Always On 가용성 그룹이 있는 데이터베이스 스냅숏(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  가용성 그룹의 주 데이터베이스 또는 보조 데이터베이스에서 데이터베이스 스냅숏을 만들 수 있습니다. 복제본 역할은 RESOLVING 상태가 아닌 PRIMARY 또는 SECONDARY 상태여야 합니다.  
  
 데이터베이스 동기화 상태가 SYNCHRONIZING 또는 SYNCHRONIZED인 상태에서 데이터베이스 스냅숏을 만드는 것이 좋습니다. 데이터베이스 동기화 상태가 NOT SYNCHRONIZING인 경우에도 데이터베이스 스냅숏을 만들 수는 있습니다.  
  
 복제본이 주 복제본에서 DISCONNECTED된 경우 보조 복제본의 데이터베이스 스냅숏은 계속 작업해야 합니다.  
  
 일부 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 조건에서는 원본 데이터베이스와 데이터베이스 스냅숏이 모두 다시 시작되어 일시적으로 사용자와의 연결이 끊어집니다. 이러한 조건은 다음과 같습니다.  
  
-   동일한 서버 인스턴스에서 현재 주 복제본이 오프라인으로 전환되었다가 다시 온라인으로 돌아오거나 가용성 그룹이 장애 조치를 수행하기 때문에 주 복제본이 역할을 변경합니다.  
  
-   데이터베이스가 보조 역할로 전환됩니다.  
  
 데이터베이스 스냅숏을 호스팅하는 가용성 복제본이 장애 조치되는 경우 데이터베이스 스냅숏은 처음 만들어진 서버 인스턴스에 그대로 유지됩니다. 사용자는 장애 조치 후에도 스냅숏을 계속 사용할 수 있습니다. 사용자 환경에서 성능이 중요한 경우 수동 장애 조치 모드에 대해 구성되는 보조 복제본에서 호스팅되는 보조 데이터베이스에서만 데이터베이스 스냅숏을 만드는 것이 좋습니다.  가용성 그룹을 이 보조 복제본으로 수동으로 장애 조치하는 경우 다른 보조 복제본에서 새 데이터베이스 스냅숏 집합을 만들고 클라이언트를 새 데이터베이스 스냅숏으로 리디렉션한 다음 새 주 데이터베이스의 모든 데이터베이스 스냅숏을 삭제할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [데이터베이스 스냅숏&#40;SQL Server&#41;](../../../relational-databases/databases/database-snapshots-sql-server.md)  
  
  

