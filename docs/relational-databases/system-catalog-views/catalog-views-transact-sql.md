---
title: 카탈로그 뷰 (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 45
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: fc5a3c84b171a3cd0cf6353462b0de4b69ad2e0a
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/04/2018
ms.locfileid: "34708611"
---
# <a name="system-catalog-views-transact-sql"></a>시스템 카탈로그 뷰 (Transact SQL)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  카탈로그 뷰는 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]에서 사용하는 정보를 반환합니다. 카탈로그 뷰는 카탈로그 메타데이터에 대한 가장 일반적인 인터페이스이며 정보를 획득 및 변환하고 사용자 지정 형태로 제공하는 데 가장 효과적인 방법을 제공하므로 카탈로그 뷰를 사용하는 것이 좋습니다. 사용자가 이용할 수 있는 모든 카탈로그 메타데이터는 카탈로그 뷰를 통해 표시됩니다.  
  
> [!NOTE]  
>  카탈로그 뷰는 복제, 백업, 데이터베이스 유지 관리 계획 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 카탈로그 데이터에 대한 정보는 포함하지 않습니다.  
  
 일부 카탈로그 뷰는 다른 카탈로그 뷰의 행을 상속합니다. 예를 들어는 [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) 에서 상속 되는 카탈로그 뷰는 [sys.objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) 카탈로그 뷰에 있습니다. sys.objects 카탈로그 뷰를 기본 뷰라고 하고 sys.tables 뷰를 파생 뷰라고 합니다. sys.tables 카탈로그 뷰는 테이블에 관련된 열과 sys.objects 카탈로그 뷰에서 반환되는 모든 열을 반환합니다. sys.objects 카탈로그 뷰는 테이블이 아닌 저장 프로시저, 뷰 등의 개체에 대한 행을 반환합니다. 테이블을 만들면 해당 테이블의 메타데이터가 두 뷰에 모두 반환됩니다. 두 카탈로그 뷰는 테이블에 대해 서로 다른 수준의 정보를 반환하지만 이 테이블의 메타데이터에는 이름과 object_id를 하나씩 포함하는 한 개 항목만 있습니다. 이 내용은 다음과 같이 요약할 수 있습니다.  
  
-   기본 뷰에는 열의 하위 집합과 행의 상위 집합이 포함됩니다.  
  
-   파생된 뷰에는 열의 상위 집합과 행의 하위 집합이 포함됩니다.  
  
> [!IMPORTANT]  
>  이후 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 [!INCLUDE[msCoName](../../includes/msconame-md.md)]는 열 목록의 끝에 열을 추가하여 시스템 카탈로그 뷰의 정의를 보강할 수 있습니다.  SELECT 구문을 사용 하 여 좋습니다 \* FROM *sys.catalog_view_name* 프로덕션 환경에서 코드 반환 된 열 수가 수 변경 하 고 응용 프로그램을 중단 합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 카탈로그 뷰는 다음 범주로 구성됩니다.  
  
|||  
|-|-|  
|[Always On 가용성 그룹 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)|[메시지 &#40;오류에 대 한&#41; 카탈로그 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/8ac78c53-7b97-41b3-9cbd-5f97c179f1f2)|  
|[Azure SQL 데이터베이스 카탈로그 뷰](../../relational-databases/system-catalog-views/azure-sql-database-catalog-views.md)|[개체 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)|  
|[변경 내용 추적 카탈로그 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/6e8fd949-5560-4b34-879f-4e25aa24b183)|[파티션 함수 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/partition-function-catalog-views-transact-sql.md)|  
|[CLR 어셈블리 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)|[정책 기반 관리 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/policy-based-management-views-transact-sql.md)|  
|[데이터 수집기 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)|[리소스 관리자 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md)|  
|[데이터 공간 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)|[쿼리 저장소 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/query-store-catalog-views-transact-sql.md)|  
|[데이터베이스 메일 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md)|[스칼라 유형 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)|  
|[데이터베이스 미러링 모니터 카탈로그 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/8a0c9053-5d76-4aa9-a18d-0ea1c514034d)|[스키마 카탈로그 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)|  
|[데이터베이스 및 파일 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)|[보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)|  
|[끝점 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)|[Service Broker 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/service-broker-catalog-views-transact-sql.md)|  
|[확장 이벤트 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)|[서버 차원의 구성 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/server-wide-configuration-catalog-views-transact-sql.md)|  
|[확장 속성 카탈로그 뷰&#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/f39fd324-efd4-4468-884c-bf77ed1a026f)|[공간 데이터 카탈로그 뷰](../../relational-databases/system-catalog-views/spatial-data-catalog-views.md)|  
|[외부 작업 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/external-operations-catalog-views-transact-sql.md)|[SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 카탈로그 뷰](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)|  
|[Filestream 및 FileTable 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)|[스트레치 데이터베이스 카탈로그 뷰 &#40;Transact SQL&#41;](http://msdn.microsoft.com/library/bee78e39-e07d-4b0f-b8ad-09a01a5eb795)|  
|[전체 텍스트 검색 및 의미 체계 검색 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/full-text-search-and-semantic-search-catalog-views-transact-sql.md)|[XML 스키마 &#40;XML 유형 시스템&#41; 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)|  
|[연결 된 서버 카탈로그 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)||  
  
## <a name="see-also"></a>관련 항목  
 [정보 스키마 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [시스템 테이블 &#40;Transact SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
