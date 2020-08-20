---
description: MSdistpublishers(Transact-SQL)
title: MSdistpublishers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdistpublishers
- MSdistpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdistpublishers system table
ms.assetid: 31844099-4b33-4dc9-84b4-bac70aa82598
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: ccbc9a47974a0bbd5429cc8b92cd1f5bbffae792
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88488822"
---
# <a name="msdistpublishers-transact-sql"></a>MSdistpublishers(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  **Msdistpublishers** 테이블은 로컬 배포자에서 지 원하는 각 원격 게시자에 대해 하나의 행을 포함 합니다. 이 테이블은 **msdb** 데이터베이스에 저장 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|게시자 배포자의 이름입니다.|  
|**distribution_db**|**sysname**|배포 데이터베이스의 이름입니다.|  
|**working_directory**|**nvarchar(255)**|게시할 데이터 및 스키마 파일을 저장하기 위해 사용하는 작업 디렉터리의 이름입니다.|  
|**security_mode**|**int**|배포자에서 구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증.<br /><br /> **1** = Windows 인증|  
|**로그인**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증에 대한 로그인 ID입니다.|  
|**password**|**nvarchar (524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 암호화된 암호입니다.|  
|**active**|**bit**|원격 게시자가 로컬 배포자를 사용하고 있는지 여부를 나타냅니다.|  
|**trusted**|**bit**|원격 게시자가 로컬 배포자와 동일한 암호를 사용하는지 여부를 나타냅니다.<br /><br /> **0** = 원격 게시자에서 배포자에 연결 하는 데 암호가 필요 합니다.<br /><br /> **1** = 암호가 필요 하지 않습니다.|  
|**third_party**|**bit**|게시자가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치인지 여부를 나타냅니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치.** 1** = 유형이 다른 데이터 원본입니다.|  
|**publisher_type**|**sysname**|게시자 유형<br /><br /> **MSSQLSERVER**  =  MSSQLSERVER [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 발행자.<br /><br /> **Oracle** = 표준 oracle 게시자<br /><br /> **ORACLE gateway** = Oracle gateway 게시자입니다.|  
|**storage_connection_string**|**nvarchar (779)**|Azure SQL Database 저장소 연결 문자열의 값입니다.|  

  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블 ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
