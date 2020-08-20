---
description: sp_vupgrade_replication(Transact-SQL)
title: sp_vupgrade_replication (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_replication_TSQL
- sp_vupgrade_replication
helpviewer_keywords:
- sp_vupgrade_replication
ms.assetid: d2c0ed66-07d1-4adc-82e5-a654376879bc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d8630a02b31f7589a54cf8b9428f4fbb6a1980be
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480947"
---
# <a name="sp_vupgrade_replication-transact-sql"></a>sp_vupgrade_replication(Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  복제 서버를 업그레이드할 때 설치 프로그램에 의해 활성화됩니다. 현재 제품 수준에서 복제를 지원하기 위해 필요한 경우 스키마 및 시스템 데이터를 업그레이드합니다. 시스템 및 사용자 데이터베이스에서 새로운 복제 시스템 개체를 만듭니다. 이 저장 프로시저는 복제 업그레이드가 수행될 컴퓨터에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_vupgrade_replication [ [@login=] 'login' ]  
    [ , [ @password= ] 'password' ]  
    [ , [ @ver_old= ] 'old_version' ]  
    [ , [ @force_remove= ] 'force_removal' ]  
    [ , [ @security_mode= ] security_mode ]  
```  
  
## <a name="arguments"></a>인수  
`[ @login = ] 'login'` 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 로그인입니다. *login*은 **sysname**이며 기본값은 NULL입니다. 이 매개 변수는 Windows 인증용 *security_mode* **1**로 설정 된 경우에는 필요 하지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
`[ @password = ] 'password'` 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 암호입니다. *password* 는 **sysname**이며 기본값은 **' '** (빈 문자열)입니다. 이 매개 변수는 Windows 인증용 *security_mode* **1**로 설정 된 경우에는 필요 하지 않습니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
`[ @ver_old = ] 'old_version'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 이 저장 프로시저는 더 이상 사용되지 않으며 차후의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 릴리스에서 제거될 예정입니다.  
  
`[ @force_remove = ] 'force_removal'` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @security_mode = ] 'security_mode'` 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 로그인 보안 모드입니다. *security_mode* 은 **bit** 이며 기본값은 **0**입니다. **0**인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증이 사용 됩니다. **1**인 경우 Windows 인증이 사용 됩니다.  
  
> [!NOTE]  
>  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전으로 업그레이드할 경우 이 매개 변수가 무시됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_vupgrade_replication** 은 모든 유형의 복제를 업그레이드할 때 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버만 **sp_vupgrade_replication**를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [Transact-sql&#41;를 &#40;하는 복제 저장 프로시저 ](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [복제된 데이터의 유효성 검사](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
