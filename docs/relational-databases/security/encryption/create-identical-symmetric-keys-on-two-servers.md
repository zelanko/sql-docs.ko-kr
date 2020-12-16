---
title: 두 서버에서 동일한 대칭 키 만들기 | Microsoft 문서
description: Transact-SQL을 사용하여 SQL Server에서 두 서버에 동일한 대칭 키를 만드는 방법을 알아봅니다. 이는 별도의 데이터베이스 또는 서버에서의 암호화를 지원합니다.
ms.custom: ''
ms.date: 05/30/2019
ms.prod: sql
ms.reviewer: vanto
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: jaszymas
ms.author: jaszymas
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: c0cdf5dee29f2035ddb700f29df9c0bbb993c0aa
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479374"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>두 서버에서 동일한 대칭 키 만들기
[!INCLUDE [SQL Server Azure SQL Database](../../../includes/applies-to-version/sql-asdb.md)]
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 서로 다른 두 서버에서 동일한 대칭 키를 만드는 방법에 대해 설명합니다. ciphertext를 해독하려면 암호화하는 데 사용된 키가 필요합니다. 단일 데이터베이스에서 암호화와 암호 해독이 모두 수행되는 경우 키가 데이터베이스에 저장되며 사용 권한에 따라 암호화와 암호 해독에 모두 사용할 수 있습니다. 그러나 암호화와 암호 해독이 개별 데이터베이스나 개별 서버에서 수행되는 경우 한 데이터베이스에 저장된 키를 다른 데이터베이스에서 사용할 수 없습니다.
  
## <a name="before-you-begin"></a>시작하기 전에  
  
### <a name="limitations-and-restrictions"></a>제한 사항  
  
- 대칭 키를 만들 때 대칭 키는 인증서, 암호, 대칭 키, 비대칭 키 또는 PROVIDER 중 하나 이상을 사용하여 암호화해야 합니다. 키에는 각 유형에 대해 두 개 이상의 암호화가 포함될 수 있습니다. 즉, 여러 인증서, 암호, 대칭 키 및 비대칭 키를 동시에 사용하여 단일 대칭 키를 암호화할 수 있습니다.  
  
- 데이터베이스 마스터 키의 공개 키 대신 암호를 사용하여 대칭 키를 암호화한 경우 TRIPLE DES 암호화 알고리즘이 사용됩니다. 따라서 AES와 같은 강력한 암호화 알고리즘을 사용하여 만든 키는 더 약한 알고리즘으로 보호됩니다.  
  
## <a name="security"></a>보안  
  
### <a name="permissions"></a>사용 권한  
 데이터베이스에 대한 ALTER ANY SYMMETRIC KEY 권한이 필요합니다. AUTHORIZATION이 지정된 경우 데이터베이스 사용자에 대한 IMPERSONATE 권한 또는 애플리케이션 역할에 대한 ALTER 권한이 필요합니다. 인증서 또는 비대칭 키를 통한 암호화의 경우에는 해당 인증서 또는 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 및 애플리케이션 역할만 대칭 키를 소유할 수 있습니다. 그룹 및 역할은 대칭 키를 소유할 수 없습니다.  
  
## <a name="using-transact-sql"></a>Transact-SQL 사용  
  
### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>서로 다른 두 서버에 동일한 대칭 키를 만들려면  
  
1. **개체 탐색기** 에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2. 표준 도구 모음에서 **새 쿼리** 를 클릭합니다.  
  
3. 다음 CREATE MASTER KEY, CREATE CERTIFICATE 및 CREATE SYMMETRIC KEY 문을 실행하여 키를 만듭니다.  
  
    ```sql
    CREATE MASTER KEY ENCRYPTION BY PASSWORD = 'My p@55w0Rd';  
    GO  
    CREATE CERTIFICATE [cert_keyProtection] WITH SUBJECT = 'Key Protection';  
    GO  
    CREATE SYMMETRIC KEY [key_DataShare] WITH  
        KEY_SOURCE = 'My key generation bits. This is a shared secret!',  
        ALGORITHM = AES_256,   
        IDENTITY_VALUE = 'Key Identity generation bits. Also a shared secret'  
        ENCRYPTION BY CERTIFICATE [cert_keyProtection];  
    GO  
    ```  
  
4. 별개의 서버 인스턴스에 연결하고, 다른 쿼리 창을 열고, 위의 SQL 문을 실행하여 보조 서버에서 동일한 키를 만듭니다.  
  
5. 첫 번째 서버에서 아래의 OPEN SYMMETRIC KEY 문과 SELECT 문을 먼저 실행하여 키를 테스트합니다.  
  
    ```sql
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6. 두 번째 서버에서 이전 SELECT 문의 결과를 다음 코드에 `@blob` 값으로 붙여 넣고 다음 코드를 실행하여 중복 키가 ciphertext를 해독할 수 있는지 확인합니다.  
  
    ```sql
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7. 두 서버에서 대칭 키를 닫습니다.  
  
    ```sql
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  

### <a name="encryption-changes-in-sql-server-2017-cu2"></a>SQL Server 2017 CU2의 암호화 변경 내용

SQL Server 2016에서는 암호화 작업에 SHA1 해시 알고리즘을 사용합니다. SQL Server 2017부터 SHA2를 대신 사용합니다. 즉, 추가 단계는 SQL Server 2016에서 암호화된 항목을 SQL Server 2017에서 암호 해독하기 위해 추가적인 단계가 필요할 수 있습니다. 추가 단계는 다음과 같습니다.

- SQL Server 2017이 최소 누적 업데이트 2(CU2)로 업데이트되었는지 확인합니다.
  - 중요한 세부 정보는 [SQL Server 2017용 누적 업데이트 2(CU2)](https://support.microsoft.com/help/4052574)를 참조하세요.
- CU2를 설치한 후 SQL Server 2017에서 추적 플래그 4631을 켭니다. `DBCC TRACEON(4631, -1);`
  - 추적 플래그 4631은 SQL Server 2017의 새로운 기능입니다. SQL Server 2017에서 마스터 키, 인증서 또는 대칭 키를 만들려면 먼저 추적 플래그 4631이 전역적으로 `ON`이어야 합니다. 이를 통해 만들어진 항목이 SQL Server 2016 및 그 이전 버전과 상호 운용할 수 있게 됩니다.

자세한 지침은 다음을 참조하세요.

- [수정: SQL Server 2017이 동일한 대칭 키를 사용하여 이전 SQL Server 버전에서 암호화된 데이터를 암호 해독할 수 없음](https://support.microsoft.com/help/4053407/sql-server-2017-cannot-decrypt-data-encrypted-by-earlier-versions)
- [SQL Server 2017과 다른 SQL Server 버전 간에 동일한 대칭 키가 작동하지 않음](https://feedback.azure.com/forums/908035-sql-server/suggestions/33116269-identical-symmetric-keys-do-not-work-between-sql-s) <!-- Issue 2225. Thank you Stephen W and Sam Rueby. -->

## <a name="for-more-information"></a>참조 항목

-   [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/create-master-key-transact-sql.md)  
  
-   [CREATE CERTIFICATE&#40;Transact-SQL&#41;](../../../t-sql/statements/create-certificate-transact-sql.md)  
  
-   [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](../../../t-sql/statements/create-symmetric-key-transact-sql.md)  
  
-   [ENCRYPTBYKEY&#40;Transact-SQL&#41;](../../../t-sql/functions/encryptbykey-transact-sql.md)  
  
-   [DECRYPTBYKEY&#40;Transact-SQL&#41;](../../../t-sql/functions/decryptbykey-transact-sql.md)  
  
-   [OPEN SYMMETRIC KEY&#40;Transact-SQL&#41;](../../../t-sql/statements/open-symmetric-key-transact-sql.md)  
