---
title: "SSMA MySQL 클라이언트 (MySQLToSQL)에 대 한 설치 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords: Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
caps.latest.revision: "22"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2ceca393e8c7dc37d181364129d64d5f69bf0791
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>MySQL 클라이언트 (MySQLToSQL) 용 SSMA를 설치합니다.
다음 작업을 수행 하는 프로그램 파일의 MySQL 클라이언트 용 SSMA 구성 됩니다.  
  
-   MySQL 데이터베이스에 연결 합니다.  
  
-   인스턴스에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
-   MySQL 데이터베이스 개체를 변환의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure 개체입니다.  
  
-   에 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
-   데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 SQL Azure입니다.  
  
이 항목에서는 설치 필수 구성 요소 및 MySQL 클라이언트에 대 한 SSMA를 설치 하기 위한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
MySQL 용 SSMA는 MySQL 4.1 또는 그 이후 버전 및 SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016 및 Azure SQL DB의 모든 버전에서 실행 되도록 설계 되었습니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 또는 이후 버전 또는 Windows Server 2008 또는 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 또는 이후 버전입니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0 또는 이후 버전입니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0은 SQL Server 제품 미디어에서 사용할 수 있습니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   MySQL ODBC 5.1 드라이버 및 마이그레이션하려는 MySQL 데이터베이스에 연결 합니다. MySQL MySQL 웹 사이트에서 설치할 수 있습니다. 연결에 대 한 정보를 참조 하세요. [MySQL &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)  
  
-   에 대 한 액세스 및 SQL Server에는 수 마이그레이션하려 데이터베이스 개체 및 데이터의 대상 인스턴스를 호스트 하는 컴퓨터에 대 한 권한이 있습니다. 자세한 내용은 참조 [SQL Server &#40;에 연결 MySQLToSQL &#41;](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)  
  
-   SQL Azure 프로젝트의 경우에 대 한 액세스 및 권한이 마이그레이션 수는 Azure SQL DB의 인스턴스에 데이터베이스 개체와 데이터입니다. 자세한 내용은 참조 [Azure SQL DB &#40;에 연결 MySQLToSQL &#41; ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md).  
  
-   4GB RAM 권장 합니다.  
  
## <a name="installing-ssma-for-mysql-client"></a>MySQL 클라이언트 용 SSMA를 설치합니다.  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](http://aka.ms/ssmaformysql)합니다.  
  
최신 버전을 다운로드 한 후 SSMA를 설치 하기 전에 설치 파일을 추출 해야 합니다.  
  
**SSMA 클라이언트를 설치 하려면**  
  
1.  MySQL 용 SSMA를 두 번 클릭  *n* 합니다. Install.exe 여기서  *n*  는 빌드 번호입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소가 없는 경우 나타내는 필수 구성 요소를 먼저 설치 해야 한다는 메시지가 표시 됩니다. 설치 프로그램을 다시 실행 하기 전에 모든 필수 구성 요소를 설치 했는지 확인 합니다.  
  
3.  최종 사용자 사용권 계약을 읽어보십시오. 동의 하면 선택 **사용권 계약에 동의**, 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **일반**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 MySQL 용 SSMA의 모든 이전 버전을 제거 하십시오.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL.  
  
64 비트 Windows 컴퓨터에서 MySQL C:\Microsoft SQL Server Migration Assistant에 제품이 설치 되어 있습니다.  
  
## <a name="see-also"></a>관련 항목:  
[Azure SQL DB &#40; SQL Server-MySQL 데이터베이스 마이그레이션 MySQLToSql &#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
