---
description: xp_enumgroups(Transact-SQL)
title: xp_enumgroups (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_enumgroups_TSQL
- xp_enumgroups
dev_langs:
- TSQL
helpviewer_keywords:
- xp_enumgroups
ms.assetid: 0bd3ed36-e260-469c-a5ff-b033fb9ea59d
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 59535a5dd2d5df7b5d165e58a30358001378d360
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551096"
---
# <a name="xp_enumgroups-transact-sql"></a>xp_enumgroups(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  로컬 Microsoft Windows 그룹의 목록 또는 지정된 Windows 도메인에 정의된 글로벌 그룹의 목록을 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_enumgroups [ 'domain_name' ]  
```  
  
## <a name="arguments"></a>인수  
 **'** *domain_name* **'**  
 글로벌 그룹의 목록을 열거할 Windows 도메인의 이름입니다. *domain_name* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**group**|**sysname**|Windows 그룹의 이름입니다.|  
|**comment**|**sysname**|Windows에서 제공한 Windows 그룹에 대한 설명입니다.|  
  
## <a name="remarks"></a>설명  
 *Domain_name* 가 인스턴스가 실행 되는 Windows 기반 컴퓨터의 이름 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이거나 도메인 이름을 지정 하지 않은 경우 **xp_enumgroups** 를 실행 하는 컴퓨터에서 로컬 그룹을 열거 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
 **xp_enumgroups** 인스턴스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Windows 98에서 실행 중인 경우에는 xp_enumgroups 사용할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 **Master** 데이터베이스에서 **db_owner** 고정 데이터베이스 역할의 멤버 이거나 **sysadmin** 고정 서버 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 `sales` 도메인에 있는 그룹을 나열합니다.  
  
```  
EXEC xp_enumgroups 'sales';  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;xp_loginconfig &#40;](../../relational-databases/system-stored-procedures/xp-loginconfig-transact-sql.md)   
 [Transact-sql&#41;xp_logininfo &#40;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
