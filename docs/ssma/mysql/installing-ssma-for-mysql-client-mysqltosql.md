---
title: MySQL 클라이언트 (MySQLToSQL) 용 SSMA 설치 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 9dcdeaff1c4782453a9fd57cc709e17ad3200d28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68086822"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>MySQL용 SSMA 클라이언트 설치(MySQLToSQL)
SSMA MySQL 클라이언트에 대 한 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.  
  
-   MySQL 데이터베이스에 연결 합니다.  
  
-   인스턴스에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
-   MySQL 데이터베이스 개체를 변환 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체입니다.  
  
-   에 개체를 로드할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
-   데이터를 마이그레이션하기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure입니다.  
  
이 항목에서는 설치 필수 구성 요소 및 용 SSMA MySQL 클라이언트 설치에 대 한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
MySQL 용 SSMA MySQL 4.1 또는 이후 버전 및 모든 버전의 SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 및 Azure SQL DB를 사용 하 여 작동 하도록 설계 되었습니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 이상 버전 또는 Windows Server 2008 또는 이상 버전.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 이상이 있습니다.  
  
-   합니다 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0 이상이 있습니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0은 SQL Server 제품 미디어에서 사용할 수 있습니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   MySQL Odbc 5.1 및 마이그레이션하려는 MySQL 데이터베이스에 연결 합니다. MySQL 웹 사이트에서 MySQL을 설치할 수 있습니다. 연결에 대 한 정보를 참조 하세요 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   에 대 한 액세스 및 권한이 있는 마이그레이션될 데이터베이스 개체 및 데이터는 SQL Server의 대상 인스턴스를 호스팅하는 컴퓨터입니다. 자세한 내용은 [SQL Server에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   SQL Azure 프로젝트의 경우에 대 한 액세스 및 권한이 마이그레이션 수는 Azure SQL DB의 인스턴스를 데이터베이스 개체 및 데이터입니다. 자세한 내용은 [Azure SQL DB에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)합니다.  
  
-   4GB RAM이 권장 됩니다.  
  
## <a name="installing-ssma-for-mysql-client"></a>MySQL용 SSMA 클라이언트 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaformysql)합니다.  
  
최신 버전을 다운로드 한 후 SSMA를 설치 하기 전에 설치 파일을 추출 해야 합니다.  
  
**SSMA 클라이언트 설치**  
  
1.  MySQL 용 SSMA를 두 번 클릭 *n*합니다. Install.exe, 여기서 *n* 빌드입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소가 없는 경우 메시지에 필수 구성 요소를 먼저 설치 해야 한다는 나타내는 메시지가 표시 됩니다. 설치 프로그램을 다시 실행 하기 전에 모든 필수 구성 요소를 설치 했는지 확인 합니다.  
  
3.  최종 사용자 사용권 계약을 읽습니다. 동의 하는 경우 선택 **사용권 계약에 동의**를 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **표준**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 MySQL 용 SSMA의 모든 이전 버전을 제거 하세요.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL입니다.  
  
64 비트 Windows 컴퓨터에서 MySQL에 대 한 제품 C:\Microsoft SQL Server Migration Assistant에서 설치 됩니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server-Azure SQL DB로 마이그레이션 MySQL 데이터베이스 &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
