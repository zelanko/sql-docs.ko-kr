---
title: 기본 SQL Server에 대 한 기계 학습에 대 한 패키지 라이브러리 | Microsoft Docs
ms.custom: ''
ms.date: 02/19/2018
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
dev_langs:
- R
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: 97dc375dcee9dab2eb38c568b410e8ea2084842f
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/04/2018
---
# <a name="default-package-libraries-for-machine-learning-on-sql-server"></a>기본 SQL Server에 대 한 기계 학습에 대 한 패키지 라이브러리
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

이 문서에서는 R 및 SQL Server와 함께 설치 된 Python에 대 한 기본 라이브러리를 설명 합니다. 이 문서는 이러한 라이브러리에 대 한 기본 위치를 제공 하 고 패키지 및 R의 버전을 확인 하는 방법을 설명 또는 Python 각 인스턴스 라이브러리에 설치 됩니다.

## <a name="using-the-default-instance-library"></a>기본 인스턴스 라이브러리를 사용 하 여

기계 학습 SQL Server를 설치 하면 단일 패키지 라이브러리를 설치 하는 각 언어에 대 한 인스턴스 수준에서 만들어집니다. SQL Server는 다른 라이브러리에 설치 된 패키지를 액세스할 수 없습니다.

원격 클라이언트에서 서버로 연결 server 계산 컨텍스트에서 실행 하려는 모든 Python 또는 R 코드 인스턴스 라이브러리에 설치 된 패키지에만 사용할 수 있습니다.

기본 인스턴스 라이브러리는 서버 자산을 보호 하려면 SQL Server와 함께 등록 되 고 컴퓨터 관리자만 수정할 수 있는 보안된 폴더에 설치 됩니다. 컴퓨터의 소유자가 아니거나,이 라이브러리에 패키지를 설치 하려면 관리자 로부터 권한을 부여 받아야 할 수 있습니다. 

컴퓨터를 소유 하는 경우에 인스턴스 라이브러리에 패키지를 추가 하기 전에 모든 특정 Python 또는 R 패키지를 서버 환경에서의 유용성을 고려해 야 합니다. 여러 버전에 대 한 필요성 및 패키지 파일의 크기와 같은 요소를 뿐만 아니라 패키지 네트워크 또는 인터넷이 필요한 지 여부 고려 액세스 합니다.

### <a name="sql-server"></a>SQL Server

|버전 | 인스턴스 이름|기본 경로|
|------|------|------|
| SQL Server 2016 |기본 인스턴스(default instance)|`C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\R_SERVICES\library`|
| SQL Server 2016 |명명된 인스턴스(named instance) |`C:\Program Files\Microsoft SQL Server\MSSQL13.<instance_name>\R_SERVICES\library`|
| SQL Server 2017 with R|기본 인스턴스(default instance) |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\library` |
| SQL Server 2017 with R|명명된 인스턴스(named instance)|`C:\Program Files\Microsoft SQL Server\MSSQL14.MyNamedInstance\R_SERVICES\library` |
| SQL Server 2017 python |기본 인스턴스(default instance) |`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\PYTHON_SERVICES\library` |
| SQL Server 2017 python|명명된 인스턴스(named instance)|`C:\Program Files\Microsoft SQL Server\MSSQL14.<instance_name>\PYTHON_SERVICES\library` |

### <a name="r-server-standalone-or-machine-learning-server-standalone"></a>R 서버 (독립 실행형) 또는 컴퓨터 학습 서버 (독립 실행형)

이 표에서 SQL Server 설치 프로그램을 사용 하 여 독립 실행형 서버를 설치할 때 이진 파일의 기본 경로 보여 줍니다. 

|버전| 설치|기본 경로|
|------|------|------|
| SQL Server 2016|R Server (Standalone)| |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|기계 학습 R 통한 서버 |`C:\Program Files\Microsoft SQL Server\130\R_SERVER`|
|SQL Server 2017|기계 학습 python 서버 |`C:\Program Files\Microsoft SQL Server\130\PYTHON_SERVER`|

기본 경로 다른 별도 Windows installer를 사용 하 여 기계 학습 서버 또는 Microsoft R Server를 설치 하는 경우: 일반적으로 같은 `C:\Program Files\Microsoft\R Server\R_SERVER`합니다. 참조 항목:
 
+ [Windows에 대 한 서버를 학습 하는 컴퓨터를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows 용 R Server 9.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows)

## <a name="what-is-included-in-a-default-installation"></a>기본 설치에 포함 된 항목

이 섹션에서는 기본적으로 설치 하는 R, Python 기능의 요약 합니다.

### <a name="default-r-installation-for-sql-server"></a>SQL Server에 대 한 기본 R 설치

기본적으로 R **기본** 패키지도 설치 합니다. 과 같은 패키지에서 제공 하는 핵심 기능을 포함 하는 기본 패키지 `stats` 및 `utils`합니다.

R의 기본 설치에는 다양 한 샘플 데이터 집합 및 관리자 권한 (경량 대화형 편집기) 및 (R 명령 프롬프트) rterm이 같은 표준 R 도구 포함 됩니다.

SQL Server 2016 또는 SQL Server 2017에서 R의 설치도 포함 되어는 **RevoScaleR** 패키지 및 관련된 향상 된 패키지 및 공급자가 원격 계산 컨텍스트를 지 원하는 스트리밍, 병렬 rx 함수를 실행 하 고 다른 여러 기능이 있습니다.

RevoScaleR 패키지를 업그레이드 하기 위해 사용 하 여 하거나 바인딩 방금 기계 학습 구성 요소를 업그레이드 또는 패치 또는 SQL Server의 최신 버전으로 인스턴스를 업그레이드 합니다.

+ 향상된 된 R 기능 개요를 참조 하세요. [컴퓨터 학습 서버에 대 한](https://docs.microsoft.com/machine-learning-server/what-is-microsoft-r-server)

+ 설치 하는 클라이언트 컴퓨터로 RevoScaleR 라이브러리를 다운로드 하려면 [Microsoft R Client](https://docs.microsoft.com/machine-learning-server/r-client/what-is-microsoft-r-client)

### <a name="default-python-installation-for-sql-server"></a>SQL Server에 대 한 기본 Python 설치

기계 학습 기능 및 Python 언어 옵션을 선택 하면 Anaconda 배포 설치 되어 있습니다. 정확한 버전을 설치한 상태는 SQL Server의 버전 및 컴퓨터 학습 서버 설치 관리자를 사용 하 여 인스턴스 업그레이드 여부에 따라 달라 집니다.

|릴리스| Anaconda 버전| 기타 변경 내용|
|------|------|------|
| SQL Server 2017 RTM| 3.5.2| New: revoscalepy|
| 2017 년 9 월 9.2.1 컴퓨터 학습 서버를 통해 업데이트| 4.2 anaconda| revoscalepy에 대 한 업데이트 |
| SQL Server 2017 CU3| 4.2 anaconda| revoscalepy에 대 한 업데이트 |

Python 코드 라이브러리 외에도 표준 설치 예제 데이터, 단위 테스트 및 예제 스크립트를 포함합니다.

## <a name="restrictions-and-known-issues"></a>제한 사항 및 알려진된 문제

SQL Server에서 실행 되는 모든 솔루션 צ ְ ײ **만** 인스턴스와 연결 된 기본 라이브러리에서 설치 된 패키지입니다.

바인딩을 사용 하 여 인스턴스에 R 구성 요소를 업그레이드 하는 경우 경로 인스턴스 라이브러리를 변경할 수 있습니다. SQL Server에서 현재 사용 되는 라이브러리 경로 확인 해야 합니다.

## <a name="administrative-permissions-required-for-package-installation"></a>패키지 설치에 필요한 관리 권한

패키지 설치에 필요한 사용 권한에 SQL Server 2016 및 SQL Server 2017 사이 변경 되었습니다.

+ SQL Server 2016에서 관리 액세스 권한을 새 R 패키지의 설치에 필요한 경우

+ SQL Server 2017 년 1에서 R와 Python에 대 한 관리자 권한으로 패키지를 설치 하 계속 수 있으며,이 가장 쉬운 방법은 아마도 합니다.

    DDL 문, 외부 라이브러리 만들기는 R 도구를 사용 하지 않고 패키지를 설치 하려면 데이터베이스 관리자를 있습니다. 

    서버를 학습 하는 컴퓨터에 대 한 패키지 관리 기능을 사용 하는 경우 데이터베이스 수준에서 R 패키지를 설치 하려면 RevoScaleR을 사용할 수 있습니다. 데이터베이스 관리자는 기능을 설정 하 고 사용자에 게 부여할 데이터베이스 단위로에 자체 패키지를 설치 해야 합니다. 자세한 내용은 참조 [Ddl을 사용 하 여 패키지 관리를 사용 하도록 설정](r-package-how-to-enable-or-disable.md)합니다.

### <a name="user-libraries-are-not-supported"></a>사용자 라이브러리는 지원 되지 않습니다.

보안 된 위치에 패키지를 종종 설치할 수 없는 사용자가 사용자 라이브러리에는 패키지를 설치에 의존 합니다. 그러나 SQL Server 환경에서 가능한 아닙니다. 종종 파일 시스템 액세스는 서버에서 제한 됩니다.

서버에서 사용자 문서 폴더에 대 한 관리자 권한 및 액세스 해야 하는 경우에 SQL Server에서 실행 되는 외부 스크립트 런타임 기본 인스턴스 라이브러리 외부 설치 된 모든 패키지를 액세스할 수 없습니다.

사용자 라이브러리와 관련 된 문제를 해결 하는 방법에 대 한 팁을 참조 하십시오. [사용자 라이브러리에 설치 된 패키지](packages-installed-in-user-libraries.md)합니다.