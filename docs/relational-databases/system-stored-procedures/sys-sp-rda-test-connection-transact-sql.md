---
title: sys. sp_rda_test_connection (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 69b3b9eae6c292b9501dfbe74b84d7399304a291
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305156"
---
# <a name="syssp_rda_test_connection-transact-sql"></a>sys. sp_rda_test_connection (Transact-sql)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  SQL Server에서 원격 Azure 서버로의 연결을 테스트 하 고 데이터 마이그레이션을 방해할 수 있는 문제를 보고 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
EXECUTE sys.sp_rda_test_connection  
   @database_name = N'db_name',   
   @server_address = N'azure_server_fully_qualified_address',  
   @azure_username = N'azure_username',   
   @azure_password = N'azure_password',  
   @credential_name = N'credential_name'  
  
```  
  
## <a name="arguments"></a>인수  
 @database_name = N'*db_name*'  
 스트레치 사용 SQL Server 데이터베이스의 이름입니다. 이 매개 변수는 선택 사항입니다.  
  
 @server_address = N'*azure_server_fully_qualified_address*'  
 Azure 서버의 정규화 된 주소입니다.  
  
-   **\@database_name**에 값을 제공 했지만 지정 된 데이터베이스가 스트레치를 사용 하도록 설정 되어 있지 않은 경우에는 **\@server_address**에 대 한 값을 제공 해야 합니다.  
  
-   **\@database_name**에 값을 제공 하 고 지정 된 데이터베이스를 스트레치를 사용 하는 경우 **\@server_address**에 대 한 값을 제공할 필요가 없습니다. **\@server_address**값을 제공 하는 경우 저장 프로시저는이를 무시 하 고 스트레치 사용 데이터베이스에 이미 연결 되어 있는 기존 Azure 서버를 사용 합니다.  
  
 @azure_username = N'*azure_username*  
 원격 Azure 서버에 대 한 사용자 이름입니다.  
  
 @azure_password = N'*azure_password*'  
 원격 Azure 서버에 대 한 암호입니다.  
  
 @credential_name = N'*credential_name*'  
 사용자 이름 및 암호를 제공 하는 대신 스트레치 사용 데이터베이스에 저장 된 자격 증명의 이름을 제공할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 **성공**하는 경우 sp_rda_test_connection는 심각도 EX_INFO 및 성공 반환 코드와 함께 오류 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED)을 반환 합니다.  
  
 오류가 **발생 하는**경우 sp_rda_test_connection는 심각도 EX_USER 및 오류 반환 코드와 함께 오류 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED)을 반환 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|link_state|int|**Link_state_desc**값에 해당 하는 다음 값 중 하나입니다.<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar(32)|**Link_state**의 앞에 있는 값에 해당 하는 다음 값 중 하나입니다.<br /><br /> -정상<br />     SQL Server와 원격 Azure 서버가 정상입니다.<br />-   ERROR_AZURE_FIREWALL<br />     Azure 방화벽에서 SQL Server와 원격 Azure 서버 간의 연결을 방지 하 고 있습니다.<br />-   ERROR_NO_CONNECTION<br />     SQL Server 원격 Azure 서버에 연결할 수 없습니다.<br />-   ERROR_AUTH_FAILURE<br />     인증 오류가 발생 하 여 SQL Server와 원격 Azure 서버 간의 연결을 방지 하 고 있습니다.<br />-   ERROR<br />     인증 문제, 연결 문제 또는 방화벽 문제로 인 한 오류는 SQL Server와 원격 Azure 서버 간의 연결을 방지 하는 것입니다.|  
|error_number|int|오류 수입니다. 오류가 없으면이 필드는 NULL입니다.|  
|error_message|nvarchar(1024)|오류 메시지. 오류가 없으면이 필드는 NULL입니다.|  
  
## <a name="permissions"></a>사용 권한  
 Db_owner 권한이 필요 합니다.  
  
## <a name="examples"></a>예  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>SQL Server에서 원격 Azure 서버에 대 한 연결 확인  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 결과는 SQL Server 원격 Azure 서버에 연결할 수 없음을 보여 줍니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*연결 관련 오류 번호를 \<>*|*연결 관련 오류 메시지를 \<>*|  
  
### <a name="check-the-azure-firewall"></a>Azure 방화벽 확인  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 결과는 Azure 방화벽이 SQL Server와 원격 Azure 서버 간의 링크를 차단 하 고 있음을 보여 줍니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1\.|ERROR_AZURE_FIREWALL|*\<방화벽 관련 오류 번호 >*|*방화벽 관련 오류 메시지를 \<>*|  
  
### <a name="check-authentication-credentials"></a>인증 자격 증명 확인  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 결과는 인증 실패로 인해 SQL Server와 원격 Azure 서버 간의 링크를 방지 하 고 있음을 보여 줍니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<인증 관련 오류 번호 >*|*인증 관련 오류 메시지를 \<>*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>원격 Azure 서버의 상태를 확인 합니다.  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 그러면 연결이 정상 상태 이며 지정 된 데이터베이스에 대 한 Stretch Database를 사용 하도록 설정할 수 있습니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
