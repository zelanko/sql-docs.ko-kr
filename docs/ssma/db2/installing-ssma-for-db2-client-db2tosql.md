---
title: "SSMA DB2 클라이언트 (DB2ToSQL)에 대 한 설치 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 4e003c72b6fea28c3048384701f3dc8839faacce
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>DB2 클라이언트 (DB2ToSQL) 용 SSMA를 설치합니다.
다음 작업을 수행 하는 프로그램 파일의 SSMA 클라이언트 구성 됩니다.  
  
-   DB2 데이터베이스에 연결 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 연결합니다.  
  
-   DB2 데이터베이스 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문입니다.  
  
-   에 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
이 항목에서는 설치 필수 구성 요소 및 SSMA를 설치 하기 위한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA는 z/OS 버전 9.0 / 10.0에서 DB2 또는 LUW 버전 9.8 및 10.1 이상 버전에서 d b 2와 작동 하도록 설계 되었습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 2014 합니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 또는 이후 버전 또는 Windows Server 2008 또는 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 또는 이후 버전입니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0 또는 이후 버전입니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0을 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품 미디어입니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   Microsoft OLEDB Provider DB2 버전 5 이상 버전 및 마이그레이션하려는 DB2 데이터베이스에 연결 합니다.  
  
-   에 대 한 액세스 및의 대상 인스턴스를 호스트 하는 컴퓨터에 대 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 위치 하는 마이그레이션 데이터베이스 개체 및 데이터입니다. 자세한 내용은 참조 [SQL Server &#40; DB2eToSQL &#41;에 연결](../../ssma/db2/connecting-to-sql-server-db2etosql.md)합니다.  
  
-   4GB RAM 권장 합니다.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLE DB Provider for DB2  
OLEDB provider for DB2 버전 5.0 다운로드 하려면로 이동 하십시오 [Microsoft® SQL Server® 2014 기능 팩](http://www.microsoft.com/download/details.aspx?id=42295)합니다.  
  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](http://aka.ms/ssmafordb2)합니다.  
  
SSMA를 설치 하기 전에 최신 버전을 다운로드 한 후의 설치 파일을 추출 해야 합니다.  
  
**SSMA 클라이언트를 설치 하려면**  
  
1.  D b 2 용 SSMA를 두 번 클릭  *n* 합니다. Install.exe 여기서  *n*  는 빌드 번호입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소가 없는 필수 구성 요소를 먼저 설치 해야 한다는 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 하 고 다음 설치 프로그램을 다시 실행 했는지 확인 합니다.  
  
3.  최종 사용자 사용권 계약을 읽어보십시오. 동의 하면 선택 **사용권 계약에 동의**, 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **일반**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 d b 2에 대 한 모든 이전 버전의 SSMA 제거 하십시오.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for d b 2입니다.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server &#40; DB2ToSQL &#41;에 SSMA 구성 요소 설치](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[SQL Server &#40; DB2ToSQL &#41; DB2 데이터베이스 마이그레이션](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  

