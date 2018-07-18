---
title: SQL Server 2016 R Server (독립 실행형) 설치 | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e5457698120536247ad1823b842bb1b8e52b484d
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38979285"
---
# <a name="install-sql-server-2016-r-server-standalone"></a>SQL Server 2016 R Server (독립 실행형) 설치
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 설명의 독립 실행형 버전을 설치 하려면 SQL Server 2016 설치 프로그램을 사용 하는 방법 **SQL Server 2016 R Server**합니다.

## <a name="bkmk_prereqs"> </a> 설치 전 검사 목록

SQL Server 2016가 필요 합니다. SQL Server 2017에 있는 경우 설치 하세요 [SQL Server 2017 Machine Learning Server (독립 실행형)](sql-machine-learning-standalone-windows-install.md) 대신 합니다.

이전 버전의 Revolution Analytics 도구 또는 패키지를 설치한 경우에 먼저 제거 해야 합니다. 

## <a name="get-the-installation-media"></a>설치 미디어 다운로드

[!INCLUDE[GetInstallationMedia](../../includes/getssmedia.md)]

 ###  <a name="bkmk_ga_instalpatch"></a> 패치 설치 요구 사항 

Microsoft는 SQL Server에서 필수 조건으로 설치되는 Microsoft VC++ 2013 런타임 이진 파일의 특정 버전과 관련된 문제를 확인했습니다. VC 런타임 이진 파일에 대한 이 업데이트가 없으면 SQL Server의 특정 시나리오에서 안정성 문제를 발생할 수 있습니다. SQL Server를 설치하기 전에 [SQL Server 릴리스 정보](../../sql-server/sql-server-2016-release-notes.md#bkmk_ga_instalpatch) 의 지침에 따라 해당 컴퓨터에 VC 런타임 이진 파일에 대한 패치가 필요한지 확인하세요.  

## <a name="run-setup"></a>설치 프로그램 실행

로컬 설치의 경우 관리자로 설치 프로그램을 실행해야 합니다. 원격 공유로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 설치하는 경우 원격 공유에 대한 읽기 및 실행 권한이 있는 도메인 계정을 사용해야 합니다.

1. SQL Server 2016 설치 마법사를 시작 합니다. 서비스 팩 1 이상을 설치 하는 것이 좋습니다.

2. 에 **설치가** 탭을 클릭 **새 R Server (독립 실행형) 설치**합니다.
    
     ![R Server 독립 실행형 설치 프로그램을 시작한](media/2016-setup-installation-rsvr.png "R 서버 독립 실행형 설치를 시작 합니다.")
    
3.  **기능 선택** 페이지에서 다음 옵션은 이미 선택되어 있습니다.
    
    **R 서버(독립 실행형)**  
    
    ![기능 선택에 대 한 R Server 독립 실행형](media/2016setup-rserver-features.png "R 서버 독립 실행형에 대 한 선택 항목 기능")
    
    기타 모든 옵션은 무시해도 됩니다. 
    
    > [!NOTE]
    > 설치를 방지 합니다 **공유 기능** R Services가 이미 설치 되어 있는 SQL Server 데이터베이스 내 분석에 대 한 컴퓨터에서 설치를 실행 하는 경우. 이 중복 된 라이브러리를 만듭니다.
    > 
    > SQL Server에서 실행 되는 R 스크립트가 관리 하는 SQL Server를 하지 못하도록 다른 데이터베이스 엔진 서비스에서 사용 되는 메모리를 사용 하 여 충돌 하는 반면 독립 실행형 R Server에는 이러한 제한이 및 다른 데이터베이스 작업을 방해할 수 있습니다.
    > 
    > 일반적으로 권장 R Server (독립 실행형)를 설치 하는 별도 컴퓨터에서 SQL Server R Services (In-database).

4.  Microsoft R Open을 다운로드 및 설치하려면 사용 조건에 동의합니다. **동의** 단추를 사용할 수 없게 되면 **다음**을 클릭할 수 있습니다.
    
    이러한 구성 요소 이며, 필요한 모든 필수 구성 요소 설치 시간이 걸릴 수 있습니다.
    
5.  **설치 준비 완료** 페이지에서 선택 내용을 확인하고 **설치**를 클릭합니다.

## <a name="default-installation-folders"></a>기본 설치 폴더

SQL Server 설치 프로그램을 사용 하 여 R Server를 설치할 때 R 라이브러리 설치에 사용 하는 SQL Server 버전에 연결 된 폴더에 설치 됩니다. 이 폴더에 샘플 데이터, R 기본 패키지에 대 한 설명서 및 R 도구 및 런타임 설명서 찾을 있습니다.

그러나 별도 Windows 설치 관리자 (하지 SQL 설치 프로그램)를 사용 하 여 Microsoft R Server를 설치 하거나 별도 Windows 설치 관리자를 사용 하 여 업그레이드 하는 경우 R 라이브러리는 다른 폴더에 설치 됩니다.

을 권장 하지만 한도 동일한 컴퓨터에 R Services (In-database)를 사용 하 여 SQL server 인스턴스를 설치 하는 경우 R 라이브러리 및 도구는 두 번째 복사본을 다른 폴더에 설치 됩니다.

다음 표에서 각 설치에 대 한 경로 나열합니다.

|버전| 설치 방법 | 기본 폴더|
|----|----|----|
|R Server (Standalone) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|R Server (Standalone) |Windows 독립 실행형 설치 관리자|`C:\Program Files\Microsoft\R Server\R_SERVER`|
|Machine Learning Server(독립 실행형) |  R 언어 옵션을 사용 하 여 SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\R_SERVER`|
|Machine Learning Server(독립 실행형) |  Python 언어 옵션을 사용 하 여 SQL Server 2017 설치 마법사 |`C:\Program Files\Microsoft SQL Server\140\PYTHON_SERVER`|
|Machine Learning Server(독립 실행형) |  Windows 독립 실행형 설치 관리자 |`C:\Program Files\Microsoft\R Server\R_SERVER`|
|R Services(In-database) |SQL Server 2016 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES`|
|Machine Learning Services(데이터베이스 내) |R 언어 옵션을 사용 하 여 SQL Server 2017 설치 마법사|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\R_SERVICES`  |
|Machine Learning Services(데이터베이스 내) |Python 언어 옵션을 사용 하 여 SQL Server 2017 설치 마법사| `C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES` |

## <a name="development-tools"></a>개발 도구

개발 IDE 설치의 일부로 설치 되지 않았습니다. 추가 도구 필요 하지 않은, 포함 된 모든 표준 도구와는 제공 되는 R 또는 Python 배포를 사용 하 여 합니다.

새 릴리스를 시도 하는 것이 좋습니다 [!INCLUDE[rsql_rtvs](../../includes/rsql-rtvs-md.md)] 나 [Visual Studio 용 Python](https://docs.microsoft.com/visualstudio/python/installing-python-support-in-visual-studio)합니다. Visual Studio는 모두 R 및 Python으로 SQL Server를 사용 하 여 연결 데이터베이스 개발 도구 및 BI 도구를 지원합니다. 그러나 RStudio를 포함 하 여 모든 기본 개발 환경을 사용할 수 있습니다.
  
## <a name="get-help"></a>도움말 보기

설치 또는 업그레이드를 사용 하 여 도움이 필요 하세요? 알려진 문제와 관련 된 일반적인 질문에 대 한 답변을 다음 문서를 참조 하세요.

* [업그레이드 및 설치 FAQ-Machine Learning 서비스](../r/upgrade-and-installation-faq-sql-server-r-services.md)

인스턴스의 설치 상태를 확인 하 고 일반적인 문제를 해결 하려면 이러한 사용자 지정 보고서를 봅니다.

* [SQL Server R Services에 대 한 사용자 지정 보고서](../r/monitor-r-services-using-custom-reports-in-management-studio.md)

## <a name="next-steps"></a>다음 단계

R 개발자가 몇 가지 간단한 예제를 사용 하 여 시작할 수 있습니다 및 SQL Server를 사용 하 여 R을 작동 하는 방법의 기본 사항을 알아봅니다. 다음 단계를 다음 링크를 참조 하세요.

+ [자습서: T-SQL에서 R을 실행](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)합니다.
+ [자습서: R 개발자를 위한 데이터베이스 내 분석](../tutorials/sqldev-in-database-r-for-sql-developers.md)

실제 시나리오를 기반으로 하는 기계 학습의 예제를 보려면 [기계 학습 자습서](../tutorials/machine-learning-services-tutorials.md)합니다.

