---
title: 메모리 액세스에 최적화된 테이블 소개 | Microsoft 문서
ms.custom: ''
ms.date: 12/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ef1cc7de-63be-4fa3-a622-6d93b440e3ac
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0dc7ab298607964f4b9a6d7c1c7fa74a53c6bc83
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399276"
---
# <a name="introduction-to-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블 소개
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  메모리 최적화 테이블은 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)을 사용하여 만들어집니다.  
  
 메모리 최적화 테이블은 기본적으로 완전 지속 가능하며, 기존 디스크 기반 테이블의 트랜잭션과 마찬가지로 메모리 최적화 테이블의 트랜잭션은 완전 ACID(원자성, 일관성, 격리 및 지속성)을 가집니다. 메모리 최적화 테이블과 네이티브 컴파일 저장 프로시저는 [!INCLUDE[tsql](../../includes/tsql-md.md)]의 하위 집합만 지원합니다.
 
SQL Server 2016부터 Azure SQL Database에는 메모리 내 OLTP에 한정되는 [데이터 정렬 또는 코드 페이지](../../relational-databases/collations/collation-and-unicode-support.md) 에 대한 제한이 없습니다.
  
 메모리 최적화 테이블에 대한 기본 저장소는 주 메모리입니다. 테이블의 행은 메모리에서 읽고 메모리에 기록합니다. 테이블 데이터의 보조 복사본이 디스크에서 유지 관리되는데, 이는 내구성 목적입니다. 내구성이 있는 테이블에 대한 자세한 내용은 [메모리 액세스에 최적화된 개체의 저장소 만들기 및 관리](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md) 를 참조하세요. 메모리 최적화 테이블의 데이터는 데이터베이스 복구 중에 디스크에서만 읽습니다(예: 서버를 다시 시작한 후).  
  
 보다 큰 성능 향상을 위해 메모리 내 OLTP는 트랜잭션 내구성이 지연된 영구 테이블을 지원합니다. 지연된 지속적 트랜잭션은 트랜잭션이 커밋되고 제어를 클라이언트에 반환한 후 곧바로 디스크에 저장됩니다. 성능이 향상되는 대신 디스크에 저장되지 않은 커밋된 트랜잭션이 서버 충돌 또는 장애 조치(Failover)에서 손실됩니다.  
  
 기본 내구성 메모리 최적화 테이블 외에도 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 기록되지 않고 데이터가 디스크에 지속되지 않는 비 내구성 메모리 최적화 테이블도 지원합니다. 따라서 이러한 테이블의 트랜잭션에는 디스크 IO가 필요하지 않지만 서버 충돌이나 장애 조치가 있는 경우 데이터가 복구되지 않습니다.  
  
 메모리 내 OLTP는 개발, 배포, 관리 효율성 및 지원 가능성과 같은 모든 영역에서 원활한 환경을 제공하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 와 통합되었습니다. 데이터베이스는 메모리 내 개체뿐만 아니라 디스크 기반 개체를 포함할 수 있습니다.  
  
 메모리 최적화 테이블의 행에는 버전이 있습니다. 즉, 테이블의 각 행에 여러 버전이 있을 수 있습니다. 모든 행 버전은 동일한 테이블 데이터 구조에서 유지 관리됩니다. 행 버전 관리는 동일한 행에 대한 동시 읽기 및 쓰기를 가능하게 합니다. 동일한 행에 대한 동시 읽기 및 쓰기에 대한 자세한 내용은 [Transactions with Memory-Optimized Tables](../../relational-databases/in-memory-oltp/transactions-with-memory-optimized-tables.md)(메모리 액세스에 최적화된 테이블 트랜잭션)를 참조하세요.  
  
 다음 그림에서는 다중 버전 관리를 보여 줍니다. 이 그림에서는 세 개의 행이 있고 각 행에 서로 다른 버전이 있는 테이블을 보여 줍니다.  
  
![다중 버전 관리](../../relational-databases/in-memory-oltp/media/hekaton-tables-1.gif "다중 버전 관리")  
  
 테이블에 3개의 행 즉, r1, r2, r3이 있습니다. r1에는 세 개의 버전, r2에는 두 개의 버전, r3에는 네 개의 버전이 있습니다. 동일한 행의 서로 다른 버전은 반드시 연속된 메모리 위치에 배치하지 않아도 되며, 테이블 데이터 구조의 여러 위치에 분산하여 배치할 수 있습니다.  
  
 메모리 최적화 테이블 데이터 구조는 행 버전의 컬렉션처럼 보일 수 있습니다. 디스크 기반 테이블의 행은 페이지 및 익스텐트에 구성되고 개별 행은 페이지 번호 및 페이지 오프셋을 사용하여 지정되는 반면 메모리 최적화 테이블의 행 버전은 8바이트 메모리 포인터를 사용하여 지정됩니다.  
  
 메모리 최적화 테이블의 데이터는 다음 두 가지 방법으로 액세스됩니다.  
  
-   고유하게 컴파일된 저장 프로시저를 통해  
  
-   고유하게 컴파일된 저장 프로시저 외부의 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 통해 이러한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 해석된 저장 프로시저 내부에 있거나 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 될 수 있습니다.  
  
## <a name="accessing-data-in-memory-optimized-tables"></a>메모리 액세스에 최적화된 테이블에서 데이터 액세스  

메모리 액세스에 최적화된 테이블은 고유하게 컴파일된 저장 프로시저([고유하게 컴파일된 저장 프로시저](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md))에서 가장 효율적으로 액세스할 수 있습니다. (기존의) 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]로 메모리 액세스에 최적화된 테이블에 액세스할 수도 있습니다. 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)]은 고유하게 컴파일된 저장 프로시저를 사용하지 않고 메모리 최적화 테이블에 액세스함을 나타냅니다. 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스의 예로는 DML 트리거, 임시 [!INCLUDE[tsql](../../includes/tsql-md.md)] 일괄 처리, 뷰 및 테이블 반환 함수에서 메모리 최적화 테이블에 액세스 등이 있습니다.  
  
 다음 표에서는 다양한 개체에 대한 고유 및 해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스를 요약하여 보여 줍니다.  
  
|기능|고유하게 컴파일된 저장 프로시저를 통한 액세스|해석된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 액세스|CLR 액세스|  
|-------------|-------------------------------------------------------|-------------------------------------------|----------------|  
|메모리 액세스에 최적화된 테이블|예|예|아니요*|  
|메모리 액세스에 최적화된 테이블 형식|예|예|아니오|  
|고유하게 컴파일된 저장 프로시저|고유하게 컴파일된 저장 프로시저 중첩은 지원되지 않습니다. 참조되는 프로시저도 고유하게 컴파일된 경우 저장 프로시저 내에서 EXECUTE 구문을 사용할 수 있습니다.|예|아니요*|  
  
 *컨텍스트 연결(CLR 모듈을 실행하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 연결)에서는 메모리 최적화 테이블이나 고유하게 컴파일된 저장 프로시저에 액세스할 수 없습니다. 하지만 메모리 최적화 테이블과 고유하게 컴파일된 저장 프로시저에 액세스할 수 있는 다른 연결을 만들어서 열 수 있습니다.  
  
## <a name="performance-and-scalability"></a>성능 및 확장성  

다음과 같은 요인이 메모리 내 OLTP에서 얻을 수 있는 성능 향상에 영향을 미칩니다.  
  
*통신:* 짧은 저장 프로시저에 대해 여러 번 호출을 하는 응용 프로그램은 적은 호출을 하고 각 저장 프로시저에 더 많은 기능이 구현된 응용 프로그램이 비해 성능 향상이 적을 수 있습니다.  
  
*[!INCLUDE[tsql](../../includes/tsql-md.md)] 실행:* 메모리 내 OLTP는 해석된 저장 프로시저 또는 쿼리 실행보다는 고유하게 컴파일된 저장 프로시저를 사용할 때 최상의 성능을 얻을 수 있습니다. 이러한 저장 프로시저에서 메모리 최적화 테이블에 액세스하면 효율적일 수 있습니다.  
  
*범위 검색 및 포인트 조회:* 메모리 액세스에 최적화된 비클러스터형 인덱스는 범위 검색 및 정렬된 검색을 지원합니다. 메모리 최적화 비클러스터형 인덱스보다 메모리 최적화 해시 인덱스를 사용할 경우 포인트 조회 성능이 개선됩니다. 메모리 액세스에 최적화된 비클러스터형 인덱스는 디스크 기반 인덱스보다 성능이 우수합니다.

- SQL Server 2016부터 메모리 최적화 테이블에 대한 쿼리 계획은 테이블을 병렬로 검색할 수 있습니다. 그 결과로 분석 쿼리 성능이 향상됩니다.
  - 해시 인덱스도 SQL Server 2016에서 병렬로 검색할 수 있게 되었습니다.
  - 또한 비클러스터형 인덱스도 SQL Server 2016에서 병렬로 검색할 수 있게 되었습니다.
  - Columnstore 인덱스는 SQL Server 2014 이래로 병렬로 검색 가능합니다.
  
*인덱스 작업:* 인덱스 작업은 기록되지 않으며 메모리에만 있습니다.  
  
*동시성:* 성능이 래치 경합 또는 차단과 같은 엔진 수준 동시성의 영향을 받는 응용 프로그램은 응용 프로그램이 메모리 내 OLTP로 이동하면 성능이 크게 개선됩니다.  
  
다음 표에서는 관계형 데이터베이스에서 일반적으로 발견되는 성능 및 확장성 문제와 메모리 내 OLTP를 사용하여 성능을 개선할 수 있는 방법을 나열합니다.  
  
|문제점|메모리 내 OLTP 영향|  
|-----------|----------------------------|  
|성능<br /><br /> 많은 리소스(CPU, I/O, 네트워크 또는 메모리) 사용량|CPU<br /> 고유하게 컴파일된 저장 프로시저를 사용할 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하는 데 필요한 명령이 해석된 저장 프로시저에 비해 매우 적기 때문에 CPU 사용량도 크게 줄어들 수 있습니다.<br /><br /> 메모리 내 OLTP는 서버 한 대가 서버 5 - 10대의 처리량을 발휘할 수 있기 때문에 확장된 작업에서 하드웨어 투자를 줄일 수 있습니다.<br /><br /> 입력/출력<br /> 데이터 또는 인덱스 페이지 처리에 I/O 병목 현상이 발생하는 경우 메모리 내 OLTP를 사용하면 병목 현상을 줄일 수 있습니다. 또한 메모리 내 OLTP 개체의 검사점은 연속되며 I/O 작업의 갑작스러운 증가를 초래하지 않습니다. 그러나 성능에 중요한 영향을 미치는 테이블의 작업 집합이 메모리에 맞지 않을 경우 데이터가 메모리에 상주할 필요가 없기 때문에 메모리 내 OLTP는 성능을 개선하지 않습니다. 로깅에서 I/O 병목 현상이 발생하는 경우 메모리 내 OLTP를 사용하면 로깅이 적게 수행되므로 병목 현상을 줄일 수 있습니다. 하나 이상의 메모리 최적화 테이블을 비내구성 테이블로 구성한 경우 데이터에 대한 로깅을 제거할 수 있습니다.<br /><br /> 메모리<br /> 메모리 내 OLTP는 성능 이점을 제공하지 않습니다. 개체가 메모리에 상주해야 하기 때문에 메모리 내 OLTP는 메모리에 추가 부담을 줄 수 있습니다.<br /><br /> 네트워크<br /> 메모리 내 OLTP는 성능 이점을 제공하지 않습니다. 데이터는 데이터 계층에서 애플리케이션 계층으로 통신해야 합니다.|  
|확장성<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 응용 프로그램에서 발생하는 대부분의 확장 문제는 잠금, 래치 및 spinlock의 경합 같은 동시성 문제로 인한 것입니다.|래치 경합<br /> 일반적인 시나리오는 키 순서로 행을 동시에 삽입할 때 인덱스의 마지막 페이지에서의 경합입니다. 메모리 내 OLTP는 데이터에 액세스할 때 래치를 수행하지 않으므로 래치 경합과 관련한 확장성 문제가 완전히 제거됩니다.<br /><br /> Spinlock 경합<br /> 메모리 내 OLTP는 데이터에 액세스할 때 래치를 수행하지 않으므로 spinlock 경합과 관련한 확장성 문제가 완전히 제거됩니다.<br /><br /> 잠금 관련 경합<br /> 데이터베이스 애플리케이션의 읽기와 쓰기 작업 간에 잠금 문제가 발생하는 경우 새로운 형태의 낙관적 동시성 제어를 사용하여 모든 트랜잭션 격리 수준을 구현하기 때문에 메모리 내 OLTP는 차단 문제를 제거합니다. 메모리 내 OLTP는 행 버전을 저장하는 데 TempDB를 사용하지 않습니다.<br /><br /> 같은 행을 업데이트하려는 두 동시 트랜잭션 같이 두 쓰기 작업 간의 충돌로 인해 확장 문제가 발생하는 경우 메모리 내 OLTP를 사용하면 한 트랜잭션은 성공하고 다른 트랜잭션은 실패합니다. 실패한 트랜잭션은 명시적으로 또는 암시적으로 다시 제출해야 하며 트랜잭션을 다시 시도해야 합니다. 어느 경우나 애플리케이션을 변경해야 합니다.<br /><br /> 애플리케이션의 두 쓰기 작업 간에 충돌이 자주 발생하는 경우 낙관적 잠금 값이 감소합니다. 애플리케이션은 메모리 내 OLTP에 적합하지 않습니다. 충돌이 잠금 에스컬레이션으로 인해 발생하지 않는다면 대부분의 OLTP 애플리케이션에는 쓰기 충돌이 없습니다.|  
  
##  <a name="rls"></a> 메모리 액세스에 최적화된 테이블의 행 수준 보안  

[행 수준 보안](../../relational-databases/security/row-level-security.md) 은 메모리 최적화 테이블에서 지원됩니다. 메모리 최적화 테이블에 행 수준 보안 정책을 적용하는 작업은 디스크 기반 테이블에서와 기본적으로 동일합니다. 단, 메모리 최적화 테이블의 경우에는 보안 조건자로 사용되는 인라인 테이블 반환 함수를 고유하게 컴파일해야 합니다(WITH NATIVE_COMPILATION 옵션을 사용하여 함수를 작성해야 함). 자세한 내용은 [행 수준 보안](../../relational-databases/security/row-level-security.md#Limitations) 항목의 [기능 간 호환성](../../relational-databases/security/row-level-security.md) 섹션을 참조하세요.  
  
 행 수준 보안에 반드시 필요한 여러 기본 제공 보안 함수가 메모리 내 테이블에 사용할 수 있도록 설정되었습니다. 자세한 내용은 [고유하게 컴파일된 모듈의 기본 제공 함수](../../relational-databases/in-memory-oltp/supported-features-for-natively-compiled-t-sql-modules.md#bfncsp)를 참조하세요.  
  
 **EXECUTE AS CALLER** - 이제 모든 네이티브 모듈에서는 힌트를 지정하지 않더라도 EXECUTE AS CALLER를 기본적으로 지원하며 사용합니다. 호출하는 사용자의 컨텍스트에서 함수와 함수 내에서 사용되는 모든 기본 제공 함수를 평가할 수 있도록, 모든 행 수준 보안 조건자 함수는 EXECUTE AS CALLER를 사용하기 때문입니다.   
EXECUTE AS CALLER 사용 시에는 호출자의 권한 확인으로 인해 성능이 약간(약 10%) 저하됩니다. 모듈에서 EXECUTE AS OWNER 또는 EXECUTE AS SELF를 명시적으로 지정하는 경우에는 이러한 권한 검사 및 관련 성능 비용을 방지할 수 있습니다. 그러나 이 두 옵션 중 하나를 위의 기본 제공 함수와 함께 사용하면 필요한 컨텍스트 전환으로 인해 성능이 훨씬 더 많이 저하됩니다.  
  
## <a name="scenarios"></a>시나리오

[!INCLUDE[hek_1](../../includes/hek-1-md.md)] 를 사용하여 성능을 향상시킬 수 있는 일반적인 시나리오에 대한 간단한 설명은 [메모리 내 OLTP](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목

[메모리 내 OLTP&#40;메모리 내 최적화&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
