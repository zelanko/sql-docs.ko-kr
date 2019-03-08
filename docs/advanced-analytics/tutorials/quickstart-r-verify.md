---
title: SQL Server에 있는 R 확인 하기 위한 빠른 시작
description: R 및 Machine Learning Services SQL Server에 있는지 확인 하기 위한 빠른 시작입니다.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 0f461a00c1b9ecca1569b2b4f6257966c075491c
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/07/2019
ms.locfileid: "57579693"
---
# <a name="quickstart-verify-r-exists-in-sql-server"></a>빠른 시작: SQL Server에 R이 있는지 확인 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server에 있는 SQL Server 데이터에 대 한 데이터 과학 분석에 대 한 R 언어 지원이 포함 됩니다. R 스크립트와 같은 오픈 소스 R 함수, 타사 R 라이브러리 또는 기본 제공 Microsoft R 라이브러리의 구성할 수 있습니다 [RevoScaleR](../r/revoscaler-overview.md) 규모에서 예측 분석에 대 한 합니다.

다음 방법 중 하나를 사용 하 여 저장된 프로시저를 통해 스크립트 실행이 됩니다.

+ 기본 제공 [sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql) 저장 프로시저에서 R 스크립트를 입력된 매개 변수로 전달 합니다.
+ R 스크립트를 래핑하는 [사용자 지정 저장 프로시저](sqldev-in-database-r-for-sql-developers.md) 만든 합니다.

이 빠른 시작에서는 하는지 확인 [SQL Server 2017의 Machine Learning Services](../what-is-sql-server-machine-learning.md) 하거나 [SQL Server 2016 R Services](../r/sql-server-r-services.md) 설치 및 구성 합니다.

## <a name="prerequisites"></a>사전 요구 사항

이 연습에서는 이미 설치 되어 다음 중 하나를 사용 하 여 SQL Server 인스턴스에 대 한 액세스를 필요 합니다.

+ [SQL Server 2017의 Machine Learning Services](../install/sql-machine-learning-services-windows-install.md), 설치 된 R 언어를 사용 하 여
+ [SQL Server 2016 R Services](../install/sql-r-services-windows-install.md)

SQL Server 인스턴스는 Azure 가상 머신 또는 온-프레미스에 있을 수 있습니다. 해야 하므로 해당 외부 스크립팅 기능이 기본적으로 비활성화 됩니다는 알고 있어야 [외부 스크립팅을 사용 하도록 설정](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature) 되어 있는지 확인 하 고 **SQL Server 실행 패드 서비스** 시작 하기 전에 실행 됩니다.

또한 SQL 쿼리를 실행 하기 위한 도구가 필요 합니다. 데이터베이스 관리를 사용 하 여 R 스크립트를 실행할 수도 있고 SQL Server 인스턴스에 연결 하는 T-SQL 쿼리 또는 저장된 프로시저를 실행 하기만 도구인 쿼리 수 있습니다. 이 빠른 시작에서는 [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)합니다.

## <a name="verify-r-exists"></a>R 있는지 확인

Machine Learning 서비스 (R)로 설치 된 r 버전 SQL Server 인스턴스에 대해 활성화 되어 있는지 확인할 수 있습니다. 다음 단계를 수행 합니다.

1. SQL Server Management Studio를 열고 SQL Server 인스턴스에 연결 합니다.

2. 아래 코드를 실행 합니다. 

    ```SQL
    EXECUTE sp_execute_external_script
    @language =N'R',
    @script=N'print(version)';
    GO
    ```

3. R `print` 함수는 버전을 반환 합니다 **메시지** 창입니다. 다음 예제 출력에서 볼 수 있습니다 SQL Server에이 경우 R 버전 3.3.3 설치 해야 합니다.

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

이 쿼리에서 오류를 받게 되 면 설치 문제를 배제 합니다. 설치 후 구성은 외부 코드 라이브러리를 사용 하도록 설정 하려면 필요 합니다. 참조 [SQL Server 2017 Machine Learning 서비스 설치](../install/sql-machine-learning-services-windows-install.md) 하거나 [SQL Server 2016 R Services 설치](../install/sql-r-services-windows-install.md)합니다. 마찬가지로, 실행 패드 서비스가 실행 중인지 확인 합니다.

환경에 따라 SQL Server에 연결할 R 작업자 계정을 사용하도록 설정하거나, 추가 네트워크 라이브러리를 설치하거나, 원격 코드 실행을 사용하도록 설정하거나, 구성이 완료된 후 인스턴스를 다시 시작해야 할 수 있습니다. 자세한 내용은 [R Services 설치 및 업그레이드 FAQ](../r/upgrade-and-installation-faq-sql-server-r-services.md)합니다.

## <a name="list-r-packages"></a>목록 R 패키지

Microsoft은 SQL Server 인스턴스에서 Machine Learning 서비스를 사용 하 여 미리 설치 된 R 패키지의 수를 제공 합니다. r 패키지도 설치, 버전, 종속성, 라이선스 및 라이브러리 경로 정보를 포함 하 여 목록을 보려면 다음 단계를 수행 합니다.

1. SQL Server 인스턴스에서 아래 스크립트를 실행 합니다.

    ```SQL
    EXECUTE sp_execute_external_script @language = N'R'
    , @script = N'
    OutputDataSet <- data.frame(installed.packages()[,c("Package", "Version", "Depends", "License", "LibPath")]);'
    WITH result sets((Package NVARCHAR(255), Version NVARCHAR(100), Depends NVARCHAR(4000)
        , License NVARCHAR(1000), LibPath NVARCHAR(2000)));
    ```

2. 출력은 `installed.packages()` R에서 결과적으로 집합을 반환 합니다.

    **결과**

    ![R에서 패키지 설치](./media/rsql-installed-packages.png)

## <a name="next-steps"></a>다음 단계

인스턴스에 R을 사용 하 여 사용할 준비가 되었는지 확인 했으므로 자세히 보기 기본 R 상호 작용을 수행 합니다.

> [!div class="nextstepaction"]
> [빠른 시작: SQL Server에서 R 스크립트의 "hello world"](quickstart-r-run-using-tsql.md)
