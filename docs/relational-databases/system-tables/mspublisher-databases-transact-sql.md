---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 65d174c38d4d6fe22c73b16af40bcee9d4ff63a3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82833138"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSpublisher_databases** 테이블에는 로컬 배포자가 서비스 하는 각 게시자/게시자 데이터베이스 쌍에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**id**|**int**|행의 ID입니다.|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 버전을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **10** = 개인용 버전<br /><br /> **11** = 데스크톱 엔진 (MSDE)<br /><br /> **20** = 표준<br /><br /> **21** = 작업 그룹<br /><br /> **30** = Enterprise (Evaluation)<br /><br /> **31** = 개발자<br /><br /> **40** = Express (express는 게시자가 될 수 없습니다. 이 값은 완결성을 위해 존재합니다.)|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
