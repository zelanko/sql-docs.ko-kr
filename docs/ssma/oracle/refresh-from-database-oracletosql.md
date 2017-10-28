---
title: "(OracleToSQL) 데이터베이스에서 새로 고침 | Microsoft Docs"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 536fa920910c56698be8b161f59294f555747917
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="refresh-from-database-oracletosql"></a>(OracleToSQL) 데이터베이스에서 새로 고침
**데이터베이스에서 새로 고침** 대화 상자를 사용 하면 Oracle 데이터베이스에서 새로 고칠 개체를 선택할 수 있습니다. 대화 상자에 있는 행은 코딩 된 색 메타 데이터의 상태에 따라:  
  
-   개체 메타 데이터에 로컬 및 Oracle 데이터베이스에서 변경 된 경우 행은 파란색입니다.  
  
-   SSMA 아니라 Oracle 데이터베이스에 있는 개체 메타 데이터가 변경 된 경우 노란색입니다.  
  
-   개체 메타 데이터를 로컬로 변경 되었지만 Oracle 데이터베이스에는 없는 행은 녹색입니다.  
  
-   Oracle 데이터베이스에서 새 개체가 있으면 해당 행은 분홍색.  
  
기본 개체 새로 고침 설정을 지정할 수는 **프로젝트 설정** 대화 상자. 자세한 내용은 참조 [프로젝트 설정 &#40; 동기화 &#41; &#40; OracleToSQL &#41; ](../../ssma/oracle/project-settings-synchronization-oracletosql.md).  
  
액세스는 **데이터베이스에서 새로 고침** 대화 상자에서 마우스 오른쪽 단추로 클릭 하 고 Oracle 메타 데이터 탐색기에서 개체 **데이터베이스에서 새로 고침**합니다.  
  
## <a name="options"></a>옵션  
**축소 (-)**  
개별 개체를 숨기려면 모든 개체 그룹을 축소 합니다.  
  
**확장 (+)**  
개별 개체를 표시 하는 모든 개체 그룹을 확장 합니다.  
  
**같은 개체를 표시/숨기기**  
개체 메타 데이터 및 SSMA는 Oracle 데이터베이스에서 동일 경우 목록에서 개체를 숨깁니다.  
  
**(화살표 단추) 데이터베이스에서 새로 고침**  
화살표 단추를 사용 하 여 SSMA에서 선택한 개체에 대 한 메타 데이터를 업데이트 해야 함을 지정 합니다.  
  
**데이터베이스에서 새로 고치지 않습니다 (X 단추)**  
X 단추를 사용 하 여 지정 SSMA에서 선택한 개체에 대 한 메타 데이터를 업데이트 되지 않아야 합니다.  
  
**범례**  
표시는 **범례** 대화 상자. 범례는 색 행 및 메타 데이터 상태 간의 매핑을 포함합니다.  
  
유지 하는 **범례** 대화 상자 맨 위에 **데이터베이스에서 새로 고침** 대화 상자는 **맨 위에 표시** 확인란 합니다.  
  

