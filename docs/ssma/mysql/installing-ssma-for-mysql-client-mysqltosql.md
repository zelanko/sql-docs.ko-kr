---
title: MySQL 용 SSMA 클라이언트 설치 (MySQLToSQL) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68086822"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>MySQL용 SSMA 클라이언트 설치(MySQLToSQL)
MySQL 용 SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.  
  
-   MySQL 데이터베이스에 연결 합니다.  
  
-   인스턴스에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 하거나 SQL Azure 합니다.  
  
-   MySQL 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체로 변환 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 SQL Azure 개체를 로드 합니다.  
  
-   또는 SQL Azure으로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터를 마이그레이션합니다.  
  
이 항목에서는 설치 필수 구성 요소 및 MySQL 용 SSMA 클라이언트를 설치 하기 위한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
MySQL 용 SSMA는 MySQL 4.1 이상 버전 및 모든 버전의 SQL Server 2005, SQL Server 2008, SQL Server 2012, SQL Server 2014, SQL Server 2016, SQL Server 2017 및 Azure SQL DB와 함께 작동 하도록 설계 되었습니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 이상 버전 또는 Windows Server 2008 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0은 SQL Server 제품 미디어에서 사용할 수 있습니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수도 있습니다.  
  
-   MySQL ODBC 5.1 드라이버 및 마이그레이션하려는 MySQL 데이터베이스에 연결 합니다. Mysql 웹 사이트에서 MySQL을 설치할 수 있습니다. 연결에 대 한 자세한 내용은 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md) 을 참조 하세요.  
  
-   데이터베이스 개체와 데이터를 마이그레이션할 SQL Server의 대상 인스턴스를 호스트 하는 컴퓨터에 대 한 액세스 권한이 있어야 합니다. 자세한 내용은 [SQL Server &#40;MySQLToSQL에 연결](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md) 을 참조 하세요&#41;  
  
-   SQL Azure 프로젝트의 경우 데이터베이스 개체와 데이터를 마이그레이션하려는 Azure SQL DB 인스턴스에 대 한 액세스 권한이 있어야 합니다. 자세한 내용은 [AZURE SQL DB &#40;MySQLToSQL&#41;에 연결 ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)을 참조 하세요.  
  
-   4gb RAM 권장.  
  
## <a name="installing-ssma-for-mysql-client"></a>MySQL용 SSMA 클라이언트 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaformysql)를 참조 하세요.  
  
최신 버전을 다운로드 한 후에 설치 파일을 추출 해야 SSMA를 설치할 수 있습니다.  
  
**SSMA 클라이언트를 설치 하려면**  
  
1.  MySQL *n*용 ssma를 두 번 클릭 합니다. Setup.exe를 설치 합니다. 여기서 *n* 은 빌드 번호입니다.  
  
2.  Welcome 페이지에서 **다음**을 클릭합니다.  
  
    필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 한다는 메시지가 표시 됩니다. 설치 프로그램을 다시 실행 하기 전에 모든 필수 구성 요소를 설치 했는지 확인 합니다.  
  
3.  최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.  
  
4.  설치 유형 선택 페이지에서 **일반**을 클릭 합니다.  
  
5.  **Install**을 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 먼저 MySQL 용 SSMA의 모든 이전 버전을 제거 하세요.  
  
기본 설치 위치는 Files\Microsoft에 대 한 C:\Program SQL Server Migration Assistant입니다.  
  
64 비트 Windows 컴퓨터에서는 제품이 MySQL 용 C:\Microsoft SQL Server Migration Assistant에 설치 되어 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
  
