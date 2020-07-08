---
title: 사용자 지정 충돌 해결 프로그램 구현(병합)
description: SQL Server에서 병합 게시의 사용자 지정 충돌 해결 프로그램을 구현하는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
dev_langs:
- TSQL
helpviewer_keywords:
- merge replication conflict resolution [SQL Server replication], stored procedure-based resolvers
- articles [SQL Server replication], conflict resolution
- conflict resolution [SQL Server replication], merge replication
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8410ffdf38f8ae2d7dc5676debd13343c02c8f5a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85716824"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>병합 아티클용 사용자 지정 충돌 해결 프로그램 구현
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  이 항목에서는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [COM 기반 사용자 지정 해결 프로그램](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)을 사용하여 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 병합 아티클을 위한 사용자 지정 충돌 해결 프로그램을 구현하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **다음을 사용하는 병합 아티클용 사용자 지정 충돌 해결 프로그램 구현**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM 기반 해결 프로그램](#COM)  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Transact-SQL 사용  
 각 게시자에서 사용자 지정 충돌 해결 프로그램을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저로 작성할 수 있습니다. 동기화하는 동안 해결 프로그램이 등록된 아티클에서 충돌이 발생하면 이 저장 프로시저가 호출됩니다. 충돌 행에 대한 정보는 병합 에이전트에서 프로시저의 필수 매개 변수로 전달됩니다. 저장 프로시저 기반 사용자 지정 충돌 해결 프로그램은 항상 게시자에서 만들어집니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 해결 프로그램은 행 변경에 따른 충돌을 처리할 때만 호출됩니다. PRIMARY KEY 위반 또는 고유 인덱스 제약 조건 위반으로 인한 삽입 실패와 같은 다른 충돌 유형을 처리하는 데는 사용할 수 없습니다.
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>저장 프로시저 기반 사용자 지정 충돌 해결 프로그램을 만들려면  
  
1.  게시 또는 **msdb** 데이터베이스에 있는 게시자에서 다음 필수 매개 변수를 구현하는 새 시스템 저장 프로시저를 만듭니다.  
  
    |매개 변수|데이터 형식|Description|  
    |---------------|---------------|-----------------|  
    |**\@tableowner**|**sysname**|충돌을 해결 중인 테이블의 소유자 이름. 게시 데이터베이스에 있는 테이블의 소유자입니다.|  
    |**\@tablename**|**sysname**|충돌을 해결 중인 테이블의 이름|  
    |**\@rowguid**|**uniqueidentifier**|충돌이 있는 행의 고유 식별자입니다.|  
    |**\@subscriber**|**sysname**|충돌 변경 내용을 전파 중인 서버의 이름입니다.|  
    |**\@subscriber_db**|**sysname**|충돌 변경 내용을 전파 중인 데이터베이스의 이름입니다.|  
    |**\@log_conflict OUTPUT**|**int**|병합 프로세스에서 나중에 충돌을 해결할 수 있도록 충돌을 기록할지 여부를 설정합니다.<br /><br /> **0** = 충돌을 기록하지 않습니다.<br /><br /> **1** = 충돌 시 구독자의 변경 내용이 무시됩니다.<br /><br /> **2** = 충돌 시 게시자의 변경 내용이 무시됩니다.|  
    |**\@conflict_message OUTPUT**|**nvarchar(512)**|충돌을 기록할 경우 해결 정보로 제공되는 메시지|  
    |**\@destowner**|**sysname**|구독자에 있는 게시된 테이블의 소유자|  
  
     이 저장 프로시저는 병합 에이전트에서 이러한 매개 변수에 전달하는 값을 사용하여 사용자 지정 충돌 해결 논리를 구현합니다. 이 저장 프로시저는 기본 테이블과 구조가 동일하고 해당 행의 최우선 버전에 대한 데이터 값을 포함하는 단일 행 결과 집합을 반환해야 합니다.  
  
2.  게시자에 연결할 때 구독자가 사용하는 모든 로그인에 저장 프로시저에 대한 EXECUTE 권한을 부여합니다.  

#### <a name="use-a-custom-conflict-resolver-with-a-new-table-article"></a>새 테이블 아티클에 사용자 지정 충돌 해결 프로그램 사용  
  
1. [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 아티클을 정의합니다. 
1. **\@article_resolver** 매개 변수에 대해 **MicrosoftSQL** **Server 저장 프로시저 해결 프로그램** 값을 지정합니다. 
1. **\@resolver_info** 매개 변수에 대한 충돌 해결 프로그램 논리를 구현하는 저장 프로시저의 이름을 지정합니다. 

   자세한 내용은 [아티클 정의](../../relational-databases/replication/publish/define-an-article.md)를 참조하세요.
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>기존 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  **\@publication**, **\@article**을 지정하고 **\@property**에 **article_resolver** 값, **\@value**에 **MicrosoftSQL** **Server 저장 프로시저 해결 프로그램** 값을 지정하여 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다.  
  
2.  **\@publication** 및 **\@article**을 지정하고 **\@property**에 **resolver_info** 값, **\@value**에 충돌 해결 프로그램 논리를 구현하는 저장 프로시저 이름을 지정하여 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다.  
  
##  <a name="using-a-com-based-custom-resolver"></a><a name="COM"></a> COM 기반 사용자 지정 해결 프로그램 사용  
 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 네임스페이스는 이벤트를 처리하고 병합 복제 동기화 프로세스 중에 발생하는 충돌을 해결하는 복잡한 비즈니스 논리를 작성할 수 있게 해주는 인터페이스를 구현합니다. 자세한 내용은 [병합 아티클에 대한 비즈니스 논리 처리기 구현](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)을 참조하세요. 네이티브 코드 기반 사용자 지정 비즈니스 논리를 직접 작성하여 충돌을 해결할 수도 있습니다. 이 논리는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++와 같은 제품을 사용하여 COM 구성 요소로 빌드되며 DLL(동적 연결 라이브러리)로 컴파일됩니다. 이러한 종류의 COM 기반 사용자 지정 충돌 해결 프로그램은 충돌 해결을 위해 특별히 설계된 **ICustomResolver** 인터페이스를 구현해야 합니다.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>COM 기반 사용자 지정 충돌 해결 프로그램을 만들고 등록하려면  
  
1.  COM 호환 제작 환경에서 사용자 지정 충돌 해결 프로그램 라이브러리에 대한 참조를 추가합니다.  
  
2.  Visual C++ 프로젝트의 경우 #import 지시어를 사용하여 이 라이브러리를 프로젝트로 가져옵니다.  
  
3.  **ICustomResolver** 인터페이스를 구현하는 클래스를 만듭니다.  
  
4.  특정 메서드와 속성을 구현합니다.  
  
5.  프로젝트를 빌드하여 사용자 지정 충돌 해결 프로그램 라이브러리 파일을 만듭니다.  
  
6.  병합 에이전트 실행 파일이 포함된 디렉터리에 라이브러리를 배포합니다(일반적으로 \Microsoft SQL Server\100\COM).  
  
    > [!NOTE]  
    >  사용자 지정 충돌 해결 프로그램은 끌어오기 구독의 경우 구독자에, 밀어넣기 구독의 경우 배포자에, 또는 웹 동기화에 사용되는 웹 서버에 배포해야 합니다.  
  
7.  다음과 같이 배포 디렉터리에서 regsvr32.exe를 실행하여 사용자 지정 충돌 해결 프로그램 라이브러리를 등록합니다.  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)를 실행하여 라이브러리가 이미 사용자 지정 충돌 해결 프로그램으로 등록되어 있지 않은지 확인합니다.  
  
9. 라이브러리를 사용자 지정 충돌 해결 프로그램으로 등록하려면 배포자에서 [sp_registercustomresolver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)를 실행합니다. **\@article_resolver**에 COM 개체 식별 이름, **\@resolver_clsid**에 라이브러리의 ID(CLSID)를 지정하고 **\@is_dotnet_assembly**에 **false** 값을 지정합니다.  
  
    > [!NOTE]  
    >  사용자 지정 충돌 해결 프로그램이 더 이상 필요하지 않으면 [sp_unregistercustomresolver&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)을 사용하여 등록을 취소할 수 있습니다.  
  
10. 필요에 따라 클러스터에서 6-9단계를 반복하여 클러스터의 모든 노드에 사용자 지정 해결 프로그램을 등록합니다. 장애 조치(failover) 이후에 사용자 지정 해결 프로그램에서 조정자를 올바르게 로드하려면 이러한 단계가 필요합니다.
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>새 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)을 실행하고 원하는 해결 프로그램의 이름을 확인합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)을 실행하여 아티클을 정의합니다. **\@article_resolver**에 1단계의 아티클 해결 프로그램 식별 이름을 지정합니다. 자세한 내용은 [아티클 정의](../../relational-databases/replication/publish/define-an-article.md)를 참조하세요.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>기존 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md)을 실행하고 원하는 해결 프로그램의 이름을 확인합니다.  
  
2.  **\@publication**, **\@article**을 지정하고 **\@property**에 **article_resolver** 값, **\@value**에 1단계의 아티클 해결 프로그램 식별 이름을 지정하여 [sp_changemergearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)을 실행합니다.  
  

## <a name="see-also"></a>참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM 기반 사용자 지정 해결 프로그램](../../relational-databases/replication/merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  
