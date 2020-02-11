---
title: 필터링 된 및 계층 구조 레코드 집합 유지 | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 11ab68775e19ec1d3ce3c888917588f41ad65287
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924635"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>필터링된 계층적 레코드 집합 유지
[필터](../../../ado/reference/ado-api/filter-property.md) 속성이 **레코드 집합**에 적용 되는 경우 필터에서 액세스할 수 있는 행만 저장 됩니다. **레코드 집합이** 계층적 이면 부모 **레코드**집합을 포함 하 여 현재 자식 **레코드 집합과** 해당 자식 항목이 저장 됩니다. 자식 **레코드 집합** 의 **Save** 메서드를 호출 하면 자식 및 모든 자식 항목이 저장 되지만 부모는 저장 되지 않습니다. 계층적 **레코드 집합**에 대 한 자세한 내용은 [데이터 셰이핑](../../../ado/guide/data/data-shaping.md)을 참조 하세요.  
  
> [!NOTE]
>  계층적 **레코드 집합** (데이터 셰이프)을 XML 형식으로 저장할 때 몇 가지 제한 사항이 적용 됩니다. 자세한 내용은 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)를 참조 하세요.
