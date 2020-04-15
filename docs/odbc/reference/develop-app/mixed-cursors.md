---
title: 혼합 커서 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/20/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a91dacf8ea9c0ed0db2c3b64634ddd53b854a534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307438"
---
# <a name="mixed-cursors"></a>혼합 커서

혼합 커서는 키집합 기반 커서와 동적 커서의 조합입니다. 결과 집합이 너무 커서 전체 결과 집합에 대한 키를 합리적으로 저장하지 않는 경우에 사용됩니다. 혼합 커서는 전체 결과 집합보다 작지만 행 집합보다 큰 키 집합을 만들어 구현됩니다.  
  
 응용 프로그램이 키 집합 내에서 스크롤되는 한 동작은 키 집합 기반입니다. 응용 프로그램이 키 집합 외부로 스크롤되면 커서가 요청된 행을 가져오고 새 키 집합을 만듭니다. 새 키 집합을 만든 후 동작은 해당 키 집합 내에서 키 집합 기반으로 되돌아갑니다.  
  
 예를 들어 결과 집합에 1,000개의 행이 있고 키 집합 크기가 100이고 행 집합 크기가 10인 혼합 커서를 사용한다고 가정합니다. 첫 번째 행 집합을 가져오면 커서는 처음 100개 행에 대한 키로 구성된 키 집합을 만듭니다. 그런 다음 요청에 따라 처음 10개의 행을 반환합니다.  
  
 이제 다른 응용 프로그램이 행 11 및 101을 삭제한다고 가정합니다. 커서가 행 11을 검색하려고 하면 이 행에 대한 키가 있지만 행이 없기 때문에 간격이 발생합니다. 키집합 기반 동작입니다. 커서가 행 101을 검색하려고 하면 커서가 행에 대한 키가 없기 때문에 행이 누락된 것을 검색하지 않습니다. 대신 이전에 행 102였던 것을 검색합니다. 동적 커서 동작입니다.  
  
 혼합 커서는 키집합 크기가 결과 집합 크기와 같을 때 키 집합 기반 커서와 동일합니다. 혼합 커서는 키 집합 크기가 1인 경우 동적 커서와 같습니다.
