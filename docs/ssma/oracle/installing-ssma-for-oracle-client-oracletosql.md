---
title: Oracle 클라이언트 (OracleToSQL) 용 SSMA를 설치 합니다. | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 33abd4c84e195760791c417b3eb629fa5af3fe01
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Oracle 클라이언트 (OracleToSQL) 용 SSMA를 설치합니다.
다음 작업을 수행 하는 프로그램 파일의 SSMA 클라이언트 구성 됩니다.  
  
-   Oracle 데이터베이스에 연결합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 인스턴스에 연결합니다.  
  
-   Oracle 데이터베이스 개체를 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 구문입니다.  
  
-   에 개체를 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
-   데이터를 마이그레이션할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
이 항목에서는 설치 필수 구성 요소 및 SSMA를 설치 하기 위한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>필수 구성 요소  
SSMA는 Oracle 9 또는 이후 버전의 모든 버전와 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다.  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 또는 이후 버전 또는 Windows Server 2008 또는 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 또는 이후 버전입니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0 또는 이후 버전입니다. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0을 사용할 수는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 제품 미디어입니다. 가져올 수도 있습니다는 [.NET Framework 개발자 센터](http://go.microsoft.com/fwlink/?LinkId=48882)합니다.  
  
-   Oracle 클라이언트 9.0 또는 이후 버전와 마이그레이션하려는 Oracle 데이터베이스에 연결 합니다. Oracle 클라이언트 버전와 동일한 버전 또는 Oracle 데이터베이스 버전 보다 이후 버전 이어야 합니다.  
  
    Oracle 제품 미디어 또는 Oracle 웹 사이트에서 Oracle 클라이언트를 설치할 수 있습니다. 연결에 대 한 정보를 참조 하십시오. [Oracle 데이터베이스에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)합니다.  
  
-   에 대 한 액세스 및의 대상 인스턴스를 호스트 하는 컴퓨터에 대 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 또는 Azure SQL DB 위치 하는 마이그레이션 데이터베이스 개체 및 데이터입니다. 자세한 내용은 참조 [SQL Server에 연결 &#40;OracleToSQL&#41;](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)합니다.  
  
-   4GB RAM 권장 합니다.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>SSMA는 Oracle 클라이언트에 대 한 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](http://aka.ms/ssmafororacle)합니다.  
  
SSMA를 설치 하기 전에 최신 버전을 다운로드 한 후의 설치 파일을 추출 해야 합니다.  
  
**SSMA 클라이언트를 설치 하려면**  
  
1.  Oracle 용 SSMA를 두 번 클릭 *n*합니다. Install.exe 여기서 *n* 는 빌드 번호입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소가 없는 필수 구성 요소를 먼저 설치 해야 한다는 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 하 고 다음 설치 프로그램을 다시 실행 했는지 확인 합니다.  
  
3.  최종 사용자 사용권 계약을 읽어보십시오. 동의 하면 선택 **사용권 계약에 동의**, 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **일반**합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 Oracle 용 SSMA의 모든 이전 버전을 제거 하십시오.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for Oracle입니다.  
  
SSMA 프로그램 파일 외에 설치 해야 Oracle 확장 팩 용 SSMA에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]합니다. 자세한 내용은 참조 [SQL Server에서 SSMA 구성 요소 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)합니다.  
  
## <a name="see-also"></a>관련 항목:  
[SQL Server에 SSMA 구성 요소 설치 &#40;OracleToSQL&#41;](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[SQL Server로 데이터베이스 마이그레이션 Oracle &#40;OracleToSQL&#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
