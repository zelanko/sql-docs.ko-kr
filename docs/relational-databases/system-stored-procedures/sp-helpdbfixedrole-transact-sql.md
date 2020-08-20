---
description: sp_helpdbfixedrole(Transact-SQL)
title: sp_helpdbfixedrole (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpdbfixedrole
- sp_helpdbfixedrole_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpdbfixedrole
ms.assetid: ad87e9a0-b901-4e37-9950-aa517d680fc3
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9f7d2518a14ba15a7cd91ea4c9a41d6710d9572e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88474087"
---
# <a name="sp_helpdbfixedrole-transact-sql"></a>sp_helpdbfixedrole(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  고정 데이터베이스 역할의 목록을 반환합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpdbfixedrole [ [ @rolename = ] 'role' ]   
```  
  
## <a name="arguments"></a>인수  
`[ @rolename = ] 'role'` 고정 데이터베이스 역할의 이름입니다. *role* 은 **sysname**이며 기본값은 NULL입니다. *Role* 을 지정 하면 해당 역할에 대 한 정보만 반환 됩니다. 그렇지 않으면 모든 고정 데이터베이스 역할에 대 한 목록 및 설명이 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 1(실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**DbFixedRole**|**sysname**|고정 데이터베이스 역할의 이름입니다.|  
|**설명**|**nvarchar (70)**|**Dbfixedrole** 에 대 한 설명입니다.|  
  
## <a name="remarks"></a>설명  
 다음 표에 표시된 것과 같이 고정 데이터베이스 역할은 데이터베이스 수준에서 정의되며 특정 데이터베이스 수준의 관리 작업을 수행할 수 있는 사용 권한이 있습니다. 고정 데이터베이스 역할은 추가하거나 제거할 수 없습니다. 고정 데이터베이스 역할에 부여된 사용 권한은 변경할 수 없습니다.  
  
|고정 데이터베이스 역할|Description|  
|-------------------------|-----------------|  
|**db_owner**|데이터베이스 소유자입니다.|  
|**db_accessadmin**|데이터베이스 액세스 관리자입니다.|  
|**db_securityadmin**|데이터베이스 보안 관리자입니다.|  
|**db_ddladmin**|데이터베이스 DDL 관리자입니다.|  
|**db_backupoperator**|데이터베이스 백업 운영자입니다.|  
|**db_datareader**|데이터베이스의 데이터 판독기입니다.|  
|**db_datawriter**|데이터베이스의 데이터 기록기입니다.|  
|**db_denydatareader**|데이터베이스의 거부 데이터 판독기입니다.|  
|**db_denydatawriter**|데이터베이스의 거부 데이터 기록기입니다.|  
  
 다음 표에서는 데이터베이스 역할을 수정하는 데 사용되는 저장 프로시저를 보여 줍니다.  
  
|저장 프로시저|작업|  
|----------------------|------------|  
|**sp_addrolemember**|고정 데이터베이스 역할에 데이터베이스 사용자를 추가합니다.|  
|**sp_helprole**|고정 데이터베이스 역할의 멤버 목록을 표시합니다.|  
|**sp_droprolemember**|고정 데이터베이스 역할에서 멤버를 제거합니다.|  
  
## <a name="permissions"></a>사용 권한  
 **public** 역할의 멤버 자격이 필요합니다.  
  
 반환되는 정보는 메타데이터에 대한 액세스 제한 사항에 따라 달라집니다. 보안 주체에 사용 권한이 없는 엔터티는 나타나지 않습니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="examples"></a>예제  
 다음 예에서는 모든 고정 데이터베이스 역할의 목록을 보여 줍니다.  
  
```  
EXEC sp_helpdbfixedrole;  
GO  
```  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;보안 저장 프로시저 ](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [Transact-sql&#41;sp_addrolemember &#40;](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)   
 [Transact-sql&#41;sp_dbfixedrolepermission &#40;](../../relational-databases/system-stored-procedures/sp-dbfixedrolepermission-transact-sql.md)   
 [Transact-sql&#41;sp_droprolemember &#40;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [Transact-sql&#41;sp_helprole &#40;](../../relational-databases/system-stored-procedures/sp-helprole-transact-sql.md)   
 [Transact-sql&#41;sp_helprolemember &#40;](../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
