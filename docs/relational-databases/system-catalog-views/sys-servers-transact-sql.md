---
description: sys.servers(Transact-SQL)
title: sys. servers (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 06/16/2020
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- servers_TSQL
- sys.servers_TSQL
- servers
- sys.servers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.servers catalog view
ms.assetid: 4e774ed9-4e83-4726-9f1d-8efde8f9feff
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: a3befa2740bd11fcd88233cef3000deec0d7006e
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809329"
---
# <a name="sysservers-transact-sql"></a>sys.servers(Transact-SQL)
[!INCLUDE [SQL Server - ASDBMI](../../includes/applies-to-version/sql-asdbmi.md)]

  등록 된 원격 서버 또는 등록 된 원격 서버 당 행과 **server_id** = 0 인 로컬 서버에 대 한 행을 포함 합니다.  

|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|연결된 서버의 로컬 ID입니다.|  
|**name**|**sysname**|**Server_id** = 0 인 경우 반환 되는 값은 서버 이름입니다.<br /><br /> **Server_id** > 0 인 경우 반환 되는 값은 연결 된 서버의 로컬 이름입니다.|  
|**product**|**sysname**|연결된 서버의 제품 이름입니다. "SQL Server" 값은의 다른 인스턴스를 나타냅니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|**공급자별**|**sysname**|연결된 서버에 연결하기 위한 OLE DB 공급자 이름입니다.<br /><br />부터 [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)] "SQLNCLI" 값은 기본적으로 [Microsoft OLE DB Driver for SQL SERVER (MSOLEDBSQL)](../../connect/oledb/oledb-driver-for-sql-server.md) 에 매핑됩니다. 이전 버전에서 값 "SQLNCLI"는 [SQLNCLI11 (SQL Server Native Client OLE DB 공급자)](../../relational-databases/native-client/sql-server-native-client.md)에 매핑됩니다.|  
|**data_source**|**nvarchar(4000)**|OLE DB 데이터 원본 연결 속성입니다.|  
|**location**|**nvarchar(4000)**|OLE DB 위치 연결 속성입니다. 이 속성이 없으면 NULL입니다.|  
|**provider_string**|**nvarchar(4000)**|OLE DB 공급자 문자열 연결 속성입니다.<br /><br /> 호출자에 게 권한이 없는 경우는 NULL입니다 `ALTER ANY LINKED SERVER` .|  
|**catalog**|**sysname**|카탈로그 연결 속성을 OLE DB 합니다. 이 속성이 없으면 NULL입니다.|  
|**connect_timeout**|**int**|연결 제한 시간(초)이며 제한 시간이 없으면 0입니다.|  
|**query_timeout**|**int**|쿼리 제한 시간(초)이며 제한 시간이 없으면 0입니다.|  
|**is_linked**|**bit**|0 = 다른 RPC 및 분산 트랜잭션 동작을 통해 **sp_addserver**를 사용 하 여 추가 된 이전 스타일의 서버입니다.<br /><br /> 1 = 표준 연결된 서버입니다.|  
|**is_remote_login_enabled**|**bit**|이 서버에 들어오는 원격 로그인을 허용하도록 RPC 옵션이 설정됩니다.|  
|**is_rpc_out_enabled**|**bit**|이 서버에서 보내는 RPC가 가능합니다.|  
|**is_data_access_enabled**|**bit**|서버에서 분산 쿼리 사용이 가능합니다.|  
|**is_collation_compatible**|**bit**|사용할 수 있는 데이터 정렬 정보가 없을 경우 원격 데이터의 데이터 정렬이 로컬 데이터와 호환되는 것으로 가정합니다.|  
|**uses_remote_collation**|**bit**|1인 경우 원격 서버에 의해 보고된 데이터 정렬을 사용하고, 그렇지 않으면 다음 열에 의해 지정된 데이터 정렬을 사용합니다.|  
|**collation_name**|**sysname**|사용할 데이터 정렬의 이름입니다. 로컬 데이터 정렬을 사용하는 경우에는 NULL입니다.|  
|**lazy_schema_validation**|**bit**|값이 1인 경우 쿼리를 시작할 때 스키마 유효성 검사를 하지 않습니다.|  
|**is_system**|**bit**|이 서버는 내부 시스템에 의해서만 액세스할 수 있습니다.|  
|**is_publisher**|**bit**|서버가 복제 게시자입니다.|  
|**is_subscriber**|**bit**|서버가 복제 구독자입니다.|  
|**is_distributor**|**bit**|서버가 복제 배포자입니다.|  
|**is_nonsql_subscriber**|**bit**|서버가 SQL Server 이외 복제 구독자입니다.|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|1로 설정하면 원격 저장 프로시저를 호출하여 분산 트랜잭션이 시작하고 MS DTC를 사용하여 이 트랜잭션을 참여시킵니다. 자세한 내용은 [sp_serveroption&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md)의 데이터에 액세스하는 방법을 보여 줍니다.|  
|**modify_date**|**datetime**|서버 정보가 마지막으로 변경된 날짜입니다.|  
|**is_rda_server**|**bit**|**적용 대상:** 부터 시작 [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 합니다.<br /><br />서버에서 원격 데이터 보관 사용 (스트레치 사용)입니다. 자세한 내용은 [서버에서 Stretch Database 사용](../../sql-server/stretch-database/enable-stretch-database-for-a-database.md#EnableTSQLServer)을 참조 하세요.|
  
## <a name="permissions"></a>사용 권한  
 호출자에 게 ALTER ANY 연결 된 서버 권한이 없으면 **provider_string** 의 값은 항상 NULL입니다.  
  
 로컬 서버 (**server_id** = 0)를 보는 데 사용 권한이 필요 하지 않습니다.  
  
 연결 된 서버 또는 원격 서버를 만들 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **public** 서버 역할에 대 한 기본 로그인 매핑을 만듭니다. 기본 로그인 매핑은 모든 로그인이 모든 연결 된 서버 및 원격 서버를 볼 수 있음을 의미 합니다. 이러한 서버에 대 한 표시 여부를 제한 하려면 [sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) 를 실행 하 고 *locallogin* 매개 변수에 NULL을 지정 하 여 기본 로그인 매핑을 제거 합니다.  
  
 기본 로그인 매핑이 삭제되면 연결된 로그인 또는 원격 로그인으로 명시적으로 추가된 사용자만 로그인 권한이 있으며 연결된 서버 또는 원격 서버를 볼 수 있습니다.  기본 로그인 매핑 후에 모든 연결 된 서버 및 원격 서버를 보려면 다음 권한이 필요 합니다.  
  
- `ALTER ANY LINKED SERVER` 또는 `ALTER ANY LOGIN ON SERVER`  
- **Setupadmin** 또는 **sysadmin** 고정 서버 역할의 멤버 자격  
  
## <a name="see-also"></a>참고 항목  
 [카탈로그 뷰&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [연결 된 서버 카탈로그 뷰 &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
