---
title: FTP를 통해 스냅숏 배달 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- snapshots [SQL Server replication], FTP snapshots
- FTP snapshots [SQL Server replication]
- snapshot replication [SQL Server], FTP
ms.assetid: 99872c4f-40ce-4405-8fd4-44052d3bd827
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d1a8989492c9efb670b00bda00dbfa757c549fca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62960067"
---
# <a name="deliver-a-snapshot-through-ftp"></a>FTP를 통해 스냅숏 배달
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 을 사용하여 [!INCLUDE[tsql](../../../includes/tsql-md.md)]에서 FTP를 통해 스냅숏을 배달하는 방법에 대해 설명합니다.  
  
##  <a name="Restrictions"></a> 제한 사항  
  
-   스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\ftpserver\home\snapshots과 같이 UNC(Universal Naming Convention) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](../security/secure-the-snapshot-folder.md)을 참조하세요.  
  
###  <a name="Prerequisites"></a> 필수 구성 요소  
  
-   FTP(파일 전송 프로토콜)를 사용하여 스냅숏 파일을 전송하려면 먼저 FTP 서버를 구성해야 합니다. 자세한 내용은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 인터넷 정보 서비스(IIS) 설명서를 참조하세요.  
  
###  <a name="Security"></a> 보안  
 인터넷을 통해 FTP 스냅숏 배달을 사용하는 경우에는 보안 향상을 위해 VPN(가상 프라이빗 네트워크)을 구현하는 것이 좋습니다. 자세한 내용은 [VPN을 사용하여 인터넷을 통해 데이터 게시](../publish-data-over-the-internet-using-vpn.md)를 참조하세요.  
  
 FTP 서버에 익명 로그인을 허용하지 않는 것이 가장 좋은 보안 방법입니다. 스냅숏 에이전트는 지정한 디렉터리에 대해 쓰기 권한이 있어야 하며 배포 에이전트 또는 병합 에이전트는 읽기 권한이 있어야 합니다. 끌어오기 구독을 사용하는 경우 공유 디렉터리를 \\\ftpserver\home\snapshots과 같이 UNC(Universal Naming Convention) 경로로 지정해야 합니다. 자세한 내용은 [스냅숏 폴더 보안 설정](../security/secure-the-snapshot-folder.md)을 참조하세요.  
  
 가능한 경우 런타임에 사용자에게 자격 증명을 입력하라는 메시지를 표시합니다. 스크립트 파일에 자격 증명을 저장하는 경우에는 이 파일에 보안을 설정해야 합니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
 FTP 서버를 구성한 후 **게시 속성 \<게시>** 대화 상자에서 이 서버에 대한 디렉터리 및 보안 정보를 지정합니다. 이 대화 상자에 액세스하는 방법은 [View and Modify Publication Properties](view-and-modify-publication-properties.md)을 참조하세요.  
  
#### <a name="to-specify-ftp-information"></a>FTP 정보를 지정하려면  
  
1.  **게시 속성 - \<게시>** 대화 상자의 다음 두 페이지 중 하나에서 **구독자가 FTP(파일 전송 프로토콜)를 사용하여 스냅숏 파일을 다운로드하도록 허용**을 선택합니다.   
    -   **FTP 스냅숏** 페이지 - [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]이전 버전을 실행하는 구독자에 대한 병합 게시와 스냅숏 및 트랜잭션 게시의 경우    
    -   **FTP 스냅숏 및 인터넷** 페이지 - [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 이후 버전을 실행하는 게시자의 병합 게시의 경우    
2.  **FTP 서버 이름**, **포트 번호**, **FTP 루트 폴더에서의 경로**, **로그인**및 **암호**에 대한 값을 지정합니다.    
     예를 들어 FTP 서버 루트가 \\\ftpserver\home이고 스냅숏을 \\\ftpserver\home\snapshots에 저장하려면 **FTP 루트 폴더에서의 경로** 속성에 대해 \snapshots\ftp를 지정합니다. 복제는 스냅숏 파일을 만들 때 스냅숏 폴더 경로에 'ftp'를 추가합니다.    
3.  스냅숏 에이전트가 스냅숏 파일을 2단계에서 지정한 디렉터리에 쓰도록 지정합니다. 예를 들어 스냅숏 에이전트가 스냅숏 파일을 \\\ftpserver\home\snapshots\ftp에 쓰도록 하려면 다음 두 위치 중 하나에 \\\ftpserver\home\snapshots 경로를 지정해야 합니다.    
    -   이 게시와 연결된 배포자의 기본 스냅숏 위치    
         기본 스냅숏 위치를 지정 하는 방법에 대 한 자세한 내용은 참조 하세요. [기본 스냅숏 위치 지정](../snapshot-options.md#snapshot-folder-locations)합니다.    
    -   이 게시의 대체 스냅숏 폴더 위치. 대체 위치는 스냅숏이 압축된 경우에 필요합니다.    
         **게시 속성 - \<게시>** 대화 상자의 스냅숏 페이지에 있는 **다음 폴더에 파일 보관** 텍스트 상자에 경로를 입력합니다.   
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
 FTP 서버에서 스냅숏 파일을 사용할 수 있게 해주는 옵션을 설정할 수 있으며, 이러한 FTP 설정은 복제 저장 프로시저를 사용하여 프로그래밍 방식으로 수정할 수 있습니다. 사용되는 절차는 게시 유형에 따라 달라집니다. FTP 스냅숏 배달은 끌어오기 구독에만 사용됩니다.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 FTP 스냅숏 배달을 설정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql)을 실행합니다. 지정할 **@publication** 를 값 `true` 에 대 한 **@enabled_for_internet** , 적절 한 다음 매개 변수 값:    
    -   **@ftp_address** - 스냅숏을 배달하는 데 사용되는 FTP 서버의 주소입니다.    
    -   (옵션) **@ftp_port** - FTP 서버에서 사용되는 포트입니다.    
    -   (옵션) **@ftp_subdirectory** - FTP 로그온에 할당된 기본 FTP 디렉터리의 하위 디렉터리입니다. 예를 들어 FTP 서버 루트가 \\\ftpserver\home이고 스냅숏을 \\\ftpserver\home\snapshots에 저장하려면 **@ftp_subdirectory** 에 **\snapshots\ftp**를 지정합니다. 복제는 스냅숏 파일을 만들 때 스냅숏 폴더 경로에 'ftp'를 추가합니다.    
    -   (옵션) **@ftp_login** - FTP 서버에 연결할 때 사용되는 로그인 계정입니다.    
    -   (옵션) **@ftp_password** - FTP 로그인에 대한 암호입니다.  
  
     이렇게 하면 FTP를 사용하는 게시가 만들어집니다. 자세한 내용은 [Create a Publication](create-a-publication.md)를 참조하세요.  
  
#### <a name="to-enable-ftp-snapshot-delivery-for-a-merge-publication"></a>병합 게시에 대한 FTP 스냅숏 배달을 설정하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_addmergepublication](/sql/relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql)을 실행합니다. 지정할 **@publication** 에 값 `true` 에 대 한 **@enabled_for_internet** 적절 한 다음 매개 변수 값:  
  
    -   **@ftp_address** - 스냅숏을 배달하는 데 사용되는 FTP 서버의 주소입니다.    
    -   (옵션) **@ftp_port** - FTP 서버에서 사용되는 포트입니다.    
    -   (옵션) **@ftp_subdirectory** - FTP 로그온에 할당된 기본 FTP 디렉터리의 하위 디렉터리입니다. 예를 들어 FTP 서버 루트가 \\\ftpserver\home이고 스냅숏을 \\\ftpserver\home\snapshots에 저장하려면 **@ftp_subdirectory** 에 **\snapshots\ftp**를 지정합니다. 복제는 스냅숏 파일을 만들 때 스냅숏 폴더 경로에 'ftp'를 추가합니다.    
    -   (옵션) **@ftp_login** - FTP 서버에 연결할 때 사용되는 로그인 계정입니다.    
    -   (옵션) **@ftp_password** - FTP 로그인에 대한 암호입니다.  
  
     이렇게 하면 FTP를 사용하는 게시가 만들어집니다. 자세한 내용은 [Create a Publication](create-a-publication.md)를 참조하세요.  
  
#### <a name="to-create-a-pull-subscription-to-a-snapshot-or-transactional-publication-that-uses-ftp-snapshot-delivery"></a>FTP 스냅숏 배달을 사용하는 스냅숏 또는 트랜잭션 게시에 대한 끌어오기 구독을 만들려면  
  
1.  구독 데이터베이스의 구독자에서 [sp_addpullsubscription](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-transact-sql)을 실행합니다. 이때 **@publisher** 및 **@publication** 에서 사용 가능합니다.  
  
    -   구독 데이터베이스의 구독자에서 [sp_addpullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)를 실행합니다. 지정 **@publisher** , **@publisher_db** 를 **@publication** , [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 는 Windows 자격 증명에서 배포 에이전트는 구독자에 대 한 실행 **@job_login** 하 고 **@job_password** 에 값 `true` 에 대 한 **@use_ftp** 합니다.  
  
2.  게시 데이터베이스의 게시자에서 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql) 을 실행하여 끌어오기 구독을 등록합니다. 자세한 내용은 [끌어오기 구독 만들기](../create-a-pull-subscription.md)를 참조하세요.  
  
#### <a name="to-create-a-pull-subscription-to-a-merge-publication-that-uses-ftp-snapshot-delivery"></a>FTP 스냅숏 배달을 사용하는 병합 게시에 대한 끌어오기 구독을 만들려면  
  
1.  구독 데이터베이스의 구독자에서 [sp_addmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-transact-sql)을 실행합니다. 이때 **@publisher** 및 **@publication** 에서 사용 가능합니다.   
2.  구독 데이터베이스의 구독자에서 [sp_addmergepullsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)를 실행합니다. 지정할 **@publisher** 를 **@publisher_db** 를 **@publication** , 구독자에서 배포 에이전트가 실행 되는 Windows 자격 증명 **@job_login** 하 고 **@job_password** 에 값 `true` 에 대 한 **@use_ftp** 합니다.    
3.  게시 데이터베이스의 게시자에서 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql) 을 실행하여 끌어오기 구독을 등록합니다. 자세한 내용은 [끌어오기 구독 만들기](../create-a-pull-subscription.md)를 참조하세요.  
  
#### <a name="to-change-one-or-more-ftp-snapshot-delivery-settings-for-a-snapshot-or-transactional-publication"></a>스냅숏 또는 트랜잭션 게시에 대한 하나 이상의 FTP 스냅숏 배달 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)을 실행합니다. **@property** 에 다음 중 한 가지 값을 지정하고, 이 설정의 새 값을 **@value** 에 지정합니다.    
    -   `ftp_address` - 스냅숏을 배달하는 데 사용되는 FTP 서버의 주소입니다.    
    -   `ftp_port` - FTP 서버에서 사용되는 포트입니다.    
    -   `ftp_subdirectory` - FTP 스냅숏에 사용되는 기본 FTP 디렉터리의 하위 디렉터리입니다.    
    -   `ftp_login` - FTP 서버에 연결하는 데 사용되는 로그인입니다.    
    -   `ftp_password` - FTP 로그인에 대한 암호입니다.  
  
2.  (옵션) 변경되는 각 FTP 설정에 대해 1단계를 반복합니다.    
3.  (옵션) FTP 스냅숏 배달을 해제하려면 게시 데이터베이스의 게시자에서 [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql) 을 실행합니다. 값을 지정 `enabled_for_internet` 에 대 한 **@property** 값 `false` 에 대 한 **@value** 합니다.  
  
#### <a name="to-change-ftp-snapshot-delivery-settings-for-a-merge-publication"></a>병합 게시에 대한 FTP 스냅숏 배달 설정을 변경하려면  
  
1.  게시 데이터베이스의 게시자에서 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)을 실행합니다. **@property** 에 다음 중 한 가지 값을 지정하고, 이 설정의 새 값을 **@value** 에 지정합니다.  
  
    -   `ftp_address` - 스냅숏을 배달하는 데 사용되는 FTP 서버의 주소입니다.    
    -   `ftp_port` - FTP 서버에서 사용되는 포트입니다.    
    -   `ftp_subdirectory` - FTP 스냅숏에 사용되는 기본 FTP 디렉터리의 하위 디렉터리입니다.   
    -   `ftp_login` - FTP 서버에 연결하는 데 사용되는 로그인입니다.    
    -   `ftp_password` - FTP 로그인에 대한 암호입니다.    
2.  (옵션) 변경되는 각 FTP 설정에 대해 1단계를 반복합니다.    
3.  (옵션) FTP 스냅숏 배달을 해제하려면 게시 데이터베이스의 게시자에서 [sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql) 을 실행합니다. 값을 지정 `enabled_for_internet` 에 대 한 **@property** 값 `false` 에 대 한 **@value** 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 다음 예에서는 구독자가 FTP를 사용하여 스냅숏 데이터에 액세스할 수 있는 병합 게시를 만듭니다. 구독자는 FTP 공유에 액세스할 때 보안 VPN 연결을 사용해야 합니다. **sqlcmd** 스크립팅 변수는 로그인 및 암호 값을 제공하는 데 사용됩니다. 자세한 내용은 [스크립팅 변수와 함께 sqlcmd 사용](../../scripting/sqlcmd-use-with-scripting-variables.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_createmergepub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepubftp.sql#sp_createmergepub_ftp)]  
  
 다음 예에서는 구독자가 FTP를 사용하여 스냅숏을 얻는 병합 게시에 대한 구독을 만듭니다. 구독자는 FTP 공유에 액세스할 때 보안 VPN 연결을 사용해야 합니다. **sqlcmd** 스크립팅 변수는 로그인 및 암호 값을 제공하는 데 사용됩니다. 자세한 내용은 [스크립팅 변수와 함께 sqlcmd 사용](../../scripting/sqlcmd-use-with-scripting-variables.md)을 참조하세요.  
  
 [!code-sql[HowTo#sp_createmergepullsub_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsub_ftp)]  
  
 [!code-sql[HowTo#sp_createmergepullsubagent_ftp](../../../snippets/tsql/SQL15/replication/howto/tsql/createmergepullsubftp.sql#sp_createmergepullsubagent_ftp)]  
  
## <a name="see-also"></a>관련 항목  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [FTP를 통해 스냅숏 전송](../transfer-snapshots-through-ftp.md)   
 [게시 및 아티클 속성 변경](change-publication-and-article-properties.md)   
 [스냅숏으로 구독 초기화](../initialize-a-subscription-with-a-snapshot.md)  
  
  
