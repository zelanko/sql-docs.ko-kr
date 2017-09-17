---
title: "테이블 문 제한 만들기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- CREATE TABLE statement limitations [ODBC]
- ODBC SQL grammar, CREATE TABLE statement limitations
ms.assetid: c5067855-20c9-456f-8d63-f375b4297f2e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0f7cec23f3ec8103b2805e0ee3c0f04d20011cb6
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="create-table-statement-limitations"></a>만들 테이블 문 제한 사항
Microsoft Access, Microsoft Excel 또는 Paradoxdriver 사용 될 때 지정 되지 않은 (또는 0으로 지정) 텍스트 또는 이진 열의 길이, 열 길이 255로 설정 됩니다.  
  
 DBASE 드라이버를 사용 하면 지정 되지 않은 (또는 0으로 지정) 텍스트 또는 이진 열의 길이, 열 길이 254로 설정 됩니다.  
  
 열이 255의 최대 지원 됩니다.  
  
 Microsoft Excel 드라이버, 5.0, 7.0, 또는 97 데이터 원본, 워크시트에 사용 되는 경우 이전에 삭제 된 워크시트로 동일한 이름으로 만들 수 없습니다. Microsoft Excel 드라이버를 사용 하 여 버전 5.0, 7.0, 또는 97 워크시트를 액세스, DROP TABLE 문 워크시트 지워지지만 워크시트 이름이 삭제 되지 않습니다.  
  
 Paradox 드라이버를 사용 하는 열 인덱스는 테이블에 정의 되어 되 면 추가할 수 없습니다. CREATE TABLE 문의 인수 목록의 첫 번째 열 인덱스를 만드는 경우 인수 목록에 두 번째 열을 포함할 수 없습니다.
