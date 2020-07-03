---
title: sp_showpendingchanges (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2f6d22fb18989022676eb06751d583383a14d783
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881498"
---
# <a name="sp_showpendingchanges-transact-sql"></a>sp_showpendingchanges(Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  복제 대기 중인 변경 내용을 보여 주는 결과 집합을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
> [!NOTE]  
>  이 프로시저는 대략적인 변경 내용 수와 이러한 변경 내용과 관련된 행을 제공합니다. 예를 들어 이 프로시저는 게시자 또는 구독자 중 하나에서 정보를 검색하지만 동시에 둘 다에서 정보를 검색하지는 않습니다. 다른 노드에 저장된 정보는 동기화할 변경 내용 집합을 프로시저가 예상한 것보다 줄어들게 할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_showpendingchanges [ [ @destination_server = ] 'destination_server' ]  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article']  
    [ , [ @show_rows = ] show_rows]  
```  
  
## <a name="arguments"></a>인수  
`[ @destination_server = ] 'destination_server'`복제 된 변경 내용이 적용 되는 서버의 이름입니다. *destination_server* 는 **sysname**이며 기본값은 NULL입니다.  
  
`[ @publication = ] 'publication'`게시의 이름입니다. *게시* 는 **sysname**이며 기본값은 NULL입니다. *게시* 를 지정 하면 결과는 지정 된 게시로만 제한 됩니다.  
  
`[ @article = ] 'article'`아티클의 이름입니다. *article* 은 **sysname**이며 기본값은 NULL입니다. *Article* 을 지정 하면 결과는 지정 된 아티클로만 제한 됩니다.  
  
`[ @show_rows = ] 'show_rows'`결과 집합에 보류 중인 변경 내용에 대 한 보다 구체적인 정보가 포함 되어 있는지 여부를 지정 합니다. 기본값은 **0**입니다. 값 **1** 을 지정 하면 결과 집합에 is_delete 및 rowguid 열이 포함 됩니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|변경 내용이 복제되는 대상 서버의 이름입니다.|  
|pub_name|**sysname**|게시의 이름입니다.|  
|destination_db_name|**sysname**|변경 내용이 복제되는 대상 데이터베이스의 이름입니다.|  
|is_dest_subscriber|**bit**|변경 내용이 구독자로 복제되는 중임을 나타냅니다. 값 **1** 은 변경 내용이 구독자에 복제 되 고 있음을 나타냅니다. **0** 은 변경 내용이 게시자에 복제 됨을 의미 합니다.|  
|article_name|**sysname**|변경이 시작된 테이블에 대한 아티클의 이름입니다.|  
|pending_deletes|**int**|복제 대기 중인 삭제 수입니다.|  
|pending_ins_and_upd|**int**|복제 대기 중인 삽입 및 업데이트 수입니다.|  
|is_delete|**bit**|보류 중인 변경 내용의 삭제 여부를 나타냅니다. 값 **1** 은 변경 내용이 삭제 임을 나타냅니다. 에는 값 **1** 이 필요 @show_rows 합니다.|  
|rowguid|**uniqueidentifier**|변경된 행을 식별하는 GUID입니다. 에는 값 **1** 이 필요 @show_rows 합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 sp_showpendingchanges는 병합 복제에 사용됩니다.  
  
 sp_showpendingchanges는 병합 복제의 문제를 해결할 때 사용합니다.  
  
 sp_showpendingchanges의 결과는 생성 0의 행을 포함하지 않습니다.  
  
 *아티클에* 지정 된 아티클이 *게시* 에 대해 지정 된 게시에 속하지 않는 경우 pending_deletes 및 pending_ins_and_upd에 대해 수가 0이 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버만 sp_showpendingchanges를 실행할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
