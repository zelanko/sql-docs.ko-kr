---
title: 필터링 및 계층적 레코드 집합 유지 | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: cbd237580dc8c56284552e6fe2fb00e469832c5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702051"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>필터링된 계층적 레코드 집합 유지
경우는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성에 적용 되는 **레코드 집합**, 필터에서 액세스할 수 있는 행만 저장 됩니다. 경우는 **Recordset** 계층형 현재 자식 **레코드 집합** 및 자식의 부모를 포함 하 여 저장 됩니다 **레코드 집합**. 경우는 **저장** 메서드는 자식 **레코드 집합** 는 자식 노드와 모든 자식이 저장 되지만 호출 합니다. 계층에 대 한 자세한 내용은 **레코드 집합**를 참조 하십시오 [데이터 셰이핑](../../../ado/guide/data/data-shaping.md)합니다.  
  
> [!NOTE]
>  계층을 저장 하는 경우 일부 제한 사항이 적용 됩니다 **레코드 집합** (데이터 셰이프)를 XML 형식입니다. 자세한 내용은 [XML 형식으로 레코드 유지](../../../ado/guide/data/persisting-records-in-xml-format.md)합니다.
