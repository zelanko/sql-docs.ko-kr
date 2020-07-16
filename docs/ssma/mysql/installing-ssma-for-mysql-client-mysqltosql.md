---
title: MySQL 용 SSMA 클라이언트 설치 (MySQLToSQL) | Microsoft Docs
description: MySQL 클라이언트의 SSMA (SQL Server Migration Assistant)에 대 한 설치 필수 구성 요소 및 설치 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Installing client,Licensing
ms.assetid: ede3128c-370d-45a5-a815-3d94eecaea30
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 7dc2cb4216386e13c57d31f121809a604e91b67d
ms.sourcegitcommit: fd7b268a34562d70d46441f689543ecce7df2e4d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411611"
---
# <a name="installing-ssma-for-mysql-client-mysqltosql"></a>MySQL 용 SSMA 클라이언트 설치 (MySQLToSQL)

MySQL 용 SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.

- MySQL 데이터베이스에 연결 합니다.  
- 또는의 인스턴스에 연결 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 합니다.
- MySQL 데이터베이스 개체를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 개체로 변환 합니다.
- 개체를 또는로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로드 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 합니다.
- 또는로 데이터를 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

이 항목에서는 설치 필수 구성 요소 및 MySQL 용 SSMA 클라이언트를 설치 하기 위한 지침을 제공 합니다.

## <a name="prerequisites"></a>필수 조건

MySQL 용 SSMA는 MySQL 4.1 이상 버전 및 2012 이상의 모든 버전 및에서 작동 하도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] .

SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.

- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)]Windows Installer 3.1 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.7.2 이상 버전입니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수 있습니다.
- MySQL ODBC 5.1 드라이버 및 마이그레이션하려는 MySQL 데이터베이스에 연결 합니다. Mysql 웹 사이트에서 MySQL을 설치할 수 있습니다. 연결에 대 한 자세한 내용은 [MySQL에 연결 &#40;MySQLToSQL&#41;](../../ssma/mysql/connecting-to-mysql-mysqltosql.md)을 참조 하세요.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]데이터베이스 개체와 데이터를 마이그레이션할 대상 인스턴스를 호스트 하는 컴퓨터에 대 한 액세스 및 충분 한 권한 자세한 내용은 [MySQLToSQL&#41;&#40;SQL Server에 연결 ](../../ssma/mysql/connecting-to-sql-server-mysqltosql.md)을 참조 하세요.
- 프로젝트의 경우 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 데이터베이스 개체와 데이터를 마이그레이션할 인스턴스에 액세스 하 고이에 대 한 충분 한 권한을 부여 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 합니다. 자세한 내용은 [AZURE SQL DB &#40;MySQLToSQL&#41;에 연결 ](../../ssma/mysql/connecting-to-azure-sql-db-mysqltosql.md)을 참조 하세요.
- 4gb RAM 권장.

## <a name="installing-ssma-for-mysql-client"></a>MySQL 용 SSMA 클라이언트 설치

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaformysql)를 참조 하세요.

SSMA 클라이언트를 설치 하려면:

1. **SSMAforMySQL_*n*.msi**를 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.
2. **Welcome** 페이지에서 **다음**을 클릭합니다.

   필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 한다는 메시지가 표시 됩니다. 설치 프로그램을 다시 실행 하기 전에 모든 필수 구성 요소를 설치 했는지 확인 합니다.

3. 최종 사용자 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.
4. **설치 유형 선택** 페이지에서 **일반**을 클릭 합니다.
5. **설치 준비 완료** 페이지에서 도구를 시작할 때마다 원격 분석 및 자동 업데이트 검사를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. **설치**를 클릭하여 설치를 시작합니다.

> [!IMPORTANT]
> 새 버전을 설치 하기 전에 먼저 MySQL 용 SSMA의 모든 이전 버전을 제거 하세요.

기본 설치 위치는 `C:\Program Files\Microsoft SQL Server Migration Assistant for MySQL`입니다.

## <a name="see-also"></a>추가 정보

- [MySQL 데이터베이스를 SQL Server로 마이그레이션-Azure SQL DB](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md)  
