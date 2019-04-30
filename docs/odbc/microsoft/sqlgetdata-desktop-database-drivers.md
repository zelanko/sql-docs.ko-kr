---
title: SQLGetData (데스크톱 데이터베이스 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Desktop Database Drivers
ms.assetid: c9d9a32d-5dc2-4189-9bfb-2b008bc3d6a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6f362d725f8b734ab9ecdbdc79c268af08a495b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63313137"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData(데스크톱 데이터베이스 드라이버)
이 함수 후 및 열 검색 되는 순서에 관계 없이 바인딩된 열이 있는 여부 모든 열에서 데이터를 검색할 수 있습니다.  
  
> [!NOTE]  
>  \*pcbValue **SQLGetData** 반환할 수 있습니다 배의 실제로 사용할 수 있는 문자로 Jet 4.0 데이터베이스에는 510 자를 초과 하는 ANSI 데이터에 바인딩하는 경우. 문자 값이 510 이하의 실제 cbValue 반환 됩니다.
