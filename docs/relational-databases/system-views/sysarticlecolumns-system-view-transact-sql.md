---
title: sysarticlecolumns (시스템 뷰) (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns view
ms.assetid: a8dd8d13-c827-45c4-87ba-802725301382
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 85ed85bcff82f44fa4522dbcd65e4d1d2d4a8fcc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33010500"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns(시스템 뷰)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **sysarticlecolumns** 뷰는 게시 된 문서에서 열에 대 한 추가 정보를 표시 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클을 식별합니다.|  
|**colid**|**int**|아티클의 열을 식별합니다.|  
|**is_udt**|**int**|열이 UDT(사용자 정의 데이터 형식) 열인지 여부를 나타냅니다. 값이 **1** UDT 열을 나타냅니다.|  
|**is_xml**|**int**|열이 되는 **xml** 열입니다. 값이 **1** 나타냅니다는 **xml** 열입니다.|  
|**is_max**|**int**|열에 큰 값 데이터 형식 열이 됩니다 (**varchar (max)**, **nvarchar (max)** 또는 **varbinary (max)**). 값이 **1** 큰 값 열을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [sp_articlecolumn&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
