---
description: Paradox용 CREATE INDEX
title: Paradox의 인덱스 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c0274f3f7cfdb79bf64e3616b16b7f3383063e07
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483646"
---
# <a name="create-index-for-paradox"></a>Paradox용 CREATE INDEX
ODBC Paradox 드라이버에 대 한 CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 **CREATE** [**UNIQUE**] **인덱스** *인덱스-이름*  
  
 **ON** *테이블 이름*  
  
 **(** *열 식별자* [**ASC**]  
  
 [**,** *열 식별자* [**ASC**] ...] **)**  
  
 ODBC Paradox 드라이버는 CREATE INDEX 문에 대해 ODBC SQL 문법의 **DESC** 키워드를 지원 하지 않습니다. *테이블 이름* 인수는 테이블의 전체 경로를 지정할 수 있습니다.  
  
 **Unique** 키워드를 지정 하면 ODBC Paradox 드라이버가 고유 인덱스를 만듭니다. 첫 번째 고유 인덱스는 기본 인덱스로 생성 됩니다. 이는 *테이블 이름*이라는 Paradox 기본 키 파일입니다. PX. 기본 인덱스에는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   테이블에 행을 추가 하기 전에 기본 인덱스를 만들어야 합니다.  
  
-   주 인덱스는 테이블의 첫 번째 "n" 개 열에 대해 정의 되어야 합니다.  
  
-   테이블당 하나의 주 인덱스만 사용할 수 있습니다.  
  
-   테이블에 기본 인덱스가 정의 되어 있지 않은 경우에는 Paradox 드라이버가 테이블을 업데이트할 수 없습니다. 이는 테이블에 고유 인덱스가 정의 되어 있지 않은 경우에도 업데이트 될 수 있는 빈 테이블에는 적용 되지 않습니다.  
  
-   주 인덱스의 *인덱스 이름* 인수는 Paradox에 필요한 테이블의 기본 이름과 동일 해야 합니다.  
  
 **Unique** 키워드를 생략 하면 ODBC Paradox 드라이버가 고유 하지 않은 인덱스를 만듭니다. 이는 *테이블 이름*이라는 두 개의 Paradox 보조 인덱스 파일로 구성 됩니다. X*nn* 및 *테이블 이름*입니다. Y*nn*, 여기서 *nn* 은 테이블의 열 번호입니다. 고유 하지 않은 인덱스에는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   테이블에 대해 고유 하지 않은 인덱스를 만들려면 해당 테이블에 대 한 기본 인덱스가 있어야 합니다.  
  
-   Paradox 3의 경우. *x*, 기본 인덱스 (고유 또는 고유 하지 않음) 이외의 인덱스에 대 한 *인덱스 이름* 인수는 열 이름과 동일 해야 합니다. Paradox 4의 경우. *x* 및 5. *x*, 이러한 인덱스의 이름은 열 이름과 같을 수 있지만 반드시 같을 필요는 없습니다.  
  
-   고유 하지 않은 인덱스에는 열을 하나만 지정할 수 있습니다.  
  
 테이블에 인덱스를 정의한 후에는 열을 추가할 수 없습니다. CREATE TABLE 문의 인수 목록에 있는 첫 번째 열이 인덱스를 만드는 경우 두 번째 열은 인수 목록에 포함할 수 없습니다.  
  
 예를 들어 sales order number와 line number 열을 SO_LINES 테이블의 고유 인덱스로 사용 하려면 다음 문을 사용 합니다.  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 Part number 열을 SO_LINES 테이블의 고유 하지 않은 인덱스로 사용 하려면 다음 문을 사용 합니다.  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 두 개의 CREATE INDEX 문을 수행할 때 첫 번째 문은 항상 테이블과 이름이 같은 기본 인덱스를 만들고 두 번째 문은 항상 열과 이름이 같은 고유 하지 않은 인덱스를 만듭니다. 이러한 인덱스는 CREATE INDEX 문에 다른 이름을 입력 하 고 두 번째 CREATE INDEX 문에 인덱스를 고유 하 게 지정 하는 경우에도 이러한 방식으로 이름이 지정 됩니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진를 구현 하지 않고 Paradox 드라이버를 사용 하는 경우에는 읽기 및 추가 문만 사용할 수 있습니다.
