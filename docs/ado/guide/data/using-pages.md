---
title: 페이지 사용 | Microsoft Docs
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
ms.openlocfilehash: 0d697fa5b411d9000c03a700f6b4fe0e4b39aa5e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "67923519"
---
# <a name="using-pages"></a>페이지 사용
**PageCount** 속성을 사용 하 여 **레코드 집합** 개체에 있는 데이터 페이지 수를 확인 합니다. *페이지* 는 크기가 **PageSize** 속성 설정과 같은 레코드의 그룹입니다. **PageSize** 값 보다 레코드 수가 적기 때문에 마지막 페이지가 불완전 한 경우에도 **PageCount** 값에서 추가 페이지로 계산 됩니다. **레코드 집합** 개체가이 속성을 지원 하지 않는 경우 **PageCount** 은 **PageCount** 을 확인할 수 없음을 나타내는-1입니다.  
  
 **PageSize** 속성을 사용 하 여 데이터의 논리적 페이지를 구성 하는 레코드 수를 확인 합니다. 페이지 크기를 설정 하면 **AbsolutePage** 속성을 사용 하 여 특정 페이지의 첫 번째 레코드로 이동할 수 있습니다. 이 기능은 사용자가 데이터를 통해 페이지를 이동 하 여 한 번에 특정 개수의 레코드를 볼 수 있도록 하려는 경우에 유용 합니다.  
  
 이 속성은 언제 든 지 설정할 수 있으며 해당 값은 특정 페이지의 첫 번째 레코드 위치를 계산 하는 데 사용 됩니다.  
  
 **AbsolutePage** 속성을 사용 하 여 현재 레코드가 있는 페이지 번호를 식별할 수 있습니다. 공급자는이 속성을 사용할 수 있는 적절 한 기능을 지원 해야 합니다.  
  
 **AbsolutePage** 는 1부터 시작 하 고 현재 레코드가 **레코드 집합**의 첫 번째 레코드인 경우 1과 같습니다. 특정 페이지의 첫 번째 레코드로 이동 하려면이 속성을 설정 합니다. **PageCount** 속성에서 총 페이지 수를 가져옵니다.
