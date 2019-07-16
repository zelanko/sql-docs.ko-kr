---
title: sysarticlecolumns (시스템 뷰) (TRANSACT-SQL) | Microsoft Docs
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
ms.openlocfilehash: 8a0505b8316254090fe5f2310fa68011d8289679
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129548"
---
# <a name="sysarticlecolumns-system-view-transact-sql"></a>sysarticlecolumns(시스템 뷰)(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **sysarticlecolumns** 뷰는 게시 된 아티클의 열에 대 한 추가 정보를 표시 합니다. 이 뷰는 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|아티클을 식별합니다.|  
|**colid**|**int**|아티클의 열을 식별합니다.|  
|**is_udt**|**int**|열이 UDT(사용자 정의 데이터 형식) 열인지 여부를 나타냅니다. 값이 **1** UDT 열을 나타냅니다.|  
|**is_xml**|**int**|열이 경우는 **xml** 열입니다. 값이 **1** 나타냅니다는 **xml** 열입니다.|  
|**is_max**|**int**|열에 큰 값 데이터 형식 열이 경우 (**varchar (max)** 를 **nvarchar (max)** 하거나 **varbinary (max)** ). 값이 **1** 큰 값 열을 나타냅니다.|  
  
## <a name="see-also"></a>관련 항목  
 [sp_articlecolumn&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
