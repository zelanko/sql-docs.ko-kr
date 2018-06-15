---
title: 드라이버에 직접 연결 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 431269b9a9ddad5f31500d025aa6122cc2c1e5a4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32909798"
---
# <a name="connecting-directly-to-drivers"></a>드라이버에 직접 연결
설명한 대로 [데이터 원본이 나 드라이버 선택](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)이 섹션의 앞부분에 나오는 데이터 소스를 전혀 사용 하지 않으려는 일부 응용 프로그램입니다. 대신, 드라이버에 직접 연결 하려고 합니다. **SQLDriverConnect** 데이터 소스를 지정 하지 않고 드라이버에 직접 연결 하는 응용 프로그램에 대 한 방법을 제공 합니다. 개념적으로 임시 데이터 원본에서 런타임에 생성 됩니다.  
  
 응용 프로그램을 지정 하는 드라이버에 직접 연결할는 **드라이버** 아닌 연결 문자열 키워드는 **DSN** 키워드입니다. 값은 **드라이버** 에서 반환 된 키워드는 드라이버에 대 한 설명을 **SQLDrivers**합니다. 예를 들어 드라이버에 대 한 설명이 Paradox 드라이버 및 데이터 파일을 포함 하는 디렉터리의 이름이 필요 합니다. 이 드라이버에 연결 하려면 응용 프로그램 다음 연결 문자열의 하나를 사용할 수 있습니다.  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 첫 번째 문자열과 드라이버는 추가 정보를 않아도 됩니다. 두 번째 문자열로 드라이버 데이터 파일이 포함 된 디렉터리의 이름에 대 한 메시지를 표시 해야 합니다.
