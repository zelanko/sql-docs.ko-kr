---
title: SQLGetData (데스크톱 데이터베이스 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cdf875d594d84143ec45afca22805e533837c676
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData (데스크톱 데이터베이스 드라이버)
이 함수 뒤 및 열 검색 되는 순서에 관계 없이 바인딩된 열이 없는 여부 모든 열에서 데이터를 검색할 수 있습니다.  
  
> [!NOTE]  
>  \*pcbValue **SQLGetData** 반환할 수 있습니다 배의 문자로 실제로 사용할 수 있는 Jet 4.0 데이터베이스에는 510 자를 넘는 ANSI 데이터에 바인딩하는 경우. 문자 값 510 이하의 실제 cbValue를 반환 합니다.
