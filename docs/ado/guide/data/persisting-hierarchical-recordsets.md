---
title: 계층적 레코드 집합 유지 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3382e222a03f7538d3c666c3b85527b487d499f7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911516"
---
# <a name="persisting-hierarchical-recordsets"></a>계층적 레코드 집합 유지
계층을 저장할 수 있습니다 **레코드 집합** ADTG 또는 XML 형식으로 호출 하 여 파일에는 [저장](../../../ado/reference/ado-api/save-method.md) 메서드. 그러나 두 가지 제한 사항 적용 계층을 저장 하는 경우 **레코드 집합**XML 형식에서: 경우 XML에 저장할 수 없습니다는 계층적 **Recordset** 보류 중인 업데이트가 포함 매개 변수가 있는 저장할 수 없습니다 계층적 **레코드 집합**.  
  
 데이터 셰이핑 공급자에 대 한 자세한 내용은 참조 하세요. [OLE DB에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) 및 [for OLE DB Data Shaping Service 개요](https://msdn.microsoft.com/9f51e471-8e85-448e-9fb8-b64bbf767bf3)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [데이터 셰이핑 예제](../../../ado/guide/data/data-shaping-example.md)   
 [공식적인 셰이프 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
