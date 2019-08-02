---
title: Management Studio에서 사용자 지정 보고서를 사용 하 여 R Services 모니터링
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a7ab7a4ccd4956bd1752be398b25a6ff9fd92ce5
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715078"
---
# <a name="monitor-machine-learning-services-using-custom-reports-in-management-studio"></a>Management Studio에서 사용자 지정 보고서를 사용하여 Machine Learning Services 모니터링
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

기계 학습에 사용 되는 인스턴스를 보다 쉽게 관리할 수 있도록 제품 팀은 SQL Server Management Studio에 추가할 수 있는 다양 한 샘플 사용자 지정 보고서를 제공 합니다. 이러한 보고서에서 다음과 같은 세부 정보를 볼 수 있습니다.

- 활성 R 또는 Python 세션
- 인스턴스에 대 한 구성 설정
- Machine learning 작업에 대 한 실행 통계
- R Services에 대 한 확장 이벤트
- 현재 인스턴스에 설치 된 R 또는 Python 패키지

이 문서에서는 기계 학습을 위해 특별히 제공 된 사용자 지정 보고서를 설치 하 고 사용 하는 방법을 설명 합니다. 

Management Studio의 보고서에 대 한 일반적인 소개는 [Management Studio의 사용자 지정 보고서](../../ssms/object/custom-reports-in-management-studio.md)를 참조 하세요.

## <a name="how-to-install-the-reports"></a>보고서를 설치하는 방법

보고서는 SQL Server Reporting Services를 사용하여 만듭니다. 하지만 Reporting Services가 인스턴스에서 설치되어 있지 않더라도 SQL Server Management Studio에서 바로 보고서를 사용할 수도 있습니다. 

이러한 보고서를 사용하려면:

* SQL Server 제품 샘플용 GitHub 리포지토리에서 RDL 파일을 다운로드합니다.
* SQL Server Management Studio에 사용되는 사용자 지정 보고서 폴더에 파일을 추가합니다.
* SQL Server Management Studio에서 보고서를 엽니다.


### <a name="step-1-download-the-reports"></a>1단계. 보고서 다운로드

1. [SQL Server 제품 샘플이](https://github.com/Microsoft/sql-server-samples)포함 된 GitHub 리포지토리를 열고 샘플 보고서를 다운로드 합니다. 

    + [SSMS 사용자 지정 보고서](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/machine-learning-services/ssms-custom-reports)

    > [!NOTE]
    > 보고서는 SQL Server 2017 Machiine Learning Services 또는 SQL Server 2016 R Services와 함께 사용할 수 있습니다.

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

GitHub의 제품 샘플 리포지토리에는 현재 다음과 같은 보고서가 포함 되어 있습니다.

+ **R Services - 활성 세션**

  이 보고서를 사용 하 여 SQL Server 인스턴스에 현재 연결 되어 있고 machine learning 작업을 실행 중인 사용자를 볼 수 있습니다. 
  
+ **R Services - 구성**

  이 보고서를 사용 하 여 외부 스크립트 런타임 및 관련 서비스의 구성을 볼 수 있습니다. 보고서는 다시 시작이 필요한지 표시하고 필요한 네트워크 프로토콜을 확인합니다. 
  
  SQL Server에서 실행 되는 기계 학습 작업에는 계산 컨텍스트로 암시적 인증이 필요 합니다. 묵시적 인증이 구성 되어 있는지 확인 하기 위해 보고서는 SQLRUserGroup 그룹에 대 한 데이터베이스 로그인이 있는지 여부를 확인 합니다.

 + **R Services - 인스턴스 구성** 

   이 보고서는 기계 학습을 구성 하는 데 도움을 주기 위해 작성 되었습니다. 이 보고서를 실행 하 여 앞의 보고서에 있는 구성 오류를 해결할 수도 있습니다.
 
+ **R Services - 실행 통계**

  이 보고서를 사용 하 여 machine learning 작업에 대 한 실행 통계를 볼 수 있습니다. 예를 들어 실행한 R 스크립트의 총 개수, 병렬 실행 개수, 가장 자주 사용한 RevoScaleR 함수 정보를 알 수 있습니다. **Sql 스크립트 보기** 를 클릭 하 여이 보고서 뒤에 전체 t-sql 코드를 가져옵니다.

  이 보고서는 현재 RevoScaleR 패키지 함수의 통계만 모니터링합니다.

+ **R Services - 확장 이벤트**

  이 보고서를 사용 하 여 외부 스크립트 런타임과 관련 된 모니터링 태스크에 사용할 수 있는 확장 이벤트 목록을 볼 수 있습니다. **Sql 스크립트 보기** 를 클릭 하 여이 보고서 뒤에 전체 t-sql 코드를 가져옵니다.

+ **R Services - 패키지**

  이 보고서를 사용 하 여 SQL Server 인스턴스에 설치 된 R 또는 Python 패키지의 목록을 볼 수 있습니다.

+ **R Services - 리소스 사용량**

  이 보고서를 사용 하 여 외부 스크립트 실행의 CPU, 메모리 및 i/o 리소스 사용량을 볼 수 있습니다. 또한 외부 리소스 풀의 메모리 설정도 볼 수 있습니다.

## <a name="see-also"></a>참고 항목

[서비스 모니터링](managing-and-monitoring-r-solutions.md)

[R Services에 대한 확장된 이벤트](extended-events-for-sql-server-r-services.md)
