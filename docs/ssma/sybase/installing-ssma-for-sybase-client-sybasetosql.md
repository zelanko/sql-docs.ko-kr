---
title: Sybase 클라이언트 (SybaseToSQL) 용 SSMA를 설치 합니다. | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
caps.latest.revision: 18
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 96c227a0bff583c9cc399e2ec453f708bbb4c9b4
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="installing-ssma--for-sybase-client-sybasetosql"></a>Sybase 클라이언트 (SybaseToSQL) 용 SSMA를 설치합니다.
Sybase 적응형 Server Enterprise (ASE) 데이터베이스 서버와의 인스턴스를 연결 하는 데 사용 되는 프로그램 파일의 SSMA 클라이언트 구성 됩니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 ASE 데이터베이스 개체를 변환, Azure SQL DB [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는에 개체를 로드 하는 Azure SQL DB 구문 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB, 다음 데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQLDB 합니다.  
  
이 항목에서는 설치 필수 구성 요소 및 SSMA를 설치 하기 위한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA ASE 11.9.2 또는 이후 버전의 모든 버전와 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 또는 이후 버전 또는 Windows Server 2008 또는 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 또는 이후 버전입니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 버전 4.0 또는 이후 버전입니다. .NET Framework 버전 4.0에서 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품 미디어입니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   Sybase OLEDB/ADO.Net/ODBC 공급자 및 마이그레이션할 데이터베이스가 포함 된 Sybase ASE 데이터베이스 서버에 연결 합니다. Sybase ASE 제품 미디어에서 공급자를 설치할 수 있습니다. 연결에 대 한 정보를 참조 하십시오. [Sybase ASE 연결할 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)합니다.  
  
-   에 대 한 액세스 및의 대상 인스턴스를 호스트 하는 컴퓨터에 대 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 위치 하는 마이그레이션 데이터베이스 개체 및 데이터입니다. 자세한 내용은 참조 [SQL Server에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md)/[Azure SQL DB에 연결 &#40;SybaseToSQL&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)합니다.  
  
-   4GB RAM 권장 합니다.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>SSMA는 Sybase 클라이언트에 대 한 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](http://aka.ms/ssmaforsybase)합니다.  
  
SSMA를 설치 하기 전에 최신 버전을 다운로드 한 후의 설치 파일을 추출 해야 합니다.  
  
**SSMA 클라이언트를 설치 하려면**  
  
1.  Sybase 용 SSMA를 두 번 클릭 *n*합니다. Install.exe 여기서 *n* 는 빌드 번호입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소가 없는 필수 구성 요소를 먼저 설치 해야 한다는 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 하 고 다음 설치 프로그램을 다시 실행 했는지 확인 합니다.  
  
3.  최종 사용자 사용권 계약을 읽어보십시오. 동의 하면 선택 **사용권 계약에 동의**, 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **일반**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 Sybase 용 SSMA의 모든 이전 버전을 제거 하십시오.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase 합니다.  
  
SSMA 프로그램 파일 외에 설치 해야 SSMA for Sybase 확장 팩에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 합니다. 자세한 내용은 참조 [SQL Server에서 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[SQL Server-Azure SQL DB Sybase ASE 데이터베이스 마이그레이션 &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
  
