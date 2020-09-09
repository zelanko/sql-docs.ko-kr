---
description: sp_get_distributor(Transact-SQL)
title: sp_get_distributor (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_get_distributor
- sp_get_distributor_TSQL
helpviewer_keywords:
- sp_get_distributor
ms.assetid: f0134448-bc17-4f2f-bd81-619351ce56ac
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6cdc15f66c918b0d320c9c2ad2106fbded5fc256
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89549749"
---
# <a name="sp_get_distributor-transact-sql"></a>sp_get_distributor(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  배포자가 서버에 설치되어 있는지 확인합니다. 이 저장 프로시저는 모든 데이터베이스의 배포자를 찾고 있는 컴퓨터에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_get_distributor   
```  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**설치한**|**int**|**0** = 아니요; **1** = 예|  
|**distribution server**|**sysname**|배포자 서버의 이름입니다.|  
|**배포 db가 설치 됨**|**int**|**0** = 아니요; **1** = 예|  
|**is distribution publisher**|**int**|**0** = 아니요; **1** = 예|  
|**has remote distribution publisher**|**int**|**0** = 아니요; **1** = 예|  
  
## <a name="remarks"></a>설명  
 **sp_get_distributor** 는 주로 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 스냅숏, 트랜잭션 및 병합 복제에서 사용 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 모든 사용자가 **sp_get_distributor**를 실행할 수 있습니다. 배포 데이터베이스의 **db_owner** 또는 **replmonitor** 고정 데이터베이스 역할 또는 하나 이상의 게시 된 데이터베이스에 대 한 **db_owner** 고정 데이터베이스 역할의 멤버가이 저장 프로시저를 실행 하면 NULL이 아닌 결과 집합이 반환 됩니다. 하나 이상의 게시 된 데이터베이스의 PAL (게시 액세스 목록)에 있는 사용자가이 저장 프로시저를 실행 하거나, SQL Server 이외 게시자에 대 한 배포 데이터베이스의 PAL에서이 저장 프로시저를 실행 하는 경우에도 NULL이 아닌 결과 집합이 반환 됩니다. **sp_get_distributor**를 실행할 수도 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [게시 및 배포 구성](../../relational-databases/replication/configure-publishing-and-distribution.md)   
 [배포자 및 게시자 정보 스크립트](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
