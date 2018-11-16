---
title: Sybase 클라이언트 (SybaseToSQL) 용 SSMA 설치 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 6cca10f2a54a70e91e46bb8b98e9799885b5f175
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/15/2018
ms.locfileid: "51671723"
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Sybase용 SSMA 클라이언트 설치(SybaseToSQL)
SSMA 클라이언트 Sybase 적응형 Server Enterprise (ASE) 데이터베이스 서버 및 인스턴스에 연결 하는 데 사용 되는 프로그램 파일 이루어져 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB, ASE 데이터베이스 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 구문, 로드를 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB 및 데이터를 마이그레이션하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQLDB 합니다.  
  
이 항목에서는 설치 필수 구성 요소 및 SSMA 설치에 대 한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA 11.9.2 ASE 및 이후 버전의 모든 버전을 사용 하 여 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 이상 버전 또는 Windows Server 2008 또는 이상 버전.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 이상이 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 버전 4.0 이상이 있습니다. .NET Framework 버전 4.0에서 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 미디어입니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   Sybase OLEDB/ADO.Net/ODBC 공급자 및 마이그레이션할 데이터베이스가 포함 된 Sybase ASE 데이터베이스 서버에 연결 합니다. Sybase ASE 제품 미디어에서 공급자를 설치할 수 있습니다. 연결에 대 한 정보를 참조 하세요 [Sybase ASE에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)합니다.  
  
-   에 대 한 액세스 및 대상 인스턴스를 호스팅하는 컴퓨터에서 충분 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB는 마이그레이션될 데이터베이스 개체 및 데이터입니다. 자세한 내용은 [SQL Server에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[Azure SQL DB에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md).  
  
-   4GB RAM이 권장 됩니다.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>용 SSMA는 Sybase 클라이언트 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaforsybase)합니다.  
  
최신 버전을 다운로드 한 후 SSMA를 설치 하기 전에 설치 파일에서 추출 해야 합니다.  
  
**SSMA 클라이언트 설치**  
  
1.  Sybase 용 SSMA를 두 번 클릭 *n*합니다. Install.exe, 여기서 *n* 빌드입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소에 필수 구성 요소를 먼저 설치 해야 한다는 나타내는 메시지가 나타납니다. 모든 필수 구성 요소가 설치 되어 있고 다음 설치 프로그램을 다시 실행 해야 합니다.  
  
3.  최종 사용자 사용권 계약을 읽습니다. 동의 하는 경우 선택 **사용권 계약에 동의**를 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **표준**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 Sybase 용 SSMA의 모든 이전 버전을 제거 하세요.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase입니다.  
  
SSMA 프로그램 파일 외에 설치 해야 SSMA for Sybase 확장 팩에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다. 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 SSMA 구성 요소를 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Sybase ASE 데이터베이스를 SQL Server-Azure SQL DB로 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
