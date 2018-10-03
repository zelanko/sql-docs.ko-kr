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
manager: craigg
ms.openlocfilehash: 17425e76814a8397b9d2e6167248f35e52ac6cfa
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47697441"
---
# <a name="read-only-status-excel-driver"></a>읽기 전용 상태(Excel 드라이버)
Microsoft Excel 드라이버를 사용 하면 데이터 원본 테이블 기본적으로 읽기 전용으로 열려 및 한 번에 한 명의 사용자만 열 수 있습니다. 하지만 테이블 읽기 전용 상태에 있는 경우에 응용 프로그램에 수행할 수 삽입 및 업데이트 Microsoft Excel 테이블.  
  
 Microsoft Excel 드라이버를 통해 Microsoft Excel 데이터에 대해 다른 이름으로 저장 명령을 수행 하는 응용 프로그램, 응용 프로그램이 새 테이블을 만들고 새 테이블에 저장할 데이터를 삽입 해야 합니다. 삽입 될 테이블에 추가 합니다. 닫고 다시 열 때까지 테이블에 없는 다른 작업을 수행할 수 있습니다. 테이블 닫히면 테이블이 읽기 전용 테이블을 다음 이므로 없습니다 후속 insert는 수행할 수 있습니다.  
  
 Microsoft Excel 드라이버를 사용 하는 경우 값을 업데이트 하는 것이 가능 하지만 공식적으로 Microsoft Excel 드라이버에서 지 원하는 업데이트 된 것으로 간주 되지 Microsoft Excel 스프레드시트를 기반으로 테이블에서 행을 삭제할 수 없습니다.
