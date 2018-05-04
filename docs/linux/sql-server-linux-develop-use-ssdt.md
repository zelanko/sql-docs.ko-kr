---
title: 개발 및 Linux 용 SQL Server 배포 데이터베이스 | Microsoft Docs
description: ''
author: erickangMSFT
ms.author: erickang
manager: jroth
ms.date: 03/17/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: ''
ms.suite: sql
ms.technology: database-engine
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: sql-linux
ms.openlocfilehash: 9f6d63674253171bdb21519af0604502c2e61f9e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Visual Studio를 사용 하 여 Linux에서 SQL Server에 대 한 데이터베이스를 만들 수

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT)는 Linux에서 SQL Server에 대 한 강력한 개발 및 데이터베이스 수명 주기 관리 (DLM) 환경으로 Visual Studio를 설정합니다. 개발 빌드 및 테스트 하 고, 응용 프로그램 코드를 개발 하는 것 처럼 소스 제어 프로젝트에서 데이터베이스를 게시할 수 있습니다.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Visual Studio와 SQL Server Data Tools 설치

1. Windows 컴퓨터에 Visual Studio를 이미 설치 되지 않은 경우 [다운로드 하 고 Visual Studio 설치]합니다. Visual Studio Community 버전 학생에 대 한 무료 이며 완전 한 기능의 IDE가 Visual Studio 라이선스가 없는 경우 오픈 소스 및 개별 개발자.

2. Visual Studio를 설치 하는 동안 선택 **사용자 지정** 에 대 한는 **설치 유형을 선택** 옵션입니다. **다음**을 클릭합니다.

3. 선택 **Microsoft SQL Server Data Tools**, **Windows 용 Git**, 및 **Visual Studio 용 GitHub 확장** 기능 선택 목록에서 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. 계속 하 고 Visual Studio의 설치를 마칩니다. 몇 분 정도 걸릴 수 있습니다.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>SQL Server Data Tools를 SSDT 17.0 RC 버전으로 업그레이드

SQL Server 2017 Linux에서 SSDT 17.0 RC 이상 버전에서 지원 됩니다.

* [다운로드 및 설치 17.0 SSDT RC2](https://go.microsoft.com/fwlink/?linkid=837939)합니다.

## <a name="create-a-new-database-project-in-source-control"></a>소스 제어에서 새 데이터베이스 프로젝트 만들기

1. Visual Studio를 시작합니다.

2. 선택 **팀 탐색기** 에 **보기** 메뉴. 

3. 클릭 **새로** 에 **로컬 Git 리포지토리** 섹션에서 **연결** 페이지.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. **만들기**를 클릭합니다. 로컬 Git 리포지토리를 만든 후 두 번 클릭 **SSDTRepo**합니다.

4. 클릭 **새로** 에 **솔루션** 섹션. 선택 **SQL Server** 아래 **다른 언어** 에서 노드는 **새 프로젝트** 대화 상자.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. 에 입력 **TutorialDB** 이름과 클릭 **확인** 새 데이터베이스 프로젝트를 만듭니다.

## <a name="create-a-new-table-in-the-database-project"></a>데이터베이스 프로젝트에 새 테이블을 만듭니다.

1. 선택 **솔루션 탐색기** 에 **보기** 메뉴.

2. 마우스 오른쪽 단추로 클릭 하 여 데이터베이스 프로젝트 메뉴를 열고 **TutorialDB** 솔루션 탐색기에서 합니다.

3. 선택 **테이블** 아래 **추가**합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. 테이블 디자이너를 사용 하 여 두 개의 열 이름 추가 `nvarchar(50)` 및 위치 `nvarchar(50)`그림에 표시 된 것 처럼 합니다. SSDT에서는 오류가 발생 하는 `CREATE TABLE` 디자이너에서 열을 추가한 것 처럼 스크립트입니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. 저장 된 **Table1.sql** 파일입니다.

## <a name="build-and-validate-the-database"></a>빌드 및 데이터베이스 유효성 검사

1. 데이터베이스 프로젝트 메뉴를 열고 **TutorialDB** 선택 **빌드**합니다. SSDT은 프로젝트에서.sql 소스 코드 파일을 컴파일하고 데이터 계층 응용 프로그램 패키지 (dacpac) 파일을 작성 합니다. Linux에서 SQL Server 2017 인스턴스에 데이터베이스를 게시 데 될 수 있습니다. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. 빌드 성공 메시지 체크인 **출력** Visual Studio의 창. 

## <a name="publish-the-database-to-sql-server-2017-instance-on-linux"></a>SQL Server 2017 Linux 인스턴스로 데이터베이스를 게시 합니다.

1. 데이터베이스 프로젝트 메뉴를 열고 **TutorialDB** 선택 **게시**합니다.

2. 클릭 **편집** Linux에서 SQL Server 인스턴스를 선택 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. 연결 대화 상자에서 Linux, 사용자 이름 및 암호에 해당 SQL Server 인스턴스의 IP 주소 또는 호스트 이름을 입력 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. 클릭는 **게시** 게시 대화 상자에서 단추입니다.

5. 게시 상태를 확인 합니다.는 **데이터 도구 작업** 창.

6. 클릭 **보기 Reulst** 또는 **스크립트 보기** 결과 Linux에서 SQL Server에 게시 데이터베이스의 정보를 확인할 수 있습니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Linux에서 SQL Server 인스턴스에 새 데이터베이스를 생성 하 고 소스 제어 데이터베이스 프로젝트를 사용 하 여 데이터베이스 개발 자습서 했습니다 있습니다.

## <a name="next-steps"></a>다음 단계

T-SQL을 처음 접하는 경우 참조 [자습서: TRANSACT-SQL 문 쓰기] 및 [TRANSACT-SQL 참조 (데이터베이스 엔진)]합니다.

SQL Data Tools를 사용 하 여 데이터베이스를 개발 하는 방법에 대 한 자세한 내용은 참조 [SSDT MSDN 문서]

[다운로드 하 고 Visual Studio 설치]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[SSDT MSDN 문서]: https://msdn.microsoft.com/en-us/library/hh272686(v=vs.103).aspx
[자습서: TRANSACT-SQL 문 쓰기]:https://msdn.microsoft.com/library/ms365303.aspx
[TRANSACT-SQL 참조 (데이터베이스 엔진)]:https://msdn.microsoft.com/library/bb510741.aspx
