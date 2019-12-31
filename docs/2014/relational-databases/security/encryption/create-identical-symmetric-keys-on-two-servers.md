---
title: 두 서버에서 동일한 대칭 키 만들기 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- symmetric keys [SQL Server], creating
ms.assetid: a13d0b21-a43b-43c0-9c22-7ba8f3d15e80
author: jaszymas
ms.author: jaszymas
manager: craigg
ms.openlocfilehash: 1ff075880833be8179697cb4047babee67cfe61e
ms.sourcegitcommit: 39ea690996a7390e3d13d6fb8f39d8641cd5f710
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/10/2019
ms.locfileid: "74957232"
---
# <a name="create-identical-symmetric-keys-on-two-servers"></a>두 서버에서 동일한 대칭 키 만들기
  이 항목에서는 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 에서 [!INCLUDE[tsql](../../../includes/tsql-md.md)]을 사용하여 서로 다른 두 서버에서 동일한 대칭 키를 만드는 방법에 대해 설명합니다. ciphertext를 해독하려면 암호화하는 데 사용된 키가 필요합니다. 단일 데이터베이스에서 암호화와 암호 해독이 모두 수행되는 경우 키가 데이터베이스에 저장되며 사용 권한에 따라 암호화와 암호 해독에 모두 사용할 수 있습니다. 그러나 암호화와 암호 해독이 개별 데이터베이스나 개별 서버에서 수행되는 경우 한 데이터베이스에 저장된 키를 다른 데이터베이스에서 사용할 수 없습니다.  
  
 **항목 내용**  
  
-   **시작 하기 전에:**  
  
     [제한 사항](#Restrictions)  
  
     [보안](#Security)  
  
-   [Transact-sql을 사용 하 여 서로 다른 두 서버에 동일한 대칭 키를 만들려면](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a>시작 하기 전에  
  
###  <a name="Restrictions"></a>제한 사항  
  
-   대칭 키를 만들 때 대칭 키는 인증서, 암호, 대칭 키, 비대칭 키 또는 PROVIDER 중 하나 이상을 사용하여 암호화해야 합니다. 키에는 각 유형에 대해 두 개 이상의 암호화가 포함될 수 있습니다. 즉, 여러 인증서, 암호, 대칭 키 및 비대칭 키를 동시에 사용하여 단일 대칭 키를 암호화할 수 있습니다.  
  
-   데이터베이스 마스터 키의 공개 키 대신 암호를 사용하여 대칭 키를 암호화한 경우 TRIPLE DES 암호화 알고리즘이 사용됩니다. 따라서 AES와 같은 강력한 암호화 알고리즘을 사용하여 만든 키는 더 약한 알고리즘으로 보호됩니다.  
  
###  <a name="Security"></a>보안  
  
####  <a name="Permissions"></a>권한에  
 데이터베이스에 대한 ALTER ANY SYMMETRIC KEY 권한이 필요합니다. AUTHORIZATION이 지정된 경우 데이터베이스 사용자에 대한 IMPERSONATE 권한 또는 애플리케이션 역할에 대한 ALTER 권한이 필요합니다. 인증서 또는 비대칭 키를 통한 암호화의 경우에는 해당 인증서 또는 비대칭 키에 대한 VIEW DEFINITION 권한이 필요합니다. Windows 로그인, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 로그인 및 애플리케이션 역할만 대칭 키를 소유할 수 있습니다. 그룹 및 역할은 대칭 키를 소유할 수 없습니다.  
  
##  <a name="TsqlProcedure"></a>Transact-sql 사용  
  
#### <a name="to-create-identical-symmetric-keys-on-two-different-servers"></a>서로 다른 두 서버에 동일한 대칭 키를 만들려면  
  
1.  
  **개체 탐색기**에서 [!INCLUDE[ssDE](../../../includes/ssde-md.md)]인스턴스에 연결합니다.  
  
2.  
  표준 도구 모음에서 **새 쿼리**를 클릭합니다.  
  
3.  다음 CREATE MASTER KEY, CREATE CERTIFICATE 및 CREATE SYMMETRIC KEY 문을 실행하여 키를 만듭니다.  
  
    ```  
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
  
4.  별개의 서버 인스턴스에 연결하고, 다른 쿼리 창을 열고, 위의 SQL 문을 실행하여 보조 서버에서 동일한 키를 만듭니다.  
  
5.  첫 번째 서버에서 아래의 OPEN SYMMETRIC KEY 문과 SELECT 문을 먼저 실행하여 키를 테스트합니다.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    SELECT encryptbykey(key_guid('key_DataShare'), 'MyData' )  
    GO  
    -- For example, the output might look like this: 0x2152F8DA8A500A9EDC2FAE26D15C302DA70D25563DAE7D5D1102E3056CE9EF95CA3E7289F7F4D0523ED0376B155FE9C3  
    ```  
  
6.  두 번째 서버에서 이전 SELECT 문의 결과를 다음 코드에 `@blob` 값으로 붙여 넣고 다음 코드를 실행하여 중복 키가 ciphertext를 해독할 수 있는지 확인합니다.  
  
    ```  
    OPEN SYMMETRIC KEY [key_DataShare]   
        DECRYPTION BY CERTIFICATE cert_keyProtection;  
    GO  
    DECLARE @blob varbinary(8000);  
    SET @blob = SELECT CONVERT(varchar(8000), decryptbykey(@blob));  
    GO  
    ```  
  
7.  두 서버에서 대칭 키를 닫습니다.  
  
    ```  
    CLOSE SYMMETRIC KEY [key_DataShare];  
    GO  
    ```  
  
 자세한 내용은  
  
-   [Transact-sql&#41;&#40;마스터 키 만들기](/sql/t-sql/statements/create-master-key-transact-sql)  
  
-   [Transact-sql&#41;인증서 &#40;만들기](/sql/t-sql/statements/create-certificate-transact-sql)  
  
-   [Transact-sql&#41;&#40;대칭 키 만들기](/sql/t-sql/statements/create-symmetric-key-transact-sql)  
  
-   [ENCRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/encryptbykey-transact-sql)  
  
-   [DECRYPTBYKEY &#40;Transact-sql&#41;](/sql/t-sql/functions/decryptbykey-transact-sql)  
  
-   [Transact-sql&#41;&#40;대칭 키를 엽니다.](/sql/t-sql/statements/open-symmetric-key-transact-sql)  
  
  
