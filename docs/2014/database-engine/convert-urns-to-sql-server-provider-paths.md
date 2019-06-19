---
title: URN을 SQL Server 공급자 경로로 변환 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 06e59cd00382610e330e2c288f44fda50244256f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065114"
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>URN을 SQL Server 공급자 경로로 변환
  SMO( [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object) 모델은 개체의 URN(Uniform Resource Names)을 작성합니다. 각 URN은 SMO 개체를 고유하게 식별하며 `Convert-UrnToPath` cmdlet을 사용하여 SQL Server PowerShell 공급자 경로로 변환될 수 있습니다.  
  
## <a name="converting-urns-to-paths"></a>URN을 경로로 변환  
 각 URN에는 개체에 대한 경로와 동일한 정보가 다른 형식으로 존재합니다. 예를 들어 테이블에 대한 경로는 다음과 같습니다.  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 동일한 개체에 대한 URN은 다음과 같습니다.  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 Windows PowerShell 스크립트로 SMO 개체를 만든 경우 `Urn` 속성을 참조하여 개체에 대한 URN을 가져온 다음 `Convert-UrnToPath` cmdlet을 사용하여 SMO URN 문자열을 Windows PowerShell 경로로 변환할 수 있습니다. 그런 다음 공급자를 사용하여 경로의 다른 위치를 탐색할 수 있습니다.  
  
 노드 이름에 Windows PowerShell 경로 이름에서 지원되지 않는 확장 문자가 포함된 경우 `Convert-UrnToPath`는 이러한 문자를 해당 16진수 표현으로 인코딩합니다. 예를 들어 "My:Table"은 "My%3ATable"로 반환됩니다.  
  
 cmdlet 사용 예를 보려면 Windows PowerShell에서 다음을 실행하십시오.  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>관련 항목  
 [쿼리 식 및 URN](../powershell/query-expressions-and-uniform-resource-names.md)   
 [SQL Server PowerShell 공급자](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
