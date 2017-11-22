---
title: "내보내기 및 가져오기 Linux에서 데이터베이스 | Microsoft Docs"
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.technology: database-engine
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.custom: 
ms.workload: On Demand
ms.openlocfilehash: 41d3647796306cb1a9b89f5af47c75416de79c01
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>내보내기 및 SSMS 또는 SqlPackage.exe windows와 Linux에서 데이터베이스 가져오기

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

이 항목에서는 사용 하는 방법을 보여 줍니다. [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) 및 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) 내보내고 SQL Server 2017 linux에서 데이터베이스를 가져옵니다. Windows 응용 프로그램은 SSMS 및 SqlPackage.exe, 따라서 Linux에서 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터는 하는 경우이 방법을 사용 합니다.

항상 설치 하 고에 설명 된 대로 SQL Server Management Studio (SSMS)의 가장 최신 버전을 사용 해야 [Linux에서 SQL Server에 연결 하는 Windows에서 SSMS를 사용 하 여](sql-server-linux-develop-use-ssms.md)

> [!NOTE]
> 다른 한 SQL Server 인스턴스에서 데이터베이스를 마이그레이션하는, 경우 않는 것이 좋습니다 사용 [백업 및 복원](sql-server-linux-migrate-restore-database.md)합니다.

## <a name="export-a-database-with-ssms"></a>SSMS 사용 하 여 데이터베이스 내보내기

1. SSMS를 입력 하 여 시작 **Microsoft SQL Server Management Studio** Windows에서 검색 상자 및 데스크톱 응용 프로그램을 클릭 합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png) 

2. 개체 탐색기에서 원본 데이터베이스에 연결 합니다. 원본 데이터베이스에는 온-프레미스를 실행 중인 Microsoft SQL Server 또는 Linux, Windows 또는 Docker 및 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 클라우드에 수 있습니다.

3. 개체 탐색기에서 원본 데이터베이스를 마우스 오른쪽 단추로 클릭, 가리킨 **작업**를 클릭 하 고 **데이터 계층 응용 프로그램 내보내기...**

4. 내보내기 마법사에서 **다음**를 선택한 다음는 **설정** 탭 로컬 디스크 위치 또는 Azure blob에 BACPAC 파일을 저장 하려면 내보내기를 구성 합니다.

5. 기본적으로 데이터베이스에 개체를 모두 내보냅니다. 클릭는 **고급 탭** 내보낼 하는 데이터베이스 개체를 선택 합니다.

6. **다음** , **마침**을 차례로 클릭합니다.

*입니다. 선택한 위치에 성공적으로 만들어지면 BACPAC 파일 및 대상 데이터베이스에 가져올 준비가 되었습니다. 합니다.

## <a name="import-a-database-with-ssms"></a>SSMS 사용 하 여 데이터베이스 가져오기

1. SSMS를 입력 하 여 시작 **Microsoft SQL Server Management Studio** Windows에서 검색 상자 및 데스크톱 응용 프로그램을 클릭 합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-develop-use-ssms/ssms.png) 

2. 개체 탐색기에서 대상 서버에 연결 합니다. 대상 서버에는 Microsoft SQL Server 온-프레미스로 실행 될 수 있습니다 또는 Linux, Windows 또는 Docker 및 Azure SQL 데이터베이스 또는 Azure SQL 데이터 웨어하우스 클라우드에서 합니다.

3. 마우스 오른쪽 단추로 클릭는 **데이터베이스** 클릭 고 개체 탐색기에서 폴더 **데이터 계층 응용 프로그램 가져오기...**

4. 대상 서버에서 데이터베이스를 만들려면 로컬 디스크에서 BACPAC 파일을 지정 하거나 Azure 저장소 계정 및 BACPAC 파일을 업로드 하는 컨테이너를 선택 합니다.

5. 데이터베이스에 대 한 새 데이터베이스 이름을 제공 합니다. Azure SQL 데이터베이스에서 데이터베이스를 가져오는 경우 버전의 Microsoft Azure SQL 데이터베이스 (서비스 계층), 최대 데이터베이스 크기 및 서비스 목표 (성능 수준)를 설정 합니다.

6. 클릭 **다음** 클릭 하 고 **마침** BACPAC 파일을 대상 서버에 있는 새 데이터베이스로 가져오려는 합니다.

*입니다. 지정한 대상 서버에서 새 데이터베이스를 만들려는 BACPAC 파일을 가져옵니다.

## <a id="sqlpackage"></a>SqlPackage 명령줄 옵션

SQL Server Data Tools (SSDT) 명령줄 도구를 사용 하 여 이기도 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx),으로 내보내고 가져올 BACPAC 파일입니다.

다음 예제 명령은 BACPAC 파일을 내보냅니다.

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

다음 명령을 사용 하 여 데이터베이스 스키마 및 사용자 데이터를 가져올는 합니다. BACPAC 파일:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>참고 항목
SSMS를 사용 하는 방법에 대 한 자세한 내용은 참조 하십시오. [사용 하 여 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)합니다. SqlPackage.exe에 자세한 내용은 참조는 [SqlPackage 참조 설명서](https://msdn.microsoft.com/library/hh550080.aspx)합니다.
