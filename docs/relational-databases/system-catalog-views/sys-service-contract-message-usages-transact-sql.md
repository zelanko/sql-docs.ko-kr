---
title: sys.service_contract_message_usages (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- service_contract_message_usages_TSQL
- sys.service_contract_message_usages
- sys.service_contract_message_usages_TSQL
- service_contract_message_usages
dev_langs: TSQL
helpviewer_keywords: sys.service_contract_message_usages catalog view
ms.assetid: f783e662-126c-4595-8e22-f9d05191f5d0
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 011a54077a6b58420746e74ce7c39cfddaa7ffed
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="sysservicecontractmessageusages-transact-sql"></a>sys.service_contract_message_usages(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  이 카탈로그 뷰에는 각 계약-메시지 유형 쌍에 대한 행이 포함되어 있습니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**service_contract_id**|**int**|메시지 유형을 사용하는 계약의 ID입니다. NULL을 허용하지 않습니다.|  
|**message_type_id**|**int**|계약이 사용하는 메시지 유형의 ID입니다. NULL을 허용하지 않습니다.|  
|**is_sent_by_initiator**|**bit**|대화를 시작한 쪽에서 메시지 유형을 보낼 수 있습니다. NULL을 허용하지 않습니다.|  
|**is_sent_by_target**|**bit**|대화를 받는 쪽에서 메시지 유형을 보낼 수 있습니다. NULL을 허용하지 않습니다.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
  
