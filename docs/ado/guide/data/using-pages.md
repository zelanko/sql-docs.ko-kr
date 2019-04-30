---
title: 페이지를 사용 하 여 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c1eced0fae443a67c85cc1f3f8ec9b44867ce464
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63184919"
---
# <a name="using-pages"></a>페이지 사용
사용 합니다 **PageCount** 속성에서 데이터 페이지 수를 결정 합니다 **레코드 집합** 개체입니다. *페이지* 레코드 같은 크기의 그룹이 합니다 **PageSize** 속성을 설정 합니다. 보다 적은 레코드가 있기 때문에 마지막 페이지 완료 되지 않더라도 **PageSize** 에서 추가 페이지로 계산 값을 **PageCount** 값입니다. 경우는 **레코드 집합** 개체는이 속성을 지원 하지 **PageCount** 나타내는-1이 됩니다는 **PageCount** 확인할 아닙니다.  
  
 사용 된 **PageSize** 데이터의 논리 페이지를 구성 하는 레코드 수를 결정 하는 속성입니다. 사용할 수 있도록 페이지 크기를 설정 합니다 **AbsolutePage** 속성을 특정 페이지의 첫 번째 레코드를 이동 합니다. 이 특정 수의 레코드를 한 번에 보기를 사용자 데이터의 페이지 수 있도록 하려는 경우 웹 서버 시나리오에서 유용 합니다.  
  
 언제 든 지가이 속성을 설정할 수 있습니다 하 고 해당 값이 특정 페이지의 첫 번째 레코드의 위치를 계산 하는 데 사용 됩니다.  
  
 사용 된 **AbsolutePage** 현재 레코드에 있는 페이지 번호를 식별 하는 속성입니다. 다시 공급자 사용 가능 하도록이 속성에 대 한 적절 한 기능을 지원 해야 합니다.  
  
 **AbsolutePage** 는 1부터 시작 하 고 현재 레코드에서 첫 번째 레코드인 경우 합니다 **레코드 집합**합니다. 특정 페이지의 첫 번째 레코드를 이동 하려면이 속성을 설정 합니다. 페이지 합계를 구할 합니다 **PageCount** 속성입니다.
