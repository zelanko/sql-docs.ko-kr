---
title: SSMS에서 사용자 지정 보고서를 사용 하 여 Python 및 R 스크립트 실행 모니터링
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 549cdcd35b939b2247b14817271e3d1063fab1e0
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714397"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>SQL Server Management Studio에서 사용자 지정 보고서를 사용 하 여 Python 및 R 스크립트 실행 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SSMS (SQL Server Management Studio)의 사용자 지정 보고서를 사용 하 여 외부 스크립트 (Python 및 R)의 실행을 모니터링 하 고, 사용 되는 리소스, 문제를 진단 하 고, SQL Server Machine Learning Services에서 성능을 조정 합니다.

이러한 보고서에서 다음과 같은 세부 정보를 볼 수 있습니다.

- 활성 Python 또는 R 세션
- 인스턴스에 대 한 구성 설정
- Machine learning 작업에 대 한 실행 통계
- R Services에 대 한 확장 이벤트
- 현재 인스턴스에 설치 된 Python 또는 R 패키지

이 문서에서는 SQL Server Machine Learning Services에 제공 된 사용자 지정 보고서를 설치 하 고 사용 하는 방법을 설명 합니다.

SQL Server Management Studio의 보고서에 대 한 자세한 내용은 [Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)를 참조 하세요.

## <a name="how-to-install-the-reports"></a>보고서를 설치하는 방법

보고서는 SQL Server Reporting Services를 사용 하 여 디자인 되었지만 SQL Server Management Studio에서 직접 사용할 수 있습니다. SQL Server 인스턴스에 Reporting Services를 설치할 필요가 없습니다.

이러한 보고서를 사용 하려면 다음 단계를 수행 합니다.

1. GitHub에서 SQL Server Machine Learning Services 용 [SSMS 사용자 지정 보고서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) 를 다운로드 합니다.

2. Management Studio에 보고서 복사

    1. SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더를 찾습니다. 기본적으로 사용자 지정 보고서는이 폴더에 저장 됩니다. 여기서 **user_name** 은 Windows 사용자 이름입니다.

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       다른 폴더를 지정 하거나 하위 폴더를 만들 수도 있습니다.

    2. *를 복사 합니다. 사용자 지정 보고서 폴더에 다운로드 한 RDL 파일입니다.

3. Management Studio에서 보고서를 실행 합니다.

    1. 보고서를 실행할 인스턴스의 **데이터베이스** 노드를 Management Studio에서 마우스 오른쪽 단추로 클릭합니다.

    2. **보고서**를 클릭하고 **사용자 지정 보고서**를 클릭합니다.

    3. **파일 열기** 대화 상자에서 사용자 지정 보고서 폴더를 찾습니다.

    4. 다운로드한 RDL 파일 중 하나를 선택한 다음 **열기**를 클릭합니다.

## <a name="reports"></a>보고서

[GitHub의 SSMS 사용자 지정 보고서 리포지토리에](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports) 는 다음 보고서가 포함 되어 있습니다.

| 보고서 | 설명 |
|-|-|
| Active Sessions | 현재 SQL Server 인스턴스에 연결 되어 있고 Python 또는 R 스크립트를 실행 하는 사용자입니다. |
| Configuration | Python 또는 R 런타임의 Machine Learning Services 및 속성 설치 설정입니다. |
| 인스턴스 구성 | Machine Learning Services를 구성 합니다. |
| 실행 통계 | Machine Learning services의 실행 통계입니다. 예를 들어 총 외부 스크립트 실행 수와 병렬 실행 수를 가져올 수 있습니다. |
| 확장 이벤트 | 외부 스크립트 실행에 대 한 자세한 정보를 얻기 위해 사용할 수 있는 확장 이벤트입니다. |
| 패키지 | SQL Server 인스턴스에 설치 된 R 또는 Python 패키지와 버전, 이름 등의 속성을 나열 합니다. |
| Resource Usage | CPU, 메모리, IO 사용 SQL Server 및 외부 스크립트 실행을 확인 합니다. 외부 리소스 풀의 메모리 설정을 볼 수도 있습니다. |

## <a name="next-steps"></a>다음 단계

- [Dmv (동적 관리 뷰)를 사용 하 여 SQL Server Machine Learning Services 모니터링](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [R Services에 대한 확장된 이벤트](../r/extended-events-for-sql-server-r-services.md)
