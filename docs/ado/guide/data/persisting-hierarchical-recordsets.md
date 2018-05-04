---
title: 계층적 레코드 집합을 지속 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1506bd80eee82c2b93a3f3f543825efef394ef07
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="persisting-hierarchical-recordsets"></a>계층적 레코드 집합 유지
계층적 구조를 저장할 수 있습니다 **레코드 집합** ADTG 또는 XML 형식으로 호출 하 여 파일에는 [저장](../../../ado/reference/ado-api/save-method.md) 메서드. 그러나 두 가지 제한 사항이 적용 계층적 저장할 때 **레코드 집합**XML 형식으로 s: 경우 XML에 저장할 수 없습니다 계층적 **레코드 집합** 보류 중인 업데이트가 포함 되어 매개 변수가 있는 저장할 수 없습니다 계층적 **레코드 집합**합니다.  
  
 데이터 모양 지정 공급자에 대 한 자세한 내용은 참조 [OLE DB에 대 한 Microsoft Data Shaping Service](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) 및 [for OLE DB Data Shaping Service의 개요](http://msdn.microsoft.com/en-us/9f51e471-8e85-448e-9fb8-b64bbf767bf3)합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [데이터 예제를 셰이핑](../../../ado/guide/data/data-shaping-example.md)   
 [형식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)
