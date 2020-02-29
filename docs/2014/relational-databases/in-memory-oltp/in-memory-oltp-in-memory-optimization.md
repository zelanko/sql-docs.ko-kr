---
title: 메모리 내 OLTP(메모리 내 최적화) | Microsoft 문서
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- In-Memory OLTP
- memory-optimized tables
ms.assetid: e1d03d74-2572-4a55-afd6-7edf0bc28bdb
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 530e620be1a1c0f9d457eb23712c5228a3883d45
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/28/2020
ms.locfileid: "78175935"
---
# <a name="in-memory-oltp-in-memory-optimization"></a>메모리 내 OLTP(메모리 내 최적화)

  
  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]의 새로운 기능인 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 로 OLTP 데이터베이스 애플리케이션 성능이 상당히 개선될 수 있습니다. 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 엔진에 통합된 메모리 최적화 데이터베이스 엔진으로 OLTP에 최적화되어 있습니다.

|||
|-|-|
|![Azure 가상 머신](../../master-data-services/media/azure-virtual-machine.png "Azure Virtual Machine")|SQL Server 2016을 사용해 보시겠나요? Microsoft Azure에 등록한 다음 **[여기](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm)** 로 이동하여 이미 설치된 SQL Server 2016으로 가상 머신을 실행합니다. 완료 되 면 가상 컴퓨터를 삭제할 수 있습니다.|

 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]를 사용하려면 자주 액세스하는 테이블을 메모리 액세스에 최적화된 상태로 정의합니다. 메모리 액세스에 최적화된 테이블은 내구성 있는 완전 트랜잭션이며 디스크 기반 테이블과 같은 방법으로 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 을 사용하여 액세스됩니다. 쿼리는 메모리 최적화 테이블 및 디스크 기반 테이블을 모두 참조할 수 있습니다. 트랜잭션은 메모리 최적화 테이블 및 디스크 기반 테이블에서 데이터를 업데이트할 수 있습니다. 메모리 최적화 테이블만 참조하는 저장 프로시저는 성능 향상을 위해 기계어 코드에 고유하게 컴파일될 수 있습니다. 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 엔진은 고도로 확장된 중간 계층에서 파생되는 OLTP 유형의 트랜잭션을 위한 매우 높은 수준의 세션 동시성을 지원하도록 설계되었습니다. 이를 위해서 래치가 설정되지 않은 데이터 구조와 낙관적인 여러 버전의 동시성 제어를 사용합니다. 따라서 결과는 예측 가능하며, 지연 시간은 밀리초 미만으로 짧고, 처리량은 많으며 데이터베이스 트랜잭션을 위해 직선형으로 확장됩니다. 실제 성능 향상은 많은 요인에 따라 달라지지만 일반적으로 성능이 5 - 20배 향상됩니다.

 다음 표에는 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]를 사용하여 가장 이점을 얻을 수 있는 작업 패턴이 요약되어 있습니다.

|구현 시나리오|구현 시나리오|
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]의 이점|
|-----------------------------|-----------------------------|-------------------------------------|
|다중 동시 연결을 위한 높은 데이터 삽입률|기본적으로 방식만을 사용하는 저장소<br /><br /> 삽입 작업을 처리할 수 없음|경합 제거<br /><br /> 로깅 감소|
|성능을 읽고 정기적인 일괄 삽입 및 업데이트로 확장|많은 성능 읽기 작업, 특히 각 서버가 다중 읽기 작업을 수행하도록 요청하는 경우<br /><br /> 확장 요구 사항을 충족할 수 없음|새로운 데이터 유입 시 경합 제거<br /><br /> 데이터 검색 대기 시간 단축<br /><br /> 코드 실행 시간 최소화|
|데이터베이스 서버의 집중적인 비즈니스 논리 처리|삽입, 업데이트 및 삭제 작업<br /><br /> 저장 프로시저 내 계산 집중적인 작업<br /><br /> 읽기 및 쓰기 경합|경합 제거<br /><br /> 코드 실행 시간을 최소화하여 대기 시간 단축 및 처리량 향상|
|짧은 대기 시간|일반적인 데이터베이스 솔루션으로 구현할 수 없는 짧은 대기 시간 비즈니스 트랜잭션 필요|경합 제거<br /><br /> 코드 실행 시간 최소화<br /><br /> 코드 실행 대기 시간 단축<br /><br /> 효율적인 데이터 검색|
|세션 상태 관리|삽입, 업데이트 및 지점 검색을 자주 수행<br /><br /> 수많은 상태 비저장 웹 서버의 대규모 부하|경합 제거<br /><br /> 효율적인 데이터 검색<br /><br /> 내구성 없는 테이블을 사용할 경우 옵션 IO 절감 또는 제거|

 에서 가장 큰 성능 이점을 얻을 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 수 있는 시나리오에 대 한 자세한 내용은 [메모리 내 OLTP-일반적인 작업 패턴 및 마이그레이션 고려 사항](https://msdn.microsoft.com/library/dn673538.aspx)을 참조 하세요.

 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]는 짧은 트랜잭션 실행 시간으로 OLTP에서 가장 높은 성능 개선을 보입니다.

 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 에서 개선하는 프로그래밍 패턴으로는 동시성, 지점 검색, 많은 삽입 및 업데이트가 사용되는 작업 및 저장 프로시저의 비즈니스 논리가 있습니다.

 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 통합되어 메모리 최적화 테이블과 디스크 기반 테이블을 모두 같은 데이터베이스에 넣을 수 있으며 두 형식의 테이블을 모두 쿼리할 수 있습니다.

 
  [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] 에서는 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 에 대해 지원되는 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]노출 영역이 제한됩니다.

 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]는 다음을 사용하여 성능과 확장성을 크게 향상합니다.

-   메모리 상주 데이터에 액세스할 수 있도록 최적화된 알고리즘

-   논리적 잠금을 제거하는 낙관적 동시성 제어.

-   모든 실제 잠금 및 래치를 제거하는 잠금 없는 개체. 트랜잭션 작업을 수행 하는 스레드는 동시성 제어를 위해 잠금이나 래치를 사용 하지 않습니다.

-   메모리 최적화 테이블에 액세스할 때 해석된 저장 프로시저보다 성능이 크게 향상된 기본적으로 컴파일된 저장 프로시저

> [!IMPORTANT]
>  
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]를 사용하려면 일부 구문을 테이블과 저장 프로시저로 변경해야 합니다. 자세한 내용은 [메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)을 참조하세요. 디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션하기 전에 [메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인](determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp.md)을 읽고 어떤 테이블과 저장 프로시저가 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]에서 이익을 얻을지 확인하세요.

## <a name="in-this-section"></a>섹션 내용
 이 섹션에서는 다음과 같은 개념에 대해 설명합니다.

|항목|Description|
|-----------|-----------------|
|[메모리 액세스에 최적화된 테이블 사용을 위한 요구 사항](memory-optimized-tables.md)|하드웨어 및 소프트웨어 요구 사항과 메모리 최적화 테이블의 사용 지침에 대해 설명합니다.|
|[VM 환경에서 메모리 내 OLTP 사용](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)|가상화된 환경에서 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 사용에 대해 다룹니다.|
|[메모리 내 OLTP 코드 예제](in-memory-oltp-code-samples.md)|메모리 최적화 테이블을 만들고 사용하는 방법을 보여 주는 코드 예제가 포함되어 있습니다.|
|[메모리 최적화 테이블](memory-optimized-tables.md)|메모리 최적화 테이블을 소개합니다.|
|[메모리 액세스에 최적화된 테이블 변수](../../database-engine/memory-optimized-table-variables.md)|기존의 테이블 변수 대신 메모리 최적화 테이블 변수를 사용하여 tempdb 사용을 줄이는 방법을 보여주는 코드 예제입니다.|
|[메모리 액세스에 최적화된 테이블의 인덱스](../../database-engine/indexes-on-memory-optimized-tables.md)|메모리 최적화 인덱스를 소개합니다.|
|[고유하게 컴파일된 저장 프로시저](natively-compiled-stored-procedures.md)|고유하게 컴파일된 저장 프로시저를 소개합니다.|
|[메모리 내 OLTP의 메모리 관리](../../database-engine/managing-memory-for-in-memory-oltp.md)|시스템의 메모리 사용을 이해하고 관리하는 방법에 대해 설명합니다.|
|[메모리 최적화 개체에 대한 스토리지 만들기 및 관리](creating-and-managing-storage-for-memory-optimized-objects.md)|메모리 최적화 테이블의 트랜잭션에 대한 정보를 저장하는 데이터 및 델타 파일에 대해 설명합니다.|
|[메모리 액세스에 최적화된 테이블의 백업, 복원 및 복구](restore-and-recovery-of-memory-optimized-tables.md)|메모리 최적화 테이블의 백업, 복원 및 복구를 논의합니다.|
|[메모리 내 OLTP에 대한 Transact-SQL 지원](transact-sql-support-for-in-memory-oltp.md)|[!INCLUDE[tsql](../../../includes/tsql-md.md)] 에 대한 [!INCLUDE[hek_2](../../../includes/hek-2-md.md)]지원을 논의합니다.|
|[메모리 내 OLTP 데이터베이스에 대한 고가용성 지원](high-availability-support-for-in-memory-oltp-databases.md)|[!INCLUDE[hek_2](../../../includes/hek-2-md.md)]의 가용성 그룹 및 장애 조치(failover) 클러스터링을 논의합니다.|
|[메모리 내 OLTP에 대한 SQL Server 지원](sql-server-support-for-in-memory-oltp.md)|메모리 최적화 테이블을 지원하는 새 구문/기능과 업데이트된 구문/기능을 나열합니다.|
|[메모리 내 OLTP로 마이그레이션](migrating-to-in-memory-oltp.md)|디스크 기반 테이블을 메모리 최적화 테이블로 마이그레이션하는 방법에 대해 설명합니다.|

 
  [!INCLUDE[hek_2](../../../includes/hek-2-md.md)] 에 대한 자세한 내용은 다음을 참조하세요.

-   [Microsoft?? SQL Server?? 2014 제품 가이드](https://www.microsoft.com/download/confirmation.aspx?id=39269)

-   [메모리 내 OLTP 블로그](https://go.microsoft.com/fwlink/?LinkId=311696)

-   [메모리 내 OLTP – 일반적인 워크로드 패턴 및 마이그레이션 고려 사항](https://msdn.microsoft.com/library/dn673538.aspx)

-   [SQL Server 메모리 내 OLTP 내부 개요(영문)](https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
    <!--
         (https://download.microsoft.com/download/8/3/6/8360731A-A27C-4684-BC88-FC7B5849A133/SQL_Server_2016_In_Memory_OLTP_White_Paper.pdf)
         (/sql/relational-databases/in-memory-oltp/sql-server-in-memory-oltp-internals-for-sql-server-2016?view=sql-server-2016)
    -->

## <a name="see-also"></a>참고 항목
 [데이터베이스 기능](../database-features.md)


