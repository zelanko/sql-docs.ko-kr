---
title: MSpublisher_databases (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSpublisher_databases
- MSpublisher_databases_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSpublisher_databases system table
ms.assetid: 59b0166e-a64c-46b8-befc-c222fa1ccce2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5c9ceb08b4757af09cfc5eba8c4d9f26da3cf931
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52817715"
---
# <a name="mspublisherdatabases-transact-sql"></a>MSpublisher_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSpublisher_databases** 로컬 배포자 각 게시자/게시자 데이터베이스 쌍에 대해 하나의 행을 포함 하는 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**id**|**int**|행의 ID입니다.|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 버전을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **10** = 개인용 버전<br /><br /> **11** desktop Engine (MSDE) =<br /><br /> **20** = 표준<br /><br /> **21** = 작업 그룹<br /><br /> **30** = Enterprise (Evaluation)<br /><br /> **31** 개발자 =<br /><br /> **40** = express (Express는 게시자가 될 수 없습니다. 이 값은 완결성을 위해 존재합니다.)|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
