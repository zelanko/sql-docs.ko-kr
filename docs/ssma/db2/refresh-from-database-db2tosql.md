---
title: "(DB2ToSQL) 데이터베이스에서 새로 고침 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 613a8368-b372-443f-8252-fb6dc31a003d
caps.latest.revision: "5"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8fa3c91de2468da1ba9a7d67f597a2eae716632c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="refresh-from-database-db2tosql"></a>(DB2ToSQL) 데이터베이스에서 새로 고침
**데이터베이스에서 새로 고침** 대화 상자에서는 DB2 데이터베이스에서 새로 고칠 개체를 선택할 수 있습니다. 대화 상자에 있는 행은 코딩 된 색 메타 데이터의 상태에 따라:  
  
-   개체 메타 데이터에 로컬 및 DB2 데이터베이스에서 변경 된 경우 행은 파란색입니다.  
  
-   SSMA 아니라 DB2 데이터베이스에 있는 개체 메타 데이터가 변경 된 경우 노란색입니다.  
  
-   개체 메타 데이터를 로컬로 변경 되었지만 DB2 데이터베이스에는 없는 행은 녹색입니다.  
  
-   DB2 데이터베이스에서 새 개체가 있으면 해당 행은 분홍색.  
  
기본 개체 새로 고침 설정을 지정할 수는 **프로젝트 설정** 대화 상자. 자세한 내용은 참조 [프로젝트 설정 &#40; 동기화 &#41; &#40; DB2ToSQL &#41; ](../../ssma/db2/project-settings-synchronization-db2tosql.md).  
  
액세스는 **데이터베이스에서 새로 고침** 대화 상자에서 마우스 오른쪽 단추로 클릭 하 고 DB2 메타 데이터 탐색기에서 개체 **데이터베이스에서 새로 고침**합니다.  
  
## <a name="options"></a>옵션  
**축소 (-)**  
개별 개체를 숨기려면 모든 개체 그룹을 축소 합니다.  
  
**확장 (+)**  
개별 개체를 표시 하는 모든 개체 그룹을 확장 합니다.  
  
**같은 개체를 표시/숨기기**  
개체 메타 데이터는 SSMA 및 DB2 데이터베이스에서 동일 하는 경우 목록에서 개체를 숨깁니다.  
  
**(화살표 단추) 데이터베이스에서 새로 고침**  
화살표 단추를 사용 하 여 SSMA에서 선택한 개체에 대 한 메타 데이터를 업데이트 해야 함을 지정 합니다.  
  
**데이터베이스에서 새로 고치지 않습니다 (X 단추)**  
X 단추를 사용 하 여 지정 SSMA에서 선택한 개체에 대 한 메타 데이터를 업데이트 되지 않아야 합니다.  
  
**범례**  
표시는 **범례** 대화 상자. 범례는 색 행 및 메타 데이터 상태 간의 매핑을 포함합니다.  
  
유지 하는 **범례** 대화 상자 맨 위에 **데이터베이스에서 새로 고침** 대화 상자는 **맨 위에 표시** 확인란 합니다.  
  
