---
title: 역할 (데이터베이스 미러링) 전환 중 서비스 중단 예측 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- parallel redo [SQL Server]
- role switching [SQL Server]
- database mirroring [SQL Server], queues
- failover [SQL Server], database mirroring
- redo [database mirroring]
- database mirroring [SQL Server], failover
ms.assetid: 586a6f25-672b-491b-bc2f-deab2ccda6e2
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4104fd32688abaf379db30a6ecf604a35c557778
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62806857"
---
# <a name="estimate-the-interruption-of-service-during-role-switching-database-mirroring"></a>역할 전환 중 서비스 중단 예측(데이터베이스 미러링)
  역할 전환 중에 데이터베이스 미러링의 서비스가 중단되는 시간은 역할 전환의 유형 및 원인에 따라 달라집니다.  
  
-   자동 장애 조치(Failover)의 경우 서비스 중단 시간은 미러 서버에서 주 서버 인스턴스의 실패를 인식하는 데 필요한 시간(오류 검색)과 데이터베이스 장애 조치에 필요한 시간(장애 조치 시간)에 의해 결정됩니다.  
  
-   강제 서비스 작업에서는 오류가 발생한 경우에도 사용자의 응답 능력에 따라 오류의 검색 및 응답이 달라집니다. 그러나 잠재적 서비스 중단 예측은 강제 서비스 명령이 실행된 후 미러 서버에서 역할을 전환하는 데 걸리는 시간을 예측하는 것으로 제한됩니다.  
  
    > [!NOTE]  
    >  일부 오류 유형과 같은 특정 조건을 검색하는 데 필요한 시간을 줄이려면 해당 조건에 대해 경고를 정의할 수 있습니다.  
  
-   수동 장애 조치의 경우 장애 조치 명령이 실행된 후 데이터베이스를 장애 조치하는 데 필요한 시간만 고려됩니다.  
  
## <a name="error-detection"></a>오류 검색  
 시스템에서 오류를 검색하는 데 걸리는 시간은 오류 유형에 따라 달라집니다. 예를 들어 네트워크 오류는 즉시 검색되지만 서버 중지는 기본적으로 검색하는 데 기본 제한 시간인 10초가 걸립니다.  
  
 데이터베이스 미러링 세션 중에 실패를 발생시킬 수 있는 오류와 자동 장애 조치를 지원하는 보호 우선 모드에서의 제한 시간 검색에 대한 자세한 내용은 [데이터베이스 미러링 중에 발생 가능한 오류](possible-failures-during-database-mirroring.md)를 참조하세요.  
  
## <a name="failover-time"></a>장애 조치 시간  
 장애 조치 시간은 주로 이전 미러 서버에서 Redo Queue에 남아 있는 로그를 롤포워드해야 하는 시간과 짧은 추가 시간으로 구성됩니다. 미러 서버에서 로그 레코드를 처리하는 방법은 [데이터베이스 미러링&#40;SQL Server&#41;](database-mirroring-sql-server.md)을 참조하세요. 장애 조치 시간을 계산하는 방법은 이 항목의 뒷부분에서 장애 조치 다시 실행 속도 계산을 참조하십시오.  
  
> [!IMPORTANT]  
>  인덱스 또는 테이블을 만든 후 변경하는 트랜잭션 중에 장애 조치를 수행하면 평소보다 시간이 오래 걸릴 수 있습니다.  예를 들어 장애 조치는 다음과 같은 일련의 작업 중에 장애 조치 시간이 길어질 수 있습니다.  BEGIN TRANSACTION, 테이블에 CREATE INDEX 및 SELECT INTO 테이블입니다. 이러한 트랜잭션 중에 증가한 장애 조치 시간은 COMMIT TRANSACTION 또는 ROLLBACK TRANSACTION 문으로 트랜잭션이 완료될 때까지 유지됩니다.  
  
### <a name="the-redo-queue"></a>Redo Queue  
 데이터베이스를 롤포워드하는 것은 현재 미러 서버에 있는 Redo Queue의 모든 로그 레코드를 적용하는 것입니다. *Redo Queue* 는 미러 서버의 디스크에 기록되었지만 미러 데이터베이스에서 롤포워드되지 않은 로그 레코드로 구성됩니다.  
  
 데이터베이스의 장애 조치 시간은 미러 서버에서 Redo Queue의 로그를 롤포워드할 수 있는 속도에 따라 달라지며 이 속도는 주로 시스템 하드웨어와 현재 작업에 의해 결정됩니다. 주 데이터베이스의 사용량이 많으므로 주 서버는 미러 서버에서 로그를 롤포워드할 수 있는 시간보다 훨씬 빠르게 로그를 미러 서버로 전달할 수도 있습니다. 이 경우 미러 서버에서 Redo Queue의 로그를 롤포워드하는 동안 장애 조치에 오랜 시간이 걸릴 수 있습니다. Redo Queue의 현재 크기를 확인하려면 데이터베이스 미러링 성능 개체의 **Redo Queue** 카운터를 사용합니다. 자세한 내용은 [SQL Server, Database Mirroring Object](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)을(를) 참조하세요.  
  
### <a name="estimating-the-failover-redo-rate"></a>장애 조치 다시 실행 속도 예측  
 프로덕션 데이터베이스의 테스트 복사본을 사용하여 로그 레코드를 롤포워드하는 데 필요한 시간(*다시 실행 속도*)을 측정할 수 있습니다.  
  
 장애 조치 중에 롤포워드 시간을 측정하는 방법은 다시 실행 단계 중에 미러 서버가 사용하는 스레드 수에 따라 결정됩니다. 스레드 수는 다음 경우에 따라 달라집니다.  
  
-   [!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]에서 미러 서버는 항상 단일 스레드를 사용하여 데이터베이스를 롤포워드합니다.  
  
-   [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]에서 CPU가 5개 미만인 시스템에 있는 미러 서버도 단일 스레드만 사용합니다. 5개 이상의 CPU가 있으면 미러 서버는 장애 조치 중에 해당 롤포워드 작업을 여러 스레드로 분산합니다. 이 분산 작업을 *병렬 다시 실행*이라고 합니다. 병렬 다시 실행은 CPU 4개당 스레드 하나를 사용하도록 최적화되었습니다.  
  
#### <a name="estimating-the-single-threaded-redo-rate"></a>단일 스레드 다시 실행 속도 예측  
 단일 스레드 다시 실행의 경우 장애 조치 중에 미러 데이터베이스를 롤포워드하는 데 걸리는 시간은 로그 백업에서 동일한 양의 로그를 롤포워드하는 데 걸리는 시간과 거의 같습니다. 장애 조치 시간을 계산하려면 미러링을 실행할 환경에 테스트 데이터베이스를 만듭니다. 그런 다음 프로덕션 데이터베이스로부터 로그 백업을 가져옵니다. 해당 로그 백업의 다시 실행 속도를 측정하려면 WITH NORECOVERY 로그 백업을 테스트 데이터베이스로 복원하는 데 걸리는 시간을 측정합니다.  
  
 미러 서버의 다시 실행 속도를 알고 있으면 **Redo Queue** 성능 카운터로 측정된 대로 미러 서버에서 다시 실행할 현재 로그 양을 다시 실행 속도로 나누어 지정된 시점에 데이터베이스를 장애 조치하는 데 걸리는 시간을 예측할 수 있습니다. 정상 조건에서 미러 서버가 주 서버의 로드를 처리할 수 있으면 **Redo Queue** 는 작거나 0에 가까운 값이며 장애 조치(Failover)에 몇 초밖에 걸리지 않습니다.  
  
#### <a name="estimating-the-parallel-redo-rate"></a>병렬 다시 실행 속도 예측  
 [!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]에서 병렬 다시 실행은 CPU 4개당 스레드 하나를 사용하도록 최적화되었습니다. 병렬 다시 실행의 롤포워드 시간을 예측하려면 테스트 데이터베이스보다 실행 중인 테스트 시스템에 액세스하는 것이 더 정확합니다. 미러 서버에서 Redo Queue를 모니터링하는 동안 주 서버의 로드를 늘리십시오. 정상 작업 시 Redo Queue는 0에 가깝습니다. Redo Queue가 지속적으로 증가하기 시작할 때까지 주 서버에 대한 로드를 증가시키십시오. 그러면 시스템의 최대 다시 실행 속도가 되고 이 지점에서 **Redo Bytes/sec** 성능 카운터는 최대 다시 실행 속도를 나타냅니다. 자세한 내용은 [SQL Server, Database Mirroring Object](../../relational-databases/performance-monitor/sql-server-database-mirroring-object.md)을(를) 참조하세요.  
  
## <a name="estimating-interruption-of-service-during-automatic-failover"></a>자동 장애 조치 중 서비스 중단 예측  
 다음 그림에서는 오류 검색 및 장애 조치 시간이 **Partner_B**에서 자동 장애 조치를 완료하는 데 필요한 전체 시간에 어떤 영향을 주는지를 보여 줍니다. 장애 조치에는 데이터베이스를 롤포워드할 시간(다시 실행 단계)과 데이터베이스를 온라인 상태로 만들기 위한 약간의 시간이 필요합니다. 커밋되지 않은 모든 트랜잭션이 롤백되는 실행 취소 단계는 새로운 주 데이터베이스가 온라인 상태가 된 다음 수행되고 장애 조치 후에도 계속됩니다. 데이터베이스는 실행 취소 단계 중에 사용할 수 있습니다.  
  
 ![오류 검색 및 장애 조치 시간](../media/dbm-failovauto-time.gif "오류 검색 및 장애 조치 시간")  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스 미러링 운영 모드](database-mirroring-operating-modes.md)   
 [데이터베이스 미러링 세션 중 역할 전환&#40;SQL Server&#41;](role-switching-during-a-database-mirroring-session-sql-server.md)   
 [데이터베이스 미러링 모니터링&#40;SQL Server&#41;](monitoring-database-mirroring-sql-server.md)  
  
  
