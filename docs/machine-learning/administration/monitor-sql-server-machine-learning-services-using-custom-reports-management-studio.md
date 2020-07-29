---
title: 사용자 지정 보고서를 사용하여 스크립트 모니터링
description: SSMS(SQL Server Management Studio)의 사용자 지정 보고서를 사용하여 외부 스크립트(Python 및 R)의 실행, 사용된 리소스, 문제 진단 및 SQL Server Machine Learning Services의 성능 조정을 모니터링합니다.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 09/17/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 708d805ff810876ba5871b2e1e887dd97aceba3a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85659624"
---
# <a name="monitor-python-and-r-script-execution-using-custom-reports-in-sql-server-management-studio"></a>SQL Server Management Studio에서 사용자 지정 보고서를 사용하여 Python 및 R 스크립트 실행 모니터링
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

SSMS(SQL Server Management Studio)의 사용자 지정 보고서를 사용하여 외부 스크립트(Python 및 R)의 실행, 사용된 리소스, 문제 진단 및 SQL Server Machine Learning Services의 성능 조정을 모니터링합니다.

이러한 보고서에서 다음과 같은 세부 정보를 볼 수 있습니다.

- 활성 Python 또는 R 세션
- 인스턴스에 대한 구성 설정
- 기계 학습 작업에 대한 실행 통계
- R Services에 대한 확장 이벤트
- 현재 인스턴스에 설치된 Python 또는 R 패키지

이 문서에서는 SQL Server Machine Learning Services에 제공된 사용자 지정 보고서를 설치하고 사용하는 방법을 설명합니다.

SQL Server Management Studio의 보고서에 대한 자세한 내용은 [Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)를 참조하세요.

## <a name="how-to-install-the-reports"></a>보고서를 설치하는 방법

보고서는 SQL Server Reporting Services를 사용하여 설계되었지만 SQL Server Management Studio에서 직접 사용할 수 있습니다. SQL Server 인스턴스에 Reporting Services를 설치할 필요가 없습니다.

이러한 보고서를 사용하려면 다음 단계를 수행합니다.

1. GitHub에서 SQL Server Machine Learning Services에 대한 [SSMS 사용자 지정 보고서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)를 다운로드합니다.

2. Management Studio에 보고서 복사

    1. SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더를 찾습니다. 기본적으로 사용자 지정 보고서는이 폴더에 저장됩니다(여기서 **user_name**은 Windows 사용자 이름임).

        `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

       다른 폴더를 지정하거나 하위 폴더를 만들 수도 있습니다.

    2. 다운로드한 *.RDL 파일을 사용자 지정 보고서 폴더에 복사합니다.

3. Management Studio에서 보고서 실행

    1. 보고서를 실행할 인스턴스의 **데이터베이스** 노드를 Management Studio에서 마우스 오른쪽 단추로 클릭합니다.

    2. **보고서**를 클릭하고 **사용자 지정 보고서**를 클릭합니다.

    3. **파일 열기** 대화 상자에서 사용자 지정 보고서 폴더를 찾습니다.

    4. 다운로드한 RDL 파일 중 하나를 선택한 다음 **열기**를 클릭합니다.

## <a name="reports"></a>보고서

[GitHub의 SSMS 사용자 지정 보고서 리포지토리](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)에는 다음 보고서가 포함되어 있습니다.

| 보고서 | Description |
|-|-|
| Active Sessions | 현재 SQL 인스턴스에 현재 연결되어 있고 Python 또는 R 스크립트를 실행 중인 사용자입니다. |
| 구성 | Machine Learning Services의 설치 설정 및 Python 또는 R 런타임의 속성입니다. |
| 인스턴스 구성 | Machine Learning Services를 구성합니다. |
| 실행 통계 | Machine Learning Services의 실행 통계입니다. 예를 들어 총 외부 스크립트 실행 수와 병렬 실행 수를 가져올 수 있습니다. |
| 확장 이벤트 | 외부 스크립트 실행에 대한 자세한 인사이트를 가져오는 데 사용할 수 있는 확장 이벤트입니다. |
| 패키지 | SQL Server 인스턴스에 설치된 R 또는 Python 패키지와 버전 및 이름 등의 속성을 나열합니다. |
| Resource Usage | SQL Server의 CPU, 메모리, IO 사용량 및 외부 스크립트 실행을 확인합니다. 외부 리소스 풀에 대한 메모리 설정도 볼 수 있습니다. |

## <a name="next-steps"></a>다음 단계

- [DMV(동적 관리 뷰)를 사용하여 SQL Server Machine Learning Services 모니터링](monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)
- [SQL Server Machine Learning Services에서 확장 이벤트를 사용하여 Python 및 R 스크립트 모니터링](extended-events.md)
