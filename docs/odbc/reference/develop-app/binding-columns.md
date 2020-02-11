---
title: 열 바인딩 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], binding columns
- binding columns [ODBC]
ms.assetid: c4407694-c8e1-4b0b-a39d-b007e6c3b54d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a634a553672b83931091056dd489f7559c4269b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68106210"
---
# <a name="binding-columns"></a>열 바인딩
데이터 원본에서 가져온 데이터는 응용 프로그램이이 목적을 위해 할당 한 변수의 응용 프로그램으로 반환 됩니다. 이 작업을 수행 하려면 응용 프로그램에서 이러한 변수를 결과 집합의 열에 연결 하거나 *바인딩해야*합니다. 개념적으로이 프로세스는 문 매개 변수에 응용 프로그램 변수를 바인딩하는 것과 같습니다. 응용 프로그램은 결과 집합 열에 변수를 바인딩할 때 해당 변수 주소, 데이터 형식 등을 드라이버에 설명 합니다. 드라이버는 해당 문에 대해 유지 관리 하는 구조에이 정보를 저장 하 고 정보를 사용 하 여 행이 인출 될 때 열에서 값을 반환 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [바인딩 결과 집합 열](../../../odbc/reference/develop-app/binding-result-set-columns.md)  
  
-   [SQLBindCol 사용](../../../odbc/reference/develop-app/using-sqlbindcol.md)
