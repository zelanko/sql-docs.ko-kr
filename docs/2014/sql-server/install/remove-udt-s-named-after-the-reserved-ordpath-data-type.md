---
title: UDT를 제거 합니다&#39;예약 된 ORDPATH 데이터 형식의 이름을 따서 s | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 474e910a-6abb-4e28-acc2-055338c011d4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3ee155c70a8b10d4437d6b2f374c8b9497bf3faa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66092916"
---
# <a name="remove-udt39s-named-after-the-reserved-ordpath-data-type"></a>UDT를 제거 합니다&#39;s의 예약 된 ORDPATH 데이터 형식의 이름을 딴
  업그레이드 관리자가 `ORDPATH` 데이터 형식용으로 예약된 용어를 따서 명명된 UDT(사용자 정의 형식)를 발견했습니다.  
  
## <a name="component"></a>구성 요소  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Description  
 기본 제공 데이터 형식에 사용되는 용어는 CLR(공용 언어 런타임) 또는 별칭 UDT의 이름으로 사용할 수 없습니다.  
  
## <a name="corrective-action"></a>수정 동작  
 데이터 형식의 이름을 따서 명명된 UDT를 제거하고 예약되지 않은 이름을 사용하여 UDT를 다시 만듭니다.  
  
## <a name="external-resources"></a>외부 리소스  
 [사용자 정의 형식 만들기](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
