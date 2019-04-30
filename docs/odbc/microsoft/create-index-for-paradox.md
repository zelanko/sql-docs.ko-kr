---
title: Paradox 용 CREATE INDEX | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 15e16fb311bf3c9acb2823772247e0fc16eabeef
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63232299"
---
# <a name="create-index-for-paradox"></a>Paradox용 CREATE INDEX
ODBC Paradox 드라이버에 대 한 CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 **CREATE** [**UNIQUE**] **INDEX** *index-name*  
  
 **ON** *table-name*  
  
 **(** *column-identifier* [**ASC**]  
  
 [**하십시오** *열 식별자* [**ASC**]...] **)**  
  
 ODBC Paradox 드라이버를 지원 하지 않습니다 합니다 **DESC** CREATE INDEX 문에 대 한 ODBC SQL 문법의 키워드입니다. 합니다 *테이블 이름* 인수 테이블의 전체 경로 지정할 수 있습니다.  
  
 경우 키워드 **UNIQUE** 를 지정 하면 ODBC Paradox 드라이버에 고유 인덱스가 생성 됩니다. 첫 번째 고유 인덱스는 기본 인덱스로 생성 됩니다. Paradox 기본 라는 키 파일을 이것이 *테이블 이름*합니다. PX입니다. 기본 인덱스는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   모든 행이 테이블에 추가 되기 전에 기본 인덱스를 만들어야 합니다.  
  
-   기본 인덱스는 테이블의 첫 번째 "n 개" 열에 정의 되어야 합니다.  
  
-   테이블 당 기본 인덱스는 하나만 허용 됩니다.  
  
-   기본 인덱스를 테이블에 정의 되어 있지 않으면 Paradox 드라이버에서 테이블을 업데이트할 수 없습니다. (이 고유 인덱스를 테이블에 정의 되어 있지 않더라도 업데이트할 수 있는 빈 테이블에 대 한 true note 합니다.)  
  
-   합니다 *인덱스 이름* Paradox에 필요한 대로 테이블의 기본 이름으로 기본 인덱스에 대 한 인수 같아야 합니다.  
  
 경우 키워드 **UNIQUE** 는 생략 하면 ODBC Paradox 드라이버 만들어집니다 비고유 인덱스입니다. 이 구성 이라는 두 개의 Paradox 보조 인덱스 파일 *테이블 이름*합니다. X*nn* 하 고 *테이블 이름*합니다. Y*nn*, 여기서 *nn* 테이블의 열입니다. 고유 하지 않은 인덱스는 다음과 같은 제한 사항이 적용 됩니다.  
  
-   테이블에 대 한 고유 하지 않은 인덱스를 만들 수 있습니다, 전에 해당 테이블에 대 한 기본 인덱스 존재 해야 합니다.  
  
-   에는 3. *x*서 *인덱스 이름* (고유 또는 고유 하지 않은) 기본 인덱스 이외의 인덱스에 대 한 인수가 열 이름과 동일 해야 합니다. 에는 4. *x* 5. *x*, 이러한 인덱스의 이름 일 수 있지만 열 이름과 같을 수 없습니다.  
  
-   고유 하지 않은 인덱스에 대 한 열을 하나만 지정할 수 있습니다.  
  
 테이블에 인덱스를 정의한 후에 열을 추가할 수 없습니다. CREATE TABLE 문의 인수 목록의 첫 번째 열 인덱스를 만드는 경우 인수 목록의 두 번째 열을 포함할 수 없습니다.  
  
 예를 들어, 판매 주문 번호를 사용 하 고 숫자 열 SO_LINES 테이블에 고유 인덱스로 줄에 문을 사용 합니다.  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 부품 번호 열 SO_LINES 테이블에 고유 하지 않은 인덱스를 사용 하려면 문을 사용 합니다.  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Note 두 CREATE INDEX 문을 수행 될 때 첫 번째 문에서 테이블과 동일한 이름을 가진 기본 인덱스를 만들려면 항상 및 두 번째 문은 항상 동일한 열 이름을 사용 하 여 비고유 인덱스를 만듭니다. 이러한 인덱스는 이름은이 방식으로 CREATE INDEX 문에서 서로 다른 이름을 입력 하는 경우에 인덱스는 두 번째 CREATE INDEX 문에서 UNIQUE 라고 하는 경우에 됩니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진만 읽기를 구현 하지 않고도 Paradox 드라이버를 사용 하 고 추가 하는 경우에 문이 허용 됩니다.
