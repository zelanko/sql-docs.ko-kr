---
title: 에는 인덱스를 만들 | Microsoft Docs
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
- CREATE INDEX [ODBC]
- Paradox driver [ODBC], create index
ms.assetid: 6472bd69-b931-4bc2-a9bf-f1873ed4cdfe
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 473c8d73e33504e7cc22d3b02aaca789d9c7a620
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32902038"
---
# <a name="create-index-for-paradox"></a>에는 인덱스 만들기
ODBC Paradox 드라이버에 대 한 CREATE INDEX 문의 구문은 다음과 같습니다.  
  
 **만들** [**UNIQUE**] **인덱스** *인덱스 이름*  
  
 **ON** *테이블 이름*  
  
 **(** *열 식별자* [**ASC**]  
  
 [**,** *열 식별자* [**ASC**]...] **)**  
  
 Paradox ODBC 드라이버가 지원 하지 않습니다는 **DESC** CREATE INDEX 문에 대 한 ODBC SQL 문법의 키워드입니다. *테이블 이름* 인수는 테이블의 전체 경로 지정할 수 있습니다.  
  
 경우 키워드 **UNIQUE** 지정, Paradox ODBC 드라이버에 고유 인덱스가 생성 됩니다. 첫 번째 고유 인덱스가 기본 인덱스도 만들어집니다. 이것은 Paradox 기본 키 파일 이름은 *테이블 이름*합니다. 픽셀입니다. 기본 인덱스 다음과 같은 제한 사항이 적용 됩니다.  
  
-   모든 행이 테이블에 추가 하기 전에 기본 인덱스를 만들어야 합니다.  
  
-   기본 인덱스는 테이블의 첫 번째 "n" 열에 정의 되어야 합니다.  
  
-   테이블 기본 인덱스는 하나만 허용 됩니다.  
  
-   기본 인덱스를 테이블에 정의 되어 있지 않으면 Paradox 드라이버에서 테이블을 업데이트할 수 없습니다. (Note:이 고유 인덱스는 테이블에 정의 되어 있지 않더라도 업데이트할 수 있는 빈 테이블에 적용 되지 않습니다.)  
  
-   *인덱스 이름* 기본 인덱스에 대 한 인수 Paradox 요구에 따라 테이블의 기본 이름과 동일 해야 합니다.  
  
 경우 키워드 **UNIQUE** 은 생략 하면 ODBC Paradox 드라이버 만들어집니다 비고유 인덱스입니다. 이 주기 라는 Paradox 보조 인덱스 위해 *테이블 이름*합니다. X*nn* 및 *테이블 이름*합니다. Y*nn*여기서 *nn* 테이블의 열 수입니다. 고유 하지 않은 인덱스 다음과 같은 제한 사항이 적용 됩니다.  
  
-   테이블에 대해 고유 하지 않은 인덱스를 만들 수 있습니다, 전에 해당 테이블에 대 한 기본 인덱스 존재 해야 합니다.  
  
-   에는 3. *x*, *인덱스 이름* 기본 인덱스 (고유 또는 고유 하지 않은) 이외의 모든 인덱스에 대 한 인수가 열 이름과 동일 해야 합니다. 에는 4. *x* 5. *x*, 이와 같은 인덱스의 이름이 될 수 있지만 열 이름과 동일 지정할 필요가 없습니다.  
  
-   고유 하지 않은 인덱스에 대 한 하나의 열만 지정할 수 있습니다.  
  
 인덱스는 테이블에 정의한 후에 열을 추가할 수 없습니다. CREATE TABLE 문의 인수 목록의 첫 번째 열 인덱스를 만드는 경우 인수 목록에 두 번째 열을 포함할 수 없습니다.  
  
 예를 들어 판매 주문 번호를 사용 하 고 SO_LINES 테이블에 고유 인덱스와 숫자 열 줄을 하려면 문을 사용 합니다.  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 부품 번호 열 SO_LINES 테이블에 고유 하지 않은 인덱스를 사용 하려면 문을 사용 합니다.  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 Note 첫 번째 문은 항상 만들어집니다 기본 인덱스는 테이블과 동일한 이름을 가진 두 개의 CREATE INDEX 문을 수행 될 때 및 두 번째 문은 항상 열과 동일한 이름을 가진 고유 인덱스가 생성 됩니다. CREATE INDEX 문에서 서로 다른 이름을 입력 하는 경우에 그리고 인덱스가 UNIQUE 레이블이 지정 된 두 번째 CREATE INDEX 문에 경우에 이러한 방식으로 이러한 인덱스 이름은 됩니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진만 읽기를 구현 하지 않고 Paradox 드라이버를 사용 하 고 추가 문은 사용할 수 있습니다.
