---
title: Management Studio에서 속성 창 사용
description: 속성 창을 사용하여 연결과 같은 SQL Server Management Studio 항목에 대한 정보와 데이터베이스 개체에 대한 정보를 보는 방법을 알아봅니다.
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.prod: sql
ms.technology: ssms
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- viewing properties
- Properties window [SQL Server Management Studio]
- complex properties [SQL Server Management Studio]
ms.assetid: 903d4aca-f57c-43d9-a893-702eceaa7004
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9f18cec0f6ac8754fc5826e75325c810e965b692
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97480584"
---
# <a name="use-the-properties-window-in-management-studio"></a>Management Studio에서 속성 창 사용
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  속성 창은 연결 또는 실행 계획 연산자와 같은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]의 항목의 상태와 테이블, 뷰, 디자이너 등과 같은 데이터베이스 개체에 대한 정보를 설명합니다.  
  
 속성 창을 사용하여 현재 연결의 속성을 볼 수 있습니다. 대부분의 속성은 속성 창에서 읽기 전용이지만 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]의 다른 위치에서 변경할 수 있습니다. 예를 들어 쿼리의 데이터베이스 속성은 속성 창에서 읽기 전용이지만 도구 모음에서 변경할 수 있습니다.  
  
### <a name="to-view-properties-using-the-properties-window"></a>속성 창을 사용하여 속성을 보려면  
  
1.  속성 창이 표시되지 않은 경우 **보기** 메뉴에서 **속성 창** 을 클릭하거나 F4 키를 누릅니다.  
  
2.  보려는 개체에 포커스를 설정합니다.  
  
3.  속성 창에서 특정 속성을 찾습니다.  
  
### <a name="to-view-connection-properties-of-a-query-window"></a>쿼리 창의 연결 속성을 보려면  
  
1.  속성 창이 표시되지 않은 경우 **보기** 메뉴에서 **속성 창** 을 클릭하거나 F4 키를 누릅니다.  
  
2.  속성 창에서 모든 연결 속성을 볼 수 있습니다.  
  
### <a name="to-view-the-properties-of-a-showplan-operator"></a>실행 계획 연산자의 속성을 보려면  
  
1.  **쿼리** 메뉴에서 **실제 실행 계획 포함** 을 클릭합니다.  
  
2.  SQL 쿼리 편집기에서 쿼리를 입력 및 실행합니다.  
  
3.  속성 창이 표시되지 않은 경우 **보기** 메뉴에서 **속성 창** 을 클릭하거나 F4 키를 누릅니다.  
  
4.  SQL 쿼리 편집기의 **실행 계획** 탭에서 연산자의 아이콘을 클릭하여 속성 창에서 연산자에 대한 정보를 확인합니다.  
  
## <a name="see-also"></a>참고 항목  
 [속성 창&#40;Management Studio&#41;](../properties-window-management-studio.md)  
  
