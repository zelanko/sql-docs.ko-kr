---
title: sp_adddistributiondb (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_adddistributiondb_TSQL
- sp_adddistributiondb
helpviewer_keywords:
- sp_adddistributiondb
ms.assetid: e9bad56c-d2b3-44ba-a4d7-ff2fd842e32d
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6657074bade1db3cb050d6ca0c33e358d05e5f0c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="spadddistributiondb-transact-sql"></a>sp_adddistributiondb(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  새 배포 데이터베이스를 만들고 배포자 스키마를 설치합니다. 배포 데이터베이스는 복제에 사용하는 프로시저, 스키마 및 메타데이터를 저장합니다. 이 저장 프로시저는 배포 데이터베이스를 만들기 위해 master 데이터베이스의 배포자에서 실행되며 복제 배포를 사용하는 데 필요한 테이블 및 저장 프로시저를 설치합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_adddistributiondb [ @database= ] 'database'   
    [ , [ @data_folder= ] 'data_folder' ]   
    [ , [ @data_file= ] 'data_file' ]   
    [ , [ @data_file_size= ] data_file_size ]   
    [ , [ @log_folder= ] 'log_folder' ]   
    [ , [ @log_file= ] 'log_file' ]   
    [ , [ @log_file_size= ] log_file_size ]   
    [ , [ @min_distretention= ] min_distretention ]   
    [ , [ @max_distretention= ] max_distretention ]   
    [ , [ @history_retention= ] history_retention ]   
    [ , [ @security_mode= ] security_mode ]   
    [ , [ @login= ] 'login' ]   
    [ , [ @password= ] 'password' ]   
    [ , [ @createmode= ] createmode ]  
    [ , [ @from_scripting = ] from_scripting ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@database=**] *데이터베이스 '*  
 만들 배포 데이터베이스의 이름입니다. *데이터베이스* 은 **sysname**, 기본값은 없습니다. 지정한 데이터베이스가 이미 존재하지만 아직 배포 데이터베이스로 표시되지 않은 경우 배포를 활성화하는 데 필요한 개체가 설치되고 데이터베이스가 배포 데이터베이스로 표시됩니다. 지정한 데이터베이스가 이미 배포 데이터베이스로 활성화된 경우 오류가 반환됩니다.  
  
 [  **@data_folder=**] **'***data_folder'*  
 배포 데이터베이스 데이터 파일을 저장하는 데 사용되는 디렉터리의 이름입니다. *data_folder* 은 **nvarchar (255)**, 기본값은 NULL입니다. NULL인 경우 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 인스턴스에 대한 데이터 디렉터리(예: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`)가 사용됩니다.  
  
 [  **@data_file=**] **'***data_file***'**  
 데이터베이스 파일의 이름입니다. *data_file* 은 **nvarchar (255)**, 기본값은 **데이터베이스**합니다. NULL인 경우 저장 프로시저는 데이터베이스 이름을 사용하여 새 파일 이름을 생성합니다.  
  
 [  **@data_file_size=**] *data_file_size*  
 초기 데이터 파일 크기(MB)입니다. *data_file_size i*s **int**, 기본값은 5MB입니다.  
  
 [  **@log_folder=**] **'***log_folder***'**  
 데이터베이스 로그 파일의 디렉터리 이름입니다. *log_folder* 은 **nvarchar (255)**, 기본값은 NULL입니다. NULL인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 해당 인스턴스(예: `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Data`)에 대한 데이터 디렉터리가 사용됩니다.  
  
 [  **@log_file=**] **'***log_file***'**  
 로그 파일의 이름입니다. *log_file* 은 **nvarchar (255)**, 기본값은 NULL입니다. NULL인 경우 저장 프로시저는 데이터베이스 이름을 사용하여 새 파일 이름을 생성합니다.  
  
 [  **@log_file_size=**] *log_file_size*  
 초기 로그 파일 크기(MB)입니다. *log_file_size* 은 **int**, 기본값은 0MB으로 파일 크기가 가장 작은 로그를 사용 하 여 만들어집니다. 즉 파일 크기에서 허용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 [  **@min_distretention=**] *min_distretention*  
 배포 데이터베이스에서 트랜잭션을 삭제하기 전의 최소 보존 기간(시간)입니다. *min_distretention* 은 **int**, 기본값은 0 시간입니다.  
  
 [  **@max_distretention=**] *max_distretention*  
 트랜잭션을 삭제하기 전의 최대 보존 기간(시)입니다. *max_distretention* 은 **int**, 기본값: 72 시간입니다. 배포의 최대 보존 기간보다 오래된 복제 명령을 받지 않은 구독은 비활성 상태로 표시되어 다시 초기화해야 합니다. RAISERROR 21011 오류는 각 비활성 구독에 대해 발생됩니다. 값이 **0** 즉 복제 된 트랜잭션을 배포 데이터베이스에 저장 되지 않습니다.  
  
 [  **@history_retention=**] *history_retention*  
 기록을 보존할 시간입니다. *history_retention* 은 **int**, 기본값은 48 시간입니다.  
  
 [  **@security_mode=**] *security_mode*  
 배포자에 연결하는 데 사용할 보안 모드입니다. *security_mode* 은 **int**, 기본값은 1입니다. **0** 지정 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증; **1** Windows 통합 인증을 지정 합니다.  
  
 [  **@login=**] **'***로그인***'**  
 배포 데이터베이스를 만들기 위해 배포자에 연결할 때 사용하는 로그인 이름입니다. 이 소프트웨어가 필요 *security_mode* 로 설정 된 **0**합니다. *로그인* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@password=**] **'***암호***'**  
 배포자에 연결할 때 사용하는 암호입니다. 이 소프트웨어가 필요 *security_mode* 로 설정 된 **0**합니다. *암호* 은 **sysname**, 기본값은 NULL입니다.  
  
 [  **@createmode=**] *createmode*  
 *createmode* 은 **int**, 기본값은 1, 다음 값 중 하나가 될 수 있습니다.  
  
|값|설명|  
|-----------|-----------------|  
|**0**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**1** (기본값)|CREATE DATABASE 또는 기존 데이터베이스에 있으며 다음 적용 **instdist.sql** 파일을 배포 데이터베이스에서 복제 개체를 만듭니다.|  
|**2**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
  
 [  **@from_scripting =** ] *from_scripting*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>주의  
 **sp_adddistributiondb** 모든 유형의 복제에 사용 됩니다. 단, 이 저장 프로시저는 배포자에서만 실행합니다.  
  
 실행 하 여 배포자를 구성 해야 [sp_adddistributor](../../relational-databases/system-stored-procedures/sp-adddistributor-transact-sql.md) 실행 하기 전에 **sp_adddistributiondb**합니다.  
  
 실행 **sp_adddistributor** 실행 한 후 **sp_adddistributiondb**합니다.  
  
## <a name="example"></a>예제  
  
```  
-- This script uses sqlcmd scripting variables. They are in the form  
-- $(MyVariable). For information about how to use scripting variables    
-- on the command line and in SQL Server Management Studio, see the   
-- "Executing Replication Scripts" section in the topic  
-- "Programming Replication Using System Stored Procedures".  
  
-- Install the Distributor and the distribution database.  
DECLARE @distributor AS sysname;  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
DECLARE @directory AS nvarchar(500);  
DECLARE @publicationDB AS sysname;  
-- Specify the Distributor name.  
SET @distributor = $(DistPubServer);  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
-- Specify the replication working directory.  
SET @directory = N'\\' + $(DistPubServer) + '\repldata';  
-- Specify the publication database.  
SET @publicationDB = N'AdventureWorks2012';   
  
-- Install the server MYDISTPUB as a Distributor using the defaults,  
-- including autogenerating the distributor password.  
USE master  
EXEC sp_adddistributor @distributor = @distributor;  
  
-- Create a new distribution database using the defaults, including  
-- using Windows Authentication.  
USE master  
EXEC sp_adddistributiondb @database = @distributionDB,   
    @security_mode = 1;  
GO  
  
-- Create a Publisher and enable AdventureWorks2012 for replication.  
-- Add MYDISTPUB as a publisher with MYDISTPUB as a local distributor  
-- and use Windows Authentication.  
DECLARE @distributionDB AS sysname;  
DECLARE @publisher AS sysname;  
-- Specify the distribution database.  
SET @distributionDB = N'distribution';  
-- Specify the Publisher name.  
SET @publisher = $(DistPubServer);  
  
USE [distribution]  
EXEC sp_adddistpublisher @publisher=@publisher,   
    @distribution_db=@distributionDB,   
    @security_mode = 1;  
GO  
  
```  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_adddistributiondb**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [sp_changedistributiondb &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40; Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [sp_helpdistributiondb&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [배포 구성](../../relational-databases/replication/configure-distribution.md)  
  
  
