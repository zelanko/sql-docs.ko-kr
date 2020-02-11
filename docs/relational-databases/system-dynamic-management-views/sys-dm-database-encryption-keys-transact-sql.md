---
title: sys. dm_database_encryption_keys (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_database_encryption_keys
- sys.dm_database_encryption_keys_TSQL
- dm_database_encryption_keys
- dm_database_encryption_keys_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_database_encryption_keys dynamic management view
ms.assetid: 56fee8f3-06eb-4fff-969e-abeaa0c4b8e4
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2c66fbc1cdf98d45a7440d2def9cb3fd1be5635a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68255749"
---
# <a name="sysdm_database_encryption_keys-transact-sql"></a>sys.dm_database_encryption_keys(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  연결된 데이터베이스 암호화 키 및 데이터베이스의 암호화 상태에 대한 정보를 반환합니다. 데이터 암호화에 대한 자세한 내용은 [Transparent Data Encryption &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)를 참조하십시오.  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|데이터베이스의 ID입니다.|  
|encryption_state|**int**|데이터베이스가 암호화되었는지 여부를 나타냅니다.<br /><br /> 0 = 데이터베이스 암호화 키가 없고 암호화되지 않음<br /><br /> 1 = 암호화되지 않음<br /><br /> 2 = 암호화 진행 중<br /><br /> 3 = 암호화됨<br /><br /> 4 = 키 변경 진행 중<br /><br /> 5 = 해독 진행 중<br /><br /> 6 = 보호 변경 진행 중. 데이터베이스 암호화 키를 암호화하는 인증서 또는 비대칭 키를 변경하고 있습니다.|  
|create_date|**datetime**|암호화 키가 만들어진 날짜 (UTC)를 표시 합니다.|  
|regenerate_date|**datetime**|암호화 키를 다시 생성 한 날짜 (UTC)를 표시 합니다.|  
|modify_date|**datetime**|암호화 키가 수정 된 날짜 (UTC)를 표시 합니다.|  
|set_date|**datetime**|암호화 키가 데이터베이스에 적용 된 날짜 (UTC)를 표시 합니다.|  
|opened_date|**datetime**|데이터베이스 키가 마지막으로 열린 시간 (UTC)을 표시 합니다.|  
|key_algorithm|**nvarchar (32)**|키에 사용된 알고리즘을 표시합니다.|  
|key_length|**int**|키의 길이를 표시합니다.|  
|encryptor_thumbprint|**varbinary (20)**|암호기의 손도장을 표시합니다.|  
|encryptor_type|**nvarchar (32)**|**적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ~ [현재 버전](https://go.microsoft.com/fwlink/p/?LinkId=299658)).<br /><br /> 암호기를 설명합니다.|  
|percent_complete|**실제로**|데이터베이스 암호화 상태 변경의 완료 비율입니다. 상태 변경이 없으면 0이 됩니다.|
|encryption_state_desc|**nvarchar (32)**|**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상<br><br> 데이터베이스가 암호화 되었는지 아니면 암호화 되지 않는지를 나타내는 문자열입니다.<br><br>없음<br><br>즉<br><br>됨<br><br>DECRYPTION_IN_PROGRESS<br><br>ENCRYPTION_IN_PROGRESS<br><br>KEY_CHANGE_IN_PROGRESS<br><br>PROTECTION_CHANGE_IN_PROGRESS|
|encryption_scan_state|**int**|**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상<br><br>암호화 검색의 현재 상태를 나타냅니다. <br><br>0 = 검색이 시작 되지 않았습니다. TDE가 사용 하도록 설정 되어 있지 않습니다.<br><br>1 = 검사가 진행 중입니다.<br><br>2 = 검사가 진행 중이지만 일시 중단 되었습니다. 사용자를 다시 시작할 수 있습니다.<br><br>3 = 검사가 성공적으로 완료 되었으며 TDE가 사용 하도록 설정 되 고 암호화가 완료 되었습니다.<br><br>4 = 어떤 이유로 검사가 중단 되었으며 수동 작업이 필요 합니다. 자세한 내용은 Microsoft 지원를 문의 하세요.|
|encryption_scan_state_desc|**nvarchar (32)**|**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상<br><br>암호화 검색의 현재 상태를 나타내는 문자열입니다.<br><br> 없음<br><br>RUNNING<br><br>SUSPENDED<br><br>완료<br><br>ABORTED|
|encryption_scan_modify_date|**datetime**|**적용 대상**: [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] 이상<br><br> 암호화 검색 상태를 마지막으로 수정한 날짜 (UTC)를 표시 합니다.|
  
## <a name="permissions"></a>사용 권한

에 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]는 권한이 `VIEW SERVER STATE` 필요 합니다.   
Premium [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 계층에서는 데이터베이스에 대 `VIEW DATABASE STATE` 한 권한이 필요 합니다. [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 표준 및 기본 계층에서는 **서버 관리자** 또는 **Azure Active Directory 관리자** 계정이 필요 합니다.   

## <a name="see-also"></a>참고 항목  

 [Transact-sql&#41;&#40;보안 관련 동적 관리 뷰 및 함수](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)   
 [투명한 데이터 암호화 &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md)   
 [SQL Server 암호화](../../relational-databases/security/encryption/sql-server-encryption.md)   
 [SQL Server 및 데이터베이스 암호화 키&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/sql-server-and-database-encryption-keys-database-engine.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [Transact-sql&#41;&#40;데이터베이스 암호화 키 만들기](../../t-sql/statements/create-database-encryption-key-transact-sql.md)   
 [ALTER DATABASE ENCRYPTION KEY &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-encryption-key-transact-sql.md)   
 [DROP DATABASE ENCRYPTION KEY &#40;Transact-sql&#41;](../../t-sql/statements/drop-database-encryption-key-transact-sql.md)  
  
  
