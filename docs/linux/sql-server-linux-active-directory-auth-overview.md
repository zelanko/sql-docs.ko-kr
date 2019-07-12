---
title: Linux의 SQL Server에 대 한 active Directory 인증
titleSuffix: SQL Server
description: 이 문서에서는 Linux의 SQL Server에 대 한 Active Directory 인증 개요를 제공 합니다.
ms.date: 04/01/2019
author: Dylan-MSFT
ms.author: dygray
ms.reviewer: vanto
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
helpviewer_keywords:
- Linux, AAD authentication
ms.openlocfilehash: 14cb6a377e6aeb0fbd24f9808a794d68633f4ce6
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2019
ms.locfileid: "67834419"
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Linux의 SQL Server에 대 한 active Directory 인증

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는 Active Directory (AD) 인증에 대 한 개요를 제공 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux. AD 인증에서 통합된 인증이 라고도 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 

## <a name="ad-authentication-overview"></a>AD 인증 개요

AD 인증을 사용 하면 Windows 또는 Linux에서 인증할 수 있는 도메인에 가입 된 클라이언트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 자신의 도메인 자격 증명 및 Kerberos 프로토콜을 사용 하 여 합니다.

AD 인증을 통해 다음과 같은 이점을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증:

- Single sign-on을 통해 암호를 입력 하지 않고 사용자를 인증 합니다.   
- AD 그룹에 대 한 로그인을 만들어 액세스 및 권한을 관리할 수 있습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 그룹 멤버 자격을 사용 합니다.  
- 각 사용자가 단일 id를 조직 전체에서 추적할 수는 없는 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 어떤 사용자에 해당 하는 로그인입니다.   
- AD를 사용 하면 조직 전체에서 중앙 집중화 된 암호 정책을 적용할 수 있습니다.   

## <a name="configuration-steps"></a>구성 단계

Active Directory 인증을 사용 하려면 네트워크에서 AD 도메인 컨트롤러 (Windows) 해야 합니다.

AD 인증을 구성 하는 방법에 대 한 세부 정보는 자습서에 나와 [자습서: Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 하 여](sql-server-linux-active-directory-authentication.md)입니다. 다음은 자습서의 각 섹션에 대 한 링크를 사용 하 여 요약을 제공:

1. [SQL Server 호스트는 Active Directory 도메인에 가입](sql-server-linux-active-directory-join-domain.md)합니다.
1. [SQL Server에 대 한 AD 사용자를 만들고 ServicePrincipalName 설정](sql-server-linux-active-directory-authentication.md#createuser)합니다.
1. [SQL Server 서비스 keytab 구성](sql-server-linux-active-directory-authentication.md#configurekeytab)합니다.
1. [Keytab 파일을 보호](sql-server-linux-active-directory-authentication.md#securekeytab)합니다.
1. [Kerberos 인증에 대 한 키 파일을 사용 하도록 SQL Server 구성](sql-server-linux-active-directory-authentication.md#keytabkerberos)합니다.
1. [TRANSACT-SQL에서 AD 기반 SQL Server 로그인을 만들](sql-server-linux-active-directory-authentication.md#createsqllogins)합니다.
1. [AD 인증을 사용 하 여 SQL Server에 연결](sql-server-linux-active-directory-authentication.md#connect)합니다.

## <a name="known-issues"></a>알려진 문제

- 이때 데이터베이스 미러링 끝점에 지원 되는 유일한 인증 방법에는 인증서가 있습니다. 향후 릴리스에서 WINDOWS 인증 방법을 활성화 됩니다.

## <a name="next-steps"></a>다음 단계

Linux에서 SQL Server 용 Active Directory 인증을 구현 하는 방법에 대 한 자세한 내용은 참조 하세요. [자습서: Linux의 SQL Server를 사용 하 여 Active Directory 인증을 사용 하 여](sql-server-linux-active-directory-authentication.md)입니다.
