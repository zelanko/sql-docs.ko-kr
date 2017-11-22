---
title: "R 코드를 사용 하 여 transact-sql (SQL 빠른 시작에서 R) | Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 08/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 4e6fe30d-a105-4d5b-bc05-5e5204753847
caps.latest.revision: "36"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d0915986d39aa6fb376063bf6a2a31a5c5953aa9
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="using-r-code-in-transact-sql-r-in-sql-quickstart"></a>R 코드를 사용 하 여 transact-sql (SQL 빠른 시작에서 R)

이 자습서에서는 T-SQL 저장 프로시저에서 R 스크립트를 호출하는 기본 메커니즘을 단계별로 안내합니다.

**학습 내용**

+ T-SQL 함수에 R을 포함하는 방법
+ R 및 SQL 데이터 형식과 데이터 개체로 작업 하기 위한 몇 가지 팁
+ 간단한 모델을 만들고 SQL Server에 저장 하는 방법
+ 예측 및 모델을 사용 하는 R 플롯을 만드는 방법

**예상된 시간**

30분, 설치 제외

## <a name="prerequisites"></a>필수 구성 요소

이미 설치 된 다음 중 하나가 지정 된 SQL Server의 인스턴스에 액세스할 수 있어야 합니다.

+ SQL Server 2017 컴퓨터 학습 서비스 함께 설치 된 R 언어
+ SQL Server 2016 R Services

Azure 가상 컴퓨터 또는 온-프레미스 SQL Server 인스턴스가 될 수 있습니다. 염두에 두어야 외부 스크립팅 기능 작동 하기 위한 몇 가지 추가 단계를 수행 해야 할 수 있으므로 기본적으로 비활성화 됩니다.

R 스크립트를 포함 하는 SQL 쿼리를 실행 하려면 데이터베이스에 연결 하 고 T-SQL 코드를 실행할 수 있는 다른 응용 프로그램을 사용할 수 있습니다. SQL Server Management Studio (SSMS) 또는 Visual Studio SQL 전문가가 사용할 수 있습니다.

이 자습서에서는 R 내부 SQL Server를 실행 하는 것이 얼마나 쉬운지 표시를 사용 했습니다 새 **Visual Studio Code 확장명이 mssql**합니다. VS Code는 Windows, Linux 또는 macOS 등에서 실행할 수 있는 무료 개발 환경입니다. **mssql*** 확장은 SLq 쿼리를 실행 하기 위한 간단한 확장 합니다. 이 확장을 설치하려면 [Use the mssql extension for Visual Studio Code](https://docs.microsoft.com/sql/linux/sql-server-linux-develop-use-vscode)(Visual Studio Code용 mssql 확장 사용) 문서를 참조하세요.

## <a name="connect-to-a-database-and-run-a-hello-world-test-script"></a>데이터베이스에 연결하고 Hello World 테스트 스크립트 실행

1. Visual Studio Code에서 새 텍스트 파일을 만들고 이름을 BasicRSQL.sql로 지정합니다.
2. 이 파일이 열리면 CTRL+SHIFT+P(macOS의 경우 COMMAND + P)를 누르고, **sql**을 입력하여 SQL 명령을 나열하고, **CONNECT**를 선택합니다. Visual Studio 코드를 사용 하면 특정 데이터베이스에 연결할 때 사용할 프로필을 만들 것인지 묻는 합니다. 이 변수는 옵션 이지만 쉽게 데이터베이스와 로그인 사이 전환할 수 있습니다.
    + 서버 또는 SQL Server에서 R 설치 되어 있는 인스턴스를 선택 합니다.
    + 새 데이터베이스를 만들 권한이 있는 계정을 사용하여 SELECT 문을 실행하고 테이블 정의를 확인합니다.
2. 연결에 성공하면 상태 표시줄에 서버 및 데이터베이스 이름과 현재 자격 증명이 표시되어야 합니다. 연결에 실패하면 컴퓨터 이름과 서버 이름이 정확한지 확인하세요.
3. 이 문을 붙여넣고 실행합니다.

    ```sql
    EXEC sp_execute_external_script
      @language =N'R',
      @script=N'OutputDataSet<-InputDataSet',
      @input_data_1 =N'SELECT 1 AS hello'
      WITH RESULT SETS (([hello] int not null));
    GO
    ```

    Visual Studio Code에서는 실행할 코드를 선택하고 CTRL+SHIFT+E를 누르면 됩니다. 바로 가기 키를 기억하기 어려우면 변경할 수 있습니다. [Customize the shortcut key bindings](https://github.com/Microsoft/vscode-mssql/wiki/customize-shortcuts)(바로 가기 키 바인딩 사용자 지정)를 참조하세요.

    ![rsql-basictut_hello1code](media/rsql-basictut-hello1code.PNG)

**결과**

![rsql_basictut_hello1](media/rsql-basictut-hello1.PNG)

## <a name="troubleshooting"></a>문제 해결

+ 이 쿼리의 모든 오류를 발생 하는 경우 설치 완료 수 있습니다. SQL Server 설치 마법사를 사용하여 기능을 추가한 후 외부 코드 라이브러리를 사용할 수 있도록 몇 가지 추가 단계를 수행해야 합니다.  [SQL Server R Services 설치](../r/set-up-sql-server-r-services-in-database.md)를 참조하세요.

+ 실행 패드 서비스가 실행 중인지 확인합니다. 환경에 따라 SQL Server에 연결할 R 작업자 계정을 사용하도록 설정하거나, 추가 네트워크 라이브러리를 설치하거나, 원격 코드 실행을 사용하도록 설정하거나, 구성이 완료된 후 인스턴스를 다시 시작해야 할 수 있습니다. [R Services 설치 및 업그레이드 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조하세요.

+ Visual Studio Code를 다운로드하려면 [Download and install Visual Studio Code](https://code.visualstudio.com/Download)(Visual Studio Code 다운로드 및 설치)를 참조하세요.

## <a name="next-lesson"></a>다음 단원

인스턴스가 R을 사용할 준비가 상태인 했으므로 이제 시작 하겠습니다.

1 단원: [입 / 출력 작업](rtsql-working-with-inputs-and-outputs.md)

2 단원: [R 및 SQL 데이터 형식과 데이터 개체](rtsql-r-and-sql-data-types-and-data-objects.md)

3 단원: [SQL Server 데이터를 사용 하 여 R 함수](rtsql-using-r-functions-with-sql-server-data.md)

4 단원: [예측 모델 만들기](rtsql-create-a-predictive-model-r.md)

5 단원: [예측 및 플롯 모델에서](rtsql-predict-and-plot-from-model.md)
