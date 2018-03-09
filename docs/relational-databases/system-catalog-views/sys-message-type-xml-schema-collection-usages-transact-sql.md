---
title: sys.message_type_xml_schema_collection_usages (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- message_type_xml_schema_collection_usages_TSQL
- sys.message_type_xml_schema_collection_usages_TSQL
- sys.message_type_xml_schema_collection_usages
- message_type_xml_schema_collection_usages
dev_langs: TSQL
helpviewer_keywords: sys.message_type_xml_schema_collection_usages catalog view
ms.assetid: 544f61a1-c7b7-44b4-bf8d-980ba87d0665
caps.latest.revision: "13"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 86727e43d590f5c7fd8c73759ceab95b865d521f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="sysmessagetypexmlschemacollectionusages-transact-sql"></a>sys.message_type_xml_schema_collection_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰는 XML 스키마 컬렉션이 유효성을 검사하는 각 서비스 메시지 유형에 대해 행을 반환합니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**message_type_id**|**int**|서비스 메시지 유형의 ID입니다. NULL을 허용하지 않습니다.|  
|**xml_collection_id**|**int**|유효성을 검사하는 XML 스키마 네임스페이스를 포함하는 컬렉션의 ID입니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
