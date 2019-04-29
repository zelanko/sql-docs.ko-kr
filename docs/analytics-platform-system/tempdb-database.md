---
title: Tempdb 데이터베이스-병렬 데이터 웨어하우스 | Microsoft Docs
description: 병렬 데이터 웨어하우스에서 Tempdb 데이터베이스입니다.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7e11f4eff980358f4b4906f8a100cfc509d19dd5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156965"
---
# <a name="tempdb-database-in-parallel-data-warehouse"></a>병렬 데이터 웨어하우스에서 tempdb 데이터베이스
**tempdb** 사용자 데이터베이스에 대 한 로컬 임시 테이블을 저장 하는 SQL Server PDW 시스템 데이터베이스입니다. 임시 테이블 쿼리 성능을 향상 시키기 위해 자주 사용 됩니다. 예를 들어, 스크립트 모듈화 임시 테이블을 사용 하 고 계산 된 데이터를 재사용할 수 있습니다.  
  
시스템 데이터베이스에 대 한 자세한 내용은 참조 하세요. [시스템 데이터베이스](system-databases.md)합니다.  
  
## <a name="Basics"></a>주요 용어 및 개념  
*로컬 임시 테이블*  
A *로컬 임시 테이블* 로컬 사용자 세션을 통해 생성 된 임시 테이블 이며 테이블 이름 앞에 # 접두사를 사용 합니다. 만 각 세션은 자체 세션에 대 한 로컬 임시 테이블의 데이터를 액세스할 수 있습니다.  
  
각 세션 모든 세션에서 로컬 임시 테이블에 대 한 메타 데이터를 볼 수 있습니다. 모든 세션에서 사용 하 여 모든 로컬 임시 테이블에 대 한 메타 데이터를 볼 수는 예를 들어를 `SELECT * FROM tempdb.sys.tables` 쿼리 합니다.  
  
전역 임시 테이블  
*전역 임시 테이블*, SQL Server에서 지원 되는 # # 구문을이 릴리스의 SQL Server PDW에서 지원 되지 않습니다.  
  
pdwtempdb  
**pdwtempdb** 로컬 임시 테이블을 저장 하는 데이터베이스입니다.  
  
PDW SQL Server를 사용 하 여 임시 테이블을 구현 하지 않습니다**tempdb** 데이터베이스입니다. 대신 PDW pdwtempdb 라는 데이터베이스에 저장 됩니다. 이 데이터베이스는 각 Compute 노드에 존재 하며 PDW 인터페이스를 통해 사용자에 게 표시 되지 않습니다. 저장소 페이지의 관리자 콘솔에서에 표시 됩니다 이러한 검사기에 대 한 호출 PDW 시스템 데이터베이스 **tempdb sql**합니다.  
  
tempdb  
**tempdb** SQL Server tempdb 데이터베이스입니다. 최소 로깅을 사용합니다. SQL Server 계산 노드에서 tempdb를 사용 하 여 SQL Server 작업을 수행 하는 과정에서 필요한 임시 테이블을 저장 합니다.  
  
테이블을 삭제 하는 SQL Server PDW **tempdb** 때:  
  
-   DROP TABLE 문이 실행 됩니다.  
  
-   세션 연결이 끊어졌습니다. 세션에 대 한 임시 테이블만 삭제 됩니다.  
  
-   어플라이언스를 종료 했습니다.  
  
-   제어 노드는 클러스터 장애 조치를 있습니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
SQL Server PDW 별도로 명시 하지 않는 임시 테이블 및 영구 테이블에서 동일한 작업을 수행 합니다. 예를 들어, 영구 테이블과 마찬가지로 로컬 임시 테이블의 데이터는 배포 또는 계산 노드 간에 복제 합니다.  
  
## <a name="LimitationsRestrictions"></a>제한 사항  
제한 사항 및 SQL Server PDW에 대 한 제한이**tempdb** 데이터베이스입니다. 있습니다 *수 없습니다.*  
  
-   만들기 시작 하는 전역 임시 테이블 # #.  
  
-   백업 또는 복원을 수행 **tempdb**합니다.  
  
-   사용 권한을 수정 하 **tempdb** 사용 하 여는 **GRANT**, **거부**, 또는 **해지** 문.  
  
-   실행할 **DBCC SHRINKLOG** 에 대 한 **tempdb**tempdb입니다.  
  
-   DDL 작업을 수행할 **tempdb**합니다. 이 두 가지 예외가 있습니다. 자세한 내용은 로컬 임시 테이블의 제한 사항 및 제한 사항을 다음 목록을 참조 합니다.  
  
로컬 임시 테이블의 제한 사항입니다. 있습니다 *수 없습니다.*  
  
-   임시 테이블 이름 바꾸기  
  
-   임시 테이블에 파티션, 뷰 또는 비클러스터형 인덱스를 만듭니다. **ALTER INDEX** 하나를 사용 하 여 만든 테이블에 대 한 클러스터형된 인덱스를 다시 작성할 수 있습니다.  
  
-   GRANT, DENY 사용 하 여 임시 테이블에 사용 권한을 수정 하거나 REVOKE 문을 합니다.  
  
-   임시 테이블에서 데이터베이스 콘솔 명령을 실행 합니다.  
  
-   동일한 일괄 처리 내에서 두 개 이상의 임시 테이블에 동일한 이름을 사용 합니다. 일괄 처리 내에서 둘 이상의 로컬 임시 테이블을 사용하는 경우 각각에 고유 이름이 있어야 합니다. 여러 세션이 동일한 일괄 처리를 실행 하 고 동일한 로컬 임시 테이블 만들기, 하는 경우 SQL Server PDW 각 로컬 임시 테이블에 대 한 고유한 이름을 유지 하기 위해 로컬 임시 테이블 이름에 숫자 접미사를 내부적으로 추가 합니다.  
  
> [!NOTE]  
> 있습니다 *수 있습니다* 만들고 임시 테이블에 대 한 통계를 업데이트 합니다. **ALTER INDEX** 클러스터형된 인덱스를 다시 작성할 수 있습니다.  
  
## <a name="permissions"></a>사용 권한  
모든 사용자가 tempdb에 임시 개체를 만들 수 있습니다. 사용자가 추가 사용 권한을 받는 경우를 제외하고 자신의 고유 개체에만 액세스할 수 있습니다. tempdb 연결 권한을 취소하여 사용자가 tempdb를 사용하지 못하도록 할 수 있지만 일부 일상적인 작업에서 tempdb를 사용해야 하므로 권장하지 않습니다.  
  
## <a name="RelatedTasks"></a>관련된 태스크  
  
|태스크|Description|  
|---------|---------------|  
|테이블을 만들 **tempdb**합니다.|CREATE TABLE 및 CREATE TABLE AS SELECT 문을 사용 하 여 사용자 임시 테이블을 만들 수 있습니다. 자세한 내용은 [CREATE TABLE](../t-sql/statements/create-table-azure-sql-data-warehouse.md) 하 고 [CREATE TABLE AS SELECT](../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)합니다.|  
|기존 테이블의 목록을 보려면 **tempdb**합니다.|`SELECT * FROM tempdb.sys.tables;`|  
|에 있는 기존 열의 목록을 보려면 **tempdb**합니다.|`SELECT * FROM tempdb.sys.columns;`|  
|기존 개체의 목록을 보려면 **tempdb**합니다.|`SELECT * FROM tempdb.sys.objects;`|  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
