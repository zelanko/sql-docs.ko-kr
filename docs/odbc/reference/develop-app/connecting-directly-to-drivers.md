---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 44b9de304069849e965fc335e130ae57d9ec8bad
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68083161"
---
# <a name="connecting-directly-to-drivers"></a>드라이버에 직접 연결
살펴본 것 처럼 [데이터 원본 또는 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)이 섹션의 앞부분에 나오는 데이터 소스를 전혀 사용 하지 않으려는 일부 응용 프로그램입니다. 따라서 드라이버에 직접 연결 하려고 합니다. **SQLDriverConnect** 데이터 소스를 지정 하지 않고 드라이버에 직접 연결 하도록 응용 프로그램에 대 한 방법을 제공 합니다. 개념적으로 임시 데이터 소스는 런타임에 생성 됩니다.  
  
 응용 프로그램은 지정 된 드라이버에 직접 연결할 합니다 **드라이버** 대신 연결 문자열 키워드는 **DSN** 키워드입니다. 값을 **드라이버** 반환한 키워드는 드라이버에 대 한 설명을 **SQLDrivers**합니다. 예를 들어 드라이버에 설명이 Paradox 드라이버 및 데이터 파일이 포함 된 디렉터리의 이름이 필요 합니다. 이 드라이버에 연결 하려면 응용 프로그램 다음 연결 문자열의 하나를 사용할 수 있습니다.  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 첫 번째 문자열을 사용 하 여 드라이버가 추가 정보를 필요는 없습니다. 두 번째 문자열을 사용 하 여 드라이버를 데이터 파일을 포함 하는 디렉터리의 이름을 묻는 해야 합니다.
