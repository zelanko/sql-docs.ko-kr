---
title: "아티클 유형 정의(복제 Transact-SQL 프로그래밍) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "게시 [SQL Server 복제], 저장 프로시저 실행"
  - "아티클 [SQL Server 복제], 트랜잭션 복제 옵션"
  - "아티클 [SQL Server 복제], 병합 복제 옵션"
  - "저장 프로시저 [SQL Server 복제], 게시"
ms.assetid: d7effbac-c45b-423f-97ae-fd426b1050ba
caps.latest.revision: 26
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 26
---
# 아티클 유형 정의(복제 Transact-SQL 프로그래밍)
  복제를 위한 기본 아티클 유형은 테이블 아티클이지만 뷰, 저장 프로시저, 사용자 정의 함수 및 저장 프로시저 실행을 포함한 다른 데이터베이스 개체를 아티클로 게시할 수 있습니다. 아티클을 정의할 때 복제 저장 프로시저를 사용하여 아티클 유형을 프로그래밍 방식으로 지정할 수 있습니다. 사용되는 저장 프로시저는 복제 유형 및 아티클 유형에 따라 다릅니다.  
  
> [!NOTE]  
>  테이블, 뷰 및 저장 프로시저 아티클을 정의하는 경우 스키마 전용 지정은 개체 정의만 복제됨을 나타냅니다.  
  
### 트랜잭션 또는 스냅숏 게시에 테이블 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. **@type** 에 대해 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **logbased** -로그 기반 테이블 아티클에 트랜잭션 및 스냅숏 복제에 대 한 기본값입니다. 행 필터링에 사용되는 저장 프로시저와 열 필터링된 아티클을 정의하는 뷰가 자동으로 생성됩니다.  
  
    -   **logbased manualfilter** -는 로그 기반의 행 필터링 된 아티클입니다 여기서 행 필터링에 사용 되는 저장된 프로시저 수동으로 생성 하 고 사용자가 정의 되어에 대해 지정 된 **@filter**합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
    -   **logbased manualview** -열 필터링 된 아티클을 정의 하는 뷰 생성 하 고 사용자가 정의 및에 대해 지정 된 로그를 기반으로 필터링 문서 **@sync_object**합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
    -   **logbased manualboth** -는 로그 기반의 가로 및 세로로 아티클이 행 필터링 및 열 필터링 된 아티클을 정의 하는 보기에 사용 되는 저장된 프로시저는 생성 하 고 사용자가 정의 및에 대해 지정 된 **@filter** 및 **@sync_object**, 각각. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  에 대 한 **logbased manualboth** 및 **logbased manualfilter** 기사, 실행 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 행 필터링 된 아티클에 대 한 필터링 저장된 프로시저를 생성 하 합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
3.  에 대 한 **logbased manualboth**, **logbased manualview**, 및 **logbased manualfilter** 기사, 실행 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 열 필터링 된 아티클을 정의 하는 뷰를 생성 하 합니다. 자세한 내용은 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요.  
  
### 트랜잭션 또는 스냅숏 게시에 뷰 또는 인덱싱된 뷰 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. **@type** 에 대해 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **indexed view l** -로그 기반의 인덱싱된 뷰 아티클입니다. 행 필터링에 사용되는 저장 프로시저와 열 필터링된 아티클을 정의하는 뷰가 자동으로 생성됩니다.  
  
    -   **뷰 스키마 전용** -스키마 전용 뷰 아티클입니다. 기본 테이블도 복제되어야 합니다.  
  
    -   **인덱싱된 뷰 스키마 전용** -스키마 전용 인덱싱된 뷰 아티클입니다. 기본 테이블도 복제되어야 합니다.  
  
    -   **인덱싱된 뷰 logbased manualfilter** -는 로그 기반의 행 필터링 된 인덱싱된 뷰 아티클입니다 여기서 행 필터링에 사용 되는 저장된 프로시저 수동으로 생성 하 고 사용자가 정의 되어에 대해 지정 된 **@filter**합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
    -   **인덱싱된 뷰 logbased manualview** -열 필터링 된 아티클을 정의 하는 뷰 생성 하 고 사용자가 정의 및에 대해 지정 된 로그를 기반으로 필터링 된 인덱싱된 뷰 아티클에 **@sync_object**합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
    -   **인덱싱된 뷰 logbased manualboth** -는 로그 기반의 필터링 된 인덱싱된 뷰 아티클입니다 행 필터링 및 열 필터링 된 아티클을 정의 하는 보기에 사용 되는 저장된 프로시저 생성 하 고 사용자가 정의 및에 대해 지정 된 **@filter** 및 **@sync_object**, 각각. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md) 및 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)를 참조하세요.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
2.  에 대 한 **logbased manualboth** 및 **logbased manualfilter** 기사, 실행 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 행 필터링 된 아티클에 대 한 필터링 저장된 프로시저를 생성 하 합니다. 자세한 내용은 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)을 참조하세요.  
  
3.  에 대 한 **logbased manualboth**, **logbased manualview**, 및 **logbased manualfilter** 기사, 실행 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 열 필터링 된 아티클을 정의 하는 뷰를 생성 하 합니다. 자세한 내용은 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요.  
  
### 저장 프로시저, 저장 프로시저 실행 또는 사용자 정의 함수 아티클을 트랜잭션 또는 스냅숏 게시에 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)합니다. **@type** 에 대해 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **프로시저 스키마 전용** -스키마 전용 저장된 프로시저 아티클입니다.  
  
    -   **proc exec** -아티클의 모든 구독자로 저장된 프로시저의 실행을 복제 합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
    -   **serializable proc exec** -직렬화 가능 트랜잭션의 컨텍스트 내에서 실행 되는 경우에 저장된 프로시저의 실행을 복제 합니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)를 참조하세요.  
  
    -   **func 스키마만** -스키마 전용 사용자 정의 함수 아티클을 합니다.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
### 병합 게시에 테이블 또는 뷰 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. **@type** 에 대해 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **테이블** -테이블 아티클에 합니다.  
  
    -   **인덱싱된 뷰 스키마 전용** -스키마 전용 인덱싱된 뷰 아티클입니다.  
  
    -   **뷰 스키마 전용** -스키마 전용 뷰 아티클입니다.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
### 병합 게시에 저장 프로시저 또는 사용자 정의 함수 아티클을 게시하려면  
  
1.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)합니다. **@type** 에 대해 다음 값 중 하나를 지정하여 아티클 유형을 정의합니다.  
  
    -   **func 스키마만** -스키마 전용 사용자 정의 함수 아티클을 합니다.  
  
    -   **프로시저 스키마 전용** -스키마 전용 저장된 프로시저 아티클입니다.  
  
     게시에 대한 새 아티클을 정의합니다. 자세한 내용은 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
## 참고 항목  
 [복제 시스템 저장 프로시저 개념](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  