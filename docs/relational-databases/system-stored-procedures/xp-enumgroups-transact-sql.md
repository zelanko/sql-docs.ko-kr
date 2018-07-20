---
title: xp_enumgroups (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 844460db0fd4cec42b8b89bf70deb72098d3ce6a
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39101551"
---
# <a name="xpenumgroups-transact-sql"></a>xp_enumgroups(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  로컬 Microsoft Windows 그룹의 목록 또는 지정된 Windows 도메인에 정의된 글로벌 그룹의 목록을 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>인수  
 **'** *domain_name* **'**  
 글로벌 그룹의 목록을 열거할 Windows 도메인의 이름입니다. *domain_name* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**그룹**|**sysname**|Windows 그룹의 이름입니다.|  
|**주석**|**sysname**|Windows에서 제공한 Windows 그룹에 대한 설명입니다.|  
  
## <a name="remarks"></a>Remarks  
 하는 경우 *domain_name* 는 Windows 기반 컴퓨터의 이름인는 인스턴스의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 실행 또는 도메인 이름이 없는 지정 **xp_enumgroups** 컴퓨터에서 로컬 그룹을 열거 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
 **xp_enumgroups** 의 인스턴스가 사용할 수 없습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 98에서 실행 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **db_owner** 고정된 데이터베이스 역할의는 **마스터** 의 멤버 자격 또는 데이터베이스를 **sysadmin** 고정된 서버 역할.  
  
## <a name="examples"></a>예  
 다음 예에서는 `sales` 도메인에 있는 그룹을 나열합니다.  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [일반 확장 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [xp_loginconfig &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
