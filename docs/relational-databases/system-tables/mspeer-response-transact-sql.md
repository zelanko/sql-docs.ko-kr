---
title: MSpeer_response (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_response
- MSpeer_response_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_response system table
ms.assetid: 510e24cf-0292-47a9-b1d9-71a30fef030f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 371ee711cbae4c97dc95e9d31d51739c29e85d14
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889635"
---
# <a name="mspeer_response-transact-sql"></a>MSpeer_response(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpeer_response** 테이블은 피어 투 피어 복제에서 게시 상태 요청에 대 한 각 노드의 응답을 저장 하는 데 사용 됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|[MSpeer_request](../../relational-databases/system-tables/mspeer-request-transact-sql.md) 테이블의 상태 요청 항목을 식별 합니다.|  
|**피어는**|**sysname**|응답을 생성한 피어입니다.|  
|**peer_db**|**sysname**|응답을 생성한 피어에 있는 구독 데이터베이스입니다.|  
|**received_date**|**datetime**|피어 요청을 받은 날짜 및 시간입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
