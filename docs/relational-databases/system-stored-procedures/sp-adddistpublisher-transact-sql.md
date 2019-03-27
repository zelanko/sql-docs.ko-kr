---
title: sp_adddistpublisher (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2018
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
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: c01d00362dc55deb1fa9da8df49beebdaf82b170
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492775"
---
# <a name="spadddistpublisher-transact-sql"></a>sp_adddistpublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdbmi-xxxx-xxx-md.md)]

  지정된 배포 데이터베이스를 사용하기 위해 게시자를 구성합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다. 저장된 프로시저 [sp_adddistributor &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) 하 고 [sp_adddistributiondb &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md) 저장이 사용 하기 전에 실행 해야 합니다 프로시저입니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'` 게시자 이름이입니다. *게시자* 됩니다 **sysname**, 기본값은 없습니다.  
  
`[ @distribution_db = ] 'distribution_db'` 배포 데이터베이스의 이름이입니다. *distributor_db* 됩니다 **sysname**, 기본값은 없습니다. 이 매개 변수는 복제 에이전트가 게시자에 연결할 때 사용합니다.  
  
`[ @security_mode = ] security_mode` 구현 된 보안 모드가입니다. 이 매개 변수는만 데 복제 에이전트가 지연된 업데이트 구독 또는 비-를 사용 하 여 게시자에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다. *security_mode* 됩니다 **int**, 이며 다음이 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0**|배포자의 복제 에이전트는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용하여 게시자에 연결합니다.|  
|**1** (기본값)|배포자의 복제 에이전트는 Windows 인증을 사용하여 게시자에 연결합니다.|  
  
`[ @login = ] 'login'` 로그인이입니다. 이 매개 변수는 필요한 경우 *security_mode* 됩니다 **0**합니다. *login*은 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 복제 에이전트가 게시자에 연결할 때 사용합니다.  
  
`[ @password = ] 'password']` 암호가입니다. *암호* 됩니다 **sysname**, 기본값은 NULL입니다. 이 매개 변수는 복제 에이전트가 게시자에 연결할 때 사용합니다.  
  
> [!IMPORTANT]  
>  빈 암호를 사용하지 마세요. 강력한 암호를 사용하세요.  
  
`[ @working_directory = ] 'working_directory'` 게시용 데이터 및 스키마 파일을 저장 하는 데 작업 디렉터리의 이름이입니다. *working_directory* 됩니다 **nvarchar(255)**, 및 ReplData 폴더의이 인스턴스에 대 한 기본값 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]예를 들어 `C:\Program Files\Microsoft SQL Server\MSSQL\MSSQ.1\ReplData`합니다. 이름은 UNC 형식으로 지정해야 합니다.  

 Azure SQL database를 사용 하 여 `\\<storage_account>.file.core.windows.net\<share>`입니다.

`[ @storage_connection_string = ] 'storage_connection_string'` SQL Database에 필요 합니다. 저장소에서 Azure Portal에서 액세스 키를 사용 하 여 > 설정 합니다.

 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]

`[ @trusted = ] 'trusted'` 이 매개 변수는 사용 되지 않으며 이전 버전과 호환성만 제공 됩니다. *신뢰할 수 있는* 됩니다 **nvarchar(5)** 도로 설정 **false** 오류가 발생 합니다.  
  
`[ @encrypted_password = ] encrypted_password` 설정 *encrypted_password* 는 지원 되지 않습니다. 이 설정 하려고 **비트** 매개 변수를 **1** 오류가 발생 합니다.  
  
`[ @thirdparty_flag = ] thirdparty_flag` 게시자 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. *thirdparty_flag* 됩니다 **비트**, 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**0** (기본값)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스입니다.|  
|**1**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 데이터베이스입니다.|  
  
`[ @publisher_type = ] 'publisher_type'` 게시자 되지 않을 때 게시자 유형을 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. *publisher_type* 은 sysname 이며 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|**MSSQLSERVER**<br /><br /> (기본값)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자를 지정합니다.|  
|**ORACLE**|표준 Oracle 게시자를 지정합니다.|  
|**ORACLE GATEWAY**|Oracle Gateway 게시자를 지정합니다.|  
  
 Oracle 게시자와 Oracle Gateway 게시자의 차이점에 대 한 자세한 내용은 참조 하세요. [Oracle 게시자 구성](../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_adddistpublisher** 스냅숏 복제, 트랜잭션 복제 및 병합 복제에서 사용 됩니다.  
  
## <a name="example"></a>예제  
 [!code-sql[HowTo#AddDistPub](../../relational-databases/replication/codesnippet/tsql/sp-adddistpublisher-tran_1.sql)]  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_adddistpublisher**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [sp_helpdistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)  
  
  
