---
title: 중단점 설정/해제
description: '중단점을 설정/해제하여 연결된 Transact-SQL 문을 강조 표시하는 방법과 문에 다양한 작업(예: 편집)을 수행하는 방법을 알아봅니다.'
titleSuffix: T-SQL debugger
ms.prod: sql
ms.technology: ssms
ms.topic: conceptual
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f9b9ddfd58beed00a00c3512b5db51e7a3a7907c
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036219"
---
# <a name="toggle-a-breakpoint"></a>중단점 설정/해제

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 중단점을 설정하는 작업을 중단점 설정/해제라고 합니다.  

[!INCLUDE[ssms-old-versions](../../includes/ssms-old-versions.md)]

## <a name="breakpoints"></a>중단점

중단점이 설정되면 문 왼쪽에 있는 회색 막대에서 아이콘으로 표시됩니다. 이 아이콘을 중단점 문자 모양이라고 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 중단점은 완전한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 적용됩니다. 중단점을 설정/해제하면 디버거는 관련 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 강조 표시합니다.  
  
 한 줄에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 여러 개 있는 경우 각 문에 대해 중단점을 설정/해제할 수 있습니다. 창 왼쪽에 있는 회색 막대를 클릭하면 줄의 첫 번째 문에서 중단점이 설정/해제됩니다. 다음 문의 아무 부분이나 강조 표시하거나 커서를 다음 문으로 이동한 후 F9 키를 누르거나 **디버그** 메뉴에서 **중단점 설정/해제** 를 클릭하여 다음 문에서 중단점을 설정/해제할 수 있습니다. 한 줄에 중단점이 여러 개 있더라도 왼쪽의 회색 막대에는 중단점 문자 모양이 하나만 나타납니다.  
  
 중단점을 설정/해제한 후 중단점에 대한 다양한 동작(예: 중단점 속성 편집, 중단점 일시 해제)을 수행할 수 있습니다. 자세한 내용은 [Transact-SQL 중단점](./transact-sql-breakpoints.md)을 참조하세요.  
  
## <a name="toggle-a-breakpoint"></a>중단점 설정/해제  
 **Transact-SQL 문에서 중단점을 설정/해제하려면**  
  
1.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 왼쪽에 있는 회색 막대를 클릭합니다.  
  
2.  또는 문의 일부를 강조 표시하거나 커서를 문으로 이동한 후 다음 중 하나의 동작을 수행합니다.  
  
    -   F9 키를 누릅니다.  
  
    -   **디버그** 메뉴에서 **중단점 설정/해제**를 클릭합니다.  
  
