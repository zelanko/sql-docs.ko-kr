---
title: "병합 아티클용 사용자 지정 충돌 해결 프로그램 구현 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "병합 복제 충돌 해결 [SQL Server 복제], 저장 프로시저 기반 해결 프로그램"
  - "아티클 [SQL Server 복제], 충돌 해결"
  - "충돌 해결 [SQL Server 복제], 병합 복제"
ms.assetid: 76bd8524-ebc1-4d80-b5a2-4169944d6ac0
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 병합 아티클용 사용자 지정 충돌 해결 프로그램 구현
  이 항목의 병합 아티클 위한 사용자 지정 충돌 해결 프로그램을 구현 하는 방법에 설명 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 를 사용 하 여 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [COM 기반 사용자 지정 해결 프로그램](../../relational-databases/replication/merge/com-based-custom-resolvers.md)합니다.  
  
 **항목 내용**  
  
-   **다음을 사용하여 병합 아티클용 사용자 지정 충돌 해결 프로그램을 구현하려면**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM 기반 해결 프로그램](#COM)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 각 게시자에서 사용자 지정 충돌 해결 프로그램을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저로 작성할 수 있습니다. 동기화하는 동안 해결 프로그램이 등록된 아티클에서 충돌이 발생하면 이 저장 프로시저가 호출되고 병합 에이전트가 충돌 행에 대한 정보를 프로시저의 필수 매개 변수에 전달합니다. 저장 프로시저 기반 사용자 지정 충돌 해결 프로그램은 항상 게시자에서 만들어집니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장된 프로시저 해결 프로그램은 행 변경 기반 충돌을 처리할 때만 호출 됩니다. PRIMARY KEY 위반 또는 고유 인덱스 제약 조건 위반으로 인한 삽입 실패와 같은 다른 충돌 유형을 처리하는 데 사용할 수 없습니다.  
  
#### 저장 프로시저 기반 사용자 지정 충돌 해결 프로그램을 만들려면  
  
1.  게시 또는 **msdb** 데이터베이스에 있는 게시자에서 다음 필수 매개 변수를 구현하는 새 시스템 저장 프로시저를 만듭니다.  
  
    |매개 변수|데이터 형식|설명|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|**sysname**|충돌을 해결 중인 테이블의 소유자 이름. 게시 데이터베이스에 있는 테이블의 소유자입니다.|  
    |**@tablename**|**sysname**|충돌을 해결 중인 테이블의 이름|  
    |**@rowguid**|**uniqueidentifier**|충돌이 있는 행의 고유 식별자|  
    |**@subscriber**|**sysname**|충돌 변경 내용을 전파 중인 서버의 이름|  
    |**@subscriber_db**|**sysname**|충돌 변경 내용을 전파 중인 데이터베이스의 이름|  
    |**@log_conflict OUTPUT**|**int**|병합 프로세스에서 나중에 충돌을 해결할 수 있도록 충돌을 기록할지 여부를 나타냅니다.<br /><br /> **0** = 충돌을 기록 하지 않습니다.<br /><br /> **1** = 구독자는 무시 합니다.<br /><br /> **2** = 게시자는 무시 합니다.|  
    |**@conflict_message OUTPUT**|**nvarchar(512)**|충돌을 기록할 경우 해결 정보로 제공되는 메시지|  
    |**@destowner**|**sysname**|구독자에 있는 게시된 테이블의 소유자|  
  
     이 저장 프로시저는 병합 에이전트가 이 매개 변수에 전달한 값을 사용하여 사용자 지정 충돌 해결 논리를 구현합니다. 이 저장 프로시저는 기본 테이블과 구조가 같고 충돌 시 적용되는 행의 데이터 값을 포함하는 단일 행 결과 집합을 반환해야 합니다.  
  
2.  게시자에 연결할 때 구독자가 사용하는 모든 로그인에 저장 프로시저에 대한 EXECUTE 권한을 부여합니다.  
  
#### 새 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  실행 [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 값을 지정 하면 아티클을 정의 하려면 **MicrosoftSQL** **서버 저장 프로시저 해결 프로그램** 에 대 한는 **@article_resolver** 에 대 한 충돌 해결 프로그램 논리를 구현 하는 저장된 프로시저의 이름과 매개 변수는 **@resolver_info** 매개 변수입니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### 기존 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  실행 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), 로 지정 하 여 **@publication**, **@article**, 값이 **article_resolver** 에 대 한 **@property**, 및의 값 **MicrosoftSQL** **서버 저장 ProcedureResolver** 에 대 한 **@value**합니다.  
  
2.  실행 [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), 로 지정 하 여 **@publication**, **@article**, 값이 **resolver_info** 에 대 한 **@property**, 및에 대 한 충돌 해결 프로그램 논리를 구현 하는 저장된 프로시저의 이름을 **@value**합니다.  
  
##  <a name="COM"></a> COM 기반 사용자 지정 해결 프로그램 사용  
  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 네임 스페이스는 이벤트를 처리 하 고 병합 복제 동기화 프로세스 동안 발생 하는 충돌을 해결 하는 복잡 한 비즈니스 논리를 작성할 수 있게 해 주는 인터페이스를 구현 합니다. 자세한 내용은 [Implement a Business Logic Handler for a Merge Article](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)을 참조하세요. 네이티브 코드 기반 사용자 지정 비즈니스 논리를 직접 작성하여 충돌을 해결할 수도 있습니다. 이 논리는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++와 같은 제품을 사용하여 COM 구성 요소로 빌드되며 DLL(동적 연결 라이브러리)로 컴파일됩니다. 이러한 COM 기반 사용자 지정 충돌 해결 프로그램을 구현 해야는 **ICustomResolver** 충돌 해결을 위해 특별히 설계 된 인터페이스입니다.  
  
#### COM 기반 사용자 지정 충돌 해결 프로그램을 만들고 등록하려면  
  
1.  COM 호환 제작 환경에서 사용자 지정 충돌 해결 프로그램 라이브러리에 대한 참조를 추가합니다.  
  
2.  Visual C++ 프로젝트의 경우 #import 지시어를 사용하여 이 라이브러리를 프로젝트로 가져옵니다.  
  
3.  **ICustomResolver** 인터페이스를 구현하는 클래스를 만듭니다.  
  
4.  특정 메서드와 속성을 구현합니다.  
  
5.  프로젝트를 빌드하여 사용자 지정 충돌 해결 프로그램 라이브러리 파일을 만듭니다.  
  
6.  병합 에이전트 실행 파일이 포함된 디렉터리에 라이브러리를 배포합니다(일반적으로 \Microsoft SQL Server\100\COM).  
  
    > [!NOTE]  
    >  사용자 지정 충돌 해결 프로그램은 끌어오기 구독의 경우 구독자에, 밀어넣기 구독의 경우 배포자에, 또는 웹 동기화에 사용되는 웹 서버에 배포해야 합니다.  
  
7.  배포 디렉터리에서 regsvr32.exe를 사용하여 다음과 같이 사용자 지정 충돌 해결 프로그램 라이브러리를 등록합니다.  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  게시자에서 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 라이브러리는 사용자 지정 충돌 해결 프로그램으로 아직 등록 되지 않은 것을 확인 합니다.  
  
9. 라이브러리는 사용자 지정 충돌 해결 프로그램을 등록 하려면 실행 [sp_registercustomresolver (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), 배포자에 있습니다. 에 대 한 COM 개체의 이름을 지정 **@article_resolver**, 라이브러리의 ID (CLSID)에 대 한 **@resolver_clsid**, 및의 값 **false** 에 대 한 **@is_dotnet_assembly**합니다.  
  
    > [!NOTE]  
    >  사용자 지정 충돌 해결 프로그램을 사용 하 여 등록 수 더 이상 필요 [sp_unregistercustomresolver (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)합니다.  
  
10. 필요에 따라 클러스터에서 5-8 단계를 반복하여 클러스터의 모든 노드에 사용자 지정 해결 프로그램을 등록합니다. 장애 조치 이후에 사용자 지정 해결 프로그램에서 조정자를 올바르게 로드하려면 이 단계가 필요합니다.  
  
#### 새 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  게시자에서 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 고 원하는 해결 프로그램의 이름을 확인 합니다.  
  
2.  게시 데이터베이스의 게시자에서 실행 [sp_addmergearticle & #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 아티클을 정의 합니다. 1 단계의 아티클 해결 프로그램 이름을 지정 **@article_resolver**합니다. 자세한 내용은 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)을 참조하세요.  
  
#### 기존 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  게시자에서 실행 [sp_enumcustomresolvers (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 고 원하는 해결 프로그램의 이름을 확인 합니다.  
  
2.  실행 [sp_changemergearticle (& a) #40; TRANSACT-SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), 로 지정 하 여 **@publication**, **@article**, 값이 **article_resolver** 에 대 한 **@property**, 1 단계의 아티클 해결 프로그램의 이름 및 **@value**합니다.  
  
#### 예제 사용자 지정 해결 프로그램 보기  
  
1.  예제는 SQL Server 2000 예제 파일에서 제공됩니다. **SQL Server 2000 서비스 팩 3의 업데이트된 예제**[에서 sql2000samples.cab](http://www.microsoft.com/download/details.aspx?id=8560)을 다운로드하세요. 그러면 크기가 6.9MB에 이르는 8개 파일이 다운로드됩니다.  
  
2.  다운로드한 압축 .cab 파일에서 파일의 압축을 풉니다.  
  
3.   **setup.exe**를 실행합니다.  
  
    > [!NOTE]  
    >  설치 옵션을 선택할 때 **복제** 예제만 설치하면 됩니다. (기본 설치 경로 **C:\Program 파일 (x86) \Microsoft SQL Server 2000 Samples\1033\\**)  
  
4.  설치 폴더로 이동합니다. (기본 폴더는 **C:\Program 파일 (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**)  
  
5.  실행 된 **unzip_sqlreplSP3.exe** 프로그램입니다.  
  
    > [!NOTE]  
    >  샘플 com 해결 프로그램에 설치 합니다 (기본값)는 **C:\Program Files (x86) \Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** 폴더입니다.  
  
6.  에 **subspres** 폴더를 모두 찾습니다 **#include sqlres.h** 소스 파일의 모든으로 바꿉니다 **#import "replrec.dll" no_namespace, raw_interfaces_only**  
  
## 참고 항목  
 [고급 병합 복제 충돌 감지 및 해결](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM 기반 사용자 지정 해결 프로그램](../../relational-databases/replication/merge/com-based-custom-resolvers.md)   
 [복제 보안을 위한 최선의 구현 방법](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  