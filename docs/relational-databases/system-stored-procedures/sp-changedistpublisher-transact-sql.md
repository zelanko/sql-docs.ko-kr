---
title: sp_changedistpublisher (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changedistpublisher_TSQL
- sp_changedistpublisher
helpviewer_keywords:
- sp_changedistpublisher
ms.assetid: 7ef5c89d-faaa-4f8e-aef7-00649ebc8bc9
author: stevestein
ms.author: sstein
ms.openlocfilehash: 80eb30fc6b6b2cea9fc058780831af3915fd9007
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68771360"
---
# <a name="sp_changedistpublisher-transact-sql"></a>sp_changedistpublisher(Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  배포 게시자의 속성을 변경합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changedistpublisher [ @publisher = ] 'publisher'  
    [ , [ @property = ] 'property' ]  
    [ , [ @value = ] 'value' ]  
    [ , [ @storage_connection_string = ] 'storage_connection_string']
```  
  
## <a name="arguments"></a>인수  
`[ @publisher = ] 'publisher'`게시자 이름입니다. *publisher* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @property = ] 'property'`지정 된 게시자에 대해 변경할 속성입니다. *속성* 은 **sysname** 이며 다음 값 중 하나일 수 있습니다.  
  
`[ @value = ] 'value'`지정 된 속성에 대 한 값입니다. *value* 는 **nvarchar (255)** 이며 기본값은 NULL입니다.  
  
`[ @storage_connection_string = ] 'storage_connection_string'`SQL Database 관리 되는 인스턴스에 필요 합니다. Azure SQL Database 저장소 볼륨에 대 한 액세스 키와 일치 해야 합니다. 


 > [!INCLUDE[Azure SQL Database link](../../includes/azure-sql-db-repl-for-more-information.md)]
 
 다음 표에서는 게시자의 속성 및 해당 속성 값을 설명합니다.  
  
|속성|값|Description|  
|--------------|------------|-----------------|  
|**활성**|**true**|게시자를 활성화합니다.|  
||**false**|게시자를 비활성화합니다.|  
|**distribution_db**||배포 데이터베이스의 이름입니다.|  
|**로그인**||로그인 이름입니다.|  
|**password**||제공된 로그인에 대한 강력한 암호입니다.|  
|**security_mode**|**1**|게시자에 연결할 때 Windows 인증을 사용합니다. *This cannot be changed for a non-*[!INCLUDE[msCoName](../../includes/msconame-md.md)] 이외 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *게시자* 에 대해서는 변경할 수 없습니다.|  
||**0**|게시자에 연결할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용합니다. *이외 게시자에 대해서는 변경할 수 없습니다* [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] *.*|  
|**working_directory**||게시용 데이터 및 스키마 파일을 저장하는 데 사용되는 작업 디렉터리입니다.|  
|NULL(기본값)||사용 가능한 모든 *속성* 옵션이 출력 됩니다.| 
|**storage_connection_string**| 액세스 키 | 데이터베이스가 Azure SQL Database Managed Instance 될 때의 작업 디렉터리에 대 한 액세스 키입니다. 
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_changedistpublisher** 은 모든 유형의 복제에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_changedistpublisher**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [배포자 및 게시자 속성 보기 및 수정](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [Transact-sql&#41;sp_adddistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_dropdistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-dropdistpublisher-transact-sql.md)   
 [Transact-sql&#41;sp_helpdistpublisher &#40;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
