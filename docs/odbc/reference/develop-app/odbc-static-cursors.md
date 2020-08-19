---
description: ODBC 정적 커서
title: ODBC 정적 커서 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], static
- static cursors [ODBC]
ms.assetid: 28cb324c-e1c3-4b5c-bc3e-54df87037317
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9689badd39e21f82c268be904b29ffb1fa90a8ae
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429165"
---
# <a name="odbc-static-cursors"></a>ODBC 정적 커서
정적 커서는 결과 집합이 정적으로 표시 되는 커서입니다. 일반적으로 커서를 연 후 결과 집합의 멤버 자격, 순서 또는 값에 대 한 변경 내용을 검색 하지 않습니다. 예를 들어 정적 커서에서 행을 인출 하 고 다른 응용 프로그램에서 해당 행을 업데이트 한다고 가정 합니다. 정적 커서가 행을 refetches 다른 응용 프로그램에서 변경한 내용에도 불구 하 고 표시 되는 값은 변경 되지 않습니다.  
  
 정적 커서는 자신의 업데이트, 삭제 및 삽입을 검색할 수 있지만 반드시 그럴 필요는 없습니다. 특정 정적 커서가이 변경 내용을 감지 하는지 여부는 **SQLGetInfo**의 SQL_STATIC_SENSITIVITY 옵션을 통해 보고 됩니다. 정적 커서는 다른 업데이트, 삭제 및 삽입을 검색 하지 않습니다.  
  
 SQL_ATTR_ROW_STATUS_PTR statement 특성에 의해 지정 된 행 상태 배열에는 모든 행에 대 한 SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO 또는 SQL_ROW_ERROR 포함 될 수 있습니다. 커서를 통해 업데이트, 삭제 또는 삽입 된 행에 대 한 SQL_ROW_UPDATED, SQL_ROW_DELETED 또는 SQL_ROW_ADDED를 반환 합니다 .이 경우 커서는 이러한 변경 내용을 검색할 수 있다고 가정 합니다.  
  
 일반적으로 정적 커서는 결과 집합의 행을 잠그거나 결과 집합의 복사본 또는 스냅숏을 만들어 구현 합니다. 행을 비교적 쉽게 잠글 수 있지만 동시성을 크게 줄일 수 있는 단점이 있습니다. 복사본을 만들면 동시성이 향상 되 고, 커서에서 복사본을 수정 하 여 자체 업데이트, 삭제 및 삽입을 추적할 수 있습니다. 그러나 다른 사용자가 데이터를 변경 하는 경우에는 복사본을 만드는 데 비용이 많이 들고 기본 데이터에서 분기할 수 있습니다.
