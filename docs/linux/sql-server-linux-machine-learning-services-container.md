---
title: 컨테이너에서 SQL Server Machine Learning Services 실행 | Microsoft Docs
description: 이 자습서에서는 Docker에서 실행되는 Linux 컨테이너에서 SQL Server Machine Learning Services를 사용하는 방법을 보여줍니다.
author: uc-msft
ms.author: umajay
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
monikerRange: '>= sql-server-linux-ver15  || >= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 28bdf20b51769e15a887b4f9ec227f7aaf6afc95
ms.sourcegitcommit: 071065bc5433163ebfda4fdf6576349f9d195663
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/03/2019
ms.locfileid: "71923818"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>컨테이너에서 SQL Server Machine Learning Services 실행

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 자습서에서는 SQL Server Machine Learning Services를 사용하여 Docker 컨테이너를 빌드하고 Transact-SQL에서 Machine Learning 스크립트를 실행하는 방법을 보여줍니다. 적용 범위에는 다음 작업이 포함됩니다.

> [!div class="checklist"]
> * mssql-docker 리포지토리를 복제합니다.
> * Machine Learning Services를 사용하여 SQL Server Linux 컨테이너 이미지를 빌드합니다.
> * Machine Learning Services를 사용하여 SQL Server Linux 컨테이너 이미지를 실행합니다.
> * Transact-SQL 문을 사용하여 R 또는 Python 스크립트를 실행합니다.
> * SQL Server Linux 컨테이너를 중지하고 제거합니다.

## <a name="prerequisites"></a>사전 요구 사항

* Git 명령줄 인터페이스.
* 지원되는 모든 Linux 배포판에서 Docker Engine 1.8 이상 또는 Mac/Windows용 Docker. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.
* 최소 2GB(기가바이트)의 디스크 공간.
* 최소 2GB의 RAM.
* [Linux에서 SQL Server에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)

## <a name="clone-the-mssql-docker-repository"></a>mssql-docker 리포지토리 복제

1. Linux/Mac에서 Bash 터미널을 열거나 Windows에서 WSL 터미널에서 엽니다.

1. mssql-docker 리포지토리의 로컬 복사본을 보관할 로컬 디렉터리를 만듭니다.
1. Git 복제 명령을 실행하여 mssql-docker 리포지토리 복제:

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-a-sql-server-linux-container-image-with-machine-learning-services"></a>Machine Learning Services를 사용하여 SQL Server Linux 컨테이너 이미지 빌드

1. 디렉터리를 mssql-mlservices 디렉터리로 변경:

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. build.sh 스크립트 실행:

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Docker 이미지를 빌드하려면 크기가 몇 GB인 패키지를 설치해야 합니다. 스크립트는 네트워크 대역폭에 따라 실행을 완료하는 데 최대 20분이 걸릴 수 있습니다.

## <a name="run-the-sql-server-linux-container-image-with-machine-learning-services"></a>Machine Learning Services를 사용하여 SQL Server Linux 컨테이너 이미지 실행

1. 컨테이너를 실행하기 전에 환경 변수를 설정합니다. PATH_TO_MSSQL 환경 변수를 호스트 디렉터리로 설정:

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. run.sh 스크립트 실행:

   ```bash
   ./run.sh
   ```

   이 명령은 Developer Edition(기본값)을 사용하여 Machine Learning Services가 포함된 SQL Server 컨테이너를 만듭니다. SQL Server 포트 **1433**은 호스트에서 포트 **1401**로 공개됩니다.

   > [!NOTE]
   > 컨테이너에서 프로덕션 SQL Server 버전을 실행하는 프로세스는 약간 다릅니다. 자세한 내용은 [Docker에서 SQL Server 컨테이너 이미지 구성](sql-server-linux-configure-docker.md)을 참조하세요. 동일한 컨테이너 이름 및 포트를 사용하는 경우 이 연습의 나머지 부분은 여전히 프로덕션 컨테이너로 진행됩니다.

1. Docker 컨테이너를 보려면 `docker ps` 명령 실행:

   ```bash
   sudo docker ps -a
   ```

1. **STATUS** 열이 **Up**의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **PORTS** 열의 지정된 포트에서 수신 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited**를 표시하는 경우, [구성 가이드의 문제 해결 섹션](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

   ```bash
   $ sudo docker ps -a
   ```

    출력: 
    
    ```
    CONTAINER ID        IMAGE                          COMMAND                  CREATED             STATUS              PORTS                    NAMES
    941e1bdf8e1d        mcr.microsoft.com/mssql/server/mssql-server-linux   "/bin/sh -c /opt/m..."   About an hour ago   Up About an hour     0.0.0.0:1401->1433/tcp   sql1
    ```

## <a name="change-the-sa-password"></a>SA 암호 변경

[!INCLUDE [Change docker password](../includes/sql-server-linux-change-docker-password.md)]

## <a name="execute-r--python-scripts-from-transact-sql"></a>Transact-SQL에서 R/Python 스크립트 실행

1. 컨테이너의 SQL Server에 연결하고 다음 T-SQL 문을 실행하여 외부 스크립트 구성 옵션을 사용하도록 설정합니다.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. 다음과 같은 간단한 R/Python sp_execute_external_script를 실행하여 Machine Learning Services가 작동하는지 확인합니다.

    ```sql
    execute sp_execute_external_script 
    @language = N'R',
    @script = N'
    print("Hello World!")
    print(R.version)
    print(Revo.version)
    OutputDataSet <- InputDataSet', 
    @input_data_1 = N'select 1'
    with result sets((i int));
    go
    ```

    ```sql
    execute sp_execute_external_script 
    @language = N'Python',
    @script = N'
    import sys
    print(sys.version)
    print("Hello World!")
    OutputDataSet = InputDataSet',
    @input_data_1 = N'select 1'
    with result sets((i int));
    go 
    ```

## <a name="next-steps"></a>다음 단계

이 자습서에서는 다음을 수행하는 방법을 배웠습니다.

> [!div class="checklist"]
> * mssql-docker 리포지토리 복제
> * Machine Learning Services를 사용하여 SQL Server Linux 컨테이너 이미지 빌드
> * Machine Learning Services를 사용하여 SQL Server Linux 컨테이너 이미지 실행
> * Transact-SQL 문을 사용하여 R 또는 Python 스크립트 실행
> * SQL Server Linux 컨테이너를 중지하고 제거

다음으로, 다른 Docker 구성 및 문제 해결 시나리오를 검토합니다.

> [!div class="nextstepaction"]
>[Docker에서 SQL Server에 대한 구성 가이드](sql-server-linux-configure-docker.md)
