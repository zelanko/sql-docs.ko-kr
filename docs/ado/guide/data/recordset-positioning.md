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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924438"
---
# <a name="recordset-positioning"></a>레코드 집합 위치 지정
**AbsolutePosition** 속성을 사용 하 여 레코드 **집합** 개체의 서 수 위치에 따라 레코드를 이동 하거나 현재 레코드의 서 수 위치를 확인 합니다. 공급자는이 속성을 사용할 수 있는 적절 한 기능을 지원 해야 합니다.  
  
 **AbsolutePosition** 는 1부터 시작 하 고 현재 레코드가 **레코드 집합**의 첫 번째 레코드인 경우 1과 같습니다. 앞에서 설명한 것 처럼 **RecordCount** 속성에서 레코드 **집합** 개체의 총 레코드 수를 가져올 수 있습니다.  
  
 **AbsolutePosition** 속성을 설정 하는 경우 현재 캐시의 레코드를 사용 하는 경우에도 ADO는 지정 된 레코드부터 시작 하 여 새 레코드 그룹을 사용 하 여 캐시를 다시 로드 합니다. **CacheSize** 속성은이 그룹의 크기를 결정 합니다.  
  
> [!NOTE]
>  **AbsolutePosition** 속성은 서로게이트 레코드 번호로 사용 하면 안 됩니다. 이전 레코드를 삭제 하면 지정 된 레코드의 위치가 변경 됩니다. 또한 **레코드 집합** 개체를 다시 만들거나 다시 열 경우 지정 된 레코드가 동일한 **AbsolutePosition** 를 갖게 됩니다. 책갈피는 지정 된 위치를 유지 하 고 반환 하는 데 권장 되는 방법 이며 모든 형식의 **레코드 집합** 개체에서 위치를 지정 하는 유일한 방법입니다.
