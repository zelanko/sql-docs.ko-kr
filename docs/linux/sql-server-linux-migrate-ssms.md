---
title: Linux에서 데이터베이스 내보내기 및 가져오기
description: 이 문서에서는 SQL Server Management Studio 및 SqlPackage.exe를 사용하여 SQL Server on Linux에서 데이터베이스를 내보내고 가져오는 방법을 보여 줍니다.
author: VanMSFT
ms.author: vanto
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 2210cfc3-c23a-4025-a551-625890d6845f
ms.openlocfilehash: f83f95fa17e99c20754bbde9d1d4a7fb388df74b
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85887838"
---
# <a name="export-and-import-a-database-on-linux-with-ssms-or-sqlpackageexe-on-windows"></a>Windows에서 SSMS 또는 SqlPackage를 사용하여 Linux에서 데이터베이스 내보내기 및 가져오기

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 SSMS([SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)) 및 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)를 사용하여 Linux의 SQL Server에서 데이터베이스를 내보내고 가져오는 방법을 보여 줍니다. SSMS 및 SqlPackage.exe는 Windows 애플리케이션이므로 Linux의 원격 SQL Server 인스턴스에 연결할 수 있는 Windows 컴퓨터가 있는 경우 이 기술을 사용합니다.

[Windows의 SSMS를 사용하여 Linux의 SQL Server에 연결](sql-server-linux-manage-ssms.md)에 설명된 대로 항상 최신 버전의 SSMS(SQL Server Management Studio)를 설치한 후 사용해야 합니다.

> [!NOTE]
> 한 SQL Server 인스턴스에서 다른 인스턴스로 데이터베이스를 마이그레이션하는 경우 [백업 및 복원](sql-server-linux-migrate-restore-database.md)을 사용하는 것이 좋습니다.

## <a name="export-a-database-with-ssms"></a>SSMS를 사용하여 데이터베이스 내보내기

1. Windows 검색 상자에 **Microsoft SQL Server Management Studio**를 입력하여 SSMS를 시작한 다음, 데스크톱 앱을 클릭합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 개체 탐색기에서 원본 데이터베이스에 연결합니다. 원본 데이터베이스는 온-프레미스 또는 클라우드, Linux, Windows 또는 Docker, Azure SQL Database 또는 Azure SQL Data Warehouse에서 실행되는 Microsoft SQL Server에 있을 수 있습니다.

3. 개체 탐색기에서 원본 데이터베이스를 마우스 오른쪽 단추로 클릭하고 **작업**을 가리킨 다음, **데이터 계층 애플리케이션 내보내기...** 를 클릭합니다.

4. 내보내기 마법사에서 **다음**을 클릭한 다음, **설정** 탭에서 BACPAC 파일을 로컬 디스크 위치 또는 Azure Blob에 저장하도록 내보내기를 구성합니다.

5. 기본적으로 데이터베이스의 모든 개체가 내보내집니다. **고급 탭**을 클릭하고 내보낼 데이터베이스 개체를 선택합니다.

6. **다음** , **마침**을 차례로 클릭합니다.

*.BACPAC 파일이 선택한 위치에 만들어지고, 대상 데이터베이스로 가져올 준비가 됩니다.

## <a name="import-a-database-with-ssms"></a>SSMS를 사용하여 데이터베이스 가져오기

1. Windows 검색 상자에 **Microsoft SQL Server Management Studio**를 입력하여 SSMS를 시작한 다음, 데스크톱 앱을 클릭합니다.

    ![SQL Server Management Studio](./media/sql-server-linux-manage-ssms/ssms.png) 

2. 개체 탐색기에서 대상 서버에 연결합니다. 대상 서버는 온-프레미스 또는 클라우드, Linux, Windows 또는 Docker, Azure SQL Database 또는 Azure SQL Data Warehouse에서 실행되는 Microsoft SQL Server에 있을 수 있습니다.

3. 개체 탐색기에서 **데이터베이스** 폴더를 마우스 오른쪽 단추로 클릭하고 **데이터 계층 애플리케이션 가져오기...** 를 클릭합니다.

4. 대상 서버에 데이터베이스를 만들려면 로컬 디스크에서 BACPAC 파일을 지정하거나 BACPAC 파일을 업로드한 Azure Storage 계정 및 컨테이너를 선택합니다.

5. 데이터베이스의 새 데이터베이스의 이름을 입력합니다. Azure SQL Database에서 데이터베이스를 가져오는 경우 Microsoft Azure SQL Database 버전(서비스 계층), 최대 데이터베이스 크기 및 서비스 목표(성능 수준)를 설정합니다.

6. **다음**을 클릭하고 **마침**을 클릭하여 대상 서버의 새 데이터베이스로 BACPAC 파일을 가져옵니다.

*.BACPAC 파일을 가져와 지정한 대상 서버에 새 데이터베이스를 만듭니다.

## <a name="sqlpackage-command-line-option"></a><a id="sqlpackage"></a> SqlPackage 명령줄 옵션

또한 SSDT(SQL Server Data Tools) 명령줄 도구인 [SqlPackage.exe](https://msdn.microsoft.com/library/hh550080.aspx)를 사용하여 BACPAC 파일을 내보내고 가져올 수도 있습니다.

다음 예제 명령은 BACPAC 파일을 내보냅니다.

```bash
SqlPackage.exe /a:Export /ssn:tcp:<your_server> /sdn:<your_database> /su:<username> /sp:<password> /tf:<path_to_bacpac>
```

다음 명령을 사용하여 .BACPAC 파일에서 데이터베이스 스키마 및 사용자 데이터를 가져옵니다.

```bash
SqlPackage.exe /a:Import /tsn:tcp:<your_server> /tdn:<your_database> /tu:<username> /tp:<password> /sf:<path_to_bacpac>

```

## <a name="see-also"></a>참고 항목
SSMS 사용 방법에 대한 자세한 내용은 [SQL Server Management Studio 사용](https://msdn.microsoft.com/library/ms174173.aspx)을 참조하세요. SqlPackage.exe에 대한 자세한 내용은 [SqlPackage 참조 설명서](https://msdn.microsoft.com/library/hh550080.aspx)를 참조하세요.
