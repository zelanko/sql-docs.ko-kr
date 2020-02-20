---
title: SQL Server의 스냅샷 격리
description: 트랜잭션 애플리케이션에서 차단을 줄이도록 설계된 행 버전 관리 메커니즘인 스냅샷 격리에 대한 지원을 설명합니다.
ms.date: 08/15/2019
dev_langs:
- csharp
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 2d2e27fafabc259be6bfbc0137b66e34d310f449
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75251153"
---
# <a name="snapshot-isolation-in-sql-server"></a>SQL Server의 스냅샷 격리

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

스냅샷 격리는 OLTP 애플리케이션의 동시성을 향상시킵니다.  
  
## <a name="understanding-snapshot-isolation-and-row-versioning"></a>스냅샷 격리 및 행 버전 관리 이해  
스냅샷 격리가 활성화되면 각 트랜잭션의 업데이트된 행 버전이 **tempdb**에 보관됩니다. 고유한 트랜잭션 시퀀스 번호가 각 트랜잭션을 식별하며 이러한 고유 번호는 각 행 버전에 대해 기록됩니다. 트랜잭션은 트랜잭션의 시퀀스 번호 앞에 시퀀스 번호가 있는 최신 행 버전에서 작동합니다. 트랜잭션이 시작된 후에 생성된 최신 행 버전은 트랜잭션에서 무시됩니다.  
  
"스냅샷" 이라는 용어는 트랜잭션의 모든 쿼리가 트랜잭션이 시작되는 시점의 데이터베이스 상태를 기반으로 데이터베이스의 동일한 버전 또는 스냅샷을 본다는 것을 의미합니다. 스냅샷 트랜잭션의 기본 데이터 행 또는 데이터 페이지에 대한 잠금은 획득되지 않으므로 이전의 미완료 트랜잭션에 의해 차단되지 않고 다른 트랜잭션을 실행할 수 있습니다. 데이터를 수정하는 트랜잭션은 데이터를 읽는 트랜잭션을 차단하지 않으며 데이터를 읽는 트랜잭션은 일반적으로 SQL Server의 기본 READ COMMITTED 격리 수준에 따라 데이터를 쓰는 트랜잭션을 차단하지 않습니다. 이 비차단 동작 덕분에 복잡한 트랜잭션에 대한 교착 상태의 가능성이 크게 줄어듭니다.  
  
스냅샷 격리는 낙관적 동시성 모델을 사용합니다. 스냅샷 트랜잭션이 시작된 이후 변경된 데이터에 대한 수정 내용을 커밋하려는 경우 트랜잭션이 롤백되고 오류가 발생합니다. 수정할 데이터에 액세스하는 SELECT 문에 대해 UPDLOCK 힌트를 사용하여 이를 방지할 수 있습니다. 자세한 내용은 SQL Server 온라인 설명서 "잠금 힌트"를 참조하세요.  
  
스냅샷 격리는 트랜잭션에 사용하기 전에 ALLOW_SNAPSHOT_ISOLATION 데이터베이스 옵션을 ON으로 설정하여 사용하도록 설정해야 합니다. 이렇게 하면 임시 데이터베이스인 **tempdb**에 행 버전을 저장하는 메커니즘이 활성화됩니다. Transact-SQL ALTER DATABASE 문과 함께 사용하는 각 데이터베이스에서 스냅샷 격리를 사용하도록 설정해야 합니다. 이러한 점에서 스냅샷 격리는 구성을 필요로 하지 않는 기존 격리 수준 READ COMMITTED, REPEATABLE READ, SERIALIZABLE 및 READ UNCOMMITTED와는 다릅니다. 다음 문은 스냅샷 격리를 활성화하고 기본 READ COMMITTED 동작을 SNAPSHOT으로 바꿉니다.  
  
```sql  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
READ_COMMITTED_SNAPSHOT 옵션을 ON으로 설정하면 기본 READ COMMITTED 격리 수준에서 버전이 지정된 행에 액세스할 수 있습니다. READ_COMMITTED_SNAPSHOT 옵션이 OFF로 설정되어 있으면 버전이 지정된 행에 액세스하기 위해 각 세션마다 스냅샷 격리 수준을 명시적으로 설정해야 합니다.  
  
## <a name="managing-concurrency-with-isolation-levels"></a>격리 수준을 사용하여 동시성 관리  
Transact-SQL 문이 실행되는 격리 수준에 따라 잠금 및 행 버전 관리 동작이 결정됩니다. 격리 수준은 전체 연결 범위를 가지며 SET TRANSACTION ISOLATION LEVEL 문을 사용하여 연결에 대해 설정되면 연결이 닫히거나 다른 격리 수준이 설정될 때까지 계속 적용됩니다. 연결이 닫히고 풀로 반환되면 마지막 SET TRANSACTION ISOLATION LEVEL 문의 격리 수준이 유지됩니다. 풀링된 연결을 다시 사용하는 후속 연결은 연결이 풀링되는 시점에 적용된 격리 수준을 사용합니다.  
  
연결 내에서 실행된 개별 쿼리에는 단일 문 또는 트랜잭션에 대한 격리를 수정하는 잠금 힌트가 포함될 수 있지만 연결의 격리 수준에는 영향을 주지 않습니다. 저장 프로시저 또는 함수에서 설정된 격리 수준 또는 잠금 힌트는 이를 호출하는 연결의 격리 수준을 변경하지 않으며 저장 프로시저 또는 함수 호출 기간 동안만 적용됩니다.  
  
이전 버전의 SQL Server에서는 SQL-92 표준에 정의된 네 가지 격리 수준이 지원되었습니다.  
  
- READ UNCOMMITTED 다른 트랜잭션에 의해 배치된 잠금을 무시하므로 가장 제한적인 격리 수준입니다. READ UNCOMMITTED로 실행 중인 트랜잭션은 다른 트랜잭션에서 아직 커밋되지 않은 수정된 데이터 값을 읽을 수 있습니다. 이를 "더티" 읽기라고 합니다.  
  
- READ COMMITTED는 SQL Server의 기본 격리 수준입니다. 이를 통해 다른 트랜잭션에 의해 수정되었지만 아직 커밋되지 않은 데이터 값을 문이 읽을 수 없도록 지정하여 더티 읽기를 방지할 수 있습니다. 다른 트랜잭션은 여전히 현재 트랜잭션의 개별 문 실행 사이에 데이터를 수정, 삽입 또는 삭제할 수 있습니다. 이 경우 반복되지 않은 읽기 또는 "가상" 데이터가 생성됩니다.  
  
- REPEATABLE READ는 READ COMMITTED보다 더 제한적인 격리 수준입니다. READ COMMITTED를 포함하며, 현재 트랜잭션이 커밋될 때까지 다른 트랜잭션이 현재 트랜잭션에서 읽은 데이터를 수정하거나 삭제할 수 없도록 지정합니다. 읽기 데이터의 공유 잠금은 각 문이 끝날 때 해제되지 않고 트랜잭션 기간 동안 유지되기 때문에 동시성이 READ COMMITTED보다 낮습니다.  
  
- SERIALIZABLE은 전체 키 범위를 잠그고 트랜잭션이 완료될 때까지 해당 잠금을 보유하므로 격리 수준 중에서 가장 제한적입니다. REPEATABLE READ를 포함하며 트랜잭션이 완료될 때까지 다른 트랜잭션이 새 행을 현재 트랜잭션에서 읽은 범위에 삽입할 수 없다는 제한을 추가합니다.  
  
더 자세한 내용은 [트랜잭션 잠금 및 행 버전 관리 지침](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)을 참조하세요.  
  
### <a name="snapshot-isolation-level-extensions"></a>스냅샷 격리 수준 확장  
SQL Server에서는 SNAPSHOT 격리 수준을 도입하고 READ COMMITTED를 추가로 구현함으로써 SQL-92 격리 수준이 확장되었습니다. READ_COMMITTED_SNAPSHOT 격리 수준은 모든 트랜잭션에 대해 READ COMMITTED를 투명하게 대체할 수 있습니다.  
  
- SNAPSHOT 격리는 트랜잭션 내에서 읽은 데이터에 다른 동시 트랜잭션이 변경한 내용을 반영하지 않도록 지정합니다. 트랜잭션은 트랜잭션이 시작할 때 존재하는 데이터 행 버전을 사용합니다. 데이터를 읽을 때 데이터에 잠금이 배치되지 않으므로 SNAPSHOT 트랜잭션은 다른 트랜잭션이 데이터를 쓰지 못하도록 차단하지 않습니다. 데이터를 쓰는 트랜잭션은 스냅샷 트랜잭션의 데이터 읽기를 차단하지 않습니다. 사용하려면 ALLOW_SNAPSHOT_ISOLATION 데이터베이스 옵션을 설정하여 스냅샷 격리를 사용하도록 설정해야 합니다.  
  
- 데이터베이스에서 스냅샷 격리를 사용하는 경우 READ_COMMITTED_SNAPSHOT 데이터베이스 옵션이 READ COMMITTED 격리 수준의 기본 동작을 결정합니다. READ_COMMITTED_SNAPSHOT을 명시적으로 ON으로 지정하지 않으면 READ COMMITTED는 모든 암시적 트랜잭션에 적용됩니다. 이렇게 하면 READ_COMMITTED_SNAPSHOT OFF(기본값)를 설정하는 것과 동일한 동작이 생성됩니다. READ_COMMITTED_SNAPSHOT OFF가 적용되는 경우 데이터베이스 엔진은 공유 잠금을 사용하여 기본 격리 수준을 적용합니다. READ_COMMITTED_SNAPSHOT 데이터베이스 옵션을 ON으로 설정하면 데이터베이스 엔진이 잠금을 사용하여 데이터를 보호하는 대신 행 버전 관리 및 스냅샷 격리를 기본값으로 사용합니다.  
  
## <a name="how-snapshot-isolation-and-row-versioning-work"></a>스냅샷 격리 및 행 버전 관리 작동 방식  
SNAPSHOT 격리 수준이 활성화된 경우 행이 업데이트될 때마다 SQL Server 데이터베이스 엔진에서 **tempdb**에 원래 행의 복사본을 저장하고 행에 트랜잭션 시퀀스 번호를 추가합니다. 다음은 이벤트가 발생하는 순서입니다.  
  
1. 새 트랜잭션이 시작되고 트랜잭션 시퀀스 번호가 할당됩니다.  
  
2. 데이터베이스 엔진이 트랜잭션 내에서 행을 읽고 트랜잭션 시퀀스 번호보다 낮으면서 시퀀스 번호에 가장 근접한 행 버전을 **tempdb**에서 검색합니다.  
  
3. 데이터베이스 엔진은 트랜잭션 시퀀스 번호가 스냅샷 트랜잭션이 시작될 때 활성 상태인 커밋되지 않은 트랜잭션의 트랜잭션 시퀀스 번호 목록에 있지 않은지 확인합니다.  
  
4. 트랜잭션에서 트랜잭션을 시작할 당시의 행 버전을 **tempdb**에서 읽습니다. 트랜잭션이 시작된 후 삽입된 새 행은 표시되지 않습니다. 이러한 시퀀스 번호 값이 트랜잭션 시퀀스 번호 값보다 높기 때문입니다.  
  
5. **tempdb**에 시퀀스 번호 값이 낮은 행 버전이 있으므로 현재 트랜잭션에서 트랜잭션이 시작된 후 삭제된 행이 표시됩니다.  
  
스냅샷 격리의 결과는 트랜잭션이 기본 테이블에 대한 잠금을 준수 또는 배치하지 않고 트랜잭션이 시작할 때 존재한 모든 데이터를 확인하는 것입니다. 그러므로 경합이 있는 경우 성능이 향상될 수 있습니다.  
  
스냅샷 트랜잭션은 항상 낙관적 동시성 제어를 사용하여 다른 트랜잭션이 행을 업데이트하지 못하게 하는 잠금을 보류합니다. 스냅샷 트랜잭션이 트랜잭션 시작 후 변경된 행에 업데이트를 커밋하려고 하면 트랜잭션이 롤백되고 오류가 발생합니다.  
  
## <a name="working-with-snapshot-isolation-in-adonet"></a>ADO.NET에서 스냅샷 격리 사용  
스냅샷 격리는 ADO.NET에서 <xref:Microsoft.Data.SqlClient.SqlTransaction> 클래스를 통해 지원됩니다. 데이터베이스가 스냅샷 격리에 대해 활성화되었지만 READ_COMMITTED_SNAPSHOT ON에 대해 구성되지 않은 경우 <xref:Microsoft.Data.SqlClient.SqlConnection.BeginTransaction%2A> 메서드를 호출할 때 **IsolationLevel.Snapshot** 열거형 값을 사용하여 <xref:Microsoft.Data.SqlClient.SqlTransaction>을 시작해야 합니다. 이 코드 조각에서는 연결이 열린 <xref:Microsoft.Data.SqlClient.SqlConnection> 개체인 것으로 가정합니다.  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### <a name="example"></a>예제  
다음 예제는 잠긴 데이터에 액세스하려고 시도하여 여러 격리 수준이 어떻게 동작하는지 보여 주며 프로덕션 코드에서는 사용할 수 없습니다.  
  
이 코드에서는 SQL Server의 **AdventureWorks** 샘플 데이터베이스에 연결하고 **TestSnapshot**이라는 테이블을 만들어 데이터 행 하나를 삽입합니다. 이 코드는 ALTER DATABASE Transact-SQL 문을 사용하여 데이터베이스에 스냅샷 격리를 설정하지만 READ_COMMITTED_SNAPSHOT 옵션을 설정하지 않으므로 기본 READ COMMITTED 격리 수준 동작이 그대로 적용됩니다. 그런 다음 코드는 다음 작업을 수행합니다.  
  
1. SERIALIZABLE 격리 수준을 사용하여 업데이트 트랜잭션을 시작하는 sqlTransaction1을 시작하되 완료하지는 않습니다. 이렇게 하면 테이블을 잠그는 효과가 있습니다.  
  
2. 두 번째 연결을 열고 SNAPSHOT 격리 수준을 사용하여 두 번째 트랜잭션을 시작함으로써 **TestSnapshot** 테이블의 데이터를 읽습니다. 스냅샷 격리를 사용하도록 설정했으므로 이 트랜잭션은 sqlTransaction1이 시작하기 전에 존재했던 데이터를 읽을 수 있습니다.  
  
3. 세 번째 연결을 열고 READ COMMITTED 격리 수준을 사용하여 트랜잭션을 시작해 테이블의 데이터를 읽으려고 시도합니다. 이 경우 첫 번째 트랜잭션에서 테이블에 있는 잠금을 통과하여 읽을 수 없기 때문에 코드에서 데이터를 읽을 수 없으며 제한 시간이 초과됩니다. REPEATABLE READ 및 SERIALIZABLE 격리 수준에서도 첫 번째 트랜잭션에 있는 잠금을 통과하여 읽을 수 없으므로 이러한 격리 수준이 사용되는 경우 동일한 결과가 발생합니다.  
  
4. 네 번째 연결을 열고 READ UNCOMMITTED 격리 수준을 사용하여 트랜잭션을 시작합니다. 그러면 sqlTransaction1의 커밋되지 않은 값에 대한 더티 읽기가 수행됩니다. 첫 번째 트랜잭션이 커밋되지 않으면 이 값은 실제로는 데이터베이스에 절대 존재할 수 없습니다.  
  
5. **TestSnapshot** 테이블을 삭제하고 **AdventureWorks** 데이터베이스의 스냅샷 격리 기능을 해제하여 첫 번째 트랜잭션을 롤백하고 정리합니다.  
  
> [!NOTE]
>  다음 예제에서는 연결 풀링이 해제된 상태에서 동일한 연결 문자열을 사용합니다. 연결이 풀링된 경우 해당 격리 수준을 다시 설정 해도 서버에서 격리 수준이 다시 설정되지 않습니다. 따라서 풀링된 내부 연결을 사용하는 후속 연결은 풀링된 연결의 격리 수준이 설정된 상태로 시작합니다. 연결 풀링을 해제하는 또 다른 방법은 각 연결에 대해 명시적으로 격리 수준을 설정하는 것입니다.  
  
[!code-csharp[DataWorks Isolation_Snapshot.Demo#1](~/../sqlclient/doc/samples/Isolation_Snapshot.cs#1)]
  
### <a name="example"></a>예제  
다음 예제에서는 데이터를 수정하는 경우의 스냅샷 격리 동작을 보여 줍니다. 코드는 다음 작업을 수행합니다.  
  
1. **AdventureWorks** 샘플 데이터베이스에 연결하고 SNAPSHOT 격리를 활성화합니다.  
  
2. **TestSnapshotUpdate**라는 테이블을 만들고 샘플 데이터의 행 세 개를 삽입합니다.  
  
3. 스냅샷 격리를 사용하여 sqlTransaction1을 시작하되 완료하지는 않습니다. 트랜잭션에서 세 개의 데이터 행이 선택됩니다.  
  
4. **AdventureWorks**에 대한 두 번째 **SqlConnection**을 만들고 sqlTransaction1에서 선택한 행 중 하나에서 값을 업데이트하는 READ COMMITTED 격리 수준을 사용하여 두 번째 트랜잭션을 만듭니다.  
  
5. sqlTransaction2를 커밋합니다.  
  
6. sqlTransaction1로 돌아가 sqlTransaction1이 이미 커밋한 동일한 행을 업데이트하려고 시도합니다. 오류 3960이 발생하고 sqlTransaction1이 자동으로 롤백됩니다. 콘솔 창에 **SqlException.Number** 및 **SqlException.Message**가 표시됩니다.  
  
7. **AdventureWorks**에서 스냅샷 격리를 해제하고 **TestSnapshotUpdate** 테이블을 삭제할 정리 코드를 실행합니다.  
  
    [!code-csharp[DataWorks Isolation_Snapshot1#1](~/../sqlclient/doc/samples/Isolation_Snapshot1.cs#1)]
  
### <a name="using-lock-hints-with-snapshot-isolation"></a>스냅샷 격리와 함께 잠금 힌트 사용  
이전 예제에서는 첫 번째 트랜잭션이 데이터를 선택하고, 첫 번째 트랜잭션이 완료되기 전에 두 번째 트랜잭션이 데이터를 업데이트하여 첫 번째 트랜잭션이 같은 행을 업데이트하려고 할 때 업데이트 충돌이 발생합니다. 트랜잭션 시작 부분에 잠금 힌트를 제공하여 장기 실행 스냅샷 트랜잭션에서 업데이트 충돌이 발생할 가능성을 줄일 수 있습니다. 다음 SELECT 문은 UPDLOCK 힌트를 사용하여 선택된 행을 잠급니다.  
  
```sql  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
UPDLOCK 잠금 힌트를 사용하면 첫 번째 트랜잭션이 완료되기 전에 행을 업데이트하려고 시도하는 모든 행이 차단됩니다. 그러면 선택한 행이 트랜잭션에서 나중에 업데이트될 때 충돌이 발생하지 않습니다. SQL Server 온라인 설명서의 "잠금 힌트"를 참조하세요.  
  
애플리케이션에 충돌이 많은 경우 스냅샷 격리를 선택하지 않는 것이 좋습니다. 힌트는 정말 필요한 경우에만 사용해야 합니다. 지속적으로 잠금 힌트를 사용하여 작업을 수행하도록 애플리케이션을 디자인하면 안 됩니다.  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server 및 ADO.NET](index.md)
- [트랜잭션 잠금 및 행 버전 관리 지침](../../../relational-databases/sql-server-transaction-locking-and-row-versioning-guide.md)
