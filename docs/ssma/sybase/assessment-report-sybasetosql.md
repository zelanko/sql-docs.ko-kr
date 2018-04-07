---
title: 평가 보고서 (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f7d282ec97f55631c35e7e7f544d9f924d96b49a
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/06/2018
---
# <a name="assessment-report-sybasetosql"></a>평가 보고서 (SybaseToSQL)
데이터베이스 개체를 변환의 결과 표시 하는 평가 보고서 창 [!INCLUDE[tsql](../../includes/tsql_md.md)] 구문, 복잡성과 비용이 마이그레이션 프로젝트를 예상할 수 있습니다.  
  
원본 메타 데이터 탐색기에서 변환할 개체를 선택할 평가 보고서에 액세스 하려면 마우스 단추로 클릭 **데이터베이스**를 선택한 후 **보고서 만들기**합니다.  
  
## <a name="options"></a>옵션  
**변환 통계**  
문 유형으로 변환 통계가 표시 됩니다. 이 창 그룹 개체를 스키마와 같은 경우에 표시 됩니다. 또는 왼쪽된 창에서 코드 없이 개체를 선택 합니다.  
  
**범주별 개체**  
개체 유형별 변환 통계가 표시 됩니다. 이 창 그룹 개체를 스키마와 같은 경우에 표시 됩니다. 또는 왼쪽된 창에서 코드 없이 개체를 선택 합니다.  
  
**통계**  
선택한 개체에 대 한 변환 통계가 표시 됩니다. 이 창의 왼쪽된 창에서 코드와 함께 개별 개체를 선택 하는 경우에 표시 됩니다. 확장 해야 할 수도 **통계** 이 창을 보려면 합니다.  
  
**소스 탐색**  
선택한 개체에 대 한 ASE 코드 보여주며, 변환 변환 되지 않은 코드를 강조 표시 [!INCLUDE[tsql](../../includes/tsql_md.md)]합니다. 이 창의 왼쪽된 창에서 코드와 함께 개별 개체를 선택 하는 경우에 표시 됩니다.  
  
설정 하거나 책갈피를 지웁니다. 줄 번호를 클릭 합니다. 코드를 통해 탐색 하는 창 맨 위에 있는 단추를 사용 합니다.  
  
**대상 탐색**  
변환의 결과로 만들어진 표시 [!INCLUDE[tsql](../../includes/tsql_md.md)] 변환 되지 않은 코드에 대 한 오류 메시지와 선택한 개체에 대 한 코드입니다. 이 창의 왼쪽된 창에서 코드와 함께 개별 개체를 선택 하는 경우에 표시 됩니다.  
  
설정 하거나 책갈피를 지웁니다. 줄 번호를 클릭 합니다. 코드를 통해 탐색 하는 창 맨 위에 있는 단추를 사용 합니다.  
  
**메시지 창**  
오류, 경고 및 평가 보고서를 만들 때 생성 되는 정보 메시지를 표시 합니다. 메시지 수로 그룹화 됩니다. 이 오류를 발생 시킨 코드를 보려면 클릭 **오류**, **경고**, 또는 **정보**, 메시지, 범주를 확장 한 다음 메시지를 클릭 합니다.  
  
