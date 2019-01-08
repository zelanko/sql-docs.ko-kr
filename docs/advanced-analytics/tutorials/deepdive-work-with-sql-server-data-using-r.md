---
title: 데이터베이스를 만들고 RevoScaleR 자습서-SQL Server Machine Learning에 대 한 사용 권한
description: R 자습서에 대 한 SQL Server 데이터베이스를 만드는 방법에 대 한 연습 자습서...
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 15032b604d7ea28ad03acb837f997dac3afa84b8
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645272"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>데이터베이스를 만들고 사용 권한 (SQL Server 및 RevoScaleR 자습서)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 단원에서는의 일부인를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 자습서를 완료 하는 데 필요한 권한과 SQL Server 데이터베이스를 설정 하는 방법에 대 한 단원 하나 이며 사용 하 여 [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) 또는 다음 작업을 완료 하려면 다른 쿼리 편집기:

> [!div class="checklist"]
> * 학습 및 두 개의 R 모델 점수 매기기에 대 한 데이터를 저장할 새 데이터베이스 만들기
> * 데이터베이스 개체 만들기 및 사용에 대 한 권한이 있는 데이터베이스 사용자 로그인 만들기
  
## <a name="create-the-database"></a>데이터베이스 만들기

이 자습서는 데이터베이스 데이터 및 코드를 저장 하는 데 필요 합니다. 관리자가 아닌 경우 사용자에 대 한 데이터베이스 및 로그인을 만들려면 DBA를 요청 합니다. 데이터를 읽고 쓰는 데 및 R 스크립트를 실행할 권한이 필요 합니다.

1. SQL Server Management studio에서 R 사용 데이터베이스 인스턴스에 연결 합니다.

2. 마우스 오른쪽 단추로 클릭 **데이터베이스**, 선택한 **새 데이터베이스**합니다.
  
2. 새 데이터베이스의 이름을 입력 합니다. RevoDeepDive 합니다.
  

## <a name="create-a-login"></a>로그인을 만듭니다.
  
1. **새 쿼리**를 클릭하고 데이터베이스 컨텍스트를 master 데이터베이스로 변경합니다.
  
2. 새 **쿼리** 창에서 다음 명령을 실행하여 사용자 계정을 만들고 이 자습서에 사용되는 데이터베이스에 할당합니다. 필요한 경우 데이터베이스 이름을 변경해야 합니다.

3. 로그인을 확인 하려면 새 데이터베이스를 선택, 확장 **보안**를 확장 하 고 **사용자**합니다.
  
**Windows 사용자**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL 로그인**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>사용 권한 할당

이 자습서는 R 스크립트 및 응용 프로그램을 만드는 테이블 및 저장된 프로시저를 삭제 하 고 외부 프로세스에서 SQL Server에서 R 스크립트를 실행 등과 같은 DDL 작업을 보여 줍니다. 이 단계에서는 이러한 작업을 허용 하려면 아래를 할당 합니다.

이 예에서는 SQL 로그인 (DDUser01) 가정 하지만 Windows 로그인을 만든 경우 복사본을 대신 사용 합니다.

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>연결 문제 해결

이 섹션에서는 데이터베이스를 설정하는 과정에서 발생할 수 있는 몇 가지 일반적인 문제를 보여 줍니다.

- **데이터베이스 연결을 확인하고 SQL 쿼리를 검사하려면 어떻게 하나요?**
  
    서버를 사용하여 R 코드를 실행하기 전에 R 개발 환경에서 데이터베이스에 연결할 수 있는지 확인하는 것이 좋습니다. [Visual Studio의 서버 탐색기](https://msdn.microsoft.com/library/x603htbk.aspx) 및 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 는 둘 다 강력한 데이터베이스 연결 및 관리 기능을 갖춘 무료 도구입니다.
  
    추가 데이터베이스 관리 도구를 설치하지 않으려는 경우 제어판의 [ODBC 데이터 원본 관리자](https://msdn.microsoft.com/library/ms714024.aspx) 를 사용하여 SQL Server 인스턴스에 대한 테스트 연결을 만들 수 있습니다. 데이터베이스가 올바르게 구성되고 올바른 사용자 이름 및 암호를 입력한 경우 방금 만든 데이터베이스가 표시되며 기본 데이터베이스로 선택할 수 있습니다.
  
    연결 실패에 대 한 일반적인 이유는 원격 서버에 대 한 연결이 활성화 되지 않습니다 및 명명 된 파이프 프로토콜이 활성화 되어 있지. 이 문서에서 자세한 문제 해결 팁을 찾을 수 있습니다. [SQL Server 데이터베이스 엔진 연결 문제 해결](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)합니다.
  
- **내 테이블 이름 앞에 datareader가 붙는 것은 무엇 때문인가요?**
  
    이 사용자에 대한 기본 스키마를 **db_datareader**로 지정하는 경우, 모든 테이블과 이 사용자가 만든 새 개체의 이름은 *스키마*를 접두사로 갖습니다. 스키마는 개체를 구성하기 위해 데이터베이스에 추가할 수 있는 폴더와 비슷합니다. 또한 스키마는 데이터베이스 내에서 사용자 권한을 정의합니다.
  
    스키마가 특정 유저 이름과 연관되어 있다면, 그 유저는 _스키마 소유자_ 입니다. 개체를 만들 때 다른 스키마에서 만들도록 요청하지 않으면 항상 그 유저의 고유한 스키마에서 만들어집니다.
  
    예를 들어 **TestData**라는 이름으로 테이블을 생성하고 기본 스키마가 **db_datareader**라면, 테이블의 이름은`<database_name>.db_datareader.TestData`가 됩니다.
  
    이러한 이유로 테이블이 서로 다른 스키마에 속하기만 하면 한 데이터베이스에 같은 이름의 테이블이 여러 개 포함될 수 있습니다.
   
    스키마를 지정하지 않고 테이블을 찾고 있는 경우 데이터베이스 서버는 사용자가 소유한 스키마를 찾습니다. 따라서 로그인과 연결된 스키마의 테이블에 액세스할 때는 스키마 이름을 지정하지 않아도 됩니다.
  
- **DDL 권한이 없습니다. 그래도 자습서를 실행할 수 있나요?**
  
    예, 데이터를 미리 로드에 다른 사람에 게 문의 해야 하지만 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블과 계속 해 서 다음 단원으로 건너뜁니다. DDL 권한이 필요한 함수는 가능한 경우 항상 자습서에서 언급될 것입니다.

    또한 EXECUTE ANY EXTERNAL SCRIPT 사용 권한을 부여받으려면 관리자에게 문의하십시오. 원격이나 `sp_execute_external_script`를 통해 R 스크립트를 실행할 때 필요합니다.

## <a name="next-steps"></a>다음 단계

> [!div class="nextstepaction"]
> [RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)