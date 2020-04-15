---
title: 비주얼 FoxPro 데이터베이스에서 마이크로 소프트 엑셀로 데이터 가져오기 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1bfd86233e5a0a406febcb30bf7a4fae595e53d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287673"
---
# <a name="importing-data-into-microsoft-excel-from-a-visual-foxpro-database"></a>Visual FoxPro 데이터베이스에서 Microsoft Excel로 데이터 가져오기
데이터 원본을 정의한 경우 Visual FoxPro 데이터를 Microsoft Excel 워크시트로 가져올 수 있습니다. 시각적 FoxPro 데이터 원본을 만드는 것에 대한 자세한 내용은 [Microsoft Excel의 시각적 FoxPro 데이터 원본 액세스를](../../odbc/microsoft/accessing-a-visual-foxpro-data-source-from-microsoft-excel.md)참조하십시오.  
  
### <a name="to-import-visual-foxpro-data-into-an-microsoft-excel-worksheet"></a>비주얼 FoxPro 데이터를 Microsoft Excel 워크시트로 가져오려면  
  
1.  Microsoft Excel 스프레드시트를 엽니다.  
  
2.  데이터 메뉴에서 외부 데이터 받기를 선택합니다. Microsoft 쿼리가 열립니다.  
  
3.  데이터 원본 선택 대화 상자에서 Visual FoxPro 데이터 원본을 선택한 다음 사용을 클릭합니다.  
  
4.  데이터 원본에서 액세스하는 데이터베이스에 테이블이 포함된 경우 테이블 추가 대화 상자에서 테이블을 선택합니다. Microsoft 쿼리는 쿼리 디자이너의 위쪽 절반에 추가된 테이블을 표시합니다.  
  
    > [!NOTE]  
    >  드라이버가 소유자를 지원하지 않으므로 이 대화 상자에서 소유자 목록을 사용할 수 없습니다. 드라이버가 데이터 원본의 여러 데이터베이스를 지원하지 않으므로 데이터베이스 목록을 사용할 수 없습니다.  
  
5.  테이블에서 디자이너의 아래쪽 절반으로 끌어 쿼리필드를 선택합니다.  
  
6.  Microsoft 쿼리를 닫습니다. 선택한 데이터가 Microsoft Excel 스프레드시트로 가져옵니다.
