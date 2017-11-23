---
title: "명령줄에서 컴퓨터 학습 Server (독립 실행형) 또는 Microsoft R Server (독립 실행형) 설치 | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: "4"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 400f743bfbb065a5e271b5ff335d0896bb2ac3ef
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="install-machine-learning-server-standalone-or-microsoft-r-server-standalone-from-the-command-line"></a>명령줄에서 컴퓨터 학습 Server (독립 실행형) 또는 Microsoft R Server (독립 실행형) 설치

이 문서에서는 명령줄을 사용 하 여 다음 SQL Server 기능을 설치 하려면 SQL Server 명령줄 인수를 사용 하는 방법을 설명 합니다.

+ [SQL server 2017 기계 Server (독립 실행형) 학습](#bkmk_mls2017) 
+ [SQL Server 2016에서에서 Microsoft R Server (독립 실행형)](#bkmk_mrs2016)

**무인** 설치 유틸리티의 위치를 지정 하 고 설치할 기능을 나타내기 위해 인수를 사용 하 여 설치 해야 합니다.

**자동** 설치의 경우 동일한 인수를 제공하고 **/q** 스위치를 추가합니다. 어떠한 프롬프트도 제공 되며 상호 작용이 필요 합니다. 그러나 모든 필수 인수를 생략 하면 설치가 실패 합니다.

## <a name="prerequisites"></a>필수 구성 요소

SQL Server의 명령줄 설치를 수행 하 고 스크립팅 인수를 잘 알고 있어야 하는 방법을 알아야 합니다.

자세한 내용은 참조 [명령 프롬프트에서 SQL Server 설치](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)합니다.

인터넷 액세스가 없는 컴퓨터에서 컴퓨터 학습 서버 또는 Microsoft R Server (독립 실행형)를 설치 하는 경우에 필요한 R (또는 Python) 구성 요소를 사전에 다운로드 하 고 로컬 폴더를 복사 해야 합니다. 다운로드 위치에 대 한 참조 [인터넷 연결 되지 않은 컴퓨터 학습 구성 요소 설치](installing-ml-components-without-internet-access.md)합니다.


## <a name="bkmk_mls2017"></a>Microsoft 컴퓨터 학습 Server (독립 실행형) 설치

**적용 대상: SQL Server 2017**

만 컴퓨터 학습 Server (독립 실행형) 및 해당 필수 구성 요소를 설치 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.

+ SQL Server 라이선스 조건을 기능 인수는 필요 합니다.
+ 한 언어에서 또는 둘 다 R 및 Python을 설치할 수 있지만 각각에 대해 별도 라이선스가 있어야 합니다.

이 예제에서는 오른쪽을 설치 하는 데 사용 되는 인수를 보여 줍니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

이 예제에서는 Python을 설치 하는 데 사용 되는 인수를 보여 줍니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MPY  /IACCEPTPYTHONOPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

+ 진행률 및 프롬프트를 보려면 _/q_ 인수를 제거합니다.
+ 인수를 사용 하는 경우 **기능 SQL_SHARED_MR =**, R 아니고 Python으로 컴퓨터 학습 서버 구성 요소만 설치 됩니다. 이 설치에는 기본적으로 자동으로 설치 된 모든 필수 구성 요소가 포함 됩니다. 처음으로 설치 하는 경우 하나 이상의 언어를 추가 하는 것이 좋습니다.
+ 추가 **SQL_INST_MR** r 지원을 설치 하려면
+ 추가 **SQL_INST_MPY** Python에 대 한 지원을 설치 해야 합니다.
+ **IACCEPTROPENLICENSETERMS** 오픈 소스 R 구성 요소의 사용 약관에 동의했음을 나타냅니다.
+ **IACCEPTPYTHONLICENSETERMS** Python 구성 요소를 사용 하기 위한 사용 조건에 동의한 나타냅니다.
+ **IACCEPTSQLSERVERLICENSETERMS** 설치 마법사를 실행하는 데 필요합니다.


## <a name="bkmk_mrs2016"></a> Microsoft R Server(독립 실행형) 설치

**적용 대상: SQL Server 2016**

설치 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 **만** Microsoft R Server (독립 실행형) 및 해당 필수 구성 요소입니다. 

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

> [!TIP]
> 설치 하지 않으면이 SQL Server R Services의 인스턴스를 호스팅하는 동일한 컴퓨터에 두는 것이 좋습니다.

## <a name="post-installation-tasks"></a>사후 설치 태스크

동일한 매개 변수를 가진 Microsoft R Server의 다른 인스턴스를 설정 하려면 설치 중에 생성 된 구성 파일을 다시 사용할 수 있습니다. 자세한 내용은 참조 [구성 파일을 사용 하 여 SQL Server 설치](../../database-engine/install-windows/install-sql-server-using-a-configuration-file.md)합니다.

### <a name="review-installed-components"></a>구성 요소 설치 검토

설치가 완료되면 설치 작업에 대한 요약 정보와 함께 SQL Server 설치 프로그램에서 만든 구성 파일을 검토할 수 있습니다.

기본적으로 SQL Server에 대 한 로그 및 요약 모든 설치 하 고 관련된 기능 다음 폴더에 만들어집니다.

+ SQL Server 2017:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`
+ SQL Server 2016의 경우:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`

별도 하위 폴더는 설치 된 각 기능에 대해 생성 됩니다.

### <a name="customize-the-r-or-python-environment"></a>R 또는 Python 환경을 사용자 지정

설치 후 추가 Python 또는 R 패키지를 설치할 수 있습니다. 과정에는 SQL Server 2016 또는 SQL Server 2017 사용 여부에 따라 약간씩 다릅니다.

SQl Server 2017 년 1에서 설치 하 고 T-SQL을 사용 하 여 R 패키지를 관리할 수 있습니다. 자세한 내용은 참조 [R 패키지를 관리 및 설치](../r/install-additional-r-packages-on-sql-server.md)합니다.

Python 및 SQL Server 2016에서 관리자가 필요할 수 있는 모든 추가 라이브러리를 설치 해야 합니다.

> [!IMPORTANT]
> SQL Server에서 R 코드를 실행 하려는 경우 SQL Server 인스턴스를 실행 합니다 또는 솔루션을 배포 하는 위치 및 솔루션을 개발 하는 데 사용할 컴퓨터에는 동일한 패키지를 설치 하는 있는지 확인 합니다.

### <a name="upgrading-r-server-or-sql-server-machine-learning"></a>기계 학습 R 서버 또는 SQL Server 업그레이드

SQL Server를 사용 하려면 별도 Windows installer를 사용 하 여 Microsoft R Server 또는 서버를 학습 하는 컴퓨터에 설치할 수 있습니다. 다운로드 위치 및 지침을 보려면 다음이 링크 참조:

+ [Windows에 대 한 서버를 학습 하는 컴퓨터를 설치 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)
+ [Windows 용 R Server 9.0.1 설치](https://docs.microsoft.com/machine-learning-server/install/r-server-install-windows) 

서버를 학습 하는 컴퓨터에 대 한 별도 windows installer는 기계 학습 인스턴스와 연결 된 구성 요소를 업그레이드 하려면 데도 사용할 수 있습니다.  자세한 내용은 다음 링크를 참조하십시오.

+ [SqlBindR를 사용 하 여 R을 업그레이드 하려면](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)
