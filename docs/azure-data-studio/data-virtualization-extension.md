---
title: 데이터 가상화 확장
titleSuffix: Azure Data Studio
description: Azure Data Studio용 데이터 가상화 확장
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: rajmera3
ms.author: raajmera
ms.custom: seodec18
ms.date: 11/04/2019
ms.openlocfilehash: 98a93895b8f552bf7506880a612ab2ae68c48afb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/30/2020
ms.locfileid: "73801127"
---
# <a name="data-virtualization-extension-for-azure-data-studio"></a>Azure Data Studio용 데이터 가상화 확장

Azure Data Studio용 데이터 가상화 확장은 PolyBase [외부 테이블 만들기 마법사](../relational-databases/polybase/data-virtualization.md?toc=/sql/toc/toc.json)를 지원합니다.

## <a name="install-the-data-virtualization-extension"></a>데이터 가상화 확장 설치

데이터 가상화 확장을 설치하려면 Azure Data Studio를 열고 확장 탭에서 다운로드합니다. [여기](extensions.md)의 지침을 따르세요.

## <a name="changes-in-release-10"></a>릴리스 1.0의 변경 내용
* 확장의 이름이 데이터 가상화로 바뀌었습니다.
* 외부 테이블 만들기 마법사:
    * 가상화 MongoDB 및 Teradata 원본용 가이드 Notebooks가 포함되어 있습니다.
    * MongoDB 및 Teradata 가상화 Notebooks에서 변수를 채우는 대화 상자가 추가되었습니다. 

## <a name="changes-in-release-016"></a>릴리스 0.16의 변경 내용
* 외부 테이블 만들기 마법사:
  * 개체 매핑 페이지에서 테이블 및 뷰를 로드할 때 발생하는 오류 처리가 개선되었습니다.

## <a name="changes-in-release-015"></a>릴리스 0.15의 변경 내용
* 외부 테이블 만들기 마법사:
  * 개체 매핑 페이지에서 테이블 및 열 정보를 로드하는 데 걸리는 시간이 단축되었습니다.
  * 연결 정보 페이지에서 기존 데이터베이스 범위 자격 증명을 로드할 때의 버그를 수정했습니다.
* CSV 파일에서 외부 테이블 만들기 마법사:
  * PROSE 구문 분석에 사용되는 기본 샘플 크기가 커졌습니다.

## <a name="changes-in-release-0141"></a>릴리스 0.14.1의 변경 내용
* CTP 3.1 데이터 원본 지원

## <a name="changes-in-release-0121"></a>릴리스 0.12.1의 변경 내용

* 이 릴리스에서는 **SQL Server 빅 데이터 클러스터** 연결 형식이 제거되었습니다. SQL Server 빅 데이터 클러스터 연결에서 이전에 사용할 수 있던 모든 기능을 이제 SQL Server 연결에서 사용할 수 있습니다.
* HDFS 검색은 **Data Services** 폴더 아래에서 찾을 수 있습니다.
* Notebook의 경우 PySpark 및 기타 빅 데이터 커널은 SQL Server 빅 데이터 클러스터의 SQL Server 마스터 인스턴스에 연결될 때 작동합니다.
* 외부 테이블 만들기 마법사:
  * 기존 외부 데이터 원본을 사용하여 외부 테이블을 만들 수 있도록 지원합니다.
  * 마법사 전체에서 성능이 향상되었습니다.
  * 특수 문자를 포함하는 개체 이름의 처리가 개선되었습니다. 이러한 개체 이름으로 인해 마법사가 실패하는 경우가 있었습니다.
  * 개체 매핑 페이지의 안정성이 개선되었습니다.
  * 데이터베이스 드롭다운에서 'DWConfiguration', 'Dwconfiguration', 'Dwconfiguration' 등의 시스템 데이터베이스가 제거되었습니다.
  * **CSV 파일에서 외부 테이블 만들기** 마법사에서 외부 파일 형식 개체의 이름을 설정할 수 있도록 지원합니다.
  * **CSV 파일에서 외부 테이블 만들기** 마법사의 첫 번째 페이지에 새로 고침 단추를 추가했습니다.

## <a name="release-notes-v0110"></a>릴리스 정보(v0.11.0)

* Jupyter Notebook 지원, 특히 Python3 및 Spark 커널 지원이 Azure Data Studio으로 이동되었습니다. 이 확장은 더 이상 Notebook을 사용하는 데 필요하지 않습니다.
* 외부 데이터 마법사의 여러 버그 수정:
  * Oracle 형식 매핑이 SQL Server 2019 CTP 2.3에서 제공되는 변경 내용에 맞게 업데이트되었습니다.
  * 테이블 매핑 컨트롤에 입력한 새 스키마가 손실되는 문제가 해결되었습니다.
  * 테이블 매핑의 데이터베이스 노드를 확인할 때 모든 테이블과 뷰가 확인되지는 않는 문제가 해결되었습니다.


## <a name="release-notes-v0102"></a>릴리스 정보(v0.10.2)
### <a name="sql-server-2019-support"></a>SQL Server 2019 지원
SQL Server 2019에 대한 지원이 업데이트되었습니다. SQL Server 빅 데이터 클러스터 인스턴스에 연결하면 탐색기 트리에 새 _Data Services_ 폴더가 나타납니다. 이 폴더에는 연결에 대해 새 Notebook 열기, Spark 작업 제출, HDFS 사용 등의 작업을 위한 시작 지점이 있습니다. HDFS 파일/폴더에 대한 _외부 데이터 만들기_ 등의 일부 작업을 수행하려면 _SQL Server 2019_ 확장을 설치해야 합니다.

### <a name="notebook-support"></a>Notebook 지원
이 릴리스에서는 Notebook 사용자 인터페이스의 중요한 기능이 업데이트되었습니다. 이러한 업데이트는 사용자와 공유하는 Notebook을 쉽게 읽을 수 있도록 하는 데 중점을 두고 진행되었습니다. 즉, 선택하거나 가리키지 않으면 셀 주변의 모든 개요 상자가 제거되고, 셀을 선택하지 않고도 쉬운 셀 수준 작업을 수행하기 위한 가리키기 지원이 추가되고, 실행 횟수, 애니메이션 _실행 중지_ 단추 등을 추가하여 실행 상태를 명확히 나타냅니다. 또한 _새 Notebook_(`Ctrl+Shift+N`), _셀 실행_(`F5`), _새 코드 셀_(`Ctrl+Shift+C`), _새 텍스트 셀_(`Ctrl+Shift+T`)의 바로 가기 키도 추가했습니다. 앞으로 모든 주요 작업을 바로 가기로 실행할 수 있도록 할 예정이므로 놓치기 쉬운 작업이 있으면 알려주세요.

기타 개선 사항 및 수정 내용은 다음과 같습니다.
* 이제 _SQL Server 2019_ 확장에서 Python 종속성의 설치 디렉터리를 선택하라는 메시지를 사용자에게 표시합니다. 또한 `.vsix file`에 더 이상 Python이 포함되지 않으므로 전반적인 확장 크기가 줄어듭니다. Python 종속성은 Spark 및 Python3 커널을 지원합니다.
* 명령줄에서 새 Notebook을 시작할 수 있는 지원이 추가되었습니다. 인수 `--command=notebook.command.new --server=myservername`을 사용하여 시작하면 새 Notebook이 열리고 이 서버에 연결됩니다.
* 셀에 길이가 긴 코드가 포함된 Notebook의 성능이 수정되었습니다. 코드 셀이 250줄을 초과하면 스크롤 막대가 추가됩니다.
* .ipynb 파일 지원이 개선되었습니다. 이제 버전 3 이상이 지원됩니다. 저장 시 파일이 버전 4 이상으로 업데이트됩니다.
* 기본 제공 노트북 뷰어가 안정화되었으므로 `notebook.enabled` 사용자 설정이 제거되었습니다.
* 이 경우 개체 레이아웃의 다양한 수정을 통해 고대비 테마가 지원됩니다.
* 출력에 많은 `,,,` 문자가 잘못 표시되는 #3680 문제가 해결되었습니다.
* Azure Data Studio 밖으로 이동한 후 셀 편집기가 사라지는 #3602 문제가 해결되었습니다.
* `application/vnd.dataresource+json` 출력 MIME 형식에 대한 그리드 보기를 사용하도록 지원이 추가되었습니다. 즉, 이 보기를 사용하는 많은 Notebook(예: Python Notebook에서 `pd.options.display.html.table_schema` 설정)은 보다 나은 테이블 형식 출력을 표시합니다. Azure Data Studio가 Notebook을 닫은 후에 Notebook 서버를 두 번 종료하려고 하는 #3959 문제를 해결했습니다.

#### <a name="known-issues"></a>알려진 문제
* Notebook을 열면 python 설치 대화 상자가 표시됩니다. 이 설치를 취소하면 커널 및 연결 대상 드롭다운에 예상되는 값이 표시되지 않습니다. 해결 방법은 Python 설치를 완료하는 것입니다.
* 지원되지 않는 커널을 사용하여 Notebook을 열면 커널 및 _연결 대상_ 드롭다운에서 Azure Data Studio가 더 이상 응답하지 않습니다. Azure Data Studio를 닫고 지원되는 커널을 사용하고 있는지 확인해야 합니다(Python3, Spark | R, Spark | Scala, PySpark, PySpark3).
* SQL Server 엔드포인트에 대해 PySpark3 또는 기타 Spark 커널을 사용하는 경우 Spark UI 링크가 실패합니다. 해결 방법으로 대시보드에서 Spark UI를 클릭하거나 SQL Server 빅 데이터 클러스터 연결 유형을 사용하여 연결합니다. 이 연결 유형은 올바른 Spark UI 하이퍼링크를 사용합니다.

### <a name="extensibility-improvements"></a>확장성 향상
Extender를 지원하는 다양한 개선 기능이 이 릴리스에 추가되었습니다.
* 새 `ObjectExplorerNodeProvider` API를 사용하면 확장을 통해 SQL Server 또는 다른 연결 노드 아래에 폴더가 배치될 수 있습니다. `Data Services` 노드는 이러한 방식으로 SQL Server 2019 인스턴스 아래에 추가되지만, 모니터링 또는 기타 폴더를 UI에 쉽게 추가하는 데 이 API를 사용할 수 있습니다.
* 대시보드에 기여를 표시하거나 숨기는 데 사용할 수 있는 두 가지 새로운 컨텍스트 키 값이 제공됩니다.
  * `mssql:iscluster`는 SQL Server 2019 빅 데이터 클러스터 인지 여부를 나타냅니다.
  * `mssql:servermajorversion`에는 서버 버전(SQL Server 2019의 경우 15, SQL Server 2017의 경우 14 등)이 표시됩니다. 이 값은 예를 들어, SQL Server 2017 이상에 대해서만 기능을 표시해야 하는 경우에 유용할 수 있습니다.


## <a name="release-notes-v080"></a>릴리스 정보(v0.8.0)
*Notebook*:
* 이제 "추가 작업" 셀 단추를 클릭하여 기존 셀 앞/뒤에 셀을 추가할 수 있습니다.
* "연결 대상" 드롭다운의 연결에 **새 연결 추가** 옵션이 추가되었습니다.
* **Notebook 종속성 다시 설치** 명령은 Python 패키지 업데이트를 지원하고, 애플리케이션을 닫아 설치가 중단되는 경우를 해결하기 위해 추가되었습니다. 이 명령은 명령 팔레트에서 실행할 수 있습니다(`Ctrl/Cmd+Shift+P`를 사용하고 `Reinstall Notebook Dependencies` 입력).
* PROSE python 패키지는 1.1.0으로 업데이트되었으며 많은 버그 수정이 포함되어 있습니다. 이 패키지를 업데이트하려면 **Notebook 종속성 다시 설치** 명령을 사용합니다.
* 이제 **추가 작업** 셀 단추를 클릭하여 **출력 지우기** 명령을 수행할 수 있습니다.
* 고객이 보고한 다음 문제를 수정했습니다.
  * 경로 문제로 인해 Windows에서 Notebook 세션을 시작할 수 없습니다.
  * 드라이브의 루트 폴더(예: C:\ 또는 D:\)에서 Notebook을 시작할 수 없습니다.
  * [#2820](https://github.com/Microsoft/azuredatastudio/issues/2820) ADS에서 만든 Notebook을 VS Code에서 편집할 수 없습니다.
  * Spark UI 링크는 이제 Spark 커널을 실행할 때 작동합니다.
  * "관리형 패키지"가 "패키지 설치"로 바뀌었습니다.

*외부 데이터 만들기*:

* 오류 메시지는 복사 가능하며 더 쉽게 볼 수 있게 요약 및 상세 보기로 분리되었습니다.
* UI 레이아웃이 향상되고 안정성 및 오류 처리가 크게 개선되었습니다.
* 고객이 보고한 다음 문제를 수정했습니다.
  * 열 매핑이 잘못된 테이블은 사용 안 함으로 표시되고 경고에 오류 설명이 표시됩니다.

## <a name="release-notes-v072"></a>릴리스 정보(v0.7.2)
* Azure Resource Explorer는 이제 Azure Data Studio에 기본적으로 제공되며 이 확장에서 제거되었습니다. 피드백을 주셔서 감사합니다.
* 많은 Markdown 셀이 있는 Notebook의 성능이 개선되었습니다.
* Notebook에서 코드 셀 크기를 자동으로 조정합니다. 최소 크기는 여전히 셀 도구 모음을 기준으로 합니다.
* Notebook 종속성을 설치할 때 사용자에게 알립니다. 특히 Windows에서 이 작업은 시간이 오래 걸릴 수 있으므로 이제 작업 보기에 알림이 표시됩니다.
* Notebook 종속성을 다시 설치할 수 있습니다. 이러한 기능은 이전에 사용자가 설치 도중에 Azure Data Studio를 닫은 경우에 유용합니다.
* Notebook에서 셀 실행을 취소할 수 있습니다.
* 특히, 연결 오류가 발생할 때 외부 데이터 만들기 마법사를 사용할 경우의 안정성이 향상되었습니다.
* 대상 서버에서 PolyBase를 사용하도록 설정하지 않았거나 실행하고 있지 않은 경우에는 외부 데이터 만들기 마법사의 사용을 차단합니다.
* SQL Server 2019 및 외부 데이터 만들기와 관련해서 철자 및 이름이 수정되었습니다.
* Azure Data Studio 디버그 콘솔에서 다수의 오류가 제거되었습니다.
