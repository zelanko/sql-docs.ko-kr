---
title: sp_changereplicationserverpasswords (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_changereplicationserverpasswords_TSQL
- sp_changereplicationserverpasswords
helpviewer_keywords:
- sp_changereplicationserverpasswords
ms.assetid: 9333da96-3a1c-4adb-9a74-5dac9ce596df
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f95ea9768d9aaf6e599cb353f32fe6cfd19b4ee8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="spchangereplicationserverpasswords-transact-sql"></a>sp_changereplicationserverpasswords(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  에 대 한 저장 된 암호 변경의 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 계정 또는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복제 토폴로지에 있는 서버에 연결할 때 복제 에이전트에서 사용 되는 로그인입니다. 서버에서 실행 중인 모든 에이전트가 동일한 로그인 또는 계정을 사용하더라도 보통은 각 에이전트의 암호를 개별적으로 변경해야 합니다. 이 저장 프로시저를 사용하면 서버에서 실행 중인 모든 복제 에이전트에서 사용하는 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이나 Windows 계정의 모든 인스턴스에 대한 암호를 변경할 수 있습니다. 이 저장 프로시저는 master 데이터베이스의 복제 토폴로지에 있는 모든 서버에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_changereplicationserverpasswords [ @login_type = ] login_type  
        , [ @login = ] 'login'   
        , [ @password = ] 'password'  
    [ , [ @server = ] 'server' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@login_type** =] *login_type*  
 제공한 자격 증명의 인증 유형입니다. *login_type* 은 **tinyint**, 기본값은 없습니다.  
  
 **1** = Windows 통합된 인증  
  
 **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증  
  
 [ **@login** =] **'***로그인***'**  
 변경할 Windows 계정 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인의 이름입니다. *로그인* 은 **nvarchar (257)**, 기본값은 없습니다  
  
 [ **@password** =] **'***암호***'**  
 새 암호를 저장할 수는 지정 된 *로그인*합니다. *암호* 은 **sysname**, 기본값은 없습니다.  
  
> [!NOTE]  
>  복제 암호를 변경한 후 해당 암호를 사용하는 각 에이전트를 중지한 다음 다시 시작해야 에이전트에 변경 내용이 적용됩니다.  
  
 [ **@server** =] **'***서버***'**  
 저장된 암호를 변경할 서버 연결입니다. *서버* 은 **sysname**, 다음이 값 중 하나일 수 있습니다.  
  
|Value|Description|  
|-----------|-----------------|  
|**배포자**|배포자에 대한 모든 에이전트 연결입니다.|  
|**publisher**|게시자에 대한 모든 에이전트 연결입니다.|  
|**subscriber**|구독자에 대한 모든 에이전트 연결입니다.|  
|**%** (기본값)|복제 토폴로지의 모든 서버에 대한 모든 에이전트 연결입니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_changereplicationserverpasswords** 모든 유형의 복제와 함께 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_changereplicationserverpasswords**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 보안 설정 보기 및 수정](../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
