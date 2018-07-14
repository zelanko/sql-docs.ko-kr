---
title: '자습서: 인증서로 저장 프로시저 서명 | Microsoft 문서'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- signing stored procedures tutorial [SQL Server]
ms.assetid: a4b0f23b-bdc8-425f-b0b9-e0621894f47e
caps.latest.revision: 11
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: fc43b135ce263a187009fbc0f7e42a45d6d049b5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270619"
---
# <a name="tutorial-signing-stored-procedures-with-a-certificate"></a>자습서: 인증서로 저장 프로시저 서명
  이 자습서에서는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 생성한 인증서를 사용하여 저장 프로시저에 서명하는 방법에 대해 설명합니다.  
  
> [!NOTE]  
>  이 자습서의 코드를 실행하려면 혼합 모드 보안을 구성하고 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스를 설치해야 합니다. 시나리오  
  
 저장 프로시저에 대한 사용 권한을 요구하려고 하지만 사용자에게 해당 권한을 명시적으로 부여하지 않으려는 경우 인증서를 사용하여 저장 프로시저에 서명하면 유용합니다. EXECUTE AS 문을 사용하거나 다른 방법으로 이 태스크를 수행할 수도 있지만 인증서를 사용하면 추적을 통해 저장 프로시저를 원래 호출한 사용자를 찾을 수 있습니다. 이를 통해 특히 보안 또는 DDL(데이터 정의 언어) 작업을 수행하는 동안 감사의 수준을 높일 수 있습니다.  
  
 master 데이터베이스에서 인증서를 만들어 서버 수준 사용 권한을 허용하거나 사용자 데이터베이스에서 인증서를 만들어 데이터베이스 수준 사용 권한을 허용할 수 있습니다. 이 시나리오에서는 기본 테이블에 대한 권한이 없는 사용자가 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스의 저장 프로시저에 액세스해야 하며 관리자는 개체 액세스 내역을 감사합니다. 여기서는 다른 소유권 체인 방법을 사용하는 대신 기본 개체에 대한 권한이 없는 서버 및 데이터베이스 사용자 계정과 테이블 및 저장 프로시저에 대한 권한이 있는 데이터베이스 사용자 계정을 만듭니다. 저장 프로시저와 두 번째 데이터베이스 사용자 계정 모두 인증서를 사용하여 보안이 설정됩니다. 두 번째 데이터베이스 계정은 모든 개체에 대한 액세스 권한을 가지며 첫 번째 데이터베이스 사용자 계정에 저장 프로시저에 대한 액세스 권한을 부여합니다.  
  
 이 시나리오에서는 먼저 데이터베이스 인증서, 저장 프로시저 및 사용자를 만든 후 다음 단계를 따라 프로세스를 테스트합니다.  
  
1.  환경 구성  
  
2.  인증서 만들기  
  
3.  저장 프로시저를 만들고 여기에 인증서로 서명  
  
4.  인증서를 사용하여 인증서 계정 만들기  
  
5.  인증서 계정에 데이터베이스 권한 부여  
  
6.  액세스 컨텍스트 표시  
  
7.  환경 다시 설정  
  
 이 예제의 각 코드 블록에 대한 설명도 함께 나와 있습니다. 전체 예제를 복사하려면 이 자습서 끝에 있는 [전체 예제](#CompleteExample) 를 참조하세요.  
  
## <a name="1-configure-the-environment"></a>1. 환경 구성  
 예제의 초기 컨텍스트를 설정하려면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 새 쿼리를 열고 다음 코드를 실행하여 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스를 엽니다. 이 코드는 데이터베이스 컨텍스트를 `AdventureWorks2012`로 변경하고 암호를 사용하여 새 서버 로그인 및 데이터베이스 사용자 계정(`TestCreditRatingUser`)을 만듭니다.  
  
```  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
```  
  
 CREATE USER 문에 대한 자세한 내용은 [CREATE USER&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql)를 참조하세요. CREATE LOGIN 문에 대한 자세한 내용은 [CREATE LOGIN&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)을 참조하세요.  
  
## <a name="2-create-a-certificate"></a>2. 인증서 만들기  
 master 데이터베이스를 컨텍스트로 사용하거나, 사용자 데이터베이스를 사용하거나, 두 가지 방법을 모두 사용하여 서버에서 인증서를 만들 수 있습니다. 인증서의 보안을 설정하는 옵션에는 여러 가지가 있습니다. 인증서에 대한 자세한 내용은 [CREATE CERTIFICATE&#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)를 참조하세요.  
  
 다음 코드를 실행하여 데이터베이스 인증서를 만들고 암호를 사용하여 이 인증서에 보안을 설정합니다.  
  
```  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
```  
  
## <a name="3-create-and-sign-a-stored-procedure-using-the-certificate"></a>3. 저장 프로시저를 만들고 여기에 인증서로 서명  
 다음 코드를 사용하여 `Vendor` 데이터베이스 스키마의 `Purchasing`테이블에서 데이터를 선택하는 저장 프로시저를 만들어 신용 등급이 1인 회사만 여기에 액세스할 수 있도록 제한할 수 있습니다. 저장 프로시저의 첫 번째 섹션은 저장 프로시저를 실행하는 사용자 계정의 컨텍스트를 표시합니다. 이 섹션은 개념을 보여 주기 위한 것으로, 요구 사항을 만족할 필요는 없습니다.  
  
```  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Show who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1  
END  
GO  
```  
  
 다음 코드를 실행하여 암호와 함께 데이터베이스 인증서로 저장 프로시저에 서명합니다.  
  
```  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
```  
  
 저장 프로시저에 대한 자세한 내용은 [저장 프로시저&#40;데이터베이스 엔진&#41;](stored-procedures/stored-procedures-database-engine.md)를 참조하세요.  
  
 저장 프로시저에 서명하는 방법에 대한 자세한 내용은 [ADD SIGNATURE&#40;Transact-SQL&#41;](/sql/t-sql/statements/add-signature-transact-sql)를 참조하세요.  
  
## <a name="4-create-a-certificate-account-using-the-certificate"></a>4. 인증서를 사용하여 인증서 계정 만들기  
 다음 코드를 실행하여 인증서에서 데이터베이스 사용자(`TestCreditRatingcertificateAccount`)를 만듭니다. 이 계정에는 서버 로그인이 없으므로 해당 계정으로 기본 테이블에 대한 액세스가 제어됩니다.  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="5-grant-the-certificate-account-database-rights"></a>5. 인증서 계정에 데이터베이스 권한 부여  
 다음 코드를 실행하여 기본 테이블 및 저장 프로시저에 대한 권한을 `TestCreditRatingcertificateAccount`에 부여합니다.  
  
```  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
```  
  
 개체에 사용 권한을 부여하는 방법에 대한 자세한 내용은 [GRANT&#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-transact-sql)를 참조하세요.  
  
## <a name="6-display-the-access-context"></a>6. 액세스 컨텍스트 표시  
 저장 프로시저 액세스와 관련된 권한을 표시하려면 다음 코드를 실행하여 `TestCreditRatingUser` 사용자에게 저장 프로시저를 실행할 수 있는 권한을 부여합니다.  
  
```  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
```  
  
 그런 다음 아래 코드를 실행하여 서버에서 사용한 dbo 로그인으로 저장 프로시저를 실행합니다. 사용자 컨텍스트 정보 출력을 살펴봅니다. 그룹 멤버로서가 아니라 자체의 고유한 권한을 가진 컨텍스트로 dbo 계정이 표시되는 것을 확인할 수 있습니다.  
  
```  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 다음 코드를 실행하여 `EXECUTE AS` 계정이 되도록 `TestCreditRatingUser` 문을 사용하고 저장 프로시저를 실행합니다. 이번에는 사용자 컨텍스트가 USER MAPPED TO CERTIFICATE 컨텍스트로 설정되어 있는 것을 확인할 수 있습니다.  
  
```  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXECUTE TestCreditRatingSP;  
GO  
```  
  
 여기서는 저장 프로시저에 서명했기 때문에 사용 가능한 감사가 표시됩니다.  
  
> [!NOTE]  
>  데이터베이스 내에서 컨텍스트 전환에 EXECUTE를 사용합니다.  
  
## <a name="7-reset-the-environment"></a>7. 환경 다시 설정  
 다음 코드는 `REVERT` 문을 사용하여 현재 계정의 컨텍스트를 dbo로 되돌리고 환경을 다시 설정합니다.  
  
```  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
 REVERT 문에 대한 자세한 내용은 [REVERT&#40;Transact-SQL&#41;](/sql/t-sql/statements/revert-transact-sql)를 참조하세요.  
  
##  <a name="CompleteExample"></a> 전체 예제  
 이 섹션에서는 전체 예제 코드를 보여 줍니다.  
  
```  
/* Step 1 - Open the AdventureWorks2012 database */  
USE AdventureWorks2012;  
GO  
-- Set up a login for the test user  
CREATE LOGIN TestCreditRatingUser  
   WITH PASSWORD = 'ASDECd2439587y'  
GO  
CREATE USER TestCreditRatingUser  
FOR LOGIN TestCreditRatingUser;  
GO  
  
/* Step 2 - Create a certificate in the AdventureWorks2012 database */  
CREATE CERTIFICATE TestCreditRatingCer  
   ENCRYPTION BY PASSWORD = 'pGFD4bb925DGvbd2439587y'  
      WITH SUBJECT = 'Credit Rating Records Access',   
      EXPIRY_DATE = '12/05/2014';  
GO  
  
/* Step 3 - Create a stored procedure and  
sign it using the certificate */  
CREATE PROCEDURE TestCreditRatingSP  
AS  
BEGIN  
   -- Shows who is running the stored procedure  
   SELECT SYSTEM_USER 'system Login'  
   , USER AS 'Database Login'  
   , NAME AS 'Context'  
   , TYPE  
   , USAGE   
   FROM sys.user_token;     
  
   -- Now get the data  
   SELECT AccountNumber, Name, CreditRating   
   FROM Purchasing.Vendor  
   WHERE CreditRating = 1;  
END  
GO  
  
ADD SIGNATURE TO TestCreditRatingSP   
   BY CERTIFICATE TestCreditRatingCer  
    WITH PASSWORD = 'pGFD4bb925DGvbd2439587y';  
GO  
  
/* Step 4 - Create a database user for the certificate.   
This user has the ownership chain associated with it. */  
USE AdventureWorks2012;  
GO  
CREATE USER TestCreditRatingcertificateAccount  
   FROM CERTIFICATE TestCreditRatingCer;  
GO  
  
/* Step 5 - Grant the user database rights */  
GRANT SELECT   
   ON Purchasing.Vendor   
   TO TestCreditRatingcertificateAccount;  
GO  
  
GRANT EXECUTE  
   ON TestCreditRatingSP   
   TO TestCreditRatingcertificateAccount;  
GO  
  
/* Step 6 - Test, using the EXECUTE AS statement */  
GRANT EXECUTE   
   ON TestCreditRatingSP   
   TO TestCreditRatingUser;  
GO  
  
-- Run the procedure as the dbo user, notice the output for the type  
EXEC TestCreditRatingSP;  
GO  
  
EXECUTE AS LOGIN = 'TestCreditRatingUser';  
GO  
EXEC TestCreditRatingSP;  
GO  
  
/* Step 7 - Clean up the example */  
REVERT;  
GO  
DROP PROCEDURE TestCreditRatingSP;  
GO  
DROP USER TestCreditRatingcertificateAccount;  
GO  
DROP USER TestCreditRatingUser;  
GO  
DROP LOGIN TestCreditRatingUser;  
GO  
DROP CERTIFICATE TestCreditRatingCer;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 데이터베이스 엔진 및 Azure SQL Database에 대한 보안 센터](security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
