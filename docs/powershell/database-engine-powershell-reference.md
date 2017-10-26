---
title: "데이터베이스 엔진 PowerShell 참조 | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3c379a43-c497-47dd-8e7d-2b015c068bb7
caps.latest.revision: 8
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: dc3df1d697b05201ac48520c1e344c28648cdfaf
ms.contentlocale: ko-kr
ms.lasthandoff: 06/22/2017

---
# <a name="database-engine-powershell-reference"></a>데이터베이스 엔진 PowerShell 참조
  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 에는 [!INCLUDE[ssDE](../includes/ssde-md.md)]에서 일반적인 작업을 수행하는 데 사용할 수 있는 여러 가지 Windows PowerShell cmdlet이 포함되어 있습니다. 또한 쿼리 식과 URN(Uniform Resource Name)을 SQL Server PowerShell 경로로 변경하거나 [!INCLUDE[ssDE](../includes/ssde-md.md)]에서 하나 이상의 개체를 지정하는 데 사용할 수 있습니다.  
  
## <a name="database-engine-cmdlets"></a>데이터베이스 엔진 cmdlet  
 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 에 있는 [!INCLUDE[ssDE](../includes/ssde-md.md)]용 cmdlet은 상대적으로 적습니다. [!INCLUDE[ssDE](../includes/ssde-md.md)] 에서 사용할 수 있는 대부분의 PowerShell 스크립트는 SQL Server PowerShell 공급자 및 관리 효율성 개체 모델을 사용합니다. 자세한 내용은 [SQL Server PowerShell Provider](../relational-databases/scripting/sql-server-powershell-provider.md)을(를) 참조하세요.  
  
 Windows PowerShell 환경의 SQL Server cmdlet에 대한 도움말을 보는 방법은 [Get Help SQL Server PowerShell](../relational-databases/scripting/get-help-sql-server-powershell.md)를 참조하십시오.  
  
### <a name="in-this-section"></a>섹션 내용  
 이 섹션에는 이러한 cmdlet에 대한 정보가 들어 있습니다.  
  
|설명|Cmdlet|  
|-----------------|------------|  
|**sqlcmd** 유틸리티를 사용하여 실행할 수 있는 Transact-SQL 스크립트 및 XQuery 스크립트를 실행합니다.|[Invoke-Sqlcmd cmdlet](../powershell/invoke-sqlcmd-cmdlet.md)|  
|데이터베이스 엔진 개체가 정책 기반 관리 정책을 준수하는지 여부를 평가합니다.|[Invoke-PolicyEvaluation cmdlet](../powershell/invoke-policyevaluation-cmdlet.md)|  
  
### <a name="information-about-other-cmdlets"></a>다른 cmdlet에 대한 정보  
 **Encode-Sqlname** 및 **Decode-Sqlname** cmdlet을 사용하면 PowerShell 경로에서 지원되지 않는 문자가 포함된 SQL Server 식별자를 지정할 수 있습니다. 자세한 내용은 [SQL Server Identifiers in PowerShell](../relational-databases/scripting/sql-server-identifiers-in-powershell.md)을(를) 참조하세요.  
  
 **Convert-UrnToPath** cmdlet을 사용하면 [!INCLUDE[ssDE](../includes/ssde-md.md)] 개체의 URN을 SQL Server PowerShell 공급자의 경로로 변환할 수 있습니다. 자세한 내용은 [Convert URNs to SQL Server Provider Paths](../relational-databases/scripting/convert-urns-to-sql-server-provider-paths.md)을(를) 참조하세요.  
  
## <a name="query-expressions-and-unique-resource-names"></a>쿼리 식 및 Unique Resource Names  
 쿼리 식은 개체 모델 계층 구조에 있는 하나 이상의 개체를 열거하는 조건 집합을 지정하기 위해 XPath와 유사한 구문을 사용하는 문자열입니다. URN(Unique Resource Name)은 단일 개체를 고유하게 식별하는 특정 유형의 쿼리 식 문자열입니다. 자세한 내용은 [Query Expressions and Uniform Resource Names](../powershell/query-expressions-and-uniform-resource-names.md)을(를) 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server PowerShell](../relational-databases/scripting/sql-server-powershell.md)  
  
  

