---
title: "분할 테이블 및 인덱스 복제 | Microsoft Docs"
ms.custom: ""
ms.date: "09/10/2015"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "분할된 인덱스 [SQL Server], 복제"
  - "분할된 표 [SQL Server], 복제"
  - "복제 [SQL Server], 분할된 표"
  - "게시 [SQL Server 복제], 분할된 표"
  - "트랜잭션 복제, 분할된 표"
ms.assetid: c9fa81b1-6c81-4c11-927b-fab16301a8f5
caps.latest.revision: 20
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 20
---
# 분할 테이블 및 인덱스 복제
  분할을 사용하면 데이터 하위 집합을 빠르고 효율적으로 관리 및 액세스하는 동시에 데이터 컬렉션의 무결성을 유지할 수 있으므로 큰 테이블 또는 인덱스를 보다 편리하게 관리할 수 있습니다. 자세한 내용은 [Partitioned Tables and Indexes](../../../relational-databases/partitions/partitioned-tables-and-indexes.md)을 참조하세요. 복제는 분할된 테이블 및 인덱스를 처리하는 방법을 지정하는 속성 집합을 제공하여 분할을 지원합니다.  
  
## 트랜잭션 및 병합 복제에 대한 아티클 속성  
 다음 표에서는 데이터를 분할하는 데 사용되는 개체를 나열합니다.  
  
|개체|개체를 만드는 데 사용되는 명령|  
|------------|----------------------|  
|분할된 테이블 또는 인덱스|CREATE TABLE 또는 CREATE INDEX|  
|파티션 함수|CREATE PARTITION FUNCTION|  
|파티션 구성표|CREATE PARTITION SCHEME|  
  
 분할과 관련된 첫 번째 속성 집합은 파티션 개체를 구독자에 복사해야 하는지 여부를 결정하는 아티클 스키마 옵션입니다. 이러한 스키마 옵션은 다음과 같은 방법으로 설정할 수 있습니다.  
  
-   새 게시 마법사의 **아티클 속성** 페이지 또는 게시 속성 대화 상자를 사용합니다. 위의 표에 나온 개체를 복사하려면 **테이블 파티션 구성표 복사** 및 **인덱스 파티션 구성표 복사** 속성에 **true**값을 지정합니다. 액세스 하는 방법에 대 한 내용은 **아티클 속성** 페이지에서 참조 [보기 및 게시 속성을 수정](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)합니다.  
  
-   사용 하 여는 *schema_option* 다음 저장된 프로시저 중 하나의 매개 변수:  
  
    -   [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 또는 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md) 트랜잭션 복제에 대 한  
  
    -   [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 또는 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) 병합 복제에 대 한  
  
     위의 표에 나온 개체를 복사하려면 적절한 스키마 옵션 값을 지정합니다. 스키마 옵션을 지정하는 방법은 [Specify Schema Options](../../../relational-databases/replication/publish/specify-schema-options.md)을 참조하십시오.  
  
 복제는 초기 동기화 중에 개체를 구독자에 복사합니다. 파티션 구성표에서 PRIMARY 파일 그룹 이외의 파일 그룹을 사용하는 경우 초기 동기화 전에 이러한 파일 그룹이 구독자에 있어야 합니다.  
  
 구독자를 초기화하면 데이터 변경 사항이 구독자로 전파되고 해당 파티션에 적용됩니다. 그러나 파티션 구성표에 대한 변경은 지원되지 않습니다. 트랜잭션 및 병합 복제는 다음 명령의 복제를 지원하지 않습니다. ALTER INDEX의 ALTER PARTITION FUNCTION, ALTER PARTITION SCHEME 또는 REBUILD WITH PARTITION 문을 지원하지 않습니다. 연결된 변경 내용은 구독자에게 자동으로 복제되지 않습니다. 구독자에서 수동으로 비슷한 변경을 하려면 사용자에게 책임이 있습니다.  
  
## 파티션 전환을 위한 복제 지원  
 테이블 분할의 주요 이점 중 하나는 파티션 간에 데이터의 하위 집합을 빠르고 효율적으로 이동할 수 있다는 것입니다. 데이터는 SWITCH PARTITION 문을 사용하여 이동합니다. 기본적으로 복제를 사용할 수 있도록 테이블을 설정하면 다음과 같은 이유로 SWITCH PARTITION 작업이 차단됩니다.  
  
-   게시자에는 있지만 구독자에는 없는 테이블 안팎으로 데이터를 이동하면 게시자와 구독자 간에 일관성이 유지되지 않을 수 있습니다. 일반적으로 이 문제는 준비 테이블 안팎으로 데이터를 이동하는 경우 발생합니다.  
  
-   구독자에 있는 분할된 테이블에 대한 정의가 게시자에 있는 것과 다를 경우 배포 에이전트가 구독자에서 변경 내용을 적용하려고 하면 오류가 발생합니다.  
  
 이러한 잠재적인 문제에도 불구하고 트랜잭션 복제에 파티션 전환을 사용하도록 설정할 수 있습니다. 파티션 전환을 사용하도록 설정하기 전에 게시자와 구독자에서 파티션 전환과 관련된 모든 테이블이 있는지 확인하고 테이블과 파티션 정의가 동일한지 확인합니다.  
  
 파티션이 게시자 및 구독자를 설정할 수에서 정확 하 게 동일한 파티션 스키마를 포함 하는 경우 *allow_partition_switch* 와 함께 *replication_partition_switch* 파티션 전환 문만 구독자에만 복제 됩니다입니다. 또한 켤 수 *allow_partition_switch* DDL을 복제 하지 않고 있습니다. 이 기능은 파티션 중 오래된 개월을 롤링하지만 복제된 파티션을 구독자에서 백업 목적으로 다른 연도에도 유지하려는 경우에 유용합니다.  
  
 SQL Server 2008 R2 ~ 현재 버전에서 파티션 전환을 사용하도록 설정하는 경우 머지않아 분할 및 병합 작업이 필요할 수도 있습니다. 복제된 테이블에서 분할 또는 병합 작업을 실행하려면 먼저 문제의 파티션에 보류 중인 복제된 명령이 없는지 확인해야 합니다. 또한 분할 및 병합 작업 중에는 파티션에서 DML 작업이 실행되고 있지 않아야 합니다. 로그 판독기에서 처리하지 않은 트랜잭션이 있거나 복제된 표의 파티션에서 동일한 파티션과 관련된 분할 또는 병합 작업이 실행되는 동안 DML 작업이 수행되는 경우 로그 판독기 에이전트에서 처리 오류가 발생할 수 있습니다. 오류를 수정하기 위해 구독을 다시 초기화해야 할 수 있습니다.  
  
> [!WARNING]  
>  충돌을 감지하고 해결하는 데 사용되는 숨겨진 열로 인해 피어 투 피어 게시에 대해서는 파티션 전환을 사용하지 않아야 합니다.  
  
### 파티션 전환 설정  
 다음과 같은 트랜잭션 게시 속성을 사용하면 사용자가 복제된 환경에서 파티션 전환의 동작을 제어할 수 있습니다.  
  
-   **@allow_partition_switch**, 를로 설정 하면 **true**, 게시 데이터베이스에 대해 SWITCH PARTITION을 실행할 수 있습니다.  
  
-   **@replicate_partition_switch** SWITCH PARTITION DDL 문을 구독자에 복제 해야 하는지 여부를 결정 합니다. 이 옵션은 경우에만 유효 **@allow_partition_switch** 로 설정 된 **true**합니다.  
  
 사용 하 여 이러한 속성을 설정할 수 [sp_addpublication](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md) 게시를 만든 경우 또는 사용 하 여 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md) 게시를 만든 후입니다. 위에서 설명한 것처럼 병합 복제는 파티션 전환을 지원하지 않습니다. 병합 복제를 사용할 수 있도록 설정된 테이블에서 SWITCH PARTITION을 실행하려면 게시에서 해당 테이블을 제거합니다.  
  
## 참고 항목  
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  