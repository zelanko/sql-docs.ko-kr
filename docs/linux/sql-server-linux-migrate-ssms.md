---
title: Linux에서 데이터베이스를 내보내고 | Microsoft Docs
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.custom: sql-linux
ms.openlocfilehash: 7a7c1c73ca70e0d42104e74c868d6acd32cc01b1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2018
ms.locfileid: "38020131"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>SSMS 또는 Windows에서 SqlPackage.exe를 사용 하 여 Linux에서 데이터베이스 가져오기 및 내보내기

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 사용 하는 방법을 보여 줍니다 [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) 하 고 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx) Linux의 SQL Server 2017에서 데이터베이스를 내보내고 합니다. SSMS 및 SqlPackage.exe는 Windows 응용 프로그램, 따라서 Linux에서 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터의 경우이 기법을 사용 합니다.

항상 설치 하 고에 설명 된 대로 최신 버전의 SQL Server Management Studio (SSMS)를 사용 해야 [Linux의 SQL Server에 연결 하는 Windows에서 사용 하 여 SSMS](sql-server-linux-manage-ssms.md)

> [!NOTE]
> 마이그레이션하려는 경우 데이터베이스를 SQL Server 인스턴스에서 다른를 사용 하는 것이 좋습니다 [백업 및 복원](sql-server-linux-migrate-restore-database.md)합니다.

## <a name="export-a-database-with-ssms"></a>SSMS 사용 하 여 데이터베이스 내보내기

1. 입력 하 여 SSMS를 시작할 **Microsoft SQL Server Management Studio** 검색 상자에는 Windows 및 데스크톱 앱을 클릭 합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 개체 탐색기에서 원본 데이터베이스에 연결 합니다. 원본 데이터베이스는 Microsoft SQL Server 온-프레미스 또는 클라우드에서 Linux, Windows 또는 Docker 및 Azure SQL Database 또는 Azure SQL Data Warehouse에서 수 있습니다.

3. 개체 탐색기에서 원본 데이터베이스를 마우스 오른쪽 **태스크**를 클릭 하 고 **데이터 계층 응용 프로그램 내보내기...**

4. 내보내기 마법사에서 클릭 **다음**, 한 후 합니다 **설정** 탭, 로컬 디스크 위치 또는 Azure blob에 BACPAC 파일을 저장 하는 내보내기를 구성 합니다.

5. 데이터베이스의 모든 개체는 기본적으로 내보내집니다. 클릭 합니다 **고급 탭** 내보낼 데이터베이스 개체를 선택 합니다.

6. **다음** , **마침**을 차례로 클릭합니다.

*입니다. 선택한 위치에 성공적으로 만들어지면 BACPAC 파일 및 대상 데이터베이스로 가져올 수 있습니다.

## <a name="import-a-database-with-ssms"></a>SSMS로 데이터베이스 가져오기

1. 입력 하 여 SSMS를 시작할 **Microsoft SQL Server Management Studio** 검색 상자에는 Windows 및 데스크톱 앱을 클릭 합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 개체 탐색기에서 대상 서버에 연결 합니다. 대상 서버는 Microsoft SQL Server 온-프레미스 실행 수 또는 클라우드에서 Linux, Windows 또는 Docker 및 Azure SQL Database 또는 Azure SQL Data Warehouse에서 합니다.

3. 마우스 오른쪽 단추로 클릭 합니다 **데이터베이스** 고 개체 탐색기에서 폴더 **데이터 계층 응용 프로그램 가져오기...**

4. 대상 서버에서 데이터베이스를 만들려면 로컬 디스크에서 BACPAC 파일을 지정 하거나 Azure 저장소 계정 및 BACPAC 파일을 업로드 하는 컨테이너를 선택 합니다.

5. 데이터베이스에 대 한 새 데이터베이스 이름을 제공 합니다. Azure SQL Database에서 데이터베이스를 가져오는 경우의 Microsoft Azure SQL Database 버전 (서비스 계층), 최대 데이터베이스 크기 및 서비스 목표 (성능 수준)를 설정 합니다.

6. 클릭 **다음** 을 클릭 한 다음 **마침** 대상 서버에서 새 데이터베이스로 BACPAC 파일을 가져오려면.

*입니다. 지정한 대상 서버에서 새 데이터베이스를 만드는 BACPAC 파일을 가져옵니다.

## <a id="sqlpackage"></a> SqlPackage 명령줄 옵션

SQL Server Data Tools (SSDT) 명령줄 도구를 사용 하 여 가능한 이기도 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)BACPAC 파일을 내보내고로 합니다.

다음 예제 명령은 BACPAC 파일로를 내보냅니다.

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

다음 명령을 사용 하 여 데이터베이스 스키마 및 사용자 데이터를 가져올를 합니다. BACPAC 파일:

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>참고자료
SSMS를 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [사용 하 여 SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)합니다. SqlPackage.exe에 대 한 자세한 내용은 참조는 [SqlPackage 참조 설명서](https://msdn.microsoft.com/library/hh550080.aspx)합니다.
