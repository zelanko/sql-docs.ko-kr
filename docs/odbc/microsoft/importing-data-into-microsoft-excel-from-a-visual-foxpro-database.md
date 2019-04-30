---
title: Visual FoxPro 데이터베이스에서 Microsoft Excel로 데이터 가져오기 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- importing data [ODBC]
- FoxPro ODBC driver [ODBC], Excel
- Visual FoxPro data [ODBC], Excel
- Visual FoxPro data [ODBC], importing
- Visual FoxPro ODBC driver [ODBC], Excel
ms.assetid: 3085bc4c-00a7-40e5-bffb-c3962cd3d509
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de81b606d31514cf6e7a518deeb68794d1011132
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63127281"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Visual FoxPro 데이터베이스에서 Microsoft Excel로 데이터 가져오기
데이터 원본에 대 한 정의 하는 경우 Microsoft Excel 워크시트로 Visual FoxPro 데이터를 가져올 수 있습니다. Visual FoxPro 데이터 원본 만들기에 대 한 자세한 내용은 [Microsoft Excel에서 Visual FoxPro 데이터 원본 액세스](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)합니다.  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>Visual FoxPro 데이터 Microsoft Excel 워크시트를 가져오려면  
  
1.  Microsoft Excel 스프레드시트를 엽니다.  
  
2.  데이터 메뉴에서 외부 데이터 가져오기를 선택 합니다. Microsoft 쿼리가 열립니다.  
  
3.  데이터 원본 선택 대화 상자에서 Visual FoxPro 데이터 원본 선택 하 고 사용을 클릭 합니다.  
  
4.  데이터 원본에서 액세스 한 데이터베이스 테이블에 포함 된 경우 테이블 추가 대화 상자에서 테이블을 선택 합니다. 쿼리 디자이너의 위쪽 절반에서 추가 된 테이블을 표시 하는 Microsoft 쿼리 합니다.  
  
    > [!NOTE]  
    >  소유자 목록 아니므로이 대화 상자에서 사용할 수 있는 드라이버 소유자를 지원 하지 않습니다. 데이터베이스 목록을 사용할 수 없는 경우 드라이버는 데이터 원본에서 여러 데이터베이스를 지원 하지 않으므로  
  
5.  드래그 하 여 테이블의 아래쪽 절반 디자이너의 쿼리에 대 한 필드를 선택 합니다.  
  
6.  Microsoft 쿼리를 닫습니다. 선택한 데이터를 Microsoft Excel 스프레드시트로 가져온 합니다.
