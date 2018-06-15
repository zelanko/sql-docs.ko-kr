---
title: sp_helpmergealternatepublisher (Transact SQL) | Microsoft Docs
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
- sp_helpmergealternatepublisher_TSQL
- sp_helpmergealternatepublisher
helpviewer_keywords:
- sp_helpmergealternatepublisher
ms.assetid: a96e365f-5967-4580-9d79-5bacf2d12211
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: f51c69c6034963dff80377570120dcd65027b762
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32995330"
---
# <a name="sphelpmergealternatepublisher-transact-sql"></a>sp_helpmergealternatepublisher(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  병합 게시에 대한 대체 게시자로 사용할 수 있는 모든 서버의 목록의 반환합니다. 이 저장 프로시저는 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_helpmergealternatepublisher [ @publisher = ] 'publisher', [ @publisher_db = ] 'publisher_db', [ @publication = ] 'publication'  
```  
  
## <a name="arguments"></a>인수  
 [ **@publisher=**] **'***publisher***'**  
 대체 게시자의 이름이입니다. *게시자* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publisher_db=**] **'***publisher_db***'**  
 게시 데이터베이스의 이름이입니다. *publisher_db* 은 **sysname**, 기본값은 없습니다.  
  
 [ **@publication=**] **'***publication***'**  
 게시의 이름이입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**alternate_publisher**|**sysname**|대체 게시자의 이름입니다.|  
|**alternate_publisher_db**|**sysname**|게시 데이터베이스의 이름입니다.|  
|**alternate_publication**|**sysname**|게시의 이름입니다.|  
|**alternate_distributor**|**sysname**|배포자의 이름입니다.|  
|**friendly_name**|**nvarchar(255)**|대체 게시자에 관한 설명입니다.|  
|**enabled**|**bit**|서버가 대체 게시자인지 여부를 지정합니다. **1** 게시자가 동기화 대상이 대체 게시자로 활성화 되어 있는지를 지정 합니다. **0** 사용 하지 않음을 지정 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_helpmergealternatepublisher** 병합 복제에 사용 됩니다.  
  
 모든 병합 세션 동안 시스템은 게시자와 구독자에서 대체 게시자의 각 목록을 쿼리합니다. 병합 프로세스는 구독자와 게시자 모두에 있는 대체 게시자 목록이 일치하도록 대체 게시자 목록의 항목을 추가하거나 삭제합니다.  
  
## <a name="permissions"></a>Permissions  
 게시에 대 한 게시 액세스 목록의 멤버만 실행할 수 있습니다 **sp_helpmergealternatepublisher**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
