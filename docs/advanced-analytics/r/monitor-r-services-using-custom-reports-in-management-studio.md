---
title: Management Studio-SQL Server Machine Learning Services에서에서 사용자 지정 보고서를 사용 하 여 R Services 모니터링
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 55fcb4e145481f98b0cba065ddab75e7cfa0a538
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62641983"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>Management Studio에서 사용자 지정 보고서를 사용하여 Machine Learning Services 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

기계 학습에 사용 되는 인스턴스 관리를 쉽게 제품 팀은 여러 SQL Server Management Studio에 추가할 수 있는 샘플 사용자 지정 보고서를 제공 했습니다. 이러한 보고서에서와 같은 세부 정보를 볼 수 있습니다.

- 현재 R 또는 Python 세션
- 인스턴스에 대 한 구성 설정
- Machine learning 작업에 대 한 실행 통계
- R Services에 대 한 확장된 이벤트
- 현재 인스턴스에 설치 된 R 또는 Python 패키지

이 문서는 설치 컴퓨터 leaerning 위해 특별히 제공 되는 사용자 지정 보고서를 사용 하는 방법을 설명 합니다. 

Management Studio의 보고서에 대 한 일반 소개를 참조 하세요 [Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)합니다.

## <a name="how-to-install-the-reports"></a>보고서를 설치하는 방법

보고서는 SQL Server Reporting Services를 사용하여 만듭니다. 하지만 Reporting Services가 인스턴스에서 설치되어 있지 않더라도 SQL Server Management Studio에서 바로 보고서를 사용할 수도 있습니다. 

이러한 보고서를 사용하려면:

* SQL Server 제품 샘플용 GitHub 리포지토리에서 RDL 파일을 다운로드합니다.
* SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더에 파일을 추가합니다.
* SQL Server Management Studio에서 보고서를 엽니다.


### <a name="step-1-download-the-reports"></a>1단계. 보고서 다운로드

1. 포함 된 GitHub 리포지토리를 엽니다 [SQL Server 제품 샘플](https://github.com/Microsoft/sql-server-samples), 예제 보고서를 다운로드 합니다. 

    + [SSMS 사용자 지정 보고서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > SQL Server 2017 때문 Learning Services 또는 SQL Server 2016 R Services를 사용 하 여 보고서를 사용할 수 있습니다.

2. 샘플을 다운로드하려면 GitHub에 로그인하고 샘플의 로컬 분기를 만들면 됩니다. 

### <a name="step-2-copy-the-reports-to-management-studio"></a>2단계. Management Studio에 보고서 복사

3. SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더를 찾습니다. 기본적으로 사용자 지정 보고서는 이 폴더에 저장됩니다.
    
   `C:\Users\user_name\Documents\SQL Server Management Studio\Custom Reports`

   그러나 다른 폴더를 지정하거나 하위 폴더를 만들 수 있습니다.

4. *.RDL 파일을 사용자 지정 보고서 폴더에 복사합니다.


### <a name="step-3-run-the-reports"></a>3단계. 보고서 실행

5. 보고서를 실행할 인스턴스의 **데이터베이스** 노드를 Management Studio에서 마우스 오른쪽 단추로 클릭합니다.
6. **보고서**를 클릭하고 **사용자 지정 보고서**를 클릭합니다.
7. **파일 열기** 대화 상자에서 사용자 지정 보고서 폴더를 찾습니다.
8. 다운로드한 RDL 파일 중 하나를 선택한 다음 **열기**를 클릭합니다.

> [!IMPORTANT]
> 일부 컴퓨터에서는 이러한 보고서를 사용할 수 없습니다. 예를 들면 DPI가 높거나 해상도가 1080p보다 큰 디스플레이 디바이스가 있는 컴퓨터입니다. SSMS의 보고서 뷰어 컨트롤에는 보고서와 충돌하는 버그가 있습니다.

## <a name="report-list"></a>보고서 목록

GitHub의 제품 샘플 리포지토리에 다음과 같은 보고서를 현재 포함 되어 있습니다.

+ **R Services - 활성 세션**

  SQL Server 인스턴스 및 작업을 학습 하는 실행 중인 컴퓨터에 현재 연결 되어 있는 사용자를 보려면이 보고서를 사용 합니다. 
  
+ **R Services - 구성**

  외부 스크립트 런타임 및 관련된 서비스의 구성을 보려면이 보고서를 사용 합니다. 보고서는 다시 시작이 필요한지 표시하고 필요한 네트워크 프로토콜을 확인합니다. 
  
  묵시적 인증이 SQL Server 계산 컨텍스트로 실행 되는 기계 학습 작업에 대 한 필요 합니다. 묵시적된 인증이 구성 된를 확인 하려면 보고서 그룹 SQLRUserGroup에 대 한 데이터베이스 로그인이 있는지 확인 합니다.

 + **R Services - 인스턴스 구성** 

   이 보고서 기계를 구성 하는 데 도움이 됩니다. 또한 이전 보고서에서 발견 된 구성 오류를 해결 하려면이 보고서를 실행할 수 있습니다.
 
+ **R Services - 실행 통계**

  이 보고서를 사용 하 여 machine learning 작업에 대 한 실행 통계를 볼 수 있습니다. 예를 들어 실행한 R 스크립트의 총 개수, 병렬 실행 개수, 가장 자주 사용한 RevoScaleR 함수 정보를 알 수 있습니다. 클릭 **SQL 스크립트 보기** 전체 T-SQL 코드 뒤에이 보고서를 가져올 수 있습니다.

  이 보고서는 현재 RevoScaleR 패키지 함수의 통계만 모니터링합니다.

+ **R Services - 확장 이벤트**

  외부 스크립트 런타임에 관련 된 태스크를 모니터링 하는 데 사용할 수 있는 확장된 이벤트의 목록을 보려면이 보고서를 사용 합니다. 클릭 **SQL 스크립트 보기** 전체 T-SQL 코드 뒤에이 보고서를 가져올 수 있습니다.

+ **R Services - 패키지**

  SQL Server 인스턴스에 설치 된 R 또는 Python 패키지의 목록을 보려면이 보고서를 사용 합니다.

+ **R Services - 리소스 사용량**

  이 보고서를 사용 하 여 외부 스크립트를 실행 하 여 CPU, 메모리 및 I/O 리소스 사용량을 볼 수 있습니다. 또한 외부 리소스 풀의 메모리 설정도 볼 수 있습니다.

## <a name="see-also"></a>참고 항목

[모니터링 서비스](managing-and-monitoring-r-solutions.md)

[R Services에 대한 확장된 이벤트](extended-events-for-sql-server-r-services.md)
