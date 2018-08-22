---
title: 액세스 (AccessToSQL)에 대 한 SQL Server Migration Assistant를 설치 합니다. | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
helpviewer_keywords:
- installing SSMA
- instructions, installation
- instructions, upgrade
- licensing SSMA
- prerequisites for installing SSMA
- procedure, installation
- procedure, licensing
- procedure, upgrading
- removing SSMA
- Setup
- uninstalling SSMA
- upgrading SSMA
ms.assetid: dd50eebd-75df-4e0d-8c4d-88b511aae4c7
caps.latest.revision: 31
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: dacd6634e57043ca53dfceb9bf3d793b35c90a47
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393087"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>액세스 (AccessToSQL)에 대 한 SQL Server Migration Assistant 설치
[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) 액세스를 위한 Windows Installer 기반 마법사를 사용 하 여 설치 됩니다. 이 항목에서는 최신 버전의 SSMA 연결할 설치 필수 구성 요소에 대 한 정보 및 설치, 라이선스, 제거 및 SSMA 업그레이드에 대 한 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항  
SSMA를 설치 하기 전에 시스템에는 다음 요구 사항을 충족 하는지 확인 합니다.  
  
-   Windows 7 또는 이후 버전 또는 Windows Server 2008 또는 이상 버전.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 이상이 있습니다.  
  
-   [!INCLUDE[msCoName](../../includes/msconame_md.md)] .NET Framework 버전 4.0 이상이 있습니다. .NET Framework 버전 4.0에서 사용할 수는 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 제품 디스크에서 정보를 사용 하 여 합니다 [Microsoft.NET 가이드](https://docs.microsoft.com/dotnet/framework/)합니다.
  
-   에 대 한 액세스 및 대상 인스턴스를 호스팅하는 컴퓨터에서 충분 한 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]SQL Azure DB를 마이그레이션될 데이터베이스 개체 및 데이터입니다.  
  
-   Microsoft 데이터 액세스 개체 (DAO) 공급자 버전 12.0 또는 14.0입니다. 2007 Microsoft Office 2010 제품에서 DAO 공급자를 설치 하거나 Microsoft 웹 사이트에서 다운로드할 수 있습니다.  
  
-   SQL Server Native Access 클라이언트 (SNAC) 버전 10.5 이상을 SQL Azure 마이그레이션에 대 한 합니다. SNAC의 최신 버전을 가져올 수 있습니다 [Microsoft® SQL Server® 2008 R2 기능 팩](http://go.microsoft.com/fwlink/?LinkId=196940)  
  
-   4GB RAM (권장)입니다.  
  
## <a name="installing-ssma"></a>SSMA 설치  
SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 참조는 [SQL Server Migration Assistant 다운로드 페이지](http://aka.ms/ssmaforaccess)합니다.  
  
최신 버전을 다운로드 한 후 SSMA를 설치 하기 전에 설치 파일에서 추출 해야 합니다.

> [!IMPORTANT]  
> -   새 버전을 설치 하기 전에 모든 이전 버전의 SSMA for Access 제거 하세요.  
  
**SSMA를 설치 하려면**  
  
1.  SSMA for Access 두 번 클릭 *n*.msi, 여기서 *n* 빌드입니다.  
  
2.  시작 페이지에서 클릭 **다음**합니다.  
  
    설치 필수 구성 요소가 없으면 설치 해야 하는 먼저 필수 구성 요소를 나타내는 메시지가 나타납니다. 모든 필수 구성 요소가 설치 되어 있고 다음 설치 프로그램을 다시 실행 해야 합니다.  
  
3.  최종 사용자 사용권 계약; 읽기 동의 하는 경우 선택 **계약에 동의**를 클릭 하 고 **다음**합니다.  
  
4.  설치 유형 선택 페이지에서 클릭 **표준**합니다.  
  
5.  **설치**를 클릭합니다.  
  
기본 설치 위치는 C:\Program Files\Microsoft SQL Server Migration Assistant for Access입니다.  
  
## <a name="uninstalling-ssma-for-access"></a>제거 SSMA for Access  
SSMA를 사용 하 여 제거할 **프로그램 추가 / 제거** 제어판에서. 프로그램을 제거 하지 SSMA 프로젝트 파일을 삭제 않거나 로그 파일을 알아야 합니다.  
  
**SSMA를 제거 하려면**  
  
1.  클릭 **시작**, 클릭 **제어판**를 클릭 하 고 **프로그램 추가 / 제거**합니다.  
  
2.  선택 **Microsoft SQL Server Migration Assistant for Access**를 클릭 하 고 **제거**합니다.  
  
## <a name="upgrading-to-a-later-version"></a>이후 버전으로 업그레이드  
Access 용 SSMA의 이후 버전으로 업그레이드 하려는 경우 먼저 SSMA for Access 제거 하 고 최신 버전을 설치 해야 합니다. 이 프로세스를 완료 하려면 액세스 섹션에 대 한 제거 SSMA의 지침을 따릅니다.  
  
Access 용 SSMA의 이전 버전에서 만든 프로젝트를 열면 SSMA 프로젝트를 최신 버전으로 변환 하려는 경우 요청 합니다. 클릭 **예** 최신 버전의 SSMA에서 프로젝트를 사용 하 여 작동 합니다.  
  
## <a name="see-also"></a>참고자료  
[Access 데이터베이스 마이그레이션 준비](preparing-access-databases-for-migration-accesstosql.md)  
[SQL Server에 대 한 액세스 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
[SQL Server에 대 한 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
