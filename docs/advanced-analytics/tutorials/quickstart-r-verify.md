---
title: SQL Server에 R이 있는지 확인 하는 빠른 시작
description: R 및 Machine Learning Services가 SQL Server에 있는지 확인 하기 위한 빠른 시작입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 951ffc07a32434b2f8d333140445f12c2971b811
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470612"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>빠른 시작: SQL Server에 R이 있는지 확인 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server에는 상주 하는 SQL Server 데이터에 대 한 데이터 과학 분석에 대 한 R 언어 지원이 포함 됩니다. R 스크립트는 오픈 소스 R 함수, 타사 R 라이브러리 또는 기본 제공 Microsoft R 라이브러리로 구성 됩니다 (예: [RevoScaleR](../r/revoscaler-overview.md) 예측 분석의 경우).

다음 방법 중 하나를 사용 하 여 저장 프로시저를 통해 스크립트를 실행 합니다.

+ 에서 R 스크립트를 입력 매개 변수로 전달 하는 기본 제공 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 저장 프로시저입니다.
+ 사용자가 만든 [사용자 지정 저장 프로시저](sqldev-in-database-r-for-sql-developers.md) 에서 R 스크립트를 래핑합니다.

이 빠른 시작에서는 [SQL Server 2017 Machine Learning Services](../what-is-sql-server-machine-learning.md) 또는 [SQL Server 2016 R 서비스가](../r/sql-server-r-services.md) 설치 및 구성 되었는지 확인 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 연습을 수행 하려면 다음 중 하나를 사용 하 여 SQL Server 인스턴스에 액세스 해야 합니다.

+ R 언어가 설치 된 [SQL Server 2017 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md)
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 외부 스크립팅 기능은 기본적으로 사용 하지 않도록 설정 되어 있으므로 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 하 고 시작 하기 전에 **SQL Server 실행 패드 서비스가** 실행 중인지 확인 해야 할 수 있습니다.

또한 SQL 쿼리를 실행 하기 위한 도구도 필요 합니다. 모든 데이터베이스 관리 또는 쿼리 도구를 사용 하 여 SQL Server 인스턴스에 연결 하 고 T-sql 쿼리 또는 저장 프로시저를 실행 하 여 R 스크립트를 실행할 수 있습니다. 이 빠른 시작에서는 [SSMS (SQL Server Management Studio)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)를 사용 합니다.

## <a name="verify-r-exists"></a>R 존재 확인

SQL Server 인스턴스에 Machine Learning Services (R 사용)를 사용 하도록 설정 하 고 설치 된 R 버전을 확인할 수 있습니다. 다음 단계를 수행 합니다.

1. SQL Server Management Studio를 열고 SQL Server 인스턴스에 연결 합니다.

2. 아래 코드를 실행 합니다. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R `print` 함수는 버전을 **메시지** 창에 반환 합니다. 아래 예제 출력에서이 경우에 R 버전 3.3.3가 설치 되어 SQL Server 확인할 수 있습니다.

    **결과**

    ```text
    platform       x86_64-w64-mingw32          
    arch           x86_64                      
    os             mingw32                     
    system         x86_64, mingw32             
    status                                     
    major          3                           
    minor          3.3                         
    year           2017                        
    month          03                          
    day            06                          
    svn rev        72310                       
    language       R                           
    version.string R version 3.3.3 (2017-03-06)
    nickname       Another Canoe               
    ```

이 쿼리에서 오류가 발생 하면 설치 문제를 모두 해결 하십시오. 외부 코드 라이브러리를 사용 하도록 설정 하려면 설치 후 구성이 필요 합니다. [SQL Server 2017 Machine Learning Services 설치](../install/sql-machine-learning-services-windows-install.md) 또는 [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)를 참조 하세요. 마찬가지로 실행 패드 서비스가 실행 중인지 확인 합니다.

환경에 따라 SQL Server에 연결할 R 작업자 계정을 사용하도록 설정하거나, 추가 네트워크 라이브러리를 설치하거나, 원격 코드 실행을 사용하도록 설정하거나, 구성이 완료된 후 인스턴스를 다시 시작해야 할 수 있습니다. 자세한 내용은 [R Services 설치 및 업그레이드 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)를 참조 하세요.

## <a name="list-r-packages"></a>R 패키지 나열

Microsoft는 SQL Server 인스턴스에서 Machine Learning Services와 함께 미리 설치 된 여러 R 패키지를 제공 합니다. 버전, 종속성, 라이선스 및 라이브러리 경로 정보를 포함 하 여 설치 된 R 패키지 목록을 보려면 아래 단계를 수행 합니다.

1. SQL Server 인스턴스에서 아래 스크립트를 실행 합니다.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. 출력은 R의 `installed.packages()` 에서 가져온 후 결과 집합으로 반환 됩니다.

    **결과**

    ![R의 설치 된 패키지](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>다음 단계

이제 인스턴스가 R에서 사용할 준비가 되었는지 확인 했으므로 기본 R 상호 작용에 대해 자세히 살펴보겠습니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server에서 "Hello 세계" R 스크립트](quickstart-r-run-using-tsql.md)
