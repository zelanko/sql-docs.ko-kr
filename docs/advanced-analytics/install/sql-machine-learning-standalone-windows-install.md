---
title: SQL Server 2017 컴퓨터 학습 Server (독립 실행형) 설치 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: cb906a8a05221204ec10310d652f6891861d35e2
ms.sourcegitcommit: 2d93cd115f52bf3eff3069f28ea866232b4f9f9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/01/2018
ms.locfileid: "34708271"
---
# <a name="install-sql-server-2017-machine-learning-server-standalone-on-windows"></a>Windows Server (독립 실행형)를 학습 하는 SQL Server 2017 컴퓨터 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

SQL Server 설치 프로그램에는 기계 학습 SQL Server 외부에서 실행 하는 서버를 설치 하는 옵션이 포함 되어 있습니다. 이 옵션은 계산 컨텍스트를 원격으로 사용할 수 있는 솔루션을 학습, 로컬 서버와 원격 컴퓨터 학습 서버 또는 다른 SQL Server Spark 클러스터에서 같은 의미로 전환 고성능 시스템을 개발 해야 하는 경우 유용할 수 있습니다. 인스턴스입니다.
  
이 문서에서는 독립 실행형 버전을 설치 하려면 SQL Server 설치 프로그램을 사용 하는 방법을 설명 **SQL Server 2017 컴퓨터 학습 서버**합니다. 

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

SQL Server 2017이 필요합니다. SQL Server 2016를 설정한 경우 설치 하십시오 [SQL Server 2016 R 서버 (독립 실행형)](sql-r-standalone-windows-install.md) 대신 합니다.

SQL Server 2016 R 서버 (독립 실행형) 또는 Microsoft R Server 등의 이전 버전을 설치한 경우 계속 하기 전에 기존 설치를 제거 합니다.

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2017에 대 한 설치 마법사를 시작 합니다.

2. 클릭는 **설치** 탭을 선택 **새 컴퓨터 학습 Server (독립 실행형) 설치**합니다.
    
     ![시스템 학습 서버 독립 실행형 설치](media/2017setup-installation-page-mlsvr.png "학습 서버 독립 실행형 컴퓨터의 설치를 시작 합니다.")

3. 규칙 확인이 완료 된 후에 SQL Server 라이선스 조건에 동의 하 고 새로 설치를 선택 합니다.

4. 에 **기능 선택** 페이지에서 다음 옵션을 이미 선택 되어 있어야 합니다.

    - Microsoft 기계 Server (독립 실행형)를 학습 합니다.

    - R 및 Python 기본적으로 선택 됩니다. 두 언어 선택을 취소할 수 있지만 지원 되는 언어 중 하나 이상을 설치 하는 것이 좋습니다.

     ![시스템 학습 서버 독립 실행형 설치](media/2017setup-features-page-mlsvr-rpy.png "학습 서버 독립 실행형 컴퓨터의 설치를 시작 합니다.")
    
    기타 모든 옵션은 무시해야 합니다. 
    
    > [!NOTE]
    > 설치 하지 않습니다는 **공유 기능** 컴퓨터에 SQL Server 데이터베이스에서 분석에 대 한 설치 된 컴퓨터 학습 서비스 하는 경우. 중복 된 라이브러리를 만듭니다.
    > 
    > 또한 SQL Server에서 실행 되는 R, Python 스크립트를 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리와 충돌 하 여 관리 하는 반면 서버는 독립 실행형 컴퓨터 학습에는 이러한 제한이 있으며, 다른 데이터베이스 작업을 방해할 수 있습니다. . 마지막으로, 화에 대해 자주 사용 되는 RDP 세션을 통한 원격 액세스는 일반적으로 데이터베이스 관리자가 차단 됩니다.
    > 
    > 이러한 이유로, 일반적으로 권장 SQL Server 컴퓨터 학습 서비스와에서 별도 컴퓨터에 학습 Server 컴퓨터 (독립 실행형)를 설치 하는 합니다.

5.  다운로드 하 고 기계 학습 구성 요소 설치에 대 한 사용 조건에 동의 합니다. 언어를 모두 설치 하는 경우 별도 사용권 계약은 Python 및 Microsoft R에 필요 합니다.
    
     ![Python 사용권 계약](media/2017setup-python-license.png "Python 사용권 계약")
    
    이러한 구성 요소 및 해야, 모든 필수 구성 요소 설치에는 시간이 걸릴 수 있습니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다.

6.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

### <a name="default-installation-folders"></a>기본 설치 폴더

R 서버를 설치할 때 또는 SQL Server 설치 프로그램을 사용 하 여 컴퓨터 학습 서버, R 라이브러리 설치에 사용 된 SQL Server 버전에 연결 하는 폴더에 설치 됩니다. 이 폴더에 샘플 데이터, R 기본 패키지에 대 한 설명서 및 R 도구 및 런타임의 설명서도 찾을 수 있습니다.

그러나 별도 Windows installer를 사용 하 여 설치 하는 경우 또는 별도 Windows installer를 사용 하 여 업그레이드 하는 경우 R 라이브러리는 다른 폴더에 설치 됩니다.

참조를 위해 R Services (In-database) 또는 컴퓨터 학습 Services (In-database)와 SQL Server의 인스턴스를 설치 했 고 인스턴스가 동일한 컴퓨터에 해당 하는 경우 R 라이브러리 및 도구를 다른 폴더에 기본적으로 설치 됩니다.

다음 표에서 각 설치에 대 한 경로 나열합니다.

|버전| 설치 방법 | 기본 폴더|
|----|----|----|
|SQL Server 2017 컴퓨터 학습 서버 (독립 실행형) |  SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER` <br/>`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Microsoft 기계 Server (독립 실행형)를 학습 합니다. |  독립 실행형 응용 프로그램 |`C:\Program Files\Microsoft\ML Server\R_SERVER`<br/>`C:\Program Files\Microsoft\ML Server\PYTHON_SERVER`|
|SQL Server 2017 컴퓨터 학습 Services (In-database) |SQL Server 2017 설치 마법사에서 R 언어 옵션|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  <br/>`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |
|SQL Server 2016 R Server (독립 실행형) |  SQL Server 2016 설치 마법사 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2016 R Services (In-database) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|

## <a name="development-tools"></a>개발 도구

개발 IDE 설정의 일부분으로 설치 되지 않았습니다. 추가 도구 필요 하지 않은, 포함 된 모든 표준 도구와는 제공 되는 R, Python의 배포와 함께 합니다.

새 릴리스를 시도 하는 것이 좋습니다 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 또는 [Visual Studio 용 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)합니다. Visual Studio 모두 R 및 Python으로 데이터베이스 개발 도구, SQL Server와의 연결 및 BI 도구를 지원합니다. 그러나 RStudio를 포함 하 여 모든 기본 설정된 개발 환경에 사용할 수 있습니다.

## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드로 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대답 하십시오에 대 한 다음 문서를 참조 합니다.

* [업그레이드 및 설치 FAQ-컴퓨터 학습 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자 몇 가지 간단한 예제 차별화할 수 및 R SQL Server와 함께 작동 하는 방법에 대 한 기본 사항을 설명 합니다. 다음 단계에서는 다음 링크 참조:

+ [자습서: T-SQL에서 R을 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)
+ [R 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

Python 개발자는이 자습서를 수행 하 여 SQL Server와 함께 Python을 사용 하는 방법을 배울 수 있습니다.

+ [자습서: T-SQL에서 Python 실행](../tutorials/run-python-using-t-sql.md)
+ [Python 개발자를 위한 자습서: 데이터베이스에서 분석](../tutorials/sqldev-in-database-python-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 참조 [자습서 학습 컴퓨터](../tutorials/machine-learning-services-tutorials.md)합니다.
