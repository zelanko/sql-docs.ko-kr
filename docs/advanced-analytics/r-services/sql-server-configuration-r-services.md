---
title: "SQL Server 구성 (R 서비스) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server 구성 (R 서비스)
이 섹션의 정보 사용 되는 컴퓨터의 하드웨어 및 네트워크 구성에 대 한 일반적인 지침 제공 호스트로 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다. 일반 외에도 고려해 야 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 성능 튜닝에 제공 된 정보는 [SQL Server 데이터베이스 엔진 및 Azure SQL 데이터베이스에 대 한 성능 센터](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)합니다.

## 프로세서

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 시스템에서 사용 가능한 코어를 사용 하 여 병렬에서 작업을 수행할 수 있습니다. 를 사용할 수 있는 더 많은 코어 성능이 좋아집니다. 이후 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 일반적으로 사용 되는 여러 사용자가 동시에, 데이터베이스 관리자가 결정 해야 이상적인 최대 작업 부하 계산 지 원하는 데 필요한 코어 수입니다. CPU 바인딩된 알고리즘 IO 바인딩된 작업에 대 한 코어 수가 도움이 되지 않을 수, 하는 동안 많은 코어와 더 빠른 Cpu에서 이점을 얻을 수 있습니다.

## 메모리

컴퓨터에서 사용 가능한 메모리 양을 고급 분석 알고리즘의 성능에 큰 영향을 줄 수 있습니다. 메모리가 부족 하 여 SQL 계산 컨텍스트를 사용 하는 경우 병렬 처리 수준에 영향을 줄 수 있습니다. 처리할 수 있는 청크 크기 (행 읽기 작업당) 및 지원할 수 있는 동시 세션 수에도 영향을 줄 수 있습니다.

32GB의 최소값을 사용 하는 것이 좋습니다. 32 g B 이상의 사용 가능한 경우에 성능 향상을 위해 모든 읽기 작업에 더 많은 행을 사용 하 여 SQL 데이터 소스를 구성할 수 있습니다.

## 전원 옵션

Windows 운영 체제에는 __고성능__ 전원 옵션을 사용 해야 합니다. 다른 전원 설정을 사용 하 여 하면 성능이 저하 되거나 일치 하지 않는 사용 하는 경우 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다.

## 디스크 IO

사용 하 여 학습 및 예측 작업 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] IO은 본질적으로 바인딩되고 데이터베이스에 저장 되어 있는 디스크의 속도에 따라 달라 집니다. 솔리드 스테이트 드라이브 (SSD)와 같은 고속 드라이브 도움이 될 수 있습니다. 

디스크에 액세스 하는 다른 응용 프로그램에서 디스크 IO 영향도: 예를 들어, 다른 클라이언트가 데이터베이스에 대해 작업을 읽고 있습니다. 디스크 IO 성능 파일 시스템에서 사용 되는 블록 크기 등 사용 중인 파일 시스템의 설정으로도 적용 될 수 있습니다. 여러 드라이브를 사용할 수 있는 경우 다른 드라이브에서 데이터베이스를 저장할 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 에 대 한 요청 하므로 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 동일한 디스크에 도달 하지 데이터베이스에 저장 된 데이터에 대 한 요청으로 합니다.

디스크 IO 학습 하는 동안 여러 차례 반복을 사용 하는 RevoScaleR 분석 함수를 실행 하는 경우 성능 영향을 크게 수 있습니다. 예를 들어 `rxLogit`, `rxDTree`, `rxDForest` 및 `rxBTrees` 모두 여러 차례 반복을 사용 합니다. 데이터 원본의 경우 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], 이러한 알고리즘으로 데이터를 캡처하기 위해 최적화 된 임시 파일을 사용 합니다. 이러한 파일은 자동으로 세션 완료 된 후 정리 합니다. 읽기/쓰기 작업에 대 한 고성능 디스크를 가진 이러한 알고리즘에 대 한 전체 경과 된 시간을 크게 향상 시킬 수 있습니다.

> [!NOTE]
> [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Windows 운영 체제에서 8.3 파일 이름을 지원을 해야합니다. Fsutil.exe 드라이브 8.3 파일을 지원 하는지 여부를 확인 하거나 지원을 사용 하도록 설정 하지 않으면 사용할 수 있습니다. Fsutil.exe 8.3 파일 사용에 대 한 자세한 내용은 참조 하십시오. [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)합니다.

### 테이블 압축

IO 성능은 압축 또는 columstore 인덱스를 사용 하 여 자주 향상 될 수 있습니다. 일반적으로 데이터 columnstore 인덱스를 사용 하 여 활용 이러한 반복 데이터를 압축 하므로 자주 테이블 내에서 여러 열에서 반복 됩니다.

Columnstore 인덱스 다양 한 테이블에 대 한 삽입 하는 경우 효율적인 않지만 데이터는 정적 또는 자주 변경 되지 않는 경우에 것이 좋습니다. 칼럼 형식 저장소 적합 하지 않은 행 주 테이블에 압축을 사용 하도록 설정 IO를 개선 하기 위해 사용 수 있습니다.

자세한 내용은 다음 문서를 참조 합니다.

* [데이터 압축](../../relational-databases/data-compression/data-compression.md)

* [테이블 또는 인덱스에 압축 사용](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [Columnstore 인덱스 가이드](Columnstore%20Indexes%20Guide.md)

## 페이징 파일

Windows 운영 체제는 페이징 파일을 사용 하 여 크래시 덤프를 관리 하 고 가상 메모리 페이지를 저장 하기 위한 합니다. 과다 한 페이징이 보면 컴퓨터에 실제 메모리를 늘려 하는 것이 좋습니다. 하지만 더 많은 실제 메모리 페이징 제거 하지 않습니다, 페이징에 대 한 필요성을 저하 됩니다.

페이지 파일에 저장 되어 있는 디스크 속도 성능에 영향을 수도 있습니다. SSD가에 페이지 파일을 저장 하거나 여러 SSDs에서 여러 페이지 파일을 사용 하 여 성능을 향상 시킬 수 있습니다.

참조 [64 비트 버전의 Windows에 대 한 적절 한 페이지 파일 크기를 결정 하는 방법을](https://support.microsoft.com/en-us/kb/2860880) 페이지 파일 크기 조정에 대 한 내용은 합니다.

## 리소스 관리

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 리소스 관리를 사용 하는 다양 한 리소스를 제어 하기 위한 지원 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]합니다. 예를 들어 r 메모리 사용에 대 한 기본값은 20%의 사용 가능한 총 메모리 제한 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]합니다. 이렇게 되도록 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 워크플로 심각 하 게 오랫동안 실행 되는 R 작업으로 영향을 받지 않습니다. 그러나 데이터베이스 관리자가 이러한 한도 변경할 수 있습니다. 

제한 된 리소스는 __MAX_CPU_PERCENT__, __MAX_MEMORY_PERCENT__, 및 __MAX_PROCESSES__합니다. 현재 설정을 보려면 사용 하 여이 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 문:

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

경우 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 주로 R 서비스에 대 한 사용, 것이 좋습니다 MAX_CPU_PERCENT 40% 또는 60% 증가 합니다. 하는 경우 동일한를 사용 하 여 많은 R 세션이 있을 수 있습니다 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 는 동시에 세 가지 모두 증가 합니다. 할당 된 리소스 값을 변경 하려면 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 문입니다. 

메모리 사용량을 40%로 설정 하는이 예제:

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
다음 예제에서는 세 가지 구성 가능한 값을 설정합니다.
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> 문을 실행을 즉시 적용 하는 이러한 설정을 변경 하려면 `ALTER RESOURCE GOVERNOR RECONFIGURE` 메모리, CPU, 또는 최대 프로세스 설정을 변경한 후입니다. 

## 관련 항목:
[리소스 관리자](../../relational-databases/resource-governor/resource-governor.md)

[외부 리소스 풀 만들기](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R 서비스 성능 조정 가이드](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [성능 사례 연구](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 및 데이터 최적화](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)