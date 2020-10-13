---
title: 액세스용 SQL Server Migration Assistant 설치 (AccessToSQL) | Microsoft Docs
description: SSMA (SQL Server Migration Assistant)의 설치 필수 구성 요소에 대해 알아보고 설치, 라이선스, 업그레이드 및 제거 하는 방법에 대해 알아봅니다.
ms.prod: sql
ms.custom: ''
ms.date: 07/14/2020
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
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
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 1313699a3d82e0dbced8469f251a0a105f296246
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985249"
---
# <a name="installing-sql-server-migration-assistant-for-access-accesstosql"></a>액세스용 SQL Server Migration Assistant 설치 (AccessToSQL)

[!INCLUDE[msCoName](../../includes/msconame_md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Access 용 SSMA (Migration Assistant)는 Windows Installer 기반 마법사를 사용 하 여 설치 됩니다. 이 항목에서는 설치 필수 구성 요소, 최신 버전의 SSMA 링크 및 SSMA 설치, 라이선스, 제거 및 업그레이드에 대 한 지침을 제공 합니다.

## <a name="prerequisites"></a>필수 구성 요소

SSMA를 설치 하기 전에 시스템이 다음과 같은 요구 사항을 충족 하는지 확인 합니다.

- Windows 7 이상 버전 또는 Windows Server 2008 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Installer 3.1 이상 버전
- [!INCLUDE[msCoName](../../includes/msconame_md.md)].NET Framework 버전 4.7.2 이상 버전입니다. .NET Framework은 [Microsoft .NET 가이드](/dotnet/framework/)에서 사용할 수 있습니다.
- 대상 인스턴스를 호스트 하는 컴퓨터 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 데이터베이스 개체와 데이터를 마이그레이션할 컴퓨터에 대 한 액세스 권한이 [!INCLUDE[ssAzure](../../includes/ssazure_md.md)] 있어야 합니다.
- Microsoft DAO (Data Access Object) 공급자 버전 12.0 또는 14.0입니다. Microsoft Office 2010/2007 제품에서 DAO 공급자를 설치 하거나 Microsoft 웹 사이트에서 다운로드할 수 있습니다.
- 4gb RAM (권장).

## <a name="installing-ssma"></a>SSMA 설치

SSMA는 웹 다운로드입니다. 최신 버전을 다운로드 하려면 [SQL Server Migration Assistant 다운로드 페이지](https://aka.ms/ssmaforaccess)를 참조 하세요.

> [!IMPORTANT]
> 새 버전을 설치 하기 전에 이전 버전의 SSMA를 모두 제거 하세요.

SSMA를 설치 하려면:
  
1. **SSMAforAccess_*n*.msi**를 두 번 클릭 합니다. 여기서 *n* 은 빌드 번호입니다.
2. 시작 페이지에서 **다음**을 클릭합니다.

   필수 구성 요소가 설치 되어 있지 않은 경우 먼저 필수 구성 요소를 설치 해야 함을 나타내는 메시지가 나타납니다. 모든 필수 구성 요소를 설치 했는지 확인 한 후 설치 프로그램을 다시 실행 합니다.

3. End-User 사용권 계약을 읽습니다. 동의 하면 동의 함을 **선택 하**고 **다음**을 클릭 합니다.
4. **설치 유형 선택** 페이지에서 **일반**을 클릭 합니다.
5. **설치 준비 완료** 페이지에서 도구를 시작할 때마다 원격 분석 및 자동 업데이트 검사를 사용 하거나 사용 하지 않도록 설정할 수 있습니다. **설치**를 클릭하여 설치를 시작합니다.
  
기본 설치 위치는 `C:\Program Files\Microsoft SQL Server Migration Assistant for Access`입니다.

## <a name="uninstalling-ssma-for-access"></a>Access 용 SSMA 제거

제어판의 [ **프로그램 추가/제거** ]를 사용 하 여 ssma를 제거 합니다. 프로그램을 제거 해도 SSMA 프로젝트 파일이 나 로그 파일은 삭제 되지 않습니다.

SSMA를 제거 하려면:

1. **시작**, **제어판**, **프로그램 추가/제거**를 차례로 클릭합니다.
2. **액세스 Microsoft SQL Server Migration Assistant**선택 하 고 **제거**를 클릭 합니다.

## <a name="upgrading-to-a-later-version"></a>최신 버전으로 업그레이드

Access 용 SSMA의 이후 버전으로 업그레이드 하려면 먼저 액세스를 위해 SSMA를 제거한 다음 최신 버전을 설치 해야 합니다. Access 용 SSMA 제거 섹션의 지침에 따라이 프로세스를 완료 합니다.

Access 용 SSMA의 이전 버전에서 만든 프로젝트를 여는 경우 SSMA는 프로젝트를 최신 버전으로 변환할지 여부를 묻는 메시지를 표시할 수 있습니다. 최신 버전의 SSMA에서 프로젝트를 사용 하려면 **예** 를 클릭 합니다.

## <a name="see-also"></a>추가 정보

- [마이그레이션을 위해 Access 데이터베이스 준비](preparing-access-databases-for-migration-accesstosql.md)
- [SQL Server로 Access 데이터베이스 마이그레이션](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)
- [SQL Server에 액세스 응용 프로그램 연결](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)