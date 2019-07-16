---
title: sp_describe_parameter_encryption (TRANSACT-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
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
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 377a1e342970e9593b37924c3739ee7a706d5264
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68053029"
---
# <a name="spdescribeparameterencryption-transact-sql"></a>sp_describe_parameter_encryption (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  지정 된 분석 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문과 Always Encrypted 기능을 사용 하 여 보호 되는 데이터베이스 열에 해당 하는 매개 변수를 확인 하려면 해당 매개 변수입니다. 암호화 된 열에 해당 하는 매개 변수 암호화 메타 데이터를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
sp_describe_parameter_encryption   
    [ @tsql = ] N'Transact-SQL_batch' ,   
    [ @params = ] N'parameters'   
[ ;]  
```  
  
## <a name="arguments"></a>인수  
 [ \@tsql =] ' Transact-SQL_batch'  
 하나 이상의 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문입니다. Transact SQL_batch nvarchar (n) 또는 nvarchar (max) 수 있습니다.  
  
 [ \@params =] N'parameters'  
 *\@params* TRANSACT-SQL 일괄 처리는 sp_executesql과 비슷하게 매개 변수에 대 한 선언 문자열을 제공 합니다. 매개 변수는 nvarchar (n) 또는 nvarchar (max) 수 있습니다.  
  
 에 포함 된 모든 매개 변수의 정의 포함 하는 하나의 문자열을 [!INCLUDE[tsql](../../includes/tsql-md.md)]_batch 합니다. 문자열은 유니코드 상수 또는 유니코드 변수여야 합니다. 각 매개 변수의 정의는 매개 변수 이름과 데이터 형식으로 구성됩니다. *n* 추가 매개 변수 정의 나타내는 자리 표시자입니다. 문에 지정 된 모든 매개 변수에서 정의 되어야 합니다  *\@params*합니다. 경우는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 또는 문의 일괄 처리에 매개 변수가 없습니다  *\@params* 필요 하지 않습니다. NULL이 이 매개 변수의 기본값입니다.  
  
## <a name="return-value"></a>반환 값  
 0은 성공을 나타냅니다. 다른 작업 실패를 나타냅니다.  
  
## <a name="result-sets"></a>결과 집합  
 **sp_describe_parameter_encryption** 두 결과 집합을 반환 합니다.  
  
-   데이터베이스 열에 지정 된 매개 변수를 구성 하는 암호화 키를 설명 하는 결과 집합 [!INCLUDE[tsql](../../includes/tsql-md.md)] 에 해당 하는 문입니다.  
  
-   결과 집합을 어떻게 특정 매개 변수를 설명 하는 암호화 되어야 합니다. 이 결과 첫 번째 결과 집합에서 설명 하는 키는 대 한 참조를 설정 합니다.  
  
 첫 번째 결과 집합의 각 행의 키 쌍을 설명합니다. 암호화 된 열 암호화 키 및 해당 열 마스터 키입니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**column_encryption_key_ordinal**|**int**|결과 집합에서 행의 id입니다.|  
|**database_id**|**int**|데이터베이스 id입니다.|  
|**column_encryption_key_id**|**int**|열 암호화 키 id입니다. 참고:이 id의 행을 나타냅니다 합니다 [sys.column_encryption_keys &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md) 카탈로그 뷰에 있습니다.|  
|**column_encryption_key_version**|**int**|나중에 사용하도록 예약되어 있습니다. 현재 1 항상 포함 됩니다.|  
|**column_encryption_key_metadata_version**|**binary(8)**|열 암호화 키의 생성 시간을 나타내는 타임 스탬프입니다.|  
|**column_encryption_key_encrypted_value**|**varbinary(4000)**|열 암호화 키의 암호화 된 값입니다.|  
|**column_master_key_store_provider_name**|**sysname**|열 암호화 키의 암호화 된 값을 생성 하는 데 사용 된 열 마스터 키를 포함 하는 키 저장소에 대 한 공급자의 이름입니다.|  
|**column_master_key_path**|**nvarchar(4000)**|열 암호화 키의 암호화 된 값을 생성 하는 데 사용 된 열 마스터 키의 키 경로입니다.|  
|**column_encryption_key_encryption_algorithm_name**|**sysname**|열 암호화 키의 암호화 값을 생성 하는 데 암호화 알고리즘의 이름입니다.|  
  
 두 번째 결과 집합의 각 행에는 하나의 매개 변수에 대 한 암호화 메타 데이터 포함 되어 있습니다.  
  
|열 이름|데이터 형식|설명|  
|-----------------|---------------|-----------------|  
|**parameter_ordinal**|**int**|결과 집합에서 행의 id입니다.|  
|**parameter_name**|**sysname**|지정 된 매개 변수 중 하나의 이름을 합니다  *\@params* 인수입니다.|  
|**column_encryption_algorithm**|**tinyint**|매개 변수 열에 대해 구성 하는 암호화 알고리즘을 나타내는 코드에 해당 합니다. 현재 지원 되는 값은 다음과 같습니다. 에 대 한 2 **AEAD_AES_256_CBC_HMAC_SHA_256**합니다.|  
|**column_encryption_type**|**tinyint**|매개 변수 열에 대 한 구성 암호화 종류를 나타내는 코드에 해당 합니다. 지원 되는 값은 다음과 같습니다.<br /><br /> 0-일반 텍스트 (열이 암호화 되지 않습니다.)<br /><br /> 1-임의 암호화<br /><br /> 2-결정적 암호화 합니다.|  
|**column_encryption_key_ordinal**|**int**|코드의 첫 번째 결과의 행을 설정합니다. 에 해당 하는 매개 변수, 참조 되는 행의 열에 대해 구성 된 열 암호화 키를 설명 합니다.|  
|**column_encryption_normalization_rule_version**|**tinyint**|버전 번호 형식 정규화 알고리즘입니다.|  
  
## <a name="remarks"></a>설명  
 A [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 상시 암호화 지원 클라이언트 드라이버를 자동으로 호출 **sp_describe_parameter_encryption** 응용 프로그램에서 발급 한 매개 변수가 있는 쿼리에 대 한 암호화 메타 데이터를 검색 합니다. 이후에, 드라이버 암호화 메타 데이터를 사용 하 여 상시 암호화로 보호 된 데이터베이스 열에 해당 하는 매개 변수의 값을 암호화 하 고 암호화를 사용 하 여 응용 프로그램에 제출 된 일반 텍스트 매개 변수 값을 대체 데이터베이스 엔진에 쿼리를 보내기 전에 매개 변수 값입니다.  
  
## <a name="permissions"></a>사용 권한  
 필요 합니다 **VIEW ANY COLUMN ENCRYPTION KEY DEFINITION** 하 고 **VIEW ANY COLUMN MASTER KEY DEFINITION** 데이터베이스의 권한.  
  
## <a name="examples"></a>예  
  
```  
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
|1|5|1|1|0x99EDA60083A50000|0x016E000001630075007200720065006E00740075007300650072002F006D0079002F006100360036006200620030006600360064006400370030006200640066006600300032006200360032006400300066003800370065003300340030003200380038006500360066003900330030003500CA0D0CEC74ECADD1804CF99137B4BD06BBAB15D7EA 74E0C249A779C7768A5B659E0125D24FF827F5EA8CA517A8E197ECA1353BA814C2B0B2E6C8AB36E3AE6A1E972D69C3C573A963ADAB6686CF5D24F95FE43140C4F9AF48FBA7DF2D053F3B4A1F5693A1F905440F8015BDB43AF8A04BE4E045B89876A0097E5FBC4E6A3B9C3C0D278C540E46C53938B8C957B689C4DC095821C465C73117CBA95B758232 F9E5B2FCC7950B8CA00AFE374DE42847E3FBC2FDD277035A2DEF529F4B735C20D980073B4965B4542A34723276A1646998FC6E1C40A3FDB6ABCA98EE2B447F114D2AC7FF8C7D51657550EC5C2BABFFE8429B851272086DCED94332CF18FA854C1D545A28B1EF4BE64F8E035175C1650F6FC5C4702ACF99850A4542B3747EAEC0CC726E091B36CE2439 2D801ECAA684DE344FECE05812D12CD72254A014D42D0EABDA41C89FC4F545E88B4B8781E5FAF40D7199D4842D2BFE904D209728ED4F527CBC169E2904F6E711FF81A8F4C25382A2E778DD2A58552ED031AFFDA9D9D891D98AD82155F93C58202FC24A77F415D4F8EF22419D62E188AC609330CCBD97CEE1AEF8A18B01958833604707FDF03B2B3864 87CC679D7E352D0B69F9FB002E51BCD814D077E82A09C14E9892C1F8E0C559CFD5FA841CEF647DAB03C8191DC46B772E94D579D8C80FE93C3827C9F0AE04D5325BC73111E07EEEDBE67F1E2A73580085|  
  
 (결과 계속 합니다.)  
  
|column_master_key_store_provider_name|column_master_key_path|column_encryption_key_encryption_algorithm_name|  
|------------------------------------------------|-------------------------------|----------------------------------------------------------|  
|MSSQL_CERTIFICATE_STORE|CurrentUser/my/A66BB0F6DD70BDFF02B62D0F87E340288E6F9305|RSA_OAEP|  
  
 두 번째 결과 집합은 다음과 같습니다.  
  
|parameter_ordinal|parameter_name|column_encryption_algorithm|column_encryption_type|  
|------------------------|---------------------|-----------------------------------|------------------------------|  
|1|\@c1|1|1|  
  
 (결과 계속 합니다.)  
  
|column_encryption_key_ordinal|column_encryption_normalization_rule_version|  
|--------------------------------------|------------------------------------------------------|  
|1|1|  
  
## <a name="see-also"></a>관련 항목  
 [상시 암호화&#40;데이터베이스 엔진&#41;](../../relational-databases/security/encryption/always-encrypted-database-engine.md)   
 [상시 암호화&#40;클라이언트 개발&#41;](../../relational-databases/security/encryption/always-encrypted-client-development.md)  
  
  
