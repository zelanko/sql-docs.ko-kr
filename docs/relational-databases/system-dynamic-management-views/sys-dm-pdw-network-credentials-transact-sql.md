---
title: sys.dm_pdw_network_credentials (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.component: dmv's
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f782d832dc5f3d962fcfc7aa72b1fa196159312d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  에 저장 된 모든 네트워크 자격 증명 목록을 반환은 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 기기 모든 대상 서버에 있습니다. 결과 제어 노드에 및 모든 계산 노드에 나열 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
|target_server_name|**nvarchar(32)**|대상 서버의 IP 주소는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용자 이름 및 암호 자격 증명을 사용 하 여 액세스 합니다.|  
|username|**nvarchar(32)**|사용자 이름 암호 저장 됩니다.|  
|last_modified|**datetime**|자격 증명을 수정 하는 마지막 작업 날짜/시간입니다.|  
  
## <a name="permissions"></a>Permissions  
 서버 상태 보기를 필요합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 동적 관리 뷰에 대 한 키가 *pdw_node_id* 플러스 *target_server_name*합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [SQL 데이터 웨어하우스 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
