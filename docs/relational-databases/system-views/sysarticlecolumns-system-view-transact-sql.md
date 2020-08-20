---
description: sysarticlecolumns(시스템 뷰)(Transact-SQL)
title: sysarticlecolumns (시스템 뷰) (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1a6e359aa7f6c0e7efc4090152b152ab1bfb6fbc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460291"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns(시스템 뷰)(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **Sysarticlecolumns** 뷰는 게시 된 아티클의 열에 대 한 추가 정보를 제공 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클을 식별합니다.|  
|**id**|**int**|아티클의 열을 식별합니다.|  
|**is_udt**|**int**|열이 UDT(사용자 정의 데이터 형식) 열인지 여부를 나타냅니다. 값 **1** 은 UDT 열을 나타냅니다.|  
|**is_xml**|**int**|열이 **xml** 열인지 여부입니다. 값 **1** 은 **xml** 열을 나타냅니다.|  
|**is_max**|**int**|열이 많은 값 데이터 형식 열 (**varchar (max)**, **nvarchar (max)** 또는 **varbinary (max)**) 인지 여부입니다. 값 **1** 은 많은 값 열을 나타냅니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;sp_articlecolumn &#40;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
