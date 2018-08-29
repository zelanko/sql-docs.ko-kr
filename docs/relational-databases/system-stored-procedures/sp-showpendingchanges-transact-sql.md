---
title: sp_showpendingchanges (TRANSACT-SQL) | Microsoft Docs
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
- sp_showpendingchanges
- sp_showpendingchanges_TSQL
helpviewer_keywords:
- sp_showpendingchanges
ms.assetid: 8013a792-639d-4550-b262-e65d30f9d291
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 229136548d40e985869bd1f01685cb0c3dad6f4f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43030704"
---
# <a name="spshowpendingchanges-transact-sql"></a>sp_showpendingchanges(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  복제 대기 중인 변경 내용을 보여 주는 결과 집합을 반환합니다. 이 저장 프로시저는 게시 데이터베이스의 게시자와 구독 데이터베이스의 구독자에서 실행됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @destination_server **=** ] **'***destination_server***'**  
 복제된 변경 내용을 적용할 서버의 이름입니다. *destination_server* 됩니다 **sysname**, 기본값은 NULL입니다.  
  
 [ @publication **=** ] **'***게시***'**  
 게시의 이름입니다. *게시* 됩니다 **sysname**, 기본값은 NULL입니다. 때 *게시* 를 지정 하면 결과 지정된 된 게시에만 제한 됩니다.  
  
 [ @article **=** ] **'***문서***'**  
 아티클의 이름입니다. *문서* 됩니다 **sysname**, 기본값은 NULL입니다. 때 *문서* 를 지정 하면 결과 지정 된 문서에만 제한 됩니다.  
  
 [ @show_rows **=** ] *show_rows*  
 포함 되는지 여부를 결과 집합 보다 구체적인 정보에 대 한 보류 중인 변경 내용을 기본 값을 사용 하 여 지정 **0**합니다. 값 **1** 를 지정 하면 결과 집합 열 is_delete 및 rowguid를 포함 합니다.  
  
## <a name="result-set"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|destination_server|**sysname**|변경 내용이 복제되는 대상 서버의 이름입니다.|  
|pub_name|**sysname**|게시의 이름입니다.|  
|destination_db_name|**sysname**|변경 내용이 복제되는 대상 데이터베이스의 이름입니다.|  
|is_dest_subscriber|**bit**|변경 내용이 구독자로 복제되는 중임을 나타냅니다. 값이 **1** 변경 내용이 구독자로 복제 되 고 나타냅니다. **0** 게시자에 변경 내용이 복제 되는지 의미 합니다.|  
|article_name|**sysname**|변경이 시작된 테이블에 대한 아티클의 이름입니다.|  
|pending_deletes|**int**|복제 대기 중인 삭제 수입니다.|  
|pending_ins_and_upd|**int**|복제 대기 중인 삽입 및 업데이트 수입니다.|  
|is_delete|**bit**|보류 중인 변경 내용의 삭제 여부를 나타냅니다. 값이 **1** 변경 삭제 임을 나타냅니다. 값이 필요 **1** 에 대 한 @show_rows합니다.|  
|rowguid|**uniqueidentifier**|변경된 행을 식별하는 GUID입니다. 값이 필요 **1** 에 대 한 @show_rows합니다.|  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>Remarks  
 sp_showpendingchanges는 병합 복제에 사용됩니다.  
  
 sp_showpendingchanges는 병합 복제의 문제를 해결할 때 사용합니다.  
  
 sp_showpendingchanges의 결과는 생성 0의 행을 포함하지 않습니다.  
  
 에 대 한 지정 된 아티클이 *문서* 에 대 한 지정 된 게시에 속하지 *게시* 0 않으면 pending_deletes 및 pending_ins_and_upd에 대해 반환 됩니다.  
  
## <a name="permissions"></a>사용 권한  
 sysadmin 고정 서버 역할 또는 db_owner 고정 데이터베이스 역할의 멤버만 sp_showpendingchanges를 실행할 수 있습니다.  
  
## <a name="see-also"></a>관련 항목  
 [복제 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
