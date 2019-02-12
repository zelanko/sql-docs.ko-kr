---
title: sys.dm_pdw_network_credentials (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7d9e18284ac4d97efaa217802682fe79ebb2dfc5
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56041524"
---
# <a name="sysdmpdwnetworkcredentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  에 저장 된 모든 네트워크 자격 증명의 목록을 반환 합니다 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 모든 대상 서버에 대 한 어플라이언스입니다. 제어 노드 및 모든 계산 노드에 대 한 결과가 나열 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
|target_server_name|**nvarchar(32)**|대상 서버의 IP 주소는 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용자 이름 및 암호 자격 증명을 사용 하 여 액세스 됩니다.|  
|username|**nvarchar(32)**|사용자 이름 암호 저장 됩니다.|  
|last_modified|**datetime**|자격 증명을 수정 하는 마지막 작업 날짜/시간입니다.|  
  
## <a name="permissions"></a>사용 권한  
 VIEW SERVER STATE 필요합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 동적 관리 뷰에 대 한 키는 *pdw_node_id* plus *target_server_name*합니다.  
  
## <a name="see-also"></a>관련 항목  
 [SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
