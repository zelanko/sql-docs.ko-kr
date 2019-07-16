---
title: sp_vupgrade_mergeobjects (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_vupgrade_mergeobjects
- sp_vupgrade_mergeobjects_TSQL
helpviewer_keywords:
- sp_vupgrade_mergeobjects
ms.assetid: 73257c2e-cc4c-48e7-9d66-7ef045bdd4f5
author: stevestein
ms.author: sstein
ms.openlocfilehash: ed0992ff1b6b7de6f93213b612ff05ebcbdb3df5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042701"
---
# <a name="spvupgrademergeobjects-transact-sql"></a>sp_vupgrade_mergeobjects(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 복제의 데이터 변경 내용을 추적하고 적용하는 데 사용되는 아티클별 트리거, 저장 프로시저 및 뷰를 다시 생성합니다. 다음과 같은 경우 이 프로시저를 실행합니다.  
  
-   복제에 필요한 개체가 실수로 삭제된 경우  
  
-   복제 개체를 하나 이상 수정해야 하는 핫픽스 등의 업데이트를 적용하는 경우. 업데이트를 적용한 후 각 노드에서 프로시저를 실행합니다.  
  
 이 저장 프로시저를 실행하는 경우 구독을 다시 초기화하지 않아도 됩니다. 서비스 팩을 설치하거나 최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 업그레이드하는 경우에는 이 프로시저가 필요하지 않습니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_vupgrade_mergeobjects [ [@login = ] 'login' ]  
    [ , [ @password = ] 'password' ]  
    [ , [ @security_mode = ] security_mode ]  
```  
  
## <a name="arguments"></a>인수  
`[ @login = ] 'login'` 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 로그인이입니다. *login*은 **sysname**이며 기본값은 NULL입니다. 경우에이 매개 변수가 필요 하지 않습니다 *security_mode* 로 설정 된 **1**, Windows 인증이 있는 합니다.  
  
`[ @password = ] 'password'` 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 시스템 관리자 암호가입니다. *암호* 됩니다 **sysname**, 기본값은 **'** (빈 문자열)입니다. 경우에이 매개 변수가 필요 하지 않습니다 *security_mode* 로 설정 된 **1**, Windows 인증이 있는 합니다.  
  
`[ @security_mode = ] 'security_mode'` 배포 데이터베이스에서 새 시스템 개체를 만들 때 사용할 로그인 보안 모드가입니다. *security_mode* 됩니다 **비트** 이며 기본값은 **1**합니다. 하는 경우 **0**, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 사용 합니다. 하는 경우 **1**, Windows 인증을 사용 합니다. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_vupgrade_mergeobjects** 병합 복제에만 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 **sysadmin** 고정 서버 역할의 멤버 자격이 필요합니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [복제된 데이터베이스 업그레이드](../../database-engine/install-windows/upgrade-replicated-databases.md)  
  
  
