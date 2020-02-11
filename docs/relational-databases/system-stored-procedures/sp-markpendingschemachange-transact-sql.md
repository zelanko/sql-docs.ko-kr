---
title: sp_markpendingschemachange (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
author: stevestein
ms.author: sstein
ms.openlocfilehash: 56ed176d8b4b29e1ed4caafabd0893b7a33b1293
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73962390"
---
# <a name="sp_markpendingschemachange-transact-sql"></a>sp_markpendingschemachange(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  선택한 보류 중인 스키마의 변경 내용이 복제되지 않도록 관리자가 이를 건너뛸 수 있게 함으로써 병합 게시의 지원 가능성을 확보하는 데 사용합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
> [!CAUTION]  
>  이 저장 프로시저는 스키마 변경 내용이 복제되지 않도록 할 수 있습니다. 다시 초기화와 같은 다른 방법을 먼저 시도했지만 해결되지 않은 경우, 또는 다른 방법이 성능 면에서 비용이 큰 경우에만 이 저장 프로시저를 사용하여 문제를 해결하십시오.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_markpendingschemachange [@publication = ] 'publication'  
    [ , [ @schemaversion = ] schemaversion ]  
    [ , [ @status = ] 'status' ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @schemaversion = ] schemaversion`보류 중인 스키마 변경 내용을 식별 합니다. *schemaversion* 은 **int**이며 기본값은 **0**입니다. [Sp_enumeratependingschemachanges &#40;transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) 를 사용 하 여 게시에 대 한 보류 중인 스키마 변경 내용을 나열 합니다.  
  
`[ @status = ] 'status'`보류 중인 스키마 변경 내용을 건너뛸 것인지 여부를 나타냅니다. *status* 는 **nvarchar (10)** 이며 기본값은 **active**입니다. *상태* 값을 **건너뛰면**선택한 스키마 변경이 복제 되지 않습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_markpendingschemachange** 는 병합 복제에 사용 됩니다.  
  
 **sp_markpendingschemachange** 는 병합 복제의 지원 가능성을 위한 저장 프로시저 이며, 다시 초기화와 같은 다른 수정 작업이 상황을 해결 하는 데 실패 했거나 성능 측면에서 비용이 많이 드는 경우에만 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_markpendingschemachange**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
