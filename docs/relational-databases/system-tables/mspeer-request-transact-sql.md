---
description: MSpeer_request(Transact-SQL)
title: MSpeer_request (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpeer_request
- MSpeer_request_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpeer_request system table
ms.assetid: ed048c46-7a2f-4ad0-bc7c-c2d65e83b4fb
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5b4c0352e9e0b0fab04be0dbbc1ff2a62d691c48
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545591"
---
# <a name="mspeer_request-transact-sql"></a>MSpeer_request(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  MSpeer_request 테이블은 피어 투 피어 복제에서 지정된 게시에 대한 상태 요청을 추적하는 데 사용됩니다. 이 테이블은 게시 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|id|**int**|요청을 식별합니다.|  
|publication|**sysname**|상태 요청이 시작된 게시의 이름입니다.|  
|sent_date|**datetime**|상태 요청이 시작된 날짜 및 시간입니다.|  
|description|**nvarchar(4000)**|개별 상태 요청을 식별하는 데 사용할 수 있는 사용자 정의 정보입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
