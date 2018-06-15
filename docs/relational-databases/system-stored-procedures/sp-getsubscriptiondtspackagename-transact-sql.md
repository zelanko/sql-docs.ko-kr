---
title: sp_getsubscriptiondtspackagename (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
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
- sp_getsubscriptiondtspackagename
- sp_getsubscriptiondtspackagename_TSQL
helpviewer_keywords:
- sp_getsubscriptiondtspackagename
ms.assetid: 606c40aa-2593-43af-9762-0f260bbb51f2
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 755cd58c1e67ad0136e030cc63ae5d03437b76da
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32994270"
---
# <a name="spgetsubscriptiondtspackagename-transact-sql"></a>sp_getsubscriptiondtspackagename(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  데이터를 구독자로 보내기 전에 변환하는 데 사용되는 DTS(데이터 변환 서비스) 패키지의 이름을 반환합니다. 이 저장 프로시저는 모든 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_getsubscriptiondtspackagename [ @publication = ] 'publication'   
    [ , [ @subscriber = ] 'subscriber' ]  
```  
  
## <a name="arguments"></a>인수  
 [ **@publication**=] **'***게시***'**  
 게시의 이름입니다. **'***게시***'** 은 **sysname**, 기본값은 없습니다.  
  
 [  **@subscriber=**] **'***구독자***'**  
 구독자의 이름입니다. *구독자* 는 sysname 이며 기본값은 NULL입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**new_package_name**|**sysname**|DTS 패키지의 이름입니다.|  
  
## <a name="remarks"></a>주의  
 **sp_getsubscriptiondtspackagename** 스냅숏 복제 및 트랜잭션 복제에 사용 됩니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_getsubscriptiondtspackagename**합니다.  
  
  
