---
title: SAP ASE 용 SSMA 클라이언트 설치 (SybaseToSQL) | Microsoft Docs
description: ASE (SAP 적응 서버 엔터프라이즈)의 SSMA (SQL Server Migration Assistant 설치 필수 구성 요소 및 설치 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 1325e9ba882bed76ecfc1b11f8ca1c379ca74bb4
ms.sourcegitcommit: 6593b3b6365283bb76c31102743cdccc175622fe
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/02/2020
ms.locfileid: "84306252"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>SAP ASE 클라이언트용 SSMA 설치 (SybaseToSQL)

SSMA 클라이언트는 ASE (SAP 적응 서버 엔터프라이즈) 데이터베이스 서버와 인스턴스 또는 Azure SQL DB에 연결 하는 데 사용 되는 프로그램 파일로 구성 되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ase 데이터베이스 개체를 또는 AZURE sql db 구문으로 변환 하 고, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체를 또는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] azure sql db로 로드 한 다음, 데이터를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 Azure SQL Database로 마이그레이션합니다.  
  
이 항목에서는 SSMA 설치를 위한 필수 구성 요소 및 지침을 제공 합니다.  
  
## <a name="prerequisites"></a>사전 요구 사항

SSMA는 ASE 11.9.2 이상 버전 및 모든 버전에서 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.  
  
- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전  
- [!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 버전 4.0 이상 버전입니다. .NET Framework 버전 4.0은 제품 미디어에서 사용할 수 있습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수도 있습니다.  
- Sybase OLEDB/ADO.Net/ODBC 공급자 및 마이그레이션하려는 데이터베이스를 포함 하는 Sybase ASE 데이터베이스 서버에 대 한 연결입니다. Sybase ASE 제품 미디어에서 공급자를 설치할 수 있습니다. 연결에 대 한 자세한 내용은 [SYBASE ASE &#40;SybaseToSQL&#41;에 연결을 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)참조 하세요.  
- 데이터베이스 개체와 데이터를 마이그레이션할 대상 인스턴스 또는 Azure SQL DB를 호스트 하는 컴퓨터에 대 한 액세스 권한이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 있어야 합니다. 자세한 내용은 [SQL Server에 연결 &#40;sybasetosql&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [Azure SQL DB에 연결 &#40;sybasetosql&#41;](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)을 참조 하세요.  
- 4gb RAM 권장.  
  
## <a name="installing-the-ssma-for-sybase-client"></a>Sybase 클라이언트용 SSMA 설치

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaforsybase)를 참조 하세요.  
  
최신 버전을 다운로드 한 후에는에서 설치 파일을 추출 해야 SSMA를 설치할 수 있습니다.  
  
**SSMA 클라이언트를 설치 하려면**
  
1. Sybase *n*.Install.exe 용 ssma를 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.  
  
2. Welcome 페이지에서 **다음**을 클릭합니다.  
  
    필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 함을 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.  
  
3. 최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.  
  
4. 설치 유형 선택 페이지에서 **일반**을 클릭 합니다.  
  
5. **설치**를 클릭합니다.  
  
> [!IMPORTANT]  
> 1. 새 버전을 설치 하기 전에 먼저 Sybase 용 SSMA의 모든 이전 버전을 제거 하세요.
  
기본 설치 위치는 Sybase에 대 한 C:\Program Files\Microsoft SQL Server Migration Assistant입니다.  
  
SSMA 프로그램 파일 외에도 Sybase 용 SSMA 확장 팩을 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목

[SQL Server &#40;SybaseToSQL&#41;에 SSMA 구성 요소 설치](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
[Sybase ASE 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
