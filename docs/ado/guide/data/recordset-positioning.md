---
title: 레코드 집합 위치 지정 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924438"
---
# <a name="recordset-positioning"></a>레코드 집합 위치 지정
사용 하 여는 **AbsolutePosition** 서 수 위치를 기반으로 레코드를 이동 하는 속성을 **레코드 집합** 개체 또는 현재 레코드의 서 수 위치를 결정. 공급자 사용 가능 하도록이 속성에 대 한 적절 한 기능을 지원 해야 합니다.  
  
 **AbsolutePosition** 는 1부터 시작 하 고 현재 레코드에서 첫 번째 레코드인 경우 합니다 **레코드 집합**합니다. 이전에 설명한 대로 레코드의 총 수를 가져올 수 있습니다는 **Recordset** 에서 개체를 **RecordCount** 속성.  
  
 설정한 경우 합니다 **AbsolutePosition** 속성인 경우에 현재 캐시에서 레코드를 ADO 캐시를 다시 로드 하면 지정 된 레코드를 사용 하 여 시작 하는 레코드의 새 그룹을 사용 하 여 합니다. 합니다 **CacheSize** 속성이이 그룹의 크기를 결정 합니다.  
  
> [!NOTE]
>  사용 하지 않아야 합니다 **AbsolutePosition** 서로게이트 레코드 숫자로 속성입니다. 지정된 된 레코드의 위치는 이전 레코드를 삭제 하는 경우 변경 됩니다. 또한 방법이 확신할 수 같은 지정 된 레코드를 가질 수 없습니다 **AbsolutePosition** 경우는 **레코드 집합** 개체 다시 쿼리되어 되었거나 다시 합니다. 책갈피를 유지 하 고 지정된 된 위치를 반환 하는 권장된 방법이 되며 모든 형식의 위치 통해서만 **레코드 집합** 개체입니다.
