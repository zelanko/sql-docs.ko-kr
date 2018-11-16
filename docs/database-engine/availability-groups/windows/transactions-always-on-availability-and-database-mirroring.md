---
title: 트랜잭션 - Always On 가용성 그룹 및 데이터베이스 미러링 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], interoperability
- cross-database transactions [SQL Server]
- transactions [database mirroring]
- Availability Groups [SQL Server], interoperability
- troubleshooting [SQL Server], cross-database transactions
ms.assetid: 9f7ed895-ad65-43e3-ba08-00d7bff1456d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad9700e9b1c86b454191e51c6a7e4ee52c393c6b
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/13/2018
ms.locfileid: "51606843"
---
# <a name="transactions---availability-groups-and-database-mirroring"></a>트랜잭션 - Always On 가용성 그룹 및 데이터베이스 미러링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

이 아티클에서는 Always On 가용성 그룹 및 데이터베이스 미러링에 대한 데이터베이스 간 트랜잭션 및 분산 트랜잭션 지원에 대해 설명합니다.  

## <a name="support-for-distributed-transactions"></a>분산 트랜잭션 지원

SQL Server 2017은 가용성 그룹의 데이터베이스에 대한 분산 트랜잭션을 지원합니다. 이 지원에는 SQL Server의 동일한 인스턴스에 있는 데이터베이스 또는 SQL Server의 다른 인스턴스에 있는 데이터베이스가 포함됩니다. 데이터베이스 미러링을 위해 구성된 데이터베이스에는 분산 트랜잭션이 지원되지 않습니다.

>[!NOTE]
>[!INCLUDE[SQL Server 2016]](../../../includes/sssql15-md.md)] 서비스 팩 2 이상은 가용성 그룹에서 분산 트랜잭션에 대한 완전한 지원을 제공합니다. 
>
>[!INCLUDE[SQL Server 2016]](../../../includes/sssql15-md.md)] 서비스 팩 2 이전 버전은 가용성 그룹의 데이터베이스가 포함된 데이터베이스 간 분산 트랜잭션(예: 동일한 SQL Server 인스턴스에서 데이터베이스를 사용하는 트랜잭션)을 지원하지 않습니다.

분산 트랜잭션에 대한 가용성 그룹을 구성하려면 [분산 트랜잭션에 대한 가용성 그룹 구성](configure-availability-group-for-distributed-transactions.md)을 참조하세요.

자세한 내용은 다음을 참조하세요.

- [DTC 관리 가이드(영문)](https://msdn.microsoft.com/library/ms681291.aspx)
- [DTC 개발자 가이드(영문)](https://msdn.microsoft.com/library/ms679938.aspx)
- [DTC 프로그래머 참조(영문)](https://msdn.microsoft.com/library/ms686108.aspx)

## <a name="sql-server-2016-sp1-and-before-support-for-cross-database-transactions-within-the-same-sql-server-instance"></a>SQL Server 2016 SP1 이전 버전: 동일한 SQL Server 인스턴스 내의 데이터베이스 간 트랜잭션 지원  

SQL Server 2016 SP1 이전 버전에서는 가용성 그룹에 대해 동일한 SQL Server 인스턴스 내의 데이터베이스 간 트랜잭션이 지원되지 않습니다. 데이터베이스 간 트랜잭션의 두 데이터베이스 중 하나가 가용성 그룹에 위치한 경우 같은 SQL Server 인스턴스에서 호스트할 수는 없습니다. 해당 데이터베이스가 같은 가용성 그룹에 속하는 경우에도 이 제한 사항이 적용됩니다.  
  
데이터베이스 미러링에는 데이터베이스 간 트랜잭션도 지원되지 않습니다.  
  
##  <a name="dtcsupport"></a> SQL Server 2016 SP1 이전 버전: 분산 트랜잭션 지원  
데이터베이스가 다른 SQL Server 인스턴스에서 호스팅되는 경우 가용성 그룹에서 분산 트랜잭션이 지원됩니다. SQL Server 인스턴스와 다른 DTC 호환 서버 간의 분산 트랜잭션에도 적용됩니다.  
 
MSDTC 또는 DTC(Microsoft Distributed Transaction Coordinator)는 분산 시스템에 대한 트랜잭션 인프라를 제공하는 Windows 서비스입니다. MSDTC는 클라이언트 응용 프로그램이 한 트랜잭션에 여러 데이터 원본을 포함한 다음, 트랜잭션에 포함된 모든 서버에서 커밋할 수 있게 합니다. 예를 들어 MSDTC를 사용하여 서로 다른 서버의 여러 데이터베이스에 걸쳐 있는 트랜잭션을 조정할 수 있습니다.

SQL Server 2016에서는 트랜잭션에 포함된 하나 이상의 데이터베이스가 가용성 그룹에 있는 분산 트랜잭션을 사용하는 기능이 도입되었습니다. SQL Server 2016 이전에는 가용성 그룹의 데이터베이스에 대해 분산 트랜잭션이 지원되지 않았습니다. SQL Server 2016에서는 데이터베이스당 하나의 리소스 관리자를 등록할 수 있습니다. 이 새로운 기능 때문에 분산 트랜잭션에 가용성 그룹의 데이터베이스가 포함될 수 있습니다.
  
 분산 트랜잭션과 관련하여 충족해야 하는 요구 사항은 다음과 같습니다.  
  
-   Windows Server 2012 R2 이상에서 가용성 그룹을 실행해야 합니다. Windows Server 2012 R2의 경우 [https://support.microsoft.com/kb/3090973](https://support.microsoft.com/kb/3090973)에서 제공되는 KB3090973의 업데이트를 설치해야 합니다.  
  
-   **CREATE AVAILABILITY GROUP** 명령 및 **WITH DTC\_SUPPORT = PER_DB** 절을 사용하여 가용성 그룹을 만들어야 합니다. 현재는 기존 가용성 그룹을 변경할 수 없습니다.  

- 가용성 그룹에 참여한 모든 SQL Server 인스턴스가 SQL Server 2016 이상이어야 합니다.
 
 ## <a name="non-support-for-distributed-transactions"></a>분산 트랜잭션 미지원
 분산 트랜잭션이 지원되지 않는 특정 경우는 다음과 같습니다.
 
 - SQL Server 2016 SP1 이전 버전에서 트랜잭션에 관련된 둘 이상의 데이터베이스가 동일한 가용성 그룹에 있는 경우
 
 - SQL Server 2016 SP1 이전 버전에서 하나 이상의 데이터베이스가 가용성 그룹에 있고, 또 다른 데이터베이스가 SQL Server의 동일한 인스턴스에 있는 경우 
 
 - 가용성 그룹이 분산 트랜잭션 사용으로 만들어지지 않은 경우.
 
 - 데이터베이스 미러링.
 
 > [!IMPORTANT]
 > 사용자 환경에서 DTC가 해결할 수 없는 트랜잭션의 적절한 기본 결과를 확인합니다.  기본 결과를 구성하는 방법에 대한 내용은 [in-doubt xact resolution 서버 구성 옵션](../../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md)을 참조하세요.
  
## <a name="example-scenario-with-database-mirroring"></a>데이터베이스 미러링을 수행하는 예제 시나리오  
 다음 데이터베이스 미러링 예에서는 논리적 불일치가 발생하는 방식을 보여 줍니다. 이 예에서 응용 프로그램은 데이터베이스 간 트랜잭션을 사용하여 두 행의 데이터를 삽입합니다. 한 행은 미러된 데이터베이스 A의 테이블에 삽입되고 다른 행은 데이터베이스 B의 테이블에 삽입됩니다. 데이터베이스 A는 자동 장애 조치(failover) 있는 보호 우선 모드로 미러됩니다. 트랜잭션이 커밋되는 동안 데이터베이스 A를 사용할 수 없게 되고 미러링 세션이 자동으로 데이터베이스 A의 미러로 장애 조치됩니다.  
  
 장애 조치 후에 데이터베이스 B에서는 데이터베이스 간 트랜잭션이 성공적으로 커밋될 수 있지만 장애 조치된 데이터베이스에서는 커밋되지 않습니다. 예를 들어 데이터베이스 A의 원래 주 서버가 실패하기 전에 데이터베이스 간 트랜잭션 로그를 미러 서버로 보내지 않은 경우입니다. 장애 조치 후에 새로운 주 서버에는 해당 트랜잭션이 없습니다. 데이터베이스 B에 삽입한 데이터는 그대로 유지되고 데이터베이스 A에 삽입한 데이터는 손실되었으므로 데이터베이스 A와 B가 일치하지 않습니다.  
  
 MS DTC 트랜잭션을 사용하는 동안 이와 유사한 시나리오가 발생할 수 있습니다. 예를 들어 장애 조치 후에 새로운 주 서버가 MS DTC에 연결합니다. 그러나 MS DTC는 새로운 주 서버를 알지 못하며 다른 데이터베이스에서 커밋된 것으로 간주되는 "커밋 준비 중"인 모든 트랜잭션을 종료합니다.  
  
> [!NOTE]  
>  이 아티클에서 승인되지 않은 방식으로 DTC에서 데이터베이스 미러링 또는 가용성 그룹을 사용하는 것은 지원되지 않습니다.  DTC와 관련이 없는 제품 측면이 지원되지 않는 것은 아니지만, 분산 트랜잭션을 부적절하게 사용하는 경우 발생하는 문제는 지원되지 않습니다.  
  
## <a name="next-steps"></a>다음 단계  
 [Always On availability groups: Interoperability &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-availability-groups-interoperability-sql-server.md)  
  
  
