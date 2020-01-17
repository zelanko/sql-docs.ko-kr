---
title: FILESTREAM 호환성 | Microsoft Docs
description: FILESTREAM과 기타 SQL Server 기능 간 호환성
ms.custom: seo-lt-2019
ms.date: 12/13/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FILESTREAM [SQL Server], other SQL Server features and
- FILESTREAM [SQL Server], limitations
ms.assetid: d2c145dc-d49a-4f5b-91e6-89a2b0adb4f3
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c4d32598cfab0cc08ece6721b0ff593c8577394d
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75245402"
---
# <a name="filestream-compatibility-with-other-sql-server-features"></a>FILESTREAM과 기타 SQL Server 기능 간 호환성

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  FILESTREAM 데이터는 파일 시스템에 있으므로 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다음 기능과 함께 FILESTREAM을 사용할 경우 몇 가지 고려 사항, 지침 및 제한 사항에 대해 설명합니다.  
  
-   [SSIS(SQL Server Integration Services)](#ssis)  
  
-   [분산 쿼리 및 연결된 서버](#distqueries)  
  
-   [암호화](#encryption)  
  
-   [데이터베이스 스냅샷](#DatabaseSnapshot)  
  
-   [복제](#Replication)  
  
-   [로그 전달](#LogShipping)  
  
-   [데이터베이스 미러링](#DatabaseMirroring)  
  
-   [전체 텍스트 인덱싱](#FullText)  
  
-   [장애 조치(Failover) 클러스터링](#FailoverClustering)  
  
-   [SQL Server Express](#SQLServerExpress)  
  
-   [포함된 데이터베이스](#contained)  
  
##  <a name="ssis"></a> SSIS(SQL Server Integration Services)  
 SSIS(SQL Server Integration Services)는 DT_IMAGE SSIS 데이터 형식을 사용하여 다른 BLOB 데이터와 마찬가지로 데이터 흐름의 FILESTREAM 데이터를 처리합니다.  
  
 열 가져오기 변환을 사용하여 파일 시스템에서 FILESTREAM 열로 파일을 로드할 수 있습니다. 열 내보내기 변환을 사용하여 FILESTREAM 열에서 파일 시스템의 다른 위치로 파일을 추출할 수도 있습니다.  
  
##  <a name="distqueries"></a> 분산 쿼리 및 연결된 서버  
 FILESTREAM 데이터를 **varbinary(max)** 데이터로 처리하여 분산 쿼리 및 연결된 서버를 통해 사용할 수 있습니다. 네 부분으로 된 이름을 사용하는 분산 쿼리에는 FILESTREAM **PathName()** 함수를 사용할 수 없습니다. 해당 이름이 로컬 서버를 참조하는 경우에도 마찬가지입니다. 그러나 **OPENQUERY()** 를 사용하는 통과 쿼리의 내부 쿼리에는 **PathName()** 을 사용할 수 있습니다.  
  
##  <a name="encryption"></a> 암호화  
 투명한 데이터 암호화를 사용하는 경우에도 FILESTREAM 데이터는 암호화되지 않습니다.  
  
##  <a name="DatabaseSnapshot"></a> 데이터베이스 스냅샷  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 FILESTREAM 파일 그룹에 대해 [데이터베이스 스냅샷](../../relational-databases/databases/database-snapshots-sql-server.md) 을 지원하지 않습니다. FILESTREAM 파일 그룹이 CREATE DATABASE ON 절에 들어 있으면 이 문이 실패하고 오류가 발생합니다.  
  
 FILESTREAM을 사용할 경우 FILESTREAM이 아닌 표준 파일 그룹의 데이터베이스 스냅샷을 만들 수 있습니다. FILESTREAM 파일 그룹은 이러한 데이터베이스 스냅샷에 대해 오프라인으로 표시됩니다.  
  
 데이터베이스 스냅샷의 FILESTREAM 테이블에서 실행되는 SELECT 문에는 FILESTREAM 열이 포함되지 않아야 합니다. 이 열이 포함되면 다음 오류 메시지가 반환됩니다.  
  
 `Could not continue scan with NOLOCK due to data movement.`  
  
##  <a name="Replication"></a> Replication  
 게시자에서 FILESTREAM 특성을 사용할 수 있는 **varbinary(max)** 열을 FILESTREAM 특성을 사용하거나 사용하지 않고 구독자로 복제할 수 있습니다. 열의 복제 방법을 지정하려면 **아티클 속성 - \<Article>** 대화 상자를 사용하거나 [sp_addarticle](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 또는 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)의 @schema_option 매개 변수를 사용합니다. FILESTREAM 특성이 없는 **varbinary(max)** 열에 복제된 데이터는 해당 데이터 형식에 대해 2GB 제한을 초과할 수 없습니다. 초과할 경우 런타임 오류가 발생합니다. 데이터를 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에 복제하는 경우가 아니면 FILESTREAM 특성을 복제하는 것이 좋습니다. FILESTREAM 열이 있는 테이블은 지정된 스키마 옵션에 상관없이 [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] 구독자에 복제할 수 없습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 구독자로 대형 데이터 값을 복제하면 최대 256MB 데이터 값으로 제한됩니다. 자세한 내용은 [SQL Server 2005의 최대 용량 사양](https://go.microsoft.com/fwlink/?LinkId=103810)을 참조하십시오.  
  
### <a name="considerations-for-transactional-replication"></a>트랜잭션 복제에 대한 고려 사항  
 트랜잭션 복제를 위해 게시된 테이블의 FILESTREAM 열을 사용할 경우 다음 사항을 고려하십시오.  
  
-   FILESTREAM 특성을 포함하는 열이 테이블에 있으면 [sp_addpublication](../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)의 @sync_method 속성에 *database snapshot* 또는 *database snapshot character* 값을 사용할 수 없습니다.  
  
-   max text repl size 옵션은 복제를 위해 게시된 열에 삽입할 수 있는 데이터의 최대 크기를 지정합니다. 이 옵션을 사용하여 복제되는 FILESTREAM 데이터의 크기를 제어할 수 있습니다.  
  
-   스키마 옵션을 지정하여 FILESTREAM 특성을 복제할 때 FILESTREAM에 필요한 **uniqueidentifier** 열을 필터링하거나 해당 열에 대한 UNIQUE 제약 조건을 복제하지 않도록 지정하면 복제가 FILESTREAM 특성을 복제하지 않습니다. 열은 **varbinary(max)** 열로만 복제됩니다.  
  
### <a name="considerations-for-merge-replication"></a>병합 복제에 대한 고려 사항  
 병합 복제를 위해 게시된 테이블에서 FILESTREAM 열을 사용할 경우 다음 사항을 고려하십시오.  
  
-   병합 복제 및 FILESTREAM은 테이블의 각 행을 식별하는 데 **uniqueidentifier** 데이터 형식의 열을 필요로 합니다. 병합 복제 시 테이블에 이러한 열이 없으면 자동으로 열이 추가됩니다. 병합 복제를 수행하려면 열에는 ROWGUIDCOL 속성 집합과 NEWID() 또는 NEWSEQUENTIALID()의 기본값이 있어야 합니다. 또한 FILESTREAM의 경우에는 열에 대해 UNIQUE 제약 조건이 정의되어야 합니다. 결과적으로 다음과 같은 작업이 필요합니다.  
  
    -   병합 복제를 위해 이미 게시된 테이블에 FILESTREAM 열을 추가할 경우 **uniqueidentifier** 열에 UNIQUE 제약 조건이 있는지 확인합니다. UNIQUE 제약 조건이 없을 경우 게시 데이터베이스의 테이블에 명명된 제약 조건을 추가합니다. 기본적으로 병합 복제에서는 이러한 스키마 변경을 게시하고 각 구독 데이터베이스에 적용합니다.  
  
         설명한 대로 UNIQUE 제약 조건을 수동으로 추가하고 병합 복제를 제거하려면 먼저 UNIQUE 제약 조건부터 제거해야 합니다. 그렇지 않으면 복제 제거가 실패합니다.  
  
    -   NEWSEQUENTIALID()가 NEWID()보다 성능이 더 좋으므로 병합 복제에서는 기본적으로 NEWSEQUENTIALID()를 사용합니다. 병합 복제를 위해 게시될 테이블에 **uniqueidentifier** 열을 추가할 경우 NEWSEQUENTIALID()를 기본값으로 지정합니다.  
  
-   병합 복제에는 큰 개체 유형을 위한 최적화가 포함됩니다. 이 최적화 작업은 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)의 @stream_blob_columns 매개 변수를 통해 제어됩니다. FILESTREAM 특성을 복제하도록 스키마 옵션을 설정하면 @stream_blob_columns 매개 변수 값이 **true**로 설정됩니다. 이러한 최적화 작업은 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 사용하여 덮어쓸 수 있습니다. 다음 저장 프로시저를 통해 @stream_blob_columns를 **false**로 설정할 수 있습니다. 병합 복제를 위해 이미 게시된 테이블에 FILESTREAM 열을 추가하는 경우 sp_changemergearticle을 사용하여 옵션을 **true** 로 설정하는 것이 좋습니다.  
  
-   아티클이 만들어진 후 FILESTREAM의 스키마 옵션을 사용하면 FILESTREAM 열의 데이터가 2GB가 넘고 복제 도중 충돌이 있을 경우 복제에 실패할 수 있습니다. 이러한 상황의 발생을 예상할 경우 만들 때 사용할 수 있는 적절한 FILESTREAM 스키마 옵션을 사용하여 테이블 아티클을 삭제하고 다시 만드는 것이 좋습니다.  
  
-   병합 복제는 [웹 동기화](../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 사용하여 HTTPS 연결을 통해 FILESTREAM 데이터를 동기화할 수 있습니다. 이 데이터는 웹 동기화에 대해 50MB 제한을 초과할 수 없습니다. 초과할 경우 런타임 오류가 발생합니다.  
  
##  <a name="LogShipping"></a> 로그 전달  
 [로그 전달](../../database-engine/log-shipping/about-log-shipping-sql-server.md) 은 FILESTREAM을 지원합니다. 주 서버 및 보조 서버는 모두 [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]이상 버전을 실행해야 하고 FILESTREAM이 설정되어 있어야 합니다.  
  
##  <a name="DatabaseMirroring"></a> 데이터베이스 미러링  
 데이터베이스 미러링은 FILESTREAM을 지원하지 않습니다. 주 서버에서 FILESTREAM 파일 그룹을 만들 수 없습니다. FILESTREAM 파일 그룹이 포함된 데이터베이스에 대해 데이터베이스 미러링을 구성할 수 없습니다.  
  
##  <a name="FullText"></a> 전체 텍스트 인덱싱  
 [전체 텍스트 인덱싱](../../relational-databases/search/populate-full-text-indexes.md) 은 **varbinary(max)** 열과 함께 작동하는 것과 동일한 방식으로 FILESTREAM 열과 함께 작동합니다. FILESTREAM 테이블에는 각 FILESTREAM BLOB에 대한 파일 이름 확장명을 포함하는 열이 있어야 합니다. 자세한 내용은 [전체 텍스트 검색을 사용한 쿼리](../../relational-databases/search/query-with-full-text-search.md), [검색 필터 구성 및 관리](../../relational-databases/search/configure-and-manage-filters-for-search.md), [sys.fulltext_document_types&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md)를 참조하세요.  
  
 전체 텍스트 엔진은 FILESTREAM BLOB의 내용을 인덱싱합니다. 이미지와 같은 인덱싱 파일은 유용하지 않을 수도 있습니다. FILESTREAM BLOB이 업데이트되면 인덱스가 다시 작성됩니다.  
  
##  <a name="FailoverClustering"></a> 장애 조치(Failover) 클러스터링  
 장애 조치(failover) 클러스터링의 경우 FILESTREAM 파일 그룹이 공유 디스크에 있어야 합니다. FILESTREAM은 FILESTREAM 인스턴스를 호스팅할 클러스터의 각 노드에 설정되어 있어야 합니다. 자세한 내용은 [장애 조치(failover) 클러스터에서 FILESTREAM 설정](../../relational-databases/blob/set-up-filestream-on-a-failover-cluster.md)을 참조하세요.  
  
##  <a name="SQLServerExpress"></a> SQL Server Express  
 [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] 은 FILESTREAM을 지원합니다. 10GB의 데이터베이스 크기 제한에는 FILESTREAM 데이터 컨테이너가 포함되지 않습니다.  
  
##  <a name="contained"></a> 포함된 데이터베이스  
 FILESTREAM 기능을 사용하려면 데이터베이스 외부에서의 몇 가지 구성이 필요합니다. 따라서 FILESTREAM 또는 FileTable을 사용하는 데이터베이스는 완전히 포함되지 않습니다.  
  
 포함된 사용자와 같은 포함된 데이터베이스의 특정 기능을 사용하려면 데이터베이스 포함 옵션을 PARTIAL로 설정하면 됩니다. 그러나 이 경우 일부 데이터베이스 설정은 데이터베이스에 포함되지 않으며 데이터베이스를 이동할 때 자동으로 이동되지 않는다는 것을 알고 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [Blob&#40;Binary Large Object&#41; 데이터&#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md)  
  
  
