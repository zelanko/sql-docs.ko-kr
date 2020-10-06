---
description: 계층적 레코드 집합 유지
title: 계층 구조 레코드 집합 유지 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO], persisting
- persisting hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 43798bb5-98a6-4ad6-9bf8-78154b3a1827
author: rothja
ms.author: jroth
ms.openlocfilehash: b3764011c0ce0e3a49a17b20cbb344b5e98218d7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/05/2020
ms.locfileid: "91724954"
---
# <a name="persisting-hierarchical-recordsets"></a>계층적 레코드 집합 유지
[Save](../../../ado/reference/ado-api/save-method.md) 메서드를 호출 하 여 ADTG 또는 XML 형식의 파일에 계층적 **레코드 집합** 을 저장할 수 있습니다. 그러나 계층적 **레코드**집합을 xml 형식으로 저장할 때 두 가지 제한 사항이 적용 됩니다. 계층적 **레코드 집합** 에 보류 중인 업데이트가 포함 되어 있고 매개 변수가 있는 계층적 **레코드 집합**을 저장할 수 없는 경우에는 xml로 저장할 수 없습니다.  
  
 데이터 셰이핑 공급자에 대 한 자세한 내용은 [Microsoft 데이터 셰이핑 service for OLE DB](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) (ADO) 및 [OLE DB 데이터 셰이핑 서비스 개요](/previous-versions/windows/desktop/ms719615(v=vs.85))를 참조 하세요.  
  
## <a name="see-also"></a>참고 항목  
 [데이터 셰이핑 예](../../../ado/guide/data/data-shaping-example.md)   
 [공식 모양 문법](../../../ado/guide/data/formal-shape-grammar.md)   
 [일반적인 셰이핑 명령](../../../ado/guide/data/shape-commands-in-general.md)