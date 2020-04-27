---
title: sys. dm_pdw_network_credentials (Transact-sql) | Microsoft Docs
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
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: b75eb53da9961025e3310f27e4a12608dd4fda78
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899357"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys. dm_pdw_network_credentials (Transact-sql)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  모든 대상 서버에 대해 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 어플라이언스에 저장 된 모든 네트워크 자격 증명의 목록을 반환 합니다. 결과는 제어 노드 및 모든 계산 노드에 대해 나열 됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
|target_server_name|**nvarchar(32)**|사용자 이름 및 암호 자격 증명을 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] 사용 하 여에 액세스 하는 대상 서버의 IP 주소입니다.|  
|username|**nvarchar(32)**|암호가 저장 되는 사용자 이름입니다.|  
|last_modified|**datetime**|자격 증명을 수정한 마지막 작업의 날짜/시간입니다.|  
  
## <a name="permissions"></a>사용 권한  
 뷰 서버 상태가 필요 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 동적 관리 뷰의 키는 *pdw_node_id* 및 *target_server_name*입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;SQL Data Warehouse 및 병렬 데이터 웨어하우스 동적 관리 뷰](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
