---
title: 구성 관리용 WMI 공급자 사용
description: 바인딩, 연결 문자열 지정 및 권한/서버 인증을 포함 하 여 구성 관리용 WMI 공급자에 대해 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: da0f68133473e746b7eaae898273b3c8a8bab0cd
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85880456"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>구성 관리용 WMI 공급자 작업

[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 문서에서는 컴퓨터 관리용 WMI 공급자를 사용 하 여 프로그래밍 하는 방법에 대 한 지침을 제공 합니다.

## <a name="binding"></a>바인딩  
 구성 관리용 WMI 공급자는 COM 개체 모델이며 초기 바인딩과 런타임에 바인딩을 지원합니다. 런타임에 바인딩의 경우 VBScript와 같은 스크립트 언어를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스, 네트워크 설정 및 별칭을 프로그래밍 방식으로 조작할 수 있습니다.  
  
## <a name="specifying-a-connection-string"></a>연결 문자열 지정

애플리케이션은 공급자가 정의한 WMI 네임스페이스에 연결하여 구성 관리용 WMI 공급자를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 보냅니다. Windows WMI 서비스는이 네임 스페이스를 공급자 DLL에 매핑하고 DLL을 메모리에 로드 합니다. 모든 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스는 단일 WMI 네임스페이스로 나타냅니다.

네임 스페이스의 기본값은 다음과 같습니다. 형식에서 `VV` 는 SQL Server의 주 버전 번호입니다. 는를 실행 하 여 검색할 수 `SELECT @@VERSION;` 있습니다.

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

PowerShell을 사용 하 여 연결 하는 경우 선행을 `\\.\` 제거 해야 합니다. 예를 들어 다음 PowerShell 코드는 주 버전 13 인 SQL Server 2016에 대 한 모든 WMI 클래스를 나열 합니다.

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

다음 PowerShell 코드를 사용 하 여 사용 가능한 모든 WMI ComputerManagement 네임 스페이스를 쿼리할 수 있습니다.

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **참고:** Windows 방화벽을 통해 연결 하는 경우에는 컴퓨터가 적절히 구성 되어 있는지 확인 해야 합니다. [!INCLUDE[msCoName](../../includes/msconame-md.md)]MSDN [웹 사이트](https://go.microsoft.com/fwlink/?linkid=15426)의 WMI(Windows Management Instrumentation) 설명서에서 "Windows 방화벽을 통해 연결" 문서를 참조 하세요.  
  
## <a name="permissions-and-server-authentication"></a>권한과 서버 인증  
 구성 관리용 WMI 공급자에 액세스하려면 클라이언트 WMI 관리 스크립트가 대상 컴퓨터에서 관리자 컨텍스트로 실행되고 있어야 합니다. 관리할 컴퓨터에서 로컬 Windows Administrators 그룹의 멤버여야 합니다.  
  
 관리자는 그룹 정책을 설정하여 WMI 공급자에 대한 사용자 액세스를 제어할 수 있습니다. 그룹 정책 설정에 대한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 구성 관리자 도움말의 "그룹 정책 및 MMC"를 참조하십시오.  
  
 WMI 관리 스크립트를 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정을 업데이트할 수 있습니다.  
  
 구성 관리용 WMI 공급자는 보안 인증서를 지원합니다. 인증서에 대 한 자세한 내용은 [암호화 계층](../../relational-databases/security/encryption/encryption-hierarchy.md)을 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 구성 관리자](../../relational-databases/sql-server-configuration-manager.md)  
  
  
