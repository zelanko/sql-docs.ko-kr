---
title: SQL Server 오류 로그(가용성 그룹)
description: Always On 가용성 그룹에 영향을 주는 SQL Server 오류 로그 이벤트 및 오류 로그를 검토해야 하는 증상에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
ms.assetid: 39d0c98d-75af-4dd1-b908-30d31af56f2a
author: rothja
ms.author: jroth
ms.openlocfilehash: b33827f37d02edf783c4688c9ad08cd4673706e7
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670888"
---
# <a name="sql-server-error-log-always-on-availability-groups"></a>SQL Server 오류 로그(Always On 가용성 그룹)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  SQL Server 오류 로그는 다음과 같은 Always On 가용성 그룹에 영향을 주는 이벤트를 보고합니다.  
  
-   WSFC(Windows Server 장애 조치(Failover) 클러스터링) 클러스터와 통신    
-   가용성 복제본의 상태 전환    
-   가용성 데이터베이스의 상태 전환    
-   주 복제본과 보조 복제본 간 가용성 데이터베이스의 연결 상태    
-   가용성 그룹 엔드포인트의 상태    
-   가용성 그룹 수신기의 상태    
-   SQL Server 리소스 DLL(WSFC 클러스터에서 실행) 및 SQL Server 인스턴스 간의 임대 시간(자세한 내용은 [작동 방법: SQL Server Always On 임대 시간 제한](/archive/blogs/psssql/how-it-works-sql-server-alwayson-lease-timeout) 참조)    
-   가용성 그룹의 오류 이벤트  

다음과 같은 현상은 SQL Server 오류 로그를 검토해야 합니다.  

-   가용성 데이터베이스에 액세스할 수 없음    
-   예기치 않은 가용성 그룹 장애 조치(failover)    
-   예기치 않게 확인 중 상태의 가용성 그룹    
-   비활성화 상태의 가용성 그룹  
  
자세한 내용은[SQL Server 오류 로그 보기&#40;SQL Server Management Studio&#41;](~/relational-databases/performance/view-the-sql-server-error-log-sql-server-management-studio.md)를 참조하세요.  
  
