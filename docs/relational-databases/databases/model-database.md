---
title: model 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- template databases [SQL Server]
- model database [SQL Server], about model databases
- model database [SQL Server]
ms.assetid: 4e4f739b-fd27-4dce-8be6-3d808040d8d7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9febf511aef30bde1b01a5cad8eba3e3f8845b2f
ms.sourcegitcommit: eb1f3a2f5bc296f74545f17d20c6075003aa4c42
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2018
ms.locfileid: "52191033"
---
# <a name="model-database"></a>model 데이터베이스
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **model** 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 생성된 모든 데이터베이스에 대한 템플릿으로 사용됩니다. **을(를) 시작할 때마다** tempdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 생성되기 때문에 **model** 데이터베이스는 항상 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템에 있어야 합니다. 데이터베이스 옵션을 포함한 **model** 데이터베이스의 전체 내용이 새 데이터베이스에 복사됩니다. 또한 **model** 의 일부 설정이 시작되는 동안 새 **tempdb** 를 만드는 데 사용되므로 **시스템에 항상** model [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스가 있어야 합니다.  
  
 새로 만든 사용자 데이터베이스는 model 데이터베이스와 같은 [복구 모델](../../relational-databases/backup-restore/recovery-models-sql-server.md) 을 사용합니다. 기본값은 사용자 구성입니다. 모델의 현재 복구 모델에 대한 자세한 내용은 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  사용자별 템플릿 정보를 사용하여 **model** 데이터베이스를 수정하는 경우 **model**을 백업하는 것이 좋습니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요.  
  
## <a name="model-usage"></a>model 사용  
 CREATE DATABASE 문을 실행하면 **model** 데이터베이스의 내용을 복사하여 데이터베이스의 첫 번째 부분이 생성됩니다. 그런 다음 새 데이터베이스의 나머지 부분이 빈 페이지로 채워집니다.  
  
 **model** 데이터베이스를 수정하면 해당 변경 내용이 나중에 생성되는 모든 데이터베이스에 상속됩니다. 예를 들어 사용 권한 또는 데이터베이스 옵션을 설정하거나 테이블, 함수 또는 저장 프로시저 같은 개체를 추가할 수 있습니다. **model** 데이터베이스의 파일 속성은 예외이며 데이터 파일의 처음 크기를 제외하고 무시됩니다. model 데이터베이스 데이터 및 로그 파일의 기본 초기 크기는 8MB입니다.  
  
## <a name="physical-properties-of-model"></a>model의 물리적 속성  
 다음 표에서는 **model** 데이터와 로그 파일의 초기 구성 값을 나열합니다.  
  
|파일|논리적 이름|물리적 이름|파일 증가|  
|----------|------------------|-------------------|-----------------|  
|주 데이터|modeldev|model.mdf|디스크가 꽉 찰 때까지 64MB씩 자동 증가|  
|Log|modellog|modellog.ldf|최대 2TB까지 64MB씩 자동 증가|  

SQL Server 2014의 경우 기본 파일 증가 값은 [model 데이터베이스](https://docs.microsoft.com/sql/relational-databases/databases/model-database?view=sql-server-2014)를 참조하세요.  

 **model** 데이터베이스나 로그 파일을 이동하려면 [시스템 데이터베이스 이동](../../relational-databases/databases/move-system-databases.md)을 참조하세요.  
  
### <a name="database-options"></a>데이터베이스 옵션  
 다음 표에서는 **model** 데이터베이스의 각 데이터베이스 옵션에 대한 기본값과 수정 가능 여부를 나열합니다. 이러한 옵션의 현재 설정을 보려면 [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) 카탈로그 뷰를 사용하세요.  
  
|데이터베이스 옵션|기본값|수정 가능|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|예|  
|ANSI_NULL_DEFAULT|OFF|예|  
|ANSI_NULLS|OFF|예|  
|ANSI_PADDING|OFF|예|  
|ANSI_WARNINGS|OFF|예|  
|ARITHABORT|OFF|예|  
|AUTO_CLOSE|OFF|예|  
|AUTO_CREATE_STATISTICS|ON|예|  
|AUTO_SHRINK|OFF|예|  
|AUTO_UPDATE_STATISTICS|ON|예|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|예|  
|CHANGE_TRACKING|OFF|아니오|  
|CONCAT_NULL_YIELDS_NULL|OFF|예|  
|CURSOR_CLOSE_ON_COMMIT|OFF|예|  
|CURSOR_DEFAULT|GLOBAL|예|  
|데이터베이스 가용성 옵션|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|아니오<br /><br /> 예<br /><br /> 예|  
|DATE_CORRELATION_OPTIMIZATION|OFF|예|  
|DB_CHAINING|OFF|아니오|  
|ENCRYPTION|OFF|아니오|  
|MIXED_PAGE_ALLOCATION|ON|아니오|  
|NUMERIC_ROUNDABORT|OFF|예|  
|PAGE_VERIFY|CHECKSUM|예|  
|PARAMETERIZATION|SIMPLE|예|  
|QUOTED_IDENTIFIER|OFF|예|  
|READ_COMMITTED_SNAPSHOT|OFF|예|  
|RECOVERY|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에 따라 다름*|예|  
|RECURSIVE_TRIGGERS|OFF|예|  
|Service Broker 옵션|DISABLE_BROKER|아니오|  
|TRUSTWORTHY|OFF|아니오|  
  
 *데이터베이스의 현재 복구 모델을 확인하려면 [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](../../relational-databases/backup-restore/view-or-change-the-recovery-model-of-a-database-sql-server.md) 또는 [sys.databases&#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)를 참조하세요.  
  
 이러한 데이터베이스 옵션에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
## <a name="restrictions"></a>Restrictions  
 **model** 데이터베이스에서는 다음 작업을 수행할 수 없습니다.  
  
-   파일이나 파일 그룹 추가  
  
-   데이터 정렬 변경. 기본 데이터 정렬은 서버 데이터 정렬입니다.  
  
-   데이터베이스 소유자 변경. **model** 은 **sa**가 소유합니다.  
  
-   데이터베이스 삭제  
  
-   데이터베이스에서 **guest** 사용자 삭제  
  
-   변경 데이터 캡처 설정  
  
-   데이터베이스 미러링 참여  
  
-   주 파일 그룹, 주 데이터 파일 또는 로그 파일 제거  
  
-   데이터베이스 또는 주 파일 그룹 이름 바꾸기  
  
-   데이터베이스를 OFFLINE으로 설정  
  
-   주 파일 그룹을 READ_ONLY로 설정  
  
-   WITH ENCRYPTION 옵션을 사용하여 프로시저, 뷰 또는 트리거 생성. 암호화 키는 개체가 생성되는 데이터베이스에 연결됩니다. **model** 데이터베이스에 생성된 암호화된 개체는 **model**에서만 사용할 수 있습니다.  
  
## <a name="related-content"></a>관련 내용  
 [시스템 데이터베이스](../../relational-databases/databases/system-databases.md)  
  
 [sys.databases&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)  
  
 [sys.master_files&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
 [데이터베이스 파일 이동](../../relational-databases/databases/move-database-files.md)  
  
  
