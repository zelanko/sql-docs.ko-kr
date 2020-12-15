---
description: sys.dm_pdw_network_credentials (Transact-sql)
title: sys.dm_pdw_network_credentials (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: d4fee3ad-6285-4ea5-8513-5e6eb617abb0
author: markingmyname
ms.author: maghan
monikerRange: '>= aps-pdw-2016'
ms.openlocfilehash: 7d94853e62c1e9e97ddd65ad973e9e481d90bcb0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472744"
---
# <a name="sysdm_pdw_network_credentials-transact-sql"></a>sys.dm_pdw_network_credentials (Transact-sql)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]모든 대상 서버에 대해 어플라이언스에 저장 된 모든 네트워크 자격 증명의 목록을 반환 합니다. 결과는 제어 노드 및 모든 계산 노드에 대해 나열 됩니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|노드와 연결 된 고유 숫자 id입니다.|  
|target_server_name|**nvarchar(32)**|[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]사용자 이름 및 암호 자격 증명을 사용 하 여에 액세스 하는 대상 서버의 IP 주소입니다.|  
|사용자 이름|**nvarchar(32)**|암호가 저장 되는 사용자 이름입니다.|  
|last_modified|**datetime**|자격 증명을 수정한 마지막 작업의 날짜/시간입니다.|  
  
## <a name="permissions"></a>사용 권한  
 뷰 서버 상태가 필요 합니다.  
  
## <a name="general-remarks"></a>일반적인 주의 사항  
 이 동적 관리 뷰의 키는 *pdw_node_id* 및 *target_server_name* 입니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;Azure Synapse 분석 및 병렬 데이터 웨어하우스 동적 관리 뷰 ](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
