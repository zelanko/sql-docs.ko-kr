---
title: sp_enumeratependingschemachanges (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_enumeratependingschemachanges
- sp_enumeratependingschemachanges_TSQL
helpviewer_keywords:
- sp_enumeratependingschemachanges
ms.assetid: df169b21-d10a-41df-b3a1-654cfb58bc21
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4f1e6d9b7f9bce06a8003b56fc6767c992636957
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82831090"
---
# <a name="sp_enumeratependingschemachanges-transact-sql"></a>sp_enumeratependingschemachanges(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  보류 중인 모든 스키마 변경의 목록을 반환합니다. 이 저장 프로시저는 [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)와 함께 사용할 수 있습니다 .이를 통해 관리자는 선택한 보류 중인 스키마 변경 내용이 복제 되지 않도록 건너뛸 수 있습니다. 이 저장 프로시저는 게시 데이터베이스의 게시자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_enumeratependingschemachanges [ @publication = ] 'publication'   
    [ , [ @starting_schemaversion = ] starting_schemaversion ]  
```  
  
## <a name="arguments"></a>인수  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 없습니다.  
  
`[ @starting_schemaversion = ] starting_schemaversion`결과 집합에 포함할 가장 낮은 수의 스키마 변경입니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**article_name**|**sysname**|스키마 변경이 적용 되는 아티클의 이름 또는 전체 게시에 적용 되는 스키마 변경 내용에 대 한 **게시 전체** 이름입니다.|  
|**schemaversion**|**int**|보류 중인 스키마 변경 수입니다.|  
|**schematype**|**sysname**|스키마 변경의 유형을 나타내는 텍스트 값입니다.|  
|**schematext**|**nvarchar(max)**|스키마 변경 내용을 설명하는 [!INCLUDE[tsql](../../includes/tsql-md.md)]입니다.|  
|**schemastatus**|**nvarchar (10)**|스키마 변경이 아티클에 대해 보류 중인지 여부를 나타내며 다음 값 중 하나를 사용할 수 있습니다.<br /><br /> **활성** = 스키마 변경이 보류 중입니다.<br /><br /> **비활성** = 스키마 변경이 비활성 상태임<br /><br /> **skip** = 스키마 변경이 복제 되지 않습니다.|  
|**schemaguid**|**uniqueidentifier**|스키마 변경 내용을 식별합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 **sp_enumeratependingschemachanges** 는 병합 복제에 사용 됩니다.  
  
 [sp_markpendingschemachange](../../relational-databases/system-stored-procedures/sp-markpendingschemachange-transact-sql.md)와 함께 사용 되는 **sp_enumeratependingschemachanges**는 병합 복제의 지원 가능성을 위한 것 이며, 다시 초기화와 같은 다른 수정 동작으로 상황을 해결 하지 못한 경우에만 사용 해야 합니다.  
  
## <a name="permissions"></a>사용 권한  
 **Sysadmin** 고정 서버 역할 또는 **db_owner** 고정 데이터베이스 역할의 멤버만 **sp_enumeratependingschemachanges**을 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [Transact-sql&#41;를 &#40;하는 복제 저장 프로시저](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)   
 [sysmergeschemachange &#40;Transact-sql&#41;](../../relational-databases/system-tables/sysmergeschemachange-transact-sql.md)  
  
  
