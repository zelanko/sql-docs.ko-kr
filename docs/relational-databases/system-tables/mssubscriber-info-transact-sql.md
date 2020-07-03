---
title: MSsubscriber_info (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSsubscriber_info_TSQL
- MSsubscriber_info
dev_langs:
- TSQL
helpviewer_keywords:
- MSsubscriber_info system table
ms.assetid: 5ca22f41-6020-4f72-8110-e69baf3447cb
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 454b3504db5c159135d257229bb24581a254cd77
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889381"
---
# <a name="mssubscriber_info-transact-sql"></a>MSsubscriber_info(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  **MSsubscriber_info** 테이블에는 로컬 배포자에서 푸시되는 각 게시자/구독자 쌍에 대 한 행이 하나씩 포함 되어 있습니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
 **참고** 이 시스템 테이블은 더 이상 사용 되지 않으며 이전 버전의를 지원 하기 위해 유지 관리 되 고 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있습니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**발행자**|**sysname**|게시자의 이름입니다.|  
|**구독자**|**sysname**|구독자 이름입니다.|  
|**type**|**tinyint**|구독자 유형입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자.<br /><br /> **1** = ODBC 데이터 원본|  
|**로그인**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 로그인입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 모드로 구독자를 추가한 경우에는 암호화된 형식으로 저장됩니다.|  
|**password**|**nvarchar (524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 암호입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 모드로 구독자를 추가한 경우에는 암호화된 형식으로 저장됩니다.|  
|**한**|**nvarchar(255)**|구독자에 대한 설명입니다.|  
|**security_mode**|**int**|구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;&#40;복제 테이블](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
