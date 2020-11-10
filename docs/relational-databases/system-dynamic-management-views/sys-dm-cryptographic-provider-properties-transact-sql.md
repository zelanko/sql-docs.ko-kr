---
description: sys.dm_cryptographic_provider_properties(Transact-SQL)
title: sys.dm_cryptographic_provider_properties (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_cryptographic_provider_properties_TSQL
- sys.dm_cryptographic_provider_properties
- sys.dm_cryptographic_provider_properties_TSQL
- dm_cryptographic_provider_properties
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cryptographic_provider_properties dynamic management view
ms.assetid: 024b0095-6766-4189-a39a-d316c5ec2874
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 419793e94cc85a8dba1e29f4b79694820518eaad
ms.sourcegitcommit: 49ee3d388ddb52ed9cf78d42cff7797ad6d668f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2020
ms.locfileid: "94384677"
---
# <a name="sysdm_cryptographic_provider_properties-transact-sql"></a>sys.dm_cryptographic_provider_properties(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  등록된 암호화 공급자에 대한 정보를 반환합니다.  
  
 
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|provider_id|**int**|암호화 공급자의 ID 번호입니다.|  
|guid|**uniqueidentifier**|고유한 공급자 GUID입니다.|  
|provider_version|**nvarchar(256)**|' *Aa.bb.cccc.dd* ' 형식의 공급자 버전입니다.|  
|sqlcrypt_version|**nvarchar(256)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]' *Aa.bb.cccc.dd* ' 형식으로 된 암호화 API의 주 버전입니다.|  
|friendly_name|**nvarchar(2048)**|공급자가 제공한 이름입니다.|  
|authentication_type|**nvarchar(256)**|WINDOWS, BASIC 또는 OTHER입니다.|  
|symmetric_key_support|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|symmetric_key_export|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|symmetric_key_import|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|symmetric_key_persistance|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|asymmetric_key_support|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|asymmetric_key_export|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|symmetric_key_import|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
|symmetric_key_persistance|**tinyint**|0(지원되지 않음)<br /><br /> 1(지원됨)|  
  
## <a name="permissions"></a>권한  
 **Sys.dm_cryptographic_provider_properties** 뷰는 public에 표시 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [보안 카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)   
 [확장 가능 키 관리 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)   
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](../../t-sql/statements/create-cryptographic-provider-transact-sql.md)   
 [보안 관련 동적 관리 뷰 및 함수&#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
