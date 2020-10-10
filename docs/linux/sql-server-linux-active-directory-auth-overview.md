---
title: Linux의 SQL Server에 대한 Active Directory 인증
titleSuffix: SQL Server
description: 이 문서에서는 Linux의 SQL Server에 대한 Active Directory 인증 개요를 제공합니다.
ms.date: 04/01/2019
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: efce6c9f297c3dba58a37a3d097a9c8176efa287
ms.sourcegitcommit: b93beb4f03aee2c1971909cb1d15f79cd479a35c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91497999"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Linux의 SQL Server에 대한 Active Directory 인증

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

이 문서에서는 Linux의 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에 대한 AD(Active Directory) 인증 개요를 제공합니다. AD 인증은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 통합 인증으로도 알려져 있습니다.

## <a name="ad-authentication-overview"></a>AD 인증 개요

AD 인증을 사용할 경우 Windows 또는 Linux의 도메인 가입 클라이언트는 도메인 자격 증명 및 Kerberos 프로토콜을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 인증을 받을 수 있습니다.

AD 인증에는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증에 비해 다음과 같은 이점이 있습니다.

- 암호 입력 요구 없이, 사용자는 Single Sign-On을 통해 인증을 받습니다.
- AD 그룹에 대한 로그인을 만들면 AD 그룹 멤버 자격을 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]에서 액세스 및 사용 권한을 관리할 수 있습니다.  
- 각 사용자는 조직 전체에서 단일 ID를 유지하므로 어떤 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 로그인이 어떤 사용자에게 해당하는지를 추적할 필요가 없습니다.   
- AD를 사용하면 조직 전체에서 중앙 집중식 암호 정책을 적용할 수 있습니다.

## <a name="configuration-steps"></a>구성 단계

Active Directory 인증을 사용하려면 네트워크에 AD 도메인 컨트롤러(Windows)가 있어야 합니다.

AD 인증을 구성하는 방법에 대한 자세한 내용은 [자습서: Linux에서 SQL Server와 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md)을 참조하세요. 다음 목록에서는 자습서의 각 섹션에 대한 링크를 포함하는 요약을 제공합니다.

1. [SQL Server 호스트를 Active Directory 도메인 가입](sql-server-linux-active-directory-join-domain.md)
1. [SQL Server의 AD 사용자를 만들고 ServicePrincipalName 설정](sql-server-linux-active-directory-authentication.md#createuser)
1. [SQL Server 서비스 키탭 구성](sql-server-linux-active-directory-authentication.md#configurekeytab)
1. [키탭 파일 보호](sql-server-linux-active-directory-authentication.md#configurekeytab)
1. [Kerberos 인증에 키탭 파일을 사용하도록 SQL Server 구성](sql-server-linux-active-directory-authentication.md#configurekeytab)
1. [Transact-SQL에서 AD 기반 SQL Server 로그인 만들기](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [AD 인증을 사용하여 SQL Server에 연결](sql-server-linux-active-directory-authentication.md#connect)

## <a name="known-issues"></a>알려진 문제

- 현재, 데이터베이스 미러링 엔드포인트에 지원되는 인증 방법은 인증서뿐입니다. 이후 릴리스에서는 WINDOWS 인증 방법을 사용할 수 있습니다.
- SQL Server on Linux는 원격 연결용 NTLM 프로토콜을 지원하지 않습니다. NTLM을 사용하여 로컬 연결을 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

Linux의 SQL Server에 대한 Active Directory 인증 구현 방법과 관련된 자세한 내용은 [자습서: Linux에서 SQL Server와 Active Directory 인증 사용](sql-server-linux-active-directory-authentication.md)을 참조하세요.
