---
title: "온라인 인덱스 작업에 대한 지침 | Microsoft 문서"
ms.custom: 
ms.date: 07/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-indexes
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- clustered indexes, online operations
- online index operations
- indexes [SQL Server], online operations
- disk space [SQL Server], indexes
- nonclustered indexes [SQL Server], online operations
- transaction logs [SQL Server], indexes
ms.assetid: d82942e0-4a86-4b34-a65f-9f143ebe85ce
caps.latest.revision: 64
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 0c85f3e3417afc5943baee86eff0c3248172f82a
ms.openlocfilehash: 9b6d3aabe451c35c25822a2114e825e980ad01d3
ms.contentlocale: ko-kr
ms.lasthandoff: 07/31/2017

---
# <a name="guidelines-for-online-index-operations"></a>온라인 인덱스 작업에 대한 지침
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  온라인 인덱스 작업을 수행할 때 다음 지침이 적용됩니다.  
  
-   기본 테이블에 **image**, **ntext**및 **text**LOB(Large Object) 데이터 형식이 포함된 경우 클러스터형 인덱스는 오프라인으로 생성, 다시 작성 또는 삭제해야 합니다.  
  
-   테이블에 LOB 데이터 형식이 들어 있는 경우 비고유 비클러스터형 인덱스를 온라인 상태로 만들 수 있지만 이러한 열은 인덱스 정의에 키 또는 키가 아닌 포괄 열로 사용되지 않습니다.  
  
-   로컬 임시 테이블의 인덱스를 온라인 상태로 만들거나 다시 작성하거나 삭제할 수 없습니다. 이 제한 사항은 전역 임시 테이블의 인덱스에는 적용되지 않습니다.
- 예기치 않은 오류, 데이터베이스 장애 조치(failover) Ehsms **PAUSE** 명령 실행 후 중지된 위치에서 인덱스를 다시 시작할 수 있습니다. [Alter Index](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요. 이 기능은 SQL Server 2017 및 Azure SQL Database에 대한 공용 미리 보기입니다.

> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 지원되는 기능 목록은 [버전에서 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 다음 표는 온라인으로 수행할 수 있는 인덱스 작업, 이러한 온라인 작업에서 제외되는 인덱스 및 다시 시작 가능한 인덱스 제한을 보여 줍니다. 추가 제한 사항도 포함됩니다.  
  
| 온라인 인덱스 작업 | 제외되는 인덱스 | 기타 제한 사항 |  
|----------------------------|----------------------|------------------------|  
|ALTER  INDEX  REBUILD|비활성화된 클러스터형 인덱스 또는 비활성화된 인덱싱된 뷰<br /><br /> XML 인덱스<br /><br />columnstore 인덱스 <br /><br /> 로컬 임시 테이블의 인덱스|키워드를 ALL로 지정하면 테이블에 제외된 인덱스가 들어 있는 경우 작업이 실패할 수 있습니다.<br /><br /> 비활성 인덱스를 다시 작성하는 작업에 추가 제한 사항이 적용됩니다. 자세한 내용은 [인덱스 및 제약 조건 비활성화](../../relational-databases/indexes/disable-indexes-and-constraints.md)를 참조하세요.|  
|CREATE  INDEX|XML 인덱스<br /><br /> 뷰의 초기 고유 클러스터형 인덱스<br /><br /> 로컬 임시 테이블의 인덱스||  
|CREATE  INDEX  WITH  DROP_EXISTING|비활성화된 클러스터형 인덱스 또는 비활성화된 인덱싱된 뷰<br /><br /> 로컬 임시 테이블의 인덱스<br /><br /> XML 인덱스||  
|DROP  INDEX|비활성 인덱스<br /><br /> XML 인덱스<br /><br /> 비클러스터형 인덱스<br /><br /> 로컬 임시 테이블의 인덱스|단일 문에 여러 인덱스를 지정할 수 없습니다.|  
|ALTER  TABLE  ADD  CONSTRAINT(PRIMARY  KEY  또는 UNIQUE)|로컬 임시 테이블의 인덱스<br /><br /> 클러스터형 인덱스|한 번에 하나의 하위 절만 허용됩니다. 예를 들어 동일한 ALTER  TABLE  문에서 PRIMARY  KEY  또는 UNIQUE  제약 조건을 추가하거나 삭제할 수 없습니다.|  
|ALTER TABLE DROP CONSTRAINT(PRIMARY KEY 또는 UNIQUE)|클러스터형 인덱스||  
  
 온라인 인덱스 작업이 진행되는 동안에는 기본 테이블을 수정하거나 자르거나 삭제할 수 없습니다.  
  
 클러스터형 인덱스를 만들거나 삭제할 때 지정한 온라인 옵션 설정(ON  또는 OFF)은 다시 작성해야 하는 모든 비클러스터형 인덱스에 적용됩니다. 예를 들어 클러스터형 인덱스를 CREATE  INDEX  WITH  DROP_EXISTING,  ONLINE=ON을 사용하여 온라인 상태에서 작성한 경우 관련된 모든 비클러스터형 인덱스도 온라인 상태로 다시 만들어집니다.  
  
 UNIQUE  인덱스를 온라인 상태로 만들거나 다시 작성하면 인덱스 작성기 및 동시 사용자 트랜잭션이 동일한 키를 삽입하므로 고유성을 위반하게 됩니다. 원본 테이블의 원래 행이 대상인 새 인덱스로 옮겨지기 전에 사용자가 입력한 행이 새 인덱스로 삽입되면 온라인 인덱스 작업이 실패합니다.  
  
 자주 발생하지 않지만 온라인 인덱스 작업이 데이터베이스 업데이트와 상호 작용 시 사용자 또는 응용 프로그램 작업으로 인해 교착 상태가 될 수 있습니다. 이러한 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 에서는 해당 사용자 또는 응용 프로그램 작업을 교착 상태로 선택합니다.  
  
 여러 개의 새 비클러스터형 인덱스를 만들거나 비클러스터형 인덱스를 다시 구성할 때만 동일한 테이블 또는 뷰에서 동시 온라인 인덱스 DDL  작업을 수행할 수 있습니다. 동시에 수행된 다른 온라인 인덱스 작업이 모두 실패합니다. 예를 들어 동일한 테이블에서 기존 인덱스를 온라인 상태로 다시 작성하는 동안 새 인덱스를 온라인 상태로 만들 수 없습니다.  
  
 인덱스에 큰 개체 유형의 열이 포함되어 있고 동일한 트랜잭션에서 이 온라인 작업 전에 업데이트 작업이 있는 경우 온라인 작업을 수행할 수 없습니다. 이 문제를 해결하려면 온라인 작업을 트랜잭션 외부에 배치하거나 트랜잭션 내에서 업데이트 전에 배치합니다.  
  
## <a name="disk-space-considerations"></a>디스크 공간 고려 사항  
 온라인 인덱스 작업에는 오프라인 인덱스 작업보다 더 많은 디스크 공간 요구 사항이 필요합니다. 
 - 인덱스 만들기 및 인덱스 다시 빌드 작업 동안 빌드(또는 다시 빌드)할 인덱스에 대해 추가 공간이 필요합니다. 
 - 또한 임시 매핑 인덱스에 대해서도 디스크 공간이 필요합니다. 이 임시 인덱스는 클러스터형 인덱스를 만들거나 다시 작성하거나 삭제하는 온라인 인덱스 작업에 사용됩니다.
- 온라인 상태에서 클러스터형 인덱스를 삭제하는 작업은 온라인 상태에서 클러스터형 인덱스를 만드는 작업(또는 다시 빌드)에 필요한 공간과 동일한 크기가 필요합니다. 

자세한 내용은 [Disk Space Requirements for Index DDL Operations](../../relational-databases/indexes/disk-space-requirements-for-index-ddl-operations.md)을 참조하세요.  
  
## <a name="performance-considerations"></a>성능 고려 사항  
 온라인 인덱스 작업에서 동시 사용자 업데이트 작업을 할 수 있지만 업데이트 작업이 많은 경우에는 인덱스 작업을 하는 데 많은 시간이 소요됩니다. 일반적으로 온라인 인덱스 작업은 동시 업데이트 작업 수준과 상관없이 같은 양의 오프라인 인덱스 작업보다 느립니다.  
  
 온라인 인덱스 작업 동안 원본 및 대상 구조가 유지되므로 트랜잭션을 삽입하고,  업데이트하고,  삭제하는 데 최고 두 배까지 리소스 사용이 증가합니다. 이렇게 되면 인덱스 작업 동안 성능이 저하되며,  특히 CPU  시간 등의 리소스 사용이 증가합니다. 온라인 인덱스 작업이 모두 기록됩니다.  
  
 온라인 작업을 권장하지만 사용 환경 및 특정 요구 사항도 고려해야 합니다. 인덱스 작업을 오프라인 상태에서 실행하는 것이 가장 좋을 수도 있습니다. 이 경우 사용자가 작업 수행 동안 데이터 액세스를 제한하지만 작업은 더욱 빨리 끝나고 보다 적은 리소스를 사용합니다.  
  
 SQL Server 2016을 실행하는 다중 프로세서 컴퓨터에서는 다른 쿼리와 마찬가지로 인덱스 문이 추가 프로세서를 사용하여 인덱스 문과 관련된 검색 및 정렬 작업을 수행할 수 있습니다. MAXDOP 인덱스 옵션을 사용하여 온라인 인덱스 작업에만 사용되는 프로세서 수를 제어할 수 있습니다. 이 방법으로 인덱스 작업에서 사용하는 리소스와 동시 사용자가 사용하는 리소스의 균형을 맞출 수 있습니다. 자세한 내용은 [병렬 인덱스 작업 구성](../../relational-databases/indexes/configure-parallel-index-operations.md)을 참조하세요. 병렬 인덱스 작업을 지원하는 SQL Server에 대한 자세한 내용은 [버전에서 지원하는 기능](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 인덱스 작업의 마지막 단계에 S  잠금 또는 Sch-M  잠금이 보유되므로 BEGIN  TRANSACTION...COMMIT  블록 등의 명시적 사용자 트랜잭션 내에서 온라인 인덱스 작업을 실행할 때는 주의해야 합니다. 이 작업을 실행하면 트랜잭션이 끝날 때까지 잠금이 보유되어 사용자 동시성을 방해할 수 있습니다.  
  
 `MAX DOP > 1` 및 `ALLOW_PAGE_LOCKS = OFF` 옵션과 함께 실행할 수 있도록 허용된 경우 온라인 인덱스를 다시 빌드하면 조각이 늘어날 수 있습니다. 자세한 내용은 [작동 방법: 온라인 인덱스 다시 빌드 - 조각이 늘어날 수 있음](http://blogs.msdn.com/b/psssql/archive/2012/09/05/how-it-works-online-index-rebuild-can-cause-increased-fragmentation.aspx)을 참조하세요.  
  
## <a name="transaction-log-considerations"></a>트랜잭션 로그 고려 사항  
 오프라인 상태 또는 온라인 상태에서 수행되는 대규모 인덱스 작업은 트랜잭션 로그를 빨리 채워 대용량 데이터 로드를 생성할 수 있습니다. 인덱스 작업을 확실히 롤백하려면 인덱스 작업이 완료될 때까지 트랜잭션 로그를 자를 수 없지만,  인덱스 작업 중에 이 로그를 백업할 수 있습니다. 따라서 트랜잭션 로그에는 인덱스 작업을 수행하는 동안 인덱스 작업 트랜잭션 및 동시 사용자 트랜잭션을 모두 저장할 수 있는 충분한 공간이 있어야 합니다. 자세한 내용은 [Transaction Log Disk Space for Index Operations](../../relational-databases/indexes/transaction-log-disk-space-for-index-operations.md)을 참조하세요.  

## <a name="resumable-index-rebuild-considerations"></a>다시 시작 가능한 인덱스 다시 작성 시 고려 사항

> [!NOTE]
> [Alter Index](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요. 이 기능은 SQL Server 2017 및 Azure SQL Database에 대한 공용 미리 보기입니다.
>

다시 시작 가능한 온라인 인덱스 다시 작성을 수행할 때 다음 지침이 적용됩니다.
-   인덱스 유지 관리 기간 관리, 계획 및 확장. 유지 관리 기간에 맞게 인덱스 다시 작성 작업을 여러 번 일시 중지 및 다시 시작할 수 있습니다.
- 인덱스 다시 작성 오류 (예: 데이터베이스 장애 조치(failover)나 디스크 공간 부족)에서 복구
- 인덱스 작업이 일시 중지된 경우 원래 인덱스와 새로 만든 인덱스 모두 저장할 디스크 공간이 필요하고 DML 작업 중 업데이트해야 합니다.

- 인덱스 다시 작성 작업 중 잘림 로그의 잘림 지원(일반 온라인 인덱스 작업에서는 이 작업을 수행할 수 없음)
- SORT_IN_TEMPDB=ON 옵션이 지원되지 않음

> [!IMPORTANT]
> 다시 시작 가능한 다시 작성에서는 오래 실행되는 잘림을 계속 열어둘 필요가 없으므로 이 작업 중 로그 잘림이 허용되고 로그 공간을 더 효율적으로 관리할 수 있습니다. 새로운 디자인에서는 다시 시작 가능한 작업을 다시 시작하는 데 필요한 모든 참조와 함께 필요한 데이터를 하나의 데이터베이스에 유지할 수 있도록 했습니다.
>

일반적으로 온라인 인덱스 다시 작성 시 다시 시작 가능 여부에 따른 성능 차이는 없습니다. 다시 시작 가능한 인덱스를 업데이트할 때 인덱스 다시 작성 작업이 일시 중지되는 경우 다음과 같습니다.
- 읽기가 대부분인 작업의 경우 성능에 미치는 영향이 크지 않습니다. 
- 업데이트가 많은 작업의 경우 약간의 처리량 저하가 발생할 수 있습니다(테스트에 따르면 10% 미만의 저하가 나타남).

일반적으로 온라인 인덱스 다시 작성 시 다시 시작 가능 여부에 따른 조각 모음 품질 차이는 없습니다.
 
## <a name="related-content"></a>관련 내용  
 [온라인 인덱스 작업 작동 방식](../../relational-databases/indexes/how-online-index-operations-work.md)  
  
 [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)  
  
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
  

