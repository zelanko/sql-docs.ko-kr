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
ms.openlocfilehash: 6db774a52344d3e0938a8caf7691fd0e1dbd2a84
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85751599"
---
# <a name="mspublisher_databases-transact-sql"></a>MSpublisher_databases(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  **MSpublisher_databases** 테이블에는 로컬 배포자가 서비스 하는 각 게시자/게시자 데이터베이스 쌍에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|게시자의 ID입니다.|  
|**publisher_db**|**sysname**|게시자 데이터베이스의 이름입니다.|  
|**id**|**int**|행의 ID입니다.|  
|**publisher_engine_edition**|**int**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자의 버전을 나타내며 다음 중 하나일 수 있습니다.<br /><br /> **10** = 개인용 버전<br /><br /> **11** = 데스크톱 엔진 (MSDE)<br /><br /> **20** = 표준<br /><br /> **21** = 작업 그룹<br /><br /> **30** = Enterprise (Evaluation)<br /><br /> **31** = 개발자<br /><br /> **40** = Express (express는 게시자가 될 수 없습니다. 이 값은 완결성을 위해 존재합니다.)|  
  
## <a name="see-also"></a>참고 항목  
 [복제 테이블&#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
