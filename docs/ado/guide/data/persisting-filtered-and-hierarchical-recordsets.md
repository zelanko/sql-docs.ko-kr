---
title: "지속 필터링 되 고 계층적 레코드 집합 | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 6d7ad27e3694b7a92e560170e699f62d76d5e6b0
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/09/2018
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>필터링을 유지 하 고 계층적 레코드 집합
경우는 [필터](../../../ado/reference/ado-api/filter-property.md) 속성에 적용 되는 **레코드 집합**, 필터 액세스할 수 있는 행만 저장 됩니다. 경우는 **레코드 집합** 계층형 현재 자식 **레코드 집합** 및 자식의 부모를 포함 하 여 저장 됩니다 **레코드 집합**합니다. 경우는 **저장** 메서드는 자식 **레코드 집합** 가 자식 및 모든 자식 저장 되지만 부모를 호출 합니다. 계층에 대 한 자세한 내용은 **레코드 집합**, 참조 [데이터 셰이핑](../../../ado/guide/data/data-shaping.md)합니다.  
  
> [!NOTE]
>  계층 구조를 저장할 때 몇 가지 제한이 적용 **레코드 집합** (데이터 셰이프)를 XML 형식입니다. 자세한 내용은 참조 [XML 형식의 레코드 지속](../../../ado/guide/data/persisting-records-in-xml-format.md)합니다.
