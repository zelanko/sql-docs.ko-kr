---
description: sys.assembly_files(Transact-SQL)
title: sys. assembly_files (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.assembly_files
- assembly_files_TSQL
- assembly_files
- sys.assembly_files_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_files catalog view
ms.assetid: 1a384a2c-5556-4d12-a2ba-4da781363143
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f1e0a3b19a23cfd999ec2b4c1fc5468f53b746ee
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542696"
---
# <a name="sysassembly_files-transact-sql"></a>sys.assembly_files(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  어셈블리를 구성하는 각 파일당 한 개의 행을 포함합니다.  
    
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|이 파일이 속한 어셈블리의 ID입니다.|  
|**name**|**nvarchar(260)**|어셈블리 파일의 이름입니다.|  
|**file_id**|**int**|파일의 ID입니다. 어셈블리 내에서 고유한 ID이며 파일 ID 번호 1은 어셈블리 DLL을 나타냅니다.|  
|**content**|**varbinary(max)**|파일의 내용입니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;CLR 어셈블리 카탈로그 뷰 ](../../relational-databases/system-catalog-views/clr-assembly-catalog-views-transact-sql.md)   
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ASSEMBLYPROPERTY &#40;Transact-sql&#41;](../../t-sql/functions/assemblyproperty-transact-sql.md)  
  
  
