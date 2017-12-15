---
title: "데이터베이스 엔진 cmdlet 사용 | Microsoft 문서"
ms.custom: 
ms.date: 08/04/2016
ms.prod: sql-non-specified
ms.prod_service: ssms
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Cmdlets [SQL Server], Encode-Sqlname
- Encode-Sqlname cmdlet
- PowerShell [SQL Server], Encode-Sqlname
- Convert-UrnToPath cmdlet
- PowerShell [SQL Server], cmdlets
- Cmdlets [SQL Server]
- PowerShell [SQL Server], Convert-UrnToPath
- Cmdlets [SQL Server], Convert-UrnToPath
- Decode-Sqlname cmdlet
- PowerShell [SQL Server], Decode-Sqlname
- Cmdlets [SQL Server], Decode-Sqlname
ms.assetid: 720aa982-09ae-41a3-b603-a91004cfbe3e
caps.latest.revision: "25"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: b3833567185c16097983cfce99fca2e33d61d88e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="use-the-database-engine-cmdlets"></a>데이터베이스 엔진 cmdlet 사용
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Windows PowerShell cmdlet은 **Get-Help** 또는 **Set-MachineName**과 같이 일반적으로 동사-명사 명명 규칙을 사용하는 단일 함수 명령입니다. Windows PowerShell의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 공급자는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]관련 cmdlet을 제공합니다.  
  
## <a name="database-engine-cmdlets"></a>데이터베이스 엔진 cmdlet  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 은 적은 수의 [!INCLUDE[ssDE](../../includes/ssde-md.md)]cmdlet을 구현합니다. 이러한 cmdlet은 새 PowerShell 스크립트에서 기존 Transact-SQL 스크립트를 실행하고 정책 기반 관리 정책을 평가하며 SQL Server 공급자 경로에서 SQL Server 식별자 지정을 지원하는 데 주로 사용됩니다.  
  
 대부분의 Windows PowerShell 스크립트는 SQL Server PowerShell 공급자 및 SQL Server 관리 효율성 개체 모델을 사용하여 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 에서 작동합니다. 자세한 내용은 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)을(를) 참조하세요.  
  
### <a name="get-cmdlet-help"></a>Cmdlet 도움말 보기  
 Windows PowerShell 환경에서 **Get-Help** cmdlet은 각 cmdlet에 대한 도움말 정보를 제공합니다. **Get-Help** 는 구문, 매개 변수 정의, 입력 및 출력 유형, cmdlet에서 수행하는 동작에 대한 설명과 같은 정보를 반환합니다. 자세한 내용은 [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md)을 참조하세요.  
  
### <a name="partial-parameter-names"></a>부분 매개 변수 이름  
 cmdlet 매개 변수의 전체 이름을 지정할 필요는 없습니다. cmdlet에서 지원하는 다른 매개 변수와 고유하게 구분될 수 있도록 이름을 지정하기만 하면 됩니다. 예를 들어 이 예에서는 **Invoke-Sqlcmd -QueryTimeout** 매개 변수를 지정하는 3가지 방법을 보여 줍니다.  
  
```  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTimeout 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryTime 3  
Invoke-Sqlcmd -Query "SELECT @@VERSION;" -QueryT 3  
```  
  
## <a name="database-engine-cmdlet-tasks"></a>데이터베이스 엔진 cmdlet 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|**Invoke-Sqlcmd** 를 사용하여 **또는 XQuery 문이 포함된** sqlcmd [!INCLUDE[tsql](../../includes/tsql-md.md)] 스크립트 또는 명령을 실행하는 방법을 설명합니다. **sqlcmd** 입력을 문자열 입력 매개 변수 또는 열려는 스크립트 파일의 이름으로 사용할 수 있습니다.|[Invoke-Sqlcmd cmdlet](../../powershell/invoke-sqlcmd-cmdlet.md)|  
|**Invoke-PolicyEvaluation** 을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 개체의 대상 집합이 정책 기반 관리 정책에 정의된 조건을 준수하는지 여부를 보고하는 방법을 설명합니다. 필요에 따라 cmdlet을 사용하여 정책 조건을 준수하지 않는 대상 개체의 설정할 수 있는 옵션을 다시 구성할 수 있습니다.|[Invoke-PolicyEvaluation cmdlet](../../powershell/invoke-policyevaluation-cmdlet.md)|  
|**Encode-Sqlname** 및 **Decode-Sqlname** 을 사용하여 Windows PowerShell 경로에서 지원되지 않는 문자가 포함된 SQL Server 식별자를 처리하는 방법을 설명합니다.|[SQL Server 식별자 인코딩 및 디코딩](../../relational-databases/scripting/encode-and-decode-sql-server-identifiers.md)|  
|**Convert-UrnToPath** 를 사용하여 SQL Server 관리 효율성 개체 URN(Uniform Resource Name)을 해당 SQL Server 공급자 경로로 변환하는 방법을 설명합니다.|[URN을 SQL Server 공급자 경로로 변환](../../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)|  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell 공급자](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
[Always On 가용성 그룹에 대한 PowerShell Cmdlet 개요(SQL Server)](../../database-engine/availability-groups/windows/overview-of-powershell-cmdlets-for-always-on-availability-groups-sql-server.md)
  
  
