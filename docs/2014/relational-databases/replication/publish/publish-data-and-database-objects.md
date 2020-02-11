---
title: 데이터 및 데이터베이스 개체 게시 | Microsoft 문서
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- user-defined types [SQL Server replication]
- articles [SQL Server replication], dropping
- objects [SQL Server replication]
- publications [SQL Server replication], creating
- merge replication [SQL Server replication], publications
- schema-only articles [SQL Server replication]
- publishing [SQL Server replication], database objects
- articles [SQL Server replication], defining
- publishing [SQL Server replication], functions
- replication [SQL Server], publications
- publishing [SQL Server replication], views
- tables [SQL Server replication]
- schemas [SQL Server replication]
- publishing [SQL Server replication], data
- schemas [SQL Server replication], publishing
- articles [SQL Server replication], stored procedures and
- publishing [SQL Server replication], tables
- alias data types [SQL Server replication]
- publications [SQL Server replication], deleting
- snapshot replication [SQL Server], publications
- articles [SQL Server replication], modifying
- transactional replication, publications
- publishing [SQL Server replication], stored procedures
- publishing [SQL Server replication]
- views [SQL Server replication]
- stored procedures [SQL Server replication], publishing
- publications [SQL Server replication], schema options
- articles [SQL Server replication], adding
- publications [SQL Server replication], modifying
- user-defined functions [SQL Server replication]
ms.assetid: d986032c-3387-4de1-a435-3ec5e82185a2
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70e31ec60f8f47dfbc0a4761357c99a42623c6eb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74479322"
---
# <a name="publish-data-and-database-objects"></a>데이터 및 데이터베이스 개체 게시
  게시를 만들 때 게시할 테이블 및 다른 데이터베이스 개체를 선택할 수 있습니다. 복제를 사용하여 다음 데이터베이스 개체를 게시할 수 있습니다.  
  
|데이터베이스 개체|스냅샷 복제 및 트랜잭션 복제|병합 복제|  
|---------------------|--------------------------------------------------------|-----------------------|  
|테이블|X|X|  
|분할된 테이블|X|X|  
|저장 프로시저 - 정의([!INCLUDE[tsql](../../../includes/tsql-md.md)] 및 CLR)|X|X|  
|저장 프로시저 - 실행([!INCLUDE[tsql](../../../includes/tsql-md.md)] 및 CLR)|X|아니요|  
|뷰|X|X|  
|인덱싱된 뷰|X|X|  
|인덱싱된 뷰(테이블 형식)|X|아니요|  
|사용자 정의 형식(CLR)|X|X|  
|사용자 정의 함수([!INCLUDE[tsql](../../../includes/tsql-md.md)] 및 CLR)|X|X|  
|별칭 데이터 형식|X|X|  
|전체 텍스트 인덱스|X|X|  
|스키마 개체(제약 조건, 인덱스, 사용자 DML 트리거, 확장 속성 및 데이터 정렬)|X|X|  
  
## <a name="creating-publications"></a>게시 만들기  
 게시를 만들려면 다음 정보를 제공해야 합니다.  
  
-   배포자  
  
-   스냅샷 파일의 위치  
  
-   게시 데이터베이스  
  
-   만들 게시의 유형(스냅샷, 트랜잭션, 업데이트할 수 있는 구독이 있는 트랜잭션 또는 병합)  
  
-   게시에 포함할 데이터 및 데이터베이스 개체(아티클)  
  
-   모든 유형의 게시에 대한 정적 행 필터 및 열 필터, 병합 게시에 대한 매개 변수가 있는 행 필터 및 조인 필터  
  
-   스냅샷 에이전트 일정  
  
-   다음 에이전트가 실행되는 계정 - 모든 게시에 대한 스냅샷 에이전트, 모든 트랜잭션 게시에 대한 로그 판독기 에이전트, 구독 업데이트를 허용하는 모든 트랜잭션 게시에 대한 큐 판독기 에이전트  
  
-   게시에 대한 이름 및 설명  
  
 게시로 작업하는 방법은 다음 항목을 참조하십시오.  
  
-   [게시 만들기](create-a-publication.md)  
  
-   [아티클 정의](define-an-article.md)  
  
-   [게시 속성 보기 및 수정](view-and-modify-publication-properties.md)  
  
-   [아티클 속성 보기 및 수정](view-and-modify-article-properties.md)  
  
-   [게시 삭제](delete-a-publication.md)  
  
-   [아티클 삭제](delete-an-article.md)  
  
> [!NOTE]  
>  아티클 또는 게시를 삭제해도 구독자에서 개체가 제거되지 않습니다.  
  
## <a name="publishing-tables"></a>테이블 게시  
 가장 일반적으로 게시되는 개체는 테이블입니다. 다음 링크는 테이블 게시와 관련된 영역에 대한 추가 정보를 제공합니다.  
  
-   [게시된 데이터 필터링](filter-published-data.md)  
  
-   [Article Options for Transactional Replication](../transactional/article-options-for-transactional-replication.md)  
  
-   [병합 복제를 위한 아티클 옵션](../merge/article-options-for-merge-replication.md)  
  
-   [ID 열 복제](replicate-identity-columns.md)  
  
 복제를 위해 테이블을 게시할 때는 구독자로 복사할 선언된 참조 무결성(PRIMARY KEY 제약 조건, 참조 제약 조건, UNIQUE 제약 조건), 인덱스, 사용자 DML 트리거(DDL 트리거는 복제할 수 없음), 확장 속성, 데이터 정렬 등의 스키마 개체를 지정할 수 있습니다. 확장 속성은 게시자와 구독자 간의 초기 동기화 수행 시에만 복제됩니다. 초기 동기화 후에 확장 속성을 추가하거나 수정하면 변경 내용이 복제되지 않습니다.  
  
 스키마 옵션을 지정하려면 [스키마 옵션 지정](specify-schema-options.md) 또는 <xref:Microsoft.SqlServer.Replication.Article.SchemaOption%2A>을 참조하세요.  
  
### <a name="partitioned-tables-and-indexes"></a>Partitioned Tables and Indexes  
 복제는 분할된 테이블 및 인덱스의 게시를 지원합니다. 지원 수준은 사용하는 복제 유형, 지정하는 게시 옵션 및 분할된 테이블과 연결된 아티클에 의해 결정됩니다. 자세한 내용은 [분할 테이블 및 인덱스 복제](replicate-partitioned-tables-and-indexes.md)를 참조하세요.  
  
## <a name="publishing-stored-procedures"></a>저장 프로시저 게시  
 모든 복제 유형을 사용하여 저장 프로시저 정의를 복제할 수 있으며 CREATE PROCEDURE가 각 구독자에 복사됩니다. CLR(공용 언어 런타임) 저장 프로시저의 경우 연결된 어셈블리도 복사됩니다. 프로시저에 대한 변경 내용은 구독자에 복제되는 반면 연결된 어셈블리에 대한 변경 내용은 복제되지 않습니다.  
  
 트랜잭션 복제를 사용하면 저장 프로시저의 정의를 복제할 수 있을 뿐만 아니라 저장 프로시저 실행도 복제할 수 있습니다. 이는 많은 데이터에 영향을 주는 유지 관리 관련 저장 프로시저의 결과를 복제할 때 유용합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
## <a name="publishing-views"></a>뷰 게시  
 모든 복제 유형을 사용하여 뷰를 복제할 수 있습니다. 뷰 및 해당 인덱스(인덱싱된 뷰의 경우)를 구독자로 복사할 수 있지만 이때 기본 테이블도 복제해야 합니다.  
  
 인덱싱된 뷰의 경우 트랜잭션 복제를 사용하면 인덱싱된 뷰를 뷰가 아닌 테이블로 복제하므로 기본 테이블을 함께 복제할 필요가 없습니다. 이렇게 하려면 *sp_addarticle&#40;Transact-SQL&#41;\@의* [type](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql) 매개 변수에 대해 "indexed view logbased" 옵션 중 하나를 지정합니다. **sp_addarticle**의 사용 방법은 [아티클 정의](define-an-article.md)를 참조하세요.  
  
## <a name="publishing-user-defined-functions"></a>사용자 정의 함수 게시  
 CLR 함수 및 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 함수의 CREATE FUNCTION 문이 각 구독자에 복사됩니다. CLR 함수의 경우 연결된 어셈블리도 복사됩니다. 함수에 대한 변경 내용은 구독자에 복제되지만 연결된 어셈블리에 대한 변경 내용은 복제되지 않습니다.  
  
## <a name="publishing-user-defined-types-and-alias-data-types"></a>사용자 정의 형식 및 별칭 데이터 형식 게시  
 사용자 정의 형식 또는 별칭 데이터 형식을 사용하는 열은 다른 열과 마찬가지로 구독자에 복제됩니다. 복제된 각 유형에 대한 CREATE TYPE 문이 테이블 생성 전에 구독자에서 실행됩니다. 사용자 정의 형식의 경우 연결된 어셈블리도 각 구독자에 복사됩니다. 사용자 정의 형식 및 별칭 데이터 형식에 대한 변경 내용은 구독자에 복제되지 않습니다.  
  
 특정 유형이 데이터베이스에 정의되어 있지만 게시를 만들 때 어떤 열에서도 참조되지 않으면 해당 유형은 구독자에 복사되지 않습니다. 이후 데이터베이스에 해당 유형의 열을 만들고 이를 복제하려면 먼저 수동으로 해당 유형 및 사용자 정의 형식에 연결된 어셈블리를 각 구독자에 복사해야 합니다.  
  
## <a name="publishing-full-text-indexes"></a>전체 텍스트 인덱스 게시  
 CREATE FULLTEXT INDEX 문이 각 구독자에 복사되고 전체 텍스트 인덱스가 구독자에서 생성됩니다. ALTER FULLTEXT INDEX를 사용하여 적용된 전체 텍스트 인덱스의 변경 내용은 복제되지 않습니다.  
  
## <a name="making-schema-changes-to-published-objects"></a>게시된 개체의 스키마 변경  
 복제는 게시된 개체에 대한 다양한 스키마 변경을 지원합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자에 게시된 개체에 대해 다음 스키마 변경을 수행하면 기본적으로 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자에 변경 내용이 전파됩니다.  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 자세한 내용은 [게시 데이터베이스의 스키마 변경](make-schema-changes-on-publication-databases.md)을 참조하세요.  
  
## <a name="considerations-for-publishing"></a>게시 고려 사항  
 데이터베이스 개체를 게시할 때는 다음 사항을 고려하십시오.  
  
-   게시 및 초기 스냅샷을 만드는 동안 사용자가 데이터베이스에 액세스할 수 있지만 게시자에서 작업량이 적은 시간에 게시를 만드는 것이 좋습니다.  
  
-   데이터베이스 내에 게시를 만든 후에는 데이터베이스의 이름을 바꿀 수 없습니다. 데이터베이스의 이름을 바꾸려면 먼저 데이터베이스에서 복제를 제거해야 합니다.  
  
-   하나 이상의 다른 데이터베이스 개체에 종속된 데이터베이스 개체를 게시하는 경우 참조된 개체를 모두 게시해야 합니다. 예를 들어 테이블에 종속된 뷰를 게시하는 경우 테이블도 게시해야 합니다.  
  
    > [!NOTE]  
    >  병합 게시에 아티클을 추가하고 기존 아티클이 새 아티클에 종속된 경우 **sp_addmergearticle\@ 및** sp_changemergearticle[의 ](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)[processing_order](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql) 매개 변수를 사용하여 두 아티클의 처리 순서를 지정해야 합니다. 다음과 같은 시나리오를 고려해 보십시오. 테이블을 게시하지만 테이블이 참조하는 함수는 게시하지 않는 경우가 있습니다. 함수를 게시하지 않을 경우 구독자에서 테이블을 만들 수 없습니다. 게시에 함수를 추가할 경우에는 **sp_addmergearticle**의 **\@processing_order** 매개 변수에 값 **1**을 지정하고 **sp_changemergearticle**의 **\@processing_order** 매개 변수에 값 **2**를 지정하며 **\@article** 매개 변수에는 테이블 이름을 지정합니다. 이 처리 순서를 사용하면 함수에 종속된 테이블이 생성되기 전에 해당 함수가 구독자에서 생성됩니다. 함수 번호가 테이블 번호보다 낮은 경우 각 아티클에 다른 번호를 사용할 수 있습니다.  
  
-   게시 이름은 % * [ ] | : " ?와 같은 문자를 포함할 수 없습니다. \/ \< >입니다.  
  
### <a name="limitations-on-publishing-objects"></a>개체 게시의 제한 사항  
  
-   게시할 수 있는 최대 아티클 및 열 개수는 게시 유형에 따라 달라집니다. 자세한 내용은 [SQL Server의 최대 용량 사양](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)의 "복제 개체" 섹션을 참조하세요.  
  
-   WITH ENCRYPTION으로 정의된 저장 프로시저, 뷰, 트리거 및 사용자 정의 함수는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 복제의 일부로 게시할 수 없습니다.  
  
-   XML 스키마 컬렉션을 복제할 수는 있지만 초기 스냅샷 이후에는 변경 내용이 복제되지 않습니다.  
  
-   트랜잭션 복제에 대해 게시된 테이블에는 기본 키가 있어야 합니다. 트랜잭션 복제 게시의 테이블에서는 기본 키 열과 연결된 인덱스를 해제할 수 없습니다. 이러한 인덱스는 복제에 필요합니다. 인덱스를 해제하려면 먼저 게시에서 테이블을 삭제해야 합니다.  
  
-   [sp_bindefault&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-bindefault-transact-sql)로 생성된 바인딩된 기본값은 복제되지 않습니다. 바인딩된 기본값은 ALTER TABLE 또는 CREATE TABLE의 DEFAULT 키워드로 생성된 기본값으로 대체되었습니다.  
  
-   인덱싱된 뷰에 대한 `NOEXPAND` 힌트를 포함하는 함수는 배포 에이전트가 전달하는 순서 때문에 참조된 테이블 및 인덱싱된 뷰와 같은 게시로 게시할 수 없습니다. 이 문제를 해결하려면 첫 번째 게시에 테이블 및 인덱싱된 뷰 만들기를 배치하고 첫 번째 게시가 완료된 후 게시하는 두 번째 게시에 인덱싱된 뷰에 대한 `NOEXPAND` 힌트를 포함하는 함수를 추가합니다. 또는 이러한 함수에 대 한 스크립트를 만들고의 `sp_addpublication` * \@post_snapshot_script* 매개 변수를 사용 하 여 스크립트를 전달 합니다.  
  
### <a name="schemas-and-object-ownership"></a>스키마 및 개체 소유권  
 복제는 새 게시 마법사에서 스키마 및 개체 소유권에 대해 기본적으로 다음과 같이 작동합니다.  
  
-   호환성 수준이 90 이상인 병합 게시, 스냅샷 게시, 트랜잭션 게시의 아티클에 대해 기본적으로 구독자의 개체 소유자는 게시자에 있는 해당 개체의 소유자와 동일합니다. 개체를 소유한 스키마가 구독자에 없으면 자동으로 생성됩니다.  
  
-   호환성 수준이 90 이하인 병합 게시의 아티클에 대해 기본적으로 소유자는 빈 상태였다가 구독자에서 개체를 생성하는 중에 **dbo** 로 지정됩니다.  
  
-   Oracle 게시의 아티클에 대해 기본적으로 소유자는 **dbo**로 지정됩니다.  
  
-   문자 모드 스냅샷([!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 구독자 및 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] 구독자에 사용됨)을 사용하는 게시의 아티클에 대해 기본적으로 소유자는 빈 상태입니다. 소유자는 기본적으로 배포 에이전트 또는 병합 에이전트를 구독자에 연결하는 데 사용하는 계정과 연결된 소유자입니다.  
  
 개체 소유자는 **아티클 속성 - \<***Article***>** 대화 상자와 **sp_addarticle**, **sp_addmergearticle**, **sp_changearticle** 및 **sp_changemergearticle** 저장 프로시저를 통해 변경할 수 있습니다. 자세한 내용은 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md), [아티클 정의](define-an-article.md) 및 [아티클 속성 보기 및 수정](view-and-modify-article-properties.md)을 참조하세요.  
  
### <a name="publishing-data-to-subscribers-running-previous-versions-of-sql-server"></a>이전 버전의 SQL Server를 실행하는 구독자에 데이터 게시  
  
-   이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하는 구독자에 게시할 경우에는 복제 기능은 물론 제품 전체 기능에 있어서 해당 버전에서 지원하는 기능만 사용할 수 있습니다.  
  
-   병합 게시는 게시에 사용할 수 있는 기능을 결정하고 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하는 구독자를 지원할 수 있는 호환성 수준을 사용합니다.  
  
### <a name="publishing-tables-in-more-than-one-publication"></a>둘 이상의 게시에 테이블 게시  
 복제에서는 여러 게시에 아티클을 게시할 수 있을 뿐만 아니라 데이터를 다시 게시할 수 있습니다. 단, 다음과 같은 제한 사항이 있습니다.  
  
-   아티클을 트랜잭션 게시 및 병합 게시에 게시하는 경우 병합 아티클에 대해 *\@published_in_tran_pub* 속성을 TRUE로 설정해야 합니다. 속성을 설정하는 방법은 [게시 속성 보기 및 수정](view-and-modify-publication-properties.md) 및 [아티클 속성 보기 및 수정](view-and-modify-article-properties.md)을 참조하세요.  
  
     트랜잭션 구독에 속한 아티클을 병합 게시에 포함시킬 경우 *\@published_in_tran_pub* 속성도 설정해야 합니다. 이 경우에는 기본적으로 트랜잭션 복제 시 구독자의 테이블이 읽기 전용으로 처리될 것으로 예상합니다. 병합 복제에서 트랜잭션 구독의 테이블에 데이터 변경을 수행할 경우 데이터 수렴이 발생하지 않습니다. 이렇게 되지 않도록 하려면 병합 게시에서 이러한 테이블을 다운로드 전용으로 지정하는 것이 좋습니다. 그러면 병합 구독자가 테이블에 데이터 변경을 업로드하지 않게 됩니다. 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
-   병합 게시와 지연 업데이트 구독이 있는 트랜잭션 게시 모두에 아티클을 게시할 수는 있습니다.  
  
-   구독 업데이트를 지원하는 트랜잭션 게시에 포함된 아티클은 다시 게시할 수 없습니다.  
  
-   지연 업데이트 구독을 지원하는 둘 이상의 트랜잭션 게시에 아티클을 게시하는 경우 모든 게시의 아티클에 대해 다음 속성 값이 같아야 합니다.  
  
    |속성|sp_addarticle의 매개 변수|  
    |--------------|---------------------------------|  
    |ID 범위 관리|**\@auto_identity_range**(사용되지 않음) 및 **\@identityrangemangementoption**|  
    |게시자 ID 범위|**\@pub_identity_range**|  
    |ID 범위|**\@identity_range**|  
    |ID 범위 임계값|**\@threshold**|  
  
     이러한 매개 변수에 대한 자세한 내용은 [sp_addarticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addarticle-transact-sql)을 참조하세요.  
  
-   아티클이 둘 이상의 병합 게시에 게시된 경우 모든 게시의 아티클에 대해 다음 속성 값이 같아야 합니다.  
  
    |속성|sp_addmergearticle의 매개 변수|  
    |--------------|--------------------------------------|  
    |열 추적|**\@column_tracking**|  
    |스키마 옵션|**\@schema_option**|  
    |열 필터링|**\@vertical_partition**|  
    |구독자 업로드 옵션|**\@subscriber_upload_options**|  
    |조건부 삭제 추적|**\@delete_tracking**|  
    |오류 보정|**\@compensate_for_errors**|  
    |ID 범위 관리|**\@auto_identity_range**(사용되지 않음) 및 **\@identityrangemangementoption**|  
    |게시자 ID 범위|**\@pub_identity_range**|  
    |ID 범위|**\@identity_range**|  
    |ID 범위 임계값|**\@threshold**|  
    |파티션 옵션|**\@partition_options**|  
    |BLOB 열 스트리밍|**\@stream_blob_columns**|  
    |필터 형식|**\@filter_type**(**sp_addmergefilter**의 매개 변수)|  
  
     이러한 매개 변수에 대한 자세한 내용은 [sp_addmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql) 및 [sp_addmergefilter&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql)를 참조하세요.  
  
-   트랜잭션 복제 및 필터링되지 않은 병합 복제에서는 여러 게시에 테이블을 게시한 다음 구독 데이터베이스의 단일 테이블 내에서 구독할 수 있습니다. 이를 일반적으로 롤업 시나리오라고 합니다. 롤업은 중앙 구독자의 한 테이블에서 여러 위치에 있는 데이터 하위 집합을 집계하는 데 주로 사용됩니다. 필터링된 병합 게시는 중앙 구독자 시나리오를 지원하지 않습니다. 병합 복제의 경우 롤업은 일반적으로 매개 변수가 있는 행 필터가 포함된 단일 게시를 통해 구현됩니다. 자세한 내용은 [매개 변수가 있는 행 필터](../merge/parameterized-filters-parameterized-row-filters.md)를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [기존 게시에 대한 아티클 추가 및 삭제](add-articles-to-and-drop-articles-from-existing-publications.md)   
 [배포 구성](../configure-distribution.md)   
 [구독 초기화](../initialize-a-subscription.md)   
 [복제 스크립팅](../scripting-replication.md)   
 [게시자 보안 설정](../security/secure-the-publisher.md)   
 [게시 구독](../subscribe-to-publications.md)  
  
  
