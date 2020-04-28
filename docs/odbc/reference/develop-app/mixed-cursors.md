---
title: 혼합 커서 | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81307438"
---
# <a name="mixed-cursors"></a>혼합 커서

혼합 커서는 키 집합 커서와 동적 커서의 조합입니다. 결과 집합이 너무 커서 전체 결과 집합에 대 한 키를 저장 하는 데 사용 됩니다. 혼합 커서는 전체 결과 집합 보다 작고 행 집합 보다 큰 키 집합을 만들어 구현 합니다.  
  
 응용 프로그램이 키 집합 내에서 스크롤하면 동작은 키 집합을 기반으로 합니다. 응용 프로그램이 키 집합 외부에서 스크롤하면 동작은 동적입니다. 커서가 요청 된 행을 인출 하 고 새 키 집합을 만듭니다. 새 키 집합을 만든 후이 동작은 키 집합 내에서 키 집합으로 되돌아갑니다.  
  
 예를 들어 결과 집합에는 1000 개의 행이 있고 키 집합 크기가 100이 고 행 집합 크기가 10 인 혼합 커서를 사용 한다고 가정 합니다. 첫 번째 행 집합을 인출 하면 커서는 처음 100 개 행에 대 한 키로 구성 된 키 집합을 만듭니다. 그런 다음 요청에 따라 처음 10 개 행을 반환 합니다.  
  
 이제 다른 응용 프로그램이 11 및 101 행을 삭제 한다고 가정 합니다. 커서에서 행 11을 검색 하려고 하면이 행에 대 한 키가 있지만 행이 없기 때문에 간격이 발생 합니다. 키 집합 기반 동작입니다. 커서에서 행 101를 검색 하려고 하면 행에 대 한 키가 없기 때문에 커서가 누락 된 행을 검색 하지 못합니다. 대신 이전에 102 행 이었던 항목을 검색 합니다. 동적 커서 동작입니다.  
  
 혼합 커서는 키 집합 크기가 결과 집합 크기와 같을 때 키 집합 커서와 동일 합니다. 혼합 커서는 키 집합 크기가 1 인 경우 동적 커서와 동일 합니다.
