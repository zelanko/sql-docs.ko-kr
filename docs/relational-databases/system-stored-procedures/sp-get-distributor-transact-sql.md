---
title: sp_get_distributor (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: cf685a9dec6f815d30b11db3e4f4933cd7ac19d2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47634451"
---
# <a name="spgetdistributor-transact-sql"></a>sp_get_distributor(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  배포자가 서버에 설치되어 있는지 확인합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자를 찾고 있는 컴퓨터에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**설치**|**int**|**0** = 아니요. **1** = 예|  
|**배포 서버**|**sysname**|배포자 서버의 이름입니다.|  
|**배포 db가 설치 됨**|**int**|**0** = 아니요. **1** = 예|  
|**배포 게시자**|**int**|**0** = 아니요. **1** = 예|  
|**원격 배포 게시자가 있음**|**int**|**0** = 아니요. **1** = 예|  
  
## <a name="remarks"></a>Remarks  
 **sp_get_distributor** 는 주로 합니다 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스냅숏, 트랜잭션 및 병합 복제에 있습니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자가 실행할 수 있습니다 **sp_get_distributor**합니다. NULL이 아닌 결과 집합이 반환 됩니다이 저장 하는 경우의 멤버에서 프로시저를 실행 합니다 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버 또는 배포 데이터베이스에는  **db_owner** 하나 이상의 게시 된 데이터베이스에서 고정된 데이터베이스 역할. NULL이 아닌 결과 집합에도 반환 됩니다이 저장된 프로시저를 실행할 때의 게시 액세스 목록 (PAL)의 사용자가 적어도 하나의 게시 된 데이터베이스에서 또는 배포 데이터베이스에 대 한-SQL Server 이외 게시자의 PAL에 실행할 수도 있습니다 **sp _get_distributor**합니다.  
  
## <a name="see-also"></a>관련 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [배포자 및 게시자 정보 스크립트](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
