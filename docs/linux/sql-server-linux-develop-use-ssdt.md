---
title: 개발 및 Linux 용 SQL Server 배포 데이터베이스 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/17/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 1e924704-e07c-4a8b-b243-8c1dd8cff0d3
ms.custom: sql-linux
ms.openlocfilehash: 0de0286065166137ebe83ce2a46dfb41d1670fc0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47816061"
---
# <a name="use-visual-studio-to-create-databases-for-sql-server-on-linux"></a>Visual Studio를 사용 하 여 Linux의 SQL Server에 대 한 데이터베이스를 만들려면

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

SQL Server Data Tools (SSDT)는 Linux의 SQL Server에 대 한 강력한 개발 및 데이터베이스 수명 주기 관리 (DLM) 환경에 Visual Studio를 설정합니다. 개발 빌드 및 테스트 응용 프로그램 코드를 개발 하는 것 처럼 소스 제어 프로젝트에서 데이터베이스를 게시할 수 있습니다.

## <a name="install-visual-studio-and-sql-server-data-tools"></a>Visual Studio 및 SQL Server Data Tools 설치

1. Windows 컴퓨터에 Visual Studio를 이미 설치 되지 않은 경우 [다운로드 하 여 Visual Studio를 설치 합니다.]합니다. Visual Studio Community edition은 학생에 대 한 무료, 완전 한 기능의 IDE를 Visual Studio 라이선스가 없는 경우 오픈 소스 및 개인 개발자.

2. Visual Studio 설치 중 선택 **사용자 지정** 에 대 한 합니다 **설치 유형을 선택** 옵션입니다. **다음**을 클릭합니다.

3. 선택 **Microsoft SQL Server Data Tools**하십시오 **Git에 대 한 Windows**, 및 **Visual Studio 용 GitHub 확장** 기능 선택 목록에서.

    <img src="./media/sql-server-linux-develop-use-ssdt/ssdt-setup.png" alt="ssdt setup" style="width: 400px;"/>

4. 계속 하 고 Visual Studio의 설치를 완료 합니다. 몇 분 정도 걸릴 수 있습니다.

## <a name="upgrade-sql-server-data-tools-to-ssdt-170-rc-release"></a>SQL Server Data Tools를 SSDT 17.0 RC 릴리스로 업그레이드

Linux의 SQL Server는 SSDT 버전 17.0 RC 이상에서 지원 됩니다.

* [다운로드 및 설치 SSDT 17.0 RC2](https://go.microsoft.com/fwlink/?linkid=837939)합니다.

## <a name="create-a-new-database-project-in-source-control"></a>소스 제어에서 새 데이터베이스 프로젝트 만들기

1. Visual Studio를 시작합니다.

2. 선택 **팀 탐색기** 에 **보기** 메뉴. 

3. 클릭 **새로 만들기** 에서 **로컬 Git 리포지토리** 섹션을 **Connect** 페이지.

    <img src="./media/sql-server-linux-develop-use-ssdt/git-repository.png" alt="local repository" style="width: 300px;"/>

3. **만들기**를 클릭합니다. 로컬 Git 리포지토리를 만든 후 두 번 클릭 **SSDTRepo**합니다.

4. 클릭 **새로 만들기** 에 **솔루션** 섹션입니다. 선택 **SQL Server** 아래에서 **다른 언어** 에 노드를 **새 프로젝트** 대화 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/new-project.png" alt="local repository" style="width: 480px;"/>

5. 입력 **TutorialDB** 이름 및 클릭 **확인** 새 데이터베이스 프로젝트를 만들려면.

## <a name="create-a-new-table-in-the-database-project"></a>데이터베이스 프로젝트에 새 테이블을 만들려면

1. 선택 **솔루션 탐색기** 에 **보기** 메뉴.

2. 마우스 오른쪽 단추로 클릭 하 여 데이터베이스 프로젝트 메뉴를 열고 **TutorialDB** 솔루션 탐색기에서.

3. 선택 **테이블** 아래에서 **추가**합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/create-table.png" alt="create table" style="width: 480px;"/>

4. 테이블 디자이너를 사용 하 여 두 개의 열을 이름 추가 `nvarchar(50)` 및 위치 `nvarchar(50)`그림에 나와 있는 것 처럼 합니다. SSDT에서는 오류가 발생 하는 `CREATE TABLE` 디자이너에서 열을 추가 하면 스크립트입니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/add-columns.png" alt="add columns" style="width: 480px;"/>

5. 저장 된 **Table1.sql** 파일입니다.

## <a name="build-and-validate-the-database"></a>빌드 및 데이터베이스의 유효성을 검사합니다

1. 데이터베이스 프로젝트 메뉴를 열고 **TutorialDB** 선택한 **빌드**합니다. SSDT은 프로젝트에.sql 소스 코드 파일을 컴파일하고 데이터 계층 응용 프로그램 패키지 (dacpac) 파일을 빌드합니다. 이 Linux의 SQL Server 인스턴스로 데이터베이스를 게시할 수 있습니다. 

    <img src="./media/sql-server-linux-develop-use-ssdt/build.png" alt="add columns" style="width: 400px;"/>

2. 빌드 성공 메시지를 체크 **출력** Visual Studio의 창. 

## <a name="publish-the-database-to-sql-server-instance-on-linux"></a>Linux의 SQL Server 인스턴스로 데이터베이스를 게시 합니다.

1. 데이터베이스 프로젝트 메뉴를 열고 **TutorialDB** 선택한 **게시**합니다.

2. 클릭 **편집** Linux에서 SQL Server 인스턴스를 선택 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-dialog.png" alt="publish dialog" style="width: 480px;"/>

3. 연결 대화 상자에서 Linux, 사용자 이름 및 암호 기반 SQL Server 인스턴스의 IP 주소 또는 호스트 이름을 입력 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/connection-dialog.png" alt="connection dialog" style="width: 400px;"/>

4. 클릭 합니다 **게시** 게시 대화 상자에서 단추입니다.

5. 게시 상태를 확인 합니다 **Data Tools 작업** 창입니다.

6. 클릭 **보기 Reulst** 또는 **스크립트 보기** Linux에서 SQL Server에서 결과 게시 데이터베이스의 세부 정보를 확인 합니다.

    <img src="./media/sql-server-linux-develop-use-ssdt/publish-result.png" alt="publish result" style="width: 480px;"/>

Linux의 SQL Server 인스턴스에 새 데이터베이스를 생성 하 고 소스 제어 데이터베이스 프로젝트를 사용 하 여 데이터베이스를 개발 하는 기본 사항을 파악 했습니다 있습니다.

## <a name="next-steps"></a>다음 단계

T-SQL을 처음 접하는 경우 참조 [자습서: TRANSACT-SQL 문 작성] 하며 [TRANSACT-SQL 참조 (데이터베이스 엔진)]합니다.

SQL Data Tools를 사용 하 여 데이터베이스를 개발 하는 방법에 대 한 자세한 내용은 참조 하세요. [SSDT MSDN 문서]

[다운로드 하 여 Visual Studio를 설치 합니다.]:https://www.visualstudio.com/downloads/
[Download and Install SSDT 17.0 RC2]:https://aka.ms/ssdt-download
[SSDT MSDN 문서]: https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx
[자습서: Transact-SQL 문 작성]:https://msdn.microsoft.com/library/ms365303.aspx
[TRANSACT-SQL 참조 (데이터베이스 엔진)]:https://msdn.microsoft.com/library/bb510741.aspx
