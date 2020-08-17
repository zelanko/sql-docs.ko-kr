---
description: sys.key_encryptions(Transact-SQL)
title: sys. key_encryptions (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.key_encryptions
- key_encryptions_TSQL
- sys.key_encryptions_TSQL
- key_encryptions
dev_langs:
- TSQL
helpviewer_keywords:
- sys.key_encryptions catalog view
ms.assetid: c39cecf8-af63-40b9-98e5-f84a5bf3ae54
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c2c8f8126e3b9a1216e30801dc1d23be5b74cd48
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88377829"
---
# <a name="syskey_encryptions-transact-sql"></a>sys.key_encryptions(Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  CREATE SYMMETRIC KEY 문의 ENCRYPTION BY 절을 사용하여 지정된 각 대칭 키 암호화에 대해 행을 반환합니다.  

  
|열 이름|데이터 형식|설명|  
|------------------|----------------|-----------------|  
|**key_id**|**int**|암호화된 키의 ID입니다.|  
|**n**|**varbinary(32)**|키 암호화에 사용되는 인증서의 SHA-1 해시이거나 대칭 키의 GUID입니다.|  
|**crypt_type**|**char (4)**|암호화 유형입니다.<br /><br /> ESKS = 대칭 키를 사용한 암호화<br /><br /> ESKP, ESP2 또는 ESP3 = 암호로 암호화<br /><br /> EPUC = 인증서를 사용한 암호화<br /><br /> EPUA = 비대칭 키를 사용한 암호화<br /><br /> ESKM = 마스터 키를 사용한 암호화|  
|**crypt_type_desc**|**nvarchar(60)**|암호화 유형의 설명입니다.<br /><br /> ENCRYPTION BY SYMMETRIC KEY<br /><br /> ENCRYPTION BY PASSWORD <br />(부터 [!INCLUDE[sssqlv14_md](../../includes/sssqlv14-md.md)] 는 CSS에서 사용할 버전 번호를 포함 합니다.)<br /><br /> ENCRYPTION BY CERTIFICATE<br /><br /> ENCRYPTION BY ASYMMETRIC KEY<br /><br /> ENCRYPTION BY MASTER KEY<br /><br /> 참고: Windows DPAPI는 서비스 마스터 키를 보호 하는 데 사용 됩니다.|  
|**crypt_property**|**varbinary(max)**|부호 있는 비트 또는 암호화된 비트입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
