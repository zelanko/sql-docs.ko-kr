---
title: 읽기 전용 상태(엑셀 드라이버) | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb585d4712b6cac5e09b65ee8e13604763cd0164
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304024"
---
# <a name="read-only-status-excel-driver"></a>읽기 전용 상태(Excel 드라이버)
Microsoft Excel 드라이버를 사용하면 기본적으로 데이터 원본 테이블이 읽기 전용으로 열리며 한 번에 한 명의 사용자만 열 수 있습니다. 테이블에 읽기 전용 상태가 있더라도 응용 프로그램은 Microsoft Excel 테이블에 대한 삽입 및 업데이트를 수행할 수 있습니다.  
  
 응용 프로그램이 Microsoft Excel 드라이버를 통해 Microsoft Excel 데이터에 대해 As 로 저장 명령을 수행하는 경우 응용 프로그램은 새 테이블을 만들고 새 테이블에 저장할 데이터를 삽입해야 합니다. 삽입은 테이블에 추가됩니다. 테이블에서 닫고 다시 열 때까지 다른 작업을 수행할 수 없습니다. 테이블이 닫히면 테이블이 읽기 전용 테이블이기 때문에 후속 삽입을 수행할 수 없습니다.  
  
 Microsoft Excel 드라이버를 사용할 때 값을 업데이트할 수 있지만 Microsoft Excel 스프레드시트를 기반으로 하는 테이블에서 행을 삭제할 수 없으므로 업데이트는 Microsoft Excel 드라이버에서 공식적으로 지원하는 것으로 간주되지 않습니다.
