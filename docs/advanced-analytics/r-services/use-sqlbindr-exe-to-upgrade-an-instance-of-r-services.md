---
title: "SqlBindR.exe를 사용하여 R Services 인스턴스 업그레이드 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server (starting with 2016 CTP3)"
ms.assetid: 4da80998-f929-4fad-a86f-87d09c1a79ef
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# SqlBindR.exe를 사용하여 R Services 인스턴스 업그레이드
Windows용 Microsoft R Server에는 인스턴스에 대한 R 구성 요소를 업그레이드하는 데 사용할 수 있는 **SqlBindR.exe**라는 새로운 도구가 포함되어 있습니다. 이 프로세스는 SQL Server 2016 인스턴스에서 새 Microsoft 최신 소프트웨어 수명 주기 지원 라이선스를 사용하도록 라이선스 모델을 변경하기 때문에 **바인딩**이라고 합니다.

일반적으로 이 라이선스 시스템은 데이터 과학자가 항상 최신 버전의 R을 사용하도록 합니다. Microsoft 소프트웨어 사용 조건 및 이점에 대한 자세한 내용은 [Windows용 Microsoft R Server 실행](https://msdnstage.redmond.corp.microsoft.com/en-us/microsoft-r/rserver-install-windows?branch=r-server-nov16-dev)을 참조하세요.

인스턴스를 바인딩하면 다음 세 가지 작업이 수행됩니다.
+ 인스턴스에 대한 지원 정책이 SQL Server 2016 지원 정책에서 새 Microsoft 최신 소프트웨어 사용권 계약으로 변경됩니다.
+ 새 최신 소프트웨어 사용 조건에서 최신 버전인 R 서버 버전과 잠금 단계에서는 각 릴리스마다 해당 인스턴스와 연결된 R 구성 요소가 자동으로 업그레이드됩니다.
+ 새 패키지를 추가하는 경우를 제외하고 더 이상 수동으로 인스턴스를 업데이트할 수 없습니다. 

나중에 각 릴리스마다 인스턴스를 업그레이드하지 않으려는 경우 인스턴스를 **바인딩 해제**한 다음 [Windows용 Microsoft R Server 실행](https://msdn.microsoft.com/microsoft-r/rserver-install-windows) 문서에 설명된 대로 Microsoft R Server 구성 요소를 제거해야 합니다. 프로세스가 완료되면 이후 R 서버 업그레이드는 인스턴스에 더 이상 영향을 주지 않습니다.

> [!NOTE] 업그레이드 프로세스는 누적 업데이트 3.0으로 패치된 SQL Server 2016 인스턴스에 대해서만 지원됩니다.  
> 
> SQL Server vNext에서 R Services를 사용하는 경우에는 이 업그레이드를 적용할 필요가 없습니다. R 구성 요소는 각 중요 시점마다 항상 자동으로 업그레이드됩니다.

## <a name="how-to-upgrade-an-instance"></a>인스턴스를 업그레이드하는 방법


1. 업그레이드하려는 인스턴스가 있는 컴퓨터에서 Microsoft R Server 설치 관리자를 실행합니다.
2. 설치가 완료되면 **SqlBindR.exe** 도구가 포함된 폴더를 찾습니다. 기본 위치는 `C:\Program Files\Microsoft\R Server\Setup`입니다.
2. 관리자 권한으로 명령 프롬프트를 엽니다.
3. 다음 명령을 입력하여 사용 가능한 인스턴스 목록을 표시합니다. `SqlBindR.exe /list`
4. */bind* 인수와 함께 **SqlBindR.exe** 명령을 실행하여 업그레이드할 인스턴스의 이름을 지정합니다. 
   예를 들어 기본 인스턴스만 업그레이드하려면 다음을 입력합니다.  `SqlBindR.exe /bind MSSQL14.MSSQLSERVER`

## <a name="how-to-downgrade-an-instance-of-r-services"></a>R Services 인스턴스를 다운그레이드하는 방법

인스턴스 상태를 되돌리려면 SqlBindR 도구를 실행하여 라이선스를 제거한 다음 인스턴스를 복구하거나 다시 설치해야 합니다.

1. */unbind* 인수와 함께 **SqlBindR.exe** 명령을 실행하고 인스턴스를 지정합니다. 
   예를 들어 다음 명령은 SQL Server 라이선스 및 SQL Server 업데이트 일정을 준수하도록 기본 인스턴스를 되돌립니다.  `SqlBindR.exe /unbind MSSQL14.MSSQLSERVER`
2. 다음 중 하나를 수행하여 인스턴스를 원래 상태로 복원합니다.
    + 인스턴스를 복구합니다. 복구 작업은 설치된 모든 기능에 업데이트를 적용합니다.
    + 모든 서비스 릴리스를 제거하고 다시 설치한 다음 적용합니다. 인스턴스를 다시 시작해야 합니다.
3. R 서버를 제거하면 인스턴스와 함께 설치된 패키지도 모두 제거되므로 다시 설치해야 합니다.

## <a name="requirements"></a>요구 사항
업그레이드는 다음 요구 사항을 충족하는 SQL Server 2016 인스턴스에 대해서만 지원됩니다.
+ SQL Server 2016 SP1 이상
+ 누적 업데이트 3.0(OD)이 적용됨

현재 업그레이드는 명령줄 도구를 사용해야만 지원됩니다. 대화형 인터페이스는 이후 릴리스에서 제공됩니다.

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
|인스턴스가 바인딩되어 있지 않습니다.| *unbind* 명령을 실행했지만 지정한 인스턴스가 바인딩되어 있지 않습니다. 다른 인스턴스를 선택하세요.|
|유효한 SQL 인스턴스 ID가 아닙니다.| 인스턴스 이름을 잘못 입력했을 수 있습니다. *list* 인수와 함께 명령을 다시 실행하여 사용 가능한 인스턴스 ID를 표시합니다.|
|인스턴스를 찾을 수 없습니다.| 이 컴퓨터에 SQL Server R Services 인스턴스가 없습니다.|
|인스턴스에 호환되는 버전의 SQL R Services(In-Database)가 설치되어 있어야 합니다.| 자세한 내용은 https://go.microsoft.com/fwlink/?linkid=835761을 참조하세요.|
|인스턴스를 바인딩 해제하는 동안 오류가 발생했습니다.| 인스턴스를 바인딩 해제할 수 없습니다. 지원 서비스에 문의하세요.|
|예기치 않은 오류가 발생했습니다.| 기타 오류입니다. 지원 서비스에 문의하세요.  |
|SQL 인스턴스를 찾을 수 없습니다.| 이 컴퓨터에 SQL Server 인스턴스가 없습니다. |


## <a name="see-also"></a>관련 항목:

[R 서버 릴리스 정보](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes)
