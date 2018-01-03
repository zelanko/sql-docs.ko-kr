---
title: "SQL Server 인스턴스의 컴퓨터 학습 구성 요소를 업그레이드 | Microsoft Docs"
ms.custom: 
ms.date: 10/31/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server (starting with 2016 CTP3)
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: "15"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: e83922e15c8bea5f26dcc5c1992acc0529daf18c
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/20/2017
---
# <a name="upgrade-machine-learning-components-in-a-sql-server-instance"></a>SQL Server 인스턴스의 컴퓨터 학습 구성 요소 업그레이드

이 문서에서는의 과정을 설명 합니다. _바인딩_, 기계 학습 SQL Server에서 사용 되는 구성 요소를 업그레이드 하는 데 사용할 수 있습니다. 바인딩 프로세스 서버 기반으로 컴퓨터 학습 서버의 릴리스에서 업데이트 흐름으로, SQL Server를 사용 하는 대신 릴리스를 잠그고 일정을 업데이트 합니다.

> [!IMPORTANT]
> SQL Server 업데이트의 일부로 업그레이드 확보 하려는 경우이 업그레이드 프로세스를 사용할 필요가 없습니다. 새 서비스 팩 또는 서비스 릴리스를 설치할 때마다 컴퓨터 학습 구성 요소는 항상 자동으로 최신 버전으로 업그레이드 됩니다. 만 사용 하 여는 _바인딩_ 서비스 릴리스에서 SQL Server에서 제공 하는 것 보다 더 빠른 속도로 구성 요소를 업그레이드 하려는 경우를 처리 합니다.

언제 든 지 서버를 학습 하는 컴퓨터 일정에 따라 업그레이드를 중지 하려면 수행 해야 하는 경우 _바인딩 해제_ 에 설명 된 대로 인스턴스 [이 섹션](#bkmk_Unbind), 및 학습 서버 컴퓨터를 제거 합니다.

**적용 대상:** SQL Server 2016 R Services, SQL Server 2017 기계 학습 서비스

## <a name="binding-vs-upgrading"></a>업그레이드 및 바인딩

기계 학습 구성 요소를 업그레이드 하는 프로세스 라고 **바인딩**새로운 최신 소프트웨어 수명 주기 정책을 사용 하 여 SQL Server 컴퓨터 학습 구성 요소에 대 한 지원 모델을 변경 하기 때문에, 합니다. 

일반적으로 새 라이선스 모델을 전환 하면 데이터 과학자 R, Python의 최신 버전을 항상 사용할 수 있습니다. 최신 수명 주기 정책 조건에 대 한 자세한 내용은 참조 [Microsoft R Server에 대 한 지원 타임 라인](https://docs.microsoft.com/machine-learning-server/resources-servicing-support)합니다.

> [!NOTE]
> 업그레이드는 SQL Server 데이터베이스에 대 한 지원 모델을 변경 하지 하 고 SQL Server의 버전을 변경 하지 않습니다.

인스턴스를 바인딩하면 다음과 같은 여러 작업이 수행됩니다.

+ 지원 모델 변경 됩니다. SQL Server 서비스 릴리스를 사용 하지 않고 지원 새로운 최신 주기 정책을 기반으로 합니다.
+ 인스턴스와 연결 된 컴퓨터 학습 구성 요소의 새 최신 수명 주기 정책에 따라 최신 버전으로 잠금 단계에서는 각 릴리스마다 자동으로 업그레이드 됩니다. 
+ 새 R, Python 패키지 추가 될 수 있습니다. 예를 들어 이전 업데이트가 Microsoft R Server 9.1에 따라 추가 새 R 패키지와 같은 [MicrosoftML](../using-the-microsoftml-package.md), [olapR](../r/how-to-create-mdx-queries-using-olapr.md), 및 [sqlrutils](../r/how-to-create-a-stored-procedure-using-sqlrutils.md)합니다.
+ 새 패키지를 추가하는 경우를 제외하고 더 이상 수동으로 인스턴스를 업데이트할 수 없습니다.
+ Microsoft에서 제공 하는 미리 학습 된 모델을 설치 하는 옵션을 얻게 됩니다.

## <a name="bkmk_prereqs"></a>Prerequisites

먼저에 적합 한 업그레이드 인스턴스를 확인 합니다. 설치 프로그램을 실행 하 고 바인딩 옵션을 선택 하는 경우 업그레이드와 호환 되는 인스턴스 목록을 반환 합니다.

지원 되는 업그레이드 및 요구 사항 목록은 다음 표를 참조 하십시오.

| SQL Server 버전| 지원 되는 업그레이드| 참고|
|-----|-----|------|
| SQL Server 2016| 기계 학습 9.2.1 서버| 최소한 서비스 팩 1을 더한 CU3 합니다. R Services는 설치 하 고 사용 하도록 설정 해야 합니다.|
| SQL Server 2017| 기계 학습 9.2.1 서버| 컴퓨터 학습 Services (In-database) 설치 하 고 사용 하도록 설정 해야 합니다. |

## <a name="bind-or-upgrade-an-instance"></a>바인딩 또는 인스턴스 업그레이드

컴퓨터 학습 서버에 대 한 Windows 언어 및 SQL Server의 인스턴스에 연결 된 도구를 학습 하는 컴퓨터를 업그레이드 하는 데 사용할 수 있는 도구에 포함 됩니다. 두 가지 버전의 도구: 마법사, 그리고 명령줄 유틸리티입니다.

마법사 또는 명령줄 도구를 실행 하려면 먼저 구성 요소를 학습 하는 컴퓨터에 대 한 독립 실행형 설치 관리자의 최신 버전을 다운로드 해야 합니다.

+ [Windows에 대 한 서버 9.2.1 학습 컴퓨터 설치](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-install)

+ [오프 라인 설치에 필요한 구성 요소를 다운로드 합니다.](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-offline)

### <a name="bkmk_BindWizard"></a>새로운 설치 마법사를 사용 하 여 업그레이드

1. 서버를 학습 하는 컴퓨터에 대 한 새 설치 관리자를 시작 합니다. 업그레이드 하려는 인스턴스가 있는 컴퓨터에서 설치 프로그램을 실행 해야 합니다.

    ![Microsoft 컴퓨터 학습 서버 설치 마법사](media/mls-921-installer-start.PNG)

2. 페이지에서 **설치를 구성**를 업그레이드 하려면 구성 요소를 확인 하 고 호환 인스턴스 목록을 검토 합니다. 인스턴스가 표시 되 면 확인는 [필수 구성 요소](#bkmk_prereqs)합니다.

    인스턴스를 업그레이드 하려면 인스턴스 이름 옆의 확인란을 선택 합니다. 인스턴스 선택 하지 않으면 서버를 학습 하는 컴퓨터의 별도 설치 만들어지고 SQL Server 라이브러리는 변경 되지 않습니다.

    ![Microsoft 컴퓨터 학습 서버 설치 마법사](media/configure-the-installation.PNG)

3. 에 **사용권 계약** 페이지에서 **이러한 조건에 동의** 학습 서버 컴퓨터에 대 한 라이선스 조건에 동의 합니다. 

4. 연속 페이지에서 선택한 Microsoft R Open 또는 Python Anaconda 배포와 같은 오픈 소스 구성 요소에 대 한 추가 라이선스 조건에 동의 하 게 제공 합니다.

5. 에 **얼마 남지** 페이지에서 설치 폴더를 기록 합니다. 기본 폴더는 `~\Program Files\Microsoft\ML Server`합니다.

    설치 폴더를 변경 하려면 클릭 **고급** 마법사의 첫 페이지로 돌아갑니다. 그러나 이전에 선택한 항목을 반복 해야 합니다.

6. 오프 라인 구성 요소를 설치 하는 경우 Microsoft R Open, Python 서버 및 Python 열기 등 필요한 컴퓨터 학습 구성 요소 위치에 대 한 라는 메시지가 표시 될 수 있습니다.

설치 과정에서 SQL Server에서 사용 하는 모든 Python 또는 R 라이브러리 대체 하 고 실행 패드 최신 구성 요소를 사용 하도록 업데이트 됩니다. 결과적으로, 인스턴스 라이브러리 기본 R_SERVICES 폴더에 이전에 사용한 경우 업그레이드 후 이러한 라이브러리 제거 되 고 새 위치에는 라이브러리를 사용 하는 실행 패드 서비스에 대 한 속성 변경 됩니다.

### <a name="bkmk_BindCmd"></a>명령줄을 사용 하 여 업그레이드

마법사를 사용 하지 않을 경우 컴퓨터 학습 서버를 설치 하 고의 인스턴스를 업그레이드 하려면 명령줄에서 SqlBindR.exe 도구를 실행할 수 있습니다.

> [!TIP]
> 
> SqlBindR.exe를 찾을 수 없나요? 아마도 위에 나열 된 구성 요소 다운로드 하지 않은 합니다. 이 유틸리티는 학습 서버 컴퓨터에 대 한 Windows installer에만 사용할 수 있습니다.

1. 관리자 권한으로 명령 프롬프트를 열고 sqlbindr.exe가 포함된 폴더로 이동합니다. 기본 위치는`C:\Program Files\Microsoft\MLServer\Setup`

2. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
  
   전체 인스턴스 이름을 나열된 대로 기록해 둡니다. 예를 들어, 인스턴스 이름 수 있습니다 `MSSQL14.MSSQLSERVER` 기본 인스턴스 또는 같은 `SERVERNAME.MYNAMEDINSTANCE`합니다.

3. 실행 된 **SqlBindR.exe** 명령에 *바인딩/* 인수를 하 고 이전 단계에서 반환 된 인스턴스 이름을 사용 하 여를 업그레이드 하려면 인스턴스의 이름을 지정 합니다.

   예를 들어 기본 인스턴스를 업그레이드 하려면 다음을 입력 합니다.`SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

4. 업그레이드가 완료 되 면 수정 된 인스턴스와 관련 된 실행 패드 서비스를 다시 시작 합니다.

## <a name="bkmk_Unbind"></a>Revert 또는 인스턴스를 바인딩 해제

먼저는 더 이상 업그레이드 하려는 기계 학습 서버를 학습 하는 컴퓨터를 사용 하 여 구성 요소를 결정 한 경우 _바인딩 해제_ 인스턴스를 다음 서버를 학습 하는 컴퓨터를 제거 합니다.

+ 인스턴스를 바인딩 해제

    인스턴스를 바인딩 해제 및 이러한 두 가지 방법 중 하나를 사용 하 여 SQL Server가 설치 된 원래 라이브러리도 되돌릴 수 있습니다.

    + [설치 마법사를 사용 하 여](#bkmk_wizunbind) 컴퓨터 학습 서버에 대 한 인스턴스의 모든 기능을 선택 취소 하 고
    + [SqlBindR 유틸리티를 사용 하 여](#bkmk_cmdunbind) 와 `/unbind` 인수, 인스턴스 이름이 차례로 나옵니다.

    바인딩 해제 프로세스가 완료 되 면 이후 기계 학습 서버 컴퓨터에 따라 업그레이드 학습 인스턴스에 더 이상 적용 됩니다.

+ 기계 학습 서버 제거

    자세한 내용은 [Windows 용 컴퓨터 학습 서버 제거](https://docs.microsoft.com/machine-learning-server/install/machine-learning-server-windows-uninstall)합니다. 

### <a name="bkmk_wizunbind"></a>마법사를 사용 하 여 바인딩 해제

1. 서버를 학습 하는 컴퓨터에 대 한 설치 관리자를 찾습니다. 설치 프로그램을 제거한 경우 다시 다운로드 하거나 다른 컴퓨터에서 복사를 할 수 있습니다.
2. 바인딩 해제 하려는 인스턴스가 있는 컴퓨터에서 설치 프로그램을 실행 해야 합니다.
2. 설치 프로그램을 바인딩 해제 수 있는 로컬 인스턴스를 식별 합니다.
3. 인스턴스를 원래 구성으로 되돌리려고 옆의 확인란을 선택 취소 합니다.
4. 사용권 계약에 동의 합니다. 설치 하는 경우에 사용 조건 수락을 지정 해야 합니다.
5. **마침**을 클릭합니다. 프로세스 시간이 걸립니다.

### <a name="bkmk_cmdunbind"></a>명령줄을 사용 하 여 바인딩 해제

1. 이전 섹션에 설명된 대로 명령 프롬프트를 열고 **sqlbindr.exe**가 포함된 폴더로 이동합니다.

2. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다.

   예를 들어 다음 명령은 되돌립니다 기본 인스턴스:
   
    `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`

## <a name="known-issues"></a>알려진 문제

이 섹션의 SqlBindR.exe 유틸리티 또는 업그레이드에 영향을 미치는 SQL Server 인스턴스 학습 서버 컴퓨터의 경우에 사용 하 여 관련 알려진된 문제를 나열 합니다.

### <a name="restoring-packages-that-were-previously-installed"></a>이전에 설치 된 패키지를 복원

Microsoft R Server 9.0.1와 함께 포함 된 업그레이드 유틸리티에서이 유틸리티는 원래 패키지를 복원 하지 않고 또는 R 구성 요소 완전히, 사용자는 인스턴스 복구를 실행 되도록 모든 서비스 릴리스를 적용 하 고 인스턴스를 다시 시작 합니다.

그러나 최신 버전의 업그레이드 유틸리티는 자동으로 원래 R 기능을 복원합니다. R 구성 요소를 다시 설치 하거나 다시 서버에 패치 필요가 없습니다. 그러나 초기 설치 후 추가 된 모든 R 패키지를 설치 해야 합니다.

이 작업은 훨씬 더 쉽게 패키지 관리 역할 설치 및 패키지 공유를 사용한 경우: R 명령을 사용 하 여 데이터베이스의 레코드를 사용 하 여 파일 시스템에 설치 된 패키지를 동기화 하 하며 그 반대 과정도 수행 합니다. 자세한 내용은 참조 [SQL Server에 대 한 R 패키지 관리](r-package-management-for-sql-server-r-services.md)합니다.

### <a name="problems-with-multiple-upgrades-from-sql-server"></a>SQL Server에서 여러 업그레이드 문제

Microsoft R Server 9.1.0에 대 한 새 설치 관리자를 실행 하면 SQL Server 2016 R Services의 인스턴스를 9.0.1, 업그레이드 이전에 한 경우 모든 유효한 인스턴스 목록을 표시 하 고 기본적으로 이전에 바인딩된 인스턴스를 선택 합니다. 계속 하면 이전에 바인딩된 인스턴스 바인딩 해제 됩니다. 결과적으로 이전 9.0.1 설치한이 제거, 관련 된 패키지를 비롯 하 여 되지만 새 버전의 Microsoft R Server (9.1.0) 설치 되지 않습니다.

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

|속성|Description|
|------|------|
|*list*| 현재 컴퓨터의 모든 SQL Database 인스턴스 ID 목록을 표시합니다.|
|*bind*| 지정된 SQL Database 인스턴스를 최신 버전의 R 서버로 업그레이드하고 인스턴스가 R 서버의 향후 업그레이드를 자동으로 가져오도록 합니다.|
|*unbind*|지정된 SQL Database 인스턴스에서 최신 버전의 R 서버를 제거하고 향후 R 서버 업그레이드가 인스턴스에 영향을 주지 않도록 합니다.|

### <a name="errors"></a>오류

이 도구는 다음과 같은 오류 메시지를 반환합니다.

|Error|해결 방법|
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

+ [서버를 학습 하는 컴퓨터의 알려진된 문제](https://docs.microsoft.com/machine-learning-server/resources-known-issues)

+ [R Server의 이전 릴리스에서 기능 공지 사항](https://docs.microsoft.com/r-server/whats-new-in-r-server)

+ [사용 되지 않는, 지원 되지 않는 추가 되거나 변경 된 기능](https://docs.microsoft.com/machine-learning-server/resources-deprecated-features)
