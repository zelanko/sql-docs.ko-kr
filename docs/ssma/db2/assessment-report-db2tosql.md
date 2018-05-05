---
title: 평가 보고서 (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b599255141505f7d354863006f4ec2aa2e2fdea1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-db2tosql"></a>평가 보고서 (DB2ToSQL)
데이터베이스 개체를 변환의 결과 표시 하는 평가 보고서 창 [!INCLUDE[tsql](../../includes/tsql_md.md)] 구문, 복잡성과 비용이 마이그레이션 프로젝트를 예상할 수 있습니다.  
  
원본 메타 데이터 탐색기에서 변환할 개체를 선택할 평가 보고서에 액세스 하려면 마우스 단추로 클릭 **스키마** 또는 **동의어**를 선택한 후 **보고서 만들기**합니다.  
  
## <a name="options"></a>옵션  
  
|||  
|-|-|  
|용어|정의|  
|**변환 통계**|문 유형으로 변환 통계가 표시 됩니다. 이 창은 될 때 스키마와 같은 그룹 개체를 표시 하거나 왼쪽된 창에서 코드 없이 개체를 선택 합니다.|  
|**범주별으로 개체**|범주별으로 개체 수를 표시합니다. 이 창 그룹 개체를 스키마와 같은 경우에 표시 됩니다. 또는 왼쪽된 창에서 코드 없이 개체를 선택 합니다.|  
|**통계**|선택한 개체에 대 한 변환 통계가 표시 됩니다. 이 창의 왼쪽된 창에서 코드와 함께 개별 개체를 선택 하는 경우에 표시 됩니다. 확장 해야 할 수도 **통계**, 바로 위에 되는 **소스** 이 창을 보려면 창.|  
|**원본**|변환 변환 되지 않은 코드를 강조 표시 및 선택한 개체에 대 한 DB2 코드를 보여 줍니다 [!INCLUDE[tsql](../../includes/tsql_md.md)]합니다. 이 창의 왼쪽된 창에서 코드와 함께 개별 개체를 선택 하는 경우에 표시 됩니다.<br /><br />설정 하거나 책갈피를 지웁니다. 줄 번호를 클릭 합니다. 코드를 통해 탐색 하는 창 맨 위에 있는 단추를 사용 합니다.|  
|**대상**|변환의 결과로 만들어진 표시 [!INCLUDE[tsql](../../includes/tsql_md.md)] 변환 되지 않은 코드에 대 한 오류 메시지와 선택한 개체에 대 한 코드입니다. 이 창의 왼쪽된 창에서 코드와 함께 개별 개체를 선택 하는 경우에 표시 됩니다.<br /><br />설정 하거나 책갈피를 지웁니다. 줄 번호를 클릭 합니다. 코드를 통해 탐색 하는 창 맨 위에 있는 단추를 사용 합니다.|  
|**메시지 창**|오류, 경고 및 평가 보고서를 만드는 동안 생성 된 정보 메시지를 표시 합니다. 메시지 수로 그룹화 됩니다. 이 오류를 발생 시킨 코드를 보려면 클릭 **오류**, **경고**, 또는 **정보**, 메시지, 범주를 확장 한 다음 메시지를 클릭 합니다.|  
  
