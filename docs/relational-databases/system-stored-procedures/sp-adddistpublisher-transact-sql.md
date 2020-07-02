---
title: sp_adddistpublisher (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_adddistpublisher
- sp_adddistpublisher_TSQL
helpviewer_keywords:
- sp_adddistpublisher
ms.assetid: 04e15011-a902-4074-b38c-3ec2fc73b838
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: ba76aefe1b3b4f18a596c25d136c4ec6914ce5a6
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85760226"
---
# <a name="sp_adddistpublisher-transact-sql"></a>sp_adddistpublisher(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  지정된 배포 데이터베이스를 사용하기 위해 게시자를 구성합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다. 이 저장 프로시저를 사용 하기 전에 [transact-sql sp_adddistributiondb&#41;&#40;](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) transact-sql [&#40;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) sp_adddistributor 저장 프로시저를 실행 해야 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adddistpublisher [ @publisher= ] 'publisher'   
        , [ @distribution_db= ] 'distribution_db'   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @working_directory= ] 'working_directory' ]   
    [ , [ @storage_connection_string= ] 'storage_connection_string']
    [ , [ @trusted= ] 'trusted' ]   
    [ , [ @encrypted_password= ] encrypted_password ]   
    [ , [ @thirdparty_flag = ] thirdparty_flag ]  
    [ , [ @publisher_type = ] 'publisher_type' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  

> [!NOTE]
> 서버 이름은으로 지정할 수 있습니다 `<Hostname>,<PortNumber>` . 사용자 지정 포트를 사용 하 여 Linux 또는 Windows에 SQL Server를 배포할 때 연결에 대 한 포트 번호를 지정 해야 하며 browser 서비스를 사용할 수 없습니다.
  
`[ @distribution_db = ] 'distribution_db'`배포 데이터베이스의 이름입니다. *distributor_db* 는 **sysname**이며 기본값은 없습니다. 이 매개 변수는 복제 에이전트가 게시자에 연결할 때 사용합니다.  
  
`[ @security_mode = ] security_mode`는 구현 된 보안 모드입니다. 이 매개 변수는 복제 에이전트가 지연 업데이트 구독 또는 이외 게시자로 게시자에 연결 하는 데만 사용 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *security_mode* 은 **int**이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0**|배포자의 복제 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 게시자에 연결합니다.|  
|**1** (기본값)|배포자의 복제 에이전트는 Windows 인증을 사용하여 게시자에 연결합니다.|  
  
`[ @login = ] 'login'`로그인입니다. *Security_mode* 가 **0**인 경우이 매개 변수는 필수입니다. *login*은 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 복제 에이전트가 게시자에 연결할 때 사용합니다.  
  
`[ @password = ] 'password']`암호입니다. *password* 는 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 복제 에이전트가 게시자에 연결할 때 사용합니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요.  
  
`[ @working_directory = ] 'working_directory'`게시에 대 한 데이터 및 스키마 파일을 저장 하는 데 사용 되는 작업 디렉터리의 이름입니다. *working_directory* 은 **nvarchar (255)** 이며 기본값은이 인스턴스에 대 한 repldata 폴더입니다 ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 예:) `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData` . 이름은 UNC 형식으로 지정해야 합니다.  

 Azure SQL Database의 경우를 사용 `\\<storage_account>.file.core.windows.net\<share>` 합니다.

`[ @storage_connection_string = ] 'storage_connection_string'`SQL Database에 필요 합니다. 저장소 > 설정에서 Azure Portal의 액세스 키를 사용 합니다.

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'`이 매개 변수는 더 이상 사용 되지 않으며 이전 버전과의 호환성을 위해서만 제공 됩니다. *trusted* 는 **nvarchar (5)** 이며 **false** 로 설정 하면 오류가 발생 합니다.  
  
`[ @encrypted_password = ] encrypted_password`*Encrypted_password* 설정은 더 이상 지원 되지 않습니다. 이 **비트** 매개 변수를 **1** 로 설정 하려고 하면 오류가 발생 합니다.  
  
`[ @thirdparty_flag = ] thirdparty_flag`게시자가 인 경우입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *thirdparty_flag* **bit**이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0** (기본값)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 데이터베이스입니다.|  
  
`[ @publisher_type = ] 'publisher_type'`게시자가가 아닌 경우 게시자 유형을 지정 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *publisher_type* 는 sysname 이며 다음 값 중 하나일 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (기본값)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정합니다.|  
|**ORACLE**|표준 Oracle 게시자를 지정합니다.|  
|**ORACLE GATEWAY**|Oracle Gateway 게시자를 지정합니다.|  
  
 Oracle 게시자와 Oracle Gateway 게시자 간의 차이점에 대 한 자세한 내용은 [Oracle 게시자 구성](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)을 참조 하세요.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 **sp_adddistpublisher** 는 스냅숏 복제, 트랜잭션 복제 및 병합 복제에 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_adddistpublisher**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [Transact-sql&#41;sp_changedistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)  
  
  
