---
title: xp_logininfo (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- xp_logininfo_TSQL
- xp_logininfo
dev_langs:
- TSQL
helpviewer_keywords:
- xp_logininfo
ms.assetid: ee7162b5-e11f-4a0e-a09c-1878814dbbbd
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: b5a1a7067e1ebda150d0236020288514eb90a8fc
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890735"
---
# <a name="xp_logininfo-transact-sql"></a>xp_logininfo(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Windows 사용자와 Windows 그룹에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>인수  
`[ @acctname = ] 'account_name'`는에 대 한 액세스 권한이 부여 된 Windows 사용자 또는 그룹의 이름입니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . *account_name* 는 **sysname**이며 기본값은 NULL입니다. *Account_name* 지정 하지 않으면 로그인 권한이 명시적으로 부여 된 모든 windows 그룹 및 windows 사용자가 보고 됩니다. *account_name* 정규화 되어야 합니다. 정규화된 이름이어야 합니다.  
  
 **' 모두 '**  |  **' members '**  
 계정에 대한 모든 사용 권한 경로에 관한 정보를 보고할 것인지 Windows 그룹의 멤버에 관한 정보를 보고할 것인지 지정합니다. ** \@ 옵션** 은 **varchar (10)** 이며 기본값은 NULL입니다. **All** 을 지정 하지 않으면 첫 번째 권한 경로만 표시 됩니다.  
  
`[ @privilege = ] variable_name`는 지정 된 Windows 계정의 권한 수준을 반환 하는 출력 매개 변수입니다. *variable_name* 는 **varchar (10)** 이며 기본값은 ' Not '이 됩니다. 반환 된 권한 수준은 **user**, **admin**또는 **null**입니다.  
  
 OUTPUT  
 이 매개 변수를 지정 하면 출력 매개 변수에 *variable_name* 을 배치 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**계정 이름**|**sysname**|정규화된 Windows 계정 이름입니다.|  
|**type**|**char (8)**|Windows 계정의 유형입니다. 유효한 값은 **사용자** 또는 **그룹**입니다.|  
|**권한과**|**char(9)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한입니다. 유효한 값은 **admin**, **user**또는 **null**입니다.|  
|**mapped login name**|**sysname**|사용자 권한이 있는 사용자 계정의 경우, **매핑된 로그인 이름** 에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 이전에 추가 된 도메인 이름으로 매핑된 규칙을 사용 하 여이 계정으로 로그인 할 때 사용을 시도 하는 매핑된 로그인 이름이 표시 됩니다.|  
|**permission path**|**sysname**|계정 액세스 권한을 부여한 그룹 멤버 자격입니다.|  
  
## <a name="remarks"></a>설명  
 *Account_name* 지정 된 경우 **xp_logininfo** 는 지정 된 Windows 사용자 또는 그룹의 가장 높은 권한 수준을 보고 합니다. Windows 사용자가 시스템 관리자 및 도메인 사용자로서의 액세스 권한을 둘 다 갖고 있으면 시스템 관리자로서 보고됩니다. 사용자가 권한 수준이 같은 여러 Windows 그룹의 멤버인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 처음 부여 받은 그룹만 보고됩니다.  
  
 *Account_name* 로그인과 연결 되지 않은 유효한 Windows 사용자 또는 그룹인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 빈 결과 집합이 반환 됩니다. *Account_name* 를 유효한 Windows 사용자 또는 그룹으로 식별할 수 없는 경우 오류 메시지가 반환 됩니다.  
  
 *Account_name* 및 **all** 이 지정 된 경우 Windows 사용자 또는 그룹에 대 한 모든 사용 권한 경로가 반환 됩니다. *Account_name* 여러 그룹의 멤버인 경우 모두에 대 한 액세스 권한을 부여 받은 경우에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 여러 행이 반환 됩니다. **관리자** 권한 행은 **사용자** 권한 행 이전에 반환 되며 권한 수준 행 내에서는 해당 로그인이 만들어진 순서 대로 반환 됩니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 *Account_name* 및 **멤버가** 지정 된 경우 그룹의 다음 수준 멤버 목록이 반환 됩니다. *Account_name* 로컬 그룹인 경우 목록에는 로컬 사용자, 도메인 사용자 및 그룹이 포함 될 수 있습니다. *Account_name* 도메인 계정인 경우 도메인 사용자로 목록이 구성 됩니다. 그룹 멤버 자격 정보를 검색하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 도메인 컨트롤러에 연결해야 합니다. 서버에서 도메인 컨트롤러에 연결할 수 없는 경우에는 아무 정보도 반환되지 않습니다.  
  
 **xp_logininfo** 는 유니버설 그룹이 아닌 Active Directory 글로벌 그룹의 정보만 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할의 멤버 자격 또는 EXECUTE 권한이 부여 된 **master** 데이터베이스의 **public** 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 Windows 그룹에 대 한 정보를 표시 합니다 `BUILTIN\Administrators` .  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_denylogin &#40;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [Transact-sql&#41;sp_grantlogin &#40;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [Transact-sql&#41;sp_revokelogin &#40;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [Transact-sql&#41;&#40;시스템 저장 프로시저](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;일반 확장 저장 프로시저 &#40;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
