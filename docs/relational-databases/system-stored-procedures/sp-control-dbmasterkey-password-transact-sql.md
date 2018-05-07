---
title: sp_control_dbmasterkey_password (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_control_dbmasterkey_password
- sp_control_dbmasterkey_password_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_control_dbmasterkey_password
ms.assetid: 63979a87-42a2-446e-8e43-30481faaf3ca
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: a9894a10965affbd65406276445f6c84f05ce76e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/04/2018
---
# <a name="spcontroldbmasterkeypassword-transact-sql"></a>sp_control_dbmasterkey_password(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터베이스 마스터 키를 여는 데 필요한 암호가 포함된 자격 증명을 추가 또는 삭제합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_control_dbmasterkey_password @db_name = 'database_name,  
     @password = 'master_key_password' , @action = { 'add' | 'drop' }  
```  
  
## <a name="arguments"></a>인수  
 @db_name=N'*database_name*'  
 이 자격 증명에 연결된 데이터베이스의 이름을 지정합니다. 시스템 데이터베이스일 수 없습니다. *a s e _* 은 **nvarchar**합니다.  
  
 @password= N'*암호*'  
 마스터 키의 암호를 지정합니다. *암호* 은 **nvarchar**합니다.  
  
 @action= N'add'  
 지정된 데이터베이스에 대한 자격 증명이 자격 증명 저장소에 추가되도록 지정합니다. 자격 증명에는 데이터베이스 마스터 키의 암호가 포함됩니다. 에 전달 된 값 @action 은 **nvarchar**합니다.  
  
 @action=N'drop'  
 지정된 데이터베이스에 대한 자격 증명이 자격 증명 저장소에서 삭제되도록 지정합니다. 에 전달 된 값 @action 은 **nvarchar**합니다.  
  
## <a name="remarks"></a>주의  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 키 암호화 및 암호 해독을 위한 데이터베이스 마스터 키가 필요한 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 인스턴스의 서비스 마스터 키로 데이터베이스 마스터 키의 암호를 해독하려고 시도합니다. 암호 해독에 실패하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]는 마스터 키가 필요한 데이터베이스와 패밀리 GUID가 동일한 마스터 키 자격 증명을 자격 증명 저장소에서 검색합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 암호 해독이 성공하거나 남은 자격 증명이 없을 때까지 일치하는 각 자격 증명을 사용하여 데이터베이스 마스터 키의 암호화를 해독하려고 시도합니다.  
  
> [!CAUTION]  
>  sa 및 기타 고급 권한의 서버 보안 주체에서 액세스할 수 없어야 하는 데이터베이스에 대해서는 마스터 키 자격 증명을 만들지 마십시오. 서비스 마스터 키로 키 계층을 해독할 수 없도록 데이터베이스를 구성할 수 있습니다. 이 옵션은 sa 또는 기타 상위 권한 서버 보안 주체에서 액세스할 수 없어야 하는 암호화된 정보가 포함된 데이터베이스를 방어하기 위한 수단으로 지원됩니다. 이러한 데이터베이스에 대해 마스터 키 자격 증명을 만들면 이러한 방어 수단이 무력화되어 sa 및 기타 상위 권한 서버 보안 주체에서 데이터베이스를 암호 해독할 수 있습니다.  
  
 Sp_control_dbmasterkey_password를 사용 하 여 만든 자격 증명에 표시 되는 [sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) 카탈로그 뷰에 있습니다. 데이터베이스 마스터 키에 대해 만든 자격 증명의 이름은 `##DBMKEY_<database_family_guid>_<random_password_guid>##` 형식입니다. 암호는 자격 증명 암호로 저장됩니다. 자격 증명 저장소에 추가된 각 암호의 경우 sys.credentials에 관련 행이 있습니다.  
  
 master, model, msdb 또는 tempdb 시스템 데이터베이스에 대해서는 sp_control_dbmasterkey_password를 사용하여 자격 증명을 만들 수 없습니다.  
  
 sp_control_dbmasterkey_password로는 암호를 사용하여 지정된 데이터베이스의 마스터 키를 열 수 있는지 여부를 확인할 수 없습니다.  
  
 지정된 데이터베이스에 대한 자격 증명에 이미 저장되어 있는 암호를 지정하면 sp_control_dbmasterkey_password가 실패합니다.  
  
> [!NOTE]  
>  다른 서버 인스턴스에 있는 두 데이터베이스는 같은 패밀리 GUID를 공유할 수 있습니다. 이 경우 데이터베이스는 자격 증명 저장소에서 동일한 마스터 키 레코드를 공유합니다.  
  
 sp_control_dbmasterkey_password에 전달된 매개 변수는 추적에 표시되지 않습니다.  
  
> [!NOTE]  
>  sp_control_dbmasterkey_password로 추가한 자격 증명을 사용하여 데이터베이스 마스터 키를 여는 경우 데이터베이스 마스터 키는 서비스 마스터 키에 의해 다시 암호화됩니다. 데이터베이스가 읽기 전용 모드인 경우 재암호화 작업이 실패하고 데이터베이스 마스터 키가 암호화되지 않은 상태로 남습니다. 이후에 데이터베이스 마스터 키에 액세스하려면 OPEN MASTER KEY 문과 암호를 사용해야 합니다. 암호를 사용하지 않아도 되도록 하려면 데이터베이스를 읽기 전용 모드로 전환하기 전에 자격 증명을 만들어야 합니다.  
  
 **이전 버전과 호환성 문제 잠재적인:** 현재 저장된 프로시저는 확인 하지는 마스터 키가 있는지 여부를 합니다. 이전 버전과의 호환성을 위해 허용되지만 경고가 표시됩니다. 이 기능은 더 이상 지원되지 않습니다. 이후 릴리스에서 마스터 키가 있어야 하 고 저장된 프로시저에 사용 되는 암호에 **sp_control_dbmasterkey_password** 데이터베이스 마스터 키를 암호화 하는 데 사용 된 암호 중 하 나와 동일 해야 합니다.  
  
## <a name="permissions"></a>Permissions  
 데이터베이스에 대한 CONTROL 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="a-creating-a-credential-for-the-adventureworks2012-master-key"></a>1. AdventureWorks2012 마스터 키에 대한 자격 증명 만들기  
 다음 예에서는 `AdventureWorks2012` 데이터베이스 마스터 키에 대한 자격 증명을 만들고 마스터 키 암호를 자격 증명에 암호로 저장합니다. 때문에 전달 되는 모든 매개 변수 `sp_control_dbmasterkey_password` 데이터 형식 이어야 합니다 **nvarchar**, 캐스팅 연산자와 함께 텍스트 변환 됩니다 `N`합니다.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'add';  
GO  
```  
  
### <a name="b-dropping-a-credential-for-a-database-master-key"></a>2. 데이터베이스 마스터 키에 대한 자격 증명 삭제  
 다음 예에서는 예 1에서 만든 자격 증명을 삭제합니다. 여기에는 암호를 포함한 모든 매개 변수가 필요합니다.  
  
```  
EXEC sp_control_dbmasterkey_password @db_name = N'AdventureWorks2012',   
    @password = N'sdfjlkj#mM00sdfdsf98093258jJlfdk4', @action = N'drop';  
GO  
```  
  
## <a name="see-also"></a>관련 항목:  
 [암호화된 미러 데이터베이스 설정](../../database-engine/database-mirroring/set-up-an-encrypted-mirror-database.md)   
 [Security Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sys.credentials&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)   
 [자격 증명&#40;데이터베이스 엔진&#41;](../../relational-databases/security/authentication-access/credentials-database-engine.md)  
  
  
