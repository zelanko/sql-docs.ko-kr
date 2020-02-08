---
title: 게시 속성 - 대화 상자
description: SSMS(SQL Server Management Studio) ‘게시 속성’ 대화 상자에 있는 페이지를 설명합니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.agentsecurity.f1
- sql13.rep.newpubwizard.pubproperties.filterrows.f1
- sql13.rep.newpubwizard.pubproperties.internetsynchronization.f1
- sql13.rep.newpubwizard.pubproperties.general.f1
- sql13.rep.newpubwizard.pubproperties.publicationaccesslist.f1
- sql13.rep.newpubwizard.pubproperties.snapshotformat.f1
helpviewer_keywords:
- Publication Properties dialog box
ms.assetid: 66e845e9-1308-4288-9110-ad2f22f1fc58
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c4d1c2c09c764e1e5102e520ccb2f6152e57ce7c
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76286585"
---
# <a name="sql-server-replication-publication-properties--dialog-box"></a>SQL Server 복제 '게시 속성' 대화 상자
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

이 페이지에서는 게시 속성 대화 상자 내에 있는 페이지를 설명합니다. 

## <a name="general"></a>일반
 **게시 속성** 대화 상자의 **일반** 페이지에는 이름, 설명 및 구독 만료 정책을 포함하여 게시에 대한 기본 정보가 들어 있습니다.  
  
### <a name="options"></a>옵션  
 **이름**  
 게시의 이름입니다(읽기 전용).  
  
 **Database**  
 게시 데이터베이스의 이름입니다(읽기 전용).  
  
 **설명**  
 게시에 대한 설명입니다.  
  
 **형식**  
 게시의 유형입니다(읽기 전용).  
  
 **구독 만료**  
 구독 만료에 대한 옵션 중 하나를 선택합니다. 명시적 기간(**간격**)이 있는 **구독이 만료되지 않음** 또는 **구독이 만료됨**.  
  
 스냅샷 및 트랜잭션 게시의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 은 기본값인 **구독이 만료되지는 않지만 다시 초기화될 때까지 비활성화될 수 있습니다**를 사용하는 것을 권장합니다.  
  
 병합 게시의 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 은 기본값인 **구독이 다음 시간 내에 동기화되지 않으면 만료되어 삭제될 수 있습니다** 를 사용하고 **간격**에 가능한 낮은 값을 설정하는 것을 권장합니다. 구독 만료 기간이 증가할수록 저장된 메타데이터의 양도 증가하므로 성능에 영향을 줄 수 있습니다. 연결을 끊거나 대량의 메타데이터를 저장 및 처리하는 잠재적 성능 문제에 대해 연장된 기간 동안 동기화하지 않는 간단한 방법으로 구독자 간에 균형을 유지합니다.  
  
 자세한 내용은 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)을(를) 참조하세요.  
  
 **호환성 수준**  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전과 병합 게시에만 해당됩니다. 이 게시와 동기화하는 구독자에 필요한 가장 낮은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전을 선택합니다. 호환성 수준 결정과 관련된 여러 가지 규칙이 있습니다.  

## <a name="filter-rows"></a>행 필터
  **게시 속성** 대화 상자의 **행 필터** 페이지를 사용하여 추가, 편집 또는 삭제할 수 있습니다.  
  
-   스냅샷, 트랜잭션 및 병합 게시의 테이블 아티클에 정적 행 필터를 적용합니다.   
-   병합 게시의 테이블 아티클에 매개 변수가 있는 행 필터를 적용합니다.    
-   조인 필터를 사용하여 병합 테이블 아티클의 필터를 관련 테이블 아티클로 확장할 수 있습니다. 필터링 옵션에 대한 자세한 내용은 [게시된 데이터 필터링](../../relational-databases/replication/publish/filter-published-data.md)을 참조하세요.  
  
> [!NOTE]  
>  필터를 추가, 편집 또는 삭제하려면 게시에 대한 새 스냅샷이 필요하며 모든 구독을 다시 초기화해야 합니다.  
  
애플리케이션 성능을 최대화하고 필요한 원격 스토리지를 줄이거나 특정 구독자가 사용할 수 있는 데이터를 제한하려면 필요한 데이터만 게시해야 합니다. 게시에는 필터링되지 않은 테이블과 필터링된 테이블이 모두 포함될 수 있습니다. 예를 들어 필터링되지 않은 전체 회사 제품 테이블을 포함할 수도 있고 행 필터를 사용하여 특정 영역으로 필터링된 고객 테이블을 제공할 수 있습니다. 게시된 데이터를 필터링하여 다음 작업을 수행할 수 있습니다.  
  
-   네트워크로 보내지는 데이터 양을 최소화합니다.    
-   구독자에 필요한 스토리지 공간을 줄입니다.    
-   개별 구독자 요구 사항에 기초하여 게시 및 애플리케이션을 사용자 지정합니다.    
-   서로 다른 구독자에 서로 다른 데이터 파티션을 보낼 수 있으므로 구독자가 데이터를 업데이트할 때 충돌을 방지하거나 충돌 횟수를 줄일 수 있습니다. 즉, 두 개의 구독자가 같은 데이터 값을 업데이트하지 않게 됩니다.    
-   중요한 데이터를 전송하지 못하게 할 수 있습니다. 행 필터와 열 필터를 사용하여 구독자의 데이터 액세스를 제한할 수 있습니다. 병합 복제에서 HOST_NAME()을 포함하는 매개 변수가 있는 필터를 사용할 경우 보안 고려 사항이 있습니다. 자세한 내용은 [Parameterized Row Filters](../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)의 "HOST_NAME()으로 필터링" 섹션을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **필터링된 테이블**  
 이 창은 게시의 테이블 아티클에 필터를 추가하면 추가된 필터로 채워집니다. 행 필터가 있는 테이블은 창에서 최상위 노드로 표시됩니다. 병합 게시의 경우 조인 필터를 통해 필터링이 확장된 테이블은 자식 노드로 표시됩니다.  
  
 **추가**  
 **추가** 를 클릭하면 테이블 아티클을 필터링할 수 있는 대화 상자가 시작됩니다. 스냅샷 또는 트랜잭션 게시에 대해 **추가** 를 클릭하면 대화 상자가 바로 시작됩니다. 병합 게시에 대해 **추가**를 클릭하면 **필터 추가**, **선택한 필터 확장을 위해 조인 추가**, **자동으로 필터 생성**의 세 가지 선택 사항이 표시됩니다.  
  
-   **필터 추가** 를 선택하면 **필터 추가** 대화 상자가 시작됩니다. 이 대화 상자를 사용하여 테이블 아티클에 행 필터를 적용할 수 있습니다. 예를 들어 **필터 추가** 대화 상자에서 고객 데이터가 들어 있는 테이블을 구독자로 복제할 때 프랑스 고객의 데이터만 포함되도록 지정할 수 있습니다.  
  
-   **선택한 필터 확장을 위해 조인 추가** 를 선택하면 **조인 추가** 대화 상자가 시작됩니다. **조인 추가** 대화 상자를 사용하여 행 필터가 있는 테이블과 관련된 테이블의 데이터를 필터링하도록 행 필터를 확장할 수 있습니다. 예를 들어 프랑스 고객의 데이터만 포함하도록 고객 테이블을 필터링하고 고객 주문과 관련된 테이블이 있으면 주문 테이블에 프랑스 고객의 주문만 포함되도록 두 테이블 간 조인을 정의할 수 있습니다.  
  
    > [!NOTE]  
    >  이 옵션을 사용하려면 먼저 필터 창에서 조인의 기본 테이블을 선택해야 합니다.  
  
-   **자동으로 필터 생성** 을 선택하면 **필터 생성** 대화 상자가 시작됩니다. 이 대화 상자를 사용하여 외래 키 관계를 통해 관련된 다른 테이블로 복제가 자동으로 확장되는 병합 게시의 한 테이블에 행 필터를 정의할 수 있습니다. 예를 들어 게시에 고객 테이블, 고객 테이블에 대한 외래 키가 있는 주문 테이블, 주문 테이블에 대한 외래 키가 있는 주문 세부 정보 테이블 등 3개의 테이블이 있을 수 있습니다. 고객 테이블에 행 필터를 정의하면 복제가 해당 필터를 다른 테이블로 확장합니다.  
  
    > [!NOTE]  
    >  복제 시 필터가 자동으로 생성되면 게시의 기존 필터는 모두 삭제됩니다. 자동으로 생성된 필터와 수동으로 지정한 필터를 모두 포함하려면 먼저 필터를 생성합니다. 각 게시에 대해 자동으로 생성된 필터 집합을 하나만 지정할 수 있습니다.  
  
 **편집**  
 필터 창에서 행 필터 또는 조인 필터를 선택하고 **편집** 을 클릭하면 **필터 편집** 또는 **조인 편집** 대화 상자가 시작됩니다.  
  
 **Delete**  
 필터 창에서 행 필터 또는 조인 필터를 선택하고 **삭제** 를 클릭하면 필터가 삭제됩니다.  
  
 **테이블 찾기**  
 병합 게시에만 사용할 수 있습니다. **테이블 찾기** 를 클릭하여 복잡한 필터 트리에서 테이블을 찾을 수 있습니다. 관계가 복잡하게 설정된 데이터베이스에서는 한 테이블이 여러 테이블에 조인될 수 있으므로 필터 트리에서 두 개 이상의 위치에 표시될 수 있습니다.  
  
 실제 테이블은 트리의 한 위치에만 표시되고 나머지 위치에서는 바로 가기로 표시됩니다. 테이블 바로 가기는 테이블에 대한 참조일 뿐이므로 해당 테이블의 자식 노드는 표시되지 않습니다. 바로 가기 노드는 바로 가기 화살표로 표시되며 해당 노드를 확장하면 **\<tablename>에 대한 테이블을 보려면 [테이블 찾기]를 클릭하십시오.** 라는 텍스트가 표시됩니다.  
  
 창에서 바로 가기 노드를 선택하고 **테이블 찾기** 를 클릭하면 창이 확장되고 테이블이 강조 표시됩니다. 바로 가기 노드를 선택하지 않고 **테이블 찾기** 를 클릭하면 **테이블 찾기** 대화 상자가 시작됩니다.  
  
 **Filter**  
 필터 창에서 선택한 필터의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 정의를 포함합니다.  

## <a name="publication-access-list"></a>게시 액세스 목록
  **게시 속성** 대화 상자의 **게시 액세스 목록** 페이지를 사용하여 PAL(게시 액세스 목록)에서 로그인, 계정 및 그룹을 추가 및 제거할 수 있습니다. PAL은 게시자의 보안을 유지하는 기본 메커니즘입니다. 게시를 만들면 복제에서 게시에 대한 PAL을 만듭니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 액세스 제어 목록과 기능이 비슷한 PAL에는 게시에 대한 액세스가 부여된 로그인, 계정 및 그룹이 있습니다.  
  
 구독자가 게시자 또는 배포자에 연결하여 게시에 대한 액세스를 요청하면 구독자의 로그인을 PAL의 인증 정보와 비교합니다. 이 방법은 클라이언트 도구가 게시자에서 직접 수정 작업을 수행하는 데 게시자 및 배포자 로그인을 사용하지 못하도록 하여 게시자에 대한 보안을 강화합니다. 자세한 내용은 [게시자 보안 설정](../../relational-databases/replication/security/secure-the-publisher.md)을 참조하세요.  
  
### <a name="options"></a>옵션  
 **추가**  
 새 항목을 목록에 추가합니다. 게시자 및 배포자에서 이미 정의한 로그인, 계정 또는 그룹 이름만 추가할 수 있습니다. 두 서버 모두에서 도메인 계정이 사용되거나 로컬 계정이 생성되면 로그인, 계정 또는 그룹 이름이 두 서버에 정의됩니다.  
  
 **제거**  
 선택한 항목을 목록에서 제거합니다.  
  
 **모두 제거**  
 목록에서 항목을 모두 제거합니다.  

## <a name="ftp-snapshot-and-internet"></a>FTP 스냅샷 및 인터넷

-   FTP(파일 전송 프로토콜)를 통해 스냅샷을 배달하는 속성을 설정합니다. 자세한 내용은 [FTP를 통해 스냅샷 배달](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)을 참조하세요. FTP를 사용하여 스냅샷을 배달하려면 FTP 서버를 설정해야 합니다. 자세한 내용은 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 설명서를 참조하십시오.  
  
    > [!NOTE]  
    >  FTP 설정을 변경하면 새 스냅샷을 생성해야 합니다.  
  
-   HTTPS(Secure Hypertext Transfer Protocol)를 통해 구독을 동기화하도록 허용하는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전의 병합 복제에 대한 웹 동기화 속성을 설정합니다. 웹 동기화를 사용하려면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 서버를 구성해야 합니다. 자세한 내용은 [Web Synchronization for Merge Replication](../../relational-databases/replication/web-synchronization-for-merge-replication.md)를 참조하세요.  
  
### <a name="options"></a>옵션  
 **FTP를 통해 스냅샷 파일 액세스**  
 **구독자가 FTP(파일 전송 프로토콜)를 사용하여 스냅샷 파일을 다운로드하도록 허용**을 선택하고 **FTP 서버 이름**, **포트 번호**, **FTP 루트 폴더에서의 경로**, **로그인**및 **암호**를 지정하여 구독자가 스냅샷 배달에 FTP를 사용할 수 있도록 허용합니다.  
  
 이 옵션을 사용하면 구독자는 FTP를 사용하여 스냅샷 파일을 검색할 수 있지만 반드시 그럴 필요는 없습니다. 이 옵션을 선택하면 새 구독 마법사는 구독자가 FTP를 통해 스냅샷 파일을 검색하는 것을 기본값으로 설정합니다. 설정을 변경하려면 **구독 속성** 대화 상자를 사용합니다. 구독자가 FTP를 통해 스냅샷 파일에 액세스할 수 있도록 허용하는 경우 **게시 속성** 대화 상자의 **스냅샷** 페이지에서 FTP 폴더를 스냅샷 파일의 위치로 지정합니다. 이렇게 하면 새 스냅샷이 생성될 때 스냅샷 에이전트가 FTP 폴더의 파일을 자동으로 업데이트합니다. 위치가 FTP 폴더로 설정되어 있지 않으면 새 스냅샷을 생성할 때 파일을 수동으로 업데이트해야 합니다. 자세한 내용은 [FTP를 통해 스냅샷 배달](../../relational-databases/replication/publish/deliver-a-snapshot-through-ftp.md)을 참조하세요.  
  
 **웹 동기화**  
 병합 복제에 대해서만 사용할 수 있습니다. **구독자가 웹 서버에 연결하여 동기화하도록 허용**을 선택하고 병합 구독자가 웹 동기화를 사용할 수 있는 웹 서버 주소를 지정합니다. 웹 서버는 SSL(Secure Sockets Layer)을 사용해야 하고 웹 주소는 `https://server.domain.com/synchronize`와 같이 정규화된 주소여야 합니다. 자세한 내용은 [Configure Web Synchronization](../../relational-databases/replication/configure-web-synchronization.md)을 참조하세요.  


## <a name="agent-security"></a>에이전트 보안
  **게시 속성** 대화 상자의 **에이전트 보안** 페이지를 사용하여 다음 에이전트를 실행하고 복제 토폴로지의 컴퓨터에 연결할 때 사용되는 계정의 설정에 액세스할 수 있습니다.  
  
-   모든 게시에 대한 스냅샷 에이전트입니다.  
  
-   모든 트랜잭션 게시에 대한 로그 판독기 에이전트입니다. 트랜잭션 복제에 대해 게시된 각 데이터베이스에 하나의 로그 판독기 에이전트가 있습니다. 로그 판독기 에이전트 설정을 변경하면 데이터베이스의 모든 트랜잭션 게시에 영향을 줍니다.  
  
-   지연 업데이트 구독을 허용하는 트랜잭션 게시에 대한 큐 판독기 에이전트 각 배포 데이터베이스에 대해 하나의 큐 판독기 에이전트가 있습니다. 큐 판독기 에이전트 설정을 변경하면 같은 배포 데이터베이스를 사용하는 지연 업데이트 구독이 있는 모든 트랜잭션 게시에 영향을 줍니다. 큐 판독기 에이전트 보안 설정에 대한 자세한 내용은 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)을 참조하세요.  
  
 각 에이전트에 필요한 보안 설정 및 사용 권한에 대한 자세한 내용은 [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md)을 참조하십시오.  
  
### <a name="options"></a>옵션  
 **보안 설정** 또는 **에이전트 만들기**  
 에이전트 작업이 생성된 경우 **보안 설정** 을 클릭하여 에이전트 보안 설정을 변경할 수 있는 대화 상자에 액세스합니다. 에이전트 작업이 생성되지 않은 경우 **에이전트 만들기** 를 클릭하여 새 에이전트를 만들고 보안 설정을 지정합니다.  

## <a name="data-partitions"></a>데이터 파티션
데이터 파티션  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  **게시 속성** 대화 상자의 **데이터 파티션** 페이지를 사용하여 매개 변수가 있는 필터링을 사용하는 병합 게시를 위한 데이터 파티션을 정의할 수 있습니다. 파티션을 정의하고 나면 이들 파티션에 대한 스냅샷을 생성하여 구독자의 연결 속성(로그인 및/또는 컴퓨터 이름)을 기준으로 다양한 구독자에 대한 각기 다른 초기 데이터 집합을 제공할 수 있습니다. 또한 구독자가 처음 동기화할 때 파티션에 사용할 수 있는 스냅샷을 가지고 있지 않은 경우 스냅샷 배달 및 생성을 요청할 수 있도록 선택할 수 있습니다. 자세한 내용은 [매개 변수가 있는 필터로 병합 게시에 대한 스냅샷 만들기](../../relational-databases/replication/create-a-snapshot-for-a-merge-publication-with-parameterized-filters.md)을 참조하세요.  
  
### <a name="options"></a>옵션  
 **추가**  
 파티션을 정의하려면 **추가** 를 클릭합니다. **데이터 파티션 추가** 대화 상자에서 **HOST_NAME()** 및/또는 **SUSER_SNAME()** 에 대한 값을 지정하고 스냅샷을 새로 고칠 일정을 정의합니다.  
  
 **편집**  
 표에서 기존 파티션을 선택하고 **편집** 을 클릭하여 파티션을 편집합니다.  
  
 **Delete**  
 표에서 기존 파티션을 선택하고 **삭제** 를 클릭하여 파티션을 삭제합니다.  
  
 **선택한 스냅샷 지금 생성**  
 표에서 하나 이상의 파티션을 선택하고 **선택한 스냅샷 지금 생성** 을 클릭하여 이러한 파티션에 대한 스냅샷을 생성합니다.  
  
 **기존 스냅샷 정리**  
 표에서 하나 이상의 파티션을 선택하고 **기존 스냅샷 정리** 를 클릭하여 이러한 파티션에 대한 스냅샷을 정리합니다.  
  
 **새 구독자가 동기화할 때 필요한 경우 자동으로 파티션 정의 및 스냅샷 생성**  
 구독자가 스냅샷 생성 및 적용을 요청할 수 있도록 할 경우 이 옵션을 선택합니다. 구독자가 처음 동기화할 때 파티션에 사용할 수 있는 스냅샷을 가지고 있지 않은 경우 이 옵션이 필요할 수 있습니다.  

## <a name="snapshot"></a>스냅샷
스냅샷  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]  
  **게시 속성** 대화 상자의 **스냅샷** 페이지를 사용하여 스냅샷 형식, 스냅샷 폴더 위치 및 스냅샷 적용 전후 실행할 스크립트를 설정할 수 있습니다. 스냅샷 폴더를 공유로 지정해야 하며 파일을 읽고 폴더에 쓰는 에이전트에 대한 충분한 권한이 있어야 합니다. 폴더의 적절한 보안 유지 방법에 대한 자세한 내용은 [스냅샷 폴더 보안 설정](../../relational-databases/replication/security/secure-the-snapshot-folder.md)을 참조하세요.  
  
> [!NOTE]  
>  게시 속성을 변경하려면 게시에 대한 새 스냅샷이 필요합니다. 자세한 내용은 [게시 및 아티클 속성 변경](../../relational-databases/replication/publish/change-publication-and-article-properties.md)을 참조하세요.  
  
### <a name="options"></a>옵션  
 **스냅샷 형식**  
 스냅샷 형식에 대해 네이티브 모드 또는 문자 모드를 선택합니다.  
  
-   모든 구독자가 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssEW](../../includes/ssew-md.md)] 이외의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스인 경우 **네이티브 SQL Server - 모든 구독자는 SQL Server를 실행하는 서버여야 합니다.** 를 선택합니다. 네이티브 스냅샷 형식을 사용할 때 최상의 성능을 제공합니다.    
-   구독자가 **에서 실행되고 있거나** 이외 구독자인 경우 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 문자 - 게시자 또는 구독자가 SQL Server를 실행하지 않는 경우 필요합니다[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 선택합니다.    
 **스냅샷 파일 위치**  
 스냅샷 파일을 저장할 위치를 선택합니다. 파일을 기본 위치에 저장할 수 있으며 기본 위치 대신 대체 위치에 저장할 수도 있습니다. 대체 위치에 저장된 파일을 압축할 수 있습니다.  
  
-   게시자에 대해 기본 스냅샷 폴더를 사용하려면 **기본 폴더에 파일 보관** 을 선택합니다. 스냅샷 폴더 위치는 **배포자 속성** 대화 상자에서 게시자에 대해서만 변경할 수 있으므로 이 대화 상자에서는 읽기 전용입니다. 자세한 내용은 [스냅샷 속성 수정](../../relational-databases/replication/snapshot-options.md)을 참조하세요.    
-   기본 위치 대신 대체 위치를 지정하려면 **다음 폴더에 파일 보관** 을 선택합니다. 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하고 위치를 탐색합니다. 대체 스냅샷 위치의 파일을 압축하려면 **이 폴더에 있는 스냅샷 파일 압축** 을 선택합니다. 대체 위치는 다른 서버, 네트워크 드라이브 또는 이동식 미디어(CD-ROM 또는 이동식 디스크 등)가 될 수 있습니다. 자세한 내용은 [스냅샷 속성 수정](../../relational-databases/replication/snapshot-options.md)을 참조하세요.  
  
 **추가 스크립트 실행**  
 구독자에 스냅샷 적용 전후에 실행할 스크립트를 지정합니다. **스냅샷 형식** 이 **문자**인 경우에는 스크립트를 지정할 수 없습니다.  
  
 스크립트는 선택 사항이지만 명령을 실행하고 구독자에 관리 변경 내용을 적용하는 편리한 방법을 제공합니다. 스크립트 실행에 대한 자세한 내용은 [스냅샷 적용 전후에 스크립트 실행](../../relational-databases/replication/snapshot-options.md#execute-scripts-before-and-after-snapshot-is-applied)을 참조하세요.  
  
-   **스냅샷 적용 전 다음 스크립트 실행** 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하여 스크립트의 위치를 지정합니다.    
-   **스냅샷 적용 후 다음 스크립트 실행** 입력란에 경로를 입력하거나 **찾아보기** 를 클릭하여 스크립트의 위치를 지정합니다. 
  
## <a name="see-also"></a>참고 항목  
 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)   
 [게시 속성 보기 및 수정](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [데이터 및 데이터베이스 개체 게시](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   

  
  
