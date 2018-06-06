---
title: 메모리 내 OLTP(메모리 내 최적화) | Microsoft 문서
ms.custom: ''
ms.date: 11/22/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
caps.latest.revision: 106
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 54fa82bd4f225847214211cf3549858bf9bf3182
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34707761"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>메모리 내 OLTP(메모리 내 최적화)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 트랜잭션 처리, 데이터 수집 및 데이터 로드, 일시적인 데이터 시나리오의 성능을 크게 개선할 수 있습니다.  기본 코드 및 정보를 즉시 활용하려면 직접 작성한 메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저를 빠르게 테스트해야 합니다. 자세한 내용은 다음을 참조하세요.
 -  [빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)  
 
메모리 내 OLTP를 설명하고 성능상의 이점을 설명하는 17분 분량의 비디오

-  [SQL Server 2016의 메모리 내 OLTP](https://www.youtube.com/watch?v=l5l5eophmK4)

비디오에 사용되는 메모리 내 OLTP에 대한 성능 데모를 다운로드하려면 다음을 참조하세요. 

- [메모리 내 OLTP 성능 데모 v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

메모리 내 OLTP 및 이 기술의 성능 이점을 보여 주는 시나리오에 대한 자세한 내용은 다음을 참조하세요.

- [개요 및 사용 시나리오](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)
 
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 는 트랜잭션 처리 성능을 향상시키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술입니다. 보고 및 분석 쿼리 성능을 향상시키는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술은 [Columnstore 인덱스 가이드](../../relational-databases/indexes/columnstore-indexes-overview.md)를 참조하세요.
  
 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]는 물론 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 및 [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]의 메모리 내 OLTP는 다양한 방식으로 개선되었습니다. Transact-SQL 노출 영역이 늘어나 데이터베이스 응용 프로그램을 보다 쉽게 마이그레이션할 수 있습니다. 메모리 최적화 테이블 및 고유하게 컴파일된 저장 프로시저에 대한 ALTER 작업 수행이 추가로 지원되어 응용 프로그램을 보다 쉽게 관리할 수 있습니다. [!INCLUDE[hek_2](../../includes/hek-2-md.md)]의 새로운 기능에 대한 자세한 내용은 [Columnstore 인덱스 - 새로운 기능](../../relational-databases/indexes/columnstore-indexes-what-s-new.md)을 참조하세요.  
  
> [!NOTE]  
>  **사용해 보기**  
>   
>  메모리 내 OLTP는 프리미엄 및 중요 비즈니스용 계층 Azure SQL 데이터베이스 및 탄력적 풀에서 사용할 수 있습니다. Azure SQL Database의 Columnstore 및 메모리 내 OLTP를 시작하려면 [SQL Database에서 메모리 내 기술을 사용하여 성능 최적화](https://azure.microsoft.com/documentation/articles/sql-database-in-memory/)를 참조하세요.  
  

## <a name="in-this-section"></a>섹션 내용  
 이 섹션에서는 다음 항목을 다룹니다.  
  
|항목|설명|  
|-----------|-----------------|  
|[빠른 시작 1: 더 빠른 Transact-SQL 성능을 위한 메모리 내 OLTP 기술](../../relational-databases/in-memory-oltp/survey-of-initial-areas-in-in-memory-oltp.md)|메모리 내 OLTP 살펴보기|
|[개요 및 사용 시나리오](../../relational-databases/in-memory-oltp/overview-and-usage-scenarios.md)|메모리 내 OLTP의 정의와 성능 이점을 보여 주는 시나리오에 대한 개요입니다.|
|[메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항](../../relational-databases/in-memory-oltp/requirements-for-using-memory-optimized-tables.md)|하드웨어 및 소프트웨어 요구 사항과 메모리 최적화 테이블의 사용 지침에 대해 설명합니다.|  
|[메모리 내 OLTP 코드 예제](../../relational-databases/in-memory-oltp/in-memory-oltp-code-samples.md)|메모리 최적화 테이블을 만들고 사용하는 방법을 보여 주는 코드 예제가 포함되어 있습니다.|  
|[Memory-Optimized Tables](../../relational-databases/in-memory-oltp/memory-optimized-tables.md)|메모리 최적화 테이블을 소개합니다.|  
|[메모리 액세스에 최적화된 테이블 변수](http://msdn.microsoft.com/library/bd102e95-53e2-4da6-9b8b-0e4f02d286d3)|기존의 테이블 변수 대신 메모리 최적화 테이블 변수를 사용하여 tempdb 사용을 줄이는 방법을 보여주는 코드 예제입니다.|  
|[메모리 액세스에 최적화된 테이블의 인덱스](http://msdn.microsoft.com/library/86805eeb-6972-45d8-8369-16ededc535c7)|메모리 최적화 인덱스를 소개합니다.|  
|[고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md)|고유하게 컴파일된 저장 프로시저를 소개합니다.|  
|[메모리 내 OLTP의 메모리 관리](http://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)|시스템의 메모리 사용을 이해하고 관리하는 방법에 대해 설명합니다.|  
|[메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)|메모리 최적화 테이블의 트랜잭션에 대한 정보를 저장하는 데이터 및 델타 파일에 대해 설명합니다.|  
|[메모리 액세스에 최적화된 테이블의 백업, 복원 및 복구](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)|메모리 최적화 테이블의 백업, 복원 및 복구를 논의합니다.|  
|[메모리 내 OLTP에 대한 Transact-SQL 지원](../../relational-databases/in-memory-oltp/transact-sql-support-for-in-memory-oltp.md)|[!INCLUDE[tsql](../../includes/tsql-md.md)] 에 대한 [!INCLUDE[hek_2](../../includes/hek-2-md.md)]지원을 논의합니다.|  
|[메모리 내 OLTP 데이터베이스에 대한 고가용성 지원](../../relational-databases/in-memory-oltp/high-availability-support-for-in-memory-oltp-databases.md)|[!INCLUDE[hek_2](../../includes/hek-2-md.md)]의 가용성 그룹 및 장애 조치(failover) 클러스터링을 논의합니다.|  
|[메모리 내 OLTP에 대한 SQL Server 지원](../../relational-databases/in-memory-oltp/sql-server-support-for-in-memory-oltp.md)|메모리 최적화 테이블을 지원하는 새 구문/기능과 업데이트된 구문/기능을 나열합니다.|  
|[메모리 내 OLTP로 마이그레이션](../../relational-databases/in-memory-oltp/migrating-to-in-memory-oltp.md)|디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션하는 방법에 대해 설명합니다.|  
  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 에 대한 자세한 내용은 다음을 참조하세요.  

- [메모리 내 OLTP를 설명하고 성능상의 이점을 보여 주는 비디오](https://www.youtube.com/watch?v=l5l5eophmK4).

- [메모리 내 OLTP 성능 데모 v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)

-   [SQL Server 메모리 내 OLTP 내부 기술 백서](https://msdn.microsoft.com/library/mt764316.aspx)  

-   [SQL Server 메모리 내 OLTP와 Columnstore 기능 비교](http://download.microsoft.com/download/D/0/0/D0075580-6D72-403D-8B4D-C3BD88D58CE4/SQL_Server_2016_In_Memory_OLTP_and_Columnstore_Comparison_White_Paper.pdf)

-   SQL Server 2016의 메모리 내 OLTP에 대한 새로운 기능 [1부](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2015/11/12/in-memory-oltp-whats-new-in-sql2016-ctp3/) 및 [2부](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/25/whats-new-for-in-memory-oltp-in-sql-server-2016-since-ctp3/)
  
-   [메모리 내 OLTP – 자주 사용되는 작업 패턴 및 마이그레이션 고려 사항](http://msdn.microsoft.com/library/dn673538.aspx)  
  
-   [메모리 내 OLTP 블로그](http://go.microsoft.com/fwlink/?LinkId=311696)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 기능](../../relational-databases/database-features.md)  
  
  
