---
title: 게시 데이터베이스의 스키마 변경 | Microsoft 문서
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], schema changes
- snapshot replication [SQL Server], replicating schema changes
- merge replication [SQL Server replication], replicating schema changes
- transactional replication, replicating schema changes
- schemas [SQL Server replication], replicating changes
- publishing [SQL Server replication], schema changes
ms.assetid: 926c88d7-a844-402f-bcb9-db49e5013b69
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c82c9913b75ca363d4ace1413c0c4413989c116a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605371"
---
# <a name="make-schema-changes-on-publication-databases"></a>게시 데이터베이스의 스키마 변경
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  복제는 게시된 개체에 대한 다양한 스키마 변경을 지원합니다. [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자에 게시된 개체에 대해 다음 스키마 변경을 수행하면 기본적으로 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 구독자에 변경 내용이 전파됩니다.  
  
-   ALTER TABLE  
  
-   스키마 변경 복제가 활성화되어 있고 토폴로지에 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 또는 [!INCLUDE[ssEWnoversion](../../../includes/ssewnoversion-md.md)] Subscribers가 포함된 경우 ALTER TABLE SET LOCK ESCALATION을 사용해서는 안 됩니다.

-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
     DDL(데이터 정의 언어) 트리거는 복제할 수 없기 때문에 DML(데이터 조작 언어) 트리거에 대해서만 ALTER TRIGGER를 사용할 수 있습니다.  
  
> [!IMPORTANT]  
>  테이블에 대한 스키마 변경은 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 또는 SMO( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects)를 사용하여 수행해야 합니다. [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]에서 스키마를 변경하면 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] 에서는 해당 테이블을 삭제하고 다시 만들려고 합니다. 그러나 게시된 개체는 삭제할 수 없으므로 스키마 변경에 실패합니다.  
  
 트랜잭션 복제 및 병합 복제의 경우 배포 에이전트 또는 병합 에이전트가 실행될 때 스키마 변경이 증분 방식으로 전파됩니다. 스냅숏 복제의 경우 새 스냅숏을 구독자에서 적용할 때 스키마 변경이 전파됩니다. 스냅숏 복제에서 스키마의 새 복사본은 동기화가 발생할 때마다 구독자로 전달됩니다. 그러므로 이전에 게시된 개체에 대한 모든 스키마 변경(위에서 나열한 것 이외의 스키마 변경도 포함)이 동기화를 수행할 때마다 자동으로 전파됩니다.  
  
 게시에서 아티클을 추가 및 제거하는 방법에 대한 자세한 내용은 [기존 게시에 대한 아티클 추가 및 삭제](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)를 참조하세요.  
  
 **스키마 변경을 복제하려면**  
  
 위에 나열된 스키마 변경은 기본적으로 복제됩니다. 스키마 변경 복제를 해제하는 방법은 [Replicate Schema Changes](../../../relational-databases/replication/publish/replicate-schema-changes.md)를 참조하십시오.  
  
## <a name="considerations-for-schema-changes"></a>스키마 변경에 대한 고려 사항  
 스키마 변경 복제 시 다음 사항을 고려하십시오.  
  
### <a name="general-considerations"></a>일반적인 고려 사항  
  
-   스키마 변경에는 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 설정한 제한 사항이 적용됩니다. 예를 들어 ALTER TABLE을 사용하여 기본 키 열을 변경할 수 없습니다.  
  
-   데이터 형식 매핑은 초기 스냅숏에 대해서만 수행됩니다. 스키마 변경은 이전 버전의 데이터 형식으로 매핑되지 않습니다. 예를 들어 `ALTER TABLE ADD datetime2 column` 에서 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]문을 사용하는 경우 데이터 형식이 **ssVersion2005** 구독자에 대한 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 로 변환되지 않습니다. 게시자에서 스키마 변경이 차단되는 경우도 있습니다.  
  
-   게시에서 스키마 변경을 전파할 수 있도록 설정하면 게시의 아티클에 대해 관련 스키마 옵션이 어떻게 설정되었는지에 상관없이 스키마 변경이 전파됩니다. 예를 들어 테이블 아티클에 대해 FOREIGN KEY 제약 조건을 복제하지 않도록 선택하고 게시자의 테이블에 외래 키를 추가하는 ALTER TABLE 명령을 실행하면 구독자의 테이블에 외래 키가 추가됩니다. 이를 방지하려면 ALTER TABLE 명령을 실행하기 전에 스키마 변경 전파를 해제합니다.  
  
-   스키마 변경은 구독자(재게시 구독자 포함)가 아닌 게시자에서만 수행해야 합니다. 병합 복제에서는 구독자에서 스키마를 변경할 수 없습니다. 트랜잭션 복제에서는 스키마를 변경할 수 있지만 이러한 변경으로 인해 복제가 실패할 수 있습니다.  
  
-   재게시 구독자로 전파된 변경 내용은 기본적으로 해당 구독자로 전파됩니다.  
  
-   스키마 변경이 게시자에는 존재하지만 구독자에는 존재하는 않는 개체 또는 제약 조건을 참조하면 게시자에서는 스키마 변경이 성공하지만 구독자에서는 실패합니다.  
  
-   외래 키를 추가할 때 참조되는 구독자에 있는 모든 개체의 이름 및 소유자는 게시자에 있는 해당 개체의 이름 및 소유자와 같아야 합니다.  
  
-   명시적인 인덱스 추가, 삭제 및 변경은 지원되지 않습니다. PRIMARY KEY 제약 조건과 같이 제약 조건에 대해 암시적으로 생성된 인덱스는 지원됩니다.  
  
-   복제에서 관리하는 ID 열은 변경 또는 삭제할 수 없습니다. ID 열 자동 관리에 대한 자세한 내용은 [ID 열 복제](../../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
-   게시자 데이터와 구독자 데이터가 서로 달라질 수 있기 때문에(데이터 불일치성이라고 함) 비결정적 함수를 포함하는 스키마 변경은 지원되지 않습니다. 예를 들어 게시자: `ALTER TABLE SalesOrderDetail ADD OrderDate DATETIME DEFAULT GETDATE()`에서 다음 명령을 실행하는 경우 다른 명령이 구독자에 복제되고 실행되면 값은 달라집니다. 비결정적 함수에 대한 자세한 내용은 [Deterministic and Nondeterministic Functions](../../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)를 참조하십시오.  
  
-   제약 조건의 이름을 명시적으로 지정하는 것이 좋습니다. 제약 조건의 이름을 명시적으로 지정하지 않은 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서 제약 조건에 이름을 생성하며 이러한 이름은 게시자와 각 구독자에서 다르게 됩니다. 이로 인해 스키마 변경 복제 시 문제가 발생할 수 있습니다. 예를 들어 게시자에서 열을 삭제하여 종속 제약 조건이 삭제된 경우 복제에서 구독자의 제약 조건을 삭제하려고 시도하지만 제약 조건의 이름이 다르기 때문에 구독자에서의 삭제 작업은 실패하게 됩니다. 제약 조건 명명 문제로 인해 동기화가 실패할 경우 구독자에서 수동으로 제약 조건을 삭제하고 병합 에이전트를 다시 실행하십시오.  
  
-   테이블을 복제용으로 게시하면 게시 스냅숏이 이미 생성되어 있는 경우 해당 테이블의 열을 XML 데이터 형식으로 변경할 수 없습니다. 열을 변경하려면 먼저 복제를 제거해야 합니다.  
  
-   커밋되지 않은 읽기는 게시된 테이블에서 DDL을 수행할 때 지원되는 격리 수준이 아닙니다.  
  
-   **SET CONTEXT_INFO** 는 게시된 개체에 대해 스키마 변경 내용이 수행된 트랜잭션 컨텍스트 수정에 사용할 수 없습니다.  
  
#### <a name="adding-columns"></a>열 추가  
  
-   테이블에 새 열을 추가한 후 이 열을 기존 게시에 포함하려면 ALTER TABLE \<Table> ADD \<Column>을 실행합니다. 기본적으로 이 열은 모든 구독자로 복제됩니다. 이 열에는 NULL 값이 허용되거나 기본 제약 조건이 포함되어야 합니다. 열을 추가하는 방법은 이 항목의 "병합 복제" 섹션을 참조하십시오.  
  
-   테이블에 새 열을 추가한 후 이 열을 기존 게시에 포함시키지 않으려면 스키마 변경 복제를 해제한 다음 ALTER TABLE \<Table> ADD \<Column>을 실행합니다.  
  
-   기존 게시에 기존 열을 포함시키려면 [sp_articlecolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), [sp_mergearticlecolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 또는 **게시 속성 - \<Publication>** 대화 상자를 사용합니다.  
  
     자세한 내용은 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요. 이 작업을 수행하려면 구독을 다시 초기화해야 합니다.  
  
-   열이 구독자로 복제될 때 데이터가 일치하지 않을 수 있기 때문에 게시된 테이블에 ID 열을 추가할 수 없습니다. 게시자의 ID 열 값은 영향을 받는 테이블 행이 실제로 저장된 순서에 따라 달라집니다. 구독자에서는 행이 다르게 저장될 수 있으므로 ID 열의 값이 같은 행에 대해 다를 수 있습니다.  
  
#### <a name="dropping-columns"></a>열 삭제  
  
-   기존 게시에서 열을 삭제하고 해당 열을 게시자의 테이블에서 삭제하려면 ALTER TABLE \<Table> DROP \<Column>을 실행합니다. 기본적으로 해당 열이 모든 구독자의 테이블에서 삭제됩니다.  
  
-   열을 기존 게시에서는 삭제하지만 게시자의 테이블에서는 유지하려면 [sp_articlecolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md), [sp_mergearticlecolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 또는 **게시 속성 - \<게시>** 대화 상자를 사용합니다.  
  
     자세한 내용은 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)을 참조하세요. 이 작업을 수행하려면 새 스냅숏을 생성해야 합니다.  
  
-   삭제할 열은 데이터베이스에 있는 모든 게시 아티클의 필터 절에 사용할 수 없습니다.  
  
-   다음과 같이 게시된 아티클에서 열을 삭제할 때는 데이터베이스에 영향을 줄 수 있는 열의 제약 조건, 인덱스 또는 속성을 예를 들어 다음과 같이 사용할 수 있습니다.  
  
    -   트랜잭션 게시 아티클에서 기본 키에 사용되는 열은 복제에 사용되므로 삭제할 수 없습니다.  
  
    -   병합 게시 아티클의 rowguid 열이나 구독 업데이트를 지원하는 트랜잭션 게시 아티클의 mstran_repl_version 열은 복제에 사용되므로 삭제할 수 없습니다.  
  
    -   인덱스 변경은 구독자에 전파되지 않습니다. 게시자에서 열을 삭제하여 종속 인덱스가 삭제된 경우 인덱스 삭제는 복제되지 않습니다. 게시자에서 구독자로 복제 시에 열 삭제가 성공하려면 게시자에서 열을 삭제하기 전에 구독자에서 인덱스를 삭제해야 합니다. 구독자의 인덱스 때문에 동기화가 실패할 경우 수동으로 인덱스를 삭제하고 병합 에이전트를 다시 실행하십시오.  
  
    -   삭제가 가능하려면 제약 조건의 이름이 명시적으로 지정되어야 합니다. 자세한 내용은 이 항목의 앞에 나오는 "일반적인 고려 사항" 섹션을 참조하십시오.  
  
### <a name="transactional-replication"></a>트랜잭션 복제  
  
-   스키마 변경은 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하는 구독자로 전파되지만 DDL 문에는 구독자에서 해당 버전에 지원되는 구문만 포함되어야 합니다.  
  
     구독자에서 데이터를 다시 게시하면 열을 추가 및 삭제하는 스키마 변경만 지원됩니다. 이러한 변경은 게시자에서 ALTER TABLE DDL 구문이 아니라 [sp_repladdcolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) 및 [sp_repldropcolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md)을 사용하여 수행해야 합니다.  
  
-   SQL Server 이외 구독자로는 스키마 변경이 복제되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 이외 게시자로부터는 스키마 변경이 전파되지 않습니다.  
  
-   테이블로 복제되는 인덱싱된 뷰는 변경할 수 없습니다. 인덱싱된 뷰로 복제되는 인덱싱된 뷰는 변경할 수 있지만 변경하면 인덱싱된 뷰가 아닌 일반 뷰가 됩니다.  
  
-   게시에서 즉시 업데이트 구독 또는 지연 업데이트 구독을 지원하면 스키마를 변경하기 전에 시스템을 정지해야 합니다. 즉, 게시된 테이블에 대한 모든 작업을 게시자와 구독자에서 중지하고 보류 중인 데이터 변경 내용을 모든 노드에 전파해야 합니다. 스키마 변경을 모든 노드로 전파하면 게시된 테이블에 대한 작업을 재개할 수 있습니다.  
  
-   피어 투 피어 토폴로지의 게시에서는 스키마를 변경하기 전에 시스템을 정지해야 합니다. 자세한 내용은 [복제 토폴로지 정지&#40;복제 Transact-SQL 프로그래밍&#41;](../../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)를 참조하세요.  
  
-   테이블에 타임스탬프 열을 추가하고 이 타임스탬프를 binary(8)로 매핑하면 아티클이 모든 활성 구독에 대해 다시 초기화됩니다.  
  
### <a name="merge-replication"></a>병합 복제  
  
-   병합 복제에서 스키마 변경을 처리하는 방법은 게시 호환성 수준 및 스냅숏이 기본 모드(기본값) 또는 문자 모드로 설정되었는지에 의해 결정됩니다.  
  
    -   스키마 변경을 복제하려면 게시의 호환성 수준이 적어도 90RTM 이상이어야 합니다. 구독자에서 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]를 실행하거나 호환성 수준이 90RTM 이하인 경우에도 [sp_repladdcolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repladdcolumn-transact-sql.md) 및 [sp_repldropcolumn&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-repldropcolumn-transact-sql.md)을 사용하여 열을 추가 및 삭제할 수 있습니다. 그러나 이러한 프로시저는 더 이상 사용되지 않습니다.  
  
    -   [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에서 도입된 데이터 형식의 열을 기존 아티클에 추가하려는 경우 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 다음과 같이 동작합니다.  
  
        ||100RTM, 기본 스냅숏|100RTM, 문자 스냅숏|다른 모든 호환성 수준|  
        |-|-----------------------------|--------------------------------|------------------------------------|  
        |**hierarchyid**|변경 허용|변경 차단|변경 차단|  
        |**geography** 및 **geometry**|변경 허용|변경 허용*|변경 차단|  
        |**filestream**|변경 허용|변경 차단|변경 차단|  
        |**date**, **time**, **datetime2**및 **datetimeoffset**|변경 허용|변경 허용*|변경 차단|  
  
         *SQL Server Compact 구독자는 구독자에서의 이러한 데이터 형식을 변환합니다.  
  
-   스키마 변경을 적용할 때 오류(예: 구독자에서 사용할 수 없는 테이블을 참조하는 외래 키를 추가할 때 발생하는 오류)가 발생하면 동기화가 실패하므로 구독을 다시 초기화해야 합니다.  
  
-   조인 필터 또는 매개 변수가 있는 필터와 관련된 열에 스키마 변경을 수행하면 모든 구독을 다시 초기화하고 스냅숏을 다시 생성해야 합니다.  
  
-   병합 복제에서는 문제를 해결하는 동안 스키마 변경을 건너뛸 수 있는 저장 프로시저를 제공합니다. 자세한 내용은 [sp_markpendingschemachange&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md) 및 [sp_enumeratependingschemachanges&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER TABLE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER VIEW&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-view-transact-sql.md)   
 [ALTER PROCEDURE&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-procedure-transact-sql.md)   
 [ALTER FUNCTION&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-function-transact-sql.md)   
 [ALTER TRIGGER&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-trigger-transact-sql.md)   
 [데이터 및 데이터베이스 개체 게시](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [스키마 변경 내용을 반영하기 위해 사용자 지정 트랜잭션 프로시저 다시 생성](../../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md)  
  
  
