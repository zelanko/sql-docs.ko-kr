---
title: SQL Server Management Studio에서 Windows PowerShell 실행 | Microsoft 문서
description: 사용자가 선택한 개체의 위치로 미리 설정된 경로를 사용하여 SQL Server Management Studio 개체 탐색기에서 Windows PowerShell 세션을 시작하는 방법을 알아봅니다.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 1f841825-da1f-4062-9a81-3cdbab03845b
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 03/14/2017
ms.openlocfilehash: c074b0f0ed5f5b041a8a4c4ed341837fec2b1926
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006172"
---
# <a name="run-windows-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio에서 Windows PowerShell 실행

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

**의** 개체 탐색기 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]에서 Windows PowerShell 세션을 시작할 수 있습니다. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 Windows PowerShell을 시작하고, **SqlServer** 모듈을 로드한 다음 경로 컨텍스트를 **개체 탐색기** 트리의 연결된 노드로 설정합니다.  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

**개체 탐색기**에서 개체에 대해 PowerShell을 실행하도록 지정하면 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] 에서 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell 스냅인이 로드 및 등록된 Windows PowerShell 세션을 시작합니다. 세션 경로는 사용자가 개체 탐색기에서 마우스 오른쪽 단추로 클릭한 개체의 위치로 미리 설정됩니다. 예를 들어 개체 탐색기에서 [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] 데이터베이스 개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택하면 Windows PowerShell 경로가 다음과 같이 설정됩니다.  

```powershell
SQLSERVER:\SQL\MyComputer\MyInstance\Databases\AdventureWorks2012>  
```

## <a name="run-powershell"></a>PowerShell 실행

### <a name="to-run-powershell-from-sql-server-management-studio"></a>SQL Server Management Studio에서 PowerShell을 실행하려면

1. **개체 탐색기**를 엽니다.

2. 작업할 개체에 대한 노드로 이동합니다.

3. 개체를 마우스 오른쪽 단추로 클릭하고 **PowerShell 시작**을 선택합니다.

## <a name="permissions"></a>사용 권한

PowerShell을 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)]에서 열 경우 관리자 권한으로 실행되지 않아 WMI에 대한 호출 등 일부 작업을 수행하지 못할 수 있습니다.  
  
## <a name="see-also"></a>참고 항목

- [SQL Server PowerShell](sql-server-powershell.md)