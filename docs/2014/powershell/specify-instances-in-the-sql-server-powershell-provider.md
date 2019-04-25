---
title: SQL Server PowerShell 공급자에 인스턴스 지정 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 9373de68-fd43-45f2-b9a6-149c96610aeb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 595bd70b97b6586071177e2e93281e14ca62c32c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62762352"
---
# <a name="specify-instances-in-the-sql-server-powershell-provider"></a>SQL Server PowerShell 공급자에 인스턴스 지정
  SQL Server PowerShell 공급자에 대해 지정되는 경로는 [!INCLUDE[ssDE](../includes/ssde-md.md)] 의 인스턴스와 해당 인스턴스가 실행 중인 컴퓨터를 식별해야 합니다. 컴퓨터와 인스턴스를 지정하는 구문은 SQL Server 식별자 규칙과 Windows PowerShell 경로 규칙을 모두 준수해야 합니다.  
  
1.  **시작하기 전 주의 사항:**  [제한 사항](#LimitationsRestrictions)  
  
2.  **인스턴스를 지정 합니다.**  [예](#Examples)  
  
## <a name="before-you-begin"></a>시작하기 전 주의 사항  
 SQL Server 공급자 경로에서 SQLSERVER:\SQL 다음에 오는 첫 번째 노드는 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스를 실행하는 컴퓨터 이름입니다. 예를 들면 다음과 같습니다.  
  
```  
SQLSERVER:\SQL\MyComputer  
```  
  
 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스와 동일한 컴퓨터에 Windows PowerShell을 실행하는 경우 컴퓨터 이름 대신 localhost 또는 (local)을 사용할 수 있습니다. localhost 또는 (로컬)을 사용하는 스크립트는 다른 컴퓨터 이름을 반영하도록 변경하지 않고도 모든 컴퓨터에서 실행할 수 있습니다.  
  
 [!INCLUDE[ssDE](../includes/ssde-md.md)] 실행 프로그램의 여러 인스턴스를 동일한 컴퓨터에서 실행할 수 있습니다. SQL Server 공급자 경로에서 컴퓨터 이름 다음에 오는 노드는 인스턴스를 식별합니다. 예를 들면 다음과 같습니다.  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance  
```  
  
 각 컴퓨터는 기본 [!INCLUDE[ssDE](../includes/ssde-md.md)]인스턴스를 한 개 가질 수 있습니다. 기본 인스턴스는 설치할 때 이름을 지정하지 마세요. 연결 문자열에 컴퓨터 이름만 지정하면 해당 컴퓨터의 기본 인스턴스로 연결됩니다. 컴퓨터의 다른 모든 인스턴스는 명명된 인스턴스여야 합니다. 인스턴스 이름은 설치 시 지정하고, 연결 문자열에는 컴퓨터 이름과 인스턴스 이름을 모두 지정해야 합니다.  
  
###  <a name="LimitationsRestrictions"></a> 제한 사항  
 PowerShell 스크립트에서 마침표(.)를 사용하여 로컬 컴퓨터를 지정할 수 없습니다. 마침표는 PowerShell에서 명령으로 해석되기 때문에 지원되지 않습니다.  
  
 (local)의 괄호 문자는 일반적으로 Windows PowerShell에서 명령으로 처리됩니다. 따라서 경로에 사용할 수 있도록 괄호 문자를 인코딩 또는 이스케이프하거나, 경로를 큰따옴표로 묶어야 합니다. 자세한 내용은 SQL Server 식별자 인코딩 및 디코딩을 참조하세요.  
  
 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 공급자는 항상 인스턴스 이름을 지정하도록 요청합니다. 기본 인스턴스의 인스턴스 이름은 DEFAULT로 지정해야 합니다.  
  
##  <a name="Examples"></a> 예: 컴퓨터 및 인스턴스 이름  
 이 예에서는 localhost 및 DEFAULT를 사용하여 로컬 컴퓨터의 기본 인스턴스를 지정합니다.  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT   
```  
  
 (local)의 괄호 문자는 일반적으로 Windows PowerShell에서 명령으로 처리됩니다. 다음 중 하나를 수행해야 합니다.  
  
-   경로 문자열을 따옴표로 묶습니다.  
  
    ```  
    Set-Location "SQLSERVER:\SQL\(local)\DEFAULT"  
    ```  
  
-   역따옴표 문자(`)를 사용하여 괄호를 이스케이프 처리합니다.  
  
    ```  
    Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
    ```  
  
-   16진수 표현을 사용하여 괄호를 인코딩합니다.  
  
    ```  
    Set-Location SQLSERVER:\SQL\%28local%29\DEFAULT  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [PowerShell의 SQL Server 식별자](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell 공급자](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
