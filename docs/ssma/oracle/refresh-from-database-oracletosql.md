---
title: 데이터베이스 (OracleToSQL)에서 새로 고침 | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 84492f44-c368-4c75-954d-7307a2d2bbc0
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: decc6e25cc8480dfaf041a79baa0972bdd78e569
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62625863"
---
# <a name="refresh-from-database-oracletosql"></a>데이터베이스에서 새로 고침(OracleToSQL)
합니다 **데이터베이스에서 새로 고침** 대화 상자를 사용 하면 Oracle 데이터베이스에서 새로 고칠 개체를 선택 합니다. 대화 상자에서 행은 색으로 구분 된 메타 데이터의 상태를 기반으로 합니다.  
  
-   개체 메타 데이터를 로컬 및 Oracle 데이터베이스에서 변경 된 경우 행은 파란색입니다.  
  
-   SSMA 아니라 Oracle 데이터베이스에서 개체 메타 데이터를 변경 하는 경우 노란색입니다.  
  
-   개체 메타 데이터를 로컬에서 변경 된 경우 Oracle 데이터베이스에는 없는 행은 녹색입니다.  
  
-   Oracle 데이터베이스에서 새 개체가 있으면 분홍색입니다.  
  
기본 개체 새로 고침 설정을 지정할 수 있습니다 합니다 **프로젝트 설정** 대화 상자. 자세한 내용은 [프로젝트 설정&#40;동기화&#41; &#40;OracleToSQL&#41;](../../ssma/oracle/project-settings-synchronization-oracletosql.md)합니다.  
  
액세스 하는 **데이터베이스에서 새로 고침** 대화 상자에서 마우스 오른쪽 단추로 클릭 하 고 Oracle 메타 데이터 탐색기에서 개체 **데이터베이스에서 새로 고침**합니다.  
  
## <a name="options"></a>변수  
**축소 (-)**  
개별 개체를 숨기려면 모든 개체 그룹을 축소 합니다.  
  
**확장 (+)**  
개별 개체를 표시 하는 모든 개체 그룹을 확장 합니다.  
  
**동일한 개체를 표시/숨기기**  
SSMA는 Oracle 데이터베이스에 동일한 개체 메타 데이터를 목록에서 개체를 숨깁니다.  
  
**데이터베이스 (화살표 단추)에서 새로 고침**  
SSMA에서 선택한 개체에 대 한 메타 데이터를 업데이트 해야를 지정 하려면 화살표 단추를 사용 합니다.  
  
**데이터베이스에서 새로 고쳐지지 않습니다 (X 단추)**  
SSMA에서 선택한 개체에 대 한 메타 데이터를 업데이트 되지 않아야 지정 하려면 X 단추를 사용 합니다.  
  
**범례**  
표시 된 **범례** 대화 상자. 범례 행 색 및 메타 데이터 상태 간의 매핑을 포함합니다.  
  
유지 하는 **범례** 대화 상자 위쪽에 **데이터베이스에서 새로 고침** 대화 상자에서를 **맨 위에 표시** 확인란 합니다.  
  
