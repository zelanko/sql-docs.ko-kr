---
title: sys. server_sql_modules (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.server_sql_modules
- sys.server_sql_modules_TSQL
- server_sql_modules_TSQL
- server_sql_modules
dev_langs:
- TSQL
helpviewer_keywords:
- sys.server_sql_modules catalog view
ms.assetid: 9ef9a8b9-c470-4a61-b0c4-ee24ad871d63
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 23c8596a1dc2d4cfa75f01b123d1f11cffcfe546
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882940"
---
# <a name="sysserver_sql_modules-transact-sql"></a>sys.server_sql_modules(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  TR 유형의 서버 수준 트리거에 대한 SQL 모듈 집합을 포함합니다. 이 관계를 sys.server_triggers에 조인할 수 있습니다. 튜플(object_id)은 관계의 키입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|해당 모듈이 정의된 서버 수준 트리거에 대한 FOREIGN KEY 참조입니다.|  
|**정의**|**nvarchar(max)**|이 모듈을 정의하는 SQL 텍스트입니다.<br /><br /> NULL = 암호화됨|  
|**uses_ansi_nulls**|**bit**|ANSI NULLS 설정 옵션을 ON으로 설정하여 모듈을 만들었습니다.|  
|**uses_quoted_identifier**|**bit**|QUOTED IDENTIFIER 설정 옵션을 ON으로 설정하여 모듈을 만들었습니다.|  
|**execute_as_principal_id**|**int**|EXECUTE AS 서버 보안 주체의 ID입니다.<br /><br /> 기본값은 NULL이며 EXECUTE AS CALLER인 경우에도 NULL입니다.<br /><br /> EXECUTE as SELF as SELF as principal-2 = EXECUTE AS OWNER 인 경우 지정 된 보안 주체의 ID입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
