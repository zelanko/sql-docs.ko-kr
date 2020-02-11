---
title: 병합 아티클용 사용자 지정 충돌 해결 프로그램 구현 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 47d0f7c4eb6c78b9e551fafdc1e018a27604086e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721231"
---
# <a name="implement-a-custom-conflict-resolver-for-a-merge-article"></a>병합 아티클용 사용자 지정 충돌 해결 프로그램 구현
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]또는 COM 기반 사용자 지정 해결 프로그램[!INCLUDE[tsql](../../includes/tsql-md.md)][을 사용하여](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md) 의 병합 아티클을 위한 사용자 지정 충돌 해결 프로그램을 구현하는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **다음을 사용 하 여 병합 아티클에 대 한 사용자 지정 충돌 해결 프로그램을 구현 하려면**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [COM 기반 해결 프로그램](#COM)  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 각 게시자에서 사용자 지정 충돌 해결 프로그램을 [!INCLUDE[tsql](../../includes/tsql-md.md)] 저장 프로시저로 작성할 수 있습니다. 동기화하는 동안 해결 프로그램이 등록된 아티클에서 충돌이 발생하면 이 저장 프로시저가 호출되고 병합 에이전트가 충돌 행에 대한 정보를 프로시저의 필수 매개 변수에 전달합니다. 저장 프로시저 기반 사용자 지정 충돌 해결 프로그램은 항상 게시자에서 만들어집니다.  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 저장 프로시저 해결 프로그램은 행 변경 기반 충돌을 처리 하기 위해서만 호출 됩니다. PRIMARY KEY 위반 또는 고유 인덱스 제약 조건 위반으로 인한 삽입 실패와 같은 다른 충돌 유형을 처리하는 데 사용할 수 없습니다.  
  
#### <a name="to-create-a-stored-procedure-based-custom-conflict-resolver"></a>저장 프로시저 기반 사용자 지정 충돌 해결 프로그램을 만들려면  
  
1.  게시 또는 **msdb** 데이터베이스에 있는 게시자에서 다음 필수 매개 변수를 구현하는 새 시스템 저장 프로시저를 만듭니다.  
  
    |매개 변수|데이터 형식|Description|  
    |---------------|---------------|-----------------|  
    |**@tableowner**|`sysname`|충돌을 해결 중인 테이블의 소유자 이름. 게시 데이터베이스에 있는 테이블의 소유자입니다.|  
    |**@tablename**|`sysname`|충돌을 해결 중인 테이블의 이름|  
    |**@rowguid**|`uniqueidentifier`|충돌이 있는 행의 고유 식별자|  
    |**@subscriber**|`sysname`|충돌 변경 내용을 전파 중인 서버의 이름|  
    |**@subscriber_db**|`sysname`|충돌 변경 내용을 전파 중인 데이터베이스의 이름|  
    |**@log_conflict출력**|`int`|병합 프로세스에서 나중에 충돌을 해결할 수 있도록 충돌을 기록할지 여부를 나타냅니다.<br /><br /> **0** = 충돌을 기록 하지 않습니다.<br /><br /> **1** = 구독자가 충돌 내용.<br /><br /> **2** = 게시자가 충돌 내용.|  
    |**@conflict_message출력**|`nvarchar(512)`|충돌을 기록할 경우 해결 정보로 제공되는 메시지|  
    |**@destowner**|`sysname`|구독자에 있는 게시된 테이블의 소유자|  
  
     이 저장 프로시저는 병합 에이전트가 이 매개 변수에 전달한 값을 사용하여 사용자 지정 충돌 해결 논리를 구현합니다. 이 저장 프로시저는 기본 테이블과 구조가 같고 충돌 시 적용되는 행의 데이터 값을 포함하는 단일 행 결과 집합을 반환해야 합니다.  
  
2.  게시자에 연결할 때 구독자가 사용하는 모든 로그인에 저장 프로시저에 대한 EXECUTE 권한을 부여합니다.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>새 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  
  [
  ](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)
  ** 매개 변수에 MicrosoftSQL** **** Server Stored Procedure Resolver** 값, @article_resolver**** 매개 변수에 충돌 해결 프로그램 논리를 구현하는 저장 프로시저 이름을 지정하여 @resolver_infosp_addmergearticle**을 실행하고 아티클을 정의합니다. 자세한 내용은 [아티클을 정의](publish/define-an-article.md)을 참조하세요.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>기존 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  [Sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)를 실행 하 **@publication**고 **@article**,에 **@property** **article_resolver** 값을 지정 하 고,에 **MicrosoftSQL** **Server Stored ProcedureResolver** 값을 **@value**지정 합니다.  
  
2.  [Sp_changemergearticle](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)를 실행 하 **@publication**고 **@article**, **@property**에 **@value** **resolver_info** 값,에 충돌 해결 프로그램 논리를 구현 하는 저장 프로시저의 이름을 지정 합니다.  
  
##  <a name="COM"></a>COM 기반 사용자 지정 해결 프로그램 사용  
 
  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 네임스페이스는 이벤트를 처리하고 병합 복제 동기화 프로세스 중에 발생하는 충돌을 해결하는 복잡한 비즈니스 논리를 작성할 수 있게 해주는 인터페이스를 구현합니다. 자세한 내용은 [병합 아티클에 대 한 비즈니스 논리 처리기 구현](implement-a-business-logic-handler-for-a-merge-article.md)을 참조 하세요. 네이티브 코드 기반 사용자 지정 비즈니스 논리를 직접 작성하여 충돌을 해결할 수도 있습니다. 이 논리는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C++와 같은 제품을 사용하여 COM 구성 요소로 빌드되며 DLL(동적 연결 라이브러리)로 컴파일됩니다. 이러한 COM 기반 사용자 지정 충돌 해결 프로그램은 충돌 해결을 위해 특별히 설계 된 **ICustomResolver** 인터페이스를 구현 해야 합니다.  
  
#### <a name="to-create-and-register-a-com-based-custom-conflict-resolver"></a>COM 기반 사용자 지정 충돌 해결 프로그램을 만들고 등록하려면  
  
1.  COM 호환 제작 환경에서 사용자 지정 충돌 해결 프로그램 라이브러리에 대한 참조를 추가합니다.  
  
2.  Visual C++ 프로젝트의 경우 #import 지시어를 사용하여 이 라이브러리를 프로젝트로 가져옵니다.  
  
3.  
  **ICustomResolver** 인터페이스를 구현하는 클래스를 만듭니다.  
  
4.  특정 메서드와 속성을 구현합니다.  
  
5.  프로젝트를 빌드하여 사용자 지정 충돌 해결 프로그램 라이브러리 파일을 만듭니다.  
  
6.  병합 에이전트 실행 파일이 포함된 디렉터리에 라이브러리를 배포합니다(일반적으로 \Microsoft SQL Server\100\COM).  
  
    > [!NOTE]  
    >  사용자 지정 충돌 해결 프로그램은 끌어오기 구독의 경우 구독자에, 밀어넣기 구독의 경우 배포자에, 또는 웹 동기화에 사용되는 웹 서버에 배포해야 합니다.  
  
7.  배포 디렉터리에서 regsvr32.exe를 사용하여 다음과 같이 사용자 지정 충돌 해결 프로그램 라이브러리를 등록합니다.  
  
    ```  
    regsvr32.exe mycustomresolver.dll  
    ```  
  
8.  게시자에서 [sp_enumcustomresolvers&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql)를 실행하여 라이브러리가 이미 사용자 지정 충돌 해결 프로그램으로 등록되어 있지 않은지 확인합니다.  
  
9. 라이브러리를 사용자 지정 충돌 해결 프로그램으로 등록 하려면 배포자에서 [sp_registercustomresolver &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql)를 실행 합니다. 에 대 **@article_resolver**한 COM 개체의 이름,의 **@resolver_clsid**라이브러리 ID (CLSID) 및 `false` 에 **@is_dotnet_assembly**값을 지정 합니다.  
  
    > [!NOTE]  
    >  사용자 지정 충돌 해결 프로그램이 더 이상 필요하지 않으면 [sp_unregistercustomresolver&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql)를 사용하여 등록을 취소할 수 있습니다.  
  
10. 필요에 따라 클러스터에서 5-8 단계를 반복하여 클러스터의 모든 노드에 사용자 지정 해결 프로그램을 등록합니다. 장애 조치 이후에 사용자 지정 해결 프로그램에서 조정자를 올바르게 로드하려면 이 단계가 필요합니다.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-a-new-table-article"></a>새 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  게시자에서 [transact-sql&#41;&#40;sp_enumcustomresolvers](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) 을 실행 하 고 원하는 해결 프로그램의 이름을 확인 합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addmergearticle&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql)을 실행하여 아티클을 정의합니다. 에 **@article_resolver**1 단계의 아티클 해결 프로그램 이름을 지정 합니다. 자세한 내용은 [아티클을 정의](publish/define-an-article.md)을 참조하세요.  
  
#### <a name="to-use-a-custom-conflict-resolver-with-an-existing-table-article"></a>기존 테이블 아티클에 사용자 지정 충돌 해결 프로그램을 사용하려면  
  
1.  게시자에서 [transact-sql&#41;&#40;sp_enumcustomresolvers](/sql/relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql) 을 실행 하 고 원하는 해결 프로그램의 이름을 확인 합니다.  
  
2.  [Sp_changemergearticle &#40;transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql)를 실행 하 고, **@publication** **@article**에 **article_resolver** **@property**값,에 1 단계에서 가져온 아티클 해결 프로그램의 이름을 지정 **@value**합니다.  
  
#### <a name="viewing-a-sample-custom-resolver"></a>예제 사용자 지정 해결 프로그램 보기  
  
1.  예제는 SQL Server 2000 예제 파일에서 제공됩니다. [**Sql2000samples.cab**](https://github.com/Microsoft/sql-server-samples/blob/master/samples/tutorials/Miscellaneous/sql2000samples.zip)를 다운로드 합니다. 이렇게 하면 3 개의 파일이 6.9 MB로 다운로드 됩니다.  
  
2.  다운로드한 압축 .cab 파일에서 파일의 압축을 풉니다.  
  
3.  **Setup.exe를 실행 합니다.**  
  
    > [!NOTE]  
    >  설치 옵션을 선택할 때 **복제** 예제만 설치하면 됩니다. 기본 설치 경로는 **C:\Program files (x86) \Microsoft SQL Server 2000 Samples\1033\\**)입니다.  
  
4.  설치 폴더로 이동합니다. 기본 폴더는 **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\unzip_sqlreplSP3.exe**입니다.  
  
5.  
  **unzip_sqlreplSP3.exe** 프로그램을 실행합니다.  
  
    > [!NOTE]  
    >  샘플 컴퓨터 해결 프로그램은 (기본적으로) **C:\Program Files (x86)\Microsoft SQL Server 2000 Samples\1033\sqlrepl\resolver\subspres** 폴더에 설치됩니다.  
  
6.  
  **subspres** 폴더에서 모든 원본 파일에 발생한 **#include sqlres.h** 를 찾고 **#import "replrec.dll" no_namespace, raw_interfaces_only**로 바꿉니다.  
  
## <a name="see-also"></a>참고 항목  
 [Advanced Merge Replication Conflict Detection and Resolution](merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [COM 기반 사용자 지정 해결 프로그램](merge/advanced-merge-replication-conflict-com-based-custom-resolvers.md)   
 [복제 보안을 위한 최선의 구현 방법](security/replication-security-best-practices.md)  
  
  
