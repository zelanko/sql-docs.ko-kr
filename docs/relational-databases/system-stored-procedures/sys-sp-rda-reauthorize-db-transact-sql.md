---
title: sys. sp_rda_reauthorize_db (Transact-sql) | Microsoft Docs
description: Sp_rda_reauthorize_db를 사용 하 여 로컬 스트레치 사용 데이터베이스와 원격 데이터베이스 간의 인증 된 연결을 복원 하는 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sp_rda_reauthorize_db
- sp_rda_reauthorize_db_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_reauthorize_db stored procedure
ms.assetid: f6f3e4b2-8c72-4d23-a5de-fe671ca5c5cd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5bb6c7ff0d9e2025e5036043c8a48616b0679a54
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87247572"
---
# <a name="syssp_rda_reauthorize_db-transact-sql"></a>sys.sp_rda_reauthorize_db(Transact-SQL)
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  스트레치를 사용 하도록 설정 된 로컬 데이터베이스와 원격 데이터베이스 간의 인증 된 연결을 복원 합니다.  
  
 ![항목 링크 아이콘](../../database-engine/configure-windows/media/topic-link.gif "항목 링크 아이콘") [Transact-SQL 구문 표기 규칙](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>구문  
  
```  
  
sp_rda_reauthorize_db @credential = @credential, @with_copy = @with_copy [ , @azure_servername = @azure_servername, @azure_databasename = @azure_databasename ]  
```  
  
## <a name="arguments"></a>인수  
 @credential= * \@ 자격 증명*  
 로컬 스트레치 사용 데이터베이스와 연결 된 데이터베이스 범위 자격 증명입니다.  
  
 @with_copy= * \@ with_copy*  
 원격 데이터의 복사본을 만들고 복사본에 연결할지 여부를 지정 합니다 (권장). * \@ with_copy* 비트입니다.  
  
 @azure_servername= * \@ azure_servername*  
 원격 데이터를 포함 하는 Azure 서버의 이름을 지정 합니다. * \@ azure_servername* 는 sysname입니다.  
  
 @azure_databasename= * \@ azure_databasename*  
 원격 데이터를 포함 하는 Azure 데이터베이스의 이름을 지정 합니다. * \@ azure_databasename* 는 sysname입니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 0 (성공) 또는 >0 (실패)  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요 합니다.  
  
## <a name="remarks"></a>설명  
 [Sp_rda_reauthorize_db (transact-sql)](../../relational-databases/system-stored-procedures/sys-sp-rda-reauthorize-db-transact-sql.md) 을 실행 하 여 원격 Azure 데이터베이스에 다시 연결 하는 경우이 작업은 자동으로 쿼리 모드를 Stretch Database의 기본 동작인 LOCAL_AND_REMOTE으로 다시 설정 합니다. 즉, 쿼리는 로컬 및 원격 데이터에서 결과를 반환 합니다.  
  
## <a name="example"></a>예제  
 다음 예에서는 스트레치를 사용 하도록 설정 된 로컬 데이터베이스와 원격 데이터베이스 간의 인증 된 연결을 복원 합니다. 원격 데이터의 복사본을 만들고 (권장) 새 복사본에 연결 합니다.  
  
```sql  
DECLARE @credentialName nvarchar(128);   
SET @credentialName = N'<existing_database_scoped_credential_name>';   
EXEC sp_rda_reauthorize_db @credential = @credentialName, @with_copy = 1;  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [sp_rda_deauthorize_db &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sys-sp-rda-deauthorize-db-transact-sql.md)   
 [Stretch Database](../../sql-server/stretch-database/stretch-database.md)  
  
  
