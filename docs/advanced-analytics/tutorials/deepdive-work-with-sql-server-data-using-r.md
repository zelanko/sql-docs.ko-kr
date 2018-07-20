---
title: R (SQL 및 R 심층 분석)를 사용 하 여 SQL Server 데이터 작업 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: ea8fee364cd69580b8b7d0b6438349dbf2b1298c
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39084185"
---
# <a name="lesson-1-create-a-database-and-permissions"></a>1 단원: 데이터베이스 및 권한 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서는의 일부를 [RevoScaleR 자습서](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) 사용 하는 방법에 [RevoScaleR 함수](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) SQL Server를 사용 하 여 합니다.

이 단원에서는 모델 학습에 필요한 데이터를 추가 및 데이터의 몇 가지 빠른 요약 실행 환경을 설정 합니다. 프로세스의 일부로, 이러한 작업을 완료 해야 합니다.
  
- 두 개의 R 모델 학습 및 점수 매기기에 사용되는 데이터를 저장할 새 데이터베이스를 만듭니다.
  
- 워크스테이션과 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 컴퓨터 간에 통신할 때 사용할 계정(Windows 사용자 또는 SQL 로그인)을 만듭니다.
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 및 데이터베이스 개체 작업을 위한 데이터 원본을 R에서 만듭니다.
  
- R 데이터 원본을 사용하여 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 로드합니다.
  
- R을 사용하여 변수 목록을 가져오고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블의 메타데이터를 수정합니다.
  
- R 코드의 원격 실행이 가능하도록 계산 컨텍스트를 만듭니다.
  
- (선택 사항) 원격 계산 컨텍스트에서 추적을 사용 하도록 설정 합니다.
  
## <a name="create-the-database-and-user"></a>데이터베이스 및 사용자 만들기

이 연습에서 새 데이터베이스를 만들 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], 데이터를 읽고 쓰는 데 및 R 스크립트를 실행할 권한이 있는 SQL 로그인을 추가 합니다.

> [!NOTE]
> R 스크립트를 실행 하는 계정에 대 한 SELECT 권한 필요만 데이터를 읽는 경우 (**db_datareader** 역할)에 지정된 된 데이터베이스입니다. 그러나이 자습서에서는 데이터베이스를 준비 하 고 점수 매기기 결과 저장 하는 테이블을 만드는 DDL 관리자 권한이 있어야 합니다.
> 
> 또한가 아닌 데이터베이스 소유자는 권한 EXECUTE ANY EXTERNAL SCRIPT, R 스크립트를 실행 하기 위해 필요 합니다.

1. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 을 사용할 수 있는 인스턴스를 선택하고 **데이터베이스**를 마우스 오른쪽 단추로 클릭한 다음 **새 데이터베이스**를 선택합니다.
  
2. 새 데이터베이스의 이름을 입력합니다. 원하는 이름을 임의로 사용할 수 있지만 이 연습의 모든 [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 및 R 스크립트를 적절하게 편집해야 합니다.
  
    > [!TIP]
    > 업데이트된 데이터베이스 이름을 보려면 **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **새로 고침** 을 선택합니다.
  
3. **새 쿼리**를 클릭하고 데이터베이스 컨텍스트를 master 데이터베이스로 변경합니다.
  
4. 새 **쿼리** 창에서 다음 명령을 실행하여 사용자 계정을 만들고 이 자습서에 사용되는 데이터베이스에 할당합니다. 필요한 경우 데이터베이스 이름을 변경해야 합니다.
  
**Windows 사용자**
  
```SQL
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[DeepDive]

 --Add the new user to tutorial database
USE [DeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**SQL 로그인**

```SQL
-- Create new SQL login
USE master
GO
CREATE LOGIN DDUser01 WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE [DeepDive]
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

5. 사용자가 만들어졌는지 확인하려면 새 데이터베이스를 선택하고 **보안**및 **사용자**를 차례로 확장합니다.

## <a name="troubleshooting"></a>문제 해결

이 섹션에서는 데이터베이스를 설정하는 과정에서 발생할 수 있는 몇 가지 일반적인 문제를 보여 줍니다.

- **데이터베이스 연결을 확인하고 SQL 쿼리를 검사하려면 어떻게 하나요?**
  
    서버를 사용하여 R 코드를 실행하기 전에 R 개발 환경에서 데이터베이스에 연결할 수 있는지 확인하는 것이 좋습니다. [Visual Studio의 서버 탐색기](https://msdn.microsoft.com/library/x603htbk.aspx) 및 [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) 는 둘 다 강력한 데이터베이스 연결 및 관리 기능을 갖춘 무료 도구입니다.
  
    추가 데이터베이스 관리 도구를 설치하지 않으려는 경우 제어판의 [ODBC 데이터 원본 관리자](https://msdn.microsoft.com/library/ms714024.aspx) 를 사용하여 SQL Server 인스턴스에 대한 테스트 연결을 만들 수 있습니다. 데이터베이스가 올바르게 구성되고 올바른 사용자 이름 및 암호를 입력한 경우 방금 만든 데이터베이스가 표시되며 기본 데이터베이스로 선택할 수 있습니다.
  
    데이터베이스에 연결할 수 없는 경우 서버에 대해 원격 연결을 사용할 수 있고 명명된 파이프 프로토콜이 사용하도록 설정되었는지 확인합니다. 이 문서에서 추가 문제 해결 팁을 제공 합니다. [SQL Server 데이터베이스 엔진에 연결 문제 해결](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine)합니다.
  
- **내 테이블 이름 앞에 datareader가 붙는 것은 무엇 때문인가요?**
  
    이 사용자에 대 한 기본 스키마를 지정 하는 경우 **db_datareader**, 모든 테이블 및이 사용자가 만든 새 개체 다른 접두사로 합니다 *스키마* 이름입니다. 스키마는 개체를 구성하기 위해 데이터베이스에 추가할 수 있는 폴더와 비슷합니다. 또한 스키마는 데이터베이스 내에서 사용자 권한을 정의합니다.
  
    사용자가 스키마를 하나의 특정 사용자 이름과 연결 된 경우는 _스키마 소유자_합니다. 개체를 만들 때 다른 스키마에서 만들도록 요청하지 않을 경우 항상 고유한 스키마에서 만듭니다.
  
    예를 들어 이름으로 테이블을 만들 `*`TestData`, and your default schema is **db\_datareader**, the table is created with the name `< database_name >.db_datareader 합니다. TestData'.
  
    이러한 이유로 테이블이 서로 다른 스키마에 속하기만 하면 한 데이터베이스에 같은 이름의 테이블이 여러 개 포함될 수 있습니다.
   
    테이블을 찾고 있는 경우 스키마를 지정 하지 않으면 데이터베이스 서버 사용자가 소유한 스키마를 찾습니다. 따라서 로그인과 연결된 스키마의 테이블에 액세스할 때는 스키마 이름을 지정하지 않아도 됩니다.
  
- **DDL 권한이 없습니다. 그래도 자습서를 실행할 수 있나요?**
  
    예, 그러나 다른 사람에게 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 테이블에 미리 로드하도록 요청하고 새 테이블을 만들기 위해 호출하는 섹션을 건너뛰어야 합니다. DDL 권한이 필요한 함수는 가능한 경우 항상 자습서에서 호출 됩니다.

    또한 EXECUTE ANY EXTERNAL SCRIPT 사용 권한을 부여 받으려면 관리자에 게 문의 합니다. 원격 여부를 사용 하 여 R 스크립트 실행을 위해 필요할 `sp_execute_external_script`합니다.

## <a name="next-step"></a>다음 단계

[RxSqlServerData를 사용하여 SQL Server 데이터 개체 만들기](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>개요

[데이터 과학 심층 분석: RevoScaleR 패키지 사용](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)



