---
title: 커서를 혼합 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16fd4840718c286adfe711b6b7322154f7f5f9cb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="mixed-cursors"></a>혼합된 커서
혼합 커서가 키 집합 커서와 동적 커서입니다. 결과 집합은 너무 커서 합리적으로 전체 결과 집합에 대 한 키를 저장할 때 사용 됩니다. 혼합 된 커서는 전체 결과 집합 보다 작은 하지만 행 집합 보다 큰 키 집합을 만들어 구현 됩니다.  
  
 키 집합 내에서 스크롤 하는 응용 프로그램으로 동작은 키 집합 구동 합니다. 응용 프로그램을 키 집합 외부 스크롤하면 경우 동작은 동적: 커서 요청 된 행을 인출 하 고 새 키 집합을 만듭니다. 새 키 집합을 만든 후 해당 키 집합 내에서 키 집합 커서 동작이 되돌아갑니다.  
  
 예를 들어 결과 집합에 1000 개의 행 및 행 집합 크기가 10 100의 키 집합 크기와 혼합된 커서를 사용 합니다. 첫 번째 행을 인출할 때 커서의 처음 100 개의 행에 대 한 키로 구성 된 키 집합을 만듭니다. 다음 요청에 따라 처음 10 개의 행을 반환 합니다.  
  
 이제 다른 응용 프로그램 삭제 행 11 및 101를 가정 합니다. 커서를 11 행을 검색 하려고 하는 경우이 발생 하 게 구멍이이 행에 대 한 키를 포함 하지만 행이 없습니다. 키 집합 커서 동작입니다. 커서를 101 행을 검색 하려고 하는 경우 커서 행이 누락 된 행에 대 한 키 없기 때문에 검색 하지 않습니다. 대신, 무엇 이었습니까 행 102 이전에 검색 합니다. 동적 커서 동작입니다.  
  
 키 집합 크기는 결과 집합 크기와 같은 때 혼합 커서가 키 집합 커서와 동일 합니다. 키 집합 크기는 1과 같을 때 혼합 커서가 동적 커서와 동일 합니다.
