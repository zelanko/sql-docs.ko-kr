---
title: "TSQL 디버거를 실행하기 전에 방화벽 규칙 구성 | Microsoft 문서"
ms.custom: 
ms.date: 10/20/2016
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- vs.debug.error.sqlde_register_failed
- vs.debug.error.sqlde_accessdenied
- vs.debug.error.sqlde_firewall.remotemachines
helpviewer_keywords:
- Transact-SQL debugger, remote connections
- Windows Firewall [Database Engine], Transact-SQL debugger
- Transact-SQL debugger, Windows Firewall
- Transact-SQL debugger, configuring
- ports [SQL Server], Transact-SQL debugger
- TCP/IP [SQL Server], port numbers
ms.assetid: f50e0b0d-eaf0-4f4a-be83-96f5be63e7ea
caps.latest.revision: "43"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 072d92452d554a439ab05010d62f5fcf624f2c4c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-firewall-rules-before-running-the-tsql-debugger"></a>TSQL 디버거를 실행 하기 전에 방화벽 규칙 구성
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기와 다른 컴퓨터에서 실행 중인 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스에 연결된 경우 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버깅을 사용하도록 Windows 방화벽 규칙을 구성해야 합니다.  
  
## <a name="configuring-the-transact-sql-debugger"></a>Transact-SQL 디버거 구성  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거는 서버 쪽 구성 요소와 클라이언트 쪽 구성 요소를 모두 포함합니다. 서버 쪽 디버거 구성 요소는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2(서비스 팩 2) 이상의 각 데이터베이스 엔진 인스턴스와 함께 설치됩니다. 클라이언트 쪽 디버거 구성 요소는 다음과 같은 경우에 설치됩니다.  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상에서 클라이언트 쪽 도구를 설치할 때  
  
-   Microsoft Visual Studio 2010 이상을 설치할 때  
  
-   웹 다운로드에서 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 를 설치할 때  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 또는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 가 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 인스턴스와 같은 컴퓨터에서 실행되는 경우 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]디버거를 실행하기 위한 구성 요구 사항이 없습니다. 그러나 [!INCLUDE[tsql](../../includes/tsql-md.md)] 의 원격 인스턴스에 연결된 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)]디버거를 실행하려면 두 컴퓨터 모두에서 Windows 방화벽의 프로그램 및 포트 규칙을 사용하도록 설정해야 합니다. 이러한 규칙은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 설치 프로그램에서 만들 수 있습니다. 원격 디버거 세션을 열려고 하는 동안 오류가 발생하면 다음 방화벽 규칙이 컴퓨터에 정의되어 있는지 확인합니다.  
  
 **고급 보안이 포함된 Windows 방화벽** 응용 프로그램을 사용하여 방화벽 규칙을 관리합니다. [!INCLUDE[win7](../../includes/win7-md.md)] 및 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]에서 **제어판**, **Windows 방화벽**을 차례로 열고 **고급 설정**을 선택합니다. [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] 에서는 **서비스 관리자**를 열고 왼쪽 창에서 **구성** 을 확장한 다음 **고급 보안이 포함된 Windows 방화벽**을 확장할 수도 있습니다.  
  
> [!CAUTION]  
>  Windows 방화벽의 규칙을 사용하도록 설정하면 방화벽에 의해 차단되도록 설계된 컴퓨터가 보안 위협에 노출될 수 있습니다. 원격 디버깅에 대한 규칙을 사용하도록 설정하면 이 항목에 나열된 포트와 프로그램이 차단됩니다.  
  
## <a name="firewall-rules-on-the-server"></a>서버의 방화벽 규칙  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]인스턴스를 실행하는 컴퓨터에서 **고급 보안이 포함된 Windows 방화벽** 을 사용하여 다음 정보를 지정합니다.  
  
-   sqlservr.exe에 대한 인바운드 프로그램 규칙을 추가합니다. 원격 디버깅 세션을 지원해야 하는 인스턴스당 하나의 규칙이 있어야 합니다.  
  
    1.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 작업 창에서 **새 규칙** 을 선택합니다.  
  
    2.  **규칙 유형** 대화 상자에서 **프로그램**을 선택하고 **다음**을 클릭합니다.  
  
    3.  **프로그램** 대화 상자에서 **다음 프로그램 경로:** 를 선택하고 이 인스턴스에 대한 sqlservr.exe의 전체 경로를 입력합니다. 기본적으로 sqlservr.exe는 C:\Program Files\Microsoft SQL Server\MSSQL13.*InstanceName*\MSSQL\Binn에 설치됩니다. 여기서 *InstanceName* 은 기본 인스턴스의 경우 MSSQLSERVER이고 명명된 임의 인스턴스의 경우 해당 인스턴스 이름입니다.  
  
    4.  **동작** 대화 상자에서 **연결 허용**을 선택하고 **다음**을 클릭합니다.  
  
    5.  **프로필** 대화 상자에서 해당 인스턴스와 함께 디버깅 세션을 열 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택하고 **다음**을 클릭합니다.  
  
    6.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
    7.  **인바운드 규칙** 목록에서 방금 만든 규칙을 마우스 오른쪽 단추로 클릭한 다음 동작 창에서 **속성** 을 선택합니다.  
  
    8.  **프로토콜 및 포트** 탭을 선택합니다.  
  
    9. **프로토콜 종류:** 상자에서는 **TCP** 를 선택하고 **로컬 포트:** 상자에서는 **RPC 동적 포트** 를 선택한 후에 **적용**, **확인**을 차례로 클릭합니다.  
  
-   svchost.exe에 대한 인바운드 프로그램을 추가하여 원격 디버거 세션에서 DCOM 통신을 사용하도록 설정합니다.  
  
    1.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 작업 창에서 **새 규칙** 을 선택합니다.  
  
    2.  **규칙 유형** 대화 상자에서 **프로그램**을 선택하고 **다음**을 클릭합니다.  
  
    3.  **프로그램** 대화 상자에서 **다음 프로그램 경로:** 를 선택하고 svchost.exe의 전체 경로를 입력합니다. 기본적으로 svchost.exe는 %systemroot%\System32\svchost.exe에 설치됩니다.  
  
    4.  **동작** 대화 상자에서 **연결 허용**을 선택하고 **다음**을 클릭합니다.  
  
    5.  **프로필** 대화 상자에서 해당 인스턴스와 함께 디버깅 세션을 열 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택하고 **다음**을 클릭합니다.  
  
    6.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
    7.  **인바운드 규칙** 목록에서 방금 만든 규칙을 마우스 오른쪽 단추로 클릭한 다음 동작 창에서 **속성** 을 선택합니다.  
  
    8.  **프로토콜 및 포트** 탭을 선택합니다.  
  
    9. **프로토콜 종류:** 상자에서는 **TCP** 를 선택하고 **로컬 포트:** 상자에서는 **RPC 끝점 매퍼** 를 선택한 후에 **적용**, **확인**을 차례로 클릭합니다.  
  
-   도메인 정책에 따라 IPSec을 통해 네트워크 통신을 수행해야 하는 경우 UDP 포트 4500 및 UDP 포트 500을 여는 인바운드 규칙도 추가해야 합니다.  
  
## <a name="firewall-rules-on-the-client"></a>클라이언트의 방화벽 규칙  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기를 실행하는 컴퓨터에서는 SQL Server 설치 프로그램이나 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 설치 프로그램이 원격 디버깅을 허용하도록 Windows 방화벽을 구성했을 수 있습니다.  
  
 원격 디버깅 세션을 열려고 하는 동안 오류가 발생하면 다음과 같이 **고급 보안이 포함된 Windows 방화벽** 을 사용하여 방화벽 규칙을 구성함으로써 수동으로 프로그램 및 포트 예외를 구성할 수 있습니다.  
  
-   다음과 같이 svchost에 대한 프로그램 항목을 추가합니다.  
  
    1.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 작업 창에서 **새 규칙** 을 선택합니다.  
  
    2.  **규칙 유형** 대화 상자에서 **프로그램**을 선택하고 **다음**을 클릭합니다.  
  
    3.  **프로그램** 대화 상자에서 **다음 프로그램 경로:** 를 선택하고 svchost.exe의 전체 경로를 입력합니다. 기본적으로 svchost.exe는 %systemroot%\System32\svchost.exe에 설치됩니다.  
  
    4.  **동작** 대화 상자에서 **연결 허용**을 선택하고 **다음**을 클릭합니다.  
  
    5.  **프로필** 대화 상자에서 해당 인스턴스와 함께 디버깅 세션을 열 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택하고 **다음**을 클릭합니다.  
  
    6.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
    7.  **인바운드 규칙** 목록에서 방금 만든 규칙을 마우스 오른쪽 단추로 클릭한 다음 동작 창에서 **속성** 을 선택합니다.  
  
    8.  **프로토콜 및 포트** 탭을 선택합니다.  
  
    9. **프로토콜 종류:** 상자에서는 **TCP** 를 선택하고 **로컬 포트:** 상자에서는 **RPC 끝점 매퍼** 를 선택한 후에 **적용**, **확인**을 차례로 클릭합니다.  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기를 호스팅하는 응용 프로그램에 대한 프로그램 항목을 추가합니다. 같은 컴퓨터에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 및 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 의 원격 디버깅 세션을 둘 다 열어야 하는 경우 다음과 같이 두 세션 모두에 대한 프로그램 규칙을 추가해야 합니다.  
  
    1.  **고급 보안이 포함된 Windows 방화벽**의 왼쪽 창에서 **인바운드 규칙**을 마우스 오른쪽 단추로 클릭한 다음 작업 창에서 **새 규칙** 을 선택합니다.  
  
    2.  **규칙 유형** 대화 상자에서 **프로그램**을 선택하고 **다음**을 클릭합니다.  
  
    3.  **프로그램** 대화 상자에서 **다음 프로그램 경로:** 를 선택하고 다음 세 값 중 하나를 입력합니다.  
  
        -   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 경우 ssms.exe에 대한 전체 경로를 입력합니다. 기본적으로 ssms.exe는 C:\Program Files (x86)\Microsoft SQL Server\130\Tools\Binn\Management Studio에 설치됩니다.  
  
        -   [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 의 경우 devenv.exe의 전체 경로를 입력합니다.  
  
            1.  기본적으로 Visual Studio 2010용 devenv.exe는 C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\IDE에 있습니다.  
  
            2.  기본적으로 Visual Studio 2012용 devenv.exe는 C:\Program Files (x86)\Microsoft Visual Studio 11.0\Common7\IDE에 있습니다.  
  
            3.  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 시작하기 위해 사용하는 바로 가기에서 ssms.exe에 대한 경로를 찾을 수 있습니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]를 시작하기 위해 사용하는 바로 가기에서 devenv.exe에 대한 경로를 찾을 수 있습니다. 바로 가기를 마우스 오른쪽 단추로 클릭하고 **속성**을 선택합니다. 실행 파일과 경로가 **대상** 상자에 나열됩니다.  
  
    4.  **동작** 대화 상자에서 **연결 허용**을 선택하고 **다음**을 클릭합니다.  
  
    5.  **프로필** 대화 상자에서 해당 인스턴스와 함께 디버깅 세션을 열 때의 컴퓨터 연결 환경을 설명하는 프로필을 선택하고 **다음**을 클릭합니다.  
  
    6.  **이름** 대화 상자에 이 규칙의 이름 및 설명을 입력한 다음 **마침**을 클릭합니다.  
  
    7.  **인바운드 규칙** 목록에서 방금 만든 규칙을 마우스 오른쪽 단추로 클릭한 다음 동작 창에서 **속성** 을 선택합니다.  
  
    8.  **프로토콜 및 포트** 탭을 선택합니다.  
  
    9. **프로토콜 종류:** 상자에서는 **TCP** 를 선택하고 **로컬 포트:** 상자에서는 **RPC 동적 포트** 를 선택한 후에 **적용**, **확인**을 차례로 클릭합니다.  
  
## <a name="requirements-for-starting-the-debugger"></a>디버거 시작을 위한 요구 사항  
 다음 요구 사항을 충족해야 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 시작할 수 있습니다.  
  
* [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 는 sysadmin 고정 서버 역할의 멤버인 Windows 계정으로 실행해야 합니다.  
  
* sysadmin 고정 서버 역할의 멤버인 Windows 인증 또는 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인증 로그인을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 쿼리 편집기 창을 연결해야 합니다.  
  
* [!INCLUDE[ssDE](../../includes/ssde-md.md)] 쿼리 편집기 창을 [!INCLUDE[ssDE](../../includes/ssde-md.md)] SP2(서비스 팩 2) 이상의 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 인스턴스에 연결해야 합니다. 쿼리 편집기 창이 단일 사용자 모드에 있는 인스턴스에 연결되어 있는 경우에는 디버거를 실행할 수 없습니다.

* 서버는 RPC를 통해 클라이언트와 다시 통신해야 합니다. SQL Server 서비스를 실행 중인 계정에 클라이언트에 대한 인증 권한이 있어야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [Transact-SQL 디버거](../../relational-databases/scripting/transact-sql-debugger.md)   
 [Transact-SQL 디버거 실행](../../relational-databases/scripting/run-the-transact-sql-debugger.md)   
 [Transact-SQL 코드 단계별 실행](../../relational-databases/scripting/step-through-transact-sql-code.md)   
 [Transact-SQL 디버거 정보](../../relational-databases/scripting/transact-sql-debugger-information.md)   
 [데이터베이스 엔진 쿼리 편집기&#40;SQL Server Management Studio&#41;](../../relational-databases/scripting/database-engine-query-editor-sql-server-management-studio.md)  
  
  
