---
title: 개체 삭제
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.swb.deleteobjects.f1
helpviewer_keywords:
- Delete Objects dialog box
ms.assetid: 49541441-179c-40d3-ba0c-01bcae545984
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 07972c72c89d5098c528ab65f886b1935d47b2a1
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001978"
---
# <a name="delete-objects"></a>개체 삭제
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
이 대화 상자를 사용하여 데이터베이스나 데이터베이스 개체를 삭제할 수 있습니다.  
  
## <a name="ui-element-list"></a>UI 요소 목록  
**삭제할 개체**  
삭제하려고 하는 개체의 이름, 유형, 소유자 및 상태와 실행하는 동안 발생한 오류에 대한 메시지를 표시합니다.  
  
> [!NOTE]  
> 데이터베이스에서 **삭제** 를 실행하는 것은 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 DROP DATABASE를 실행하는 것과 같습니다.  
  
**종속성 표시**  
현재 선택한 개체에 종속된 개체와 현재 개체가 종속된 개체(상향 및 하향 종속성)를 모두 표시하려면 클릭합니다. **종속성 표시** 대화 상자에 표시된 정보는 읽기 전용입니다.  
  
> [!NOTE]  
> **종속성 표시** 단추는 모든 유형의 데이터베이스 개체에 대해 표시되지 않습니다. **종속성 표시** 단추를 사용할 수 없을 때 종속성을 보려면 개체 탐색기에서 개체를 마우스 오른쪽 단추로 클릭한 다음 **종속성 보기**를 클릭합니다.  
  
**백업 삭제 및 데이터베이스에 대한 기록 정보 복원**  
데이터베이스가 삭제될 때만 나타나는 이 확인란을 선택하면 **msdb** 데이터베이스에서 주제 데이터베이스에 대한 백업 및 복원 기록이 삭제됩니다.  
  
**기존 연결 닫기**  
데이터베이스가 삭제될 때만 나타나는 이 확인란을 선택하면 주제 데이터베이스에 대한 연결이 종료됩니다.  
  
