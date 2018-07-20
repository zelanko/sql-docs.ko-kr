---
title: sp_helpdistpublisher (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
caps.latest.revision: 37
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4eed56a7e9356ac7f42c5f1bf2a5d55e85111523
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39082415"
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포자를 사용하여 게시자의 속성을 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>인수  
 [  **@publisher=** ] **'***게시자***'**  
 속성이 반환되는 게시자입니다. *게시자* 됩니다 **sysname**, 기본값은 **%** 합니다.  
  
 [  **@check_user=** ] *check_user*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|게시자의 이름입니다.|  
|**distribution_db**|**sysname**|지정된 게시자에 대한 배포 데이터베이스입니다.|  
|**security_mode**|**int**|복제 에이전트가 지연 업데이트 구독을 위해 게시자에 연결하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 게시자와 연결하는 데 사용한 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증<br /><br /> **1** = Windows 인증|  
|**login**|**sysname**|복제 에이전트가 지연 업데이트 구독을 위해 게시자에 연결하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 게시자와 연결하는 데 사용한 로그인 이름입니다.|  
|**password**|**nvarchar(524)**|간단히 암호화된 형식으로 반환되는 암호입니다. 암호는 NULL에 대 한 사용자 이외의 **sysadmin**합니다.|  
|**Active**|**bit**|원격 게시자가 배포자로 로컬 서버를 사용하는지 여부를 지정합니다.<br /><br /> **0** = 아니요<br /><br /> **1** = 예|  
|**working_directory**|**nvarchar(255)**|작업 디렉터리의 이름입니다.|  
|**신뢰할 수 있는**|**bit**|게시자가 배포자에 연결할 때 암호가 필요한지 여부입니다. 에 대 한 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전에서는이 항상 반환 하 고 **0**, 즉, 암호가 필요 합니다.|  
|**thirdparty_flag**|**bit**|게시를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 타사 응용 프로그램에 사용할 수 있는지 여부를 지정합니다.<br /><br /> **0** = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oracle 또는 Oracle Gateway 게시자입니다.<br /><br /> **1** = 게시자에 통합할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 타사 응용 프로그램을 사용 합니다.|  
|**publisher_type**|**sysname**|게시자의 유형으로 다음 중 하나일 수 있습니다.<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE GATEWAY**|  
|**publisher_data_source**|**nvarchar(4000)**|게시자의 OLE DB 데이터 원본 이름입니다.|  
|**storage_connection_string**|**nvarchar(4000)**|작업 디렉터리에 대 한 저장소 액세스 키 때 Azure SQL 데이터베이스의 게시자 또는 배포자입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpdistpublisher** 모든 유형의 복제에 사용 됩니다.  
  
 **sp_helpdistpublisher** 게시자 로그인이 표시 되지 것입니다 또는 결과에서 암호 설정 되어 비-**sysadmin** 로그인 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할 실행 될 수 있습니다 **sp_helpdistpublisher** 로컬 서버를 배포자로 사용 하 여 게시자에 대 한 합니다. 멤버는 **db_owner** 고정된 데이터베이스 역할 또는 **replmonitor** 배포 데이터베이스의 역할을 실행할 수 있습니다 **sp_helpdistpublisher** 는 사용 하 여 게시자에 대해 배포 데이터베이스입니다. 지정 된 게시에 대 한 사용자가 게시 액세스에서 목록 *publisher* 실행할 수 있습니다 **sp_helpdistpublisher**합니다. 하는 경우 *게시자* 지정 하지 않으면 사용자가 액세스 권한을 갖는 모든 게시자에 대 한 정보를 반환 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
