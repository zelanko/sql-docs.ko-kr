---
title: "SQL Server 인스턴스의 컴퓨터 학습 구성 요소를 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 07/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2d9d7ddd95bdbcf6efca98ed94bc305924902b98
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>SQL Server 인스턴스의 컴퓨터 학습 구성 요소 업그레이드

Windows 용 Microsoft 컴퓨터 학습 서버에 SQL Server의 인스턴스에 연결 된 R 구성 요소를 업그레이드 하는 데 사용할 수 있는 도구가 있습니다. 두 가지 버전의 도구: 마법사, 그리고 명령줄 유틸리티입니다.

이 문서에는 호환 되는 SQL Server 인스턴스를 업그레이드 하려면 이러한 도구를 사용 하는 방법 및 이전에 업그레이드 된 인스턴스로 되돌리는 방법을 설명 합니다.

SQL Server 업데이트의 일부로 업그레이드 확보 하려는 경우이 업그레이드 프로세스를 사용할 필요가 없습니다. 새 서비스 팩 또는 서비스 릴리스를 설치할 때마다 컴퓨터 학습 구성 요소는 항상 자동으로 최신 버전으로 업그레이드 됩니다. SLQ Server 서비스 릴리스에서 affored 것 보다 더 빠른 속도로 구성 요소를 업그레이드 하려는 경우에이 proess를 사용 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

> [!NOTE]
> 이 문서 작성 된 시간에 업그레이드 호환 가능한 SQL Server 2016 인스턴스에만 적용 됩니다.  SQL Server 2017에 대 한 업그레이드는 지원 되지만 새 버전의 Microsoft 컴퓨터 학습에 사용할 서버를 업그레이드 하지 릴리스 되었습니다.

## <a name="upgrade-an-instance"></a>인스턴스 업그레이드

업그레이드 프로세스 라고 **바인딩**새로운 최신 수명 주기 정책을 사용 하 여 SQL Server 컴퓨터 학습 구성 요소에 대 한 지원 모델을 변경 하기 때문에, 합니다. 그러나 업그레이드는 SQL Server 데이터베이스에 대 한 지원 모델을 변경 되지 않습니다.

일반적으로 이 라이선싱 시스템은 데이터 과학자가 항상 최신 버전의 R을 사용하도록 합니다. 최신 수명 주기 정책의 조건에 대한 자세한 내용은 [Support Timeline for Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver-servicing-support)(Microsoft R Server에 대한 지원 시간대)를 참조하세요.

인스턴스를 바인딩하면 다음과 같은 여러 작업이 수행됩니다.

+ 지원 모델 변경 됩니다. SQL Server 서비스 릴리스를 사용 하지 않고 지원 새로운 최신 주기 정책을 기반으로 합니다.
+ 기계 학습 인스턴스와 연결 된 구성 요소는 새로운 최신 수명 주기 정책에 따라 최신 버전으로 잠금 단계에서는 각 릴리스마다 자동으로 업그레이드 됩니다. 
+ 새 R, Python 패키지 추가 될 수 있습니다. 예를 들어 이전 업데이트가 Microsoft R Server에서 추가 새 R 패키지와 같은 [MicrosoftML](../using-the-microsoftml-package.md), [olapR](../r/how-to-create-mdx-queries-using-olapr.md), 및 [sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)합니다.
+ 새 패키지를 추가하는 경우를 제외하고 더 이상 수동으로 인스턴스를 업데이트할 수 없습니다.
+ 미리 학습 된 모델을 추가 하는 옵션이 있습니다.

나중에 각 버전에서 인스턴스를 업그레이드 하지 않으려면, 해야 **바인딩 해제** 에 설명 된 대로 인스턴스 [이 여기서](#bkmk_Unbind), 설명 된 대로 업그레이드를 학습 하는 컴퓨터를 제거한 다음 이 문서의: [Windows 용 Microsoft R Server 실행](https://msdn.microsoft.com/microsoft-r/rserver-install-windows)합니다. 프로세스가 완료 되 면 이후 기계 학습 서버 컴퓨터에 따라 업그레이드 학습 인스턴스에 더 이상 적용 됩니다.

### <a name="bkmk_prereqs"></a>업그레이드를 위한 필수 구성 요소

1. 업그레이드의 후보인 인스턴스를 식별합니다.
    + SQL Server 2016 R Services가 설치됨
    + 최소한 서비스 팩 1과 c u 3

2. 가져오기 **Microsoft R Server**, 별도 Windows 설치 관리자를 다운로드 하 여 합니다.

    [How to install R Server 9.0.1 on Windows using the standalone Windows installer](https://msdn.microsoft.com/microsoft-r/rserver-install-windows#howtoinstall)(독립 실행형 Windows Installer를 사용하여 Windows에 R Server 9.0.1을 설치하는 방법)

> [!TIP]
> 
> SqlBindR.exe를 찾을 수 없나요? 아마도 다운로드 하지 않은 R Server 아직 합니다. 이 유틸리티는 Microsoft R Server에 대 한 Windows installer에만 사용할 수 있습니다.

### <a name="bkmk_BindWizard"></a>새로운 설치 마법사를 사용 하 여 업그레이드

1. 업그레이드 하려는 인스턴스가 있는 컴퓨터에 R Server에 대 한 새 설치 관리자를 시작 합니다.
  ![Microsoft R Server 설치 마법사](media/r-server-installer-01.PNG)
2. Microsoft R Server 9.1.0에 대 한 라이선스 계약에 동의 하 고 클릭 **다음**합니다.
3. R 오픈 소스 구성 요소에 대 한 라이선스 조건에 동의 하 고 클릭 **다음**합니다.
4. **설치 폴더 선택**기본값을 그대로 사용 하거나 R 라이브러리를 설치할 다른 위치를 지정 합니다. 
5. 설치 관리자 후보 바인딩에 대 한 모든 로컬 인스턴스를 식별 합니다. 인스턴스가 표시 되 면 의미 유효한 인스턴스를 찾지 못했습니다. 서버에 패치 또는 R Services가 설치 되어 있는지 확인 해야 합니다.
6. 인스턴스를 업그레이드 하 고 클릭를 옆의 확인란을 선택 **다음**합니다.
7. 프로세스는 시간이 오래 걸릴 수 있습니다.
    
    설치 하는 동안 Microsoft R Server 9.1.0에 대 한 SQL Server R Services에서 사용 하는 R 라이브러리는 라이브러리와 대체 됩니다.
    
    실행 패드 프로세스에 의해 영향을 받지 않습니다 되지만 라이브러리 R_SERVICES 폴더에서 제거 되 고 서비스에 대 한 속성 변경 되는 라이브러리를 사용 하 `C:\Program Files\Microsoft\R Server\R_SERVER`합니다.

### <a name="bkmk_BindCmd"></a>명령줄을 사용 하 여 업그레이드

Microsoft R Server를 설치한 후 단순한 SqlBindR.exe 도구의 명령줄에서 실행할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는`C:\Program Files\Microsoft\R Server\Setup`
2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어, 인스턴스 이름 수 있습니다 `MSSQL13.MSSQLSERVER` 기본 인스턴스 또는 같은 `SERVERNAME.MYNAMEDINSTANCE`합니다.
3. */bind* 인수와 함께 **SqlBindR.exe** 명령을 실행하여 이전 단계에서 반환된 대로 업그레이드할 인스턴스의 이름을 지정합니다.

   예를 들어 기본 인스턴스를 업그레이드 하려면 다음을 입력 합니다.`SqlBindR.exe /bind MSSQL13.MSSQLSERVER`
4. 업그레이드가 완료되면 수정된 인스턴스와 연결된 실행 패드 서비스를 다시 시작합니다.


## <a name="bkmk_Unbind"></a>Revert 또는 인스턴스를 바인딩 해제

SQL Server가 설치 된 원래 라이브러리를 사용 하도록 SQL Server의 인스턴스를 복원 하려면 수행 해야 합니다는 **바인딩 해제** 작업 합니다. 이렇게 하려면 Microsoft R Server에 대 한 설치 마법사를 다시 실행 하거나 명령줄에서 SqlBindR 유틸리티를 실행 합니다.

바인딩 해제가 완료, Microsoft R server 9.1.0 라이브러리 제거 되 고 SQL Server R Services에서 사용 하는 원래 R 라이브러리 복원 됩니다.

R_SERVICES에 대 한 기본 폴더에 R 라이브러리를 사용 하도록 SQL Server 실행 패드의 속성은 편집 `C:\Program Files\Microsoft\R Server\R_SERVER`합니다.

### <a name="unbind-using-the-wizard"></a>마법사를 사용 하 여 바인딩 해제

1. Microsoft R Server 9.1.0에 대 한 새 설치 관리자를 다운로드 합니다.
2. 바인딩 해제 하려는 인스턴스가 있는 컴퓨터에 설치 관리자를 실행 합니다.
2. 설치 프로그램을 바인딩 해제 수 있는 로컬 인스턴스를 식별 합니다.
3. 인스턴스를 원래 SQL Server R Services 구성으로 되돌리려고 옆의 확인란을 선택 취소 합니다.
4. Microsoft R Server 9.1.0에 대 한 라이선스 계약에 동의 합니다. R 서버를 제거 하는 경우에 사용권 계약에 동의 해야 합니다.
5. **마침**을 클릭합니다. 프로세스 시간이 걸립니다.

### <a name="unbind-using-the-command-line"></a>명령줄을 사용 하 여 바인딩 해제

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 되돌립니다 기본 인스턴스:
   
    `SqlBindR.exe /unbind MSSQL13.MSSQLSERVER`

## <a name="known-issues"></a>알려진 문제

이 섹션의 SqlBindR.exe 유틸리티 또는 SQL Server 인스턴스에 적용 하는 Microsoft R Server 설치 유틸리티를 사용 하 여 업그레이드를 사용 하 여 관련 알려진된 문제를 나열 합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치 된 패키지를 복원

Microsoft R Server 9.0.1와 함께 포함 된 업그레이드 유틸리티에서이 유틸리티는 원래 패키지를 복원 하지 않고 또는 R 구성 요소 완전히, 사용자는 인스턴스 복구를 실행 되도록 모든 서비스 릴리스를 적용 하 고 인스턴스를 다시 시작 합니다.

그러나 최신 버전의 Microsoft R Server 9.1.0에 대 한 업그레이드 유틸리티 원래 R 기능을 자동으로 복원 됩니다. R 구성 요소를 다시 설치 하거나 다시 서버에 패치 필요가 없습니다. 그러나 초기 설치 후 추가 된 모든 R 패키지를 설치 해야 계속 합니다.

이 작업은 훨씬 더 쉽게 패키지 관리 역할 설치 및 패키지 공유를 사용한 경우: R 명령을 사용 하 여 데이터베이스의 레코드를 사용 하 여 파일 시스템에 설치 된 패키지를 동기화 하 하며 그 반대 과정도 수행 합니다. 자세한 내용은 참조 [R 패키지를 관리 및 설치](installing-and-managing-r-packages.md)

### <a name="cannot-perform-upgrade-from-901"></a>9.0.1에서 업그레이드를 수행할 수 없습니다.

이전에 업그레이드를 완료 하면 SQL Server 2016 R Services의 인스턴스, 9.0.1 9.1.0 Microsoft R Server에 대 한 새 설치 관리자를 실행 하는 경우, 모든 유효한 인스턴스 목록이 표시 되며 기본적으로 이전에 바인딩된 인스턴스를 선택 합니다. 계속 하면 이전에 바인딩된 인스턴스 바인딩 해제 됩니다. 결과적으로 이전 9.0.1 설치한이 제거, 관련 된 패키지를 비롯 하 여 되지만 새 버전의 Microsoft R Server (9.1.0) 설치 되지 않습니다.

이 문제를 해결 기존 R 서버 설치를 다음과 같이 수정할 수 있습니다.
1. 제어판을 열고 **프로그램 추가 / 제거**합니다.
2. Microsoft R Server를 찾아서 클릭 하 여 **변경/수정**합니다.
3. 설치 관리자를 시작할 때 9.1.0 바인딩할 인스턴스를 선택 합니다.

### <a name="binding-or-unbinding-leaves-multiple-temporary-folders"></a>바인딩 또는 바인딩 해제 여러 임시 폴더에 둡니다.

경우에 따라 바인딩 및 바인딩 해제 작업이 임시 폴더를 정리 하려면 실패 합니다.
다음과 같은 이름의 폴더를 찾을 경우 설치가 완료 된 후 제거할 수 있습니다.`R_SERVICES_<guid>`

> [!NOTE]
> 설치가 완료 될 때까지 대기 해야 합니다. 하나의 버전과 관련 된 R 라이브러리를 제거한 다음 새 R 라이브러리를 추가 하는 데 시간이 오래 걸릴 수 있습니다. 작업이 완료 되 면 임시 폴더 제거 됩니다.

## <a name="sqlbindrexe-command-syntax"></a>Sqlbindr.exe 명령 구문

### <a name="usage"></a>사용법

`sqlbindr [/list] [/bind <SQL_instance_ID>] [/unbind <SQL_instance_ID>]`

### <a name="parameters"></a>매개 변수

|이름|Description|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R 서버의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R 서버를 제거하고 향후 R 서버 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

### <a name="errors"></a>오류

이 도구는 다음과 같은 오류 메시지를 반환합니다.

|오류|해결 방법|
|------|------|
|인스턴스를 바인딩하는 동안 오류가 발생했습니다.| 인스턴스를 바인딩할 수 없습니다. 지원 서비스에 문의하세요.|
|인스턴스가 이미 바인딩되어 있습니다.| *bind* 명령을 실행했지만 지정한 인스턴스가 이미 바인딩되어 있습니다. 다른 인스턴스를 선택하세요.|
|인스턴스가 바인딩되어 있지 않습니다.| *unbind* 명령을 실행했지만 지정한 인스턴스가 바인딩되어 있지 않습니다. 호환되는 다른 인스턴스를 선택하세요.|
|유효한 SQL 인스턴스 ID가 아닙니다.| 인스턴스 이름을 잘못 입력했을 수 있습니다. *list* 인수와 함께 명령을 다시 실행하여 사용 가능한 인스턴스 ID를 표시합니다.|
|인스턴스를 찾을 수 없습니다.| 이 컴퓨터에 SQL Server R Services 인스턴스가 없습니다.|
|인스턴스에 호환되는 버전의 SQL R Services(In-Database)가 설치되어 있어야 합니다.| 자세한 내용은 이 항목에서 호환성 요구 사항을 참조하세요.|
|인스턴스를 바인딩 해제하는 동안 오류가 발생했습니다.| 인스턴스를 바인딩 해제할 수 없습니다. 지원 서비스에 문의하세요.|
|예기치 않은 오류가 발생했습니다.| 기타 오류입니다. 지원 서비스에 문의하세요.  |
|SQL 인스턴스를 찾을 수 없습니다.| 이 컴퓨터에 SQL Server 인스턴스가 없습니다. |

자세한 내용은 Microsoft R Server에 대 한 릴리스 정보를 참조 합니다.

+ [R Server의 새로운 기능](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [R 서버 알려진 문제](https://docs.microsoft.com/r-server/resources-known-issues)

