---
title: 역설을 위한 인덱스 만들기 | 마이크로 소프트 문서
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
ms.openlocfilehash: 2e68484efdc5194f93f2acab31973377d9c66f1c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280913"
---
# <a name="create-index-for-paradox"></a>Paradox용 CREATE INDEX
ODBC 역설 드라이버에 대 한 CREATE INDEX 문의 구문은 다음과 있습니다.  
  
 **만들기** [**고유]** **인덱스** *이름*  
  
 **ON** *테이블 이름*  
  
 **(열** *식별자* [**ASC**]  
  
 [**,** *열 식별자* [**ASC**[...] **)**  
  
 ODBC 역설 드라이버는 인덱스 만들기 문에 대 한 ODBC SQL 문법에서 **DESC** 키워드를 지원 하지 않습니다. *테이블 이름* 인수는 테이블의 전체 경로를 지정할 수 있습니다.  
  
 **고유** 키워드를 지정하면 ODBC 역설 드라이버가 고유한 인덱스를 만듭니다. 첫 번째 고유 인덱스는 기본 인덱스로 만들어집니다. 테이블 *이름이라는*역설기본 키 파일입니다. 픽셀. 기본 인덱스에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   행이 테이블에 추가되기 전에 기본 인덱스를 만들어야 합니다.  
  
-   기본 인덱스는 테이블의 첫 번째 "n" 열에 정의되어야 합니다.  
  
-   테이블당 하나의 기본 인덱스만 허용됩니다.  
  
-   기본 인덱스가 테이블에 정의되지 않은 경우 Paradox 드라이버에서 테이블을 업데이트할 수 없습니다. (테이블에 고유 인덱스가 정의되어 있지 않은 경우에도 업데이트할 수 있는 빈 테이블에는 해당되지 않습니다.)  
  
-   기본 인덱스에 대한 *인덱스 이름* 인수는 Paradox에서 요구하는 대로 테이블의 기본 이름과 같아야 합니다.  
  
 **고유** 키워드를 생략하면 ODBC 역설 드라이버가 고유하지 않은 인덱스를 만듭니다. 이것은 *테이블 이름이라는*두 개의 역설 보조 인덱스 파일로 구성됩니다. X*nn* 및 *테이블 이름*. N*nn은* *nn이* 테이블의 열 수입니다. 고유가 아닌 인덱스에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   테이블에 대해 고유하지 않은 인덱스를 만들려면 해당 테이블에 대한 기본 인덱스가 있어야 합니다.  
  
-   역설 3. *x,* 기본 인덱스(고유 또는 비고유)가 아닌 모든 인덱스에 대한 *인덱스 이름* 인수는 열 이름과 같아야 합니다. 역설 4. *x* 및 5. *x*, 이러한 인덱스의 이름은 열 이름과 같을 수 있지만 같을 필요는 없습니다.  
  
-   고유하지 않은 인덱스에는 하나의 열만 지정할 수 있습니다.  
  
 테이블에 인덱스가 정의된 후에는 열을 추가할 수 없습니다. CREATE TABLE 문의 인수 목록의 첫 번째 열이 인덱스를 만드는 경우 두 번째 열은 인수 목록에 포함할 수 없습니다.  
  
 예를 들어 판매 주문 번호 및 줄 번호 열을 SO_LINES 테이블의 고유 인덱스로 사용하려면 문을 사용합니다.  
  
```  
CREATE UNIQUE INDEX SO_LINES  
 ON SO_LINES (SONum, LineNum)  
```  
  
 SO_LINES 테이블에서 부품 번호 열을 고유하지 않은 인덱스로 사용하려면 다음 문을 사용합니다.  
  
```  
CREATE INDEX PartNum  
 ON SO_LINES (PartNum)  
```  
  
 두 CREATE INDEX 문이 수행될 때 첫 번째 문은 항상 테이블과 이름이 같은 기본 인덱스를 만들고 두 번째 문은 항상 열과 같은 이름의 비고유 인덱스를 만듭니다. 이러한 인덱스는 CREATE INDEX 문에 다른 이름을 입력하고 인덱스가 두 번째 CREATE INDEX 문에서 UNIQUE로 레이블이 지정된 경우에도 이러한 방식으로 이름이 지정됩니다.  
  
> [!NOTE]  
>  Borland 데이터베이스 엔진을 구현하지 않고 역설 드라이버를 사용하는 경우 읽기 및 추가 문만 허용됩니다.
