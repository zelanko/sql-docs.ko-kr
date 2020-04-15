---
title: 드라이버에 직접 연결 | 마이크로 소프트 문서
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
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299083"
---
# <a name="connecting-directly-to-drivers"></a>드라이버에 직접 연결
[데이터 원본 또는 드라이버 선택에서](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)설명한 것처럼 이 섹션의 앞에서 일부 응용 프로그램은 데이터 원본을 전혀 사용하지 않으려고 합니다. 대신 드라이버에 직접 연결하려고 합니다. **SQLDriverConnect는** 응용 프로그램이 데이터 원본을 지정하지 않고 드라이버에 직접 연결할 수 있는 방법을 제공합니다. 개념적으로 런타임에 임시 데이터 원본이 만들어집니다.  
  
 드라이버에 직접 연결하려면 응용 프로그램은 **DSN** 키워드 대신 연결 문자열에 **DRIVER** 키워드를 지정합니다. **DRIVER** 키워드의 값은 **SQLDriver에서**반환된 드라이버에 대한 설명입니다. 예를 들어 드라이버에 역설 드라이버 설명이 있고 데이터 파일이 포함된 디렉터리 이름이 필요하다고 가정합니다. 이 드라이버에 연결하려면 응용 프로그램에서 다음 연결 문자열 중 하나를 사용할 수 있습니다.  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 첫 번째 문자열을 사용하면 드라이버에 추가 정보가 필요하지 않습니다. 두 번째 문자열을 사용하면 드라이버가 데이터 파일을 포함하는 디렉터리 이름을 묻는 메시지를 표시해야 합니다.
