---
title: MSsubscriber_info (TRANSACT-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 45065f7cde525d65997df2c97c972d684cadd90f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139818"
---
# <a name="mssubscriberinfo-transact-sql"></a>MSsubscriber_info(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  합니다 **MSsubscriber_info** 구독 로컬 배포자에서 푸시되는 각 게시자/구독자 쌍에 대 한 하나의 행을 포함 하는 테이블입니다. 이 테이블은 배포 데이터베이스에 저장됩니다.  
  
 **참고** 이 시스템 테이블에 사용 되지 않으며 이전 버전의 지원 하기 위해 유지 됩니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
## <a name="definition"></a>정의  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**publisher**|**sysname**|게시자의 이름입니다.|  
|**subscriber**|**sysname**|구독자 이름입니다.|  
|**type**|**tinyint**|구독자 유형입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구독자입니다.<br /><br /> **1** = ODBC 데이터 원본입니다.|  
|**login**|**sysname**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 로그인입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 모드로 구독자를 추가한 경우에는 암호화된 형식으로 저장됩니다.|  
|**password**|**nvarchar(524)**|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 위한 암호입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 모드로 구독자를 추가한 경우에는 암호화된 형식으로 저장됩니다.|  
|**description**|**nvarchar(255)**|구독자에 대한 설명입니다.|  
|**security_mode**|**int**|구현된 보안 모드입니다.<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증 합니다.<br /><br /> **1**  =  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 인증입니다.|  
  
## <a name="see-also"></a>관련 항목  
 [복제 테이블 &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [복제 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
