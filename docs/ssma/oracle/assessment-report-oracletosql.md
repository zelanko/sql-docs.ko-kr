---
title: 평가 보고서 (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
author: Shamikg
ms.author: Shamikg
manager: shamikg
ms.openlocfilehash: 75fdb97b5b7d763694289d762edc65b4536a86c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68264521"
---
# <a name="assessment-report-oracletosql"></a>평가 보고서(OracleToSQL)
평가 보고서 창에는 데이터베이스 개체를 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문으로 변환한 결과가 표시 되며 마이그레이션 프로젝트의 복잡성과 비용을 예측 하는 데에도 도움이 될 수 있습니다.  
  
평가 보고서에 액세스 하려면 원본 메타 데이터 탐색기에서 변환할 개체를 선택 하 고 **스키마** 또는 **동의어**를 마우스 오른쪽 단추로 클릭 한 다음 **보고서 만들기**를 선택 합니다.  
  
## <a name="options"></a>옵션  
  
|||  
|-|-|  
|용어|정의|  
|**변환 통계**|문 유형별 변환 통계를 표시 합니다. 이 창은 스키마와 같은 그룹 개체 또는 코드 없는 개체를 왼쪽 창에서 선택할 때 표시 됩니다.|  
|**범주별 개체**|범주별로 개체 수를 표시 합니다. 이 창은 스키마와 같은 그룹 개체 또는 코드 없는 개체를 왼쪽 창에서 선택한 경우에만 표시 됩니다.|  
|**통계**|선택한 개체에 대 한 변환 통계를 표시 합니다. 이 창은 왼쪽 창에서 코드가 있는 개별 개체를 선택한 경우에만 표시 됩니다. 이 창을 보려면 **소스** 창 바로 위의 **통계**를 확장 해야 할 수도 있습니다.|  
|**소스**|선택한 개체에 대 한 Oracle 코드를 표시 하 고로 [!INCLUDE[tsql](../../includes/tsql-md.md)]변환 되지 않은 코드를 강조 표시 합니다. 이 창은 왼쪽 창에서 코드가 있는 개별 개체를 선택한 경우에만 표시 됩니다.<br /><br />줄 번호를 클릭 하 여 책갈피를 설정 하거나 선택 취소 합니다. 창 맨 위에 있는 단추를 사용 하 여 코드를 탐색 합니다.|  
|**대상**|선택한 개체에 대 한 [!INCLUDE[tsql](../../includes/tsql-md.md)] 변환 결과 코드와 변환 되지 않은 코드에 대 한 오류 메시지를 표시 합니다. 이 창은 왼쪽 창에서 코드가 있는 개별 개체를 선택한 경우에만 표시 됩니다.<br /><br />줄 번호를 클릭 하 여 책갈피를 설정 하거나 선택 취소 합니다. 창 맨 위에 있는 단추를 사용 하 여 코드를 탐색 합니다.|  
|**메시지 창**|평가 보고서를 만드는 동안 생성 된 오류, 경고 및 정보 메시지를 표시 합니다. 메시지는 숫자로 그룹화 됩니다. 오류를 발생 시킨 코드를 보려면 **오류**, **경고**또는 **정보**를 클릭 하 고 메시지 범주를 확장 한 다음 메시지를 클릭 합니다.|  
  
