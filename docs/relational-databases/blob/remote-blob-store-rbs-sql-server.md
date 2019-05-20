---
title: RBS(원격 Blob 저장소)(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 11/03/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- Remote Blob Store (RBS) [SQL Server]
- RBS (Remote Blob Store) [SQL Server]
ms.assetid: 31c947cf-53e9-4ff4-939b-4c1d034ea5b1
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 589edbc9b3f19597a84a3393f693078bca89dee7
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65094180"
---
# <a name="remote-blob-store-rbs-sql-server"></a>RBS(Remote Blob Store)(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] RBS(Remote BLOB Store)는 데이터베이스 관리자가 기본 데이터베이스 서버에 직접 저장하지 않고 상용 스토리지 솔루션에 BLOB(Binary Large Object)를 저장할 수 있도록 해 주는 선택적 추가 기능 구성 요소입니다.  
  
 RBS는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 설치 미디어에 포함되어 있지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에 의해 설치되지 않습니다.  
  
 
  
## <a name="why-rbs"></a>RBS를 사용하는 이유  
  
### <a name="optimized-database-storage-and-performance"></a>최적화된 데이터베이스 스토리지 및 성능  
 데이터베이스에 BLOB을 저장하면 많은 양의 파일 공간과 값비싼 서버 리소스를 소비할 수 있습니다. RBS는 사용자가 선택한 전용 스토리지 솔루션에 BLOB을 전송하고 해당 BLOB에 대한 참조를 데이터베이스에 저장합니다. 이렇게 하면 구조화된 데이터용 서버 스토리지와 데이터베이스 작업용 서버 리소스가 확보됩니다.  
  
### <a name="efficient-blob-management"></a>효율적인 BLOB 관리  
 여러 RBS 기능이 저장된 BLOB 관리를 지원합니다.  
  
-   BLOB은 ACID(원자성, 일관성, 격리성 및 내구성) 트랜잭션을 사용하여 관리됩니다.  
  
-   BLOB은 컬렉션으로 구성되어 있습니다.  
  
-   가비지 수집, 일관성 검사 및 기타 유지 관리 기능이 포함됩니다.  
  
### <a name="standardized-api"></a>표준화된 API  
 RBS는 애플리케이션의 BLOB 저장소 액세스 및 수정을 위한 표준화된 프로그래밍 모델을 제공하는 API 집합을 정의합니다. 각 BLOB 저장소에서는 자체 공급자 라이브러리를 지정할 수 있는데, 이 라이브러리는 RBS 클라이언트 라이브러리에 연결되어 BLOB을 저장하고 액세스하는 방법을 지정합니다.  
  
 많은 타사 스토리지 솔루션 공급업체가 이러한 표준 API를 준수하고 다양한 스토리지 플랫폼에서 BLOB 스토리지를 지원하는 RBS 공급자를 개발했습니다.  
  
## <a name="rbs-requirements"></a>RBS 요구 사항  
 - RBS를 사용하려면 BLOB 메타데이터가 저장된 기본 데이터베이스 서버용 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise가 필요합니다.  그러나 제공된 FILESTREAM 공급자를 사용하는 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard에 BLOB 자체를 저장할 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 연결하려면 RBS에는 적어도 [!INCLUDE[ssSQL14_md](../../includes/sssql14-md.md)] 용 ODBC 드라이버 버전 11 및 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]용 ODBC 드라이버 버전 13이 필요합니다. 드라이버는 [SQL Server용 ODBC 드라이버 다운로드](https://msdn.microsoft.com/library/mt703139.aspx)에서 제공됩니다.    
  
 RBS에는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 인스턴스에 RBS가 BLOB을 저장할 수 있는 FILESTREAM 공급자가 포함되어 있습니다. 다른 스토리지 솔루션에 RBS를 사용하여 BLOB을 저장하려면 해당 스토리지 솔루션을 위해 개발된 타사 RBS 공급자를 사용하거나 RBS API를 사용하여 사용자 지정 RBS 공급자를 개발해야 합니다. NTFS 파일 시스템에 BLOB을 저장하는 예제 공급자는 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190)에서 학습 리소스로 사용할 수 있습니다.  
  
## <a name="rbs-security"></a>RBS 보안  
 SQL Remote Blob Storage 팀 블로그에서 이 기능에 대한 유익한 정보를 참고할 수 있습니다. RBS 보안 모델은 [RBS 보안 모델](https://blogs.msdn.com/b/sqlrbs/archive/2010/08/05/rbs-security-model.aspx)의 게시물에 설명되어 있습니다.  
  
### <a name="custom-providers"></a>사용자 지정 공급자  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]외부에 BLOB를 저장하기 위해 사용자 지정 공급자를 사용하는 경우, 사용자 지정 공급자가 사용하는 스토리지 미디어에 적합한 권한과 암호화 옵션을 사용하여 저장된 BLOB를 보호해야 합니다.  
  
### <a name="credential-store-symmetric-key"></a>자격 증명 저장소 대칭 키  
 공급자가 자격 증명 저장소 내에 저장되는 비밀의 설정 및 사용을 요구하는 경우, RBS는 대칭 키를 사용하여 공급자의 Blob 저장소에 대한 권한을 확보하기 위해 클라이언트가 사용할 수 있는 공급자 비밀을 암호화합니다.  
  
-   RBS 2016은 **AES_128** 대칭 키를 사용합니다. [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]은 이전 버전과의 호환성을 위한 경우를 제외하고 새로운 **TRIPLE_DES** 키 생성을 허용하지 않습니다. 자세한 내용은 [CREATE SYMMETRIC KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)를 참조하세요.  
  
-   RBS 2014 이전 버전은 오래된 **TRIPLE_DES** 대칭 키 알고리즘을 사용하여 암호화된 암호를 유지하는 자격 증명 저장소를 사용합니다. 현재 **TRIPLE_DES**[!INCLUDE[msCoName](../../includes/msconame-md.md)] 을(를) 사용하는 경우, 이 항목에 포함된 단계에 따라 보다 강력한 암호화 방법으로 키를 회전하도록 보안을 향상시키는 것이 좋습니다.  
  
 RBS 데이터베이스에서 다음 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 실행하여 RBS 자격 증명 저장소 대칭 키 속성을 결정할 수 있습니다.   
`SELECT * FROM sys.symmetric_keys WHERE name = 'mssqlrbs_encryption_skey';` 해당 문의 출력에 **TRIPLE_DES** 가 아직 사용 중인 것으로 나타나면 이 키를 순환해야 합니다.  
  
### <a name="rotating-the-symmetric-key"></a>대칭 키 회전  
 RBS를 사용하는 경우, 자격 증명 저장소 대칭 키를 정기적으로 회전해야 합니다. 이것은 조직의 보안 정책을 충족하기 위한 일반적인 보안 모범 사례입니다.  RBS 자격 증명 저장소 대칭 키를 회전하는 한 가지 방법은 RBS 데이터베이스에 [아래 스크립트](#Key_rotation) 를 사용하는 것입니다.  이 스크립트를 사용하여 알고리즘 또는 키 길이와 같은 보다 강력한 암호화 강도 속성으로 마이그레이션할 수 있습니다. 키를 회전하기 전에 데이터베이스를 백업합니다.  스크립트의 결론에 몇 가지 확인 단계가 있습니다.  
보안 정책에 의해 제공된 것과 다른 키 속성(예: 알고리즘 또는 키 길이)이 요구되면 스크립트가 템플릿으로 사용될 수 있습니다. 다음 두 위치에서 키 속성을 수정합니다. 1) 임시 키 생성 2) 영구적인 키 생성.  
  
##  <a name="rbsresources"></a> RBS 리소스  
  
 **RBS 예제**  
 [Codeplex](https://go.microsoft.com/fwlink/?LinkId=210190) 에서 제공하는 RBS 샘플은 RBS 애플리케이션을 개발하는 방법과 사용자 지정 RBS 공급자를 설치하고 사용자 지정하는 방법을 보여 줍니다.  
  
 **RBS 블로그**  
 [RBS 블로그](https://go.microsoft.com/fwlink/?LinkId=210315) 는 RBS를 이해하고 배포하고 유지하는 데 도움이 되는 추가 정보를 제공합니다.  
  
##  <a name="Key_rotation"></a> 키 회전 스크립트  
 이 예제는 현재 사용된 RBS 자격 증명 저장소 대칭 키를 선택한 키로 바꾸기 위해 `sp_rotate_rbs_symmetric_credential_key` 라는 이름의  
저장 프로시저를 만듭니다.  정기적인 키 순환이 요구되는 보안 정책이 있거나   
특정 알고리즘 요구 사항이 있는 경우에 이 작업을 수행할 수 있습니다.  
 이 저장 프로시저에서는 **AES_256** 을 사용하는 대칭 키가 현재 키를 대체합니다.  대칭 키가  
대체되었으므로, 새로운 키로 암호를 다시 암호화해야 합니다.  이 저장   
프로시저가 암호도 다시 암호화합니다.  키를 회전하기 전에 데이터베이스를 백업해야 합니다.  
  
```  
CREATE PROC sp_rotate_rbs_symmetric_credential_key  
AS  
BEGIN  
BEGIN TRANSACTION;  
BEGIN TRY  
CLOSE ALL SYMMETRIC KEYS;  
  
/* Prove that all secrets can be re-encrypted, by creating a   
temporary key (#mssqlrbs_encryption_skey) and create a   
temp table (#myTable) to hold the re-encrypted secrets.    
Check to see if all re-encryption worked before moving on.*/  
  
CREATE TABLE #myTable(sql_user_sid VARBINARY(85) NOT NULL,  
    blob_store_id SMALLINT NOT NULL,  
    credential_name NVARCHAR(256) COLLATE Latin1_General_BIN2 NOT NULL,  
    old_secret VARBINARY(MAX), -- holds secrets while existing symmetric key is deleted  
    credential_secret VARBINARY(MAX)); -- holds secrets with the new permanent symmetric key  
  
/* Create a new temporary symmetric key with which the credential store secrets   
can be re-encrypted. These will be used once the existing symmetric key is deleted.*/  
CREATE SYMMETRIC KEY #mssqlrbs_encryption_skey    
    WITH ALGORITHM = AES_256 ENCRYPTION BY   
    CERTIFICATE [cert_mssqlrbs_encryption];  
  
OPEN SYMMETRIC KEY #mssqlrbs_encryption_skey    
    DECRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
INSERT INTO #myTable   
    SELECT cred_store.sql_user_sid, cred_store.blob_store_id, cred_store.credential_name,   
    encryptbykey(  
        key_guid('#mssqlrbs_encryption_skey'),   
        decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'),   
            NULL, cred_store.credential_secret)  
        ),   
    NULL  
    FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials] AS cred_store;  
  
IF( EXISTS(SELECT * FROM #myTable WHERE old_secret IS NULL))  
BEGIN  
    PRINT 'Abort. Failed to read some values';  
    SELECT * FROM #myTable;  
    ROLLBACK;  
END;  
ELSE  
BEGIN  
/* Re-encryption worked, so go ahead and drop the existing RBS credential store   
 symmetric key and replace it with a new symmetric key.*/  
DROP SYMMETRIC KEY [mssqlrbs_encryption_skey];  
  
CREATE SYMMETRIC KEY [mssqlrbs_encryption_skey]   
WITH ALGORITHM = AES_256   
ENCRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
OPEN SYMMETRIC KEY [mssqlrbs_encryption_skey]   
DECRYPTION BY CERTIFICATE [cert_mssqlrbs_encryption];  
  
/*Re-encrypt using the new permanent symmetric key.    
Verify if encryption provided a result*/  
UPDATE #myTable   
SET [credential_secret] =   
    encryptbykey(key_guid('mssqlrbs_encryption_skey'), decryptbykey(old_secret))  
  
IF( EXISTS(SELECT * FROM #myTable WHERE credential_secret IS NULL))  
BEGIN  
    PRINT 'Aborted. Failed to re-encrypt some values'  
    SELECT * FROM #myTable  
    ROLLBACK  
END  
ELSE  
BEGIN  
  
/* Replace the actual RBS credential store secrets with the newly   
encrypted secrets stored in the temp table #myTable.*/                
SET NOCOUNT ON;  
DECLARE @sql_user_sid varbinary(85);  
DECLARE @blob_store_id smallint;  
DECLARE @credential_name varchar(256);  
DECLARE @credential_secret varbinary(256);  
DECLARE curSecretValue CURSOR   
    FOR SELECT sql_user_sid, blob_store_id, credential_name, credential_secret   
FROM #myTable ORDER BY sql_user_sid, blob_store_id, credential_name;  
  
OPEN curSecretValue;  
FETCH NEXT FROM curSecretValue   
    INTO @sql_user_sid, @blob_store_id, @credential_name, @credential_secret  
WHILE @@FETCH_STATUS = 0  
BEGIN  
    UPDATE [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
        SET [credential_secret] = @credential_secret   
        FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
        WHERE sql_user_sid = @sql_user_sid AND blob_store_id = @blob_store_id AND   
            credential_name = @credential_name  
FETCH NEXT FROM curSecretValue   
    INTO @sql_user_sid, @blob_store_id, @credential_name, @credential_secret  
END  
CLOSE curSecretValue  
DEALLOCATE curSecretValue  
  
DROP TABLE #myTable;  
CLOSE ALL SYMMETRIC KEYS;  
DROP SYMMETRIC KEY #mssqlrbs_encryption_skey;  
  
/* Verify that you can decrypt all encrypted credential store entries using the certificate.*/  
IF( EXISTS(SELECT * FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials]   
WHERE decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'),   
    NULL, credential_secret) IS NULL))  
BEGIN  
    print 'Aborted. Failed to verify key rotation'  
    ROLLBACK;  
END;  
ELSE  
    COMMIT;  
END;  
END;  
END TRY  
BEGIN CATCH  
     PRINT 'Exception caught: ' + cast(ERROR_NUMBER() as nvarchar) + ' ' + ERROR_MESSAGE();  
     ROLLBACK  
END CATCH  
END;  
GO  
```  
  
 이제 `sp_rotate_rbs_symmetric_credential_key` 저장 프로시저를 RBS 자격 증명 저장소 대칭 키 회전에 사용할 수 있으며, 암호는 키 회전 전과 후에 동일하게 유지됩니다.  
  
```  
SELECT *, decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'), NULL, credential_secret)   
FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials];  
  
EXEC sp_rotate_rbs_symmetric_credential_key;  
  
SELECT *, decryptbykeyautocert(cert_id('cert_mssqlrbs_encryption'), NULL, credential_secret)   
FROM [mssqlrbs_resources].[rbs_internal_blob_store_credentials];  
  
/* See that the RBS credential store symmetric key properties reflect the new changes*/  
SELECT * FROM sys.symmetric_keys WHERE name = 'mssqlrbs_encryption_skey';  
```  
  
## <a name="see-also"></a>참고 항목  
[Remote Blob Store 및 Always On 가용성 그룹(SQL Server)](../../database-engine/availability-groups/windows/remote-blob-store-rbs-and-always-on-availability-groups-sql-server.md)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
  
