---
title: sp_vupgrade_replication (Transact SQL) | Microsoft Docs
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
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d07f50261726675d921f39226cd97f9b163b1f7f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
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
 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 로그인입니다. *로그인* 은 **sysname**, 기본값은 NULL입니다. 경우에이 매개 변수가 필요 하지 않습니다 *security_mode* 로 설정 되어 **1**은 Windows 인증입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
 [  **@password=**] **'***암호***'**  
 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 암호입니다. *암호* 은 **sysname**, 기본값은 **'** (빈 문자열)입니다. 경우에이 매개 변수가 필요 하지 않습니다 *security_mode* 로 설정 되어 **1**은 Windows 인증입니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
 [  **@ver_old=**] **'***old_version***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 이 저장 프로시저는 더 이상 사용되지 않으며 차후의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 제거될 예정입니다.  
  
 [  **@force_remove=**] **'***force_removal***'**  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@security_mode=**] **'***security_mode***'**  
 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 로그인 보안 모드입니다. *security_mode* 은 **비트** 의 기본값은 **0**합니다. 경우 **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용 합니다. 경우 **1**, Windows 인증을 사용 합니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_vupgrade_replication** 모든 유형의 복제를 업그레이드 하는 경우 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할을 실행할 수 있는 **sp_vupgrade_replication**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-replicated-data.md)  
  
  
