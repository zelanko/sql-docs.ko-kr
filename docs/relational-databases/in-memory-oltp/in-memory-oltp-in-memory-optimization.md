---
title: 메모리 내 OLTP(메모리 내 최적화) | Microsoft 문서
ms.custom: ''
ms.date: 11/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 87ad093d5be6f4fa394e934e6c0d88796a22e196
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "74401650"
---
# <a name="in-memory-oltp-and-memory-optimization"></a>메모리 내 OLTP 및 메모리 최적화

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 트랜잭션 처리, 데이터 수집 및 데이터 로드, 일시적인 데이터 시나리오의 성능을 크게 개선할 수 있습니다.  기본 코드 및 정보를 즉시 활용하려면 직접 작성한 메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저를 빠르게 테스트해야 합니다. 자세한 내용은 다음을 참조하세요.
 -  [빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)을 참조하세요.  
 
SQL Server의 메모리 내 OLTP를 설명하고 성능상의 이점을 보여 주는 [**17분 분량의 비디오**](#anchorname-17minute-video)가 YouTube에 업로드되었습니다.

메모리 내 OLTP 및 이 기술의 성능 이점을 보여 주는 시나리오에 대한 자세한 내용은 다음을 참조하세요.

- [개요 및 사용 시나리오](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 트랜잭션 처리 성능을 향상시키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술입니다. 보고 및 분석 쿼리 성능을 향상시키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술은 [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)를 참조하세요.
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 물론 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]의 메모리 내 OLTP는 다양한 방식으로 개선되었습니다. Transact-SQL 노출 영역이 늘어나 데이터베이스 애플리케이션을 보다 쉽게 마이그레이션할 수 있습니다. 메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저에 대한 ALTER 작업 수행이 추가로 지원되어 애플리케이션을 보다 쉽게 관리할 수 있습니다.
  
> [!NOTE]  
>  **사용해 보기**  
>   
>  메모리 내 OLTP는 프리미엄 및 중요 비즈니스용 계층 Azure SQL 데이터베이스 및 탄력적 풀에서 사용할 수 있습니다. Azure SQL Database의 Columnstore 및 메모리 내 OLTP를 시작하려면 [SQL Database에서 메모리 내 기술을 사용하여 성능 최적화](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/)를 참조하세요.  
  

## <a name="in-this-section"></a>섹션 내용  
 이 섹션에서는 다음 항목을 다룹니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|메모리 내 OLTP 살펴보기|
|[개요 및 사용 시나리오](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|메모리 내 OLTP의 정의와 성능 이점을 보여 주는 시나리오에 대한 개요입니다.|
|[메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|하드웨어 및 소프트웨어 요구 사항과 메모리 최적화 테이블의 사용 지침에 대해 설명합니다.|  
|[메모리 내 OLTP 코드 예제](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|메모리 최적화 테이블을 만들고 사용하는 방법을 보여 주는 코드 예제가 포함되어 있습니다.|  
|[메모리 최적화 테이블](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|메모리 최적화 테이블을 소개합니다.|  
|[메모리 액세스에 최적화된 테이블 변수](https://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|기존의 테이블 변수 대신 메모리 최적화 테이블 변수를 사용하여 tempdb 사용을 줄이는 방법을 보여주는 코드 예제입니다.|  
|[메모리 액세스에 최적화된 테이블의 인덱스](https://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|메모리 최적화 인덱스를 소개합니다.|  
|[고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|고유하게 컴파일된 저장 프로시저를 소개합니다.|  
|[메모리 내 OLTP의 메모리 관리](https://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|시스템의 메모리 사용을 이해하고 관리하는 방법에 대해 설명합니다.|  
|[메모리 최적화 개체에 대한 스토리지 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|메모리 최적화 테이블의 트랜잭션에 대한 정보를 저장하는 데이터 및 델타 파일에 대해 설명합니다.|  
|[메모리 액세스에 최적화된 테이블의 백업, 복원 및 복구](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|메모리 최적화 테이블의 백업, 복원 및 복구를 논의합니다.|  
|[메모리 내 OLTP에 대한 Transact-SQL 지원](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대한 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]지원을 논의합니다.|  
|[메모리 내 OLTP 데이터베이스에 대한 고가용성 지원](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|[!INCLUDE[hek_2](../../includes/hek-2-md.md)]의 가용성 그룹 및 장애 조치(failover) 클러스터링을 논의합니다.|  
|[메모리 내 OLTP에 대한 SQL Server 지원](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|메모리 최적화 테이블을 지원하는 새 구문/기능과 업데이트된 구문/기능을 나열합니다.|  
|[메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션하는 방법에 대해 설명합니다.|  
| &nbsp; | &nbsp; |

## <a name="links-to-other-websites"></a>다른 웹 사이트 링크

이 섹션에서는 SQL Server의 I메모리 내 OLTP에 대한 정보가 포함된 다른 웹 사이트의 링크를 제공합니다.

- [메모리 내 OLTP를 설명하고 성능상의 이점을 보여 주는 **비디오**](#anchorname-17minute-video)

- [메모리 내 OLTP 성능 데모 v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [SQL Server 메모리 내 OLTP 내부 기술 백서](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [SQL Server 메모리 내 OLTP와 Columnstore 기능 비교](https://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   SQL Server 2016의 메모리 내 OLTP에 대한 새로운 기능 [1부](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) 및 [2부](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [메모리 내 OLTP – 일반적인 워크로드 패턴 및 마이그레이션 고려 사항](https://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [메모리 내 OLTP 블로그](https://go.microsoft.com/fwlink/?LinkId=311696)  

## <a name="anchorname-17minute-video"></a>인덱싱된 17분 분량의 비디오

- _비디오 제목:_ &nbsp; **SQL Server 2016의 메모리 내 OLTP**
- _게시 날짜:_ &nbsp; 2019-03-10, `YouTube.com`.
- _길이:_ &nbsp; 17:32 &nbsp; &nbsp;(비디오 링크는 다음 [**인덱스**](#anchorname-index-17minute-video) 참조)
- _호스팅 담당자:_ &nbsp; Jos de Bruijn, SQL Server 선임 프로그램 관리자

### <a name="demo-can-be-downloaded"></a>데모 다운로드 가능

시간이 08:09로 표시되면 비디오에서 데모를 두 번 실행합니다. 비디오에 사용된 실행 가능한 성능 데모의 소스 코드는 다음 링크에서 다운로드할 수 있습니다.

- [메모리 내 OLTP 성능 데모 v1.0, 소스 코드](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

비디오에 표시되는 일반적인 단계는 다음과 같습니다.

1. 먼저 데모는 일반 테이블로 실행됩니다.
2. 그 다음 SQL Server Management Studio(SSMS.exe)에서 몇 번의 클릭으로 생성하여 채울 수 있는 메모리 최적화 테이블 버전을 확인할 수 있습니다.
3. 그런 다음 메모리 최적화 테이블을 사용하여 데모를 다시 실행합니다. 속도가 크게 향상되었음을 확인할 수 있습니다.

### <a name="anchorname-index-17minute-video"></a>비디오의 각 섹션에 대한 인덱스

| 시간 표시 링크 | 섹션 제목 |
| :------------- | :------------ |
| A.&nbsp; [00:00](https://www.youtube.com/watch?v=l5l5eophmK4&t=0) | 시작. |
| <br/>B.&nbsp; [00:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=56) | <br/>고객이 메모리 내 OLTP를 적용해야 하는 이유는 다음과 같습니다. |
| &nbsp; &nbsp; [01:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=63) | 최신 하드웨어에는 최신 데이터베이스 시스템 아키텍처가 필요합니다. |
| &nbsp; &nbsp; [02:10](https://www.youtube.com/watch?v=l5l5eophmK4&t=130) | 생성되는 데이터가 급증하여 작업을 즉시 진행해야 합니다(대기 시간 짧음). |
| &nbsp; &nbsp; [03:19](https://www.youtube.com/watch?v=l5l5eophmK4&t=199) | TCO 절감 - 보유한 리소스로 더 많은 작업을 수행할 수 있습니다. |
| <br/>C.&nbsp; [03:33](https://www.youtube.com/watch?v=l5l5eophmK4&t=213) | <br/>메모리 내 OLTP의 의미<br/>메모리 최적화 기술을 사용하여 성능 최적화 |
| &nbsp; &nbsp; [05:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=303) | 최대 30배 빠른 트랜잭션 처리 |
| &nbsp; &nbsp; [05:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=322) | 완전한 내구성 – 서버 오류가 발생해도 데이터는 유지됩니다. |
| &nbsp; &nbsp; [06:15](https://www.youtube.com/watch?v=l5l5eophmK4&t=375) | SQL Server에 완전히 통합되었습니다. 따라서 새로운 언어 또는 도구를 배울 필요가 없습니다. |
| &nbsp; &nbsp; [07:22](https://www.youtube.com/watch?v=l5l5eophmK4&t=442) | SQL Server 2014에서 처음 릴리스되었지만 2016에 주요 개선 사항이 적용되었습니다. |
| &nbsp; &nbsp; [07:58](https://www.youtube.com/watch?v=l5l5eophmK4&t=558) | Microsoft Azure SQL Database에서도 사용할 수 있습니다(클라우드). |
| <br/>D.&nbsp; [08:09](https://www.youtube.com/watch?v=l5l5eophmK4&t=489) | <br/>성능 데모.<br/> 일반 테이블을 사용하여 데모를 실행합니다. |
| &nbsp; &nbsp; [09:11](https://www.youtube.com/watch?v=l5l5eophmK4&t=551) | SSMS 바로 가기 메뉴: **보고서** &gt; **트랜잭션 성능 분석** |
| &nbsp; &nbsp; [10:38](https://www.youtube.com/watch?v=l5l5eophmK4&t=638) | SSMS 바로 가기 메뉴: **메모리 최적화 관리자**<br/> &nbsp; &nbsp; 실제로 일반 테이블에서 메모리 최적화 테이블을 생성하고 데이터를 마이그레이션합니다. |
| &nbsp; &nbsp; [11:28](https://www.youtube.com/watch?v=l5l5eophmK4&t=688) | 데모를 다시 실행하고 45배 향상된 속도를 경험하세요. |
| <br/>E.&nbsp; [12:17](https://www.youtube.com/watch?v=l5l5eophmK4&t=737) | <br/>SQL Server 2016에서 메모리 내 OLTP를 2014보다 더 쉽게 사용할 수 있습니다. |
| &nbsp; &nbsp; [12:43](https://www.youtube.com/watch?v=l5l5eophmK4&t=763) | 앱 마이그레이션에 도움이 되는 간략한 분석. |
| &nbsp; &nbsp; [13:03](https://www.youtube.com/watch?v=l5l5eophmK4&t=783) | Transact-SQL 언어 지원의 개선(예: 외래 키 및 트리거)으로 앱 마이그레이션의 복잡성이 줄어들었습니다. |
| &nbsp; &nbsp; [13:56](https://www.youtube.com/watch?v=l5l5eophmK4&t=836) | 관리 효율성 향상.<br/> &nbsp; &nbsp; 예를 들어 스키마 및 인덱스 변경, 통계 자동 업데이트 등이 있습니다. |
| <br/>F.&nbsp; [14:46](https://www.youtube.com/watch?v=l5l5eophmK4&t=886) | <br/>확장성 향상. |
| &nbsp; &nbsp; [15:12](https://www.youtube.com/watch?v=l5l5eophmK4&t=912) | 대규모 메모리 최적화 테이블(데이터베이스 당 최대 2TB). |
| &nbsp; &nbsp; [15:34](https://www.youtube.com/watch?v=l5l5eophmK4&t=934) | 더 효과적인 크기 조정. |
| &nbsp; &nbsp; [16:41](https://www.youtube.com/watch?v=l5l5eophmK4&t=1001) | 이미 보유한 리소스로 더 많은 작업을 수행할 수 있습니다! |
| <br/>G.&nbsp; [16:53](https://www.youtube.com/watch?v=l5l5eophmK4&t=1013) | <br/>최종 설명. (17:32에서 종료) |
| &nbsp; | &nbsp; |

## <a name="see-also"></a>참고 항목  
 [데이터베이스 기능](../../relational-databases/database-features.md)  
  
  
