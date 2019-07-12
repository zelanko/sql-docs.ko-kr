---
title: SQL Server Machine Learning 컨테이너에서 서비스를 실행 합니다. | Microsoft Docs
description: 이 자습서에서는 Docker에서 실행 중인 Linux 컨테이너에서 SQL Server Machine Learning Services를 사용 하는 방법을 보여 줍니다.
author: uc-msft
ms.author: umajay
manager: craigg
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.collection: linux-container
moniker: '>= sql-server-linux-ver15 || =sqlallproducts-allversions'
ms.openlocfilehash: 3e654e29d6c49d3bf68cdfe7c4e3b479b47a973c
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67840472"
---
# <a name="run-sql-server-machine-learning-services-in-a-container"></a>SQL Server Machine Learning 컨테이너에서 서비스를 실행 합니다.

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 자습서에는 SQL Server Machine Learning Services를 사용 하 여 Docker 컨테이너를 빌드하고 TRANSACT-SQL에서 기계 학습 스크립트를 실행 하는 방법을 보여 줍니다.

> [!div class="checklist"]
> * Mssql docker 리포지토리를 복제 합니다.
> * Machine Learning 서비스를 사용 하 여 SQL Server Linux 컨테이너 이미지를 빌드하십시오.
> * Machine Learning 서비스를 사용 하 여 SQL Server Linux 컨테이너 이미지를 실행 합니다.
> * TRANSACT-SQL 문을 사용 하 여 R 또는 Python 스크립트를 실행 합니다.
> * 중지 하 고 SQL Server Linux 컨테이너를 제거 합니다. 

## <a name="prerequisites"></a>사전 요구 사항

* Git 명령줄 인터페이스입니다.
* 지원되는 모든 Linux 배포판 또는 Mac/Windows용 Docker에서 Docker Engine 1.8+. 자세한 내용은 [사용자 Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.
* 최소 2gb의 디스크 공간입니다.
* 최소 2gb의 RAM입니다.
* [Linux에서 SQL Server에 대한 시스템 요구 사항](sql-server-linux-setup.md#system)

## <a name="clone-the-mssql-docker-repository"></a>Mssql docker 리포지토리 복제

1. Windows에서 Linux/Mac 또는 WSL 터미널에서 bash 터미널을 엽니다.

1. Mssql docker 리포지토리 복사본을 로컬로 저장 하도록 로컬 디렉터리를 만듭니다.
1. Mssql docker 리포지토리를 복제 git 복제 명령은 실행 합니다.

    ```bash
    git clone https://github.com/microsoft/mssql-docker mssql-docker
    ```

## <a name="build-sql-server-linux-container-image-with-machine-learning-services"></a>Machine Learning 서비스를 사용 하 여 SQL Server Linux 컨테이너 이미지 빌드

1. Mssql mlservices 디렉터리로 디렉터리를 변경 합니다.

    ```bash
    cd mssql-docker/linux/preview/examples/mssql-mlservices
    ```

1. Build.sh 스크립트를 실행 합니다.

   ```bash
   ./build.sh
   ```

   > [!NOTE]
   > Docker 이미지의 크기가 몇 Gb 수 있는 패키지를 설치에 필요 합니다. 스크립트에는 네트워크 대역폭에 따라 20 분 정도 걸릴 수 있습니다.

## <a name="run-sql-server-linux-container-image-with-machine-learning-services"></a>Machine Learning 서비스를 사용 하 여 SQL Server Linux 컨테이너 이미지 실행

1. 컨테이너를 실행 하기 전에 환경 변수를 설정 합니다. 호스트 디렉터리 PATH_TO_MSSQL 환경 변수를 설정 합니다.

   ```bash
    export MSSQL_PID='Developer'
    export ACCEPT_EULA='Y'
    export ACCEPT_EULA_ML='Y'
    export PATH_TO_MSSQL='/home/mssql/'
   ```

1. Run.sh 스크립트를 실행 합니다.

   ```bash
   ./run.sh
   ```

   이 명령은 Developer edition (기본값)를 사용 하 여 Machine Learning 서비스를 사용 하 여 SQL Server 컨테이너를 만듭니다. SQL Server 포트 **1433** 포트와 호스트에 노출 됩니다 **1401**합니다.

   > [!NOTE]
   > 컨테이너에서 프로덕션 SQL Server 버전을 실행 하기 위한 프로세스는 약간 다릅니다. 자세한 내용은 [프로덕션 컨테이너 이미지 실행](sql-server-linux-configure-docker.md#production)을 참조하세요. 동일한 컨테이너 이름 및 포트를 사용 하는 경우이 연습의 나머지 프로덕션 컨테이너를 사용 하 여 계속 작동 합니다.

1. Docker 컨테이너를 보려면 `docker ps` 명령을 사용합니다.

   ```bash
   sudo docker ps -a
   ```

1. **상태** 열이 **Up**의 상태를 표시하는 경우, SQL Server는 컨테이너에서 실행되며 **포트** 열의 지정된 포트에서 수신 대기합니다. SQL Server 컨테이너의 **상태** 열이 **Exited**를 표시하는 경우, [구성 가이드의 문제 해결 섹션](sql-server-linux-configure-docker.md#troubleshooting)을 참조하세요.

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

## <a name="execute-r--python-scripts-from-transact-sql"></a>R 실행 Transact SQL에서 Python 스크립트 /

1. 컨테이너의 SQL Server에 연결한 다음 T-SQL 문을 실행 하 여 외부 스크립트 구성 옵션을 사용 하도록 설정 합니다.

    ```sql
    EXEC sp_configure  'external scripts enabled', 1
    RECONFIGURE WITH OVERRIDE
    go
    ```

1. Machine Learning 서비스는 다음과 같은 간단한 R/Python sp_execute_external_script를 실행 하 여 작업을 확인 합니다.

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

이 자습서에서는 다음 작업을 알아보았습니다.

> [!div class="checklist"]
> * Mssql docker 리포지토리를 복제 합니다.
> * Machine Learning 서비스를 사용 하 여 SQL Server Linux 컨테이너 이미지를 빌드하십시오.
> * Machine Learning 서비스를 사용 하 여 SQL Server Linux 컨테이너 이미지를 실행 합니다.
> * TRANSACT-SQL 문을 사용 하 여 R 또는 Python 스크립트를 실행 합니다.
> * 중지 하 고 SQL Server Linux 컨테이너를 제거 합니다.

다음으로, 다른 Docker 구성 및 문제 해결 시나리오를 검토 합니다.

> [!div class="nextstepaction"]
>[Docker에서 SQL Server에 대 한 구성 가이드](sql-server-linux-configure-docker.md)
