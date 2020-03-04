---
title: SQL Notebook을 사용하는 방법
titleSuffix: Azure Data Studio
description: Azure Data Studio에서 SQL Notebook을 사용하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; maghan; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.custom: seodec18
ms.date: 06/28/2019
ms.openlocfilehash: b2651dd2d95f0fb8b5aba37b1d755bc26a781dde
ms.sourcegitcommit: 844793cd1c058e6bba136f050734e7dc62024a82
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/25/2020
ms.locfileid: "77575413"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Azure Data Studio에서 Notebook을 사용하는 방법

이 문서에서는 Azure Data Studio에서 Notebook 환경을 시작하는 방법 및 고유한 Notebook 작성을 시작하는 방법을 설명합니다. 또한 다양한 커널을 사용하여 Notebook을 작성하는 방법을 보여 줍니다.

## <a name="connect-to-sql-server"></a>SQL Server에 연결

Azure Data Studio에서 Microsoft SQL Server 연결 형식에 연결할 수 있습니다.
Azure Data Studio에서 F1 키를 누른 다음, **새 연결**을 클릭하여  해당 SQL Server에 연결할 수도 있습니다.

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Notebook 시작

새 Notebook을 시작하는 방법에는 여러 가지가 있습니다.

1. Azure Data Studio에서 **파일 메뉴**로 이동한 다음, **새 Notebook**을 클릭합니다.

    ![image3](media/sql-notebooks/file-new-notebook.png)

2. **SQL Server** 연결을 마우스 오른쪽 단추로 클릭하고 **새 Notebook**을 시작합니다. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

3. 명령 팔레트(**Ctrl+Shift+P**)를 열고 **새 Notebook**을 입력합니다. `Notebook-1.ipynb`라는 새 파일이 열립니다.

## <a name="supported-kernels-and-attach-to-context"></a>지원되는 커널 및 컨텍스트에 연결

Azure Data Studio의 Notebook 설치는 기본적으로 SQL 커널을 지원합니다. SQL 개발자이고 Notebook을 사용하려는 경우 이 커널을 선택하면 됩니다.

SQL 커널을 사용하여 PostgreSQL 서버 인스턴스에 연결할 수도 있습니다. PostgreSQL 개발자이며 PostgreSQL 서버에 연결하려는 경우 Azure Data Studio 확장 Marketplace에서 [**PostgreSQL 확장**](postgres-extension.md)을 다운로드합니다.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL 커널

Microsoft는 쿼리 편집기와 유사한 Notebook 내의 코드 셀에서 다양한 기능의 SQL 편집기, IntelliSense 및 기본 제공 코드 조각과 같은 기본 제공 기능을 통해 일상적인 작업을 간편하게 수행할 수 있는 최신 SQL 코딩 환경을 지원합니다. 코드 조각을 사용하여 데이터베이스, 테이블, 뷰, 저장 프로시저 등을 만드는 적절한 SQL 구문을 생성하고 기존 데이터베이스 개체를 업데이트할 수 있습니다. 코드 조각을 통해 개발 또는 테스트 목적으로 데이터베이스 복사본을 빠르게 만들고 스크립트를 생성 및 실행할 수도 있습니다.

**실행**을 클릭하여 각 셀을 실행합니다.

SQL Server 인스턴스에 연결하기 위한 SQL 커널

![image7](media/sql-notebooks/intellisense-code-cell.png)

쿼리 결과

![image19](media/sql-notebooks/sql-cell-results.png)

PostgreSQL Server 인스턴스에 연결하기 위한 SQL 커널 

![image18](media/sql-notebooks/pgsql-code-cell.png)

쿼리 결과

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Notebook에 대해 Python 구성

커널 드롭다운에서 SQL 이외의 커널을 선택하면 **Notebook에 대해 Python을 구성**하라는 메시지가 표시됩니다. Notebook 종속성은 지정된 위치에 설치되지만, 설치 위치의 설정 여부를 결정할 수 있습니다. 이 설치는 시간이 걸릴 수 있으며, 설치가 완료될 때까지 애플리케이션을 닫지 않는 것이 좋습니다. 설치가 완료되면 지원되는 언어로 코드 작성을 시작할 수 있습니다.

![image21](media/sql-notebooks/configure-python.png)

설치가 성공적으로 완료되면 작업 기록에서 알림을 볼 수 있으며, 출력 터미널에서 실행 중인 Jupyter 백 엔드 서버의 위치를 확인할 수도 있습니다.

![image22](media/sql-notebooks/jupyter-backend.png)

|커널|Description
|:-----|:-----
| SQL 커널 | 관계형 데이터베이스를 대상으로 하는 SQL 코드를 작성합니다.
|PySpark3 및 PySpark 커널| 클러스터의 Spark 컴퓨팅을 사용하여 Python 코드를 작성합니다.
|Spark 커널|클러스터의 Spark 컴퓨팅을 사용하여 Scala 및 R 코드를 작성합니다.
|Python 커널|로컬 개발을 위한 Python 코드를 작성합니다.

`Attach to`는 커널이 연결되는 컨텍스트를 제공합니다. SQL 커널을 사용하는 경우 SQL Server 인스턴스 중 하나를 `Attach to`에 지정할 수 있습니다.

Python3 커널을 사용하는 경우 `Attach to`는 `localhost`입니다. 이 커널을 로컬 Python 개발에 사용할 수 있습니다.

SQL Server 2019 빅 데이터 클러스터에 연결된 경우 기본 `Attach to`는 클러스터의 Spark 컴퓨팅을 사용하여 Python, Scala, R 코드를 제출할 수 있게 해주는 클러스터의 해당 엔드포인트입니다.

### <a name="code-cells-and-markdown-cells"></a>코드 셀 및 markdown 셀

도구 모음에서 **+코드** 명령을 클릭하여 새 코드 셀을 추가합니다.

도구 모음에서 **+텍스트** 명령을 클릭하여 새 텍스트 셀을 추가합니다.

![image8](media/sql-notebooks/notebook-toolbar.png)

셀이 편집 모드로 바뀌고, 이제 markdown을 입력하면서 동시에 미리 보기를 확인할 수 있습니다.

![image9](media/sql-notebooks/notebook-markdown-cell.png)

텍스트 셀 바깥쪽을 클릭하면 markdown 텍스트가 표시됩니다.

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>신뢰할 수 있음 및 신뢰할 수 없음

Azure Data Studio에서 열린 Notebook은 기본적으로 **신뢰할 수 있습니다**.

다른 원본의 Notebook을 여는 경우 **신뢰할 수 없음** 모드로 열린 다음, **신뢰할 수 있음**으로 설정할 수 있습니다.

### <a name="save"></a>저장

**Ctrl+S**를 누르거나, 파일 메뉴에서 **파일 저장**, **다른 이름으로 파일 저장...** 및 **파일 모두 저장l** 명령을 클릭하거나, 명령 팔레트에서 **파일: 저장** 명령을 입력하여 Notebook을 저장할 수 있습니다.

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 커널

`PySpark Kernel`을 선택하고 셀에 다음 코드를 입력합니다.

**실행**을 클릭합니다.

Spark 애플리케이션이 시작되고 다음 출력이 반환됩니다.

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 커널 | Scala 언어

`Spark|Scala Kernel`을 선택하고 셀에 다음 코드를 입력합니다.

![image13](media/sql-notebooks/spark-scala.png)

아래의 옵션 아이콘을 클릭하면 “셀 옵션”을 볼 수도 있습니다.

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 커널 | R 언어

커널 드롭다운에서 Spark | R을 선택합니다. 셀에서 코드를 입력하거나 붙여넣습니다. **실행**을 클릭하여 다음 출력을 확인합니다.

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>로컬 Python 커널

로컬 Python 커널을 선택하고 셀에 다음을 입력합니다.

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>패키지 관리

로컬 Python 개발에 최적화된 작업 중 하나는 고객 시나리오에 필요한 패키지를 설치하는 기능을 포함하는 것이었습니다. 기본적으로 `pandas`, `numpy` 등의 일반적인 패키지를 포함하지만, 포함되지 않은 패키지가 필요한 경우 Notebook 셀에 다음 코드를 작성합니다.

```python
import <package-name>
```

이 명령을 실행하면 `Module not found`가 반환됩니다. 패키지가 있으면 오류가 발생하지 않습니다.

`Module not Found` 오류가 반환되면 **패키지 관리**를 클릭하여 마법사 환경을 시작합니다. 

![image17](media/sql-notebooks/manage-packages.png)

이 마법사에서 **설치된** 패키지를 확인할 수 있습니다. 패키지 목록과 각 패키지의 관련 버전을 검색할 수 있습니다. 패키지를 제거해야 하는 경우 패키지 중 하나를 클릭한 다음, **선택한 패키지 제거** 옵션을 클릭할 수 있습니다.

**새 패키지 추가**를 클릭하여 특정 패키지를 **검색**하고 관련 버전을 선택한 다음, **설치**를 클릭할 수도 있습니다. 기본적으로 검색된 패키지의 최신 버전을 선택합니다.

패키지가 설치되면 Notebook 셀로 이동하여 다음 명령을 입력할 수 있습니다.

```python
import <package-name>
```

패키지를 제거해야 하는 경우 패키지 중 하나 또는 여러 개를 클릭한 다음, **선택한 패키지 제거** 옵션을 클릭할 수 있습니다.

## <a name="next-steps"></a>다음 단계

기존 Notebook을 사용하는 방법에 대한 자세한 내용은 [Azure Data Studio에서 Notebook을 관리하는 방법](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions)을 참조하세요.