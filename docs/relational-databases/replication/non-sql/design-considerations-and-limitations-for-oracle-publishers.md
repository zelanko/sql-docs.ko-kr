---
title: Oracle 게시자에 대한 디자인 고려 사항 및 제한 사항 | Microsoft 문서
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Oracle publishing [SQL Server replication], design considerations and limitations
ms.assetid: 8d9dcc59-3de8-4d36-a61f-bc3ca96516b6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 8fbef18dc28786fc6455af68e09c788a3f0e2db1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47748751"
---
# <a name="design-considerations-and-limitations-for-oracle-publishers"></a>Oracle 게시자에 대한 디자인 고려 사항 및 제한 사항
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Oracle 데이터베이스에서의 게시 작업은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스에서의 게시 작업과 거의 동일합니다. 그러나 Oracle 데이터베이스에서의 게시 작업에 대한 다음과 같은 제한 사항 및 문제점을 알고 있어야 합니다.  
  
-   Oracle Gateway 옵션은 Oracle Complete 옵션을 사용할 때보다 더 나은 성능을 제공하지만 여러 트랜잭션 게시에서 동일한 테이블을 게시할 때는 사용할 수 없습니다. 트랜잭션 게시의 경우 특정 테이블이 한 번만 나타날 수 있지만 스냅숏 게시의 경우에는 이러한 제한이 없습니다. 여러 트랜잭션 게시에서 동일한 테이블을 게시해야 할 경우에는 Oracle Complete 옵션을 선택하십시오.  
  
-   복제에서 테이블, 인덱스 및 구체화된 뷰를 게시할 수 있습니다. 다른 개체는 복제되지 않습니다.  
  
-   Oracle 데이터베이스와 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 데이터베이스 간의 일부 데이터 스토리지 및 처리 방법 차이로 인해 복제가 영향을 받습니다.  
  
-   Oracle 게시자 사용 시 트랜잭션 복제 기능이 지원되는 방식이 매우 다릅니다.  
  
## <a name="support-for-publishing-objects-from-oracle"></a>Oracle 개체 게시 지원  
 다음은 복제에서 지원하는 Oracle 데이터베이스 개체입니다.  
  
-   테이블  
  
-   인덱스로 구성된 테이블  
  
-   인덱스  
  
-   구체화된 뷰(구체화된 뷰는 테이블로 복제됨)  
  
 다음 개체는 게시된 테이블에 표시할 수는 있지만 복제할 수는 없습니다.  
  
-   도메인 기반 인덱스  
  
-   함수 기반 인덱스  
  
-   기본값  
  
-   CHECK 제약 조건  
  
-   외래 키  
  
-   스토리지 옵션(예: 테이블스페이스, 클러스터 등)  
  
 다음 개체는 복제할 수 없습니다.  
  
-   중첩 테이블  
  
-   뷰  
  
-   패키지, 패키지 본문, 프로시저 및 트리거  
  
-   큐  
  
-   시퀀스  
  
-   동의어  
  
 지원되는 데이터 형식에 대한 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
## <a name="differences-between-oracle-and-sql-server"></a>Oracle과 SQL Server의 차이점  
  
-   Oracle에서는 일부 개체에 대한 최대 크기 제한이 서로 다릅니다. Oracle 게시 데이터베이스에서 생성된 모든 개체는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서의 해당 개체에 대한 최대 크기 제한을 따라야 합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]의 제한에 대한 자세한 내용은 [SQL Server의 최대 용량 사양](../../../sql-server/maximum-capacity-specifications-for-sql-server.md)을 참조하세요.  
  
-   기본적으로 Oracle 개체 이름은 대문자로 생성됩니다. Oracle 데이터베이스에서 Oracle 개체 이름이 대문자인 경우 이 개체를 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자를 통해 게시할 때 해당 이름을 대문자로 입력해야 합니다. 대/소문자를 올바르게 입력하지 않으면 개체를 찾을 수 없다는 오류 메시지가 나타납니다.  
  
-   Oracle의 SQL 언어는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]와 조금 다릅니다. 행 필터를 Oracle 호환 구문으로 작성해야 합니다.  
  
### <a name="considerations-for-large-objects"></a>큰 개체에 대한 고려 사항  
 LOB(큰 개체) 데이터는 아티클 로그 테이블에 저장되지 않으며 LOB 데이터의 업데이트 내용은 게시된 테이블에서 언제든지 검색할 수 있습니다. LOB에 영향을 주는 작업이 복제된 테이블의 복제 트리거를 발생시키는 경우에만 트랜잭션 게시에 업데이트가 복제됩니다. LOB을 포함하는 행이 삽입 또는 삭제되는 경우 Oracle 트리거가 발생되지만 LOB 열이 업데이트되는 경우에는 트리거가 발생되지 않습니다. 같은 행의 비-LOB 열이 같은 Oracle 트랜잭션에서도 업데이트되는 경우에만 LOB 열 업데이트를 즉시 복제합니다. 그렇지 않으면 같은 행에 있는 비-LOB 열에서 다음 업데이트가 발생할 경우 구독자에서 LOB 열을 새로 고칩니다. 이 동작을 애플리케이션에 사용할 수 있는지 확인합니다.  
  
 트랜잭션 게시에서 LOB 열 업데이트를 복제하려면 애플리케이션을 작성할 때 다음 전략 중 하나를 고려하십시오.  
  
-   트랜잭션 내에서 행을 업데이트하지 않고 행을 삭제 또는 다시 삽입합니다. 행을 다시 삽입할 때 새 LOB을 지정합니다. 삭제와 삽입 모두 트리거를 발생시키므로 행이 복제됩니다.  
  
-   행 업데이트에 LOB 열 외에 비-LOB 열을 포함시키거나 행의 비-LOB 열을 동일한 Oracle 트랜잭션의 일부로 업데이트합니다. 두 경우 모두 비-LOB 열을 업데이트하면 트리거가 발생됩니다.  
  
 LOB에 대한 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하십시오.  
  
### <a name="unique-indexes-and-constraints"></a>고유 인덱스 및 제약 조건  
 스냅숏과 트랜잭션 복제에서 고유 인덱스 및 UNIQUE 제약 조건(PRIMARY KEY 제약 조건 포함)에 포함된 열이 특정 제한 사항을 따라야 합니다. 이러한 제한 사항을 따르지 않으면 제약 조건이나 인덱스가 복제되지 않습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 의 인덱스에서 허용된 최대 열 수는 16입니다.  
  
-   UNIQUE 제약 조건에 포함된 모든 열에 지원되는 데이터 형식이 있어야 합니다. 데이터 형식에 대한 자세한 내용은 [Data Type Mapping for Oracle Publishers](../../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)을 참조하세요.  
  
-   UNIQUE 제약 조건에 포함된 모든 열이 게시되어야 합니다. 이러한 열은 필터링할 수 없습니다.  
  
-   UNIQUE 제약 조건이나 고유 인덱스에 포함된 열은 Null이 아니어야 합니다.  
  
 또한 다음 문제를 고려해야 합니다.  
  
-   Oracle 및 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 은 NULL을 다르게 처리합니다.Oracle은 NULL을 허용하고 UNIQUE 제약 조건 또는 고유 인덱스에 포함된 열에 대해 NULL 값을 갖는 행을 여러 개 허용합니다. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 는 동일한 열에 대해 NULL 값을 갖는 행을 하나만 허용하여 고유성을 갖도록 합니다. 게시된 테이블에 인덱스 또는 제약 조건에 포함된 열에 대해 NULL 값을 갖는 행이 여러 개 포함된 경우 구독자에서 제약 조건 위반이 발생하므로 NULL을 허용하는 UNIQUE 제약 조건이나 고유 인덱스를 게시할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 고유성을 테스트할 때 필드의 후행 공백을 무시하지만 Oracle에서는 무시하지 않습니다.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 트랜잭션 복제에서처럼 Oracle 트랜잭션 게시의 테이블에는 기본 키가 필요하며 기본 키는 위에 지정된 규칙에 따라 고유해야 합니다. 기본 키가 위의 글머리 기호로 요약된 규칙을 따르지 않을 경우 테이블을 트랜잭션 복제용으로 게시할 수 없습니다.  
  
## <a name="differences-between-oracle-publishing-and-standard-transactional-replication"></a>Oracle 게시와 표준 트랜잭션 복제의 차이점  
  
-   Oracle 게시자는 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 배포자 또는 동일한 배포자를 사용하는 모든 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 게시자 또는 게시를 받는 모든 구독자와 동일한 이름을 가질 수 없습니다. 같은 배포자가 서비스하는 게시의 경우 각 게시에 고유 이름이 있어야 합니다.  
  
-   Oracle 게시에 게시된 테이블은 복제된 데이터를 받을 수 없습니다. 따라서 Oracle 게시는 즉시 업데이트 구독 또는 지연 업데이트 구독을 사용하는 게시나 게시 테이블이 피어 투 피어 및 양방향 복제와 같은 구독 테이블로도 사용되는 토폴로지를 지원하지 않습니다.  
  
-   Oracle 데이터베이스에서 기본 키와 외래 키의 관계는 구독자에 복제되지 않습니다. 그러나 변경 내용이 배달될 때는 데이터에 관계가 유지됩니다.  
  
-   표준 트랜잭션 게시는 최대 1000개의 열로 구성된 테이블을 지원합니다. Oracle 트랜잭션 게시는 995개의 열을 지원하고 복제 시 게시된 각 테이블에 5개의 열이 추가됩니다.  
  
-   COLLATE 절은 기본 키와 UNIQUE 제약 조건에 중요한 대/소문자 비교를 사용할 수 있도록 CREATE TABLE 문에 추가됩니다. 이 동작은 [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)의 **@schema_option** 매개 변수로 지정하는 스키마 옵션 0x1000에 의해 제어됩니다.  
  
-   저장 프로시저를 사용하여 Oracle 게시자를 구성하거나 유지 관리하는 경우 프로시저를 명시적 트랜잭션 내에 두지 마십시오. 이 기능은 Oracle 게시자에 연결하는 데 사용된 연결된 서버에서는 지원되지 않습니다.  
  
-   마법사로 Oracle 게시에 대한 끌어오기 구독을 만드는 경우 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이상 버전에서 제공하는 새 구독 마법사를 사용해야 합니다. 그러나 이전 버전의 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]에서는 저장 프로시저 및 SQL-DMO 인터페이스를 사용하여 Oracle 게시에 대한 끌어오기 구독을 설정할 수 있습니다.  
  
-   저장 프로시저를 사용하여 변경 내용을 구독자(기본값)에게 전파할 경우 MCALL 구문은 지원되지만 Oracle 게시자의 게시에서 다르게 작동합니다. 일반적으로 MCALL은 게시자에서 업데이트된 열을 보여 주는 비트맵을 제공합니다. Oracle 게시에서의 비트맵은 항상 모든 열이 업데이트되었음을 보여 줍니다. 저장 프로시저 사용에 대한 자세한 내용은 [트랜잭션 아티클에 대한 변경 내용을 전파하는 방법 지정](../../../relational-databases/replication/transactional/transactional-articles-specify-how-changes-are-propagated.md)을 참조하세요.  
  
### <a name="transactional-replication-feature-support"></a>트랜잭션 복제 기능 지원  
  
-   SQL Server 게시에서 지원되는 스키마 옵션 중 일부는 Oracle 게시에서 지원되지 않습니다. 스키마 옵션에 대한 자세한 내용은 [sp_addarticle&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)을 참조하세요.  
  
-   Oracle 게시의 구독자는 즉시 업데이트 구독 또는 지연 업데이트 구독을 사용할 수 없거나 피어 투 피어 또는 양방향 토폴로지의 노드입니다.  
  
-   Oracle 게시의 구독자는 백업에서 자동으로 초기화할 수 없습니다.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 이진 유효성 검사와 행 개수 유효성 검사를 지원합니다. Oracle 게시자에서는 행 개수 유효성 검사를 지원합니다. 자세한 내용은 [복제된 데이터의 유효성 검사](../../../relational-databases/replication/validate-replicated-data.md)를 참조하세요.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 에서는 네이티브 bcp 모드 스냅숏과 문자 모드 스냅숏을 제공합니다. Oracle 게시자에서는 문자 모드 스냅숏을 지원합니다.  
  
-   게시된 Oracle 테이블의 스키마 변경은 지원되지 않습니다. 스키마를 변경하려면 먼저 게시를 삭제하고 스키마를 변경한 다음 게시 및 구독을 다시 만듭니다.  
  
    > [!NOTE]  
    >  게시된 테이블에서 어떠한 동작도 발생하지 않을 때 스키마가 변경된 후 게시 및 구독의 삭제와 다시 생성 작업이 한 번에 수행되는 경우에는 해당 구독에 대해 'replication support only' 옵션을 지정할 수 있습니다. 이렇게 하면 각 구독자에 스냅숏을 복사하지 않고도 구독을 동기화할 수 있습니다. 자세한 내용은 [스냅숏 없이 트랜잭션 구독 초기화](../../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)를 참조하세요.  
  
### <a name="replication-security-model"></a>복제 보안 모델  
 Oracle 게시의 보안 모델은 표준 트랜잭션 복제의 보안 모델과 동일합니다. 단 다음과 같은 경우는 예외입니다.  
  
-   배포자에서 게시자로 스냅숏 에이전트와 로그 판독기 에이전트를 연결하는 계정은 다음 중 한 가지 방법으로 지정됩니다.  
  
    -   [sp_adddistpublisher&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)의 **@security_mode** 매개 변수(Oracle 인증을 사용하는 경우 **@login** 및 **@password**에 대한 값도 지정)  
  
    -   **배포자에서 Oracle 게시자를 구성할 때 사용하는 SQL Server Management Studio의** 서버에 연결 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 대화 상자에서 지정합니다.  
  
     표준 트랜잭션 복제에서 계정은 [sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) 및 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)로 지정됩니다.  
  
-   스냅숏 에이전트와 로그 판독기 에이전트가 연결되는 계정은 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) 또는 속성 시트를 통해 변경할 수 없지만 암호는 변경할 수 있습니다.  
  
-   [sp_adddistpublisher&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)의 **@security_mode** 매개 변수 값을 1(Windows 통합 인증)로 지정하는 경우  
  
    -   스냅숏 에이전트와 로그 판독기 에이전트에 사용된 프로세스 계정 및 암호([sp_addpublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md) 및 [sp_addlogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)의 **@job_login** 및 **@job_password** 매개 변수)는 Oracle 게시자에 연결하는 데 사용된 계정 및 암호와 같아야 합니다.  
  
    -   [sp_changepublication_snapshot&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md) 또는 [sp_changelogreader_agent&#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md)에서 **@job_login** 매개 변수는 변경할 수 없지만 암호는 변경할 수 있습니다.  
  
 복제 보안에 대한 자세한 내용은 [보안 및 보호&#40;복제&#41;](../../../relational-databases/replication/security/security-and-protection-replication.md)를 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Oracle 게시자에 대한 관리 고려 사항](../../../relational-databases/replication/non-sql/administrative-considerations-for-oracle-publishers.md)   
 [Oracle 게시자 구성](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)   
 [Oracle 게시 개요](../../../relational-databases/replication/non-sql/oracle-publishing-overview.md)  
  
  
