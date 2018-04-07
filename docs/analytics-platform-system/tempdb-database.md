---
title: tempdb 데이터베이스 (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5840033d-2dc6-4576-8a5f-067e2a58b170
caps.latest.revision: 22
ms.workload: not set
ms.openlocfilehash: 6a52f21b266d277f3bda205803d38431598545f7
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="tempdb-database"></a>tempdb 데이터베이스
**tempdb** 사용자 데이터베이스에 대 한 로컬 임시 테이블을 저장 하는 SQL Server PDW 시스템 데이터베이스입니다. 임시 테이블 쿼리 성능 향상을 위해 종종 사용 됩니다. 예를 들어 임시 테이블을 사용 하 여 스크립트를 모듈화 할 수 있으며 계산 된 데이터를 다시 사용.  
  
시스템 데이터베이스에 대 한 자세한 내용은 참조 [시스템 데이터베이스](system-databases.md)합니다.  
  
## <a name="Basics"></a>주요 용어 및 개념  
*로컬 임시 테이블*  
A *로컬 임시 테이블* 테이블 이름 앞 # 접두사를 사용 하 고 로컬 사용자 세션에 의해 생성 된 임시 테이블입니다. 각 세션은 자체 세션에 대 한 로컬 임시 테이블의 데이터만 액세스할 수 있습니다.  
  
각 세션 모든 세션에서 로컬 임시 테이블에 대 한 메타 데이터를 볼 수 있습니다. 예를 들어 모든 세션으로 로컬 임시 테이블의 모든 메타 데이터를 볼 수는 `SELECT * FROM tempdb.sys.tables` 쿼리 합니다.  
  
전역 임시 테이블  
*전역 임시 테이블*, SQL Server에서 지원 되는 # # 구문,이 버전의 SQL Server PDW에서 지원 되지 않습니다.  
  
pdwtempdb  
**pdwtempdb** 로컬 임시 테이블을 저장 하는 데이터베이스입니다.  
  
PDW SQL Server를 사용 하 여 임시 테이블을 구현 하지 않는**tempdb** 데이터베이스입니다. 대신, PDW pdwtempdb 라는 데이터베이스에 저장 합니다. 이 데이터베이스는 각 계산 노드에 있으며 PDW 인터페이스를 통해 사용자에 게 표시 되지 않습니다. 저장소 페이지에서 관리 콘솔에서 이러한 검사기에 대 한에 나타나는 라는 PDW 시스템 데이터베이스 **tempdb sql**합니다.  
  
tempdb  
**tempdb** 는 SQL Server tempdb 데이터베이스입니다. 최소 로깅을 사용합니다. SQL Server를 사용 하 여 tempdb에서 계산 노드의 SQL Server 작업을 수행 하는 과정에서 필요로 하는 임시 테이블에 저장 합니다.  
  
SQL Server PDW에서 테이블 삭제 **tempdb** 경우:  
  
-   DROP TABLE 문이 실행 됩니다.  
  
-   세션 연결이 끊어집니다. 세션에 대 한 임시 테이블에만 삭제 됩니다.  
  
-   어플라이언스를 종료 했습니다.  
  
-   제어 노드에 장애 조치 클러스터에 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
SQL Server PDW 명시적인 언급이 없는 한 임시 테이블 및 영구 테이블에 같은 작업을 수행 합니다. 예를 들어 영구 테이블 처럼 로컬 임시 테이블의 데이터는 배포 또는 계산 노드에 복제 합니다.  
  
## <a name="LimitationsRestrictions"></a>제한 사항  
SQL Server PDW에 대 한 제한 사항**tempdb** 데이터베이스입니다. 하면 *수 없습니다.*  
  
-   로 시작 하는 전역 임시 테이블 만들기 # #.  
  
-   백업 또는 복원을 수행 **tempdb**합니다.  
  
-   에 대 한 수정 **tempdb** 와 **GRANT**, **DENY**, 또는 **해지** 문.  
  
-   실행 **DBCC SHRINKLOG** 에 대 한 **tempdb**tempdb입니다.  
  
-   DDL 작업을 수행할 **tempdb**합니다. 이 몇 가지 예외가 있습니다. 자세한 내용은 로컬 임시 테이블에 다음과 같은 제한 사항 참조 합니다.  
  
로컬 임시 테이블에 대 한 제한 사항입니다. 하면 *수 없습니다.*  
  
-   임시 테이블 이름 바꾸기  
  
-   임시 테이블에 파티션을, 뷰 또는 비클러스터형 인덱스를 만듭니다. **ALTER INDEX** 하나를 사용 하 여 만든 테이블에 대 한 클러스터형된 인덱스를 다시 작성에 사용할 수 있습니다.  
  
-   임시 테이블에 대 한 GRANT, DENY와 수정 하거나 문을 취소 합니다.  
  
-   임시 테이블에서 데이터베이스 콘솔 명령을 실행 합니다.  
  
-   동일한 일괄 처리 내에서 둘 이상의 임시 테이블에 동일한 이름을 사용 합니다. 일괄 처리 내에서 둘 이상의 로컬 임시 테이블을 사용하는 경우 각각에 고유 이름이 있어야 합니다. 여러 세션 동일한 일괄 처리를 실행 하 고 동일한 로컬 임시 테이블을 만들지, 하는 경우 SQL Server PDW 각 로컬 임시 테이블에 대 한 고유한 이름을 유지 하기 위해 로컬 임시 테이블 이름에 숫자 접미사를 내부적으로 추가 합니다.  
  
> [!NOTE]  
> 하면 *수* 만들고 임시 테이블에 대 한 통계를 업데이트 합니다. **ALTER INDEX** 는 클러스터형된 인덱스를 다시 작성 하는 데 사용할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
모든 사용자가 tempdb에 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다. tempdb 연결 권한을 취소하여 사용자가 tempdb를 사용하지 못하도록 할 수 있지만 일부 일상적인 작업에서 tempdb를 사용해야 하므로 권장하지 않습니다.  
  
## <a name="RelatedTasks"></a>관련된 태스크  
  
|태스크|Description|  
|---------|---------------|  
|테이블을 만들 **tempdb**합니다.|CREATE TABLE 및 CREATE TABLE AS SELECT 문과 함께 사용자의 임시 테이블을 만들 수 있습니다. 자세한 내용은 참조 [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) 및 [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)합니다.|  
|에 있는 기존 테이블의 목록을 보려면 **tempdb**합니다.|`SELECT * FROM tempdb.sys.tables;`|  
|기존 열 목록을 볼 **tempdb**합니다.|`SELECT * FROM tempdb.sys.columns;`|  
|기존 개체의 목록을 보려면 **tempdb**합니다.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
