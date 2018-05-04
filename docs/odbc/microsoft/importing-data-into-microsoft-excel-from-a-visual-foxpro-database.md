---
title: Visual FoxPro 데이터베이스, Microsoft Excel로 데이터를 가져오는 | Microsoft Docs
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
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa6da8abaca5b3b14c48bc4324a50301d5a36d87
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Visual FoxPro 데이터베이스에서 Microsoft Excel로 데이터 가져오기
에 대 한 데이터 원본을 정의 하면 Microsoft Excel 워크시트로 Visual FoxPro 데이터를 가져올 수 있습니다. Visual FoxPro 데이터 원본을 만드는 방법은 참조 [Microsoft Excel에서 Visual FoxPro 데이터 원본에 액세스 하](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)합니다.  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro 데이터 Microsoft Excel 워크시트를 가져오려면  
  
1.  Microsoft Excel 스프레드시트를 엽니다.  
  
2.  데이터 메뉴에서 외부 데이터 가져오기를 선택 합니다. Microsoft 쿼리가 열립니다.  
  
3.  데이터 원본 선택 대화 상자에서 Visual FoxPro 데이터 원본을 선택한 다음 사용을 클릭 합니다.  
  
4.  데이터 원본에서 액세스 한 데이터베이스 테이블을 포함 하는 경우 테이블 추가 대화 상자에서 테이블을 선택 합니다. Microsoft Query 쿼리 디자이너의 위쪽 절반에 추가 된 테이블을 표시합니다.  
  
    > [!NOTE]  
    >  소유자 목록을 사용할 수 없는 경우이 대화 상자에 드라이버에서 소유자를 지원 하지 않으므로 데이터베이스 목록을 사용할 수 없는 경우 드라이버는 데이터 원본의 여러 데이터베이스를 지원 하지 않으므로  
  
5.  에서 끌어서 테이블 아래에는 디자이너의 절반 쿼리에 대 한 필드를 선택 합니다.  
  
6.  Microsoft 쿼리를 닫습니다. Microsoft Excel 스프레드시트에 선택한 데이터를 가져옵니다.
