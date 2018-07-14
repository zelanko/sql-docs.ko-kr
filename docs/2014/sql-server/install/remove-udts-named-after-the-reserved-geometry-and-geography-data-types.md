---
title: 예약된 된 GEOMETRY 및 GEOGRAPHY 데이터 형식의 명명 된 Udt 제거 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- geometry data type [SQL Server], UDTs
- geography data type [SQL Server], UDTs
ms.assetid: a167ce3a-50b4-4e77-a884-adb23b586c72
caps.latest.revision: 12
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e557c8c41596045390127ad066681a2f5c872875
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208523"
---
# <a name="remove-udts-named-after-the-reserved-geometry-and-geography-data-types"></a>예약된 GEOMETRY 및 GEOGRAPHY 데이터 형식의 이름을 따서 명명된 UDT를 제거합니다.
  업그레이드 관리자가 `geometry` 또는 `geography` 데이터 형식용으로 예약된 용어를 따서 명명된 UDT(사용자 정의 형식)를 발견했습니다. `geometry` 및 `geography` 데이터 형식은 공간 데이터 기능의 일부입니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 공간 데이터 형식에 사용되는 용어는 CLR(공용 언어 런타임) 또는 별칭 UDT의 이름으로 사용할 수 없습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 데이터 형식의 이름을 따서 명명된 UDT를 제거하고 예약되지 않은 이름을 사용하여 UDT를 다시 만듭니다.  
  
## <a name="external-resources"></a>외부 리소스  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
 [공간 데이터 형식 개요](../../relational-databases/spatial/spatial-data-types-overview.md)  
  
  
