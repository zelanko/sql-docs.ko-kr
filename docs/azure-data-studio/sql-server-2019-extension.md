---
title: Azure 데이터 Studio SQL Server 2019 확장 (미리 보기) | Microsoft Docs
description: Azure Data Studio에 대 한 SQL Server 2019 미리 보기 확장
ms.custom: tools|sos
ms.date: 10/11/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: d73f4a0d55cbe3fe3bacc0b2bb68f191046fe01b
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/12/2018
ms.locfileid: "49168802"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 확장 (미리 보기)

SQL Server 2019 확장 (미리 보기) 새로운 기능과 도구를 지 원하는 전달에 대 한 미리 보기 지원 제공 [!INCLUDE [sql-server-2019](..\includes\sssqlv15-md.md)]합니다. 에 대 한 미리 보기 지원을 포함 합니다. [SQL Server 2019 빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md), 통합 된 [노트 환경과](../big-data-cluster/notebooks-guidance.md)를 PolyBase [Create External Table 마법사](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json), 및 [Azure 리소스 탐색기](azure-resource-explorer.md)합니다.

## <a name="install-the-sql-server-2019-extension-preview"></a>SQL Server 2019 확장 (미리 보기) 설치

SQL Server 2019 확장 (미리 보기)을 설치 하려면 다운로드 하 고 연결된.vsix 파일을 설치 합니다.

1. SQL Server 2019 확장 (미리 보기).vsix 파일을 로컬 디렉터리로 다운로드:

   |플랫폼|다운로드|릴리스 날짜|
   |:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024911)|2018 년 9 월 24 일|
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024587)|2018 년 9 월 24 일 |
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2024841)|2018 년 9 월 24 일 |

1. Azure 데이터 studio **VSIX 패키지에서 확장 설치** 에서 합니다 **파일** 메뉴 및 다운로드 한.vsix 파일을 선택 합니다.

1. 선택할 **예** 나타나면 설치를 확인 하 고 설치 성공 했다는 알림을 기다립니다.

1. 선택 **다시 로드** (처음 확장을 설치 하면 필수)에 확장을 사용 하도록 설정 합니다.

1. 다시 로드 한 후 확장 종속성을 설치 합니다. 출력 창에서 진행률을 볼 수 있습니다 하 고 몇 분 정도 걸릴 수 있습니다.

##  <a name="sql-server-2019-big-data-cluster-support"></a>SQL Server 2019 빅 데이터 클러스터 지원

* 클릭 **연결 추가** 에 *개체 탐색기* 선택한 **SQL Server 빅 데이터 클러스터** 연결 유형으로 합니다.

   > [!TIP]
   > 표시 되지 않으면 합니다 **SQL Server 빅 데이터 클러스터** 연결 형식으로 Azure 데이터 Studio 다시 시작 합니다.

* 호스트 이름 또는 IP 주소 클러스터 끝점 및 사용자 이름 및 연결 하는 데 사용 되는 암호를 입력 합니다.
* 필요에 따라에 친숙 한 표시 이름을 포함 합니다 **이름을** 필드입니다.
* 클릭 **Connect** 일반적인 작업을 시작할 수 있습니다 및 대시보드에서 찾아보기 **HDFS** 개체 탐색기 및 여기에서 상황에 맞는 작업을 실행된 합니다.
* 클러스터에 대해 Spark 작업을 제출 하려면 마우스 오른쪽 단추로 클릭에서 서버 노드 *개체 탐색기* 선택한 **Spark 작업 제출** 제출 대화 상자를 표시 합니다.
* Notebook을 열려면 다음 섹션을 참조 합니다.

자세한 내용은 참조 하세요 [빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md)합니다.


## <a name="azure-data-studio-notebooks"></a>Azure Data Studio Notebook

* 다음 방법 중 하나에서 notebook을 엽니다.
  * 새 notebook을 엽니다는 *명령 팔레트*합니다.
  * SQL Server 2019 빅 데이터 클러스터 중 하나를 HDFS 개체 탐색기 트리를 엽니다.
    * 해당 서버 노드를 마우스 오른쪽 단추로 클릭 하 고 선택 **새 Jupyter 노트북**합니다.
    * CSV 파일을 마우스 오른쪽 단추로 클릭 하 고 선택 **Notebook에서 분석**합니다.
  * 기존.ipynb 파일을 엽니다는 **파일** 메뉴 또는 파일 탐색기 *(.ipynb 파일 올바르게 로드 4 이상 버전으로 업그레이드 해야 합니다)*
* 커널을 선택 합니다. 로컬 전자 필기장 실행을 위한 Python 3를 선택 합니다. 원격 실행을 위해 PySpark 또는 Spark 선택 | Scala 합니다.
* 원격으로 실행 하는 경우 연결할 SQL Server 빅 데이터 클러스터 끝점을 선택 (필요 없는 Python 3를 사용 하 여 로컬 개발에 대 한).
* Notebook 헤더의 단추를 통해 코드 또는 markdown 셀을 추가 합니다. 각 셀의 왼쪽에 휴지통 아이콘을 사용 하 여 셀을 제거 합니다.
* 코드 셀에 대 한 재생 단추를 사용 하 여 셀을 실행 하 고 markdown 편집 간을 전환 눈 모양 아이콘을 사용 하 여 미리 보기


## <a name="azure-resource-explorer"></a>Azure 리소스 탐색기

* Azure에 로그인 하려면 Azure Data Studio의 왼쪽 아래에서에서 사용자 아이콘을 클릭 하 고 대화 상자를 Azure에 로그인을 수행 합니다.
* 로그인 한 후 삼각가 중 Azure 아이콘의 왼쪽된 막대의 Azure 데이터 Studio를 클릭 하 고 구독과 연결 된 SQL 리소스를 표시할 트리를 확장 합니다.
* 마우스 오른쪽 단추로 클릭 하거나 연결 대화 상자를 열려면 SQL Server 나 SQL database에 있는 플러그 아이콘을 클릭 합니다. 연결 리소스는 Azure 데이터 Studio 개체 탐색기를 추가 하 여 암호를 입력 합니다.

자세한 내용은 참조 하세요 [Azure Resource Explorer](azure-resource-explorer.md)합니다.


## <a name="polybase-create-external-table-wizard"></a>Polybase 외부 테이블 마법사 만들기

* SQL Server 2019 인스턴스에서 *외부 테이블 만들기 마법사* 세 가지 방법으로 열 수 있습니다.
  * 서버를 마우스 오른쪽 단추로 클릭, 선택 **관리**SQL Server 2019 (미리 보기)에 대 한 탭을 클릭 하 고 선택 **Create External Table**합니다.
  * 선택한 SQL Server 2019 인스턴스와 *개체 탐색기*, 불러옵니다 *외부 만들기 마법사* 를 통해 합니다 *명령 팔레트*합니다.
  * SQL Server 2019 데이터베이스를 마우스 오른쪽 단추로 클릭 *개체 탐색기* 선택한 **Create External Table**합니다.
* 확장의이 버전에서는 원격 SQL Server 및 Oracle 테이블에 액세스 하려면 외부 테이블을 만들 수 있습니다.

  > [!NOTE]
  > 외부 테이블 기능을 SQL 2019 기능 이지만, 원격 SQL Server 이전 버전의 SQL Server를 실행할 수 있습니다.

* 마법사의 첫 번째 페이지에서 SQL Server 또는 Oracle 액세스 하 고 계속 있는지 여부를 선택 합니다.
* 하나 아직 만들어지지 않은 경우 데이터베이스 마스터 키를 만들려면 나타납니다 (암호 복잡성이 부족 하 여 차단).
* 데이터 원본 연결을 만들고 원격 서버에 대 한 자격 증명 이름이 있습니다.
* 새 외부 테이블에 매핑할 개체를 선택 합니다.
* 선택 **스크립트 생성** 하거나 **만들기** 마법사를 마칩니다.
* 외부 테이블을 만든 후 즉시 나타나는 데이터베이스의 개체 트리 생성 된 것입니다.


## <a name="known-issues"></a>알려진 문제

* 연결을 만들 때 암호를 저장 하지 않으면, Spark 작업을 제출 하는 등 일부 작업이 실패할 수 있습니다.
* 기존.ipynb notebook 뷰어에 내용을 로드할 4 이상 버전으로 업그레이드 해야 합니다.
