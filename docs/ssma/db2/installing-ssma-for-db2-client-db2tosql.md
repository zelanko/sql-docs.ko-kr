---
title: DB2 용 SSMA 클라이언트 설치 (DB2ToSQL) | Microsoft Docs
description: DB2 클라이언트용 SSMA (SQL Server Migration Assistant)의 설치 필수 구성 요소 및 설치 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 3ae2a470-6afd-4512-b6d1-fcbe6afe88ad
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a223f5dbf6e100ac776e2f3aebad51c9bb885abf
ms.sourcegitcommit: 82b92f73ca32fc28e1948aab70f37f0efdb54e39
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94869611"
---
# <a name="installing-ssma-for-db2-client-db2tosql"></a>DB2 용 SSMA 클라이언트 설치 (DB2ToSQL)

SSMA 클라이언트는 다음 작업을 수행 하는 프로그램 파일로 구성 됩니다.

- DB2 데이터베이스에 연결합니다.
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결합니다.
- DB2 데이터베이스 개체를 구문으로 변환 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.
- 개체를에 로드 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 합니다.
- 데이터를로 마이그레이션합니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

이 항목에서는 SSMA 설치를 위한 필수 구성 요소 및 지침을 제공 합니다.

## <a name="prerequisites"></a>사전 요구 사항

SSMA는 z/OS 버전 9.0 및 10.0 9.8, d b 2의 경우 d b 2와 10.1 이상 7.1 버전의 db2와 함께 사용할 수 있도록 설계 되었습니다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .

SSMA를 설치 하기 전에 컴퓨터가 다음 요구 사항을 충족 하는지 확인 합니다.

- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] 3.1 이상 버전을 Windows Installer 합니다.
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort_md.md)] 버전 4.7.2 이상 버전입니다. [.NET Framework 개발자 센터](https://go.microsoft.com/fwlink/?LinkId=48882)에서 가져올 수 있습니다.
- Microsoft OLE DB Provider for DB2 버전 5 이상 버전 및 마이그레이션할 DB2 데이터베이스에 대 한 연결을 선택 합니다.
- 의 대상 인스턴스를 호스트 하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 데이터베이스 개체와 데이터를 마이그레이션할 Azure SQL Database에 대 한 액세스 권한이 있어야 합니다. 자세한 내용은 [SQL Server &#40;DB2ToSQL&#41;에 연결 ](../../ssma/db2/connecting-to-sql-server-db2tosql.md)을 참조 하세요.
- 4gb RAM 권장.

## <a name="microsoft-ole-db-provider-for-db2"></a>Microsoft OLE DB Provider for DB2

OLE DB provider for DB2 버전 6.0을 다운로드 하려면 [Microsoft® SQL Server® 2017 기능 팩](https://www.microsoft.com/download/details.aspx?id=55992)으로 이동 합니다.

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmafordb2)를 참조 하세요.

SSMA 클라이언트를 설치 하려면:

1. **SSMAforDB2_ *n*.msi** 를 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.
2. **Welcome** 페이지에서 **다음** 을 선택합니다.

   필수 구성 요소를 설치 하지 않은 경우 먼저 필수 구성 요소를 설치 해야 한다는 메시지가 표시 됩니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.

3. End-User 사용권 계약을 읽습니다. 동의 **하면 동의 함을 선택 하** 고 **다음** 을 선택 합니다.
4. **설치 유형 선택** 페이지에서 **일반** 을 선택 합니다.
5. **설치 준비 완료** 페이지에서 도구를 시작할 때마다 원격 분석 및 자동 업데이트 검사를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. **설치** 를 클릭하여 설치를 시작합니다.

> [!IMPORTANT]
> 새 버전을 설치 하기 전에 d b 2 용 SSMA의 모든 이전 버전을 제거 하세요.

기본 설치 위치는 `C:\Program Files\Microsoft SQL Server Migration Assistant for DB2`입니다.

## <a name="see-also"></a>참조

- [SQL Server에 SSMA 구성 요소 설치](../../ssma/db2/installing-ssma-components-on-sql-server-db2tosql.md)
- [DB2 데이터베이스를 SQL Server로 마이그레이션](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md)
