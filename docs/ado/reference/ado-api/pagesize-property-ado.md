---
description: PageSize 속성(ADO)
title: PageSize 속성 (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::PageSize
helpviewer_keywords:
- PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
author: rothja
ms.author: jroth
ms.openlocfilehash: 2c073d0ef7cceb74864b7f526ef9a5283ca946a7
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88773532"
---
# <a name="pagesize-property-ado"></a>PageSize 속성(ADO)
레코드 [집합](./recordset-object-ado.md)에서 한 페이지를 구성 하는 레코드 수를 나타냅니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 페이지에 있는 레코드 수를 나타내는 **Long** 값을 설정 하거나 반환 합니다. 기본값은 **10**입니다.  
  
## <a name="remarks"></a>설명  
 **PageSize** 속성을 사용 하 여 데이터의 논리적 페이지를 구성 하는 레코드 수를 확인 합니다. 페이지 크기를 설정 하면 [AbsolutePage](./absolutepage-property-ado.md) 속성을 사용 하 여 특정 페이지의 첫 번째 레코드로 이동할 수 있습니다. 이 기능은 사용자가 데이터를 통해 페이지를 이동 하 여 한 번에 특정 개수의 레코드를 볼 수 있도록 하려는 경우에 유용 합니다.  
  
 이 속성은 언제 든 지 설정할 수 있으며 해당 값은 특정 페이지의 첫 번째 레코드 위치를 계산 하는 데 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>참고 항목  
 [AbsolutePage, PageCount 및 PageSize 속성 예제 (VB)](./absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount 및 PageSize 속성 예제 (VC + +)](./absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](./absolutepage-property-ado.md)   
 [PageCount 속성(ADO)](./pagecount-property-ado.md)