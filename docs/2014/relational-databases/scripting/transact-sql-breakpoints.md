---
title: Transact-SQL 중단점
ms.custom: seo-lt-2019
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Transact-SQL debugger, breakpoints
ms.assetid: c234430f-bd94-4d0d-9e74-2bf11681fa50
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 84ff925f2aa68ee81268eaca2faa3920f3ec407b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/01/2020
ms.locfileid: "82718533"
---
# <a name="transact-sql-breakpoints"></a>Transact-SQL 중단점
  중단점은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거가 특정 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문에서 실행을 일시 중지하도록 지정하여 사용자가 해당 지점에 있는 코드 요소의 상태를 확인할 수 있게 해 줍니다.  
  
## <a name="breakpoints"></a>중단점  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 디버거를 실행하는 경우 특정 문에 대해 중단점을 설정/해제할 수 있습니다. 실행 중에 중단점이 있는 문에 도달하면 디버거는 변수 및 매개 변수 값과 같은 디버깅 정보를 볼 수 있도록 실행을 일시 중지합니다.  
  
 중단점은 편집기 창에서 개별적으로 관리하거나 **중단점** 창을 사용하여 전체적으로 관리할 수 있습니다. 실행을 일시 중지할 특정 조건, 중단점이 실행되는 경우에 수행할 동작 등과 같은 항목을 지정하여 중단점을 편집할 수 있습니다.  
  
## <a name="breakpoint-tasks"></a>중단점 태스크  
  
|태스크 설명|항목|  
|----------------------|-----------|  
|디버거를 일시 중지할 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문을 지정하는 방법에 대해 설명합니다.|[중단점 설정/해제](../spatial/point.md)|  
|중단점을 일시적으로 비활성화하고 나중에 다시 활성화하는 방법에 대해 설명합니다. 또한 중단점을 삭제하는 방법에 대해 설명합니다.|[중단점 설정, 해제 및 삭제](enable-disable-and-delete-breakpoints.md)|  
|지정한 Transact-SQL 식의 평가 결과에 따라 중단점을 적용할지 여부를 정의하는 조건을 지정하는 방법에 대해 설명합니다.|[중단점 조건 지정](specify-a-breakpoint-condition.md)|  
|중단점을 포함하는 문이 지정한 횟수만큼 실행된 경우에만 중단점을 적용하도록 적중 횟수를 지정하는 방법에 대해 설명합니다.|[적중 횟수 지정](specify-a-hit-count.md)|  
|중단점이 지정된 프로세스 또는 스레드에서만 작동하도록 필터를 지정하는 방법에 대해 설명합니다.|[중단점 필터 지정](specify-a-breakpoint-filter.md)|  
|중단점 문이 실행될 때 수행되는 사용자 지정 작업인 **적중될 때** 동작을 지정하는 방법에 대해 설명합니다. 예에서는 메시지를 인쇄합니다.|[중단점 동작 지정](specify-a-breakpoint-action.md)|  
|중단점의 위치를 편집하는 방법에 대해 설명합니다.|[중단점 위치 편집](edit-a-breakpoint-location.md)|  
  
## <a name="see-also"></a>참고 항목  
 [Transact-SQL 디버거 정보](transact-sql-debugger-information.md)  
  
  
