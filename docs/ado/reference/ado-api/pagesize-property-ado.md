---
title: "PageSize 속성 (ADO) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset15::PageSize
helpviewer_keywords: PageSize property [ADO]
ms.assetid: e57930a6-46c4-4a17-a3b6-f79e94d5c9c7
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9c0417012a1c68d0a3e3951a11f3a9ec84d8e89e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="pagesize-property-ado"></a>PageSize 속성 (ADO)
레코드 수를 구성 나타냅니다에서 한 페이지는 [레코드 집합](../../../ado/reference/ado-api/recordset-object-ado.md)합니다.  
  
## <a name="settings-and-return-values"></a>설정 및 반환 값  
 설정 하거나 반환는 **긴** 페이지에 있는 레코드 수를 나타내는 값입니다. 기본값은 **10**합니다.  
  
## <a name="remarks"></a>주의  
 사용 하 여는 **PageSize** 속성을 데이터의 논리 페이지를 구성 하는 레코드 수를 지정 합니다. 페이지 크기를 설정 하면 사용 하 여 [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md) 속성을 특정 페이지의 첫 번째 레코드로 이동 합니다. 이 특정 레코드 수가 한 번에 보기를 사용자 데이터의 페이지 수 있도록 하려는 경우 웹 서버 시나리오에서 유용 합니다.  
  
 언제 든 지가이 속성을 설정할 수 있습니다 및 특정 페이지의 첫 번째 레코드의 위치를 계산 하는 것에 대 한 해당 값이 사용 됩니다.  
  
## <a name="applies-to"></a>적용 대상  
 [레코드 집합 개체(ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>관련 항목:  
 [AbsolutePage, PageCount, 및 PageSize 속성 예제 (VB)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vb.md)   
 [AbsolutePage, PageCount, 및 PageSize 속성 예제 (VC + +)](../../../ado/reference/ado-api/absolutepage-pagecount-and-pagesize-properties-example-vc.md)   
 [AbsolutePage 속성 (ADO)](../../../ado/reference/ado-api/absolutepage-property-ado.md)   
 [PageCount 속성(ADO)](../../../ado/reference/ado-api/pagecount-property-ado.md)
