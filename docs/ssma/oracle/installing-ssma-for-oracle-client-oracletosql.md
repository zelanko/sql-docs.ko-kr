---
title: Oracle 용 SSMA 클라이언트 설치 (OracleToSQL) | Microsoft Docs
description: Oracle 클라이언트용 SSMA (SQL Server Migration Assistant)의 설치 필수 구성 요소 및 설치 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Licensing SSMA
ms.assetid: d5d4903d-e296-4bbf-8780-63674c4d62d5
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: be5f48508c44dc456c2d19e1ff1eba985b982111
ms.sourcegitcommit: 59cda5a481cfdb4268b2744edc341172e53dede4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84293920"
---
# <a name="installing-ssma-for-oracle-client-oracletosql"></a>Oracle용 SSMA 클라이언트 설치(OracleToSQL)
SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.  
  
-   Oracle 데이터베이스에 연결합니다.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.  
  
-   Oracle 데이터베이스 개체를 구문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
-   개체를에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.  
  
-   데이터를로 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
이 항목에서는 SSMA 설치를 위한 필수 구성 요소 및 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
SSMA는 Oracle 9 이상 버전 및의 모든 버전에서 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 이상 버전 또는 Windows Server 2008 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.0 이상 버전 [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)]제품 미디어에서 버전 4.0을 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수도 있습니다.  
  
-   Oracle 클라이언트 9.0 이상 버전 및 마이그레이션할 Oracle 데이터베이스에 대 한 연결을 선택 합니다. Oracle 클라이언트 버전은 Oracle 데이터베이스 버전과 같거나 그 이후 버전 이어야 합니다.  
  
    Oracle 제품 미디어 또는 Oracle 웹 사이트에서 Oracle 클라이언트를 설치할 수 있습니다. 연결에 대 한 자세한 내용은 [Oracle Database &#40;OracleToSQL&#41;에 연결 ](../../ssma/oracle/connecting-to-oracle-database-oracletosql.md)을 참조 하세요.  
  
-   데이터베이스 개체와 데이터를 마이그레이션할 대상 인스턴스 또는 Azure SQL DB를 호스트 하는 컴퓨터에 대 한 액세스 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있어야 합니다. 자세한 내용은 [SQL Server &#40;OracleToSQL&#41;에 연결 ](../../ssma/oracle/connecting-to-sql-server-oracletosql.md)을 참조 하세요.  
  
-   4gb RAM 권장.  
  
## <a name="installing-the-ssma-for-oracle-client"></a>Oracle 용 SSMA 클라이언트 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmafororacle)를 참조 하세요.  
  
최신 버전을 다운로드 한 후에는에서 설치 파일을 추출 해야 SSMA를 설치할 수 있습니다.  
  
**SSMA 클라이언트를 설치 하려면**  
  
1.  SSMA for Oracle *n*.Install.exe을 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.  
  
2.  Welcome 페이지에서 **다음**을 클릭합니다.  
  
    필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 함을 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.  
  
3.  최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.  
  
4.  설치 유형 선택 페이지에서 **일반**을 클릭 합니다.  
  
5.  **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1.  새 버전을 설치 하기 전에 Oracle 용 SSMA의 모든 이전 버전을 제거 하세요.  
  
기본 설치 위치는 Files\Microsoft SQL Server Migration Assistant (Oracle의 경우)입니다.  
  
SSMA 프로그램 파일 외에도 Oracle 용 SSMA 확장 팩을 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SQL Server &#40;OracleToSQL&#41;에 SSMA 구성 요소 설치 ](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
[SQL Server &#40;OracleToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/oracle/installing-ssma-components-on-sql-server-oracletosql.md)  
[Oracle 데이터베이스를 SQL Server &#40;OracleToSQL&#41;로 마이그레이션](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md)  
  
