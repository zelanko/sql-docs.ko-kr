---
title: '자습서: DB 개체에 대한 권한 구성'
ms.custom: seo-lt-2019
ms.date: 07/31/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- database permissions
ms.assetid: f964b66a-ec32-44c2-a185-6a0f173bfa22
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 991bdef702b1ed298bb492172ef65c6d25d5d0ab
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75244753"
---
# <a name="lesson-2-configure-permissions-on-database-objects"></a>2단원: 데이터베이스 개체에 대한 사용 권한 구성
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
데이터베이스에 대한 액세스 권한을 사용자에게 부여하는 작업은 3개의 단계로 구성됩니다. 먼저 로그인을 만듭니다. 로그인을 사용하여 사용자는 [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]에 연결할 수 있습니다. 그런 다음 지정된 데이터베이스에서 로그인을 사용자로 구성합니다. 마지막으로 데이터베이스 개체에 대한 사용 권한을 사용자에게 부여합니다. 이 단원에서는 이러한 3개의 단계와 뷰 및 저장 프로시저를 개체로 만드는 방법을 보여 줍니다.  

  >[!NOTE]
  > 이 단원에서는 [1 단원 - 데이터베이스 개체 만들기](lesson-1-creating-database-objects.md)에서 만든 개체를 사용합니다. 2단원을 계속하기 전에 1단원을 완료합니다. 

## <a name="prerequisites"></a>사전 요구 사항
이 자습서를 완료하려면 SQL Server Management Studio 및 SQL Server 인스턴스에 대한 액세스 권한이 필요합니다. 

- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.

SQL Server 인스턴스에 대한 액세스 권한이 없는 경우 다음 링크에서 플랫폼을 선택합니다. SQL 인증을 선택한 경우 SQL Server 로그인 자격 증명을 사용합니다.
- **Windows**: [SQL Server 2017 Developer Edition 다운로드](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [Docker에서 SQL Server 2017 다운로드](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-a-login"></a>로그인을 만듭니다.
[!INCLUDE[ssDE](../includes/ssde-md.md)]에 액세스하려면 사용자는 로그인이 필요합니다. 로그인은 사용자의 ID를 Windows 계정 또는 Windows 그룹의 멤버로 나타내거나 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에만 존재하는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]로그인이 될 수 있습니다. 가능하면 Windows 인증을 사용해야 합니다.  
  
기본적으로 컴퓨터의 관리자는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 모든 액세스 권한을 가집니다. 따라서 낮은 권한의 사용자가 필요할 것이므로 컴퓨터에서 새로운 로컬 Windows 인증 계정을 만듭니다. 이 작업을 수행하려면 컴퓨터의 관리자여야 합니다. 그런 다음 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 액세스 권한을 새 사용자에게 부여합니다.  
  
### <a name="create-a-new-windows-account"></a>새 Windows 계정 만들기  
  
1.  **시작**, **실행**을 차례로 클릭하고 **열기** 상자에 **%SystemRoot%\system32\compmgmt.msc /s**를 입력한 다음 **확인** 을 클릭하여 컴퓨터 관리 프로그램을 엽니다. 
2.  **시스템 도구**에서 **로컬 사용자 및 그룹**을 확장하고 **사용자**를 마우스 오른쪽 단추로 클릭한 다음 **새 사용자**를 클릭합니다.    
3.  **사용자 이름** 상자에 **Mary**를 입력합니다.    
4.  **암호** 및 **암호 확인** 상자에 강력한 암호를 입력한 다음 **만들기** 를 클릭하여 새 로컬 Windows 사용자를 만듭니다.  
  
### <a name="create-a-sql-login"></a>SQL 로그인 만들기  

[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]의 쿼리 편집기 창에서 `computer_name` 을 컴퓨터 이름으로 바꾸어서 다음 코드를 입력하고 실행합니다. `FROM WINDOWS` 는 Windows가 사용자를 인증한다는 것을 나타냅니다. 사용자의 연결 문자열에서 다른 데이터베이스를 나타내지 않는 경우 선택적 `DEFAULT_DATABASE` 인수는 `Mary` 를 `TestData` 데이터베이스에 연결합니다. 이 문에서는 [!INCLUDE[tsql](../includes/tsql-md.md)] 문을 종료하기 위한 선택적 문자로 세미콜론이 사용됩니다.
  
  ```sql  
  CREATE LOGIN [computer_name\Mary]  
      FROM WINDOWS  
      WITH DEFAULT_DATABASE = [TestData];  
  GO  
  ```  
  
  이 코드는 컴퓨터가 인증하는 사용자 이름 `Mary`에게 이 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]인스턴스에 액세스할 수 있는 권한을 부여합니다. 컴퓨터에 둘 이상의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인스턴스가 있을 경우 `Mary` 가 액세스해야 하는 각 인스턴스에서 로그인을 만들어야 합니다.    
  > [!NOTE]  
  > `Mary` 가 도메인 계정이 아니므로 이 사용자 이름은 이 컴퓨터에서만 인증될 수 있습니다. 


## <a name="grant-access-to-a-database"></a>데이터베이스에 액세스 권한 부여
현재 Mary는 이 인스턴스의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 액세스할 수 있지만 데이터베이스에 액세스할 수 있는 권한은 없습니다. Mary에게 데이터베이스 사용자의 권한을 부여할 때까지 Mary는 자신의 기본 데이터베이스인 **TestData** 에도 액세스할 수 없습니다.  
  
Mary에게 액세스 권한을 부여하려면 **TestData** 데이터베이스로 전환한 다음 CREATE USER 문을 사용하여 Mary의 로그인을 Mary라는 사용자에게 매핑합니다.  
  
### <a name="to-create-a-user-in-a-database"></a>데이터베이스에서 사용자를 만들려면  
  
다음 문을 입력하고 실행하여( `computer_name` 을 컴퓨터의 이름으로 바꿈) `Mary` 데이터베이스에 대한 액세스 권한을 `TestData` 에게 부여합니다.
  
 ```sql  
 USE [TestData];  
 GO  
 
 CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
 GO    
 ```  
  
 이제 Mary는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 및 `TestData` 데이터베이스에 대한 액세스 권한을 가집니다.  


## <a name="create-views-and-stored-procedures"></a>보기 및 저장 프로시저 만들기
관리자는 **Products** 테이블 및 **vw_Names** 뷰에서 SELECT를 실행하고 **pr_Names** 프로시저를 실행할 수 있지만 Mary는 이러한 작업을 수행할 수 없습니다. Mary에게 필요한 사용 권한을 부여하려면 GRANT 문을 사용합니다.  

### <a name="grant-permission-to-stored-procedure"></a>저장 프로시저에 사용 권한 부여  
다음 문을 실행하여 `Mary` 저장 프로시저에 대한 `EXECUTE` 권한을 `pr_Names` 에게 제공합니다.
  
  ```sql  
  GRANT EXECUTE ON pr_Names TO Mary;  
  GO  
  ```  
  
이 시나리오에서 Mary는 이 저장 프로시저를 사용하여 **Products** 테이블에만 액세스할 수 있습니다. Mary가 SELECT 문을 뷰에 대해 실행할 수 있도록 하려면 또한 `GRANT SELECT ON vw_Names TO Mary`를 실행해야 합니다. 데이터베이스 개체에 대한 액세스 권한을 제거하려면 REVOKE 문을 사용합니다.  
  
> [!NOTE]  
> 테이블, 뷰 및 저장 프로시저를 동일한 스키마에서 소유하지 않을 경우 사용 권한을 부여하는 것은 더 복잡해집니다.  
  
### <a name="about-grant"></a>GRANT 정보  
저장 프로시저를 실행하려면 EXECUTE 권한이 있어야 합니다. 데이터를 액세스 및 변경하려면 SELECT, INSERT, UPDATE 및 DELETE 권한이 있어야 합니다. 또한 GRANT 문은 테이블 작성 권한과 같은 다른 사용 권한에도 사용됩니다.  
  
## <a name="next-steps"></a>다음 단계
다음 아티클에서는 다른 단원에서 만든 데이터베이스 개체를 제거하는 방법을 설명합니다. 

자세히 알아보려면 다음 문서로 이동합니다.
> [!div class="nextstepaction"]
>[다음 단계](lesson-3-deleting-database-objects.md)
  
