---
title: MSpeer_topologyrequest (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSpeer_topologyrequest_TSQL
- MSpeer_topologyrequest
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_topologyrequest
ms.assetid: c644814b-4e40-44d7-b6b4-5954b0d4db7c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f638d95416336a3d74eaafbdf7c6fdd25407ce18
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818883"
---
# <a name="mspeertopologyrequest-transact-sql"></a>MSpeer_topologyrequest(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  피어 투 피어 복제에서 게시에 대한 토폴로지 상태 요청을 추적하기 위해 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|토폴로지 상태 요청을 식별합니다. request_id 열에서 [MSpeer_topologyresponse](../../relational-databases/system-tables/mspeer-topologyresponse-transact-sql.md) 이 값을 사용 합니다.|  
|publication|**sysname**|토폴로지 상태 요청이 시작된 게시의 이름입니다.|  
|sent_date|**datetime**|토폴로지 상태 요청이 시작된 날짜와 시간입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
