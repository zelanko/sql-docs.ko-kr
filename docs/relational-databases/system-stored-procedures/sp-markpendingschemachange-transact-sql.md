---
title: sp_markpendingschemachange (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
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
- sp_markpendingschemachange
- sp_markpendingschemachange_TSQL
helpviewer_keywords:
- sp_markpendingschemachange
ms.assetid: 01100309-7bef-4154-85bf-f18489577e37
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: e3bfd0bb51e6d269b84fdb57a5a64139ce23cedc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32994820"
---
# <a name="spmarkpendingschemachange-transact-sql"></a>sp_markpendingschemachange(Transact-SQL)
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
 [**@publication=** ] **'***게시***'**  
 게시의 이름입니다. *게시* 은 **sysname**, 기본값은 없습니다.  
  
 [  **@schemaversion=** ] *스키마 버전*  
 보류 중인 스키마 변경 내용을 식별합니다. *schemaversion* 은 **int**의 기본값은 **0**합니다. 사용 하 여 [sp_enumeratependingschemachanges &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-enumeratependingschemachanges-transact-sql.md) 게시에 대 한 보류 중인 스키마 변경 내용 나열 합니다.  
  
 [  **@status=** ] **'***상태***'**  
 보류 중인 스키마 변경 내용을 건너뛸 것인지 여부입니다. *상태* 은 **nvarchar (10)** 의 기본값은 **활성**합니다. 하는 경우의 값 *상태* 은 **건너뛴**, 다음 선택한 스키마 변경 복제 되지 것입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>주의  
 **sp_markpendingschemachange** 병합 복제와 함께 사용 됩니다.  
  
 **sp_markpendingschemachange** 저장된 프로시저는 병합 복제의 지원 가능성을 위한 하 고, 다시 초기화와 같은 다른 수정 동작으로 상황을 해결 하려면 실패 한 되거나에서 비용이 큰 경우에 사용 해야 성능 조건입니다.  
  
## <a name="permissions"></a>Permissions  
 구성원만는 **sysadmin** 고정된 서버 역할 또는 **db_owner** 고정된 데이터베이스 역할을 실행할 수 있는 **sp_markpendingschemachange**합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [sysmergeschemachange &#40;TRANSACT-SQL&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
