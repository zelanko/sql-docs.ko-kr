---
title: "명령줄에서 Microsoft R Server 설치 | Microsoft 문서"
ms.custom: 
ms.date: 04/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fb4446ba-e9ce-4b93-9854-5e8a58507da0
caps.latest.revision: 4
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 811709fae77dee6daa46a97a51c44c02e372d9a8
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="install-microsoft-r-server-from-the-command-line"></a>명령줄에서 Microsoft R Server 설치
    
이 항목에서는 SQL Server 2016의 Microsoft R Server를 설치 하거나 SQL Server 2017에서 컴퓨터 학습 서버 (독립 실행형) 설치 하려면 SQL Server 명령줄 인수를 사용 하는 방법에 설명 합니다. 

> [!NOTE]
또한 별도 Windows installer를 사용 하 여 Microsoft R Server를 설치할 수 있습니다. 자세한 내용은 참조 [R 서버 설치 9.0.1 Windows 용](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)합니다. 

## <a name="prerequisites"></a>필수 구성 요소

이 설치 방법을 SQL Server의 명령줄 설치를 수행 하는 방법을 알고 스크립팅 인수에 잘 알고 필요 합니다.

- **무인** 설치에서는 설치 유틸리티의 위치를 지정하고 인수를 사용하여 설치할 기능을 나타내야 합니다. 
- **자동** 설치의 경우 동일한 인수를 제공하고 **/q** 스위치를 추가합니다. 프롬프트가 제공되지 않으며 상호 작용도 필요하지 않습니다. 그러나 필수 인수를 생략하면 설치가 실패합니다.

자세한 내용은 명령 프롬프트에서 [SQL Server 2016 설치](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)를 참조하세요.

## <a name="sql-server-2017-microsoft-machine-learning-server-standalone"></a>SQL Server 2017: Microsoft 기계 Server (독립 실행형)를 학습 합니다.

Microsoft 컴퓨터 학습 서버만 (독립 실행형) 및 해당 필수 구성 요소를 설치 하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.  예제는 오른쪽을 설치 하는 데 사용 되는 인수를 보여 줍니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR, SQL_INST_MR  /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS 
```

진행률 및 프롬프트를 보려면 _/q_ 인수를 제거합니다.

- **기능 SQL_SHARED_MR =** 컴퓨터 학습 서버 구성 요소를 가져옵니다. 여기에 모든 필수 구성 요소는 기본적으로 자동으로 설치 됩니다.
- **SQL_INST_MR** installl R 언어를 지원 하는 데 필요 합니다.
- **SQL_INST_MPY** 는 Python에 대 한 지원을 설치 해야 합니다.
- **IACCEPTROPENLICENSETERMS** 오픈 소스 R 구성 요소의 사용 약관에 동의했음을 나타냅니다.
- **IACCEPTPYTHONLICENSETERMS** Python 구성 요소를 사용 하기 위한 사용 조건에 동의한 나타냅니다.
- **IACCEPTSQLSERVERLICENSETERMS** 설치 마법사를 실행하는 데 필요합니다.

**참고**

1. SQL Server 라이선스 조건을 기능 인수는 필요 합니다.
2. 라이선스 계약 플래그와 함께 하나 이상의 언어를 지정 합니다.
3. 한 언어에서 또는 둘 다 R 및 Python을 설치할 수 있지만 각각에 대해 별도 라이선스가 있어야 합니다.

## <a name="sql-server-2016-microsoft-r-server-standalone"></a>SQL Server 2016: Microsoft R Server (독립 실행형)

Microsoft R Server(독립 실행형)와 해당 필수 조건만 설치하려면 관리자 권한 명령 프롬프트에서 다음 명령을 실행 합니다.  SQL Server 2016 설치 프로그램을 사용 하는 인수를 보여 줍니다.

```
Setup.exe /q /ACTION=Install /FEATURES=SQL_SHARED_MR /IACCEPTROPENLICENSETERMS /IACCEPTSQLSERVERLICENSETERMS
```

## <a name="offline-installation"></a>오프라인 설치

인터넷 액세스가 없는 컴퓨터에서 컴퓨터 학습 서버 또는 Microsoft R Server (독립 실행형)를 설치 하는 경우에 필요한 R 구성 요소를 사전에 다운로드 하 고 로컬 폴더를 복사 해야 합니다. 다운로드 위치는 [인터넷에 연결하지 않고 R 구성 요소 설치](../r/installing-ml-components-without-internet-access.md)를 참조하세요.

## <a name="what-is-installed"></a>설치 된 기능

설치가 완료되면 설치 작업에 대한 요약 정보와 함께 SQL Server 설치 프로그램에서 만든 구성 파일을 검토할 수 있습니다.

기본적으로 SQL Server에 대 한 로그 및 요약 모든 설치 하 고 관련된 기능 다음 폴더에 만들어집니다.

- SQL Server 2016의 경우:`C:\Program Files\Microsoft SQL Server\130\Setup Bootstrap\Log`
- SQL Server 2017:`C:\Program Files\Microsoft SQL Server\140\Setup Bootstrap\Log`

설치된 각 기능에 대해 별도의 하위 폴더가 생성됩니다.

동일한 매개 변수를 가진 Microsoft R Server의 다른 인스턴스를 설정 하려면 설치 중에 생성 된 구성 파일을 다시 사용할 수 있습니다. 자세한 내용은 [구성 파일을 사용하여 SQL Server 설치](https://msdn.microsoft.com/library/dd239405.aspx)


## <a name="customize-your-r-environment"></a>R 환경 사용자 지정

설치 후 추가 R 패키지를 설치할 수 있습니다. 자세한 내용은 [R 패키지 설치 및 관리](../r/install-additional-r-packages-on-sql-server.md)를 참조하세요.

> [!IMPORTANT]
> SQL Server에서 R 코드를 실행 하려는 경우 SQL Server 인스턴스를 실행 합니다 또는 솔루션을 배포 하는 위치 및 솔루션을 개발 하는 데 사용할 컴퓨터에는 동일한 패키지를 설치 하는 있는지 확인 합니다.

R (In-database)에 대 한 컴퓨터 학습 서비스를 설치한 후 지정 된 SQL Server 인스턴스에 연결 되는 R의 버전을 업그레이드 하는 별도 Windows installer를 사용할 수 있습니다. 자세한 내용은 참조 [R 업그레이드를 사용 하 여 SqlBindR](../r/use-sqlbindr-exe-to-upgrade-an-instance-of-sql-server.md)합니다.



