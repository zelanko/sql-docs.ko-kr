---
title: Azure Data Studio 릴리스 정보
description: 이 문서에는 2017년 11월부터 현재까지의 Azure Data Studio 릴리스에 대한 릴리스 정보가 안내되어 있습니다. 요약된 문제 중 다수에 추가 세부 정보로 연결되는 링크가 있습니다.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.reviewer: maghan
ms.custom: seodec18
ms.date: 12/9/2020
ms.openlocfilehash: cd990278d7478c089df7b01fa4a3738ad36368c3
ms.sourcegitcommit: d983ad60779d90bb1c89a34d7b3d6da18447fdd8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/09/2020
ms.locfileid: "96933849"
---
# <a name="release-notes-for-azure-data-studio"></a>Azure Data Studio의 릴리스 정보

**[최신 릴리스 다운로드 및 설치](./download-azure-data-studio.md)**

## <a name="december-2020"></a>2020년 12월

2020년 12월 9일 &nbsp; / &nbsp; 버전: 1.25.0

&nbsp;

| 변경 | 세부 정보 |
| ------ | ------- |
| 버그 수정 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%22December+2020+Release%22)를 참조하세요. |
| 데이터베이스 프로젝트 확장 업데이트 | 작업 영역 추가 및 사이드바 개선 |

## <a name="november-2020"></a>2020년 11월

2020년 11월 12일 &nbsp; / &nbsp; 버전: 1.24.0

&nbsp;

| 변경 | 세부 정보 |
| ------ | ------- |
| 버그 수정 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22November+2020+Release%22+is%3Aclosed)를 참조하세요. |
| 연결 대화 상자 | 연결 대화 상자에 새 찾아보기 탭이 추가되었습니다. |
| 확장 업데이트 | Postgres 확장 업데이트를 릴리스했습니다. |
| 새로운 Notebook 기능 | Notebook 지원에 SQL의 새로운 기능이 추가되었습니다. <br/> Notebook 매개 변수화 지원에 새로운 기능이 추가되었습니다. <br/>  SQL Notebooks의 결과 스트리밍에 새로운 기능이 추가되었습니다. |
| Python 설치 | 기본 Python 설치에서 PROSE 패키지가 제거되었습니다. |

### <a name="known-issues-1240"></a>알려진 문제(1.24.0)

| 새 항목 | 세부 정보 | 해결 방법 |
|----------|---------|------------|
| Azure Arc 확장 | [알려진 문제:](https://github.com/microsoft/azuredatastudio/issues/13319) Arc MIAA 및 PG 배포를 위한 "Notebook으로 스크립트" 단추는 Notebook으로 스크립팅 전에 필드 유효성 검사를 수행하지 않습니다. 즉, 사용자가 암호 확인 입력에 잘못된 암호를 입력할 경우 잘못된 암호 값을 가진 Notebook이 생깁니다.| 사용자가 대신 사용해야 하는 "배포" 단추는 예상대로 작동합니다. |
| 개체 탐색기 | 1\.24.0 이전의 ADS 릴리스에는 [Azure Synapse Analytics 서버리스 SQL 풀](https://docs.microsoft.com/azure/synapse-analytics/sql/on-demand-workspace-overview)과 관련된 엔진 변경으로 인해 개체 탐색기에 호환성이 손상되는 변경이 있습니다. | Azure Synapse Analytics 서버리스 SQL 풀이 있는 Azure Data Studio에서 개체 탐색기를 계속 활용하려면 Azure Data Studio 1.24.0 이상을 사용해야 합니다. |

다른 알려진 문제를 확인하고 제품 팀에 피드백을 제공하려면 [Azure Data Studio 피드백](https://github.com/microsoft/azuredatastudio)을 참조할 수 있습니다.

## <a name="october-2020"></a>2020년 10월

2020년 10월 14일 &nbsp; / &nbsp; 버전: 1.23.0

&nbsp;

| 변경 | 세부 정보 |
| ------ | ------- |
| Azure SQL Edge | Azure SQL Edge 개체를 지원합니다. |
| 버그 수정 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is:issue+milestone:%22October+2020+Release%22+is:closed)를 참조하세요. |
| 데이터베이스| 동일한 데이터베이스 참조를 지원합니다. |
| 확장 업데이트 | [Azure Arc](extensions/azure-arc-extension.md)</br>[azdata](../azdata/install/deploy-install-azdata.md)</br>[Machine Learning](extensions/machine-learning-extension.md)</br>[Kusto(KQL)](extensions/kusto-extension.md)</br>[스키마 비교](extensions/schema-compare-extension.md)</br>SQL 평가</br>[SQL Database 프로젝트](extensions/sql-database-project-extension.md)</br>[SQL Server 가져오기](extensions/sql-server-import-extension.md) |
| 새 배포 기능 | Azure SQL DB 및 VM 배포가 추가되었습니다. |
| PowerShell | PowerShell 커널 결과 스트리밍 지원이 추가되었습니다. |

## <a name="september-2020-hotfix"></a>2020년 9월(핫픽스)

2020년 9월 30일 &nbsp; / &nbsp; 버전: 1.22.1

&nbsp;

| 변경 | 세부 정보 |
| ------ | ------- |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/releases/tag/1.22.1)를 참조하세요. |

## <a name="september-2020"></a>2020년 9월

2020년 9월 22일 &nbsp; / &nbsp; 버전: 1.22.0

&nbsp;

| 변경 | 세부 정보 |
| ------ | ------- |
| 새로운 Notebook 기능 | <br/> &bull; &nbsp; 다양한 텍스트 서식 및 markdown으로의 원활한 변환을 기반으로 하며 WYSIWYG(What You See Is What You Get) 도구 모음이라고도 하는 새로운 텍스트 셀 편집 환경을 지원합니다. <br/> &bull; &nbsp; Kusto 커널을 지원합니다. <br/> &bull; &nbsp; Notebook 고정을 지원합니다. <br/> &bull; &nbsp; 새 버전의 Jupyter Book 지원을 추가했습니다. <br/> &bull; &nbsp; Jupyter 바로 가기를 개선했습니다. <br/> &bull; &nbsp; 로드 성능 개선 사항을 도입했습니다. |
| SQL Database Projects 확장 | SQL Database Projects 확장은 프로젝트 기반 데이터베이스 개발을 Azure Data Studio로 가져옵니다. 이 미리 보기 릴리스에서는 Azure Data Studio를 통해 SQL 프로젝트를 만들고 게시할 수 있습니다. |
| Kusto(KQL) 확장 | Azure Data Explorer에 저장된 대량 실시간 스트리밍 데이터에 대한 데이터 탐색 및 데이터 분석을 위해 Azure Data Studio에 기본 Kusto 환경을 구현합니다. 이 미리 보기 릴리스에서는 Azure Data Explorer 클러스터를 연결하고 찾아볼 수 있을 뿐 아니라 KQL 쿼리를 작성하고 Kusto 커널을 사용하여 Notebook을 작성할 수 있습니다. |
| Azure Arc 확장 | 사용자는 Azure Data Studio를 통해 Azure Arc 퍼블릭 미리 보기를 사용해 볼 수 있습니다. 다음 내용이 포함됩니다. <br/> &bull; &nbsp; 데이터 컨트롤러 배포 <br/> &bull; &nbsp; Postgres 배포 <br/> &bull; &nbsp; Azure Arc용 Managed Instance 배포 <br/> &bull; &nbsp; 데이터 컨트롤러에 연결 <br/> &bull; &nbsp; 데이터 서비스 대시보드 액세스 <br/> &bull; &nbsp; Azure Arc Jupyter Book |
| 배포 옵션 | <br/> &bull; &nbsp; Azure SQL Database Edge <br/> (Edge를 사용하려면 Azure SQL Edge 배포 확장이 필요함) |
| SQL Server 가져오기 확장 GA(일반 공급) | SQL Server 가져오기 확장의 GA와 더 이상 미리 보기로 제공되지 않는 기능을 발표합니다. 이 확장을 통해 csv/txt 파일을 쉽게 가져올 수 있습니다. [관련 문서](./extensions/sql-server-import-extension.md)에서 확장에 대해 자세히 알아보세요. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22September+2020+Release%22+is%3Aclosed)를 참조하세요. |

## <a name="august-2020"></a>2020년 8월

2020년 8월 12일 &nbsp; / &nbsp; 버전: 1.21.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 새로운 Notebook 기능 | &bull; &nbsp; 셀 위치 이동 <br/> &bull; &nbsp; 셀을 텍스트 셀 또는 코드 셀로 변환
| Jupyter Book 선택기 | 이제 사용자가 GitHub 릴리스의 Jupyter Book을 선택하여 Azure Data Studio에서 원활하게 열 수 있습니다. |
| Notebook 뷰렛에 검색 추가 | 사용자가 해당 Notebook 및 Jupyter Book에서 콘텐츠를 쉽게 검색할 수 있습니다. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22August+2020+Release%22+is%3Aclosed)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="july-2020-hotfix"></a>2020년 7월(핫픽스)

2020년 7월 17일 &nbsp; / &nbsp; 버전: 1.20.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 수정됨: 버그 #11372 개체 탐색기 끌어서 놓기 테이블이 테이블 이름을 잘못 래핑함 | [#11372](https://github.com/microsoft/azuredatastudio/issues/11372) |
| 수정됨: 버그 #11356 이제 어두운 테마가 기본 테마임 | [#11356](https://github.com/microsoft/azuredatastudio/issues/11356) |
| &nbsp; | &nbsp; |

### <a name="known-issue"></a>알려진 문제

- 일부 사용자가 이번 릴리스에 포함된 새로운 Microsoft.Data.SqlClient v2.0.0에서 연결 오류를 보고했습니다. [이 지침을 따르면](https://github.com/microsoft/azuredatastudio/issues/11367#issuecomment-659614111) 연결을 성공적으로 수행할 수 있습니다.

## <a name="july-2020"></a>2020년 7월

2020년 7월 15일 &nbsp; / &nbsp; 버전: 1.20.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 새로운 기능 둘러보기가 추가됨 | 이제 사용자는 환영 페이지 및 명령 팔레트에서 기능 둘러보기를 시작하여 연결 뷰렛, Notebook 뷰렛, 확장 Marketplace 등 일반적으로 사용되는 기능을 둘러볼 수 있습니다. |
| 새로운 Notebook 기능 | &bull; &nbsp; Markdown 도구 모음의 헤더 지원<br/> &bull; &nbsp; 텍스트 셀의 병렬 Markdown 미리 보기
| 쿼리 편집기에서 열 및 테이블 끌어서 놓기 | 이제 사용자는 연결 뷰렛에서 쿼리 편집기로 열과 테이블을 직접 끌어서 놓을 수 있습니다. |
| 작업 막대에 Azure 계정 아이콘이 추가됨 | 이제 사용자가 Azure에 로그인하는 위치를 쉽게 확인할 수 있습니다. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22July+2020+Release%22+is%3Aclosed)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="june-2020"></a>2020년 6월

2020년 6월 15일 &nbsp; / &nbsp; 버전: 1.19.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| Azure Portal 통합에 Azure Data Studio가 추가됨 | 이제 사용자는 Azure SQL Database 연결과 Azure Postgres 등에서 Azure Portal을 바로 열 수 있습니다. |
| 새로운 Notebook 기능 | &bull; &nbsp; 새로운 Notebook 도구 모음 <br/> &bull; &nbsp; 새로운 셀 편집 도구 모음 <br/> &bull; &nbsp; Python 종속성 마법사 UX 업데이트 <br/> &bull; &nbsp; Notebook에서의 간격 개선 |
| SQL 평가 API 확장 발표 | 이 확장은 ADS에 SQL Server 모범 사례 평가를 추가합니다. 이전에는 PowerShell SqlServer 모듈과 SMO에서만 사용할 수 있었던 SQL 평가 API를 노출하여 사용자가 SQL Server 인스턴스를 평가하고 SQL Server 팀의 추천을 받을 수 있게 합니다. SQL 평가 API와 관련 기능에 관한 자세한 내용은 [이 문서를 참조하세요.](../tools/sql-assessment-api/sql-assessment-api-overview.md) |
| [Machine Learning 확장 개선](./extensions/machine-learning-extension.md) | 이제 Azure SQL Managed Instance를 지원합니다. |
| 데이터 가상화 확장 개선 | 이제 MongoDB 및 Teradata를 지원합니다. |
| Postgres 확장 버그 수정 | Azure MFA를 수정했습니다. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2020+Release%22+is%3Aclosed)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="may-2020-hotfix"></a>2020년 5월(핫픽스)

2020년 5월 27일 &nbsp; / &nbsp; 버전: 1.18.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| “현재 쿼리 실행” 키바인드가 정상적으로 작동하지 않는 버그 #10538 수정 | [#10538](https://github.com/microsoft/azuredatastudio/issues/10538)  |
| v1.18에서 신규 또는 기존 sql 파일을 열 수 없는 #10537 버그 수정 | [#10537](https://github.com/microsoft/azuredatastudio/issues/10537)  |
| &nbsp; | &nbsp; |

## <a name="may-2020"></a>2020년 5월

2020년 5월 20일 &nbsp; / &nbsp; 버전: 1.18.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| Redgate SQL 프롬프트 확장 발표 | 이 확장을 사용하면 Azure Data Studio 내에서 직접 서식 스타일을 관리할 수 있으므로 IDE에서 나가지 않고 스타일을 만들고 편집할 수 있습니다. |
| Machine Learning 확장 발표 | 이 확장을 이용하면 다음 작업을 할 수 있습니다. <br/> &bull; &nbsp; Azure Data Studio에서 SQL Server 기계 학습 서비스를 사용하여 Python 및 R 패키지를 관리합니다.<br/> &bull; &nbsp; ONNX 모델을 사용하여 Azure SQL Edge에서 예측을 수행합니다.<br/> &bull; &nbsp; Azure SQL Edge 데이터베이스에서 ONNX 모델을 확인합니다. <br/> &bull; &nbsp; 파일이나 Azure Machine Learning에서 ONNX 모델을 Azure SQL Edge 데이터베이스로 가져옵니다. <br/> &bull; &nbsp; 실험을 실행할 Notebook을 만듭니다. |
| 새로운 Notebook 기능 | &bull; &nbsp; Python 종속성을 쉽게 설치할 수 있도록 새로운 Python 종속성 마법사 추가 <br/> &bull; &nbsp; Markdown 도구 모음에 밑줄 지원 추가 |
| Always Encrypted에 대한 매개 변수화 | 암호화된 데이터베이스 열을 기준으로 삽입, 업데이트 또는 필터링하는 쿼리를 실행할 수 있습니다.|
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22May+2020+Release%22+is%3Aclosed)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="april-2020-hotfix"></a>2020년 4월(핫픽스)

2020년 4월 30일 &nbsp; / &nbsp; 버전: 1.17.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 버그 #10197 MFA를 통해 연결할 수 없음 수정 | [#10197](https://github.com/microsoft/azuredatastudio/issues/10197)  |
| &nbsp; | &nbsp; |

## <a name="april-2020"></a>2020년 4월

2020년 4월 27일 &nbsp; / &nbsp; 버전: 1.17.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 홈페이지 개선 | 일반적인 작업을 쉽게 볼 수 있도록 홈페이지의 UI 업데이트를 개선하고 확장을 강조 표시했습니다. |
| 새로운 Notebook 기능 | &bull; &nbsp; Markdown을 사용한 쉬운 작성을 위해 텍스트 셀을 편집할 때 Markdown 도구 모음이 추가되었습니다. <br/> &bull; &nbsp; Jupyter Books 뷰렛을 Jupyter Books와 Notebook을 함께 관리할 수 있는 Notebook 뷰렛으로 강화했습니다. <br/>&bull; &nbsp; Notebook을 저장할 때 영구 차트에 대한 지원이 추가되었습니다. <br/> &bull; &nbsp; Python Notebook에 KQL 매직에 대한 지원이 추가되었습니다.|
| 대시보드 개선 | Azure Data Studio 전체의 대시보드가 동작 도구 모음을 포함하는 최신 디자인 패턴으로 업데이트되었습니다. 이는 여러 확장에도 적용됩니다. |
| Azure 보기에 Cloud Shell 통합이 추가되었습니다. | |
| Always Encrypted 및 보안 enclave를 사용한 Always Encrypted에 대한 지원이 추가되었습니다. | |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%22April+2020+Release%22)를 참조하세요. |
| &nbsp; | &nbsp; |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%22April+2020+Release%22)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="march-2020"></a>2020년 3월

2020년 3월 18일 &nbsp; / &nbsp; 버전: 1.16.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SQL Notebooks에 차트 지원이 추가됨 | 이제 코드 셀에서 SQL 쿼리를 실행할 때 차트를 만들고 저장할 수 있습니다. |
| Jupyter Book 만들기 환경이 추가됨 | 이제 Notebook을 사용하여 자체 Jupyter Book을 만들 수 있습니다. |
| Postgres 확장을 위한 Azure AD 지원이 추가됨 | |
| 여러 접근성 버그가 수정됨 | [접근성 버그 목록](https://github.com/microsoft/azuredatastudio/issues?page=1&q=is%3Aissue+is%3Aclosed+milestone%3A%22S360+-+Accessibility%22+label%3AA11y_AzureDataStudio) |
| 1\.42로 VS Code 병합 | 이 릴리스에는 이전 VS Code 릴리스 3개의 VS Code에 대한 업데이트가 포함되어 있습니다. 자세한 내용은 [릴리스 정보](https://code.visualstudio.com/updates/v1_42)를 참조하세요. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22March+2020%22+is%3Aclosed)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="february-hotfix"></a>2월(핫픽스)

2020년 2월 19일 &nbsp; / &nbsp; 버전: 1.15.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 버그 수정 #9149 활성 연결 표시 | [#9149](https://github.com/microsoft/azuredatastudio/issues/9149)  |
| 버그 수정 #9061 SQL 창을 표시하거나 숨길 때 데이터 편집 그리드의 크기가 제대로 조정되지 않음 | [#9061](https://github.com/microsoft/azuredatastudio/issues/9061)  |
| &nbsp; | &nbsp; |

## <a name="february-2020"></a>2020년 2월

2020년 2월 13일 &nbsp; / &nbsp; 버전: 1.15.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 새 Azure 로그인 향상 | 좀 더 원활한 연결 환경을 만들기 위해 디바이스 코드의 복사/붙여넣기 제거를 포함하여 향상된 Azure 로그인 환경이 추가되었습니다. |
| Notebook 지원 찾기 | 이제 사용자는 Notebook 내에서 Ctrl+F를 사용할 수 있습니다. Notebook 지원 검색에서 코드와 텍스트 셀 모두를 통해 한 줄씩 찾습니다. |
| 1\.38에서 1.42로 VS Code 병합 | 이 릴리스에는 이전 VS Code 릴리스 3개의 VS Code에 대한 업데이트가 포함되어 있습니다. 자세한 내용은 [릴리스 정보](https://code.visualstudio.com/updates/v1_42)를 참조하세요. |
| 여러 사용자가 보고한 [“흰색/빈 화면”](https://github.com/microsoft/azuredatastudio/issues/8775) 문제를 해결합니다. | |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%22February+2020%22)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issue"></a>알려진 문제

- macOS Catalina의 사용자는 Azure Data Studio를 마우스 오른쪽 단추로 클릭한 다음, 열기를 클릭해야 합니다.

## <a name="december-2019-hotfix"></a>2019년 12월(핫픽스)

2019년 12월 26일 &nbsp; / &nbsp; 버전: 1.14.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 버그 수정 #8747 OE 확장 실패 | [#8747](https://github.com/microsoft/azuredatastudio/issues/8747)  |
| &nbsp; | &nbsp; |

## <a name="december-2019"></a>2019년 12월

2019년 12월 19일 &nbsp; / &nbsp; 버전: 1.14.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 현재 활성 연결만 나열하도록 Notebooks의 연결에 연결 드롭다운 변경됨 | [#8129](https://github.com/microsoft/azuredatastudio/issues/8129) |
| BDC에 연결할 때 TLS/SSL 확인 오류를 무시할 수 있도록 bigdatacluster.ignoreSslVerification 설정 추가됨 | [#8582](https://github.com/microsoft/azuredatastudio/pull/8582) |
| 오프라인 쿼리 편집기의 기본 언어 버전 변경 허용 | [#8419](https://github.com/microsoft/azuredatastudio/pull/8419) |
| 빅 데이터 클러스터/SQL 2019 기능의 GA 상태 | [#8269](https://github.com/microsoft/azuredatastudio/issues/8269) |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/44?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |


## <a name="november-2019-hotfix"></a>2019년 11월(핫픽스)

2019년 11월 15일 &nbsp; / &nbsp; 버전: 1.13.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 버그 수정 #8210 복사/붙여넣기 결과의 순서가 잘못됨 |  |
| &nbsp; | &nbsp; |

## <a name="november-2019"></a>2019년 11월

2019년 11월 4일 &nbsp; / &nbsp; 버전: 1.13.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 새로운 SQL Server 2019 지원 | &bull; &nbsp; BDC 배포 마법사를 사용하여 SQL Server 2019 빅 데이터 클러스터 배포 <br/>&bull; &nbsp; 컨트롤러 대시보드를 사용하여 클러스터 상태 관리 <br/>&bull; &nbsp; 보안 ACL 대화 상자를 사용하여 HDFS 액세스 제어 목록 관리 <br/> &bull; &nbsp; HDFS 계층화 대화 상자를 사용하여 탑재 추가 <br/> &bull; &nbsp; 기본 제공 Jupyter Book인 SQL Server 2019 가이드를 사용하여 문제 해결 <br/> &bull; &nbsp; SQL vNext 확장 데이터 가상화 확장으로 이름 변경됨 <br/> &bull; &nbsp; 외부 테이블 마법사에 Teradata 및 Mongo 지원 추가됨|
| 새로운 Notebook 기능 | &bull; &nbsp; PowerShell Notebooks 발표 <br/> &bull; &nbsp; 접을 수 있는 코드 셀 발표 <br/>&bull; &nbsp; Notebooks의 성능 개선 <br/> &bull; &nbsp; 전체 개선 사항 목록은 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22November+2019+Release%22+is%3Aclosed+label%3A%22Area+-+Notebooks%22)에서 확인할 수 있음 |
| Jupyter Book 발표  | Jupyter Book는 목차에 구성된 전자 필기장 및 markdown 파일의 컬렉션입니다. |
| 새 SQL Server 배포 마법사  | 이제 다음과 같은 배포에 대한 지원이 포함됩니다. <br/> &bull; &nbsp; Windows의 SQL Server 2019 <br/> &bull; &nbsp; Windows의 SQL Server 2017 <br/> &bull; &nbsp; Docker의 SQL Server 2019 <br/> &bull; &nbsp; Docker의 SQL Server 2017 |
| 스키마 비교 확장 GA 발표| &bull; &nbsp; SQLCMD 모드 <br/> &bull; &nbsp; 지역화 지원 <br/> &bull; &nbsp; 접근성 수정 <br/> &bull; &nbsp; 보안 버그  |
| SQL Server Dacpac 확장 GA 발표| <br/> &bull; &nbsp; 지역화 지원 <br/> &bull; &nbsp; 접근성 수정 <br/> &bull; &nbsp; 보안 버그 |
| Visual Studio IntelliCode 확장 발표 | Visual Studio IntelliCode는 이제 SQL을 지원하므로 예약된 키워드를 보다 스마트하게 제안할 수 있습니다. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22November+2019+Release%22+is%3Aclosed)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="october-2019-hotfix-2"></a>2019년 10월(핫픽스 2)

2019년 10월 11일 &nbsp; / &nbsp; 버전: 1.12.2

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 검사 모드에서 EH 자동 시작 사용 안 함 |  |
| &nbsp; | &nbsp; |

## <a name="october-2019-hotfix"></a>2019년 10월(핫픽스)

2019년 10월 8일 &nbsp; / &nbsp; 버전: 1.12.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 전자 필기장의 따옴표와 백슬래시가 올바르게 이스케이프되도록 문제가 해결되었습니다. |  |
| &nbsp; | &nbsp; |

## <a name="october-2019"></a>2019년 10월

2019년 10월 2일 &nbsp; / &nbsp; 버전: 1.12.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 쿼리 기록 확장 릴리스 | SQL 기록 확장은 Azure Data Studio 세션에서 실행된 이전 쿼리를 모두 저장하고 실행 순서대로 나열합니다. 사용자는 쿼리 열기, 쿼리 실행, 쿼리 삭제, 쿼리 기록 일시 중지 또는 모든 쿼리 기록 항목 삭제 작업을 수행할 수 있습니다. |
| 새로운 결과 복사/붙여넣기 기능 | 결과 그리드에서 결과를 복사/붙여넣는 새로운 방법을 추가했습니다. |
| PowerShell 확장 업데이트 |  |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/42?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

- Notebooks
  - [7080](https://github.com/microsoft/azuredatastudio/issues/7080) Notebook을 잘못 직렬화할 때 드물게 발생

## <a name="september-2019"></a>2019년 9월

2019년 9월 10일 &nbsp; / &nbsp; 버전: 1.11.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SQLCMD 모드 사용 | 이제 쿼리 편집기는 쿼리를 SQLCMD 스크립트로 작성 및 편집하기 위한 SQLCMD 모드 토글을 지원합니다. |
| 커뮤니티 확장: Query Editor Boost | Query Editor Boost는 쿼리를 자주 작성하는 사용자를 위해 Azure Data Studio 쿼리 편집기를 개선하는 데 초점을 맞춘 오픈 소스 확장입니다. &bull; &nbsp; 현재 쿼리를 코드 조각으로 저장 <br/>&bull; &nbsp; Ctrl+U를 사용하여 데이터베이스 전환 <br/> &bull; &nbsp; 템플릿의 새 쿼리 <br/> &bull; &nbsp; 전체 개선 사항 목록은 [여기](https://github.com/dzsquared/query-editor-boost)에서 확인할 수 있음 |
| Notebook 기능 개선 | &bull; &nbsp; 더 큰 Notebook 파일을 지원하기 위한 성능 개선 <br/> &bull; &nbsp; 전체 개선 사항 목록은 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22September+2019+Release%22+label%3A%22Area%3A+Notebooks%22+is%3Aclosed)에서 확인할 수 있음 |
| Visual Studio Code 8월 릴리스 병합 1.38 | 최신 개선 사항은 [여기](https://code.visualstudio.com/updates/v1_38)에서 확인할 수 있습니다. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/39?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

- Notebooks
  - [7080](https://github.com/microsoft/azuredatastudio/issues/7080) Notebook을 잘못 직렬화할 때 드물게 발생

## <a name="august-2019"></a>2019년 8월

2019년 8월 15일 &nbsp; / &nbsp; 버전: 1.10.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SandDance 1.3.1 확장의 릴리스 | &bull; &nbsp; 스마트 차트 검색 <br/>&bull; &nbsp; 3D 시각화 <br/> &bull; &nbsp; 데이터 필터링 |
| Notebook 기능 개선 | &bull; &nbsp; 인라인으로 코드 또는 텍스트 셀 추가 <br/>&bull; &nbsp; SQL 결과 표를 마우스 오른쪽 단추로 클릭하여 결과를 CSV, JSON 등으로 저장하는 기능 추가됨 <br/> &bull; &nbsp; JSON을 더 빠르게 로드할 수 있도록 Notebook 로드 성능 개선 <br/> &bull; &nbsp; 전체 개선 사항 목록은 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+label%3A%22Area%3A+Notebooks%22+milestone%3A%22August+2019+Release%22+is%3Aclosed)에서 확인할 수 있음 |
| SQL Server 2019 지원 |  이 릴리스에서는 다음을 포함하여 추가 SQL Server 2019 빅 데이터 클러스터 기능을 지원합니다. <br/> &bull; &nbsp; 개체 매핑 페이지에서 테이블 및 열 정보를 로드하는 데 걸리는 시간이 단축됨 <br/> &bull; &nbsp; 연결 정보 페이지에서 기존 데이터베이스 범위 자격 증명을 로드할 때 발생하는 버그 수정됨 <br/> &bull; &nbsp; PROSE 구문 분석에 사용되는 기본 샘플 크기 커짐 | 
| Dacpac 확장에서 이제 Azure AD를 지원함 | 
| Visual Studio Code 7월 릴리스 병합 1.37 | 최신 개선 사항은 [여기](https://code.visualstudio.com/updates/v1_37)에서 확인할 수 있습니다. |
| 버그 및 이슈 해결 | 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/39?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="july-2019"></a>2019년 7월

2019년 7월 11일 &nbsp; / &nbsp; 버전: 1.9.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SentryOne Plan Explorer 확장 릴리스 | Microsoft의 소중한 파트너인 SentryOne은 [Azure Data Studio용 SentryOne Plan Explorer 확장](https://www.sentryone.com/products/sentryone-plan-explorer-extension-azure-data-studio)을 제공할 예정입니다. <br> 이 확장은 쿼리 성능에 영향을 주는 가장 고비용 연산자를 빠르게 식별할 수 있도록 지원하는 최적화된 레이아웃 알고리즘과 간단한 색 구분을 통해 Azure Data Studio에서 실행되는 쿼리에 향상된 계획 다이어그램을 제공하는 무료 확장입니다. 이 확장에 대한 자세한 내용을 보려면 [여기](https://sqlperformance.com/2019/07/sentryone/plan-explorer-extension-azure-data-studio)에서 SentryOne 블로그 게시물을 확인하세요. |
| 스키마 비교를 위한 새로운 기능 | &bull; &nbsp; 스키마 비교 파일 지원(.SCMP) <br/>&bull; &nbsp; 스키마 비교 취소 지원 <br/>&bull; &nbsp; 전체 변경 내용은 [여기](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed+)에서 확인할 수 있음|
| Notebook 기능 개선 | &bull; &nbsp; 플롯 Python 지원 <br/>&bull; &nbsp; 브라우저에서 Notebook 열기 <br/> &bull; &nbsp; Python 패키지 관리 대화 상자 <br/> &bull; &nbsp; 성능 및 Markdown 개선 <br/> &bull; &nbsp; 바로 가기 키 업데이트 <br/>  &bull; &nbsp; 버그 수정 및 사소한 기능은 [여기](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A%22July+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22+)에서 확인할 수 있음 |
| SQL Server 2019 지원 |  이 릴리스에서는 다음을 포함하여 추가 SQL Server 2019 빅 데이터 클러스터 기능을 지원합니다. <br/> &bull; &nbsp; 클러스터의 모든 핵심 서비스를 나열하는 서비스 엔드포인트 테이블이 관리 대시보드에 포함됨 <br/> &bull; &nbsp; 클러스터 상태 Notebook에 모든 서비스 및 Pod에서 클러스터 상태를 쿼리하고 관련 문제를 해결할 수 있는 방법이 표시됨| 
| 업데이트된 언어 팩 사용 가능| 이제 확장 관리자 마켓플레이스에서 10개의 언어 팩을 사용할 수 있습니다. 간단히, 확장 마켓플레이스를 사용하여 특정 언어를 검색하고 설치합니다. 선택한 언어를 설치하면 Azure Data Studio에서 새 언어로 다시 시작하라는 메시지가 표시됩니다. |
| SQL Server Profiler 업데이트 | SQL Server 프로필 확장이 다음을 비롯한 새로운 기능을 포함하도록 업데이트되었습니다. <br/> &bull; &nbsp; 데이터베이스 이름을 기준으로 필터링 <br/> &bull; &nbsp; 복사 및 붙여넣기 지원 <br/> &bull; &nbsp; 필터 저장/로드 <br/>SQL Server Profiler 확장 개선 사항의 전체 목록은 [여기](https://github.com/microsoft/azuredatastudio/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aclosed+milestone%3A%22July+2019+Release%22+label%3A%22Area%3A+SQL+Profiler%22+)에서 확인할 수 있습니다.  |
| Visual Studio Code 5월 릴리스 병합 1.35 | 최신 개선 사항은 [여기](https://code.visualstudio.com/updates/v1_35)에서 확인할 수 있습니다. |
| 버그 및 이슈 해결 | 이전 Azure Data Studio 릴리스에서는 연결 대화 상자에서 연결할 때 사용자 데이터베이스를 선택하면 결과 개체 탐색기 항목의 범위가 해당 단일 데이터베이스로만 지정되었습니다. 이 릴리스부터 서버 수준 속성도 개체 탐색기에 표시되도록 동작이 변경됩니다. <br/> 전체 수정 목록은 [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/35?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="june-2019"></a>2019년 6월

2019년 6월 6일 &nbsp; / &nbsp; 버전: 1.8.0

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| CMS(중앙 관리 서버) 확장 릴리스 | 중앙 관리 서버는 하나 이상의 중앙 관리 서버 그룹으로 구성된 SQL Server 인스턴스 목록을 저장합니다. 사용자는 고유한 기존 CMS 서버에 연결하고 서버 추가 및 제거와 같은 서버 관리 작업을 수행할 수 있습니다. 자세한 내용은 [여기](../relational-databases/administer-multiple-servers-using-central-management-servers.md)를 참조하세요. |
| Windows용 데이터베이스 관리 도구 확장 릴리스 | 이 확장은 Azure Data Studio를 통해 SQL Server Management Studio에서 가장 많이 사용되는 두 가지 환경을 시작합니다. 사용자는 여러 가지 개체(예: 데이터베이스, 테이블, 열, 뷰 등)를 마우스 오른쪽 단추로 클릭하고 속성을 선택하여 해당 개체의 SSMS 속성 대화 상자를 볼 수 있습니다. 또한 사용자는 데이터베이스를 마우스 오른쪽 단추로 클릭하고 스크립트 생성을 선택하여 잘 알려진 SSMS 스크립트 생성 마법사를 시작할 수 있습니다. 
| 스키마 비교 기능 개선 | &bull; &nbsp; 제외/포함 옵션 추가됨 <br/>&bull; &nbsp; 스크립트 생성 시 생성된 스크립트 열림 <br/>&bull; &nbsp; 이중 스크롤 막대 제거됨  <br/>&bull; &nbsp; 서식 및 레이아웃 개선 <br/>&bull; &nbsp; 전체 변경 내용은 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+label%3A%22Area%3A+Schema+Compare%22+is%3Aclosed)에서 확인할 수 있음|
| 메시지 섹션이 고유한 탭으로 이동됨 | 사용자가 SQL 쿼리를 실행하면 결과 및 메시지가 누적된 패널에 표시되었습니다. 이제 SSMS와 같이 한 패널의 개별 탭으로 표시됩니다. |
| SQL Notebook 기능 개선 | &bull; &nbsp; 이제 사용자가 Notebook에서 고유한 Python 3 또는 Anaconda 설치를 사용하도록 선택할 수 있음 <br/>&bull; &nbsp; 여러 가지 안정성 + 맞춤/마침 수정 <br/> &bull; &nbsp; 전체 개선 사항 목록은 [여기](https://github.com/microsoft/azuredatastudio/issues?q=is%3Aissue+milestone%3A%22June+2019+Release%22+is%3Aclosed+label%3A%22Area%3A+Notebooks%22)에서 확인할 수 있음|
| Visual Studio Code 4월 릴리스 병합 1.34 | 최신 개선 사항은 [여기](https://code.visualstudio.com/updates/v1_34)에서 확인할 수 있습니다. |
| 버그 및 이슈 해결 | [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/32?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제

- Windows용 데이터베이스 관리 도구 확장
    - 연결되지 않은 서버 노드의 속성을 시작할 수 없습니다.
    - Azure 서버의 속성을 시작할 수 없습니다.
    - 일부 개체에 속성 대화 상자가 없습니다.
    - 대화 상자를 시작하는 데 시간이 오래 걸립니다.
    - 일부 연결 형식(예: Azure AD)으로 서버를 시작할 때 오류가 발생합니다.
- Notebooks
    - [5838](https://github.com/microsoft/azuredatastudio/issues/5838) 사용자가 시스템 Python을 Notebook에 사용할 수 있습니다.
- 스키마 비교
    - [5804](https://github.com/microsoft/azuredatastudio/issues/5804) 스키마 비교 작업에 아무 동작도 수행하지 않는 기본 취소 상황에 맞는 메뉴가 표시됩니다.

## <a name="may-2019"></a>2019년 5월

2019년 5월 8일 &nbsp; / &nbsp; 버전: 1.7.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 스키마 비교 확장 릴리스 | 스키마 비교는 SSDT(SQL Server Data Tools)의 잘 알려진 기능이며, 주 사용 사례는 데이터베이스와 .dacpac 파일 간의 차이점을 비교 및 시각화하고 동일하게 만드는 작업을 실행하는 것입니다. |
| 작업 뷰가 출력 창으로 이동됨 | 이제 출력 창의 작업 뷰에서 백업, 복원 및 스키마 비교와 같은 장기 실행 작업의 상태를 볼 수 있습니다.
| 시작 페이지가 추가됨 | &bull; &nbsp; 새 쿼리, 새 파일, 새 Notebook과 같은 일반적인 작업 링크 <br/>&bull; &nbsp; 문서 및 GitHub 링크 |
| SQL Notebook 기능 개선 | &bull; &nbsp; 노트 및 테이블 지원 향상을 비롯한 Markdown 렌더링 개선 <br/>&bull; &nbsp; 도구 모음의 유용성 개선 <br/>&bull; &nbsp; 신뢰할 수 있는 Notebook의 Markdown 링크를 더 이상 Cmd/Ctrl+클릭할 필요 없이 직접 클릭할 수 있음 <br/>&bull; &nbsp; Notebook을 닫은 후 Jupyter 프로세스를 정리하고 여러 Notebook을 동시에 시작할 때 오류를 줄이는 기능 개선 <br/>&bull; &nbsp; 동일한 데이터베이스에 대해 2개의 Notebook을 실행할 때 오류가 발생하지 않도록 SQL Notebook 연결 개선 <br/>&bull; &nbsp; 도구 모음에서 셀 실행 단추를 클릭할 때 현재 실행 중인 셀로 자동 스크롤되도록 Notebook 개선 <br/>&bull; &nbsp; 일반적인 안정성 및 성능 개선 |
| 버그 및 이슈 해결 | [GitHub의 버그 및 이슈](https://github.com/microsoft/azuredatastudio/milestone/31?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="april-2019"></a>2019년 4월

2019년 4월 18일 &nbsp; / &nbsp; 버전: 1.6.0 

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| **서버** 탭의 이름이 **연결** 로 바뀜 | |
| Azure Resource Explorer가 연결 아래의 Azure 뷰렛으로 이동됨 | 이제 사용자가 연결 뷰에서 Azure 뷰렛을 통해 Azure SQL 인스턴스를 보고, 펼쳐서 각 서버 또는 데이터베이스 아래의 개체를 볼 수 있습니다.|
| SQL Notebook 기능 개선 | &bull; &nbsp; 모든 셀의 출력을 지우는 단추가 도구 모음에 추가됨 <br/>&bull; &nbsp; 모든 셀을 실행하는 단추가 도구 모음에 추가됨 <br/>&bull; &nbsp; 연결 대상 드롭다운에 서버 이름(설정된 경우) 대신 연결 이름이 표시되도록 수정됨 <br/>&bull; &nbsp; 상대 이미지 경로를 사용할 때 Markdown의 이미지가 렌더링되지 않는 문제가 해결됨 <br/>&bull; &nbsp; 두 번 클릭하여 열 크기를 자동으로 조정하는 기능을 추가하여 Notebook 그리드 기능 개선 및 마우스 휠 지원 개선 <br/>&bull; &nbsp; Notebook을 통해 python을 설치할 때 오류 처리 및 python 설치 복원력 개선 <br/>&bull; &nbsp; Notebook 셀을 선택할 때 “모두 선택” 기능 개선 <br/>&bull; &nbsp; Notebook을 닫을 때 개체 탐색기 연결에 영향을 주지 않도록 Notebook 연결 개선 <br/>&bull; &nbsp; Notebook 연결이 끊겼으며 셀 실행을 위해 연결해야 하는 경우 사용자에게 메시지를 표시하도록 Notebook 환경 개선<br/>&bull; &nbsp; ADS를 다시 시작할 때 저장하지 않은 Notebook이 ADS에서 리하이드레이션되도록 지원 개선 |
| 버그 및 이슈 해결 | [GitHub의 버그 및 이슈](https://github.com/Microsoft/azuredatastudio/milestone/26?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="march-2019-hotfix"></a>2019년 3월(핫픽스)

2019년 3월 22일 &nbsp; / &nbsp; 버전: 1.5.2 &nbsp; / &nbsp; 핫픽스 릴리스

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 1\.5.1에서 발견된 몇 가지 문제가 해결됨 | [GitHub의 3월 핫픽스 릴리스](https://github.com/Microsoft/azuredatastudio/milestone/28)를 참조하세요.<br/> <br/>&bull; &nbsp; 사용자가 대시보드의 “Notebook 열기” 작업을 통해 열린 Notebook을 닫을 수 없는 문제가 해결됨 <br/>&bull; &nbsp; 저장 후에 Notebook JSON에 불필요한 }가 표시되는 문제가 해결됨 <br/>&bull; &nbsp; Notebook 그리드가 테마 변경에 응답하지 않는 문제가 해결됨 <br/>&bull; &nbsp; 전체 Notebook 경로가 탭 머리글에 표시되는 문제가 해결됨. 이제 파일 이름만 표시됩니다. |
| &nbsp; | &nbsp; |

## <a name="march-2019"></a>2019년 3월

2019년 3월 18일 &nbsp; / &nbsp; 버전: 1.5.1

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| [Azure Data Studio용 PostgreSQL 확장](./extensions/postgres-extension.md)이 추가됨 | 지원되는 기능: <br/>&bull; &nbsp; 연결 대화 상자 <br/>&bull; &nbsp; 개체 탐색기 <br/>&bull; &nbsp; 쿼리 편집기 <br/>&bull; &nbsp; 차트 작성 <br/>&bull; &nbsp; 대시보드 <br/>&bull; &nbsp; 코드 조각 <br/>&bull; &nbsp; 데이터 편집 <br/>&bull; &nbsp; Notebooks |
| SQL Notebook이 추가됨 | 기본 제공 Notebook 뷰어에 SQL 커널 지원을 추가했습니다. <br/>&bull; &nbsp; T-SQL 지원 <br/>&bull; &nbsp; PGSQL 지원 |
| PowerShell 확장이 추가됨 | VS Code에서 [PowerShell 확장](https://marketplace.visualstudio.com/items?itemName=ms-vscode.PowerShell) 환경을 가져옵니다.  |
| SQL Server dacpac 확장이 추가됨  | SQL Server 가져오기 확장의 데이터 계층 애플리케이션 마법사를 제거하고 새 확장으로 대체합니다.  |
| 커뮤니티 확장 QueryPlan.show가 추가됨 | 통합 지원을 추가하여 쿼리 계획을 시각화합니다.  |
| SQL Server 2019 미리 보기 확장이 업데이트됨 | &bull; &nbsp; Jupyter Notebook 지원, 특히 Python3 및 Spark 커널이 핵심 Azure Data Studio 도구로 이동되었습니다. <br/>&bull; &nbsp; 외부 데이터 마법사 버그 수정 |
| 버그 및 이슈 해결 | [GitHub의 버그 및 이슈](https://github.com/Microsoft/azuredatastudio/milestone/25?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>알려진 문제
- [#4427](https://github.com/Microsoft/azuredatastudio/issues/4427): 커널이 Spark에 대해 준비되기 전에 셀에서 실행을 클릭하면 심각한 오류가 발생합니다. **해결 방법:** 커널이 로드될 때까지 기다린 후에 셀을 실행합니다.
- [#4493](https://github.com/Microsoft/azuredatastudio/issues/4493): SQL 인증을 사용하여 SSMS에서 ADS를 시작할 경우 암호를 묻는 메시지가 표시됩니다. **해결 방법:** 당분간 Windows 인증을 사용합니다. 
- [#4494](https://github.com/Microsoft/azuredatastudio/issues/4494): SQL Notebook 기능을 설치할 수 없습니다. <br/>
**해결 방법:** [여기](https://github.com/Microsoft/azuredatastudio/issues/4494#issuecomment-473043832)에 제공된 해결 단계를 따릅니다. 
- [#4503](https://github.com/Microsoft/azuredatastudio/issues/4503): 다운로드 폴더에서 바로 Azure Data Studio를 열 수 없습니다(Mac). <br />
**해결 방법:** 앱 압축을 푼 후 컴퓨터를 다시 시작합니다. 이 문제는 조사될 예정입니다. 
- [#4539](https://github.com/Microsoft/azuredatastudio/issues/4539):  다른 이름으로 Notebook을 저장하면 연결 컨텍스트가 손실됩니다. <br />
**해결 방법:** 다음 릴리스에서 수정될 예정입니다. 
- [#4458](https://github.com/Microsoft/azuredatastudio/issues/4458): 잘못된 버전을 사용하면 Dacpac Extract와 SqlToolsService가 충돌합니다. <br/>
**해결 방법:** Azure Data Studio를 다시 시작하고 올바른 버전이 사용되는지 확인합니다.
- 새 Notebook 및 Notebook 열기 아이콘이 손실됩니다. <br/>
**해결 방법:** 레거시 연결 형식은 더 이상 사용되지 않습니다. SQL Server 엔드포인트에 연결하는 것이 좋습니다. 그러면 모든 작업(새 Notebook, Spark 작업)이 예상대로 표시됩니다. 

## <a name="february-2019"></a>2019년 2월

2019년 2월 13일 &nbsp; / &nbsp; 버전: 1.4.5

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| **SQL Server 관리 팩** 확장 팩이 추가됨 | 이 확장 팩을 사용하면 보다 간편하게 SQL Server 관리 관련 확장을 설치할 수 있습니다. 다음 내용이 포함됩니다.<br/>&bull; &nbsp; [SQL Server 에이전트](./extensions/sql-server-agent-extension.md)<br/>&bull; &nbsp; [SQL Server Profiler](./extensions/sql-server-profiler-extension.md)<br/>&bull; &nbsp; [SQL Server 가져오기](./extensions/sql-server-import-extension.md) |
| Profiler 확장에 확장 이벤트 필터링 지원이 추가됨 | &nbsp; |
| T-SQL 결과를 XML로 저장할 수 있는 XML로 저장 기능이 추가됨 | &nbsp; |
| 데이터 계층 애플리케이션 마법사 개선 사항이 추가됨 | &bull; &nbsp; 스크립트 생성 단추 추가됨<br/>&bull; &nbsp; 배포 중에 데이터가 손실될 수 있다는 경고를 표시하는 뷰 추가됨 |
| SQL Server 2019 미리 보기 확장 업데이트 | [데이터 가상화 확장](./extensions/data-virtualization-extension.md)을 참조하세요. |
| 장기 실행 쿼리에 대해 결과 스트리밍이 기본적으로 사용됨 | &nbsp; |
| 버그 및 이슈 해결 | [GitHub의 버그 및 이슈](https://github.com/Microsoft/azuredatastudio/milestone/23?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="january-2019-hotfix"></a>2019년 1월(핫픽스)

2019년 1월 16일 &nbsp; / &nbsp; 버전: 1.3.9 &nbsp; / &nbsp; 핫픽스 릴리스

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 1\.3.8에서 발견된 몇 가지 문제가 해결됨 | [GitHub의 1월 핫픽스 릴리스](https://github.com/Microsoft/azuredatastudio/milestone/24?closed=1)를 참조하세요.<br/><br/>자세한 내용은 다음을 참조하세요.<br/>&bull; &nbsp; [GitHub의 변경 로그](https://github.com/Microsoft/azuredatastudio/blob/main/CHANGELOG.md)<br/>&bull; &nbsp; [GitHub의 릴리스](https://github.com/Microsoft/azuredatastudio/releases) |
| &nbsp; | &nbsp; |

## <a name="january-2019"></a>2019년 1월

2019년 1월 9일 &nbsp; / &nbsp; 버전: 1.3.8

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| Windows용 새 사용자 설치 관리자가 추가됨 | 기존 시스템 설치 관리자와 달리, 새 사용자 설치 관리자에는 관리자 권한이 필요하지 않습니다. 따라서 관리자가 아닌 사용자가 보다 쉽게 업그레이드할 수도 있습니다. |
| Azure Active Directory 인증 지원이 추가됨 | &nbsp; |
| Idera SQL DM Performance Insights(미리 보기) 발표 | &nbsp; |
| SQL Server 가져오기 확장의 데이터 계층 애플리케이션 마법사 지원 | &nbsp; |
| SQL Server 2019 미리 보기 확장 업데이트 | [데이터 가상화 확장](./extensions/data-virtualization-extension.md)을 참조하세요. |
| SQL Server Profiler 기능 개선 | &nbsp; |
| 대규모 쿼리의 결과 스트리밍(미리 보기) | &nbsp; |
| 커뮤니티 확장: SQL 및 새 데이터베이스에 대한 sp_executesql | &nbsp; |
| 버그 및 이슈 해결 | [GitHub의 버그 및 이슈](https://github.com/Microsoft/azuredatastudio/milestone/19?closed=1)를 참조하세요. |
| &nbsp; | &nbsp; |

## <a name="november-2018"></a>2018년 11월

2018년 11월 6일 &nbsp; / &nbsp; 버전: 1.2.4

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SQL Server 2019 미리 보기 확장 업데이트 | [데이터 가상화 확장](./extensions/data-virtualization-extension.md)을 참조하세요. |
| 계획 붙여넣기 확장 도입 | &nbsp; |
| SSMS 편집기 테마를 비롯한 하이 컬러 쿼리 확장 도입 | &nbsp; |
| SQL Server 에이전트, Profiler 및 가져오기 확장 수정 | &nbsp; |
| macOS에서 비활성 연결을 삭제하는 .NET Core 소켓 KeepAlive 문제 해결 | &nbsp; |
| .NET Core 2.2 미리 보기 3으로 SQL Tools Service 업그레이드(최종 Azure AD 지원 제공) | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-november-2018"></a>버그 수정, 2018년 11월

- [이슈 #2933](https://github.com/Microsoft/azuredatastudio/issues/2933) 해결: Azure SQL Database와의 연결이 끊김
- [이슈 #2914](https://github.com/Microsoft/azuredatastudio/issues/2914) 해결: OE 데이터베이스 노드를 확장하는 “잘못된 인수” 예외
- [이슈 #2935](https://github.com/Microsoft/azuredatastudio/pull/2935) 해결: 쿼리 결과에 여러 줄 메시지를 올바르게 표시
- [이슈 #2906](https://github.com/Microsoft/azuredatastudio/pull/2906) 해결: 테이블 이름에 특수 문자가 포함된 경우 데이터 편집 문서 이름 수정
- [이슈 #2929](https://github.com/Microsoft/azuredatastudio/issues/2929) 해결: VSCode 릴리스 정보에서 변경 내용을 확인하기 위한 기본 제공 확장 변경 로그
- [이슈 #2719](https://github.com/Microsoft/azuredatastudio/issues/2719) 해결: 고대비 테마 이중/삼중 쌍 아이콘
- [이슈 #3047](https://github.com/Microsoft/azuredatastudio/pull/3047) 해결: SQL Server에 연결하기 위한 명령줄 인터페이스가 추가되었습니다.
- [이슈 #3031](https://github.com/Microsoft/azuredatastudio/pull/3031) 해결: 쿼리 계획 테마 지원 추가

## <a name="october-2018"></a>2018년 10월

2018년 10월 29일 &nbsp; / &nbsp; 버전: 1.1.4

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| Azure SQL Database를 검색하기 위한 Azure Resource Explorer 도입 | &nbsp; |
| 개체 탐색기와 쿼리 편집기 간의 연결이 강화됨 | &nbsp; |
| SQL 에이전트 확장 기능 개선 | &nbsp; |
| SQL Server 2019 미리 보기 확장 업데이트 | [데이터 가상화 확장](./extensions/data-virtualization-extension.md)을 참조하세요. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-october-2018"></a>버그 수정, 2018년 10월

- [이슈 #2717](https://github.com/Microsoft/azuredatastudio/issues/2717) 해결: XML 열 결과 클릭 서식 지정
- [이슈 #2993](https://github.com/Microsoft/azuredatastudio/issues/2993) 해결: 너비의 결과 창이 완전하지 않음
- [이슈 #2999](https://github.com/Microsoft/azuredatastudio/issues/2999) 해결: DB에 연결할 때 Mac에서 System.Diagnostics.Tracing 파일을 로드할 수 없음
- [이슈 #2851](https://github.com/Microsoft/azuredatastudio/issues/2851) 해결: TimeSeries 차트가 올바르게 렌더링되지 않음
- [이슈 #2996](https://github.com/Microsoft/azuredatastudio/issues/2996) 해결: 갑작스러운 세션 변경으로 인한 일시적 테이블 손실

자세한 내용은 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/main/CHANGELOG.md) 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)를 참조하세요.

## <a name="september-2018-ga-release"></a>2018년 9월(GA 릴리스)

2018년 9월 24일 &nbsp; / &nbsp; 버전: 1.0 &nbsp; / &nbsp; GA 릴리스

Azure Data Studio(이전 SQL Operations Studio)의 일반 공급 릴리스

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 다수의 결과 집합에 대한 쿼리 결과 그리드 성능 및 UX 향상 | &nbsp; |
| Visual Studio Code 소스 코드가 1.23에서 그리드 레이아웃 및 향상된 설정 편집기(미리 보기)를 포함하는 1.26.1로 업그레이드됨 | &nbsp; |
| 화면 판독기, 키보드 탐색 및 고대비를 통해 접근성 향상 | &nbsp; |
| 서버 뷰렛에 대체 표시 이름을 제공하는 `Connection name` 옵션이 추가됨 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="announcing-the-sql-server-2019-preview-extension"></a>SQL Server 2019 미리 보기 확장 발표

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| [빅 데이터 클러스터](../big-data-cluster/big-data-cluster-overview.md) 지원을 포함하는 SQL Server 2019 미리 보기 기능 지원 | SQL Server 2019 미리 보기와 함께 제공되는 HDFS/Spark 게이트웨이에 연결합니다.<br/><br/>HDFS를 찾아보고, 파일을 업로드 및 저장하며, Notebook에서 CSV 파일 분석 등의 유용한 작업을 시작합니다.<br/><br/>대시보드에서 Spark 작업을 제출하거나 개체 탐색기에서 HDFS/Spark 연결을 마우스 오른쪽 단추로 클릭합니다. |
| Azure Data Studio Notebook | 통합 Notebook 뷰어를 사용하여 Notebook을 만들거나 엽니다. 이 릴리스에서는 Notebook 뷰어를 통해 로컬 커널 및 SQL Server 2019 빅 데이터 클러스터에만 연결할 수 있습니다.<br/><br/>Notebook에서 PROSE Code Accelerator 라이브러리를 사용하여 빠른 데이터 준비를 위한 파일 형식 및 데이터 형식을 알아봅니다. |
| Azure Resource Explorer | Azure Resource Explorer 뷰를 사용하여 Azure 계정의 데이터 관련 엔드포인트를 검색하고 개체 탐색기를 통해 해당 엔드포인트에 연결할 수 있습니다. 이 릴리스에서는 Azure SQL Database가 지원됩니다. |
| SQL Server PolyBase 외부 테이블 만들기 마법사 | 간편한 마법사를 사용하여 외부 테이블 및 해당하는 지원 메타데이터 구조를 만듭니다. 이 릴리스에서는 원격 SQL Server 및 Oracle 서버가 지원됩니다. |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-september-2018"></a>버그 수정, 2018년 9월

- [이슈 #2647](https://github.com/Microsoft/azuredatastudio/issues/143) 해결: 차트 기능이 크게 퇴보함
- [이슈 #2648](https://github.com/Microsoft/azuredatastudio/issues/143) 해결: JSON을 반환하는 SELECT가 전체 열에 하이퍼링크를 지정함

자세한 내용은 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/main/CHANGELOG.md) 및 [릴리스](https://github.com/Microsoft/azuredatastudio/releases)를 참조하세요.

## <a name="august-2018"></a>2018년 8월

2018년 8월 30일 &nbsp; / &nbsp; 버전: 0.32.8 &nbsp; / &nbsp; 공개 미리 보기

‘8월 공개 미리 보기’에서는 기존 시나리오에서 버그 수정, 제품 안정화 및 간극 완화에 중점을 둡니다.

_0.32.8에는 0.32.7의 몇 가지 기능 저하_ 에 대한 수정([#1971](https://github.com/Microsoft/azuredatastudio/issues/1971), [#2372](https://github.com/Microsoft/azuredatastudio/issues/2372))이 포함되어 있습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SQL Server 가져오기 확장 발표 | &nbsp; |
| SQL Server Profiler 세션 관리 | &nbsp; |
| SQL Server Profiler 세션 템플릿 지원 | &nbsp; |
| SQL Server 에이전트 기능 개선 | &nbsp; |
| 새 커뮤니티 확장: 첫 번째 응답자 키트 | &nbsp; |
| 수명 품질 개선: 연결 문자열 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-august-2018"></a>버그 수정, 2018년 8월

- `Parse Syntax` 명령을 사용하여 쿼리 편집기 창에서 SQL 구문 분석
- [이슈 #143](https://github.com/Microsoft/azuredatastudio/issues/143) 해결: 두 번 클릭해도 변수 이름에서 @가 선택되지 않음
- [이슈 #387](https://github.com/Microsoft/azuredatastudio/issues/387) 해결: SQL 탭 DB 아이콘이 빨간색으로 표시됨
- [이슈 #825](https://github.com/Microsoft/azuredatastudio/issues/825) 해결: 요청: 다음으로 스크립트 후 현재 서버에 자동으로 연결됨 
- [이슈 #1278](https://github.com/Microsoft/azuredatastudio/issues/1278) 해결: sqlops.desktop[데스크톱 항목] - 이름 및 주석 값 중복
- [이슈 #1285](https://github.com/Microsoft/azuredatastudio/issues/1285) 해결: 업데이트하면 Windows에서 애플리케이션 아이콘이 제거됨/바뀜
- [이슈 #1317](https://github.com/Microsoft/azuredatastudio/issues/1317) 해결: 소수 구분 기호 수정
- [이슈 #1474](https://github.com/Microsoft/azuredatastudio/issues/1474) 해결: 연결 변경을 취소하면 현재 연결이 끊어짐
- [이슈 #1497](https://github.com/Microsoft/azuredatastudio/issues/1497) 해결: 차트 옵션이 아래쪽에서 잘린 상태로 표시됨
- [이슈 #1524](https://github.com/Microsoft/azuredatastudio/issues/1524) 해결: 셸/대시보드: 주 뷰렛 아이콘이 끌기 가능하며 앱과 충돌할 수 있음
- [이슈 #1578](https://github.com/Microsoft/azuredatastudio/issues/1578) 해결: 이름을 클릭하여 원격 파일 브라우저 폴더를 확장/축소할 수 없음
- [이슈 #1620](https://github.com/Microsoft/azuredatastudio/issues/1620) 해결: 기능 제안: 기존 연결의 연결 문자열 가져오기
- [이슈 #1624](https://github.com/Microsoft/azuredatastudio/issues/1624) 해결: 사용하지 않도록 설정된 경우 SelectBox의 색이 바뀌지 않음
- [이슈 #1728](https://github.com/Microsoft/azuredatastudio/issues/1728) 해결: JSON/EXCEL/CSV로 저장 기능이 작동하지 않음
- [이슈 #1744](https://github.com/Microsoft/azuredatastudio/issues/1744) 해결: 탭 간을 전환할 때 결과 창의 스크롤 위치가 손실됨
- [이슈 #1748](https://github.com/Microsoft/azuredatastudio/issues/1748) 해결: Excel 파일을 두 번째(및 후속) 저장할 때 오류 메시지가 표시됨
- [이슈 #1782](https://github.com/Microsoft/azuredatastudio/issues/1782) 해결: 데이터 편집: Esc 키를 눌러도 셀이 원래 값으로 돌아가지 않음
- [이슈 #1836](https://github.com/Microsoft/azuredatastudio/issues/1836) 해결: .sql 파일이 SQL Operations Studio와 연결되지 않음
- [이슈 #1850](https://github.com/Microsoft/azuredatastudio/issues/1850) 해결: N’’을 입력하면 N’’’으로 자동 완성됨
- [이슈 #1985](https://github.com/Microsoft/azuredatastudio/issues/1985) 해결 : 쿼리 결과 그리드에서 복사할 때 한 열씩 벗어남
- [이슈 #1998](https://github.com/Microsoft/azuredatastudio/pull/1998) 해결: 정보 대화 상자에 VS Code 버전 추가
- [이슈 #2042](https://github.com/Microsoft/azuredatastudio/pull/2042) 해결: 에이전트: sql 파일에서 쿼리를 가져오는 단추를 사용할 수 있음
- [이슈 #2091](https://github.com/Microsoft/azuredatastudio/issues/2091) 해결: Ctrl+C 바로 가기를 사용하여 결과 창에서 복사할 수 없음
- [이슈 #2099](https://github.com/Microsoft/azuredatastudio/pull/2099) 해결: saveAsCsv 옵션이 더 추가됨
- [이슈 #2107](https://github.com/Microsoft/azuredatastudio/issues/2107) 해결: 대시보드 및 Profiler 문서의 문서 아이콘 업데이트
- [이슈 #2129](https://github.com/Microsoft/azuredatastudio/pull/2129) 해결: 탭을 전환할 때 데이터 편집 스크롤 위치 저장
- [이슈 #2152](https://github.com/Microsoft/azuredatastudio/issues/2152) 해결: 결과 그리드 행 표시기가 0부터 시작함

### <a name="known-issues-august-2018"></a>알려진 문제, 2018년 8월

- [이슈 #2371](https://github.com/Microsoft/azuredatastudio/issues/2371) Excel로 저장하면 첫 번째 데이터 행만 저장됨
- [이슈 #2150](https://github.com/Microsoft/azuredatastudio/issues/2150): Ubuntu 16.04에서 컨테이너의 SQL에 연결할 수 없음

## <a name="july-2018"></a>2018년 7월

2018년 7월 19일 &nbsp; / &nbsp; 버전: 0.31.4 &nbsp; / &nbsp; 공개 미리 보기

*7월 공개 미리 보기* 에서는 다음 항목에 중점을 둡니다.

- SQL Server 에이전트 구성 시나리오의 최초 릴리스
- SQL Server Profiler 세션 및 보기 템플릿 기능 개선
- 고객이 보고한 GitHub 이슈에 대한 버그 수정 계속

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| [SQL Operations Studio용 SQL Server 에이전트 확장](./extensions/sql-server-agent-extension.md) 기능 개선 | 왼쪽 창에 경고, 운영자 및 프록시 뷰와 아이콘이 추가되었습니다.<br/><br/>새 작업, 새 작업 단계, 새 경고 및 새 운영자 대화 상자가 추가되었습니다.<br/><br/>작업 삭제, 경고 삭제 및 운영자 삭제(마우스 오른쪽 단추 클릭)가 추가되었습니다.<br/><br/>이전 실행 시각화가 추가되었습니다.<br/><br/>각 열 이름의 필터가 추가되었습니다. |
| [SQL Operations Studio용 SQL Server Profiler 확장](./extensions/sql-server-profiler-extension.md) 기능 개선 | 확장 이벤트를 볼 수 있는 기본 템플릿 5개가 추가되었습니다.<br/><br/>서버/데이터베이스 연결 이름이 추가되었습니다.<br/><br/>Azure SQL Database 인스턴스 지원이 추가되었습니다.<br/><br/>Profiler가 실행 중일 때 탭을 닫을 경우 Profiler를 종료하라는 제안이 추가되었습니다. |
| 스크립트 결합 확장 릴리스 | &nbsp; |
| 확장 작성자를 위한 마법사 및 대화 상자 확장성 지점이 추가됨 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="bug-fixes-july-2018"></a>버그 수정, 2018년 7월

- [이슈 728](https://github.com/Microsoft/azuredatastudio/issues/728) 해결: macOS에서 연결 추가 시 응답이 없음
- [이슈 1612](https://github.com/Microsoft/azuredatastudio/issues/1612) 해결: 국제 문자가 있는 경우 결과 그리드 텍스트가 제대로 표시되지 않음
- [이슈 1693](https://github.com/Microsoft/azuredatastudio/issues/1693) 해결: 백업 대화 상자: 파일 브라우저 UI가 손상됨
- [이슈 1713](https://github.com/Microsoft/azuredatastudio/issues/1713) 해결: 행 수가 영향을 받음
- [이슈 1718](https://github.com/Microsoft/azuredatastudio/issues/1718) 해결: 데이터 원본에 연결할 수 없음
- [이슈 1719](https://github.com/Microsoft/azuredatastudio/issues/1719) 해결: 서버에 연결할 때 TypeError가 발생함
- [이슈 1724](https://github.com/Microsoft/azuredatastudio/issues/1724) 해결: 확장 대화 상자의 작동이 중지됨
- [이슈 1749](https://github.com/Microsoft/azuredatastudio/issues/1749) 해결: 버그: 열의 HTML 데이터가 해석됨
- [이슈 1789](https://github.com/Microsoft/azuredatastudio/issues/1789) 해결: 확장성: 연결 공급자를 추가할 경우 제거해도 목록에서 제거되지 않음
- [이슈 1791](https://github.com/Microsoft/azuredatastudio/issues/1791) 해결: sqlops 확장: queryeditor.connect()가 대상 데이터베이스에 연결되지만, UI에 편집기가 연결된 것으로 표시되지 않음
- [이슈 1799](https://github.com/Microsoft/azuredatastudio/issues/1799) 해결: 상위 10개 DB 크기 차트가 대/소문자 구분 인스턴스에서 작동하지 않음
- [이슈 1814](https://github.com/Microsoft/azuredatastudio/issues/1814) 해결: sqlops.d.ts의 철자를 잘못 입력하면 암시적 ‘any’ 형식 정의가 발생함
- [이슈 1817](https://github.com/Microsoft/azuredatastudio/issues/1817) 해결: de Ortografia 오류
- [이슈 1830](https://github.com/Microsoft/azuredatastudio/issues/1830) 해결: component()를 호출한 후 ButtonComponent에서 iconPath를 설정할 경우 아이콘이 변경되지 않음
- [이슈 1843](https://github.com/Microsoft/azuredatastudio/issues/1843) 해결: 테이블 구성 개선

## <a name="june-2018"></a>2018년 6월

2018년 6월 20일 &nbsp; / &nbsp; 버전: 0.30.6 &nbsp; / &nbsp; 공개 미리 보기

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| **SQL Operations Studio용 SQL Server Profiler ‘미리 보기’** 확장 최초 릴리스 | &nbsp; |
| 새 **SQL Data Warehouse** 확장에는 데이터 웨어하우스에 대한 인사이트를 제공하는, 사용자 지정 가능한 다양한 기능의 대시보드 위젯이 포함되어 있음 | 이 확장을 통해 데이터 웨어하우스를 관리 및 튜닝하여 일관된 성능을 제공하도록 최적화하는 다양한 방법을 구현할 수 있습니다. |
| **데이터 편집 “필터링 및 정렬”** 지원 | &nbsp; |
| **SQL Operations Studio용 SQL Server 에이전트 ‘미리 보기’** 확장의 작업 및 작업 기록 뷰 개선 | &nbsp; |
| **마법사 및 대화 상자 UI 빌더 프레임워크** 확장성 API가 향상됨 | &nbsp; |
| VS Code 플랫폼 소스 코드가 업데이트됨 | 다음 릴리스가 통합되었습니다.<br/>&bull; &nbsp; [2018년 3월(1.22)](https://code.visualstudio.com/updates/v1_22)<br/>&bull; &nbsp; [2018년 4월(1.23)](https://code.visualstudio.com/updates/v1_23) |
| &nbsp; | &nbsp; |

### <a name="github-issues-fixes-june-2018"></a>GitHub 이슈 해결, 2018년 6월

- 기능 요청([이슈 1204](https://github.com/Microsoft/azuredatastudio/issues/1204)): 결과 그리드에서 열 너비가 데이터에 맞게 자동으로 조정되도록 하고, 동일한 쿼리를 다시 실행하는 경우 수동으로 변경해야 함
- [이슈 1398](https://github.com/Microsoft/azuredatastudio/issues/1398) 해결: 연결된 계정이 비어 있는 경우 추가 메시지와 계정 추가 단추를 표시해야 함
- [이슈 1399](https://github.com/Microsoft/azuredatastudio/issues/1399) 해결: 뷰를 축소하면 연결된 계정 탭이 손상됨
- [이슈 1374](https://github.com/Microsoft/azuredatastudio/issues/1374) 해결: 디스크에서 .sql 파일을 열 때 SQL Tools 서비스가 충돌함
- [이슈 1372](https://github.com/Microsoft/azuredatastudio/issues/1372) 해결: SQL 키워드 “BETWEEN”이 누락됨
- [이슈 1395](https://github.com/Microsoft/azuredatastudio/issues/1395) 해결: ‘MATCH’ 키워드가 SQL Tools 서비스와 충돌함
- [이슈 1496](https://github.com/Microsoft/azuredatastudio/issues/1496) 해결: 개체 탐색기의 “새 프로파일러” 상황에 맞는 메뉴 옵션을 선택해도 아무 작업도 수행되지 않음
- [이슈 1495](https://github.com/Microsoft/azuredatastudio/issues/1495) 해결: 쿼리 편집기 “설명” 쿼리 계획이 손상됨

## <a name="may-2018"></a>2018년 5월

2018년 5월 7일 &nbsp; / &nbsp; 버전: 0.29.3 &nbsp; / &nbsp; 공개 미리 보기

*5월 공개 미리 보기* 에서는 안정화 및 버그 수정에 중점을 둡니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 확장 관리자에서 사용할 수 있는 Redgate SQL Search 확장 발표 | &nbsp; |
| 10개 언어로 커뮤니티 지역화 제공 | 독일어, 스페인어, 프랑스어, 이탈리아어, 일본어, 한국어, 포르투갈어, 러시아어, 중국어 간체 및 중국어 번체 |
| 원격 분석 수집 변경 | &bull; &nbsp; 원격 분석 수집 감소됨<br/>&bull; &nbsp; 옵트아웃(opt out) 환경 개선<br/>&bull; &nbsp; 개인정보처리방침의 제품 내 링크 |
| 확장 관리자의 마켓플레이스 환경이 향상됨 | 커뮤니티 확장을 보다 쉽게 검색할 수 있습니다. |
| SQL 에이전트 확장 | &bull; &nbsp; 작업<br/>&bull; &nbsp; 작업 기록 뷰 개선 |
| whoisactive 및 서버 보고서 확장 업데이트 | &nbsp; |
| 대시보드 속성 관리의 스크롤 기능이 향상됨 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues"></a>GitHub 이슈 해결

- [이슈 703](https://github.com/Microsoft/azuredatastudio/issues/703) 해결: 데이터 편집에서 HTML과 유사한 텍스트를 입력하면 새로 고칠 때까지 값이 올바르게 표시되지 않음
- [이슈 821](https://github.com/Microsoft/azuredatastudio/issues/821) 해결: azuredatastudio.deb 패키지 종속성
- [이슈 1260](https://github.com/Microsoft/azuredatastudio/issues/1260) 해결: ‘distinct’ 키워드가 강조 표시되지 않음
- [이슈 1332](https://github.com/Microsoft/azuredatastudio/issues/1332) 해결: 데이터 편집의 행 되돌리기가 작동하지 않음
- [이슈 1215](https://github.com/Microsoft/azuredatastudio/issues/1215) 해결: SQL 에이전트 확장 및 상태 표시줄
- [이슈 1316](https://github.com/Microsoft/azuredatastudio/issues/1316) 해결: 창 크기 변경 후 SQL 에이전트 크기가 조정되지 않음

## <a name="april-2018"></a>2018년 4월

2018년 4월 25일 &nbsp; / &nbsp; 버전: 0.28.6 &nbsp; / &nbsp; 공개 미리 보기

*4월 공개 미리 보기* 에는 버그 수정 및 개선 사항이 포함되었습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| SQL 에이전트 미리 보기 확장 기능 개선: | &nbsp; |
| &nbsp; &nbsp; &nbsp; 파일 지원 개선 | &bull; &nbsp; 큰 파일<br/>&bull; &nbsp; 관리자 권한으로 보호된 파일을 저장하기 위한 보호된 파일<br/>&bull; &nbsp; SQL Operations Studio에서 256M보다 큰 파일 저장 |
| &nbsp; &nbsp; &nbsp; 통합 터미널 분할 | 동시에 여러 개의 열린 터미널에서 작업합니다. |
| &nbsp; &nbsp; &nbsp; 더 빨라진 설치 및 시작 시간 | 디스크에 있는 파일 수의 설치 공간을 줄였습니다. |
| &nbsp; | &nbsp; |

### <a name="fix-github-issues-april-2018"></a>GitHub 이슈 해결, 2018년 4월

- [이슈 37](https://github.com/Microsoft/azuredatastudio/issues/37) 해결: 차트 뷰어에서 오류가 발생하면 예기치 않은 동작이 수행됨
- [이슈 462](https://github.com/Microsoft/azuredatastudio/issues/462) 해결: 기능 요청: 서버 그룹 옵션이 기본적으로 펼쳐져야 함
- [이슈 606](https://github.com/Microsoft/azuredatastudio/issues/606) 해결: intellisense - ‘update’ 명령에 대해 잘못된 제안이 표시됨
- [이슈 967](https://github.com/Microsoft/azuredatastudio/issues/967) 해결: 결과 그리드에서 XML 실행 계획을 선택하는 경우 쿼리 계획이 표시됨
- [이슈 1023](https://github.com/Microsoft/azuredatastudio/issues/1023) 해결: flyfishingdba의 ms_foreachdb 호출에 대해 대괄호 추가
- [이슈 1048](https://github.com/Microsoft/azuredatastudio/issues/1048) 해결: 사전 로그인 SSL/TLS 핸드셰이크 오류
- [이슈 1050](https://github.com/Microsoft/azuredatastudio/issues/1050) 해결: 오류를 표시하기 전에 인사이트 뷰가 지워짐
- [이슈 1057](https://github.com/Microsoft/azuredatastudio/issues/1057) 해결: 탐색기 위젯의 복원 및 새 쿼리 작업이 손상됨
- [이슈 1068](https://github.com/Microsoft/azuredatastudio/issues/1068) 해결: 대시보드 출력 창에 Azure SQL Database에 대한 오류 메시지가 팝업됨
- [이슈 1069](https://github.com/Microsoft/azuredatastudio/issues/1069) 해결: 처음 표시할 때 연결 대화 상자에 서버 필요 오류가 표시됨
- [이슈 1070](https://github.com/Microsoft/azuredatastudio/issues/1070) 해결: 이제 서버 그룹을 펼치려면 두 번 클릭해야 함
- [이슈 1072](https://github.com/Microsoft/azuredatastudio/issues/1072) 해결: 선택 컨트롤 배경이 반투명하게 표시됨
- [이슈 1115](https://github.com/Microsoft/azuredatastudio/issues/1115) 해결: SQL Operations Studio의 모든 고대비 접근성 문제 해결
- [이슈 1101](https://github.com/Microsoft/azuredatastudio/issues/1101) 해결: 확장 업그레이드에 실패하면 “수동으로 다운로드” 링크가 잘못된 위치로 연결됨
- [이슈 1103](https://github.com/Microsoft/azuredatastudio/issues/1103) 해결: 홈 탭에서 세로 스크롤이 작동하지 않음
- [이슈 1104](https://github.com/Microsoft/azuredatastudio/issues/1104) 해결: SQL 확장 탭의 작동이 중지됨

### <a name="visual-studio-code-121-platform"></a>Visual Studio Code 1.21 플랫폼

4월 공개 미리 보기에서는 주로 Visual Studio Code 1.21 플랫폼의 소스 코드를 새로 고쳤습니다. 이 새로 고침을 통해 핵심 편집기 및 워크벤치가 이전 1.19 동기화 지점에서 일부 업데이트되었습니다. 몇 가지 예는 다음과 같습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| [새 알림 UI](https://code.visualstudio.com/updates/v1_21#_new-notifications-ui) | SQL Operations Studio 알림을 쉽게 관리하고 검토합니다. |
| [통합 터미널 분할](https://code.visualstudio.com/updates/v1_21#_split-terminals) | 한 번에 여러 개의 열린 터미널에서 작업합니다. |
| [보호된 큰 파일 저장](https://code.visualstudio.com/updates/v1_20#_save-files-that-need-admin-privileges) | SQL Operations Studio에서 관리자 권한으로 보호된 256M보다 큰 파일을 저장합니다. |
| [향상된 큰 파일 지원](https://code.visualstudio.com/updates/v1_21#_text-buffer-improvements) | 큰 파일을 위해 텍스트 버퍼 최적화가 지원됩니다. |
| [향상된 설정 검색 기능](https://code.visualstudio.com/updates/v1_20#_settings-search) | 자연어 검색을 사용하여 적절한 설정을 쉽게 찾습니다. |
| [전역 코드 조각](https://code.visualstudio.com/updates/v1_20#_global-snippets) | 모든 파일 형식에서 사용할 수 있는 코드 조각을 만듭니다. |
| [탐색기 다중 선택](https://code.visualstudio.com/updates/v1_20#_multi-select-in-the-explorer) | 한 번에 여러 파일에 대해 작업을 수행합니다. |
| [탐색기의 오류 및 경고](https://code.visualstudio.com/updates/v1_20#_error-indicators-in-the-explorer) | 코드베이스에서 오류로 빠르게 이동합니다. |
| [창 간에 복사하여 붙여넣기, 끌어서 놓기](https://code.visualstudio.com/updates/v1_21#_better-drag-and-drop-support) | 열려 있는 SQL Operations Studio 창 간에 파일을 이동합니다. |
| [Git 하위 모듈 지원](https://code.visualstudio.com/updates/v1_20#_git-submodules) | 중첩된 Git 리포지토리에서 Git 작업을 수행합니다. |
| [터미널 화면 판독기 지원](https://code.visualstudio.com/updates/v1_20#_screen-reader-support) | 이제 통합 터미널에 **화면 판독기 최적화** 모드가 제공됩니다. |
| [가운데 맞춤 편집기 레이아웃](https://code.visualstudio.com/updates/v1_21#_centered-editor-layout) | 코드 보기 화면 공간을 최대화합니다. |
| [가로 검색 결과(미리 보기)](https://code.visualstudio.com/updates/v1_21#_horizontal-search). | 이제 가로 패널에서 검색 결과를 볼 수 있습니다. |
| &nbsp; | &nbsp; |

자세한 내용은 [Visual Studio Code 2월 릴리스 정보](https://code.visualstudio.com/updates/v1_21) 및 [Visual Studio Code 1월 릴리스 정보](https://code.visualstudio.com/updates/v1_20)를 확인하세요.

자세한 내용은 [변경 로그](https://github.com/Microsoft/azuredatastudio/blob/main/CHANGELOG.md)를 참조하세요.

## <a name="march-2018"></a>2018년 3월

2018년 3월 28일 &nbsp; / &nbsp; 버전: 0.27.3 &nbsp; / &nbsp; 공개 미리 보기

*3월 공개 미리 보기* 에서는 자주 발생하는 GitHub 이슈를 해결하고 확장성을 개선하는 데 중점을 둡니다. 특히 확장 관리자를 사용하도록 설정하고, 대시보드 관리를 개선하며, SQL 에이전트 및 인사이트 확장을 제공합니다. 이 릴리스에는 다음과 같은 개선 사항이 포함되어 있습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 탭 인사이트 및 구성 창을 지원하도록 대시보드 확장성 모델 개선 | 확장 관리자를 사용하여 확장을 간단하게 가져올 수 있습니다.<br/><br/>[whoisactive.com](http://www.whoisactive.com)의 sp\_whoisactive용 대시보드 확장이 제공됩니다.<br/><br/>자세한 내용은 [SQL Operations Studio 기능 확장](./extensions/add-extensions.md)을 참조하세요. |
| [연결 및 개체 탐색기 관리를 위한 확장성 API](https://github.com/Microsoft/azuredatastudio/wiki/Extensibility-API) 추가 | &nbsp; |
| 고객에게 영향을 미치는 중요한 [GitHub 이슈](https://github.com/Microsoft/azuredatastudio/issues) 해결 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="february-2018"></a>2018년 2월

2018년 2월 15일 &nbsp; / &nbsp; 버전: 0.26.7 &nbsp; / &nbsp; 공개 미리 보기

*2월 공개 미리 보기* 에는 몇 가지 기능 제안과 높은 우선 순위의 버그 수정이 포함되었습니다. 이 릴리스에는 다음과 같은 개선 사항이 포함되어 있습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 새 릴리스를 다운로드할 수 있는 경우 알림을 제공하는 자동 업데이트 설치 도입 | &nbsp; |
| 연결 대화 상자 **데이터베이스** 필드가 이제 지정된 서버에서 채워진 데이터베이스 목록을 포함하는 동적으로 채워진 드롭다운 목록으로 제공됨 | &nbsp; |
| 연결 확장성 API 도입 | &nbsp; |
| VS 코드 편집기 1.19 통합 | &nbsp; |
| 몇 가지 향상된 쿼리 계획 뷰어 기능을 도입하기 위해 JustinPealing/html-query-plan 구성 요소 업데이트 | &nbsp; |
| &nbsp; | &nbsp; |

### <a name="fixed-issues-february-2018"></a>해결된 문제, 2018년 2월

- [이슈 6](https://github.com/Microsoft/azuredatastudio/issues/6) 해결: 새 쿼리 탭을 열 때 연결 및 선택한 데이터베이스 유지
- [이슈 22](https://github.com/Microsoft/azuredatastudio/issues/22) 해결: ‘서버 이름’ 및 ‘데이터베이스 이름' - 이러한 항목을 텍스트 상자 대신 드롭다운으로 표시될 수 있나요?
- [이슈 549](https://github.com/Microsoft/azuredatastudio/issues/549) 해결: 자동 설치를 수행하면 설치 후에 애플리케이션이 열림
- [이슈 481](https://github.com/Microsoft/azuredatastudio/issues/481) 해결: “업데이트 확인” 옵션 추가
- SQL 편집기 색 지정 및 자동 완성 수정:
  - [이슈 584](https://github.com/Microsoft/azuredatastudio/issues/584) 해결: “FULL” 키워드가 IntelliSense에서 강조 표시되지 않음
  - [이슈 345](https://github.com/Microsoft/azuredatastudio/issues/345) 해결: 편집기 내에서 SQL 함수에 색 지정
  - [이슈 300](https://github.com/Microsoft/azuredatastudio/issues/300) 해결: [#tempData] 최신 “]”가 녹색으로 표시됨
  - [이슈 225](https://github.com/Microsoft/azuredatastudio/issues/225) 해결: 키워드 색이 일치하지 않음
  - [이슈 60](https://github.com/Microsoft/azuredatastudio/issues/60) 해결: from 절에 임시 테이블을 사용하는 경우 SQL 구문 색 강조 표시가 잘못됨

## <a name="january-2018"></a>2018년 1월

2018년 1월 17일 &nbsp; / &nbsp; 버전: 0.25.4 &nbsp; / &nbsp; 공개 미리 보기

*1월 공개 미리 보기* 에는 몇 가지 기능 제안과 높은 우선 순위의 버그 수정이 포함되었습니다. 이 릴리스에는 다음과 같은 개선 사항이 포함되어 있습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 연결 대화 상자에서 저장된 서버 연결을 사용할 수 있음 | &nbsp; |
| Hot Exit 사용. Hot Exit는 기본적으로 해제됩니다. 사용하도록 설정하는 방법은 [Hot Exit 설정](settings.md#hot-exit)을 참조하세요. | &nbsp; |
| 서버 그룹 기반의 탭 색 지정 탭 색 지정은 기본적으로 해제됩니다. 사용하도록 설정하는 방법은 [탭 색 설정](settings.md#tab-color)을 참조하세요. | &nbsp; |
| 연결 대화 상자에서 ‘서버 이름’을 ‘서버’로 변경 | &nbsp; |
| 손상된 ‘현재 쿼리 실행’ 명령 수정 | &nbsp; |
| 끌어서 놓기 중단 스크립팅 버그 수정 | &nbsp; |
| 잘못된 고정된 시작 메뉴 아이콘 수정 | &nbsp; |
| 누락된 Azure 계정 브랜딩 아이콘 수정 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="december-2017"></a>2017년 12월

2017년 12월 19일 &nbsp; / &nbsp; 버전: 0.24.1 &nbsp; / &nbsp; 공개 미리 보기

*12월 공개 미리 보기* 에는 다음과 같은 개선 사항뿐만 아니라 모든 기능 영역의 여러 버그 수정이 포함되었습니다.

&nbsp;

| 변경 | 세부 정보 |
| :----- | :------ |
| 이제 방화벽 규칙 만들기 대화 상자를 사용하여 Azure SQL Database 및 Azure Synapse Analytics에 연결할 수 있습니다. | &nbsp; |
| Windows 설치 프로그램과 Linux DEB 및 RPM 설치 패키지가 추가됨 | &nbsp; |
| 대시보드 관리 시각적 레이아웃 편집기 | &nbsp; |
| ‘Alter로 스크립트’ 및 ‘Execute로 스크립트’ 명령 | &nbsp; |
| ‘실제 계획을 사용하여 현재 쿼리 실행’ 명령 | &nbsp; |
| VS Code 1.18.1 편집기 플랫폼 통합 | &nbsp; |
| VSIX 확장 파일의 사이드로드 사용 | &nbsp; |
| “GO N” 일괄 처리 반복 구문 지원 | &nbsp; |
| &nbsp; | &nbsp; |

## <a name="november-2017"></a>2017년 11월

2017년 11월 15일 &nbsp; / &nbsp; 버전: 0.23.6

- Azure Data Studio의 초기 릴리스입니다.

## <a name="next-steps"></a>다음 단계

시작하려면 다음 빠른 시작 중 하나를 참조하세요.

- [SQL Server 연결 및 쿼리](quickstart-sql-server.md)
- [Azure SQL Database 연결 및 쿼리](quickstart-sql-database.md)
- [Azure Synapse Analytics 연결 및 쿼리](quickstart-sql-dw.md)

Azure Data Studio에 참여:

- [https://github.com/Microsoft/azuredatastudio](https://github.com/Microsoft/azuredatastudio)
