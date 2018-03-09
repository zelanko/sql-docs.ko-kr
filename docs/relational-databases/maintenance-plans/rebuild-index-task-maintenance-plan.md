---
title: "인덱스 다시 빌드 태스크(유지 관리 계획) | Microsoft 문서"
ms.custom: 
ms.date: 07/21/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: maintenance-plans
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- reindex
- sql13.swb.maint.reindex.f1
helpviewer_keywords:
- Rebuild Index Task dialog box
ms.assetid: 33e2940b-139f-4563-b0cb-5683f08bd879
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: f077a5071cfb7f3da4114fde9453cfa2c331783f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="rebuild-index-task-maintenance-plan"></a>인덱스 다시 작성 태스크(유지 관리 계획)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] **인덱스 다시 작성 태스크** 대화 상자를 사용하여 데이터베이스에 있는 테이블의 인덱스를 새 채우기 비율로 다시 만들 수 있습니다. 채우기 비율은 향후 확장을 수용하기 위해 각 인덱스 페이지에 남겨 둘 빈 공간을 결정합니다. 데이터를 테이블에 추가할 때는 채우기 비율이 유지되지 않으므로 사용 가능한 공간이 꽉 찹니다. 데이터 및 인덱스 페이지를 다시 구성하면 사용 가능한 공간을 다시 확보할 수 있습니다.  
  
 **인덱스 다시 작성 태스크** 는 ALTER INDEX 문을 사용합니다. 이 페이지에서 설명하는 옵션에 대한 자세한 내용은 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)를 참조하세요.  
  
## <a name="options"></a>옵션  
 **연결**  
 이 태스크를 수행할 때 사용할 서버 연결을 선택합니다.  
  
 **새로 만들기**  
 이 태스크를 수행할 때 사용할 새 서버 연결을 만듭니다. 아래에서는 **새 연결** 대화 상자에 대해 설명합니다.  
  
 **데이터베이스**  
 이 태스크의 영향을 받는 데이터베이스를 지정합니다.  
  
-   **모든 데이터베이스**  
  
     tempdb를 제외한 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다.  
  
-   **모든 시스템 데이터베이스**  
  
     tempdb를 제외한 각 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 사용자가 만든 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **모든 사용자 데이터베이스**  
  
     사용자가 만든 모든 데이터베이스에 대해 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템 데이터베이스에 대해서는 유지 관리 태스크가 실행되지 않습니다.  
  
-   **다음 데이터베이스**  
  
     선택한 데이터베이스에 대해서만 유지 관리 태스크를 실행하는 유지 관리 계획을 생성합니다. 이 옵션을 선택한 경우에는 목록에서 하나 이상의 데이터베이스를 선택해야 합니다.  
  
    > [!NOTE]  
    >  유지 관리 계획은 호환성 수준 80 이상으로 설정된 데이터베이스에 대해서만 실행합니다. 호환성 수준 70 이하로 설정된 데이터베이스는 표시되지 않습니다.  
  
 **개체**  
 테이블, 뷰 또는 둘 다를 표시하도록 **선택** 표를 제한합니다.  
  
 **선택**  
 이 태스크의 영향을 받는 테이블 또는 인덱스를 지정합니다. 개체 상자에서 **테이블 및 뷰** 를 선택한 경우에는 사용할 수 없습니다.  
  
 **페이지당 기본 여유 공간**  
 데이터베이스 테이블의 인덱스를 삭제하고 인덱스를 만들 때 지정한 채우기 비율로 인덱스를 다시 만듭니다.  
  
 **페이지당 빈 공간을 다음으로 변경**  
 데이터베이스 테이블의 인덱스를 삭제하고 자동으로 계산된 새 채우기 비율로 인덱스를 다시 만들기 때문에 인덱스 페이지에 대해 지정된 크기의 사용 가능한 공간이 예약됩니다. 이 비율이 커질수록 인덱스 페이지에 대해 더 많은 사용 가능한 공간이 예약되고 인덱스가 더 커집니다. 유효한 값은 0에서 100까지입니다.  
  
 **tempdb에 결과 정렬**  
 인덱스를 만드는 동안 생성된 중간 정렬 결과가 임시로 저장되는 위치를 결정하려면 `SORT_IN_TEMPDB` 옵션을 사용합니다. 정렬 작업이 필요하지 않거나 메모리에서 정렬을 수행할 수 있으면 `SORT_IN_TEMPDB`옵션이 무시됩니다.  
  
 **인덱스 패딩(Pad index)**  
 인덱스 패딩 지정  
  
 **인덱스를 온라인으로 유지**  
 사용자가 인덱스 작업을 수행하는 동안 기본 테이블이나 클러스터형 인덱스 데이터 및 연관된 모든 비클러스터형 인덱스에 액세스할 수 있는 `ONLINE` 옵션을 사용합니다.  
  
> [!NOTE]  
>  온라인 인덱스 작업은 일부 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 사용할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]버전에서 지원되는 기능 목록은 [SQL Server 2016 버전에서 지원하는 기능](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)을 참조하세요.  
  
 **인덱스 다시 작성 안 함 | 오프라인 인덱스 다시 작성**  
 온라인 상태인 동안 다시 작성할 수 없는 인덱스 유형에 대해 수행할 작업을 지정합니다.  
  
 **MAXDOP**  
 병렬 계획 실행에 사용되는 프로세서 수를 제한할 값을 지정합니다.  
  
 **낮은 우선 순위 사용**  
 낮은 우선 순위 잠금을 대기하려면 이 옵션을 선택합니다.  
  
 **대기 후 중단**  
 **최대 기간** 에 지정된 시간이 경과한 후에 수행할 작업을 지정합니다.  
  
 **최대 기간**  
 낮은 우선 순위 잠금을 대기할 시간을 지정합니다.  
  
 **T-SQL 보기**  
 선택한 옵션을 기반으로 서버에 대해 수행한 이 태스크의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 표시합니다.  
  
> [!NOTE]  
>  영향을 받은 개체 수가 많은 경우에는 표시하는 데 시간이 오래 걸릴 수 있습니다.  


[!INCLUDE[index-stats-options-reorg-5589131-2999104](../../includes/paragraph-content/index-stats-options-reorganize-maintenance-plan-include.md)]

  
## <a name="new-connection-dialog-box"></a>새 연결 대화 상자  
 **연결 이름**  
 새 연결의 이름을 입력합니다.  
  
 **서버 이름 선택 또는 입력**  
 이 태스크를 수행할 때 연결할 서버를 선택합니다.  
  
 **새로 고침**  
 사용할 수 있는 서버 목록을 새로 고칩니다.  
  
 **서버 로그온 정보 입력**  
 서버에 대한 인증 방법을 지정합니다.  
  
 **Windows NT 통합 보안 사용**  
 Windows 인증을 사용하여 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인스턴스에 연결합니다.  
  
 **특정 사용자 이름 및 암호 사용**  
 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 인증을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다. 이 옵션은 사용할 수 없습니다.  
  
 **사용자 이름**  
 인증 시 사용할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인을 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
 **암호**  
 인증 시 사용할 암호를 입력합니다. 이 옵션은 사용할 수 없습니다.  
  
## <a name="see-also"></a>참고 항목  
 [ALTER INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [DBCC DBREINDEX&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)   
 [CREATE INDEX&#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [인덱스에 대한 SORT_IN_TEMPDB 옵션](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md)   
 [온라인 인덱스 작업에 대한 지침](../../relational-databases/indexes/guidelines-for-online-index-operations.md)   
 [온라인 인덱스 작동 방식](../../relational-databases/indexes/how-online-index-operations-work.md)   
 [온라인으로 인덱스 작업 수행](../../relational-databases/indexes/perform-index-operations-online.md)  
  
  
