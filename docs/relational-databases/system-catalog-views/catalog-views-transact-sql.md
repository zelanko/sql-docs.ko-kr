---
title: 카탈로그 뷰 (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sql13.SysViewExpandPortal.f1
dev_langs:
- TSQL
helpviewer_keywords:
- catalog metadata [SQL Server]
- system views [SQL Server], catalog
- metadata [SQL Server], views
- catalogs [SQL Server], metadata
- catalog views [SQL Server]
- Database Engine [SQL Server], metadata
- catalog views [SQL Server], about catalog views
ms.assetid: 13bccc2f-ed3c-4b58-abd0-ca8bf34a66b8
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a9fe9717342edb8f02cdc503b6efb8e47b755bb9
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85997317"
---
# <a name="system-catalog-views-transact-sql"></a>시스템 카탈로그 뷰 (Transact-sql)

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

카탈로그 뷰는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 사용하는 정보를 반환합니다. 카탈로그 뷰는 카탈로그 메타데이터에 대한 가장 일반적인 인터페이스이며 정보를 획득 및 변환하고 사용자 지정 형태로 제공하는 데 가장 효과적인 방법을 제공하므로 카탈로그 뷰를 사용하는 것이 좋습니다. 사용자가 이용할 수 있는 모든 카탈로그 메타데이터는 카탈로그 뷰를 통해 표시됩니다.

> [!NOTE]
> 카탈로그 뷰는 복제, 백업, 데이터베이스 유지 관리 계획 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 카탈로그 데이터에 대한 정보는 포함하지 않습니다.

 일부 카탈로그 뷰는 다른 카탈로그 뷰의 행을 상속합니다. 예를 들어, [sys. tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) 카탈로그 뷰는 [sys. objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에서 상속 됩니다. sys.objects 카탈로그 뷰를 기본 뷰라고 하고 sys.tables 뷰를 파생 뷰라고 합니다. sys.tables 카탈로그 뷰는 테이블에 관련된 열과 sys.objects 카탈로그 뷰에서 반환되는 모든 열을 반환합니다. sys.objects 카탈로그 뷰는 테이블이 아닌 저장 프로시저, 뷰 등의 개체에 대한 행을 반환합니다. 테이블을 만들면 해당 테이블의 메타데이터가 두 뷰에 모두 반환됩니다. 두 카탈로그 뷰는 테이블에 대해 서로 다른 수준의 정보를 반환하지만 이 테이블의 메타데이터에는 이름과 object_id를 하나씩 포함하는 한 개 항목만 있습니다. 이 내용은 다음과 같이 요약할 수 있습니다.

- 기본 뷰에는 열의 하위 집합과 행의 상위 집합이 포함됩니다.
- 파생된 뷰에는 열의 상위 집합과 행의 하위 집합이 포함됩니다.

> [!IMPORTANT]
> 이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 열 목록의 끝에 열을 추가하여 시스템 카탈로그 뷰의 정의를 보강할 수 있습니다. \*반환 된 열 수가 응용 프로그램을 변경 하 고 중단할 수 있으므로 프로덕션 코드에서 SELECT FROM *sys. catalog_view_name* 구문을 사용 하지 않는 것이 좋습니다.

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 카탈로그 뷰는 다음 범주로 구성됩니다.

|||
|-|-|
|[AlwaysOn 가용성 그룹 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[메시지 &#40;&#41; 카탈로그 뷰 &#40;transact-sql&#41;](../system-catalog-views/messages-for-errors-catalog-views-sys-messages.md))|
|[Azure SQL Database 카탈로그 뷰](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[개체 카탈로그 뷰 &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|
|[Transact-sql&#41;&#40;카탈로그 뷰 변경 내용 추적](../system-catalog-views/change-tracking-catalog-views-sys-change-tracking-databases.md)|[Transact-sql&#41;&#40;파티션 함수 카탈로그 뷰](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|
|[Transact-sql&#41;&#40;CLR 어셈블리 카탈로그 뷰](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|
|[데이터 수집기 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[Transact-sql&#41;&#40;카탈로그 뷰 Resource Governor](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|
|[데이터 공간 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|
|[Transact-sql&#41;&#40;데이터베이스 메일 뷰](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[Transact-sql&#41;&#40;스칼라 형식 카탈로그 뷰](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|
|[Transact-sql&#41;&#40;데이터베이스 미러링 모니터 서버 카탈로그 뷰](../system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)|[스키마 카탈로그 뷰 &#40;Transact-sql&#41;](../system-catalog-views/schemas-catalog-views-sys-schemas.md)|
|[데이터베이스 및 파일 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|
|[엔드포인트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Service Broker 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|
|[확장 이벤트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[Transact-sql&#41;&#40;서버 차원의 구성 카탈로그 뷰](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|
|[확장 속성 카탈로그 뷰&#40;Transact-SQL&#41;](../system-catalog-views/extended-properties-catalog-views-sys-extended-properties.md)|[공간 데이터 카탈로그 뷰](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|
|[Transact-sql&#41;&#40;외부 작업 카탈로그 뷰](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL Data Warehouse 및 병렬 Data Warehouse 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|
|[Transact-sql&#41;&#40;Filestream 및 FileTable 카탈로그 뷰](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[Transact-sql&#41;&#40;카탈로그 뷰 Stretch Database](../system-catalog-views/stretch-database-catalog-views-sys-remote-data-archive-databases.md)|
|[Transact-sql&#41;&#40;전체 텍스트 검색 및 의미 체계 검색 카탈로그 뷰](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[Xml 스키마 &#40;XML 형식 시스템&#41; 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|
|[연결 된 서버 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||

## <a name="see-also"></a>참고 항목

- [Transact-sql&#41;&#40;정보 스키마 뷰](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)
- [시스템 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)
- [SQL Server 시스템 카탈로그 쿼리에 대한 질문과 대답](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)
