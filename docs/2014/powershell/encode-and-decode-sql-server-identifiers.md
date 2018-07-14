---
title: SQL Server 식별자 인코딩 및 디코딩 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0c2a997ec2df79b600b73be0bd5a33f7144fe119
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195363"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>SQL Server 식별자 인코딩 및 디코딩
  SQL Server 구분 식별자에 Windows PowerShell 경로 이름에서 지원되지 않는 문자가 사용되는 경우가 있습니다. 이러한 문자는 16진수 값을 인코딩하여 지정할 수 있습니다.  
  
1.  **시작하기 전에:**  [제한 사항](#LimitationsRestrictions)  
  
2.  **특수 문자를 처리하려면:**  [식별자 인코딩](#EncodeIdent), [식별자 디코딩](#DecodeIdent)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 Windows PowerShell 경로 이름에 지원되지 않는 문자는 "%" 문자 뒤에 해당 문자를 나타내는 비트 패턴의 16진수 값(예: "**%** xx")을 사용하여 표현하거나 인코딩할 수 있습니다. 인코딩은 Windows PowerShell 경로에 지원되지 않는 모든 문자를 처리하는 데 사용할 수 있습니다.  
  
 **Encode-SqlName** cmdlet은 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자를 입력으로 사용합니다. Windows PowerShell 언어에서 지원하지 않는 모든 문자를 "%xx"로 인코딩하여 문자열을 출력합니다. **Decode-SqlName** cmdlet은 인코딩된 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 식별자를 입력으로 사용하고 원래 식별자를 반환합니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 합니다 `Encode-Sqlname` 및 `Decode-Sqlname` cmdlet만 인코딩 또는 디코딩 문자는 SQL Server 구분 식별자에서 허용 되지만 PowerShell 경로에서 지원 되지 않습니다. **Encode-SqlName** 으로 인코딩되고 **Decode-SqlName**으로 디코딩된 문자입니다.  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**문자**|\|/|으로 디코딩된 문자입니다.|%|\<|>|*|?|[|]|&#124;|  
|**16진수 인코딩**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> 식별자 인코딩  
 **PowerShell 경로에서 SQL Server 식별자를 인코딩하려면**  
  
-   두 방법 중 하나를 사용하여 SQL Server 식별자를 인코딩합니다.  
  
    -   %XX 구문을 사용하여 지원되지 않는 문자에 대한 16진수 코드를 지정합니다. 여기서 XX는 16진수 코드입니다.  
  
    -   따옴표로 묶인 식별자를 `Encode-Sqlname` cmdlet에 전달  
  
### <a name="examples-encoding"></a>예(인코딩)  
 이 예에서는 ":" 문자의 인코딩된 버전(%3A)을 지정합니다.  
  
```  
Set-Location Table%3ATest  
```  
  
 또는 **Encode-SqlName** 을 사용하여 Windows PowerShell에서 지원되는 이름을 작성할 수 있습니다.  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> 식별자 디코딩  
 **PowerShell 경로에서 SQL Server 식별자를 디코딩하려면**  
  
 사용 된 `Decode-Sqlname` cmdlet을 16 진수 인코딩을 인코딩에 의해 표시 되는 문자로 바꿉니다.  
  
### <a name="examples-decoding"></a>예(디코딩)  
 이 예에서는 “Table:Test”를 반환합니다.  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>관련 항목  
 [PowerShell의 SQL Server 식별자](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
