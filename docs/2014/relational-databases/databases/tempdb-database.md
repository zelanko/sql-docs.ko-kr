---
title: tempdb 데이터베이스 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- temporary tables [SQL Server], tempdb database
- tempdb database [SQL Server], about tempdb
- temporary stored procedures [SQL Server]
- tempdb database [SQL Server]
ms.assetid: ce4053fb-e37a-4851-b711-8e504059a780
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0b1265d3ef58f6ef0946937b15411b0cb79a3c20
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62916893"
---
# <a name="tempdb-database"></a>tempdb 데이터베이스
  **tempdb** 시스템 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결된 모든 사용자가 사용할 수 있는 전역 리소스로서 다음 항목을 보관하는 데 사용됩니다.  
  
-   전역 또는 로컬 임시 테이블, 임시 저장 프로시저, 테이블 변수, 커서 등 명시적으로 생성된 임시 사용자 개체  
  
-   스풀 또는 정렬의 중간 결과를 저장하기 위한 작업 테이블 등 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 만든 내부 개체  
  
-   행 버전 관리 격리를 사용하여 커밋된 읽기 또는 스냅샷 격리 트랜잭션을 사용하는 데이터베이스의 데이터 수정 트랜잭션에서 생성된 행 버전  
  
-   온라인 인덱스 작업, MARS(Multiple Active Result Sets) 및 AFTER 트리거 같은 기능에 대한 데이터 수정 트랜잭션에서 생성된 행 버전  
  
 **tempdb** 내의 작업은 최소한으로 기록됩니다. 이렇게 하면 트랜잭션을 롤백할 수 있습니다. **tempdb** 시스템이 항상 깨끗 한 데이터베이스 복사본으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시작 되도록를 시작할 때마다 tempdb가 다시 생성 됩니다. 연결이 끊길 때 임시 테이블 및 저장 프로시저는 자동으로 제거되고 시스템이 종료될 때 활성 상태인 연결이 없습니다. 따라서 **tempdb** 에는 한 세션에서 다른 세션 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 으로 저장 하는 것이 없습니다. **tempdb**에서는 백업 및 복원 작업이 허용되지 않습니다.  
  
## <a name="physical-properties-of-tempdb"></a>tempdb의 물리적 속성  
 다음 표에는 **tempdb** 데이터 및 로그 파일의 초기 구성 값이 나열되어 있습니다. 이러한 파일의 크기는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에 따라 조금씩 다를 수 있습니다.  
  
|파일|논리적 이름|물리적 이름|파일 증가|  
|----------|------------------|-------------------|-----------------|  
|주 데이터|tempdev|tempdb.mdf|디스크가 꽉 찰 때까지 10%씩 자동 증가|  
|로그|templog|templog.ldf|최대 2TB까지 10%씩 자동 증가|  
  
 **Tempdb** 의 크기는 시스템의 성능에 영향을 줄 수 있습니다. 예를 들어 **tempdb** 크기가 너무 작은 경우 시작할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]때마다 워크 로드 요구 사항을 지원 하기 위해 데이터베이스를 자동 증가 시키기 때문에 시스템 처리에 너무 많은 시간이 걸릴 수 있습니다. **Tempdb**의 크기를 늘려서 이러한 오버 헤드를 방지할 수 있습니다.  
  
## <a name="performance-improvements-in-tempdb"></a>tempdb의 성능 향상  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 다음과 같은 방법으로 **tempdb** 의 성능이 향상됩니다.  
  
-   임시 테이블과 테이블 변수를 캐시할 수 있습니다. 캐싱을 사용하면 임시 개체를 삭제하고 만드는 작업이 매우 신속하게 실행되며 페이지 할당 경합이 줄어듭니다.  
  
-   할당 페이지 래치 프로토콜이 향상되어 사용되는 UP(업데이트) 래치 수가 줄어듭니다.  
  
-   **tempdb** 에 대한 로깅 오버헤드가 감소하여 **tempdb** 로그 파일의 디스크 I/O 대역폭 사용이 줄어듭니다.  
  
-   **Tempdb** 에서 혼합 페이지를 할당 하는 알고리즘이 향상 되었습니다.  
  
### <a name="moving-the-tempdb-data-and-log-files"></a>tempdb 데이터 및 로그 파일 이동  
 **Tempdb** 데이터 및 로그 파일을 이동 하려면 [시스템 데이터베이스 이동](system-databases.md)을 참조 하세요.  
  
### <a name="database-options"></a>데이터베이스 옵션  
 다음 표에서는 **tempdb** 데이터베이스의 각 데이터베이스 옵션에 대 한 기본값과 옵션을 수정할 수 있는지 여부를 나열 합니다. 이러한 옵션의 현재 설정을 보려면 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql) 카탈로그 뷰를 사용하세요.  
  
|데이터베이스 옵션|기본값|수정 가능|  
|---------------------|-------------------|---------------------|  
|ALLOW_SNAPSHOT_ISOLATION|OFF|예|  
|ANSI_NULL_DEFAULT|OFF|예|  
|ANSI_NULLS|OFF|예|  
|ANSI_PADDING|OFF|예|  
|ANSI_WARNINGS|OFF|예|  
|ARITHABORT|OFF|예|  
|AUTO_CLOSE|OFF|아니요|  
|AUTO_CREATE_STATISTICS|켜기|예|  
|AUTO_SHRINK|OFF|아니요|  
|AUTO_UPDATE_STATISTICS|켜기|예|  
|AUTO_UPDATE_STATISTICS_ASYNC|OFF|예|  
|CHANGE_TRACKING|OFF|예|  
|CONCAT_NULL_YIELDS_NULL|OFF|예|  
|CURSOR_CLOSE_ON_COMMIT|OFF|예|  
|CURSOR_DEFAULT|GLOBAL|예|  
|데이터베이스 가용성 옵션|ONLINE<br /><br /> MULTI_USER<br /><br /> READ_WRITE|아니요<br /><br /> 아니요<br /><br /> 아니요|  
|DATE_CORRELATION_OPTIMIZATION|OFF|예|  
|DB_CHAINING|켜기|예|  
|ENCRYPTION|OFF|예|  
|NUMERIC_ROUNDABORT|OFF|예|  
|PAGE_VERIFY|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]새 설치의 경우 CHECKSUM입니다.<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]업그레이드의 경우 NONE입니다.|예|  
|PARAMETERIZATION|SIMPLE|예|  
|QUOTED_IDENTIFIER|OFF|예|  
|READ_COMMITTED_SNAPSHOT|OFF|예|  
|RECOVERY|SIMPLE|예|  
|RECURSIVE_TRIGGERS|OFF|예|  
|Service Broker 옵션|ENABLE_BROKER|예|  
|TRUSTWORTHY|OFF|아니요|  
  
 이러한 데이터베이스 옵션에 대한 자세한 내용은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)을 참조하세요.  
  
## <a name="restrictions"></a>제한  
 다음 작업은 **tempdb** 데이터베이스에 대해 수행할 수 없습니다.  
  
-   파일 그룹 추가  
  
-   데이터베이스 백업 또는 복원  
  
-   데이터 정렬 변경. 기본 데이터 정렬은 서버 데이터 정렬입니다.  
  
-   데이터베이스 소유자 변경. **tempdb** 는 **sa**가 소유 합니다.  
  
-   데이터베이스 스냅샷 만들기  
  
-   데이터베이스 삭제  
  
-   데이터베이스에서 **게스트** 사용자를 삭제 합니다.  
  
-   변경 데이터 캡처 설정  
  
-   데이터베이스 미러링 참여  
  
-   주 파일 그룹, 주 데이터 파일 또는 로그 파일 제거  
  
-   데이터베이스 또는 주 파일 그룹 이름 바꾸기  
  
-   DBCC CHECKALLOC 실행  
  
-   DBCC CHECKCATALOG 실행  
  
-   데이터베이스를 OFFLINE으로 설정  
  
-   데이터베이스나 주 파일 그룹을 READ_ONLY로 설정  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자가 tempdb에 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다. tempdb 연결 권한을 취소하여 사용자가 tempdb를 사용하지 못하도록 할 수 있지만 일부 일상적인 작업에서 tempdb를 사용해야 하므로 권장하지 않습니다.  
  
## <a name="related-content"></a>관련 내용  
 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../indexes/indexes.md)  
  
 [시스템 데이터베이스](system-databases.md)  
  
 [sys.databases&#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)  
  
 [sys.master_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-master-files-transact-sql)  
  
 [데이터베이스 파일 이동](move-database-files.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 2005에서의 tempdb 사용](https://chresandro.wordpress.com/2014/09/29/working-with-tempdb-in-sql-server-2005/)  
  
  
