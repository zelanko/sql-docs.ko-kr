---
title: sp_get_distributor (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1f4cd34760ff4bd447bc5a2621508629264adee1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32994100"
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
  
## <a name="remarks"></a>주의  
 **sp_get_distributor** 에서 주로 사용 되는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스냅숏, 트랜잭션 및 병합 복제에 있습니다.  
  
## <a name="permissions"></a>Permissions  
 모든 사용자가 실행할 수 **sp_get_distributor**합니다. NULL이 아닌 결과 집합이 반환 됩니다 때이 저장 프로시저의 멤버에 의해 실행 되는 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할의 멤버 또는 배포 데이터베이스에는  **db_owner** 게시 된 데이터베이스를 하나 이상에 고정된 데이터베이스 역할입니다. NULL이 아닌 결과 집합이 반환 됩니다이 저장된 프로시저를 실행할 때의 게시 액세스 목록 (PAL)의 사용자가 적어도 하나의 게시 된 데이터베이스 또는 배포 데이터베이스에 대 한-SQL Server 이외 게시자의 PAL에 실행할 수도 **sp _get_distributor**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [배포자 및 게시자 정보 스크립트](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
