---
title: SQL Server 에이전트 속성(연결 탭) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.connection.f1
ms.assetid: d6a677ff-60ad-47ba-a0cb-df4193b165e0
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2a65d1bbc27fc968dfa26a9406b9371db85ba9fc
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681830"
---
# <a name="sql-server-agent-properties-connection-page"></a>SQL Server 에이전트 속성(연결 탭)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> 현재 [Azure SQL Database Managed Instance](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance)에서 일부 SQL Server 에이전트 기능이 지원됩니다. 자세한 내용은 [SQL Server에서 Azure SQL Database Managed Instance T-SQL 차이점](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent)을 참조하세요.

이 페이지를 사용하여 [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스와 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]간의 연결 설정을 확인하고 수정할 수 있습니다.  
  
## <a name="options"></a>옵션  
**로컬 호스트 서버 별칭**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 로컬 인스턴스에 연결하는 데 사용할 별칭을 지정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트에 기본 연결 옵션을 사용할 수 없는 경우 인스턴스에 대한 별칭을 정의한 후 여기에서 해당 별칭을 지정합니다.  
  
**Windows 인증 사용**  
[!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows 인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 연결에 사용하는 인증 방법으로 설정합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트 서비스 실행에 사용되는 계정으로 연결하게 됩니다.  
  
**SQL Server 인증 사용**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증을 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스 연결에 사용하는 인증 방법으로 설정합니다.  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인증은 이전 버전과의 호환성을 위해 제공됩니다. 보안 향상을 위해 가능하면 Windows 인증을 사용합니다.  
  
**로그인**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결에 사용할 로그인 이름을 지정합니다.  
  
**암호**  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]연결에 사용할 암호를 지정합니다.  
  
