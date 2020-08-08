---
title: 데이터베이스에서 새로 고침 (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 59a6db8f-2db6-4071-9005-928a7231de92
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: a3ca412381cf31edce8cf735fab630a6db92e5df
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/07/2020
ms.locfileid: "87935167"
---
# <a name="refresh-from-database-mysqltosql"></a>데이터베이스에서 새로 고침(MySQLToSQL)
**데이터베이스에서 새로 고침** 대화 상자를 사용 하 여 MySQL 데이터베이스에서 새로 고칠 개체를 선택할 수 있습니다. 대화 상자의 행은 메타 데이터의 상태를 기반으로 하는 색으로 구분 됩니다.  
  
-   개체 메타 데이터가 로컬 및 MySQL 데이터베이스에서 변경 된 경우 해당 행은 파랑입니다.  
  
-   개체 메타 데이터가 MySQL 데이터베이스에서 변경 되었지만 SSMA에서는 변경 되지 않은 경우에는 해당 행이 노란색입니다.  
  
-   개체 메타 데이터가 로컬에서 변경 되었지만 MySQL 데이터베이스에서는 변경 되지 않은 경우 행은 녹색입니다.  
  
-   MySQL 데이터베이스에서 새로운 개체인 경우에는 해당 행이 분홍색입니다.  
  
**프로젝트 설정** 대화 상자에서 기본 개체 새로 고침 설정을 지정할 수 있습니다. 자세한 내용은 [프로젝트 설정 &#40;동기화&#41; &#40;MySQLToSQL&#41;](../../ssma/mysql/project-settings-synchronization-mysqltosql.md) 를 참조 하세요.  
  
**데이터베이스에서 새로 고침** 대화 상자에 액세스 하려면 MySQL 메타 데이터 탐색기에서 개체를 마우스 오른쪽 단추로 클릭 하 고 **데이터베이스에서 새로 고침**을 클릭 합니다.  
  
## <a name="options"></a>옵션  
  
|||  
|-|-|  
|**용어**|**정의**|  
|**축소 (-)**|모든 개체 그룹을 축소 하 여 개별 개체를 숨깁니다.|  
|**확장 (+)**|모든 개체 그룹을 확장 하 여 개별 개체를 표시 합니다.|  
|**동일 개체 숨기기/표시**|MySQL 데이터베이스 및 SSMA에서 개체 메타 데이터가 동일한 경우 목록에서 개체를 숨깁니다.|  
|**데이터베이스에서 새로 고침 (화살표 단추)**|화살표 단추를 사용 하 여 SSMA에서 선택한 개체의 메타 데이터를 업데이트 하도록 지정 합니다.|  
|**데이터베이스에서 새로 고치지 않음 (X 단추)**|X 단추를 사용 하 여 SSMA에서 선택한 개체의 메타 데이터를 업데이트 하지 않도록 지정 합니다.|  
|**범례**|**범례** 대화 상자를 표시 합니다. 범례에는 행 색상과 메타 데이터 상태 간의 매핑이 포함 되어 있습니다.<br /><br />**데이터베이스에서 새로 고침** 대화 상자 위쪽의 **범례** 대화 상자를 유지 하려면 **맨 위에 표시** 확인란을 선택 합니다.|  
  
