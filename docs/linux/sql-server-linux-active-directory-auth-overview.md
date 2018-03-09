---
title: "Linux에서 SQL Server 용 active Directory 인증 | Microsoft Docs"
description: "이 문서는 Linux에서 SQL Server에 대 한 Active Directory 인증에 대 한 개요를 제공합니다."
author: rothja
ms.date: 02/23/2018
ms.author: jroth
manager: craigg
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
helpviewer_keywords:
- Linux, AAD authentication
ms.workload: On Demand
ms.openlocfilehash: f3c516465d9703ae736350e660aefba15a5636c9
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/24/2018
---
# <a name="active-directory-authentication-for-sql-server-on-linux"></a>Linux에서 SQL Server 용 active Directory 인증

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

이 문서에서는의 Active Directory (AD) 인증에 대 한 개요를 제공 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] linux. AD 인증을 프로젝트에서 통합된 인증 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]합니다. 

## <a name="ad-authentication-overview"></a>AD 인증 개요

AD 인증을 통해 인증 하는 데 Windows 또는 Linux에서 도메인에 가입 된 클라이언트 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 해당 도메인 자격 증명 및 Kerberos 프로토콜을 사용 하 여 합니다.

AD 인증을 통해 다음과 같은 이점을 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 인증:

- Single sign-on을 통해 암호를 입력 하지 않고 사용자를 인증 합니다.   
- AD 그룹에 대 한 로그인을 만들어 액세스 및 권한을 관리할 수 있습니다 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] AD 그룹 멤버 자격을 사용 하 여 합니다.  
- 추적 하는 필요 없이 조직 전체에서 단일 id는 각 사용자가 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 사람에 해당 하는 로그인입니다.   
- AD를 사용 하면 조직 전체에서 중앙 집중화 된 암호 정책을 적용할 수 있습니다.   

## <a name="configuration-steps"></a>구성 단계

Active Directory 인증을 사용 하려면 네트워크에서 AD 도메인 컨트롤러 (Windows) 있어야 합니다.

AD 인증을 구성 하는 방법에 대 한 세부 정보는 자습서에 제공 됩니다 [자습서: Linux에서 SQL Server와 함께 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다. 다음 목록에는 자습서의 각 섹션에 대 한 링크가 있는 요약을 제공합니다.

1. [SQL Server 호스트는 Active Directory 도메인에 가입](sql-server-linux-active-directory-authentication.md#join)합니다.
1. [SQL Server에 대 한 AD 사용자를 만들고 ServicePrincipalName 설정](sql-server-linux-active-directory-authentication.md#createuser)합니다.
1. [SQL Server 서비스 keytab 구성](sql-server-linux-active-directory-authentication.md#configurekeytab)합니다.
1. [TRANSACT-SQL에서 AD 기반 SQL Server 로그인을 만들고](sql-server-linux-active-directory-authentication.md#createsqllogins)합니다.
1. [AD 인증을 사용 하 여 SQL Server에 연결](sql-server-linux-active-directory-authentication.md#connect)합니다.

## <a name="known-issues"></a>알려진 문제

- 이 경우 데이터베이스 미러링 끝점에 지원 되는 유일한 인증 방법에는 인증서입니다. 이후 릴리스에서 WINDOWS 인증 방법을 사용할 수 있습니다.
- Vintela 지원 되지 않습니다 및 제 3 자 AD 도구 같은 Centrify, Powerbroker, 합니다.

## <a name="next-steps"></a>다음 단계

Linux에서 SQL Server 용 Active Directory 인증을 구현 하는 방법에 대 한 자세한 내용은 참조 하십시오. [자습서: Linux에서 SQL Server와 함께 사용 하 여 Active Directory 인증](sql-server-linux-active-directory-authentication.md)합니다.