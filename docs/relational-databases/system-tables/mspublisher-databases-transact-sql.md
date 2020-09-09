---
description: MSpublisher_databases(Transact-SQL)
title: MSpublisher_databases (Transact-sql) | Microsoft Docs
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: caba0fa6bf5bee0d00b182a82fc2add0c5061720
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550992"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSpublisher_databases** 테이블에는 로컬 배포자가 서비스 하는 각 게시자/게시자 데이터베이스 쌍에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**id**|**int**|행의 ID입니다.|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 버전을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **10** = 개인용 버전<br /><br /> **11** = 데스크톱 엔진 (MSDE)<br /><br /> **20** = 표준<br /><br /> **21** = 작업 그룹<br /><br /> **30** = Enterprise (Evaluation)<br /><br /> **31** = 개발자<br /><br /> **40** = Express (express는 게시자가 될 수 없습니다. 이 값은 완결성을 위해 존재합니다.)|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
