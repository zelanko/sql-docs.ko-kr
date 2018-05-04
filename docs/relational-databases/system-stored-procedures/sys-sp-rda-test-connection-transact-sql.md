---
title: sys.sp_rda_test_connection (Transact SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_rda_test_connection
- sys.sp_rda_test_connection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_rda_test_connection stored procedure
ms.assetid: e2ba050c-d7e3-4f33-8281-c9b525b4edb4
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ec0a7675b28edecfeed5ecab89afc984f1528bb0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="syssprdatestconnection-transact-sql"></a>sys.sp_rda_test_connection (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  원격 Azure 서버에 SQL Server에서 연결을 테스트 하 고 데이터 마이그레이션을 방해할 수 있는 문제를 보고 합니다.  
  
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
  
-   에 대 한 값을 제공 하는 경우 **@database_name**, 지정된 된 데이터베이스는 스트레치 지원 하지 않습니다 다음에 대 한 값을 제공 해야 하지만 **@server_address**합니다.  
  
-   에 대 한 값을 제공 하는 경우 **@database_name**, 지정한 데이터베이스는 스트레치 사용 하 고 다음 값을 제공 하지 않아도 **@server_address**합니다. 에 대 한 값을 제공 하는 경우 **@server_address**, 저장된 프로시저를 무시 하 고 스트레치 사용 데이터베이스와 연결 된 기존 Azure 서버를 이미 사용 하 여 합니다.  
  
 @azure_username = N'*azure_username*  
 원격 Azure 서버에 대 한 사용자 이름입니다.  
  
 @azure_password = N'*azure_password*'  
 원격 Azure 서버에 대 한 암호입니다.  
  
 @credential_name = N'*credential_name*'  
 사용자 이름 및 암호를 제공 하는 대신 스트레치 사용 데이터베이스에 저장 된 자격 증명의 이름을 제공할 수 있습니다.  
  
## <a name="return-code-values"></a>반환 코드 값  
 경우 **성공**, sp_rda_test_connection 심각도 EX_INFO 14855 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_SUCCEEDED) 오류를 반환 하 고 성공 코드를 반환 합니다.  
  
 경우 **오류**, sp_rda_test_connection 심각도 EX_USER 14856 (STRETCH_MAJOR, STRETCH_CONNECTION_TEST_PROC_FAILED) 오류를 반환 하 고 오류 코드를 반환 합니다.  
  
## <a name="result-sets"></a>결과 집합  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|link_state|int|에 대 한 값에 해당 하는 다음 값 중 하나 **link_state_desc**합니다.<br /><br /> -   0<br />-   1<br />-   2<br />-   3<br />-   4|  
|link_state_desc|varchar(32)|에 대 한 값 앞에 해당 하는 다음 값 중 하나 **link_state**합니다.<br /><br /> -정상<br />     SQL Server와 원격 Azure 서버는 정상 상태입니다.<br />-   ERROR_AZURE_FIREWALL<br />     Azure 방화벽이 SQL Server와 원격 Azure 서버 간의 링크 수 없습니다.<br />-ERROR_NO_CONNECTION<br />     SQL Server가 원격 Azure 서버에 연결할 수 없습니다.<br />-   ERROR_AUTH_FAILURE<br />     인증 실패 때문에 SQL Server와 원격 Azure 서버 간의 링크 수 없습니다.<br />-오류<br />     인증 문제, 연결 문제 또는 방화벽 문제가 없는 오류 때문에 SQL Server와 원격 Azure 서버 간의 링크 수 없습니다.|  
|error_number|int|오류의 수입니다. 오류가 없으면 이면이 필드는 NULL입니다.|  
|error_message|nvarchar(1024)|오류 메시지. 오류가 없으면 이면이 필드는 NULL입니다.|  
  
## <a name="permissions"></a>Permissions  
 Db_owner 권한이 필요합니다.  
  
## <a name="examples"></a>예  
  
### <a name="check-the-connection-from-sql-server-to-the-remote-azure-server"></a>원격 Azure 서버에 SQL Server 연결 확인  
  
```sql  
EXECUTE sys.sp_rda_test_connection @database_name = N'<Stretch-enabled database>'  
GO  
  
```  
  
 결과 표시 SQL Server가 원격 Azure 서버에 연결할 수 없습니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|2|ERROR_NO_CONNECTION|*\<연결 관련 오류 번호 >*|*\<연결 관련 오류 메시지 >*|  
  
### <a name="check-the-azure-firewall"></a>Azure 방화벽 확인  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 결과 Azure 방화벽이 SQL Server와 원격 Azure 서버 간의 링크를 방지 하 고 있는지 보여 줍니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|1.|ERROR_AZURE_FIREWALL|*\<방화벽와 관련 된 오류 번호 >*|*\<방화벽 관련 오류 메시지 >*|  
  
### <a name="check-authentication-credentials"></a>인증 자격 증명 확인  
  
```sql  
USE <Stretch-enabled database>  
GO  
EXECUTE sys.sp_rda_test_connection  
GO  
  
```  
  
 결과는 인증이 실패 하는 SQL Server와 원격 Azure 서버 간의 링크를 방지 하 고 있는지 보여 줍니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|3|ERROR_AUTH_FAILURE|*\<인증 관련 오류 번호 >*|*\<인증 관련 오류 메시지 >*|  
  
### <a name="check-the-status-of-the-remote-azure-server"></a>원격 Azure 서버 상태 확인  
  
```sql  
USE <SQL Server database>  
GO  
EXECUTE sys.sp_rda_test_connection   
    @server_address = N'<server name>.database.windows.net',   
    @azure_username = N'<user name>',   
    @azure_password = N'<password>'  
GO  
  
```  
  
 결과 표시 연결 상태가 정상 인지 확인 하 고 지정된 된 데이터베이스에 대 한 스트레치 데이터베이스를 사용할 수 있습니다.  
  
|link_state|link_state_desc|error_number|error_message|  
|-----------------|-----------------------|-------------------|--------------------|  
|0|HEALTHY|NULL|NULL|  
  
  
