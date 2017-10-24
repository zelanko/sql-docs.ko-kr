---
title: "페이지를 사용 하 여 | Microsoft Docs"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- PageSize property [ADO]
- pages [ADO]
- Recordset object [ADO]
- AbsolutePage property [ADO]
- PageCount property [ADO]
ms.assetid: 442b08c5-ccc7-4192-a1cc-22f250867782
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 34361d01b914d68cba1ff1e0e0f9378baf035be5
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="using-pages"></a>페이지를 사용 하 여
사용 하 여는 **PageCount** 속성에 있는 데이터 페이지 수를 확인 하 고 **레코드 집합** 개체입니다. *페이지* 같은 크기의 레코드의 그룹은 **PageSize** 속성을 설정 합니다. 보다 적은 수의 레코드가 있기 때문에 마지막 페이지가 완료 되는 경우에는 **PageSize** 에서 추가 페이지로 계산 값은 **PageCount** 값입니다. 경우는 **레코드 집합** 개체가이 속성을 지원 하지 않는 **PageCount** 임을 나타내는-1이 됩니다는 **PageCount** 결정할 수 있는있지 않습니다.  
  
 사용 하 여는 **PageSize** 속성을 데이터의 논리 페이지를 구성 하는 레코드 수를 지정 합니다. 페이지 크기를 설정 하면 사용 하 여 **AbsolutePage** 속성을 특정 페이지의 첫 번째 레코드로 이동 합니다. 이 특정 레코드 수가 한 번에 보기를 사용자 데이터의 페이지 수 있도록 하려는 경우 웹 서버 시나리오에서 유용 합니다.  
  
 언제 든 지가이 속성을 설정할 수 있습니다 및 특정 페이지의 첫 번째 레코드의 위치를 계산 하는 것에 대 한 해당 값이 사용 됩니다.  
  
 사용 하 여는 **AbsolutePage** 속성을 기본값인이 있는 페이지 번호를 식별 합니다. 다시, 공급자는이 속성을 사용할 수에 대 한 적절 한 기능을 지원 해야 합니다.  
  
 **AbsolutePage** 는 1부터 시작 하 고 현재 레코드의 첫 번째 레코드는 경우는 **레코드 집합**합니다. 특정 페이지의 첫 번째 레코드로 이동 하려면이 속성을 설정 합니다. 페이지 합계를 구할는 **PageCount** 속성입니다.

