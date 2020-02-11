---
title: core. sp_update_data_source (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_data_source
- sp_update_data_source_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_data_source
- management data warehouse, data collector stored procedures
- core.sp_update_data_source stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 66b95f96-6df7-4657-9b3c-86a58c788ca5
author: stevestein
ms.author: sstein
ms.openlocfilehash: a840c749222cc7c01fa1b1ff5a27489e0e9d322a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942464"
---
# <a name="coresp_update_data_source-transact-sql"></a>core.sp_update_data_source(Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  관리 데이터 웨어하우스 core.source_info_internal 테이블에서 기존 행을 업데이트하거나 새 행을 삽입합니다. 이 프로시저는 업로드 패키지에서 관리 데이터 웨어하우스로 데이터를 업로드하기 시작할 때마다 데이터 수집기 런타임 구성 요소에서 호출됩니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
core.sp_update_data_source [ @collection_set_uid = ] 'collection_set_uid'  
    ,[ @machine_name = ] 'machine_name'  
    , [ @named_instance = ] 'named_instance'  
    , [ @days_until_expiration = ] days_until_expiration  
    , [ @source_id = ] source_id OUTPUT  
```  
  
## <a name="arguments"></a>인수  
 [ @collection_set_uid = ] '*collection_set_uid*'  
 컬렉션 집합에 대한 GUID입니다. *collection_set_uid* 은 **uniqueidentifier**이며 기본값은 없습니다. GUID를 확인하려면 msdb 데이터베이스에서 dbo.syscollector_collection_sets 뷰를 쿼리합니다.  
  
 [ @machine_name = ] '*machine_name*'  
 컬렉션 집합이 있는 서버의 이름입니다. *machine_name* 는 **sysname** 이며 기본값은 없습니다.  
  
 [ @named_instance = ] '*named_instance*'  
 컬렉션 집합의 인스턴스 이름입니다. *named_instance* 는 **sysname**이며 기본값은 없습니다.  
  
> [!NOTE]  
>  *named_instance* 는 *computername*\\*instancename*형식의 컴퓨터 이름과 인스턴스 이름으로 구성 된 정규화 된 인스턴스 이름 이어야 합니다.  
  
 [ @days_until_expiration = ] *days_until_expiration*  
 스냅샷 데이터 보존 기간 중 남은 일수입니다. *days_until_expiration* 은 **smallint**입니다.  
  
 [ @source_id = ] *source_id*  
 업데이트 원본의 고유 식별자입니다. *source_id* **int** 이며 OUTPUT으로 반환 됩니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **0** (성공) 또는 **1** (실패)  
  
## <a name="remarks"></a>설명  
 업로드 패키지에서 관리 데이터 웨어하우스로 데이터를 업로드하기 시작할 때마다 데이터 수집기 런타임 구성 요소에서 core.sp_update_data_source를 호출합니다. 마지막 업로드 이후에 다음과 같은 변경이 수행된 경우 core.source_info_internal 테이블이 업데이트됩니다.  
  
-   새 컬렉션 집합이 추가된 경우  
  
-   days_until_expiration의 값이 변경된 경우  
  
## <a name="permissions"></a>사용 권한  
 **Mdw_writer** (실행 권한 포함) 고정 데이터베이스 역할의 멤버 자격이 필요 합니다.  
  
## <a name="examples"></a>예  
 다음 예에서는 데이터 원본(이 경우에는 디스크 사용 컬렉션 집합)을 업데이트하고 만료 기간(일)을 설정한 다음 원본의 식별자를 반환합니다. 이 예에서는 기본 인스턴스가 사용됩니다.  
  
```  
USE <management_data_warehouse>;  
GO  
DECLARE @source_id int;  
EXEC core.sp_update_data_source   
@collection_set_uid = '7B191952-8ECF-4E12-AEB2-EF646EF79FEF',   
@machine_name = '<computername>',  
@named_instance = 'MSSQLSERVER',  
@days_until_expiration = 10,  
@source_id = @source_id OUTPUT;  
```  
  
## <a name="see-also"></a>참고 항목  
 [시스템 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [데이터 수집기 저장 프로시저&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [관리 데이터 웨어하우스](../../relational-databases/data-collection/management-data-warehouse.md)  
  
  
