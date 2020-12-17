---
title: tablediff 유틸리티
description: tablediff 유틸리티를 사용하면 두 테이블에 포함된 데이터의 불일치 여부를 비교하고 복제 토폴로지의 데이터 불일치 문제를 해결할 수 있습니다.
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- comparing data
- tablediff utility
- tables [SQL Server replication]
- table comparisons [SQL Server]
- command prompt utilities [SQL Server], tablediff
- troubleshooting [SQL Server replication], non-convergence
- non-convergence [SQL Server]
ms.assetid: 3c3cb865-7a4d-4d66-98f2-5935e28929fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017'
ms.openlocfilehash: 71becc4645aa71a3e6d60a00766b913546ff7c22
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97463714"
---
# <a name="tablediff-utility"></a>tablediff 유틸리티
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  **tablediff** 유틸리티는 두 테이블에 포함된 데이터의 불일치 여부를 비교하는 데 사용되며, 복제 토폴로지의 데이터 불일치 문제를 해결하는 데 특히 유용합니다. 명령 프롬프트나 배치 파일에서 이 유틸리티를 사용하여 다음 태스크를 수행할 수 있습니다.  
  
-   복제 게시자 역할을 하는 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 있는 원본 테이블과 복제 구독자 역할을 하는 하나 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스에 있는 대상 테이블을 행 단위로 비교할 수 있습니다.  
  
-   행 개수와 스키마만 비교하여 비교 작업을 빨리 수행합니다.  
  
-   열 수준에서 비교할 수 있습니다.  
  
-   대상 서버의 불일치를 해결하는 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 생성하여 원본 테이블과 대상 테이블을 일치시킬 수 있습니다.  
  
-   결과를 출력 파일이나 대상 데이터베이스의 테이블에 기록할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
tablediff   
[ -? ] |   
{  
        -sourceserver source_server_name[\instance_name]  
        -sourcedatabase source_database  
        -sourcetable source_table_name   
    [ -sourceschema source_schema_name ]  
    [ -sourcepassword source_password ]  
    [ -sourceuser source_login ]  
    [ -sourcelocked ]  
        -destinationserver destination_server_name[\instance_name]  
        -destinationdatabase subscription_database   
        -destinationtable destination_table   
    [ -destinationschema destination_schema_name ]  
    [ -destinationpassword destination_password ]  
    [ -destinationuser destination_login ]  
    [ -destinationlocked ]  
    [ -b large_object_bytes ]   
    [ -bf number_of_statements ]   
    [ -c ]   
    [ -dt ]   
    [ -et table_name ]   
    [ -f [ file_name ] ]   
    [ -o output_file_name ]   
    [ -q ]   
    [ -rc number_of_retries ]   
    [ -ri retry_interval ]   
    [ -strict ]  
    [ -t connection_timeouts ]   
}  
```  
  
## <a name="arguments"></a>인수  
 [ **-?** ]  
 지원되는 매개 변수 목록을 반환합니다.  
  
 **-sourceserver** _source_server_name_[ **\\** _instance\_name_]  
 원본 서버의 이름입니다. *의 기본 인스턴스에 대해* source_server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]을 지정합니다. _의 명명된 인스턴스에 대해_ **\\** _source_server_name_ instance_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]을 지정합니다.  
  
 **-sourcedatabase** _source_database_  
 원본 데이터베이스의 이름입니다.  
  
 **-sourcetable** _source_table_name_  
 검사할 원본 테이블의 이름입니다.  
  
 **-sourceschema** _source_schema_name_  
 원본 테이블의 스키마 소유자입니다. 기본적으로 테이블 소유자를 dbo로 간주합니다.  
  
 **-sourcepassword** _source_password_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 원본 서버에 연결하는 데 사용되는 로그인 암호입니다.  
  
> [!IMPORTANT]  
>  가능하면 런타임 동안 보안 자격 증명을 지정합니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
 **-sourceuser** _source_login_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 원본 서버에 연결하는 데 사용되는 로그인입니다. *source_login* 을 지정하지 않으면 원본 서버에 연결할 때 Windows 인증이 사용됩니다. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-sourcelocked**  
 비교를 수행하는 동안 TABLOCK 및 HOLDLOCK 테이블 힌트를 사용하여 원본 테이블이 잠깁니다.  
  
 **-destinationserver** _destination_server_name_[ **\\** _instance_name_]  
 대상 서버의 이름입니다. *의 기본 인스턴스에 대해* destination_server_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]을 지정합니다. _의 명명된 인스턴스에 대해_ **\\** _destination_server_name_ instance_name [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]을 지정합니다.  
  
 **-destinationdatabase** _subscription_database_  
 대상 데이터베이스의 이름입니다.  
  
 **-destinationtable** _destination_table_  
 대상 테이블의 이름입니다.  
  
 **-destinationschema** _destination_schema_name_  
 대상 테이블의 스키마 소유자입니다. 기본적으로 테이블 소유자를 dbo로 간주합니다.  
  
 **-destinationpassword** _destination_password_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 대상 서버에 연결하는 데 사용되는 로그인 암호입니다.  
  
> [!IMPORTANT]  
>  가능하면 런타임 동안 보안 자격 증명을 지정합니다. 스크립트 파일에 자격 증명을 저장해야 하는 경우에는 무단으로 액세스하지 못하도록 파일에 보안을 설정해야 합니다.  
  
 **-destinationuser** _destination_login_  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증을 사용하여 대상 서버에 연결하는 데 사용되는 로그인입니다. *destination_login* 을 지정하지 않으면 대상 서버에 연결할 때 Windows 인증이 사용됩니다. [!INCLUDE[ssNoteWinAuthentication](../includes/ssnotewinauthentication-md.md)]  
  
 **-destinationlocked**  
 비교를 수행하는 동안 TABLOCK 및 HOLDLOCK 테이블 힌트를 사용하여 대상 테이블이 잠깁니다.  
  
 **-b** _large_object_bytes_  
 큰 개체 데이터 형식 열에 대해 비교할 바이트 수입니다. 이 데이터 형식에는 **text**, **ntext**, **이미지**, **varchar(max)** , **nvarchar(max)** 및 **varbinary(max)** 가 포함됩니다. *large_object_bytes* 는 기본적으로 열 크기로 설정됩니다. *large_object_bytes* 에 지정한 바이트 수를 초과하는 데이터는 비교되지 않습니다.  
  
 **-bf**  _number_of_statements_  
 [!INCLUDE[tsql](../includes/tsql-md.md)] -f [!INCLUDE[tsql](../includes/tsql-md.md)] 옵션을 사용할 경우 현재 **스크립트 파일에 쓸** 문의 수입니다. [!INCLUDE[tsql](../includes/tsql-md.md)] 문의 수가 *number_of_statements* 를 초과하면 새 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트 파일이 생성됩니다.  
  
 **-c**  
 열 수준에서 차이점을 비교합니다.  
  
 **-dt**  
 *table_name* 에 지정된 결과 테이블이 이미 있는 경우 삭제합니다.  
  
 **-et** _table_name_  
 만들 결과 테이블의 이름을 지정합니다. 이 테이블이 이미 있을 경우 **-DT** 를 사용해야 합니다. 그렇지 않으면 작업이 실패합니다.  
  
 **-f** [ *file_name* ]  
 대상 서버의 테이블을 원본 서버의 테이블과 일치시키는 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트를 생성합니다. 생성된 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트 파일의 이름과 경로를 필요에 따라 지정할 수 있습니다. *file_name* 을 지정하지 않으면 유틸리티가 실행되는 디렉터리에 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트 파일이 생성됩니다.  
  
 **-o** _output_file_name_  
 출력 파일의 전체 이름 및 경로입니다.  
  
 **-q**  
 행 개수와 스키마만 비교하여 비교 작업을 빨리 수행합니다.  
  
 **-rc** _number_of_retries_  
 유틸리티가 실패한 작업을 다시 시도하는 횟수입니다.  
  
 **-ri** _retry_interval_  
 다시 시도 작업 사이의 대기 간격(초)입니다.  
  
 **-strict**  
 원본 스키마와 대상 스키마를 엄격하게 비교합니다.  
  
 **-t** _connection_timeouts_  
 원본 서버 및 대상 서버에 대한 연결 제한 시간(초)을 설정합니다.  
  
## <a name="return-value"></a>Return Value  
  
|값|Description|  
|-----------|-----------------|  
|**0**|Success|  
|**1**|오류|  
|**2**|테이블 차이|  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 이외 서버에서는 **tablediff** 유틸리티를 사용할 수 없습니다.  
  
 데이터 형식이 **sql_variant** 인 열이 있는 테이블은 지원되지 않습니다.  
  
 기본적으로 **tablediff** 유틸리티는 원본 열과 대상 열 간에 다음 데이터 형식 매핑을 지원합니다.  
  
|원본 데이터 형식|대상 데이터 형식|  
|----------------------|---------------------------|  
|**tinyint**|**smallint**, **int** 또는 **bigint**|  
|**smallint**|**int** 또는 **bigint**|  
|**int**|**bigint**|  
|**timestamp**|**varbinary**|  
|**varchar(max)**|**text**|  
|**nvarchar(max)**|**ntext**|  
|**varbinary(max)**|**image**|  
|**text**|**varchar(max)**|  
|**ntext**|**nvarchar(max)**|  
|**image**|**varbinary(max)**|  
  
 **-strict** 옵션을 사용하여 이러한 매핑을 허용하지 않고 유효성 검사를 엄격하게 수행할 수 있습니다.  
  
 비교할 원본 테이블에는 하나 이상의 기본 키, ID 또는 ROWGUID 열이 있어야 합니다. **-strict** 옵션을 사용하는 경우에는 대상 테이블에도 기본 키, ID 또는 ROWGUID 열이 있어야 합니다.  
  
 대상 테이블을 일치시키기 위해 생성된 [!INCLUDE[tsql](../includes/tsql-md.md)] 스크립트에는 다음 데이터 형식이 포함되지 않습니다.  
  
-   **varchar(max)**  
  
-   **nvarchar(max)**  
  
-   **varbinary(max)**  
  
-   **timestamp**  
  
-   **xml**  
  
-   **text**  
  
-   **ntext**  
  
-   **image**  
  
## <a name="permissions"></a>사용 권한  
 테이블을 비교하려면 비교할 테이블 개체에 대한 SELECT ALL 권한이 있어야 합니다.  
  
 **-et** 옵션을 사용하려면 db_owner 고정 데이터베이스 역할의 멤버이거나 적어도 구독 데이터베이스에 대한 CREATE TABLE 권한과 대상 서버의 대상 소유자 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
 **-dt** 옵션을 사용하려면 db_owner 고정 데이터베이스 역할의 멤버이거나 적어도 대상 서버의 대상 소유자 스키마에 대한 ALTER 권한이 있어야 합니다.  
  
 **-o** 또는 **-f** 옵션을 사용하려면 지정된 파일 디렉터리 위치에 대한 쓰기 권한이 있어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
 [복제된 테이블의 차이점 비교&#40;복제 프로그래밍&#41;](../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)  
  
  
