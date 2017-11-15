---
title: "메모리 액세스에 최적화된 테이블 구독자로 복제 | Microsoft 문서"
ms.custom: SQL2016_New_Updated
ms.date: 11/21/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1a8e6bc7-433e-471d-b646-092dc80a2d1a
caps.latest.revision: "23"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: eda94d43e65319f152ea387372c5f28193697818
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="replication-to-memory-optimized-table-subscribers"></a>메모리 액세스에 최적화된 테이블 구독자로 복제
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 트랜잭션 복제를 제외하고는 스냅숏 및 트랜잭션 복제 구독자 역할을 수행하는 테이블을 메모리 최적화 테이블로 구성할 수 있습니다. 다른 복제 구성은 메모리 최적화 테이블과 호환되지 않습니다. 이 기능은 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]부터 사용할 수 있습니다.  
  
## <a name="two-configurations-are-required"></a>필요한 두 가지 구성  
  
-   
            **메모리 최적화 테이블로의 복제를 지원하도록 구독자 데이터베이스 구성**  
  
     [sp_addsubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 또는 [sp_changesubscription&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)을 사용하여 **@memory_optimized** 속성을 **true**로 설정합니다.  
  
-   
            **메모리 최적화 테이블로의 복제를 지원하도록 아티클 구성**  
  
     [sp_addarticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md) 또는 [sp_changearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)을 사용하여 아티클의 `@schema_option = 0x40000000000` 옵션을 설정합니다.  
  
#### <a name="to-configure-a-memory-optimized-table-as-a-subscriber"></a>메모리 최적화 테이블을 구독자로 구성하려면  
  
1.  트랜잭션 게시를 만듭니다. 자세한 내용은 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)를 참조하세요.  
  
2.  아티클을 게시에 추가합니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
     [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 구성하는 경우 **sp_addarticle** 저장 프로시저의 **@schema_option** 매개 변수를   
    **0x40000000000**으로 설정합니다.  
  
3.  아티클 속성 창에서 **메모리 최적화 사용** 을 **true**로 설정합니다.  
  
4.  스냅숏 에이전트 작업을 시작하여 이 게시에 대한 초기 스냅숏을 생성합니다. 자세한 내용은 [Create and Apply the Initial Snapshot](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)을 참조하세요.  
  
5.  이제 새 구독을 만듭니다. **새 구독 마법사** 에서 **메모리 액세스에 최적화된 구독** 을 **true**로 설정합니다.  
  
 메모리 액세스에 최적화된 테이블이 이제 게시자로부터 업데이트 수신을 시작합니다.  
  
#### <a name="reconfigure-an-existing-transaction-replication"></a>기존 트랜잭션 복제 다시 구성  
  
1.  [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 구독 속성으로 이동한 다음 **메모리 액세스에 최적화된 구독** 을 **true**로 설정합니다. 구독을 다시 초기화해야 변경 내용이 적용됩니다.  
  
     [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 구성하는 경우 **sp_addsubscription** 저장 프로시저의 **@memory_optimized** 매개 변수를 true로 설정합니다.  
  
2.  	[!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 에서 아티클 속성으로 이동한 다음 **메모리 최적화 사용** 을 true로 설정합니다.  
  
     [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 구성하는 경우 **sp_addarticle** 저장 프로시저의 **@schema_option** 매개 변수를   
    **0x40000000000**으로 설정합니다.  
  
3.  메모리 액세스에 최적화된 테이블은 클러스터형 인덱스를 지원하지 않습니다. 클러스터형 인덱스를 대상에서 비클러스터형 인덱스로 변환하여 복제에서 해당 인덱스를 처리하도록 하려면 **메모리 액세스에 최적화된 아티클에 대해 클러스터형 인덱스를 비클러스터형 인덱스로 변환** 을 true로 설정합니다.  
  
     [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 구성하는 경우 **sp_addarticle** 저장 프로시저의 **@schema_option** 매개 변수를 **0x0000080000000000**으로 설정합니다.  
  
4.  스냅숏을 다시 생성합니다.  
  
5.  구독을 다시 초기화합니다.  
  
## <a name="remarks-and-restrictions"></a>주의 및 제한 사항  
 단방향 트랜잭션 복제만 지원됩니다. 피어 투 피어 트랜잭션 복제는 지원되지 않습니다.  
  
 메모리 액세스에 최적화된 테이블은 게시할 수 없습니다.  
  
 배포자의 복제 테이블은 메모리 최적화 테이블로 구성할 수 없습니다.  
  
 병합 복제는 메모리 최적화 테이블을 포함할 수 없습니다.  
  
 구독자에서 트랜잭션 복제와 관련된 테이블은 메모리 최적화 테이블로 구성할 수 있지만 구독자 테이블은 메모리 최적화 테이블의 요구 사항을 충족해야 합니다. 여기에는 다음과 같은 제한 사항이 필요합니다.  
 
-   구독자에서 메모리 최적화 테이블로 복제된 테이블은 메모리 최적화 테이블에 허용된 데이터 형식으로 제한됩니다. 자세한 내용은 [메모리 내 OLTP에 지원되는 데이터 형식](../../relational-databases/in-memory-oltp/supported-data-types-for-in-memory-oltp.md)을 참조하세요.  
  
-   모든 Transact-SQL 기능이 메모리 최적화 테이블에서 지원되는 것은 아닙니다. 자세한 내용은 [메모리 내 OLTP에서 지원되지 않는 Transact-SQL 구문](../../relational-databases/in-memory-oltp/transact-sql-constructs-not-supported-by-in-memory-oltp.md)을 참조하세요.  
  
##  <a name="Schema"></a> 스키마 파일 수정  
  
-   메모리 최적화 테이블 옵션 `DURABILITY = SCHEMA_AND_DATA`를 사용할 경우 테이블은 비클러스터형 기본 키 인덱스를 포함해야 합니다.  
  
-   ANSI_PADDING은 ON이어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 기능 및 태스크](../../relational-databases/replication/replication-features-and-tasks.md)  
  
  
