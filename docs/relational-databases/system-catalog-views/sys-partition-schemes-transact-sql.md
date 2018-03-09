---
title: sys.partition_schemes (Transact SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- partition_schemes_TSQL
- partition_schemes
- sys.partition_schemes_TSQL
- sys.partition_schemes
dev_langs: TSQL
helpviewer_keywords: sys.partition_schemes catalog view
ms.assetid: ed557fd5-12b0-4cef-9e4f-440b02e99d1f
caps.latest.revision: "37"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c77fcc9083c46921197554b256ca1af46e159e5
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2017
---
# <a name="syspartitionschemes-transact-sql"></a>sys.partition_schemes(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  파티션 구성표와 된 각 데이터 공간 마다 한 행을 포함 **형식** 구성표인  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**\<열을 상속 >**||열을 상속 [sys.data_spaces &#40; Transact SQL &#41; ](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**function_id**|**int**|구성표에서 사용되는 파티션 함수의 ID입니다.|  
  
 이 뷰가 상속 하는 열 목록은 참조 [sys.data_spaces &#40; Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md)  
  
## <a name="permissions"></a>Permissions  
 **public** 역할의 멤버 자격이 필요합니다. 자세한 내용은 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [SQL Server 시스템 카탈로그 쿼리 FAQ](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
