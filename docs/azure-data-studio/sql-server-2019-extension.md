---
title: SQL Server 2019 확장 (미리 보기)
titleSuffix: Azure Data Studio
description: Azure Data Studio에 대 한 SQL Server 2019 미리 보기 확장
ms.custom: seodec18
ms.date: 02/13/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c90be7f91c4f3bb465e2cf29b8ee69e2f8d8b6e9
ms.sourcegitcommit: 009bee6f66142c48477849ee03d5177bcc3b6380
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/13/2019
ms.locfileid: "56231060"
---
# <a name="sql-server-2019-extension-preview"></a>SQL Server 2019 확장 (미리 보기)

SQL Server 2019 확장 (미리 보기) 새로운 기능과 도구를 지 원하는 전달에 대 한 미리 보기 지원을 제공 [!INCLUDE[sql-server-2019](../includes/sssqlv15-md.md)]합니다. 에 대 한 미리 보기 지원을 포함 합니다. [SQL Server 2019 빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md), 통합 된 [노트북 환경](../big-data-cluster/notebooks-guidance.md), 및는 PolyBase [Create External Table 마법사](../relational-databases/polybase/data-virtualization.md?toc=%2fsql%2fbig-data-cluster%2ftoc.json)합니다.

## <a name="install-the-sql-server-2019-extension-preview"></a>SQL Server 2019 확장 (미리 보기) 설치

SQL Server 2019 확장 (미리 보기)을 설치 하려면 다운로드 하 고 연결된.vsix 파일을 설치 합니다.

1. SQL Server 2019 확장 (미리 보기).vsix 파일을 로컬 디렉터리로 다운로드:

   |플랫폼|다운로드|릴리스 날짜|버전
   |:---|:---|:---|:---|
   |Windows|[.vsix](https://go.microsoft.com/fwlink/?linkid=2072794)|2019 년 2 월 13 일 |0.10.2
   |macOS|[.vsix](https://go.microsoft.com/fwlink/?linkid=2072793)|2019 년 2 월 13 일 |0.10.2
   |Linux|[.vsix](https://go.microsoft.com/fwlink/?linkid=2072792)|2019 년 2 월 13 일 |0.10.2

1. Azure 데이터 studio **VSIX 패키지에서 확장 설치** 에서 합니다 **파일** 메뉴 및 다운로드 한.vsix 파일을 선택 합니다.

1. 선택할 **예** 나타나면 설치를 확인 하 고 설치 성공 했다는 알림을 기다립니다.

1. 선택 **다시 로드** (처음 확장을 설치 하면 필수)에 확장을 사용 하도록 설정 합니다.

1. 다시 로드 한 후 확장 종속성을 설치 합니다. 출력 창에서 진행률을 볼 수 있습니다 하 고 몇 분 정도 걸릴 수 있습니다.

1. 종속성 후 설치를 완료, Azure Data Studio를 닫았다가 다시 엽니다. 합니다 **SQL Server 빅 데이터 클러스터** 연결 유형을 사용할 수 없는 Azure Data Studio를 다시 시작 해야 합니다.

## <a name="release-notes-v0102"></a>릴리스 정보 (v0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 지원
SQL Server 2019에 대 한 지원이 새로 고쳤습니다. SQL Server 빅 데이터 클러스터에 연결 하는 방법에 새 인스턴스에 _Data Services_ 폴더 탐색기 트리에 표시 됩니다. 이 연결에 대해 새 노트북을 열고 Spark 작업 제출, HDFS 사용 등의 작업에 대 한 시작 지점에 있습니다. 와 같은 일부 작업에 대 한 유의 _외부 데이터 만들기_ HDFS 파일/폴더를 통해 합니다 _SQL Server 2019 Preview_ 확장을 설치 해야 합니다.

### <a name="notebook-support"></a>Notebook 지원
이 릴리스에서 노트북 사용자 인터페이스에 중요 한 업데이트를 했습니다. 이번에 사용자와 공유 되는 전자 필기장 읽기 쉽게 했습니다. 이 셀 주위의 상자 선택, 마우스가 가리키는 경우가 아니면 모든 개요 제거를 위한 쉬운 셀 수준 작업 하지 않고 셀을 선택 해야 할에 대 한 가리킨 항목 지원을 추가 및 애니메이션된 실행 횟수를 추가 하 여 실행 상태를 명확히 _중지실행_ 단추를 더 합니다. 또한 바로 가기 키를 추가 했습니다 _새 노트북_ (`Ctrl+Shift+N`), _실행 셀_ (`F5`), _새 코드 셀_ (`Ctrl+Shift+C`),  _새 텍스트 셀_ (`Ctrl+Shift+T`). 앞에서는 됩니다 것을 목표로 컴파일되는 모든 주요 작업 바로 가기가 보겠습니다 무엇을 하 고 누락 된 알고!

기타 개선 사항 및 수정은 다음과 같습니다.
* 합니다 _SQL Server 2019 Preview_ 확장은 이제 프롬프트 사용 하 여 Python 종속성에 대 한 설치 디렉터리를 선택 합니다. 더 이상 또한에서 Python을 `.vsix file`, 전체 확장 크기를 줄일 합니다. Python 종속성이이 확장을 설치 해야 사용 하 여 Spark 및 Python3 커널은 지원에 필요 합니다.
* 명령줄에서 새 notebook을 실행 하기 위한 지원이 추가 되었습니다. 인수를 사용 하 여 시작 `--command=notebook.command.new --server=myservername` 새 노트북을 열고이 서버에 연결 해야 합니다.
* 노트북 셀에는 대규모 코드 길이에 대 한 성능을 수정 합니다. 코드 셀 250 개 이상의 줄을 추가 하는 스크롤 막대를 갖게 됩니다.
* 향상 된.ipynb 파일을 지원 합니다. 버전 3 이상 이제 지원 됩니다. 파일 저장에 버전으로 업데이트 4 이상 note 하십시오.
* `notebook.enabled` 사용자 설정 되었습니다. 제거 이제는 기본 제공 전자 필기장에서 뷰어는 안정적인
* 이 경우 여러 개체 레이아웃을 수정 높은 대비 테마 지원 이제 됩니다.
* #3680 출력 많은 경우에 따라 표시 되는 위치를 고정 `,,,` 올바르게 문자
* Azure 데이터 studio 외부로 이동한 후 편집기가 사라집니다 셀에 대 한 고정된 # 3602
* 에 대 한 표 뷰를 사용 하도록 지원이 추가 되었습니다는 `application/vnd.dataresource+json` MIME 형식을 출력 합니다. 즉,이 사용 하는 많은 Notebook (설정 하 여 예를 들어 `pd.options.display.html.table_schema` Python notebook에서) 고정 #3959 Azure Data Studio notebook 닫으면 두 번 노트북 서버를 종료 하려고 하는 멋진 테이블 형식 출력 해야 합니다.

#### <a name="known-issues"></a>알려진 문제
* Notebook을 열면 설치 python 대화 상자가 표시 됩니다. 커널 하면이 설치를 취소 하 고 연결 대상 드롭다운 표시 되지 않는 값을 예상 합니다. Python 설치를 완료 하려면이 문제를 해결 합니다.
* 지원 되지 않는 커널을 사용 하 여 notebook을 열면, 커널 및 _연결할_ 드롭다운에는 Azure 데이터 Studio가 중단 하면 됩니다. Azure Data Studio 닫아야 하며, 지원 되는 커널을 사용 해야 합니다 (Python3, Spark | R, Spark | Scala, PySpark, PySpark3)
* Spark UI 링크 PySpark3 또는 SQL Server 끝점에 대해 다른 Spark 커널을 사용 하는 경우 실패 합니다. 문제를 해결 하세요. 대시보드에서 Spark UI에서 클릭 하거나 올바른 Spark UI 하이퍼링크 해야 하는 대로 SQL Server 빅 데이터 클러스터 연결 형식을 사용 하 여 연결

### <a name="extensibility-improvements"></a>확장성 향상
이 릴리스에서 추가 된 다양 한 extender는 데 도움이 되는 향상 된 기능
* 새 `ObjectExplorerNodeProvider` API 확장 SQL Server 또는 기타 연결 노드 아래의 폴더에 적용할 수 있습니다. 이 방법을 `Data Services` 노드 SQL Server 2019 인스턴스 아래에 추가 됩니다 있지만 UI를 쉽게 모니터링 또는 다른 폴더를 추가할 수 있습니다.
* 두 개의 새 상황에 맞는 키 값이 대시보드에 표시/숨기기 기여 하는 데 사용할 수 있습니다.
  * `mssql:iscluster` SQL Server 2019 빅 데이터 클러스터 인지 여부를 나타냅니다.
  * `mssql:servermajorversion` 서버 버전 (SQL Server 2019, SQL Server 2017 등에 대 한 14에 대 한 15)에 있습니다. 이 기능은 요소가 표시 되 면 SQL Server 2017 이상의 경우, 예를 들어 수 있습니다.


## <a name="release-notes-v080"></a>릴리스 정보 (v0.8.0)
*Notebook*:
* 셀 추가 셀 "기타 작업" 셀 단추를 클릭 하면 이제는 전 / 후 기존
* **새 연결 추가** "다른 이름에 연결" 드롭다운 목록에서 연결 옵션이 추가 되었습니다
* A **Notebook 종속성을 다시 설치** Python 패키지 업데이트를 지원 하 고 설치 응용 프로그램을 닫거나 걸리거나 도중에 중단 된 경우 해결에 명령이 추가 되었습니다. 이 명령 팔레트에서 실행할 수 있습니다 (사용 하 여 `Ctrl/Cmd+Shift+P` 형식과 `Reinstall Notebook Dependencies`)
* PROSE python 패키지 1.1.0으로 업데이트 된 버그 수정 포함 하 고 있습니다. 사용 된 **Notebook 종속성을 다시 설치** 이 패키지를 업데이트 하는 명령
* A **출력 지우기** 명령을 클릭 하 여 이제 지원 되는 **기타 작업** 셀 단추
* 다음을 고정 고객 문제를 보고 합니다.
  * Notebook 세션 경로 문제로 인해 Windows에서 시작할 수 없음
  * 예: C:\ 또는 D:\ 드라이브의 루트 폴더에서 notebook은 시작할 수 없습니다.
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) VS Code에서 광고에서 만든 notebook을 편집할 수 없습니다.
  * Spark UI 링크 Spark 커널을 실행 하는 경우 이제 작동
  * "패키지 관리" 이름이 "패키지 설치"

*외부 데이터 만들기*:

* 오류 메시지 복사할 및에 대 한 요약 및 세부 보기도 쉽게 구분 되었습니다.
* 향상 된 UI 레이아웃이 크게 향상 된 안정성 및 오류 처리
* 다음을 고정 고객 문제를 보고 합니다.
  * 잘못 된 열 매핑 사용 하 여 테이블은 사용 안 함으로 표시 되 고 경고에서 오류를 설명 합니다.

## <a name="release-notes-v072"></a>릴리스 정보 (v0.7.2)
* Azure 리소스 탐색기는 이제 Azure Data Studio에 기본 제공 하 고이 확장에서 제거 되었습니다. 이에 대 한 피드백을 주셔서 감사 합니다!
* Markdown 셀 수를 사용 하 여 notebook의 성능이 향상 되었습니다.
* Notebook에서 자동 크기 조정 코드 셀입니다. 셀 도구 모음에 따라 최소 크기를 아직이 있습니다.
* Notebook 종속성을 설치 하는 경우 사용자를 게 알립니다. Windows에서 특히이 걸릴 수 있습니다 시간이 있도록 알림을 이제 작업 보기에 표시 됩니다.
* Notebook 종속성을 다시 설치를 지원 합니다. 사용자 이미 닫혀 Azure Data Studio만 설치 하는 경우에 유용 합니다.
* Notebook 셀 실행 취소를 지원 합니다.
* 외부 데이터 만들기 마법사를 사용 하는 경우 향상 된 안정성, 특히 연결 오류가 발생 한 경우.
* PolyBase 사용 또는 대상 서버에서 실행 되는 경우에 외부 데이터 만들기 마법사의 사용을 차단 합니다.
* 맞춤법 및 SQL Server 2019 및 외부 데이터 만들기와 관련 된 픽스를 명명 합니다.
* Azure Data Studio 디버그 콘솔에서 많은 오류를 제거 합니다.

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

## <a name="polybase-create-external-table-wizard"></a>PolyBase 외부 테이블 마법사 만들기

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
* 실행 합니다 **Notebook 종속성을 다시 설치** 명령 2 개의 태스크가 실패 한 작업 보기를 표시 될 수 있습니다. 설치에 실패 해도이
* 선택 **새 연결 추가** Notebook을 및 취소를 클릭 하면 **연결 선택** 이미 연결 된 경우에 표시 됩니다.