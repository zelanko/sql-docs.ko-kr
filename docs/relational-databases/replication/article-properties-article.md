---
title: 아티클 속성 - &lt;Article&gt; | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql13.rep.newpubwizard.articleproperties.f1
helpviewer_keywords:
- Article Properties dialog box
ms.assetid: 6dd601a4-1233-43d9-a9f0-bc8d84e5d188
caps.latest.revision: 38
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: acee0f4698c9a1c6d26bd042f1413257df528828
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="article-properties---ltarticlegt"></a>아티클 속성 - &lt;Article&gt;
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  **아티클 속성** 대화 상자는 새 게시 마법사 및 **게시 속성** 대화 상자에서 사용할 수 있습니다. 이 대화 상자를 사용하여 모든 아티클 유형에 대한 속성을 보고 설정할 수 있습니다. 게시가 생성된 경우에만 설정할 수 있거나 게시에 활성 구독이 없는 경우에만 설정할 수 있는 속성이 있습니다. 설정할 수 없는 속성은 읽기 전용으로 표시됩니다.  
  
> [!NOTE]  
>  게시가 생성되면 일부 속성 변경으로 인해 새 스냅숏이 필요합니다. 게시에 구독이 있는 경우에는 이러한 변경 내용으로 인해 모든 구독도 다시 초기화해야 합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
 **아티클 속성** 대화 상자의 각 속성에는 설명이 포함되어 있습니다. 속성을 클릭하면 대화 상자 아래쪽에 해당 설명이 표시됩니다. 이 항목에서는 여러 가지 속성에 대한 추가 정보를 제공합니다. 속성은 다음 범주로 그룹화됩니다.  
  
-   모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시에 적용되는 속성  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 트랜잭션 게시에 적용되는 속성  
  
-   병합 게시에 적용되는 속성  
  
-   Oracle 게시자의 트랜잭션 게시 및 스냅숏 게시에 적용되는 속성  
  
## <a name="options-for-all-publications"></a>모든 게시에 대한 옵션  
 **테이블 파티션 구성표 복사** 및 **인덱스 파티션 구성표 복사**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서는 복제에서 행 필터 및 열 필터를 통해 제공하는 분할과는 관계없는 테이블 파티션 및 인덱스 파티션이 도입되었습니다. **테이블 파티션 구성표 복사** 및 **인덱스 파티션 구성표 복사** 옵션은 파티션 구성표를 구독자에 복사해야 하는지 여부를 지정합니다. 분할에 대한 자세한 내용은 [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md)를 참조하십시오.  
  
 **데이터 형식 변환**  
 구독자에서 개체 생성 시 사용자 정의 데이터 형식에서 기본 데이터 형식으로 변환할지 여부를 결정합니다. 사용자 정의 데이터 형식에는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서 도입된 사용자 정의 CLR 유형이 포함됩니다. 이러한 데이터 형식을 이전 버전의 **로 복제하려면 값을** True [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 지정합니다. 이렇게 하면 구독자에서 해당 데이터 형식을 올바르게 처리할 수 있습니다.  
  
 **구독자에서 스키마 만들기**  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 에서는 CREATE SCHEMA 문을 사용하여 정의되는 스키마가 도입되었습니다. 스키마는 개체의 소유자로 \<Database>.\<Schema>.\<Object>와 같이 여러 부분으로 구성된 이름에 사용됩니다. DBO 이외의 스키마가 소유하고 있는 데이터베이스에 개체가 있는 경우 복제 시 구독자에서 이러한 스키마를 만들 수 있으므로 게시된 개체를 만들 수 있습니다.  
  
 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]로 복제하려면 다음을 수행하십시오.  
  
-   이전 버전에서는 CREATE SCHEMA 문을 지원하지 않으므로 이 옵션을 **False**로 설정합니다.  
  
-   각 스키마에 대해 해당 스키마와 이름이 같은 구독 데이터베이스에 사용자를 추가합니다.  
  
 **XML을 NTEXT로 변환**, **MAX 데이터 형식을 NTEXT 및 IMAGE로 변환**, **새 datetime을 NVARCHAR로 변환**, **filestream을 MAX 데이터 형식으로 변환**, **large CLR을 MAX 데이터 형식으로 변환**, **hierarchyId를 MAX 데이터 형식으로 변환**및 **spatial을 MAX 데이터 형식으로 변환**  
 설명한 대로 데이터 형식과 특성을 변환할지 여부를 결정합니다. 이러한 데이터 형식을 이전 버전의 **로 복제하려면** True [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 지정합니다. 이렇게 하면 해당 데이터 형식이 구독자에서 올바르게 처리됩니다.  
  
 **대상 개체 이름**  
 구독 데이터베이스에서 생성되는 개체의 이름입니다. 피어 투 피어 트랜잭션 복제가 설정된 게시의 아티클에 대해서는 이 옵션을 변경할 수 없습니다.  
  
 **대상 개체 소유자**  
 구독 데이터베이스에서 개체가 생성되는 스키마입니다. 기본값은 게시 데이터베이스에서 개체가 속한 스키마입니다. 그러나 다음 경우는 예외입니다.  
  
-   호환성 수준이 90 이하인 병합 게시의 아티클에 대해 기본적으로 소유자는 빈 상태였다가 구독자에서 개체를 생성하는 중에 **dbo** 로 지정됩니다.  
  
-   Oracle 게시의 아티클에 대해 기본적으로 소유자는 **dbo**로 지정됩니다.  
  
-   문자 모드 스냅숏([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이외 구독자 및 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 구독자에 사용됨)을 사용하는 게시의 아티클에 대해 기본적으로 소유자는 빈 상태입니다. 소유자는 기본적으로 배포 에이전트 또는 병합 에이전트를 구독자에 연결하는 데 사용하는 계정과 연결된 소유자입니다.  
  
 피어 투 피어 트랜잭션 복제가 설정된 게시의 아티클에 대해서는 이 옵션을 변경할 수 없습니다.  
  
 **자동으로 ID 범위 관리**  
 기본적으로 복제는 게시자와 각 구독자에서 모든 ID 열을 관리합니다. 지정된 값을 한 노드에서만 사용하도록 각 복제 노드에 ID 값의 범위( **게시자 범위 크기** 및 **구독자 범위 크기** 옵션으로 지정)가 할당됩니다. 자세한 내용은 [ID 열 복제](../../relational-databases/replication/publish/replicate-identity-columns.md)를 참조하세요.  
  
## <a name="options-for-transactional-publications"></a>트랜잭션 게시에 대한 옵션  
 **INSERT, UPDATE 및 DELETE 저장 프로시저 복사**  
 이 대화 상자의 **문 배달** 섹션에서 저장 프로시저를 사용하여 변경 내용을 구독자(기본값)로 전파하도록 선택한 경우 해당 프로시저를 각 구독자에 복사할지 여부를 선택합니다. **False**를 선택할 경우 수동으로 프로시저를 복사해야 하며, 수동으로 복사하지 않을 경우 배포 에이전트에서 변경 내용을 배달하려고 하면 오류가 발생합니다.  
  
 **Statement delivery**  
 이 섹션의 옵션은 테이블로 복제된 인덱싱된 뷰를 포함하여 모든 테이블에 적용됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 응용 프로그램에 다른 기능이 필요 하지 않는 한 기본 옵션을 사용할 것을 권장합니다. 기본적으로 트랜잭션 복제는 각 구독자에 설치된 저장 프로시저 집합를 통하여 변경 내용을 구독자로 전파합니다. 게시자에서 테이블에 삽입, 업데이트 또는 삭제 작업을 수행하면 구독자에서 저장 프로시저 호출로 변환됩니다.  
  
 **문 배달** 옵션은 저장 프로시저 사용 여부를 지정하며, 사용할 경우 이 형식이 해당 프로시저로 전달되는 매개 변수에 사용됩니다. **저장 프로시저** 옵션을 사용하여 복제에서 자동으로 만든 프로시저 또는 사용자가 만든 대체 사용자 지정 프로시저를 사용할 수 있습니다.  
  
 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
 **복제**  
 이 옵션은 저장 프로시저에만 적용됩니다. 저장 프로시저의 정의(CREATE PROCEDURE 문)를 복제할 것인지 아니면 저장 프로시저의 실행을 복제할 것인지를 결정합니다. 저장 프로시저의 실행을 복제하면 구독이 초기화될 때 프로시저 정의가 구독자로 복제됩니다. 게시자에서 이 프로시저를 실행하면 이러한 복제의 결과로 구독자에서 해당 프로시저가 실행됩니다. 이렇게 하면 대규모 일괄 처리 작업이 수행되는 경우 성능을 크게 향상시킬 수 있습니다. 자세한 내용은 [Publishing Stored Procedure Execution in Transactional Replication](../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)을 참조하세요.  
  
## <a name="options-for-merge-publications"></a>병합 게시에 대한 옵션  
 병합 게시의 **아티클 속성** 대화 상자에는 **속성** 및 **해결 프로그램**탭이 있습니다.  
  
### <a name="properties-tab"></a>속성 탭  
 **동기화 방향**  
 클라이언트 구독 유형을 사용하는 구독자에서 변경 내용을 업로드할 수 있는지 여부를 결정합니다.  
  
-   **양방향** (기본값): 변경 내용을 구독자로 다운로드하고 게시자로 업로드할 수 있습니다.  
  
-   **구독자로 다운로드 전용, 구독자 변경 금지**: 변경 내용을 구독자로 다운로드할 수 있지만 게시자로 업로드할 수는 없습니다. 트리거는 구독자에서 변경 작업을 수행하지 못하게 합니다.  
  
-   **구독자로 다운로드 전용, 구독자 변경 허용**: 변경 내용을 구독자로 다운로드할 수 있지만 게시자로 업로드할 수는 없습니다.  
  
 자세한 내용은 [다운로드 전용 아티클로 병합 복제 성능 최적화](../../relational-databases/replication/merge/optimize-merge-replication-performance-with-download-only-articles.md)를 참조하세요.  
  
 **파티션 옵션**  
 매개 변수가 있는 필터에서 만드는 파티션 유형을 지정합니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)의 "'partition options' 설정" 섹션을 참조하십시오.  
  
 **추적 수준**  
 같은 행 또는 같은 열의 변경을 충돌로 처리할지 여부를 결정합니다.  
  
 **INSERT 권한 확인**, **UPDATE 권한 확인**및 **DELETE 권한 확인**  
 동기화 중 구독자 로그인이 게시 데이터베이스에 게시된 테이블에 대해 INSERT, UPDATE 또는 DELETE 권한을 가지고 있는지를 확인할 것인지 결정합니다. 병합 복제에서는 이러한 권한을 부여할 필요가 없으므로 기본값은 **False** 입니다. 게시된 테이블에 대한 액세스는 PAL(게시 액세스 목록)을 통해 제어합니다. PAL에 대한 자세한 내용은 [게시자 보안 설정](../../relational-databases/replication/security/secure-the-publisher.md)을 참조하세요.  
  
 사용 권한을 확인하면 하나 이상의 구독자가 일부 변경 내용을 게시된 데이터에 업로드할 수는 있지만 다른 작업은 수행하지 못하게 할 수 있습니다. 예를 들어 PAL에 구독자를 추가하지만 추가된 구독자에게 게시 데이터베이스의 테이블에 대한 권한은 부여하지 않을 수 있습니다. 그런 다음 DELETE 권한 확인을 **True**로 설정하면 구독자는 삽입 및 업데이트는 업로드할 수 있지만 삭제는 업로드할 수 없습니다.  
  
 **여러 열 UPDATE**  
 병합 복제는 업데이트 수행 시 하나의 UPDATE 문으로 변경된 모든 열을 업데이트하고 변경되지 않은 열은 원래 값으로 다시 설정합니다. 이러한 경우 변경된 각 열에 UPDATE 문을 하나씩 사용하여 여러 UPDATE 문을 실행해도 됩니다. 일반적으로 여러 열 UPDATE 문이 보다 효율적입니다. 그러나 테이블의 트리거가 특정 열의 업데이트에 응답하도록 설정되어 있는데 업데이트를 수행할 때마다 이러한 열이 다시 설정되어 이 트리거가 올바르게 응답하지 않는 경우에는 이 옵션을 **False** 로 설정해야 합니다.  
  
> [!IMPORTANT]  
>  이 옵션은 더 이상 사용되지 않으며 후속 릴리스에서 제거될 예정입니다.  
  
### <a name="resolver-tab"></a>해결 프로그램 탭  
 **기본 해결 프로그램 사용**  
 기본 해결 프로그램을 선택한 경우 사용된 구독 유형에 따라 각 구독자에 할당된 우선 순위나 게시자에 기록된 첫 번째 변경 내용을 기준으로 충돌을 해결합니다. 자세한 내용은 [병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-resolve-merge-replication-conflicts.md)을 참조하세요.  
  
 **사용자 지정 해결 프로그램 사용(배포자에 등록됨)**  
 아티클 해결 프로그램( [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서 제공하는 해결 프로그램 또는 사용자가 작성한 해결 프로그램) 사용을 선택한 경우 목록 상자에서 해결 프로그램을 선택해야 합니다. 자세한 내용은 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)을 참조하세요.  
  
 해결 프로그램에 입력이 필요한 경우 **해결 프로그램에 필요한 정보 입력** 입력란에 필요한 입력을 지정합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 사용자 지정 해결 프로그램에 필요한 입력에 대한 자세한 내용은 [Microsoft COM 기반 해결 프로그램](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-resolvers.md)을 참조하세요.  
  
 **요청 시 동기화 작업 중 구독자가 대화형으로 충돌 해결**  
 대화형으로 충돌을 해결하고 구독자가 요청 시 동기화(병합 복제의 기본값)를 사용하게 하려면 이 옵션을 선택합니다. 새 구독 마법사의 **동기화 일정** 페이지에서 요청 시 동기화를 지정합니다. 충돌을 대화형으로 해결하려면 대화형 해결 프로그램 사용자 인터페이스를 사용합니다. 자세한 내용은 [Interactive Conflict Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-interactive-resolution.md)을 참조하세요.  
  
 **병합 전 디지털 서명 확인 필요**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 에서 제공하는 모든 COM 기반 해결 프로그램이 서명됩니다. 동기화할 때 해결 프로그램이 유효한지 확인하려면 이 옵션을 선택합니다.  
  
## <a name="options-for-oracle-publications"></a>Oracle 게시에 대한 옵션  
 Oracle 게시의 **아티클 속성** 대화 상자에는 **속성** 및 **데이터 매핑**탭이 있습니다. Oracle 게시는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시에서 지원하는 속성 중 일부만 지원합니다. 자세한 내용은 [Design Considerations and Limitations for Oracle Publishers](../../relational-databases/replication/non-sql/design-considerations-and-limitations-for-oracle-publishers.md)을 참조하세요.  
  
### <a name="properties-tab"></a>속성 탭  
 **INSERT, UPDATE 및 DELETE 저장 프로시저 복사**  
 아티클이 트랜잭션 게시에 있고 이 대화 상자의 **문 배달** 섹션에서 저장 프로시저를 사용하여 변경 내용을 구독자(기본값)로 전파하기로 선택한 경우 해당 프로시저를 각 구독자에 복사할지 여부를 선택합니다. **False**를 선택할 경우 수동으로 프로시저를 복사해야 하며, 수동으로 복사하지 않을 경우 배포 에이전트에서 변경 내용을 배달하려고 하면 오류가 발생합니다.  
  
 **대상 개체 소유자**  
 **dbo**이외의 값을 입력한 경우  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 실행하는 구독자의 경우 입력한 값과 이름이 같은 구독자에서 스키마가 생성되었는지 확인해야 합니다. 자세한 내용은 [CREATE SCHEMA&#40;Transact-SQL&#41;](../../t-sql/statements/create-schema-transact-sql.md)를 참조하세요.  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]이전 버전을 실행하는 구독자의 경우 각 스키마에 대해 해당 스키마와 이름이 같은 구독 데이터베이스에 사용자를 추가합니다.  
  
 **테이블스페이스 이름**  
 Oracle 서버 인스턴스에서 복제 변경 추적 테이블을 만들 테이블스페이스입니다. 자세한 내용은 [Oracle 테이블스페이스 관리](../../relational-databases/replication/non-sql/manage-oracle-tablespaces.md)를 참조하세요.  
  
 **Statement delivery**  
 이 섹션의 옵션은 트랜잭션 게시의 모든 테이블에 적용됩니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 응용 프로그램에 다른 기능이 필요 하지 않는 한 기본 옵션을 사용할 것을 권장합니다. 기본적으로 트랜잭션 복제는 각 구독자에 설치된 저장 프로시저 집합를 통하여 변경 내용을 구독자로 전파합니다. 게시자에서 테이블에 삽입, 업데이트 또는 삭제 작업을 수행하면 구독자에서 저장 프로시저 호출로 변환됩니다.  
  
 **문 배달** 옵션은 저장 프로시저 사용 여부를 지정하며, 사용할 경우 이 형식이 해당 프로시저로 전달되는 매개 변수에 사용됩니다. **저장 프로시저** 옵션을 사용하여 복제에서 자동으로 만든 프로시저 또는 사용자가 만든 대체 사용자 지정 프로시저를 사용할 수 있습니다.  
  
 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
### <a name="data-mapping-tab"></a>데이터 매핑 탭  
 **열 이름**  
 게시자의 열 이름입니다(읽기 전용).  
  
 **게시자 데이터 형식**  
 게시자의 열에 대한 Oracle 데이터 형식입니다(읽기 전용). 데이터 형식은 Oracle 데이터베이스에서 직접 변경해야 합니다. 자세한 내용은 Oracle 설명서를 참조하십시오.  
  
 **구독자 데이터 형식**  
 데이터가 복제될 때 Oracle 데이터 형식이 매핑되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 형식입니다.  
  
-   하나의 매핑만 사용할 수 있는 데이터 형식의 경우 속성 표의 열이 읽기 전용입니다.  
  
-   일부 형식의 경우 두 개 이상의 매핑을 선택할 수 있습니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] 는 응용 프로그램에 다른 매핑이 필요 하지 않는 한 기본 매핑을 사용할 것을 권장합니다. 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [초기 스냅숏 만들기 및 적용](../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)   
 [구독 다시 초기화](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  
