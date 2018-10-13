---
title: T-SQL (SQL Server Machine Learning)에서 "Hello World" 기본 R 코드 실행 빠른 시작 | Microsoft Docs
description: SQL Server에서 R 스크립트에 대 한 빠른 시작입니다. Sp_execute_external_script 시스템 저장 프로시저를 사용 하 여 hello world 연습에서 R 스크립트를 호출 하는 기본 사항을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/08/2018
ms.topic: quickstart
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 1a51fcb9e67bef48346ff74ebfb1e911a6ee3365
ms.sourcegitcommit: ce4b39bf88c9a423ff240a7e3ac840a532c6fcae
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/09/2018
ms.locfileid: "48878086"
---
# <a name="quickstart-hello-world-r-script-in-sql-server"></a>SQL Server의 빠른 시작: "Hello world" R 스크립트 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server에 있는 SQL Server 데이터에 대 한 데이터 과학 분석에 대 한 R 언어 지원이 포함 됩니다. R 스크립트와 같은 오픈 소스 R 함수, 타사 R 라이브러리 또는 기본 제공 Microsoft R 라이브러리의 구성할 수 있습니다 [RevoScaleR](../r/revoscaler-overview.md) 규모에서 예측 분석에 대 한 합니다. 

다음 방법 중 하나를 사용 하 여 저장된 프로시저를 통해 스크립트 실행이 됩니다.

+ 기본 제공 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 저장 프로시저에서 R 스크립트를 입력된 매개 변수로 전달 합니다.
+ R 스크립트를 래핑하는 [사용자 지정 저장 프로시저](sqldev-in-database-r-for-sql-developers.md) 만든 합니다.

이 빠른 시작에 알아봅니다 "Hello World" R을 실행 하 여 주요 개념 소개를 사용 하 여 inT SQL 스크립트를 **sp_execute_external_script** 시스템 저장 프로시저입니다. 

## <a name="prerequisites"></a>필수 구성 요소

이 연습에서는 이미 설치 되어 다음 중 하나를 사용 하 여 SQL Server 인스턴스에 대 한 액세스를 필요 합니다.

+ [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md), 설치 된 R 언어를 사용 하 여
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

  SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 해야 하므로 해당 외부 스크립팅 기능이 기본적으로 비활성화 됩니다는 알고 있어야 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 되어 있는지 확인 하 고 **SQL Server 실행 패드 서비스** 시작 하기 전에 실행 됩니다.

+ SQL 쿼리를 실행 하는 데 사용 되는 도구입니다. SQL Server 데이터베이스에 연결 하 고 T-SQL 코드를 실행할 수 있는 모든 응용 프로그램을 사용할 수 있습니다. SQL 전문가라면 SQL Server Management Studio(SSMS) 또는 Visual Studio를 사용할 수 있습니다.

이 빠른 시작에서는 SQL Server 내에서 R을 실행 하려면 얼마나 쉬운지 표시할 했습니다 새 **Visual Studio Code 용 mssql 확장**합니다. VS Code는 Windows, Linux, macOS에서 실행할 수 있는 무료 개발 환경입니다. **mssql** 확장은 SQL 쿼리를 실행하기 위한 가벼운 확장입니다. Visual Studio Code를 다운로드하려면 [Download and install Visual Studio Code](https://code.visualstudio.com/Download)(Visual Studio Code 다운로드 및 설치)를 참조하세요. 추가할 합니다 **mssql** 확장을이 문서를 참조 하세요: [Visual Studio Code 용 mssql 확장 사용](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)합니다.

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>데이터베이스에 연결하고 Hello World 테스트 스크립트 실행

1. Visual Studio Code에서 새 텍스트 파일을 만들고 이름을 BasicRSQL.sql로 지정합니다.

2. 이 파일이 열리면 CTRL+SHIFT+P(macOS의 경우 COMMAND + P)를 누르고, **sql**을 입력하여 SQL 명령을 나열하고, **CONNECT**를 선택합니다. Visual Studio Code를 사용하면 특정 데이터베이스에 연결할 때 사용할 프로필을 만들 것인지 묻습니다. 이것은 선택 사항이지만 데이터베이스와 로그인 간에 전환을 쉽게할 수 있습니다.
    + SQL Server의 R이 설치된 서버 또는 인스턴스를 선택합니다.
    + 새 데이터베이스를 만들 권한이 있는 계정을 사용하여 SELECT 문을 실행하고 테이블 정의를 확인합니다.

2. 연결에 성공하면 상태 표시줄에 서버 및 데이터베이스 이름과 현재 자격 증명이 표시되어야 합니다. 연결에 실패하면 컴퓨터 이름과 서버 이름이 정확한지 확인하세요.

3. 이 문을 붙여넣고 실행합니다.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([Hello World] int));
    GO
    ```

이 저장된 프로시저에 대 한 입력은 다음과 같습니다.

+ *@language* 이 경우 R.를 호출 하려면 언어 확장을 정의 하는 매개 변수
+ *@script* 매개 변수를 R 런타임에 전달할 명령을 정의 합니다. 전체 R 스크립트는 이 인수에 유니코드 텍스트로 포함되어야 합니다. **nvarchar** 형식의 변수에 텍스트를 추가한 다음 변수를 호출할 수도 있습니다.
+ *@input_data_1* 데이터를 SQL Server 데이터 프레임으로 데이터를 반환 하는 R 런타임에 전달할 쿼리에 의해 반환 됩니다.
+ WITH RESULT SETS 절 열 이름으로 "Hello World"를 추가 하 고 SQL Server에 대해 반환된 된 데이터 테이블의 스키마를 정의 **int** 데이터 형식에 대 한 합니다.

**결과**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

이 쿼리에서 오류를 받게 되 면 설치 문제를 배제 합니다. 설치 후 구성은 외부 코드 라이브러리를 사용 하도록 설정 하려면 필요 합니다. 참조 [SQL Server 2017 Machine Learning 서비스 설치](../install/sql-machine-learning-services-windows-install.md) 하거나 [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)합니다. 마찬가지로, 실행 패드 서비스가 실행 중인지 확인 합니다. 

환경에 따라 SQL Server에 연결할 R 작업자 계정을 사용하도록 설정하거나, 추가 네트워크 라이브러리를 설치하거나, 원격 코드 실행을 사용하도록 설정하거나, 구성이 완료된 후 인스턴스를 다시 시작해야 할 수 있습니다. 자세한 내용은 참조 하세요. [R Services 설치 및 업그레이드 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)

> [!TIP]
> Visual Studio Code에서 실행할 코드를 강조 표시하고 CTRL+SHIFT+E를 누르면 됩니다. 바로 가기 키를 기억하기 어려우면 변경할 수도 있습니다. [Customize the shortcut key bindings](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)(바로 가기 키 바인딩 사용자 지정)를 참조하세요.
> 
> ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)
> 

## <a name="next-steps"></a>다음 단계

이제 확인 했으면 인스턴스 준비가 되었는지 R을 사용 하 여 작업, 입력 및 출력을 구성에 대해 자세히 살펴보겠습니다.

> [!div class="nextstepaction"]
> [입력 및 출력을 처리 하는 빠른 시작:](rtsql-working-with-inputs-and-outputs.md)
