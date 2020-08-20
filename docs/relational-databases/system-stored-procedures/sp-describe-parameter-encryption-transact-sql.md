---
description: sp_describe_parameter_encryption (Transact-sql)
title: sp_describe_parameter_encryption (Transact-sql) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: vanto
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_describe_parameter_encryption
- sp_describe_parameter_encryption_TSQL
- sys.sp_describe_parameter_encryption
- sys.sp_describe_parameter_encryption_TSQL
helpviewer_keywords:
- sp_describe_parameter_encryption
ms.assetid: 706ed441-2881-4934-8d5e-fb357ee067ce
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 35bf38e3c6ac85fe27af595571785f8d34a6f0d4
ms.sourcegitcommit: 331b8495e4ab37266945c81ff5b93d250bdaa6da
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88646493"
---
# <a name="sp_describe_parameter_encryption-transact-sql"></a>sp_describe_parameter_encryption (Transact-sql)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  지정 된 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 해당 매개 변수를 분석 하 여 Always Encrypted 기능을 사용 하 여 보호 되는 데이터베이스 열에 해당 하는 매개 변수를 확인 합니다. 암호화 된 열에 해당 하는 매개 변수에 대 한 암호화 메타 데이터를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>인수  
 [ \@ tsql =] ' transact-sql SQL_batch '  
 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. SQL_batch는 nvarchar (n) 또는 nvarchar (max) 일 수 있습니다.  
  
 [ \@ params =] N'parameters '  
 * \@ Params* 는 transact-sql 일괄 처리에 대 한 매개 변수에 대 한 선언 문자열을 제공 합니다 .이는 sp_executesql와 비슷합니다. 매개 변수는 nvarchar (n) 또는 nvarchar (max) 일 수 있습니다.  
  
 _Batch에 포함 된 모든 매개 변수의 정의를 포함 하는 하나의 문자열입니다 [!INCLUDE[tsql](../../includes/tsql-md.md)] . 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. *n* 은 추가 매개 변수 정의를 나타내는 자리 표시자입니다. 문에 지정 된 모든 매개 변수는 * \@ params*에 정의 되어야 합니다. 문의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 일괄 처리에 매개 변수가 없는 경우 * \@ params* 가 필요 하지 않습니다. NULL이 이 매개 변수의 기본값입니다.  
  
## <a name="return-value"></a>반환 값  
 0은 성공을 나타냅니다. 다른 모든 항목은 실패를 표시 합니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_describe_parameter_encryption** 는 두 개의 결과 집합을 반환 합니다.  
  
-   데이터베이스 열에 대해 구성 된 암호화 키를 설명 하는 결과 집합입니다. 지정 된 문의 매개 변수는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 해당 합니다.  
  
-   특정 매개 변수를 암호화 하는 방법을 설명 하는 결과 집합입니다. 이 결과 집합은 첫 번째 결과 집합에 설명 된 키를 참조 합니다.  
  
 첫 번째 결과 집합의 각 행은 키 쌍을 설명 합니다. 암호화 된 열 암호화 키 및 해당 열 마스터 키입니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|결과 집합에 있는 행의 Id입니다.|  
|**database_id**|**int**|데이터베이스 id입니다.|  
|**column_encryption_key_id**|**int**|열 암호화 키 id입니다. 참고:이 id는 [column_encryption_keys &#40;transact-sql&#41;](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) 카탈로그 뷰의 행을 나타냅니다.|  
|**column_encryption_key_version**|**int**|다음에 사용하도록 예약됩니다. 현재에는 항상 1이 포함 되어 있습니다.|  
|**column_encryption_key_metadata_version**|**binary (8)**|열 암호화 키를 만든 시간을 나타내는 타임 스탬프입니다.|  
|**column_encryption_key_encrypted_value**|**varbinary(4000)**|열 암호화 키의 암호화 된 값입니다.|  
|**column_master_key_store_provider_name**|**sysname**|열 암호화 키의 암호화 된 값을 생성 하는 데 사용 된 열 마스터 키를 포함 하는 키 저장소의 공급자 이름입니다.|  
|**column_master_key_path**|**nvarchar(4000)**|열 암호화 키의 암호화 된 값을 생성 하는 데 사용 된 열 마스터 키의 키 경로입니다.|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|열 암호화 키의 암호화 값을 생성 하는 데 사용 되는 암호화 알고리즘의 이름입니다.|  
  
 두 번째 결과 집합의 각 행에는 하나의 매개 변수에 대 한 암호화 메타 데이터가 포함 됩니다.  
  
|열 이름|데이터 형식|Description|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|결과 집합에 있는 행의 Id입니다.|  
|**parameter_name**|**sysname**|* \@ Params* 인수에 지정 된 매개 변수 중 하나의 이름입니다.|  
|**column_encryption_algorithm**|**tinyint**|열에 대해 구성 된 암호화 알고리즘을 나타내는 코드입니다. 매개 변수는에 해당 합니다. 현재 지원 되는 값은 **AEAD_AES_256_CBC_HMAC_SHA_256**의 경우 2입니다.|  
|**column_encryption_type**|**tinyint**|열에 대해 구성 된 암호화 유형을 나타내는 코드입니다. 매개 변수는에 해당 합니다. 지원되는 값은<br /><br /> 0-일반 텍스트 (열이 암호화 되지 않음)<br /><br /> 1-임의 암호화<br /><br /> 2-결정적 암호화|  
|**column_encryption_key_ordinal**|**int**|첫 번째 결과 집합의 행에 대 한 코드입니다. 참조 된 행은 열에 대해 구성 된 열 암호화 키를 설명 하 고 매개 변수는에 해당 합니다.|  
|**column_encryption_normalization_rule_version**|**tinyint**|유형 정규화 알고리즘의 버전 번호입니다.|  
  
## <a name="remarks"></a>설명  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Always Encrypted를 지 원하는 클라이언트 드라이버는 **sp_describe_parameter_encryption** 를 자동으로 호출 하 여 응용 프로그램에서 실행 한 매개 변수가 있는 쿼리에 대 한 암호화 메타 데이터를 검색 합니다. 그런 다음, 드라이버는 암호화 메타 데이터를 사용 하 여 Always Encrypted로 보호 되는 데이터베이스 열에 해당 하는 매개 변수의 값을 암호화 하 고, 데이터베이스 엔진에 쿼리를 보내기 전에 응용 프로그램에서 전송한 일반 텍스트 매개 변수 값을 암호화 된 매개 변수 값으로 대체 합니다.  
  
## <a name="permissions"></a>사용 권한  
 데이터베이스에서 **VIEW ANY COLUMN ENCRYPTION key** Definition 및 **VIEW ANY COLUMN MASTER KEY definition** 권한이 필요 합니다.  
  
## <a name="examples"></a>예제  
  
```sql  
CREATE COLUMN MASTER KEY [CMK1]  
WITH  
(  
       KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',  
    KEY_PATH = N'CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305'  
);  
GO  
  
CREATE COLUMN ENCRYPTION KEY [CEK1]  
WITH VALUES  
(  
       COLUMN_MASTER_KEY = [CMK1],  
    ALGORITHM = 'RSA_OAEP',  
    ENCRYPTED_VALUE =   
0x016E000001630075007200720065006E00740075007300650072002F006D007  
9002F00610036003600620062003000660036006400640037003000620064006  
6006600300032006200360032006400300066003800370065003300340030003  
200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF991  
37B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA51  
7A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6  
686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015B  
DB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8  
C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE3  
74DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A3472  
3276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550E  
C5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E0  
35175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D8  
01ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B  
4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF8  
1A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202F  
C24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B0195883360  
4707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E  
9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C  
3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085  
);  
GO  
  
CREATE TABLE t1 (  
c1 INT ENCRYPTED WITH (  
    COLUMN_ENCRYPTION_KEY = [CEK_Auto1],   
    ENCRYPTION_TYPE = Randomized,   
    ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256') NULL,  
);  
  
EXEC sp_describe_parameter_encryption N'INSERT INTO t1 VALUES(@c1)',  N'@c1 INT';  
```  
  
 첫 번째 결과 집합은 다음과 같습니다.  
  
|column_encryption_key_ordinal|database_id|column_encryption_key_id|column_encryption_key_version|column_encryption_key_metadata_version|column_encryption_key_encrypted_value|  
|--------------------------------------|------------------|---------------------------------|--------------------------------------|------------------------------------------------|-----------------------------------------------|  
|1|5|1|1|0x99EDA60083A50000|0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE24392D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98 AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B386487CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085|  
  
 (결과가 계속 됩니다.)  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 두 번째 결과 집합은 다음과 같습니다.  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@c1|1|1|  
  
 (결과가 계속 됩니다.)  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>관련 항목  
 [Always Encrypted](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [Always Encrypted를 사용 하 여 응용 프로그램 개발](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
