---
title: DB2 클라이언트 (DB2ToSQL) 용 SSMA 설치 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
caps.latest.revision: 8
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c0c356d54dd74ae75962d9893968ff302e7e5f98
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/14/2018
ms.locfileid: "40396151"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>DB2 클라이언트 (DB2ToSQL) 용 SSMA 설치
SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.  
  
-   DB2 데이터베이스에 연결 합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
-   DB2 데이터베이스 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구문입니다.  
  
-   에 개체를 로드할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
-   데이터를 마이그레이션하기 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]합니다.  
  
이 항목에서는 설치 필수 구성 요소 및 SSMA 설치에 대 한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
SSMA는 DB2 버전 9.0 / 10.0 z/os 또는 LUW 버전 9.8 및 10.1 이상 버전에서 DB2를 사용 하 여 작동 하도록 설계 되었습니다 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2012 및 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2014입니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 이상 버전 또는 Windows Server 2008 또는 이상 버전.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 이상이 있습니다.  
  
-   합니다 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0 이상이 있습니다. 합니다 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0에서 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 미디어입니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   DB2 버전 5 이상 버전 및 마이그레이션하려는 DB2 데이터베이스에 대 한 연결에 대 한 Microsoft OLEDB 공급자입니다.  
  
-   에 대 한 액세스 및 대상 인스턴스를 호스팅하는 컴퓨터에서 충분 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL DB는 마이그레이션될 데이터베이스 개체 및 데이터입니다. 자세한 내용은 [SQL Server에 연결 &#40;DB2eToSQL&#41;](../../ssma/db2/connecting-to-sql-server-db2etosql.md)합니다.  
  
-   4GB RAM이 권장 됩니다.  
  
## <a name="microsoft-oledb-provider-for-db2"></a>Microsoft OLE DB Provider for DB2  
OLEDB provider for DB2 버전 5.0 다운로드 하려면로 이동 하십시오 [Microsoft® SQL Server® 2014 기능 팩](http://www.microsoft.com/download/details.aspx?id=42295)합니다.  
  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](http://aka.ms/ssmafordb2)합니다.  
  
최신 버전을 다운로드 한 후 SSMA를 설치 하기 전에 설치 파일에서 추출 해야 합니다.  
  
**SSMA 클라이언트 설치**  
  
1.  DB2 용 SSMA를 두 번 클릭 *n*합니다. Install.exe, 여기서 *n* 빌드입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소에 필수 구성 요소를 먼저 설치 해야 한다는 나타내는 메시지가 나타납니다. 모든 필수 구성 요소가 설치 되어 있고 다음 설치 프로그램을 다시 실행 해야 합니다.  
  
3.  최종 사용자 사용권 계약을 읽습니다. 동의 하는 경우 선택 **사용권 계약에 동의**를 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **표준**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 DB2 용 SSMA의 모든 이전 버전을 제거 하세요.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for DB2입니다.  
  
## <a name="see-also"></a>관련 항목  
[SQL Server에 SSMA 구성 요소를 설치 &#40;DB2ToSQL&#41;](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)  
[SQL Server로 데이터베이스 마이그레이션 DB2 &#40;DB2ToSQL&#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)  
  
