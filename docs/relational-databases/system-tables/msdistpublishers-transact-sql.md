---
title: MSdistpublishers (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b0cf48f494c04bd57e1bf20930917e4f9a3d015b
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102681"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  합니다 **MSdistpublishers** 테이블은 로컬 배포자에서 지원 되는 각 원격 게시자에 대해 하나의 행을 포함 합니다. 이 테이블에 저장 되는 **msdb** 데이터베이스입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|게시자 배포자의 이름입니다.|  
|**distribution_db**|**sysname**|배포 데이터베이스의 이름입니다.|  
|**working_directory**|**nvarchar(255)**|게시할 데이터 및 스키마 파일을 저장하기 위해 사용하는 작업 디렉터리의 이름입니다.|  
|**security_mode**|**int**|배포자에서 구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.<br /><br /> **1** = Windows 인증입니다.|  
|**login**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 대한 로그인 ID입니다.|  
|**password**|**nvarchar(524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 암호화된 암호입니다.|  
|**Active**|**bit**|원격 게시자가 로컬 배포자를 사용하고 있는지 여부를 나타냅니다.|  
|**신뢰할 수 있는**|**bit**|원격 게시자가 로컬 배포자와 동일한 암호를 사용하는지 여부를 나타냅니다.<br /><br /> **0** = 원격 게시자에서 배포자에 연결할 암호가 필요 합니다.<br /><br /> **1** = No 암호가 필요 합니다.|  
|**탐색기**|**bit**|게시자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치인지 여부를 나타냅니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 합니다. **1** = 유형이 다른 데이터 원본입니다.|  
|**publisher_type**|**sysname**|게시자 유형<br /><br /> **MSSQLSERVER**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 게시자입니다.<br /><br /> **ORACLE** = 표준 Oracle 게시자입니다.<br /><br /> **ORACLE GATEWAY** = Oracle 게이트웨이 게시자입니다.|  
|**storage_connection_string**|**nvarchar(779)**|Azure SQL Database 저장소 연결 문자열의 값입니다.|  

  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
