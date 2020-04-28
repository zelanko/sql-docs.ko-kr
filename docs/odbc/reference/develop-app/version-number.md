---
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
ms.openlocfilehash: 37b7924380b9e9beb60792b50436eaa13a503c76
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306721"
---
# <a name="version-number"></a>버전 번호
여러 버전의 ODBC가 있으며, 각 버전에는 서로 다른 기능이 있습니다. 응용 프로그램은 SQL_ODBC_VER 및 SQL_DRIVER_ODBC_VER 옵션으로 **SQLGetInfo** 를 호출 하 여 드라이버 관리자 및 특정 드라이버에서 지 원하는 ODBC 버전을 결정 합니다.
