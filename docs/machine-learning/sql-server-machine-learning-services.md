---
title: SQL Server Machine Learning Services(Python 및 R)이란?
titleSuffix: ''
description: Machine Learning Services는 관계형 데이터를 사용하여 Python 및 R 스크립트를 실행할 수 있는 기능을 제공하는 SQL Server의 기능입니다. 예측 분석 및 기계 학습에 오픈 소스 패키지와 프레임워크, Microsoft Python과 R 패키지를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동하지 않고 데이터베이스 내에서 실행됩니다. 이 문서에서는 SQL Server Machine Learning Services의 기본 사항 및 시작하는 방법에 대해 설명합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 11/10/2020
ms.topic: overview
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2017||>=sql-server-linux-ver15||=azuresqldb-mi-current'
ms.openlocfilehash: b73b8521593b81e38d5b0b3931da793f943c45a0
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97470694"
---
# <a name="what-is-sql-server-machine-learning-services-with-python-and-r"></a>Python 및 R을 사용하는 SQL Server Machine Learning Services란?
[!INCLUDE [SQL Server 2017 SQL MI](../includes/applies-to-version/sqlserver2017-asdbmi.md)]

Machine Learning Services는 관계형 데이터를 사용하여 Python 및 R 스크립트를 실행할 수 있는 기능을 제공하는 SQL Server의 기능입니다. 예측 분석 및 기계 학습에 오픈 소스 패키지와 프레임워크, [Microsoft Python과 R 패키지](#packages)를 사용할 수 있습니다. 스크립트는 SQL Server 외부에서 또는 네트워크를 통해 데이터를 이동하지 않고 데이터베이스 내에서 실행됩니다. 이 문서에서는 SQL Server Machine Learning Services의 기본 사항 및 시작하는 방법에 대해 설명합니다.

다른 SQL 플랫폼의 기계 학습에 대한 내용은 [SQL 기계 학습 설명서](index.yml)를 참조하세요.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
> [!NOTE]
> SQL Server에서 Java를 실행하는 방법은 [Java 언어 확장 설명서](../language-extensions/java-overview.md)를 참조하세요.
::: moniker-end

## <a name="execute-python-and-r-scripts-in-sql-server"></a>SQL Server에서 Python 및 R 스크립트 실행

SQL Server Machine Learning Services를 사용하여 데이터베이스에서 Python 또는 R 스크립트를 실행할 수 있습니다. 이를 사용하여 데이터를 준비 및 정리하고, 기능 엔지니어링을 수행하고, 데이터베이스 내에서 기계 학습 모델을 학습, 평가 및 배포할 수 있습니다. 이 기능은 데이터가 상주하는 스크립트를 실행하고 네트워크를 통해 다른 서버에 데이터를 전송하는 작업을 제거합니다.

SQL Server 인스턴스에서 저장 프로시저 [sp_execute_external_script](../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)를 사용하여 Python 및 R 스크립트를 실행할 수 있습니다.

Python 및 R의 기본 배포판은 Machine Learning Services에 포함되어 있습니다. Microsoft 패키지 외에도 PyTorch, TensorFlow, scikit-learn 같은 오픈 소스 패키지 및 프레임워크를 설치하여 사용할 수 있습니다.

Machine Learning Services는 확장성 프레임워크를 사용하여 SQL Server에서 Python 및 R 스크립트를 실행합니다. 다음에서 이 작업을 수행하는 방법을 자세히 알아보세요.

+ [확장성 프레임워크](concepts/extensibility-framework.md)
+ [Python 확장](concepts/extension-python.md)
+ [R 확장](concepts/extension-r.md)

## <a name="get-started-with-machine-learning-services"></a>Machine Learning Services 시작

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
1. [Linux](../linux/sql-server-linux-setup-machine-learning.md?toc=/sql/machine-learning/toc.json) 또는 [Windows에 SQL Server Machine Learning Services를 설치합니다](install/sql-machine-learning-services-windows-install.md). [빅 데이터 클러스터의 Machine Learning Services](../big-data-cluster/machine-learning-services.md) 및 [Azure SQL Managed Instance의 Machine Learning Services](/azure/azure-sql/managed-instance/machine-learning-services-overview)를 사용할 수도 있습니다.

1. 개발 도구 구성. [Azure Data Studio Notebook에서 Python 및 R 스크립트를 실행](install/sql-machine-learning-azure-data-studio.md)할 수 있습니다. 또한 [Azure Data Studio](../azure-data-studio/what-is.md)에서 T-SQL을 실행할 수 있습니다.

1. 첫 번째 Python 또는 R 스크립트를 작성합니다.

   + [SQL 기계 학습용 Python 자습서](tutorials/python-tutorials.md)
   + [SQL 기계 학습용 R 자습서](tutorials/r-tutorials.md)
::: moniker-end

::: moniker range="=azuresqldb-mi-current"
+ 첫 번째 Python 또는 R 스크립트를 작성합니다.

   + [SQL 기계 학습용 Python 자습서](tutorials/python-tutorials.md)
   + [SQL 기계 학습용 R 자습서](tutorials/r-tutorials.md)
::: moniker-end

::: moniker range="=sql-server-2017"
1. [Windows에 SQL Server Machine Learning Services 설치](install/sql-machine-learning-services-windows-install.md)

1. 개발 도구 구성. [Azure Data Studio Notebook에서 Python 및 R 스크립트를 실행](install/sql-machine-learning-azure-data-studio.md)할 수 있습니다. [Azure Data Studio](../azure-data-studio/what-is.md)에서 T-SQL을 사용할 수도 있습니다.

1. 첫 번째 Python 또는 R 스크립트를 작성합니다.

   + [SQL 기계 학습용 Python 자습서](tutorials/python-tutorials.md)
   + [SQL 기계 학습용 R 자습서](tutorials/r-tutorials.md)
::: moniker-end

<a name="versions"></a>

## <a name="python-and-r-versions"></a>Python 및 R 버전

다음은 Machine Learning Services에 포함된 Python 및 R 버전 목록입니다.

| SQL Server 버전 | Python 버전 | R 버전 |
|-|-|-|
| SQL Server 2017 | 3.5.2 | 3.3.3 |
| SQL Server 2019 | 3.7.3 | 3.5.2 |

SQL Server 2016의 R 버전에 대한 자세한 내용은 [R Services란?의 R 버전 섹션](r/sql-server-r-services.md?view=sql-server-2016&preserve-view=true#version)을 참조하세요.

<a name="packages"></a>

## <a name="python-and-r-packages"></a>Python 및 R 패키지

Microsoft의 엔터프라이즈 패키지 외에도 오픈 소스 패키지 및 프레임워크를 사용할 수 있습니다. 가장 일반적인 오픈 소스 Python 및 R 패키지는 Machine Learning Services에 미리 설치되어 있습니다. Microsoft의 다음 Python 및 R 패키지도 포함되어 있습니다.

| 언어 | 패키지 | Description |
|-|-|-|
| Python | [revoscalepy](python/ref-py-revoscalepy.md) | 확장 가능한 Python의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링에 사용됩니다. 또한 이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 워크로드를 자동으로 분산합니다. |
| Python | [microsoftml](python/ref-py-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다. | 
| R | [RevoScaleR](r/ref-r-revoscaler.md) | 확장 가능한 R의 기본 패키지입니다. 데이터 변환 및 조작, 통계 요약, 시각화 및 많은 형식의 모델링에 사용됩니다. 또한 이 패키지의 함수는 병렬 처리를 위해 사용 가능한 코어 간에 워크로드를 자동으로 분산합니다. |
| R | [MicrosoftML(R)](r/ref-r-microsoftml.md) | 텍스트 분석, 이미지 분석 및 감정 분석을 위한 사용자 지정 모델을 만들기 위한 기계 학습 알고리즘을 추가합니다. |
| R | [olapR](r/ref-r-olapr.md) | SQL Server Analysis Services OLAP 큐브에 대한 MDX 쿼리에 사용되는 R 함수입니다. |
| R | [sqlrutils](r/ref-r-sqlrutils.md) | T-SQL 저장 프로시저에서 R 스크립트를 사용하고, 데이터베이스에 해당 저장 프로시저를 등록하고, [R 개발 환경](r/set-up-a-data-science-client.md)에서 저장 프로시저를 실행하는 메커니즘입니다. |
| R | [Microsoft R Open](https://mran.microsoft.com/rro) | MRO(Microsoft R Open)는 Microsoft에서 출시한 R의 고급 배포판입니다. 통계 분석 및 데이터 과학을 위한 완전한 오픈 소스 플랫폼입니다. R을 기준으로 하고 R과 100% 호환되며, 향상된 성능 및 재현 가능성을 위한 추가 기능을 포함합니다. |

Machine Learning Services와 함께 설치되는 패키지와 기타 패키지를 설치하는 방법에 대한 자세한 내용은 다음을 참조하세요.

::: moniker range=">=sql-server-ver15||>=sql-server-linux-ver15"
+ [Python 패키지 정보 가져오기](package-management/python-package-information.md)
+ [sqlmlutils를 사용하여 Python 패키지 설치](package-management/install-additional-python-packages-on-sql-server.md)
+ [R 패키지 정보 가져오기](package-management/r-package-information.md)
+ [sqlmlutils를 사용하여 새 R 패키지 설치](package-management/install-additional-r-packages-on-sql-server.md)
::: moniker-end
::: moniker range="=sql-server-2017"
+ [Python 패키지 정보 가져오기](package-management/python-package-information.md)
+ [SQL Server에서 Python 도구를 사용하여 패키지 설치](package-management/install-python-packages-standard-tools.md)
+ [R 패키지 정보 가져오기](package-management/r-package-information.md)
+ [T-SQL(CREATE EXTERNAL LIBRARY)을 사용하여 SQL Server에 R 패키지 설치](package-management/install-r-packages-with-tsql.md)
::: moniker-end

## <a name="next-steps"></a>다음 단계

+ [Windows에 SQL Server Machine Learning Services 설치](install/sql-machine-learning-services-windows-install.md) 또는 [Linux에 SQL Server Machine Learning Services 설치](../linux/sql-server-linux-setup-machine-learning.md?toc=/sql/machine-learning/toc.json)
+ [SQL 기계 학습용 Python 자습서](tutorials/python-tutorials.md)
+ [SQL 기계 학습용 R 자습서](tutorials/r-tutorials.md)
