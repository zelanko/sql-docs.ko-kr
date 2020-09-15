---
title: Azure Data Studio Notebook(Python, R)
description: SQL Server Machine Learning Services를 사용하여 Azure Data Studio Notebook에서 Python 및 R 스크립트를 실행하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/09/2020
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: b7f711ae8b90762003f903b7fd4a59771c5d3f53
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/13/2020
ms.locfileid: "88178690"
---
# <a name="run-python-and-r-scripts-in-azure-data-studio-notebooks-with-sql-server-machine-learning-services"></a>SQL Server Machine Learning Services를 사용하여 Azure Data Studio Notebook에서 Python 및 R 스크립트 실행
[!INCLUDE [SQL Server 2017 and later](../../includes/applies-to-version/sqlserver2017.md)]

[SQL Server Machine Learning Services](../sql-server-machine-learning-services.md)를 사용하여 [Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/what-is) Notebook에서 Python 및 R 스크립트를 실행하는 방법을 알아봅니다. Azure Data Studio는 플랫폼 간 데이터베이스 도구입니다.

## <a name="prerequisites"></a>사전 요구 사항

- 워크스테이션 컴퓨터에서 [Azure Data Studio 다운로드 및 설치](https://docs.microsoft.com/sql/azure-data-studio/download-azure-data-studio). Azure Data Studio는 플랫폼 간 도구이며 Windows, macOS, Linux에서 실행됩니다.

- SQL Server Machine Learning Services가 설치되고 사용하도록 설정된 서버. Windows, Linux 또는 빅 데이터 클러스터에서 Machine Learning Services를 사용할 수 있습니다.

  - [Windows에 SQL Server Machine Learning Services 설치](sql-machine-learning-services-windows-install.md)
  - [Linux에 SQL Server Machine Learning Services 설치](../../linux/sql-server-linux-setup-machine-learning.md)
  - [SQL Server 빅 데이터 클러스터에서 Machine Learning Services를 사용하여 Python 및 R 스크립트 실행](../../big-data-cluster/machine-learning-services.md)

## <a name="create-a-sql-notebook"></a>SQL Notebook 만들기

> [!IMPORTANT]
> Machine Learning Services는 SQL Server의 일부로 실행됩니다. 따라서 Python 커널이 아닌 SQL 커널을 사용해야 합니다.

Azure Data Studio에서 SQL Notebook과 함께 Machine Learning Services를 사용할 수 있습니다. 새 Notebook을 만들려면 다음 단계를 수행합니다.

1. **파일**, **새 Notebook**을 차례로 클릭하여 새 Notebook을 만듭니다. Notebook은 기본적으로 **SQL 커널**을 사용합니다.

1. **연결 대상**, **연결 변경**을 차례로 클릭합니다. 

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook 연결 변경](media/ads-attach-to-connection.png)
    
1. 기존 SQL Server나 새 SQL Server에 연결합니다. 다음 작업 중 하나를 수행할 수 있습니다.

    1. **최근 연결** 또는 **저장된 연결**에서 기존 연결을 선택합니다.

    1. **연결 정보**에서 새 연결을 만듭니다. SQL Server 및 데이터베이스에 대한 연결 정보를 입력합니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook 연결 정보](media/ads-connection-details.png)  

## <a name="run-python-or-r-scripts"></a>Python 또는 R 스크립트 실행

SQL Notebook은 코드와 텍스트 셀로 구성됩니다. 코드 셀은 저장 프로시저 [sp_execute_external_scripts](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 통해 Python 또는 R 스크립트를 실행하는 데 사용됩니다. 텍스트 셀은 Notebook에서 코드를 문서화하는 데 사용할 수 있습니다.

### <a name="run-a-python-script"></a>Python 스크립트 실행

Python 스크립트를 실행하려면 다음 단계를 수행합니다.

1. **+ 코드**를 클릭하여 코드 셀을 추가합니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook 코드 블록 추가](media/ads-add-code.png)  

1. 코드 셀에 다음 스크립트를 입력합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'Python'
        , @script = N'
    a = 1
    b = 2
    c = a/b
    d = a*b
    print(c, d)
    '
    ```

1. **셀 실행**(원형 검은색 화살표)을 클릭하거나 **F5** 키를 눌러 단일 셀을 실행합니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook Python 코드 실행](media/ads-run-python.png)  

1. 결과가 코드 셀 아래에 표시됩니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook Python 코드 출력](media/ads-run-python-output.png)  

### <a name="run-an-r-script"></a>R 스크립트 실행

R 스크립트를 실행하려면 다음 단계를 수행합니다.

1. **+ 코드**를 클릭하여 코드 셀을 추가합니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook 코드 블록 추가](media/ads-add-code.png)  

1. 코드 셀에 다음 스크립트를 입력합니다.

    ```sql
    EXECUTE sp_execute_external_script @language = N'R'
        , @script = N'
    a <- 1
    b <- 2
    c <- a/b
    d <- a*b
    print(c(c, d))
    '
    ```

1. **셀 실행**(원형 검은색 화살표)을 클릭하거나 **F5** 키를 눌러 단일 셀을 실행합니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook R 코드 실행](media/ads-run-r.png)  

1. 결과가 코드 셀 아래에 표시됩니다.

    > [!div class="mx-imgBorder"]
    > ![Azure Data Studio SQL Notebook R 코드 출력](media/ads-run-r-output.png)  

## <a name="next-steps"></a>다음 단계

- [Azure Data Studio에서 Notebook을 사용하는 방법](../../azure-data-studio/notebooks-guidance.md)
- [SQL Server Notebook 만들기 및 실행](../../azure-data-studio/notebooks-tutorial-sql-kernel.md)
- [빠른 시작: SQL Server Machine Learning Services로 간단한 Python 스크립트 실행](../tutorials/quickstart-python-create-script.md)
- [빠른 시작: SQL Server Machine Learning Services로 간단한 R 스크립트 실행](../tutorials/quickstart-r-create-script.md)
