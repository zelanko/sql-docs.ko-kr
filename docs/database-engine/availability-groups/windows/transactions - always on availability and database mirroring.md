---
title: "데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대해 지원되지 않는 데이터베이스 간 트랜잭션(SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-high-availability"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "데이터베이스 미러링 [SQL Server], 상호 운용성"
  - "데이터베이스 간 트랜잭션 [SQL Server]"
  - "트랜잭션 [데이터베이스 미러링]"
  - "가용성 그룹 [SQL Server], 상호 운용성"
  - "문제 해결 [SQL Server], 데이터베이스 간 트랜잭션"
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
caps.latest.revision: 33
ms.author: "mikeray"
manager: "jhubbard"
---
# 데이터베이스 미러링 또는 AlwaysOn 가용성 그룹에 대해 지원되지 않는 데이터베이스 간 트랜잭션(SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

이 항목에서는 Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션 지원에 대해 설명합니다.  
  
## 같은 SQL Server 인스턴스 내의 데이터베이스 간 트랜잭션 지원  
Always On 가용성 그룹의 경우 같은 SQL Server 인스턴스 내의 데이터베이스 간 트랜잭션이 지원되지 않습니다. 즉, 데이터베이스 간 트랜잭션을 수행하는 두 데이터베이스를 같은 SQL Server 인스턴스가 호스트할 수는 없습니다. 해당 데이터베이스가 같은 가용성 그룹에 속하는 경우에도 마찬가지입니다.  
  
데이터베이스 미러링에는 데이터베이스 간 트랜잭션도 지원되지 않습니다.  
  
##  <a name="dtcsupport"></a> 분산 트랜잭션 지원  
Always On 가용성 그룹에서는 분산 트랜잭션이 지원됩니다. 서로 다른 두 SQL Server 인스턴스가 호스트하는 데이터베이스 간의 분산 트랜잭션이 지원됩니다. SQL Server와 다른 DTC 호환 서버 간의 분산 트랜잭션도 지원됩니다.  
 
MSDTC 또는 DTC(Microsoft Distributed Transaction Coordinator)는 분산 시스템에 대한 트랜잭션 인프라를 제공하는 Windows 서비스입니다. MSDTC는 클라이언트 응용 프로그램이 한 트랜잭션에 여러 데이터 원본을 포함한 다음 트랜잭션에 포함된 모든 서버에서 커밋할 수 있게 합니다. 예를 들어 MSDTC를 사용하여 서로 다른 서버의 여러 데이터베이스에 걸쳐 있는 트랜잭션을 조정할 수 있습니다.

SQL Server 2016에서는 트랜잭션에 포함된 하나 이상의 데이터베이스가 가용성 그룹에 있는 분산 트랜잭션을 사용하는 기능이 도입되었습니다. SQL Server 2016 이전에는 가용성 그룹의 데이터베이스에 대해 분산 트랜잭션이 지원되지 않았습니다. SQL Server 2016에서는 데이터베이스당 하나의 리소스 관리자를 등록할 수 있습니다. 이 새로운 기능 때문에 분산 트랜잭션에 가용성 그룹의 데이터베이스가 포함될 수 있습니다.

  
 분산 트랜잭션과 관련하여 충족해야 하는 요구 사항은 다음과 같습니다.  
  
-   Windows Server 2016 또는 Windows Server 2012 R2에서 가용성 그룹을 실행해야 합니다. Windows Server 2012 R2의 경우 [https://support.microsoft.com/en-us/kb/3090973](https://support.microsoft.com/en-us/kb/3090973)에서 제공되는 KB3090973의 업데이트를 설치해야 합니다.  
  
-   **CREATE AVAILABILITY GROUP** 명령 및 **WITH DTC_SUPPORT = PER_DB** 절을 사용하여 가용성 그룹을 만들어야 합니다. 현재는 기존 가용성 그룹을 변경할 수 없습니다.  

- 가용성 그룹에 참여할 모든 SQL Server 인스턴스가 SQL Server 2016 이상이어야 합니다.
  
 
 ## 분산 트랜잭션 미지원
 분산 트랜잭션이 지원되지 않는 특정 경우는 다음과 같습니다.
 
 -  트랜잭션에 관련된 둘 이상의 데이터베이스가 같은 가용성 그룹에 있는 경우.
 
 -  하나 이상의 데이터베이스가 가용성 그룹에 있고 또 다른 데이터베이스가 SQL Server의 같은 인스턴스에 있는 경우. 
 
 -  가용성 그룹이 분산 트랜잭션 사용으로 만들어지지 않은 경우.
 
 -  데이터베이스 미러링.
 
 ## 권장
 프로덕션 환경에서 DTC 서비스를 클러스터해야 합니다. DTC 서비스를 클러스터하지 않으면 SQL Server가 로컬 DTC 서비스를 사용합니다. 로컬 DTC 서비스를 사용할 경우 솔루션의 전반적인 가용성이 줄어듭니다. DTC가 클러스터된 경우 클러스터 노드가 실패하면 In-process 트랜잭션을 복구할 수 있습니다.
 
 > [!IMPORTANT]
 > 사용자 환경에서 DTC가 해결할 수 없는 트랜잭션의 적절한 기본 결과를 확인합니다.  기본 결과를 구성하는 방법에 대한 내용은 [in-doubt xact resolution 서버 구성 옵션](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md)을 참조하세요.
  
## 데이터베이스 미러링을 수행하는 예제 시나리오  
 다음 데이터베이스 미러링 예에서는 논리적 불일치가 발생하는 방식을 보여 줍니다. 이 예에서 응용 프로그램은 데이터베이스 간 트랜잭션을 사용하여 두 행의 데이터를 삽입합니다. 한 행은 미러된 데이터베이스 A의 테이블에 삽입되고 다른 행은 데이터베이스 B의 테이블에 삽입됩니다. 데이터베이스 A는 자동 장애 조치(failover) 있는 보호 우선 모드로 미러됩니다. 트랜잭션이 커밋되는 동안 데이터베이스 A를 사용할 수 없게 되고 미러링 세션이 자동으로 데이터베이스 A의 미러로 장애 조치됩니다.  
  
 장애 조치 후에 데이터베이스 B에서는 데이터베이스 간 트랜잭션이 성공적으로 커밋될 수 있지만 장애 조치된 데이터베이스에서는 커밋되지 않습니다. 데이터베이스 A의 원래 주 서버가 실패하기 전에 데이터베이스 간 트랜잭션 로그를 미러 서버로 보내지 않은 경우 이런 문제가 발생합니다. 장애 조치 후에 새로운 주 서버에는 해당 트랜잭션이 없습니다. 데이터베이스 B에 삽입한 데이터는 그대로 유지되고 데이터베이스 A에 삽입한 데이터는 손실되었으므로 데이터베이스 A와 B가 일치하지 않습니다.  
  
 MS DTC 트랜잭션을 사용하는 동안 이와 유사한 시나리오가 발생할 수 있습니다. 예를 들어 장애 조치 후에 새로운 주 서버가 MS DTC에 연결합니다. 그러나 MS DTC는 새로운 주 서버를 알지 못하며 다른 데이터베이스에서 커밋된 것으로 간주되는 "커밋 준비 중"인 모든 트랜잭션을 종료합니다.  
  
> [!NOTE]  
>  이 항목에서 승인하지 않는 방식으로 DTC에서 데이터베이스 미러링 또는 Always On 가용성 그룹을 사용할 수는 없습니다.  DTC와 관련이 없는 제품 측면이 지원되지 않는 것은 아니지만, 분산 트랜잭션을 부적절하게 사용하는 경우 발생하는 문제는 지원되지 않습니다.  
  
## 참고 항목  
 [Always On 가용성 그룹: 상호 운용성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  