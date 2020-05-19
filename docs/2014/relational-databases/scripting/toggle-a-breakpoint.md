---
title: 중단점 설정/해제
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c477ab89-a1cd-4f2c-aa7c-40525041100f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5cf83aa10e758479d3bd7b2dff6a829515e8c39d
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718544"
---
# <a name="toggle-a-breakpoint"></a>중단점 설정/해제
  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 중단점을 설정하는 작업을 중단점 설정/해제라고 합니다.  
  
## <a name="breakpoints"></a>중단점  
 중단점이 설정되면 문 왼쪽에 있는 회색 막대에서 아이콘으로 표시됩니다. 이 아이콘을 중단점 문자 모양이라고 합니다. [!INCLUDE[tsql](../../includes/tsql-md.md)] 중단점은 완전한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에 적용됩니다. 중단점을 설정/해제하면 디버거는 관련 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 강조 표시합니다.  
  
 한 줄에 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문이 여러 개 있는 경우 각 문에 대해 중단점을 설정/해제할 수 있습니다. 창 왼쪽에 있는 회색 막대를 클릭하면 줄의 첫 번째 문에서 중단점이 설정/해제됩니다. 다음 문의 아무 부분이나 강조 표시하거나 커서를 다음 문으로 이동한 후 F9 키를 누르거나 **디버그** 메뉴에서 **중단점 설정/해제** 를 클릭하여 다음 문에서 중단점을 설정/해제할 수 있습니다. 한 줄에 중단점이 여러 개 있더라도 왼쪽의 회색 막대에는 중단점 문자 모양이 하나만 나타납니다.  
  
 중단점을 설정/해제한 후 중단점에 대한 다양한 동작(예: 중단점 속성 편집, 중단점 일시 해제)을 수행할 수 있습니다. 자세한 내용은 [Transact-SQL 중단점](transact-sql-breakpoints.md)을 참조하세요.  
  
## <a name="toggle-a-breakpoint"></a>중단점 설정/해제  
 **Transact-SQL 문에서 중단점을 설정/해제하려면**  
  
1.  [!INCLUDE[tsql](../../includes/tsql-md.md)] 문 왼쪽에 있는 회색 막대를 클릭합니다.  
  
2.  또는 문의 일부를 강조 표시하거나 커서를 문으로 이동한 후 다음 중 하나의 동작을 수행합니다.  
  
    -   F9 키를 누릅니다.  
  
    -   **디버그** 메뉴에서 **중단점 설정/해제**를 클릭합니다.  
  
  
