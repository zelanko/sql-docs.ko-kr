---
title: sp_helplogins (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helplogins_TSQL
- sp_helplogins
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helplogins
ms.assetid: f9ad3767-5b9f-420d-8922-b637811404f7
caps.latest.revision: 22
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 9ac0fd9a5fb29f63267c2bb42902341e926bd523
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sphelplogins-transact-sql"></a>sp_helplogins(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  각 데이터베이스의 로그인 및 연관된 사용자에 관한 정보를 제공합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helplogins [ [ @LoginNamePattern = ] 'login' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@LoginNamePattern =** ] **'***login***'**  
 로그인 이름입니다. *login*은 **sysname**이며 기본값은 NULL입니다. *로그인* 지정 된 경우 존재 해야 합니다. 경우 *로그인* 은 지정 하지 않으면 모든 로그인에 대 한 정보가 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
 다음 표에서 볼 수 있듯이 첫 번째 보고서에는 지정한 각 로그인에 관한 정보가 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|로그인 이름입니다.|  
|**SID**|**varbinary(85)**|로그인 SID(보안 ID)입니다.|  
|**DefDBName**|**sysname**|기본 데이터베이스입니다 **LoginName** 의 인스턴스로 연결할 때 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**DefLangName**|**sysname**|기본 언어에서 사용 하는 **LoginName**합니다.|  
|**하는지 여부가 결정**|**char (5)**|Yes = **LoginName** 데이터베이스에 연결 된 사용자 이름이 있습니다.<br /><br /> 더 = **LoginName** 연관된 된 사용자 이름을 없습니다.|  
|**ARemote**|**char (7)**|Yes = **LoginName** 연관된 된 원격 로그인 했습니다.<br /><br /> 더 = **LoginName** 연결된 된 로그인이 없습니다.|  
  
 두 번째 보고서에는 다음 표와 같이 각 로그인에 매핑된 사용자와 해당 로그인의 역할 멤버 자격에 관한 정보가 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|로그인 이름입니다.|  
|**DBName**|**sysname**|기본 데이터베이스입니다 **LoginName** 의 인스턴스로 연결할 때 사용 하 여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.|  
|**UserName**|**sysname**|사용자 계정이 **LoginName** 에 결과를 매핑할 **DBName**, 역할 및는 **LoginName** 에서의 멤버인 **DBName**합니다.|  
|**UserOrAlias**|**char(8)**|MemberOf = **UserName** 는 역할입니다.<br /><br /> 사용자 = **UserName** 사용자 계정입니다.|  
  
## <a name="remarks"></a>주의  
 로그인을 제거 하기 전에 사용 하 여 **sp_helplogins** 로그인에 매핑된 사용자 계정을 식별할 수 있습니다.  
  
## <a name="permissions"></a>Permissions  
 멤버 자격이 필요는 **securityadmin** 고정된 서버 역할입니다.  
  
 지정 된 로그인에 매핑된 모든 사용자 계정을 확인 하려면 **sp_helplogins** 서버 내에서 모든 데이터베이스를 확인 해야 합니다. 따라서 서버의 각 데이터베이스에 대해 다음 조건 중 최소한 하나를 만족해야 합니다.  
  
-   실행 중인 사용자 **sp_helplogins** 데이터베이스에 액세스할 수 있는 권한이 있습니다.  
  
-   **게스트** 사용자 계정이 데이터베이스에 사용 되어야 합니다.  
  
 경우 **sp_helplogins** 는 데이터베이스에 액세스할 수 없는 **sp_helplogins** 고 오류 메시지 15622를 표시 한 많은 정보를 반환 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 `John`이라는 로그인에 대한 정보를 보고합니다.  
  
```  
EXEC sp_helplogins 'John';  
GO  
  
LoginName SID                        DefDBName DefLangName AUser ARemote   
--------- -------------------------- --------- ----------- ----- -------   
John      0x23B348613497D11190C100C  master    us_english  yes   no  
  
(1 row(s) affected)  
  
LoginName   DBName   UserName   UserOrAlias   
---------   ------   --------   -----------   
John        pubs     John       User          
  
(1 row(s) affected)  
```  
  
## <a name="see-also"></a>관련 항목:  
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_helpdb &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
