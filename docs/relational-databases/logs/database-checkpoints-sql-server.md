---
title: 데이터베이스 검사점(SQL Server) | Microsoft 문서
ms.date: 09/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic checkpoints
- transaction logs [SQL Server], checkpoints
- logs [SQL Server], active
- pages [SQL Server], dirty
- MinLSN
- checkpoints [SQL Server]
- pages [SQL Server], flushing
- dirty pages
- transaction logs [SQL Server], active logs
- recovery interval option [SQL Server]
- buffer cache [SQL Server]
- logs [SQL Server], checkpoints
- Minimum Recovery LSN
- flushing pages
- active logs
ms.assetid: 98a80238-7409-4708-8a7d-5defd9957185
caps.latest.revision: 74
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 47d7bec624955627f8c486827b9515da7d56ecf6
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2018
ms.locfileid: "39560973"
---
# <a name="database-checkpoints-sql-server"></a>데이터베이스 검사점(SQL Server)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
 *검사점* 은 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 이 예기치 않은 종료 또는 충돌 후 복구하는 과정에서 로그에 포함된 변경 내용의 적용을 시작할 수 있는 알려진 올바른 지점을 만듭니다.  
 
  
##  <a name="Overview"></a> 개요   
성능상의 이유로 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 변경 내용이 있을 때마다 메모리(버퍼 캐시)에서 데이터베이스 페이지를 수정하며 이러한 페이지를 디스크에 기록하지는 않습니다. 대신 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 각 데이터베이스에서 정기적으로 검사점을 실행합니다. *검사점* 은 현재 메모리 내의 수정된 페이지( *더티 페이지*라고 함)와 메모리의 트랜잭션 로그 정보를 디스크에 쓰고 트랜잭션 로그에 대한 정보도 기록합니다.  
  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 자동, 간접, 수동 및 내부와 같은 여러 가지 유형의 검사점이 지원됩니다. 다음 표에는 **검사점**의 유형이 요약되어 있습니다.
  
|속성|[!INCLUDE[tsql](../../includes/tsql-md.md)] 인터페이스|설명|  
|----------|----------------------------------|-----------------|  
|자동|EXEC sp_configure **'** 복구 간격 **','***초***'**|**recovery interval** 서버 구성 옵션에 제안된 최대 제한 시간에 맞게 백그라운드에서 자동으로 실행됩니다. 자동 검사점은 완료될 때까지 실행됩니다.  자동 검사점은 진행 중인 쓰기 작업의 수와 쓰기 지연 시간이 50밀리초 이상으로 증가할 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 이를 감지하는지에 따라 제한됩니다.<br /><br /> 자세한 내용은 [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)을(를) 참조하세요.|  
|간접|ALTER DATABASE … SET TARGET_RECOVERY_TIME **=***target_recovery_time* { SECONDS &#124; MINUTES }|지정된 데이터베이스의 사용자 지정 대상 복구 시간에 맞게 백그라운드에서 실행됩니다. [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]부터 기본값은 1분입니다. 이전 버전의 기본값 0은 데이터베이스가 자동 검사점을 사용함을 나타내며, 빈도는 서버 인스턴스의 복구 간격 설정에 따라 달라집니다.<br /><br /> 자세한 내용은 [데이터베이스의 대상 복구 시간 변경&#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)을(를) 참조하세요.|  
|수동|CHECKPOINT[*checkpoint_duration*]|[!INCLUDE[tsql](../../includes/tsql-md.md)] CHECKPOINT 명령을 실행할 때 실행됩니다. 수동 검사점은 현재 연결된 데이터베이스에서 발생합니다. 기본적으로 수동 검사점은 완료될 때까지 실행됩니다. 또한 자동 검사점의 경우와 동일한 방식으로 조절됩니다.  필요한 경우 *checkpoint_duration* 매개 변수는 수동 검사점을 완료하는 데 필요한 시간(초)을 지정합니다.<br /><br /> 자세한 내용은 [CHECKPOINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)을(를) 참조하세요.|  
|내부|없음|디스크 이미지가 현재 로그 상태와 일치하도록 하는 백업 및 데이터베이스 스냅숏 생성 등의 다양한 서버 작업에 의해 실행됩니다.|  
  
> [!NOTE]
> 데이터베이스 관리자는 일부 유형의 검사점에 대해 **-k** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 고급 설정 옵션을 사용하여 I/O 하위 시스템의 처리량에 따라 검사점 I/O 동작을 제한할 수 있습니다. **-k** 설정 옵션은 자동 검사점과 그 밖의 조절되지 않는 모든 수동 및 내부 검사점에 적용됩니다.  
  
 자동, 수동 및 내부 검사점의 경우 데이터베이스 복구 중에는 마지막 검사점 다음에 수정된 내용만 롤포워드해야 합니다. 이렇게 하면 데이터베이스를 복구하는 데 필요한 시간이 줄어듭니다.  
  
> [!IMPORTANT]
> 커밋되지 않은 장기 실행 트랜잭션의 경우 모든 검사점 유형에 대해 복구 시간이 늘어납니다.   
  
##  <a name="InteractionBwnSettings"></a> TARGET_RECOVERY_TIME 옵션과 'recovery interval' 옵션의 상호 작용  
 다음 테이블에서는 서버 차원의 **sp_configure'** 복구 간격 **'** 설정과 데이터베이스별 ALTER DATABASE …간의 상호 작용을 요약합니다. TARGET_RECOVERY_TIME 설정 간의 상호 작용을 간략하게 보여 줍니다.  
  
|target_recovery_time|'recovery interval'|사용되는 검사점 유형|  
|----------------------------|-------------------------|-----------------------------|  
|0|0|대상 복구 간격이 1분인 자동 검사점|  
|0|>0|대상 복구 간격이 **sp_configure 복구 간격** 옵션의 사용자 정의 설정에 의해 지정되는 자동 검사점|  
|>0|이 오류에는 이 작업을 적용할 수 없습니다.|대상 복구 간격이 TARGET_RECOVERY_TIME 설정에 의해 초 단위로 결정되는 간접 검사점|  
  
##  <a name="AutomaticChkpt"></a> 자동 검사점  
자동 검사점은 로그 레코드의 수가 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 **복구 간격** 서버 구성 옵션에 지정된 시간 동안 처리할 수 있을 것으로 예상하는 수에 도달할 때마다 발생합니다. 자세한 내용은 [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)을(를) 참조하세요.
 
사용자 정의 대상 복구 시간이 없는 모든 데이터베이스에서 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 자동 검사점을 생성합니다. 빈도는 특정 서버 인스턴스에서 시스템을 다시 시작하는 동안 데이터베이스를 복구하는 데 사용해야 하는 최대 시간을 지정하는 **복구 간격** 고급 서버 구성 옵션에 따라 달라집니다. [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서는 복구 간격 내에 처리할 수 있는 최대 로그 레코드 수를 예상합니다. 자동 검사점을 사용하는 데이터베이스가 이 최대 로그 레코드 수에 도달하면 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 이 데이터베이스에 대해 검사점을 실행합니다. 
 
자동 검사점 사이의 시간 간격은 **매우** 가변적일 수 있습니다. 트랜잭션 작업이 많은 데이터베이스는 읽기 전용 작업에 주로 사용되는 데이터베이스보다 검사점이 더 많습니다. 단순 복구 모델에서 자동 검사점은 로그의 70%가 찬 경우에도 큐에 들어갑니다.  
  
단순 복구 모델에서는 어떤 요인으로 인해 로그 잘림이 지연되지 않는 한 자동 검사점에 의해 트랜잭션 로그의 사용되지 않는 부분이 잘립니다. 반면 전체 및 대량 로그된 복구 모델에서 로그 백업 체인이 설정된 후에는 자동 검사점에 의해 로그 잘림이 발생하지 않습니다. 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)을(를) 참조하세요.  
  
시스템 충돌이 발생한 후 특정 데이터베이스를 복구하는 데 필요한 시간은 충돌 시 더티 상태였던 페이지를 다시 실행하는 데 필요한 임의 I/O의 양에 따라 크게 달라집니다. 따라서 **recovery interval** 설정은 안정적이지 않으며 정확한 복구 기간을 결정할 수 없습니다. 또한 자동 검사점이 진행 중일 때는 데이터에 대한 일반적인 I/O 작업이 예측할 수 없게 상당히 늘어납니다.  
   
###  <a name="PerformanceImpact"></a> 복구 간격이 복구 성능에 미치는 영향  
짧은 트랜잭션을 사용하는 OLTP(온라인 트랜잭션 처리) 시스템의 경우 **복구 간격** 은 복구 시간을 결정하는 기본 요소입니다. 그러나 **복구 간격** 옵션은 장기 실행 트랜잭션의 실행을 취소하는 데 필요한 시간에는 영향을 주지 않습니다. 장기 실행 트랜잭션이 있는 데이터베이스를 복구하는 데는 **복구 간격** 옵션에 지정된 것보다 오랜 시간이 걸릴 수 있습니다. 
 
예를 들어 서버 인스턴스가 비활성화되기 전에 장기 실행 트랜잭션에서 업데이트를 수행하는 데 2시간이 걸렸었다면 장기 실행 트랜잭션을 복구하기 위한 실제 복구 시간은 **복구 간격** 값보다 훨씬 길어집니다. 장기 실행 트랜잭션이 복구 시간에 미치는 영향에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)을(를) 참조하세요.  
  
일반적으로 기본값은 최적의 복구 성능을 제공합니다. 그러나 다음과 같은 경우에는 복구 간격을 변경하면 성능이 향상될 수 있습니다.  
  
-   장기 실행 트랜잭션이 롤백되고 있지 않은 상태에서 복구하는 데 통상 1분이 훨씬 넘게 걸리는 경우  
  
-   검사점이 많아 데이터베이스의 성능이 저하되고 있음을 발견한 경우  
  
**recovery interval** 설정을 늘리려는 경우에는 값을 조금씩 늘려가며 그에 따라 복구 성능에 미치는 영향을 확인하는 것이 좋습니다. **recovery interval** 설정이 늘어나면 데이터베이스 복구를 완료하는 데 몇 배 더 긴 시간이 걸릴 수 있으므로 이 방법은 중요합니다. 예를 들어 **복구 간격** 을 10분으로 변경하면 **복구 간격** 이 1분으로 설정되었을 때보다 복구를 완료하는 데 약 10배 더 많은 시간이 걸립니다.  
  
##  <a name="IndirectChkpt"></a> 간접 검사점  
[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]에 도입된 간접 검사점은 자동 검사점 대신 사용할 수 있는 구성 가능한 데이터베이스 수준 검사점을 제공합니다. **대상 복구 시간** 데이터베이스 구성 옵션을 지정하여 구성할 수 있습니다. 자세한 내용은 [데이터베이스의 대상 복구 시간 변경&#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)서버 구성 옵션을 구성하는 방법에 대해 설명합니다.
시스템이 충돌할 경우 간접 검사점을 사용하면 자동 검사점을 사용할 때보다 복구 시간이 빠르고 보다 예측 가능합니다. 간접 검사점은 다음과 같은 이점을 제공합니다.  
  
-   간접 검사점이 구성된 데이터베이스의 온라인 트랜잭션 작업으로 인해 성능이 저하될 수 있습니다. 간접 검사점은 데이터베이스 복구가 대상 복구 시간 내에 완료되도록 더티 페이지 수가 특정 임계값보다 적어야 합니다. 

  **복구 간격** 구성 옵션은 더티 페이지 수를 사용하는 **간접 검사점**과 달리 트랜잭션 수를 사용하여 복구 시간을 결정합니다. 많은 수의 DML 작업을 수신하는 데이터베이스에서 간접 검사점을 사용하도록 설정하는 경우 복구 수행에 필요한 시간이 데이터베이스의 대상 복구 시간 설정 내로 유지되도록 백그라운드 기록기가 더티 버퍼를 디스크로 적극적으로 플러시하기 시작할 수 있습니다. 이로 인해 특정 시스템에서 추가 I/O 작업이 발생할 수 있으므로 디스크 하위 시스템이 I/O 임계값 위에서 또는 근처에서 작동하는 경우 성능 병목 현상에 영향을 줄 수 있습니다.  
  
-   간접 검사점을 사용하면 REDO 동안의 임의 I/O 비용을 줄여 데이터베이스 복구 시간을 안정적으로 제어할 수 있습니다. 이를 통해 서버 인스턴스를 특정 데이터베이스의 복구 시간 상한 내로 유지할 수 있습니다. 장기 실행 트랜잭션으로 인해 UNDO 시간이 과도하게 길어지는 경우에는 예외입니다.  
  
-   간접 검사점은 백그라운드에서 더티 페이지를 디스크에 계속 기록하여 검사점 관련 I/O의 급격한 증가를 줄여 줍니다.  
  
그러나 간접 검사점이 구성된 데이터베이스의 온라인 트랜잭션 작업으로 인해 성능이 저하될 수 있습니다. 이는 간접 검사점에 사용되는 백그라운드 기록기로 인해 서버 인스턴스에 대한 총 쓰기 부하가 늘어날 수 있기 때문입니다.  
 
> [!IMPORTANT]
> 간접 검사점은 Model 및 TempDB 데이터베이스를 포함해 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]에서 만든 새 데이터베이스에 대한 기본 동작입니다.          
> 현재 위치에서 업그레이드되었거나 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원된 데이터베이스는 명시적으로 간접 검사점을 사용하도록 변경되지 않은 경우 이전의 자동 검사점 동작을 사용합니다.       
  
##  <a name="EventsCausingChkpt"></a> 내부 검사점  
내부 검사점은 디스크 이미지가 현재 로그 상태와 일치하도록 다양한 서버 구성 요소에서 생성됩니다. 내부 검사점은 다음 이벤트에 대한 응답으로 생성됩니다.  
  
-   ALTER DATABASE를 사용하여 데이터베이스 파일을 추가 또는 제거한 경우  
  
-   데이터베이스를 백업한 경우  
  
-   DBCC CHECK를 위해 명시적으로 또는 내부적으로 데이터베이스 스냅숏이 생성된 경우  
  
-   데이터베이스를 종료해야 하는 작업을 수행한 경우. AUTO_CLOSE가 ON이고 데이터베이스에 대한 마지막 사용자 연결이 닫힌 경우 또는 데이터베이스를 다시 시작해야 하는 데이터베이스 옵션 변경을 수행한 경우를 예로 들 수 있습니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 서비스를 중지하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 중지된 경우. 두 동작은 모두 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 각 데이터베이스에 검사점을 설정합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] FCI(장애 조치(Failover) 클러스터 인스턴스)를 오프라인으로 전환한 경우      
  
##  <a name="RelatedTasks"></a> 관련 작업  
 **서버 인스턴스의 복구 간격을 변경하려면**  
  
-   [Configure the recovery interval Server Configuration Option](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md)  
  
 **데이터베이스에 간접 검사점을 구성하려면**  
  
-   [데이터베이스의 대상 복구 시간 변경&#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)  
  
 **데이터베이스에서 수동 검사점을 실행하려면**  
  
-   [CHECKPOINT&#40;Transact-SQL&#41;](../../t-sql/language-elements/checkpoint-transact-sql.md)  

  
## <a name="see-also"></a>관련 항목:  
[트랜잭션 로그&#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)            
[트랜잭션 로그 물리 아키텍처](http://technet.microsoft.com/library/ms179355.aspx) ( [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 온라인 설명서, 계속 적용!)       
  
  
