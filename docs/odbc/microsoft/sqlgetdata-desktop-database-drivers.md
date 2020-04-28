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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2b102d8435831d45aad3c2049581513e0493de9a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304124"
---
# <a name="sqlgetdata-desktop-database-drivers"></a>SQLGetData(데스크톱 데이터베이스 드라이버)
이 함수는 바인딩된 열이 있고 열이 검색 되는 순서에 관계 없이 모든 열에서 데이터를 검색할 수 있습니다.  
  
> [!NOTE]  
>  \***SQLGetData** 의 pcbValue는 Jet 4.0 데이터베이스에서 510 자 보다 긴 ANSI 데이터에 바인딩할 때 실제로 사용할 수 있는 것과 동일한 수의 문자를 두 번 반환할 수 있습니다. 510 이하의 문자 값은 실제 cbValue를 반환 합니다.
