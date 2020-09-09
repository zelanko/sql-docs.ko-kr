---
description: sys.services(Transact-SQL)
title: sys.debug (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.services
- services
- services_TSQL
- sys.services_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.services catalog view
ms.assetid: 16d0b0c5-5cce-469b-aa3d-4b9248e0c085
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 27653c3cbc38f8d7cd2bdc46c4800fd3db4067db
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539519"
---
# <a name="sysservices-transact-sql"></a>sys.services(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 카탈로그 뷰에는 데이터베이스의 각 서비스에 대한 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|데이터베이스 내에서 고유한 서비스의 이름이며 대/소문자를 구분합니다. NULL을 허용하지 않습니다.|  
|**service_id**|**int**|서비스의 ID입니다. NULL을 허용하지 않습니다.|  
|**principal_id**|**int**|이 서비스를 소유한 데이터베이스 보안 주체의 식별자입니다. NULL을 허용합니다.|  
|**service_queue_id**|**int**|이 서비스에서 사용하는 큐의 개체 ID입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>사용 권한  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
