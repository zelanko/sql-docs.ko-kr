---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c33b8a757e699a78c699cc87e7fd7dba26006b5d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47741451"
---
# <a name="pagesize-property-ado"></a>PageSize 속성(ADO)
구성 하는 레코드 수를 나타내는에서 한 페이지의 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환을 **긴** 페이지에는 레코드 수를 나타내는 값입니다. 기본값은 **10**합니다.  
  
## <a name="remarks"></a>Remarks  
 사용 된 **PageSize** 데이터의 논리 페이지를 구성 하는 레코드 수를 결정 하는 속성입니다. 사용할 수 있도록 페이지 크기를 설정 합니다 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성을 특정 페이지의 첫 번째 레코드를 이동 합니다. 이 특정 수의 레코드를 한 번에 보기를 사용자 데이터의 페이지 수 있도록 하려는 경우 웹 서버 시나리오에서 유용 합니다.  
  
 언제 든 지가이 속성을 설정할 수 있습니다 하 고 해당 값이 특정 페이지의 첫 번째 레코드의 위치를 계산 하는 데 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목  
 [AbsolutePage, PageCount, PageSize 속성 예제 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, PageSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 속성(ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
