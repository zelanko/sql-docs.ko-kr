---
title: SQL Server 식별자 이스케이프
description: SQL Server 구분 식별자에 나타날 수 있는 일부 문자는 Windows PowerShell 경로에서 지원되지 않습니다. 이 가운데 일부를 역따옴표 문자(`)로 이스케이프 처리하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 4ad4bdc7720d0c405e3982b6b4533b55c2756490
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005500"
---
# <a name="escape-sql-server-identifiers"></a>SQL Server 식별자 이스케이프

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

역따옴표 이스케이프 문자(`)를 사용하여 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 구분 식별자에는 허용되고 Windows PowerShell 경로 이름에는 허용되지 않는 문자를 이스케이프 처리할 수도 있습니다. 하지만 이스케이프 처리되지 않는 문자도 있습니다. 예를 들어 콜론 문자(:)는 Windows PowerShell에서 이스케이프 처리할 수 없습니다. 해당 문자가 포함된 식별자는 인코딩해야 합니다. 인코딩은 모든 문자에 대해 작동하므로 이스케이프 처리보다 안정적입니다.  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

역따옴표 문자(`) 키는 일반적으로 키보드 왼쪽 위에서 ESC 키 아래에 있습니다.  

## <a name="examples"></a>예제

다음은 # 문자를 이스케이프 처리하는 예입니다.  

```powershell
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```

다음은 (local)을 컴퓨터 이름으로 지정하는 경우 괄호를 이스케이프 처리하는 예입니다.  

```powershell
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```

## <a name="see-also"></a>참고 항목

- [PowerShell의 SQL Server 식별자](sql-server-identifiers-in-powershell.md)
- [SQL Server PowerShell 공급자](sql-server-powershell-provider.md)
- [SQL Server PowerShell](sql-server-powershell.md)