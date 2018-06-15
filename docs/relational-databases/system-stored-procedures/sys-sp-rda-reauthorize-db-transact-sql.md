---
title: sys.sp_rda_reauthorize_db (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b387bbd432eb01df84661a61b1f9528857cd74c3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32998540"
---
# <a name="syssprdareauthorizedb-transact-sql"></a>sys.sp_rda_reauthorize_db (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  스트레치 및 원격 데이터베이스에 사용할 수 있는 로컬 데이터베이스 간의 인증된 된 연결을 복원 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>인수  
 @credential = *@credential*  
 로컬 스트레치 사용 데이터베이스와 관련 된 데이터베이스 범위 자격 증명이입니다.  
  
 @with_copy = *@with_copy*  
 원격 데이터의 복사본을 만들고 (권장) 복사본에 연결할 것인지 지정 합니다. *@with_copy* bit입니다.  
  
 @azure_servername = *@azure_servername*  
 원격 데이터를 포함 하는 Azure 서버의 이름을 지정 합니다. *@azure_servername* sysname 합니다.  
  
 @azure_databasename = *@azure_databasename*  
 원격 데이터를 포함 하는 Azure 데이터베이스의 이름을 지정 합니다. *@azure_databasename* sysname 합니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0(성공) 또는 >0(실패)  
  
## <a name="permissions"></a>Permissions  
 Db_owner 권한이 필요합니다.  
  
## <a name="remarks"></a>주의  
 실행 하는 경우 [sys.sp_rda_reauthorize_db (Transact SQL)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 원격 Azure 데이터베이스에 다시 연결 하려면이 작업 자동으로 다시 설정 쿼리 모드, LOCAL_AND_REMOTE를 이것이 스트레치 데이터베이스에 대 한 기본 동작입니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 늘이기 및 원격 데이터베이스에 사용할 수 있는 로컬 데이터베이스 간의 인증된 된 연결을 복원 합니다. (권장) 원격 데이터의 복사본을 만들고 새 복사본에 연결 합니다.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [sys.sp_rda_deauthorize_db &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
