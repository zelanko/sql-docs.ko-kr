---
description: 버전 번호
title: 버전 번호 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- version number supported [ODBC]
- interoperability [ODBC], version number supported
ms.assetid: 6eccacdf-b837-4b66-bd48-ba31771acecb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 86da481ef7854bb9878c2bac565ef2797b61f5ab
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421427"
---
# <a name="version-number"></a>버전 번호
여러 버전의 ODBC가 있으며, 각 버전에는 서로 다른 기능이 있습니다. 응용 프로그램은 SQL_ODBC_VER 및 SQL_DRIVER_ODBC_VER 옵션으로 **SQLGetInfo** 를 호출 하 여 드라이버 관리자 및 특정 드라이버에서 지 원하는 ODBC 버전을 결정 합니다.
