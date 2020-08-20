---
description: 드라이버에 직접 연결
title: 드라이버에 직접 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6dbf1d7a11f0ca4d6e7d049d425451b5f0e26c2d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461525"
---
# <a name="connecting-directly-to-drivers"></a>드라이버에 직접 연결
이 섹션의 앞부분에 나오는 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)에 설명 된 것 처럼 일부 응용 프로그램에서는 데이터 원본을 전혀 사용 하지 않으려고 합니다. 대신, 드라이버에 직접 연결 하려고 합니다. **SQLDriverConnect** 는 응용 프로그램이 데이터 원본을 지정 하지 않고 드라이버에 직접 연결할 수 있는 방법을 제공 합니다. 개념적으로 임시 데이터 원본은 런타임에 생성 됩니다.  
  
 드라이버에 직접 연결 하기 위해 응용 프로그램은 **DSN** 키워드 대신 연결 문자열에 **driver** 키워드를 지정 합니다. **Driver** 키워드의 값은 **sqldrivers**에서 반환 된 드라이버에 대 한 설명입니다. 예를 들어 드라이버에 Paradox 드라이버가 있는 경우 데이터 파일을 포함 하는 디렉터리의 이름이 필요 하다 고 가정 합니다. 이 드라이버에 연결 하기 위해 응용 프로그램은 다음 연결 문자열 중 하나를 사용할 수 있습니다.  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 첫 번째 문자열을 사용 하는 경우 드라이버에 추가 정보가 필요 하지 않습니다. 두 번째 문자열을 사용 하는 경우 드라이버는 데이터 파일을 포함 하는 디렉터리의 이름을 묻는 메시지를 표시 해야 합니다.
