---
title: msdb 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 11/10/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, msdb database
- alerts [SQL Server], msdb database
- jobs [SQL Server], msdb database
- msdb database [SQL Server]
ms.assetid: 5032cb2d-65a0-40dd-b569-4dcecdd58ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cee4c5d802447488930ffd04d698edcd2015e86b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62871714"
---
# <a name="msdb-database"></a>msdb 데이터베이스
  **msdb** 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에서 경고 및 작업을 예약하는 데 사용되며 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSB](../../includes/sssb-md.md)] 및 데이터베이스 메일과 같은 다른 기능에서도 사용됩니다.  
  
 예를 들어 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 **msdb**의 테이블 내에서 완전한 온라인 백업과 복원 기록을 자동으로 유지 관리합니다. 이 정보에는 백업을 수행한 사람의 이름, 백업 시간 및 백업이 저장된 디바이스나 파일이 포함됩니다. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서는 이 정보를 사용하여 데이터베이스 복원 및 트랜잭션 로그 백업 적용에 관한 계획을 제안합니다. 사용자 지정 애플리케이션이나 타사의 도구로 만든 백업 이벤트를 비롯하여 모든 데이터베이스에 대한 백업 이벤트가 기록됩니다. 예를 들어 SMO(SQL Server Management Objects) 개체를 호출하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] 응용 프로그램을 사용하여 백업 작업을 실행한 경우 이벤트는 **msdb** 시스템 테이블, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 응용 프로그램 로그, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그에 기록됩니다. **msdb**에 저장된 정보를 보호하기 위해서는 **msdb** 트랜잭션 로그를 내결함성이 있는 저장소에 보관하는 것이 좋습니다.  
  
 기본적으로 **msdb** 는 단순 복구 모델을 사용합니다. [백업 및 복원 기록](../backup-restore/backup-history-and-header-information-sql-server.md) 테이블을 사용하는 경우 **msdb**에 대한 전체 복구 모델을 사용하는 것이 좋습니다. 자세한 내용은 [복구 모델&#40;SQL Server&#41;](../backup-restore/recovery-models-sql-server.md)을 참조하세요. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 설치 또는 업그레이드할 때 Setup.exe를 사용하여 시스템 데이터베이스를 다시 작성할 때마다 **msdb** 의 복구 모델이 자동으로 단순 복구 모델로 설정됩니다.  
  
> [!IMPORTANT]  
>  데이터베이스 백업 또는 복원과 같은 **msdb**업데이트 작업을 수행한 후에는 **msdb**를 백업하는 것이 좋습니다. 자세한 내용은 [시스템 데이터베이스 백업 및 복원&#40;SQL Server&#41](../backup-restore/back-up-and-restore-of-system-databases-sql-server.md)를 참조하세요.  
  
## <a name="physical-properties-of-msdb"></a>msdb의 물리적 속성  
 다음 표에서는 **msdb** 데이터와 로그 파일의 초기 구성 값을 나열합니다. 이러한 파일의 크기는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]버전에 따라 조금씩 다를 수 있습니다.  
  
|파일|논리적 이름|물리적 이름|파일 증가|  
|----------|------------------|-------------------|-----------------|  
|주 데이터|MSDBData|MSDBData.mdf|디스크가 꽉 찰 때까지 10%씩 자동 증가|  
|Log|MSDBLog|MSDBLog.ldf|최대 2TB까지 10%씩 자동 증가|  
  
 **msdb** 데이터베이스나 로그 파일을 이동하려면 [시스템 데이터베이스 이동](move-system-databases.md)을 참조하세요.  
  
### <a name="database-options"></a>데이터베이스 옵션  
 다음 표에서는 **msdb** 데이터베이스의 각 데이터베이스 옵션에 대한 기본값과 수정 가능 여부를 나열합니다. 이러한 옵션의 현재 설정을 보려면 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 카탈로그 뷰를 사용하세요.  
  
|데이터베이스 옵션|기본값|수정 가능|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|ON|아니요|  
|ANSI_NULL_DEFAULT|OFF|사용자 계정 컨트롤|  
|ANSI_NULLS|OFF|사용자 계정 컨트롤|  
|ANSI_PADDING|OFF|사용자 계정 컨트롤|  
|ANSI_WARNINGS|OFF|사용자 계정 컨트롤|  
|ARITHABORT|OFF|사용자 계정 컨트롤|  
|AUTO_CLOSE|OFF|사용자 계정 컨트롤|  
|AUTO_CREATE_STATISTICS|ON|사용자 계정 컨트롤|  
|AUTO_SHRINK|OFF|사용자 계정 컨트롤|  
|AUTO_UPDATE_STATISTICS|ON|사용자 계정 컨트롤|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|사용자 계정 컨트롤|  
|CHANGE_TRACKING|OFF|아니요|  
|CONCAT_NULL_YIELDS_NULL|OFF|사용자 계정 컨트롤|  
|CURSOR_CLOSE_ON_COMMIT|OFF|사용자 계정 컨트롤|  
|CURSOR_DEFAULT|GLOBAL|사용자 계정 컨트롤|  
|데이터베이스 가용성 옵션|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|아니요<br /><br /> 예<br /><br /> 사용자 계정 컨트롤|  
|DATE_CORRELATION_OPTIMIZATION|OFF|사용자 계정 컨트롤|  
|DB_CHAINING|ON|사용자 계정 컨트롤|  
|ENCRYPTION|OFF|아니요|  
|NUMERIC_ROUNDABORT|OFF|사용자 계정 컨트롤|  
|PAGE_VERIFY|CHECKSUM|사용자 계정 컨트롤|  
|PARAMETERIZATION|SIMPLE|사용자 계정 컨트롤|  
|QUOTED_IDENTIFIER|OFF|사용자 계정 컨트롤|  
|READ_COMMITTED_SNAPSHOT|OFF|아니요|  
|RECOVERY|SIMPLE|사용자 계정 컨트롤|  
|RECURSIVE_TRIGGERS|OFF|사용자 계정 컨트롤|  
|Service Broker 옵션|ENABLE_BROKER|사용자 계정 컨트롤|  
|TRUSTWORTHY|ON|사용자 계정 컨트롤|  
  
 이러한 데이터베이스 옵션에 대한 자세한 내용은 [ALTER DATABASE&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)를 참조하세요.  
  
## <a name="restrictions"></a>Restrictions  
 **msdb** 데이터베이스에서는 다음 작업을 수행할 수 없습니다.  
  
-   데이터 정렬 변경. 기본 데이터 정렬은 서버 데이터 정렬입니다.  
  
-   데이터베이스 삭제  
  
-   데이터베이스에서 **guest** 사용자 삭제  
  
-   변경 데이터 캡처 설정  
  
-   데이터베이스 미러링 참여  
  
-   주 파일 그룹, 주 데이터 파일 또는 로그 파일 제거  
  
-   데이터베이스 또는 주 파일 그룹 이름 바꾸기  
  
-   데이터베이스를 OFFLINE으로 설정  
  
-   주 파일 그룹을 READ_ONLY로 설정  
  
## <a name="related-content"></a>관련 내용  
 [시스템 데이터베이스](system-databases.md)  
  
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [데이터베이스 파일 이동](move-database-files.md)  
  
 [데이터베이스 메일](../database-mail/database-mail.md)  
  
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
