---
title: sp_vupgrade_replication (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e6ece6875e89f684bf0c98f54319e519a648fd84
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47640371"
---
# <a name="spvupgradereplication-transact-sql"></a>sp_vupgrade_replication(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제 서버를 업그레이드할 때 설치 프로그램에 의해 활성화됩니다. 현재 제품 수준에서 복제를 지원하기 위해 필요한 경우 스키마 및 시스템 데이터를 업그레이드합니다. 시스템 및 사용자 데이터베이스에서 새로운 복제 시스템 개체를 만듭니다. 이 저장 프로시저는 복제 업그레이드가 수행될 컴퓨터에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>인수  
 [  **@login=**] **'***로그인***'**  
 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 로그인입니다. *login*은 **sysname**이며 기본값은 NULL입니다. 경우에이 매개 변수가 필요 하지 않습니다 *security_mode* 로 설정 된 **1**, Windows 인증이 있는 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
 [  **@password=**] **'***암호***'**  
 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 암호입니다. *암호* 됩니다 **sysname**, 기본값은 **'** (빈 문자열)입니다. 경우에이 매개 변수가 필요 하지 않습니다 *security_mode* 로 설정 된 **1**, Windows 인증이 있는 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
 [  **@ver_old=**] **'***old_version***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 이 저장 프로시저는 더 이상 사용되지 않으며 차후의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 제거될 예정입니다.  
  
 [  **@force_remove=**] **'***force_removal***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'***security_mode***'**  
 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 로그인 보안 모드입니다. *security_mode* 됩니다 **비트** 이며 기본값은 **0**합니다. 하는 경우 **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용 합니다. 하는 경우 **1**, Windows 인증을 사용 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 **sp_vupgrade_replication** 모든 유형의 복제를 업그레이드 하는 경우에 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버는 **sysadmin** 고정된 서버 역할을 실행할 수 있습니다 **sp_vupgrade_replication**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)  
  
  
