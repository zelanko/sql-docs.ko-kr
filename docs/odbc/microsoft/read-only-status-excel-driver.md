---
title: 읽기 전용 상태 (Excel 드라이버) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- read-only status for Excel driver [ODBC]
- Excel driver [ODBC], read-only status
ms.assetid: ef5d773b-4f8f-4005-b985-84b53d8e9f9b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 39f9d2e7ba40ba067659a86f45d2006c83594f3e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67988048"
---
# <a name="read-only-status-excel-driver"></a>읽기 전용 상태(Excel 드라이버)
Microsoft Excel 드라이버를 사용 하는 경우 데이터 원본 테이블은 기본적으로 읽기 전용으로 열리며 한 번에 한 사용자만 열 수 있습니다. 그러나 테이블은 읽기 전용 상태 이지만 응용 프로그램은 Microsoft Excel 테이블에 대 한 삽입 및 업데이트를 수행할 수 있습니다.  
  
 응용 프로그램이 microsoft Excel 드라이버를 통해 Microsoft Excel 데이터에 대해 다른 이름으로 저장 명령을 수행할 때 응용 프로그램은 새 테이블을 만들고 새 테이블에 저장할 데이터를 삽입 해야 합니다. 삽입 결과를 테이블에 추가 합니다. 다른 작업은 닫았다가 다시 열 때까지 테이블에서 수행할 수 없습니다. 테이블이 닫히면 테이블이 읽기 전용 테이블이 되기 때문에 후속 삽입을 수행할 수 없습니다.  
  
 Microsoft excel 드라이버를 사용 하는 경우 값을 업데이트할 수 있지만 microsoft excel 스프레드시트를 기반으로 하는 테이블에서 행을 삭제할 수 없으므로 업데이트가 Microsoft Excel 드라이버에서 공식적으로 지원 되지 않는 것으로 간주 되지 않습니다.
