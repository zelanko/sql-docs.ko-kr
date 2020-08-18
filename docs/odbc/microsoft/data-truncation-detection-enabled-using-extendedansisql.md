---
description: ExtendedAnsiSQL을 사용하여 활성화된 데이터 잘림 검색
title: Extendedansisql을를 사용 하 여 데이터 잘림 검색 사용 Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- truncating data [ODBC]
- extendedANSISQL [ODBC], data truncation detection
ms.assetid: cec2359b-917d-4e1d-9625-5cd678b62f10
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 26965093caecbc11e94ef738ba6b8ff757b43258
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412893"
---
# <a name="data-truncation-detection-enabled-using-extendedansisql"></a>ExtendedAnsiSQL을 사용하여 활성화된 데이터 잘림 검색
Extendedansisql을 플래그가 설정 되 고 응용 프로그램이 char 또는 binary 열에 데이터를 삽입 하 고 데이터가 잘린 경우 잘림이 검색 됩니다. Extendedansisql을 플래그가 꺼져 있으면 이전 버전의 ODBC 데스크톱 데이터베이스 드라이버에서와 같이 데이터가 경고 없이 잘립니다.
