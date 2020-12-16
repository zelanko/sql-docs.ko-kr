---
title: Docker에 설치
titleSuffix: SQL Server Machine Learning Services
description: Docker에 SQL Server Machine Learning Services(Python 및 R)를 설치하는 방법을 알아봅니다.
author: dphansen
ms.author: davidph
manager: cgronlun
ms.date: 05/11/2020
ms.topic: how-to
ms.prod: sql
ms.technology: machine-learning-services
monikerRange: '>=sql-server-ver15||>=sql-server-linux-ver15'
ms.openlocfilehash: 271d6c9d8f2184c9625903afa9d3f8594c269359
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97471454"
---
# <a name="install-sql-server-machine-learning-services-python-and-r-on-docker"></a>Docker에 SQL Server Machine Learning Services(Python 및 R) 설치

[!INCLUDE [SQL Server 2019 - Linux](../includes/applies-to-version/sqlserver2019-linux.md)]

이 문서에서는 Docker에 SQL Server Machine Learning Services를 설치하는 방법을 설명합니다. Machine Learning Services를 사용하여 데이터베이스에서 R 또는 Python 스크립트를 실행할 수 있습니다. 미리 빌드된 컨테이너는 Machine Learning Services와 함께 제공하지 않습니다. [GitHub에서 제공되는 예제 템플릿](https://github.com/Microsoft/mssql-docker/tree/master/linux/preview/examples/mssql-mlservices)을 사용하여 SQL Server 컨테이너에서 새로 만들 수 있습니다.

## <a name="prerequisites"></a>필수 구성 요소

- Git 명령줄 인터페이스.

- 지원되는 모든 Linux 배포판에서 Docker Engine 1.8 이상 또는 Mac/Windows용 Docker. 자세한 내용은 [Get Docker](https://docs.docker.com/get-docker/)(Docker 가져오기)를 참조하세요.

- [SQL Server on Linux의 시스템 요구 사항](sql-server-linux-setup.md#system)도 참조하세요.

## <a name="clone-the-mssql-docker-repository"></a>mssql-docker 리포지토리 복제

다음 명령은 `mssql-docker` git 리포지토리를 로컬 디렉터리로 복제합니다.

1. Linux 또는 Mac에서 Bash 터미널을 엽니다.

2. mssql-docker 리포지토리의 로컬 복사본을 보관할 디렉터리를 만듭니다.

3. Git 복제 명령을 실행하여 mssql-docker 리포지토리 복제:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image"></a>SQL Server Linux 컨테이너 이미지를 빌드합니다.

다음 단계에 따라 Docker 이미지를 빌드합니다.

1. 디렉터리를 mssql-mlservices 디렉터리로 변경:
    
    ```bash
    /mssql-docker/linux/preview/examples/mssql-mlservices
    ```

2. 동일한 디렉터리에서 다음 명령을 실행합니다.

    ```bash
    docker build -t mssql-server-mlservices .
    ```

3. 명령 실행:

    ```bash
    docker run -d -e MSSQL_PID=Developer -e ACCEPT_EULA=Y -e ACCEPT_EULA_ML=Y -e MSSQL_SA_PASSWORD=<password> -v <directory on the host OS>:/var/opt/mssql -p 1433:1433 mssql-server-mlservices
    ```
  
    > [!NOTE]
    > MSSQL_PID에 다음 값을 사용할 수 있습니다. Developer(무료), Express (무료), Enteprise(유료), Standard(유료). 유료 버전을 사용하는 경우 라이선스를 구입했는지 확인하세요. (password)를 실제 암호로 바꿉니다. -v를 사용한 볼륨 탑재는 선택 사항입니다. (directory on the host OS)를 데이터베이스 데이터 및 로그 파일을 탑재하려는 실제 디렉터리로 바꿉니다.
    

4. 다음 명령을 실행하여 확인합니다.

    ```bash
    docker ps -a
    ```

   > [!NOTE]
   > Docker 이미지를 빌드하려면 크기가 몇 GB인 패키지를 설치해야 합니다. 스크립트의 실행이 완료되는 데는 네트워크 대역폭에 따라 얼마간의 시간이 걸릴 수 있습니다.

## <a name="run-the-sql-server-linux-container-image"></a>SQL Server Linux 컨테이너 이미지를 실행합니다.

1. 컨테이너를 실행하기 전에 환경 변수를 설정합니다. PATH_TO_MSSQL 환경 변수를 호스트 디렉터리로 설정:

   ```bash
   export MSSQL_PID='Developer'
   export ACCEPT_EULA='Y'
   export ACCEPT_EULA_ML='Y'
   export PATH_TO_MSSQL='/home/mssql/'
   ```
  
   > [!NOTE]
   > 컨테이너에서 프로덕션 SQL Server 버전을 실행하는 프로세스는 약간 다릅니다. 자세한 내용은 [Docker에서 SQL Server 컨테이너 이미지 구성](./sql-server-linux-docker-container-deployment.md)을 참조하세요. 동일한 컨테이너 이름 및 포트를 사용하는 경우 이 연습의 나머지 부분은 프로덕션 컨테이너에서도 계속 작동합니다.

2. Docker 컨테이너를 보려면 `docker ps` 명령 실행:

   ```bash
   sudo docker ps -a
   ```

3. **STATUS** 열이 **Up** 의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **PORTS** 열에 지정된 포트에서 수신을 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited** 를 표시하는 경우, [구성 가이드의 문제 해결 섹션](./sql-server-linux-docker-container-troubleshooting.md)을 참조하세요.

 
    출력:

    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="enable-machine-learning-services"></a>Machine Learning Services 사용 설정

Machine Learning Services를 사용하도록 설정하려면 SQL Server 인스턴스에 연결하여 다음과 같은 T-SQL 문을 실행합니다.

```sql
EXEC sp_configure  'external scripts enabled', 1;
RECONFIGURE WITH OVERRIDE
```

## <a name="next-steps"></a>다음 단계

Python 개발자는 다음 자습서에 따라 SQL Server에서 Python을 사용하는 방법을 알아볼 수 있습니다.

+ [Python 자습서: SQL Server Machine Learning Services에서 선형 회귀를 사용하여 스키 대여 예측](../machine-learning/tutorials/python-ski-rental-linear-regression-deploy-model.md)
+ [Python 자습서: Categorizing customers using k-means clustering with SQL Server Machine Learning Services](../machine-learning/tutorials/python-clustering-model.md)(SQL Server Machine Learning Services에서 k-평균 클러스터링을 사용하여 고객 분류)

R 개발자는 몇 가지 간단한 예제를 시작하고 R이 SQL Server에서 작동하는 방식의 기초를 알아볼 수 있습니다. 다음 단계로 가려면 아래 링크를 참조하세요.

+ [빠른 시작: T-SQL에서 R 사용](../machine-learning/tutorials/quickstart-r-create-script.md)
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../machine-learning/tutorials/r-taxi-classification-introduction.md)