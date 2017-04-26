---
title: "SQL Server vNext의 새로운 기능 | Microsoft 문서"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-vnext
ms.reviewer: 
ms.suite: 
ms.technology:
- server-general
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b57f375-9242-4bb2-9d4b-c560d5a93524
caps.latest.revision: 71
author: craigg-msft
ms.author: craigg
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f4a9065cccb31a8ee71e142aeba054addd6c4a5d
ms.lasthandoff: 04/11/2017

---
# <a name="what39s-new-in-sql-server-vnext"></a>SQL Server vNext의 새로운 기능
SQL Server vNext는 SQL Server의 기능을 Linux, Linux 기반 Docker 컨테이너 및 Windows로 가져와 SQL ServeR을 개발 언어, 데이터 형식, 온-프레미스 및 클라우드, 모든 운영 체제에서 선택할 수 있는 플랫폼으로 만드는 주요 단계를 나타냅니다.

이 항목은 최근 CTP(Community Technology Preview) 릴리스의 새로운 기능 요약으로, 특정 기능 영역의 새로운 기능에 대한 자세한 정보 링크입니다.

![info_tip](../sql-server/media/info-tip.png) Linux에서 SQL Server 실행! 참조 항목:
-  [Linux에서 SQL Server vNext의 새로운 기능](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-whats-new)
-  [SQL Server on Linux Documentation](https://docs.microsoft.com/en-us/sql/linux/)


**사용해보기:**    
   -   [![Download from Evaluation Center](../analysis-services/media/download.png)](http://go.microsoft.com/fwlink/?LinkID=829477) **[Download the SQL Server vNext Community Technology Preview](http://go.microsoft.com/fwlink/?LinkID=829477)**

## <a name="whats-new-in-sql-server-vnext-ctp-14-march-2017"></a>SQL Server vNext CTP 1.4(2017년 3월)의 새로운 기능
### <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진
- 이 CTP에는 새로운 데이터베이스 엔진 기능이 없습니다.
- 이 CTP에는 데이터베이스 엔진에 대한 버그 수정이 포함되어 있습니다.
- 이전 CTP 릴리스의 향상된 VNext CTP 기능의 자세한 목록은 [SQL Server vNext(데이터베이스 엔진)의 새로운 기능](../database-engine/configure-windows/what-s-new-in-sql-server-vnext-database-engine.md)을 참조하세요.

### <a name="sql-server-r-services"></a>SQL Server R Services
- 이 CTP에는 새로운 R Services 기능이 없습니다.
- 이전 CTP의 세부 정보를 포함하여 R Services의 새로운 기능에 대한 자세한 내용은 [SQL Server R Services의 새로운 기능](../advanced-analytics/r-services/what-s-new-in-sql-server-r-services.md)을 참조하세요.  

### <a name="sql-server-reporting-services-ssrs"></a>SSRS(SQL Server Reporting Services)
- 이 CTP에는 새로운 SSRS 기능이 없습니다.
- 이전 릴리스의 세부 정보를 포함하여 SSRS의 새로운 기능에 대한 자세한 내용은 [의 새로운 기능](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)을 참조하세요. 

### <a name="sql-server-analysis-services-ssas"></a>SSAS(SQL Server Analysis Services)
- 이 CTP에는 새로운 SSAS 기능이 없습니다.  
- SSDT 및 SSMS의 최신 시험판 릴리스에 있는 Analysis Services의 새로운 기능을 포함하여 자세한 내용은 [Analysis Services vNext의 새로운 기능](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md)을 참조하세요.  

### <a name="sql-server-integration-services-ssis"></a>SSIS(SQL Server Integration Services)
- 이 CTP에는 새로운 SSIS 기능이 없습니다.
- 이전 CTP의 세부 정보를 포함하여 SSIS의 새로운 기능에 대한 자세한 내용은 [Integration Services vNext의 새로운 기능](../integration-services/what-s-new-in-integration-services-in-sql-server-vnext.md)을 참조하세요.  

### <a name="master-data-services-mds"></a>MDS(Master Data Services)
- 이 CTP에는 새로운 Master Data Services 기능이 없습니다.

![horizontal_bar](../sql-server/media/horizontal-bar.png)

## <a name="whats-new-in-sql-server-vnext-ctp-13-february-2017"></a>SQL Server vNext CTP 1.3(2017년 2월)의 새로운 기능
### <a name="sql-server-database-engine"></a>SQL Server 데이터베이스 엔진
- 간접 검사점 성능 개선 사항
- 클러스터 없는 가용성 그룹 지원이 추가되었습니다.
- 최소 복제본 커밋 가용성 그룹 설정이 추가되었습니다.
- 이제 가용성 그룹은 Windows-Linux 간에 원활하게 작동되므로 OS 간 마이그레이션 및 테스트가 가능합니다.
- 임시 테이블 보존 정책 지원이 추가되었습니다.
- 새로운 DMV SYS.DM_DB_STATS_HISTOGRAM
- 온라인 비클러스터형 columnstore 인덱스 작성 및 다시 작성 지원이 추가되었습니다.
- Linux 프로세스에 대한 정보를 반환하는&5;개의 새로운 동적 관리 뷰. 자세한 내용은 [Linux 프로세스 동적 관리 뷰](../relational-databases/system-dynamic-management-views/linux-process-dynamic-management-views-transact-sql.md)를 참조하세요.   
- [sys.dm_db_stats_histogram(TRANSACT-SQL)](../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md) 이 통계 검사를 위해 추가되었습니다.

### <a name="sql-server-analysis-services-ssas-ctp-13"></a>SSAS(SQL Server Analysis Services)(CTP 1.3)
- 인코딩 힌트 - 대규모 메모리 내 테이블 형식 모델의 처리(데이터 새로 고침)를 최적화하는 데 사용하는 고급 기능입니다. 자세한 내용은 [Analysis Services vNext의 새로운 기능](../analysis-services/what-s-new-in-sql-server-analysis-services-vnext.md)을 참조하세요. 


![horizontal_bar](../sql-server/media/horizontal-bar.png)

##  <a name="infotipsql-servermediainfo-tippng-engage-with-the-sql-server-engineering-team"></a>![info_tip](../sql-server/media/info-tip.png) SQL Server 엔지니어링 팀에 문의 
- [Stack Overflow(태그 sql-server)](http://stackoverflow.com/questions/tagged/sql-server)
- [MSDN 포럼](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver)
- [Microsoft Connect - 버그 보고 및 기능 요청](https://connect.microsoft.com/SQLServer/Feedback)
- [Reddit - R에 대한 일반 토론](https://www.reddit.com/r/SQLServer/)

## <a name="see-also"></a>참고 항목    
 + [![릴리스 정보](../analysis-services/instances/install-windows/media/ssrs-fyi-note.png)] [SQL Server VNext 릴리스 정보](../sql-server/sql-server-vnext-release-notes.md). 
+ [버전에서 지원하는 기능](https://msdn.microsoft.com/library/cc645993.aspx)
 + [설치 하드웨어 및 소프트웨어 요구 사항](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
 + [설치 마법사](../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)
 
 + [설치 및 서비스 설치](http://msdn.microsoft.com/library/6df72a78-6b36-4bc1-948e-04b4ebe46094)
 
 ![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)



