---
title: 테이블 또는 저장 프로시저를 메모리 내 OLTP로 포팅해야 함
description: SQL Server Management Studio의 트랜잭션 성능 분석 보고서를 사용하여 메모리 내 OLTP로 데이터베이스 애플리케이션 성능을 향상시킬 수 있는지 여부를 평가합니다.
ms.custom: seo-dt-2019
ms.date: 08/02/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
helpviewer_keywords:
- Analyze, Migrate, Report
- AMR
ms.assetid: c1ef96f1-290d-4952-8369-2f49f27afee2
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5159591eeafc76ca16fde95f8a7b9789acc084e1
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97485315"
---
# <a name="determining-if-a-table-or-stored-procedure-should-be-ported-to-in-memory-oltp"></a>메모리 내 OLTP에 테이블 또는 저장 프로시저를 이식해야 하는지 확인
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 트랜잭션 성능 분석 보고서를 사용하면 메모리 내 OLTP를 통해 데이터베이스 애플리케이션의 성능이 향상될지 평가할 수 있습니다. 또한, 보고서는 애플리케이션에서 메모리 내 OLTP를 사용하도록 설정하기 위해 수행해야 하는 작업의 양도 나타냅니다. 메모리 내 OLTP에 이식할 디스크 기반 테이블을 식별한 후 [메모리 최적화 관리자](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md)를 사용하여 테이블을 마이그레이션할 수 있습니다. 마찬가지로 [Native Compilation Advisor](../../relational-databases/in-memory-oltp/native-compilation-advisor.md) 를 사용하여 저장 프로시저를 고유하게 컴파일된 저장 프로시저에 이식할 수 있습니다. 마이그레이션 방법에 대한 자세한 내용은 [메모리 내 OLTP – 일반적인 작업 패턴 및 마이그레이션 고려 사항](/previous-versions/dn673538(v=msdn.10))을 참조하세요.  
  
 트랜잭션 성능 분석 보고서는 프로덕션 데이터베이스 또는 프로덕션 작업과 유사한 활성 작업이 있는 테스트 데이터베이스에 대하여 직접 실행됩니다.  
  
 보고서 및 마이그레이션 관리자를 사용하면 다음 작업을 수행할 수 있습니다.  
  
-   작업을 분석하여 메모리 내 OLTP를 통해 성능 향상이 가능한 핫 스폿을 결정합니다. 트랜잭션 성능 분석 보고서는 메모리 내 OLTP로 변환할 경우 가장 이익이 되는 테이블과 저장 프로시저를 추천합니다.  
  
-   메모리 내 OLTP로 마이그레이션하는 작업을 계획하고 실행하는 데 도움이 됩니다. 디스크 기반 테이블에서 메모리 최적화 테이블로의 마이그레이션 경로는 시간이 많이 걸릴 수 있습니다. 메모리 최적화 관리자를 사용하여 테이블을 메모리 내 OLTP로 이동하기 전에 테이블에서 제거해야 하는 비호환성을 식별할 수 있습니다. 메모리 최적화 관리자는 메모리 액세스에 최적화된 테이블로의 테이블 마이그레이션이 애플리케이션에 미치는 영향을 이해하는 데도 도움이 됩니다.  
  
     메모리 내 OLTP로 마이그레이션을 계획할 때와 일부 테이블과 저장 프로시저를 메모리 내 OLTP로 마이그레이션하려고 작업할 때마다 메모리 내 OLTP가 애플리케이션에 도움이 되는지를 확인할 수 있습니다.  
  
    > [!IMPORTANT]  
    >  데이터베이스 시스템의 성능은 다양한 요소에 따라 달라지며 트랜잭션 성능 수집기 중 일부는 관찰하고 측정하지 못할 수도 있습니다. 따라서 트랜잭션 성능 분석 보고서는 실제 성능 향상 정도가 어떠한 예측과도 일치한다고 보증하지 않습니다.  
  
 트랜잭션 성능 분석 보고서 및 마이그레이션 관리자는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]을 설치 시 **관리 도구-기본** 또는 **관리 도구-고급** 을 선택하거나 [SQL Server Management Studio를 다운로드](../../ssms/download-sql-server-management-studio-ssms.md)할 때 SSMS(SQL Server Management Studio)의 일부로 설치됩니다.    
  
## <a name="transaction-performance-analysis-reports"></a>트랜잭션 성능 분석 보고서  
 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **보고서** 를 선택한 후 **표준 보고서** 를 선택하고 **트랜잭션 성능 분석 개요** 를 선택하여 **개체 탐색기** 에 트랜잭션 성능 분석 보고서를 생성할 수 있습니다. 의미 있는 분석 보고서를 생성하려면 데이터베이스에 활성 작업이 있거나 최근에 작업이 실행되어야 합니다.  
  
### <a name="tables"></a>테이블
  
 테이블에 대한 세부 정보 보고서는 다음 세 개의 섹션으로 구성됩니다.  
  
-   검색 통계 섹션  
  
     이 섹션에는 데이터베이스 테이블에 대한 검색에 대해 수집된 통계를 보여 주는 단일 테이블이 있습니다. 열은 다음과 같습니다.  
  
    -   총 액세스의 백분율. 전체 데이터베이스의 작업과 관련되어 이 테이블에서 수행된 검색에 대한 백분율입니다. 이 백분율이 높을수록 데이터베이스의 다른 테이블과 비교하여 해당 테이블이 더 많이 사용된 것입니다.  
  
    -   조회 통계/범위 검색 통계. 이 열은 프로파일링 동안 테이블에 대해 수행된 포인트 조회 및 범위 검색(인덱스 검색 및 테이블 검색) 수를 기록합니다. 트랜잭션당 평균이 예상치입니다.  
    
-   경합 통계 섹션  
  
     이 섹션에는 데이터베이스 테이블에 대한 경합을 보여 주는 테이블이 있습니다. 데이터베이스 래치 및 잠금에 대한 자세한 내용은 잠금 아키텍처를 참조하십시오. 열은 다음과 같습니다.  
  
    -   총 대기의 백분율. 데이터베이스 작업과 비교하여 이 데이터베이스 테이블에 대한 래치 및 잠금 대기에 대한 백분율입니다. 이 백분율이 높을수록 데이터베이스의 다른 테이블과 비교하여 해당 테이블이 더 많이 사용된 것입니다.  
  
    -   래치 통계. 이러한 열은 이 테이블의 관련 쿼리에 대한 래치 대기 수를 기록합니다. 래치에 대한 자세한 내용은 래칭을 참조하십시오. 이 숫자가 클수록 테이블에 대한 래치 경합이 더 큰 것입니다.  
  
    -   잠금 통계. 이 열 그룹은 이 테이블에 대한 페이지 잠금 획득 및 쿼리 대기 수를 기록합니다. 잠금에 대한 자세한 내용은 SQL Server의 잠금 이해를 참조하십시오. 대기가 많을수록 테이블에 대한 잠금 경합이 더 큰 것입니다.  
  
-   마이그레이션 문제 섹션  
  
     이 섹션에는 이 데이터베이스 테이블을 메모리 최적화 테이블로 변환할 때 발생한 문제를 보여 주는 테이블이 있습니다. 문제 등급이 높을수록 테이블 변환에 문제가 많은 것입니다. 이 데이터베이스 테이블을 변환하는 방법에 대한 자세한 내용을 보려면 메모리 최적화 관리자를 사용하십시오.  
  
테이블 세부 정보 보고서에 대한 검색 및 경합 통계는 sys.dm_db_index_operational_stats(Transact-SQL)에서 수집되고 집계됩니다.  

### <a name="stored-procedures"></a>저장 프로시저

 CPU 시간 대 경과 시간 비율이 높은 저장 프로시저는 마이그레이션 대상으로 적합합니다. 고유하게 컴파일된 저장 프로시저는 메모리 최적화 테이블을 참조만 할 수 있기 때문에 보고서에 모든 테이블 참조가 표시되므로 마이그레이션 비용이 추가될 수 있습니다.  
  
 저장 프로시저에 대한 세부 정보 보고서는 다음 두 개의 섹션으로 구성됩니다.  
  
-   실행 통계 섹션  
  
     이 섹션에는 저장 프로시저 실행에 대해 수집된 통계를 보여 주는 테이블이 포함됩니다. 열은 다음과 같습니다.  
  
    -   캐시된 시간. 이 실행 계획이 캐시된 시간입니다. 저장 프로시저가 계획 캐시에서 삭제되고 다시 입력될 때 각 캐시에 대한 시간이 발생합니다.  
  
    -   총 CPU 시간. 프로파일링 동안 저장 프로시저에서 사용한 총 CPU 시간입니다. 이 숫자가 클수록 저장 프로시저에서 CPU를 더 많이 사용한 것입니다.  
  
    -   총 실행 시간. 프로파일링 동안 저장 프로시저에서 사용한 총 실행 시간입니다. 이 숫자와 CPU 시간 간의 차이가 클수록 저장 프로시저에서 비효율적으로 CPU를 사용하는 것입니다.  
  
    -   누락된 총 캐시. 프로파일링 동안 저장 프로시저 실행으로 인해 발생한 캐시 누락(실제 스토리지에서 읽기) 수입니다.  
  
    -   실행 수. 프로파일링 동안 이 저장 프로시저가 실행한 횟수입니다.  
  
-   테이블 참조 섹션  
  
     이 섹션에는 이 저장 프로시저가 참조하는 테이블을 보여 주는 테이블이 있습니다. 저장 프로시저를 고유하게 컴파일된 저장 프로시저로 변환하기 전에 이러한 모든 테이블은 메모리 최적화 테이블로 변환되어야 하며 동일한 서버 및 데이터베이스에 있어야 합니다.  
  
 저장 프로시저 세부 정보 보고서에 대한 실행 통계는 sys.dm_exec_procedure_stats(Transact-SQL)에서 수집되고 집계됩니다. 참조는 sys.sql_expression_dependencies(TRANSACT-SQL)에서 가져옵니다.  
  
 저장 프로시저를 고유하게 컴파일된 저장 프로시저로 변환하는 방법을 자세히 알아보려면 네이티브 컴파일 관리자를 사용하십시오.  
  
## <a name="generating-in-memory-oltp-migration-checklists"></a>메모리 내 OLTP 마이그레이션 검사 목록 생성  
 마이그레이션 검사 목록은 메모리 최적화 테이블 또는 고유하게 컴파일된 저장 프로시저에서 지원되지 않는 모든 테이블 또는 저장 프로시저를 식별합니다. 메모리 최적화 및 네이티브 컴파일 관리자는 단일 디스크 기반 테이블 또는 해석된 T-SQL 저장 프로시저에 대한 검사 목록을 생성할 수 있습니다. 또한, 데이터베이스의 여러 테이블 및 저장 프로시저에 대한 마이그레이션 검사 목록을 생성하는 것도 가능합니다.  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 메모리 내 OLTP 마이그레이션 검사 목록 생성 **명령 또는 PowerShell을 사용하여** 내에 마이그레이션 검사 목록을 생성할 수 있습니다.  
  
**UI 명령을 사용하여 마이그레이션 검사 목록을 생성하려면**  
  
1.  **개체 탐색기** 에서 시스템 데이터베이스가 아닌 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크** 클릭한 후 **메모리 내 OLTP 마이그레이션 검사 목록 생성** 을 클릭합니다.  
  
2.  메모리 내 OLTP 마이그레이션 검사 목록 생성 대화 상자에서 다음을 클릭하여 **검사 목록 생성 옵션 구성** 페이지로 이동합니다. 이 페이지에서 다음을 수행합니다.  
  
    1.  **검사 목록 저장 위치** 상자에 폴더 경로를 입력합니다.  
  
    2.  **특정 테이블 및 저장 프로시저에 대한 검사 목록 생성** 이 선택되었는지 확인합니다.  
  
    3.  선택 상자에서 **테이블** 및 **저장 프로시저** 노드를 확장합니다.  
  
    4.  선택 상자에서 몇 가지 개체를 선택합니다.  
  
3.  **다음** 을 클릭하고 작업 목록이 **검사 목록 생성 옵션 구성** 페이지의 설정과 일치하는지 확인합니다.  
  
4.  **종료** 를 클릭한 후 선택한 개체에 대해서만 마이그레이션 검사 목록 보고서가 생성되었는지 확인합니다.  

 메모리 최적화 관리자 도구 및 네이티브 컴파일 관리자 도구에서 생성된 보고서와 비교하여 보고서의 정확성을 확인합니다. 자세한 내용은 [Memory Optimization Advisor](../../relational-databases/in-memory-oltp/memory-optimization-advisor.md) 및 [Native Compilation Advisor](../../relational-databases/in-memory-oltp/native-compilation-advisor.md)를 참조하세요.  
  
**SQL Server PowerShell을 사용하여 마이그레이션 검사 목록을 생성하려면**  
  
1.  **개체 탐색기** 에서 데이터베이스를 클릭한 다음 **PowerShell 시작** 을 클릭합니다. 다음과 같은 메시지가 표시되는지 확인합니다.  
  
    ```  
    PS SQLSERVER: \SQL\{Instance Name}\DEFAULT\Databases\{two-part DB Name}>  
    ```  
  
2.  다음 명령을 입력합니다.  
  
    ```  
    Save-SqlMigrationReport -FolderPath "<folder_path>"  
    ```  
  
3.  다음을 확인합니다.  
  
    -   존재하지 않는 경우 폴더 경로를 생성합니다.  
  
    -   마이그레이션 검사 목록 보고서는 데이터베이스의 모든 테이블 및 저장 프로시저에 대해 생성되고 보고서는 folder_path의 위치에 저장됩니다.  
  
**Windows PowerShell을 사용하여 마이그레이션 검사 목록을 생성하려면**  
  
1.  승격된 Windows PowerShell 세션을 시작합니다.  
  
2.  다음 명령을 입력합니다. 개체는 테이블 또는 저장 프로시저일 수 있습니다.  
  
    ```  
    [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SqlServer.SMO')  
  
    ```  
  
    ```  
    Save-SqlMigrationReport -Server "<instance_name>" -Database "<db_name>" -FolderPath "<folder_path1>"  
  
    ```  
  
    ```  
    Save-SqlMigrationReport -Server "<instance_name>" -Database "<db_name>" -Object <object_name> -FolderPath "<folder_path2>"  
  
    ```  
  
3.  다음을 확인합니다.  
  
    -   마이그레이션 검사 목록 보고서는 데이터베이스의 모든 테이블 및 저장 프로시저에 대해 생성되고 보고서는 folder_path에 저장됩니다.  
  
    -   <object_name>에 대한 마이그레이션 검사 목록 보고서는 folder_path2의 위치에 저장된 유일한 보고서입니다.  
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP로 마이그레이션](./plan-your-adoption-of-in-memory-oltp-features-in-sql-server.md)  
  
