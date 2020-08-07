---
title: SAP ASE 용 SSMA 클라이언트 설치 (SybaseToSQL) | Microsoft Docs
description: ASE (SAP 적응 서버 엔터프라이즈)의 SSMA (SQL Server Migration Assistant 설치 필수 구성 요소 및 설치 방법에 대해 알아봅니다.
ms.custom: ''
ms.date: 07/14/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: e770c2f2-52b9-4471-a207-0d35df41399c
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 5907a7cc5b93594beef8f7bd54f27f20b93fbb99
ms.sourcegitcommit: 21bedbae28840e2f96f5e8b08bcfc794f305c8bc
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864860"
---
# <a name="installing-ssma-for-sap-ase-client-sybasetosql"></a>SAP ASE 클라이언트용 SSMA 설치 (SybaseToSQL)

SSMA 클라이언트는 SAP 적응 서버 엔터프라이즈 (ASE) 데이터베이스 서버 및 인스턴스에 연결 하는 데 사용 되는 프로그램 파일로 구성 되며 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] ase 데이터베이스 개체를 또는 구문으로 변환 하 고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 개체를 또는로 로드 하 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 고, 데이터를 또는로 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

이 항목에서는 SSMA 설치를 위한 필수 구성 요소 및 지침을 제공 합니다.

## <a name="prerequisites"></a>필수 구성 요소

SSMA는 SAP ASE 11.9.2 이상 버전 및 모든 버전에서 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.

- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 버전 4.7.2 이상 버전입니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수 있습니다.
- Sybase OLE DB/ADO.Net/ODBC 공급자 및 마이그레이션할 데이터베이스가 포함 된 SAP ASE 데이터베이스 서버에 대 한 연결입니다. SAP ASE 제품 미디어에서 공급자를 설치할 수 있습니다. 연결에 대 한 자세한 내용은 [SYBASE ASE &#40;SybaseToSQL&#41;에 연결을 ](../../ssma/sybase/connecting-to-sybase-ase-sybasetosql.md)참조 하세요.
- 대상 인스턴스를 호스트 하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 데이터베이스 개체와 데이터를 마이그레이션할 컴퓨터에 대 한 액세스 권한이 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 있어야 합니다. 자세한 내용은 [SQL Server에 연결 &#40;sybasetosql&#41;](../../ssma/sybase/connecting-to-sql-server-sybasetosql.md) / [Azure SQL Database &#40;sybasetosql&#41;에 연결 ](../../ssma/sybase/connecting-to-azure-sql-db-sybasetosql.md)을 참조 하세요.
- 4gb RAM 권장.

## <a name="installing-the-ssma-for-sybase-client"></a>Sybase 클라이언트용 SSMA 설치

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaforsybase)를 참조 하세요.

SSMA 클라이언트를 설치 하려면:

1. **SSMAforSybase_*n*.msi**를 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.
2. Welcome 페이지에서 **다음**을 클릭합니다.

   필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 함을 나타내는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.

3. 최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.
4. 설치 유형 선택 페이지에서 **일반**을 클릭 합니다.
5. **설치 준비 완료** 페이지에서 도구를 시작할 때마다 원격 분석 및 자동 업데이트 검사를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. **설치**를 클릭하여 설치를 시작합니다.

> [!IMPORTANT]
> 새 버전을 설치 하기 전에 먼저 Sybase 용 SSMA의 모든 이전 버전을 제거 하세요.

기본 설치 위치는 `C:\Program Files\Microsoft SQL Server Migration Assistant for Sybase`입니다.

SSMA 프로그램 파일 외에도 Sybase 용 SSMA 확장 팩을 설치 해야 합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 자세한 내용은 [SQL Server에 SSMA 구성 요소 설치 &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)를 참조 하세요.

## <a name="see-also"></a>참고 항목

- [SQL Server에 SSMA 구성 요소 설치](../../ssma/sybase/installing-ssma-components-on-sql-server-sybasetosql.md)  
- [Sybase ASE 데이터베이스를 SQL Server-Azure SQL Database로 마이그레이션](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)
