---
description: SQLSetScrollOptions(데스크톱 데이터베이스 드라이버)
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
ms.openlocfilehash: 57237aca0a68119f6ab8f967b9641f2a2a52fc8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421647"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions(데스크톱 데이터베이스 드라이버)
전방 및 정적 커서는 SQL_CONCUR_READ_ONLY 지원 됩니다.  
  
 SQL_CONCUR_LOCK의 *Fconcurrency* 인수에는 키 집합 커서만 지원 됩니다.  
  
 SQL_CONCUR_ROWVER의 *Fconcurrency* 인수는 지원 되지 않습니다.  
  
 동적 커서 및 혼합 커서는 지원 되지 않습니다.
