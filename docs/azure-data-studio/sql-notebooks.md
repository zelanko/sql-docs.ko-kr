---
title: Azure Data Studio에서 SQL Notebook을 사용 하는 방법
titleSuffix: Azure Data Studio
description: Azure Data Studio에서 SQL Notebook을 사용 하는 방법 알아보기
ms.custom: seodec18
ms.date: 06/28/2019
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: achatter; alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: jroth
ms.openlocfilehash: 02146596b8c0c21531d269a815f97512b5c955a5
ms.sourcegitcommit: f7ad034f748ebc3e5691a5e4c3eb7490e5cf3ccf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469074"
---
# <a name="how-to-use-notebooks-in-azure-data-studio"></a>Azure Data Studio에서 notebook을 사용 하는 방법

이 문서는 Notebook 환경을 Azure 데이터 Studio에서 시작 하는 방법 및 고유한 전자 필기장 제작을 시작 하는 방법을 설명 합니다. 또한 다른 커널 사용 하 여 Notebook을 작성 하는 방법을 보여 줍니다.


## <a name="connect-to-sql-server"></a>SQL Server에 연결

Azure Data Studio에서 Microsoft SQL Server 연결 형식에 연결할 수 있습니다.
Azure Data Studio 또한 f1을 고 수 클릭 **새 연결** SQL Server에 연결 합니다.

![image1](media/sql-notebooks/connection-info.png)

## <a name="launch-notebooks"></a>Notebook 시작

새 notebook을 시작 하는 방법은 여러 가지입니다.

1. 로 이동 합니다 **파일 메뉴** Azure Data Studio 및 클릭 **새 노트북**합니다.

    ![image3](media/sql-notebooks/file-new-notebook.png)

3. 마우스 오른쪽 단추로 클릭 합니다 **SQL Server** 연결과 시작할 **새 노트북**합니다. 
    ![image3](media/sql-notebooks/server-new-notebook.png)

4. 명령 팔레트를 엽니다 (**Ctrl + Shift + P**))를 입력 하 고 **새 노트북**합니다. 라는 새 파일 `Notebook-1.ipynb` 열립니다.

## <a name="supported-kernels-and-attach-to-context"></a>커널 지원 및 컨텍스트 연결

Azure Data Studio Notebook 설치 SQL 커널을 고유 하 게 지원합니다. SQL 개발자 및 노트북을 사용 하려는 경우 선택한은 커널입니다. 

SQL 커널은 PostgreSQL 서버 인스턴스에 연결 하려면 데도 사용할 수 있습니다. PostgreSQL 개발자가 PostgreSQL 서버에 연결 하려고 하는 경우를 다운로드 합니다 [ **PostgreSQL 확장** ](postgres-extension.md) Azure Data Studio 확장 marketplace에서.

![image7](media/sql-notebooks/sql-kernel-dropdown.png)

### <a name="sql-kernel"></a>SQL 커널

Notebook, 쿼리 편집기에서 유사한 코드 셀에 코딩 환경 일상적인 작업을 더 쉽게 다양 한 SQL 편집기, IntelliSense 및 기본 제공 코드 조각 등의 기본 제공 기능으로는 최신 SQL을 지원 합니다. 코드 조각에는 데이터베이스, 테이블, 뷰, 저장된 프로시저 등을 만들고 기존 데이터베이스 개체를 업데이트 하려면 적절 한 SQL 구문을 생성 할 수 있습니다. 사용 하 여 코드 조각을 신속 하 게 개발 또는 테스트 목적으로 데이터베이스의 복사본을 만들 생성 하 고 스크립트를 실행 합니다.

클릭 **실행** 각 셀을 실행 합니다.

SQL Server 인스턴스에 연결 하려면 SQL 커널

![image7](media/sql-notebooks/intellisense-code-cell.png)

쿼리 결과

![image19](media/sql-notebooks/sql-cell-results.png)

PostgreSQL 서버 인스턴스에 연결 하려면 SQL 커널 

![image18](media/sql-notebooks/pgsql-code-cell.png)

쿼리 결과

![image20](media/sql-notebooks/pgsql-cell-results.png)

### <a name="configure-python-for-notebooks"></a>Notebook에 대 한 Python 구성

커널 드롭다운 목록에서 SQL 외에도 다른 커널도 중 하나를 선택 하면이 묻는 **노트북에 대 한 Python 구성**합니다. 지정된 된 위치에서 Notebook 종속성을 설치 하지만 설치 위치를 설정할지 여부를 결정할 수 있습니다. 이 설치에는 약간의 시간이 걸릴 수 있습니다 하 고 설치가 완료 될 때까지 응용 프로그램을 닫지 않도록 것이 좋습니다. 설치가 완료 되 면 지원 되는 언어로 코드 작성을 시작할 수 있습니다.

![image21](media/sql-notebooks/configure-python.png)

설치에 성공 하면 출력 터미널에서 실행 되는 Jupyter 백 엔드 서버 위치와 함께 작업 기록에서 알림을 확인할 수 있습니다.

![image22](media/sql-notebooks/jupyter-backend.png)

|커널|Description
|:-----|:-----
| SQL 커널 | 관계형 데이터베이스에서 대상으로 하는 SQL 코드를 작성 합니다.
|PySpark3 및 PySpark 커널| 클러스터에서 Spark 계산을 사용 하 여 Python 코드를 작성 합니다.
|Spark 커널|클러스터에서 Spark 계산을 사용 하 여 Scala 및 R 코드를 작성 합니다.
|Python Kernel|로컬 개발에 대 한 Python 코드를 작성 합니다.

`Attach to` 연결할 커널에 대 한 컨텍스트를 제공 합니다. SQL 커널을 사용 하는 경우 있습니다 `Attach to` SQL Server 인스턴스 중 하나입니다.

Python3 커널을 사용할 경우는 `Attach to` 는 `localhost`합니다. 로컬 Python 개발을 위한이 커널을 사용할 수 있습니다.

기본 SQL Server 2019 빅 데이터 클러스터에 연결 되어 있는 경우 `Attach to` 해당 끝점을 사용 하 여 클러스터에 이며 클러스터의 Spark compute를 사용 하 여 Python, Scala 및 R 코드를 제출 하면 됩니다.

### <a name="code-cells-and-markdown-cells"></a>코드 셀 및 Markdown 셀

새 코드 셀을 클릭 하 여 추가 합니다 **+ 코드** 도구 모음에서 명령을 합니다.

새 텍스트 셀을 클릭 하 여 추가 합니다 **+ 텍스트** 도구 모음에서 명령을 합니다.

![image8](media/sql-notebooks/notebook-toolbar.png)

편집 모드에 있고 markdown을 이제 입력 셀 변경 내용을 동시에 미리 보기를 표시 합니다.

![image9](media/sql-notebooks/notebook-markdown-cell.png)

텍스트 셀 바깥쪽을 클릭 하 여 markdown 텍스트를 표시 됩니다.

![image10](media/sql-notebooks/notebook-markdown-preview.png)

### <a name="trusted-and-non-trusted"></a>신뢰할 수 있는 항목과 신뢰할 수 있는 비

Azure Data Studio에서 열기 notebook은 default **신뢰할 수 있는**합니다.

열에 다른 소스에서 Notebook을 열면 **신뢰할 수 없는** 모드 및 다음 수 있도록 **신뢰할 수 있는**합니다.

### <a name="save"></a>저장 

노트북을 저장할 수 있습니다 **Ctrl + S** 누르거나 합니다 **파일 저장**, **다른 이름으로 저장...**  하 고 **모두 파일 저장** 파일 메뉴에서 명령 및 **파일: 저장** 명령 팔레트에서 입력 된 명령입니다.

### <a name="pyspark3pyspark-kernel"></a>Pyspark3/PySpark 커널

선택 된 `PySpark Kernel` 에 다음 코드에서 셀 형식입니다.

**실행**을 클릭합니다.

Spark 응용 프로그램 시작 되 고 다음 출력을 반환 합니다.

![image12](media/sql-notebooks/pyspark.png)

### <a name="spark-kernel--scala-language"></a>Spark 커널은 | Scala 언어

선택 된 `Spark|Scala Kernel` 에 다음 코드에서 셀 형식입니다.

![image13](media/sql-notebooks/spark-scala.png)

아래 – 옵션 아이콘을 클릭할 때에 "셀" 옵션을 볼 수 있습니다.

![image14](media/sql-notebooks/scala-cell-options.png)

### <a name="spark-kernel--r-language"></a>Spark 커널은 | R 언어

Spark를 선택 합니다. | 커널에 대 한 드롭다운 목록에서 R입니다. 셀에서 입력 하거나 코드를 붙여 넣습니다. 클릭 **실행** 다음 출력을 볼 수 있습니다.

![image15](media/sql-notebooks/spark-r.png)

### <a name="local-python-kernel"></a>로컬 Python 커널

로컬 Python 커널 선택 및-셀 형식

![image16](media/sql-notebooks/local-python.png)

## <a name="manage-packages"></a>패키지 관리
로컬 Python 개발에 대 한 액세스에 최적화 된 것 중 하나가 자신의 시나리오에 대 한 고객에 게 해야 하는 패키지를 설치 하는 기능을 포함 하는 것 이었습니다. 기본적으로 같은 공통 패키지가 포함 `pandas`, `numpy` 포함 되지 않은 패키지 notebook 셀에서 다음 코드를 작성 한 다음 예상 되는 경우 있지만 등. 

```python
import <package-name>
```

이 명령을 실행할 때 `Module not found` 반환 됩니다. 다음으로 패키지가 있으면 오류가으로 표시 됩니다.

반환 하는 경우는 `Module not Found` 오류를 클릭 **패키지 관리** 마법사 환경을 시작 합니다. 

![image17](media/sql-notebooks/manage-packages.png)

이 마법사에 표시 됩니다는 **설치 됨** 패키지 있습니다. 목록 및 이러한 각 패키지의 연결 된 버전을 통해 검색할 수 있습니다. 해야 할 경우 **제거할** 패키지 중 하나를 클릭 하 고 클릭 한 다음 이러한 패키지는 **선택한 패키지를 제거** 옵션입니다.

클릭할 수 있습니다 **새로 추가** 패키지 **검색** 특정 패키지에 대 한 관련된 버전을 선택 하 고 클릭 **설치**합니다. 기본적으로 검색 결과 패키지의 최신 버전을 선택 합니다. 

패키지를 설치한 후에 Notebook 셀에서 이동 하 고 다음 명령을 입력 하는 일을 할 해야 합니다.

```python
import <package-name>
```

해야 할 경우 **제거할** 하나 또는 여러 패키지에서를 클릭 하 고 클릭 한 다음 이러한 패키지는 **선택한 패키지를 제거** 옵션입니다.

## <a name="next-steps"></a>다음 단계

기존 노트북을 사용 하는 방법에 알아보려면 참조 [Azure Data Studio에서 notebook을 관리 하는 방법](https://docs.microsoft.com/sql/big-data-cluster/notebooks-how-to-manage?view=sqlallproducts-allversions)합니다.