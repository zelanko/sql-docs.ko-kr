---
title: Tempdb 데이터베이스-병렬 데이터 웨어하우스 | Microsoft Docs
description: 병렬 데이터 웨어하우스의 Tempdb 데이터베이스.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6bdba302778224ab2615018d6c5dec0740328d93
ms.sourcegitcommit: 495913aff230b504acd7477a1a07488338e779c6
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810943"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스의 tempdb 데이터베이스
**tempdb** 는 사용자 데이터베이스에 대 한 로컬 임시 테이블을 저장 하는 SQL Server PDW 시스템 데이터베이스입니다. 임시 테이블은 일반적으로 쿼리 성능을 향상 시키는 데 사용 됩니다. 예를 들어 임시 테이블을 사용 하 여 스크립트를 모듈화 계산 된 데이터를 다시 사용할 수 있습니다.  
  
시스템 데이터베이스에 대 한 자세한 내용은 [시스템 데이터베이스](system-databases.md)를 참조 하세요.  
  
## <a name="Basics"></a>주요 용어 및 개념  
*로컬 임시 테이블*  
*로컬 임시 테이블* 은 테이블 이름 앞에 # 접두사를 사용 하 고는 로컬 사용자 세션에서 만든 임시 테이블입니다. 각 세션은 자체 세션에 대해 로컬 임시 테이블의 데이터에만 액세스할 수 있습니다.  
  
각 세션은 모든 세션에서 로컬 임시 테이블에 대 한 메타 데이터를 볼 수 있습니다. 예를 들어 모든 세션은 `SELECT * FROM tempdb.sys.tables` 쿼리를 사용 하 여 모든 로컬 임시 테이블에 대 한 메타 데이터를 볼 수 있습니다.  
  
전역 임시 테이블  
이 SQL Server PDW 릴리스에서는 # # 구문을 사용 하 여 SQL Server에서 지원 되는 *전역 임시 테이블*은 지원 되지 않습니다.  
  
pdwtempdb  
**pdwtempdb** 는 로컬 임시 테이블을 저장 하는 데이터베이스입니다.  
  
PDW는 SQL Server**tempdb** 데이터베이스를 사용 하 여 임시 테이블을 구현 하지 않습니다. 대신 PDW는 이러한 데이터베이스를 pdwtempdb 라는 데이터베이스에 저장 합니다. 이 데이터베이스는 각 계산 노드에 있으며 PDW 인터페이스를 통해 사용자에 게 표시 되지 않습니다. 관리 콘솔의 저장소 페이지에는 **tempdb-sql**이라는 PDW 시스템 데이터베이스에 대 한이 표시 됩니다.  
  
tempdb  
tempdb는 tempdb 데이터베이스 SQL Server 합니다. 최소 로깅을 사용 합니다. SQL Server는 계산 노드에서 tempdb를 사용 하 여 SQL Server 작업을 수행 하는 과정에 필요한 임시 테이블을 저장 합니다.  
  
SQL Server PDW은 다음과 같은 경우 **tempdb** 에서 테이블을 삭제 합니다.  
  
-   DROP TABLE 문이 실행 됩니다.  
  
-   세션의 연결이 끊겼습니다. 세션에 대 한 임시 테이블만 삭제 됩니다.  
  
-   기기가 종료 되었습니다.  
  
-   제어 노드에 클러스터 장애 조치가 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
명시적으로 다르게 지정 되지 않는 한 SQL Server PDW 임시 테이블 및 영구 테이블에 대해 동일한 작업을 수행 합니다. 예를 들어 영구 테이블과 마찬가지로 로컬 임시 테이블의 데이터는 계산 노드 간에 분산 또는 복제 됩니다.  
  
## <a name="LimitationsRestrictions"></a>제한 사항  
SQL Server PDW**tempdb** 데이터베이스에 대 한 제한 사항입니다. 다음을 할 *수 없습니다.*  
  
-   # #으로 시작 하는 전역 임시 테이블을 만듭니다.  
  
-   **Tempdb**의 백업 또는 복원을 수행 합니다.  
  
-   **GRANT**, **DENY**또는 **REVOKE** 문을 사용 하 여 **tempdb** 에 대 한 권한을 수정 합니다.  
  
-   **Tempdb**tempdb에 대해 **DBCC SHRINKLOG** 를 실행 합니다.  
  
-   **Tempdb**에서 DDL 작업을 수행 합니다. 이에 대 한 몇 가지 예외가 있습니다. 자세한 내용은 로컬 임시 테이블에 대 한 제한 사항 및 제한 사항 목록을 참조 하세요.  
  
로컬 임시 테이블에 대 한 제한 사항입니다. 다음을 할 *수 없습니다.*  
  
-   임시 테이블 이름 바꾸기  
  
-   임시 테이블에서 파티션, 뷰 또는 비클러스터형 인덱스를 만듭니다. **ALTER INDEX** 는 클러스터형 인덱스를 사용 하 여 만든 테이블에 대 한 클러스터형 인덱스를 다시 작성 하는 데 사용할 수 있습니다.  
  
-   GRANT, DENY 또는 REVOKE 문을 사용 하 여 임시 테이블에 대 한 사용 권한을 수정 합니다.  
  
-   임시 테이블에서 데이터베이스 콘솔 명령을 실행 합니다.  
  
-   동일한 일괄 처리 내에서 둘 이상의 임시 테이블에 동일한 이름을 사용 합니다. 일괄 처리 내에서 둘 이상의 로컬 임시 테이블을 사용하는 경우 각각에 고유 이름이 있어야 합니다. 여러 세션이 동일한 일괄 처리를 실행 하 고 동일한 로컬 임시 테이블을 만드는 경우 SQL Server PDW는 내부적으로 로컬 임시 테이블 이름에 숫자 접미사를 추가 하 여 각 로컬 임시 테이블에 고유한 이름을 유지 합니다.  
  
> [!NOTE]  
> 임시 테이블에 대 한 통계를 만들고 업데이트할 *수* 있습니다. **ALTER INDEX** 는 클러스터형 인덱스를 다시 작성 하는 데 사용할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
모든 사용자가 tempdb에 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다. tempdb 연결 권한을 취소하여 사용자가 tempdb를 사용하지 못하도록 할 수 있지만 일부 일상적인 작업에서 tempdb를 사용해야 하므로 권장하지 않습니다.  
  
## <a name="RelatedTasks"></a>관련 태스크  
  
|태스크|설명|  
|---------|---------------|  
|**Tempdb**에 테이블을 만듭니다.|CREATE TABLE 및 CREATE TABLE SELECT 문으로 사용자 임시 테이블을 만들 수 있습니다. 자세한 내용은 [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) 및 [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)를 참조 하세요.|  
|**Tempdb**의 기존 테이블 목록을 표시 합니다.|`SELECT * FROM tempdb.sys.tables;`|  
|**Tempdb**의 기존 열 목록을 표시 합니다.|`SELECT * FROM tempdb.sys.columns;`|  
|**Tempdb**에서 기존 개체의 목록을 봅니다.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
