---
title: xp_logininfo (TRANSACT-SQL) | Microsoft Docs
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
ms.openlocfilehash: 2b3af47a1c09160faab97494d9749fd67c051cd4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67898404"
---
# <a name="xplogininfo-transact-sql"></a>xp_logininfo(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Windows 사용자와 Windows 그룹에 대한 정보를 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
xp_logininfo [ [ @acctname = ] 'account_name' ]   
     [ , [ @option = ] 'all' | 'members' ]   
     [ , [ @privilege = ] variable_name OUTPUT]  
```  
  
## <a name="arguments"></a>인수  
`[ @acctname = ] 'account_name'` Windows 사용자 또는 액세스 권한을 부여 하는 그룹의 이름인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다. *account_name* 됩니다 **sysname**, 기본값은 NULL입니다. 하는 경우 *account_name* 지정 하지 않으면에 로그인 권한을 부여 받은 모든 Windows 그룹 및 Windows 사용자가 명시적으로 보고 됩니다. *account_name* 정규화 되어야 합니다. 정규화된 이름이어야 합니다.  
  
 **'모든'**  |  **'멤버가'**  
 계정에 대한 모든 사용 권한 경로에 관한 정보를 보고할 것인지 Windows 그룹의 멤버에 관한 정보를 보고할 것인지 지정합니다. **\@옵션** 됩니다 **varchar(10)** , 기본값은 NULL입니다. 경우가 아니면 **모든** 지정, 첫 번째 권한 경로만 표시 됩니다.  
  
`[ @privilege = ] variable_name` 지정 된 Windows 계정의 권한 수준을 반환 하는 출력 매개 변수가입니다. *variable_name* 됩니다 **varchar(10)** , 'Not w'의 기본값입니다. 권한 수준을 반환 **사용자**를 **admin**, 또는 **null**합니다.  
  
 OUTPUT  
 인수를 지정 하면 *variable_name* 출력 매개 변수에서입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**계정 이름**|**sysname**|정규화된 Windows 계정 이름입니다.|  
|**type**|**char(8)**|Windows 계정의 유형입니다. 유효한 값은 **사용자** 하거나 **그룹**합니다.|  
|**privilege**|**char(9)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한입니다. 유효한 값은 **admin**를 **사용자**, 또는 **null**합니다.|  
|**매핑된 로그인 이름**|**sysname**|사용자 권한이 있는 사용자 계정에 대 한 **로그인 이름에 매핑된** 따르면 매핑된 로그인 이름을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 도메인 이름의 따른 매핑된 규칙을 사용 하 여이 계정으로 로그인 하기 전에 추가 될 때 사용 하려고 합니다.|  
|**사용 권한 경로**|**sysname**|계정 액세스 권한을 부여한 그룹 멤버 자격입니다.|  
  
## <a name="remarks"></a>설명  
 하는 경우 *account_name* 를 지정 하면 **xp_logininfo** 지정한 Windows 사용자 또는 그룹의 가장 높은 권한 수준을 보고 합니다. Windows 사용자가 시스템 관리자 및 도메인 사용자로서의 액세스 권한을 둘 다 갖고 있으면 시스템 관리자로서 보고됩니다. 사용자가 권한 수준이 같은 여러 Windows 그룹의 멤버인 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 처음 부여 받은 그룹만 보고됩니다.  
  
 하는 경우 *account_name* 유효한 Windows 사용자 또는 사용 하 여 연결 되지 않은 그룹을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 하면 빈 결과 집합이 반환 됩니다. 하는 경우 *account_name* 식별할 수 없는 유효한 Windows 사용자 또는 그룹으로 오류 메시지가 반환 됩니다.  
  
 경우 *account_name* 하 고 **모든** 는 지정 된 Windows 사용자 또는 그룹에 대 한 모든 사용 권한 경로가 반환 됩니다. 하는 경우 *account_name* 가 있는 모든 액세스 권한이 부여 된를 여러 그룹의 멤버인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], 여러 행이 반환 됩니다. **관리자** 권한 행 보다 먼저 반환 되며 합니다 **사용자** 행 권한 및 권한 내 수준 행이 반환 되는 순서에 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인이 생성 된 합니다.  
  
 하는 경우 *account_name* 하 고 **멤버** 는 지정 하면 그룹의 다음 수준 멤버 목록이 반환 됩니다. 하는 경우 *account_name* 이 로컬 그룹인 경우, 로컬 사용자, 도메인 사용자 및 그룹 목록을 포함할 수 있습니다. 하는 경우 *account_name* 도메인 계정이 도메인 사용자의 목록 이루어집니다. 그룹 멤버 자격 정보를 검색하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 도메인 컨트롤러에 연결해야 합니다. 서버에서 도메인 컨트롤러에 연결할 수 없는 경우에는 아무 정보도 반환되지 않습니다.  
  
 **xp_logininfo** 만 범용 그룹이 아니라 Active Directory 글로벌 그룹에서 정보를 반환 합니다.  
  
## <a name="permissions"></a>사용 권한  
 멤버 자격이 필요 합니다 **sysadmin** 고정 서버 역할의 멤버 자격이 **공용** 고정된 데이터베이스 역할에는 **마스터** EXECUTE 권한이 부여 된 데이터베이스.  
  
## <a name="examples"></a>예  
 다음 예제에 대 한 정보를 표시 합니다 `BUILTIN\Administrators` Windows 그룹입니다.  
  
```  
EXEC xp_logininfo 'BUILTIN\Administrators';  
```  
  
## <a name="see-also"></a>관련 항목  
 [sp_denylogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-denylogin-transact-sql.md)   
 [sp_grantlogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_revokelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [일반 확장 저장된 프로시저 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)  
  
  
