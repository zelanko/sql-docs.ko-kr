---
title: Linux용 SQL Server 데이터베이스 개발 및 배포 | Microsoft Docs
description: ''
author: VanMSFT
ms.author: vanto
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.openlocfilehash: c6d5789092ea2bbfc6fd9a8bb20cc7d078eaf6de
ms.sourcegitcommit: c4258a644ac588fc222abee2854f89a81325814c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/17/2019
ms.locfileid: "72545049"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Visual Studio를 사용하여 SQL Server on Linux 데이터베이스 만들기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SSDT(SQL Server Data Tools)를 통해 Visual Studio는 SQL Server on Linux를 위한 강력한 개발 및 DLM(데이터베이스 수명 주기 관리) 환경으로 전환됩니다. 원본 제어 프로젝트에서 데이터베이스를 개발, 빌드, 테스트 및 게시할 수 있습니다. 애플리케이션 코드를 개발하는 것과 같습니다.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Visual Studio 및 SQL Server Data Tools 설치

1. Windows 머신에서 Visual Studio를 아직 설치하지 않은 경우 [Visual Studio를 다운로드하여 설치](https://visualstudio.microsoft.com/downloads/)합니다. Visual Studio 라이선스가 없으면 학생, 오픈 소스 및 개인 개발자를 위한 모든 기능을 갖춘 체험 IDE인 Visual Studio Community 버전을 사용할 수 있습니다.

2. Visual Studio 설치 중에 **설치 유형 선택** 옵션에서 **사용자 지정**을 선택합니다. **다음**을 클릭합니다.

3. 기능 선택 목록에서 **Microsoft SQL Server Data Tools**, **Git for Windows** 및 **GitHub Extension for Visual Studio**를 선택합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. 계속 진행하여 Visual Studio 설치를 완료합니다. 몇 분 정도 걸릴 수 있습니다.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>SSDT 17.0 RC 릴리스로 SQL Server Data Tools 업그레이드

SQL Server on Linux는 SSDT 버전 17.0 RC 이상에서 지원됩니다.

* [SSDT 17.0 RC2를 다운로드하여 설치](https://go.microsoft.com/fwlink/?linkid=837939)합니다.

## <a name="create-a-new-database-project-in-source-control"></a>원본 제어에서 새 데이터베이스 프로젝트 만들기

1. Visual Studio를 시작합니다.

2. **보기** 메뉴에서 **팀 탐색기**를 선택합니다. 

3. **연결** 페이지의 **로컬 Git 리포지토리** 섹션에서 **새로 만들기**를 클릭합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. **만들기**를 클릭합니다. 로컬 Git 리포지토리를 만든 후에 **SSDTRepo**를 두 번 클릭합니다.

4. **솔루션** 섹션에서 **새로 만들기**를 클릭합니다. **새 프로젝트** 대화 상자의 **기타 언어** 노드에서 **SQL Server**를 선택합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. 이름으로 **TutorialDB**를 입력하고 **확인**을 클릭하여 새 데이터베이스 프로젝트를 만듭니다.

## <a name="create-a-new-table-in-the-database-project"></a>데이터베이스 프로젝트에서 새 테이블 만들기

1. **보기** 메뉴에서 **솔루션 탐색기**를 선택합니다.

2. 솔루션 탐색기에서 **TutorialDB**를 마우스 오른쪽 단추로 클릭하여 데이터베이스 프로젝트 메뉴를 엽니다.

3. **추가** 아래에서 **테이블**을 선택합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. 테이블 디자이너를 사용하여 그림에 표시된 대로 이름 `nvarchar(50)` 및 위치 `nvarchar(50)` 열 2개를 추가합니다. 디자이너에서 열을 추가하면 SSDT가 `CREATE TABLE` 스크립트를 생성합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. **Table1.sql** 파일을 저장합니다.

## <a name="build-and-validate-the-database"></a>데이터베이스 빌드 및 유효성 검사

1. **TutorialDB**에서 데이터베이스 프로젝트 메뉴를 열고 **빌드**를 선택합니다. SSDT는 프로젝트의 .sql 소스 코드 파일을 컴파일하고 dacpac(데이터 계층 애플리케이션 패키지) 파일을 빌드합니다. 이 파일을 사용하여 Linux의 SQL Server 인스턴스에 데이터베이스를 게시할 수 있습니다. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. Visual Studio의 **출력** 창에서 빌드 성공 메시지를 확인합니다. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Linux의 SQL Server 인스턴스에 데이터베이스 게시

1. **TutorialDB**에서 데이터베이스 프로젝트 메뉴를 열고 **게시**를 선택합니다.

2. **편집**을 클릭하여 Linux에서 해당 SQL Server 인스턴스를 선택합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. 연결 대화 상자에서 Linux SQL Server 인스턴스의 IP 주소 또는 호스트 이름, 사용자 이름 및 암호를 입력합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. 게시 대화 상자에서 **게시** 단추를 클릭합니다.

5. **Data Tools 작업** 창에서 게시 상태를 확인합니다.

6. **결과 보기** 또는 **스크립트 보기**를 클릭하여 SQL Server on Linux의 데이터베이스 게시 결과 정보를 확인합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Linux의 SQL Server 인스턴스에서 새 데이터베이스를 성공적으로 만들었으며 원본 제어 데이터베이스 프로젝트를 사용하여 데이터베이스 개발의 기본 사항을 알아보았습니다.

## <a name="next-steps"></a>다음 단계

T-SQL을 처음 사용하는 경우 [자습서: Transact-SQL 문 작성](../t-sql/tutorial-writing-transact-sql-statements.md)을 참조하세요.

SQL Data Tools를 사용하여 데이터베이스를 개발하는 방법에 대한 자세한 내용은 아래 문서를 참조하세요.

* [Visual Studio 다운로드 및 설치](https://www.visualstudio.com/downloads/)
* [SSDT를 다운로드하여 설치](https://aka.ms/ssdt-download)합니다.
* [SSDT MSDN 문서](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx)
* [자습서: Transact-SQL 문 작성](https://msdn.microsoft.com/library/ms365303.aspx)
* [Transact-SQL 참조(데이터베이스 엔진)](https://msdn.microsoft.com/library/bb510741.aspx)
