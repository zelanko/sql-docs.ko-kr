---
title: sys.service_contract_usages (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- service_contract_usages
- sys.service_contract_usages
- sys.service_contract_usages_TSQL
- service_contract_usages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.service_contract_usages catalog view
ms.assetid: 20af425e-1152-4a46-b1ac-94cff5fc9f02
caps.latest.revision: 29
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bb0bb4ad2002f42f42028b40e8626d515918c2d2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sysservicecontractusages-transact-sql"></a>sys.service_contract_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰에는 각 서비스-계약 쌍에 대한 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**service_id**|**int**|계약을 사용하는 서비스의 식별자입니다. NULL을 허용하지 않습니다.|  
|**service_contract_id**|**int**|서비스에서 사용하는 계약의 식별자입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
