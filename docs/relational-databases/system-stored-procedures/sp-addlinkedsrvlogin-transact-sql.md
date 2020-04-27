---
title: sp_addlinkedsrvlogin (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlinkedsrvlogin_TSQL
- sp_addlinkedsrvlogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlinkedsrvlogin
ms.assetid: eb69f303-1adf-4602-b6ab-f62e028ed9f6
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 1bf39a9a1262f30e3c0bbd6fd2ea5892a55540dd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "68072675"
---
# <a name="sp_addlinkedsrvlogin-transact-sql"></a>sp_addlinkedsrvlogin(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로컬 인스턴스의 로그인과 원격 서버 보안 계정 간의 매핑을 만들거나 업데이트합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
sp_addlinkedsrvlogin [ @rmtsrvname = ] 'rmtsrvname'   
     [ , [ @useself = ] { 'TRUE' | 'FALSE' | NULL } ]   
     [ , [ @locallogin = ] 'locallogin' ]   
     [ , [ @rmtuser = ] 'rmtuser' ]   
     [ , [ @rmtpassword = ] 'rmtpassword' ]   
```  
  
## <a name="arguments"></a>인수  
 `[ @rmtsrvname = ] 'rmtsrvname'`  
 로그인 매핑이 적용되는 연결된 서버의 이름입니다. *rmtsrvname* 는 **sysname**이며 기본값은 없습니다.  
  
 `[ @useself = ] { 'TRUE' | 'FALSE' | NULL }'`  
 로컬 로그인을 가장 하거나 로그인과 암호를 명시적으로 제출 하 여 *rmtsrvname* 에 연결할지 여부를 결정 합니다. 데이터 형식은 **varchar (** 8 **)** 이며 기본값은 TRUE입니다.  
  
 TRUE 값은 로그인이 자체 자격 증명을 사용 하 여 *rmtsrvname*에 연결 하도록 지정 합니다. 여기서 *rmtuser* 및 *rmtuser* 인수는 무시 됩니다. FALSE 지정 된 *locallogin*에 대해 *rmtsrvname* 에 연결 하는 데 *rmtuser* 및 *rmtuser* 인수를 사용 하도록 지정 합니다. *Rmtuser* 및 *RMTUSER* 도 NULL로 설정 된 경우 연결 된 서버에 연결 하는 데 로그인 또는 암호가 사용 되지 않습니다.  
  
 `[ @locallogin = ] 'locallogin'`  
 로컬 서버의 로그인입니다. *locallogin* 은 **sysname**이며 기본값은 NULL입니다. NULL은 *rmtsrvname*에 연결 하는 모든 로컬 로그인에이 항목이 적용 되도록 지정 합니다. NULL이 아닌 경우 *locallogin* 은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 Windows 로그인 일 수 있습니다. Windows 로그인은 직접적인 방법으로든 또는 액세스 권한이 있는 Windows 그룹의 멤버 자격을 이용한 방법으로든 반드시 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 대한 액세스 권한을 보유해야 합니다.  
  
 `[ @rmtuser = ] 'rmtuser'`  
 가 FALSE 인 경우 @useself *rmtsrvname* 에 연결 하는 데 사용 되는 원격 로그인입니다. 원격 서버가 Windows 인증을 사용 하지 않는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스인 경우 *rmtuser* 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인입니다. *rmtuser* 는 **sysname**이며 기본값은 NULL입니다.  
  
 `[ @rmtpassword = ] 'rmtpassword'`  
 *Rmtuser*와 연결 된 암호입니다. *rmtpassword* 는 **sysname**이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="remarks"></a>설명  
 사용자가 로컬 서버에 로그온하여 연결된 서버의 테이블에 액세스하는 분산 쿼리를 실행하는 경우 로컬 서버는 반드시 해당 테이블에 액세스하는 사용자를 대신하여 연결된 서버에 로그온해야 합니다. 로컬 서버가 연결된 서버에 로그온할 때 사용할 로그인 자격 증명을 지정하려면 sp_addlinkedsrvlogin을 사용합니다.  
  
> [!NOTE]  
>  연결된 서버의 테이블을 사용하여 최적의 쿼리 계획을 만들려면 연결된 서버로부터의 데이터 분포 통계를 쿼리 프로세서가 가지고 있어야 합니다. 테이블의 열에 대해 제한된 사용 권한을 가진 사용자는 유용한 모든 통계를 가져올 권한이 없으므로 덜 효율적인 쿼리 계획을 받게 되어 성능 저하 문제를 겪을 수 있습니다. 연결된 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스라면 사용자는 모든 사용 가능한 통계를 얻기 위해 해당 테이블의 소유자 또는 연결된 서버에서 sysadmin 고정 서버 역할, db_owner 고정 데이터베이스 역할 또는 db_ddladmin 고정 데이터베이스 역할의 멤버여야 합니다. SQL Server 2012 SP1에서는 통계를 가져오기 위해 권한 제한을 수정하여 사용자가 SELECT 권한을 사용하여 DBCC SHOW_STATISTICS를 통해 통계에 액세스할 수 있게 되었습니다. 자세한 내용은 [transact-sql&#41;&#40;DBCC SHOW_STATISTICS ](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)의 사용 권한 섹션을 참조 하세요.  
  
 sp_addlinkedserver를 실행하면 로컬 서버의 모든 로그인과 연결된 서버의 원격 로그인 간의 기본 매핑이 자동으로 생성됩니다. 기본 매핑은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 로컬 로그인 대신 연결된 서버에 연결할 때 해당 로그인의 사용자 자격 증명을 사용함을 나타냅니다. 이는 로컬 사용자 이름을 지정 하지 @useself 않고 연결 된 서버에 대해를 **true** 로 설정 하 여 sp_addlinkedsrvlogin를 실행 하는 것과 같습니다. 기본 매핑을 변경하거나 특정 로컬 로그인에 새 매핑을 추가하는 경우에만 sp_addlinkedsrvlogin을 사용합니다. 기본 매핑 또는 다른 매핑을 삭제하려면 sp_droplinkedsrvlogin을 사용합니다.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 sp_addlinkedsrvlogin을 사용하여 미리 지정된 로그인 매핑을 만드는 대신 다음 조건이 모두 충족될 때 쿼리를 실행하는 사용자의 Windows 보안 자격 증명(Windows 로그인 이름 및 암호)을 사용하여 연결된 서버에 자동으로 연결할 수 있습니다.  
  
-   사용자가 Windows 인증 모드를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결합니다.  
  
-   클라이언트 및 보내는 서버에서 보안 계정 위임을 사용할 수 있습니다.  
  
-   공급자가 Windows에서 실행되는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우와 같이 Windows 인증 모드를 지원합니다.  
  
> [!NOTE]  
>  단일 홉 시나리오에는 위임을 사용할 필요가 없지만 다중 홉 시나리오에는 위임이 필요합니다.  
  
 연결된 서버가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에서 sp_addlinkedsrvlogin을 실행하여 정의된 매핑을 사용하여 인증을 수행하면 이후 로컬 서버가 아니라 연결된 서버에 의해 원격 데이터베이스의 개별 개체에 대한 사용 권한이 결정됩니다.  
  
 사용자 정의 트랜잭션 내에서는 sp_addlinkedsrvlogin을 실행할 수 없습니다.  
  
## <a name="permissions"></a>사용 권한  
 서버에 대한 ALTER ANY LOGIN 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-connecting-all-local-logins-to-the-linked-server-by-using-their-own-user-credentials"></a>A. 자체 사용자 자격 증명을 사용하여 연결된 서버에 모든 로컬 로그인 연결  
 다음 예에서는 로컬 서버의 모든 로그인이 자체 사용자 자격 증명을 사용하여 `Accounts` 연결된 서버에 연결되도록 하는 매핑을 만듭니다.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts';  
```  
  
 Or  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'true';  
```  
  
> [!NOTE]  
>  개별 로그인에 대해 생성된 명시적 매핑이 있는 경우 이 매핑은 해당 연결된 서버에 존재할 수 있는 모든 전역 매핑보다 우선합니다.  
  
### <a name="b-connecting-a-specific-login-to-the-linked-server-by-using-different-user-credentials"></a>B. 다른 사용자 자격 증명을 사용하여 연결된 서버에 특정 로그인 연결  
 다음 예에서는 `Domain\Mary` Windows 사용자가 `Accounts` 로그인과 `MaryP` 암호를 사용하여 `d89q3w4u` 연결된 서버로 연결되도록 하는 매핑을 만듭니다.  
  
```  
EXEC sp_addlinkedsrvlogin 'Accounts', 'false', 'Domain\Mary', 'MaryP', 'd89q3w4u';  
```  
  
> [!IMPORTANT]  
>  이 예에서는 Windows 인증을 사용하지 않습니다. 암호는 암호화되지 않은 상태로 전송됩니다. 암호는 디스크, 백업 및 로그 파일에 저장되는 데이터 원본 정의와 스크립트에 표시될 수 있습니다. 따라서 이러한 유형의 연결에는 관리자 암호를 사용하지 마십시오. 사용자의 환경과 관련된 보안 지침에 대해서는 해당 네트워크 관리자에게 문의하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [연결 된 서버 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [Transact-sql&#41;sp_addlinkedserver &#40;](../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)   
 [Transact-sql&#41;sp_droplinkedsrvlogin &#40;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
