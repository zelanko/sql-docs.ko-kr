---
title: 커서를 혼합 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1905bc30afff4af0ffc74363b93f95732f4760f1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63254176"
---
# <a name="mixed-cursors"></a>혼합 커서
혼합된 커서는 키 집합 커서 및 동적 커서의 조합입니다. 결과 집합은 너무 커서 합리적으로 전체 결과 집합에 대 한 키를 저장할 때 사용 됩니다. 혼합된 커서는 전체 결과 집합 보다 작지만 행 집합 보다 큰 키 집합 커서를 만들어 구현 됩니다.  
  
 키 집합 내에서 스크롤하면 응용 프로그램으로 동작은 키 집합 구동 합니다. 응용 프로그램 키 집합 외부 스크롤하면 동작은 동적: 커서 요청 된 행을 인출 하 고 새 키를 만듭니다. 새 키 집합을 만든 후 키 집합 내에서 키 집합 커서에 동작을 되돌립니다.  
  
 예를 들어 결과 집합을 1,000 개의 행 및 키 집합 크기는 100 및 10 행 집합 크기를 사용 하 여 혼합된 커서를 사용 합니다. 첫 번째 행을 인출할 때 커서의 처음 100 개 행 키로 구성 된 키를 만듭니다. 그런 다음 요청에 따라 처음 10 개 행을 반환 합니다.  
  
 이제 또 다른 응용 프로그램 삭제 행 11 및 101을 가정 합니다. 커서를 11 행을 검색 하려고 하는 경우 발생 하는 것 구멍이이 행에 대 한 키가 있지만 행이 있습니다. 키 집합 커서 동작입니다. 커서를 않지만 101 행을 검색 하려고 하는 경우 커서는 행이 누락 된 행에 대 한 키에 없기 때문에 검색 되지 않습니다. 대신 던 행 102 이전에 검색 합니다. 동적 커서 동작입니다.  
  
 키 집합 크기를 결과 집합 크기와 같은 경우 혼합 커서가 키 집합 커서와 동일 합니다. 혼합된 커서 동적 커서에 해당 하는 경우 키 집합 크기가 1과 같습니다.
