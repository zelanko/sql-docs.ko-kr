---
title: "게시 및 아티클 만들기, 수정 및 삭제(복제) | Microsoft 문서"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], creating
- articles [SQL Server replication], defining
ms.assetid: e66d06ec-a12b-444d-875b-77f958af2f21
caps.latest.revision: "36"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee95ce967637c9b1be05d0ee4de552b1cb7ea4e4
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/18/2018
---
# <a name="create-modify-and-delete-publications-and-articles-replication"></a>게시 및 아티클 만들기, 수정 및 삭제(복제)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] 이 설명서 섹션에는 게시 생성 및 아티클 정의와 관련된 태스크에 대한 절차 정보가 포함되어 있습니다.  
  
## <a name="in-this-section"></a>섹션 내용  
  
-   [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)  
  
-   [아티클 정의](../../../relational-databases/replication/publish/define-an-article.md)  
  
-   [게시 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)  
  
-   [아티클 속성 보기 및 수정](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
-   [게시 삭제](../../../relational-databases/replication/publish/delete-a-publication.md)  
  
-   [아티클 삭제](../../../relational-databases/replication/publish/delete-an-article.md)  
  
-   [Oracle 데이터베이스에서 게시 만들기](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)  
  
-   [구독에 대한 만료 기간 설정](../../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)  
  
-   [스키마 옵션 지정](../../../relational-databases/replication/publish/specify-schema-options.md)  
  
-   [스키마 변경 내용 복제](../../../relational-databases/replication/publish/replicate-schema-changes.md)  
  
-   [ID 열 관리](../../../relational-databases/replication/publish/manage-identity-columns.md)  
  
-   [병합 게시에 대한 호환성 수준 설정](../../../relational-databases/replication/publish/set-the-compatibility-level-for-merge-publications.md)  
  
## <a name="snapshot-options"></a>스냅숏 옵션  
  
-   [스냅숏 형식 지정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-snapshot-format-sql-server-management-studio.md)  
  
-   [대체 스냅숏 폴더 위치 지정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/specify-an-alternate-snapshot-folder-location-sql-server-management-studio.md)  
  
-   [스냅숏 파일 압축&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/compress-snapshot-files-sql-server-management-studio.md)  
  
-   [스냅숏 속성 구성&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/configure-snapshot-properties-replication-transact-sql-programming.md)  
  
-   [스냅숏 적용 전후에 스크립트 실행&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/execute-scripts-before-and-after-a-snapshot-is-applied.md)  
  
-   [FTP를 통해 스냅숏 배달](../../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)  
  
## <a name="filtering-data"></a>데이터 필터링  
  
-   [열 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)  
  
-   [정적 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)  
  
-   [병합 아티클에 대한 매개 변수가 있는 행 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)  
  
-   [매개 변수가 있는 행 필터 최적화](../../../relational-databases/replication/publish/optimize-parameterized-row-filters.md)  
  
-   [병합 아티클 사이에서 조인 필터 정의 및 수정](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)  
  
-   [병합 아티클 간의 조인 필터 집합 자동 생성&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/automatically-generate-join-filters-between-merge-articles.md)  
  
## <a name="transactional-replication-options"></a>트랜잭션 복제 옵션  
  
-   [트랜잭션 아티클의 데이터 변경 내용을 전파하는 방법 설정](../../../relational-databases/replication/publish/set-the-propagation-method-for-data-changes-to-transactional-articles.md)  
  
-   [트랜잭션 게시에 대해 업데이트할 수 있는 구독 설정](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)  
  
-   [지연 업데이트 충돌 해결 옵션 설정&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/set-queued-updating-conflict-resolution-options-sql-server-management-studio.md)  
  
-   [저장 프로시저 실행을 트랜잭션 게시로 게시&#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/publish/publish-execution-of-stored-procedure-in-transactional-publication.md)  
  
## <a name="merge-replication-options"></a>병합 복제 옵션  
  
-   [병합 테이블 아티클 간의 논리적 레코드 관계 정의](../../../relational-databases/replication/publish/define-a-logical-record-relationship-between-merge-table-articles.md)  
  
-   [병합 테이블 아티클의 처리 순서 지정&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
-   [새 병합 테이블 아티클을 다운로드 전용으로 지정](../../../relational-databases/replication/publish/specify-that-a-merge-table-article-is-download-only.md)  
  
-   [병합 아티클에 대해 삭제가 추적되지 않도록 지정&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/publish/specify-that-deletes-should-not-be-tracked-for-merge-articles.md)  
  
-   [병합 아티클의 충돌 추적 및 해결 수준 지정](../../../relational-databases/replication/publish/specify-the-conflict-tracking-and-resolution-level-for-merge-articles.md)  
  
-   [병합 아티클 해결 프로그램 지정](../../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)  
  
-   [병합 아티클에 대한 상호 충돌 해결 프로그램 지정](../../../relational-databases/replication/publish/specify-interactive-conflict-resolution-for-merge-articles.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
