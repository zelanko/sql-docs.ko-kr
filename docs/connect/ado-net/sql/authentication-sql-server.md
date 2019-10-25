---
title: SQL Server에서 인증
description: SQL Server의 로그인 및 인증에 대해 설명 하 고 추가 리소스에 대 한 링크를 제공 합니다.
ms.date: 09/26/2019
dev_langs:
- csharp
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: eb528eb1045788469b0eb31491fd654997831468
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452315"
---
# <a name="authentication-in-sql-server"></a>SQL Server에서 인증

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[ADO.NET 다운로드](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server에서는 Windows 인증 모드와 혼합 모드의 두 가지 인증 모드를 지원합니다.  
  
- Windows 인증은 기본 인증이며 흔히 통합 보안이라고 하는데, 그 이유는 이 SQL Server 보안 모델이 Windows와 긴밀하게 통합되기 때문입니다. 특정 Windows 사용자 및 그룹 계정은 SQL Server에 로그인 할 수 있습니다. 이미 인증 된 Windows 사용자는 추가 자격 증명을 제공할 필요가 없습니다.  
  
- 혼합 모드에서는 Windows 인증과 SQL Server 인증을 모두 지원하며 사용자 이름 및 암호 쌍이 SQL Server 내에서 유지 관리됩니다.  
  
> [!IMPORTANT]
> 가능 하면 Windows 인증을 사용 하는 것이 좋습니다. Windows 인증은 일련의 암호화된 메시지를 사용하여 SQL Server에서 사용자를 인증합니다. SQL Server 로그인을 사용하는 경우 SQL Server 로그인 이름과 암호화된 암호가 네트워크를 통해 전달되므로 Windows 인증에 비해 보안이 떨어집니다.  
  
Windows 인증을 사용하는 경우 사용자가 Windows에 이미 로그온되어 있으므로 SQL Server에 별도로 로그온할 필요가 없습니다. 다음 `SqlConnection.ConnectionString`은 사용자가 사용자 이름이나 암호를 제공할 필요가 없는 Windows 인증을 지정합니다.  
  
```csharp
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
> 로그인은 데이터베이스 사용자와 다릅니다. 로그인 또는 Windows 그룹을 데이터베이스 사용자 또는 역할에 별도의 작업으로 매핑해야 합니다. 그런 다음 데이터베이스 개체에 액세스할 수 있는 권한을 사용자 또는 역할에 부여 합니다.  
  
## <a name="authentication-scenarios"></a>인증 시나리오  
Windows 인증은 일반적으로 다음과 같은 경우에 가장 적합 합니다.  
  
- 도메인 컨트롤러가 있습니다.  
  
- 응용 프로그램과 데이터베이스가 같은 컴퓨터에 있는 경우  
  
- SQL Server Express 또는 LocalDB의 인스턴스를 사용하는 경우  
  
SQL Server 로그인은 다음과 같은 경우에 자주 사용 됩니다.  
  
- 작업 그룹이 있는 경우  
  
- 사용자는 서로 다른 트러스트 되지 않은 도메인에서 연결 합니다.  
  
- ASP.NET와 같은 인터넷 응용 프로그램  
  
> [!NOTE]
> Windows 인증을 지정하더라도 SQL Server 로그인이 비활성화되지는 않습니다. 따라서 높은 수준의 권한이 있는 SQL Server 로그인은 ALTER LOGIN DISABLE Transact-SQL 문을 사용하여 비활성화해야 합니다.  
  
## <a name="login-types"></a>로그인 유형  
SQL Server에서는 세 가지 유형의 로그인을 지원합니다.  
  
- 로컬 Windows 사용자 계정 또는 신뢰할 수 있는 도메인 계정입니다. SQL Server는 Windows를 통해 Windows 사용자 계정을 인증합니다.  
  
- Windows group. Windows 그룹에 대 한 액세스 권한을 부여 하면 해당 그룹의 멤버인 모든 Windows 사용자 로그인에 대 한 액세스 권한이 부여 됩니다.  
  
- SQL Server 로그인. SQL Server에서는 사용자 이름과 암호 해시를 모두 master 데이터베이스에 저장하고, 내부 인증 방법을 사용하여 로그인 시도가 유효한지 검사합니다.  
  
> [!NOTE]
> SQL Server에서는 코드 서명에만 사용되는 인증서 또는 비대칭 키에서 만들어진 로그인을 제공합니다. SQL Server에 연결할 때는 사용할 수 없습니다.  
  
## <a name="mixed-mode-authentication"></a>혼합 모드 인증  
불가피하게 혼합 모드 인증을 사용하는 경우 SQL Server 로그인을 만들어야 합니다. 이 로그인은 SQL Server에 저장됩니다. 그런 다음 런타임에 SQL Server 사용자 이름과 암호를 제공해야 합니다.  
  
> [!IMPORTANT]
> SQL Server `sa` ("시스템 관리자"의 약어) 라는 SQL Server 로그인을 사용 하 여 설치 됩니다. @No__t_0 로그인에 강력한 암호를 할당 하 고 응용 프로그램에서 `sa` 로그인을 사용 하지 않습니다. @No__t_0 로그인은 전체 서버에 대 한 관리 자격 증명이 해지 불가능 `sysadmin` 고정 서버 역할에 매핑됩니다. 공격자가 시스템 관리자 권한으로 액세스할 수 있는 경우에는 잠재적 손상에 제한이 없습니다. Windows `BUILTIN\Administrators` 그룹(로컬 관리자 그룹)의 모든 멤버는 기본적으로 `sysadmin` 역할의 멤버이지만 이 역할에서 멤버를 제거할 수 있습니다.  
  
> [!IMPORTANT]
> 사용자 입력에서 연결 문자열을 연결 하면 연결 문자열 삽입 공격에 취약 해질 수 있습니다. @No__t_0를 사용 하 여 런타임에 구문상 유효한 연결 문자열을 만들 수 있습니다. 
  
## <a name="external-resources"></a>외부 리소스  
자세한 내용은 다음 리소스를 참조하십시오.  
  
|리소스|설명|  
|--------------|-----------------|  
|[보안 주체](../../../relational-databases/security/authentication-access/principals-database-engine.md)|SQL Server의 로그인 및 기타 보안 주체에 대해 설명합니다.|  
  
## <a name="next-steps"></a>다음 단계
- [SQL Server의 애플리케이션 보안 시나리오](application-security-scenarios-sql-server.md)
