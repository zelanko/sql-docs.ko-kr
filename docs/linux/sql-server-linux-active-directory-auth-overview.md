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
ms.openlocfilehash: 32ff23fe1ea7f0a892a19cc6be0eef8439ee907f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "75831822"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Linux의 SQL Server에 대한 Active Directory 인증

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

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

The details for how to configure AD authentication are provided in the tutorial, [Tutorial: Use Active Directory authentication with SQL Server on Linux](sql-server-linux-active-directory-authentication.md). 다음 목록에서는 자습서의 각 섹션에 대한 링크를 포함하는 요약을 제공합니다.

1. [SQL Server 호스트를 Active Directory 도메인 가입](sql-server-linux-active-directory-join-domain.md)
1. [SQL Server의 AD 사용자를 만들고 ServicePrincipalName 설정](sql-server-linux-active-directory-authentication.md#createuser)
1. [SQL Server 서비스 키탭 구성](sql-server-linux-active-directory-authentication.md#configurekeytab)
1. [키탭 파일 보호](sql-server-linux-active-directory-authentication.md#configurekeytab)
1. [Kerberos 인증에 키탭 파일을 사용하도록 SQL Server 구성](sql-server-linux-active-directory-authentication.md#configurekeytab)
1. [Transact-SQL에서 AD 기반 SQL Server 로그인 만들기](sql-server-linux-active-directory-authentication.md#createsqllogins).
1. [AD 인증을 사용하여 SQL Server에 연결](sql-server-linux-active-directory-authentication.md#connect)

## <a name="known-issues"></a>알려진 문제

- 현재, 데이터베이스 미러링 엔드포인트에 지원되는 인증 방법은 인증서뿐입니다. 이후 릴리스에서는 WINDOWS 인증 방법을 사용할 수 있습니다.

## <a name="next-steps"></a>다음 단계

For more information on how to implement Active Directory authentication for SQL Server on Linux, see [Tutorial: Use Active Directory authentication with SQL Server on Linux](sql-server-linux-active-directory-authentication.md).
