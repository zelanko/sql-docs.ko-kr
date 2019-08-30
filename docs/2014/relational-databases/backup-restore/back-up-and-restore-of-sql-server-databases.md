---
title: SQL Server 데이터베이스 백업 및 복원 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- disaster recovery [SQL Server], see restoring [SQL Server]
- backups [SQL Server]
- restoring databases [SQL Server]
- backup [SQL Server], see backing up [SQL Server]
- databases [SQL Server], restoring
- backing up databases [SQL Server]
- restore [SQL Server], see restoring [SQL Server]
- disaster recovery [SQL Server], see backing up [SQL Server]
- backing up [SQL Server]
- Database Engine [SQL Server], backups
- databases [SQL Server], backups
ms.assetid: 570a21b3-ad29-44a9-aa70-deb2fbd34f27
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3854b9b49435cf9db453527deaa9d427b04e6f74
ms.sourcegitcommit: 5e45cc444cfa0345901ca00ab2262c71ba3fd7c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2019
ms.locfileid: "70155091"
---
# <a name="back-up-and-restore-of-sql-server-databases"></a>SQL Server 데이터베이스 백업 및 복원
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 백업의 이점과 기본 백업 및 복원 용어에 대해 설명하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에 대한 백업 및 복원 전략과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원을 위한 보안 고려 사항에 대해 소개합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 및 복원 구성 요소는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 저장된 중요한 데이터를 보호하기 위한 필수 보호 방법을 제공합니다. 치명적인 데이터 손실 위험을 최소화하기 위해서는 데이터베이스를 정기적으로 백업하여 수정된 데이터를 유지해야 합니다. 백업 및 복원 전략을 적절하게 계획하면 다양한 오류로 인해 데이터베이스의 데이터가 손실되는 것을 방지할 수 있습니다. 일련의 백업 복원과 데이터베이스 복구를 통해 전략을 테스트하여 재해에 효과적으로 대처할 수 있습니다.  
  
 SQL Server는 백업을 저장 하기 위한 로컬 저장소 외에도 Azure Blob Storage 서비스에 대 한 백업과 복원도 지원 합니다. 자세한 내용은 [Azure Blob Storage 서비스를 사용 하 여 백업 및 복원 SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)를 참조 하세요.  
  

  
##  <a name="Benefits"></a> 이점  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 백업하고 백업에 대한 테스트 복원 절차를 실행한 다음 안전한 오프 사이트 위치에 백업을 저장하여 치명적인 데이터 손실을 방지할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  이렇게 하는 것이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 안정적으로 보호하는 유일한 방법입니다.  
  
     유효한 데이터베이스 백업을 사용하여 다음의 여러 오류로부터 데이터를 복구할 수 있습니다.  
  
    -   미디어 오류  
  
    -   사용자 오류(예: 실수로 테이블 삭제)  
  
    -   하드웨어 오류(예: 손상된 디스크 드라이브 또는 서버의 영구적 손실)  
  
    -   자연 재해 Azure Blob storage 서비스에 백업 SQL Server를 사용 하 여 온-프레미스 위치에 영향을 미치는 자연 재해가 발생할 경우에 사용할 오프 사이트 백업을 온-프레미스 위치와 다른 지역에 만들 수 있습니다.  
  
-   또한 데이터베이스 백업은 서버 간 데이터베이스 복사, [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 또는 데이터베이스 미러링 설정, 보관 등의 일상적인 관리 용도로 유용하게 사용할 수 있습니다.  
  

  
##  <a name="TermsAndDefinitions"></a> 구성 요소 및 개념  
 백업[동사]  
 데이터 또는 로그 레코드를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 해당 트랜잭션 로그에서 백업 디바이스(예: 디스크)로 복사하여 데이터 백업 또는 로그 백업을 만들 수 있습니다.  
  
 백업[명사]  
 오류가 발생한 이후에 데이터를 복원 및 복구하는 데 사용할 수 있는 데이터 복사본입니다. 데이터베이스 백업을 사용하여 데이터베이스 복사본을 새 위치에 복원할 수도 있습니다.  
  
 백업 디바이스(backup device)  
 SQL Server 백업이 기록되는 대상이자 백업을 복원하는 원본이 되는 디스크 또는 테이프 디바이스입니다. SQL Server 백업은 Azure Blob 저장소 서비스에 기록할 수도 있으며, **URL** 형식을 사용 하 여 백업 파일의 대상 및 이름을 지정 합니다. 자세한 내용은 [Azure Blob Storage 서비스를 사용 하 여 백업 및 복원 SQL Server](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)를 참조 하세요.  
  
 백업 미디어  
 하나 이상의 백업이 기록된 하나 이상의 테이프 또는 디스크 파일입니다.  
  
 데이터 백업(data backup)  
 전체 데이터베이스(데이터베이스 백업), 부분 데이터베이스(부분 백업) 또는 파일 집합이나 파일 그룹(파일 백업)의 데이터 백업입니다.  
  
 데이터베이스 백업(database backup)  
 데이터베이스 백업입니다. 전체 데이터베이스 백업은 백업이 완료된 시점의 전체 데이터베이스를 나타냅니다. 차등 데이터베이스 백업은 가장 최근의 전체 데이터베이스 백업 이후에 데이터베이스에 수행된 변경 내용만 포함합니다.  
  
 차등 백업(differential backup)  
 전체 또는 부분 데이터베이스, 데이터 파일 집합 또는 파일 그룹(차등 기반)에 대한 최신 전체 백업을 기반으로 하고, 해당 기준 이후에 변경된 데이터만 포함하는 데이터 백업입니다.  
  
 전체 백업(full backup)  
 특정 데이터베이스나 파일 그룹 또는 파일 집합에 있는 모든 데이터와 그러한 데이터를 복구할 수 있을 만큼의 로그를 포함하는 데이터 백업입니다.  
  
 로그 백업(log backup)  
 이전 로그 백업에서 백업되지 않은 모든 로그 레코드를 포함하는 트랜잭션 로그 백업입니다. (전체 복구 모델)  
  
 복구  
 데이터베이스를 안정적이고 일관된 상태로 되돌립니다.  
  
 recovery  
 데이터베이스를 일관된 트랜잭션 상태로 가져오는 데이터베이스 시작 단계 또는 restore with recovery 단계입니다.  
  
 복구 모델  
 데이터베이스에서 트랜잭션 로그 유지 관리를 제어하는 데이터베이스 속성입니다. 사용할 수 있는 복구 모델은 3가지로 단순, 전체 및 대량 로그 복구 모델입니다. 데이터베이스의 복구 모델에 따라 백업 및 복원 요구 사항이 결정됩니다.  
  
 복원(restore)  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에서 지정된 데이터베이스로 모든 데이터 및 로그 페이지를 복사하고 기록된 변경 사항을 적용하여 데이터를 최신 상태로 전환함으로써 백업에 기록된 모든 트랜잭션을 롤포워드하는 다단계 프로세스입니다.  
  

  
##  <a name="BnrStrategies"></a>백업 및 복원 전략 소개  
 데이터 백업 및 복원은 특정 환경에 맞게 사용자 지정되어야 하며 적절한 리소스도 마련되어야 합니다. 따라서 복구를 위해 백업 및 복원을 안정적으로 사용하려면 백업 및 복원 전략이 필요합니다. 잘 디자인된 백업 및 복원 전략은 사용자의 특정 비즈니스 요구 사항을 감안해 데이터 가용성을 극대화하고 데이터 손실을 최소화합니다.  
  
> [!IMPORTANT]  
>  데이터베이스와 백업을 서로 다른 디바이스에 배치하십시오. 그렇지 않으면 데이터베이스가 들어 있는 디바이스가 실패할 경우 백업을 사용할 수 없습니다. 데이터와 백업을 서로 다른 디바이스에 배치하면 백업 작성 및 데이터베이스의 프로덕션 사용에 대한 I/O 성능도 향상됩니다.  
  
 백업 및 복원 전략은 백업에 관련된 부분과 복원에 관련된 부분으로 이루어집니다. 전략의 백업 관련 부분에서는 백업 유형 및 빈도, 백업에 필요한 하드웨어의 특성 및 속도, 백업 테스트 방법 및 백업 미디어 보관 위치 및 보관 방법(보안 고려 사항 포함)을 정의합니다. 전략의 복원 관련 부분에서는 누가 복원을 담당할 것이며 어떻게 데이터베이스 가용성 목표를 충족시키고 데이터 손실을 최소화할 것인가를 정의합니다. 백업 및 복원 절차를 문서화하고 실행 문서에 사본을 보관하는 것이 좋습니다.  
  
 효과적인 백업 및 복원 전략 설계를 위해서는 신중한 계획, 구현 및 테스트가 필요합니다. 테스트는 반드시 필요합니다. 복원 전략에 포함된 모든 조합의 백업을 성공적으로 복원해야만 백업 전략을 갖추게 됩니다. 다음과 같은 다양한 요소를 여기에는 다음과 같은 옵션이 포함됩니다.  
  
-   데이터베이스에 대한 사용자 조직의 생산성 목표(특히 가용성 및 데이터 손실 방지 요구 사항)  
  
-   크기, 사용 패턴, 내용의 특성, 데이터 요구 사항 등과 같은 각 데이터베이스의 특성  
  
-   하드웨어, 인력, 백업 미디어 저장 공간, 저장된 미디어의 물리적 보안 등과 같은 리소스의 제약 요건  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 디스크상 저장소 형식은 64비트 및 32비트 환경에서 동일합니다. 따라서 32비트 및 64비트 환경에서 백업 및 복원 작업을 수행할 수 있습니다. 한 환경에서 실행 중인 서버 인스턴스에서 만든 백업을 다른 환경에서 실행하는 서버 인스턴스에서 복원할 수 있습니다.  
  

  
### <a name="impact-of-the-recovery-model-on-backup-and-restore"></a>백업 및 복원에 대한 복구 모델의 영향  
 백업 및 복원 작업은 복구 모델의 컨텍스트에서 수행됩니다. 복구 모델은 트랜잭션 로그의 관리 방법을 제어하는 데이터베이스 속성입니다. 또한 데이터베이스의 복구 모델은 데이터베이스에 지원되는 복원 시나리오 및 백업 유형을 결정합니다. 일반적으로 데이터베이스는 단순 복구 모델 또는 전체 복구 모델 모두 사용합니다. 전체 복구 모델은 대량 작업 이전에 대량 로그 복구 모델로 전환하여 보완될 수 있습니다. 이러한 복구 모델 및 이러한 복구 모델이 트랜잭션 로그 관리에 미치는 영향에 대한 자세한 내용은 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)를 참조하세요.  
  
 데이터베이스에 가장 적합한 복구 모델은 비즈니스 요구 사항에 따라 달라집니다. 트랜잭션 로그 관리를 방지하고 백업 및 복원을 단순화하려면 단순 복구 모델을 사용하십시오. 관리 오버헤드가 증가하더라도 작업 손실 가능성을 최소화하려면 전체 복구 모델을 사용하십시오. 백업 및 복원에 미치는 복구 모델의 영향에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)를 참조하세요.  
  
### <a name="design-the-backup-strategy"></a>백업 전략 디자인  
 지정한 데이터베이스에 대해 비즈니스 요구 사항에 맞는 복구 모델을 선택한 후에는 해당 백업 전략을 계획 및 구현해야 합니다. 백업 전략을 최적화하는 요소는 다양합니다. 그 중에서도 특히 다음과 같은 요소에 의해 주로 영향을 받습니다.  
  
-   애플리케이션이 하루에 몇 시간 데이터베이스에 액세스해야 합니까?  
  
     사용량이 적은 기간을 예측할 수 있는 경우 해당 기간에 전체 데이터베이스 백업을 예약하는 것이 좋습니다.  
  
-   얼마나 자주 변경과 업데이트가 발생합니까?  
  
     자주 변경하는 경우 다음을 고려하십시오.  
  
    -   단순 복구 모델에서는 전체 데이터베이스 백업 사이에 차등 백업을 예약하십시오. 차등 백업은 마지막 전체 데이터베이스 백업 이후의 변경 내용만 캡처합니다.  
  
    -   전체 복구 모델에서는 자주 로그 백업을 예약해야 합니다. 전체 백업 사이에 차등 백업을 예약하면 데이터를 복원한 후 복원해야 하는 로그 백업 수가 감소하므로 복원 시간이 줄어들 수 있습니다.  
  
-   변경이 데이터베이스의 일부분에서만 발생합니까? 아니면 데이터베이스의 대부분에서 발생합니까?  
  
     변경 내용이 파일 또는 파일 그룹의 일부분에만 집중되어 있는 큰 데이터베이스의 경우 부분 백업이나 파일 백업이 유용할 수 있습니다. 자세한 내용은 [부분 백업&#40;SQL Server&#41;](partial-backups-sql-server.md) 및 [전체 파일 백업&#40;SQL Server&#41;](full-file-backups-sql-server.md)을 참조하세요.  
  
-   전체 데이터베이스 백업에 필요한 디스크 공간은 어느 정도입니까?  
  
     자세한 내용은 이 항목의 뒷부분에 나오는 [전체 데이터베이스 백업의 크기 예측](#EstimateDbBuSize)을 참조하십시오.  
  
####  <a name="EstimateDbBuSize"></a>전체 데이터베이스 백업의 크기 예측  
 백업 및 복원을 구현하기 전에 전체 데이터베이스 백업에 어느 정도의 디스크 공간이 필요한지 예측해야 합니다. 백업 작업은 데이터베이스의 데이터를 백업 파일로 복사합니다. 백업에는 데이터베이스의 실제 데이터만 포함되고 사용하지 않은 공간은 포함되지 않습니다. 따라서 백업은 일반적으로 데이터베이스 자체의 크기보다 작습니다. **sp_spaceused** 시스템 저장 프로시저를 사용하여 전체 데이터베이스 백업의 크기를 예측할 수 있습니다. 자세한 내용은 [sp_spaceused&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)를 참조하세요.  
  
### <a name="schedule-backups"></a>백업 예약  
 백업 작업을 수행해도 실행 중인 트랜잭션에는 큰 영향을 미치지 않으므로 일반 작업을 수행할 때도 백업 작업을 실행할 수 있습니다. 프로덕션 작업에 거의 영향을 주지 않고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 수행할 수 있습니다.  
  
> [!NOTE]  
>  백업 중 동시성 제한 사항에 대한 자세한 내용은 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)을 참조하세요.  
  
 각 경우에 필요한 백업 유형과 수행 빈도를 결정한 후 데이터베이스 유지 관리 계획의 일부로 데이터베이스에 대한 정기 백업을 예약하는 것이 좋습니다. 유지 관리 계획에 대한 정보와 데이터베이스 백업 및 로그 백업에 대한 유지 관리 계획을 만드는 방법은 [Use the Maintenance Plan Wizard](../maintenance-plans/use-the-maintenance-plan-wizard.md)를 참조하십시오.  
  
### <a name="test-your-backups"></a>백업 테스트  
 백업을 테스트해야만 복원 전략을 갖추게 됩니다. 데이터베이스 복사본을 테스트 시스템으로 복원하여 각 데이터베이스에 대한 백업 전략을 철저히 테스트하는 것이 중요합니다. 사용할 모든 유형의 백업 복원을 테스트해야 합니다.  
  
 각 데이터베이스에 대한 작업 매뉴얼을 작성하여 관리하는 것이 좋습니다. 이 작업 매뉴얼에는 백업 위치, 백업 디바이스 이름(있는 경우) 및 테스트 백업을 복원하는 데 필요한 시간 등이 수록되어야 합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
### <a name="scheduling-backup-jobs"></a>백업 작업 예약  
  
-   [유지 관리 계획 만들기](../maintenance-plans/create-a-maintenance-plan.md)  
  
-   [작업 만들기](../../ssms/agent/create-a-job.md)  
  
-   [작업 예약](../../ssms/agent/schedule-a-job.md)  
  
### <a name="working-with-backup-devices-and-backup-media"></a>백업 디바이스 및 백업 미디어 사용  
  
-   [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [백업 장치 삭제&#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [백업의 만료 날짜 설정&#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [백업 세트의 데이터와 로그 파일 보기&#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [논리적 백업 장치의 속성 및 내용 보기&#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [장치에서 백업 복원&#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
### <a name="creating-backups"></a>백업 만들기  
  
> [!NOTE]  
>  부분 또는 복사 전용 백업의 경우 각각 PARTIAL 또는 COPY_ONLY 옵션과 함께 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) 문을 사용해야 합니다.  
  
 **SQL Server Management Studio 사용**  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
 **Transact-SQL 사용**  
  
-   [Resource GovernoR을 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [백업 또는 복원 중 백업 체크섬 설정 또는 해제&#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [오류 발생 후 백업 또는 복원 작업 계속 또는 중지 여부 지정&#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  

  
### <a name="restoring-data-backups"></a>데이터 백업 복원  
 **SQL Server Management Studio 사용**  
  
-   [데이터베이스 백업 &#40;SQL Server Management Studio 복원&#41;](restore-a-database-backup-using-ssms.md)  
  
-   [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](restore-a-database-to-a-new-location-sql-server.md)  
  
-   [차등 데이터베이스 백업 복원&#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)  
  
-   [파일 및 파일 그룹 복원&#40;SQL Server&#41;](restore-files-and-filegroups-sql-server.md)  
  
 **Transact-SQL 사용**  
  
-   [단순 복구 모델에서 데이터베이스 백업 복원&#40;Transact-SQL&#41;](restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](restore-database-to-point-of-failure-full-recovery.md)  
  
-   [기존 파일에서 파일 및 파일 그룹 복원&#40;SQL Server&#41;](restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
-   [새 위치로 파일 복원&#40;SQL Server&#41;](restore-files-to-a-new-location-sql-server.md)  
  
-   [master 데이터베이스 복원&#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  

  
### <a name="restoring-transaction-logs-full-recovery-model"></a>트랜잭션 로그 복원(전체 복구 모델)  
 **SQL Server Management Studio 사용**  
  
-   [데이터베이스를 표시된 트랜잭션으로 복원&#40;SQL Server Management Studio&#41;](restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)  
  
-   [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  
 **Transact-SQL 사용**  
  
-   [SQL Server 데이터베이스를 지정 시간으로 복원&#40;전체 복구 모델&#41;](restore-a-sql-server-database-to-a-point-in-time-full-recovery-model.md)  
  

  
### <a name="additional-restore-tasks"></a>추가 복원 태스크  
 **Transact-SQL 사용**  
  
-   [중단된 복원 작업 다시 시작&#40;Transact-SQL&#41;](restart-an-interrupted-restore-operation-transact-sql.md)  
  
-   [데이터를 복원하지 않고 데이터베이스 복구&#40;Transact-SQL&#41;](recover-a-database-without-restoring-data-transact-sql.md)  
  

  
## <a name="see-also"></a>관련 항목  
 [백업 개요&#40;SQL Server&#41;](backup-overview-sql-server.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [BACKUP&#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)   
 [Analysis Services 데이터베이스 백업 및 복원](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)   
 [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../search/back-up-and-restore-full-text-catalogs-and-indexes.md)   
 [복제된 데이터베이스 백업 및 복원](../replication/administration/back-up-and-restore-replicated-databases.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](recovery-models-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](media-sets-media-families-and-backup-sets-sql-server.md)  
  
  
