---
title: sp_helpdistpublisher (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistpublisher_TSQL
- sp_helpdistpublisher
helpviewer_keywords:
- sp_helpdistpublisher
ms.assetid: f207c22d-8fb2-4756-8a9d-6c51d6cd3470
author: stevestein
ms.author: sstein
ms.openlocfilehash: a47a81b2b19ceccf76a031e298ab60cf4a6f8c9a
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770946"
---
# <a name="sphelpdistpublisher-transact-sql"></a>sp_helpdistpublisher(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  배포자를 사용하여 게시자의 속성을 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdistpublisher [ [ @publisher=] 'publisher']   
    [ , [ @check_user = ] check_user  
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`속성이 반환 되는 게시자입니다. *publisher* 는 **sysname**이며 기본값 **%** 은입니다.  
  
`[ @check_user = ] check_user` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|게시자의 이름입니다.|  
|**distribution_db**|**sysname**|지정된 게시자에 대한 배포 데이터베이스입니다.|  
|**security_mode**|**int**|복제 에이전트가 지연 업데이트 구독을 위해 게시자에 연결하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 게시자와 연결하는 데 사용한 보안 모드입니다.<br /><br /> **0**  =  인증[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = Windows 인증|  
|**login**|**sysname**|복제 에이전트가 지연 업데이트 구독을 위해 게시자에 연결하거나 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 아닌 게시자와 연결하는 데 사용한 로그인 이름입니다.|  
|**password**|**nvarchar(524)**|간단히 암호화된 형식으로 반환되는 암호입니다. **Sysadmin**이외의 사용자에 대 한 암호는 NULL입니다.|  
|**active**|**bit**|원격 게시자가 배포자로 로컬 서버를 사용하는지 여부를 지정합니다.<br /><br /> **0** = 아니요<br /><br /> **1** = 예|  
|**working_directory**|**nvarchar(255)**|작업 디렉터리의 이름입니다.|  
|**신뢰할 수 있는**|**bit**|게시자가 배포자에 연결할 때 암호가 필요한지 여부입니다. 이상 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 버전의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 경우이는 항상 **0**을 반환 하며,이는 암호가 필요 함을 의미 합니다.|  
|**thirdparty_flag**|**bit**|게시를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 타사 응용 프로그램에 사용할 수 있는지 여부를 지정합니다.<br /><br /> **0, oracle 또는** = oracle Gateway 게시자입니다.[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]<br /><br /> **1** = 게시자가 타사 응용 프로그램 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 을 사용 하 여 통합 되었습니다.|  
|**publisher_type**|**sysname**|게시자의 유형으로 다음 중 하나일 수 있습니다.<br /><br /> **MSSQLSERVER**<br /><br /> **ORACLE**<br /><br /> **ORACLE 게이트웨이**|  
|**publisher_data_source**|**nvarchar(4000)**|게시자의 OLE DB 데이터 원본 이름입니다.|  
|**storage_connection_string**|**nvarchar(4000)**|배포자 또는 게시자 Azure SQL Database의 작업 디렉터리에 대 한 저장소 액세스 키입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_helpdistpublisher** 은 모든 유형의 복제에 사용 됩니다.  
  
 **sp_helpdistpublisher** 는**sysadmin** 이 아닌 로그인에 대 한 결과 집합에 게시자 로그인 또는 암호를 표시 하지 않습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버는 로컬 서버를 배포자로 사용 하는 모든 게시자에 대해 **sp_helpdistpublisher** 을 실행할 수 있습니다. 배포 데이터베이스의 **db_owner** 고정 데이터베이스 역할 또는 **replmonitor** 역할의 멤버는 해당 배포 데이터베이스를 사용 하는 모든 게시자에 대해 **sp_helpdistpublisher** 을 실행할 수 있습니다. 지정 된 *게시자* 에서 게시에 대 한 게시 액세스 목록의 사용자는 **sp_helpdistpublisher**을 실행할 수 있습니다. *Publisher* 를 지정 하지 않으면 사용자에 게 액세스 권한이 있는 모든 게시자에 대 한 정보가 반환 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_dropdistpublisher &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)  
  
  
