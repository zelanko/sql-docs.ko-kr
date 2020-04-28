---
title: SQLSetScrollOptions (데스크톱 데이터베이스 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c47255b455354c49133d61c3546be63ab2380a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299440"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions(데스크톱 데이터베이스 드라이버)
전방 및 정적 커서는 SQL_CONCUR_READ_ONLY 지원 됩니다.  
  
 SQL_CONCUR_LOCK의 *Fconcurrency* 인수에는 키 집합 커서만 지원 됩니다.  
  
 SQL_CONCUR_ROWVER의 *Fconcurrency* 인수는 지원 되지 않습니다.  
  
 동적 커서 및 혼합 커서는 지원 되지 않습니다.
